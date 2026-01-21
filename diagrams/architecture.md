flowchart LR
    Developer -->|Commit / PR| GitHub

    subgraph Applications["Applications Under Test"]
        FastAPI["FastAPI Mini App"]
        JuiceShop["OWASP Juice Shop"]
    end

    GitHub -->|Trigger| GitHubActions

    subgraph CI_CD_Pipeline["CI/CD Pipeline"]
        GitHubActions --> Build
        Build --> Test
        Test --> SecurityScans

        subgraph SecurityScans["Security Scanning Stage"]
            SAST
            Secrets
            IaC
            Container
            DAST
        end

        SecurityScans --> FindingsAggregation
        FindingsAggregation --> AI_Module["AI-Based Prioritization Module"]
        AI_Module --> RiskScoring
        RiskScoring --> GateDecision
    end

    Applications --> Build

    GateDecision -->|Pass| Deploy
    GateDecision -->|Fail| PipelineStop

    Deploy --> CloudRuntime["Cloud Environment (Azure Reference)"]
