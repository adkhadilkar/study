# 8-Month AI/ML Plan (Go + DevOps + Postgres → High-Paid AI/LLM Roles)

**Start:** 2026-02-06  
**Cadence:** 16 sprints × 15 days  
**Assumed weekly time:** ~8–12 hrs/week (adjust as needed)

## Target roles
- **LLM / Applied AI Engineer** (RAG, agents, evals, product features)
- **ML Platform / AI Infrastructure Engineer** (serving, scaling, observability, cost/reliability)

## Industry-friendly stack
- Python + FastAPI, Postgres + pgvector, Redis
- Docker, Kubernetes, Terraform
- OpenTelemetry + Prometheus/Grafana
- LangChain/LlamaIndex, vLLM

## Portfolio (pin these)
1. `rag-prod-assistant` (main)
2. `llm-serving-lab` (differentiator)
3. `ai-system-design-notes`
4. `go-loadtest-kit`
5. Optional: `mini-ml-lab`

## Sprint success checklist (every 15 days)
- [ ] Demo (GIF/video/screenshots)
- [ ] README updated (what changed + how to run)
- [ ] CI green (lint + tests)
- [ ] Measurable result (quality score / p95 latency / throughput / cost note)
- [ ] Reflection (what worked, what broke, next fix)

## 15-day sprints (detailed)

### Sprint 1 (2026-02-06 → 2026-02-20): Bootstrap: repo skeleton + CI + Docker

**In simple words:** Create a production-quality FastAPI repo you can confidently build on for the next 8 months.

**Time estimate:** ~14.0 hrs total (Week 1 ~7.5 hrs, Week 2 ~6.5 hrs)


**What you’ll do (checklist)**

**Week 1**

- [ ] (~2.0 hrs) Create repo structure (src/, tests/, scripts/, docs/) + basic FastAPI app with `/health`.
  - Expected: Repo runs locally; `/health` returns 200.
- [ ] (~1.5 hrs) Add config management (env vars) + typed settings (Pydantic) + `.env.example`.
  - Expected: Settings load cleanly; no secrets committed.
- [ ] (~2.0 hrs) Add dev tooling: ruff + formatting + pre-commit hooks.
  - Expected: One command checks style locally.
- [ ] (~2.0 hrs) Add pytest + at least 5 small tests (health, config, utils).
  - Expected: Tests pass locally and in CI.

**Week 2**

- [ ] (~2.0 hrs) Add Dockerfile + docker-compose for app + Postgres + Redis.
  - Expected: `docker compose up` boots everything.
- [ ] (~2.0 hrs) Add GitHub Actions CI: lint + tests + build container.
  - Expected: CI green on clean checkout.
- [ ] (~1.5 hrs) Add structured JSON logging + request ID middleware.
  - Expected: Logs include request_id and endpoint.
- [ ] (~1.0 hrs) Write README: how to run, how to test, what this project is.
  - Expected: README enables anyone to run in <10 min.

**How to validate you achieved it (Definition of Done)**

- ✅ Fresh machine can run `docker compose up` and open `/docs` without manual steps.
- ✅ CI runs lint + tests on every PR and is consistently green.
- ✅ You can add a new endpoint + test in <30 minutes.

**GitHub artifacts to publish (to show learning)**

- 📌 Repo badges: CI + lint + tests
- 📌 Short demo GIF/video in README showing `/docs` and a test run

**Learn (good sources for this sprint)**

- FastAPI Tutorial: First Steps: https://fastapi.tiangolo.com/tutorial/first-steps/
- Pydantic v2 docs: https://docs.pydantic.dev/latest/
- pytest: Getting Started: https://docs.pytest.org/en/stable/getting-started.html
- Ruff linter docs: https://docs.astral.sh/ruff/
- YouTube: FastAPI (freeCodeCamp): https://www.youtube.com/watch?v=tLKKmouUams
### Sprint 2 (2026-02-21 → 2026-03-07): Vectors 101: pgvector schema + ingestion + similarity search

**In simple words:** Make Postgres store embeddings and perform fast similarity search for RAG.

**Time estimate:** ~16.0 hrs total (Week 1 ~8.5 hrs, Week 2 ~7.5 hrs)


**What you’ll do (checklist)**

**Week 1**

- [ ] (~1.5 hrs) Enable `pgvector` in local Postgres container and verify with a small SQL query.
  - Expected: You can `SELECT '[1,2,3]'::vector;` successfully.
- [ ] (~2.5 hrs) Design schema: documents, chunks, embeddings (include metadata fields like source, page, timestamp).
  - Expected: SQL migrations exist; schema diagram in docs.
- [ ] (~2.5 hrs) Write ingestion pipeline: load markdown/text → chunk with overlap → store chunks + metadata.
  - Expected: Ingest script processes a folder into DB.
- [ ] (~2.0 hrs) Add embedding generation step (provider or local model) and store vectors.
  - Expected: Chunks have vectors in DB.

**Week 2**

- [ ] (~2.0 hrs) Add vector index (ivfflat/hnsw depending on setup) + document it.
  - Expected: Similarity queries are fast and repeatable.
- [ ] (~2.5 hrs) Implement `similarity_search(query, top_k, filters)` with scores and metadata.
  - Expected: Function returns top-k relevant chunks.
