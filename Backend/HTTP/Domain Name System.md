The Domain Name System (DNS) is the phonebook of the Internet. Humans access information online through [domain names](https://www.cloudflare.com/learning/dns/glossary/what-is-a-domain-name/), like nytimes.com or espn.com. Web browsers interact through [Internet Protocol (IP)](https://www.cloudflare.com/learning/network-layer/internet-protocol/) addresses. 

DNS translates domain names to [IP addresses](https://www.cloudflare.com/learning/dns/glossary/what-is-my-ip-address/) so browsers can load Internet resources.

Each device connected to the Internet has a unique IP address which other machines use to find the device. DNS servers eliminate the need for humans to memorize IP addresses such as 192.168.1.1 (in IPv4), or more complex newer alphanumeric IP addresses such as 2400:cb00:2048:1::c629:d7a2 (in IPv6).

## How does DNS work?
When you request `www.example.com`, here’s the typical lookup process:

1. **Client (your computer/browser)** → asks _“What is the IP of www.example.com?”_
2.  **Recursive Resolver (usually your ISP’s DNS or Google DNS 8.8.8.8)** →
    - This is the system that takes responsibility to **find the answer for you**.
    - If it already knows the answer (cached), it replies immediately.
    - If not, it goes on a “hunt.”
3. **Root DNS servers** → tell the resolver _“I don’t know www.example.com, - _but I know where the `.com` servers are.”_
4. **TLD (Top-Level Domain) servers** (for `.com`) → tell the resolver _“Ask the authoritative server for example.com.”_
5. **Authoritative DNS server** → gives the actual IP (e.g., `93.184.216.34`).
6. The **resolver returns the answer to your computer**, and your browser can now connect. 


## **What is a DNS Lookup?**

A **DNS lookup** is the process of **translating a domain name (like `example.com`) into its corresponding IP address (like `93.184.216.34`)** so that your computer can connect to the correct server.

Think of it as looking up a person’s phone number in a phonebook before calling them.

## **Types of DNS Lookups**

There are mainly **two types**:
1. **Forward DNS Lookup**
    - Input: **Domain name** (e.g., `www.google.com`)
    - Output: **IP address** (e.g., `142.250.183.206`)
    - ✅ This is what happens most of the time when you browse the web.
2. **Reverse DNS Lookup (rDNS)**
    - Input: **IP address** (e.g., `142.250.183.206`)
    - Output: **Domain name** (e.g., `google.com`)
    - ✅ Used in email servers and network troubleshooting.

## **How a DNS Lookup Works (Forward Lookup Example)**

When you type `www.example.com` in your browser:

1. **Check local cache** → Your computer first looks in its memory (DNS cache).
2. **Ask the Recursive Resolver** → Usually your ISP’s DNS server, or public DNS like Google (8.8.8.8) or Cloudflare (1.1.1.1).
3. If the resolver doesn’t know, it queries step by step:
    - **Root DNS server** → "Where are the `.com` servers?"
    - **TLD DNS server** (for `.com`) → "Where is `example.com` managed?"
    - **Authoritative DNS server** (for `example.com`) → "The IP is `93.184.216.34`."
4. Resolver returns the IP to your computer.
5. Browser uses that IP to connect to the web server and load the site.
### Example in real life:

If you run this command in a terminal:

```bash
nslookup www.google.com
```

You’ll get something like:
```yaml
Server:  8.8.8.8
Address: 8.8.8.8

Non-authoritative answer:
Name:    www.google.com
Address: 142.250.183.206
```

This is a **DNS lookup result** showing the IP address of the domain.

👉 So, in short:  
**DNS Lookup = the process of asking “What IP address belongs to this domain name?” (or vice versa for reverse lookup).**

