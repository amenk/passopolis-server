# Building the binary

We are running the server on NixOS. You can also leave out the `nix-shell` call if running on Ubuntu.

```console
$ nix-shell # only on NixOS
$ ant crypto
$ ant jar
```

# Prerequirements

* Install PostgreSQL
* Configure passwords (?)

# Running the server

```console
$ ant server
```

# Clean audit

Audit tables get very large, so the following has to run in a cron job
every so often. Better would be to have a date limit to only archive
old data but the following is betted than a full disk:

```
psql mitro -c "copy audit to '/tmp/audit.csv'; delete from audit;"
xz /tmp/audit.csv
mv /tmp/audit.csv.xz /var/log/audit-$(date -I).csv.xz
```
