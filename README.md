# `ldap-fetchmail` Docker Image

## Details

Fetch every `$FETCHMAIL_INTERVAL_SECONDS` (defaults to 300) fetchmail configuration from LDAP, configures and runs `fetchmail`.

The LDAP schema for `fetchmail` from https://github.com/LECKERBEEFde/fetchmail-ldap is used.

You need to provide configuration by mounting `/etc/fetchmail`, in which two files are expected:

* `/etc/fetchmail/fetchmailrc.header`: This will be the top of the generated `fetchmailrc` with your default settings.
* `/etc/fetchmail/fetchmail.ldap.conf`: This will contain the ldap configuration

## Example `fetchmail.ldap.conf`

``` sh
LDAP_URI='ldaps://ldap.example.com'

BASE_DN='dc=example,dc=com'

BIND_DN="cn=fetchmail,ou=Services,dc=example,dc=com"
BIND_PW='*****'
```

## Example Launch

``` sh
docker run --name fetchmail -e FETCHMAIL_INTERVAL_SECONDS=500 \
  -v /path/to/fetchmail/configs:/etc/fetchmail:ro \
  -v /path/to/fetchmail/data:/var/lib/fetchmail \
  hendriksp/ldap-fetchmail
```
