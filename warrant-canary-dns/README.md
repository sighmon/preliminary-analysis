# Store a warrant canary in DNS

**Assumptions**
WC = Warrant Canary

**Problem**: Allow a machine readable warrant canary to remain globally cached (TTLs that match WC period) and therefore available even if your website is taken down or attacked.

**Solution**: Host your WC in a DNS TXT record.

**Issues to resolve**
* Due to TTL of DNS record and older response may be supplied, DNS queries should always be performed ignoring TTL or work on a 1/2th of WC validity period for TTL and have a full DNS recheck performed if the WC has expired.
* DNS TXT records wrap every 255 characters in quotes.
* Warrant Canary needs to be base64’d first, then process only the 255 characters between the quote marks.
* Maybe host a DNS creation service that lets users point to their warrant canary file and generates a subdomain and a DNS TXT record for them. i.e. [simonsigrecom.canarywatcher.com](https://simonsigrecom.canarywatcher.com)

**SS**
[simon.sigre@duckula ~]$ dig sighmoncom.simonsigre.com txt +short | sed 's/"//g' |  sed 's/ //g' | base64 -d | gpg2 --verify 
[simon.sigre@duckula ~]$ gpg --recv-keys 89BBF41FDC97AF5D

dig sighmoncom.simonsigre.com txt +short | sed 's/"//g' |  sed 's/ //g' | base64 -d | gpg2 --verify 2>&1  | awk -F " RSA key ID " '{print $2}' | xargs gpg --recv-keys || dig sighmoncom.simonsigre.com txt +short | sed 's/"//g' |  sed 's/ //g' | base64 -d | gpg2 --verify