- [ ] (~2.0 hrs) Add tests: insert known vectors and validate nearest neighbor ordering.
  - Expected: Tests prove search correctness.
- [ ] (~1.0 hrs) Add `make ingest` + `make search` commands for quick demos.
  - Expected: One-liners show ingestion + retrieval working.

**How to validate you achieved it (Definition of Done)**

- ✅ A query retrieves the correct chunk from your sample docs with a sensible score ordering.
- ✅ Migrations and indexes are documented and reproducible.
- ✅ Tests cover schema + search logic.

**GitHub artifacts to publish (to show learning)**

- 📌 Migrations + sample docs in `examples/`
- 📌 A `demo.md` showing ingestion + sample queries + outputs

**Learn (good sources for this sprint)**

- pgvector (Postgres vector extension): https://github.com/pgvector/pgvector
- FastAPI: SQL (Relational) Databases (SQLModel example): https://fastapi.tiangolo.com/tutorial/sql-databases/
### Sprint 3 (2026-03-08 → 2026-03-22): RAG baseline: /ask endpoint + citations + minimal UI/CLI

**In simple words:** Build a working Q&A API that answers using your docs and shows citations (sources).

**Time estimate:** ~16.0 hrs total (Week 1 ~8.0 hrs, Week 2 ~8.0 hrs)


**What you’ll do (checklist)**

**Week 1**

- [ ] (~2.0 hrs) Create `/ask` endpoint (request: question; response: answer + citations + chunk_ids).
  - Expected: API returns answer + citation list.
- [ ] (~2.0 hrs) Create prompt template that forces: answer only from retrieved chunks; say 'I don’t know' otherwise.
  - Expected: Prompt file is versioned and documented.
- [ ] (~2.0 hrs) Implement context budgeting: limit tokens/characters from chunks; keep top chunks.
  - Expected: No oversized prompts; stable latency.
- [ ] (~2.0 hrs) Add citation formatting (source, page/section) and include in response.
  - Expected: Citations are human-readable and accurate.

**Week 2**

- [ ] (~2.0 hrs) Optional but strong: reranking step (simple heuristic or model) to improve relevance.
  - Expected: Better retrieval quality on tricky questions.
- [ ] (~2.0 hrs) Build a tiny client: CLI or simple HTML page to ask questions.
  - Expected: A non-engineer can try your demo.
- [ ] (~2.5 hrs) Create 20 sample questions + expected citations in `demo_questions.json`.
  - Expected: You have a repeatable demo set.
- [ ] (~1.5 hrs) Write architecture section in README (diagram + request flow).
  - Expected: Clear explanation for recruiters.

**How to validate you achieved it (Definition of Done)**

- ✅ For 20 sample questions, answers include citations pointing to the right chunk/section.
- ✅ When retrieval is weak, the system refuses or says 'I don't know' instead of hallucinating.
- ✅ You can demo end-to-end in <5 minutes.

**GitHub artifacts to publish (to show learning)**

- 📌 2–3 minute demo video (screen recording) linked in README
- 📌 Architecture diagram + sample Q/A screenshots

**Learn (good sources for this sprint)**

- LangChain: RAG (docs): https://docs.langchain.com/oss/python/langchain/rag
- LlamaIndex: Understanding RAG: https://developers.llamaindex.ai/python/framework/understanding/rag/
### Sprint 4 (2026-03-23 → 2026-04-06): Production API polish: auth + rate limits + caching + streaming

**In simple words:** Make the RAG API feel production-ready: secure, fast, and stable under repeated queries.

**Time estimate:** ~15.5 hrs total (Week 1 ~8.0 hrs, Week 2 ~7.5 hrs)


**What you’ll do (checklist)**

**Week 1**

- [ ] (~2.0 hrs) Add API-key auth (simple) or JWT auth (strong). Document how to use.
  - Expected: Unauthorized calls fail; authorized calls succeed.
- [ ] (~2.0 hrs) Add rate limiting per user (Redis-backed) and return friendly 429 errors.
  - Expected: API is protected from abuse.
- [ ] (~2.5 hrs) Add caching: retrieval cache (query→chunk_ids) and/or answer cache (question→answer).
  - Expected: Repeat questions become much faster.
- [ ] (~1.5 hrs) Add streaming responses (SSE) for `/ask` so UI feels snappy.
  - Expected: Client receives tokens progressively.

**Week 2**

- [ ] (~2.0 hrs) Add structured logging: latency, cache_hit, chunks_used, model name, prompt version.
  - Expected: Logs tell you what happened per request.
- [ ] (~2.5 hrs) Build a load test (Go recommended) and run a baseline benchmark.
  - Expected: You can report p50/p95 latency + RPS.
- [ ] (~2.0 hrs) Add a `perf/` report with charts or tables (before/after caching).
  - Expected: Measurable improvement is visible.
- [ ] (~1.0 hrs) Update README with 'Performance & Limits' section.
  - Expected: Recruiters see production thinking.

**How to validate you achieved it (Definition of Done)**

- ✅ Cache hit reduces latency noticeably for repeat questions.
- ✅ Load test produces stable p95 latency metrics.
- ✅ Logs include enough fields to debug incidents quickly.

