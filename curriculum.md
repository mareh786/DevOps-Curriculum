
# DevOps Curriculum 2026 – Detailed Outline

This is the expanded view of the curriculum from the main README. Each module links to its dedicated file in `/topics/`.

**Goal**: Build practical, production-ready skills over 8–12 weeks. Focus on free tools, hands-on practice, and real-world trade-offs.

**Total estimated effort**: 200–300 hours (theory + labs + projects)

### Module Breakdown

1. **Foundations & Culture** (Weeks 1–2)  
   - What DevOps really means (not just tools)  
   - Key frameworks: CALMS, Three Ways, DORA metrics  
   - Linux essentials: CLI, processes, file systems, networking basics, users/permissions  
   - Scripting intro (Bash basics)  
   - SDLC vs DevOps lifecycle  
   → See: [topics/01-foundations.md](./topics/01-foundations.md)

2. **Version Control & Collaboration** (Week 3)  
   - Git deep dive: branching strategies, rebasing, hooks, cherry-pick  
   - GitHub/GitLab: PRs, reviews, protected branches, issues  
   - Common workflows (GitFlow, trunk-based)  
   → See: [topics/02-version-control.md](./topics/02-version-control.md)

3. **CI & Build Automation** (Weeks 4–5)  
   - CI concepts: pipelines, triggers, artifacts  
   - GitHub Actions (primary focus): workflows, matrix builds, caching  
   - Testing integration & basic security scans  
   - Jenkins intro (if enterprise context needed)  
   → See: [topics/03-ci-cd.md](./topics/03-ci-cd.md)

4. **Containerization** (Week 6)  
   - Docker fundamentals: images, containers, Dockerfile best practices  
   - Multi-stage builds, volumes, networks  
   - Docker Compose for local multi-service apps  
   - Basic security & scanning (Trivy)  
   → See: [topics/04-containers.md](./topics/04-containers.md)

5. **Orchestration & Infrastructure as Code** (Weeks 7–8)  
   - Kubernetes basics: Pods, Deployments, Services, ConfigMaps/Secrets  
   - kubectl & Minikube/kind for local clusters  
   - Terraform: providers, modules, state management  
   - Ansible intro: playbooks, roles, ad-hoc commands  
   → See: [topics/05-orchestration-iac.md](./topics/05-orchestration-iac.md)

6. **Continuous Delivery & GitOps** (Week 9)  
   - CD patterns: blue-green, canary, rolling updates  
   - GitOps principles  
   - ArgoCD setup & app deployment  
   - Flux alternative overview  
   → See: [topics/06-gitops-cd.md](./topics/06-gitops-cd.md)

7. **Cloud & Observability** (Weeks 10–11)  
   - AWS core (focus): EC2, VPC, IAM, S3, EKS basics  
   - Observability stack: Prometheus + Grafana  
   - Logging basics (Loki or CloudWatch)  
   - Alerting & basic tracing  
   → See: [topics/07-cloud-observability.md](./topics/07-cloud-observability.md)

8. **DevSecOps & Final Deliverables** (Week 12)  
   - Shift-left security: secrets (Vault or AWS Secrets Manager), scanning (Snyk/Trivy)  
   - SLOs, error budgets intro  
   - Portfolio building: Document your work  
   - Alternatives to single capstone: 3–5 themed projects or progressive app milestones  
   → See: [topics/08-devsecops-hands-on.md](./topics/08-devsecops-hands-on.md)

