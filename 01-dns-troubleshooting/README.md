# DNS Troubleshooting Lab

## Overview

This lab demonstrates practical DNS troubleshooting on a Windows 11 system using built in Windows networking tools.

The objective was to determine whether connectivity problems were related to general network connectivity or DNS name resolution.

## Scenario

A Windows workstation is experiencing possible DNS resolution issues.

The troubleshooting process was used to determine:

* Whether the workstation had network connectivity
* Whether external IP addresses were reachable
* Whether DNS servers could resolve domain names
* Whether IPv4 and IPv6 DNS resolution were working
* Whether DNS responses were consistent when using different public DNS servers

## Environment

| Item               | Details                          |
| ------------------ | -------------------------------- |
| Operating System   | Windows 11                       |
| Connection         | Wi-Fi                            |
| Network Adapter    | Intel(R) Wi-Fi 6 AX200 160MHz    |
| Local IPv4 Address | 192.168.0.2                      |
| Subnet             | 192.168.0.0/24                   |
| Default Gateway    | 192.168.0.1                      |
| DNS Testing        | Cloudflare and Google Public DNS |
| Tools              | ipconfig, ping, nslookup         |

> Note: Personal or sensitive network information has been excluded from this documentation.

## Troubleshooting Process

### 1. Check Network Configuration

The first step was to inspect the workstation's network configuration.

```text
ipconfig
```

The workstation had a valid IPv4 address and default gateway.

**Finding:** The local network configuration appeared valid.

---

### 2. Test External IPv4 Connectivity

Connectivity was tested using Cloudflare's public IP address.

```text
ping 1.1.1.1
```

**Result:**

* 4 packets sent
* 4 packets received
* 0% packet loss
* Average response time: approximately 40 ms

**Finding:** External IPv4 connectivity was working.

---

### 3. Test Google DNS Connectivity

A second external IP address was tested.

```text
ping 8.8.8.8
```

**Result:**

* 4 packets sent
* 4 packets received
* 0% packet loss
* Average response time: approximately 96 ms

**Finding:** The workstation could communicate with Google's public DNS server by IP address.

---

### 4. Test DNS Resolution

DNS resolution was tested against Cloudflare DNS.

```text
nslookup google.com 1.1.1.1
```

The request displayed a timeout before returning valid DNS records.

**Finding:** DNS resolution was working, but the request experienced a response delay.

---

### 5. Test Google DNS Resolution

The same domain was tested against Google Public DNS.

```text
nslookup google.com 8.8.8.8
```

The request also displayed a timeout before returning valid DNS records.

**Finding:** Both public DNS servers were able to resolve the domain, although the requests showed timeout behaviour.

---

### 6. Test IPv4 DNS Resolution

An A-record lookup was performed.

```text
nslookup -type=A google.com 1.1.1.1
```

The lookup successfully returned an IPv4 address.

**Finding:** IPv4 DNS resolution was working.

---

### 7. Test IPv6 DNS Resolution

An AAAA-record lookup was performed.

```text
nslookup -type=AAAA google.com 1.1.1.1
```

The request initially displayed a timeout and then returned an IPv6 address.

**Finding:** IPv6 DNS resolution was working, although the request experienced a delay.

---

### 8. Test IPv6 Connectivity

IPv6 connectivity to the DNS server was tested.

```text
ping -6 2405:dc00:100::2
```

**Result:**

* 4 packets sent
* 4 packets received
* 0% packet loss
* Average response time: approximately 66 ms

**Finding:** IPv6 connectivity was working.

## Troubleshooting Summary

| Test                          | Result  | Finding                            |
| ----------------------------- | ------- | ---------------------------------- |
| `ipconfig`                    | Passed  | Valid local network configuration  |
| `ping 1.1.1.1`                | Passed  | External IPv4 connectivity working |
| `ping 8.8.8.8`                | Passed  | External IPv4 connectivity working |
| `nslookup google.com 1.1.1.1` | Partial | Timeout before DNS response        |
| `nslookup google.com 8.8.8.8` | Partial | Timeout before DNS response        |
| A-record lookup               | Passed  | IPv4 DNS resolution working        |
| AAAA-record lookup            | Partial | Timeout before IPv6 DNS response   |
| IPv6 ping                     | Passed  | IPv6 connectivity working          |

## Findings

The workstation had working IPv4 and IPv6 connectivity.

Both Cloudflare DNS and Google DNS were able to resolve `google.com`, but the `nslookup` tests displayed timeout messages before returning valid DNS records.

This indicates that DNS resolution was functioning, but the DNS requests showed response delays during testing.

## Further Investigation

Additional troubleshooting could include:

* Checking the configured DNS servers
* Testing the router/DHCP DNS configuration
* Comparing DNS response times
* Comparing IPv4 and IPv6 DNS behaviour
* Testing another network connection
* Checking firewall or security software
* Reviewing router logs if available

## Tools Used

* Windows Command Prompt
* `ipconfig`
* `ping`
* `nslookup`

## Skills Demonstrated

* Windows network troubleshooting
* TCP/IP fundamentals
* IPv4 troubleshooting
* IPv6 troubleshooting
* DNS troubleshooting
* DNS A and AAAA record testing
* Network connectivity testing
* Command-line troubleshooting
* Problem isolation
* Technical documentation

## Key Takeaway

This lab demonstrates a structured troubleshooting approach:

**Check configuration → Test IP connectivity → Test DNS → Isolate the problem → Document findings**
