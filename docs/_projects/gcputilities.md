---
layout: default
title: GCP Utilities
---

# GCP Utilities

The following are applications and ulities that are used in conjunction with Google Cloud Platform (GCP).

## Applications

### Documentation

[gcp-iam-catalog](https://github.com/UnitVectorY-Labs/gcp-iam-catalog): A comprehensive catalog of GCP IAM roles and permissions, designed to easily identify which roles include a specific permission.

### Containers

[firestore-batch-incrementer](https://github.com/UnitVectorY-Labs/firestore-batch-incrementer): Iterates through a Firestore collection in batches and atomically increments a specified root‑level numeric field with configurable rate limiting.

### Web Applications

[gcpmetadataexplorer](https://github.com/UnitVectorY-Labs/gcpmetadataexplorer): A web-based interface for browsing and inspecting the GCP metadata server.

[iapheaders](https://github.com/UnitVectorY-Labs/iapheaders): Displays GCP Identity-Aware Proxy headers and JWT for inspection.

[gcpidentitytokenportal](https://github.com/UnitVectorY-Labs/gcpidentitytokenportal): Web portal for vending GCP identity tokens via metadata service with flexible audience selection.

### Go Libraries

[gcpvalidate](https://github.com/UnitVectorY-Labs/gcpvalidate): Client-side validation of Google Cloud resource identifiers and attributes for Go applications, based on documented conventions (not affiliated with Google).

### Java Utilities

[firestoreproto2map](https://github.com/UnitVectorY-Labs/firestoreproto2map): Java helper library to convert Firestore Protocol Buffer from event to map that can be used by Firestore

[firestoreproto2json](https://github.com/UnitVectorY-Labs/firestoreproto2json): Java helper library to convert Firestore Protocol Buffer to JSON Object

[simplegoogleidtoken](https://github.com/UnitVectorY-Labs/simplegoogleidtoken): simplegoogleidtoken is a lightweight Java library for effortlessly exchanging Google Cloud Service Account credentials for Google ID tokens

[kubetogoogleidtoken](https://github.com/UnitVectorY-Labs/kubetogoogleidtoken): A Java library for obtaining Google ID tokens by leveraging Kubernetes Service Accounts with GCP Workload Identity Federation.

### Command Line Utilities

[pubsubmsgrestforwarder](https://github.com/UnitVectorY-Labs/pubsubmsgrestforwarder): A Go command-line application for local testing, simulating the Cloud Run Push use case by consuming Pub/Sub messages and forwarding them as RESTful HTTP POST requests.

### Firestore - crossfiresync

[crossfiresync](https://github.com/UnitVectorY-Labs/crossfiresync): A Java library enabling real-time synchronization between GCP Firestore instances across regions using Pub/Sub.

[crossfiresyncrun](https://github.com/UnitVectorY-Labs/crossfiresyncrun): Provides real-time synchronization between GCP Firestore instances across regions using Pub/Sub, packaged as a Docker image for deployment on Cloud Run.

[crossfiresyncrun-tofu](https://github.com/UnitVectorY-Labs/crossfiresyncrun-tofu): A module for OpenTofu that deploys crossfiresyncrun to GCP Cloud Run, along with configuring essential services including Firestore and Pub/Sub.

[crossfiresync-firestore](https://github.com/UnitVectorY-Labs/crossfiresync-firestore): Reference implementation of a crossfiresync Firestore publisher, featuring Java code and deployment scripts for Cloud Functions.

[crossfiresync-pubsub](https://github.com/UnitVectorY-Labs/crossfiresync-pubsub): Reference implementation of a crossfiresync Pub/Sub consumer, featuring Java code and deployment scripts for Cloud Functions.

### Pub/Sub

[http-response-collector](https://github.com/UnitVectorY-Labs/http-response-collector) - Retrieves HTTP responses and headers from specified endpoints and publishes the collected data to Google Cloud Pub/Sub for further processing.

### KMS - lockboxkms

[lockboxkms](https://github.com/UnitVectorY-Labs/lockboxkms): A simple web interface for encrypting text using Google Cloud KMS.

[lockboxkms-secretmanager-tofu](https://github.com/UnitVectorY-Labs/lockboxkms-secretmanager-tofu): OpenTofu module for decrypting value using KMS and creating a secret with that value in GCP

### Terraform/OpenTofu Modules

[gcp-cloud-run-psc-lb-tofu](https://github.com/UnitVectorY-Labs/gcp-cloud-run-psc-lb-tofu): Demonstrates how to expose a private Cloud Run service using Private Service Connect and an internal HTTPS load balancer.

[gcp-cloud-run-lb-nipio-tofu](https://github.com/UnitVectorY-Labs/gcp-cloud-run-lb-nipio-tofu): Deploys a global load-balanced Cloud Run service using nip.io for automatic SSL certificates.

[gcp-cloud-run-iap-authui-tofu](https://github.com/UnitVectorY-Labs/gcp-cloud-run-iap-authui-tofu): Deploys GCP's IaP authui-container to Cloud Run as an internet facing endpoint.

[firestore-to-bigquery-tofu](https://github.com/UnitVectorY-Labs/firestore-to-bigquery-tofu): This module automates the scheduled export of Firestore data by triggering Cloud Run jobs that export to Cloud Storage and load the data into BigQuery.

### Data Replication

[firepubauditsource](https://github.com/UnitVectorY-Labs/firepubauditsource): Publishes Firestore data changes to Pub/Sub as JSON audit records for downstream processing.

[firepubauditsource-tofu](https://github.com/UnitVectorY-Labs/firepubauditsource-tofu): A module for OpenTofu that deploys firepubauditsource to GCP Cloud Run, along with configuring essential services including Eventarc for Firestore and Pub/Sub.

[bqpubauditsink](https://github.com/UnitVectorY-Labs/bqpubauditsink): Ingests Pub/Sub audit JSON events and inserts the records into BigQuery.

[bqpubauditsink-tofu](https://github.com/UnitVectorY-Labs/bqpubauditsink-tofu): A module for OpenTofu that deploys bqpubauditsink to GCP Cloud Run, along with configuring essential services including the Pub/Sub subscription and BigQuery dataset and table.

[valkeypubauditsink](https://github.com/UnitVectorY-Labs/valkeypubauditsink): Ingests Pub/Sub audit JSON events and synchronizes the records into Valkey (Redis).
