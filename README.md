:warning: This repository is no longer maintained.
==========

[check_ssl_cert](https://github.com/matteocorti/check_ssl_cert) supports validating
DANE records with openssl >= 1.1.0


check_dane
==========

Nagios/Icinga plugin for checking DANE/TLSA records.

It compares the DANE/TLSA record against the TLS certificate provided by a service.

Usage
=====

    -h, --help            show this help message and exit
    --host HOST, -H HOST  Hostname to check.
    --port PORT, -p PORT  TCP port to check.
    --connect-host CONNECT_HOST, --ip CONNECT_HOST, -I CONNECT_HOST
                          Connect to this host instead of --host.
    --connect-port CONNECT_PORT
                          Connect to this port instead of --port.
    --starttls {smtp,imap,xmpp,quassel}
                          Send the protocol-specific messages to enable TLS.
    --check-pkix          Additionally perform traditional checks on the
                          certificate (ca trust path, hostname, expiry).
    --min-days-valid MIN_DAYS_VALID
                          Minimum number of days a certificate has to be valid.
                          Format: INTEGER[,INTEGER]. 1st is #days for warning,
                          2nd is critical.
    --no-dnssec           Continue even when DNS replies aren't DNSSEC
                          authenticated.
    --nameserver NAMESERVER
                          Use a custom nameserver.
    --timeout TIMEOUT     Network timeout in sec. Default: 10
    --version             show program's version number and exit

Supported TLSA records
======================

   * Certificate Usage: "Service certificate constraint" (1) and "Domain-issued certificate" (3) is supported
   * Selector: "Full certificate" (0) and SubjectPublicKeyInfo (1)
   * Matching Type: "Exact match" (0), SHA-256 hash (1) and SHA-512 hash (2)

Requirements
============

   * Python >= 3.4
   * [dnspython](http://www.dnspython.org/) >= 2.0
   * openssl binary
   * DNSSEC capable resolver (or use --no-dnssec but be aware of the security implications)

Examples
========

   * check_dane -H mx.example.com -p 25 --starttls smtp
   * check_dane -H example.com -p 443 --check-pkix
