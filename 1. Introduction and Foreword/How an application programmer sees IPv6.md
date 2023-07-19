## How an application programmer sees IPv6

In a very theoretical world, an application programmer could rely on a
DNS lookup to return the best (and only) address of a remote host, and
could then pass that address directly to the network socket interface
without further ado. Unfortunately the real world is not that simple.
Even without considering the version number, there are several types of
IP address, and a DNS lookup may return a variety of addresses. In most
cases, applications will use the function `getaddrinfo()` ("get address
information") to obtain a list of valid addresses, typically containing
both IPv6 and IPv4 addresses. Which is the best one to use, and should
the program try more than one?

We do not go into this subject in detail, because this book is not aimed
primarily at application programmers. However, operators need to be
aware that the default behavior of most applications is simply to use
the *first* address returned by `getaddrinfo()`. Some applications (such
as web browsers) may use a smarter approach known as "happy eyeballs"
([RFC8305](https://www.rfc-editor.org/info/rfc8305)) by means of a
heuristic to detect which address gives the fastest response. However,
operators need to understand the various address types in order to
configure systems optimally, including the `getaddrinfo()` precedence
table ([RFC6724](https://www.rfc-editor.org/info/rfc6724)) in every
host.

When developing IPv6 enabled applications keep in mind that IPv6
addresses are longer and look different than IPv4 addresses. This may
sound obvious, but the past has shown that these are two of the most
common problems, especially when you store IPv6 addresses in a database
or having an input field in you application that is too small. Also,
regular expressions for validating IP addresses are different. As you
will learn later in this book there are different types of IPv6
addresses and several ways to write them. Make sure your application
does only accept the correct type of addresses and is also not too
strict and only accepts one format. Users want to use copy-and-paste or
automation and the input format of an IP address may not always what
your application expects. Always remember: "Be conservative in what you
do, be liberal in what you accept from other". And it's probably always
a good idea not to reinvent the wheel but use library functions your
programming language of choice provides, e.g. the ipaddress module for
python. And please don't hard-code IP addresses of any kind in your
code. Always make them configurable and if possible use FQDNs instead of
IPs.

IPv6 is also important when testing software. And it gets quite complex.
If your application both supports IPv6 and IPv4 you have to test IPv4 only,
IPv6 only and dual-stack.

Address types are discussed further in
[2. Addresses](../2.%20IPv6%20Basic%20Technology/Addresses.md). How
applications relate to a mixture of IPv4 and IPv6 addresses is also
discussed in
[3. Dual stack scenarios](../3.%20Coexistence%20with%20Legacy%20IPv4/Dual%20stack%20scenarios.md).

<!-- Link lines generated automatically; do not delete -->

### [<ins>Previous</ins>](How%20a%20user%20sees%20IPv6.md) [<ins>Next</ins>](How%20a%20network%20operations%20center%20sees%20IPv6.md) [<ins>Chapter Contents</ins>](1.%20Introduction%20and%20Foreword.md)
