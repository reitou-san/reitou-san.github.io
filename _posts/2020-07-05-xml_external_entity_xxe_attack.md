---
title: "XML External Entity (XXE) attack"
date: 2020-07-05T10:00:00
categories:
  - blog
tags:
  - xxe
  - rough cuts
---

XXE detection in service endpoints
they can easily be triggered using proper Content-Type request header values (like text/xml or application/xml)

There are two types of XXE attacks: in-band and out-of-band (OOB-XXE).
1) An in-band XXE attack is the one in which the attacker can receive an immediate response to the XXE payload.

2) out-of-band XXE attacks (also called blind XXE), there is no immediate response from the web application and attacker has to reflect the output of their XXE payload to some other file or their own server.

```xml
<?xml version="1.0"?>
<!DOCTYPE root [<!ENTITY read SYSTEM 'file:///etc/passwd'>]>
<root>&read;</root>
```

https://www.christian-schneider.net/GenericXxeDetection.html
