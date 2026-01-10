---
layout: default
title: AI
---

# AI

The following applications primarily focus on Artificial Intelligence.

## Utilities

[prompt2json](https://github.com/UnitVectorY-Labs/prompt2json): Unix-style CLI that sends a system instruction, required JSON Schema, and text or file inputs to Vertex AI (Gemini models) and returns schema-validated JSON for easy batch processing.

[json2mdplan](https://github.com/UnitVectorY-Labs/json2mdplan): Unix-style CLI that extracts structure-only JSON, uses Vertex AI (Gemini) structured outputs to generate a schema-validated Markdown plan, then renders Markdown locally from the original JSON without sending raw values to the model.

## Containers

[adk-docker-base](https://github.com/UnitVectorY-Labs/adk-docker-base): Docker image based on python docker image with Google Agent Development Kit (ADK) pre-installed for streamlined AI agent development.

[gcspdf2mdapi](https://github.com/UnitVectorY-Labs/gcspdf2mdapi): An API that converts PDFs stored in Google Cloud Storage to Markdown format using OCR or direct text extraction.

[adk-family-agent](https://github.com/UnitVectorY-Labs/adk-family-agent): An ADK power agent to serve as an assistant for family related tasks and cordination.

## Model Context Protocol (MCP) Servers

[mcp-graphql-forge](https://github.com/UnitVectorY-Labs/mcp-graphql-forge): A lightweight, configuration-driven MCP server that exposes curated GraphQL queries as modular tools, enabling intentional API interactions from your agents.

[mcp-acronym-lookup](https://github.com/UnitVectorY-Labs/mcp-acronym-lookup): A lightweight, configuration-driven MCP server that ingests a CSV of acronyms and initialisms to expose a lookup tool for their full meanings and descriptions.

[mcp-tf-provider-docs](https://github.com/UnitVectorY-Labs/mcp-tf-provider-docs): A configurable MCP server that indexes and serves Terraform/Tofu provider documentation from a local Git repo to power accurate, context-aware code generation.

[mcp-markdown-rag](https://github.com/UnitVectorY-Labs/mcp-markdown-rag): A local-first command-line tool for indexing and semantically searching Markdown documents using vector embeddings and a self-contained vector database.

[mcp-shopping-list-firestore](https://github.com/UnitVectorY-Labs/mcp-shopping-list-firestore): A lightweight, Firebase-backed MCP server for management of a grocery list via simple CRUD operations.

[mcp-vertex-search-snippets](https://github.com/UnitVectorY-Labs/mcp-vertex-search-snippets): A lightweight MCP server that integrates with Vertex AI Search to retrieve configurable snippets and extractive segments for document discovery.
