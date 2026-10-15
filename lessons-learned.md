# Lessons Learned

## Incident 01: HTTP 500

Application logs help identify server-side failures. Investigate the underlying cause rather than relying on the HTTP status alone.

## Incident 02: IAM Access Denied

Check the identity, requested action, resource, and applicable permissions before recommending a change.

## Incident 03: Network Connectivity

Investigate routes, gateways, security controls, DNS, and the destination service systematically.

## Incident 04: Disk Space

Use disk diagnostics to find capacity problems and apply safe cleanup and retention procedures.

## Incident 05: High CPU

Correlate monitoring metrics with application logs and workload activity before deciding whether to change capacity.

## Overall Learning

Cloud support requires evidence-based troubleshooting, least-privilege access, careful verification, clear documentation, and prevention of recurring incidents.

## Project Limitations

The initial incident scenarios use simulated evidence. They demonstrate troubleshooting methodology, not verified fixes on live AWS infrastructure.

## Future Improvements

* Complete suitable hands-on AWS labs.
* Capture genuine test results.
* Add an architecture diagram.
* Publish the repository on GitHub.
