# Incident 04: Disk Space Exhaustion

## Incident Summary

**Incident ID:** INC-004
**Severity:** Medium (simulated)
**Service:** Linux server / EC2
**Status:** Simulated investigation
**Environment:** Local simulation

## 1. Problem Report

An application becomes slow and fails to write new log entries. The support team suspects that the server is running out of disk space.

## 2. Symptoms

* Application writes fail.
* Temporary files cannot be created.
* The server may report a no-space-left-on-device error.

## 3. Diagnostic Evidence

Simulated Linux command output:

$ df -h

Filesystem      Size  Used  Avail  Use%
/dev/root        10G   9.8G   200M   98%

Simulated application message:

ERROR: No space left on device

This is example output, not a result collected from a real server.

## 4. Investigation

1. Check filesystem usage with df -h.
2. Identify large directories using appropriate disk-usage commands.
3. Review application logs and temporary files.
4. Determine whether log rotation or cleanup has failed.
5. Check whether the disk is full or the filesystem has run out of inodes.

## 5. Root Cause

For this simulated scenario, application logs have accumulated without proper rotation and consumed most of the available disk space.

## 6. Corrective Action

* Identify the logs consuming the space.
* Follow the application's log-retention policy.
* Archive or remove only files confirmed safe to remove.
* Configure log rotation.
* Expand the storage volume if justified by capacity requirements.

Never delete unknown system files just to free space.

## 7. Verification

* Run df -h again.
* Confirm sufficient free space.
* Verify that the application can write logs and process requests.
* Check that log rotation works as expected.

## 8. Prevention

* Configure log rotation and retention.
* Monitor disk utilization.
* Set disk-space alerts.
* Review storage capacity periodically.

## 9. Learning Outcome

Linux disk diagnostics help identify capacity problems. Safe remediation requires finding the cause before removing files.

## Evidence

All command output is simulated. No actual Linux server or AWS storage volume was modified.
