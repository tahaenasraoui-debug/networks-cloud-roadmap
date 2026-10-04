# Computer Networks & Cloud Computing Roadmap

![License](https://img.shields.io/badge/license-MIT-green.svg) ![focus](https://img.shields.io/badge/focus-networks%20%2B%20cloud-blue.svg) ![tooling](https://img.shields.io/badge/tooling-docker%20%7C%20k8s%20%7C%20terraform-informational.svg)

From packets to production: how networks work, then how to deploy, scale, and operate applications on the cloud with infrastructure as code.

## Table of Contents

1. [Workflow Overview](#workflow-overview)
2. [Prerequisites](#prerequisites)
3. [Phase 1: Networking Fundamentals](#phase-1-networking-fundamentals)
4. [Phase 2: Network Programming](#phase-2-network-programming)
5. [Phase 3: Linux & Containers](#phase-3-linux--containers)
6. [Phase 4: Cloud & Infrastructure as Code](#phase-4-cloud--infrastructure-as-code)
7. [Phase 5: Reliability & Observability](#phase-5-reliability--observability)
8. [Capstone Projects](#capstone-projects)
9. [Repository Layout](#repository-layout)
10. [Engineering Rules](#engineering-rules)
11. [Exit Criteria](#exit-criteria)

---

## Workflow Overview

```
 Packets / TCP-IP --> Sockets + HTTP --> Linux + containers --> Kubernetes
                                                                    |
 Observability  <-- CI/CD <-- Infrastructure as code <-- Cloud services
 (Prometheus)      (Actions)   (Terraform)               (compute, storage, IAM)
```

## Prerequisites

- [ ] Comfortable in Linux
- [ ] Python or another scripting language
- [ ] Basic idea of client-server and HTTP

## Phase 1: Networking Fundamentals

Goal: Understand every layer between a browser and a server.

| Resource | Type | Why |
|----------|------|-----|
| [Computer Networking: A Top-Down Approach](https://gaia.cs.umass.edu/kurose_ross/index.php) | Textbook site | Standard networking text, with companion materials |
| [Kurose & Ross Wireshark Labs](https://gaia.cs.umass.edu/kurose_ross/wireshark.php) | Labs | See protocols as real packets |
| [Cloudflare Learning Center](https://www.cloudflare.com/learning/) | Articles | Short explainers on DNS, TLS, CDN, DDoS |
| [Julia Evans' Wizard Zines](https://wizardzines.com/) | Zines | Visual summaries of DNS, HTTP, and networking tools |

- [ ] Application layer: HTTP, DNS, email
- [ ] Transport layer: TCP handshake, congestion control, UDP
- [ ] Network layer: IP addressing, subnetting, routing
- [ ] Link layer: Ethernet, ARP, Wi-Fi
- [ ] Capture and annotate a full page load in Wireshark

**Deliverables**
- [ ] `labs/wireshark/` annotated captures
- [ ] `docs/subnetting_drills.md` with 30 worked problems

## Phase 2: Network Programming

Goal: Build the protocols yourself.

| Resource | Type | Why |
|----------|------|-----|
| [Beej's Guide to Network Programming](https://beej.us/guide/bgnet/) | Free book | Sockets in C |
| [High Performance Browser Networking](https://hpbn.co/) | Free book | TCP, TLS, HTTP/2, and latency in practice |
| [Cisco Networking Academy](https://www.netacad.com/) | Courses and Packet Tracer | Simulate routers and switches |

- [ ] Build a TCP echo server, then a multi-client chat server
- [ ] Build an HTTP/1.1 server from raw sockets
- [ ] Write a DNS resolver that queries root servers
- [ ] Simulate a two-subnet network with routing in Packet Tracer

**Deliverables**
- [ ] `src/netlab/` with all servers, typed or tested
- [ ] Benchmark report in `docs/http_server_bench.md`

## Phase 3: Linux & Containers

Goal: Package and run software reproducibly.

| Resource | Type | Why |
|----------|------|-----|
| [Docker Get Started](https://docs.docker.com/get-started/) | Docs | Images, containers, Compose |
| [Kubernetes Tutorials](https://kubernetes.io/docs/tutorials/) | Docs | Official hands-on path |
| [kind](https://kind.sigs.k8s.io/) | Tool | Local multi-node Kubernetes clusters |
| [Kubernetes the Hard Way](https://github.com/kelseyhightower/kubernetes-the-hard-way) | Repo | Learn the control plane by building it |

- [ ] Containerize an app with a multi-stage Dockerfile
- [ ] Compose a web app, database, and reverse proxy
- [ ] Kubernetes: Pods, Deployments, Services, Ingress, ConfigMaps
- [ ] Kubernetes: rolling updates and rollbacks

**Deliverables**
- [ ] `deploy/docker/` and `deploy/k8s/` manifests
- [ ] App running on a local `kind` cluster with a rolling update documented

## Phase 4: Cloud & Infrastructure as Code

Goal: Provision and secure real cloud infrastructure repeatably.

| Resource | Type | Why |
|----------|------|-----|
| [AWS Skill Builder](https://skillbuilder.aws/) | Free tier of training | Core services and fundamentals |
| [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/) | Framework | Design principles that apply across clouds |
| [Oracle Cloud Free Tier](https://www.oracle.com/cloud/free/) | Free-tier cloud | Always-free alternative for practice |
| [Terraform Tutorials](https://developer.hashicorp.com/terraform/tutorials) | Docs | Infrastructure as code |
| [GitHub Actions Documentation](https://docs.github.com/en/actions) | Docs | CI/CD pipelines |

- [ ] IAM: users, roles, least privilege
- [ ] Compute, object storage, managed database, VPC and security groups
- [ ] Define all infrastructure in Terraform and destroy it cleanly
- [ ] CI pipeline that tests, builds an image, and deploys

**Deliverables**
- [ ] `infra/terraform/` provisioning a 3-tier app
- [ ] `.github/workflows/` pipeline with deploy on merge
- [ ] Cost note in `docs/cost.md` showing monthly spend

## Phase 5: Reliability & Observability

Goal: Know when production is unhealthy and why.

| Resource | Type | Why |
|----------|------|-----|
| [Google SRE Books](https://sre.google/books/) | Free books | SLOs, incident response, postmortems |
| [Prometheus Documentation](https://prometheus.io/docs/introduction/overview/) | Docs | Metrics collection and alerting |
| [Grafana Getting Started](https://grafana.com/docs/grafana/latest/getting-started/) | Docs | Dashboards |
| [WireGuard Quickstart](https://www.wireguard.com/quickstart/) | Docs | Build a private VPN between your lab and the cloud |

- [ ] Define SLOs for your app and alert on them
- [ ] Run a load test and find the first bottleneck
- [ ] Write a blameless postmortem for a failure you cause deliberately
- [ ] Connect home lab and cloud VPC over WireGuard

**Deliverables**
- [ ] `ops/dashboards/` and alert rules
- [ ] `docs/postmortem.md`

## Capstone Projects

- [ ] Deploy a 3-tier app (frontend, API, database) to the cloud entirely from Terraform and CI/CD
- [ ] Run the same app on a `kind` cluster with ingress, autoscaling, and rolling updates
- [ ] Add Prometheus and Grafana with two SLO-based alerts
- [ ] Write a networking report: trace one request from DNS lookup to database query with captures at each hop

## Repository Layout

```
networks-cloud/
├── README.md
├── src/netlab/               # sockets, HTTP server, DNS resolver
├── labs/
│   ├── wireshark/
│   └── packet_tracer/
├── deploy/
│   ├── docker/
│   └── k8s/
├── infra/
│   └── terraform/
├── ops/
│   └── dashboards/
├── .github/workflows/
├── tests/
└── docs/
    ├── subnetting_drills.md
    ├── cost.md
    └── postmortem.md
```

## Engineering Rules

These are strict. A phase is not complete until its deliverables follow all of them.

### 1. Daily 1:3 Theory-to-Building Ratio

- [ ] For every 1 hour of reading or watching, spend 3 hours building, solving, or running labs
- [ ] Log hours in `docs/log.md` at the end of each session
- [ ] No new chapter until the previous one has working code or a written lab report

### 2. Git Branch Hygiene

- [ ] `main` is always green and never receives direct commits
- [ ] One branch per deliverable: `phase-N/short-description`
- [ ] Small commits with imperative messages; squash-merge via PR after checks pass
- [ ] Delete branches after merge

### 3. Quality Gates

- [ ] `terraform fmt -check` and `terraform validate` pass; [tflint](https://github.com/terraform-linters/tflint) is clean
- [ ] [hadolint](https://github.com/hadolint/hadolint) passes on every Dockerfile
- [ ] `pytest` and `mypy --strict` pass on code in `src/`

### 4. Branch-Specific Rules

- [ ] Set a billing alarm and budget before creating any cloud resource
- [ ] Destroy cloud resources after each lab (`terraform destroy`) unless the project needs them running
- [ ] Never commit cloud credentials or Terraform state; use environment variables and a remote backend
- [ ] Everything reproducible: no manual console clicks that are not captured in code

## Exit Criteria

- [ ] Subnet a network on paper and explain how a packet is routed across it
- [ ] Build and deploy an app from nothing using only code and a pipeline
- [ ] Debug a failing Kubernetes deployment using logs, events, and describe output
- [ ] Explain your app's SLOs and what happens when they are breached
