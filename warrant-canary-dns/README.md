# Store a warrant canary in DNS

**Problem**: Allow a machine readable warrant canary to remain globally cached (TTLs that match warrant canary period) and therefore available even if your website is taken down or attacked.

**Solution**: Host your warrant canary in a DNS TXT record.

**Issues to resolve**

* DNS TXT records wrap every 255 characters in quotes.
* Warrant Canary needs to be base64’d first, then process only the 255 characters between the quote marks.
* Maybe host a DNS creation service that lets users point to their warrant canary file and generates a subdomain and a DNS TXT record for them. i.e. [simonsigrecom.canarywatcher.com](https://simonsigrecom.canarywatcher.com)