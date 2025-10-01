# Tiny Proxy Ansible role

Author: Brad House<br/>
License: MIT<br/>
Original Repository: https://github.com/bradh352/ansible-role-service-tinyproxy

## Overview

Tiny Proxy is a non-caching HTTP proxy with support for HTTPS via HTTP CONNECT.
Its purpose is typically for security.  While firewalls are great for restricting
outbound access, there are some services that may not have static IPs or
predictable IPs.  So for these security-sensitive devices, it is not wise to
open a firewall port to the entire internet, instead the answer is to proxy it.

The security-sensitive device will have access to the tinyproxy service which
then reaches out to the public internet after *first* validating the requested
URL is allowed.  This validation is basically acting as a Layer 7 firewall
rule.

## Variables

- `tinyproxy_port`: The port tiny proxy will listen on.  Defaults to `8080` if
  not set.
- `tinyproxy_allow`: Required. List of allowed destinations.  These destinations
  are only the domain name, not the full url.  Wildcards may be used, and are
  honored as fnmatch rules (also known as shell wildcard syntax).  Note when
  using `*` it is not using either regex nor nameserver/dns matching rules.
  E.g. `[ "*.bradhouse.dev", "bradhouse.dev" ]`

