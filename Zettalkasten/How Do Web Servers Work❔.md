202405171846
Meta Tags: #question 
Tags: [[computer networking]] 

# How do Web Servers Work❔

>[!note] URL
>Stands for **uniform resource locator**.

## Basic Process

![[Pasted image 20240517185248.png]]

## Behind the Scenes

1. The browser takes a URL and breaks it into **three** parts:

	- The protocol ("http")
	- The server name ("www.howstuffworks.com")
	- The file name ("web-server.htm")

2. The [[browser]] communicates with a [[ How Do Domain Name Servers (DNS) Work❔|name server]] to translate the server name, "www.howstuffworks.com", into an [[#IP Addresses|IP Address]], which is then used to connect to the server machine.

3. The [[browser]] then forms a connection to the server at that [[IP Address]] on [[port]] 80.

4. Following the protocol, "http", the browser sends a GET request to the server, asking for the file "https://www.howstuffworks.com/web-server.htm". 

>[!note] 
>Cookies may be sent from browser to server with the GET request. See [[How Do Internet Cookies Work❔]].

5. The server then sends the [[How Do Web Pages Work❔|HTML text]] for the Web page to the browser. (Cookies may also be sent from server to browser in the header for the page.) The browser reads the [[How Do Web Pages Work❔|HTML tags]] and formats the page onto your screen.

## The Internet

See [[internet#From (1)|internet]].

## Clients and Servers

In general, all of the machines on the Internet can be categorized as **servers** and **clients**. 

>[!info] servers
>Machines that provide services (like Web servers or FTP servers) to other machines.

>[!info] clients
>Machines that are used to connect to services provided by **servers**.

When you connect to Yahoo! at www.yahoo.com to read a page, Yahoo! is providing a machine (probably a cluster of very large machines), for use on the Internet, to service your request - a **server**.

Your machine, on the other hand, is probably providing no services to anyone else on the Internet - a **client**. 

>[!note]
>It is possible and common for a machine to be both a server and a client, but for our purposes here you can think of most machines as one or the other.

## IP Addresses

Each machines on the Internet is assigned a unique address called an IP address. IP stands for **Internet protocol**, and these addresses are 32-bit numbers, normally expressed as four *octets* in a *dotted decimal number*. 

```
216.27.61.137
```

>[!info] octet
>Has a value between 0 and 255, which is $2^8$ possibilities per octet.

A server has a static IP address that does not change very often. A Home machine that is dialing up through a modem often has an IP address that is assigned by the ISP when the machine dials in. That IP address is unique for **that session** - it may be different the next time the machine dials in. This way, an ISP only needs one IP address for each modem it supports, rather than for each customer. 

An IP address is all you need to communicate with a server; instead of typing the server name, you can use the IP address instead. 

Some servers require more, but most large servers do not.

## Domain Names

Because

1. Most people have trouble remembering the IP addresses and
2. IP addresses sometimes need to change,

all servers on the Internet also have human-readable names, called **domain names**. For example, www.howstuffworks.com.

Domain names actually have three parts:

1. The host name ("www")
2. The domain name ("howstuffworks")
3. The top-level domain name ("com")

The ".com" and ".net" domains are managed by the registrar called **VeriSign**. Other registrars (RegistryPro, NeuLevel and Public Interest Registry) manage the other domains (like .pro, .biz and .org).

VeriSign creates the top-level domain names and guarantees that all names within a top-level domain are unique. VeriSign also maintains contact information for each site and runs the "whois" database. The host name is created by the company hosting the domain. "www" is a very common host name, but many places now either omit it or replace it with a different one that indicates a specific area of the site. For example, see stackexchange sites.

## Name Servers

A set of servers called **domain name servers** (DNS) map human-readable names to their IP addresses. These servers are simple databases that map names to IP addresses, and they are distributed all over the Internet. Most individual companies, ISPs and universities maintain small name servers to map host names to IP addresses. There are also central name servers that use data supplied by VeriSign to map domain names to IP addresses.

From the URL "https://www.howstuffworks.com/web-server.htm", your browser extracts the middle part and passes it to a DNS, and the DNS returns the correct IP address. 

A number of name servers may be involved to get the right IP address. For example, in the case of www.howstuffworks.com, the name server for the "com" top-level domain will know the IP address for the name server that knows host names, and a separate query to that name server, operated by the HowStuffWorks ISP, may deliver the actual IP address for the HowStuffWorks server machine.

## Ports

Any server machine makes its services available to the Internet using numbered **ports**, one for each service that is available on the server. For example, if a server machine is running a Web server and an FTP server, the Web server would typically be available on port 80, and the FTP server would be available on port 21. Clients connect to a service at a specific IP address and on a specific port.

Each of the most well-known services is available at a well-known port number. Here are some common port numbers:

- echo 7
- daytime 13
- qotd 17 (Quote of the Day)
- ftp 21
- telnet 23
- smtp 25 (Simple Mail Transfer, meaning e-mail)
- time 37
- nameserver 53
- nicname 43 (Who Is)
- gopher 70
- finger 79
- WWW 80

If the server machine accepts connections on a port from the outside world, and if a [[firewall]] is not protecting the port, you can connect to the port from anywhere on the Internet and use the service. 

>[!Important]
>Nothing forces a service to be on a specific port. If you were to set up your own machine and load Web server software on it, you could put the Web server on port 918, or any other unused port, if you wanted to. Then, if your machine were known as xxx.yyy.com, someone on the Internet could connect to your server with the URL **http://xxx.yyy.com:918**. the ":918" explicitly specifies the port number, and would have to be included for someone to reach your server. When no port is specified, the browser simply assumes that the server is using the well-known port.

## Protocols

Once a client has connected a service on a particular port, it accesses the service using a specific **protocol**.

>[!info] protocol
>The pre-defined way that someone who wants to use a service talks with that service. The "someone" could be a person, but more often it is a computer program like a Web browser. Protocols are often text, and simply describe how the client and server will have their conversation.

Perhaps the simplest protocol is the **daytime protocol**. If you connect to port 13 on a machine that supports a day time server, the server will send you its impression of the current date and time and then close the connection. The protocol is, "If you connect to me, I will send you the date and time and then disconnect." 

Most protocols are more involved than daytime and are specified in Request for Comment (RFC) documents that are publicly available. Every Web server on the Internet conforms to the HTTP protocol, summarized nicely in [The Original HTTP as defined in 1991](https://www.w3.org/Protocols/HTTP/AsImplemented.html). 

The most basic form of the protocol understood by an HTTP server involves just one command: GET. If you connect to a server that understands the HTTP protocol and tell it to "GET filename," the server will respond by sending you the contents of the named file and then disconnecting. 

In the original HTTP protocol, all you would have sent was the actual filename, such as "/" or "/web-server.htm". The protocol was later modified to handle the sending of the complete URL. This has allowed companies to host **virtual domains**, where many domains live on a single machine, to use one IP address for all of the domains they host.

## Security

Most servers add some level of security to the serving process. For example, if you have ever gone to a Web page and had the browser pop up a dialog box asking for your name and password, you have encountered a password-protected page. The serve lets the owner of the page maintain a list of names and passwords for those people who are allowed to access the page; the server lets only those people who know the proper password see the page. 

More advanced servers add further security to allow an [[How Does Encryption Work❔|encrypted]] connection between server and browser, so that sensitive information can be sent on the internet.

That's really all there is to a Web server that delivers standard, static pages. Static pages are those that do not change unless the creator edits the page.

## Dynamic Pages

But what about the Web pages that are **dynamic**? For example:

- Any guest book allows you to enter a message in a HTML form, and the next time the guest book is viewed, the page will contain the new entry.
- The whois form at Network Solutions allows you to enter a domain name on a form, and the page returned is different depending on the domain name entered.
- Any search engine lets you enter keywords on an HTML form, and then it dynamically creates a page based on the keywords  you enter.

In all of these cases, the Web server isn't simply "looking up a file". It is actually processing information and generating a page based on the specifics of the query.

---
# *References*
https://computer.howstuffworks.com/web-server.htm