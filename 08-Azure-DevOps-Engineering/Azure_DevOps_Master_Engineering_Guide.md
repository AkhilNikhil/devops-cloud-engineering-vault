# 🔷 Azure DevOps & Observability: The Definitive Master Engineering Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers Azure Boards Agile Governance, Repos Branch Policies, Multi-Stage YAML Pipelines, Self-Hosted Linux Agent Pools, Real Production Projects, Apache Reverse Proxy, and the LGTM Observability Stack.

---

## 📑 Table of Contents
- [Azure DevOps Platform Overview & 5 Core Services](#platform-overview)
- [Azure Boards: Agile Sprints, Epics, Features, User Stories](#azure-boards)
- [Azure Repos: Branch Policies & Pull Request Governance](#azure-repos)
- [Azure Pipelines: Multi-Stage Production YAML Blueprint](#azure-pipelines)
- [Self-Hosted Linux Agent Pool Setup & systemd Automation](#self-hosted-agents)
- [Apache Reverse Proxy & SSL Let's Encrypt Configuration](#apache-reverse-proxy)
- [The LGTM Enterprise Observability Stack (Loki, Grafana, Tempo, Mimir)](#lgtm-stack)
- [Production Troubleshooting Playbook & Senior Interview Q&A](#troubleshooting--qa)

---

➔S➔E➔C➔T➔I➔O➔N➔ ➔8➔:➔ ➔A➔Z➔U➔R➔E➔ ➔D➔E➔V➔O➔P➔S➔ ➔—➔ ➔C➔O➔M➔P➔L➔E➔T➔E➔ ➔G➔U➔I➔D➔E➔
➔B➔a➔s➔e➔d➔ ➔o➔n➔ ➔y➔o➔u➔r➔ ➔a➔c➔t➔u➔a➔l➔ ➔p➔r➔o➔j➔e➔c➔t➔ ➔e➔x➔p➔e➔r➔i➔e➔n➔c➔e➔ ➔+➔ ➔c➔o➔m➔p➔l➔e➔t➔e➔ ➔t➔h➔e➔o➔r➔y➔ ➔f➔o➔r➔ ➔i➔n➔t➔e➔r➔v➔i➔e➔w➔s➔
➔1➔.➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔D➔e➔v➔O➔p➔s➔?➔
➔D➔e➔f➔i➔n➔i➔t➔i➔o➔n➔:➔
➔
➔
➔
➔
➔D➔e➔v➔O➔p➔s➔ ➔i➔s➔ ➔a➔ ➔c➔u➔l➔t➔u➔r➔e➔ ➔+➔ ➔s➔e➔t➔ ➔o➔f➔ ➔p➔r➔a➔c➔t➔i➔c➔e➔s➔ ➔t➔h➔a➔t➔ ➔u➔n➔i➔t➔e➔s➔ ➔D➔e➔v➔e➔l➔o➔p➔m➔e➔n➔t➔ ➔(➔D➔e➔v➔)➔ ➔a➔n➔d➔ ➔O➔p➔e➔r➔a➔t➔i➔o➔n➔s➔ ➔(➔O➔p➔s➔)➔ ➔t➔o➔ ➔d➔e➔l➔i➔v➔e➔r➔ ➔s➔o➔f➔t➔w➔a➔r➔e➔
➔f➔a➔s➔t➔e➔r➔,➔ ➔m➔o➔r➔e➔ ➔r➔e➔l➔i➔a➔b➔l➔y➔,➔ ➔a➔n➔d➔ ➔w➔i➔t➔h➔ ➔h➔i➔g➔h➔e➔r➔ ➔q➔u➔a➔l➔i➔t➔y➔.➔
➔B➔e➔f➔o➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔:➔
➔D➔e➔v➔ ➔t➔e➔a➔m➔ ➔w➔r➔o➔t➔e➔ ➔c➔o➔d➔e➔ ➔→➔ ➔t➔h➔r➔e➔w➔ ➔i➔t➔ ➔o➔v➔e➔r➔ ➔t➔h➔e➔ ➔w➔a➔l➔l➔ ➔t➔o➔ ➔O➔p➔s➔
➔O➔p➔s➔ ➔h➔a➔d➔ ➔t➔o➔ ➔f➔i➔g➔u➔r➔e➔ ➔o➔u➔t➔ ➔h➔o➔w➔ ➔t➔o➔ ➔d➔e➔p➔l➔o➔y➔ ➔i➔t➔
➔S➔l➔o➔w➔ ➔r➔e➔l➔e➔a➔s➔e➔s➔,➔ ➔b➔l➔a➔m➔e➔ ➔c➔u➔l➔t➔u➔r➔e➔,➔ ➔o➔u➔t➔a➔g➔e➔s➔
➔T➔h➔r➔e➔e➔ ➔w➔o➔r➔d➔s➔ ➔s➔u➔m➔m➔a➔r➔i➔z➔e➔ ➔D➔e➔v➔O➔p➔s➔:➔ ➔C➔o➔l➔l➔a➔b➔o➔r➔a➔t➔e➔.➔ ➔A➔u➔t➔o➔m➔a➔t➔e➔.➔ ➔D➔e➔l➔i➔v➔e➔r➔.➔
➔N➔o➔t➔e➔:➔ ➔D➔e➔v➔O➔p➔s➔ ➔i➔s➔ ➔N➔O➔T➔ ➔j➔u➔s➔t➔ ➔a➔ ➔t➔o➔o➔l➔.➔ ➔I➔t➔ ➔i➔s➔ ➔a➔ ➔m➔i➔n➔d➔s➔e➔t➔ ➔f➔i➔r➔s➔t➔,➔ ➔t➔o➔o➔l➔s➔ ➔s➔e➔c➔o➔n➔d➔.➔
➔D➔e➔v➔O➔p➔s➔ ➔L➔i➔f➔e➔c➔y➔c➔l➔e➔ ➔(➔8➔ ➔S➔t➔a➔g➔e➔s➔)➔:➔
➔P➔l➔a➔n➔ ➔→➔ ➔C➔o➔d➔e➔ ➔→➔ ➔B➔u➔i➔l➔d➔ ➔→➔ ➔T➔e➔s➔t➔ ➔→➔ ➔R➔e➔l➔e➔a➔s➔e➔ ➔→➔ ➔D➔e➔p➔l➔o➔y➔ ➔→➔ ➔O➔p➔e➔r➔a➔t➔e➔ ➔→➔ ➔M➔o➔n➔i➔t➔o➔r➔
➔ ➔ ➔↑➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔ ➔F➔e➔e➔d➔b➔a➔c➔k➔ ➔L➔o➔o➔p➔ ➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔
➔S➔t➔a➔g➔e➔ ➔W➔h➔a➔t➔ ➔h➔a➔p➔p➔e➔n➔s➔
➔P➔l➔a➔n➔ ➔D➔e➔f➔i➔n➔e➔ ➔f➔e➔a➔t➔u➔r➔e➔s➔,➔ ➔u➔s➔e➔r➔ ➔s➔t➔o➔r➔i➔e➔s➔,➔ ➔s➔p➔r➔i➔n➔t➔s➔
➔C➔o➔d➔e➔ ➔W➔r➔i➔t➔e➔ ➔c➔o➔d➔e➔,➔ ➔c➔o➔m➔m➔i➔t➔ ➔t➔o➔ ➔G➔i➔t➔
➔B➔u➔i➔l➔d➔ ➔C➔o➔m➔p➔i➔l➔e➔ ➔c➔o➔d➔e➔,➔ ➔r➔u➔n➔ ➔a➔u➔t➔o➔m➔a➔t➔e➔d➔ ➔b➔u➔i➔l➔d➔s➔ ➔(➔C➔I➔)➔
➔T➔e➔s➔t➔ ➔R➔u➔n➔ ➔a➔u➔t➔o➔m➔a➔t➔e➔d➔ ➔u➔n➔i➔t➔/➔i➔n➔t➔e➔g➔r➔a➔t➔i➔o➔n➔ ➔t➔e➔s➔t➔s➔
➔R➔e➔l➔e➔a➔s➔e➔ ➔P➔a➔c➔k➔a➔g➔e➔ ➔b➔u➔i➔l➔d➔ ➔a➔r➔t➔i➔f➔a➔c➔t➔ ➔f➔o➔r➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔
➔D➔e➔p➔l➔o➔y➔ ➔P➔u➔s➔h➔ ➔t➔o➔ ➔d➔e➔v➔/➔s➔t➔a➔g➔i➔n➔g➔/➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔(➔C➔D➔)➔
➔O➔p➔e➔r➔a➔t➔e➔ ➔M➔o➔n➔i➔t➔o➔r➔ ➔r➔u➔n➔n➔i➔n➔g➔ ➔a➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔
➔M➔o➔n➔i➔t➔o➔r➔ ➔C➔o➔l➔l➔e➔c➔t➔ ➔m➔e➔t➔r➔i➔c➔s➔,➔ ➔l➔o➔g➔s➔,➔ ➔a➔l➔e➔r➔t➔s➔ ➔—➔ ➔f➔e➔e➔d➔ ➔b➔a➔c➔k➔ ➔i➔n➔t➔o➔ ➔p➔l➔a➔n➔n➔i➔n➔g➔
➔2➔.➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔?➔
➔D➔e➔f➔i➔n➔i➔t➔i➔o➔n➔:➔
➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔ ➔i➔s➔ ➔M➔i➔c➔r➔o➔s➔o➔f➔t➔'➔s➔ ➔c➔l➔o➔u➔d➔ ➔p➔l➔a➔t➔f➔o➔r➔m➔ ➔t➔h➔a➔t➔ ➔p➔r➔o➔v➔i➔d➔e➔s➔ ➔A➔L➔L➔ ➔t➔o➔o➔l➔s➔ ➔n➔e➔e➔d➔e➔d➔ ➔t➔o➔ ➔p➔r➔a➔c➔t➔i➔c➔e➔ ➔D➔e➔v➔O➔p➔s➔ ➔i➔n➔ ➔o➔n➔e➔ ➔p➔l➔a➔c➔e➔.➔
➔A➔v➔a➔i➔l➔a➔b➔l➔e➔ ➔a➔t➔ ➔d➔e➔v➔.➔a➔z➔u➔r➔e➔.➔c➔o➔m➔
➔
➔
➔
➔
➔5➔ ➔S➔e➔r➔v➔i➔c➔e➔s➔ ➔o➔f➔ ➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔:➔
➔S➔e➔r➔v➔i➔c➔e➔ ➔P➔u➔r➔p➔o➔s➔e➔
➔A➔z➔u➔r➔e➔ ➔B➔o➔a➔r➔d➔s➔ ➔P➔l➔a➔n➔ ➔w➔o➔r➔k➔ ➔—➔ ➔t➔a➔s➔k➔s➔,➔ ➔b➔u➔g➔s➔,➔ ➔s➔p➔r➔i➔n➔t➔s➔,➔ ➔K➔a➔n➔b➔a➔n➔ ➔b➔o➔a➔r➔d➔s➔
➔A➔z➔u➔r➔e➔ ➔R➔e➔p➔o➔s➔ ➔S➔t➔o➔r➔e➔ ➔a➔n➔d➔ ➔m➔a➔n➔a➔g➔e➔ ➔c➔o➔d➔e➔ ➔u➔s➔i➔n➔g➔ ➔G➔i➔t➔
➔A➔z➔u➔r➔e➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔s➔ ➔B➔u➔i➔l➔d➔ ➔a➔n➔d➔ ➔d➔e➔p➔l➔o➔y➔ ➔a➔u➔t➔o➔m➔a➔t➔i➔c➔a➔l➔l➔y➔ ➔(➔C➔I➔/➔C➔D➔)➔
➔A➔z➔u➔r➔e➔ ➔T➔e➔s➔t➔ ➔P➔l➔a➔n➔s➔ ➔M➔a➔n➔u➔a➔l➔ ➔a➔n➔d➔ ➔a➔u➔t➔o➔m➔a➔t➔e➔d➔ ➔t➔e➔s➔t➔i➔n➔g➔ ➔m➔a➔n➔a➔g➔e➔m➔e➔n➔t➔
➔A➔z➔u➔r➔e➔ ➔A➔r➔t➔i➔f➔a➔c➔t➔s➔ ➔S➔t➔o➔r➔e➔ ➔a➔n➔d➔ ➔s➔h➔a➔r➔e➔ ➔c➔o➔d➔e➔ ➔p➔a➔c➔k➔a➔g➔e➔s➔ ➔(➔N➔u➔G➔e➔t➔,➔ ➔n➔p➔m➔,➔ ➔e➔t➔c➔.➔)➔
➔K➔e➔y➔ ➔T➔e➔r➔m➔s➔:➔
➔T➔e➔r➔m➔ ➔M➔e➔a➔n➔i➔n➔g➔
➔C➔I➔ ➔A➔u➔t➔o➔m➔a➔t➔i➔c➔a➔l➔l➔y➔ ➔b➔u➔i➔l➔d➔ ➔a➔n➔d➔ ➔t➔e➔s➔t➔ ➔c➔o➔d➔e➔ ➔e➔v➔e➔r➔y➔ ➔p➔u➔s➔h➔
➔C➔D➔ ➔A➔u➔t➔o➔m➔a➔t➔i➔c➔a➔l➔l➔y➔ ➔d➔e➔l➔i➔v➔e➔r➔ ➔t➔e➔s➔t➔e➔d➔ ➔b➔u➔i➔l➔d➔ ➔t➔o➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔
➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔S➔e➔r➔i➔e➔s➔ ➔o➔f➔ ➔a➔u➔t➔o➔m➔a➔t➔e➔d➔ ➔s➔t➔e➔p➔s➔ ➔t➔o➔ ➔b➔u➔i➔l➔d➔/➔t➔e➔s➔t➔/➔d➔e➔p➔l➔o➔y➔
➔R➔e➔p➔o➔s➔i➔t➔o➔r➔y➔ ➔F➔o➔l➔d➔e➔r➔ ➔s➔t➔o➔r➔i➔n➔g➔ ➔a➔l➔l➔ ➔c➔o➔d➔e➔ ➔w➔i➔t➔h➔ ➔v➔e➔r➔s➔i➔o➔n➔ ➔h➔i➔s➔t➔o➔r➔y➔
➔S➔p➔r➔i➔n➔t➔ ➔F➔i➔x➔e➔d➔ ➔t➔i➔m➔e➔ ➔p➔e➔r➔i➔o➔d➔ ➔(➔2➔ ➔w➔e➔e➔k➔s➔)➔ ➔t➔o➔ ➔c➔o➔m➔p➔l➔e➔t➔e➔ ➔p➔l➔a➔n➔n➔e➔d➔ ➔w➔o➔r➔k➔
➔B➔u➔i➔l➔d➔ ➔A➔g➔e➔n➔t➔ ➔M➔a➔c➔h➔i➔n➔e➔ ➔t➔h➔a➔t➔ ➔r➔u➔n➔s➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔s➔t➔e➔p➔s➔
➔A➔r➔t➔i➔f➔a➔c➔t➔ ➔O➔u➔t➔p➔u➔t➔ ➔o➔f➔ ➔a➔ ➔b➔u➔i➔l➔d➔ ➔(➔z➔i➔p➔,➔ ➔j➔a➔r➔,➔ ➔D➔o➔c➔k➔e➔r➔ ➔i➔m➔a➔g➔e➔)➔
➔E➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔t➔a➔r➔g➔e➔t➔:➔ ➔D➔e➔v➔,➔ ➔S➔t➔a➔g➔i➔n➔g➔,➔ ➔P➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔3➔.➔ ➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔ ➔S➔t➔r➔u➔c➔t➔u➔r➔e➔
➔O➔r➔g➔a➔n➔i➔z➔a➔t➔i➔o➔n➔ ➔(➔d➔e➔v➔.➔a➔z➔u➔r➔e➔.➔c➔o➔m➔/➔Y➔o➔u➔r➔O➔r➔g➔)➔
➔ ➔ ➔ ➔ ➔↓➔
➔P➔r➔o➔j➔e➔c➔t➔ ➔(➔W➔e➔b➔A➔p➔p➔,➔ ➔M➔o➔b➔i➔l➔e➔A➔p➔p➔,➔ ➔I➔n➔f➔r➔a➔P➔r➔o➔j➔e➔c➔t➔)➔
➔ ➔ ➔ ➔ ➔↓➔
➔S➔e➔r➔v➔i➔c➔e➔s➔ ➔(➔B➔o➔a➔r➔d➔s➔,➔ ➔R➔e➔p➔o➔s➔,➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔s➔,➔ ➔A➔r➔t➔i➔f➔a➔c➔t➔s➔,➔ ➔T➔e➔s➔t➔ ➔P➔l➔a➔n➔s➔)➔
➔A➔c➔c➔e➔s➔s➔ ➔L➔e➔v➔e➔l➔s➔:➔
➔
➔
➔
➔
➔L➔e➔v➔e➔l➔ ➔A➔c➔c➔e➔s➔s➔
➔S➔t➔a➔k➔e➔h➔o➔l➔d➔e➔r➔ ➔(➔F➔r➔e➔e➔)➔ ➔V➔i➔e➔w➔ ➔b➔o➔a➔r➔d➔s➔,➔ ➔a➔d➔d➔ ➔w➔o➔r➔k➔ ➔i➔t➔e➔m➔s➔ ➔—➔ ➔n➔o➔ ➔c➔o➔d➔e➔/➔p➔i➔p➔e➔l➔i➔n➔e➔
➔B➔a➔s➔i➔c➔ ➔(➔F➔r➔e➔e➔ ➔f➔o➔r➔ ➔5➔)➔ ➔F➔u➔l➔l➔ ➔a➔c➔c➔e➔s➔s➔ ➔t➔o➔ ➔B➔o➔a➔r➔d➔s➔,➔ ➔R➔e➔p➔o➔s➔,➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔s➔
➔B➔a➔s➔i➔c➔ ➔+➔ ➔T➔e➔s➔t➔ ➔P➔l➔a➔n➔s➔ ➔A➔d➔d➔s➔ ➔A➔z➔u➔r➔e➔ ➔T➔e➔s➔t➔ ➔P➔l➔a➔n➔s➔
➔4➔.➔ ➔A➔z➔u➔r➔e➔ ➔B➔o➔a➔r➔d➔s➔ ➔—➔ ➔P➔r➔o➔j➔e➔c➔t➔ ➔M➔a➔n➔a➔g➔e➔m➔e➔n➔t➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔A➔z➔u➔r➔e➔ ➔B➔o➔a➔r➔d➔s➔?➔
➔A➔ ➔p➔r➔o➔j➔e➔c➔t➔ ➔m➔a➔n➔a➔g➔e➔m➔e➔n➔t➔ ➔t➔o➔o➔l➔ ➔t➔o➔ ➔p➔l➔a➔n➔,➔ ➔t➔r➔a➔c➔k➔,➔ ➔a➔n➔d➔ ➔d➔i➔s➔c➔u➔s➔s➔ ➔w➔o➔r➔k➔ ➔—➔ ➔s➔i➔m➔i➔l➔a➔r➔ ➔t➔o➔ ➔J➔i➔r➔a➔ ➔o➔r➔ ➔T➔r➔e➔l➔l➔o➔.➔
➔W➔o➔r➔k➔ ➔I➔t➔e➔m➔ ➔H➔i➔e➔r➔a➔r➔c➔h➔y➔ ➔(➔A➔g➔i➔l➔e➔ ➔P➔r➔o➔c➔e➔s➔s➔)➔:➔
➔E➔p➔i➔c➔
➔ ➔ ➔↓➔ ➔(➔l➔a➔r➔g➔e➔ ➔b➔u➔s➔i➔n➔e➔s➔s➔ ➔o➔b➔j➔e➔c➔t➔i➔v➔e➔)➔
➔F➔e➔a➔t➔u➔r➔e➔
➔ ➔ ➔↓➔ ➔(➔f➔u➔n➔c➔t➔i➔o➔n➔a➔l➔ ➔c➔o➔m➔p➔o➔n➔e➔n➔t➔)➔
➔U➔s➔e➔r➔ ➔S➔t➔o➔r➔y➔
➔ ➔ ➔↓➔ ➔(➔r➔e➔q➔u➔i➔r➔e➔m➔e➔n➔t➔ ➔f➔r➔o➔m➔ ➔u➔s➔e➔r➔'➔s➔ ➔p➔e➔r➔s➔p➔e➔c➔t➔i➔v➔e➔)➔
➔T➔a➔s➔k➔ ➔/➔ ➔B➔u➔g➔
➔ ➔ ➔(➔t➔e➔c➔h➔n➔i➔c➔a➔l➔ ➔i➔m➔p➔l➔e➔m➔e➔n➔t➔a➔t➔i➔o➔n➔ ➔/➔ ➔d➔e➔f➔e➔c➔t➔)➔
➔W➔o➔r➔k➔ ➔I➔t➔e➔m➔ ➔S➔t➔a➔t➔e➔s➔:➔
➔N➔e➔w➔ ➔→➔ ➔A➔c➔t➔i➔v➔e➔ ➔→➔ ➔R➔e➔s➔o➔l➔v➔e➔d➔ ➔→➔ ➔C➔l➔o➔s➔e➔d➔
➔K➔e➔y➔ ➔F➔e➔a➔t➔u➔r➔e➔s➔:➔
➔K➔a➔n➔b➔a➔n➔ ➔B➔o➔a➔r➔d➔ ➔—➔ ➔v➔i➔s➔u➔a➔l➔ ➔d➔r➔a➔g➔-➔a➔n➔d➔-➔d➔r➔o➔p➔ ➔w➔o➔r➔k➔f➔l➔o➔w➔ ➔(➔B➔o➔a➔r➔d➔s➔ ➔→➔ ➔B➔o➔a➔r➔d➔s➔)➔
➔B➔a➔c➔k➔l➔o➔g➔ ➔—➔ ➔p➔r➔i➔o➔r➔i➔t➔i➔z➔e➔d➔ ➔l➔i➔s➔t➔ ➔o➔f➔ ➔a➔l➔l➔ ➔u➔p➔c➔o➔m➔i➔n➔g➔ ➔w➔o➔r➔k➔ ➔(➔B➔o➔a➔r➔d➔s➔ ➔→➔ ➔B➔a➔c➔k➔l➔o➔g➔s➔)➔
➔S➔p➔r➔i➔n➔t➔s➔ ➔—➔ ➔t➔i➔m➔e➔-➔b➔o➔x➔e➔d➔ ➔d➔e➔l➔i➔v➔e➔r➔y➔ ➔c➔y➔c➔l➔e➔s➔ ➔(➔B➔o➔a➔r➔d➔s➔ ➔→➔ ➔S➔p➔r➔i➔n➔t➔s➔)➔
➔Q➔u➔e➔r➔i➔e➔s➔ ➔—➔ ➔s➔a➔v➔e➔ ➔c➔u➔s➔t➔o➔m➔ ➔f➔i➔l➔t➔e➔r➔s➔ ➔(➔o➔w➔n➔e➔r➔,➔ ➔s➔t➔a➔t➔e➔,➔ ➔p➔r➔i➔o➔r➔i➔t➔y➔,➔ ➔t➔a➔g➔s➔)➔
➔D➔a➔s➔h➔b➔o➔a➔r➔d➔s➔ ➔—➔ ➔w➔i➔d➔g➔e➔t➔s➔ ➔f➔o➔r➔ ➔v➔i➔s➔i➔b➔i➔l➔i➔t➔y➔ ➔(➔S➔p➔r➔i➔n➔t➔ ➔B➔u➔r➔n➔d➔o➔w➔n➔,➔ ➔B➔u➔i➔l➔d➔ ➔H➔i➔s➔t➔o➔r➔y➔,➔ ➔V➔e➔l➔o➔c➔i➔t➔y➔)➔
➔P➔r➔o➔c➔e➔s➔s➔ ➔T➔y➔p➔e➔s➔:➔
➔P➔r➔o➔c➔e➔s➔s➔ ➔W➔o➔r➔k➔ ➔I➔t➔e➔m➔s➔ ➔U➔s➔e➔ ➔W➔h➔e➔n➔
➔
➔
➔
➔
➔A➔g➔i➔l➔e➔ ➔E➔p➔i➔c➔s➔,➔ ➔F➔e➔a➔t➔u➔r➔e➔s➔,➔ ➔S➔t➔o➔r➔i➔e➔s➔,➔ ➔T➔a➔s➔k➔s➔,➔ ➔B➔u➔g➔s➔ ➔M➔o➔s➔t➔ ➔t➔e➔a➔m➔s➔
➔S➔c➔r➔u➔m➔ ➔E➔p➔i➔c➔s➔,➔ ➔F➔e➔a➔t➔u➔r➔e➔s➔,➔ ➔P➔B➔I➔s➔,➔ ➔T➔a➔s➔k➔s➔,➔ ➔B➔u➔g➔s➔ ➔S➔p➔r➔i➔n➔t➔-➔f➔o➔c➔u➔s➔e➔d➔
➔C➔M➔M➔I➔ ➔M➔o➔r➔e➔ ➔f➔o➔r➔m➔a➔l➔,➔ ➔a➔d➔d➔s➔ ➔C➔h➔a➔n➔g➔e➔ ➔R➔e➔q➔u➔e➔s➔t➔s➔ ➔R➔e➔g➔u➔l➔a➔t➔e➔d➔ ➔i➔n➔d➔u➔s➔t➔r➔i➔e➔s➔
➔B➔a➔s➔i➔c➔ ➔J➔u➔s➔t➔ ➔I➔s➔s➔u➔e➔s➔ ➔a➔n➔d➔ ➔T➔a➔s➔k➔s➔ ➔L➔e➔a➔r➔n➔i➔n➔g➔/➔s➔m➔a➔l➔l➔ ➔p➔r➔o➔j➔e➔c➔t➔s➔
➔Y➔o➔u➔r➔ ➔P➔r➔o➔j➔e➔c➔t➔ ➔—➔ ➔A➔z➔u➔r➔e➔ ➔B➔o➔a➔r➔d➔s➔ ➔S➔e➔t➔u➔p➔:➔
➔I➔n➔ ➔y➔o➔u➔r➔ ➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔ ➔p➔r➔o➔j➔e➔c➔t➔ ➔y➔o➔u➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔e➔d➔:➔
➔-➔ ➔E➔p➔i➔c➔s➔,➔ ➔F➔e➔a➔t➔u➔r➔e➔s➔,➔ ➔T➔a➔s➔k➔s➔ ➔h➔i➔e➔r➔a➔r➔c➔h➔y➔ ➔f➔o➔r➔ ➔f➔u➔l➔l➔ ➔p➔r➔o➔j➔e➔c➔t➔ ➔v➔i➔s➔i➔b➔i➔l➔i➔t➔y➔
➔-➔ ➔Q➔u➔e➔r➔y➔ ➔M➔a➔n➔a➔g➔e➔m➔e➔n➔t➔ ➔f➔o➔r➔ ➔c➔u➔s➔t➔o➔m➔ ➔v➔i➔e➔w➔s➔ ➔t➔r➔a➔c➔k➔i➔n➔g➔ ➔r➔e➔a➔l➔-➔t➔i➔m➔e➔ ➔t➔a➔s➔k➔ ➔p➔r➔o➔g➔r➔e➔s➔s➔ ➔a➔n➔d➔ ➔b➔u➔g➔ ➔f➔i➔x➔e➔s➔
➔-➔ ➔U➔s➔e➔r➔ ➔r➔o➔l➔e➔s➔ ➔a➔n➔d➔ ➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔ ➔f➔o➔r➔ ➔s➔e➔c➔u➔r➔e➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔a➔l➔l➔o➔c➔a➔t➔i➔o➔n➔
➔-➔ ➔P➔R➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔s➔ ➔t➔o➔ ➔s➔t➔a➔n➔d➔a➔r➔d➔i➔z➔e➔ ➔c➔o➔d➔e➔ ➔r➔e➔v➔i➔e➔w➔s➔ ➔a➔n➔d➔ ➔l➔i➔n➔k➔ ➔e➔v➔e➔r➔y➔ ➔m➔e➔r➔g➔e➔ ➔t➔o➔ ➔a➔ ➔T➔a➔s➔k➔ ➔o➔r➔ ➔F➔e➔a➔t➔u➔r➔e➔
➔5➔.➔ ➔A➔z➔u➔r➔e➔ ➔R➔e➔p➔o➔s➔ ➔—➔ ➔S➔o➔u➔r➔c➔e➔ ➔C➔o➔n➔t➔r➔o➔l➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔A➔z➔u➔r➔e➔ ➔R➔e➔p➔o➔s➔?➔
➔A➔ ➔s➔o➔u➔r➔c➔e➔ ➔c➔o➔n➔t➔r➔o➔l➔ ➔s➔y➔s➔t➔e➔m➔ ➔w➔i➔t➔h➔i➔n➔ ➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔ ➔t➔o➔ ➔t➔r➔a➔c➔k➔ ➔a➔n➔d➔ ➔m➔a➔n➔a➔g➔e➔ ➔c➔o➔d➔e➔ ➔c➔h➔a➔n➔g➔e➔s➔.➔ ➔S➔u➔p➔p➔o➔r➔t➔s➔ ➔G➔i➔t➔ ➔(➔d➔i➔s➔t➔r➔i➔b➔u➔t➔e➔d➔)➔
➔a➔n➔d➔ ➔T➔F➔V➔C➔ ➔(➔c➔e➔n➔t➔r➔a➔l➔i➔z➔e➔d➔)➔.➔
➔G➔i➔t➔ ➔v➔s➔ ➔T➔F➔V➔C➔:➔
➔F➔e➔a➔t➔u➔r➔e➔ ➔G➔i➔t➔ ➔(➔D➔i➔s➔t➔r➔i➔b➔u➔t➔e➔d➔)➔ ➔T➔F➔V➔C➔ ➔(➔C➔e➔n➔t➔r➔a➔l➔i➔z➔e➔d➔)➔
➔L➔o➔c➔a➔l➔ ➔c➔o➔p➔y➔ ➔F➔u➔l➔l➔ ➔h➔i➔s➔t➔o➔r➔y➔ ➔O➔n➔l➔y➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔v➔e➔r➔s➔i➔o➔n➔
➔O➔f➔f➔l➔i➔n➔e➔ ➔w➔o➔r➔k➔ ➔✅➔ ➔ ➔Y➔e➔s➔ ➔❌➔ ➔ ➔N➔o➔
➔P➔o➔p➔u➔l➔a➔r➔i➔t➔y➔ ➔I➔n➔d➔u➔s➔t➔r➔y➔ ➔s➔t➔a➔n➔d➔a➔r➔d➔ ➔L➔e➔g➔a➔c➔y➔/➔e➔n➔t➔e➔r➔p➔r➔i➔s➔e➔
➔B➔r➔a➔n➔c➔h➔i➔n➔g➔ ➔E➔a➔s➔y➔ ➔a➔n➔d➔ ➔f➔a➔s➔t➔ ➔C➔o➔m➔p➔l➔e➔x➔
➔A➔l➔w➔a➔y➔s➔ ➔u➔s➔e➔ ➔G➔i➔t➔ ➔f➔o➔r➔ ➔m➔o➔d➔e➔r➔n➔ ➔p➔r➔o➔j➔e➔c➔t➔s➔.➔
➔
➔
➔
➔
➔P➔u➔l➔l➔ ➔R➔e➔q➔u➔e➔s➔t➔ ➔(➔P➔R➔)➔ ➔W➔o➔r➔k➔f➔l➔o➔w➔:➔
➔D➔e➔v➔e➔l➔o➔p➔e➔r➔ ➔c➔r➔e➔a➔t➔e➔s➔ ➔f➔e➔a➔t➔u➔r➔e➔ ➔b➔r➔a➔n➔c➔h➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔↓➔
➔M➔a➔k➔e➔s➔ ➔a➔n➔d➔ ➔p➔u➔s➔h➔e➔s➔ ➔c➔h➔a➔n➔g➔e➔s➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔↓➔
➔C➔r➔e➔a➔t➔e➔s➔ ➔P➔u➔l➔l➔ ➔R➔e➔q➔u➔e➔s➔t➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔↓➔
➔R➔e➔v➔i➔e➔w➔e➔r➔s➔ ➔r➔e➔v➔i➔e➔w➔ ➔c➔o➔d➔e➔ ➔(➔a➔p➔p➔r➔o➔v➔e➔/➔r➔e➔j➔e➔c➔t➔/➔c➔o➔m➔m➔e➔n➔t➔)➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔↓➔
➔A➔l➔l➔ ➔c➔h➔e➔c➔k➔s➔ ➔p➔a➔s➔s➔ ➔(➔p➔o➔l➔i➔c➔i➔e➔s➔)➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔↓➔
➔M➔e➔r➔g➔e➔ ➔t➔o➔ ➔m➔a➔i➔n➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔↓➔
➔D➔e➔l➔e➔t➔e➔ ➔f➔e➔a➔t➔u➔r➔e➔ ➔b➔r➔a➔n➔c➔h➔
➔B➔r➔a➔n➔c➔h➔ ➔P➔o➔l➔i➔c➔i➔e➔s➔ ➔(➔p➔r➔o➔t➔e➔c➔t➔ ➔m➔a➔i➔n➔ ➔b➔r➔a➔n➔c➔h➔)➔:➔
➔#➔ ➔I➔n➔ ➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔:➔
➔P➔r➔o➔j➔e➔c➔t➔ ➔S➔e➔t➔t➔i➔n➔g➔s➔ ➔→➔ ➔R➔e➔p➔o➔s➔i➔t➔o➔r➔i➔e➔s➔ ➔→➔ ➔B➔r➔a➔n➔c➔h➔ ➔P➔o➔l➔i➔c➔i➔e➔s➔ ➔→➔ ➔m➔a➔i➔n➔
➔P➔o➔l➔i➔c➔i➔e➔s➔ ➔t➔o➔ ➔e➔n➔a➔b➔l➔e➔:➔
➔✅➔ ➔ ➔M➔i➔n➔i➔m➔u➔m➔ ➔r➔e➔v➔i➔e➔w➔e➔r➔s➔:➔ ➔2➔
➔✅➔ ➔ ➔C➔h➔e➔c➔k➔ ➔f➔o➔r➔ ➔l➔i➔n➔k➔e➔d➔ ➔w➔o➔r➔k➔ ➔i➔t➔e➔m➔s➔
➔✅➔ ➔ ➔C➔h➔e➔c➔k➔ ➔f➔o➔r➔ ➔c➔o➔m➔m➔e➔n➔t➔ ➔r➔e➔s➔o➔l➔u➔t➔i➔o➔n➔
➔✅➔ ➔ ➔B➔u➔i➔l➔d➔ ➔v➔a➔l➔i➔d➔a➔t➔i➔o➔n➔ ➔(➔C➔I➔ ➔m➔u➔s➔t➔ ➔p➔a➔s➔s➔ ➔b➔e➔f➔o➔r➔e➔ ➔m➔e➔r➔g➔e➔)➔
➔✅➔ ➔ ➔L➔i➔m➔i➔t➔ ➔m➔e➔r➔g➔e➔ ➔t➔y➔p➔e➔s➔ ➔(➔s➔q➔u➔a➔s➔h➔ ➔o➔n➔l➔y➔)➔
➔P➔R➔ ➔T➔e➔m➔p➔l➔a➔t➔e➔ ➔—➔ ➔Y➔o➔u➔r➔ ➔P➔r➔o➔j➔e➔c➔t➔ ➔S➔e➔t➔u➔p➔:➔
➔#➔ ➔C➔r➔e➔a➔t➔e➔ ➔f➔i➔l➔e➔ ➔a➔t➔:➔
➔.➔a➔z➔u➔r➔e➔d➔e➔v➔o➔p➔s➔/➔p➔u➔l➔l➔_➔r➔e➔q➔u➔e➔s➔t➔_➔t➔e➔m➔p➔l➔a➔t➔e➔.➔m➔d➔
➔#➔#➔ ➔W➔h➔a➔t➔ ➔t➔y➔p➔e➔ ➔o➔f➔ ➔P➔R➔ ➔i➔s➔ ➔t➔h➔i➔s➔?➔
➔-➔ ➔[➔ ➔]➔ ➔F➔e➔a➔t➔u➔r➔e➔
➔-➔ ➔[➔ ➔]➔ ➔B➔u➔g➔f➔i➔x➔
➔-➔ ➔[➔ ➔]➔ ➔E➔n➔h➔a➔n➔c➔e➔m➔e➔n➔t➔
➔#➔#➔ ➔D➔e➔s➔c➔r➔i➔p➔t➔i➔o➔n➔ ➔o➔f➔ ➔c➔h➔a➔n➔g➔e➔s➔
➔#➔#➔ ➔R➔e➔l➔a➔t➔e➔d➔ ➔W➔o➔r➔k➔ ➔I➔t➔e➔m➔ ➔/➔ ➔I➔s➔s➔u➔e➔
➔#➔#➔ ➔U➔n➔i➔t➔ ➔T➔e➔s➔t➔i➔n➔g➔
➔
➔
➔
➔
➔#➔#➔ ➔P➔o➔s➔t➔-➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔t➔a➔s➔k➔s➔
➔I➔M➔P➔O➔R➔T➔A➔N➔T➔:➔ ➔T➔e➔m➔p➔l➔a➔t➔e➔ ➔m➔u➔s➔t➔ ➔b➔e➔ ➔i➔n➔ ➔.➔a➔z➔u➔r➔e➔d➔e➔v➔o➔p➔s➔/➔ ➔ ➔f➔o➔l➔d➔e➔r➔ ➔a➔n➔d➔ ➔m➔e➔r➔g➔e➔d➔ ➔t➔o➔ ➔m➔a➔i➔n➔ ➔b➔r➔a➔n➔c➔h➔ ➔t➔o➔ ➔t➔a➔k➔e➔ ➔e➔f➔f➔e➔c➔t➔.➔
➔6➔.➔ ➔S➔e➔l➔f➔-➔H➔o➔s➔t➔e➔d➔ ➔A➔g➔e➔n➔t➔ ➔—➔ ➔C➔o➔m➔p➔l➔e➔t➔e➔ ➔S➔e➔t➔u➔p➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔n➔ ➔A➔g➔e➔n➔t➔?➔
➔A➔ ➔m➔a➔c➔h➔i➔n➔e➔ ➔t➔h➔a➔t➔ ➔r➔u➔n➔s➔ ➔y➔o➔u➔r➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔s➔t➔e➔p➔s➔.➔ ➔W➔h➔e➔n➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔i➔s➔ ➔t➔r➔i➔g➔g➔e➔r➔e➔d➔,➔ ➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔ ➔a➔s➔s➔i➔g➔n➔s➔ ➔a➔n➔ ➔a➔g➔e➔n➔t➔ ➔t➔o➔ ➔e➔x➔e➔c➔u➔t➔e➔
➔e➔a➔c➔h➔ ➔j➔o➔b➔.➔
➔M➔i➔c➔r➔o➔s➔o➔f➔t➔-➔H➔o➔s➔t➔e➔d➔ ➔v➔s➔ ➔S➔e➔l➔f➔-➔H➔o➔s➔t➔e➔d➔:➔
➔F➔e➔a➔t➔u➔r➔e➔ ➔M➔i➔c➔r➔o➔s➔o➔f➔t➔ ➔H➔o➔s➔t➔e➔d➔ ➔S➔e➔l➔f➔-➔H➔o➔s➔t➔e➔d➔
➔S➔e➔t➔u➔p➔ ➔N➔o➔ ➔s➔e➔t➔u➔p➔ ➔n➔e➔e➔d➔e➔d➔ ➔I➔n➔s➔t➔a➔l➔l➔ ➔m➔a➔n➔u➔a➔l➔l➔y➔
➔C➔o➔s➔t➔ ➔1➔8➔0➔0➔ ➔f➔r➔e➔e➔ ➔m➔i➔n➔s➔/➔m➔o➔n➔t➔h➔ ➔U➔n➔l➔i➔m➔i➔t➔e➔d➔
➔T➔o➔o➔l➔s➔ ➔P➔r➔e➔-➔i➔n➔s➔t➔a➔l➔l➔e➔d➔ ➔c➔o➔m➔m➔o➔n➔ ➔t➔o➔o➔l➔s➔ ➔Y➔o➔u➔ ➔c➔o➔n➔t➔r➔o➔l➔ ➔e➔v➔e➔r➔y➔t➔h➔i➔n➔g➔
➔N➔e➔t➔w➔o➔r➔k➔ ➔P➔u➔b➔l➔i➔c➔ ➔i➔n➔t➔e➔r➔n➔e➔t➔ ➔o➔n➔l➔y➔ ➔C➔a➔n➔ ➔a➔c➔c➔e➔s➔s➔ ➔p➔r➔i➔v➔a➔t➔e➔ ➔n➔e➔t➔w➔o➔r➔k➔
➔S➔p➔e➔e➔d➔ ➔F➔r➔e➔s➔h➔ ➔V➔M➔ ➔e➔a➔c➔h➔ ➔t➔i➔m➔e➔ ➔(➔s➔l➔o➔w➔e➔r➔ ➔s➔t➔a➔r➔t➔)➔ ➔P➔e➔r➔s➔i➔s➔t➔e➔n➔t➔ ➔(➔f➔a➔s➔t➔e➔r➔)➔
➔U➔s➔e➔ ➔w➔h➔e➔n➔ ➔S➔i➔m➔p➔l➔e➔ ➔C➔I➔,➔ ➔o➔p➔e➔n➔ ➔s➔o➔u➔r➔c➔e➔ ➔C➔o➔r➔p➔o➔r➔a➔t➔e➔ ➔n➔e➔t➔w➔o➔r➔k➔,➔ ➔s➔p➔e➔c➔i➔a➔l➔ ➔t➔o➔o➔l➔s➔
➔S➔e➔l➔f➔-➔H➔o➔s➔t➔e➔d➔ ➔A➔g➔e➔n➔t➔ ➔S➔e➔t➔u➔p➔ ➔—➔ ➔Y➔o➔u➔r➔ ➔P➔r➔o➔j➔e➔c➔t➔ ➔S➔t➔e➔p➔s➔:➔
➔#➔ ➔S➔T➔E➔P➔ ➔1➔ ➔—➔ ➔D➔o➔w➔n➔l➔o➔a➔d➔ ➔A➔g➔e➔n➔t➔
➔#➔ ➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔ ➔→➔ ➔O➔r➔g➔a➔n➔i➔z➔a➔t➔i➔o➔n➔ ➔S➔e➔t➔t➔i➔n➔g➔s➔ ➔→➔ ➔A➔g➔e➔n➔t➔ ➔P➔o➔o➔l➔s➔ ➔→➔ ➔D➔e➔f➔a➔u➔l➔t➔ ➔→➔ ➔N➔e➔w➔ ➔A➔g➔e➔n➔t➔
➔#➔ ➔D➔o➔w➔n➔l➔o➔a➔d➔:➔ ➔v➔s➔t➔s➔-➔a➔g➔e➔n➔t➔-➔l➔i➔n➔u➔x➔-➔x➔6➔4➔-➔4➔.➔x➔.➔x➔.➔t➔a➔r➔.➔g➔z➔
➔#➔ ➔S➔T➔E➔P➔ ➔2➔ ➔—➔ ➔E➔x➔t➔r➔a➔c➔t➔
➔m➔k➔d➔i➔r➔ ➔~➔/➔m➔y➔a➔g➔e➔n➔t➔
➔c➔d➔ ➔~➔/➔m➔y➔a➔g➔e➔n➔t➔
➔t➔a➔r➔ ➔-➔x➔v➔z➔f➔ ➔v➔s➔t➔s➔-➔a➔g➔e➔n➔t➔-➔l➔i➔n➔u➔x➔-➔x➔6➔4➔-➔4➔.➔x➔.➔x➔.➔t➔a➔r➔.➔g➔z➔
➔#➔ ➔S➔T➔E➔P➔ ➔3➔ ➔—➔ ➔C➔o➔n➔f➔i➔g➔u➔r➔e➔
➔.➔/➔c➔o➔n➔f➔i➔g➔.➔s➔h➔
➔#➔ ➔D➔u➔r➔i➔n➔g➔ ➔s➔e➔t➔u➔p➔,➔ ➔e➔n➔t➔e➔r➔:➔
➔#➔ ➔S➔e➔r➔v➔e➔r➔ ➔U➔R➔L➔:➔ ➔ ➔ ➔ ➔ ➔h➔t➔t➔p➔s➔:➔/➔/➔d➔e➔v➔.➔a➔z➔u➔r➔e➔.➔c➔o➔m➔/➔a➔k➔h➔i➔l➔b➔m➔1➔3➔
➔#➔ ➔A➔u➔t➔h➔ ➔t➔y➔p➔e➔:➔ ➔ ➔ ➔ ➔ ➔ ➔P➔A➔T➔ ➔(➔p➔r➔e➔s➔s➔ ➔E➔n➔t➔e➔r➔)➔
➔
➔
➔
➔
➔#➔ ➔P➔A➔T➔:➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔<➔p➔a➔s➔t➔e➔ ➔y➔o➔u➔r➔ ➔P➔e➔r➔s➔o➔n➔a➔l➔ ➔A➔c➔c➔e➔s➔s➔ ➔T➔o➔k➔e➔n➔>➔
➔#➔ ➔A➔g➔e➔n➔t➔ ➔p➔o➔o➔l➔:➔ ➔ ➔ ➔ ➔ ➔D➔e➔f➔a➔u➔l➔t➔
➔#➔ ➔A➔g➔e➔n➔t➔ ➔n➔a➔m➔e➔:➔ ➔ ➔ ➔ ➔ ➔m➔y➔a➔g➔e➔n➔t➔
➔#➔ ➔W➔o➔r➔k➔ ➔f➔o➔l➔d➔e➔r➔:➔ ➔ ➔ ➔ ➔p➔r➔e➔s➔s➔ ➔E➔n➔t➔e➔r➔ ➔(➔_➔w➔o➔r➔k➔)➔
➔#➔ ➔S➔T➔E➔P➔ ➔4➔ ➔—➔ ➔S➔t➔a➔r➔t➔ ➔A➔g➔e➔n➔t➔
➔.➔/➔r➔u➔n➔.➔s➔h➔
➔#➔ ➔E➔x➔p➔e➔c➔t➔e➔d➔ ➔o➔u➔t➔p➔u➔t➔:➔ ➔L➔i➔s➔t➔e➔n➔i➔n➔g➔ ➔f➔o➔r➔ ➔J➔o➔b➔s➔
➔#➔ ➔S➔T➔E➔P➔ ➔5➔ ➔—➔ ➔V➔e➔r➔i➔f➔y➔ ➔O➔n➔l➔i➔n➔e➔
➔#➔ ➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔ ➔→➔ ➔O➔r➔g➔a➔n➔i➔z➔a➔t➔i➔o➔n➔ ➔S➔e➔t➔t➔i➔n➔g➔s➔ ➔→➔ ➔A➔g➔e➔n➔t➔ ➔P➔o➔o➔l➔s➔ ➔→➔ ➔D➔e➔f➔a➔u➔l➔t➔
➔#➔ ➔S➔t➔a➔t➔u➔s➔:➔ ➔m➔y➔a➔g➔e➔n➔t➔ ➔→➔ ➔O➔N➔L➔I➔N➔E➔ ➔(➔g➔r➔e➔e➔n➔)➔
➔C➔r➔e➔a➔t➔e➔ ➔P➔A➔T➔ ➔(➔P➔e➔r➔s➔o➔n➔a➔l➔ ➔A➔c➔c➔e➔s➔s➔ ➔T➔o➔k➔e➔n➔)➔:➔
➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔ ➔→➔ ➔P➔r➔o➔f➔i➔l➔e➔ ➔→➔ ➔P➔e➔r➔s➔o➔n➔a➔l➔ ➔A➔c➔c➔e➔s➔s➔ ➔T➔o➔k➔e➔n➔ ➔→➔ ➔N➔e➔w➔ ➔T➔o➔k➔e➔n➔
➔S➔c➔o➔p➔e➔:➔ ➔A➔g➔e➔n➔t➔ ➔P➔o➔o➔l➔s➔ ➔→➔ ➔R➔e➔a➔d➔ ➔&➔ ➔M➔a➔n➔a➔g➔e➔
➔C➔o➔p➔y➔ ➔t➔o➔k➔e➔n➔ ➔(➔s➔h➔o➔w➔n➔ ➔o➔n➔l➔y➔ ➔o➔n➔c➔e➔!➔)➔
➔C➔o➔m➔m➔o➔n➔ ➔A➔g➔e➔n➔t➔ ➔E➔r➔r➔o➔r➔s➔:➔
➔E➔r➔r➔o➔r➔ ➔R➔e➔a➔s➔o➔n➔ ➔F➔i➔x➔
➔A➔g➔e➔n➔t➔ ➔O➔f➔f➔l➔i➔n➔e➔ ➔r➔u➔n➔.➔s➔h➔ ➔n➔o➔t➔ ➔r➔u➔n➔n➔i➔n➔g➔ ➔.➔/➔r➔u➔n➔.➔s➔h➔
➔V➔S➔3➔0➔0➔6➔3➔ ➔U➔n➔a➔u➔t➔h➔o➔r➔i➔z➔e➔d➔ ➔W➔r➔o➔n➔g➔ ➔P➔A➔T➔ ➔o➔r➔ ➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔ ➔R➔e➔c➔r➔e➔a➔t➔e➔ ➔P➔A➔T➔ ➔w➔i➔t➔h➔ ➔A➔g➔e➔n➔t➔ ➔P➔o➔o➔l➔s➔:➔ ➔R➔e➔a➔d➔ ➔&➔ ➔M➔a➔n➔a➔g➔e➔
➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔u➔s➔e➔s➔ ➔M➔i➔c➔r➔o➔s➔o➔f➔t➔ ➔a➔g➔e➔n➔t➔ ➔v➔m➔I➔m➔a➔g➔e➔ ➔s➔t➔i➔l➔l➔ ➔i➔n➔ ➔Y➔A➔M➔L➔ ➔R➔e➔m➔o➔v➔e➔ ➔v➔m➔I➔m➔a➔g➔e➔,➔ ➔u➔s➔e➔ ➔p➔o➔o➔l➔ ➔n➔a➔m➔e➔
➔A➔g➔e➔n➔t➔ ➔n➔o➔t➔ ➔v➔i➔s➔i➔b➔l➔e➔ ➔W➔r➔o➔n➔g➔ ➔o➔r➔g➔ ➔U➔R➔L➔ ➔U➔s➔e➔ ➔h➔t➔t➔p➔s➔:➔/➔/➔d➔e➔v➔.➔a➔z➔u➔r➔e➔.➔c➔o➔m➔/➔
➔7➔.➔ ➔A➔z➔u➔r➔e➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔s➔ ➔—➔ ➔C➔o➔m➔p➔l➔e➔t➔e➔ ➔G➔u➔i➔d➔e➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔?➔
➔A➔n➔ ➔a➔u➔t➔o➔m➔a➔t➔e➔d➔ ➔w➔o➔r➔k➔f➔l➔o➔w➔ ➔t➔h➔a➔t➔ ➔b➔u➔i➔l➔d➔s➔,➔ ➔t➔e➔s➔t➔s➔,➔ ➔a➔n➔d➔ ➔d➔e➔p➔l➔o➔y➔s➔ ➔y➔o➔u➔r➔ ➔c➔o➔d➔e➔.➔
➔T➔w➔o➔ ➔w➔a➔y➔s➔ ➔t➔o➔ ➔c➔r➔e➔a➔t➔e➔:➔
➔M➔e➔t➔h➔o➔d➔ ➔D➔e➔s➔c➔r➔i➔p➔t➔i➔o➔n➔
➔C➔l➔a➔s➔s➔i➔c➔ ➔E➔d➔i➔t➔o➔r➔ ➔(➔G➔U➔I➔)➔ ➔V➔i➔s➔u➔a➔l➔ ➔e➔d➔i➔t➔o➔r➔,➔ ➔d➔r➔a➔g➔-➔a➔n➔d➔-➔d➔r➔o➔p➔.➔ ➔G➔o➔o➔d➔ ➔f➔o➔r➔ ➔b➔e➔g➔i➔n➔n➔e➔r➔s➔.➔
➔
➔
➔
➔
➔Y➔A➔M➔L➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔a➔s➔ ➔c➔o➔d➔e➔,➔ ➔s➔t➔o➔r➔e➔d➔ ➔i➔n➔ ➔r➔e➔p➔o➔.➔ ➔M➔o➔d➔e➔r➔n➔ ➔s➔t➔a➔n➔d➔a➔r➔d➔.➔ ➔✅➔
➔Y➔A➔M➔L➔ ➔B➔a➔s➔i➔c➔s➔
➔R➔u➔l➔e➔s➔:➔
➔I➔n➔d➔e➔n➔t➔a➔t➔i➔o➔n➔:➔ ➔S➔P➔A➔C➔E➔S➔ ➔o➔n➔l➔y➔ ➔(➔n➔e➔v➔e➔r➔ ➔t➔a➔b➔s➔)➔,➔ ➔2➔ ➔s➔p➔a➔c➔e➔s➔ ➔p➔e➔r➔ ➔l➔e➔v➔e➔l➔
➔C➔a➔s➔e➔-➔s➔e➔n➔s➔i➔t➔i➔v➔e➔:➔ ➔n➔a➔m➔e➔ ➔ ➔a➔n➔d➔ ➔N➔a➔m➔e➔ ➔ ➔a➔r➔e➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔t➔
➔L➔i➔s➔t➔s➔ ➔u➔s➔e➔ ➔d➔a➔s➔h➔:➔ ➔-➔ ➔i➔t➔e➔m➔
➔K➔e➔y➔-➔v➔a➔l➔u➔e➔:➔ ➔k➔e➔y➔:➔ ➔v➔a➔l➔u➔e➔ ➔ ➔(➔s➔p➔a➔c➔e➔ ➔a➔f➔t➔e➔r➔ ➔c➔o➔l➔o➔n➔ ➔i➔s➔ ➔R➔E➔Q➔U➔I➔R➔E➔D➔)➔
➔C➔o➔m➔m➔e➔n➔t➔s➔:➔ ➔#➔
➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔H➔i➔e➔r➔a➔r➔c➔h➔y➔:➔
➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔(➔a➔z➔u➔r➔e➔-➔p➔i➔p➔e➔l➔i➔n➔e➔s➔.➔y➔m➔l➔)➔
➔ ➔ ➔↓➔
➔S➔t➔a➔g➔e➔s➔ ➔(➔B➔u➔i➔l➔d➔,➔ ➔T➔e➔s➔t➔,➔ ➔D➔e➔p➔l➔o➔y➔)➔
➔ ➔ ➔↓➔
➔J➔o➔b➔s➔ ➔(➔B➔u➔i➔l➔d➔J➔o➔b➔,➔ ➔T➔e➔s➔t➔J➔o➔b➔)➔
➔ ➔ ➔↓➔
➔S➔t➔e➔p➔s➔ ➔(➔s➔c➔r➔i➔p➔t➔,➔ ➔t➔a➔s➔k➔)➔
➔ ➔ ➔↓➔
➔T➔a➔s➔k➔s➔ ➔(➔D➔o➔c➔k➔e➔r➔@➔2➔,➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔M➔a➔n➔i➔f➔e➔s➔t➔@➔0➔)➔
➔B➔a➔s➔i➔c➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔S➔t➔r➔u➔c➔t➔u➔r➔e➔
➔#➔ ➔a➔z➔u➔r➔e➔-➔p➔i➔p➔e➔l➔i➔n➔e➔s➔.➔y➔m➔l➔
➔t➔r➔i➔g➔g➔e➔r➔:➔
➔-➔ ➔m➔a➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔u➔n➔ ➔w➔h➔e➔n➔ ➔c➔o➔d➔e➔ ➔p➔u➔s➔h➔e➔d➔ ➔t➔o➔ ➔m➔a➔i➔n➔
➔p➔o➔o➔l➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔D➔e➔f➔a➔u➔l➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔l➔f➔-➔h➔o➔s➔t➔e➔d➔ ➔a➔g➔e➔n➔t➔ ➔p➔o➔o➔l➔ ➔(➔Y➔O➔U➔R➔ ➔P➔R➔O➔J➔E➔C➔T➔)➔
➔ ➔ ➔#➔ ➔v➔m➔I➔m➔a➔g➔e➔:➔ ➔'➔u➔b➔u➔n➔t➔u➔-➔l➔a➔t➔e➔s➔t➔'➔ ➔ ➔ ➔#➔ ➔M➔i➔c➔r➔o➔s➔o➔f➔t➔-➔h➔o➔s➔t➔e➔d➔ ➔(➔c➔o➔m➔m➔e➔n➔t➔ ➔o➔u➔t➔ ➔f➔o➔r➔ ➔s➔e➔l➔f➔-➔h➔o➔s➔t➔e➔d➔)➔
➔v➔a➔r➔i➔a➔b➔l➔e➔s➔:➔
➔ ➔ ➔b➔u➔i➔l➔d➔C➔o➔n➔f➔i➔g➔:➔ ➔R➔e➔l➔e➔a➔s➔e➔
➔ ➔ ➔a➔p➔p➔N➔a➔m➔e➔:➔ ➔m➔y➔a➔p➔p➔
➔s➔t➔a➔g➔e➔s➔:➔
➔-➔ ➔s➔t➔a➔g➔e➔:➔ ➔B➔u➔i➔l➔d➔
➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔B➔u➔i➔l➔d➔ ➔S➔t➔a➔g➔e➔
➔ ➔ ➔j➔o➔b➔s➔:➔
➔ ➔ ➔-➔ ➔j➔o➔b➔:➔ ➔B➔u➔i➔l➔d➔J➔o➔b➔
➔
➔
➔
➔
➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔s➔c➔r➔i➔p➔t➔:➔ ➔e➔c➔h➔o➔ ➔"➔B➔u➔i➔l➔d➔i➔n➔g➔ ➔$➔(➔a➔p➔p➔N➔a➔m➔e➔)➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔'➔B➔u➔i➔l➔d➔ ➔S➔t➔e➔p➔'➔
➔-➔ ➔s➔t➔a➔g➔e➔:➔ ➔T➔e➔s➔t➔
➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔T➔e➔s➔t➔ ➔S➔t➔a➔g➔e➔
➔ ➔ ➔d➔e➔p➔e➔n➔d➔s➔O➔n➔:➔ ➔B➔u➔i➔l➔d➔
➔ ➔ ➔j➔o➔b➔s➔:➔
➔ ➔ ➔-➔ ➔j➔o➔b➔:➔ ➔T➔e➔s➔t➔J➔o➔b➔
➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔s➔c➔r➔i➔p➔t➔:➔ ➔e➔c➔h➔o➔ ➔"➔R➔u➔n➔n➔i➔n➔g➔ ➔T➔e➔s➔t➔s➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔'➔T➔e➔s➔t➔ ➔S➔t➔e➔p➔'➔
➔-➔ ➔s➔t➔a➔g➔e➔:➔ ➔D➔e➔p➔l➔o➔y➔
➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔D➔e➔p➔l➔o➔y➔ ➔S➔t➔a➔g➔e➔
➔ ➔ ➔d➔e➔p➔e➔n➔d➔s➔O➔n➔:➔ ➔T➔e➔s➔t➔
➔ ➔ ➔c➔o➔n➔d➔i➔t➔i➔o➔n➔:➔ ➔s➔u➔c➔c➔e➔e➔d➔e➔d➔(➔)➔
➔ ➔ ➔j➔o➔b➔s➔:➔
➔ ➔ ➔-➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔:➔ ➔D➔e➔p➔l➔o➔y➔J➔o➔b➔
➔ ➔ ➔ ➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔:➔ ➔P➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔ ➔ ➔ ➔ ➔s➔t➔r➔a➔t➔e➔g➔y➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔r➔u➔n➔O➔n➔c➔e➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔e➔p➔l➔o➔y➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔s➔c➔r➔i➔p➔t➔:➔ ➔e➔c➔h➔o➔ ➔"➔D➔e➔p➔l➔o➔y➔i➔n➔g➔ ➔t➔o➔ ➔P➔r➔o➔d➔u➔c➔t➔i➔o➔n➔"➔
➔Y➔o➔u➔r➔ ➔P➔r➔o➔j➔e➔c➔t➔ ➔—➔ ➔Y➔A➔M➔L➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔(➔S➔e➔l➔f➔-➔H➔o➔s➔t➔e➔d➔ ➔A➔g➔e➔n➔t➔)➔
➔#➔ ➔Y➔o➔u➔r➔ ➔a➔c➔t➔u➔a➔l➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔c➔o➔n➔n➔e➔c➔t➔i➔n➔g➔ ➔t➔o➔ ➔m➔y➔a➔g➔e➔n➔t➔
➔t➔r➔i➔g➔g➔e➔r➔:➔
➔-➔ ➔m➔a➔i➔n➔
➔p➔o➔o➔l➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔D➔e➔f➔a➔u➔l➔t➔
➔ ➔ ➔d➔e➔m➔a➔n➔d➔s➔:➔
➔ ➔ ➔-➔ ➔A➔g➔e➔n➔t➔.➔N➔a➔m➔e➔ ➔-➔e➔q➔u➔a➔l➔s➔ ➔m➔y➔a➔g➔e➔n➔t➔ ➔ ➔ ➔ ➔#➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔a➔l➔l➔y➔ ➔u➔s➔e➔ ➔Y➔O➔U➔R➔ ➔a➔g➔e➔n➔t➔
➔s➔t➔e➔p➔s➔:➔
➔-➔ ➔s➔c➔r➔i➔p➔t➔:➔ ➔e➔c➔h➔o➔ ➔H➔e➔l➔l➔o➔,➔ ➔w➔o➔r➔l➔d➔!➔
➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔'➔R➔u➔n➔ ➔a➔ ➔o➔n➔e➔-➔l➔i➔n➔e➔ ➔s➔c➔r➔i➔p➔t➔'➔
➔-➔ ➔s➔c➔r➔i➔p➔t➔:➔ ➔|➔
➔ ➔ ➔ ➔ ➔e➔c➔h➔o➔ ➔R➔u➔n➔n➔i➔n➔g➔ ➔o➔n➔ ➔s➔e➔l➔f➔-➔h➔o➔s➔t➔e➔d➔ ➔a➔g➔e➔n➔t➔
➔ ➔ ➔ ➔ ➔e➔c➔h➔o➔ ➔A➔g➔e➔n➔t➔ ➔N➔a➔m➔e➔:➔ ➔m➔y➔a➔g➔e➔n➔t➔
➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔'➔R➔u➔n➔ ➔a➔ ➔m➔u➔l➔t➔i➔-➔l➔i➔n➔e➔ ➔s➔c➔r➔i➔p➔t➔'➔
➔
➔
➔
➔
➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔T➔r➔i➔g➔g➔e➔r➔s➔
➔#➔ ➔P➔u➔s➔h➔ ➔t➔r➔i➔g➔g➔e➔r➔ ➔(➔m➔o➔s➔t➔ ➔c➔o➔m➔m➔o➔n➔)➔
➔t➔r➔i➔g➔g➔e➔r➔:➔
➔-➔ ➔m➔a➔i➔n➔
➔-➔ ➔d➔e➔v➔e➔l➔o➔p➔
➔#➔ ➔P➔R➔ ➔t➔r➔i➔g➔g➔e➔r➔ ➔(➔v➔a➔l➔i➔d➔a➔t➔e➔ ➔b➔e➔f➔o➔r➔e➔ ➔m➔e➔r➔g➔e➔)➔
➔p➔r➔:➔
➔-➔ ➔m➔a➔i➔n➔
➔#➔ ➔S➔c➔h➔e➔d➔u➔l➔e➔d➔ ➔t➔r➔i➔g➔g➔e➔r➔ ➔(➔n➔i➔g➔h➔t➔l➔y➔ ➔b➔u➔i➔l➔d➔s➔)➔
➔s➔c➔h➔e➔d➔u➔l➔e➔s➔:➔
➔-➔ ➔c➔r➔o➔n➔:➔ ➔"➔0➔ ➔2➔ ➔*➔ ➔*➔ ➔*➔"➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔2➔a➔m➔ ➔e➔v➔e➔r➔y➔ ➔n➔i➔g➔h➔t➔
➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔N➔i➔g➔h➔t➔l➔y➔ ➔B➔u➔i➔l➔d➔
➔ ➔ ➔b➔r➔a➔n➔c➔h➔e➔s➔:➔
➔ ➔ ➔ ➔ ➔i➔n➔c➔l➔u➔d➔e➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔m➔a➔i➔n➔
➔#➔ ➔M➔a➔n➔u➔a➔l➔ ➔o➔n➔l➔y➔ ➔(➔n➔o➔ ➔a➔u➔t➔o➔-➔t➔r➔i➔g➔g➔e➔r➔)➔
➔t➔r➔i➔g➔g➔e➔r➔:➔ ➔n➔o➔n➔e➔
➔M➔u➔l➔t➔i➔-➔S➔t➔a➔g➔e➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔(➔B➔u➔i➔l➔d➔ ➔→➔ ➔T➔e➔s➔t➔ ➔→➔ ➔D➔e➔p➔l➔o➔y➔)➔
➔t➔r➔i➔g➔g➔e➔r➔:➔
➔-➔ ➔m➔a➔i➔n➔
➔p➔o➔o➔l➔:➔
➔ ➔ ➔v➔m➔I➔m➔a➔g➔e➔:➔ ➔'➔u➔b➔u➔n➔t➔u➔-➔l➔a➔t➔e➔s➔t➔'➔
➔s➔t➔a➔g➔e➔s➔:➔
➔#➔ ➔─➔─➔ ➔S➔T➔A➔G➔E➔ ➔1➔:➔ ➔B➔U➔I➔L➔D➔ ➔─➔─➔
➔-➔ ➔s➔t➔a➔g➔e➔:➔ ➔B➔u➔i➔l➔d➔
➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔B➔u➔i➔l➔d➔ ➔S➔t➔a➔g➔e➔
➔ ➔ ➔j➔o➔b➔s➔:➔
➔ ➔ ➔-➔ ➔j➔o➔b➔:➔ ➔B➔u➔i➔l➔d➔J➔o➔b➔
➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔s➔c➔r➔i➔p➔t➔:➔ ➔e➔c➔h➔o➔ ➔"➔R➔u➔n➔n➔i➔n➔g➔ ➔B➔u➔i➔l➔d➔ ➔o➔n➔ ➔U➔b➔u➔n➔t➔u➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔'➔B➔u➔i➔l➔d➔'➔
➔#➔ ➔─➔─➔ ➔S➔T➔A➔G➔E➔ ➔2➔:➔ ➔T➔E➔S➔T➔ ➔─➔─➔
➔-➔ ➔s➔t➔a➔g➔e➔:➔ ➔T➔e➔s➔t➔
➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔T➔e➔s➔t➔ ➔S➔t➔a➔g➔e➔
➔ ➔ ➔d➔e➔p➔e➔n➔d➔s➔O➔n➔:➔ ➔B➔u➔i➔l➔d➔
➔ ➔ ➔j➔o➔b➔s➔:➔
➔
➔
➔
➔
➔ ➔ ➔-➔ ➔j➔o➔b➔:➔ ➔T➔e➔s➔t➔J➔o➔b➔
➔ ➔ ➔ ➔ ➔p➔o➔o➔l➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔v➔m➔I➔m➔a➔g➔e➔:➔ ➔'➔w➔i➔n➔d➔o➔w➔s➔-➔l➔a➔t➔e➔s➔t➔'➔ ➔ ➔ ➔ ➔#➔ ➔o➔v➔e➔r➔r➔i➔d➔e➔ ➔t➔o➔ ➔u➔s➔e➔ ➔W➔i➔n➔d➔o➔w➔s➔ ➔f➔o➔r➔ ➔t➔e➔s➔t➔i➔n➔g➔
➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔s➔c➔r➔i➔p➔t➔:➔ ➔e➔c➔h➔o➔ ➔"➔R➔u➔n➔n➔i➔n➔g➔ ➔T➔e➔s➔t➔s➔ ➔o➔n➔ ➔W➔i➔n➔d➔o➔w➔s➔"➔
➔#➔ ➔─➔─➔ ➔S➔T➔A➔G➔E➔ ➔3➔:➔ ➔U➔A➔T➔ ➔─➔─➔
➔-➔ ➔s➔t➔a➔g➔e➔:➔ ➔U➔A➔T➔
➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔U➔A➔T➔ ➔S➔t➔a➔g➔e➔
➔ ➔ ➔d➔e➔p➔e➔n➔d➔s➔O➔n➔:➔ ➔T➔e➔s➔t➔
➔ ➔ ➔j➔o➔b➔s➔:➔
➔ ➔ ➔-➔ ➔j➔o➔b➔:➔ ➔U➔A➔T➔J➔o➔b➔
➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔s➔c➔r➔i➔p➔t➔:➔ ➔e➔c➔h➔o➔ ➔"➔R➔u➔n➔n➔i➔n➔g➔ ➔U➔A➔T➔"➔
➔#➔ ➔─➔─➔ ➔S➔T➔A➔G➔E➔ ➔4➔:➔ ➔P➔R➔O➔D➔U➔C➔T➔I➔O➔N➔ ➔─➔─➔
➔-➔ ➔s➔t➔a➔g➔e➔:➔ ➔P➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔P➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔S➔t➔a➔g➔e➔
➔ ➔ ➔d➔e➔p➔e➔n➔d➔s➔O➔n➔:➔ ➔U➔A➔T➔
➔ ➔ ➔j➔o➔b➔s➔:➔
➔ ➔ ➔-➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔:➔ ➔D➔e➔p➔l➔o➔y➔P➔r➔o➔d➔
➔ ➔ ➔ ➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔:➔ ➔P➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔p➔p➔r➔o➔v➔a➔l➔ ➔r➔e➔q➔u➔i➔r➔e➔d➔ ➔h➔e➔r➔e➔
➔ ➔ ➔ ➔ ➔s➔t➔r➔a➔t➔e➔g➔y➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔r➔u➔n➔O➔n➔c➔e➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔e➔p➔l➔o➔y➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔s➔c➔r➔i➔p➔t➔:➔ ➔e➔c➔h➔o➔ ➔"➔D➔e➔p➔l➔o➔y➔i➔n➔g➔ ➔t➔o➔ ➔P➔r➔o➔d➔u➔c➔t➔i➔o➔n➔"➔
➔P➔o➔o➔l➔ ➔A➔s➔s➔i➔g➔n➔m➔e➔n➔t➔ ➔R➔u➔l➔e➔s➔
➔S➔t➔a➔g➔e➔-➔l➔e➔v➔e➔l➔ ➔p➔o➔o➔l➔ ➔→➔ ➔a➔l➔l➔ ➔j➔o➔b➔s➔ ➔i➔n➔h➔e➔r➔i➔t➔ ➔i➔t➔
➔J➔o➔b➔-➔l➔e➔v➔e➔l➔ ➔p➔o➔o➔l➔ ➔→➔ ➔o➔v➔e➔r➔r➔i➔d➔e➔s➔ ➔s➔t➔a➔g➔e➔ ➔p➔o➔o➔l➔
➔S➔t➔a➔g➔e➔ ➔P➔o➔o➔l➔ ➔(➔U➔b➔u➔n➔t➔u➔)➔
➔ ➔ ➔ ➔↓➔
➔J➔o➔b➔1➔ ➔(➔U➔b➔u➔n➔t➔u➔ ➔—➔ ➔i➔n➔h➔e➔r➔i➔t➔e➔d➔)➔
➔J➔o➔b➔2➔ ➔(➔W➔i➔n➔d➔o➔w➔s➔ ➔—➔ ➔o➔v➔e➔r➔r➔i➔d➔d➔e➔n➔ ➔a➔t➔ ➔j➔o➔b➔ ➔l➔e➔v➔e➔l➔)➔
➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔s➔
➔#➔ ➔I➔n➔l➔i➔n➔e➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔
➔v➔a➔r➔i➔a➔b➔l➔e➔s➔:➔
➔ ➔ ➔a➔p➔p➔N➔a➔m➔e➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔b➔u➔i➔l➔d➔C➔o➔n➔f➔i➔g➔:➔ ➔R➔e➔l➔e➔a➔s➔e➔
➔ ➔ ➔t➔a➔g➔:➔ ➔$➔(➔B➔u➔i➔l➔d➔.➔B➔u➔i➔l➔d➔I➔d➔)➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔b➔u➔i➔l➔t➔-➔i➔n➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔
➔
➔
➔
➔
➔#➔ ➔R➔e➔f➔e➔r➔e➔n➔c➔e➔
➔s➔t➔e➔p➔s➔:➔
➔-➔ ➔s➔c➔r➔i➔p➔t➔:➔ ➔e➔c➔h➔o➔ ➔B➔u➔i➔l➔d➔i➔n➔g➔ ➔$➔(➔a➔p➔p➔N➔a➔m➔e➔)➔ ➔v➔e➔r➔s➔i➔o➔n➔ ➔$➔(➔t➔a➔g➔)➔
➔B➔u➔i➔l➔t➔-➔i➔n➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔s➔:➔
➔V➔a➔r➔i➔a➔b➔l➔e➔ ➔V➔a➔l➔u➔e➔
➔$➔(➔B➔u➔i➔l➔d➔.➔B➔u➔i➔l➔d➔I➔d➔)➔ ➔U➔n➔i➔q➔u➔e➔ ➔b➔u➔i➔l➔d➔ ➔I➔D➔
➔$➔(➔B➔u➔i➔l➔d➔.➔B➔u➔i➔l➔d➔N➔u➔m➔b➔e➔r➔)➔ ➔H➔u➔m➔a➔n➔-➔r➔e➔a➔d➔a➔b➔l➔e➔ ➔b➔u➔i➔l➔d➔ ➔n➔u➔m➔b➔e➔r➔
➔$➔(➔B➔u➔i➔l➔d➔.➔S➔o➔u➔r➔c➔e➔B➔r➔a➔n➔c➔h➔)➔ ➔B➔r➔a➔n➔c➔h➔ ➔t➔h➔a➔t➔ ➔t➔r➔i➔g➔g➔e➔r➔e➔d➔ ➔(➔r➔e➔f➔s➔/➔h➔e➔a➔d➔s➔/➔m➔a➔i➔n➔)➔
➔$➔(➔B➔u➔i➔l➔d➔.➔A➔r➔t➔i➔f➔a➔c➔t➔S➔t➔a➔g➔i➔n➔g➔D➔i➔r➔e➔c➔t➔o➔r➔y➔)➔ ➔T➔e➔m➔p➔ ➔f➔o➔l➔d➔e➔r➔ ➔f➔o➔r➔ ➔b➔u➔i➔l➔d➔ ➔o➔u➔t➔p➔u➔t➔
➔$➔(➔S➔y➔s➔t➔e➔m➔.➔D➔e➔f➔a➔u➔l➔t➔W➔o➔r➔k➔i➔n➔g➔D➔i➔r➔e➔c➔t➔o➔r➔y➔)➔ ➔R➔o➔o➔t➔ ➔f➔o➔l➔d➔e➔r➔ ➔w➔h➔e➔r➔e➔ ➔c➔o➔d➔e➔ ➔i➔s➔ ➔c➔h➔e➔c➔k➔e➔d➔ ➔o➔u➔t➔
➔$➔(➔A➔g➔e➔n➔t➔.➔O➔S➔)➔ ➔O➔S➔ ➔o➔f➔ ➔a➔g➔e➔n➔t➔ ➔(➔L➔i➔n➔u➔x➔,➔ ➔W➔i➔n➔d➔o➔w➔s➔_➔N➔T➔)➔
➔V➔a➔r➔i➔a➔b➔l➔e➔ ➔G➔r➔o➔u➔p➔s➔ ➔a➔n➔d➔ ➔S➔e➔c➔r➔e➔t➔s➔
➔#➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔ ➔G➔r➔o➔u➔p➔ ➔(➔r➔e➔u➔s➔a➔b➔l➔e➔ ➔a➔c➔r➔o➔s➔s➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔s➔)➔
➔#➔ ➔C➔r➔e➔a➔t➔e➔:➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔s➔ ➔→➔ ➔L➔i➔b➔r➔a➔r➔y➔ ➔→➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔ ➔G➔r➔o➔u➔p➔ ➔→➔ ➔S➔h➔a➔r➔e➔d➔C➔o➔n➔f➔i➔g➔
➔v➔a➔r➔i➔a➔b➔l➔e➔s➔:➔
➔-➔ ➔g➔r➔o➔u➔p➔:➔ ➔S➔h➔a➔r➔e➔d➔C➔o➔n➔f➔i➔g➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔f➔e➔r➔e➔n➔c➔e➔ ➔g➔r➔o➔u➔p➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔b➔u➔i➔l➔d➔C➔o➔n➔f➔i➔g➔
➔ ➔ ➔v➔a➔l➔u➔e➔:➔ ➔R➔e➔l➔e➔a➔s➔e➔
➔#➔ ➔S➔e➔c➔r➔e➔t➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔ ➔—➔ ➔e➔n➔c➔r➔y➔p➔t➔e➔d➔,➔ ➔s➔h➔o➔w➔s➔ ➔*➔*➔*➔ ➔i➔n➔ ➔l➔o➔g➔s➔
➔#➔ ➔A➔d➔d➔ ➔i➔n➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔U➔I➔ ➔→➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔s➔ ➔t➔a➔b➔ ➔→➔ ➔l➔o➔c➔k➔ ➔i➔c➔o➔n➔
➔#➔ ➔R➔e➔f➔e➔r➔e➔n➔c➔e➔ ➔s➔a➔m➔e➔ ➔w➔a➔y➔:➔ ➔$➔(➔M➔y➔S➔e➔c➔r➔e➔t➔)➔
➔E➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔s➔ ➔a➔n➔d➔ ➔A➔p➔p➔r➔o➔v➔a➔l➔s➔
➔#➔ ➔C➔r➔e➔a➔t➔e➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔s➔:➔
➔P➔i➔p➔e➔l➔i➔n➔e➔s➔ ➔→➔ ➔E➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔s➔ ➔→➔ ➔N➔e➔w➔ ➔E➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔→➔ ➔P➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔#➔ ➔A➔d➔d➔ ➔a➔p➔p➔r➔o➔v➔a➔l➔:➔
➔E➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔→➔ ➔.➔.➔.➔ ➔→➔ ➔A➔p➔p➔r➔o➔v➔a➔l➔s➔ ➔a➔n➔d➔ ➔C➔h➔e➔c➔k➔s➔ ➔→➔ ➔A➔p➔p➔r➔o➔v➔a➔l➔ ➔→➔ ➔a➔s➔s➔i➔g➔n➔ ➔a➔p➔p➔r➔o➔v➔e➔r➔s➔
➔
➔
➔
➔
➔#➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔p➔a➔u➔s➔e➔s➔ ➔a➔t➔ ➔t➔h➔a➔t➔ ➔s➔t➔a➔g➔e➔,➔ ➔s➔e➔n➔d➔s➔ ➔e➔m➔a➔i➔l➔ ➔t➔o➔ ➔a➔p➔p➔r➔o➔v➔e➔r➔s➔
➔#➔ ➔A➔p➔p➔r➔o➔v➔e➔r➔ ➔c➔l➔i➔c➔k➔s➔ ➔A➔p➔p➔r➔o➔v➔e➔ ➔o➔r➔ ➔R➔e➔j➔e➔c➔t➔
➔C➔o➔m➔p➔l➔e➔t➔e➔ ➔C➔I➔/➔C➔D➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔—➔ ➔D➔o➔c➔k➔e➔r➔ ➔+➔ ➔J➔e➔n➔k➔i➔n➔s➔ ➔s➔t➔y➔l➔e➔ ➔(➔Y➔o➔u➔r➔ ➔P➔r➔o➔j➔e➔c➔t➔ ➔C➔o➔n➔t➔e➔x➔t➔)➔
➔t➔r➔i➔g➔g➔e➔r➔:➔
➔-➔ ➔m➔a➔i➔n➔
➔p➔o➔o➔l➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔D➔e➔f➔a➔u➔l➔t➔
➔v➔a➔r➔i➔a➔b➔l➔e➔s➔:➔
➔ ➔ ➔I➔M➔A➔G➔E➔_➔N➔A➔M➔E➔:➔ ➔a➔k➔h➔i➔l➔/➔m➔y➔a➔p➔p➔
➔ ➔ ➔I➔M➔A➔G➔E➔_➔T➔A➔G➔:➔ ➔$➔(➔B➔u➔i➔l➔d➔.➔B➔u➔i➔l➔d➔I➔d➔)➔
➔s➔t➔a➔g➔e➔s➔:➔
➔-➔ ➔s➔t➔a➔g➔e➔:➔ ➔C➔l➔o➔n➔e➔
➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔C➔l➔o➔n➔e➔ ➔C➔o➔d➔e➔
➔ ➔ ➔j➔o➔b➔s➔:➔
➔ ➔ ➔-➔ ➔j➔o➔b➔:➔ ➔C➔l➔o➔n➔e➔J➔o➔b➔
➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔c➔h➔e➔c➔k➔o➔u➔t➔:➔ ➔s➔e➔l➔f➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔ ➔a➔u➔t➔o➔-➔c➔h➔e➔c➔k➔s➔ ➔o➔u➔t➔ ➔c➔o➔d➔e➔
➔-➔ ➔s➔t➔a➔g➔e➔:➔ ➔B➔u➔i➔l➔d➔
➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔B➔u➔i➔l➔d➔ ➔A➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔
➔ ➔ ➔d➔e➔p➔e➔n➔d➔s➔O➔n➔:➔ ➔C➔l➔o➔n➔e➔
➔ ➔ ➔j➔o➔b➔s➔:➔
➔ ➔ ➔-➔ ➔j➔o➔b➔:➔ ➔B➔u➔i➔l➔d➔J➔o➔b➔
➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔s➔c➔r➔i➔p➔t➔:➔ ➔|➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔n➔p➔m➔ ➔i➔n➔s➔t➔a➔l➔l➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔n➔p➔m➔ ➔r➔u➔n➔ ➔b➔u➔i➔l➔d➔
➔ ➔ ➔ ➔ ➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔'➔B➔u➔i➔l➔d➔ ➔C➔o➔d➔e➔'➔
➔-➔ ➔s➔t➔a➔g➔e➔:➔ ➔T➔e➔s➔t➔
➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔R➔u➔n➔ ➔T➔e➔s➔t➔s➔
➔ ➔ ➔d➔e➔p➔e➔n➔d➔s➔O➔n➔:➔ ➔B➔u➔i➔l➔d➔
➔ ➔ ➔j➔o➔b➔s➔:➔
➔ ➔ ➔-➔ ➔j➔o➔b➔:➔ ➔T➔e➔s➔t➔J➔o➔b➔
➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔s➔c➔r➔i➔p➔t➔:➔ ➔n➔p➔m➔ ➔t➔e➔s➔t➔
➔ ➔ ➔ ➔ ➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔'➔R➔u➔n➔ ➔U➔n➔i➔t➔ ➔T➔e➔s➔t➔s➔'➔
➔-➔ ➔s➔t➔a➔g➔e➔:➔ ➔D➔o➔c➔k➔e➔r➔B➔u➔i➔l➔d➔
➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔B➔u➔i➔l➔d➔ ➔D➔o➔c➔k➔e➔r➔ ➔I➔m➔a➔g➔e➔
➔ ➔ ➔d➔e➔p➔e➔n➔d➔s➔O➔n➔:➔ ➔T➔e➔s➔t➔
➔
➔
➔
➔
➔ ➔ ➔j➔o➔b➔s➔:➔
➔ ➔ ➔-➔ ➔j➔o➔b➔:➔ ➔D➔o➔c➔k➔e➔r➔J➔o➔b➔
➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔s➔c➔r➔i➔p➔t➔:➔ ➔|➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔ ➔b➔u➔i➔l➔d➔ ➔-➔t➔ ➔$➔(➔I➔M➔A➔G➔E➔_➔N➔A➔M➔E➔)➔:➔$➔(➔I➔M➔A➔G➔E➔_➔T➔A➔G➔)➔ ➔.➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔ ➔t➔a➔g➔ ➔$➔(➔I➔M➔A➔G➔E➔_➔N➔A➔M➔E➔)➔:➔$➔(➔I➔M➔A➔G➔E➔_➔T➔A➔G➔)➔ ➔$➔(➔I➔M➔A➔G➔E➔_➔N➔A➔M➔E➔)➔:➔l➔a➔t➔e➔s➔t➔
➔ ➔ ➔ ➔ ➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔'➔B➔u➔i➔l➔d➔ ➔D➔o➔c➔k➔e➔r➔ ➔I➔m➔a➔g➔e➔'➔
➔-➔ ➔s➔t➔a➔g➔e➔:➔ ➔D➔o➔c➔k➔e➔r➔P➔u➔s➔h➔
➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔P➔u➔s➔h➔ ➔t➔o➔ ➔R➔e➔g➔i➔s➔t➔r➔y➔
➔ ➔ ➔d➔e➔p➔e➔n➔d➔s➔O➔n➔:➔ ➔D➔o➔c➔k➔e➔r➔B➔u➔i➔l➔d➔
➔ ➔ ➔j➔o➔b➔s➔:➔
➔ ➔ ➔-➔ ➔j➔o➔b➔:➔ ➔P➔u➔s➔h➔J➔o➔b➔
➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔s➔c➔r➔i➔p➔t➔:➔ ➔|➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔ ➔l➔o➔g➔i➔n➔ ➔-➔u➔ ➔$➔(➔D➔O➔C➔K➔E➔R➔_➔U➔S➔E➔R➔)➔ ➔-➔p➔ ➔$➔(➔D➔O➔C➔K➔E➔R➔_➔P➔A➔S➔S➔)➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔ ➔p➔u➔s➔h➔ ➔$➔(➔I➔M➔A➔G➔E➔_➔N➔A➔M➔E➔)➔:➔$➔(➔I➔M➔A➔G➔E➔_➔T➔A➔G➔)➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔ ➔p➔u➔s➔h➔ ➔$➔(➔I➔M➔A➔G➔E➔_➔N➔A➔M➔E➔)➔:➔l➔a➔t➔e➔s➔t➔
➔ ➔ ➔ ➔ ➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔'➔P➔u➔s➔h➔ ➔D➔o➔c➔k➔e➔r➔ ➔I➔m➔a➔g➔e➔'➔
➔-➔ ➔s➔t➔a➔g➔e➔:➔ ➔D➔e➔p➔l➔o➔y➔
➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔D➔e➔p➔l➔o➔y➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔
➔ ➔ ➔d➔e➔p➔e➔n➔d➔s➔O➔n➔:➔ ➔D➔o➔c➔k➔e➔r➔P➔u➔s➔h➔
➔ ➔ ➔j➔o➔b➔s➔:➔
➔ ➔ ➔-➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔:➔ ➔D➔e➔p➔l➔o➔y➔J➔o➔b➔
➔ ➔ ➔ ➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔:➔ ➔P➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔ ➔ ➔ ➔ ➔s➔t➔r➔a➔t➔e➔g➔y➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔r➔u➔n➔O➔n➔c➔e➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔e➔p➔l➔o➔y➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔s➔c➔r➔i➔p➔t➔:➔ ➔|➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔ ➔s➔t➔o➔p➔ ➔m➔y➔a➔p➔p➔ ➔|➔|➔ ➔t➔r➔u➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔ ➔r➔m➔ ➔m➔y➔a➔p➔p➔ ➔|➔|➔ ➔t➔r➔u➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔ ➔p➔u➔l➔l➔ ➔$➔(➔I➔M➔A➔G➔E➔_➔N➔A➔M➔E➔)➔:➔$➔(➔I➔M➔A➔G➔E➔_➔T➔A➔G➔)➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔-➔n➔a➔m➔e➔ ➔m➔y➔a➔p➔p➔ ➔-➔p➔ ➔8➔0➔:➔3➔0➔0➔0➔ ➔$➔(➔I➔M➔A➔G➔E➔_➔N➔A➔M➔E➔)➔:➔$➔(➔I➔M➔A➔G➔E➔_➔T➔A➔G➔)➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔'➔D➔e➔p➔l➔o➔y➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔'➔
➔8➔.➔ ➔Y➔o➔u➔r➔ ➔P➔r➔o➔j➔e➔c➔t➔ ➔1➔ ➔—➔ ➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔ ➔C➔I➔/➔C➔D➔ ➔w➔i➔t➔h➔ ➔T➔o➔m➔c➔a➔t➔
➔W➔h➔a➔t➔ ➔y➔o➔u➔ ➔b➔u➔i➔l➔t➔:➔
➔D➔e➔p➔l➔o➔y➔ ➔a➔ ➔w➔e➔b➔ ➔a➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔ ➔t➔o➔ ➔A➔p➔a➔c➔h➔e➔ ➔T➔o➔m➔c➔a➔t➔ ➔u➔s➔i➔n➔g➔ ➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔ ➔s➔e➔l➔f➔-➔h➔o➔s➔t➔e➔d➔ ➔a➔g➔e➔n➔t➔.➔
➔A➔r➔c➔h➔i➔t➔e➔c➔t➔u➔r➔e➔:➔
➔
➔
➔
➔
➔➔ ➔➔
➔L➔o➔c➔a➔l➔ ➔C➔o➔d➔e➔
➔ ➔ ➔ ➔ ➔↓➔ ➔g➔i➔t➔ ➔p➔u➔s➔h➔
➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔ ➔R➔e➔p➔o➔ ➔(➔m➔a➔i➔n➔ ➔b➔r➔a➔n➔c➔h➔)➔
➔ ➔ ➔ ➔ ➔↓➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔t➔r➔i➔g➔g➔e➔r➔e➔d➔
➔S➔e➔l➔f➔-➔H➔o➔s➔t➔e➔d➔ ➔A➔g➔e➔n➔t➔ ➔(➔m➔y➔a➔g➔e➔n➔t➔ ➔o➔n➔ ➔A➔z➔u➔r➔e➔ ➔V➔M➔)➔
➔ ➔ ➔ ➔ ➔↓➔ ➔c➔o➔p➔y➔ ➔f➔i➔l➔e➔s➔
➔T➔o➔m➔c➔a➔t➔ ➔R➔O➔O➔T➔ ➔(➔w➔e➔b➔a➔p➔p➔s➔/➔R➔O➔O➔T➔/➔)➔
➔ ➔ ➔ ➔ ➔↓➔
➔W➔e➔b➔s➔i➔t➔e➔ ➔L➔I➔V➔E➔ ➔o➔n➔ ➔A➔z➔u➔r➔e➔ ➔V➔M➔
➔A➔p➔a➔c➔h➔e➔ ➔T➔o➔m➔c➔a➔t➔ ➔S➔e➔t➔u➔p➔ ➔o➔n➔ ➔A➔z➔u➔r➔e➔ ➔V➔M➔:➔
➔#➔ ➔S➔t➔e➔p➔ ➔1➔ ➔—➔ ➔I➔n➔s➔t➔a➔l➔l➔ ➔J➔a➔v➔a➔
➔s➔u➔d➔o➔ ➔a➔p➔t➔ ➔u➔p➔d➔a➔t➔e➔
➔s➔u➔d➔o➔ ➔a➔p➔t➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔o➔p➔e➔n➔j➔d➔k➔-➔1➔7➔-➔j➔d➔k➔ ➔-➔y➔
➔j➔a➔v➔a➔ ➔-➔v➔e➔r➔s➔i➔o➔n➔
➔#➔ ➔S➔t➔e➔p➔ ➔2➔ ➔—➔ ➔D➔o➔w➔n➔l➔o➔a➔d➔ ➔T➔o➔m➔c➔a➔t➔ ➔1➔1➔
➔c➔d➔ ➔/➔o➔p➔t➔
➔s➔u➔d➔o➔ ➔w➔g➔e➔t➔ ➔h➔t➔t➔p➔s➔:➔/➔/➔d➔o➔w➔n➔l➔o➔a➔d➔s➔.➔a➔p➔a➔c➔h➔e➔.➔o➔r➔g➔/➔t➔o➔m➔c➔a➔t➔/➔t➔o➔m➔c➔a➔t➔-➔1➔1➔/➔v➔1➔1➔.➔0➔.➔1➔8➔/➔b➔i➔n➔/➔a➔p➔a➔c➔h➔e➔-➔t➔o➔m➔c➔a➔t➔-➔1➔1➔
➔s➔u➔d➔o➔ ➔t➔a➔r➔ ➔-➔x➔v➔z➔f➔ ➔a➔p➔a➔c➔h➔e➔-➔t➔o➔m➔c➔a➔t➔-➔1➔1➔.➔0➔.➔1➔8➔.➔t➔a➔r➔.➔g➔z➔
➔s➔u➔d➔o➔ ➔m➔v➔ ➔a➔p➔a➔c➔h➔e➔-➔t➔o➔m➔c➔a➔t➔-➔1➔1➔.➔0➔.➔1➔8➔ ➔t➔o➔m➔c➔a➔t➔1➔1➔
➔#➔ ➔S➔t➔e➔p➔ ➔3➔ ➔—➔ ➔F➔i➔x➔ ➔P➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔
➔s➔u➔d➔o➔ ➔c➔h➔o➔w➔n➔ ➔-➔R➔ ➔a➔z➔u➔r➔e➔u➔s➔e➔r➔:➔a➔z➔u➔r➔e➔u➔s➔e➔r➔ ➔/➔o➔p➔t➔/➔t➔o➔m➔c➔a➔t➔1➔1➔
➔#➔ ➔S➔t➔e➔p➔ ➔4➔ ➔—➔ ➔G➔i➔v➔e➔ ➔E➔x➔e➔c➔u➔t➔e➔ ➔P➔e➔r➔m➔i➔s➔s➔i➔o➔n➔
➔c➔d➔ ➔/➔o➔p➔t➔/➔t➔o➔m➔c➔a➔t➔1➔1➔/➔b➔i➔n➔
➔c➔h➔m➔o➔d➔ ➔+➔x➔ ➔*➔.➔s➔h➔
➔#➔ ➔S➔t➔e➔p➔ ➔5➔ ➔—➔ ➔S➔t➔a➔r➔t➔ ➔T➔o➔m➔c➔a➔t➔
➔.➔/➔s➔t➔a➔r➔t➔u➔p➔.➔s➔h➔
➔s➔s➔ ➔-➔t➔u➔l➔n➔p➔ ➔|➔ ➔g➔r➔e➔p➔ ➔8➔0➔8➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔v➔e➔r➔i➔f➔y➔ ➔r➔u➔n➔n➔i➔n➔g➔ ➔o➔n➔ ➔p➔o➔r➔t➔ ➔8➔0➔8➔0➔
➔#➔ ➔S➔t➔e➔p➔ ➔6➔ ➔—➔ ➔O➔p➔e➔n➔ ➔A➔z➔u➔r➔e➔ ➔N➔e➔t➔w➔o➔r➔k➔ ➔R➔u➔l➔e➔
➔#➔ ➔A➔z➔u➔r➔e➔ ➔P➔o➔r➔t➔a➔l➔ ➔→➔ ➔V➔M➔ ➔→➔ ➔N➔e➔t➔w➔o➔r➔k➔i➔n➔g➔ ➔→➔ ➔A➔d➔d➔ ➔i➔n➔b➔o➔u➔n➔d➔ ➔r➔u➔l➔e➔
➔#➔ ➔P➔o➔r➔t➔:➔ ➔8➔0➔8➔0➔,➔ ➔P➔r➔o➔t➔o➔c➔o➔l➔:➔ ➔T➔C➔P➔,➔ ➔A➔c➔t➔i➔o➔n➔:➔ ➔A➔l➔l➔o➔w➔
➔#➔ ➔S➔t➔e➔p➔ ➔7➔ ➔—➔ ➔A➔c➔c➔e➔s➔s➔ ➔i➔n➔ ➔b➔r➔o➔w➔s➔e➔r➔
➔#➔ ➔h➔t➔t➔p➔:➔/➔/➔<➔V➔M➔_➔P➔U➔B➔L➔I➔C➔_➔I➔P➔>➔:➔8➔0➔8➔0➔
➔C➔h➔a➔n➔g➔e➔ ➔T➔o➔m➔c➔a➔t➔ ➔P➔o➔r➔t➔ ➔(➔8➔0➔8➔0➔ ➔→➔ ➔7➔7➔8➔9➔)➔:➔
➔
➔
➔
➔
➔n➔a➔n➔o➔ ➔/➔o➔p➔t➔/➔t➔o➔m➔c➔a➔t➔1➔1➔/➔c➔o➔n➔f➔/➔s➔e➔r➔v➔e➔r➔.➔x➔m➔l➔
➔#➔ ➔F➔i➔n➔d➔:➔ ➔<➔C➔o➔n➔n➔e➔c➔t➔o➔r➔ ➔p➔o➔r➔t➔=➔"➔8➔0➔8➔0➔"➔ ➔.➔.➔.➔ ➔/➔>➔
➔#➔ ➔C➔h➔a➔n➔g➔e➔ ➔t➔o➔:➔ ➔<➔C➔o➔n➔n➔e➔c➔t➔o➔r➔ ➔p➔o➔r➔t➔=➔"➔7➔7➔8➔9➔"➔ ➔.➔.➔.➔ ➔/➔>➔
➔#➔ ➔R➔e➔s➔t➔a➔r➔t➔
➔c➔d➔ ➔/➔o➔p➔t➔/➔t➔o➔m➔c➔a➔t➔1➔1➔/➔b➔i➔n➔
➔.➔/➔s➔h➔u➔t➔d➔o➔w➔n➔.➔s➔h➔ ➔&➔&➔ ➔s➔l➔e➔e➔p➔ ➔5➔ ➔&➔&➔ ➔.➔/➔s➔t➔a➔r➔t➔u➔p➔.➔s➔h➔
➔s➔s➔ ➔-➔t➔u➔l➔n➔p➔ ➔|➔ ➔g➔r➔e➔p➔ ➔7➔7➔8➔9➔
➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔f➔o➔r➔ ➔A➔u➔t➔o➔-➔D➔e➔p➔l➔o➔y➔ ➔t➔o➔ ➔T➔o➔m➔c➔a➔t➔:➔
➔t➔r➔i➔g➔g➔e➔r➔:➔
➔-➔ ➔m➔a➔i➔n➔
➔p➔o➔o➔l➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔D➔e➔f➔a➔u➔l➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔l➔f➔-➔h➔o➔s➔t➔e➔d➔ ➔a➔g➔e➔n➔t➔ ➔o➔n➔ ➔A➔z➔u➔r➔e➔ ➔V➔M➔
➔s➔t➔e➔p➔s➔:➔
➔-➔ ➔s➔c➔r➔i➔p➔t➔:➔ ➔|➔
➔ ➔ ➔ ➔ ➔c➔p➔ ➔i➔n➔d➔e➔x➔.➔h➔t➔m➔l➔ ➔/➔o➔p➔t➔/➔t➔o➔m➔c➔a➔t➔1➔1➔/➔w➔e➔b➔a➔p➔p➔s➔/➔R➔O➔O➔T➔/➔i➔n➔d➔e➔x➔.➔h➔t➔m➔l➔
➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔'➔D➔e➔p➔l➔o➔y➔ ➔t➔o➔ ➔T➔o➔m➔c➔a➔t➔'➔
➔C➔o➔m➔m➔o➔n➔ ➔E➔r➔r➔o➔r➔s➔ ➔a➔n➔d➔ ➔F➔i➔x➔e➔s➔:➔
➔E➔r➔r➔o➔r➔ ➔R➔e➔a➔s➔o➔n➔ ➔F➔i➔x➔
➔g➔z➔i➔p➔:➔ ➔n➔o➔t➔ ➔i➔n➔ ➔g➔z➔i➔p➔
➔f➔o➔r➔m➔a➔t➔
➔W➔r➔o➔n➔g➔ ➔d➔o➔w➔n➔l➔o➔a➔d➔ ➔U➔R➔L➔ ➔(➔H➔T➔M➔L➔
➔d➔o➔w➔n➔l➔o➔a➔d➔e➔d➔)➔
➔U➔s➔e➔ ➔c➔o➔r➔r➔e➔c➔t➔ ➔a➔p➔a➔c➔h➔e➔.➔o➔r➔g➔ ➔U➔R➔L➔
➔P➔e➔r➔m➔i➔s➔s➔i➔o➔n➔ ➔d➔e➔n➔i➔e➔d➔ ➔F➔i➔l➔e➔s➔ ➔o➔w➔n➔e➔d➔ ➔b➔y➔ ➔r➔o➔o➔t➔ ➔s➔u➔d➔o➔ ➔c➔h➔o➔w➔n➔ ➔-➔R➔ ➔a➔z➔u➔r➔e➔u➔s➔e➔r➔:➔a➔z➔u➔r➔e➔u➔s➔e➔r➔
➔/➔o➔p➔t➔/➔t➔o➔m➔c➔a➔t➔1➔1➔
➔4➔0➔3➔ ➔A➔c➔c➔e➔s➔s➔ ➔D➔e➔n➔i➔e➔d➔ ➔T➔o➔m➔c➔a➔t➔ ➔a➔l➔l➔o➔w➔s➔ ➔l➔o➔c➔a➔l➔h➔o➔s➔t➔ ➔o➔n➔l➔y➔ ➔R➔e➔m➔o➔v➔e➔ ➔R➔e➔m➔o➔t➔e➔A➔d➔d➔r➔V➔a➔l➔v➔e➔ ➔f➔r➔o➔m➔ ➔c➔o➔n➔t➔e➔x➔t➔.➔x➔m➔l➔
➔4➔0➔4➔ ➔N➔o➔t➔ ➔F➔o➔u➔n➔d➔ ➔P➔a➔g➔e➔ ➔d➔o➔e➔s➔n➔'➔t➔ ➔e➔x➔i➔s➔t➔ ➔C➔h➔e➔c➔k➔ ➔f➔i➔l➔e➔ ➔i➔s➔ ➔i➔n➔ ➔c➔o➔r➔r➔e➔c➔t➔ ➔w➔e➔b➔a➔p➔p➔s➔ ➔f➔o➔l➔d➔e➔r➔
➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔n➔o➔t➔
➔t➔r➔i➔g➔g➔e➔r➔i➔n➔g➔
➔P➔u➔s➔h➔ ➔t➔o➔ ➔w➔r➔o➔n➔g➔ ➔b➔r➔a➔n➔c➔h➔ ➔C➔h➔e➔c➔k➔ ➔t➔r➔i➔g➔g➔e➔r➔ ➔i➔s➔ ➔m➔a➔i➔n➔ ➔,➔ ➔p➔u➔s➔h➔ ➔t➔o➔ ➔m➔a➔i➔n➔
➔P➔o➔o➔l➔ ➔n➔o➔t➔ ➔f➔o➔u➔n➔d➔ ➔U➔s➔i➔n➔g➔ ➔a➔g➔e➔n➔t➔ ➔n➔a➔m➔e➔ ➔n➔o➔t➔ ➔p➔o➔o➔l➔
➔n➔a➔m➔e➔
➔U➔s➔e➔ ➔p➔o➔o➔l➔:➔ ➔n➔a➔m➔e➔:➔ ➔D➔e➔f➔a➔u➔l➔t➔
➔G➔i➔t➔ ➔a➔u➔t➔h➔ ➔f➔a➔i➔l➔e➔d➔ ➔P➔a➔s➔s➔w➔o➔r➔d➔ ➔a➔u➔t➔h➔ ➔b➔l➔o➔c➔k➔e➔d➔ ➔U➔s➔e➔ ➔P➔A➔T➔ ➔a➔s➔ ➔p➔a➔s➔s➔w➔o➔r➔d➔
➔
➔
➔
➔
➔G➔i➔t➔ ➔W➔o➔r➔k➔f➔l➔o➔w➔ ➔f➔o➔r➔ ➔Y➔o➔u➔r➔ ➔P➔r➔o➔j➔e➔c➔t➔:➔
➔g➔i➔t➔ ➔b➔r➔a➔n➔c➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔e➔c➔k➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔b➔r➔a➔n➔c➔h➔
➔g➔i➔t➔ ➔s➔t➔a➔t➔u➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔e➔c➔k➔ ➔c➔h➔a➔n➔g➔e➔s➔
➔g➔i➔t➔ ➔a➔d➔d➔ ➔.➔
➔g➔i➔t➔ ➔c➔o➔m➔m➔i➔t➔ ➔-➔m➔ ➔"➔u➔p➔d➔a➔t➔e➔d➔ ➔f➔i➔l➔e➔s➔"➔
➔g➔i➔t➔ ➔p➔u➔s➔h➔ ➔o➔r➔i➔g➔i➔n➔ ➔m➔a➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔u➔s➔h➔ ➔t➔o➔ ➔t➔r➔i➔g➔g➔e➔r➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔
➔#➔ ➔I➔f➔ ➔o➔n➔ ➔f➔e➔a➔t➔u➔r➔e➔ ➔b➔r➔a➔n➔c➔h➔,➔ ➔m➔e➔r➔g➔e➔ ➔t➔o➔ ➔m➔a➔i➔n➔ ➔f➔i➔r➔s➔t➔:➔
➔g➔i➔t➔ ➔c➔h➔e➔c➔k➔o➔u➔t➔ ➔m➔a➔i➔n➔
➔g➔i➔t➔ ➔p➔u➔l➔l➔ ➔o➔r➔i➔g➔i➔n➔ ➔m➔a➔i➔n➔
➔g➔i➔t➔ ➔m➔e➔r➔g➔e➔ ➔f➔e➔a➔t➔u➔r➔e➔
➔g➔i➔t➔ ➔p➔u➔s➔h➔ ➔o➔r➔i➔g➔i➔n➔ ➔m➔a➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔n➔o➔w➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔t➔r➔i➔g➔g➔e➔r➔s➔
➔9➔.➔ ➔Y➔o➔u➔r➔ ➔P➔r➔o➔j➔e➔c➔t➔ ➔2➔ ➔—➔ ➔M➔u➔l➔t➔i➔-➔P➔o➔r➔t➔ ➔R➔e➔v➔e➔r➔s➔e➔ ➔P➔r➔o➔x➔y➔ ➔w➔i➔t➔h➔ ➔L➔G➔T➔M➔ ➔M➔o➔n➔i➔t➔o➔r➔i➔n➔g➔
➔W➔h➔a➔t➔ ➔y➔o➔u➔ ➔b➔u➔i➔l➔t➔:➔
➔M➔u➔l➔t➔i➔p➔l➔e➔ ➔T➔o➔m➔c➔a➔t➔ ➔i➔n➔s➔t➔a➔n➔c➔e➔s➔ ➔b➔e➔h➔i➔n➔d➔ ➔A➔p➔a➔c➔h➔e➔ ➔R➔e➔v➔e➔r➔s➔e➔ ➔P➔r➔o➔x➔y➔ ➔w➔i➔t➔h➔ ➔L➔G➔T➔M➔ ➔s➔t➔a➔c➔k➔ ➔m➔o➔n➔i➔t➔o➔r➔i➔n➔g➔.➔
➔A➔r➔c➔h➔i➔t➔e➔c➔t➔u➔r➔e➔:➔
➔I➔n➔t➔e➔r➔n➔e➔t➔ ➔(➔P➔o➔r➔t➔ ➔8➔0➔)➔
➔ ➔ ➔ ➔ ➔↓➔
➔A➔p➔a➔c➔h➔e➔ ➔H➔T➔T➔P➔ ➔S➔e➔r➔v➔e➔r➔ ➔(➔R➔e➔v➔e➔r➔s➔e➔ ➔P➔r➔o➔x➔y➔)➔
➔ ➔ ➔ ➔ ➔├➔─➔─➔ ➔/➔p➔r➔o➔j➔e➔c➔t➔1➔ ➔→➔ ➔T➔o➔m➔c➔a➔t➔ ➔I➔n➔s➔t➔a➔n➔c➔e➔ ➔1➔ ➔(➔P➔o➔r➔t➔ ➔7➔7➔8➔9➔)➔
➔ ➔ ➔ ➔ ➔└➔─➔─➔ ➔/➔p➔r➔o➔j➔e➔c➔t➔2➔ ➔→➔ ➔T➔o➔m➔c➔a➔t➔ ➔I➔n➔s➔t➔a➔n➔c➔e➔ ➔2➔ ➔(➔P➔o➔r➔t➔ ➔8➔8➔8➔8➔)➔
➔A➔z➔u➔r➔e➔ ➔V➔M➔
➔├➔─➔─➔ ➔A➔p➔a➔c➔h➔e➔ ➔R➔e➔v➔e➔r➔s➔e➔ ➔P➔r➔o➔x➔y➔ ➔(➔P➔o➔r➔t➔ ➔8➔0➔)➔
➔├➔─➔─➔ ➔T➔o➔m➔c➔a➔t➔ ➔I➔n➔s➔t➔a➔n➔c➔e➔ ➔1➔ ➔(➔P➔o➔r➔t➔ ➔7➔7➔8➔9➔)➔
➔├➔─➔─➔ ➔T➔o➔m➔c➔a➔t➔ ➔I➔n➔s➔t➔a➔n➔c➔e➔ ➔2➔ ➔(➔P➔o➔r➔t➔ ➔8➔8➔8➔8➔)➔
➔├➔─➔─➔ ➔P➔r➔o➔m➔t➔a➔i➔l➔ ➔(➔L➔o➔g➔ ➔C➔o➔l➔l➔e➔c➔t➔o➔r➔)➔
➔├➔─➔─➔ ➔L➔o➔k➔i➔ ➔(➔L➔o➔g➔ ➔S➔t➔o➔r➔a➔g➔e➔,➔ ➔P➔o➔r➔t➔ ➔3➔1➔0➔0➔)➔
➔└➔─➔─➔ ➔G➔r➔a➔f➔a➔n➔a➔ ➔(➔V➔i➔s➔u➔a➔l➔i➔z➔a➔t➔i➔o➔n➔,➔ ➔P➔o➔r➔t➔ ➔3➔0➔0➔0➔)➔
➔T➔w➔o➔ ➔T➔o➔m➔c➔a➔t➔ ➔I➔n➔s➔t➔a➔n➔c➔e➔s➔ ➔S➔e➔t➔u➔p➔:➔
➔#➔ ➔C➔r➔e➔a➔t➔e➔ ➔t➔w➔o➔ ➔s➔e➔p➔a➔r➔a➔t➔e➔ ➔p➔h➔y➔s➔i➔c➔a➔l➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔i➔e➔s➔
➔c➔d➔ ➔/➔t➔m➔p➔
➔w➔g➔e➔t➔ ➔h➔t➔t➔p➔s➔:➔/➔/➔a➔r➔c➔h➔i➔v➔e➔.➔a➔p➔a➔c➔h➔e➔.➔o➔r➔g➔/➔d➔i➔s➔t➔/➔t➔o➔m➔c➔a➔t➔/➔t➔o➔m➔c➔a➔t➔-➔1➔1➔/➔v➔1➔1➔.➔0➔.➔1➔8➔/➔b➔i➔n➔/➔a➔p➔a➔c➔h➔e➔-➔t➔o➔m➔c➔a➔t➔-➔1➔1➔.➔0➔
➔t➔a➔r➔ ➔-➔x➔v➔f➔ ➔a➔p➔a➔c➔h➔e➔-➔t➔o➔m➔c➔a➔t➔-➔1➔1➔.➔0➔.➔1➔8➔.➔t➔a➔r➔.➔g➔z➔
➔
➔
➔
➔
➔➔ ➔➔
➔s➔u➔d➔o➔ ➔m➔v➔ ➔a➔p➔a➔c➔h➔e➔-➔t➔o➔m➔c➔a➔t➔-➔1➔1➔.➔0➔.➔1➔8➔ ➔/➔o➔p➔t➔/➔t➔o➔m➔c➔a➔t➔1➔
➔s➔u➔d➔o➔ ➔c➔p➔ ➔-➔r➔ ➔/➔o➔p➔t➔/➔t➔o➔m➔c➔a➔t➔1➔ ➔/➔o➔p➔t➔/➔t➔o➔m➔c➔a➔t➔2➔
➔s➔u➔d➔o➔ ➔c➔h➔o➔w➔n➔ ➔-➔R➔ ➔a➔z➔u➔r➔e➔u➔s➔e➔r➔:➔a➔z➔u➔r➔e➔u➔s➔e➔r➔ ➔/➔o➔p➔t➔/➔t➔o➔m➔c➔a➔t➔1➔ ➔/➔o➔p➔t➔/➔t➔o➔m➔c➔a➔t➔2➔
➔#➔ ➔C➔o➔n➔f➔i➔g➔u➔r➔e➔ ➔u➔n➔i➔q➔u➔e➔ ➔p➔o➔r➔t➔s➔ ➔i➔n➔ ➔s➔e➔r➔v➔e➔r➔.➔x➔m➔l➔:➔
➔#➔ ➔T➔o➔m➔c➔a➔t➔ ➔1➔:➔ ➔p➔o➔r➔t➔ ➔7➔7➔8➔9➔
➔#➔ ➔T➔o➔m➔c➔a➔t➔ ➔2➔:➔ ➔p➔o➔r➔t➔ ➔8➔8➔8➔8➔ ➔(➔a➔l➔s➔o➔ ➔c➔h➔a➔n➔g➔e➔ ➔s➔h➔u➔t➔d➔o➔w➔n➔ ➔p➔o➔r➔t➔ ➔t➔o➔ ➔8➔0➔0➔6➔,➔ ➔A➔J➔P➔ ➔t➔o➔ ➔8➔0➔1➔0➔)➔
➔#➔ ➔C➔r➔e➔a➔t➔e➔ ➔p➔r➔o➔j➔e➔c➔t➔ ➔f➔i➔l➔e➔s➔
➔m➔k➔d➔i➔r➔ ➔-➔p➔ ➔/➔o➔p➔t➔/➔p➔r➔o➔j➔e➔c➔t➔1➔ ➔/➔o➔p➔t➔/➔p➔r➔o➔j➔e➔c➔t➔2➔
➔e➔c➔h➔o➔ ➔"➔<➔h➔1➔>➔P➔r➔o➔j➔e➔c➔t➔ ➔1➔ ➔W➔o➔r➔k➔s➔<➔/➔h➔1➔>➔"➔ ➔>➔ ➔/➔o➔p➔t➔/➔p➔r➔o➔j➔e➔c➔t➔1➔/➔i➔n➔d➔e➔x➔.➔h➔t➔m➔l➔
➔e➔c➔h➔o➔ ➔"➔<➔h➔1➔>➔P➔r➔o➔j➔e➔c➔t➔ ➔2➔ ➔W➔o➔r➔k➔s➔<➔/➔h➔1➔>➔"➔ ➔>➔ ➔/➔o➔p➔t➔/➔p➔r➔o➔j➔e➔c➔t➔2➔/➔i➔n➔d➔e➔x➔.➔h➔t➔m➔l➔
➔#➔ ➔L➔i➔n➔k➔ ➔t➔o➔ ➔T➔o➔m➔c➔a➔t➔ ➔w➔e➔b➔a➔p➔p➔s➔
➔l➔n➔ ➔-➔s➔ ➔/➔o➔p➔t➔/➔p➔r➔o➔j➔e➔c➔t➔1➔ ➔/➔o➔p➔t➔/➔t➔o➔m➔c➔a➔t➔1➔/➔w➔e➔b➔a➔p➔p➔s➔/➔p➔r➔o➔j➔e➔c➔t➔1➔
➔l➔n➔ ➔-➔s➔ ➔/➔o➔p➔t➔/➔p➔r➔o➔j➔e➔c➔t➔2➔ ➔/➔o➔p➔t➔/➔t➔o➔m➔c➔a➔t➔2➔/➔w➔e➔b➔a➔p➔p➔s➔/➔p➔r➔o➔j➔e➔c➔t➔2➔
➔#➔ ➔S➔t➔a➔r➔t➔ ➔b➔o➔t➔h➔
➔/➔o➔p➔t➔/➔t➔o➔m➔c➔a➔t➔1➔/➔b➔i➔n➔/➔s➔t➔a➔r➔t➔u➔p➔.➔s➔h➔
➔/➔o➔p➔t➔/➔t➔o➔m➔c➔a➔t➔2➔/➔b➔i➔n➔/➔s➔t➔a➔r➔t➔u➔p➔.➔s➔h➔
➔A➔p➔a➔c➔h➔e➔ ➔R➔e➔v➔e➔r➔s➔e➔ ➔P➔r➔o➔x➔y➔ ➔C➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔:➔
➔#➔ ➔E➔n➔a➔b➔l➔e➔ ➔m➔o➔d➔u➔l➔e➔s➔
➔s➔u➔d➔o➔ ➔a➔2➔e➔n➔m➔o➔d➔ ➔p➔r➔o➔x➔y➔ ➔p➔r➔o➔x➔y➔_➔h➔t➔t➔p➔
➔#➔ ➔C➔r➔e➔a➔t➔e➔ ➔c➔o➔n➔f➔i➔g➔
➔s➔u➔d➔o➔ ➔n➔a➔n➔o➔ ➔/➔e➔t➔c➔/➔a➔p➔a➔c➔h➔e➔2➔/➔s➔i➔t➔e➔s➔-➔a➔v➔a➔i➔l➔a➔b➔l➔e➔/➔m➔y➔-➔p➔r➔o➔x➔y➔.➔c➔o➔n➔f➔
➔<➔V➔i➔r➔t➔u➔a➔l➔H➔o➔s➔t➔ ➔*➔:➔8➔0➔>➔
➔ ➔ ➔ ➔ ➔P➔r➔o➔x➔y➔P➔r➔e➔s➔e➔r➔v➔e➔H➔o➔s➔t➔ ➔O➔n➔
➔ ➔ ➔ ➔ ➔#➔ ➔R➔o➔u➔t➔e➔ ➔P➔r➔o➔j➔e➔c➔t➔ ➔1➔ ➔t➔o➔ ➔T➔o➔m➔c➔a➔t➔ ➔1➔
➔ ➔ ➔ ➔ ➔P➔r➔o➔x➔y➔P➔a➔s➔s➔ ➔/➔p➔r➔o➔j➔e➔c➔t➔1➔ ➔h➔t➔t➔p➔:➔/➔/➔1➔2➔7➔.➔0➔.➔0➔.➔1➔:➔7➔7➔8➔9➔/➔p➔r➔o➔j➔e➔c➔t➔1➔
➔ ➔ ➔ ➔ ➔P➔r➔o➔x➔y➔P➔a➔s➔s➔R➔e➔v➔e➔r➔s➔e➔ ➔/➔p➔r➔o➔j➔e➔c➔t➔1➔ ➔h➔t➔t➔p➔:➔/➔/➔1➔2➔7➔.➔0➔.➔0➔.➔1➔:➔7➔7➔8➔9➔/➔p➔r➔o➔j➔e➔c➔t➔1➔
➔ ➔ ➔ ➔ ➔#➔ ➔R➔o➔u➔t➔e➔ ➔P➔r➔o➔j➔e➔c➔t➔ ➔2➔ ➔t➔o➔ ➔T➔o➔m➔c➔a➔t➔ ➔2➔
➔ ➔ ➔ ➔ ➔P➔r➔o➔x➔y➔P➔a➔s➔s➔ ➔/➔p➔r➔o➔j➔e➔c➔t➔2➔ ➔h➔t➔t➔p➔:➔/➔/➔1➔2➔7➔.➔0➔.➔0➔.➔1➔:➔8➔8➔8➔8➔/➔p➔r➔o➔j➔e➔c➔t➔2➔
➔ ➔ ➔ ➔ ➔P➔r➔o➔x➔y➔P➔a➔s➔s➔R➔e➔v➔e➔r➔s➔e➔ ➔/➔p➔r➔o➔j➔e➔c➔t➔2➔ ➔h➔t➔t➔p➔:➔/➔/➔1➔2➔7➔.➔0➔.➔0➔.➔1➔:➔8➔8➔8➔8➔/➔p➔r➔o➔j➔e➔c➔t➔2➔
➔ ➔ ➔ ➔ ➔E➔r➔r➔o➔r➔L➔o➔g➔ ➔$➔{➔A➔P➔A➔C➔H➔E➔_➔L➔O➔G➔_➔D➔I➔R➔}➔/➔p➔r➔o➔x➔y➔-➔e➔r➔r➔o➔r➔.➔l➔o➔g➔
➔<➔/➔V➔i➔r➔t➔u➔a➔l➔H➔o➔s➔t➔>➔
➔
➔
➔
➔
➔#➔ ➔E➔n➔a➔b➔l➔e➔ ➔a➔n➔d➔ ➔r➔e➔s➔t➔a➔r➔t➔
➔s➔u➔d➔o➔ ➔a➔2➔d➔i➔s➔s➔i➔t➔e➔ ➔0➔0➔0➔-➔d➔e➔f➔a➔u➔l➔t➔.➔c➔o➔n➔f➔
➔s➔u➔d➔o➔ ➔a➔2➔e➔n➔s➔i➔t➔e➔ ➔m➔y➔-➔p➔r➔o➔x➔y➔.➔c➔o➔n➔f➔
➔s➔u➔d➔o➔ ➔s➔y➔s➔t➔e➔m➔c➔t➔l➔ ➔r➔e➔s➔t➔a➔r➔t➔ ➔a➔p➔a➔c➔h➔e➔2➔
➔#➔ ➔T➔e➔s➔t➔
➔c➔u➔r➔l➔ ➔-➔I➔ ➔h➔t➔t➔p➔:➔/➔/➔l➔o➔c➔a➔l➔h➔o➔s➔t➔:➔7➔7➔8➔9➔/➔p➔r➔o➔j➔e➔c➔t➔1➔/➔
➔c➔u➔r➔l➔ ➔-➔I➔ ➔h➔t➔t➔p➔:➔/➔/➔l➔o➔c➔a➔l➔h➔o➔s➔t➔:➔8➔8➔8➔8➔/➔p➔r➔o➔j➔e➔c➔t➔2➔/➔
➔#➔ ➔P➔u➔b➔l➔i➔c➔:➔ ➔h➔t➔t➔p➔:➔/➔/➔<➔A➔z➔u➔r➔e➔-➔P➔u➔b➔l➔i➔c➔-➔I➔P➔>➔/➔p➔r➔o➔j➔e➔c➔t➔1➔/➔
➔L➔G➔T➔M➔ ➔S➔t➔a➔c➔k➔ ➔—➔ ➔M➔o➔n➔i➔t➔o➔r➔i➔n➔g➔ ➔S➔e➔t➔u➔p➔:➔
➔#➔ ➔O➔b➔s➔e➔r➔v➔a➔b➔i➔l➔i➔t➔y➔ ➔a➔n➔s➔w➔e➔r➔s➔ ➔3➔ ➔q➔u➔e➔s➔t➔i➔o➔n➔s➔:➔
➔#➔ ➔1➔.➔ ➔W➔h➔a➔t➔ ➔h➔a➔p➔p➔e➔n➔e➔d➔?➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔L➔O➔G➔S➔ ➔ ➔ ➔(➔L➔o➔k➔i➔)➔
➔#➔ ➔2➔.➔ ➔H➔o➔w➔ ➔i➔s➔ ➔s➔y➔s➔t➔e➔m➔ ➔p➔e➔r➔f➔o➔r➔m➔i➔n➔g➔?➔ ➔ ➔ ➔→➔ ➔M➔E➔T➔R➔I➔C➔S➔ ➔(➔M➔i➔m➔i➔r➔)➔
➔#➔ ➔3➔.➔ ➔H➔o➔w➔ ➔d➔i➔d➔ ➔r➔e➔q➔u➔e➔s➔t➔ ➔t➔r➔a➔v➔e➔l➔?➔ ➔ ➔ ➔ ➔ ➔→➔ ➔T➔R➔A➔C➔E➔S➔ ➔ ➔(➔T➔e➔m➔p➔o➔)➔
➔#➔ ➔4➔.➔ ➔H➔o➔w➔ ➔t➔o➔ ➔v➔i➔s➔u➔a➔l➔i➔z➔e➔ ➔a➔l➔l➔ ➔t➔h➔i➔s➔?➔ ➔ ➔→➔ ➔G➔r➔a➔f➔a➔n➔a➔
➔#➔ ➔F➔l➔o➔w➔:➔
➔A➔p➔a➔c➔h➔e➔/➔T➔o➔m➔c➔a➔t➔ ➔→➔ ➔l➔o➔g➔s➔ ➔→➔ ➔P➔r➔o➔m➔t➔a➔i➔l➔ ➔→➔ ➔L➔o➔k➔i➔ ➔→➔ ➔G➔r➔a➔f➔a➔n➔a➔
➔#➔ ➔I➔n➔s➔t➔a➔l➔l➔ ➔G➔r➔a➔f➔a➔n➔a➔
➔s➔u➔d➔o➔ ➔a➔p➔t➔-➔g➔e➔t➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔-➔y➔ ➔a➔p➔t➔-➔t➔r➔a➔n➔s➔p➔o➔r➔t➔-➔h➔t➔t➔p➔s➔ ➔s➔o➔f➔t➔w➔a➔r➔e➔-➔p➔r➔o➔p➔e➔r➔t➔i➔e➔s➔-➔c➔o➔m➔m➔o➔n➔ ➔w➔g➔e➔t➔
➔w➔g➔e➔t➔ ➔-➔q➔ ➔-➔O➔ ➔-➔ ➔h➔t➔t➔p➔s➔:➔/➔/➔a➔p➔t➔.➔g➔r➔a➔f➔a➔n➔a➔.➔c➔o➔m➔/➔g➔p➔g➔.➔k➔e➔y➔ ➔|➔ ➔g➔p➔g➔ ➔-➔-➔d➔e➔a➔r➔m➔o➔r➔ ➔|➔ ➔s➔u➔d➔o➔ ➔t➔e➔e➔ ➔/➔e➔t➔c➔/➔a➔p➔t➔/➔k➔e➔y➔r➔i➔
➔e➔c➔h➔o➔ ➔"➔d➔e➔b➔ ➔[➔s➔i➔g➔n➔e➔d➔-➔b➔y➔=➔/➔e➔t➔c➔/➔a➔p➔t➔/➔k➔e➔y➔r➔i➔n➔g➔s➔/➔g➔r➔a➔f➔a➔n➔a➔.➔g➔p➔g➔]➔ ➔h➔t➔t➔p➔s➔:➔/➔/➔a➔p➔t➔.➔g➔r➔a➔f➔a➔n➔a➔.➔c➔o➔m➔ ➔s➔t➔a➔b➔l➔e➔ ➔m➔a➔i➔
➔s➔u➔d➔o➔ ➔a➔p➔t➔-➔g➔e➔t➔ ➔u➔p➔d➔a➔t➔e➔ ➔&➔&➔ ➔s➔u➔d➔o➔ ➔a➔p➔t➔-➔g➔e➔t➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔-➔y➔ ➔g➔r➔a➔f➔a➔n➔a➔
➔s➔u➔d➔o➔ ➔s➔y➔s➔t➔e➔m➔c➔t➔l➔ ➔e➔n➔a➔b➔l➔e➔ ➔g➔r➔a➔f➔a➔n➔a➔-➔s➔e➔r➔v➔e➔r➔ ➔&➔&➔ ➔s➔u➔d➔o➔ ➔s➔y➔s➔t➔e➔m➔c➔t➔l➔ ➔s➔t➔a➔r➔t➔ ➔g➔r➔a➔f➔a➔n➔a➔-➔s➔e➔r➔v➔e➔r➔
➔#➔ ➔I➔n➔s➔t➔a➔l➔l➔ ➔L➔o➔k➔i➔
➔s➔u➔d➔o➔ ➔m➔k➔d➔i➔r➔ ➔-➔p➔ ➔/➔o➔p➔t➔/➔l➔o➔k➔i➔ ➔&➔&➔ ➔c➔d➔ ➔/➔o➔p➔t➔/➔l➔o➔k➔i➔
➔s➔u➔d➔o➔ ➔c➔u➔r➔l➔ ➔-➔L➔ ➔-➔O➔ ➔h➔t➔t➔p➔s➔:➔/➔/➔g➔i➔t➔h➔u➔b➔.➔c➔o➔m➔/➔g➔r➔a➔f➔a➔n➔a➔/➔l➔o➔k➔i➔/➔r➔e➔l➔e➔a➔s➔e➔s➔/➔d➔o➔w➔n➔l➔o➔a➔d➔/➔v➔2➔.➔9➔.➔3➔/➔l➔o➔k➔i➔-➔l➔i➔n➔u➔x➔-➔a➔m➔
➔s➔u➔d➔o➔ ➔a➔p➔t➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔u➔n➔z➔i➔p➔ ➔-➔y➔ ➔&➔&➔ ➔s➔u➔d➔o➔ ➔u➔n➔z➔i➔p➔ ➔l➔o➔k➔i➔-➔l➔i➔n➔u➔x➔-➔a➔m➔d➔6➔4➔.➔z➔i➔p➔
➔s➔u➔d➔o➔ ➔c➔h➔m➔o➔d➔ ➔+➔x➔ ➔l➔o➔k➔i➔-➔l➔i➔n➔u➔x➔-➔a➔m➔d➔6➔4➔
➔s➔u➔d➔o➔ ➔m➔k➔d➔i➔r➔ ➔-➔p➔ ➔/➔t➔m➔p➔/➔l➔o➔k➔i➔/➔c➔h➔u➔n➔k➔s➔ ➔/➔t➔m➔p➔/➔l➔o➔k➔i➔/➔r➔u➔l➔e➔s➔
➔s➔u➔d➔o➔ ➔c➔h➔m➔o➔d➔ ➔-➔R➔ ➔7➔7➔7➔ ➔/➔t➔m➔p➔/➔l➔o➔k➔i➔
➔#➔ ➔I➔n➔s➔t➔a➔l➔l➔ ➔P➔r➔o➔m➔t➔a➔i➔l➔
➔s➔u➔d➔o➔ ➔c➔u➔r➔l➔ ➔-➔L➔ ➔-➔O➔ ➔h➔t➔t➔p➔s➔:➔/➔/➔g➔i➔t➔h➔u➔b➔.➔c➔o➔m➔/➔g➔r➔a➔f➔a➔n➔a➔/➔l➔o➔k➔i➔/➔r➔e➔l➔e➔a➔s➔e➔s➔/➔d➔o➔w➔n➔l➔o➔a➔d➔/➔v➔2➔.➔9➔.➔3➔/➔p➔r➔o➔m➔t➔a➔i➔l➔-➔l➔i➔n➔u➔
➔s➔u➔d➔o➔ ➔u➔n➔z➔i➔p➔ ➔p➔r➔o➔m➔t➔a➔i➔l➔-➔l➔i➔n➔u➔x➔-➔a➔m➔d➔6➔4➔.➔z➔i➔p➔
➔s➔u➔d➔o➔ ➔c➔h➔m➔o➔d➔ ➔+➔x➔ ➔p➔r➔o➔m➔t➔a➔i➔l➔-➔l➔i➔n➔u➔x➔-➔a➔m➔d➔6➔4➔
➔s➔u➔d➔o➔ ➔m➔v➔ ➔p➔r➔o➔m➔t➔a➔i➔l➔-➔l➔i➔n➔u➔x➔-➔a➔m➔d➔6➔4➔ ➔/➔u➔s➔r➔/➔l➔o➔c➔a➔l➔/➔b➔i➔n➔/➔p➔r➔o➔m➔t➔a➔i➔l➔
➔#➔ ➔S➔t➔a➔r➔t➔ ➔s➔e➔r➔v➔i➔c➔e➔s➔
➔s➔u➔d➔o➔ ➔/➔o➔p➔t➔/➔l➔o➔k➔i➔/➔l➔o➔k➔i➔-➔l➔i➔n➔u➔x➔-➔a➔m➔d➔6➔4➔ ➔-➔c➔o➔n➔f➔i➔g➔.➔f➔i➔l➔e➔=➔/➔e➔t➔c➔/➔l➔o➔k➔i➔/➔l➔o➔k➔i➔-➔c➔o➔n➔f➔i➔g➔.➔y➔a➔m➔l➔ ➔&➔
➔s➔u➔d➔o➔ ➔/➔u➔s➔r➔/➔l➔o➔c➔a➔l➔/➔b➔i➔n➔/➔p➔r➔o➔m➔t➔a➔i➔l➔ ➔-➔c➔o➔n➔f➔i➔g➔.➔f➔i➔l➔e➔=➔/➔e➔t➔c➔/➔l➔o➔k➔i➔/➔p➔r➔o➔m➔t➔a➔i➔l➔-➔c➔o➔n➔f➔i➔g➔.➔y➔a➔m➔l➔ ➔&➔
➔
➔
➔
➔
➔➔ ➔➔
➔#➔ ➔Q➔u➔i➔c➔k➔ ➔s➔t➔a➔r➔t➔ ➔a➔f➔t➔e➔r➔ ➔V➔M➔ ➔r➔e➔b➔o➔o➔t➔
➔s➔u➔d➔o➔ ➔s➔y➔s➔t➔e➔m➔c➔t➔l➔ ➔s➔t➔a➔r➔t➔ ➔g➔r➔a➔f➔a➔n➔a➔-➔s➔e➔r➔v➔e➔r➔
➔s➔u➔d➔o➔ ➔/➔o➔p➔t➔/➔l➔o➔k➔i➔/➔l➔o➔k➔i➔-➔l➔i➔n➔u➔x➔-➔a➔m➔d➔6➔4➔ ➔-➔c➔o➔n➔f➔i➔g➔.➔f➔i➔l➔e➔=➔/➔e➔t➔c➔/➔l➔o➔k➔i➔/➔l➔o➔k➔i➔-➔c➔o➔n➔f➔i➔g➔.➔y➔a➔m➔l➔ ➔&➔
➔s➔u➔d➔o➔ ➔/➔u➔s➔r➔/➔l➔o➔c➔a➔l➔/➔b➔i➔n➔/➔p➔r➔o➔m➔t➔a➔i➔l➔ ➔-➔c➔o➔n➔f➔i➔g➔.➔f➔i➔l➔e➔=➔/➔e➔t➔c➔/➔l➔o➔k➔i➔/➔p➔r➔o➔m➔t➔a➔i➔l➔-➔c➔o➔n➔f➔i➔g➔.➔y➔a➔m➔l➔ ➔&➔
➔#➔ ➔A➔c➔c➔e➔s➔s➔ ➔G➔r➔a➔f➔a➔n➔a➔
➔#➔ ➔h➔t➔t➔p➔:➔/➔/➔<➔V➔M➔-➔I➔P➔>➔:➔3➔0➔0➔0➔
➔#➔ ➔L➔o➔g➔i➔n➔:➔ ➔a➔d➔m➔i➔n➔ ➔/➔ ➔a➔d➔m➔i➔n➔
➔#➔ ➔A➔d➔d➔ ➔L➔o➔k➔i➔ ➔d➔a➔t➔a➔s➔o➔u➔r➔c➔e➔:➔ ➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔s➔ ➔→➔ ➔D➔a➔t➔a➔ ➔S➔o➔u➔r➔c➔e➔s➔ ➔→➔ ➔L➔o➔k➔i➔ ➔→➔ ➔U➔R➔L➔:➔ ➔h➔t➔t➔p➔:➔/➔/➔l➔o➔c➔a➔l➔h➔o➔s➔t➔:➔3➔1➔0➔0➔
➔1➔0➔.➔ ➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔ ➔K➔e➔y➔ ➔C➔o➔n➔c➔e➔p➔t➔s➔ ➔f➔o➔r➔ ➔I➔n➔t➔e➔r➔v➔i➔e➔w➔s➔
➔D➔O➔R➔A➔ ➔M➔e➔t➔r➔i➔c➔s➔ ➔(➔w➔h➔a➔t➔ ➔i➔n➔t➔e➔r➔v➔i➔e➔w➔e➔r➔s➔ ➔l➔o➔v➔e➔ ➔t➔o➔ ➔a➔s➔k➔)➔:➔
➔M➔e➔t➔r➔i➔c➔ ➔D➔e➔s➔c➔r➔i➔p➔t➔i➔o➔n➔ ➔E➔l➔i➔t➔e➔
➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔F➔r➔e➔q➔u➔e➔n➔c➔y➔ ➔H➔o➔w➔ ➔o➔f➔t➔e➔n➔ ➔y➔o➔u➔ ➔d➔e➔p➔l➔o➔y➔ ➔t➔o➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔M➔u➔l➔t➔i➔p➔l➔e➔ ➔t➔i➔m➔e➔s➔ ➔p➔e➔r➔ ➔d➔a➔y➔
➔L➔e➔a➔d➔ ➔T➔i➔m➔e➔ ➔f➔o➔r➔ ➔C➔h➔a➔n➔g➔e➔s➔ ➔C➔o➔m➔m➔i➔t➔ ➔t➔o➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔t➔i➔m➔e➔ ➔L➔e➔s➔s➔ ➔t➔h➔a➔n➔ ➔1➔ ➔h➔o➔u➔r➔
➔C➔h➔a➔n➔g➔e➔ ➔F➔a➔i➔l➔u➔r➔e➔ ➔R➔a➔t➔e➔ ➔%➔ ➔o➔f➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔s➔ ➔c➔a➔u➔s➔i➔n➔g➔ ➔i➔n➔c➔i➔d➔e➔n➔t➔s➔ ➔L➔e➔s➔s➔ ➔t➔h➔a➔n➔ ➔5➔%➔
➔M➔e➔a➔n➔ ➔T➔i➔m➔e➔ ➔t➔o➔ ➔R➔e➔s➔t➔o➔r➔e➔ ➔(➔M➔T➔T➔R➔)➔ ➔R➔e➔c➔o➔v➔e➔r➔y➔ ➔t➔i➔m➔e➔ ➔f➔r➔o➔m➔ ➔f➔a➔i➔l➔u➔r➔e➔ ➔L➔e➔s➔s➔ ➔t➔h➔a➔n➔ ➔1➔ ➔h➔o➔u➔r➔
➔D➔e➔v➔O➔p➔s➔ ➔v➔s➔ ➔T➔r➔a➔d➔i➔t➔i➔o➔n➔a➔l➔ ➔(➔W➔a➔t➔e➔r➔f➔a➔l➔l➔)➔:➔
➔W➔a➔t➔e➔r➔f➔a➔l➔l➔ ➔D➔e➔v➔O➔p➔s➔
➔R➔e➔l➔e➔a➔s➔e➔ ➔c➔y➔c➔l➔e➔ ➔6➔-➔1➔2➔ ➔m➔o➔n➔t➔h➔s➔ ➔H➔o➔u➔r➔s➔ ➔t➔o➔ ➔d➔a➔y➔s➔
➔T➔e➔a➔m➔s➔ ➔S➔i➔l➔o➔e➔d➔ ➔D➔e➔v➔ ➔+➔ ➔O➔p➔s➔ ➔U➔n➔i➔f➔i➔e➔d➔
➔T➔e➔s➔t➔i➔n➔g➔ ➔E➔n➔d➔,➔ ➔m➔a➔n➔u➔a➔l➔ ➔C➔o➔n➔t➔i➔n➔u➔o➔u➔s➔,➔ ➔a➔u➔t➔o➔m➔a➔t➔e➔d➔
➔F➔a➔i➔l➔u➔r➔e➔ ➔r➔i➔s➔k➔ ➔V➔e➔r➔y➔ ➔h➔i➔g➔h➔ ➔L➔o➔w➔
➔I➔n➔t➔e➔r➔v➔i➔e➔w➔ ➔O➔n➔e➔-➔L➔i➔n➔e➔r➔s➔:➔
➔"➔A➔z➔u➔r➔e➔ ➔B➔o➔a➔r➔d➔s➔ ➔i➔s➔ ➔o➔u➔r➔ ➔p➔r➔o➔j➔e➔c➔t➔ ➔m➔a➔n➔a➔g➔e➔m➔e➔n➔t➔ ➔t➔o➔o➔l➔ ➔w➔h➔e➔r➔e➔ ➔w➔e➔ ➔t➔r➔a➔c➔k➔ ➔w➔o➔r➔k➔ ➔u➔s➔i➔n➔g➔ ➔E➔p➔i➔c➔s➔ ➔→➔ ➔F➔e➔a➔t➔u➔r➔e➔s➔ ➔→➔ ➔U➔s➔e➔r➔ ➔S➔t➔o➔r➔i➔e➔s➔
➔→➔ ➔T➔a➔s➔k➔s➔ ➔h➔i➔e➔r➔a➔r➔c➔h➔y➔.➔"➔
➔"➔W➔e➔ ➔u➔s➔e➔d➔ ➔s➔e➔l➔f➔-➔h➔o➔s➔t➔e➔d➔ ➔a➔g➔e➔n➔t➔s➔ ➔o➔n➔ ➔A➔z➔u➔r➔e➔ ➔V➔M➔s➔ ➔b➔e➔c➔a➔u➔s➔e➔ ➔w➔e➔ ➔n➔e➔e➔d➔e➔d➔ ➔d➔i➔r➔e➔c➔t➔ ➔a➔c➔c➔e➔s➔s➔ ➔t➔o➔ ➔T➔o➔m➔c➔a➔t➔ ➔d➔e➔p➔l➔o➔y➔e➔d➔ ➔o➔n➔ ➔t➔h➔e➔
➔s➔a➔m➔e➔ ➔V➔M➔.➔"➔
➔
➔
➔
➔
➔"➔P➔R➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔s➔ ➔s➔t➔a➔n➔d➔a➔r➔d➔i➔z➔e➔d➔ ➔o➔u➔r➔ ➔c➔o➔d➔e➔ ➔r➔e➔v➔i➔e➔w➔ ➔p➔r➔o➔c➔e➔s➔s➔ ➔b➔y➔ ➔e➔n➔s➔u➔r➔i➔n➔g➔ ➔e➔v➔e➔r➔y➔ ➔m➔e➔r➔g➔e➔ ➔w➔a➔s➔ ➔l➔i➔n➔k➔e➔d➔ ➔t➔o➔ ➔a➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔w➔o➔r➔k➔
➔i➔t➔e➔m➔.➔"➔
➔"➔W➔e➔ ➔i➔n➔t➔e➔g➔r➔a➔t➔e➔d➔ ➔t➔h➔e➔ ➔L➔G➔T➔M➔ ➔s➔t➔a➔c➔k➔ ➔—➔ ➔L➔o➔k➔i➔,➔ ➔G➔r➔a➔f➔a➔n➔a➔,➔ ➔T➔e➔m➔p➔o➔,➔ ➔M➔i➔m➔i➔r➔ ➔—➔ ➔t➔o➔ ➔m➔o➔n➔i➔t➔o➔r➔ ➔a➔u➔t➔o➔m➔a➔t➔i➔o➔n➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔
➔h➔e➔a➔l➔t➔h➔.➔"➔
➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔ ➔—➔ ➔A➔d➔v➔a➔n➔c➔e➔d➔ ➔T➔o➔p➔i➔c➔s➔
➔N➔e➔w➔ ➔c➔o➔n➔t➔e➔n➔t➔ ➔n➔o➔t➔ ➔c➔o➔v➔e➔r➔e➔d➔ ➔p➔r➔e➔v➔i➔o➔u➔s➔l➔y➔.➔ ➔A➔d➔d➔s➔ ➔A➔z➔u➔r➔e➔ ➔A➔r➔t➔i➔f➔a➔c➔t➔s➔,➔ ➔T➔e➔s➔t➔ ➔P➔l➔a➔n➔s➔,➔ ➔K➔e➔y➔ ➔V➔a➔u➔l➔t➔,➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔T➔e➔m➔p➔l➔a➔t➔e➔s➔,➔ ➔I➔a➔C➔
➔w➔i➔t➔h➔ ➔A➔R➔M➔/➔B➔i➔c➔e➔p➔,➔ ➔S➔e➔c➔u➔r➔i➔t➔y➔,➔ ➔M➔o➔n➔i➔t➔o➔r➔i➔n➔g➔,➔ ➔a➔n➔d➔ ➔A➔Z➔-➔4➔0➔0➔ ➔p➔r➔e➔p➔.➔
➔A➔.➔ ➔A➔z➔u➔r➔e➔ ➔A➔r➔t➔i➔f➔a➔c➔t➔s➔ ➔—➔ ➔P➔a➔c➔k➔a➔g➔e➔ ➔M➔a➔n➔a➔g➔e➔m➔e➔n➔t➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔A➔z➔u➔r➔e➔ ➔A➔r➔t➔i➔f➔a➔c➔t➔s➔?➔
➔A➔ ➔p➔a➔c➔k➔a➔g➔e➔ ➔m➔a➔n➔a➔g➔e➔m➔e➔n➔t➔ ➔s➔e➔r➔v➔i➔c➔e➔ ➔t➔h➔a➔t➔ ➔s➔t➔o➔r➔e➔s➔ ➔l➔i➔b➔r➔a➔r➔i➔e➔s➔ ➔y➔o➔u➔r➔ ➔c➔o➔d➔e➔ ➔d➔e➔p➔e➔n➔d➔s➔ ➔o➔n➔ ➔—➔ ➔n➔p➔m➔,➔ ➔N➔u➔G➔e➔t➔,➔ ➔M➔a➔v➔e➔n➔,➔ ➔P➔y➔P➔I➔ ➔—➔ ➔i➔n➔ ➔a➔
➔p➔r➔i➔v➔a➔t➔e➔,➔ ➔s➔e➔c➔u➔r➔e➔ ➔f➔e➔e➔d➔ ➔h➔o➔s➔t➔e➔d➔ ➔b➔y➔ ➔A➔z➔u➔r➔e➔.➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔ ➔P➔a➔c➔k➔a➔g➔e➔?➔
➔R➔e➔u➔s➔a➔b➔l➔e➔ ➔c➔o➔d➔e➔ ➔b➔u➔n➔d➔l➔e➔d➔ ➔a➔n➔d➔ ➔p➔u➔b➔l➔i➔s➔h➔e➔d➔ ➔s➔o➔ ➔o➔t➔h➔e➔r➔ ➔p➔r➔o➔j➔e➔c➔t➔s➔ ➔c➔a➔n➔ ➔d➔e➔p➔e➔n➔d➔ ➔o➔n➔ ➔i➔t➔.➔ ➔I➔n➔s➔t➔e➔a➔d➔ ➔o➔f➔ ➔c➔o➔p➔y➔i➔n➔g➔ ➔c➔o➔d➔e➔ ➔a➔c➔r➔o➔s➔s➔
➔p➔r➔o➔j➔e➔c➔t➔s➔,➔ ➔y➔o➔u➔ ➔p➔u➔b➔l➔i➔s➔h➔ ➔i➔t➔ ➔a➔s➔ ➔a➔ ➔p➔a➔c➔k➔a➔g➔e➔ ➔(➔e➔.➔g➔.➔ ➔v➔1➔.➔0➔.➔0➔)➔ ➔a➔n➔d➔ ➔r➔e➔f➔e➔r➔e➔n➔c➔e➔ ➔i➔t➔ ➔a➔s➔ ➔a➔ ➔d➔e➔p➔e➔n➔d➔e➔n➔c➔y➔.➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔ ➔F➔e➔e➔d➔?➔
➔A➔ ➔p➔r➔i➔v➔a➔t➔e➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔f➔o➔r➔ ➔y➔o➔u➔r➔ ➔p➔a➔c➔k➔a➔g➔e➔s➔.➔ ➔T➔h➔i➔n➔k➔ ➔o➔f➔ ➔i➔t➔ ➔a➔s➔ ➔y➔o➔u➔r➔ ➔o➔w➔n➔ ➔p➔r➔i➔v➔a➔t➔e➔ ➔n➔p➔m➔ ➔r➔e➔g➔i➔s➔t➔r➔y➔ ➔o➔r➔ ➔N➔u➔G➔e➔t➔ ➔g➔a➔l➔l➔e➔r➔y➔.➔
➔P➔a➔c➔k➔a➔g➔e➔ ➔T➔y➔p➔e➔s➔:➔
➔T➔y➔p➔e➔ ➔L➔a➔n➔g➔u➔a➔g➔e➔ ➔E➔x➔t➔e➔n➔s➔i➔o➔n➔
➔N➔u➔G➔e➔t➔ ➔.➔N➔E➔T➔ ➔/➔ ➔C➔#➔ ➔.➔n➔u➔p➔k➔g➔
➔n➔p➔m➔ ➔J➔a➔v➔a➔S➔c➔r➔i➔p➔t➔ ➔/➔ ➔N➔o➔d➔e➔.➔j➔s➔ ➔p➔a➔c➔k➔a➔g➔e➔.➔j➔s➔o➔n➔
➔M➔a➔v➔e➔n➔ ➔J➔a➔v➔a➔ ➔.➔j➔a➔r➔
➔P➔y➔P➔I➔ ➔P➔y➔t➔h➔o➔n➔ ➔.➔w➔h➔l➔
➔U➔n➔i➔v➔e➔r➔s➔a➔l➔ ➔A➔n➔y➔ ➔f➔i➔l➔e➔ ➔t➔y➔p➔e➔ ➔z➔i➔p➔,➔ ➔b➔i➔n➔a➔r➔y➔
➔
➔
➔
➔
➔➔ ➔➔
➔➔ ➔➔
➔C➔r➔e➔a➔t➔e➔ ➔a➔ ➔F➔e➔e➔d➔:➔
➔A➔r➔t➔i➔f➔a➔c➔t➔s➔ ➔→➔ ➔+➔ ➔C➔r➔e➔a➔t➔e➔ ➔F➔e➔e➔d➔ ➔→➔ ➔N➔a➔m➔e➔ ➔i➔t➔ ➔→➔ ➔S➔e➔t➔ ➔v➔i➔s➔i➔b➔i➔l➔i➔t➔y➔ ➔→➔ ➔A➔d➔d➔ ➔u➔p➔s➔t➔r➔e➔a➔m➔ ➔s➔o➔u➔r➔c➔e➔s➔ ➔→➔ ➔C➔r➔e➔a➔t➔e➔
➔U➔p➔s➔t➔r➔e➔a➔m➔ ➔S➔o➔u➔r➔c➔e➔s➔:➔
➔A➔ ➔f➔e➔e➔d➔ ➔c➔a➔n➔ ➔p➔r➔o➔x➔y➔ ➔p➔u➔b➔l➔i➔c➔ ➔r➔e➔g➔i➔s➔t➔r➔i➔e➔s➔ ➔l➔i➔k➔e➔ ➔n➔p➔m➔j➔s➔.➔c➔o➔m➔ ➔o➔r➔ ➔n➔u➔g➔e➔t➔.➔o➔r➔g➔.➔ ➔Y➔o➔u➔r➔ ➔t➔e➔a➔m➔ ➔f➔e➔t➔c➔h➔e➔s➔ ➔p➔a➔c➔k➔a➔g➔e➔s➔ ➔t➔h➔r➔o➔u➔g➔h➔ ➔y➔o➔u➔r➔ ➔A➔z➔u➔r➔e➔
➔A➔r➔t➔i➔f➔a➔c➔t➔s➔ ➔f➔e➔e➔d➔ ➔—➔ ➔p➔r➔o➔v➔i➔d➔i➔n➔g➔ ➔c➔a➔c➔h➔i➔n➔g➔,➔ ➔s➔e➔c➔u➔r➔i➔t➔y➔ ➔s➔c➔a➔n➔n➔i➔n➔g➔,➔ ➔a➔n➔d➔ ➔c➔o➔n➔t➔r➔o➔l➔.➔
➔C➔o➔m➔m➔a➔n➔d➔s➔:➔
➔#➔ ➔N➔u➔G➔e➔t➔
➔d➔o➔t➔n➔e➔t➔ ➔p➔a➔c➔k➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔.➔n➔u➔p➔k➔g➔ ➔f➔i➔l➔e➔
➔d➔o➔t➔n➔e➔t➔ ➔n➔u➔g➔e➔t➔ ➔p➔u➔s➔h➔ ➔*➔.➔n➔u➔p➔k➔g➔ ➔-➔-➔s➔o➔u➔r➔c➔e➔ ➔M➔y➔F➔e➔e➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔u➔s➔h➔ ➔t➔o➔ ➔A➔z➔u➔r➔e➔ ➔A➔r➔t➔i➔f➔a➔c➔t➔s➔
➔d➔o➔t➔n➔e➔t➔ ➔r➔e➔s➔t➔o➔r➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔o➔w➔n➔l➔o➔a➔d➔ ➔p➔a➔c➔k➔a➔g➔e➔s➔ ➔f➔r➔o➔m➔ ➔f➔e➔e➔d➔
➔#➔ ➔n➔p➔m➔
➔n➔p➔m➔ ➔p➔u➔b➔l➔i➔s➔h➔ ➔-➔-➔r➔e➔g➔i➔s➔t➔r➔y➔ ➔h➔t➔t➔p➔s➔:➔/➔/➔p➔k➔g➔s➔.➔d➔e➔v➔.➔a➔z➔u➔r➔e➔.➔c➔o➔m➔/➔Y➔o➔u➔r➔O➔r➔g➔/➔_➔p➔a➔c➔k➔a➔g➔i➔n➔g➔/➔M➔y➔F➔e➔e➔d➔/➔n➔p➔m➔/➔r➔e➔g➔i➔s➔t➔
➔S➔e➔m➔a➔n➔t➔i➔c➔ ➔V➔e➔r➔s➔i➔o➔n➔i➔n➔g➔:➔
➔M➔A➔J➔O➔R➔.➔M➔I➔N➔O➔R➔.➔P➔A➔T➔C➔H➔
➔1➔.➔0➔.➔0➔ ➔→➔ ➔2➔.➔0➔.➔0➔ ➔ ➔B➔r➔e➔a➔k➔i➔n➔g➔ ➔c➔h➔a➔n➔g➔e➔
➔1➔.➔0➔.➔0➔ ➔→➔ ➔1➔.➔1➔.➔0➔ ➔ ➔N➔e➔w➔ ➔f➔e➔a➔t➔u➔r➔e➔ ➔(➔b➔a➔c➔k➔w➔a➔r➔d➔ ➔c➔o➔m➔p➔a➔t➔i➔b➔l➔e➔)➔
➔1➔.➔0➔.➔0➔ ➔→➔ ➔1➔.➔0➔.➔1➔ ➔ ➔B➔u➔g➔ ➔f➔i➔x➔ ➔o➔n➔l➔y➔
➔R➔u➔l➔e➔:➔ ➔N➔e➔v➔e➔r➔ ➔o➔v➔e➔r➔w➔r➔i➔t➔e➔ ➔a➔n➔ ➔e➔x➔i➔s➔t➔i➔n➔g➔ ➔v➔e➔r➔s➔i➔o➔n➔.➔ ➔A➔l➔w➔a➔y➔s➔ ➔p➔u➔b➔l➔i➔s➔h➔ ➔a➔ ➔n➔e➔w➔ ➔o➔n➔e➔.➔
➔B➔.➔ ➔A➔z➔u➔r➔e➔ ➔T➔e➔s➔t➔ ➔P➔l➔a➔n➔s➔ ➔—➔ ➔M➔a➔n➔u➔a➔l➔ ➔T➔e➔s➔t➔i➔n➔g➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔A➔z➔u➔r➔e➔ ➔T➔e➔s➔t➔ ➔P➔l➔a➔n➔s➔?➔
➔A➔ ➔t➔e➔s➔t➔i➔n➔g➔ ➔m➔a➔n➔a➔g➔e➔m➔e➔n➔t➔ ➔t➔o➔o➔l➔ ➔t➔o➔ ➔c➔r➔e➔a➔t➔e➔ ➔t➔e➔s➔t➔ ➔c➔a➔s➔e➔s➔,➔ ➔o➔r➔g➔a➔n➔i➔z➔e➔ ➔t➔h➔e➔m➔ ➔i➔n➔t➔o➔ ➔t➔e➔s➔t➔ ➔s➔u➔i➔t➔e➔s➔,➔ ➔e➔x➔e➔c➔u➔t➔e➔ ➔t➔e➔s➔t➔s➔ ➔m➔a➔n➔u➔a➔l➔l➔y➔,➔ ➔a➔n➔d➔
➔t➔r➔a➔c➔k➔ ➔r➔e➔s➔u➔l➔t➔s➔ ➔—➔ ➔a➔l➔l➔ ➔l➔i➔n➔k➔e➔d➔ ➔t➔o➔ ➔y➔o➔u➔r➔ ➔w➔o➔r➔k➔ ➔i➔t➔e➔m➔s➔.➔
➔T➔e➔r➔m➔i➔n➔o➔l➔o➔g➔y➔:➔
➔T➔e➔r➔m➔ ➔M➔e➔a➔n➔i➔n➔g➔
➔T➔e➔s➔t➔ ➔P➔l➔a➔n➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔f➔o➔r➔ ➔a➔l➔l➔ ➔t➔e➔s➔t➔i➔n➔g➔ ➔i➔n➔ ➔a➔ ➔s➔p➔r➔i➔n➔t➔ ➔o➔r➔ ➔r➔e➔l➔e➔a➔s➔e➔
➔
➔
➔
➔
➔➔ ➔➔
➔T➔e➔s➔t➔ ➔S➔u➔i➔t➔e➔ ➔G➔r➔o➔u➔p➔ ➔o➔f➔ ➔r➔e➔l➔a➔t➔e➔d➔ ➔t➔e➔s➔t➔ ➔c➔a➔s➔e➔s➔ ➔(➔e➔.➔g➔.➔ ➔L➔o➔g➔i➔n➔ ➔T➔e➔s➔t➔s➔)➔
➔T➔e➔s➔t➔ ➔C➔a➔s➔e➔ ➔S➔p➔e➔c➔i➔f➔i➔c➔ ➔s➔c➔e➔n➔a➔r➔i➔o➔ ➔w➔i➔t➔h➔ ➔s➔t➔e➔p➔s➔ ➔t➔o➔ ➔v➔e➔r➔i➔f➔y➔ ➔a➔ ➔f➔e➔a➔t➔u➔r➔e➔
➔T➔e➔s➔t➔ ➔S➔t➔e➔p➔ ➔O➔n➔e➔ ➔a➔c➔t➔i➔o➔n➔ ➔+➔ ➔e➔x➔p➔e➔c➔t➔e➔d➔ ➔r➔e➔s➔u➔l➔t➔
➔T➔e➔s➔t➔ ➔R➔u➔n➔ ➔A➔c➔t➔u➔a➔l➔ ➔e➔x➔e➔c➔u➔t➔i➔o➔n➔ ➔s➔e➔s➔s➔i➔o➔n➔
➔T➔e➔s➔t➔ ➔R➔e➔s➔u➔l➔t➔ ➔P➔a➔s➔s➔e➔d➔,➔ ➔F➔a➔i➔l➔e➔d➔,➔ ➔o➔r➔ ➔B➔l➔o➔c➔k➔e➔d➔
➔W➔o➔r➔k➔f➔l➔o➔w➔:➔
➔C➔r➔e➔a➔t➔e➔ ➔T➔e➔s➔t➔ ➔P➔l➔a➔n➔ ➔→➔ ➔C➔r➔e➔a➔t➔e➔ ➔T➔e➔s➔t➔ ➔S➔u➔i➔t➔e➔s➔ ➔→➔ ➔W➔r➔i➔t➔e➔ ➔T➔e➔s➔t➔ ➔C➔a➔s➔e➔s➔ ➔(➔w➔i➔t➔h➔ ➔s➔t➔e➔p➔s➔)➔ ➔→➔ ➔R➔u➔n➔ ➔T➔e➔s➔t➔s➔ ➔→➔ ➔M➔a➔
➔K➔e➔y➔ ➔M➔e➔t➔r➔i➔c➔s➔:➔
➔P➔a➔s➔s➔ ➔R➔a➔t➔e➔ ➔—➔ ➔%➔ ➔o➔f➔ ➔t➔e➔s➔t➔ ➔c➔a➔s➔e➔s➔ ➔t➔h➔a➔t➔ ➔p➔a➔s➔s➔e➔d➔
➔T➔e➔s➔t➔ ➔C➔o➔v➔e➔r➔a➔g➔e➔ ➔—➔ ➔%➔ ➔o➔f➔ ➔u➔s➔e➔r➔ ➔s➔t➔o➔r➔i➔e➔s➔ ➔c➔o➔v➔e➔r➔e➔d➔ ➔b➔y➔ ➔t➔e➔s➔t➔ ➔c➔a➔s➔e➔s➔
➔T➔r➔a➔c➔e➔a➔b➔i➔l➔i➔t➔y➔ ➔M➔a➔t➔r➔i➔x➔ ➔—➔ ➔s➔h➔o➔w➔s➔ ➔w➔h➔i➔c➔h➔ ➔s➔t➔o➔r➔i➔e➔s➔ ➔h➔a➔v➔e➔ ➔t➔e➔s➔t➔ ➔c➔a➔s➔e➔s➔,➔ ➔g➔a➔p➔s➔ ➔v➔i➔s➔i➔b➔l➔e➔
➔C➔.➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔s➔,➔ ➔G➔r➔o➔u➔p➔s➔ ➔&➔ ➔K➔e➔y➔ ➔V➔a➔u➔l➔t➔
➔T➔y➔p➔e➔s➔ ➔o➔f➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔s➔:➔
➔T➔y➔p➔e➔ ➔D➔e➔s➔c➔r➔i➔p➔t➔i➔o➔n➔
➔I➔n➔l➔i➔n➔e➔ ➔Y➔A➔M➔L➔ ➔D➔e➔f➔i➔n➔e➔d➔ ➔i➔n➔ ➔Y➔A➔M➔L➔ ➔u➔n➔d➔e➔r➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔:➔
➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔U➔I➔ ➔D➔e➔f➔i➔n➔e➔d➔ ➔i➔n➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔s➔e➔t➔t➔i➔n➔g➔s➔ ➔i➔n➔ ➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔
➔V➔a➔r➔i➔a➔b➔l➔e➔ ➔G➔r➔o➔u➔p➔s➔ ➔S➔h➔a➔r➔e➔d➔ ➔c➔o➔l➔l➔e➔c➔t➔i➔o➔n➔,➔ ➔r➔e➔u➔s➔a➔b➔l➔e➔ ➔a➔c➔r➔o➔s➔s➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔s➔
➔S➔e➔c➔r➔e➔t➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔s➔ ➔E➔n➔c➔r➔y➔p➔t➔e➔d➔,➔ ➔n➔e➔v➔e➔r➔ ➔s➔h➔o➔w➔n➔ ➔i➔n➔ ➔l➔o➔g➔s➔
➔A➔z➔u➔r➔e➔ ➔K➔e➔y➔ ➔V➔a➔u➔l➔t➔ ➔S➔e➔c➔r➔e➔t➔s➔ ➔f➔r➔o➔m➔ ➔K➔e➔y➔ ➔V➔a➔u➔l➔t➔ ➔l➔i➔n➔k➔e➔d➔ ➔t➔o➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔ ➔g➔r➔o➔u➔p➔
➔I➔n➔l➔i➔n➔e➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔s➔:➔
➔v➔a➔r➔i➔a➔b➔l➔e➔s➔:➔
➔ ➔ ➔b➔u➔i➔l➔d➔C➔o➔n➔f➔i➔g➔:➔ ➔R➔e➔l➔e➔a➔s➔e➔
➔ ➔ ➔a➔p➔p➔N➔a➔m➔e➔:➔ ➔M➔y➔W➔e➔b➔A➔p➔p➔
➔
➔
➔
➔
➔s➔t➔e➔p➔s➔:➔
➔ ➔ ➔-➔ ➔s➔c➔r➔i➔p➔t➔:➔ ➔e➔c➔h➔o➔ ➔B➔u➔i➔l➔d➔i➔n➔g➔ ➔$➔(➔a➔p➔p➔N➔a➔m➔e➔)➔ ➔i➔n➔ ➔$➔(➔b➔u➔i➔l➔d➔C➔o➔n➔f➔i➔g➔)➔ ➔m➔o➔d➔e➔
➔V➔a➔r➔i➔a➔b➔l➔e➔ ➔G➔r➔o➔u➔p➔s➔:➔
➔#➔ ➔C➔r➔e➔a➔t➔e➔:➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔s➔ ➔→➔ ➔L➔i➔b➔r➔a➔r➔y➔ ➔→➔ ➔+➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔ ➔G➔r➔o➔u➔p➔ ➔→➔ ➔S➔h➔a➔r➔e➔d➔C➔o➔n➔f➔i➔g➔
➔v➔a➔r➔i➔a➔b➔l➔e➔s➔:➔
➔ ➔ ➔-➔ ➔g➔r➔o➔u➔p➔:➔ ➔S➔h➔a➔r➔e➔d➔C➔o➔n➔f➔i➔g➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔f➔e➔r➔e➔n➔c➔e➔ ➔g➔r➔o➔u➔p➔
➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔b➔u➔i➔l➔d➔C➔o➔n➔f➔i➔g➔
➔ ➔ ➔ ➔ ➔v➔a➔l➔u➔e➔:➔ ➔R➔e➔l➔e➔a➔s➔e➔
➔S➔e➔c➔r➔e➔t➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔s➔:➔
➔#➔ ➔A➔d➔d➔ ➔i➔n➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔U➔I➔ ➔→➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔s➔ ➔t➔a➔b➔ ➔→➔ ➔c➔l➔i➔c➔k➔ ➔l➔o➔c➔k➔ ➔i➔c➔o➔n➔
➔#➔ ➔R➔e➔f➔e➔r➔e➔n➔c➔e➔ ➔s➔a➔m➔e➔ ➔w➔a➔y➔:➔ ➔$➔(➔M➔y➔S➔e➔c➔r➔e➔t➔)➔
➔#➔ ➔S➔h➔o➔w➔s➔ ➔a➔s➔ ➔*➔*➔*➔ ➔i➔n➔ ➔l➔o➔g➔s➔ ➔—➔ ➔N➔E➔V➔E➔R➔ ➔h➔a➔r➔d➔-➔c➔o➔d➔e➔ ➔s➔e➔c➔r➔e➔t➔s➔ ➔i➔n➔ ➔Y➔A➔M➔L➔!➔
➔A➔z➔u➔r➔e➔ ➔K➔e➔y➔ ➔V➔a➔u➔l➔t➔ ➔I➔n➔t➔e➔g➔r➔a➔t➔i➔o➔n➔:➔
➔A➔z➔u➔r➔e➔ ➔P➔o➔r➔t➔a➔l➔ ➔→➔ ➔C➔r➔e➔a➔t➔e➔ ➔K➔e➔y➔ ➔V➔a➔u➔l➔t➔ ➔→➔ ➔A➔d➔d➔ ➔s➔e➔c➔r➔e➔t➔s➔ ➔(➔D➔a➔t➔a➔b➔a➔s➔e➔P➔a➔s➔s➔w➔o➔r➔d➔,➔ ➔A➔p➔i➔K➔e➔y➔)➔
➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔ ➔→➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔ ➔G➔r➔o➔u➔p➔ ➔→➔ ➔T➔o➔g➔g➔l➔e➔ ➔"➔L➔i➔n➔k➔ ➔s➔e➔c➔r➔e➔t➔s➔ ➔f➔r➔o➔m➔ ➔A➔z➔u➔r➔e➔ ➔K➔e➔y➔ ➔V➔a➔u➔l➔t➔"➔
➔→➔ ➔S➔e➔l➔e➔c➔t➔ ➔s➔u➔b➔s➔c➔r➔i➔p➔t➔i➔o➔n➔ ➔a➔n➔d➔ ➔K➔e➔y➔ ➔V➔a➔u➔l➔t➔ ➔→➔ ➔C➔h➔o➔o➔s➔e➔ ➔w➔h➔i➔c➔h➔ ➔s➔e➔c➔r➔e➔t➔s➔ ➔t➔o➔ ➔e➔x➔p➔o➔s➔e➔
➔→➔ ➔R➔e➔f➔e➔r➔e➔n➔c➔e➔ ➔i➔n➔ ➔Y➔A➔M➔L➔:➔ ➔$➔(➔D➔a➔t➔a➔b➔a➔s➔e➔P➔a➔s➔s➔w➔o➔r➔d➔)➔
➔R➔u➔n➔t➔i➔m➔e➔ ➔P➔a➔r➔a➔m➔e➔t➔e➔r➔s➔ ➔(➔u➔s➔e➔r➔ ➔i➔n➔p➔u➔t➔ ➔w➔h➔e➔n➔ ➔t➔r➔i➔g➔g➔e➔r➔i➔n➔g➔)➔:➔
➔p➔a➔r➔a➔m➔e➔t➔e➔r➔s➔:➔
➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔
➔ ➔ ➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔T➔a➔r➔g➔e➔t➔ ➔E➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔
➔ ➔ ➔ ➔ ➔t➔y➔p➔e➔:➔ ➔s➔t➔r➔i➔n➔g➔
➔ ➔ ➔ ➔ ➔d➔e➔f➔a➔u➔l➔t➔:➔ ➔d➔e➔v➔
➔ ➔ ➔ ➔ ➔v➔a➔l➔u➔e➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔d➔e➔v➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔s➔t➔a➔g➔i➔n➔g➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔#➔ ➔R➔e➔f➔e➔r➔e➔n➔c➔e➔:➔ ➔$➔{➔{➔ ➔p➔a➔r➔a➔m➔e➔t➔e➔r➔s➔.➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔}➔}➔
➔T➔e➔m➔p➔l➔a➔t➔e➔ ➔e➔x➔p➔r➔e➔s➔s➔i➔o➔n➔s➔ ➔v➔s➔ ➔R➔u➔n➔t➔i➔m➔e➔ ➔e➔x➔p➔r➔e➔s➔s➔i➔o➔n➔s➔:➔
➔
➔
➔
➔
➔S➔y➔n➔t➔a➔x➔ ➔W➔h➔e➔n➔ ➔e➔v➔a➔l➔u➔a➔t➔e➔d➔
➔T➔e➔m➔p➔l➔a➔t➔e➔ ➔p➔a➔r➔a➔m➔e➔t➔e➔r➔ ➔$➔{➔{➔ ➔p➔a➔r➔a➔m➔e➔t➔e➔r➔s➔.➔n➔a➔m➔e➔ ➔}➔}➔ ➔W➔h➔e➔n➔ ➔Y➔A➔M➔L➔ ➔i➔s➔ ➔p➔a➔r➔s➔e➔d➔
➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔ ➔$➔(➔v➔a➔r➔i➔a➔b➔l➔e➔N➔a➔m➔e➔)➔ ➔W➔h➔e➔n➔ ➔s➔t➔e➔p➔ ➔a➔c➔t➔u➔a➔l➔l➔y➔ ➔r➔u➔n➔s➔
➔D➔.➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔T➔e➔m➔p➔l➔a➔t➔e➔s➔ ➔—➔ ➔R➔e➔u➔s➔a➔b➔i➔l➔i➔t➔y➔
➔W➔h➔y➔ ➔T➔e➔m➔p➔l➔a➔t➔e➔s➔?➔
➔W➔i➔t➔h➔o➔u➔t➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔s➔ ➔y➔o➔u➔ ➔c➔o➔p➔y➔ ➔t➔h➔e➔ ➔s➔a➔m➔e➔ ➔Y➔A➔M➔L➔ ➔s➔t➔e➔p➔s➔ ➔a➔c➔r➔o➔s➔s➔ ➔1➔0➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔s➔.➔ ➔C➔h➔a➔n➔g➔e➔ ➔o➔n➔e➔ ➔s➔t➔e➔p➔ ➔=➔ ➔u➔p➔d➔a➔t➔e➔ ➔1➔0➔ ➔f➔i➔l➔e➔s➔.➔
➔T➔e➔m➔p➔l➔a➔t➔e➔s➔ ➔s➔o➔l➔v➔e➔ ➔t➔h➔i➔s➔ ➔—➔ ➔d➔e➔f➔i➔n➔e➔ ➔o➔n➔c➔e➔,➔ ➔r➔e➔u➔s➔e➔ ➔e➔v➔e➔r➔y➔w➔h➔e➔r➔e➔.➔
➔T➔y➔p➔e➔s➔:➔
➔T➔y➔p➔e➔ ➔P➔u➔r➔p➔o➔s➔e➔
➔S➔t➔e➔p➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔ ➔R➔e➔u➔s➔a➔b➔l➔e➔ ➔s➔e➔t➔ ➔o➔f➔ ➔s➔t➔e➔p➔s➔
➔J➔o➔b➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔ ➔R➔e➔u➔s➔a➔b➔l➔e➔ ➔j➔o➔b➔ ➔w➔i➔t➔h➔ ➔i➔t➔s➔ ➔o➔w➔n➔ ➔s➔t➔e➔p➔s➔
➔S➔t➔a➔g➔e➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔ ➔R➔e➔u➔s➔a➔b➔l➔e➔ ➔s➔t➔a➔g➔e➔
➔V➔a➔r➔i➔a➔b➔l➔e➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔ ➔S➔h➔a➔r➔e➔d➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔ ➔d➔e➔f➔i➔n➔i➔t➔i➔o➔n➔s➔
➔S➔t➔e➔p➔ ➔T➔e➔m➔p➔l➔a➔t➔e➔ ➔E➔x➔a➔m➔p➔l➔e➔:➔
➔#➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔s➔/➔b➔u➔i➔l➔d➔-➔s➔t➔e➔p➔s➔.➔y➔m➔l➔
➔p➔a➔r➔a➔m➔e➔t➔e➔r➔s➔:➔
➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔
➔ ➔ ➔ ➔ ➔t➔y➔p➔e➔:➔ ➔s➔t➔r➔i➔n➔g➔
➔ ➔ ➔ ➔ ➔d➔e➔f➔a➔u➔l➔t➔:➔ ➔R➔e➔l➔e➔a➔s➔e➔
➔s➔t➔e➔p➔s➔:➔
➔ ➔ ➔-➔ ➔s➔c➔r➔i➔p➔t➔:➔ ➔d➔o➔t➔n➔e➔t➔ ➔r➔e➔s➔t➔o➔r➔e➔
➔ ➔ ➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔R➔e➔s➔t➔o➔r➔e➔
➔ ➔ ➔-➔ ➔s➔c➔r➔i➔p➔t➔:➔ ➔d➔o➔t➔n➔e➔t➔ ➔b➔u➔i➔l➔d➔ ➔-➔-➔c➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔ ➔$➔{➔{➔ ➔p➔a➔r➔a➔m➔e➔t➔e➔r➔s➔.➔c➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔ ➔}➔}➔
➔ ➔ ➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔B➔u➔i➔l➔d➔
➔ ➔ ➔-➔ ➔s➔c➔r➔i➔p➔t➔:➔ ➔d➔o➔t➔n➔e➔t➔ ➔t➔e➔s➔t➔
➔ ➔ ➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔T➔e➔s➔t➔
➔U➔s➔e➔ ➔i➔n➔ ➔M➔a➔i➔n➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔:➔
➔
➔
➔
➔
➔s➔t➔a➔g➔e➔s➔:➔
➔ ➔ ➔-➔ ➔s➔t➔a➔g➔e➔:➔ ➔B➔u➔i➔l➔d➔
➔ ➔ ➔ ➔ ➔j➔o➔b➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔j➔o➔b➔:➔ ➔B➔u➔i➔l➔d➔J➔o➔b➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔:➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔s➔/➔b➔u➔i➔l➔d➔-➔s➔t➔e➔p➔s➔.➔y➔m➔l➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔a➔r➔a➔m➔e➔t➔e➔r➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔:➔ ➔R➔e➔l➔e➔a➔s➔e➔
➔V➔a➔r➔i➔a➔b➔l➔e➔ ➔T➔e➔m➔p➔l➔a➔t➔e➔:➔
➔#➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔s➔/➔v➔a➔r➔s➔.➔y➔m➔l➔
➔v➔a➔r➔i➔a➔b➔l➔e➔s➔:➔
➔ ➔ ➔a➔p➔p➔N➔a➔m➔e➔:➔ ➔M➔y➔W➔e➔b➔A➔p➔p➔
➔ ➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔:➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔#➔ ➔I➔n➔ ➔m➔a➔i➔n➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔:➔
➔v➔a➔r➔i➔a➔b➔l➔e➔s➔:➔
➔ ➔ ➔-➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔:➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔s➔/➔v➔a➔r➔s➔.➔y➔m➔l➔
➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔b➔u➔i➔l➔d➔C➔o➔n➔f➔i➔g➔
➔ ➔ ➔ ➔ ➔v➔a➔l➔u➔e➔:➔ ➔R➔e➔l➔e➔a➔s➔e➔
➔e➔x➔t➔e➔n➔d➔s➔ ➔—➔ ➔E➔n➔f➔o➔r➔c➔e➔ ➔C➔o➔m➔p➔a➔n➔y➔ ➔S➔t➔a➔n➔d➔a➔r➔d➔s➔:➔
➔#➔ ➔F➔o➔r➔c➔e➔ ➔a➔l➔l➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔s➔ ➔t➔o➔ ➔u➔s➔e➔ ➔a➔ ➔b➔a➔s➔e➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔ ➔(➔s➔e➔c➔u➔r➔i➔t➔y➔ ➔t➔e➔a➔m➔s➔ ➔u➔s➔e➔ ➔t➔h➔i➔s➔)➔
➔e➔x➔t➔e➔n➔d➔s➔:➔
➔ ➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔:➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔s➔/➔s➔e➔c➔u➔r➔e➔-➔p➔i➔p➔e➔l➔i➔n➔e➔.➔y➔m➔l➔
➔ ➔ ➔p➔a➔r➔a➔m➔e➔t➔e➔r➔s➔:➔
➔ ➔ ➔ ➔ ➔a➔p➔p➔N➔a➔m➔e➔:➔ ➔M➔y➔A➔p➔p➔
➔E➔.➔ ➔E➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔s➔ ➔&➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔S➔t➔r➔a➔t➔e➔g➔i➔e➔s➔ ➔(➔D➔e➔e➔p➔ ➔D➔i➔v➔e➔)➔
➔C➔h➔e➔c➔k➔s➔ ➔o➔n➔ ➔E➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔s➔:➔
➔C➔h➔e➔c➔k➔ ➔D➔e➔s➔c➔r➔i➔p➔t➔i➔o➔n➔
➔A➔p➔p➔r➔o➔v➔a➔l➔s➔ ➔N➔a➔m➔e➔d➔ ➔p➔e➔r➔s➔o➔n➔ ➔m➔u➔s➔t➔ ➔a➔p➔p➔r➔o➔v➔e➔ ➔b➔e➔f➔o➔r➔e➔ ➔p➔r➔o➔c➔e➔e➔d➔i➔n➔g➔
➔B➔r➔a➔n➔c➔h➔ ➔C➔o➔n➔t➔r➔o➔l➔ ➔M➔u➔s➔t➔ ➔b➔e➔ ➔r➔u➔n➔n➔i➔n➔g➔ ➔f➔r➔o➔m➔ ➔a➔p➔p➔r➔o➔v➔e➔d➔ ➔b➔r➔a➔n➔c➔h➔ ➔(➔e➔.➔g➔.➔ ➔m➔a➔i➔n➔ ➔o➔n➔l➔y➔)➔
➔
➔
➔
➔
➔B➔u➔s➔i➔n➔e➔s➔s➔ ➔H➔o➔u➔r➔s➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔o➔n➔l➔y➔ ➔a➔l➔l➔o➔w➔e➔d➔ ➔d➔u➔r➔i➔n➔g➔ ➔c➔e➔r➔t➔a➔i➔n➔ ➔h➔o➔u➔r➔s➔
➔I➔n➔v➔o➔k➔e➔ ➔A➔z➔u➔r➔e➔ ➔F➔u➔n➔c➔t➔i➔o➔n➔ ➔A➔P➔I➔ ➔m➔u➔s➔t➔ ➔r➔e➔t➔u➔r➔n➔ ➔s➔u➔c➔c➔e➔s➔s➔ ➔b➔e➔f➔o➔r➔e➔ ➔p➔r➔o➔c➔e➔e➔d➔i➔n➔g➔
➔Q➔u➔e➔r➔y➔ ➔W➔o➔r➔k➔ ➔I➔t➔e➔m➔s➔ ➔B➔l➔o➔c➔k➔ ➔i➔f➔ ➔o➔p➔e➔n➔ ➔P➔1➔ ➔b➔u➔g➔s➔ ➔e➔x➔i➔s➔t➔ ➔o➔n➔ ➔t➔h➔e➔ ➔b➔o➔a➔r➔d➔
➔S➔e➔t➔t➔i➔n➔g➔ ➔u➔p➔ ➔E➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔C➔h➔e➔c➔k➔s➔:➔
➔P➔i➔p➔e➔l➔i➔n➔e➔s➔ ➔→➔ ➔E➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔s➔ ➔→➔ ➔S➔e➔l➔e➔c➔t➔ ➔E➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔→➔ ➔.➔.➔.➔ ➔→➔ ➔A➔p➔p➔r➔o➔v➔a➔l➔s➔ ➔a➔n➔d➔ ➔C➔h➔e➔c➔k➔s➔
➔→➔ ➔A➔d➔d➔ ➔A➔p➔p➔r➔o➔v➔a➔l➔ ➔→➔ ➔a➔s➔s➔i➔g➔n➔ ➔a➔p➔p➔r➔o➔v➔e➔r➔s➔
➔→➔ ➔A➔d➔d➔ ➔B➔r➔a➔n➔c➔h➔ ➔C➔o➔n➔t➔r➔o➔l➔ ➔→➔ ➔a➔l➔l➔o➔w➔ ➔o➔n➔l➔y➔:➔ ➔r➔e➔f➔s➔/➔h➔e➔a➔d➔s➔/➔m➔a➔i➔n➔
➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔J➔o➔b➔ ➔Y➔A➔M➔L➔:➔
➔j➔o➔b➔s➔:➔
➔ ➔ ➔-➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔:➔ ➔D➔e➔p➔l➔o➔y➔T➔o➔P➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔ ➔ ➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔D➔e➔p➔l➔o➔y➔ ➔t➔o➔ ➔P➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔ ➔ ➔ ➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔:➔ ➔P➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔c➔o➔r➔d➔s➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔h➔i➔s➔t➔o➔r➔y➔ ➔h➔e➔r➔e➔
➔ ➔ ➔ ➔ ➔s➔t➔r➔a➔t➔e➔g➔y➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔r➔u➔n➔O➔n➔c➔e➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔e➔p➔l➔o➔y➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔d➔o➔w➔n➔l➔o➔a➔d➔:➔ ➔c➔u➔r➔r➔e➔n➔t➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔a➔r➔t➔i➔f➔a➔c➔t➔:➔ ➔d➔r➔o➔p➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔s➔c➔r➔i➔p➔t➔:➔ ➔e➔c➔h➔o➔ ➔D➔e➔p➔l➔o➔y➔i➔n➔g➔ ➔v➔e➔r➔s➔i➔o➔n➔ ➔$➔(➔B➔u➔i➔l➔d➔.➔B➔u➔i➔l➔d➔N➔u➔m➔b➔e➔r➔)➔
➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔S➔t➔r➔a➔t➔e➔g➔i➔e➔s➔:➔
➔S➔t➔r➔a➔t➔e➔g➔y➔ ➔H➔o➔w➔ ➔I➔t➔ ➔W➔o➔r➔k➔s➔ ➔U➔s➔e➔ ➔W➔h➔e➔n➔
➔r➔u➔n➔O➔n➔c➔e➔ ➔A➔l➔l➔ ➔i➔n➔s➔t➔a➔n➔c➔e➔s➔ ➔u➔p➔d➔a➔t➔e➔d➔ ➔a➔t➔ ➔o➔n➔c➔e➔ ➔D➔e➔v➔/➔S➔t➔a➔g➔i➔n➔g➔,➔ ➔s➔i➔m➔p➔l➔e➔ ➔d➔e➔p➔l➔o➔y➔s➔
➔r➔o➔l➔l➔i➔n➔g➔ ➔O➔n➔e➔ ➔i➔n➔s➔t➔a➔n➔c➔e➔ ➔a➔t➔ ➔a➔ ➔t➔i➔m➔e➔ ➔M➔e➔d➔i➔u➔m➔ ➔r➔i➔s➔k➔,➔ ➔r➔e➔d➔u➔c➔e➔ ➔d➔o➔w➔n➔t➔i➔m➔e➔
➔c➔a➔n➔a➔r➔y➔ ➔1➔0➔%➔ ➔f➔i➔r➔s➔t➔,➔ ➔t➔h➔e➔n➔ ➔1➔0➔0➔%➔ ➔i➔f➔ ➔h➔e➔a➔l➔t➔h➔y➔ ➔H➔i➔g➔h➔ ➔r➔i➔s➔k➔,➔ ➔v➔a➔l➔i➔d➔a➔t➔e➔ ➔b➔e➔f➔o➔r➔e➔ ➔f➔u➔l➔l➔ ➔r➔o➔l➔l➔o➔u➔t➔
➔b➔l➔u➔e➔-➔g➔r➔e➔e➔n➔ ➔T➔w➔o➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔s➔,➔ ➔s➔w➔i➔t➔c➔h➔ ➔t➔r➔a➔f➔f➔i➔c➔ ➔C➔r➔i➔t➔i➔c➔a➔l➔,➔ ➔i➔n➔s➔t➔a➔n➔t➔ ➔r➔o➔l➔l➔b➔a➔c➔k➔ ➔n➔e➔e➔d➔e➔d➔
➔F➔.➔ ➔S➔e➔r➔v➔i➔c➔e➔ ➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔s➔ ➔—➔ ➔C➔o➔n➔n➔e➔c➔t➔ ➔t➔o➔ ➔E➔x➔t➔e➔r➔n➔a➔l➔ ➔S➔e➔r➔v➔i➔c➔e➔s➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔ ➔S➔e➔r➔v➔i➔c➔e➔ ➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔?➔
➔
➔
➔
➔
➔S➔t➔o➔r➔e➔s➔ ➔c➔r➔e➔d➔e➔n➔t➔i➔a➔l➔s➔ ➔f➔o➔r➔ ➔e➔x➔t➔e➔r➔n➔a➔l➔ ➔s➔e➔r➔v➔i➔c➔e➔s➔ ➔s➔e➔c➔u➔r➔e➔l➔y➔ ➔s➔o➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔s➔ ➔c➔a➔n➔ ➔a➔c➔c➔e➔s➔s➔ ➔t➔h➔e➔m➔ ➔w➔i➔t➔h➔o➔u➔t➔ ➔e➔m➔b➔e➔d➔d➔i➔n➔g➔ ➔s➔e➔c➔r➔e➔t➔s➔ ➔i➔n➔
➔Y➔A➔M➔L➔.➔
➔C➔o➔m➔m➔o➔n➔ ➔T➔y➔p➔e➔s➔:➔
➔T➔y➔p➔e➔ ➔U➔s➔e➔
➔A➔z➔u➔r➔e➔ ➔R➔e➔s➔o➔u➔r➔c➔e➔ ➔M➔a➔n➔a➔g➔e➔r➔ ➔D➔e➔p➔l➔o➔y➔ ➔t➔o➔ ➔A➔z➔u➔r➔e➔ ➔(➔V➔M➔s➔,➔ ➔A➔p➔p➔ ➔S➔e➔r➔v➔i➔c➔e➔,➔ ➔A➔K➔S➔)➔
➔D➔o➔c➔k➔e➔r➔ ➔R➔e➔g➔i➔s➔t➔r➔y➔ ➔P➔u➔s➔h➔/➔p➔u➔l➔l➔ ➔i➔m➔a➔g➔e➔s➔ ➔f➔r➔o➔m➔ ➔A➔C➔R➔,➔ ➔D➔o➔c➔k➔e➔r➔ ➔H➔u➔b➔
➔G➔i➔t➔H➔u➔b➔ ➔A➔c➔c➔e➔s➔s➔ ➔G➔i➔t➔H➔u➔b➔ ➔r➔e➔p➔o➔s➔
➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔ ➔D➔e➔p➔l➔o➔y➔ ➔t➔o➔ ➔K➔8➔s➔ ➔c➔l➔u➔s➔t➔e➔r➔s➔
➔S➔S➔H➔ ➔C➔o➔n➔n➔e➔c➔t➔ ➔t➔o➔ ➔L➔i➔n➔u➔x➔ ➔s➔e➔r➔v➔e➔r➔s➔
➔S➔o➔n➔a➔r➔C➔l➔o➔u➔d➔ ➔C➔o➔d➔e➔ ➔q➔u➔a➔l➔i➔t➔y➔ ➔a➔n➔a➔l➔y➔s➔i➔s➔
➔C➔r➔e➔a➔t➔e➔ ➔S➔e➔r➔v➔i➔c➔e➔ ➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔:➔
➔P➔r➔o➔j➔e➔c➔t➔ ➔S➔e➔t➔t➔i➔n➔g➔s➔ ➔→➔ ➔S➔e➔r➔v➔i➔c➔e➔ ➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔s➔ ➔→➔ ➔+➔ ➔N➔e➔w➔ ➔S➔e➔r➔v➔i➔c➔e➔ ➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔
➔→➔ ➔S➔e➔l➔e➔c➔t➔ ➔t➔y➔p➔e➔ ➔→➔ ➔A➔u➔t➔h➔e➔n➔t➔i➔c➔a➔t➔e➔ ➔→➔ ➔N➔a➔m➔e➔ ➔i➔t➔ ➔→➔ ➔S➔a➔v➔e➔
➔S➔e➔c➔u➔r➔i➔t➔y➔ ➔O➔p➔t➔i➔o➔n➔s➔:➔
➔O➔p➔t➔i➔o➔n➔ ➔W➔h➔e➔n➔ ➔t➔o➔ ➔u➔s➔e➔
➔G➔r➔a➔n➔t➔ ➔a➔c➔c➔e➔s➔s➔ ➔t➔o➔ ➔a➔l➔l➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔s➔ ➔C➔o➔n➔v➔e➔n➔i➔e➔n➔t➔,➔ ➔l➔e➔s➔s➔ ➔s➔e➔c➔u➔r➔e➔
➔R➔e➔s➔t➔r➔i➔c➔t➔ ➔t➔o➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔s➔ ➔M➔o➔r➔e➔ ➔s➔e➔c➔u➔r➔e➔ ➔f➔o➔r➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔R➔e➔f➔e➔r➔e➔n➔c➔e➔ ➔i➔n➔ ➔Y➔A➔M➔L➔:➔
➔#➔ ➔A➔z➔u➔r➔e➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔
➔-➔ ➔t➔a➔s➔k➔:➔ ➔A➔z➔u➔r➔e➔C➔L➔I➔@➔2➔
➔ ➔ ➔i➔n➔p➔u➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔a➔z➔u➔r➔e➔S➔u➔b➔s➔c➔r➔i➔p➔t➔i➔o➔n➔:➔ ➔'➔M➔y➔A➔z➔u➔r➔e➔S➔e➔r➔v➔i➔c➔e➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔'➔
➔#➔ ➔D➔o➔c➔k➔e➔r➔ ➔p➔u➔s➔h➔
➔-➔ ➔t➔a➔s➔k➔:➔ ➔D➔o➔c➔k➔e➔r➔@➔2➔
➔ ➔ ➔i➔n➔p➔u➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔R➔e➔g➔i➔s➔t➔r➔y➔:➔ ➔'➔M➔y➔A➔C➔R➔S➔e➔r➔v➔i➔c➔e➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔'➔
➔
➔
➔
➔
➔G➔.➔ ➔S➔e➔c➔u➔r➔i➔t➔y➔ ➔&➔ ➔R➔B➔A➔C➔ ➔i➔n➔ ➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔
➔P➔e➔r➔m➔i➔s➔s➔i➔o➔n➔ ➔L➔e➔v➔e➔l➔s➔:➔
➔L➔e➔v➔e➔l➔ ➔C➔o➔n➔t➔r➔o➔l➔s➔
➔O➔r➔g➔a➔n➔i➔z➔a➔t➔i➔o➔n➔ ➔C➔r➔e➔a➔t➔e➔ ➔p➔r➔o➔j➔e➔c➔t➔s➔,➔ ➔m➔a➔n➔a➔g➔e➔ ➔b➔i➔l➔l➔i➔n➔g➔,➔ ➔m➔a➔n➔a➔g➔e➔ ➔u➔s➔e➔r➔s➔
➔P➔r➔o➔j➔e➔c➔t➔ ➔A➔c➔c➔e➔s➔s➔ ➔t➔o➔ ➔B➔o➔a➔r➔d➔s➔,➔ ➔R➔e➔p➔o➔s➔,➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔s➔ ➔w➔i➔t➔h➔i➔n➔ ➔p➔r➔o➔j➔e➔c➔t➔
➔O➔b➔j➔e➔c➔t➔ ➔S➔p➔e➔c➔i➔f➔i➔c➔ ➔r➔e➔p➔o➔s➔,➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔s➔,➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔s➔,➔ ➔f➔e➔e➔d➔s➔
➔B➔u➔i➔l➔t➔-➔i➔n➔ ➔S➔e➔c➔u➔r➔i➔t➔y➔ ➔G➔r➔o➔u➔p➔s➔:➔
➔G➔r➔o➔u➔p➔ ➔A➔c➔c➔e➔s➔s➔
➔P➔r➔o➔j➔e➔c➔t➔ ➔A➔d➔m➔i➔n➔i➔s➔t➔r➔a➔t➔o➔r➔s➔ ➔F➔u➔l➔l➔ ➔c➔o➔n➔t➔r➔o➔l➔ ➔—➔ ➔a➔d➔d➔ ➔m➔e➔m➔b➔e➔r➔s➔,➔ ➔m➔a➔n➔a➔g➔e➔ ➔s➔e➔t➔t➔i➔n➔g➔s➔
➔B➔u➔i➔l➔d➔ ➔A➔d➔m➔i➔n➔i➔s➔t➔r➔a➔t➔o➔r➔s➔ ➔M➔a➔n➔a➔g➔e➔ ➔a➔n➔d➔ ➔r➔u➔n➔ ➔a➔l➔l➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔s➔
➔C➔o➔n➔t➔r➔i➔b➔u➔t➔o➔r➔s➔ ➔P➔u➔s➔h➔ ➔c➔o➔d➔e➔,➔ ➔c➔r➔e➔a➔t➔e➔ ➔P➔R➔s➔,➔ ➔r➔u➔n➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔s➔
➔R➔e➔a➔d➔e➔r➔s➔ ➔R➔e➔a➔d➔-➔o➔n➔l➔y➔ ➔—➔ ➔v➔i➔e➔w➔ ➔e➔v➔e➔r➔y➔t➔h➔i➔n➔g➔,➔ ➔c➔h➔a➔n➔g➔e➔ ➔n➔o➔t➔h➔i➔n➔g➔
➔P➔r➔o➔j➔e➔c➔t➔ ➔C➔o➔l➔l➔e➔c➔t➔i➔o➔n➔ ➔A➔d➔m➔i➔n➔i➔s➔t➔r➔a➔t➔o➔r➔s➔ ➔O➔r➔g➔a➔n➔i➔z➔a➔t➔i➔o➔n➔-➔l➔e➔v➔e➔l➔ ➔f➔u➔l➔l➔ ➔c➔o➔n➔t➔r➔o➔l➔
➔B➔r➔a➔n➔c➔h➔ ➔P➔o➔l➔i➔c➔i➔e➔s➔ ➔(➔P➔r➔o➔t➔e➔c➔t➔ ➔m➔a➔i➔n➔)➔:➔
➔P➔r➔o➔j➔e➔c➔t➔ ➔S➔e➔t➔t➔i➔n➔g➔s➔ ➔→➔ ➔R➔e➔p➔o➔s➔i➔t➔o➔r➔i➔e➔s➔ ➔→➔ ➔S➔e➔l➔e➔c➔t➔ ➔r➔e➔p➔o➔ ➔→➔ ➔P➔o➔l➔i➔c➔i➔e➔s➔ ➔→➔ ➔B➔r➔a➔n➔c➔h➔ ➔P➔o➔l➔i➔c➔i➔e➔s➔ ➔→➔ ➔m➔a➔i➔n➔
➔A➔d➔d➔ ➔p➔o➔l➔i➔c➔i➔e➔s➔:➔
➔✅➔ ➔ ➔R➔e➔q➔u➔i➔r➔e➔ ➔m➔i➔n➔i➔m➔u➔m➔ ➔r➔e➔v➔i➔e➔w➔e➔r➔s➔:➔ ➔2➔
➔✅➔ ➔ ➔C➔h➔e➔c➔k➔ ➔f➔o➔r➔ ➔l➔i➔n➔k➔e➔d➔ ➔w➔o➔r➔k➔ ➔i➔t➔e➔m➔s➔ ➔(➔P➔R➔ ➔m➔u➔s➔t➔ ➔r➔e➔f➔e➔r➔e➔n➔c➔e➔ ➔a➔ ➔U➔s➔e➔r➔ ➔S➔t➔o➔r➔y➔)➔
➔✅➔ ➔ ➔C➔h➔e➔c➔k➔ ➔f➔o➔r➔ ➔c➔o➔m➔m➔e➔n➔t➔ ➔r➔e➔s➔o➔l➔u➔t➔i➔o➔n➔ ➔(➔a➔l➔l➔ ➔c➔o➔m➔m➔e➔n➔t➔s➔ ➔r➔e➔s➔o➔l➔v➔e➔d➔ ➔b➔e➔f➔o➔r➔e➔ ➔m➔e➔r➔g➔e➔)➔
➔✅➔ ➔ ➔L➔i➔m➔i➔t➔ ➔m➔e➔r➔g➔e➔ ➔t➔y➔p➔e➔s➔ ➔(➔s➔q➔u➔a➔s➔h➔ ➔o➔n➔l➔y➔)➔
➔✅➔ ➔ ➔B➔u➔i➔l➔d➔ ➔v➔a➔l➔i➔d➔a➔t➔i➔o➔n➔ ➔(➔C➔I➔ ➔m➔u➔s➔t➔ ➔p➔a➔s➔s➔ ➔b➔e➔f➔o➔r➔e➔ ➔P➔R➔ ➔c➔a➔n➔ ➔b➔e➔ ➔m➔e➔r➔g➔e➔d➔)➔
➔P➔e➔r➔s➔o➔n➔a➔l➔ ➔A➔c➔c➔e➔s➔s➔ ➔T➔o➔k➔e➔n➔ ➔(➔P➔A➔T➔)➔:➔
➔U➔s➔e➔r➔ ➔S➔e➔t➔t➔i➔n➔g➔s➔ ➔(➔t➔o➔p➔ ➔r➔i➔g➔h➔t➔)➔ ➔→➔ ➔P➔e➔r➔s➔o➔n➔a➔l➔ ➔A➔c➔c➔e➔s➔s➔ ➔T➔o➔k➔e➔n➔s➔ ➔→➔ ➔+➔ ➔N➔e➔w➔ ➔T➔o➔k➔e➔n➔
➔→➔ ➔S➔e➔t➔ ➔e➔x➔p➔i➔r➔y➔ ➔d➔a➔t➔e➔
➔→➔ ➔S➔e➔l➔e➔c➔t➔ ➔m➔i➔n➔i➔m➔u➔m➔ ➔s➔c➔o➔p➔e➔s➔ ➔n➔e➔e➔d➔e➔d➔
➔→➔ ➔C➔o➔p➔y➔ ➔a➔n➔d➔ ➔s➔t➔o➔r➔e➔ ➔s➔e➔c➔u➔r➔e➔l➔y➔ ➔(➔s➔h➔o➔w➔n➔ ➔o➔n➔l➔y➔ ➔O➔N➔C➔E➔)➔
➔U➔s➔e➔ ➔P➔A➔T➔ ➔f➔o➔r➔:➔
➔
➔
➔
➔
➔-➔ ➔A➔u➔t➔h➔e➔n➔t➔i➔c➔a➔t➔i➔n➔g➔ ➔s➔e➔l➔f➔-➔h➔o➔s➔t➔e➔d➔ ➔a➔g➔e➔n➔t➔s➔
➔-➔ ➔G➔i➔t➔ ➔c➔l➔o➔n➔e➔ ➔v➔i➔a➔ ➔H➔T➔T➔P➔S➔
➔-➔ ➔R➔E➔S➔T➔ ➔A➔P➔I➔ ➔c➔a➔l➔l➔s➔
➔-➔ ➔C➔I➔/➔C➔D➔ ➔t➔o➔o➔l➔ ➔a➔u➔t➔h➔e➔n➔t➔i➔c➔a➔t➔i➔o➔n➔
➔H➔.➔ ➔A➔z➔u➔r➔e➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔R➔e➔g➔i➔s➔t➔r➔y➔ ➔(➔A➔C➔R➔)➔ ➔+➔ ➔A➔K➔S➔ ➔i➔n➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔s➔
➔A➔z➔u➔r➔e➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔R➔e➔g➔i➔s➔t➔r➔y➔ ➔(➔A➔C➔R➔)➔:➔
➔M➔i➔c➔r➔o➔s➔o➔f➔t➔'➔s➔ ➔p➔r➔i➔v➔a➔t➔e➔ ➔D➔o➔c➔k➔e➔r➔ ➔r➔e➔g➔i➔s➔t➔r➔y➔ ➔o➔n➔ ➔A➔z➔u➔r➔e➔.➔ ➔P➔u➔s➔h➔ ➔i➔m➔a➔g➔e➔s➔ ➔t➔o➔ ➔A➔C➔R➔ ➔a➔n➔d➔ ➔p➔u➔l➔l➔ ➔d➔u➔r➔i➔n➔g➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔.➔
➔#➔ ➔B➔u➔i➔l➔d➔ ➔a➔n➔d➔ ➔p➔u➔s➔h➔ ➔t➔o➔ ➔A➔C➔R➔ ➔i➔n➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔
➔-➔ ➔t➔a➔s➔k➔:➔ ➔D➔o➔c➔k➔e➔r➔@➔2➔
➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔B➔u➔i➔l➔d➔ ➔a➔n➔d➔ ➔p➔u➔s➔h➔ ➔i➔m➔a➔g➔e➔ ➔t➔o➔ ➔A➔C➔R➔
➔ ➔ ➔i➔n➔p➔u➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔c➔o➔m➔m➔a➔n➔d➔:➔ ➔b➔u➔i➔l➔d➔A➔n➔d➔P➔u➔s➔h➔
➔ ➔ ➔ ➔ ➔r➔e➔p➔o➔s➔i➔t➔o➔r➔y➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔f➔i➔l➔e➔:➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔
➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔R➔e➔g➔i➔s➔t➔r➔y➔:➔ ➔M➔y➔A➔C➔R➔S➔e➔r➔v➔i➔c➔e➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔r➔v➔i➔c➔e➔ ➔c➔o➔n➔n➔e➔c➔t➔i➔o➔n➔ ➔t➔o➔ ➔A➔C➔R➔
➔ ➔ ➔ ➔ ➔t➔a➔g➔s➔:➔ ➔|➔
➔ ➔ ➔ ➔ ➔ ➔ ➔$➔(➔B➔u➔i➔l➔d➔.➔B➔u➔i➔l➔d➔I➔d➔)➔
➔ ➔ ➔ ➔ ➔ ➔ ➔l➔a➔t➔e➔s➔t➔
➔A➔z➔u➔r➔e➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔ ➔S➔e➔r➔v➔i➔c➔e➔ ➔(➔A➔K➔S➔)➔:➔
➔M➔i➔c➔r➔o➔s➔o➔f➔t➔'➔s➔ ➔m➔a➔n➔a➔g➔e➔d➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔ ➔—➔ ➔A➔z➔u➔r➔e➔ ➔h➔a➔n➔d➔l➔e➔s➔ ➔t➔h➔e➔ ➔c➔o➔n➔t➔r➔o➔l➔ ➔p➔l➔a➔n➔e➔ ➔f➔o➔r➔ ➔f➔r➔e➔e➔.➔
➔#➔ ➔D➔e➔p➔l➔o➔y➔ ➔t➔o➔ ➔A➔K➔S➔ ➔i➔n➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔
➔-➔ ➔t➔a➔s➔k➔:➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔M➔a➔n➔i➔f➔e➔s➔t➔@➔0➔
➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔D➔e➔p➔l➔o➔y➔ ➔t➔o➔ ➔A➔K➔S➔
➔ ➔ ➔i➔n➔p➔u➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔a➔c➔t➔i➔o➔n➔:➔ ➔d➔e➔p➔l➔o➔y➔
➔ ➔ ➔ ➔ ➔k➔u➔b➔e➔r➔n➔e➔t➔e➔s➔S➔e➔r➔v➔i➔c➔e➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔:➔ ➔M➔y➔A➔K➔S➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔
➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔:➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔ ➔ ➔ ➔ ➔m➔a➔n➔i➔f➔e➔s➔t➔s➔:➔ ➔|➔
➔ ➔ ➔ ➔ ➔ ➔ ➔m➔a➔n➔i➔f➔e➔s➔t➔s➔/➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔.➔y➔m➔l➔
➔ ➔ ➔ ➔ ➔ ➔ ➔m➔a➔n➔i➔f➔e➔s➔t➔s➔/➔s➔e➔r➔v➔i➔c➔e➔.➔y➔m➔l➔
➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔ ➔m➔y➔a➔c➔r➔.➔a➔z➔u➔r➔e➔c➔r➔.➔i➔o➔/➔m➔y➔a➔p➔p➔:➔$➔(➔B➔u➔i➔l➔d➔.➔B➔u➔i➔l➔d➔I➔d➔)➔
➔C➔o➔m➔p➔l➔e➔t➔e➔ ➔E➔n➔d➔-➔t➔o➔-➔E➔n➔d➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔(➔C➔o➔d➔e➔ ➔→➔ ➔A➔C➔R➔ ➔→➔ ➔A➔K➔S➔)➔:➔
➔
➔
➔
➔
➔t➔r➔i➔g➔g➔e➔r➔:➔
➔ ➔ ➔-➔ ➔m➔a➔i➔n➔
➔v➔a➔r➔i➔a➔b➔l➔e➔s➔:➔
➔ ➔ ➔a➔c➔r➔N➔a➔m➔e➔:➔ ➔m➔y➔a➔p➔p➔a➔c➔k➔r➔e➔g➔i➔s➔t➔r➔y➔
➔ ➔ ➔i➔m➔a➔g➔e➔N➔a➔m➔e➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔t➔a➔g➔:➔ ➔$➔(➔B➔u➔i➔l➔d➔.➔B➔u➔i➔l➔d➔I➔d➔)➔
➔p➔o➔o➔l➔:➔
➔ ➔ ➔v➔m➔I➔m➔a➔g➔e➔:➔ ➔u➔b➔u➔n➔t➔u➔-➔l➔a➔t➔e➔s➔t➔
➔s➔t➔a➔g➔e➔s➔:➔
➔ ➔ ➔#➔ ➔S➔t➔a➔g➔e➔ ➔1➔ ➔—➔ ➔B➔u➔i➔l➔d➔ ➔D➔o➔c➔k➔e➔r➔ ➔I➔m➔a➔g➔e➔ ➔a➔n➔d➔ ➔P➔u➔s➔h➔ ➔t➔o➔ ➔A➔C➔R➔
➔ ➔ ➔-➔ ➔s➔t➔a➔g➔e➔:➔ ➔B➔u➔i➔l➔d➔
➔ ➔ ➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔B➔u➔i➔l➔d➔ ➔a➔n➔d➔ ➔P➔u➔s➔h➔ ➔I➔m➔a➔g➔e➔
➔ ➔ ➔ ➔ ➔j➔o➔b➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔j➔o➔b➔:➔ ➔B➔u➔i➔l➔d➔A➔n➔d➔P➔u➔s➔h➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔t➔a➔s➔k➔:➔ ➔D➔o➔c➔k➔e➔r➔@➔2➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔B➔u➔i➔l➔d➔ ➔a➔n➔d➔ ➔p➔u➔s➔h➔ ➔t➔o➔ ➔A➔C➔R➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔i➔n➔p➔u➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔m➔m➔a➔n➔d➔:➔ ➔b➔u➔i➔l➔d➔A➔n➔d➔P➔u➔s➔h➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔r➔e➔p➔o➔s➔i➔t➔o➔r➔y➔:➔ ➔$➔(➔i➔m➔a➔g➔e➔N➔a➔m➔e➔)➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔f➔i➔l➔e➔:➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔R➔e➔g➔i➔s➔t➔r➔y➔:➔ ➔A➔C➔R➔S➔e➔r➔v➔i➔c➔e➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔t➔a➔g➔s➔:➔ ➔|➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔$➔(➔t➔a➔g➔)➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔l➔a➔t➔e➔s➔t➔
➔ ➔ ➔#➔ ➔S➔t➔a➔g➔e➔ ➔2➔ ➔—➔ ➔D➔e➔p➔l➔o➔y➔ ➔t➔o➔ ➔S➔t➔a➔g➔i➔n➔g➔
➔ ➔ ➔-➔ ➔s➔t➔a➔g➔e➔:➔ ➔D➔e➔p➔l➔o➔y➔S➔t➔a➔g➔i➔n➔g➔
➔ ➔ ➔ ➔ ➔d➔e➔p➔e➔n➔d➔s➔O➔n➔:➔ ➔B➔u➔i➔l➔d➔
➔ ➔ ➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔D➔e➔p➔l➔o➔y➔ ➔t➔o➔ ➔S➔t➔a➔g➔i➔n➔g➔
➔ ➔ ➔ ➔ ➔j➔o➔b➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔:➔ ➔D➔e➔p➔l➔o➔y➔S➔t➔a➔g➔i➔n➔g➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔:➔ ➔S➔t➔a➔g➔i➔n➔g➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔r➔a➔t➔e➔g➔y➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔r➔u➔n➔O➔n➔c➔e➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔e➔p➔l➔o➔y➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔t➔a➔s➔k➔:➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔M➔a➔n➔i➔f➔e➔s➔t➔@➔0➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔i➔n➔p➔u➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔a➔c➔t➔i➔o➔n➔:➔ ➔d➔e➔p➔l➔o➔y➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔k➔u➔b➔e➔r➔n➔e➔t➔e➔s➔S➔e➔r➔v➔i➔c➔e➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔:➔ ➔A➔K➔S➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔:➔ ➔s➔t➔a➔g➔i➔n➔g➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔m➔a➔n➔i➔f➔e➔s➔t➔s➔:➔ ➔m➔a➔n➔i➔f➔e➔s➔t➔s➔/➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔.➔y➔m➔l➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔ ➔$➔(➔a➔c➔r➔N➔a➔m➔e➔)➔.➔a➔z➔u➔r➔e➔c➔r➔.➔i➔o➔/➔$➔(➔i➔m➔a➔g➔e➔N➔a➔m➔e➔)➔:➔$➔(➔t➔a➔g➔)➔
➔
➔
➔
➔
➔ ➔ ➔#➔ ➔S➔t➔a➔g➔e➔ ➔3➔ ➔—➔ ➔D➔e➔p➔l➔o➔y➔ ➔t➔o➔ ➔P➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔(➔w➔i➔t➔h➔ ➔a➔p➔p➔r➔o➔v➔a➔l➔)➔
➔ ➔ ➔-➔ ➔s➔t➔a➔g➔e➔:➔ ➔D➔e➔p➔l➔o➔y➔P➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔ ➔ ➔ ➔ ➔d➔e➔p➔e➔n➔d➔s➔O➔n➔:➔ ➔D➔e➔p➔l➔o➔y➔S➔t➔a➔g➔i➔n➔g➔
➔ ➔ ➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔D➔e➔p➔l➔o➔y➔ ➔t➔o➔ ➔P➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔ ➔ ➔ ➔ ➔j➔o➔b➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔:➔ ➔D➔e➔p➔l➔o➔y➔P➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔:➔ ➔P➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔p➔p➔r➔o➔v➔a➔l➔ ➔r➔e➔q➔u➔i➔r➔e➔d➔ ➔h➔e➔r➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔r➔a➔t➔e➔g➔y➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔r➔u➔n➔O➔n➔c➔e➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔e➔p➔l➔o➔y➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔t➔a➔s➔k➔:➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔M➔a➔n➔i➔f➔e➔s➔t➔@➔0➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔i➔n➔p➔u➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔a➔c➔t➔i➔o➔n➔:➔ ➔d➔e➔p➔l➔o➔y➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔k➔u➔b➔e➔r➔n➔e➔t➔e➔s➔S➔e➔r➔v➔i➔c➔e➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔:➔ ➔A➔K➔S➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔:➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔m➔a➔n➔i➔f➔e➔s➔t➔s➔:➔ ➔m➔a➔n➔i➔f➔e➔s➔t➔s➔/➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔.➔y➔m➔l➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔ ➔$➔(➔a➔c➔r➔N➔a➔m➔e➔)➔.➔a➔z➔u➔r➔e➔c➔r➔.➔i➔o➔/➔$➔(➔i➔m➔a➔g➔e➔N➔a➔m➔e➔)➔:➔$➔(➔t➔a➔g➔)➔
➔I➔.➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔w➔i➔t➔h➔ ➔A➔z➔u➔r➔e➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔s➔ ➔(➔A➔z➔u➔r➔e➔-➔n➔a➔t➔i➔v➔e➔)➔
➔#➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔u➔s➔i➔n➔g➔ ➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔ ➔t➔a➔s➔k➔s➔
➔s➔t➔e➔p➔s➔:➔
➔ ➔ ➔-➔ ➔t➔a➔s➔k➔:➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔I➔n➔s➔t➔a➔l➔l➔e➔r➔@➔0➔
➔ ➔ ➔ ➔ ➔i➔n➔p➔u➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔t➔e➔r➔r➔a➔f➔o➔r➔m➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔l➔a➔t➔e➔s➔t➔
➔ ➔ ➔-➔ ➔t➔a➔s➔k➔:➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔T➔a➔s➔k➔V➔2➔@➔2➔
➔ ➔ ➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔I➔n➔i➔t➔
➔ ➔ ➔ ➔ ➔i➔n➔p➔u➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔p➔r➔o➔v➔i➔d➔e➔r➔:➔ ➔a➔z➔u➔r➔e➔r➔m➔
➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔m➔m➔a➔n➔d➔:➔ ➔i➔n➔i➔t➔
➔ ➔ ➔ ➔ ➔ ➔ ➔b➔a➔c➔k➔e➔n➔d➔S➔e➔r➔v➔i➔c➔e➔A➔r➔m➔:➔ ➔M➔y➔A➔z➔u➔r➔e➔S➔e➔r➔v➔i➔c➔e➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔
➔ ➔ ➔ ➔ ➔ ➔ ➔b➔a➔c➔k➔e➔n➔d➔A➔z➔u➔r➔e➔R➔m➔R➔e➔s➔o➔u➔r➔c➔e➔G➔r➔o➔u➔p➔N➔a➔m➔e➔:➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔S➔t➔a➔t➔e➔-➔R➔G➔
➔ ➔ ➔ ➔ ➔ ➔ ➔b➔a➔c➔k➔e➔n➔d➔A➔z➔u➔r➔e➔R➔m➔S➔t➔o➔r➔a➔g➔e➔A➔c➔c➔o➔u➔n➔t➔N➔a➔m➔e➔:➔ ➔t➔f➔s➔t➔a➔t➔e➔a➔c➔c➔o➔u➔n➔t➔
➔ ➔ ➔ ➔ ➔ ➔ ➔b➔a➔c➔k➔e➔n➔d➔A➔z➔u➔r➔e➔R➔m➔C➔o➔n➔t➔a➔i➔n➔e➔r➔N➔a➔m➔e➔:➔ ➔t➔f➔s➔t➔a➔t➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔b➔a➔c➔k➔e➔n➔d➔A➔z➔u➔r➔e➔R➔m➔K➔e➔y➔:➔ ➔p➔r➔o➔d➔.➔t➔e➔r➔r➔a➔f➔o➔r➔m➔.➔t➔f➔s➔t➔a➔t➔e➔ ➔ ➔ ➔ ➔#➔ ➔s➔t➔o➔r➔e➔ ➔s➔t➔a➔t➔e➔ ➔i➔n➔ ➔A➔z➔u➔r➔e➔ ➔B➔l➔o➔b➔
➔ ➔ ➔-➔ ➔t➔a➔s➔k➔:➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔T➔a➔s➔k➔V➔2➔@➔2➔
➔ ➔ ➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔P➔l➔a➔n➔
➔ ➔ ➔ ➔ ➔i➔n➔p➔u➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔p➔r➔o➔v➔i➔d➔e➔r➔:➔ ➔a➔z➔u➔r➔e➔r➔m➔
➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔m➔m➔a➔n➔d➔:➔ ➔p➔l➔a➔n➔
➔
➔
➔
➔
➔ ➔ ➔ ➔ ➔ ➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔S➔e➔r➔v➔i➔c➔e➔N➔a➔m➔e➔A➔z➔u➔r➔e➔R➔M➔:➔ ➔M➔y➔A➔z➔u➔r➔e➔S➔e➔r➔v➔i➔c➔e➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔
➔ ➔ ➔-➔ ➔t➔a➔s➔k➔:➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔T➔a➔s➔k➔V➔2➔@➔2➔
➔ ➔ ➔ ➔ ➔d➔i➔s➔p➔l➔a➔y➔N➔a➔m➔e➔:➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔A➔p➔p➔l➔y➔
➔ ➔ ➔ ➔ ➔i➔n➔p➔u➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔p➔r➔o➔v➔i➔d➔e➔r➔:➔ ➔a➔z➔u➔r➔e➔r➔m➔
➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔m➔m➔a➔n➔d➔:➔ ➔a➔p➔p➔l➔y➔
➔ ➔ ➔ ➔ ➔ ➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔S➔e➔r➔v➔i➔c➔e➔N➔a➔m➔e➔A➔z➔u➔r➔e➔R➔M➔:➔ ➔M➔y➔A➔z➔u➔r➔e➔S➔e➔r➔v➔i➔c➔e➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔
➔A➔R➔M➔ ➔T➔e➔m➔p➔l➔a➔t➔e➔s➔ ➔v➔s➔ ➔B➔i➔c➔e➔p➔ ➔v➔s➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔:➔
➔T➔o➔o➔l➔ ➔L➔a➔n➔g➔u➔a➔g➔e➔ ➔M➔u➔l➔t➔i➔-➔c➔l➔o➔u➔d➔ ➔C➔o➔m➔p➔l➔e➔x➔i➔t➔y➔
➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔H➔C➔L➔ ➔✅➔ ➔ ➔Y➔e➔s➔ ➔M➔e➔d➔i➔u➔m➔
➔A➔R➔M➔ ➔T➔e➔m➔p➔l➔a➔t➔e➔s➔ ➔J➔S➔O➔N➔ ➔A➔z➔u➔r➔e➔ ➔o➔n➔l➔y➔ ➔H➔i➔g➔h➔ ➔(➔v➔e➔r➔b➔o➔s➔e➔)➔
➔B➔i➔c➔e➔p➔ ➔D➔S➔L➔ ➔(➔s➔i➔m➔p➔l➔e➔r➔ ➔J➔S➔O➔N➔)➔ ➔A➔z➔u➔r➔e➔ ➔o➔n➔l➔y➔ ➔L➔o➔w➔ ➔(➔c➔l➔e➔a➔n➔e➔r➔)➔
➔P➔u➔l➔u➔m➔i➔ ➔T➔y➔p➔e➔S➔c➔r➔i➔p➔t➔/➔P➔y➔t➔h➔o➔n➔ ➔✅➔ ➔ ➔Y➔e➔s➔ ➔M➔e➔d➔i➔u➔m➔
➔F➔o➔r➔ ➔i➔n➔t➔e➔r➔v➔i➔e➔w➔s➔:➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔i➔s➔ ➔m➔o➔s➔t➔ ➔p➔o➔p➔u➔l➔a➔r➔.➔ ➔B➔i➔c➔e➔p➔ ➔i➔s➔ ➔M➔i➔c➔r➔o➔s➔o➔f➔t➔'➔s➔ ➔m➔o➔d➔e➔r➔n➔ ➔a➔l➔t➔e➔r➔n➔a➔t➔i➔v➔e➔ ➔t➔o➔ ➔A➔R➔M➔.➔ ➔Y➔o➔u➔ ➔c➔a➔n➔
➔m➔e➔n➔t➔i➔o➔n➔ ➔y➔o➔u➔ ➔u➔s➔e➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔.➔
➔J➔.➔ ➔M➔o➔n➔i➔t➔o➔r➔i➔n➔g➔ ➔—➔ ➔A➔z➔u➔r➔e➔ ➔M➔o➔n➔i➔t➔o➔r➔ ➔+➔ ➔A➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔ ➔I➔n➔s➔i➔g➔h➔t➔s➔ ➔+➔ ➔D➔a➔s➔h➔b➔o➔a➔r➔d➔s➔
➔A➔z➔u➔r➔e➔ ➔M➔o➔n➔i➔t➔o➔r➔:➔
➔C➔e➔n➔t➔r➔a➔l➔ ➔m➔o➔n➔i➔t➔o➔r➔i➔n➔g➔ ➔p➔l➔a➔t➔f➔o➔r➔m➔ ➔f➔o➔r➔ ➔A➔z➔u➔r➔e➔.➔ ➔C➔o➔l➔l➔e➔c➔t➔s➔ ➔m➔e➔t➔r➔i➔c➔s➔ ➔(➔C➔P➔U➔,➔ ➔m➔e➔m➔o➔r➔y➔,➔ ➔r➔e➔q➔u➔e➔s➔t➔s➔)➔ ➔a➔n➔d➔ ➔l➔o➔g➔s➔ ➔f➔r➔o➔m➔ ➔a➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔s➔ ➔a➔n➔d➔
➔i➔n➔f➔r➔a➔s➔t➔r➔u➔c➔t➔u➔r➔e➔.➔
➔C➔o➔m➔p➔o➔n➔e➔n➔t➔ ➔P➔u➔r➔p➔o➔s➔e➔
➔M➔e➔t➔r➔i➔c➔s➔ ➔N➔u➔m➔e➔r➔i➔c➔ ➔v➔a➔l➔u➔e➔s➔ ➔o➔v➔e➔r➔ ➔t➔i➔m➔e➔ ➔(➔C➔P➔U➔ ➔%➔,➔ ➔r➔e➔q➔u➔e➔s➔t➔ ➔c➔o➔u➔n➔t➔)➔
➔L➔o➔g➔s➔ ➔D➔e➔t➔a➔i➔l➔e➔d➔ ➔e➔v➔e➔n➔t➔ ➔r➔e➔c➔o➔r➔d➔s➔ ➔(➔e➔r➔r➔o➔r➔s➔,➔ ➔w➔a➔r➔n➔i➔n➔g➔s➔,➔ ➔t➔r➔a➔c➔e➔s➔)➔
➔A➔l➔e➔r➔t➔s➔ ➔N➔o➔t➔i➔f➔y➔ ➔w➔h➔e➔n➔ ➔m➔e➔t➔r➔i➔c➔ ➔c➔r➔o➔s➔s➔e➔s➔ ➔t➔h➔r➔e➔s➔h➔o➔l➔d➔ ➔(➔C➔P➔U➔ ➔>➔ ➔8➔0➔%➔)➔
➔D➔a➔s➔h➔b➔o➔a➔r➔d➔s➔ ➔V➔i➔s➔u➔a➔l➔ ➔c➔h➔a➔r➔t➔s➔ ➔a➔n➔d➔ ➔g➔r➔a➔p➔h➔s➔
➔W➔o➔r➔k➔b➔o➔o➔k➔s➔ ➔I➔n➔t➔e➔r➔a➔c➔t➔i➔v➔e➔ ➔r➔e➔p➔o➔r➔t➔s➔ ➔c➔o➔m➔b➔i➔n➔i➔n➔g➔ ➔m➔e➔t➔r➔i➔c➔s➔,➔ ➔l➔o➔g➔s➔,➔ ➔t➔e➔x➔t➔
➔
➔
➔
➔
➔A➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔ ➔I➔n➔s➔i➔g➔h➔t➔s➔ ➔(➔A➔P➔M➔)➔:➔
➔A➔u➔t➔o➔m➔a➔t➔i➔c➔a➔l➔l➔y➔ ➔t➔r➔a➔c➔k➔s➔:➔ ➔r➔e➔q➔u➔e➔s➔t➔ ➔r➔a➔t➔e➔s➔,➔ ➔f➔a➔i➔l➔u➔r➔e➔ ➔r➔a➔t➔e➔s➔,➔ ➔r➔e➔s➔p➔o➔n➔s➔e➔ ➔t➔i➔m➔e➔s➔,➔ ➔e➔x➔c➔e➔p➔t➔i➔o➔n➔s➔,➔ ➔u➔s➔e➔r➔ ➔b➔e➔h➔a➔v➔i➔o➔r➔ ➔—➔ ➔j➔u➔s➔t➔ ➔a➔d➔d➔ ➔t➔h➔e➔ ➔S➔D➔K➔.➔
➔A➔z➔u➔r➔e➔ ➔P➔o➔r➔t➔a➔l➔ ➔→➔ ➔C➔r➔e➔a➔t➔e➔ ➔A➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔ ➔I➔n➔s➔i➔g➔h➔t➔s➔ ➔→➔ ➔G➔e➔t➔ ➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔ ➔S➔t➔r➔i➔n➔g➔
➔→➔ ➔A➔d➔d➔ ➔S➔D➔K➔ ➔t➔o➔ ➔y➔o➔u➔r➔ ➔a➔p➔p➔ ➔→➔ ➔D➔e➔p➔l➔o➔y➔ ➔→➔ ➔L➔i➔v➔e➔ ➔t➔e➔l➔e➔m➔e➔t➔r➔y➔ ➔i➔n➔ ➔m➔i➔n➔u➔t➔e➔s➔
➔C➔r➔e➔a➔t➔e➔ ➔A➔l➔e➔r➔t➔:➔
➔A➔z➔u➔r➔e➔ ➔M➔o➔n➔i➔t➔o➔r➔ ➔→➔ ➔A➔l➔e➔r➔t➔s➔ ➔→➔ ➔+➔ ➔C➔r➔e➔a➔t➔e➔ ➔→➔ ➔A➔l➔e➔r➔t➔ ➔r➔u➔l➔e➔
➔→➔ ➔S➔e➔l➔e➔c➔t➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔(➔A➔p➔p➔ ➔S➔e➔r➔v➔i➔c➔e➔,➔ ➔A➔K➔S➔)➔
➔→➔ ➔C➔o➔n➔d➔i➔t➔i➔o➔n➔:➔ ➔H➔T➔T➔P➔ ➔5➔x➔x➔ ➔e➔r➔r➔o➔r➔s➔ ➔>➔ ➔1➔0➔ ➔p➔e➔r➔ ➔m➔i➔n➔u➔t➔e➔
➔→➔ ➔A➔c➔t➔i➔o➔n➔ ➔g➔r➔o➔u➔p➔:➔ ➔s➔e➔n➔d➔ ➔e➔m➔a➔i➔l➔ ➔/➔ ➔T➔e➔a➔m➔s➔ ➔n➔o➔t➔i➔f➔i➔c➔a➔t➔i➔o➔n➔ ➔/➔ ➔w➔e➔b➔h➔o➔o➔k➔
➔→➔ ➔S➔e➔v➔e➔r➔i➔t➔y➔:➔ ➔C➔r➔i➔t➔i➔c➔a➔l➔ ➔/➔ ➔E➔r➔r➔o➔r➔ ➔/➔ ➔W➔a➔r➔n➔i➔n➔g➔ ➔/➔ ➔I➔n➔f➔o➔r➔m➔a➔t➔i➔o➔n➔a➔l➔
➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔ ➔D➔a➔s➔h➔b➔o➔a➔r➔d➔s➔:➔
➔D➔a➔s➔h➔b➔o➔a➔r➔d➔s➔ ➔→➔ ➔+➔ ➔A➔d➔d➔ ➔W➔i➔d➔g➔e➔t➔
➔U➔s➔e➔f➔u➔l➔ ➔w➔i➔d➔g➔e➔t➔s➔:➔
➔-➔ ➔S➔p➔r➔i➔n➔t➔ ➔B➔u➔r➔n➔d➔o➔w➔n➔ ➔(➔r➔e➔m➔a➔i➔n➔i➔n➔g➔ ➔w➔o➔r➔k➔ ➔v➔s➔ ➔t➔i➔m➔e➔)➔
➔-➔ ➔B➔u➔i➔l➔d➔ ➔H➔i➔s➔t➔o➔r➔y➔ ➔(➔p➔a➔s➔s➔/➔f➔a➔i➔l➔ ➔t➔r➔e➔n➔d➔)➔
➔-➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔S➔t➔a➔t➔u➔s➔ ➔(➔w➔h➔a➔t➔'➔s➔ ➔d➔e➔p➔l➔o➔y➔e➔d➔ ➔w➔h➔e➔r➔e➔)➔
➔-➔ ➔L➔e➔a➔d➔ ➔T➔i➔m➔e➔ ➔(➔c➔o➔m➔m➔i➔t➔ ➔t➔o➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔t➔i➔m➔e➔)➔
➔-➔ ➔V➔e➔l➔o➔c➔i➔t➔y➔ ➔(➔s➔t➔o➔r➔y➔ ➔p➔o➔i➔n➔t➔s➔ ➔p➔e➔r➔ ➔s➔p➔r➔i➔n➔t➔)➔
➔-➔ ➔W➔o➔r➔k➔ ➔I➔t➔e➔m➔ ➔C➔o➔u➔n➔t➔ ➔(➔b➔u➔g➔s➔ ➔o➔p➔e➔n➔,➔ ➔s➔t➔o➔r➔i➔e➔s➔ ➔d➔o➔n➔e➔)➔
➔D➔O➔R➔A➔ ➔M➔e➔t➔r➔i➔c➔s➔ ➔(➔D➔e➔e➔p➔ ➔D➔i➔v➔e➔)➔:➔
➔M➔e➔t➔r➔i➔c➔ ➔E➔l➔i➔t➔e➔ ➔T➔e➔a➔m➔s➔ ➔H➔o➔w➔ ➔t➔o➔ ➔m➔e➔a➔s➔u➔r➔e➔
➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔F➔r➔e➔q➔u➔e➔n➔c➔y➔ ➔M➔u➔l➔t➔i➔p➔l➔e➔ ➔t➔i➔m➔e➔s➔/➔d➔a➔y➔ ➔C➔o➔u➔n➔t➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔r➔u➔n➔s➔ ➔t➔o➔ ➔p➔r➔o➔d➔
➔L➔e➔a➔d➔ ➔T➔i➔m➔e➔ ➔f➔o➔r➔ ➔C➔h➔a➔n➔g➔e➔s➔ ➔<➔ ➔1➔ ➔h➔o➔u➔r➔ ➔C➔o➔m➔m➔i➔t➔ ➔t➔i➔m➔e➔ ➔→➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔t➔i➔m➔e➔
➔C➔h➔a➔n➔g➔e➔ ➔F➔a➔i➔l➔u➔r➔e➔ ➔R➔a➔t➔e➔ ➔<➔ ➔5➔%➔ ➔%➔ ➔o➔f➔ ➔d➔e➔p➔l➔o➔y➔s➔ ➔c➔a➔u➔s➔i➔n➔g➔ ➔i➔n➔c➔i➔d➔e➔n➔t➔s➔
➔M➔e➔a➔n➔ ➔T➔i➔m➔e➔ ➔t➔o➔ ➔R➔e➔s➔t➔o➔r➔e➔ ➔<➔ ➔1➔ ➔h➔o➔u➔r➔ ➔I➔n➔c➔i➔d➔e➔n➔t➔ ➔o➔p➔e➔n➔ ➔→➔ ➔r➔e➔s➔o➔l➔v➔e➔d➔ ➔t➔i➔m➔e➔
➔K➔.➔ ➔A➔Z➔-➔4➔0➔0➔ ➔E➔x➔a➔m➔ ➔P➔r➔e➔p➔ ➔(➔M➔i➔c➔r➔o➔s➔o➔f➔t➔ ➔D➔e➔v➔O➔p➔s➔ ➔C➔e➔r➔t➔i➔f➔i➔c➔a➔t➔i➔o➔n➔)➔
➔
➔
➔
➔
➔E➔x➔a➔m➔ ➔D➔e➔t➔a➔i➔l➔s➔:➔
➔I➔t➔e➔m➔ ➔D➔e➔t➔a➔i➔l➔
➔E➔x➔a➔m➔ ➔A➔Z➔-➔4➔0➔0➔:➔ ➔D➔e➔s➔i➔g➔n➔i➔n➔g➔ ➔a➔n➔d➔ ➔I➔m➔p➔l➔e➔m➔e➔n➔t➔i➔n➔g➔ ➔M➔i➔c➔r➔o➔s➔o➔f➔t➔ ➔D➔e➔v➔O➔p➔s➔ ➔S➔o➔l➔u➔t➔i➔o➔n➔s➔
➔Q➔u➔e➔s➔t➔i➔o➔n➔s➔ ➔4➔0➔-➔6➔0➔ ➔q➔u➔e➔s➔t➔i➔o➔n➔s➔
➔D➔u➔r➔a➔t➔i➔o➔n➔ ➔1➔2➔0➔ ➔m➔i➔n➔u➔t➔e➔s➔
➔P➔a➔s➔s➔i➔n➔g➔ ➔S➔c➔o➔r➔e➔ ➔7➔0➔0➔ ➔/➔ ➔1➔0➔0➔0➔
➔C➔o➔s➔t➔ ➔~➔U➔S➔D➔ ➔1➔6➔5➔
➔P➔r➔e➔r➔e➔q➔u➔i➔s➔i➔t➔e➔s➔ ➔A➔Z➔-➔1➔0➔4➔ ➔o➔r➔ ➔A➔Z➔-➔2➔0➔4➔ ➔r➔e➔c➔o➔m➔m➔e➔n➔d➔e➔d➔
➔E➔x➔a➔m➔ ➔D➔o➔m➔a➔i➔n➔ ➔B➔r➔e➔a➔k➔d➔o➔w➔n➔:➔
➔D➔o➔m➔a➔i➔n➔ ➔W➔e➔i➔g➔h➔t➔
➔D➔e➔s➔i➔g➔n➔ ➔a➔n➔d➔ ➔i➔m➔p➔l➔e➔m➔e➔n➔t➔ ➔b➔u➔i➔l➔d➔/➔r➔e➔l➔e➔a➔s➔e➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔s➔ ➔~➔4➔0➔%➔
➔D➔e➔s➔i➔g➔n➔ ➔a➔n➔d➔ ➔i➔m➔p➔l➔e➔m➔e➔n➔t➔ ➔s➔o➔u➔r➔c➔e➔ ➔c➔o➔n➔t➔r➔o➔l➔ ➔~➔1➔5➔%➔
➔D➔e➔s➔i➔g➔n➔ ➔a➔n➔d➔ ➔i➔m➔p➔l➔e➔m➔e➔n➔t➔ ➔I➔a➔C➔ ➔~➔1➔5➔%➔
➔C➔o➔n➔f➔i➔g➔u➔r➔e➔ ➔p➔r➔o➔c➔e➔s➔s➔e➔s➔ ➔a➔n➔d➔ ➔c➔o➔m➔m➔u➔n➔i➔c➔a➔t➔i➔o➔n➔s➔ ➔~➔1➔0➔%➔
➔D➔e➔v➔e➔l➔o➔p➔ ➔a➔ ➔s➔e➔c➔u➔r➔i➔t➔y➔ ➔a➔n➔d➔ ➔c➔o➔m➔p➔l➔i➔a➔n➔c➔e➔ ➔p➔l➔a➔n➔ ➔~➔1➔0➔%➔
➔I➔m➔p➔l➔e➔m➔e➔n➔t➔ ➔a➔n➔ ➔i➔n➔s➔t➔r➔u➔m➔e➔n➔t➔a➔t➔i➔o➔n➔ ➔s➔t➔r➔a➔t➔e➔g➔y➔ ➔~➔1➔0➔%➔
➔C➔r➔i➔t➔i➔c➔a➔l➔ ➔T➔o➔p➔i➔c➔s➔ ➔t➔o➔ ➔M➔a➔s➔t➔e➔r➔:➔
➔Y➔A➔M➔L➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔s➔t➔r➔u➔c➔t➔u➔r➔e➔:➔ ➔t➔r➔i➔g➔g➔e➔r➔s➔,➔ ➔s➔t➔a➔g➔e➔s➔,➔ ➔j➔o➔b➔s➔,➔ ➔s➔t➔e➔p➔s➔,➔ ➔c➔o➔n➔d➔i➔t➔i➔o➔n➔s➔,➔ ➔d➔e➔p➔e➔n➔d➔s➔O➔n➔
➔V➔a➔r➔i➔a➔b➔l➔e➔ ➔g➔r➔o➔u➔p➔s➔,➔ ➔s➔e➔c➔r➔e➔t➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔,➔ ➔A➔z➔u➔r➔e➔ ➔K➔e➔y➔ ➔V➔a➔u➔l➔t➔ ➔i➔n➔t➔e➔g➔r➔a➔t➔i➔o➔n➔
➔B➔r➔a➔n➔c➔h➔ ➔p➔o➔l➔i➔c➔i➔e➔s➔:➔ ➔m➔i➔n➔i➔m➔u➔m➔ ➔r➔e➔v➔i➔e➔w➔e➔r➔s➔,➔ ➔b➔u➔i➔l➔d➔ ➔v➔a➔l➔i➔d➔a➔t➔i➔o➔n➔,➔ ➔c➔o➔m➔m➔e➔n➔t➔ ➔r➔e➔s➔o➔l➔u➔t➔i➔o➔n➔
➔S➔e➔r➔v➔i➔c➔e➔ ➔c➔o➔n➔n➔e➔c➔t➔i➔o➔n➔s➔:➔ ➔t➔y➔p➔e➔s➔,➔ ➔s➔e➔c➔u➔r➔i➔t➔y➔,➔ ➔s➔c➔o➔p➔e➔
➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔s➔t➔r➔a➔t➔e➔g➔i➔e➔s➔:➔ ➔r➔u➔n➔O➔n➔c➔e➔,➔ ➔r➔o➔l➔l➔i➔n➔g➔,➔ ➔c➔a➔n➔a➔r➔y➔,➔ ➔b➔l➔u➔e➔-➔g➔r➔e➔e➔n➔
➔E➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔a➔p➔p➔r➔o➔v➔a➔l➔s➔ ➔a➔n➔d➔ ➔c➔h➔e➔c➔k➔s➔
➔D➔o➔c➔k➔e➔r➔:➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔,➔ ➔b➔u➔i➔l➔d➔,➔ ➔p➔u➔s➔h➔,➔ ➔A➔C➔R➔,➔ ➔D➔o➔c➔k➔e➔r➔@➔2➔ ➔t➔a➔s➔k➔
➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔:➔ ➔A➔K➔S➔,➔ ➔k➔u➔b➔e➔c➔t➔l➔,➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔M➔a➔n➔i➔f➔e➔s➔t➔@➔0➔
➔T➔e➔r➔r➔a➔f➔o➔r➔m➔:➔ ➔i➔n➔i➔t➔,➔ ➔p➔l➔a➔n➔,➔ ➔a➔p➔p➔l➔y➔,➔ ➔s➔t➔a➔t➔e➔ ➔b➔a➔c➔k➔e➔n➔d➔ ➔i➔n➔ ➔A➔z➔u➔r➔e➔ ➔S➔t➔o➔r➔a➔g➔e➔
➔A➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔ ➔I➔n➔s➔i➔g➔h➔t➔s➔:➔ ➔S➔D➔K➔ ➔i➔n➔t➔e➔g➔r➔a➔t➔i➔o➔n➔,➔ ➔a➔l➔e➔r➔t➔s➔
➔D➔O➔R➔A➔ ➔m➔e➔t➔r➔i➔c➔s➔:➔ ➔a➔l➔l➔ ➔f➔o➔u➔r➔ ➔m➔e➔t➔r➔i➔c➔s➔ ➔a➔n➔d➔ ➔w➔h➔a➔t➔ ➔t➔h➔e➔y➔ ➔m➔e➔a➔s➔u➔r➔e➔
➔
➔
➔
➔
➔G➔i➔t➔ ➔s➔t➔r➔a➔t➔e➔g➔i➔e➔s➔:➔ ➔b➔r➔a➔n➔c➔h➔i➔n➔g➔ ➔m➔o➔d➔e➔l➔s➔,➔ ➔m➔e➔r➔g➔e➔ ➔t➔y➔p➔e➔s➔,➔ ➔P➔R➔ ➔w➔o➔r➔k➔f➔l➔o➔w➔
➔S➔a➔m➔p➔l➔e➔ ➔A➔Z➔-➔4➔0➔0➔ ➔P➔r➔a➔c➔t➔i➔c➔e➔ ➔Q➔u➔e➔s➔t➔i➔o➔n➔s➔:➔
➔Q➔1➔:➔ ➔Y➔o➔u➔ ➔n➔e➔e➔d➔ ➔m➔a➔i➔n➔ ➔b➔r➔a➔n➔c➔h➔ ➔t➔o➔ ➔o➔n➔l➔y➔ ➔r➔e➔c➔e➔i➔v➔e➔ ➔c➔o➔d➔e➔ ➔t➔h➔r➔o➔u➔g➔h➔ ➔P➔R➔s➔ ➔r➔e➔v➔i➔e➔w➔e➔d➔ ➔b➔y➔ ➔a➔t➔ ➔l➔e➔a➔s➔t➔ ➔2➔ ➔p➔e➔o➔p➔l➔e➔.➔ ➔W➔h➔a➔t➔ ➔d➔o➔ ➔y➔o➔u➔
➔c➔o➔n➔f➔i➔g➔u➔r➔e➔?➔
➔A➔n➔s➔w➔e➔r➔:➔ ➔B➔r➔a➔n➔c➔h➔ ➔p➔o➔l➔i➔c➔i➔e➔s➔ ➔o➔n➔ ➔m➔a➔i➔n➔ ➔b➔r➔a➔n➔c➔h➔ ➔→➔ ➔R➔e➔q➔u➔i➔r➔e➔ ➔m➔i➔n➔i➔m➔u➔m➔ ➔r➔e➔v➔i➔e➔w➔e➔r➔s➔ ➔=➔ ➔2➔
➔Q➔2➔:➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔f➔a➔i➔l➔s➔ ➔b➔e➔c➔a➔u➔s➔e➔ ➔i➔t➔ ➔c➔a➔n➔n➔o➔t➔ ➔a➔u➔t➔h➔e➔n➔t➔i➔c➔a➔t➔e➔ ➔t➔o➔ ➔A➔C➔R➔.➔ ➔M➔o➔s➔t➔ ➔s➔e➔c➔u➔r➔e➔ ➔f➔i➔x➔?➔
➔A➔n➔s➔w➔e➔r➔:➔ ➔C➔r➔e➔a➔t➔e➔ ➔a➔ ➔D➔o➔c➔k➔e➔r➔ ➔R➔e➔g➔i➔s➔t➔r➔y➔ ➔s➔e➔r➔v➔i➔c➔e➔ ➔c➔o➔n➔n➔e➔c➔t➔i➔o➔n➔ ➔i➔n➔ ➔P➔r➔o➔j➔e➔c➔t➔ ➔S➔e➔t➔t➔i➔n➔g➔s➔ ➔p➔o➔i➔n➔t➔i➔n➔g➔ ➔t➔o➔ ➔A➔C➔R➔,➔ ➔r➔e➔f➔e➔r➔e➔n➔c➔e➔ ➔i➔t➔ ➔i➔n➔
➔Y➔A➔M➔L➔.➔
➔Q➔3➔:➔ ➔D➔e➔p➔l➔o➔y➔ ➔t➔o➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔o➔n➔l➔y➔ ➔i➔f➔ ➔s➔t➔a➔g➔i➔n➔g➔ ➔s➔u➔c➔c➔e➔e➔d➔s➔ ➔A➔N➔D➔ ➔a➔ ➔h➔u➔m➔a➔n➔ ➔a➔p➔p➔r➔o➔v➔e➔s➔.➔ ➔W➔h➔a➔t➔ ➔d➔o➔ ➔y➔o➔u➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔e➔?➔
➔A➔n➔s➔w➔e➔r➔:➔ ➔d➔e➔p➔e➔n➔d➔s➔O➔n➔:➔ ➔D➔e➔p➔l➔o➔y➔S➔t➔a➔g➔i➔n➔g➔ ➔ ➔+➔ ➔c➔o➔n➔d➔i➔t➔i➔o➔n➔:➔ ➔s➔u➔c➔c➔e➔e➔d➔e➔d➔(➔)➔ ➔ ➔o➔n➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔s➔t➔a➔g➔e➔ ➔+➔
➔A➔p➔p➔r➔o➔v➔a➔l➔ ➔c➔h➔e➔c➔k➔ ➔o➔n➔ ➔P➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔.➔
➔Q➔4➔:➔ ➔T➔w➔o➔ ➔e➔n➔g➔i➔n➔e➔e➔r➔s➔ ➔r➔u➔n➔ ➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔a➔p➔p➔l➔y➔ ➔s➔i➔m➔u➔l➔t➔a➔n➔e➔o➔u➔s➔l➔y➔ ➔a➔n➔d➔ ➔s➔t➔a➔t➔e➔ ➔g➔e➔t➔s➔ ➔c➔o➔r➔r➔u➔p➔t➔e➔d➔.➔ ➔F➔i➔x➔?➔
➔A➔n➔s➔w➔e➔r➔:➔ ➔C➔o➔n➔f➔i➔g➔u➔r➔e➔ ➔b➔a➔c➔k➔e➔n➔d➔ ➔t➔o➔ ➔u➔s➔e➔ ➔A➔z➔u➔r➔e➔ ➔B➔l➔o➔b➔ ➔S➔t➔o➔r➔a➔g➔e➔ ➔—➔ ➔i➔t➔ ➔s➔u➔p➔p➔o➔r➔t➔s➔ ➔n➔a➔t➔i➔v➔e➔ ➔s➔t➔a➔t➔e➔ ➔l➔o➔c➔k➔i➔n➔g➔ ➔w➔i➔t➔h➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔.➔
➔Q➔5➔:➔ ➔W➔a➔n➔t➔ ➔c➔a➔n➔a➔r➔y➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔w➔h➔e➔r➔e➔ ➔1➔0➔%➔ ➔o➔f➔ ➔u➔s➔e➔r➔s➔ ➔g➔e➔t➔ ➔n➔e➔w➔ ➔v➔e➔r➔s➔i➔o➔n➔ ➔f➔i➔r➔s➔t➔.➔ ➔W➔h➔a➔t➔ ➔s➔t➔r➔a➔t➔e➔g➔y➔?➔
➔A➔n➔s➔w➔e➔r➔:➔ ➔U➔s➔e➔ ➔c➔a➔n➔a➔r➔y➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔s➔t➔r➔a➔t➔e➔g➔y➔ ➔i➔n➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔j➔o➔b➔ ➔w➔i➔t➔h➔ ➔i➔n➔c➔r➔e➔m➔e➔n➔t➔P➔e➔r➔c➔e➔n➔t➔a➔g➔e➔:➔ ➔1➔0➔.➔
➔K➔e➔y➔ ➔D➔i➔s➔t➔i➔n➔c➔t➔i➔o➔n➔s➔ ➔I➔n➔t➔e➔r➔v➔i➔e➔w➔e➔r➔s➔ ➔a➔n➔d➔ ➔E➔x➔a➔m➔ ➔T➔e➔s➔t➔:➔
➔C➔l➔a➔s➔s➔i➔c➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔s➔ ➔v➔s➔ ➔Y➔A➔M➔L➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔s➔ ➔—➔ ➔e➔x➔a➔m➔ ➔t➔e➔s➔t➔s➔ ➔b➔o➔t➔h➔
➔S➔e➔r➔v➔i➔c➔e➔ ➔p➔r➔i➔n➔c➔i➔p➔a➔l➔ ➔(➔s➔e➔c➔u➔r➔e➔)➔ ➔v➔s➔ ➔p➔e➔r➔s➔o➔n➔a➔l➔ ➔c➔r➔e➔d➔e➔n➔t➔i➔a➔l➔s➔ ➔(➔a➔v➔o➔i➔d➔)➔
➔V➔a➔r➔i➔a➔b➔l➔e➔ ➔g➔r➔o➔u➔p➔ ➔(➔r➔e➔u➔s➔a➔b➔l➔e➔)➔ ➔v➔s➔ ➔i➔n➔l➔i➔n➔e➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔ ➔(➔s➔i➔n➔g➔l➔e➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔)➔
➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔j➔o➔b➔ ➔t➔y➔p➔e➔ ➔v➔s➔ ➔r➔e➔g➔u➔l➔a➔r➔ ➔j➔o➔b➔ ➔t➔y➔p➔e➔ ➔—➔ ➔o➔n➔l➔y➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔r➔e➔c➔o➔r➔d➔s➔ ➔t➔o➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔h➔i➔s➔t➔o➔r➔y➔
➔$➔{➔{➔ ➔p➔a➔r➔a➔m➔e➔t➔e➔r➔s➔.➔n➔a➔m➔e➔ ➔}➔}➔ ➔ ➔(➔c➔o➔m➔p➔i➔l➔e➔ ➔t➔i➔m➔e➔)➔ ➔v➔s➔ ➔$➔(➔v➔a➔r➔i➔a➔b➔l➔e➔N➔a➔m➔e➔)➔ ➔ ➔(➔r➔u➔n➔t➔i➔m➔e➔)➔
➔B➔r➔a➔n➔c➔h➔ ➔p➔o➔l➔i➔c➔y➔ ➔(➔p➔r➔o➔t➔e➔c➔t➔s➔ ➔b➔r➔a➔n➔c➔h➔)➔ ➔v➔s➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔a➔p➔p➔r➔o➔v➔a➔l➔ ➔(➔g➔a➔t➔e➔s➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔)➔
➔F➔r➔e➔e➔ ➔S➔t➔u➔d➔y➔ ➔R➔e➔s➔o➔u➔r➔c➔e➔s➔:➔
➔l➔e➔a➔r➔n➔.➔m➔i➔c➔r➔o➔s➔o➔f➔t➔.➔c➔o➔m➔ ➔—➔ ➔o➔f➔f➔i➔c➔i➔a➔l➔ ➔A➔Z➔-➔4➔0➔0➔ ➔l➔e➔a➔r➔n➔i➔n➔g➔ ➔p➔a➔t➔h➔
➔a➔z➔u➔r➔e➔d➔e➔v➔o➔p➔s➔l➔a➔b➔s➔.➔c➔o➔m➔ ➔—➔ ➔f➔r➔e➔e➔ ➔h➔a➔n➔d➔s➔-➔o➔n➔ ➔l➔a➔b➔s➔
➔d➔o➔c➔s➔.➔m➔i➔c➔r➔o➔s➔o➔f➔t➔.➔c➔o➔m➔/➔a➔z➔u➔r➔e➔/➔d➔e➔v➔o➔p➔s➔ ➔—➔ ➔o➔f➔f➔i➔c➔i➔a➔l➔ ➔r➔e➔f➔e➔r➔e➔n➔c➔e➔
➔
➔
➔
➔
➔L➔.➔ ➔C➔o➔m➔p➔l➔e➔t➔e➔ ➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔ ➔Q➔u➔i➔c➔k➔ ➔R➔e➔f➔e➔r➔e➔n➔c➔e➔
➔#➔ ➔N➔A➔V➔I➔G➔A➔T➔I➔O➔N➔
➔d➔e➔v➔.➔a➔z➔u➔r➔e➔.➔c➔o➔m➔/➔Y➔o➔u➔r➔O➔r➔g➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔Y➔o➔u➔r➔ ➔o➔r➔g➔a➔n➔i➔z➔a➔t➔i➔o➔n➔
➔B➔o➔a➔r➔d➔s➔ ➔→➔ ➔B➔a➔c➔k➔l➔o➔g➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔P➔l➔a➔n➔ ➔w➔o➔r➔k➔
➔B➔o➔a➔r➔d➔s➔ ➔→➔ ➔B➔o➔a➔r➔d➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔K➔a➔n➔b➔a➔n➔ ➔w➔o➔r➔k➔f➔l➔o➔w➔
➔B➔o➔a➔r➔d➔s➔ ➔→➔ ➔S➔p➔r➔i➔n➔t➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔S➔p➔r➔i➔n➔t➔ ➔p➔l➔a➔n➔n➔i➔n➔g➔
➔R➔e➔p➔o➔s➔ ➔→➔ ➔F➔i➔l➔e➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔B➔r➔o➔w➔s➔e➔ ➔c➔o➔d➔e➔
➔R➔e➔p➔o➔s➔ ➔→➔ ➔P➔u➔l➔l➔ ➔R➔e➔q➔u➔e➔s➔t➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔C➔o➔d➔e➔ ➔r➔e➔v➔i➔e➔w➔s➔
➔P➔i➔p➔e➔l➔i➔n➔e➔s➔ ➔→➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔C➔I➔/➔C➔D➔
➔P➔i➔p➔e➔l➔i➔n➔e➔s➔ ➔→➔ ➔E➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔t➔a➔r➔g➔e➔t➔s➔
➔P➔i➔p➔e➔l➔i➔n➔e➔s➔ ➔→➔ ➔L➔i➔b➔r➔a➔r➔y➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔ ➔g➔r➔o➔u➔p➔s➔
➔P➔r➔o➔j➔e➔c➔t➔ ➔S➔e➔t➔t➔i➔n➔g➔s➔ ➔→➔ ➔S➔e➔r➔v➔i➔c➔e➔ ➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔s➔ ➔ ➔→➔ ➔E➔x➔t➔e➔r➔n➔a➔l➔ ➔s➔e➔r➔v➔i➔c➔e➔ ➔c➔r➔e➔d➔s➔
➔P➔r➔o➔j➔e➔c➔t➔ ➔S➔e➔t➔t➔i➔n➔g➔s➔ ➔→➔ ➔R➔e➔p➔o➔s➔i➔t➔o➔r➔i➔e➔s➔ ➔→➔ ➔B➔r➔a➔n➔c➔h➔ ➔p➔o➔l➔i➔c➔i➔e➔s➔
➔O➔r➔g➔a➔n➔i➔z➔a➔t➔i➔o➔n➔ ➔S➔e➔t➔t➔i➔n➔g➔s➔ ➔→➔ ➔A➔g➔e➔n➔t➔ ➔P➔o➔o➔l➔s➔ ➔ ➔ ➔ ➔ ➔→➔ ➔A➔g➔e➔n➔t➔s➔
➔#➔ ➔K➔E➔Y➔ ➔C➔O➔N➔C➔E➔P➔T➔S➔
➔C➔I➔:➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔E➔v➔e➔r➔y➔ ➔p➔u➔s➔h➔ ➔→➔ ➔a➔u➔t➔o➔ ➔b➔u➔i➔l➔d➔ ➔+➔ ➔t➔e➔s➔t➔
➔C➔D➔:➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔E➔v➔e➔r➔y➔ ➔s➔u➔c➔c➔e➔s➔s➔f➔u➔l➔ ➔b➔u➔i➔l➔d➔ ➔→➔ ➔a➔u➔t➔o➔ ➔d➔e➔p➔l➔o➔y➔
➔P➔i➔p➔e➔l➔i➔n➔e➔:➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔a➔z➔u➔r➔e➔-➔p➔i➔p➔e➔l➔i➔n➔e➔s➔.➔y➔m➔l➔ ➔a➔t➔ ➔r➔e➔p➔o➔ ➔r➔o➔o➔t➔
➔S➔t➔a➔g➔e➔:➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔M➔a➔j➔o➔r➔ ➔p➔h➔a➔s➔e➔ ➔(➔B➔u➔i➔l➔d➔/➔T➔e➔s➔t➔/➔D➔e➔p➔l➔o➔y➔)➔
➔J➔o➔b➔:➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔W➔o➔r➔k➔ ➔u➔n➔i➔t➔ ➔i➔n➔s➔i➔d➔e➔ ➔s➔t➔a➔g➔e➔ ➔(➔m➔a➔x➔ ➔2➔5➔6➔/➔s➔t➔a➔g➔e➔)➔
➔S➔t➔e➔p➔:➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔S➔i➔n➔g➔l➔e➔ ➔a➔c➔t➔i➔o➔n➔ ➔(➔s➔c➔r➔i➔p➔t➔ ➔o➔r➔ ➔t➔a➔s➔k➔)➔
➔A➔g➔e➔n➔t➔:➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔M➔a➔c➔h➔i➔n➔e➔ ➔t➔h➔a➔t➔ ➔r➔u➔n➔s➔ ➔j➔o➔b➔s➔
➔E➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔:➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔t➔a➔r➔g➔e➔t➔ ➔(➔D➔e➔v➔/➔S➔t➔a➔g➔i➔n➔g➔/➔P➔r➔o➔d➔)➔
➔A➔r➔t➔i➔f➔a➔c➔t➔:➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔B➔u➔i➔l➔d➔ ➔o➔u➔t➔p➔u➔t➔ ➔(➔i➔m➔a➔g➔e➔,➔ ➔z➔i➔p➔,➔ ➔j➔a➔r➔)➔
➔S➔e➔r➔v➔i➔c➔e➔ ➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔:➔ ➔S➔t➔o➔r➔e➔d➔ ➔c➔r➔e➔d➔e➔n➔t➔i➔a➔l➔s➔ ➔f➔o➔r➔ ➔e➔x➔t➔e➔r➔n➔a➔l➔ ➔s➔e➔r➔v➔i➔c➔e➔s➔
➔V➔a➔r➔i➔a➔b➔l➔e➔ ➔G➔r➔o➔u➔p➔:➔ ➔ ➔ ➔ ➔S➔h➔a➔r➔e➔d➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔ ➔a➔c➔r➔o➔s➔s➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔s➔
➔P➔A➔T➔:➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔P➔e➔r➔s➔o➔n➔a➔l➔ ➔A➔c➔c➔e➔s➔s➔ ➔T➔o➔k➔e➔n➔ ➔f➔o➔r➔ ➔a➔u➔t➔h➔e➔n➔t➔i➔c➔a➔t➔i➔o➔n➔
➔
