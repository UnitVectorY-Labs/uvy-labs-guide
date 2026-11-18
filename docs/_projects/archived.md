---
layout: default
title: Archived
---

# Archived

The following repositories are archived projects and are kept for reference only.

## Applications

[crossfiresyncrun](https://github.com/UnitVectorY-Labs/crossfiresyncrun): Provides real-time synchronization between GCP Firestore instances across regions using Pub/Sub, packaged as a Docker image for deployment on Cloud Run.

[valkeypubauditsink](https://github.com/UnitVectorY-Labs/valkeypubauditsink): Ingests Pub/Sub audit JSON events and synchronizes the records into Valkey (Redis).

[devicekeyregistry](https://github.com/UnitVectorY-Labs/devicekeyregistry): DeviceKeyRegistry is an API for securely registering, approving, disabling, and validating device public keys using JWTs and JWKS URLs.

[serviceauditreport](https://github.com/UnitVectorY-Labs/serviceauditreport): A tool for auditing and reporting on the configuration compliance of various services

[firepubauditsource](https://github.com/UnitVectorY-Labs/firepubauditsource): Publishes Firestore data changes to Pub/Sub as JSON audit records for downstream processing.

[bqpubauditsink](https://github.com/UnitVectorY-Labs/bqpubauditsink): Ingests Pub/Sub audit JSON events and inserts the records into BigQuery.

[ghwhenthen](https://github.com/UnitVectorY-Labs/ghwhenthen): Superseded by ghook4action. Archived predecessor for configurable GitHub webhook to Pub/Sub to Projects automation.

[jwks-catalog-crawler](https://github.com/UnitVectorY-Labs/jwks-catalog-crawler): Extracts URLs from jwks-catalog and publishes crawl requests to http-response-collector for HTTP response and header collection.

[mcp-markdown-rag](https://github.com/UnitVectorY-Labs/mcp-markdown-rag): A local-first command-line tool for indexing and semantically searching Markdown documents using vector embeddings and a self-contained vector database.

[mcp-shopping-list-firestore](https://github.com/UnitVectorY-Labs/mcp-shopping-list-firestore): A lightweight, Firebase-backed MCP server for management of a grocery list via simple CRUD operations.

## Deployment

[firestore-to-bigquery-tofu](https://github.com/UnitVectorY-Labs/firestore-to-bigquery-tofu): This module automates the scheduled export of Firestore data by triggering Cloud Run jobs that export to Cloud Storage and load the data into BigQuery.

[firepubauditsource-tofu](https://github.com/UnitVectorY-Labs/firepubauditsource-tofu): A module for OpenTofu that deploys firepubauditsource to GCP Cloud Run, along with configuring essential services including Eventarc for Firestore and Pub/Sub.

[bqpubauditsink-tofu](https://github.com/UnitVectorY-Labs/bqpubauditsink-tofu): A module for OpenTofu that deploys bqpubauditsink to GCP Cloud Run, along with configuring essential services including the Pub/Sub subscription and BigQuery dataset and table.

[jwks-catalog-crawler-tofu](https://github.com/UnitVectorY-Labs/jwks-catalog-crawler-tofu): OpenTofu module for deploying jwks-catalog-crawler to GCP

## Libraries

[cron-conductor-core](https://github.com/UnitVectorY-Labs/cron-conductor-core): Core Java library for cron-conductor providing the interfaces and main logic.

## Container Images

[adk-docker-base](https://github.com/UnitVectorY-Labs/adk-docker-base): Docker image based on python docker image with Google Agent Development Kit (ADK) pre-installed for streamlined AI agent development.
