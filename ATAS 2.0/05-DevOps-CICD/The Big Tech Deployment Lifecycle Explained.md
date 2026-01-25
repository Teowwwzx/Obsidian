**Phase 1: CI (Continuous Integration) - The "Gatekeeper"**
- Where: GitHub Actions / GitLab CI
- Trigger: You push code.
- Steps:
  1. Lint & Static Analysis: "Is the code written correctly?" (Ruff/Black).
  2. Unit & Integration Tests: "Does the logic actually work?" (Pytest).
  3. Build: "Can we package this?" (Docker Build).
- Rule: If any step fails, the code is rejected . It never reaches the server. 

**Phase 2: CD (Continuous Deployment) - The "Rollout"**
- Where: AWS / GCP / Kubernetes
- Trigger: Merge to main branch.
- Steps:
  1. Migration Check: The new container starts. The entrypoint.sh runs schema migrations (Alembic).
  2. Health Check: The orchestrator (Kubernetes/Docker Swarm) pings /health .
  3. Rolling Update: Replaces old containers one by one. If health check fails, it rolls back automatically. 


**Phase 3: Observability - The "Watchtower"**
- Where: Datadog (likely what you meant by "Databog"), Prometheus, Grafana.
- Metrics:
  - Latency: "How long do requests take?" (e.g., p99 < 200ms).
  - Error Rate: "Are users seeing 500 errors?"
  - Saturation: "Is CPU/Memory full?"