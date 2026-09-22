# CCST-IT-Support-Home-Lab
Hands-on IT Support labs covering Windows, networking, DNS, troubleshooting, and security.

Baseline Test Results
1. Network Configuration

The Windows endpoint was checked using ipconfig /all.

Key findings:

IPv4 address: 192.168.0.2
Subnet mask: 255.255.255.0
Default gateway: 192.168.0.1
DHCP: Enabled
DNS server: 2405:dc00:100::2
2. Internet Connectivity Test

Command:

ping 8.8.8.8

Result:

Packets sent: 4
Packets received: 4
Packet loss: 0%
Average response time: 96 ms

Conclusion: Basic IP connectivity was working.

3. DNS Resolution Test

Command:

nslookup google.com

Result:

DNS server responded successfully.
google.com resolved to IPv4 and IPv6 addresses.

Conclusion: The configured DNS service was functioning.

4. Public DNS Comparison

Cloudflare DNS:

nslookup google.com 1.1.1.1

Google DNS:

nslookup google.com 8.8.8.8

Both tests initially reported a 2-second DNS timeout but subsequently returned valid DNS responses.

5. Connectivity to Public DNS Servers

Commands:

ping 1.1.1.1

ping 8.8.8.8

Both returned 4/4 replies with 0% packet loss.

Conclusion: The public DNS server IP addresses were reachable.

6. IPv4 and IPv6 DNS Testing

Cloudflare IPv4 DNS query:

nslookup -type=A google.com 1.1.1.1

Result: Successful.

Cloudflare IPv6 DNS query:

nslookup -type=AAAA google.com 1.1.1.1

Result: Initial timeout followed by a successful response.

The configured DNS server was also tested directly:

nslookup -type=A google.com 2405:dc00:100::2

nslookup -type=AAAA google.com 2405:dc00:100::2

Both queries completed successfully.

Investigation Conclusion

The endpoint had working network connectivity and successful DNS resolution through its configured DNS server.

Direct queries to external public DNS resolvers showed an initial timeout before successful resolution. Connectivity to those resolver IP addresses was confirmed with ICMP ping.

No confirmed DNS configuration failure was identified during this investigation.

Status

🟢 Investigation Complete
