# Project 27: XML External Entity and Parser Security Review

**Level:** Intermediate  
**Focus:** XML parsing  
**Status:** Detailed training walkthrough

## Objective
Review xml parsing in application source, trace security-relevant data/control flow, verify behavior in a local fixture, and validate remediation.

## Scope and authorization
Use fictional code and synthetic data in a repository you own or are authorized to review. No production or third-party testing without written authorization. Screenshots are simulated training illustrations, not actual assessment evidence.

## Prerequisites
- Local application fixture with synthetic data
- Git, code editor, and relevant runtime
- Semgrep or approved SAST tool
- Focused unit/integration test harness
- Framework/library documentation

## Review methodology
Use a local parser fixture with harmless synthetic XML; inspect parser flags and resolver behavior; test that external resolution is disabled using a stub resolver; validate normal XML still parses.

## Detailed review steps
1. Identify entry points, trust boundaries, shared state, and sensitive operations.
2. Trace relevant values through routes, middleware, services, libraries, and configuration.
3. Verify the security control is effective under normal, error, and edge conditions.
4. Inspect alternate code paths and framework defaults.
5. Reproduce only with harmless synthetic values in the local fixture.
6. Record affected file/function, flow, preconditions, impact, and confidence.
7. Apply remediation and inspect the final diff for bypasses or regressions.

## Tools and commands
```bash
grep -RInE 'DocumentBuilder|SAXParser|XMLReader|DOCTYPE|external.*entity|resolveEntity|lxml|etree' samples/
semgrep scan --config auto samples/
git diff --check
```

SAST output is a lead. Manually confirm reachability, effective runtime configuration, and library behavior.

## Expected results
A documented review trace, tests for relevant positive/negative cases, a confirmed finding or evidence-based no-finding result, and a validated fix.

## Finding and risk analysis
**Representative finding:** An XML parser may resolve external entities or process dangerous DTD features from untrusted documents.

**Mapping:** CWE-611; OWASP A05:2021

Assess severity based on exploitability, privileges, data sensitivity, business impact, and compensating controls. Do not assign a CVE to a generic code pattern.

## Remediation
Disable DTD and external entity resolution, use hardened parser settings, and prefer safe data formats where XML is unnecessary.

## Validation and retesting
1. Add regression tests for expected and rejected behavior.
2. Exercise edge cases and alternate code paths.
3. Re-run SAST and manually triage remaining matches.
4. Run focused tests and inspect the final diff.
5. Record residual risk and reviewer sign-off.

## Evidence and reporting
Include sanitized code excerpts, flow notes, test cases/results, tool versions, severity rationale, remediation diff, and retest status. Do not publish secrets, personal data, or production source.

## Simulated screenshots
Fictional instructional mockups only; not real editor captures, scanner output, or live assessment evidence.

![Source review](../../../_assets/screenshots/27-01-source-review.svg)

![Analysis workflow](../../../_assets/screenshots/27-02-analysis.svg)

![Remediation](../../../_assets/screenshots/27-03-remediation.svg)

## Deliverables
- Scope and review checklist
- Data-flow/security-control notes
- Finding with CWE/OWASP mapping and severity rationale
- Secure change and regression tests
- Retest results and concise report
