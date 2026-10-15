# Hands-On Lab 01: Windows Network Troubleshooting

## Objective

Practice basic system identification, IP connectivity testing, and DNS troubleshooting using Windows PowerShell.

## Environment

* Operating system: Windows 11 Home Single Language
* Terminal: Windows PowerShell
* Lab type: Local computer troubleshooting
* AWS resources: Not used

## Test 1: Operating System Information

**Command:**

```powershell
systeminfo | findstr /B /C:"OS Name" /C:"OS Version"
```

**Observed result:**

* OS: Microsoft Windows 11 Home Single Language
* Version/build information: Build 26200

**Conclusion:** The operating system information command completed and returned system details.

## Test 2: IP Connectivity

**Command:**

```powershell
ping -n 4 1.1.1.1
```

**Observed result:**

* Packets sent: 4
* Packets received: 4
* Packets lost: 0
* Packet loss: 0%
* Minimum round-trip time: 16 ms
* Maximum round-trip time: 18 ms
* Average round-trip time: 17 ms

**Conclusion:** All four ICMP echo requests received replies. This confirms connectivity to the tested destination at the time of the test. It does not prove that every network destination or application is reachable.

## Test 3: DNS Resolution

**Command:**

```powershell
nslookup example.com
```

**Observed result:**

* The command returned a DNS response.
* The response included a non-authoritative answer.
* The configured DNS server was labelled `Unknown`.

**Conclusion:** DNS resolution succeeded for the tested hostname. The `Unknown` server label alone does not establish a DNS failure.

Sensitive local network details have been omitted from this report.

## Test 4: Network Adapter Inspection

**Command:**

```powershell
ipconfig
```

**Observed result:**

Some adapters displayed `Media disconnected`.

**Conclusion:** A disconnected adapter may simply be unused. The output alone does not indicate a fault with the active network connection.

Private IP addresses, usernames, and other local network details are intentionally omitted.

## Summary

| Check                           | Result     |
| ------------------------------- | ---------- |
| Operating system identification | Completed  |
| ICMP connectivity test          | Passed     |
| DNS lookup                      | Successful |
| Adapter inspection              | Completed  |

## Limitations

These tests were performed on a local Windows computer, not on an AWS EC2 instance. The results demonstrate basic diagnostic practice and do not represent live AWS troubleshooting experience.

## Next steps

* Check disk capacity and memory usage.
* Inspect running processes.
* Test an HTTP endpoint.
* Record the observed output and explain any findings.
## Test 5: Filesystem Drive Usage

**Command:**

```powershell
Get-PSDrive -PSProvider FileSystem
```

**Observed results:**

| Drive |      Used |     Free |
| ----- | --------: | -------: |
| C:    | 385.80 GB | 22.19 GB |
| F:    |   1.52 GB | 48.48 GB |

**Interpretation:** The C: drive has approximately 5.4% free space based on the displayed figures. This is a reason to monitor storage and investigate large files if free space continues to decrease. The result alone does not establish that the drive is failing.

## Test 6: Process Inspection

**Command:**

```powershell
Get-Process | Sort-Object CPU -Descending | Select-Object -First 5 ProcessName, CPU
```

**Observed result:** The command listed five processes with the highest accumulated CPU time. Chrome and ChatGPT-related processes appeared in the results.

**Interpretation:** The `CPU` property represents accumulated processor time in seconds, not an instantaneous CPU percentage. To investigate current CPU utilization, use Task Manager or a suitable real-time monitoring command.

**Privacy note:** Local usernames and unrelated personal details are excluded from this report.
## Test 7: HTTPS Endpoint Check

**Command:**

```powershell
curl.exe -I --max-time 10 https://example.com
```

**Observed result:**

```text
HTTP/1.1 200 OK
```

**Interpretation:** The HTTPS endpoint returned a successful HTTP status code. This confirms that the endpoint responded to the request at the time of testing. It does not prove that every function of the website works correctly.

**Troubleshooting skills demonstrated:** HTTP response interpretation, endpoint connectivity testing, and basic command-line diagnostics.
