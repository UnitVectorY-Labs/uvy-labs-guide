---
layout: default
title: Badges
---

# Badges

On GitHub, badges are a way to provide quick information about the status of a project.  They are typically displayed in the README.md file of a project.  

The following are badges that are used in UnitVectorY Labs projects:

## License

The [licenses]({{ site.baseurl }}{% link _bestpractices/licenses.md %}) of the specific project are included as a badge in the README.md file.

The following is the badge that is included in the README.md file of a project that uses the Apache License 2.0:

```markdown
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
```

The following is the badge that is included in the README.md file of a project that uses the MIT License:

```markdown
[![License](https://img.shields.io/badge/license-MIT-blue)](https://opensource.org/licenses/MIT)
```

The following is the badge that is included in the README.md file of a project that uses the Eclipse Public License 2.0:

```markdown
[![License](https://img.shields.io/badge/License-EPL%202.0-blue.svg)](https://www.eclipse.org/legal/epl-v20.html)
```
## GitHub Release Version

For projects that have GitHub Releases the most recent version number is included as a badge linking to the latest release.  The following URL requires the repository name to replace the `CHANGEME` segment in the URLs.

```markdown
[![GitHub release](https://img.shields.io/github/release/UnitVectorY-Labs/CHANGEME.svg)](https://github.com/UnitVectorY-Labs/CHANGEME/releases/latest)
```

## Project Status

The [project status]({{ site.baseurl }}{% link _bestpractices/status.md %}) of the specific project are included as a badge in the README.md file.

Separate badges are used for the project depending on its status:

```markdown
[![Concept](https://img.shields.io/badge/Status-Concept-white)](https://guide.unitvectorylabs.com/bestpractices/status/#concept)
```

```markdown
[![Work In Progress](https://img.shields.io/badge/Status-Work%20In%20Progress-yellow)](https://guide.unitvectorylabs.com/bestpractices/status/#work-in-progress)
```

```markdown
[![Active](https://img.shields.io/badge/Status-Active-green)](https://guide.unitvectorylabs.com/bestpractices/status/#active)
```

```markdown
[![Suspended](https://img.shields.io/badge/Status-Suspended-orange)](https://guide.unitvectorylabs.com/bestpractices/status/#suspended)
```

```markdown
[![Abandoned](https://img.shields.io/badge/Status-Abandoned-red)](https://guide.unitvectorylabs.com/bestpractices/status/#abandoned)
```

## Code Coverage

The [code coverage]({{ site.baseurl }}{% link _javadevelopment/codecoverage.md %}) badge from Codecov is included in the README.md file to display the code coverage.

## Maven Central

A badge is included in the README.md file to show the status of the latest release on Maven Central.  This badge is generated by [Shields.io](https://shields.io/) and is included in the README.md file as follows:

```markdown
[![Maven Central](https://img.shields.io/maven-central/v/com.unitvectory/fileparamunit)](https://central.sonatype.com/artifact/com.unitvectory/fileparamunit)
```

## Java Documentation

For those projects that are on Maven Central, a badge is included in the README.md file to link to the Java documentation.  This badge is generated by [Javadoc.io](https://javadoc.io/) and is included in the README.md file as follows:

```markdown
[![javadoc](https://javadoc.io/badge2/com.unitvectory/fileparamunit/javadoc.svg)](https://javadoc.io/doc/com.unitvectory/fileparamunit)
```
## Go Report Card

For Go projects, a badge is included in the README.md file to link to the [https://goreportcard.com/](https://goreportcard.com/) to show the report code representing the code quality.

```markdown
[![Go Report Card](https://goreportcard.com/badge/github.com/UnitVectorY-Labs/clip4llm)](https://goreportcard.com/report/github.com/UnitVectorY-Labs/clip4llm)
```
