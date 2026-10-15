# AWS Cloud Support and Incident Troubleshooting Lab

## Project Overview

A beginner cloud support portfolio focused on incident analysis, troubleshooting methodology, root-cause investigation, and technical documentation.

The project includes simulated AWS support incidents and hands-on troubleshooting exercises performed on a local Windows computer.

## Objectives

* Practice structured incident investigation and root-cause analysis.
* Understand common application, access, networking, storage, and performance issues.
* Document diagnostic steps, findings, corrective actions, and preventive measures.
* Develop practical command-line troubleshooting skills.

## AWS Concepts Covered

* Amazon EC2 — compute and instance troubleshooting
* Amazon S3 — storage access and permissions
* AWS Identity and Access Management (IAM) — access-denied scenarios
* Amazon VPC — networking and connectivity
* Amazon CloudWatch — monitoring and performance metrics

**Note:** The AWS incidents in this repository are simulated learning scenarios. No live AWS resources were deployed or modified.

## Hands-On Windows Troubleshooting

Performed on a local Windows 11 computer using PowerShell:

* Operating system information inspection
* Network connectivity testing with `ping`
* DNS lookup using `nslookup`
* HTTPS endpoint testing using `curl.exe`
* Filesystem drive usage inspection
* Process inspection using `Get-Process`

See [`hands-on-lab-01.md`](hands-on-lab-01.md) for commands, observed results, and interpretations.

## Incident Reports

| File                                  | Scenario                               |
| ------------------------------------- | -------------------------------------- |
| `incident-01-http-500.md`             | Simulated HTTP 500 application error   |
| `incident-02-iam-access-denied.md`    | Simulated S3 access-denied issue       |
| `incident-03-network-connectivity.md` | Simulated network connectivity failure |
| `incident-04-disk-space.md`           | Simulated disk-space issue             |
| `incident-05-high-cpu.md`             | Simulated high CPU utilization         |

Additional documentation includes a reusable incident template, lessons learned, a Linux troubleshooting guide, and a troubleshooting runbook.

## Skills Practiced

* Incident documentation
* Root-cause analysis methodology
* Basic Windows command-line troubleshooting
* Networking and DNS fundamentals
* IAM permissions concepts
* Storage and performance monitoring concepts
* Technical documentation and preventive-action planning

## Tools

* Windows PowerShell
* GitHub
* Markdown
* AWS service documentation and concepts

## Project Status

Completed as a documentation-based learning project with local Windows troubleshooting exercises. Live AWS troubleshooting and infrastructure deployment are future learning goals.
