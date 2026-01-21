# Project Charter  
## TFM – Cloud DevSecOps Pipeline with AI-Based Vulnerability Prioritization

---

## 1. Project Overview

Modern DevSecOps pipelines integrate multiple automated security tools such as SAST, SCA, IaC, and container scanners. While these tools significantly improve security coverage, they also generate a large volume of findings, many of which lack contextual prioritization. This results in excessive security noise, alert fatigue, and inefficient remediation efforts.

This Final Master's Project (TFM) focuses on the design and implementation of a cloud-native DevSecOps pipeline that integrates automated security controls and introduces an AI-based vulnerability prioritization module to support decision-making during CI/CD executions.

Azure is used as a reference implementation, while the overall architecture is designed to remain cloud-agnostic.

---

## 2. Problem Statement

Traditional DevSecOps pipelines treat security findings in isolation, relying primarily on static severity scores (e.g., CVSS). This approach does not consider contextual factors such as asset criticality, deployment environment, exploitability indicators, or pipeline stage relevance.

As a result:
- High volumes of low-priority findings block pipelines unnecessarily
- Critical vulnerabilities may not be addressed in a timely manner
- Security teams experience alert fatigue
- Development velocity is negatively impacted

There is a need for a systematic approach that enables contextual prioritization of vulnerabilities to reduce noise and improve remediation efficiency.

---

## 3. Objectives

### 3.1 General Objective
To design and implement a cloud-native DevSecOps pipeline that integrates automated security scanning and an AI-based module for contextual vulnerability prioritization.

### 3.2 Specific Objectives
- Design a modular and cloud-agnostic DevSecOps pipeline architecture
- Integrate multiple security scanners within CI/CD workflows
- Develop a vulnerability prioritization model based on contextual risk factors
- Implement decision-support outputs to guide pipeline gating decisions
- Evaluate the effectiveness of the prioritization approach using quantitative metrics

---

## 4. Project Scope

### 4.1 In Scope
- CI/CD pipeline implementation using GitHub Actions
- Integration of security tools (SAST, secrets detection, IaC, container scanning)
- Cloud-native deployment (Azure as reference)
- AI-based vulnerability prioritization and scoring
- Definition of pipeline gates based on risk thresholds
- Metrics evaluation (e.g., noise reduction, prioritization accuracy)

### 4.2 Out of Scope
- Automatic discovery of new vulnerabilities
- Replacement of existing security scanners
- Real-time production security monitoring
- Use of Large Language Models (LLMs) in runtime environments

---

## 5. AI Module Definition

The AI module implemented in this project does not perform vulnerability detection. Instead, it operates on findings produced by existing security tools.

### Inputs:
- Vulnerability metadata (severity, category)
- Contextual information (asset type, environment, pipeline stage)
- Scanner source and confidence level

### Outputs:
- Risk score
- Priority classification (e.g., Critical, High, Medium, Low)
- Explainable factors contributing to the prioritization decision

The AI module functions as a decision-support system rather than an autonomous security control.

---

## 6. Evaluation Metrics

The effectiveness of the proposed solution will be evaluated using the following metrics:
- Reduction in total vulnerability noise
- Precision@K for prioritized findings
- Percentage reduction in unnecessary pipeline blocks
- Consistency of prioritization decisions across executions

---

## 7. Deliverables

- DevSecOps pipeline implementation
- AI-based vulnerability prioritization module
- Architecture and workflow diagrams
- Project documentation and evaluation results
- Final TFM report

---

## 8. Constraints and Assumptions

- The project is developed within an academic timeframe
- Open-source tools are prioritized
- Azure services are used as reference but not as a strict dependency
- The solution is designed for demonstration and evaluation purposes

---

## 9. Success Criteria

The project will be considered successful if it demonstrates:
- A functional and reproducible DevSecOps pipeline
- Measurable reduction of security noise
- Clear and explainable vulnerability prioritization
- Alignment with academic and industry best practices
