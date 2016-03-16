# cryptoBullshit

Look at all this broken crypto!

Basically, a repository for tracking outstanding security and cryptography defects in software. References to bug reports are provided where available.

Pull requests for additions and corrections are welcome!

## PostgreSQL

* __Insecure default:__ SSL/TLS is [disabled by default](http://www.postgresql.org/docs/9.3/static/runtime-config-connection.html#GUC-SSL).
* __Insecure default:__ When SSL/TLS is enabled, PostgreSQL will default to OpenSSL's ciphers rated 'HIGH' or 'MEDIUM', which potentially includes weakened or broken ciphers. Triple-DES is also explicitly added. This is completely unnecessary for a database, where there is a strong degree of control over the environment on both ends of the connection, and defaulting to optimally secure ciphers would be completely reasonable.
* __Insecure default:__ The default ECDH curve is NIST P-256, which is [broken](https://blog.cr.yp.to/20140323-ecdsa.html) ([more on this topic](http://safecurves.cr.yp.to/)).
* __Missing security:__ It is not possible to explicitly select allowed SSL/TLS versions (eg. to disable protocol versions that are known to be broken).
* __Security theater:__ Passwords are sent over the wire either in plaintext or hashed with MD5 - the latter of which offers no benefits due to [pass-the-hash attacks](https://en.wikipedia.org/wiki/Pass_the_hash), but still gives the user a false sense of security.
