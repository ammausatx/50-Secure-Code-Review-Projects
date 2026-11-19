# Project 13: Insecure Error Handling and Information Disclosure Review

**Level:** Beginner  
**Focus:** Error handling  
**Status:** Detailed training walkthrough

## Objective
Perform a focused manual secure code review, trace the relevant input and control paths, confirm weaknesses in a local fixture, and validate secure remediation.

## Scope and authorization
Use fictional sample code and synthetic data in a repository you own or are authorized to review. Do not test production or third-party systems without written authorization. Screenshots are simulated training illustrations, not genuine tool output or assessment evidence.

## Prerequisites
- Git repository with a small local training fixture
- Code editor and relevant language runtime
- Semgrep or another approved SAST tool
- Synthetic test data and a local test harness
- Notes for source-to-sink tracing and evidence

## Review methodology
Create a local exception fixture with fake secrets; trigger expected error paths; trace what is returned to clients versus written to logs; add structured redaction and generic responses; test both client output and protected log content.

## Manual review steps
1. Identify the feature, trust boundaries, entry points, and security assumptions.
2. Locate user-controlled sources, transformations, sensitive sinks, and enforcement controls.
3. Trace the complete path, including helper functions, middleware, configuration, and error handling.
4. Compare implementation behavior with the intended security requirement.
5. Reproduce only against the local fixture with synthetic values; distinguish scanner alerts from confirmed defects.
6. Record file/function, data-flow path, preconditions, impact, and confidence.
7. Apply remediation and inspect the final diff for alternate unsafe paths.

## Tooling and commands
Suggested read-only review commands:

```bash
grep -RInE 'stack|traceback|DEBUG|display_errors|console\.log|logger\.|printStackTrace' samples/
semgrep scan --config auto samples/
git diff --check
git status --short
```

Search results are leads, not proof. Confirm reachability, framework behavior, runtime configuration, and complete data flow manually.

## Expected results
A documented review trace, a confirmed finding or evidence-based no-finding result, and a tested remediation with regression coverage.

## Finding and risk analysis
**Representative finding:** An exception response or log record reveals stack traces, filesystem paths, tokens, passwords, or sensitive request data.

**Mapping:** CWE-209; CWE-532; OWASP A09:2021 Security Logging and Monitoring Failures

Severity must reflect reachability, privileges, exploitability, data sensitivity, business impact, and compensating controls. Do not assign a CVE to a generic code pattern without a verified affected product/version.

## Remediation
Return generic external errors with correlation IDs; keep detailed diagnostics in access-controlled logs; redact secrets and personal data; disable debug mode in production.

## Validation and retesting
1. Add tests for valid behavior and relevant negative/boundary cases.
2. Confirm the unsafe path is no longer reachable or the required control is enforced.
3. Re-run SAST and manually triage remaining matches.
4. Run the focused test suite and inspect the final diff.
5. Record residual risk, limitations, and reviewer sign-off.

## Evidence and reporting
Capture affected file/function, sanitized code excerpt, source-to-sink notes, tool version/configuration, test results, severity rationale, and remediation diff. Never publish real credentials, personal data, or production source code.

## Simulated screenshots
These SVGs are fictional instructional mockups. They are not real editor captures, scanner output, or evidence of a live assessment.

![Source review environment](../../../_assets/screenshots/13-01-source-review.svg)

![Static analysis workflow](../../../_assets/screenshots/13-02-analysis.svg)

![Finding and remediation](../../../_assets/screenshots/13-03-remediation.svg)

## Deliverables
- Scope and review checklist
- Source-to-sink/control-flow notes
- Finding with CWE/OWASP mapping and severity rationale
- Secure code change and regression tests
- Retest result and concise review report
