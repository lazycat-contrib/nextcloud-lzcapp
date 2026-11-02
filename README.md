# Nextcloud (LazyCat LPK)

Self-hosted file sync and share, with calendar, contacts and notes.

- Upstream: https://github.com/nextcloud/server
- Image: `library/nextcloud:35.0.2` (official Docker Hub image, mirror mode, digest-matched)
- License: AGPL-3.0 (full text in `content/licenses/COPYING`)
- Containers: Nextcloud + MariaDB 10.11

## Notes

- Version resolved with the Docker Hub API (`ordering=last_updated`); registry `tags/list`
  truncates at 1000 entries and would have reported an older release.
- The image supports first-run provisioning via env vars: `NEXTCLOUD_ADMIN_USER` /
  `NEXTCLOUD_ADMIN_PASSWORD` plus `MYSQL_*`. The admin password comes from a platform stable
  secret, so there is no built-in credential; the username is fixed to `admin`.
- Behind the LazyCat proxy: `NEXTCLOUD_TRUSTED_DOMAINS`, `OVERWRITEPROTOCOL=https`,
  `OVERWRITECLIURL` and `TRUSTED_PROXIES=*` are all set, otherwise Nextcloud blocks requests
  with an "untrusted domain" page.
- `PHP_UPLOAD_LIMIT=2G`, `PHP_MEMORY_LIMIT=1G` for practical large-file uploads.
- Data on `/lzcapp/var/{db,html}`.
- No mail service configured.
- Not yet verified on a real device.
