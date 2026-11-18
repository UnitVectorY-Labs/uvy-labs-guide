---
layout: default
title: Archived
---

# Archived

The following repositories are archived projects and are kept for reference only.

## Applications

[firepubauditsource](https://github.com/UnitVectorY-Labs/firepubauditsource): Publishes Firestore data changes to Pub/Sub as JSON audit records for downstream processing.

[bqpubauditsink](https://github.com/UnitVectorY-Labs/bqpubauditsink): Ingests Pub/Sub audit JSON events and inserts the records into BigQuery.

[ghwhenthen](https://github.com/UnitVectorY-Labs/ghwhenthen): Superseded by ghook4action. Archived predecessor for configurable GitHub webhook to Pub/Sub to Projects automation.

[jwks-catalog-crawler](https://github.com/UnitVectorY-Labs/jwks-catalog-crawler): Extracts URLs from jwks-catalog and publishes crawl requests to http-response-collector for HTTP response and header collection.

[mcp-markdown-rag](https://github.com/UnitVectorY-Labs/mcp-markdown-rag): A local-first command-line tool for indexing and semantically searching Markdown documents using vector embeddings and a self-contained vector database.

[mcp-shopping-list-firestore](https://github.com/UnitVectorY-Labs/mcp-shopping-list-firestore): A lightweight, Firebase-backed MCP server for management of a grocery list via simple CRUD operations.

## Deployment

[firepubauditsource-tofu](https://github.com/UnitVectorY-Labs/firepubauditsource-tofu): A module for OpenTofu that deploys firepubauditsource to GCP Cloud Run, along with configuring essential services including Eventarc for Firestore and Pub/Sub.

[bqpubauditsink-tofu](https://github.com/UnitVectorY-Labs/bqpubauditsink-tofu): A module for OpenTofu that deploys bqpubauditsink to GCP Cloud Run, along with configuring essential services including the Pub/Sub subscription and BigQuery dataset and table.

[jwks-catalog-crawler-tofu](https://github.com/UnitVectorY-Labs/jwks-catalog-crawler-tofu): OpenTofu module for deploying jwks-catalog-crawler to GCP
