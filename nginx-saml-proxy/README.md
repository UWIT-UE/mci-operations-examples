# Cluster-wide NGINX SAML Proxy

Integrates SAML Proxy with the standard Ingress NGINX using annotations.

## Overview
- nginx-saml-proxy deployed standalone to handle auth requests for any Ingress. nginx-saml-proxy is stateless and is configured by whatever is passed to it, thus it can handle many different server names and saml parameters.
- Create a main Ingress for each server name which defines the TLS certificate and the /saml/ path. The /saml/ path must be reachable by client browsers.
- Create a separate Ingress for each path or path pattern that has a unique SAML configuration.
- Although the same server name is defined in multiple Ingress definitions with different paths, they are merged resulting in a unified routing for the server.
- It is important to note that each separate Ingress is effectively a separate stanza in the ingress-nginx configuration. The annotations in an Ingress definition apply to that stanza, thus one must not combine Ingress definitions.
- All resources must be in the same namespace, as usual.

## Details
See descriptive comments in the following files.

File | Description 
----- | -----------
deploy-nginx-saml-proxy | Common nginx-saml-proxy deployment, external secret
ingress-server1-main    | Main Ingress for server1
ingress-server1-*       | Additional paths for server1 with different options
ingress-server2-main    | Main Ingress for server2