**GitHub artifacts to publish (to show learning)**

- 📌 Go load-test tool + sample benchmark output
- 📌 Performance section with p50/p95 + cache hit rate

**Learn (good sources for this sprint)**

- FastAPI (official docs): https://fastapi.tiangolo.com/
- Prometheus: Getting started: https://prometheus.io/docs/prometheus/latest/getting_started/
### Sprint 5 (2026-04-07 → 2026-04-21): Evals: golden dataset + regression testing (major differentiator)

**In simple words:** Measure RAG quality and stop regressions with automated evaluation.

**Time estimate:** ~16.0 hrs total (Week 1 ~8.5 hrs, Week 2 ~7.5 hrs)


**What you’ll do (checklist)**

**Week 1**

- [ ] (~2.0 hrs) Create a golden dataset (50–150 Qs): question, expected citation(s), expected key points.
  - Expected: Dataset file exists and is documented.
- [ ] (~2.0 hrs) Build eval runner: run questions → capture answer + citations + latency + cost.
  - Expected: `make eval` produces a report.
- [ ] (~2.5 hrs) Add scoring: citation accuracy + refusal correctness + basic answer checks.
  - Expected: You get a numeric score per run.
- [ ] (~2.0 hrs) Add 'LLM-as-judge' option + spot-check at least 20 questions manually.
  - Expected: You trust the evals.

**Week 2**

- [ ] (~2.0 hrs) Add CI gate: fail PR if quality drops beyond threshold.
  - Expected: Bad changes are blocked automatically.
- [ ] (~2.0 hrs) Log eval runs to MLflow/W&B (score, latency, version tags).
  - Expected: You can compare runs over time.
- [ ] (~2.0 hrs) Write `EVALS.md`: how to add tests and interpret scores.
  - Expected: Anyone can extend the dataset.
- [ ] (~1.5 hrs) Add a small HTML/Markdown report output (top failures list).
  - Expected: Failures are easy to fix.

**How to validate you achieved it (Definition of Done)**

- ✅ `make eval` produces an understandable score report + top failures list.
- ✅ CI blocks quality regressions with clear failure messages.
- ✅ At least 20 gold answers are human-verified (not just model-judged).

**GitHub artifacts to publish (to show learning)**

- 📌 `EVALS.md` + sample evaluation report
- 📌 Badges/graph screenshots showing improvements over time

**Learn (good sources for this sprint)**

- LangSmith: Evaluate a RAG application: https://docs.langchain.com/langsmith/evaluate-rag-tutorial
- YouTube: LangSmith Evaluations (playlist): https://www.youtube.com/playlist?list=PLfaIDFEXuae0um8Fj0V4dHG37fGFU8Q5S
- MLflow tracking quickstart: https://mlflow.org/docs/latest/ml/tracking/quickstart/
- Weights & Biases quickstart: https://docs.wandb.ai/quickstart
### Sprint 6 (2026-04-22 → 2026-05-06): Observability: traces + metrics + dashboards + runbooks

**In simple words:** Make the service debuggable: you can pinpoint slow retrieval, model latency, cache misses, and errors.

**Time estimate:** ~15.0 hrs total (Week 1 ~7.5 hrs, Week 2 ~7.5 hrs)


**What you’ll do (checklist)**

**Week 1**

- [ ] (~2.0 hrs) Add OpenTelemetry tracing to FastAPI + DB calls + LLM calls (spans).
  - Expected: You can trace one request end-to-end.
- [ ] (~2.0 hrs) Expose Prometheus metrics endpoint (requests, latency, errors, cache hit rate).
  - Expected: Metrics scrape works locally.
- [ ] (~2.0 hrs) Add Grafana dashboard (JSON export) with p95 latency, error rate, cache hit rate.
  - Expected: Dashboard imports cleanly.
- [ ] (~1.5 hrs) Add log enrichment: trace_id in logs for correlation.
  - Expected: You can jump from logs → trace.

**Week 2**

- [ ] (~2.0 hrs) Define basic SLOs: e.g., 99% requests < 2s, error rate < 1%.
  - Expected: SLOs documented in README.
- [ ] (~2.0 hrs) Add alerts (local rules) for latency/error spikes (even if not paging).
  - Expected: Alert rules exist and are testable.
- [ ] (~2.5 hrs) Write runbook with 5 failure scenarios (DB down, vector index slow, model slow, cache down, bad deploy).
  - Expected: Runbook is concrete and actionable.
- [ ] (~1.0 hrs) Record a short 'debug session' demo: show trace + dashboard.
  - Expected: Recruiters see real ops skill.

**How to validate you achieved it (Definition of Done)**

- ✅ You can trace a slow request and identify whether DB, retrieval, or LLM is the bottleneck.
- ✅ Grafana shows p95 latency and cache hit rate correctly.
- ✅ Runbook has at least 5 real incident playbooks.

**GitHub artifacts to publish (to show learning)**

- 📌 Grafana dashboard JSON + screenshots
- 📌 `runbooks/` folder with incident playbooks

**Learn (good sources for this sprint)**

