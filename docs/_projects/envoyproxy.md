---
layout: default
title: Envoy Proxy
---

# Envoy Proxy

The following are applications that are used in conjunction with [EnvoyProxy](https://www.envoyproxy.io/).

## Applications

### ExtAuthz

[authzgcpk8stokeninjector](https://github.com/UnitVectorY-Labs/authzgcpk8stokeninjector):A gRPC-based ExtAuthz service for Envoy Proxy for injecting GCP identity tokens into requests in Kubernetes environments.

[authzjwtbearerinjector](https://github.com/UnitVectorY-Labs/authzjwtbearerinjector): A gRPC-based ExtAuthz service for Envoy Proxy that implements the jwt-bearer flow, injecting authentication credentials to backend services.

### GCP

[gcp-envoy-to-cloud-run-metadata-auth-tofu](https://github.com/UnitVectorY-Labs/gcp-envoy-to-cloud-run-metadata-auth-tofu): Demonstrates how to configure EnvoyProxy on Cloud Run to authenticate to a backend service, also running on Cloud Run, using GCP’s metadata service for secure service-to-service authentication.

[gcp-envoy-to-cloud-run-jwt-bearer-auth-tofu](https://github.com/UnitVectorY-Labs/gcp-envoy-to-cloud-run-jwt-bearer-auth-tofu): Demonstrates how to configure EnvoyProxy running on Cloud Run to authenticate to a backend service, using jwt-bearer flow through ExtAuthz with authzjwtbearerinjector.

