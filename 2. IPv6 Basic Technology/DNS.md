## DNS

We assume that the reader has a good general understanding of the Domain Name System (DNS). Many aspects of the DNS are unaffected by IPv6, because it was designed on very general principles.

A specific Resource Record type is defined to embed IPv6 addresses: the AAAA Record \[[RFC3596](https://www.rfc-editor.org/info/rfc3596)]. This simply provides a 128 bit IPv6 address in the same way that an A record provides an IPv4 address. (AAAA is normally pronounced "Quad-A".)

Similarly, reverse lookup is enabled by the `IP6.ARPA` domain. This is done
using 4-byte nibbles represented as hexadecimal characters, so the address
`2001:db8:4006:80b:a1b3:6d7a:3f65:dd13` will appear as
`3.1.d.d.5.6.f.3.a.7.d.6.3.b.1.a.b.0.8.0.6.0.0.4.8.b.d.0.1.0.0.2.IP6.ARPA.`
Clearly, these entries are for computers, not for humans. A neat trick, at least
on Linux, is to use the host command:

```
host 2001:db8:4006:80b:a1b3:6d7a:3f65:dd13
Host 3.1.d.d.5.6.f.3.a.7.d.6.3.b.1.a.b.0.8.0.6.0.0.4.8.b.d.0.1.0.0.2.ip6.arpa not found: 3(NXDOMAIN)
```

There are also a lot of other tools / libraries to help you with this. Note that
if you to the mapping by hand and make a mistake many DNS servers will happily
load the data and you will have a hard time finding the issues.

A corollary of defining the AAAA record is that DNS lookups that *indirectly* cause an A record lookup must also cause a AAAA lookup. This concerns NS, SRV and MX lookups.

This change also affects API calls that involve the DNS. The old `gethostbyname()` and `gethostbyaddr()` calls are **OBSOLETE** and should no longer be used. They are replaced by `getaddrinfo()` and `getnameinfo()`, which handle IPv6 as well as IPv4. In particular, `getaddrinfo()` provides the programmer with a list of both IPv6 and IPv4 addresses, and it is the programmer's job to decide which one to use. The order in which addresses are presented to the programmer is determined by a local configuration table on the host, in a way described by [RFC6724](https://www.rfc-editor.org/info/rfc6724). Unfortunately there is no standard mechanism for remote configuration of this table. Operators need to be aware of this complexity when attempting to cause users to favor IPv6 over IPv4 (or the converse).

Apart from this, in an ideal world DNS for IPv6 should not cause extra operational issues. However, in practice, there are some matters of concern:

- As noted in [2. Managed configuration](../2.%20IPv6%20Basic%20Technology/Managed%20configuration.md), the DNS server for a subnet must be announced by a Router Advertisement even if DHCPv6 is in use.

- DNS IPv6 Transport Operational Guidelines are documented in [BCP91](https://www.rfc-editor.org/info/bcp91).

- Considerations for Reverse DNS in IPv6 for Internet Service Providers are documented in [RFC8501](https://www.rfc-editor.org/info/rfc8501).


<!-- Link lines generated automatically; do not delete -->
### [<ins>Previous</ins>](Managed%20configuration.md) [<ins>Next</ins>](Routing.md) [<ins>Chapter Contents</ins>](2.%20IPv6%20Basic%20Technology.md)