- OpenTelemetry Python instrumentation: https://opentelemetry.io/docs/languages/python/instrumentation/
- OpenTelemetry Python auto-instrumentation example: https://opentelemetry.io/docs/zero-code/python/example/
- Prometheus: Getting started: https://prometheus.io/docs/prometheus/latest/getting_started/
- Grafana + Prometheus: first dashboards: https://grafana.com/docs/grafana/latest/fundamentals/getting-started/first-dashboards/get-started-grafana-prometheus/
### Sprint 7 (2026-05-07 → 2026-05-21): Deploy 1: local Kubernetes (kind/minikube) + Helm/manifests

**In simple words:** Run your app on Kubernetes like real teams do, with probes, configs, and upgrades.

**Time estimate:** ~16.0 hrs total (Week 1 ~8.5 hrs, Week 2 ~7.5 hrs)


**What you’ll do (checklist)**

**Week 1**

- [ ] (~2.0 hrs) Set up local K8s (kind/minikube). Add scripts: `make k8s-up`, `make k8s-down`.
  - Expected: Fresh cluster setup is repeatable.
- [ ] (~2.5 hrs) Write Deployment + Service + Ingress for the API.
  - Expected: Service is reachable via Ingress.
- [ ] (~2.0 hrs) Configure ConfigMaps/Secrets for settings (no secrets in repo).
  - Expected: App loads config securely.
- [ ] (~2.0 hrs) Add readiness/liveness probes + resource requests/limits.
  - Expected: Pods are healthy and restart safely.

**Week 2**

- [ ] (~2.0 hrs) Add Postgres/Redis as K8s services (or helm charts) for local stack.
  - Expected: All components run in cluster.
- [ ] (~2.5 hrs) Optional strong: package into Helm chart with values for dev/prod.
  - Expected: One command installs the app.
- [ ] (~1.5 hrs) Test rolling update and document rollback steps.
  - Expected: You can revert a bad deploy.
- [ ] (~1.5 hrs) Add a K8s deployment doc with diagrams.
  - Expected: Clear story for interviewers.

**How to validate you achieved it (Definition of Done)**

- ✅ From scratch, you can deploy to local K8s and access the API in <20 minutes.
- ✅ Rolling update works and rollback is documented.
- ✅ Probes and resource limits behave correctly under load.

**GitHub artifacts to publish (to show learning)**

- 📌 `k8s/` or `helm/` directory with README and diagrams
- 📌 Release/rollback checklist markdown

**Learn (good sources for this sprint)**

- Kubernetes Deployments: https://kubernetes.io/docs/concepts/workloads/controllers/deployment/
- Kubernetes Services: https://kubernetes.io/docs/concepts/services-networking/service/
- Kubernetes Ingress: https://kubernetes.io/docs/concepts/services-networking/ingress/
- YouTube: Kubernetes (TechWorld with Nana): https://www.youtube.com/watch?v=X48VuDVv0do
### Sprint 8 (2026-05-22 → 2026-06-05): Deploy 2: AWS deploy with Terraform + CI/CD

**In simple words:** Prove you can deploy reliably to cloud using Infrastructure as Code, not manual clicking.

**Time estimate:** ~16.5 hrs total (Week 1 ~9.5 hrs, Week 2 ~7.0 hrs)


**What you’ll do (checklist)**

**Week 1**

- [ ] (~2.0 hrs) Pick deployment target: ECS (faster) or EKS (stronger signal). Write a short decision doc.
  - Expected: You justify your choice.
- [ ] (~3.0 hrs) Terraform: networking basics + compute (ECS/EKS) + IAM roles.
  - Expected: Infra applies successfully.
- [ ] (~2.5 hrs) Terraform: managed Postgres (RDS) and minimal secrets wiring.
  - Expected: DB works and app can connect.
- [ ] (~2.0 hrs) CI/CD: GitHub Actions build → push image → deploy.
  - Expected: Merge to main triggers deploy.

**Week 2**

- [ ] (~2.0 hrs) Environment separation: dev/prod variables + state handling.
  - Expected: Dev and prod are distinct.
- [ ] (~2.0 hrs) Add rollback strategy (tagged releases + redeploy previous).
  - Expected: Rollback is one command.
- [ ] (~1.5 hrs) Add cost notes + teardown guide (`terraform destroy`).
  - Expected: You can safely clean up.
- [ ] (~1.5 hrs) Write 'Production Deployment' section in README with diagram.
  - Expected: Recruiters see cloud maturity.

**How to validate you achieved it (Definition of Done)**

- ✅ You can deploy from CI on a new environment reproducibly.
- ✅ Rollback works and is documented.
- ✅ You have a cost+teardown guide (shows senior thinking).

**GitHub artifacts to publish (to show learning)**

- 📌 `infra/terraform/` with README + diagram
- 📌 Cost & teardown guide

**Learn (good sources for this sprint)**

- Terraform official tutorials: https://developer.hashicorp.com/terraform/tutorials
- YouTube: Terraform (freeCodeCamp): https://www.youtube.com/watch?v=SLB_c_ayRMo
### Sprint 9 (2026-06-06 → 2026-06-20): Security for LLM apps: OWASP + prompt injection + output validation

**In simple words:** Make your AI system safe: prevent data leaks, prompt injection, and unsafe actions.

