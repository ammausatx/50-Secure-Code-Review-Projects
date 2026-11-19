# Project 31: Dependency and Supply Chain Code Review

**Level:** Intermediate  
**Focus:** Dependencies  
**Status:** Detailed training walkthrough

## Objective
Review dependencies across the local source repository, validate relevant security controls, and document prioritized remediation.

## Scope and authorization
Use only fictional code, synthetic data, and repositories you own or are authorized to review. No production or third-party testing without written authorization. Screenshots are simulated training illustrations, not real tool output or assessment evidence.

## Prerequisites
- Local source repository and synthetic configuration/data
- Git, code editor, and relevant toolchain
- Semgrep plus project-specific scanner where applicable
- Local test harness and documented review scope

## Review methodology
Use a disposable fixture with intentionally outdated package metadata; run the ecosystem's audit tool and OSV-Scanner; verify each advisory and reachability; update/pin safe versions; run regression tests and document residual risk.

## Detailed review steps
1. Define the repository paths, technologies, environments, and exclusions in scope.
2. Identify security-sensitive configuration and data flows.
3. Run appropriate static/configuration checks against local files only.
4. Manually validate each candidate finding, including effective configuration and runtime context.
5. Prioritize by exploitability, exposure, business impact, and compensating controls.
6. Implement remediation in the fixture and add a regression or policy test.
7. Re-run checks and review the final diff.

## Tools and commands
```bash
find samples/ -type f \( -name 'package*.json' -o -name 'requirements*.txt' -o -name 'pom.xml' -o -name 'go.mod' \) -print
semgrep scan --config auto samples/
git diff --check
```

Tool findings are leads; verify the exact resource, dependency, code path, or effective setting before reporting.

## Expected results
A sanitized inventory, a prioritized finding register, evidence-backed remediation recommendations, and repeatable validation.

## Finding and risk analysis
**Representative finding:** The application includes vulnerable, unmaintained, or unpinned components without a documented risk decision.

**Mapping:** CWE-1104; OWASP A06:2021 Vulnerable and Outdated Components

Severity must reflect context and impact. Avoid overstating risk or mapping generic configuration observations to unrelated CVEs.

## Remediation
Pin and update dependencies, commit lockfiles, remove unused packages, verify advisories and provenance, and establish a repeatable update process.

## Validation and retesting
1. Re-run the relevant scanner or test after the change.
2. Confirm the unsafe setting or code path is corrected.
3. Run functional tests to check for unintended breakage.
4. Inspect the final diff and record exceptions/residual risk.
5. Obtain owner/reviewer sign-off.

## Evidence and reporting
Include sanitized file paths, relevant excerpts, tool versions, scan configuration, validated findings, severity rationale, remediation diff, and retest status. Do not publish secrets, personal data, or proprietary source.

## Simulated screenshots
Fictional instructional mockups only; not real editor captures, scanner output, or live assessment evidence.

![Source review](../../../_assets/screenshots/31-01-source-review.svg)

![Analysis workflow](../../../_assets/screenshots/31-02-analysis.svg)

![Remediation](../../../_assets/screenshots/31-03-remediation.svg)

## Deliverables
- Scope and review checklist
- Inventory and security analysis notes
- Finding register with mapping and severity rationale
- Remediation plan and validation tests
- Retest summary and reviewer sign-off
