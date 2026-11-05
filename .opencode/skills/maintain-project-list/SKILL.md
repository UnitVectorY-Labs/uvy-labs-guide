---
name: maintain-project-list
description: Audit and maintain the UnitVectorY-Labs project lists in docs/_projects, find missing public repositories, and copy GitHub descriptions exactly.
---

# Maintain the project list

Use this skill to compare public UnitVectorY-Labs repositories with this guide's project pages, suggest additions, or apply requested updates. Work from the repository root. Read `AGENTS.md` and inspect the current pages before editing.

## Fetch and compare

1. Check `git status --short`. Preserve existing user changes.
2. Fetch every public repository, including archived repositories. Use pagination, not a fixed repository limit. GitHub CLI authentication must work; stop and report any API failure rather than treating it as an empty result.

   ```sh
   gh api --paginate --slurp 'orgs/UnitVectorY-Labs/repos?type=public&per_page=100' > /tmp/opencode/project-list-repos.json
   ```

3. Compare repository names with GitHub links in every `docs/_projects/*.md` file. Match names case-insensitively, but preserve GitHub's spelling in entries. Compare parsed sets rather than shell-sorted lists to avoid locale-dependent results.

   ```sh
   python3 - <<'PY'
   import json
   import re
   from pathlib import Path

   pages = json.loads(Path('/tmp/opencode/project-list-repos.json').read_text())
   repos = {r['name'].casefold(): r for page in pages for r in page if not r['private']}
   documented = {}
   for path in sorted(Path('docs/_projects').glob('*.md')):
       for name in re.findall(r'https://github\.com/UnitVectorY-Labs/([\w.-]+)', path.read_text(), re.I):
           documented.setdefault(name.casefold(), set()).add(path.name)
   for key in sorted(repos.keys() - documented.keys()):
       repo = repos[key]
       print(json.dumps({'missing': repo['name'], 'archived': repo['archived'],
                         'description': repo['description']}, ensure_ascii=False))
   for key in sorted(repos.keys() & documented.keys()):
       repo = repos[key]
       in_archived = 'archived.md' in documented[key]
       if repo['archived'] and not in_archived:
           print(json.dumps({'move-to-archived': repo['name'], 'pages': sorted(documented[key]),
                             'description': repo['description']}, ensure_ascii=False))
       elif in_archived and not repo['archived']:
           print(json.dumps({'move-from-archived': repo['name'], 'pages': sorted(documented[key]),
                             'description': repo['description']}, ensure_ascii=False))
   for key in sorted(documented.keys() - repos.keys()):
       print('VERIFY documented-only:', key, ', '.join(sorted(documented[key])))
   PY
   ```

4. Report missing active repositories separately from missing archived repositories. A documented-only link may indicate a rename, transfer, visibility change, or deletion. Verify it before suggesting changes; never remove it automatically. Do not list private repositories or assume forks and deployment repositories should be excluded.
5. Existence alone is not enough: every documented repository whose `archived` flag disagrees with its page placement is drift and must be reported. An archived repo on a live page is a `move-to-archived` — relocate the entry to `archived.md`, do not delete it. A live repo in `archived.md` is a `move-from-archived` — verify and relocate it to the fitting live page. When moving an entry, always re-fetch its description: GitHub descriptions are frequently rewritten at archive time (for example, a "Superseded by X." note), so the old entry text is likely stale.

## Choose placement

- Read the relevant pages and headings. Prefer the most specific existing category and avoid duplicate entries across pages.
- Put GitHub command-line tools under `docs/_projects/github.md` → `Command Line Utilities`.
- Put Omarchy plugins under `docs/_projects/ai.md` → `Omarchy` unless the user requests another location.
- Put archived repositories in `archived.md`. Check README status badges or repository custom properties before using `workinprogress.md`; do not infer maturity from age or release count.
- Propose a new heading or page when no existing category fits. Ask when placement is ambiguous and respect the user's explicit choice.
- For suggestion-only requests, return repository links and proposed page/heading placements without editing. Apply changes only when requested.

## Copy descriptions exactly

GitHub's repository `description` field is the source of truth. Immediately before editing, fetch each selected repository again:

```sh
gh api repos/UnitVectorY-Labs/REPO --jq '{name, description, archived, private}'
```

Use the existing entry format:

```markdown
[REPO](https://github.com/UnitVectorY-Labs/REPO): EXACT_GITHUB_DESCRIPTION
```

Copy the description verbatim. Do not summarize, correct spelling, change capitalization or Unicode punctuation, trim content, or add a trailing period. A description without a period must stay that way. If a description is null or empty, ask how to handle it rather than inventing text. If Markdown syntax prevents a verbatim description from displaying correctly, flag the conflict instead of silently rewriting it.

Keep surrounding formatting and front matter unchanged. New pages need the same Jekyll front matter pattern as existing project pages. Use Jekyll `link` tags for any internal documentation links.

## Verify and finish

1. Re-read every changed entry. Compare its description string directly with the fetched API value, including punctuation and whitespace. Do not rely on visual similarity.
2. Repeat the name comparison to confirm requested additions are covered and check that no duplicate entries were introduced.
3. Run `git diff --check` and review the diff, including newly created files. Keep edits limited to the requested entries and headings.
4. Do not invent build, test, or lint commands. This repository has no local build; GitHub Pages builds on push.
5. Summarize additions with page paths and headings, note unresolved items, and state whether exact descriptions were verified. Do not commit or push unless asked.
