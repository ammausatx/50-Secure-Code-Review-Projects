# Project 09: Authentication and Password Storage Review

**Level:** Beginner  
**Focus:** Authentication  
**Status:** Detailed training walkthrough

## Objective
Perform a focused manual secure code review, trace untrusted data and security decisions through the relevant code path, confirm the weakness in a local fixture, and validate a safe remediation.

## Scope and authorization
Use only fictional sample code, synthetic data, and repositories you own or are authorized to review. Do not scan or test third-party or production systems without written authorization. Screenshots are simulated training illustrations, not genuine tool output or assessment evidence.

## Prerequisites
- Git repository containing a small local training fixture
- Code editor and the relevant language runtime
- Semgrep or another approved SAST tool
- Test harness with synthetic data
- Notes for source-to-sink tracing and evidence

## Review methodology
Use fake accounts and test-only credentials; trace registration through verification and reset; inspect hash algorithm and token lifecycle; replace unsafe storage with a vetted password-hashing API; test reset expiry and one-time use.

## Manual review steps
1. Identify the feature, trust boundaries, entry points, and security assumptions.
2. Locate sources, transformations, sensitive sinks, and enforcement controls.
3. Trace the complete path, including helper functions, framework middleware, configuration, and error handling.
4. Review the implementation against the expected security property: Authentication.
5. Reproduce only against the local fixture with synthetic values; distinguish scanner alerts from confirmed defects.
6. Document file/function, source-to-sink path, preconditions, impact, and confidence.
7. Apply the remediation and inspect the final diff for regressions or alternate unsafe paths.

## Tooling and commands
Suggested read-only search for review leads:

```bash
grep -RInE 'password|hash|compare|login|reset|mfa|otp' samples/
semgrep scan --config auto samples/
git diff --check
git status --short
```

Search results are leads, not proof. Confirm reachability, framework behavior, runtime configuration, and the complete data flow manually.

## Expected results
A documented source-to-sink or control-flow trace, a confirmed finding or evidence-based no-finding result, and a tested remediation with a regression test.

## Finding and risk analysis
**Representative finding:** Passwords are stored or compared insecurely, or authentication controls can be bypassed through flawed workflow logic.

**Mapping:** CWE-256; CWE-521; CWE-916; OWASP A07:2021

Severity must reflect reachability, required privileges, exploitability, data sensitivity, business impact, and compensating controls. Do not assign a CVE to a code pattern without a verified affected product/version.

## Remediation
Use a modern password-hashing library with calibrated parameters, generic auth errors, secure reset tokens, MFA where required, and server-side rate limits.

## Validation and retesting
1. Add tests for expected valid behavior and relevant negative/boundary cases.
2. Confirm the unsafe path is no longer reachable or the required control is enforced.
3. Re-run SAST and manually inspect any remaining matches.
4. Run the focused test suite and review the final diff.
5. Record residual risk, limitations, and reviewer sign-off.

## Evidence and reporting
Capture the affected file/function, sanitized code excerpt, data-flow diagram or notes, tool version/configuration, test result, severity rationale, and remediation diff. Never include real credentials, personal data, or production source code in public training evidence.

## Simulated screenshots
The following SVGs are fictional instructional mockups. They are not real editor captures, scanner output, or proof of a live assessment.

![Source review environment](../../../_assets/screenshots/09-01-source-review.svg)

![Static analysis workflow](../../../_assets/screenshots/09-02-analysis.svg)

![Finding and remediation](../../../_assets/screenshots/09-03-remediation.svg)

## Deliverables
- Scope and review checklist
- Source-to-sink/control-flow notes
- Finding with CWE/OWASP mapping and severity rationale
- Secure code change and regression tests
- Retest result and concise review report
