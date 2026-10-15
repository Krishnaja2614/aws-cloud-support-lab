# Incident 03: Network Connectivity Failure

## Incident Summary

**Incident ID:** INC-003
**Severity:** High (simulated)
**Service:** Amazon EC2 and Amazon VPC
**Status:** Simulated investigation
**Environment:** Local simulation

## 1. Problem Report

An application server cannot connect to an external service.

## 2. Symptoms

* The application reports a connection timeout.
* The destination service cannot be reached.
* The failure may be caused by routing, firewall rules, DNS, or the destination service.

## 3. Diagnostic Evidence

Simulated diagnostic output:

Destination: 198.51.100.20:443
Result: Connection timed out
Route table review: No matching route to the internet gateway

The IP address is reserved for documentation examples. This is illustrative output, not a real connectivity test.

## 4. Investigation

1. Confirm the source and destination addresses and ports.
2. Check whether the destination service is available.
3. Review the EC2 instance subnet and route table.
4. Check security group outbound rules and network ACL rules.
5. Determine whether the instance has a valid internet access path.
6. Check DNS resolution if the destination uses a hostname.

## 5. Root Cause

For this simulated scenario, the public subnet route table lacks a default route to the internet gateway.

## 6. Corrective Action

If the instance is intended to be publicly reachable, verify that the VPC has an attached internet gateway and that the subnet route table contains the appropriate default route.

Also confirm that the instance has a public IPv4 address and that security controls permit the required traffic.

For private instances, use an architecture appropriate to the requirements instead of automatically making the instance public.

## 7. Verification

* Confirm the route table configuration.
* Test connectivity to the intended destination.
* Review the results and relevant logs.
* Confirm that only the required traffic is allowed.

## 8. Prevention

* Document network architecture and routes.
* Review security rules regularly.
* Monitor connectivity failures.
* Avoid exposing private resources unnecessarily.

## 9. Learning Outcome

Network troubleshooting requires checking the complete path between source and destination. A timeout alone does not prove that a route is missing.

## Evidence

All diagnostic output is simulated. No real AWS network resources were changed.
