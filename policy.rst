=======================
Clean Connection Policy
=======================


Motivation
==========

The Clean Connection Policy is intended for ensuring content integrity during the archiving process.


DNS
+++

DNS queries/responses can be captured and modified in transit and, as a result, archives can be compromised.

Value-added DNS services such as OpenDNS may return entries for invalid domain names. For example, a user makes a typo and enters ``google.cmo`` instead of ``google.com``. The DNS query may respond with a server that provides users with a ad-supported search query.

Government censorship may intercept any DNS query and respond with an invalid IP address. A thorough crawler may unintentionally contribute to a DDoS attack.

Captive portals may return DNS entries that point to a login server such as free wifi service agreements.

The user may have custom hostname entries in their HOSTS file. Sometimes this is intentional to block ad servers or point to websites with an expired domain name.


Proxies
+++++++

Proxies may mangle content rendering it useless.

A bandwidth-reducing proxy may compress images destroying its original data.

A proxy may be strictly caching resources. If the user makes a request to a web page, the server does not fetch the images but rather returns an "error" image requesting the user to reload the page.

A proxy may be blocking advertisements. Complete archives include advertisements.

A proxy may be stripping out HTTP headers from the original request. WARC files preserve original HTTP headers.


Firewall
++++++++

Firewalls may restrict access to content and compromise archives.

A content-filtering firewall may replace a restricted page with an "error" page. Archives should make no distinction between good or naughty content.

A firewall may restrict access to specific ports. Not all services run on their assigned ports.

A firewall may inject a TCP reset packet into the connection. Injeced TCP resets makes it impossible to access anything.


On-the-fly modification
+++++++++++++++++++++++

It may be possible for on-the-fly modification of content by a man-in-the-middle attack.

An ISP may inject or replace advertisements of web pages. Or they may inject a bandwidth usage warning.

Secure connections may be intercepted with a different SSL certificate. While an invalid certificate is common, the wrong certificate for a given host indicates a problem. This is typically used for free wifi login.


Procedure
=========


Check for DNS query uniqueness
++++++++++++++++++++++++++++++

The client should resolve the following domains:

* twitter.com
* facebook.com
* youtube.com
* microsoft.com
* icanhas.cheezburger.com
* archiveteam.org

The result should be 6 unique IP addresses. If there are any common IP addresses or any fails to resolve, the connection is not clean.


Check for positive DNS failed resolutions
+++++++++++++++++++++++++++++++++++++++++

The client should resolve the following domains:

* {RANDOMCHARS}.com
* www.{RANDOMCHARS}.com
* invalid.{RANDOMCHARS}.com
* www.yahoo.cmo (sic)
* invalid.archiveteam.org
* invalid.{RANDOMCHARS}.tracker.archiveteam.org

Where `{RANDOMCHARS}` is a set of random characters.

The result should be 0 IP addresses, that is, all non-existent domains.


Check for proxies
+++++++++++++++++

The client should fetch a page from a HTTP Header Echo service.

There should not be the following fields in the header:

* X-Forwarded-For
* Forwarded-For
* X-Real-IP
* Real-IP


Check for content integrity
+++++++++++++++++++++++++++

TODO


