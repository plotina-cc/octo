# Plotina fork

This fork carries one optional proxy-auth feature for the Plotina deployment.
It is deliberately kept as a small, isolated change so it can be rebased onto
upstream releases.

## Change

`SUBSONIC__PROXYUSERHEADER` names one extra request header that Octo's
Subsonic relay forwards to Navidrome. When the variable is unset or blank,
Octo keeps its stock allowlist and behaviour. It is used with Navidrome's
external authentication:

```yaml
environment:
  SUBSONIC__PROXYUSERHEADER: Remote-User
```

The surrounding reverse proxy must authenticate the request and set that
header. Do not expose Octo directly to untrusted clients while the header is
enabled.

## Build

```sh
docker build -t plotina/octo:2026.10.28-remote.1 .
```

`PLACES_DOWNLOAD=0` can be passed for a smaller offline build; place lookup
will then be unavailable until the image is rebuilt with place data.

## Rebase

`main` tracks `winters27/octo`. Keep the feature on
`plotina/remote-user`; merge or rebase upstream into that branch. The whole
change is in
`crates/octo/src/services/subsonic/subsonic_proxy_service.rs` and consists of
the extra header lookup plus replacing the two static header loops.
