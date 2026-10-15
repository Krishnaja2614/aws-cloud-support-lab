# Linux Troubleshooting for Cloud Support

## 1. Purpose

This guide covers basic Linux commands useful for investigating server health, disk usage, CPU utilization, running processes, logs, and network connectivity.

These commands are commonly useful when supporting Linux-based cloud servers, including Amazon EC2 instances.

**Note:** The outputs below are illustrative examples, not results collected from a live server.

## 2. Check Disk Usage

### Command

```bash
df -h
```

**Purpose:** Displays filesystem capacity, used space, available space, and usage percentage in a human-readable format.

### Example output

```text
Filesystem      Size  Used Avail Use% Mounted on
/dev/root        20G   18G  2.0G  90% /
tmpfs           1.0G     0  1.0G   0% /dev/shm
```

**Interpretation:** The root filesystem is 90% full. Investigate which directories or files are consuming space before taking action.

### Find large directories

```bash
sudo du -sh /var/log
```

This estimates the total space used by `/var/log`. Use elevated privileges only when needed and authorized.

## 3. Check CPU and Running Processes

### Command

```bash
top
```

**Purpose:** Displays running processes and system resource usage, including CPU and memory.

**What to check:**

* Whether CPU utilization remains high.
* Which processes consume the most CPU.
* Whether one process behaves unexpectedly.
* Whether the system has enough available memory.

### List processes

```bash
ps aux
```

This displays running processes and their resource information.

### Filter for a process

```bash
ps aux | grep nginx
```

This searches the process listing for text matching `nginx`. The output can also include the `grep` command itself, so interpret results carefully.

## 4. Check Memory Usage

### Command

```bash
free -m
```

**Purpose:** Shows memory and swap usage in megabytes.

### Example output

```text
               total        used        free
Mem:            4096        2800         300
Swap:           1024         100         924
```

**Interpretation:** Low free memory alone does not necessarily indicate a problem because Linux uses memory for caching. Review available memory, swap activity, and application behaviour together.

## 5. Inspect System Logs

### View recent system log messages

```bash
sudo journalctl -n 50 --no-pager
```

Displays the most recent 50 system journal entries, where systemd journal logging is available.

### Follow logs in real time

```bash
sudo journalctl -f
```

Press `Ctrl + C` to stop following the log.

### Search a log file for errors

```bash
grep -i "error" application.log
```

Searches `application.log` for lines containing “error”, ignoring case. Replace the filename with the actual log file.

**Troubleshooting tip:** Note the incident timestamp and correlate log messages with the reported symptoms. Redact secrets and sensitive information before sharing logs.

## 6. Check Network Connectivity

### Test DNS resolution

```bash
nslookup example.com
```

Checks whether a hostname can be resolved using DNS, if `nslookup` is installed.

### Test basic reachability

```bash
ping -c 4 example.com
```

Sends four ICMP echo requests where supported.

**Important:** A failed ping does not prove that a server is down. ICMP traffic may be blocked.

### Test a TCP connection or HTTP endpoint

```bash
curl -I --max-time 5 https://example.com
```

Requests HTTP response headers and limits the wait to five seconds. A response such as `200 OK` commonly indicates that the endpoint responded successfully, though it does not prove every application function works.

### Check listening ports

```bash
sudo ss -lntp
```

Displays listening TCP sockets and, where permissions allow, associated process information.

## 7. Check Application Service Status

For a systemd-managed service, such as Nginx:

```bash
systemctl status nginx
```

**Purpose:** Checks the service state and displays recent status information.

To inspect recent service logs:

```bash
sudo journalctl -u nginx -n 50 --no-pager
```

Replace `nginx` with the actual service name.

Do not restart a production service without authorization and an understanding of the impact.

## 8. Quick Troubleshooting Reference

| Symptom              | First check          | Useful command           |
| -------------------- | -------------------- | ------------------------ |
| Disk nearly full     | Filesystem usage     | `df -h`                  |
| Large log files      | Log directory size   | `sudo du -sh /var/log`   |
| High CPU             | Active processes     | `top`                    |
| Memory pressure      | Memory and swap      | `free -m`                |
| Application errors   | Recent logs          | `journalctl`             |
| DNS issue            | Name resolution      | `nslookup`               |
| HTTP endpoint issue  | Response and timeout | `curl -I`                |
| Service unavailable  | Service status       | `systemctl status nginx` |
| Listening port issue | TCP listeners        | `ss -lntp`               |

## 9. Safe Troubleshooting Workflow

1. Record the symptom, timestamp, and affected system.
2. Start with read-only diagnostic commands.
3. Collect relevant logs and resource metrics.
4. Compare findings against expected behaviour.
5. Identify and verify the likely root cause.
6. Obtain approval before making changes.
7. Apply the smallest appropriate corrective action.
8. Repeat the checks to verify recovery.
9. Document the evidence, result, and follow-up action.

## 10. Limitations

The sample outputs in this guide are illustrative. They have not been collected from a live EC2 instance. Commands and available logs can vary across Linux distributions and configurations.

This guide demonstrates troubleshooting knowledge and is intended for learning and practice. It does not claim that live production incidents have been resolved.