**Time estimate:** ~15.5 hrs total (Week 1 ~8.0 hrs, Week 2 ~7.5 hrs)


**What you’ll do (checklist)**

**Week 1**

- [ ] (~2.0 hrs) Add PII-safe logging (redact emails/phones/IDs) + verify logs don't leak.
  - Expected: Logs contain redacted values.
- [ ] (~2.0 hrs) Add prompt-injection test cases into golden eval dataset.
  - Expected: Injection cases are evaluated.
- [ ] (~2.0 hrs) Add output validation: for structured outputs, enforce schema with Pydantic.
  - Expected: Bad outputs are rejected.
- [ ] (~2.0 hrs) Add retrieval policy: only allow certain doc sources; deny unknown sources.
  - Expected: No accidental data mixing.

**Week 2**

- [ ] (~2.5 hrs) Add 'safe completion' policy: refuse requests indicating secrets/unsafe actions.
  - Expected: Safer behavior is consistent.
- [ ] (~2.0 hrs) Write a short threat model (assets, threats, mitigations) for your system.
  - Expected: Threat model doc exists.
- [ ] (~1.5 hrs) Add security checklist to PR template.
  - Expected: Security checks are habitual.
- [ ] (~1.5 hrs) Demo: run injection tests and show how system resists.
  - Expected: A convincing security demo.

**How to validate you achieved it (Definition of Done)**

- ✅ Injection test cases consistently fail-safe (refuse or ignore malicious instructions).
- ✅ Logs and responses avoid leaking secrets/PII.
- ✅ Threat model lists at least 10 realistic threats + mitigations.

**GitHub artifacts to publish (to show learning)**

- 📌 `security/THREAT_MODEL.md` + `security/PII_REDACTION.md`
- 📌 Injection test suite + report

**Learn (good sources for this sprint)**

- OWASP Top 10 for LLM Applications: https://owasp.org/www-project-top-10-for-large-language-model-applications/
- OWASP GenAI: LLM Top 10: https://genai.owasp.org/llm-top-10/
### Sprint 10 (2026-06-21 → 2026-07-05): Agents (carefully): tool calling + permissions + human approval

**In simple words:** Build an agent that can use tools, but cannot take dangerous actions without permission.

**Time estimate:** ~15.5 hrs total (Week 1 ~8.5 hrs, Week 2 ~7.0 hrs)


**What you’ll do (checklist)**

**Week 1**

- [ ] (~2.0 hrs) Define 3 tools (safe): search docs, summarize, list sources (read-only).
  - Expected: Tools work and are tested.
- [ ] (~2.5 hrs) Implement tool-calling using LangGraph or similar with strict allowlist.
  - Expected: Agent can call tools reliably.
- [ ] (~2.0 hrs) Add 'human approval' for write actions (even if mocked).
  - Expected: Write actions require approval token.
- [ ] (~2.0 hrs) Add audit log: user_id, tool, inputs, outputs, timestamps.
  - Expected: Audits are searchable.

**Week 2**

- [ ] (~2.0 hrs) Add 20 agent scenarios test suite (correct tool selection, refusal, safe behavior).
  - Expected: Agent behavior is testable.
- [ ] (~2.0 hrs) Add eval metric: tool accuracy (picked right tool?) and success rate.
  - Expected: You can quantify agent reliability.
- [ ] (~1.5 hrs) Document agent safety rules + examples.
  - Expected: Clear and persuasive documentation.
- [ ] (~1.5 hrs) Demo video: show approval flow + audit logs.
  - Expected: Recruiters see 'safe agents' skills.

**How to validate you achieved it (Definition of Done)**

- ✅ Agent cannot perform write actions without approval.
- ✅ Tool calls are logged with trace IDs and user IDs.
- ✅ At least 20 agent scenarios pass consistently in CI.

**GitHub artifacts to publish (to show learning)**

- 📌 `agents/` folder with examples + safety rules
- 📌 Short demo video (approval flow)

**Learn (good sources for this sprint)**

- LangGraph (agents) docs: https://langchain-ai.github.io/langgraph/
### Sprint 11 (2026-07-06 → 2026-07-20): Mini-ML project: training + tracking + serving (credibility boost)

**In simple words:** Show you can do real ML: train a small model, track experiments, and serve predictions.

**Time estimate:** ~17.0 hrs total (Week 1 ~9.0 hrs, Week 2 ~8.0 hrs)


**What you’ll do (checklist)**

**Week 1**

- [ ] (~2.0 hrs) Pick a small task/dataset (classification/NER) and define success metric.
  - Expected: Problem statement + metric exists.
- [ ] (~3.0 hrs) Build baseline model (Transformers or classic) + training script.
  - Expected: Baseline scores recorded.
- [ ] (~2.0 hrs) Add experiment tracking (MLflow or W&B) for runs and metrics.
  - Expected: Runs are logged and comparable.
- [ ] (~2.0 hrs) Add dataset/model versioning (optional strong): DVC.
  - Expected: Reproducibility improved.

**Week 2**

- [ ] (~3.0 hrs) Tune or LoRA fine-tune; compare to baseline; write results.
  - Expected: Improvement shown with numbers.
