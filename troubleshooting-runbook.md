# Cloud Support Troubleshooting Runbook

## 1. Purpose

This runbook provides a structured process for investigating common cloud support incidents. It focuses on gathering evidence, identifying root causes, applying safe corrective actions, and verifying recovery.

**Scope:** AWS concepts and simulated incident scenarios. No live AWS resources are modified by this document.

## 2. Standard Troubleshooting Process

### Step 1: Understand the incident

* Identify the affected service, application, or resource.
* Record the start time, symptoms, impact, and any recent changes.
* Determine whether the issue affects one user or multiple users.

### Step 2: Check available evidence

* Review application and system logs.
* Check relevant metrics and alarms.
* Examine recent configuration or deployment changes.
* Record exact error messages and timestamps.

### Step 3: Identify possible causes

* List plausible causes based on the evidence.
* Test one hypothesis at a time.
* Avoid changing several settings simultaneously.

### Step 4: Apply a safe correction

* Follow the approved change process.
* Prefer the smallest reversible change.
* Avoid disabling security controls to make an error disappear.
* Obtain authorization before changing production resources.

### Step 5: Verify recovery

* Repeat the original failing operation.
* Check relevant logs and metrics.
* Confirm that the service is working as expected.
* Monitor for recurring errors.

### Step 6: Document and close

* Record the root cause and resolution.
* Include evidence collected before and after the fix.
* Document preventive actions and lessons learned.

## 3. Incident: HTTP 500 Error

**Symptoms:** An application returns HTTP 500, indicating an internal server error.

**Investigation:**

1. Reproduce the error and note its timestamp.
2. Check application logs around that time.
3. Check application health and dependency connectivity.
4. Review recent deployments and configuration changes.
5. Check whether database credentials, endpoints, and service availability are correct.

**Possible root causes:** Application exception, incorrect configuration, unavailable dependency, or a failed deployment.

**Resolution:** Correct the confirmed cause using an approved change. Do not assume the database is responsible without evidence.

**Verification:** Repeat the failing request, confirm the expected response, and check logs for new errors.

## 4. Incident: IAM Access Denied

**Symptoms:** An AWS API request or console action returns `AccessDenied`.

**Investigation:**

1. Identify the IAM user or role making the request.
2. Record the exact action and resource involved.
3. Review applicable identity-based and resource-based policies.
4. Check for explicit denies, permissions boundaries, session policies, and organization service control policies where applicable.
5. Confirm whether the request uses the expected role or credentials.

**Possible root causes:** Missing permission, explicit deny, resource policy restriction, or an incorrect identity.

**Resolution:** Request or apply only the minimum required permission through the approved access process. Never grant unrestricted administrator access just to bypass the error.

**Verification:** Retry the specific authorized operation and confirm that unrelated permissions remain restricted.

## 5. Incident: Network Connectivity Failure

**Symptoms:** A service cannot connect to another endpoint or times out.

**Investigation:**

1. Record source, destination, protocol, port, and timestamp.
2. Confirm that the destination service is running and listening on the expected port.
3. Check DNS resolution if a hostname is used.
4. Review VPC route tables and the relevant subnet routes.
5. Check security groups, network ACLs, and host-level firewall rules.
6. Confirm that the required connectivity path exists, such as a suitable gateway, peering connection, or VPN.

**Possible root causes:** Missing route, incorrect DNS, blocked traffic, wrong port, or an unavailable destination.

**Resolution:** Correct the specific confirmed issue while preserving network security.

**Verification:** Test name resolution and connectivity using an appropriate tool, then check application-level communication.

## 6. Incident: High Disk Usage

**Symptoms:** Disk utilization approaches capacity, applications fail to write files, or logs stop updating.

**Investigation:**

1. Run `df -h` to identify filesystems with high usage.
2. Use `du -sh` on appropriate directories to locate large directories.
3. Inspect logs, temporary files, and application-generated data.
4. Check whether log rotation and retention policies are configured.
5. Determine whether disk usage is growing continuously.

**Possible root causes:** Unrotated logs, large temporary files, unexpected application output, or insufficient capacity.

**Resolution:** Follow retention policies, archive or remove only approved files, and configure appropriate log rotation. Never delete unknown system files.

**Verification:** Rerun `df -h`, confirm sufficient free space, and verify application health.

## 7. Incident: High CPU Utilization

**Symptoms:** A server responds slowly and CPU utilization remains unusually high.

**Investigation:**

1. Review CPU metrics over time, not just a single reading.
2. Use `top` to identify processes consuming CPU.
3. Check system and application logs for unusual activity.
4. Review scheduled jobs, recent deployments, and traffic changes.
5. Determine whether the workload is expected or abnormal.

**Possible root causes:** A runaway process, intensive workload, recurring job, or sudden traffic increase.

**Resolution:** Follow the approved process to correct the workload or adjust capacity. Do not terminate critical processes without understanding their purpose.

**Verification:** Confirm that CPU utilization returns to an acceptable level and that response times improve.

## 8. AWS Evidence to Collect

| Area        | Evidence to review                                            |
| ----------- | ------------------------------------------------------------- |
| Compute     | EC2 instance state, system status checks, instance metrics    |
| Monitoring  | CloudWatch metrics, alarms, and available logs                |
| Access      | IAM identity, policies, denied action, affected resource      |
| Networking  | VPC routes, security groups, network ACLs, DNS                |
| Storage     | Volume capacity, filesystem usage, storage metrics            |
| Application | Error messages, timestamps, health checks, deployment history |

Actual evidence available depends on the service configuration and monitoring that has been enabled.

## 9. Incident Report Checklist

Before closing an incident, confirm that you have documented:

* [ ] Incident summary and impact
* [ ] Start time and relevant timestamps
* [ ] Evidence and diagnostic steps
* [ ] Root cause, or the fact that it remains unconfirmed
* [ ] Corrective action taken or recommended
* [ ] Verification results
* [ ] Preventive action or follow-up task

## 10. Safety and Limitations

* Follow least privilege and approved change procedures.
* Do not expose passwords, access keys, tokens, or customer data in logs or reports.
* Do not make unapproved production changes.
* Distinguish observed evidence from assumptions.
* The incidents in this portfolio are simulated unless explicitly identified as hands-on tests. This runbook is a learning resource, not a claim of live production troubleshooting experience.
