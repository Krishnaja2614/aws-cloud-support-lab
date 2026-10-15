# Incident 01: Website Returns HTTP 500

## Incident Summary

**Incident ID:** INC-001
**Severity:** Medium (simulated)
**Service:** Web application
**Status:** Investigation in progress
**Environment:** Local simulation

## 1. Problem Report

A user reports that the website returns an HTTP 500 Internal Server Error.

## 2. Symptoms

* The server responds to the request.
* The application fails while processing the request.
* The user cannot access the expected page.

## 3. Diagnostic Evidence

Simulated application log:

2026-10-15 10:00:00 INFO Request received: GET /dashboard
2026-10-15 10:00:01 ERROR Database connection failed
2026-10-15 10:00:01 ERROR Dashboard request returned HTTP 500

These are example log entries created for this project, not logs from a real AWS environment.

## 4. Investigation

1. Confirm the reported HTTP status code.
2. Review the application logs around the failure time.
3. Identify the database connection error.
4. Check the database endpoint, connection settings, credentials, and network access.
5. Verify the suspected cause before making changes.

## 5. Root Cause

For this simulated scenario, the database endpoint in the application configuration is incorrect.

## 6. Corrective Action

Correct the database endpoint and restart or reload the application if required by its configuration.

## 7. Verification

* Confirm that the application can connect to the database.
* Repeat the dashboard request.
* Verify that the expected page loads successfully.
* Confirm that the relevant error no longer appears in the logs.

## 8. Prevention

* Validate configuration changes before deployment.
* Monitor application errors.
* Keep configuration values documented.
* Avoid storing credentials directly in source code.

## 9. Learning Outcome

HTTP 500 indicates a server-side failure. Application logs provide evidence that helps narrow down the cause; the status code alone does not prove the root cause.

## Evidence

This incident uses simulated logs and a hypothetical configuration issue. No real AWS resources were changed.