- [ ] (~2.0 hrs) Serve model behind FastAPI endpoint with schema validation.
  - Expected: API returns predictions reliably.
- [ ] (~1.5 hrs) Add a small client + example payloads.
  - Expected: Easy to demo quickly.
- [ ] (~1.5 hrs) Write `RESULTS.md` with charts, decisions, and next steps.
  - Expected: Readable ML narrative.

**How to validate you achieved it (Definition of Done)**

- ✅ Training is reproducible (same command produces similar results).
- ✅ You have an experiment dashboard screenshot or export.
- ✅ Model endpoint behaves predictably with typed input/output.

**GitHub artifacts to publish (to show learning)**

- 📌 `mini-ml-lab` repo or `training/` directory with scripts + results
- 📌 A clear `RESULTS.md` with baseline vs tuned comparison

**Learn (good sources for this sprint)**

- Hugging Face LLM Course: https://huggingface.co/learn/llm-course/en/chapter1/1
- Full Stack Deep Learning (course): https://fullstackdeeplearning.com/course/
- MLflow tracking quickstart: https://mlflow.org/docs/latest/ml/tracking/quickstart/
- DVC: Get started: https://dvc.org/doc/start
### Sprint 12 (2026-07-21 → 2026-08-04): LLM Serving Lab 1: vLLM endpoint + API wrapper + benchmarks

**In simple words:** Serve an open model like a real service and measure throughput/latency.

**Time estimate:** ~15.5 hrs total (Week 1 ~8.0 hrs, Week 2 ~7.5 hrs)


**What you’ll do (checklist)**

**Week 1**

- [ ] (~2.0 hrs) Set up vLLM locally (choose a small model that runs on your machine).
  - Expected: vLLM server responds to prompts.
- [ ] (~2.0 hrs) Wrap vLLM behind a small API (FastAPI or Go) with input validation.
  - Expected: You have a stable API contract.
- [ ] (~2.0 hrs) Add auth + rate limiting at wrapper layer.
  - Expected: Abuse protection is in place.
- [ ] (~2.0 hrs) Add metrics: tokens/sec, p95 latency, queue depth (even approximate).
  - Expected: Metrics are visible.

**Week 2**

- [ ] (~2.5 hrs) Create benchmark script (concurrency sweep) and record results.
  - Expected: You can report RPS and p95.
- [ ] (~2.0 hrs) Tune batching/caching and compare before/after.
  - Expected: You show measurable improvement.
- [ ] (~1.5 hrs) Write `BENCHMARK.md` with tables and environment details.
  - Expected: Reproducible benchmarks.
- [ ] (~1.5 hrs) Create a clean diagram of serving architecture.
  - Expected: Interview-ready diagram.

**How to validate you achieved it (Definition of Done)**

- ✅ You can serve a model and handle concurrent requests without crashes.
- ✅ You can report throughput + p95 latency from benchmarks.
- ✅ You can explain bottlenecks and improvement steps.

**GitHub artifacts to publish (to show learning)**

- 📌 `llm-serving-lab` repo with setup + benchmark report
- 📌 Before/after comparison table (batching/caching)

**Learn (good sources for this sprint)**

- vLLM docs: https://docs.vllm.ai/
- vLLM GitHub: https://github.com/vllm-project/vllm
### Sprint 13 (2026-08-05 → 2026-08-19): LLM Serving Lab 2: Kubernetes autoscaling + canary + incident drill

**In simple words:** Operate inference like production: scaling, safe deploys, and recovery drills.

**Time estimate:** ~15.0 hrs total (Week 1 ~8.0 hrs, Week 2 ~7.0 hrs)


**What you’ll do (checklist)**

**Week 1**

- [ ] (~2.5 hrs) Deploy vLLM to K8s with resource requests/limits and health checks.
  - Expected: Inference service runs in cluster.
- [ ] (~2.0 hrs) Set up autoscaling (HPA) and define scaling signals (CPU/latency proxy).
  - Expected: Scaling triggers under load.
- [ ] (~2.0 hrs) Add canary deployment approach and document rollback steps.
  - Expected: Safe deploy story exists.
- [ ] (~1.5 hrs) Add dashboards for inference: latency, error rate, saturation.
  - Expected: Dashboards display key signals.

**Week 2**

- [ ] (~2.5 hrs) Run a load test that triggers scaling; record results (screenshots).
  - Expected: Evidence of autoscaling.
- [ ] (~2.0 hrs) Simulate incident (overload or bad config) and execute recovery runbook.
  - Expected: Incident drill completed.
- [ ] (~1.5 hrs) Write a postmortem template + fill it for your incident drill.
  - Expected: Demonstrates ops maturity.
- [ ] (~1.0 hrs) Update README: 'How to run the drill' steps.
  - Expected: Repeatable drill guide.

**How to validate you achieved it (Definition of Done)**

- ✅ Autoscaling triggers and stabilizes latency under load.
- ✅ Canary rollout and rollback are documented and testable.
- ✅ You completed a realistic incident drill and wrote a postmortem.

**GitHub artifacts to publish (to show learning)**

- 📌 `incident_drills/` folder + postmortem
- 📌 Dashboard screenshots showing scaling behavior

**Learn (good sources for this sprint)**

