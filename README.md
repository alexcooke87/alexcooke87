# Alex Cooke

![Docker](https://img.shields.io/badge/Docker-Containerised-blue?logo=docker)
![Linux](https://img.shields.io/badge/Linux-Server-lightgrey?logo=linux)
![Self-Hosted](https://img.shields.io/badge/Self--Hosted-Infrastructure-green)
![GitOps](https://img.shields.io/badge/Git-Deployment-orange?logo=git)
![Private Repos](https://img.shields.io/badge/Repos-Private-important)

🧠 **Infrastructure • Docker • Self-Hosting • Automation**

This GitHub account is used primarily as **private storage and version control** for infrastructure code, with a focus on deploying and managing Docker stacks via Git-based workflows.

Most repositories are **private by design** and are not intended to function as public libraries or tutorials.

---

## 🔧 Primary Use Case

This account supports Git-driven infrastructure workflows, including:

- Docker & Docker Compose stacks
- Self-hosted services and internal tooling
- Reverse proxy and networking configurations
- Configuration-as-code for repeatable deployments
- Disaster recovery and rebuild automation

Typical stack components include:

- Reverse proxies (Nginx Proxy Manager, Traefik)
- Media automation (*arr stack)
- Databases (MariaDB, PostgreSQL)
- Monitoring & automation (Watchtower, Uptime Kuma)
- Network and smart-home–adjacent services

---

## 🐳 Docker Philosophy

- Declarative configuration over manual setup
- Minimal host-level changes
- Environment variables instead of hard-coded values
- Persistent volumes for application state
- Docker service-name networking (internal DNS)

---

## 🔐 Security & Privacy

- Sensitive infrastructure remains private
- Public repositories (if any) are shared **as-is**, without guarantees

---

## 🚀 Deployment Model

Typical deployment workflow:

```text
Git Push → Server Pull → Docker Compose Up
```

- No CI/CD runners
- No cloud build pipelines
- Simple, predictable, auditable deployments

---

## 📍 About

- **Location:** Melbourne, Australia
- **Focus:** Home lab & small-scale production infrastructure
- **Account Role:** Infrastructure state storage and deployment source

---

## 📎 Notes

This profile is not intended for:
- Open-source collaboration
- Public issue tracking
- Community support

If a repository is public, it is intentionally minimal and self-contained.

---

> “If it can’t be rebuilt from Git, it’s not finished.”
