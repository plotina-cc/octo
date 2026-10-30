# Plotina fork

Why this fork exists: Octo runs behind Authentik, which authenticates the user
and passes their identity in the `Remote-User` header. Upstream Octo does not
forward that header to Navidrome, so single sign-on users were not recognised.

The change lives on `plotina/remote-user`: Octo forwards the configured
identity header to Navidrome. Nothing else is modified, and `main` mirrors
upstream.

The image `plotina/octo:2026.10.29-remote.2` is built from that branch.

Licence: GPL-3.0, same as upstream. Full sources are in this repository.
