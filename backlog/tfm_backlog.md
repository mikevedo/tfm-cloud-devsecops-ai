# TFM Backlog – Cloud DevSecOps with AI-Based Vulnerability Prioritization

This backlog defines the planning, milestones, and deliverables for the Final Master's Project (TFM).  
Each item represents a concrete and verifiable outcome aligned with academic and engineering best practices.

---

## Phase 1 – Definition and Design

### Week 1 – Project Definition
- Define problem statement and objectives
- Establish project scope and constraints
- Deliverable: Project Charter document

### Week 2 – System Architecture
- Design high-level DevSecOps architecture
- Define CI/CD flow and security integration points
- Identify AI module position in the pipeline
- Deliverable: Architecture diagram

---

## Phase 2 – Pipeline Foundation

### Week 3 – CI/CD Base Pipeline
- Configure GitHub Actions workflow
- Implement build and test stages
- Integrate FastAPI mini application
- Deliverable: Functional CI pipeline

### Week 4 – Security Scanning Integration
- Integrate SAST, secrets detection, and dependency scanning
- Integrate container and IaC scanning
- Include OWASP Juice Shop as vulnerable benchmark
- Deliverable: Security scanning stage operational

---

## Phase 3 – AI-Based Prioritization Module

### Week 5 – Data Modeling and Feature Definition
- Define vulnerability data schema
- Identify contextual risk factors
- Prepare dataset from scanner outputs
- Deliverable: Feature definition document

### Week 6 – AI Model Design
- Select prioritization approach (rule-based + supervised learning)
- Define scoring logic and thresholds
- Implement explainability factors
- Deliverable: AI module design document

### Week 7 – AI Module Implementation
- Implement prioritization logic
- Integrate AI module into pipeline
- Generate risk scores and priority levels
- Deliverable: AI module prototype

---

## Phase 4 – Pipeline Gating and Deployment

### Week 8 – Pipeline Gates
- Define pass/fail criteria based on risk thresholds
- Implement automated gating logic
- Validate behavior across different scenarios
- Deliverable: Context-aware pipeline gates

### Week 9 – Cloud Deployment
- Deploy pipeline artifacts to Azure (reference)
- Maintain cloud-agnostic configuration
- Validate end-to-end pipeline execution
- Deliverable: Deployed pipeline

---

## Phase 5 – Evaluation and Documentation

### Week 10 – Evaluation and Metrics
- Measure noise reduction and prioritization accuracy
- Evaluate Precision@K and pipeline efficiency
- Analyze results and limitations
- Deliverable: Evaluation results

### Week 11 – Documentation and Refinement
- Finalize documentation
- Update diagrams and backlog
- Prepare conclusions
- Deliverable: Complete TFM documentation

### Week 12 – Final Review
- Perform final validation
- Prepare defense material
- Deliverable: Final TFM submission
