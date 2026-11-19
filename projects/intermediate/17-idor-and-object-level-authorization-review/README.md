# Project 17: IDOR and Object-Level Authorization Review

**Level:** Intermediate  
**Focus:** Object-level access control  
**Status:** Detailed training walkthrough

## Objective
Perform a focused secure code review of object-level access control, tracing control flow and trust boundaries, validating the behavior in a local fixture, and testing a secure remediation.

## Scope and authorization
Use fictional sample code, synthetic identities, and a repository you own or are authorized to review. Do not test third-party or production systems without written authorization. All screenshots are simulated training illustrations, not genuine tool output or assessment evidence.

## Prerequisites
- Local application fixture with synthetic data
- Git, code editor, and relevant language runtime
- Semgrep or an approved SAST tool
- Unit/integration test harness
- Framework/library security documentation

## Review methodology
Create two fake users and records in a local fixture; trace identifier to lookup and authorization; test cross-account read/update/delete; enforce ownership in query or policy; add regression tests.

## Detailed review steps
1. Identify entry points, trust boundaries, security principals, and sensitive operations.
2. Trace untrusted values and security decisions through routes, middleware, service layers, data access, and configuration.
3. Verify the security control is enforced server-side and fails closed.
4. Inspect edge cases, error paths, alternate routes, background tasks, and framework defaults.
5. Reproduce only in the local fixture with synthetic data and controlled test cases.
6. Record file/function, relevant code path, preconditions, impact, and confidence.
7. Implement the fix and inspect the final diff for bypasses or regressions.

## Tools and commands
Read-only search examples:

```bash
grep -RInE 'findById|get\(.*id|params.*id|/users/|/orders/' samples/
semgrep scan --config auto samples/
git diff --check
```

Static-analysis alerts are leads. Confirm actual reachability, library semantics, effective configuration, and runtime behavior.

## Expected results
A complete control-flow trace, tested positive and negative cases, a confirmed finding or evidence-based no-finding result, and documented remediation.

## Finding and risk analysis
**Representative finding:** Changing an object identifier may expose or alter another synthetic user's record due to missing ownership enforcement.

**Mapping:** CWE-639; CWE-862; OWASP API1:2023 Broken Object Level Authorization

Assess severity using exploitability, privileges, affected data/actions, business impact, and compensating controls. Do not claim a CVE without a verified vulnerable dependency/product version.

## Remediation
Scope database lookups to the authenticated principal or apply explicit object-level policy checks before returning or mutating data.

## Validation and retesting
1. Add regression tests for allowed and denied scenarios.
2. Test boundary conditions and alternate routes or code paths.
3. Re-run SAST and manually review residual matches.
4. Run the relevant unit/integration tests and inspect the patch.
5. Record residual risk, assumptions, and reviewer sign-off.

## Evidence and reporting
Include sanitized source excerpts, flow diagrams, test cases/results, tool versions, severity rationale, remediation diff, and retest status. Use only fictional identities and data; never publish tokens, secrets, or production source.

## Simulated screenshots
These SVGs are fictional training mockups, not real application screenshots, scanner output, or proof of a live assessment.

![Source review environment](../../../_assets/screenshots/17-01-source-review.svg)

![Static analysis workflow](../../../_assets/screenshots/17-02-analysis.svg)

![Finding and remediation](../../../_assets/screenshots/17-03-remediation.svg)

## Deliverables
- Scope and review checklist
- Security control/data-flow notes
- Finding with CWE/OWASP mapping and severity rationale
- Secure code change and regression tests
- Retest results and concise report
