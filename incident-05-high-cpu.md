# Incident 05: High CPU Utilization

## Incident Summary

**Incident ID:** INC-005
**Severity:** Medium (simulated)
**Service:** Amazon EC2 and Amazon CloudWatch
**Status:** Simulated investigation
**Environment:** Local simulation

## 1. Problem Report

Users report that an application is responding slowly. The support team suspects high CPU utilization.

## 2. Symptoms

* Application response times increase.
* Requests take longer to complete.
* CPU utilization remains unusually high.

## 3. Diagnostic Evidence

Simulated monitoring data:

Time: 10:00 AM — CPU: 35%
Time: 10:05 AM — CPU: 72%
Time: 10:10 AM — CPU: 96%
Time: 10:15 AM — CPU: 98%

These are illustrative values, not actual Amazon CloudWatch measurements.

## 4. Investigation

1. Review CPU utilization trends in CloudWatch, if available.
2. Identify when the increase started.
3. Correlate CPU metrics with application logs and recent deployments.
4. Check running processes and workload changes where system access is available.
5. Investigate repeated jobs, inefficient queries, unexpected traffic, or resource-intensive tasks.
6. Determine whether the instance is undersized for its workload.

## 5. Root Cause

For this simulated scenario, a scheduled application job repeatedly runs because its scheduling configuration is incorrect, consuming excessive CPU.

## 6. Corrective Action

* Confirm the repeated job using logs and process information.
* Correct the scheduling configuration.
* Stop or reschedule the repeated job using the approved procedure.
* Monitor CPU utilization and application response times after the correction.

Scaling the instance may be appropriate if the workload genuinely requires more capacity, but investigate the cause first.

## 7. Verification

* Confirm CPU utilization returns to an acceptable level.
* Check application response times.
* Verify that the scheduled job runs at the intended frequency.
* Review monitoring data for recurring spikes.

## 8. Prevention

* Configure CPU monitoring and suitable alarms.
* Review scheduled jobs and application workloads.
* Investigate recurring performance spikes.
* Establish capacity-planning practices.

## 9. Learning Outcome

Monitoring metrics help identify performance symptoms, but logs and workload analysis are needed to establish the root cause.

## Evidence

All monitoring data is simulated. No real EC2 instance or CloudWatch alarm was created or modified.