- Kubernetes Deployments: https://kubernetes.io/docs/concepts/workloads/controllers/deployment/
- Prometheus: Getting started: https://prometheus.io/docs/prometheus/latest/getting_started/
### Sprint 14 (2026-08-20 → 2026-09-03): System design + AI design: 10 end-to-end designs + practice

**In simple words:** Create interview-ready system designs (RAG at scale, multi-tenant, eval pipelines, serving) and practice explaining them.

**Time estimate:** ~16.0 hrs total (Week 1 ~6.5 hrs, Week 2 ~9.5 hrs)


**What you’ll do (checklist)**

**Week 1**

- [ ] (~2.0 hrs) Create repo `ai-system-design-notes` with a template for each design (problem, API, data, tradeoffs).
  - Expected: Consistent format across designs.
- [ ] (~3.0 hrs) Write 5 designs (RAG at scale, multi-tenant, caching, eval pipeline, observability).
  - Expected: 5 complete design docs.
- [ ] (~1.5 hrs) Add diagrams (Mermaid or SVG) for each design.
  - Expected: Readable diagrams.

**Week 2**

- [ ] (~3.0 hrs) Write 5 more designs (agents safety, cost control, serving, canary, incident response).
  - Expected: 10 complete design docs.
- [ ] (~2.0 hrs) Record yourself explaining 3 designs (10–15 min each).
  - Expected: You spot gaps and improve.
- [ ] (~2.0 hrs) Do 2 mock interviews with a friend or online peer.
  - Expected: Feedback captured.
- [ ] (~1.5 hrs) Create a 1-page cheat sheet for each design.
  - Expected: Fast revision material.
- [ ] (~1.0 hrs) Write 'failure modes' doc (what breaks and how to fix).
  - Expected: Strong senior signal.

**How to validate you achieved it (Definition of Done)**

- ✅ You can explain each design in 10 minutes with clear tradeoffs.
- ✅ Your diagrams are understandable without talking.
- ✅ Mocks reveal fewer gaps over time (track feedback).

**GitHub artifacts to publish (to show learning)**

- 📌 Public repo with 10 designs + diagrams
- 📌 Cheat sheets + failure modes doc

**Learn (good sources for this sprint)**

- Full Stack Deep Learning (course): https://fullstackdeeplearning.com/course/
- YouTube: Karpathy Zero to Hero (playlist): https://www.youtube.com/playlist?list=PLAqhIrjkxbuWI23v9cThsA9GvCAUhRvKZ
### Sprint 15 (2026-09-04 → 2026-09-18): Portfolio + resume pack: polish, metrics, and storytelling

**In simple words:** Make recruiters understand your impact in 60 seconds: demos, metrics, clean READMEs, and strong bullets.

**Time estimate:** ~14.5 hrs total (Week 1 ~7.5 hrs, Week 2 ~7.0 hrs)


**What you’ll do (checklist)**

**Week 1**

- [ ] (~2.0 hrs) Rewrite README for main repos: problem → solution → architecture → demo → results.
  - Expected: README reads like a product page.
- [ ] (~2.0 hrs) Add 'Results' section with real numbers (quality score, p95 latency, cache hit rate, throughput).
  - Expected: Hard metrics included.
- [ ] (~2.0 hrs) Create GitHub Pages portfolio linking your repos and demos.
  - Expected: One clean landing page.
- [ ] (~1.5 hrs) Draft 8 resume bullets from your repos (impact + metrics).
  - Expected: Bullets ready for resume.

**Week 2**

- [ ] (~2.0 hrs) Write 6 STAR stories (outage, scaling, ambiguity, leadership, conflict, learning).
  - Expected: Behavioral prep ready.
- [ ] (~2.0 hrs) Do 2 mock recruiter screens and refine your pitch.
  - Expected: Pitch becomes crisp.
- [ ] (~1.5 hrs) Create a single 'pinned' summary repo that links everything (journey timeline).
  - Expected: Easy for recruiters to navigate.
- [ ] (~1.5 hrs) Ask 5 people to review (README + resume) and apply fixes.
  - Expected: External quality signal.

**How to validate you achieved it (Definition of Done)**

- ✅ A recruiter can understand your project and metrics within 60 seconds.
- ✅ Your resume bullets are measurable and role-aligned.
- ✅ Your GitHub looks intentional (pinned repos + portfolio page).

**GitHub artifacts to publish (to show learning)**

- 📌 GitHub Pages portfolio
- 📌 Pinned summary repo (timeline + links + top demos)

**Learn (good sources for this sprint)**

- FastAPI (official docs): https://fastapi.tiangolo.com/
- LangSmith: Evaluate a RAG application: https://docs.langchain.com/langsmith/evaluate-rag-tutorial
### Sprint 16 (2026-09-19 → 2026-10-03): Application sprint: targeted outreach + mock loops + iterate

**In simple words:** Convert your work into interviews through targeted applications, referrals, and practice loops.

**Time estimate:** ~16.0 hrs total (Week 1 ~8.0 hrs, Week 2 ~8.0 hrs)


**What you’ll do (checklist)**

**Week 1**

- [ ] (~2.0 hrs) Build target list (30 companies) + role keywords (LLM engineer, AI engineer, ML platform).
  - Expected: Clear list exists.
