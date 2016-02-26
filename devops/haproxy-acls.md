# Rerouting Traffic with HaProxy ACLs

Find myself having to look up these rules all the time...
path_sub, path_beg, path_end are the ones I'll likely want to use again.
Docs: https://cbonte.github.io/haproxy-dconv/configuration-1.5.html#7.1

```
acl sync_req path_sub config_settings
redirect prefix https://artisantools.com if sync_req
```