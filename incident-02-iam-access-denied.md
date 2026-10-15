# Incident 02: IAM Access Denied

## Incident Summary

**Incident ID:** INC-002
**Severity:** Medium (simulated)
**Service:** AWS Identity and Access Management (IAM)
**Status:** Simulated investigation
**Environment:** Local simulation

## 1. Problem Report

A user reports that they cannot view objects in a particular Amazon S3 bucket. The request returns an Access Denied error.

## 2. Symptoms

* The user can authenticate successfully.
* An attempt to list objects in the bucket is denied.
* The user does not have the required effective permissions for the requested action.

## 3. Diagnostic Evidence

Simulated diagnostic output:

Error: AccessDenied
Action attempted: s3:ListBucket
Resource: arn:aws:s3:::example-support-bucket

This output is illustrative and was not obtained from a real AWS account.

## 4. Investigation

1. Confirm which IAM user or role made the request.
2. Identify the denied action and target resource.
3. Review the attached identity-based IAM policies.
4. Check for explicit denies in applicable policies.
5. Review the bucket policy and any applicable organization or permissions-boundary restrictions.
6. Confirm that the requested action is authorized for the correct resource.

## 5. Root Cause

For this simulated scenario, the user's identity-based policy does not allow the required s3:ListBucket action on the specified bucket.

## 6. Corrective Action

Request or apply a least-privilege policy that allows s3:ListBucket on the specific bucket, subject to organizational approval and any other applicable restrictions.

Do not grant broad permissions such as unrestricted administrator access merely to resolve this incident.

## 7. Verification

* Retry the listing request using the authorized identity.
* Confirm that access succeeds if no other restriction applies.
* Confirm that unrelated resources remain inaccessible.
* Review the result and record the evidence.

## 8. Prevention

* Follow the principle of least privilege.
* Review IAM policies regularly.
* Document permission changes.
* Avoid sharing credentials between users.
* Investigate denied actions before changing permissions.

## 9. Learning Outcome

AWS IAM evaluates permissions using applicable policies and restrictions. An Access Denied response requires investigation; a missing identity-based allow is only one possible cause.

## Evidence

This is a simulated incident. No actual IAM policies or AWS resources were modified.
