# DNS Troubleshooting Results

## Test Summary

| Test                          | Result  | Observation                                  |
| ----------------------------- | ------- | -------------------------------------------- |
| `ipconfig`                    | Passed  | Valid IPv4 configuration and default gateway |
| `ping 1.1.1.1`                | Passed  | 4/4 replies, 0% packet loss                  |
| `ping 8.8.8.8`                | Passed  | 4/4 replies, 0% packet loss                  |
| `nslookup google.com 1.1.1.1` | Partial | Timeout displayed before DNS response        |
| `nslookup google.com 8.8.8.8` | Partial | Timeout displayed before DNS response        |
| A record lookup               | Passed  | IPv4 DNS record returned                     |
| AAAA record lookup            | Partial | Timeout displayed before IPv6 DNS response   |
| IPv6 ping                     | Passed  | 4/4 replies, 0% packet loss                  |

## Key Findings

The workstation had working IPv4 and IPv6 connectivity.

Both Cloudflare DNS and Google DNS were able to resolve `google.com`, but the DNS tests displayed timeout messages before returning valid DNS records.

This indicates that DNS resolution was functioning, but the requests showed response delays during testing.

## Conclusion

The tests did not indicate a complete loss of internet connectivity or DNS resolution.

Further investigation would include checking local DNS configuration, router/DHCP DNS settings, IPv4 versus IPv6 DNS behaviour, and whether security software or network equipment contributes to the observed DNS delays.