- [ ] (~2.0 hrs) Apply to 10 roles with tailored bullets and links to demos.
  - Expected: First batch submitted.
- [ ] (~2.0 hrs) Ask for 10 referrals (short message + links to portfolio).
  - Expected: Referral pipeline started.
- [ ] (~2.0 hrs) Do 2 coding mocks (LeetCode-style) focused on what your target roles ask.
  - Expected: Weak areas identified.

**Week 2**

- [ ] (~2.5 hrs) Do 2 system design mocks (one classic + one AI design).
  - Expected: Feedback captured.
- [ ] (~2.0 hrs) Create tracking sheet (applications, responses, next steps, feedback).
  - Expected: You can iterate weekly.
- [ ] (~2.0 hrs) Update portfolio/resume based on feedback.
  - Expected: Iteration cycle established.
- [ ] (~1.5 hrs) Keep shipping small improvements to repos (fresh commits).
  - Expected: Repos look active.

**How to validate you achieved it (Definition of Done)**

- ✅ You have a steady cadence of recruiter screens (or clear feedback on why not).
- ✅ Mock performance improves week-over-week.
- ✅ Portfolio gets stronger and more focused with each iteration.

**GitHub artifacts to publish (to show learning)**

- 📌 Optional private repo: interview prep notes (keep private)
- 📌 Public: small 'What I built in 8 months' post (no employer info)

**Learn (good sources for this sprint)**

- YouTube: Kubernetes (TechWorld with Nana): https://www.youtube.com/watch?v=X48VuDVv0do
- YouTube: Terraform (freeCodeCamp): https://www.youtube.com/watch?v=SLB_c_ayRMo

## Master resource list

- FastAPI (official docs): https://fastapi.tiangolo.com/
- FastAPI Tutorial: First Steps: https://fastapi.tiangolo.com/tutorial/first-steps/
- FastAPI: SQL (Relational) Databases (SQLModel example): https://fastapi.tiangolo.com/tutorial/sql-databases/
- Pydantic v2 docs: https://docs.pydantic.dev/latest/
- pytest: Getting Started: https://docs.pytest.org/en/stable/getting-started.html
- Ruff linter docs: https://docs.astral.sh/ruff/
- pgvector (Postgres vector extension): https://github.com/pgvector/pgvector
- setup-pgvector (GitHub Actions helper): https://github.com/pgvector/setup-pgvector
- LangChain: RAG (docs): https://docs.langchain.com/oss/python/langchain/rag
- LlamaIndex: Understanding RAG: https://developers.llamaindex.ai/python/framework/understanding/rag/
- LangSmith: Evaluate a RAG application: https://docs.langchain.com/langsmith/evaluate-rag-tutorial
- LangGraph (agents) docs: https://langchain-ai.github.io/langgraph/
- OWASP Top 10 for LLM Applications: https://owasp.org/www-project-top-10-for-large-language-model-applications/
- OWASP GenAI: LLM Top 10: https://genai.owasp.org/llm-top-10/
- OpenTelemetry Python instrumentation: https://opentelemetry.io/docs/languages/python/instrumentation/
- OpenTelemetry Python auto-instrumentation example: https://opentelemetry.io/docs/zero-code/python/example/
- Prometheus: Getting started: https://prometheus.io/docs/prometheus/latest/getting_started/
- Grafana + Prometheus: first dashboards: https://grafana.com/docs/grafana/latest/fundamentals/getting-started/first-dashboards/get-started-grafana-prometheus/
- Terraform official tutorials: https://developer.hashicorp.com/terraform/tutorials
- Kubernetes Deployments: https://kubernetes.io/docs/concepts/workloads/controllers/deployment/
- Kubernetes Services: https://kubernetes.io/docs/concepts/services-networking/service/
- Kubernetes Ingress: https://kubernetes.io/docs/concepts/services-networking/ingress/
- Hugging Face LLM Course: https://huggingface.co/learn/llm-course/en/chapter1/1
- Full Stack Deep Learning (course): https://fullstackdeeplearning.com/course/
- YouTube: Karpathy Zero to Hero (playlist): https://www.youtube.com/playlist?list=PLAqhIrjkxbuWI23v9cThsA9GvCAUhRvKZ
- YouTube: LangSmith Evaluations (playlist): https://www.youtube.com/playlist?list=PLfaIDFEXuae0um8Fj0V4dHG37fGFU8Q5S
- YouTube: FastAPI (freeCodeCamp): https://www.youtube.com/watch?v=tLKKmouUams
- YouTube: Kubernetes (TechWorld with Nana): https://www.youtube.com/watch?v=X48VuDVv0do
- YouTube: Terraform (freeCodeCamp): https://www.youtube.com/watch?v=SLB_c_ayRMo
- vLLM docs: https://docs.vllm.ai/
- vLLM GitHub: https://github.com/vllm-project/vllm
- MLflow tracking quickstart: https://mlflow.org/docs/latest/ml/tracking/quickstart/
- Weights & Biases quickstart: https://docs.wandb.ai/quickstart
- DVC: Get started: https://dvc.org/doc/start
- Ray Serve docs: https://docs.ray.io/en/latest/serve/index.html