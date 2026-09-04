<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=22&duration=2800&pause=800&color=2BBC8A&center=true&vCenter=true&width=640&lines=building+agentic+AI+systems;that+don't+fall+over+at+3am;LangGraph+%2B+FastAPI+%2B+Postgres;human-in-the-loop%2C+not+human-in-the-way;currently%3A+India+%E2%86%92+open+to+remote" alt="typing animation" />

**[Projects](#-what-im-building-right-now)** · **[Previous work](#-previously-worked-upon)** · **[Sharing Knowledge](#-sharing-knowledge)** · **[Stack](#-stack-i-actually-use)** · **[Education](#-education)** · **[Contact](#-lets-talk)**

</div>

<br/>

## → what I'm building right now

**[Blogging Agent](https://github.com/DEV270201/Blogging-Agent)**: an AI agent that turns a topic into a fully-cited article, built like a product instead of a demo.

```
queries → research (Tavily) → plan + coverage score → [pause if evidence is weak] → parallel write → synthesize
```

- **Doesn't hallucinate confidence.** The planner scores evidence as `sufficient | partial | insufficient` and pauses the graph for a human decision, proceed or re-research, before a single word gets drafted. Bounded at 2 rounds, so it can't loop forever.
- **Doesn't lose work on crash.** Every node checkpoints to Postgres. A heartbeat thread renews a lease per running job; a sweeper reclaims anything whose owner died, safe across multiple instances.
- **Doesn't ship untested.** 162 tests gating merges via GitHub Actions + branch protection. Deploys to ECR through GitHub OIDC, no long-lived AWS keys anywhere in the pipeline.

<br/>

**[Expense Tracker Agent](https://github.com/DEV270201/AI-Agents)**: a local LLM agent, built from scratch, no framework scaffolding.

- **Function-calling loop on a local model.** Runs on Ollama, with system prompts designed to drive the model to select and invoke tools for logging and summarizing expenses, no cloud API in the loop.
- **Remembers you across sessions.** A secondary LLM extracts user preferences at session end and persists them, so the next session's system prompt already knows how you like things done.
- **Structured output over regex.** Replaced regex-based response parsing with prompt-enforced JSON schemas, eliminating an entire class of parsing failures caused by the model phrasing things slightly differently each time.

<br/>

## → previously worked upon

| | |
|---|---|
| **RBAC at scale** | Designed cohort-based access control serving 1,000+ users: schema, backend logic, admin controls, from scratch |
| **Zero-downtime auth fix** | Root-caused a distributed auth bug leaving users with half-created accounts; related support tickets went to zero |
| **RAG under load** | Built a concurrent ingestion pipeline (Node.js, Bedrock) with retries and structured logging, designed to fail loud, not silent |
| **Serverless on a budget** | Lambda + DynamoDB with 3 GSIs purpose-built to kill full table scans |
| **File infra end-to-end** | [EasyFiles](https://github.com/DEV270201/EasyFiles): full-stack app on EC2 behind NGINX, S3 for storage, async deletes via Lambda routed to an SQS dead-letter queue after 3 retries; cut download TTFB 18% by fronting S3 with CloudFront |

<br/>

## → sharing-knowledge

<details>
<summary><b>Docker, from first principles — 5-part series</b></summary>
<br/>

| | |
|---|---|
| [1 · Why Docker](https://www.linkedin.com/posts/dshah99_aws-docker-containers-activity-7217560742093336577-PszQ) | The dependency-hell problem it actually solves: pulling pre-built images instead of installing and configuring every dependency on every machine |
| [2 · Containers vs. VMs](https://www.linkedin.com/posts/dshah99_devops-virtualization-deployment-activity-7221175022130769921-mtKM) | Why containers share the host kernel instead of shipping a full OS, and why that makes them lighter and faster than VMs |
| [3 · Images, networks, volumes](https://www.linkedin.com/posts/dshah99_devops-docker-containerization-activity-7225168288723415040-CFW_) | Image vs. container, bridge vs. host networking, and why anonymous volumes silently lose data on container recreation |
| [4 · The commands you actually use](https://www.linkedin.com/posts/dshah99_devops-docker-containerization-activity-7229167600096727042-cnBT) | `ps` / `pull` / `push` / `run` / `exec` / `build`, including pulling from a private registry like AWS ECR, not just Docker Hub |
| [5 · Docker Compose](https://www.linkedin.com/posts/dshah99_devops-docker-containerization-activity-7234581738666999808-3Kjt) | Replacing "start 10 containers by hand" with one YAML file and `docker compose up` |

</details>

<details>
<summary><b>Jenkins + Docker: building and breaking a real pipeline</b></summary>
<br/>

| | |
|---|---|
| [1 · Why Docker agents over plugin sprawl](https://www.linkedin.com/posts/dshah99_jenkins-docker-devops-activity-7415085843960508416-fGSI) | Letting Jenkins orchestrate through plugins while Docker handles build execution in disposable containers: no more Node/Python/Go version conflicts on the controller |
| [2 · Four errors deep in the Jenkins–Docker handshake](https://www.linkedin.com/posts/dshah99_jenkins-docker-cicd-activity-7417618472077283329-QMD6) | `docker: not found` (missing CLI in the Jenkins image), permission denied on `docker.sock` (group membership), API version mismatch (host/CLI version skew), files "disappearing" (fixed with `reuseNode true` for workspace mounting) |
| [3 · Full CI/CD pipeline, GitHub push to running container](https://www.linkedin.com/posts/dshah99_jenkins-docker-cicd-activity-7420482372237844480-Hj6t) | Webhook triggers a build in a disposable AWS CLI container, pushes to ECR, then SSHs into EC2 to swap the container. Multi-stage builds to shrink image size, an NGINX `try_files` fix for React routing 404s, heredocs to fix commands silently running on the wrong host. Manual 3-5 min deploy cut to under 1 minute, automated |

</details>

<details>
<summary><b>Bash scripting for automation</b></summary>
<br/>

| | |
|---|---|
| [Learning Bash by writing real scripts](https://www.linkedin.com/posts/dshah99_bashscripting-linux-devops-activity-7410452417118441472-d2MB) | Wrote scripts from scratch: a Postgres container lifecycle manager, a CloudFront TTFB benchmarking tool, a disk/memory monitor, and a safe file-migration script, while working through stdout/stderr redirection and multi-line file handling |

</details>

<br/>

## → stack I actually use

**languages / core**
<p>
<img src="https://img.shields.io/badge/Python-3670A0?style=flat-square&logo=python&logoColor=ffdd54" />
<img src="https://img.shields.io/badge/TypeScript-007ACC?style=flat-square&logo=typescript&logoColor=white" />
<img src="https://img.shields.io/badge/JavaScript-323330?style=flat-square&logo=javascript&logoColor=F7DF1E" />
<img src="https://img.shields.io/badge/C++-00599C?style=flat-square&logo=c%2B%2B&logoColor=white" />
<img src="https://img.shields.io/badge/SQL-4479A1?style=flat-square&logo=postgresql&logoColor=white" />
</p>

**backend / frontend**
<p>
<img src="https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white" />
<img src="https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white" />
<img src="https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB" />
<img src="https://img.shields.io/badge/NGINX-009639?style=flat-square&logo=nginx&logoColor=white" />
</p>

**AI / agents**
<p>
<img src="https://img.shields.io/badge/LangGraph-1C1C1C?style=flat-square&logo=langchain&logoColor=white" />
<img src="https://img.shields.io/badge/LangChain-1C3C3C?style=flat-square&logo=langchain&logoColor=white" />
<img src="https://img.shields.io/badge/AWS_Bedrock-FF9900?style=flat-square&logo=amazonaws&logoColor=white" />
<img src="https://img.shields.io/badge/Ollama-000000?style=flat-square&logo=ollama&logoColor=white" />
<img src="https://img.shields.io/badge/Vector_DBs-6E56CF?style=flat-square" />
</p>

**databases**
<p>
<img src="https://img.shields.io/badge/PostgreSQL-316192?style=flat-square&logo=postgresql&logoColor=white" />
<img src="https://img.shields.io/badge/MongoDB-4EA94B?style=flat-square&logo=mongodb&logoColor=white" />
<img src="https://img.shields.io/badge/DynamoDB-4053D6?style=flat-square&logo=amazondynamodb&logoColor=white" />
<img src="https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white" />
</p>

**cloud / infra**
<p>
<img src="https://img.shields.io/badge/AWS_Lambda-FF9900?style=flat-square&logo=awslambda&logoColor=white" />
<img src="https://img.shields.io/badge/AWS_EC2-FF9900?style=flat-square&logo=amazonec2&logoColor=white" />
<img src="https://img.shields.io/badge/AWS_S3-569A31?style=flat-square&logo=amazons3&logoColor=white" />
<img src="https://img.shields.io/badge/AWS_ECR-FF9900?style=flat-square&logo=amazonaws&logoColor=white" />
<img src="https://img.shields.io/badge/AWS_VPC-FF9900?style=flat-square&logo=amazonaws&logoColor=white" />
<img src="https://img.shields.io/badge/AWS_API_Gateway-FF9900?style=flat-square&logo=amazonapigateway&logoColor=white" />
<img src="https://img.shields.io/badge/AWS_IAM-DD344C?style=flat-square&logo=amazonaws&logoColor=white" />
<img src="https://img.shields.io/badge/AWS_Route_53-8C4FFF?style=flat-square&logo=amazonroute53&logoColor=white" />
</p>
<p>
<img src="https://img.shields.io/badge/Docker-0DB7ED?style=flat-square&logo=docker&logoColor=white" />
<img src="https://img.shields.io/badge/GitHub_Actions-2671E5?style=flat-square&logo=githubactions&logoColor=white" />
<img src="https://img.shields.io/badge/Jenkins-D24939?style=flat-square&logo=jenkins&logoColor=white" />
<img src="https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black" />
</p>

**day-to-day tools**
<p>
<img src="https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white" />
<img src="https://img.shields.io/badge/Claude_Code-D97757?style=flat-square&logo=anthropic&logoColor=white" />
<img src="https://img.shields.io/badge/GitHub_Copilot-000000?style=flat-square&logo=githubcopilot&logoColor=white" />
</p>

<sub>currently deepening: distributed job orchestration, LLM-as-judge evaluation loops, infra-as-code</sub>

<br/>

## → education

| | | |
|---|---|---|
| **M.S. Computer Science** | Stevens Institute of Technology, United States | Aug 2023 - May 2025 |
| **B.Tech. Computer Science** | KJ Somaiya College of Engineering, Mumbai University | Aug 2019 - May 2023 |

<br/>

## → let's talk

<div align="center">

**[LinkedIn](https://www.linkedin.com/in/dshah99/)** · **[Mail](mailto:devanshshah649@gmail.com)** · **[Blogging Agent](https://github.com/DEV270201/Blogging-Agent)**

<sub>if it's in a repo, it has tests. if it's in prod, it has a rollback plan</sub>

</div>
