=======================
Clean Connection Policy
=======================


Motivation
==========

The Clean Connection Policy is intended for ensuring content integrity during the archiving process.


DNS
+++

DNS queries can be captured and archives can be compromised.

Value-added DNS services such as OpenDNS may return entries for invalid domain names. For example, a user makes a typo and enters ``google.cmo`` instead of ``google.com``. The DNS query may respond with a server that provides users with a ad-supported search query.

Government censorship may intercept any DNS query and respond with an invalid IP address.

Captive portals may return DNS entries that point to a login server such as free wifi service agreements.

The user may have custom hostname entries in their HOSTS file.


Proxies
+++++++

Proxies may mangle content.

A bandwidth-reducing proxy may compress images destroying its original data.

A proxy may be strictly caching resources. If the user makes a request to a web page, the server does not fetch the images but rather returns an "error" image requesting the user to reload the page.

A proxy may be blocking advertisements.

A proxy may be stripping out HTTP headers from the original request.


Firewall
++++++++

Firewalls may restrict access to content.

A content-filtering firewall may replace a restricted page with an "error" page.

A firewall may restrict access to specific ports.

A firewall may inject a TCP reset packet into the connection.


On-the-fly modification
+++++++++++++++++++++++

It may be possible for on-the-fly modification of content by a man-in-the-middle attack.

An ISP may inject or replace advertisements of web pages. Or they may inject a bandwidth usage warning.

Secure connections may be intercepted with a different SSL certificate. This is typically used for free wifi login.


Procedure
=========

