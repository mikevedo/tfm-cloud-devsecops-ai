# CI/CD Pipeline Design
## TFM – Cloud DevSecOps Pipeline with AI-Based Vulnerability Prioritization

---

## 1. Purpose

This document describes the CI/CD pipeline design used to build, test, scan, and gate application releases.  
The pipeline integrates multiple security scanners and then applies an AI-based prioritization module to reduce noise and support contextual gating decisions.

Two applications are used as test artifacts:
- **FastAPI Mini App**: controlled application to represent a modern microservice.
- **OWASP Juice Shop**: intentionally vulnerable benchmark to produce reproducible security findings.

---

## 2. Pipeline Principles

- **Shift-left security**: security scans run early and automatically on every PR/commit.
- **Reproducibility**: results must be consistent across runs.
- **Fail smart, not fail always**: blocking decisions depend on contextual risk, not raw tool severity alone.
- **Cloud-agnostic design**: Azure is a reference runtime, but pipeline logic remains portable.
- **Separation of concerns**:
  - Scanners generate findings.
  - Aggregation normalizes outputs.
  - AI module prioritizes and explains.
  - Gate enforces decisions.

---

## 3. Triggering Strategy

### 3.1 Events
- **Pull Request (PR)**: main security quality gate. Produces full reports + AI prioritization summary.
- **Push to main**: runs a full pipeline and (if passed) deploys.
- **Manual dispatch** (optional): allows controlled executions for demos and evaluation.

### 3.2 Branch Policy (recommended)
- `main`: protected branch (merges only through PR).
- Feature branches: development work.

---

## 4. Pipeline Stages (High Level)

### Stage A — Source & Preparation
**Goal:** obtain source code and pipeline context.
- Checkout code
- Setup runtime (Python) and dependencies
- Determine which app(s) are targeted (FastAPI / Juice Shop)

**Output:** ready workspace for build/test/scans.

---

### Stage B — Build & Unit Tests
**Goal:** ensure baseline quality before security.
- Build Docker image(s)
- Run unit tests (FastAPI)
- Optional linting

**Output:** tested artifacts + build metadata.

---

### Stage C — Security Scanning
**Goal:** generate findings from multiple sources.

Recommended tools (open-source / free):
- **SAST**: CodeQL (GitHub Advanced Security optional, or default CodeQL if available)
- **Secrets**: Gitleaks
- **IaC**: Checkov (Terraform)
- **Container**: Trivy
- **SCA** (dependencies): can be covered by CodeQL or additional tooling if needed

Optional (later):
- **DAST**: OWASP ZAP (mainly for Juice Shop demo)

**Output:** raw findings (SARIF/JSON) per tool.

---

### Stage D — Findings Aggregation & Normalization
**Goal:** convert scanner outputs into a single consistent schema.

Actions:
- Parse each tool output
- Normalize fields: tool_name, rule_id, severity, file, line, package, cve, cvss, confidence, etc.
- Enrich with context (see next section)

**Output:** `findings_normalized.json`

---

### Stage E — Context Enrichment (Risk Factors)
**Goal:** add project-specific context required for prioritization.

Examples of contextual factors:
- Application type: FastAPI vs Juice Shop
- Environment target: dev/test/prod (or demo)
- Asset criticality (simple classification for TFM)
- Exposure: public-facing vs internal
- Stage relevance: build vs deploy gate
- Exploitability hints (if CVE known, EPSS optional)

**Output:** `findings_enriched.json`

---

### Stage F — AI-Based Prioritization
**Goal:** produce risk score + priority + explanation for each finding.

The AI module receives enriched findings and outputs:
- `risk_score` (0–100)
- `priority` (Critical/High/Medium/Low)
- `explanation` (top factors contributing to score)

**Output:** `prioritized_findings.json` + summary table.

---

### Stage G — Gate Decision
**Goal:** decide whether the pipeline passes or fails.

Gate policy (initial recommendation):
- Fail if:
  - Any finding has `priority = Critical`, OR
  - Risk score exceeds threshold (e.g., `risk_score >= 85`)
- Warn (do not fail) if:
  - High risk findings exist but below fail threshold
- Always publish reports for transparency.

**Output:** pass/fail + artifacts published.

---

### Stage H — Deploy (Reference: Azure)
**Goal:** deploy only when gate passes.
- Deploy FastAPI app container (Azure as reference)
- Keep deploy steps isolated so cloud provider can be swapped later.

**Output:** deployed service + deployment logs.

---

## 5. Artifact & Report Strategy

The pipeline must always publish artifacts, even on failure:
- Raw scanner outputs
- Normalized + enriched findings
- Prioritized findings + explanation summary
- Gate decision report (why it passed/failed)

This improves reproducibility and supports TFM evaluation.

---

## 6. Minimal Viable Pipeline (MVP) vs Final

### MVP (first implementation)
- Build + tests
- Run scanners (SAST, Secrets, IaC, Container)
- Normalize findings
- Rule-based scoring + simple explanations
- Gate based on threshold

### Final (enhanced)
- Supervised model (optional) using labeled priorities
- Better explainability
- Optional DAST integration (ZAP) for Juice Shop
- Evaluation metrics added (Precision@K, noise reduction)

---

## 7. Acceptance Criteria

The pipeline design is considered implemented when:
- PR triggers run full pipeline with published reports
- Findings are normalized into a single schema
- AI module produces risk_score, priority, explanation
- Gate decision is automatic and reproducible
- Deployment only occurs when gate passes
