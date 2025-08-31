---
layout: default
title: Web Utilities
---

# Web Utilities

The following are simple utilities that are helpful with web development.

## Documentation

[jwks-catalog](https://github.com/UnitVectorY-Labs/jwks-catalog): A catalog of JWKS endpoints for popular websites.

[jwks-observer](https://github.com/UnitVectorY-Labs/jwks-observer): Observes and records changes to public OIDC metadata and JWKS for services listed in the jwks-catalog.

[jwks-catalog-crawler](https://github.com/UnitVectorY-Labs/jwks-catalog-crawler): Extracts URLs from jwks-catalog and publishes crawl requests to http-response-collector for HTTP response and header collection.

[jwks-catalog-crawler-tofu](https://github.com/UnitVectorY-Labs/jwks-catalog-crawler-tofu): OpenTofu module for deploying jwks-catalog-crawler to GCP

[dns-caa-catalog](https://github.com/UnitVectorY-Labs/dns-caa-catalog): Tracks CAA DNS configurations across top websites to surface insights on certificate issuance policies.

## Tools

[certsummary](https://github.com/UnitVectorY-Labs/certsummary): A tool for securely decoding and inspecting SSL/TLS certificates directly in your web browser.

[oidcfinder](https://github.com/UnitVectorY-Labs/oidcfinder): Automates the discovery of OpenID Connect configuration URLs across list of domains.

## Applications

[gologhttpbinary](https://github.com/UnitVectorY-Labs/gologhttpbinary): A lightweight HTTP server that logs HTTP requests, including the body encoded in base64, enabling logging of binary payloads.

[gologhttpjson](https://github.com/UnitVectorY-Labs/gologhttpjson): A lightweight HTTP server for logging requests, with body capture, opt-in headers, and environment variable metadata.

[goenvecho](https://github.com/UnitVectorY-Labs/goenvecho): Simple app that responds to GET requests with a JSON payload listing all environment variables.

[hellorest](https://github.com/UnitVectorY-Labs/hellorest): A minimal Go API returning {"hello": "world"} on a GET / request deployed using a container
