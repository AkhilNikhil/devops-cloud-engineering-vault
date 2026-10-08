# ☸️ Kubernetes & kOps: The Definitive Master Engineering Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers Kubernetes Architecture, Control Plane Internals, Worker Node Agents, kOps on AWS EC2 Setup, Workload Objects, Networking & Ingress, Storage, Probes, and Troubleshooting.

---

## 📑 Table of Contents
- [Why Kubernetes? (Docker Drawbacks & Orchestration)](#1-drawbacks-of-docker-standalone)
- [Docker Swarm vs Kubernetes](#2-docker-swarm--overcoming-dockers-drawbacks)
- [Kubernetes Master & Worker Architecture](#4-kubernetes-architecture)
- [How kOps Creates a Kubernetes Cluster on AWS (Step-by-Step)](#5-how-kops-creates-a-kubernetes-cluster-on-aws)
- [Core Kubernetes Objects (Pods, Deployments, Services)](#core-workload-objects)
- [Probes: Startup, Liveness, and Readiness](#probes-deep-dive)
- [Storage: PV, PVC, and StorageClasses](#storage-in-kubernetes)
- [Production Diagnostic & Troubleshooting Playbook](#troubleshooting-playbook)
- [High-Yield Technical Interview Q&A](#interview-qa)

---

➔S➔E➔C➔T➔I➔O➔N➔ ➔2➔:➔ ➔K➔U➔B➔E➔R➔N➔E➔T➔E➔S➔ ➔—➔ ➔C➔O➔M➔P➔L➔E➔T➔E➔ ➔G➔U➔I➔D➔E➔
➔F➔l➔o➔w➔:➔ ➔W➔h➔y➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔ ➔→➔ ➔A➔r➔c➔h➔i➔t➔e➔c➔t➔u➔r➔e➔ ➔→➔ ➔C➔o➔r➔e➔ ➔O➔b➔j➔e➔c➔t➔s➔ ➔→➔ ➔S➔t➔o➔r➔a➔g➔e➔ ➔→➔ ➔N➔e➔t➔w➔o➔r➔k➔i➔n➔g➔ ➔→➔ ➔S➔e➔c➔u➔r➔i➔t➔y➔ ➔→➔ ➔A➔d➔v➔a➔n➔c➔e➔d➔ ➔→➔
➔T➔r➔o➔u➔b➔l➔e➔s➔h➔o➔o➔t➔i➔n➔g➔
➔
➔
➔
➔
➔1➔.➔ ➔D➔r➔a➔w➔b➔a➔c➔k➔s➔ ➔o➔f➔ ➔D➔o➔c➔k➔e➔r➔ ➔(➔S➔t➔a➔n➔d➔a➔l➔o➔n➔e➔)➔
➔W➔h➔e➔n➔ ➔y➔o➔u➔ ➔r➔u➔n➔ ➔D➔o➔c➔k➔e➔r➔ ➔a➔l➔o➔n➔e➔ ➔w➔i➔t➔h➔o➔u➔t➔ ➔a➔n➔y➔ ➔o➔r➔c➔h➔e➔s➔t➔r➔a➔t➔i➔o➔n➔,➔ ➔y➔o➔u➔ ➔f➔a➔c➔e➔ ➔t➔h➔e➔s➔e➔ ➔p➔r➔o➔b➔l➔e➔m➔s➔:➔
➔P➔r➔o➔b➔l➔e➔m➔ ➔D➔e➔s➔c➔r➔i➔p➔t➔i➔o➔n➔
➔N➔o➔ ➔A➔u➔t➔o➔-➔h➔e➔a➔l➔i➔n➔g➔ ➔I➔f➔ ➔a➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔c➔r➔a➔s➔h➔e➔s➔,➔ ➔i➔t➔ ➔s➔t➔a➔y➔s➔ ➔d➔e➔a➔d➔.➔ ➔Y➔o➔u➔ ➔m➔a➔n➔u➔a➔l➔l➔y➔ ➔r➔e➔s➔t➔a➔r➔t➔ ➔i➔t➔.➔
➔N➔o➔ ➔A➔u➔t➔o➔-➔s➔c➔a➔l➔i➔n➔g➔ ➔C➔a➔n➔'➔t➔ ➔a➔u➔t➔o➔m➔a➔t➔i➔c➔a➔l➔l➔y➔ ➔a➔d➔d➔ ➔m➔o➔r➔e➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔w➔h➔e➔n➔ ➔l➔o➔a➔d➔ ➔i➔n➔c➔r➔e➔a➔s➔e➔s➔
➔N➔o➔ ➔L➔o➔a➔d➔ ➔B➔a➔l➔a➔n➔c➔i➔n➔g➔ ➔N➔o➔ ➔b➔u➔i➔l➔t➔-➔i➔n➔ ➔w➔a➔y➔ ➔t➔o➔ ➔d➔i➔s➔t➔r➔i➔b➔u➔t➔e➔ ➔t➔r➔a➔f➔f➔i➔c➔ ➔a➔c➔r➔o➔s➔s➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔
➔S➔i➔n➔g➔l➔e➔ ➔H➔o➔s➔t➔ ➔D➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔s➔ ➔o➔n➔ ➔o➔n➔e➔ ➔m➔a➔c➔h➔i➔n➔e➔ ➔—➔ ➔n➔o➔ ➔c➔l➔u➔s➔t➔e➔r➔i➔n➔g➔ ➔o➔u➔t➔ ➔o➔f➔ ➔t➔h➔e➔ ➔b➔o➔x➔
➔N➔o➔ ➔R➔o➔l➔l➔i➔n➔g➔ ➔U➔p➔d➔a➔t➔e➔s➔ ➔N➔o➔ ➔w➔a➔y➔ ➔t➔o➔ ➔u➔p➔d➔a➔t➔e➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔w➔i➔t➔h➔o➔u➔t➔ ➔d➔o➔w➔n➔t➔i➔m➔e➔
➔N➔o➔ ➔S➔e➔l➔f➔-➔h➔e➔a➔l➔i➔n➔g➔ ➔N➔o➔ ➔h➔e➔a➔l➔t➔h➔ ➔c➔h➔e➔c➔k➔s➔ ➔t➔h➔a➔t➔ ➔r➔e➔s➔t➔a➔r➔t➔ ➔u➔n➔h➔e➔a➔l➔t➔h➔y➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔
➔C➔o➔m➔p➔l➔e➔x➔ ➔N➔e➔t➔w➔o➔r➔k➔i➔n➔g➔ ➔C➔o➔n➔n➔e➔c➔t➔i➔n➔g➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔a➔c➔r➔o➔s➔s➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔h➔o➔s➔t➔s➔ ➔i➔s➔ ➔h➔a➔r➔d➔
➔N➔o➔ ➔S➔t➔o➔r➔a➔g➔e➔ ➔M➔a➔n➔a➔g➔e➔m➔e➔n➔t➔ ➔V➔o➔l➔u➔m➔e➔s➔ ➔a➔r➔e➔ ➔m➔a➔n➔u➔a➔l➔ ➔a➔n➔d➔ ➔h➔o➔s➔t➔-➔d➔e➔p➔e➔n➔d➔e➔n➔t➔
➔N➔o➔ ➔S➔e➔c➔r➔e➔t➔ ➔M➔a➔n➔a➔g➔e➔m➔e➔n➔t➔ ➔N➔o➔ ➔b➔u➔i➔l➔t➔-➔i➔n➔ ➔s➔e➔c➔u➔r➔e➔ ➔w➔a➔y➔ ➔t➔o➔ ➔m➔a➔n➔a➔g➔e➔ ➔p➔a➔s➔s➔w➔o➔r➔d➔s➔/➔k➔e➔y➔s➔
➔2➔.➔ ➔D➔o➔c➔k➔e➔r➔ ➔S➔w➔a➔r➔m➔ ➔—➔ ➔O➔v➔e➔r➔c➔o➔m➔i➔n➔g➔ ➔D➔o➔c➔k➔e➔r➔'➔s➔ ➔D➔r➔a➔w➔b➔a➔c➔k➔s➔
➔D➔o➔c➔k➔e➔r➔ ➔S➔w➔a➔r➔m➔ ➔i➔s➔ ➔D➔o➔c➔k➔e➔r➔'➔s➔ ➔n➔a➔t➔i➔v➔e➔ ➔c➔l➔u➔s➔t➔e➔r➔i➔n➔g➔ ➔t➔o➔o➔l➔.➔ ➔I➔t➔ ➔g➔r➔o➔u➔p➔s➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔D➔o➔c➔k➔e➔r➔ ➔h➔o➔s➔t➔s➔ ➔i➔n➔t➔o➔ ➔a➔ ➔s➔i➔n➔g➔l➔e➔ ➔v➔i➔r➔t➔u➔a➔l➔ ➔h➔o➔s➔t➔.➔
➔W➔h➔a➔t➔ ➔S➔w➔a➔r➔m➔ ➔a➔d➔d➔s➔ ➔o➔v➔e➔r➔ ➔p➔l➔a➔i➔n➔ ➔D➔o➔c➔k➔e➔r➔:➔
➔M➔u➔l➔t➔i➔-➔h➔o➔s➔t➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔m➔a➔n➔a➔g➔e➔m➔e➔n➔t➔
➔B➔a➔s➔i➔c➔ ➔l➔o➔a➔d➔ ➔b➔a➔l➔a➔n➔c➔i➔n➔g➔
➔S➔i➔m➔p➔l➔e➔ ➔s➔c➔a➔l➔i➔n➔g➔ ➔(➔ ➔d➔o➔c➔k➔e➔r➔ ➔s➔e➔r➔v➔i➔c➔e➔ ➔s➔c➔a➔l➔e➔ ➔)➔
➔B➔a➔s➔i➔c➔ ➔r➔o➔l➔l➔i➔n➔g➔ ➔u➔p➔d➔a➔t➔e➔s➔
➔S➔e➔r➔v➔i➔c➔e➔ ➔d➔i➔s➔c➔o➔v➔e➔r➔y➔
➔B➔u➔t➔ ➔S➔w➔a➔r➔m➔ ➔h➔a➔s➔ ➔i➔t➔s➔ ➔o➔w➔n➔ ➔l➔i➔m➔i➔t➔a➔t➔i➔o➔n➔s➔:➔
➔D➔o➔c➔k➔e➔r➔ ➔S➔w➔a➔r➔m➔ ➔L➔i➔m➔i➔t➔a➔t➔i➔o➔n➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔ ➔S➔o➔l➔u➔t➔i➔o➔n➔
➔L➔i➔m➔i➔t➔e➔d➔ ➔a➔u➔t➔o➔-➔s➔c➔a➔l➔i➔n➔g➔ ➔(➔n➔o➔ ➔C➔P➔U➔-➔b➔a➔s➔e➔d➔ ➔H➔P➔A➔)➔ ➔F➔u➔l➔l➔ ➔H➔P➔A➔ ➔b➔a➔s➔e➔d➔ ➔o➔n➔ ➔C➔P➔U➔/➔m➔e➔m➔o➔r➔y➔/➔c➔u➔s➔t➔o➔m➔ ➔m➔e➔t➔r➔i➔c➔s➔
➔
➔
➔
➔
➔B➔a➔s➔i➔c➔ ➔h➔e➔a➔l➔t➔h➔ ➔c➔h➔e➔c➔k➔s➔ ➔L➔i➔v➔e➔n➔e➔s➔s➔ ➔+➔ ➔R➔e➔a➔d➔i➔n➔e➔s➔s➔ ➔+➔ ➔S➔t➔a➔r➔t➔u➔p➔ ➔p➔r➔o➔b➔e➔s➔
➔N➔o➔ ➔b➔u➔i➔l➔t➔-➔i➔n➔ ➔s➔e➔c➔r➔e➔t➔s➔ ➔e➔n➔c➔r➔y➔p➔t➔i➔o➔n➔ ➔E➔n➔c➔r➔y➔p➔t➔e➔d➔ ➔s➔e➔c➔r➔e➔t➔s➔,➔ ➔i➔n➔t➔e➔g➔r➔a➔t➔i➔o➔n➔ ➔w➔i➔t➔h➔ ➔V➔a➔u➔l➔t➔
➔L➔i➔m➔i➔t➔e➔d➔ ➔s➔t➔o➔r➔a➔g➔e➔ ➔o➔p➔t➔i➔o➔n➔s➔ ➔P➔V➔,➔ ➔P➔V➔C➔,➔ ➔S➔t➔o➔r➔a➔g➔e➔C➔l➔a➔s➔s➔,➔ ➔d➔y➔n➔a➔m➔i➔c➔ ➔p➔r➔o➔v➔i➔s➔i➔o➔n➔i➔n➔g➔
➔N➔o➔ ➔R➔B➔A➔C➔ ➔F➔u➔l➔l➔ ➔R➔B➔A➔C➔ ➔w➔i➔t➔h➔ ➔r➔o➔l➔e➔s➔ ➔a➔n➔d➔ ➔b➔i➔n➔d➔i➔n➔g➔s➔
➔S➔m➔a➔l➔l➔ ➔e➔c➔o➔s➔y➔s➔t➔e➔m➔ ➔M➔a➔s➔s➔i➔v➔e➔ ➔e➔c➔o➔s➔y➔s➔t➔e➔m➔,➔ ➔C➔N➔C➔F➔ ➔p➔r➔o➔j➔e➔c➔t➔s➔
➔L➔e➔s➔s➔ ➔a➔c➔t➔i➔v➔e➔ ➔d➔e➔v➔e➔l➔o➔p➔m➔e➔n➔t➔ ➔I➔n➔d➔u➔s➔t➔r➔y➔ ➔s➔t➔a➔n➔d➔a➔r➔d➔,➔ ➔m➔a➔s➔s➔i➔v➔e➔ ➔c➔o➔m➔m➔u➔n➔i➔t➔y➔
➔N➔o➔ ➔C➔R➔D➔s➔ ➔C➔u➔s➔t➔o➔m➔ ➔R➔e➔s➔o➔u➔r➔c➔e➔ ➔D➔e➔f➔i➔n➔i➔t➔i➔o➔n➔s➔ ➔t➔o➔ ➔e➔x➔t➔e➔n➔d➔ ➔K➔8➔s➔
➔B➔a➔s➔i➔c➔ ➔n➔e➔t➔w➔o➔r➔k➔i➔n➔g➔ ➔C➔N➔I➔ ➔p➔l➔u➔g➔i➔n➔s➔,➔ ➔N➔e➔t➔w➔o➔r➔k➔ ➔P➔o➔l➔i➔c➔i➔e➔s➔
➔N➔o➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔ ➔i➔s➔o➔l➔a➔t➔i➔o➔n➔ ➔F➔u➔l➔l➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔ ➔s➔u➔p➔p➔o➔r➔t➔ ➔w➔i➔t➔h➔ ➔q➔u➔o➔t➔a➔s➔
➔3➔.➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔?➔
➔D➔e➔f➔i➔n➔i➔t➔i➔o➔n➔:➔
➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔ ➔(➔K➔8➔s➔)➔ ➔i➔s➔ ➔a➔n➔ ➔o➔p➔e➔n➔-➔s➔o➔u➔r➔c➔e➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔o➔r➔c➔h➔e➔s➔t➔r➔a➔t➔i➔o➔n➔ ➔p➔l➔a➔t➔f➔o➔r➔m➔ ➔o➔r➔i➔g➔i➔n➔a➔l➔l➔y➔ ➔c➔r➔e➔a➔t➔e➔d➔ ➔b➔y➔ ➔G➔o➔o➔g➔l➔e➔,➔ ➔n➔o➔w➔
➔m➔a➔i➔n➔t➔a➔i➔n➔e➔d➔ ➔b➔y➔ ➔t➔h➔e➔ ➔C➔N➔C➔F➔ ➔(➔C➔l➔o➔u➔d➔ ➔N➔a➔t➔i➔v➔e➔ ➔C➔o➔m➔p➔u➔t➔i➔n➔g➔ ➔F➔o➔u➔n➔d➔a➔t➔i➔o➔n➔)➔.➔ ➔I➔t➔ ➔a➔u➔t➔o➔m➔a➔t➔e➔s➔ ➔t➔h➔e➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔,➔ ➔s➔c➔a➔l➔i➔n➔g➔,➔ ➔a➔n➔d➔
➔m➔a➔n➔a➔g➔e➔m➔e➔n➔t➔ ➔o➔f➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔i➔z➔e➔d➔ ➔a➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔s➔.➔
➔K➔e➔y➔ ➔F➔e➔a➔t➔u➔r➔e➔s➔:➔
➔A➔u➔t➔o➔-➔h➔e➔a➔l➔i➔n➔g➔ ➔—➔ ➔r➔e➔s➔t➔a➔r➔t➔s➔ ➔f➔a➔i➔l➔e➔d➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔a➔u➔t➔o➔m➔a➔t➔i➔c➔a➔l➔l➔y➔
➔A➔u➔t➔o➔-➔s➔c➔a➔l➔i➔n➔g➔ ➔—➔ ➔H➔P➔A➔ ➔s➔c➔a➔l➔e➔s➔ ➔p➔o➔d➔s➔ ➔b➔a➔s➔e➔d➔ ➔o➔n➔ ➔C➔P➔U➔/➔m➔e➔m➔o➔r➔y➔
➔L➔o➔a➔d➔ ➔B➔a➔l➔a➔n➔c➔i➔n➔g➔ ➔—➔ ➔d➔i➔s➔t➔r➔i➔b➔u➔t➔e➔s➔ ➔t➔r➔a➔f➔f➔i➔c➔ ➔a➔c➔r➔o➔s➔s➔ ➔p➔o➔d➔s➔
➔R➔o➔l➔l➔i➔n➔g➔ ➔U➔p➔d➔a➔t➔e➔s➔ ➔—➔ ➔z➔e➔r➔o➔-➔d➔o➔w➔n➔t➔i➔m➔e➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔s➔
➔S➔e➔l➔f➔-➔h➔e➔a➔l➔i➔n➔g➔ ➔—➔ ➔r➔e➔p➔l➔a➔c➔e➔s➔ ➔f➔a➔i➔l➔e➔d➔ ➔n➔o➔d➔e➔s➔/➔p➔o➔d➔s➔
➔S➔t➔o➔r➔a➔g➔e➔ ➔O➔r➔c➔h➔e➔s➔t➔r➔a➔t➔i➔o➔n➔ ➔—➔ ➔a➔u➔t➔o➔m➔a➔t➔i➔c➔a➔l➔l➔y➔ ➔m➔o➔u➔n➔t➔s➔ ➔s➔t➔o➔r➔a➔g➔e➔
➔S➔e➔c➔r➔e➔t➔ ➔&➔ ➔C➔o➔n➔f➔i➔g➔ ➔M➔a➔n➔a➔g➔e➔m➔e➔n➔t➔ ➔—➔ ➔s➔e➔c➔u➔r➔e➔ ➔h➔a➔n➔d➔l➔i➔n➔g➔ ➔o➔f➔ ➔s➔e➔n➔s➔i➔t➔i➔v➔e➔ ➔d➔a➔t➔a➔
➔S➔e➔r➔v➔i➔c➔e➔ ➔D➔i➔s➔c➔o➔v➔e➔r➔y➔ ➔—➔ ➔b➔u➔i➔l➔t➔-➔i➔n➔ ➔D➔N➔S➔ ➔f➔o➔r➔ ➔p➔o➔d➔ ➔c➔o➔m➔m➔u➔n➔i➔c➔a➔t➔i➔o➔n➔
➔M➔u➔l➔t➔i➔-➔c➔l➔o➔u➔d➔ ➔—➔ ➔r➔u➔n➔s➔ ➔o➔n➔ ➔A➔W➔S➔,➔ ➔A➔z➔u➔r➔e➔,➔ ➔G➔C➔P➔,➔ ➔o➔n➔-➔p➔r➔e➔m➔i➔s➔e➔
➔D➔e➔c➔l➔a➔r➔a➔t➔i➔v➔e➔ ➔—➔ ➔y➔o➔u➔ ➔d➔e➔f➔i➔n➔e➔ ➔d➔e➔s➔i➔r➔e➔d➔ ➔s➔t➔a➔t➔e➔,➔ ➔K➔8➔s➔ ➔m➔a➔k➔e➔s➔ ➔i➔t➔ ➔h➔a➔p➔p➔e➔n➔
➔W➔h➔y➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔ ➔>➔ ➔D➔o➔c➔k➔e➔r➔ ➔S➔w➔a➔r➔m➔:➔
➔I➔n➔d➔u➔s➔t➔r➔y➔ ➔s➔t➔a➔n➔d➔a➔r➔d➔ ➔(➔u➔s➔e➔d➔ ➔b➔y➔ ➔G➔o➔o➔g➔l➔e➔,➔ ➔N➔e➔t➔f➔l➔i➔x➔,➔ ➔A➔i➔r➔b➔n➔b➔)➔
➔M➔u➔c➔h➔ ➔r➔i➔c➔h➔e➔r➔ ➔f➔e➔a➔t➔u➔r➔e➔ ➔s➔e➔t➔
➔
➔
➔
➔
➔B➔e➔t➔t➔e➔r➔ ➔a➔u➔t➔o➔-➔s➔c➔a➔l➔i➔n➔g➔
➔F➔u➔l➔l➔ ➔R➔B➔A➔C➔
➔H➔u➔g➔e➔ ➔e➔c➔o➔s➔y➔s➔t➔e➔m➔ ➔(➔H➔e➔l➔m➔,➔ ➔I➔s➔t➔i➔o➔,➔ ➔A➔r➔g➔o➔,➔ ➔P➔r➔o➔m➔e➔t➔h➔e➔u➔s➔)➔
➔B➔e➔t➔t➔e➔r➔ ➔s➔t➔o➔r➔a➔g➔e➔ ➔m➔a➔n➔a➔g➔e➔m➔e➔n➔t➔
➔M➔o➔r➔e➔ ➔a➔c➔t➔i➔v➔e➔ ➔d➔e➔v➔e➔l➔o➔p➔m➔e➔n➔t➔
➔4➔.➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔ ➔A➔r➔c➔h➔i➔t➔e➔c➔t➔u➔r➔e➔
➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔C➔O➔N➔T➔R➔O➔L➔ ➔P➔L➔A➔N➔E➔ ➔(➔M➔a➔s➔t➔e➔r➔)➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔A➔P➔I➔ ➔S➔e➔r➔v➔e➔r➔ ➔ ➔│➔ ➔ ➔│➔ ➔ ➔ ➔S➔c➔h➔e➔d➔u➔l➔e➔r➔ ➔ ➔ ➔│➔ ➔ ➔│➔ ➔ ➔C➔o➔n➔t➔r➔o➔l➔l➔e➔r➔ ➔│➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔(➔F➔r➔o➔n➔t➔ ➔d➔o➔o➔r➔)➔│➔ ➔ ➔│➔ ➔(➔A➔s➔s➔i➔g➔n➔s➔ ➔p➔o➔d➔s➔ ➔│➔ ➔ ➔│➔ ➔ ➔M➔a➔n➔a➔g➔e➔r➔ ➔ ➔ ➔ ➔│➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔│➔ ➔ ➔t➔o➔ ➔n➔o➔d➔e➔s➔)➔ ➔ ➔ ➔ ➔│➔ ➔ ➔│➔ ➔ ➔(➔W➔a➔t➔c➔h➔e➔s➔ ➔ ➔ ➔│➔ ➔ ➔│➔
➔│➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔ ➔│➔ ➔ ➔s➔t➔a➔t➔e➔)➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔│➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔ ➔│➔
➔│➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔e➔t➔c➔d➔ ➔(➔C➔l➔u➔s➔t➔e➔r➔ ➔D➔a➔t➔a➔b➔a➔s➔e➔)➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔ ➔ ➔S➔t➔o➔r➔e➔s➔ ➔A➔L➔L➔ ➔c➔l➔u➔s➔t➔e➔r➔ ➔s➔t➔a➔t➔e➔ ➔a➔n➔d➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔ ➔ ➔│➔
➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔k➔u➔b➔e➔c➔t➔l➔ ➔c➔o➔m➔m➔a➔n➔d➔s➔ ➔→➔ ➔A➔P➔I➔ ➔S➔e➔r➔v➔e➔r➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┼➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔┌➔─➔─➔─➔─➔─➔─➔─➔▼➔─➔─➔─➔─➔─➔─➔┐➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔▼➔─➔─➔─➔─➔─➔─➔┐➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔▼➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔│➔ ➔ ➔W➔o➔r➔k➔e➔r➔ ➔N➔o➔d➔e➔ ➔│➔ ➔ ➔│➔ ➔ ➔W➔o➔r➔k➔e➔r➔ ➔N➔o➔d➔e➔ ➔│➔ ➔ ➔│➔ ➔ ➔W➔o➔r➔k➔e➔r➔ ➔N➔o➔d➔e➔ ➔│➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔│➔ ➔ ➔│➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔│➔ ➔ ➔│➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔k➔u➔b➔e➔l➔e➔t➔ ➔│➔ ➔│➔ ➔ ➔│➔ ➔ ➔│➔ ➔k➔u➔b➔e➔l➔e➔t➔ ➔│➔ ➔│➔ ➔ ➔│➔ ➔ ➔│➔ ➔k➔u➔b➔e➔l➔e➔t➔ ➔│➔ ➔│➔
➔│➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔│➔ ➔ ➔│➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔│➔ ➔ ➔│➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔│➔
➔│➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔│➔ ➔ ➔│➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔│➔ ➔ ➔│➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔│➔
➔│➔ ➔ ➔│➔k➔u➔b➔e➔-➔ ➔ ➔ ➔ ➔│➔ ➔│➔ ➔ ➔│➔ ➔ ➔│➔k➔u➔b➔e➔-➔ ➔ ➔ ➔ ➔│➔ ➔│➔ ➔ ➔│➔ ➔ ➔│➔k➔u➔b➔e➔-➔ ➔ ➔ ➔ ➔│➔ ➔│➔
➔│➔ ➔ ➔│➔p➔r➔o➔x➔y➔ ➔ ➔ ➔ ➔│➔ ➔│➔ ➔ ➔│➔ ➔ ➔│➔p➔r➔o➔x➔y➔ ➔ ➔ ➔ ➔│➔ ➔│➔ ➔ ➔│➔ ➔ ➔│➔p➔r➔o➔x➔y➔ ➔ ➔ ➔ ➔│➔ ➔│➔
➔│➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔│➔ ➔ ➔│➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔│➔ ➔ ➔│➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔│➔
➔│➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔│➔ ➔ ➔│➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔│➔ ➔ ➔│➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔│➔
➔│➔ ➔ ➔│➔C➔o➔n➔t➔a➔i➔n➔e➔r➔│➔ ➔│➔ ➔ ➔│➔ ➔ ➔│➔C➔o➔n➔t➔a➔i➔n➔e➔r➔│➔ ➔│➔ ➔ ➔│➔ ➔ ➔│➔C➔o➔n➔t➔a➔i➔n➔e➔r➔│➔ ➔│➔
➔│➔ ➔ ➔│➔R➔u➔n➔t➔i➔m➔e➔ ➔ ➔│➔ ➔│➔ ➔ ➔│➔ ➔ ➔│➔R➔u➔n➔t➔i➔m➔e➔ ➔ ➔│➔ ➔│➔ ➔ ➔│➔ ➔ ➔│➔R➔u➔n➔t➔i➔m➔e➔ ➔ ➔│➔ ➔│➔
➔│➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔│➔ ➔ ➔│➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔│➔ ➔ ➔│➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔│➔
➔
➔
➔
➔
➔│➔ ➔ ➔[➔P➔o➔d➔]➔[➔P➔o➔d➔]➔ ➔ ➔│➔ ➔ ➔│➔ ➔ ➔[➔P➔o➔d➔]➔[➔P➔o➔d➔]➔ ➔ ➔│➔ ➔ ➔│➔ ➔ ➔[➔P➔o➔d➔]➔[➔P➔o➔d➔]➔ ➔ ➔│➔
➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔
➔C➔o➔n➔t➔r➔o➔l➔ ➔P➔l➔a➔n➔e➔ ➔C➔o➔m➔p➔o➔n➔e➔n➔t➔s➔
➔C➔o➔m➔p➔o➔n➔e➔n➔t➔ ➔R➔o➔l➔e➔
➔A➔P➔I➔ ➔S➔e➔r➔v➔e➔r➔ ➔E➔n➔t➔r➔y➔ ➔p➔o➔i➔n➔t➔ ➔f➔o➔r➔ ➔a➔l➔l➔ ➔c➔o➔m➔m➔a➔n➔d➔s➔ ➔(➔k➔u➔b➔e➔c➔t➔l➔)➔.➔ ➔V➔a➔l➔i➔d➔a➔t➔e➔s➔ ➔a➔n➔d➔ ➔p➔r➔o➔c➔e➔s➔s➔e➔s➔ ➔r➔e➔q➔u➔e➔s➔t➔s➔.➔
➔S➔c➔h➔e➔d➔u➔l➔e➔r➔ ➔W➔a➔t➔c➔h➔e➔s➔ ➔f➔o➔r➔ ➔u➔n➔s➔c➔h➔e➔d➔u➔l➔e➔d➔ ➔p➔o➔d➔s➔,➔ ➔a➔s➔s➔i➔g➔n➔s➔ ➔t➔h➔e➔m➔ ➔t➔o➔ ➔s➔u➔i➔t➔a➔b➔l➔e➔ ➔w➔o➔r➔k➔e➔r➔ ➔n➔o➔d➔e➔s➔
➔C➔o➔n➔t➔r➔o➔l➔l➔e➔r➔ ➔M➔a➔n➔a➔g➔e➔r➔ ➔R➔u➔n➔s➔ ➔c➔o➔n➔t➔r➔o➔l➔l➔e➔r➔s➔ ➔t➔h➔a➔t➔ ➔m➔a➔i➔n➔t➔a➔i➔n➔ ➔d➔e➔s➔i➔r➔e➔d➔ ➔s➔t➔a➔t➔e➔ ➔(➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔,➔ ➔R➔e➔p➔l➔i➔c➔a➔S➔e➔t➔,➔ ➔N➔o➔d➔e➔ ➔c➔o➔n➔t➔r➔o➔l➔l➔e➔r➔s➔)➔
➔e➔t➔c➔d➔ ➔D➔i➔s➔t➔r➔i➔b➔u➔t➔e➔d➔ ➔k➔e➔y➔-➔v➔a➔l➔u➔e➔ ➔s➔t➔o➔r➔e➔.➔ ➔S➔t➔o➔r➔e➔s➔ ➔A➔L➔L➔ ➔c➔l➔u➔s➔t➔e➔r➔ ➔s➔t➔a➔t➔e➔.➔ ➔S➔o➔u➔r➔c➔e➔ ➔o➔f➔ ➔t➔r➔u➔t➔h➔.➔
➔W➔o➔r➔k➔e➔r➔ ➔N➔o➔d➔e➔ ➔C➔o➔m➔p➔o➔n➔e➔n➔t➔s➔
➔C➔o➔m➔p➔o➔n➔e➔n➔t➔ ➔R➔o➔l➔e➔
➔k➔u➔b➔e➔l➔e➔t➔ ➔A➔g➔e➔n➔t➔ ➔o➔n➔ ➔e➔a➔c➔h➔ ➔n➔o➔d➔e➔.➔ ➔R➔e➔c➔e➔i➔v➔e➔s➔ ➔p➔o➔d➔ ➔s➔p➔e➔c➔s➔ ➔f➔r➔o➔m➔ ➔A➔P➔I➔ ➔s➔e➔r➔v➔e➔r➔,➔ ➔e➔n➔s➔u➔r➔e➔s➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔a➔r➔e➔ ➔r➔u➔n➔n➔i➔n➔g➔
➔k➔u➔b➔e➔-➔p➔r➔o➔x➔y➔ ➔M➔a➔n➔a➔g➔e➔s➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔r➔u➔l➔e➔s➔ ➔o➔n➔ ➔n➔o➔d➔e➔s➔,➔ ➔h➔a➔n➔d➔l➔e➔s➔ ➔S➔e➔r➔v➔i➔c➔e➔ ➔n➔e➔t➔w➔o➔r➔k➔i➔n➔g➔ ➔a➔n➔d➔ ➔l➔o➔a➔d➔ ➔b➔a➔l➔a➔n➔c➔i➔n➔g➔
➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔R➔u➔n➔t➔i➔m➔e➔ ➔R➔u➔n➔s➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔—➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔d➔,➔ ➔C➔R➔I➔-➔O➔ ➔(➔D➔o➔c➔k➔e➔r➔ ➔w➔a➔s➔ ➔d➔e➔p➔r➔e➔c➔a➔t➔e➔d➔ ➔i➔n➔ ➔K➔8➔s➔ ➔1➔.➔2➔4➔+➔)➔
➔5➔.➔ ➔H➔o➔w➔ ➔k➔O➔p➔s➔ ➔C➔r➔e➔a➔t➔e➔s➔ ➔a➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔ ➔C➔l➔u➔s➔t➔e➔r➔ ➔o➔n➔ ➔A➔W➔S➔
➔k➔O➔p➔s➔ ➔(➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔ ➔O➔p➔e➔r➔a➔t➔i➔o➔n➔s➔)➔ ➔—➔ ➔t➔o➔o➔l➔ ➔t➔o➔ ➔p➔r➔o➔v➔i➔s➔i➔o➔n➔,➔ ➔m➔a➔n➔a➔g➔e➔,➔ ➔a➔n➔d➔ ➔u➔p➔g➔r➔a➔d➔e➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔ ➔c➔l➔u➔s➔t➔e➔r➔s➔ ➔o➔n➔ ➔c➔l➔o➔u➔d➔
➔p➔r➔o➔v➔i➔d➔e➔r➔s➔.➔
➔#➔ ➔S➔T➔E➔P➔ ➔1➔ ➔—➔ ➔I➔n➔s➔t➔a➔l➔l➔ ➔k➔O➔p➔s➔ ➔a➔n➔d➔ ➔k➔u➔b➔e➔c➔t➔l➔
➔c➔u➔r➔l➔ ➔-➔L➔o➔ ➔k➔o➔p➔s➔ ➔h➔t➔t➔p➔s➔:➔/➔/➔g➔i➔t➔h➔u➔b➔.➔c➔o➔m➔/➔k➔u➔b➔e➔r➔n➔e➔t➔e➔s➔/➔k➔o➔p➔s➔/➔r➔e➔l➔e➔a➔s➔e➔s➔/➔d➔o➔w➔n➔l➔o➔a➔d➔/➔v➔1➔.➔2➔8➔.➔0➔/➔k➔o➔p➔s➔-➔l➔i➔n➔u➔x➔-➔
➔c➔h➔m➔o➔d➔ ➔+➔x➔ ➔k➔o➔p➔s➔ ➔&➔&➔ ➔s➔u➔d➔o➔ ➔m➔v➔ ➔k➔o➔p➔s➔ ➔/➔u➔s➔r➔/➔l➔o➔c➔a➔l➔/➔b➔i➔n➔/➔
➔#➔ ➔S➔T➔E➔P➔ ➔2➔ ➔—➔ ➔C➔r➔e➔a➔t➔e➔ ➔S➔3➔ ➔b➔u➔c➔k➔e➔t➔ ➔f➔o➔r➔ ➔k➔O➔p➔s➔ ➔s➔t➔a➔t➔e➔ ➔s➔t➔o➔r➔e➔
➔a➔w➔s➔ ➔s➔3➔ ➔m➔b➔ ➔s➔3➔:➔/➔/➔a➔k➔h➔i➔l➔-➔k➔o➔p➔s➔-➔s➔t➔a➔t➔e➔-➔s➔t➔o➔r➔e➔
➔e➔x➔p➔o➔r➔t➔ ➔K➔O➔P➔S➔_➔S➔T➔A➔T➔E➔_➔S➔T➔O➔R➔E➔=➔s➔3➔:➔/➔/➔a➔k➔h➔i➔l➔-➔k➔o➔p➔s➔-➔s➔t➔a➔t➔e➔-➔s➔t➔o➔r➔e➔
➔#➔ ➔S➔T➔E➔P➔ ➔3➔ ➔—➔ ➔C➔r➔e➔a➔t➔e➔ ➔c➔l➔u➔s➔t➔e➔r➔ ➔c➔o➔n➔f➔i➔g➔
➔k➔o➔p➔s➔ ➔c➔r➔e➔a➔t➔e➔ ➔c➔l➔u➔s➔t➔e➔r➔ ➔\➔
➔ ➔ ➔-➔-➔n➔a➔m➔e➔=➔m➔y➔c➔l➔u➔s➔t➔e➔r➔.➔k➔8➔s➔.➔l➔o➔c➔a➔l➔ ➔\➔
➔ ➔ ➔-➔-➔s➔t➔a➔t➔e➔=➔s➔3➔:➔/➔/➔a➔k➔h➔i➔l➔-➔k➔o➔p➔s➔-➔s➔t➔a➔t➔e➔-➔s➔t➔o➔r➔e➔ ➔\➔
➔
➔
➔
➔
➔➔ ➔➔
➔ ➔ ➔-➔-➔z➔o➔n➔e➔s➔=➔u➔s➔-➔e➔a➔s➔t➔-➔1➔a➔,➔u➔s➔-➔e➔a➔s➔t➔-➔1➔b➔ ➔\➔
➔ ➔ ➔-➔-➔n➔o➔d➔e➔-➔c➔o➔u➔n➔t➔=➔2➔ ➔\➔
➔ ➔ ➔-➔-➔n➔o➔d➔e➔-➔s➔i➔z➔e➔=➔t➔3➔.➔m➔e➔d➔i➔u➔m➔ ➔\➔
➔ ➔ ➔-➔-➔m➔a➔s➔t➔e➔r➔-➔s➔i➔z➔e➔=➔t➔3➔.➔m➔e➔d➔i➔u➔m➔ ➔\➔
➔ ➔ ➔-➔-➔d➔n➔s➔-➔z➔o➔n➔e➔=➔m➔y➔c➔l➔u➔s➔t➔e➔r➔.➔k➔8➔s➔.➔l➔o➔c➔a➔l➔
➔#➔ ➔S➔T➔E➔P➔ ➔4➔ ➔—➔ ➔A➔p➔p➔l➔y➔ ➔t➔h➔e➔ ➔c➔l➔u➔s➔t➔e➔r➔ ➔(➔a➔c➔t➔u➔a➔l➔l➔y➔ ➔c➔r➔e➔a➔t➔e➔s➔ ➔A➔W➔S➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔s➔)➔
➔k➔o➔p➔s➔ ➔u➔p➔d➔a➔t➔e➔ ➔c➔l➔u➔s➔t➔e➔r➔ ➔-➔-➔n➔a➔m➔e➔ ➔m➔y➔c➔l➔u➔s➔t➔e➔r➔.➔k➔8➔s➔.➔l➔o➔c➔a➔l➔ ➔-➔-➔y➔e➔s➔ ➔-➔-➔a➔d➔m➔i➔n➔
➔#➔ ➔k➔O➔p➔s➔ ➔a➔u➔t➔o➔m➔a➔t➔i➔c➔a➔l➔l➔y➔ ➔c➔r➔e➔a➔t➔e➔s➔:➔
➔#➔ ➔-➔ ➔V➔P➔C➔,➔ ➔S➔u➔b➔n➔e➔t➔s➔,➔ ➔S➔e➔c➔u➔r➔i➔t➔y➔ ➔G➔r➔o➔u➔p➔s➔
➔#➔ ➔-➔ ➔E➔C➔2➔ ➔i➔n➔s➔t➔a➔n➔c➔e➔s➔ ➔f➔o➔r➔ ➔m➔a➔s➔t➔e➔r➔ ➔a➔n➔d➔ ➔w➔o➔r➔k➔e➔r➔s➔
➔#➔ ➔-➔ ➔I➔A➔M➔ ➔r➔o➔l➔e➔s➔ ➔a➔n➔d➔ ➔p➔o➔l➔i➔c➔i➔e➔s➔
➔#➔ ➔-➔ ➔R➔o➔u➔t➔e➔5➔3➔ ➔D➔N➔S➔ ➔r➔e➔c➔o➔r➔d➔s➔
➔#➔ ➔-➔ ➔E➔L➔B➔ ➔f➔o➔r➔ ➔A➔P➔I➔ ➔s➔e➔r➔v➔e➔r➔
➔#➔ ➔-➔ ➔e➔t➔c➔d➔ ➔o➔n➔ ➔m➔a➔s➔t➔e➔r➔ ➔n➔o➔d➔e➔s➔
➔#➔ ➔-➔ ➔A➔u➔t➔o➔ ➔S➔c➔a➔l➔i➔n➔g➔ ➔G➔r➔o➔u➔p➔s➔ ➔f➔o➔r➔ ➔w➔o➔r➔k➔e➔r➔s➔
➔#➔ ➔S➔T➔E➔P➔ ➔5➔ ➔—➔ ➔V➔a➔l➔i➔d➔a➔t➔e➔ ➔c➔l➔u➔s➔t➔e➔r➔ ➔i➔s➔ ➔r➔e➔a➔d➔y➔
➔k➔o➔p➔s➔ ➔v➔a➔l➔i➔d➔a➔t➔e➔ ➔c➔l➔u➔s➔t➔e➔r➔ ➔-➔-➔w➔a➔i➔t➔ ➔1➔0➔m➔
➔#➔ ➔S➔T➔E➔P➔ ➔6➔ ➔—➔ ➔V➔e➔r➔i➔f➔y➔ ➔n➔o➔d➔e➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔n➔o➔d➔e➔s➔
➔#➔ ➔C➔o➔m➔m➔o➔n➔ ➔k➔O➔p➔s➔ ➔o➔p➔e➔r➔a➔t➔i➔o➔n➔s➔
➔k➔o➔p➔s➔ ➔g➔e➔t➔ ➔c➔l➔u➔s➔t➔e➔r➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔c➔l➔u➔s➔t➔e➔r➔s➔
➔k➔o➔p➔s➔ ➔g➔e➔t➔ ➔i➔g➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔i➔n➔s➔t➔a➔n➔c➔e➔ ➔g➔r➔o➔u➔p➔s➔
➔k➔o➔p➔s➔ ➔e➔d➔i➔t➔ ➔c➔l➔u➔s➔t➔e➔r➔ ➔m➔y➔c➔l➔u➔s➔t➔e➔r➔.➔k➔8➔s➔.➔l➔o➔c➔a➔l➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔d➔i➔t➔ ➔c➔l➔u➔s➔t➔e➔r➔ ➔c➔o➔n➔f➔i➔g➔
➔k➔o➔p➔s➔ ➔r➔o➔l➔l➔i➔n➔g➔-➔u➔p➔d➔a➔t➔e➔ ➔c➔l➔u➔s➔t➔e➔r➔ ➔-➔-➔y➔e➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔p➔p➔l➔y➔ ➔c➔h➔a➔n➔g➔e➔s➔
➔k➔o➔p➔s➔ ➔d➔e➔l➔e➔t➔e➔ ➔c➔l➔u➔s➔t➔e➔r➔ ➔-➔-➔n➔a➔m➔e➔=➔m➔y➔c➔l➔u➔s➔t➔e➔r➔.➔k➔8➔s➔.➔l➔o➔c➔a➔l➔ ➔-➔-➔y➔e➔s➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔c➔l➔u➔s➔t➔e➔r➔
➔6➔.➔ ➔R➔e➔p➔l➔i➔c➔a➔t➔i➔o➔n➔ ➔C➔o➔n➔t➔r➔o➔l➔l➔e➔r➔ ➔v➔s➔ ➔R➔e➔p➔l➔i➔c➔a➔S➔e➔t➔
➔R➔e➔p➔l➔i➔c➔a➔t➔i➔o➔n➔ ➔C➔o➔n➔t➔r➔o➔l➔l➔e➔r➔ ➔(➔O➔l➔d➔ ➔—➔ ➔D➔e➔p➔r➔e➔c➔a➔t➔e➔d➔)➔
➔D➔e➔f➔i➔n➔i➔t➔i➔o➔n➔:➔ ➔E➔n➔s➔u➔r➔e➔s➔ ➔a➔ ➔s➔p➔e➔c➔i➔f➔i➔e➔d➔ ➔n➔u➔m➔b➔e➔r➔ ➔o➔f➔ ➔p➔o➔d➔ ➔r➔e➔p➔l➔i➔c➔a➔s➔ ➔a➔r➔e➔ ➔r➔u➔n➔n➔i➔n➔g➔ ➔a➔t➔ ➔a➔l➔l➔ ➔t➔i➔m➔e➔s➔.➔ ➔I➔f➔ ➔a➔ ➔p➔o➔d➔ ➔d➔i➔e➔s➔,➔ ➔i➔t➔ ➔c➔r➔e➔a➔t➔e➔s➔ ➔a➔ ➔n➔e➔w➔
➔o➔n➔e➔.➔ ➔I➔f➔ ➔t➔h➔e➔r➔e➔ ➔a➔r➔e➔ ➔t➔o➔o➔ ➔m➔a➔n➔y➔,➔ ➔i➔t➔ ➔r➔e➔m➔o➔v➔e➔s➔ ➔s➔o➔m➔e➔.➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔R➔e➔p➔l➔i➔c➔a➔t➔i➔o➔n➔C➔o➔n➔t➔r➔o➔l➔l➔e➔r➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔r➔c➔1➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔r➔e➔p➔l➔i➔c➔a➔s➔:➔ ➔3➔
➔
➔
➔
➔
➔ ➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔:➔
➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔q➔u➔a➔l➔i➔t➔y➔-➔b➔a➔s➔e➔d➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔ ➔o➔n➔l➔y➔
➔ ➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔:➔
➔ ➔ ➔ ➔ ➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔l➔a➔b➔e➔l➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔s➔p➔e➔c➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔c➔1➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔n➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔P➔o➔r➔t➔:➔ ➔8➔0➔
➔R➔e➔p➔l➔i➔c➔a➔S➔e➔t➔ ➔(➔N➔e➔w➔ ➔—➔ ➔U➔s➔e➔ ➔T➔h➔i➔s➔)➔
➔D➔e➔f➔i➔n➔i➔t➔i➔o➔n➔:➔ ➔S➔a➔m➔e➔ ➔a➔s➔ ➔R➔e➔p➔l➔i➔c➔a➔t➔i➔o➔n➔C➔o➔n➔t➔r➔o➔l➔l➔e➔r➔ ➔b➔u➔t➔ ➔s➔u➔p➔p➔o➔r➔t➔s➔ ➔s➔e➔t➔-➔b➔a➔s➔e➔d➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔s➔ ➔(➔m➔o➔r➔e➔ ➔p➔o➔w➔e➔r➔f➔u➔l➔ ➔m➔a➔t➔c➔h➔i➔n➔g➔)➔.➔ ➔U➔s➔u➔a➔l➔l➔y➔
➔m➔a➔n➔a➔g➔e➔d➔ ➔b➔y➔ ➔a➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔.➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔a➔p➔p➔s➔/➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔R➔e➔p➔l➔i➔c➔a➔S➔e➔t➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔r➔s➔1➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔r➔e➔p➔l➔i➔c➔a➔s➔:➔ ➔3➔
➔ ➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔:➔
➔ ➔ ➔ ➔ ➔m➔a➔t➔c➔h➔L➔a➔b➔e➔l➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔t➔-➔b➔a➔s➔e➔d➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔
➔ ➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔:➔
➔ ➔ ➔ ➔ ➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔l➔a➔b➔e➔l➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔s➔p➔e➔c➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔c➔1➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔n➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔P➔o➔r➔t➔:➔ ➔8➔0➔
➔D➔i➔f➔f➔e➔r➔e➔n➔c➔e➔s➔
➔F➔e➔a➔t➔u➔r➔e➔ ➔R➔e➔p➔l➔i➔c➔a➔t➔i➔o➔n➔C➔o➔n➔t➔r➔o➔l➔l➔e➔r➔ ➔R➔e➔p➔l➔i➔c➔a➔S➔e➔t➔
➔A➔P➔I➔ ➔v➔e➔r➔s➔i➔o➔n➔ ➔v➔1➔ ➔a➔p➔p➔s➔/➔v➔1➔
➔S➔e➔l➔e➔c➔t➔o➔r➔ ➔t➔y➔p➔e➔ ➔E➔q➔u➔a➔l➔i➔t➔y➔-➔b➔a➔s➔e➔d➔ ➔o➔n➔l➔y➔ ➔S➔e➔t➔-➔b➔a➔s➔e➔d➔ ➔(➔m➔a➔t➔c➔h➔L➔a➔b➔e➔l➔s➔,➔ ➔m➔a➔t➔c➔h➔E➔x➔p➔r➔e➔s➔s➔i➔o➔n➔s➔)➔
➔
➔
➔
➔
➔S➔t➔a➔t➔u➔s➔ ➔D➔e➔p➔r➔e➔c➔a➔t➔e➔d➔ ➔C➔u➔r➔r➔e➔n➔t➔ ➔s➔t➔a➔n➔d➔a➔r➔d➔
➔U➔s➔e➔d➔ ➔b➔y➔ ➔N➔o➔t➔h➔i➔n➔g➔ ➔(➔o➔l➔d➔)➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔s➔
➔D➔i➔r➔e➔c➔t➔ ➔u➔s➔e➔ ➔A➔v➔o➔i➔d➔ ➔A➔v➔o➔i➔d➔ ➔(➔u➔s➔e➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔s➔ ➔i➔n➔s➔t➔e➔a➔d➔)➔
➔C➔o➔m➔m➔a➔n➔d➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔r➔c➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔r➔e➔p➔l➔i➔c➔a➔t➔i➔o➔n➔ ➔c➔o➔n➔t➔r➔o➔l➔l➔e➔r➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔r➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔r➔e➔p➔l➔i➔c➔a➔ ➔s➔e➔t➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔r➔s➔ ➔r➔s➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔t➔a➔i➔l➔s➔ ➔o➔f➔ ➔r➔e➔p➔l➔i➔c➔a➔ ➔s➔e➔t➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔s➔c➔a➔l➔e➔ ➔r➔s➔ ➔r➔s➔1➔ ➔-➔-➔r➔e➔p➔l➔i➔c➔a➔s➔=➔5➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔c➔a➔l➔e➔ ➔r➔e➔p➔l➔i➔c➔a➔ ➔s➔e➔t➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔l➔e➔t➔e➔ ➔r➔s➔ ➔r➔s➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔r➔e➔p➔l➔i➔c➔a➔ ➔s➔e➔t➔
➔7➔.➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔s➔ ➔—➔ ➔C➔o➔m➔p➔l➔e➔t➔e➔ ➔G➔u➔i➔d➔e➔
➔D➔e➔f➔i➔n➔i➔t➔i➔o➔n➔:➔ ➔A➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔m➔a➔n➔a➔g➔e➔s➔ ➔R➔e➔p➔l➔i➔c➔a➔S➔e➔t➔s➔ ➔a➔n➔d➔ ➔p➔r➔o➔v➔i➔d➔e➔s➔ ➔d➔e➔c➔l➔a➔r➔a➔t➔i➔v➔e➔ ➔u➔p➔d➔a➔t➔e➔s➔.➔ ➔I➔t➔'➔s➔ ➔t➔h➔e➔ ➔s➔t➔a➔n➔d➔a➔r➔d➔ ➔w➔a➔y➔ ➔t➔o➔ ➔r➔u➔n➔
➔s➔t➔a➔t➔e➔l➔e➔s➔s➔ ➔a➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔s➔.➔
➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔→➔ ➔m➔a➔n➔a➔g➔e➔s➔ ➔→➔ ➔R➔e➔p➔l➔i➔c➔a➔S➔e➔t➔ ➔→➔ ➔m➔a➔n➔a➔g➔e➔s➔ ➔→➔ ➔P➔o➔d➔s➔
➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔Y➔A➔M➔L➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔a➔p➔p➔s➔/➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔d➔p➔1➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔r➔e➔p➔l➔i➔c➔a➔s➔:➔ ➔3➔
➔ ➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔:➔
➔ ➔ ➔ ➔ ➔m➔a➔t➔c➔h➔L➔a➔b➔e➔l➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔s➔t➔r➔a➔t➔e➔g➔y➔:➔
➔ ➔ ➔ ➔ ➔t➔y➔p➔e➔:➔ ➔R➔o➔l➔l➔i➔n➔g➔U➔p➔d➔a➔t➔e➔
➔ ➔ ➔ ➔ ➔r➔o➔l➔l➔i➔n➔g➔U➔p➔d➔a➔t➔e➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔m➔a➔x➔S➔u➔r➔g➔e➔:➔ ➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔m➔a➔x➔ ➔p➔o➔d➔s➔ ➔a➔b➔o➔v➔e➔ ➔d➔e➔s➔i➔r➔e➔d➔ ➔d➔u➔r➔i➔n➔g➔ ➔u➔p➔d➔a➔t➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔m➔a➔x➔U➔n➔a➔v➔a➔i➔l➔a➔b➔l➔e➔:➔ ➔1➔ ➔ ➔ ➔ ➔#➔ ➔m➔a➔x➔ ➔p➔o➔d➔s➔ ➔b➔e➔l➔o➔w➔ ➔d➔e➔s➔i➔r➔e➔d➔ ➔d➔u➔r➔i➔n➔g➔ ➔u➔p➔d➔a➔t➔e➔
➔ ➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔:➔
➔ ➔ ➔ ➔ ➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔l➔a➔b➔e➔l➔s➔:➔
➔
➔
➔
➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔s➔p➔e➔c➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔c➔1➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔n➔g➔i➔n➔x➔:➔1➔.➔1➔9➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔P➔o➔r➔t➔:➔ ➔8➔0➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔r➔e➔q➔u➔e➔s➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔c➔p➔u➔:➔ ➔"➔2➔5➔0➔m➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔m➔e➔m➔o➔r➔y➔:➔ ➔"➔1➔2➔8➔M➔i➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔l➔i➔m➔i➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔c➔p➔u➔:➔ ➔"➔5➔0➔0➔m➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔m➔e➔m➔o➔r➔y➔:➔ ➔"➔2➔5➔6➔M➔i➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔l➔i➔v➔e➔n➔e➔s➔s➔P➔r➔o➔b➔e➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔h➔t➔t➔p➔G➔e➔t➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔a➔t➔h➔:➔ ➔/➔h➔e➔a➔l➔t➔h➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔o➔r➔t➔:➔ ➔8➔0➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔i➔n➔i➔t➔i➔a➔l➔D➔e➔l➔a➔y➔S➔e➔c➔o➔n➔d➔s➔:➔ ➔1➔0➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔e➔r➔i➔o➔d➔S➔e➔c➔o➔n➔d➔s➔:➔ ➔5➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔r➔e➔a➔d➔i➔n➔e➔s➔s➔P➔r➔o➔b➔e➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔h➔t➔t➔p➔G➔e➔t➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔a➔t➔h➔:➔ ➔/➔r➔e➔a➔d➔y➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔o➔r➔t➔:➔ ➔8➔0➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔i➔n➔i➔t➔i➔a➔l➔D➔e➔l➔a➔y➔S➔e➔c➔o➔n➔d➔s➔:➔ ➔5➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔e➔r➔i➔o➔d➔S➔e➔c➔o➔n➔d➔s➔:➔ ➔3➔
➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔
➔#➔ ➔C➔r➔e➔a➔t➔e➔ ➔/➔ ➔A➔p➔p➔l➔y➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔a➔p➔p➔l➔y➔ ➔-➔f➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔.➔y➔a➔m➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔o➔r➔ ➔u➔p➔d➔a➔t➔e➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔c➔r➔e➔a➔t➔e➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔d➔p➔1➔ ➔-➔-➔i➔m➔a➔g➔e➔=➔n➔g➔i➔n➔x➔ ➔ ➔#➔ ➔q➔u➔i➔c➔k➔ ➔c➔r➔e➔a➔t➔e➔
➔#➔ ➔V➔i➔e➔w➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔d➔e➔p➔l➔o➔y➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔r➔t➔ ➔f➔o➔r➔m➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔d➔p➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔t➔a➔i➔l➔e➔d➔ ➔i➔n➔f➔o➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔p➔o➔d➔s➔ ➔-➔l➔ ➔a➔p➔p➔=➔m➔y➔a➔p➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔o➔d➔s➔ ➔o➔f➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔
➔#➔ ➔S➔c➔a➔l➔e➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔s➔c➔a➔l➔e➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔d➔p➔1➔ ➔-➔-➔r➔e➔p➔l➔i➔c➔a➔s➔=➔5➔ ➔ ➔ ➔ ➔#➔ ➔s➔c➔a➔l➔e➔ ➔t➔o➔ ➔5➔ ➔p➔o➔d➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔a➔u➔t➔o➔s➔c➔a➔l➔e➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔d➔p➔1➔ ➔-➔-➔m➔i➔n➔=➔2➔ ➔-➔-➔m➔a➔x➔=➔1➔0➔ ➔-➔-➔c➔p➔u➔-➔p➔e➔r➔c➔e➔n➔t➔=➔7➔0➔ ➔ ➔#➔ ➔H➔P➔A➔
➔#➔ ➔U➔p➔d➔a➔t➔e➔ ➔i➔m➔a➔g➔e➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔s➔e➔t➔ ➔i➔m➔a➔g➔e➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔/➔d➔p➔1➔ ➔c➔1➔=➔n➔g➔i➔n➔x➔:➔1➔.➔2➔0➔ ➔ ➔#➔ ➔u➔p➔d➔a➔t➔e➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔i➔m➔a➔g➔e➔
➔#➔ ➔R➔o➔l➔l➔o➔u➔t➔ ➔m➔a➔n➔a➔g➔e➔m➔e➔n➔t➔
➔
➔
➔
➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔r➔o➔l➔l➔o➔u➔t➔ ➔s➔t➔a➔t➔u➔s➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔/➔d➔p➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔e➔c➔k➔ ➔r➔o➔l➔l➔o➔u➔t➔ ➔p➔r➔o➔g➔r➔e➔s➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔r➔o➔l➔l➔o➔u➔t➔ ➔h➔i➔s➔t➔o➔r➔y➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔/➔d➔p➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔v➔i➔e➔w➔ ➔r➔e➔v➔i➔s➔i➔o➔n➔ ➔h➔i➔s➔t➔o➔r➔y➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔r➔o➔l➔l➔o➔u➔t➔ ➔h➔i➔s➔t➔o➔r➔y➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔/➔d➔p➔1➔ ➔-➔-➔r➔e➔v➔i➔s➔i➔o➔n➔=➔2➔ ➔ ➔#➔ ➔d➔e➔t➔a➔i➔l➔s➔ ➔o➔f➔ ➔r➔e➔v➔i➔s➔i➔o➔n➔ ➔2➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔r➔o➔l➔l➔o➔u➔t➔ ➔u➔n➔d➔o➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔/➔d➔p➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔o➔l➔l➔b➔a➔c➔k➔ ➔t➔o➔ ➔p➔r➔e➔v➔i➔o➔u➔s➔ ➔v➔e➔r➔s➔i➔o➔n➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔r➔o➔l➔l➔o➔u➔t➔ ➔u➔n➔d➔o➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔/➔d➔p➔1➔ ➔-➔-➔t➔o➔-➔r➔e➔v➔i➔s➔i➔o➔n➔=➔2➔ ➔ ➔#➔ ➔r➔o➔l➔l➔b➔a➔c➔k➔ ➔t➔o➔ ➔r➔e➔v➔i➔s➔i➔o➔n➔ ➔2➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔r➔o➔l➔l➔o➔u➔t➔ ➔p➔a➔u➔s➔e➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔/➔d➔p➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔a➔u➔s➔e➔ ➔r➔o➔l➔l➔o➔u➔t➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔r➔o➔l➔l➔o➔u➔t➔ ➔r➔e➔s➔u➔m➔e➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔/➔d➔p➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔s➔u➔m➔e➔ ➔r➔o➔l➔l➔o➔u➔t➔
➔#➔ ➔D➔e➔l➔e➔t➔e➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔l➔e➔t➔e➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔d➔p➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔l➔e➔t➔e➔ ➔-➔f➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔.➔y➔a➔m➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔f➔r➔o➔m➔ ➔f➔i➔l➔e➔
➔#➔ ➔G➔e➔t➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔Y➔A➔M➔L➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔d➔p➔1➔ ➔-➔o➔ ➔y➔a➔m➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔v➔i➔e➔w➔ ➔a➔s➔ ➔Y➔A➔M➔L➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔d➔p➔1➔ ➔-➔o➔ ➔j➔s➔o➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔v➔i➔e➔w➔ ➔a➔s➔ ➔J➔S➔O➔N➔
➔8➔.➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔ ➔S➔e➔r➔v➔i➔c➔e➔s➔ ➔—➔ ➔3➔ ➔T➔y➔p➔e➔s➔ ➔w➔i➔t➔h➔ ➔Y➔A➔M➔L➔
➔D➔e➔f➔i➔n➔i➔t➔i➔o➔n➔:➔ ➔A➔ ➔S➔e➔r➔v➔i➔c➔e➔ ➔p➔r➔o➔v➔i➔d➔e➔s➔ ➔a➔ ➔s➔t➔a➔b➔l➔e➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔e➔n➔d➔p➔o➔i➔n➔t➔ ➔f➔o➔r➔ ➔a➔ ➔s➔e➔t➔ ➔o➔f➔ ➔p➔o➔d➔s➔.➔ ➔P➔o➔d➔s➔ ➔a➔r➔e➔ ➔e➔p➔h➔e➔m➔e➔r➔a➔l➔ ➔(➔I➔P➔s➔ ➔c➔h➔a➔n➔g➔e➔)➔,➔
➔S➔e➔r➔v➔i➔c➔e➔s➔ ➔a➔r➔e➔ ➔s➔t➔a➔b➔l➔e➔.➔
➔T➔y➔p➔e➔ ➔1➔:➔ ➔C➔l➔u➔s➔t➔e➔r➔I➔P➔ ➔(➔I➔n➔t➔e➔r➔n➔a➔l➔ ➔O➔n➔l➔y➔)➔
➔#➔ ➔c➔l➔u➔s➔t➔e➔r➔I➔P➔.➔y➔a➔m➔l➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔S➔e➔r➔v➔i➔c➔e➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔c➔i➔p➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔t➔y➔p➔e➔:➔ ➔C➔l➔u➔s➔t➔e➔r➔I➔P➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔f➔a➔u➔l➔t➔ ➔t➔y➔p➔e➔ ➔—➔ ➔i➔n➔t➔e➔r➔n➔a➔l➔ ➔a➔c➔c➔e➔s➔s➔ ➔o➔n➔l➔y➔
➔ ➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔:➔
➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔ ➔ ➔-➔ ➔p➔o➔r➔t➔:➔ ➔8➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔S➔e➔r➔v➔i➔c➔e➔ ➔p➔o➔r➔t➔ ➔(➔w➔h➔a➔t➔ ➔c➔l➔i➔e➔n➔t➔s➔ ➔c➔o➔n➔n➔e➔c➔t➔ ➔t➔o➔)➔
➔ ➔ ➔ ➔ ➔t➔a➔r➔g➔e➔t➔P➔o➔r➔t➔:➔ ➔8➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔p➔o➔r➔t➔ ➔(➔w➔h➔e➔r➔e➔ ➔t➔r➔a➔f➔f➔i➔c➔ ➔g➔o➔e➔s➔)➔
➔U➔s➔e➔ ➔w➔h➔e➔n➔:➔ ➔P➔o➔d➔-➔t➔o➔-➔P➔o➔d➔ ➔c➔o➔m➔m➔u➔n➔i➔c➔a➔t➔i➔o➔n➔ ➔i➔n➔s➔i➔d➔e➔ ➔c➔l➔u➔s➔t➔e➔r➔
➔A➔c➔c➔e➔s➔s➔:➔ ➔O➔n➔l➔y➔ ➔f➔r➔o➔m➔ ➔w➔i➔t➔h➔i➔n➔ ➔t➔h➔e➔ ➔c➔l➔u➔s➔t➔e➔r➔
➔E➔x➔a➔m➔p➔l➔e➔:➔ ➔B➔a➔c➔k➔e➔n➔d➔ ➔c➔o➔n➔n➔e➔c➔t➔i➔n➔g➔ ➔t➔o➔ ➔d➔a➔t➔a➔b➔a➔s➔e➔
➔
➔
➔
➔
➔T➔y➔p➔e➔ ➔2➔:➔ ➔N➔o➔d➔e➔P➔o➔r➔t➔ ➔(➔E➔x➔t➔e➔r➔n➔a➔l➔ ➔v➔i➔a➔ ➔N➔o➔d➔e➔ ➔I➔P➔)➔
➔#➔ ➔n➔o➔d➔e➔p➔o➔r➔t➔.➔y➔a➔m➔l➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔S➔e➔r➔v➔i➔c➔e➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔n➔p➔1➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔t➔y➔p➔e➔:➔ ➔N➔o➔d➔e➔P➔o➔r➔t➔
➔ ➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔:➔
➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔ ➔ ➔-➔ ➔p➔o➔r➔t➔:➔ ➔8➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔C➔l➔u➔s➔t➔e➔r➔I➔P➔ ➔p➔o➔r➔t➔
➔ ➔ ➔ ➔ ➔t➔a➔r➔g➔e➔t➔P➔o➔r➔t➔:➔ ➔8➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔p➔o➔r➔t➔
➔ ➔ ➔ ➔ ➔n➔o➔d➔e➔P➔o➔r➔t➔:➔ ➔3➔1➔2➔0➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔P➔o➔r➔t➔ ➔o➔n➔ ➔e➔a➔c➔h➔ ➔n➔o➔d➔e➔ ➔(➔3➔0➔0➔0➔0➔-➔3➔2➔7➔6➔7➔)➔
➔U➔s➔e➔ ➔w➔h➔e➔n➔:➔ ➔N➔e➔e➔d➔ ➔e➔x➔t➔e➔r➔n➔a➔l➔ ➔a➔c➔c➔e➔s➔s➔ ➔w➔i➔t➔h➔o➔u➔t➔ ➔c➔l➔o➔u➔d➔ ➔l➔o➔a➔d➔ ➔b➔a➔l➔a➔n➔c➔e➔r➔
➔A➔c➔c➔e➔s➔s➔:➔ ➔h➔t➔t➔p➔:➔/➔/➔<➔n➔o➔d➔e➔-➔i➔p➔>➔:➔3➔1➔2➔0➔0➔
➔E➔x➔a➔m➔p➔l➔e➔:➔ ➔D➔e➔v➔/➔t➔e➔s➔t➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔s➔
➔T➔y➔p➔e➔ ➔3➔:➔ ➔L➔o➔a➔d➔B➔a➔l➔a➔n➔c➔e➔r➔ ➔(➔C➔l➔o➔u➔d➔ ➔L➔o➔a➔d➔ ➔B➔a➔l➔a➔n➔c➔e➔r➔)➔
➔#➔ ➔l➔o➔a➔d➔b➔a➔l➔a➔n➔c➔e➔r➔.➔y➔a➔m➔l➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔S➔e➔r➔v➔i➔c➔e➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔l➔b➔1➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔t➔y➔p➔e➔:➔ ➔L➔o➔a➔d➔B➔a➔l➔a➔n➔c➔e➔r➔
➔ ➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔:➔
➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔ ➔ ➔-➔ ➔p➔o➔r➔t➔:➔ ➔8➔0➔
➔ ➔ ➔ ➔ ➔t➔a➔r➔g➔e➔t➔P➔o➔r➔t➔:➔ ➔8➔0➔
➔ ➔ ➔ ➔ ➔n➔o➔d➔e➔P➔o➔r➔t➔:➔ ➔3➔1➔2➔0➔0➔
➔U➔s➔e➔ ➔w➔h➔e➔n➔:➔ ➔P➔r➔o➔d➔u➔c➔t➔i➔o➔n➔,➔ ➔n➔e➔e➔d➔ ➔e➔x➔t➔e➔r➔n➔a➔l➔ ➔a➔c➔c➔e➔s➔s➔ ➔w➔i➔t➔h➔ ➔s➔i➔n➔g➔l➔e➔ ➔e➔n➔d➔p➔o➔i➔n➔t➔
➔A➔c➔c➔e➔s➔s➔:➔ ➔C➔l➔o➔u➔d➔ ➔p➔r➔o➔v➔i➔d➔e➔s➔ ➔e➔x➔t➔e➔r➔n➔a➔l➔ ➔I➔P➔/➔D➔N➔S➔
➔E➔x➔a➔m➔p➔l➔e➔:➔ ➔P➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔w➔e➔b➔ ➔a➔p➔p➔ ➔o➔n➔ ➔A➔W➔S➔ ➔(➔c➔r➔e➔a➔t➔e➔s➔ ➔E➔L➔B➔)➔
➔S➔e➔r➔v➔i➔c➔e➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔
➔
➔
➔
➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔s➔e➔r➔v➔i➔c➔e➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔s➔e➔r➔v➔i➔c➔e➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔s➔v➔c➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔r➔t➔ ➔f➔o➔r➔m➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔s➔v➔c➔ ➔m➔y➔s➔e➔r➔v➔i➔c➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔r➔v➔i➔c➔e➔ ➔d➔e➔t➔a➔i➔l➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔l➔e➔t➔e➔ ➔s➔v➔c➔ ➔m➔y➔s➔e➔r➔v➔i➔c➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔s➔e➔r➔v➔i➔c➔e➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔e➔x➔p➔o➔s➔e➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔d➔p➔1➔ ➔-➔-➔p➔o➔r➔t➔=➔8➔0➔ ➔-➔-➔t➔y➔p➔e➔=➔L➔o➔a➔d➔B➔a➔l➔a➔n➔c➔e➔r➔ ➔ ➔#➔ ➔q➔u➔i➔c➔k➔ ➔c➔r➔e➔a➔t➔e➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔e➔n➔d➔p➔o➔i➔n➔t➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔e➔ ➔w➔h➔i➔c➔h➔ ➔p➔o➔d➔s➔ ➔s➔e➔r➔v➔i➔c➔e➔ ➔r➔o➔u➔t➔e➔s➔ ➔t➔o➔
➔P➔o➔d➔ ➔+➔ ➔S➔e➔r➔v➔i➔c➔e➔ ➔Y➔A➔M➔L➔ ➔(➔C➔o➔m➔b➔i➔n➔e➔d➔)➔
➔#➔ ➔b➔a➔c➔k➔e➔n➔d➔-➔p➔o➔d➔-➔a➔n➔d➔-➔s➔e➔r➔v➔i➔c➔e➔.➔y➔a➔m➔l➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔P➔o➔d➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔b➔a➔c➔k➔e➔n➔d➔-➔p➔o➔d➔
➔ ➔ ➔l➔a➔b➔e➔l➔s➔:➔
➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔b➔a➔c➔k➔e➔n➔d➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔
➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔b➔a➔c➔k➔e➔n➔d➔
➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔n➔o➔d➔e➔:➔1➔8➔
➔ ➔ ➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔P➔o➔r➔t➔:➔ ➔3➔0➔0➔0➔
➔-➔-➔-➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔S➔e➔r➔v➔i➔c➔e➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔b➔a➔c➔k➔e➔n➔d➔-➔s➔e➔r➔v➔i➔c➔e➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔t➔y➔p➔e➔:➔ ➔N➔o➔d➔e➔P➔o➔r➔t➔
➔ ➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔:➔
➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔b➔a➔c➔k➔e➔n➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔m➔a➔t➔c➔h➔e➔s➔ ➔p➔o➔d➔ ➔l➔a➔b➔e➔l➔
➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔ ➔ ➔-➔ ➔p➔o➔r➔t➔:➔ ➔8➔0➔
➔ ➔ ➔ ➔ ➔t➔a➔r➔g➔e➔t➔P➔o➔r➔t➔:➔ ➔3➔0➔0➔0➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔o➔d➔'➔s➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔p➔o➔r➔t➔
➔9➔.➔ ➔N➔a➔m➔e➔s➔p➔a➔c➔e➔s➔
➔D➔e➔f➔i➔n➔i➔t➔i➔o➔n➔:➔ ➔N➔a➔m➔e➔s➔p➔a➔c➔e➔s➔ ➔l➔o➔g➔i➔c➔a➔l➔l➔y➔ ➔p➔a➔r➔t➔i➔t➔i➔o➔n➔ ➔a➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔ ➔c➔l➔u➔s➔t➔e➔r➔ ➔i➔n➔t➔o➔ ➔i➔s➔o➔l➔a➔t➔e➔d➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔s➔.➔ ➔R➔e➔s➔o➔u➔r➔c➔e➔s➔ ➔i➔n➔ ➔o➔n➔e➔
➔n➔a➔m➔e➔s➔p➔a➔c➔e➔ ➔d➔o➔n➔'➔t➔ ➔i➔n➔t➔e➔r➔a➔c➔t➔ ➔w➔i➔t➔h➔ ➔a➔n➔o➔t➔h➔e➔r➔ ➔b➔y➔ ➔d➔e➔f➔a➔u➔l➔t➔.➔
➔
➔
➔
➔
➔T➔y➔p➔e➔s➔ ➔o➔f➔ ➔N➔a➔m➔e➔s➔p➔a➔c➔e➔s➔
➔B➔u➔i➔l➔t➔-➔i➔n➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔s➔:➔
➔N➔a➔m➔e➔s➔p➔a➔c➔e➔ ➔P➔u➔r➔p➔o➔s➔e➔
➔d➔e➔f➔a➔u➔l➔t➔ ➔W➔h➔e➔r➔e➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔s➔ ➔g➔o➔ ➔i➔f➔ ➔y➔o➔u➔ ➔d➔o➔n➔'➔t➔ ➔s➔p➔e➔c➔i➔f➔y➔ ➔a➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔
➔k➔u➔b➔e➔-➔s➔y➔s➔t➔e➔m➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔ ➔s➔y➔s➔t➔e➔m➔ ➔c➔o➔m➔p➔o➔n➔e➔n➔t➔s➔ ➔(➔A➔P➔I➔ ➔s➔e➔r➔v➔e➔r➔,➔ ➔D➔N➔S➔,➔ ➔s➔c➔h➔e➔d➔u➔l➔e➔r➔)➔
➔k➔u➔b➔e➔-➔p➔u➔b➔l➔i➔c➔ ➔R➔e➔a➔d➔a➔b➔l➔e➔ ➔b➔y➔ ➔a➔l➔l➔ ➔u➔s➔e➔r➔s➔,➔ ➔u➔s➔e➔d➔ ➔f➔o➔r➔ ➔c➔l➔u➔s➔t➔e➔r➔ ➔i➔n➔f➔o➔
➔k➔u➔b➔e➔-➔n➔o➔d➔e➔-➔l➔e➔a➔s➔e➔ ➔N➔o➔d➔e➔ ➔h➔e➔a➔r➔t➔b➔e➔a➔t➔ ➔d➔a➔t➔a➔ ➔(➔i➔n➔t➔e➔r➔n➔a➔l➔ ➔u➔s➔e➔)➔
➔C➔u➔s➔t➔o➔m➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔s➔ ➔(➔y➔o➔u➔ ➔c➔r➔e➔a➔t➔e➔ ➔t➔h➔e➔s➔e➔)➔:➔
➔d➔e➔v➔ ➔ ➔—➔ ➔d➔e➔v➔e➔l➔o➔p➔m➔e➔n➔t➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔
➔s➔t➔a➔g➔i➔n➔g➔ ➔ ➔—➔ ➔s➔t➔a➔g➔i➔n➔g➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔
➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔ ➔—➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔
➔m➔o➔n➔i➔t➔o➔r➔i➔n➔g➔ ➔ ➔—➔ ➔P➔r➔o➔m➔e➔t➔h➔e➔u➔s➔,➔ ➔G➔r➔a➔f➔a➔n➔a➔
➔N➔a➔m➔e➔s➔p➔a➔c➔e➔ ➔Y➔A➔M➔L➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔N➔a➔m➔e➔s➔p➔a➔c➔e➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔d➔e➔v➔
➔N➔a➔m➔e➔s➔p➔a➔c➔e➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔
➔#➔ ➔C➔r➔e➔a➔t➔e➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔c➔r➔e➔a➔t➔e➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔ ➔d➔e➔v➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔a➔p➔p➔l➔y➔ ➔-➔f➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔.➔y➔a➔m➔l➔
➔#➔ ➔V➔i➔e➔w➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔a➔l➔l➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔n➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔r➔t➔ ➔f➔o➔r➔m➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔ ➔d➔e➔v➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔t➔a➔i➔l➔s➔
➔#➔ ➔U➔s➔e➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔p➔o➔d➔s➔ ➔-➔n➔ ➔d➔e➔v➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔o➔d➔s➔ ➔i➔n➔ ➔d➔e➔v➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔a➔l➔l➔ ➔-➔n➔ ➔k➔u➔b➔e➔-➔s➔y➔s➔t➔e➔m➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔l➔l➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔s➔ ➔i➔n➔ ➔k➔u➔b➔e➔-➔s➔y➔s➔t➔e➔m➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔a➔p➔p➔l➔y➔ ➔-➔f➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔.➔y➔a➔m➔l➔ ➔-➔n➔ ➔d➔e➔v➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔p➔l➔o➔y➔ ➔t➔o➔ ➔d➔e➔v➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔
➔
➔
➔
➔
➔➔ ➔➔
➔➔ ➔➔
➔#➔ ➔S➔e➔t➔ ➔d➔e➔f➔a➔u➔l➔t➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔ ➔f➔o➔r➔ ➔s➔e➔s➔s➔i➔o➔n➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔c➔o➔n➔f➔i➔g➔ ➔s➔e➔t➔-➔c➔o➔n➔t➔e➔x➔t➔ ➔-➔-➔c➔u➔r➔r➔e➔n➔t➔ ➔-➔-➔n➔a➔m➔e➔s➔p➔a➔c➔e➔=➔d➔e➔v➔
➔#➔ ➔D➔e➔l➔e➔t➔e➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔l➔e➔t➔e➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔ ➔d➔e➔v➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔W➔A➔R➔N➔I➔N➔G➔:➔ ➔d➔e➔l➔e➔t➔e➔s➔ ➔e➔v➔e➔r➔y➔t➔h➔i➔n➔g➔ ➔i➔n➔s➔i➔d➔e➔!➔
➔#➔ ➔R➔e➔s➔o➔u➔r➔c➔e➔ ➔Q➔u➔o➔t➔a➔ ➔p➔e➔r➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔a➔p➔p➔l➔y➔ ➔-➔f➔ ➔-➔ ➔<➔<➔E➔O➔F➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔R➔e➔s➔o➔u➔r➔c➔e➔Q➔u➔o➔t➔a➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔d➔e➔v➔-➔q➔u➔o➔t➔a➔
➔ ➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔:➔ ➔d➔e➔v➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔h➔a➔r➔d➔:➔
➔ ➔ ➔ ➔ ➔p➔o➔d➔s➔:➔ ➔"➔1➔0➔"➔
➔ ➔ ➔ ➔ ➔r➔e➔q➔u➔e➔s➔t➔s➔.➔c➔p➔u➔:➔ ➔"➔2➔"➔
➔ ➔ ➔ ➔ ➔r➔e➔q➔u➔e➔s➔t➔s➔.➔m➔e➔m➔o➔r➔y➔:➔ ➔4➔G➔i➔
➔ ➔ ➔ ➔ ➔l➔i➔m➔i➔t➔s➔.➔c➔p➔u➔:➔ ➔"➔4➔"➔
➔ ➔ ➔ ➔ ➔l➔i➔m➔i➔t➔s➔.➔m➔e➔m➔o➔r➔y➔:➔ ➔8➔G➔i➔
➔E➔O➔F➔
➔1➔0➔.➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔ ➔V➔o➔l➔u➔m➔e➔s➔ ➔—➔ ➔C➔o➔m➔p➔l➔e➔t➔e➔ ➔G➔u➔i➔d➔e➔
➔V➔o➔l➔u➔m➔e➔ ➔T➔y➔p➔e➔s➔ ➔C➔o➔m➔p➔a➔r➔i➔s➔o➔n➔
➔e➔m➔p➔t➔y➔D➔i➔r➔ ➔ ➔ ➔ ➔→➔ ➔T➔e➔m➔p➔o➔r➔a➔r➔y➔,➔ ➔s➔h➔a➔r➔e➔d➔ ➔b➔e➔t➔w➔e➔e➔n➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔i➔n➔ ➔s➔a➔m➔e➔ ➔p➔o➔d➔,➔ ➔d➔e➔l➔e➔t➔e➔d➔ ➔w➔h➔e➔n➔ ➔p➔o➔d➔ ➔d➔i➔e➔s➔
➔h➔o➔s➔t➔P➔a➔t➔h➔ ➔ ➔ ➔ ➔→➔ ➔U➔s➔e➔s➔ ➔n➔o➔d➔e➔'➔s➔ ➔f➔i➔l➔e➔s➔y➔s➔t➔e➔m➔,➔ ➔p➔e➔r➔s➔i➔s➔t➔s➔ ➔b➔e➔y➔o➔n➔d➔ ➔p➔o➔d➔,➔ ➔t➔i➔e➔d➔ ➔t➔o➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔n➔o➔d➔e➔
➔P➔V➔ ➔+➔ ➔P➔V➔C➔ ➔ ➔ ➔ ➔→➔ ➔F➔u➔l➔l➔y➔ ➔p➔e➔r➔s➔i➔s➔t➔e➔n➔t➔,➔ ➔i➔n➔d➔e➔p➔e➔n➔d➔e➔n➔t➔ ➔o➔f➔ ➔p➔o➔d➔s➔ ➔a➔n➔d➔ ➔n➔o➔d➔e➔s➔,➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔s➔t➔a➔n➔d➔a➔r➔d➔
➔C➔o➔n➔f➔i➔g➔M➔a➔p➔ ➔ ➔ ➔→➔ ➔M➔o➔u➔n➔t➔ ➔c➔o➔n➔f➔i➔g➔ ➔f➔i➔l➔e➔s➔ ➔i➔n➔t➔o➔ ➔p➔o➔d➔s➔
➔S➔e➔c➔r➔e➔t➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔M➔o➔u➔n➔t➔ ➔s➔e➔n➔s➔i➔t➔i➔v➔e➔ ➔d➔a➔t➔a➔ ➔i➔n➔t➔o➔ ➔p➔o➔d➔s➔
➔T➔y➔p➔e➔ ➔1➔:➔ ➔e➔m➔p➔t➔y➔D➔i➔r➔ ➔—➔ ➔T➔e➔m➔p➔o➔r➔a➔r➔y➔ ➔S➔h➔a➔r➔e➔d➔ ➔V➔o➔l➔u➔m➔e➔
➔D➔e➔f➔i➔n➔i➔t➔i➔o➔n➔:➔ ➔C➔r➔e➔a➔t➔e➔d➔ ➔w➔h➔e➔n➔ ➔a➔ ➔p➔o➔d➔ ➔s➔t➔a➔r➔t➔s➔.➔ ➔D➔e➔l➔e➔t➔e➔d➔ ➔w➔h➔e➔n➔ ➔t➔h➔e➔ ➔p➔o➔d➔ ➔i➔s➔ ➔r➔e➔m➔o➔v➔e➔d➔.➔ ➔S➔h➔a➔r➔e➔d➔ ➔b➔e➔t➔w➔e➔e➔n➔ ➔a➔l➔l➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔i➔n➔ ➔t➔h➔e➔
➔s➔a➔m➔e➔ ➔p➔o➔d➔.➔ ➔U➔s➔e➔d➔ ➔f➔o➔r➔ ➔c➔a➔c➔h➔i➔n➔g➔,➔ ➔t➔e➔m➔p➔o➔r➔a➔r➔y➔ ➔p➔r➔o➔c➔e➔s➔s➔i➔n➔g➔.➔
➔#➔ ➔e➔m➔p➔t➔y➔d➔i➔r➔-➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔.➔y➔a➔m➔l➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔a➔p➔p➔s➔/➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔
➔
➔
➔
➔➔ ➔➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔d➔p➔1➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔r➔e➔p➔l➔i➔c➔a➔s➔:➔ ➔2➔
➔ ➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔:➔
➔ ➔ ➔ ➔ ➔m➔a➔t➔c➔h➔L➔a➔b➔e➔l➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔:➔
➔ ➔ ➔ ➔ ➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔l➔a➔b➔e➔l➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔s➔p➔e➔c➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔c➔1➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔h➔t➔t➔p➔d➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔P➔o➔r➔t➔:➔ ➔8➔0➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔v➔o➔l➔u➔m➔e➔M➔o➔u➔n➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔v➔1➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔m➔o➔u➔n➔t➔P➔a➔t➔h➔:➔ ➔/➔u➔s➔r➔/➔l➔o➔c➔a➔l➔/➔a➔p➔a➔c➔h➔e➔2➔/➔h➔t➔d➔o➔c➔s➔ ➔ ➔ ➔#➔ ➔w➔h➔e➔r➔e➔ ➔v➔o➔l➔u➔m➔e➔ ➔a➔p➔p➔e➔a➔r➔s➔ ➔i➔n➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔ ➔ ➔ ➔ ➔ ➔ ➔v➔o➔l➔u➔m➔e➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔v➔1➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔e➔m➔p➔t➔y➔D➔i➔r➔:➔ ➔{➔}➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔m➔p➔t➔y➔,➔ ➔n➔o➔ ➔s➔o➔u➔r➔c➔e➔
➔U➔s➔e➔ ➔w➔h➔e➔n➔:➔ ➔T➔w➔o➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔i➔n➔ ➔s➔a➔m➔e➔ ➔p➔o➔d➔ ➔n➔e➔e➔d➔ ➔t➔o➔ ➔s➔h➔a➔r➔e➔ ➔d➔a➔t➔a➔ ➔t➔e➔m➔p➔o➔r➔a➔r➔i➔l➔y➔
➔E➔x➔a➔m➔p➔l➔e➔:➔ ➔S➔i➔d➔e➔c➔a➔r➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔p➔r➔o➔c➔e➔s➔s➔e➔s➔ ➔l➔o➔g➔s➔ ➔b➔e➔f➔o➔r➔e➔ ➔m➔a➔i➔n➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔r➔e➔a➔d➔s➔ ➔t➔h➔e➔m➔
➔L➔i➔f➔e➔c➔y➔c➔l➔e➔:➔ ➔D➔i➔e➔s➔ ➔w➔i➔t➔h➔ ➔t➔h➔e➔ ➔p➔o➔d➔
➔T➔y➔p➔e➔ ➔2➔:➔ ➔h➔o➔s➔t➔P➔a➔t➔h➔ ➔—➔ ➔N➔o➔d➔e➔ ➔F➔i➔l➔e➔s➔y➔s➔t➔e➔m➔ ➔V➔o➔l➔u➔m➔e➔
➔D➔e➔f➔i➔n➔i➔t➔i➔o➔n➔:➔ ➔M➔o➔u➔n➔t➔s➔ ➔a➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔f➔r➔o➔m➔ ➔t➔h➔e➔ ➔n➔o➔d➔e➔'➔s➔ ➔f➔i➔l➔e➔s➔y➔s➔t➔e➔m➔ ➔i➔n➔t➔o➔ ➔t➔h➔e➔ ➔p➔o➔d➔.➔ ➔P➔e➔r➔s➔i➔s➔t➔s➔ ➔b➔e➔y➔o➔n➔d➔ ➔p➔o➔d➔ ➔r➔e➔s➔t➔a➔r➔t➔s➔ ➔(➔a➔s➔ ➔l➔o➔n➔g➔ ➔a➔s➔
➔p➔o➔d➔ ➔s➔t➔a➔y➔s➔ ➔o➔n➔ ➔s➔a➔m➔e➔ ➔n➔o➔d➔e➔)➔.➔ ➔N➔O➔T➔ ➔r➔e➔c➔o➔m➔m➔e➔n➔d➔e➔d➔ ➔f➔o➔r➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔(➔n➔o➔d➔e➔-➔s➔p➔e➔c➔i➔f➔i➔c➔)➔.➔
➔#➔ ➔h➔o➔s➔t➔p➔a➔t➔h➔-➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔.➔y➔a➔m➔l➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔a➔p➔p➔s➔/➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔d➔p➔1➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔r➔e➔p➔l➔i➔c➔a➔s➔:➔ ➔2➔
➔ ➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔:➔
➔ ➔ ➔ ➔ ➔m➔a➔t➔c➔h➔L➔a➔b➔e➔l➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔:➔
➔ ➔ ➔ ➔ ➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔l➔a➔b➔e➔l➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔
➔
➔
➔
➔
➔ ➔ ➔ ➔ ➔s➔p➔e➔c➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔c➔1➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔h➔t➔t➔p➔d➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔P➔o➔r➔t➔:➔ ➔8➔0➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔v➔o➔l➔u➔m➔e➔M➔o➔u➔n➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔v➔1➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔m➔o➔u➔n➔t➔P➔a➔t➔h➔:➔ ➔/➔u➔s➔r➔/➔l➔o➔c➔a➔l➔/➔a➔p➔a➔c➔h➔e➔2➔/➔h➔t➔d➔o➔c➔s➔
➔ ➔ ➔ ➔ ➔ ➔ ➔v➔o➔l➔u➔m➔e➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔v➔1➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔h➔o➔s➔t➔P➔a➔t➔h➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔a➔t➔h➔:➔ ➔/➔h➔o➔m➔e➔/➔c➔e➔n➔t➔o➔s➔/➔h➔o➔s➔t➔p➔a➔t➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔c➔t➔u➔a➔l➔ ➔p➔a➔t➔h➔ ➔o➔n➔ ➔t➔h➔e➔ ➔n➔o➔d➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔t➔y➔p➔e➔:➔ ➔D➔i➔r➔e➔c➔t➔o➔r➔y➔O➔r➔C➔r➔e➔a➔t➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔i➔f➔ ➔d➔o➔e➔s➔n➔'➔t➔ ➔e➔x➔i➔s➔t➔
➔U➔s➔e➔ ➔w➔h➔e➔n➔:➔ ➔D➔a➔e➔m➔o➔n➔S➔e➔t➔s➔ ➔c➔o➔l➔l➔e➔c➔t➔i➔n➔g➔ ➔l➔o➔g➔s➔ ➔f➔r➔o➔m➔ ➔n➔o➔d➔e➔ ➔f➔i➔l➔e➔s➔y➔s➔t➔e➔m➔
➔N➔o➔t➔ ➔f➔o➔r➔:➔ ➔P➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔d➔a➔t➔a➔b➔a➔s➔e➔s➔ ➔(➔n➔o➔d➔e➔-➔s➔p➔e➔c➔i➔f➔i➔c➔,➔ ➔n➔o➔t➔ ➔p➔o➔r➔t➔a➔b➔l➔e➔)➔
➔T➔y➔p➔e➔ ➔3➔:➔ ➔P➔e➔r➔s➔i➔s➔t➔e➔n➔t➔V➔o➔l➔u➔m➔e➔ ➔(➔P➔V➔)➔ ➔+➔ ➔P➔e➔r➔s➔i➔s➔t➔e➔n➔t➔V➔o➔l➔u➔m➔e➔C➔l➔a➔i➔m➔ ➔(➔P➔V➔C➔)➔
➔H➔o➔w➔ ➔i➔t➔ ➔w➔o➔r➔k➔s➔:➔
➔A➔d➔m➔i➔n➔ ➔c➔r➔e➔a➔t➔e➔s➔ ➔P➔V➔ ➔─➔─➔→➔ ➔D➔e➔v➔e➔l➔o➔p➔e➔r➔ ➔c➔r➔e➔a➔t➔e➔s➔ ➔P➔V➔C➔ ➔─➔─➔→➔ ➔P➔o➔d➔ ➔u➔s➔e➔s➔ ➔P➔V➔C➔
➔(➔a➔c➔t➔u➔a➔l➔ ➔s➔t➔o➔r➔a➔g➔e➔)➔ ➔ ➔ ➔ ➔ ➔ ➔(➔r➔e➔q➔u➔e➔s➔t➔ ➔f➔o➔r➔ ➔s➔t➔o➔r➔a➔g➔e➔)➔
➔#➔ ➔p➔v➔.➔y➔a➔m➔l➔ ➔—➔ ➔A➔d➔m➔i➔n➔ ➔c➔r➔e➔a➔t➔e➔s➔ ➔t➔h➔i➔s➔ ➔(➔b➔a➔c➔k➔e➔d➔ ➔b➔y➔ ➔A➔W➔S➔ ➔E➔B➔S➔)➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔P➔e➔r➔s➔i➔s➔t➔e➔n➔t➔V➔o➔l➔u➔m➔e➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔p➔v➔1➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔c➔a➔p➔a➔c➔i➔t➔y➔:➔
➔ ➔ ➔ ➔ ➔s➔t➔o➔r➔a➔g➔e➔:➔ ➔1➔0➔G➔i➔
➔ ➔ ➔a➔c➔c➔e➔s➔s➔M➔o➔d➔e➔s➔:➔
➔ ➔ ➔-➔ ➔R➔e➔a➔d➔W➔r➔i➔t➔e➔O➔n➔c➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔o➔n➔e➔ ➔n➔o➔d➔e➔ ➔a➔t➔ ➔a➔ ➔t➔i➔m➔e➔
➔ ➔ ➔p➔e➔r➔s➔i➔s➔t➔e➔n➔t➔V➔o➔l➔u➔m➔e➔R➔e➔c➔l➔a➔i➔m➔P➔o➔l➔i➔c➔y➔:➔ ➔R➔e➔t➔a➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔k➔e➔e➔p➔ ➔d➔a➔t➔a➔ ➔a➔f➔t➔e➔r➔ ➔P➔V➔C➔ ➔d➔e➔l➔e➔t➔e➔d➔
➔ ➔ ➔a➔w➔s➔E➔l➔a➔s➔t➔i➔c➔B➔l➔o➔c➔k➔S➔t➔o➔r➔e➔:➔
➔ ➔ ➔ ➔ ➔v➔o➔l➔u➔m➔e➔I➔D➔:➔ ➔v➔o➔l➔-➔x➔x➔x➔x➔x➔x➔x➔x➔x➔x➔x➔x➔x➔x➔x➔x➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔y➔o➔u➔r➔ ➔a➔c➔t➔u➔a➔l➔ ➔E➔B➔S➔ ➔v➔o➔l➔u➔m➔e➔ ➔I➔D➔
➔ ➔ ➔ ➔ ➔f➔s➔T➔y➔p➔e➔:➔ ➔e➔x➔t➔4➔
➔#➔ ➔p➔v➔c➔.➔y➔a➔m➔l➔ ➔—➔ ➔D➔e➔v➔e➔l➔o➔p➔e➔r➔ ➔c➔r➔e➔a➔t➔e➔s➔ ➔t➔h➔i➔s➔ ➔(➔r➔e➔q➔u➔e➔s➔t➔s➔ ➔2➔G➔i➔ ➔f➔r➔o➔m➔ ➔a➔v➔a➔i➔l➔a➔b➔l➔e➔ ➔P➔V➔s➔)➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔P➔e➔r➔s➔i➔s➔t➔e➔n➔t➔V➔o➔l➔u➔m➔e➔C➔l➔a➔i➔m➔
➔
➔
➔
➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔p➔v➔c➔1➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔a➔c➔c➔e➔s➔s➔M➔o➔d➔e➔s➔:➔
➔ ➔ ➔-➔ ➔R➔e➔a➔d➔W➔r➔i➔t➔e➔O➔n➔c➔e➔
➔ ➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔s➔:➔
➔ ➔ ➔ ➔ ➔r➔e➔q➔u➔e➔s➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔o➔r➔a➔g➔e➔:➔ ➔2➔G➔i➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔m➔u➔s➔t➔ ➔b➔e➔ ➔≤➔ ➔P➔V➔ ➔c➔a➔p➔a➔c➔i➔t➔y➔
➔#➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔-➔w➔i➔t➔h➔-➔p➔v➔c➔.➔y➔a➔m➔l➔ ➔—➔ ➔P➔o➔d➔ ➔u➔s➔e➔s➔ ➔P➔V➔C➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔a➔p➔p➔s➔/➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔d➔p➔1➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔r➔e➔p➔l➔i➔c➔a➔s➔:➔ ➔2➔
➔ ➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔:➔
➔ ➔ ➔ ➔ ➔m➔a➔t➔c➔h➔L➔a➔b➔e➔l➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔:➔
➔ ➔ ➔ ➔ ➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔l➔a➔b➔e➔l➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔s➔p➔e➔c➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔c➔1➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔h➔t➔t➔p➔d➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔P➔o➔r➔t➔:➔ ➔8➔0➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔v➔o➔l➔u➔m➔e➔M➔o➔u➔n➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔v➔1➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔m➔o➔u➔n➔t➔P➔a➔t➔h➔:➔ ➔/➔u➔s➔r➔/➔l➔o➔c➔a➔l➔/➔a➔p➔a➔c➔h➔e➔2➔/➔h➔t➔d➔o➔c➔s➔
➔ ➔ ➔ ➔ ➔ ➔ ➔v➔o➔l➔u➔m➔e➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔v➔1➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔e➔r➔s➔i➔s➔t➔e➔n➔t➔V➔o➔l➔u➔m➔e➔C➔l➔a➔i➔m➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔c➔l➔a➔i➔m➔N➔a➔m➔e➔:➔ ➔p➔v➔c➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔f➔e➔r➔e➔n➔c➔e➔ ➔P➔V➔C➔ ➔b➔y➔ ➔n➔a➔m➔e➔
➔A➔c➔c➔e➔s➔s➔ ➔M➔o➔d➔e➔s➔
➔M➔o➔d➔e➔ ➔D➔e➔s➔c➔r➔i➔p➔t➔i➔o➔n➔ ➔U➔s➔e➔ ➔c➔a➔s➔e➔
➔R➔e➔a➔d➔W➔r➔i➔t➔e➔O➔n➔c➔e➔ ➔(➔R➔W➔O➔)➔ ➔O➔n➔e➔ ➔n➔o➔d➔e➔ ➔c➔a➔n➔ ➔r➔e➔a➔d➔+➔w➔r➔i➔t➔e➔ ➔D➔a➔t➔a➔b➔a➔s➔e➔s➔
➔R➔e➔a➔d➔O➔n➔l➔y➔M➔a➔n➔y➔ ➔(➔R➔O➔X➔)➔ ➔M➔a➔n➔y➔ ➔n➔o➔d➔e➔s➔ ➔c➔a➔n➔ ➔r➔e➔a➔d➔ ➔S➔h➔a➔r➔e➔d➔ ➔c➔o➔n➔f➔i➔g➔ ➔f➔i➔l➔e➔s➔
➔
➔
➔
➔
➔R➔e➔a➔d➔W➔r➔i➔t➔e➔M➔a➔n➔y➔ ➔(➔R➔W➔X➔)➔ ➔M➔a➔n➔y➔ ➔n➔o➔d➔e➔s➔ ➔c➔a➔n➔ ➔r➔e➔a➔d➔+➔w➔r➔i➔t➔e➔ ➔S➔h➔a➔r➔e➔d➔ ➔f➔i➔l➔e➔ ➔s➔y➔s➔t➔e➔m➔s➔ ➔(➔N➔F➔S➔,➔ ➔E➔F➔S➔)➔
➔R➔e➔c➔l➔a➔i➔m➔ ➔P➔o➔l➔i➔c➔i➔e➔s➔
➔P➔o➔l➔i➔c➔y➔ ➔M➔e➔a➔n➔i➔n➔g➔
➔R➔e➔t➔a➔i➔n➔ ➔K➔e➔e➔p➔ ➔P➔V➔ ➔d➔a➔t➔a➔ ➔a➔f➔t➔e➔r➔ ➔P➔V➔C➔ ➔d➔e➔l➔e➔t➔e➔d➔.➔ ➔M➔a➔n➔u➔a➔l➔ ➔c➔l➔e➔a➔n➔u➔p➔ ➔n➔e➔e➔d➔e➔d➔.➔
➔D➔e➔l➔e➔t➔e➔ ➔D➔e➔l➔e➔t➔e➔ ➔P➔V➔ ➔a➔n➔d➔ ➔u➔n➔d➔e➔r➔l➔y➔i➔n➔g➔ ➔s➔t➔o➔r➔a➔g➔e➔ ➔w➔h➔e➔n➔ ➔P➔V➔C➔ ➔d➔e➔l➔e➔t➔e➔d➔
➔R➔e➔c➔y➔c➔l➔e➔ ➔W➔i➔p➔e➔ ➔P➔V➔ ➔d➔a➔t➔a➔ ➔a➔n➔d➔ ➔m➔a➔k➔e➔ ➔a➔v➔a➔i➔l➔a➔b➔l➔e➔ ➔a➔g➔a➔i➔n➔ ➔(➔d➔e➔p➔r➔e➔c➔a➔t➔e➔d➔)➔
➔P➔V➔/➔P➔V➔C➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔p➔v➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔p➔e➔r➔s➔i➔s➔t➔e➔n➔t➔ ➔v➔o➔l➔u➔m➔e➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔p➔v➔c➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔p➔e➔r➔s➔i➔s➔t➔e➔n➔t➔ ➔v➔o➔l➔u➔m➔e➔ ➔c➔l➔a➔i➔m➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔p➔v➔ ➔p➔v➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔P➔V➔ ➔d➔e➔t➔a➔i➔l➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔p➔v➔c➔ ➔p➔v➔c➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔P➔V➔C➔ ➔d➔e➔t➔a➔i➔l➔s➔ ➔a➔n➔d➔ ➔b➔i➔n➔d➔i➔n➔g➔ ➔s➔t➔a➔t➔u➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔l➔e➔t➔e➔ ➔p➔v➔c➔ ➔p➔v➔c➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔P➔V➔C➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔p➔v➔c➔ ➔-➔o➔ ➔w➔i➔d➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔P➔V➔C➔ ➔w➔i➔t➔h➔ ➔m➔o➔r➔e➔ ➔i➔n➔f➔o➔
➔#➔ ➔C➔h➔e➔c➔k➔ ➔P➔V➔C➔ ➔s➔t➔a➔t➔u➔s➔
➔#➔ ➔P➔E➔N➔D➔I➔N➔G➔ ➔ ➔ ➔=➔ ➔n➔o➔ ➔m➔a➔t➔c➔h➔i➔n➔g➔ ➔P➔V➔ ➔f➔o➔u➔n➔d➔
➔#➔ ➔B➔O➔U➔N➔D➔ ➔ ➔ ➔ ➔ ➔=➔ ➔s➔u➔c➔c➔e➔s➔s➔f➔u➔l➔l➔y➔ ➔b➔o➔u➔n➔d➔ ➔t➔o➔ ➔a➔ ➔P➔V➔
➔#➔ ➔L➔O➔S➔T➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔P➔V➔ ➔w➔a➔s➔ ➔d➔e➔l➔e➔t➔e➔d➔ ➔b➔u➔t➔ ➔P➔V➔C➔ ➔r➔e➔m➔a➔i➔n➔s➔
➔1➔1➔.➔ ➔D➔a➔e➔m➔o➔n➔S➔e➔t➔
➔D➔e➔f➔i➔n➔i➔t➔i➔o➔n➔:➔ ➔E➔n➔s➔u➔r➔e➔s➔ ➔e➔x➔a➔c➔t➔l➔y➔ ➔O➔N➔E➔ ➔p➔o➔d➔ ➔r➔u➔n➔s➔ ➔o➔n➔ ➔E➔V➔E➔R➔Y➔ ➔n➔o➔d➔e➔ ➔i➔n➔ ➔t➔h➔e➔ ➔c➔l➔u➔s➔t➔e➔r➔.➔ ➔W➔h➔e➔n➔ ➔a➔ ➔n➔e➔w➔ ➔n➔o➔d➔e➔ ➔j➔o➔i➔n➔s➔,➔ ➔D➔a➔e➔m➔o➔n➔S➔e➔t➔
➔a➔u➔t➔o➔m➔a➔t➔i➔c➔a➔l➔l➔y➔ ➔c➔r➔e➔a➔t➔e➔s➔ ➔a➔ ➔p➔o➔d➔ ➔t➔h➔e➔r➔e➔.➔
➔#➔ ➔d➔a➔e➔m➔o➔n➔s➔e➔t➔.➔y➔a➔m➔l➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔a➔p➔p➔s➔/➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔D➔a➔e➔m➔o➔n➔S➔e➔t➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔d➔s➔1➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔:➔
➔ ➔ ➔ ➔ ➔m➔a➔t➔c➔h➔L➔a➔b➔e➔l➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔:➔
➔
➔
➔
➔
➔ ➔ ➔ ➔ ➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔l➔a➔b➔e➔l➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔s➔p➔e➔c➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔c➔1➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔h➔t➔t➔p➔d➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔P➔o➔r➔t➔:➔ ➔8➔0➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔d➔a➔e➔m➔o➔n➔s➔e➔t➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔d➔a➔e➔m➔o➔n➔s➔e➔t➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔d➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔r➔t➔ ➔f➔o➔r➔m➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔d➔s➔ ➔d➔s➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔t➔a➔i➔l➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔l➔e➔t➔e➔ ➔d➔s➔ ➔d➔s➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔
➔U➔s➔e➔ ➔f➔o➔r➔:➔
➔-➔ ➔L➔o➔g➔ ➔c➔o➔l➔l➔e➔c➔t➔o➔r➔s➔ ➔(➔F➔l➔u➔e➔n➔t➔d➔,➔ ➔F➔i➔l➔e➔b➔e➔a➔t➔)➔ ➔—➔ ➔c➔o➔l➔l➔e➔c➔t➔ ➔l➔o➔g➔s➔ ➔f➔r➔o➔m➔ ➔e➔v➔e➔r➔y➔ ➔n➔o➔d➔e➔
➔-➔ ➔M➔o➔n➔i➔t➔o➔r➔i➔n➔g➔ ➔a➔g➔e➔n➔t➔s➔ ➔(➔P➔r➔o➔m➔e➔t➔h➔e➔u➔s➔ ➔n➔o➔d➔e➔-➔e➔x➔p➔o➔r➔t➔e➔r➔)➔ ➔—➔ ➔m➔e➔t➔r➔i➔c➔s➔ ➔f➔r➔o➔m➔ ➔e➔v➔e➔r➔y➔ ➔n➔o➔d➔e➔
➔-➔ ➔N➔e➔t➔w➔o➔r➔k➔ ➔p➔l➔u➔g➔i➔n➔s➔ ➔(➔C➔N➔I➔ ➔—➔ ➔C➔a➔l➔i➔c➔o➔,➔ ➔F➔l➔a➔n➔n➔e➔l➔)➔ ➔—➔ ➔n➔e➔t➔w➔o➔r➔k➔i➔n➔g➔ ➔o➔n➔ ➔e➔v➔e➔r➔y➔ ➔n➔o➔d➔e➔
➔-➔ ➔S➔e➔c➔u➔r➔i➔t➔y➔ ➔a➔g➔e➔n➔t➔s➔ ➔—➔ ➔r➔u➔n➔ ➔o➔n➔ ➔e➔v➔e➔r➔y➔ ➔n➔o➔d➔e➔
➔1➔2➔.➔ ➔C➔o➔n➔f➔i➔g➔M➔a➔p➔ ➔—➔ ➔C➔o➔m➔p➔l➔e➔t➔e➔ ➔G➔u➔i➔d➔e➔
➔D➔e➔f➔i➔n➔i➔t➔i➔o➔n➔:➔ ➔S➔t➔o➔r➔e➔s➔ ➔n➔o➔n➔-➔s➔e➔n➔s➔i➔t➔i➔v➔e➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔ ➔a➔s➔ ➔k➔e➔y➔-➔v➔a➔l➔u➔e➔ ➔p➔a➔i➔r➔s➔.➔ ➔I➔n➔j➔e➔c➔t➔e➔d➔ ➔i➔n➔t➔o➔ ➔p➔o➔d➔s➔ ➔a➔s➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔
➔o➔r➔ ➔m➔o➔u➔n➔t➔e➔d➔ ➔a➔s➔ ➔f➔i➔l➔e➔s➔.➔
➔I➔m➔p➔e➔r➔a➔t➔i➔v➔e➔ ➔W➔a➔y➔ ➔(➔C➔o➔m➔m➔a➔n➔d➔ ➔l➔i➔n➔e➔)➔
➔#➔ ➔C➔r➔e➔a➔t➔e➔ ➔f➔r➔o➔m➔ ➔l➔i➔t➔e➔r➔a➔l➔ ➔v➔a➔l➔u➔e➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔c➔r➔e➔a➔t➔e➔ ➔c➔o➔n➔f➔i➔g➔m➔a➔p➔ ➔c➔m➔1➔ ➔\➔
➔ ➔ ➔-➔-➔f➔r➔o➔m➔-➔l➔i➔t➔e➔r➔a➔l➔=➔a➔p➔p➔=➔m➔y➔a➔p➔p➔ ➔\➔
➔ ➔ ➔-➔-➔f➔r➔o➔m➔-➔l➔i➔t➔e➔r➔a➔l➔=➔e➔n➔v➔=➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔\➔
➔ ➔ ➔-➔-➔f➔r➔o➔m➔-➔l➔i➔t➔e➔r➔a➔l➔=➔p➔o➔r➔t➔=➔8➔0➔8➔0➔
➔#➔ ➔C➔r➔e➔a➔t➔e➔ ➔f➔r➔o➔m➔ ➔a➔ ➔f➔i➔l➔e➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔c➔r➔e➔a➔t➔e➔ ➔c➔o➔n➔f➔i➔g➔m➔a➔p➔ ➔c➔m➔1➔ ➔-➔-➔f➔r➔o➔m➔-➔f➔i➔l➔e➔=➔c➔o➔n➔f➔i➔g➔.➔p➔r➔o➔p➔e➔r➔t➔i➔e➔s➔
➔#➔ ➔C➔r➔e➔a➔t➔e➔ ➔f➔r➔o➔m➔ ➔e➔n➔v➔ ➔f➔i➔l➔e➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔c➔r➔e➔a➔t➔e➔ ➔c➔o➔n➔f➔i➔g➔m➔a➔p➔ ➔c➔m➔1➔ ➔-➔-➔f➔r➔o➔m➔-➔e➔n➔v➔-➔f➔i➔l➔e➔=➔.➔e➔n➔v➔
➔
➔
➔
➔
➔#➔ ➔V➔i➔e➔w➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔c➔o➔n➔f➔i➔g➔m➔a➔p➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔c➔m➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔c➔m➔ ➔c➔m➔1➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔c➔m➔ ➔c➔m➔1➔ ➔-➔o➔ ➔y➔a➔m➔l➔
➔D➔e➔c➔l➔a➔r➔a➔t➔i➔v➔e➔ ➔W➔a➔y➔ ➔(➔Y➔A➔M➔L➔)➔
➔#➔ ➔c➔o➔n➔f➔i➔g➔m➔a➔p➔.➔y➔a➔m➔l➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔C➔o➔n➔f➔i➔g➔M➔a➔p➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔c➔m➔1➔
➔d➔a➔t➔a➔:➔
➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔:➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔ ➔ ➔p➔o➔r➔t➔:➔ ➔"➔8➔0➔8➔0➔"➔
➔ ➔ ➔c➔o➔n➔f➔i➔g➔.➔p➔r➔o➔p➔e➔r➔t➔i➔e➔s➔:➔ ➔|➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔m➔u➔l➔t➔i➔-➔l➔i➔n➔e➔ ➔f➔i➔l➔e➔ ➔c➔o➔n➔t➔e➔n➔t➔
➔ ➔ ➔ ➔ ➔d➔b➔.➔h➔o➔s➔t➔=➔l➔o➔c➔a➔l➔h➔o➔s➔t➔
➔ ➔ ➔ ➔ ➔d➔b➔.➔p➔o➔r➔t➔=➔5➔4➔3➔2➔
➔ ➔ ➔ ➔ ➔d➔b➔.➔n➔a➔m➔e➔=➔m➔y➔d➔b➔
➔U➔s➔i➔n➔g➔ ➔C➔o➔n➔f➔i➔g➔M➔a➔p➔ ➔i➔n➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔
➔M➔e➔t➔h➔o➔d➔ ➔1➔:➔ ➔A➔s➔ ➔E➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔s➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔
➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔c➔1➔
➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔h➔t➔t➔p➔d➔
➔ ➔ ➔ ➔ ➔e➔n➔v➔F➔r➔o➔m➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔c➔o➔n➔f➔i➔g➔M➔a➔p➔R➔e➔f➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔c➔m➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔i➔n➔j➔e➔c➔t➔ ➔A➔L➔L➔ ➔k➔e➔y➔s➔ ➔a➔s➔ ➔e➔n➔v➔ ➔v➔a➔r➔s➔
➔M➔e➔t➔h➔o➔d➔ ➔2➔:➔ ➔S➔p➔e➔c➔i➔f➔i➔c➔ ➔K➔e➔y➔ ➔a➔s➔ ➔E➔n➔v➔ ➔V➔a➔r➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔
➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔c➔1➔
➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔h➔t➔t➔p➔d➔
➔ ➔ ➔ ➔ ➔e➔n➔v➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔A➔P➔P➔_➔N➔A➔M➔E➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔n➔v➔ ➔v➔a➔r➔ ➔n➔a➔m➔e➔ ➔i➔n➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔ ➔ ➔ ➔ ➔ ➔ ➔v➔a➔l➔u➔e➔F➔r➔o➔m➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔n➔f➔i➔g➔M➔a➔p➔K➔e➔y➔R➔e➔f➔:➔
➔
➔
➔
➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔c➔m➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔n➔f➔i➔g➔m➔a➔p➔ ➔n➔a➔m➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔k➔e➔y➔:➔ ➔a➔p➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔k➔e➔y➔ ➔i➔n➔ ➔c➔o➔n➔f➔i➔g➔m➔a➔p➔
➔M➔e➔t➔h➔o➔d➔ ➔3➔:➔ ➔M➔o➔u➔n➔t➔ ➔a➔s➔ ➔F➔i➔l➔e➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔
➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔c➔1➔
➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔h➔t➔t➔p➔d➔
➔ ➔ ➔ ➔ ➔v➔o➔l➔u➔m➔e➔M➔o➔u➔n➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔c➔m➔-➔v➔o➔l➔u➔m➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔m➔o➔u➔n➔t➔P➔a➔t➔h➔:➔ ➔/➔e➔t➔c➔/➔c➔o➔n➔f➔i➔g➔ ➔ ➔#➔ ➔C➔o➔n➔f➔i➔g➔M➔a➔p➔ ➔k➔e➔y➔s➔ ➔b➔e➔c➔o➔m➔e➔ ➔f➔i➔l➔e➔s➔ ➔h➔e➔r➔e➔
➔ ➔ ➔v➔o➔l➔u➔m➔e➔s➔:➔
➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔c➔m➔-➔v➔o➔l➔u➔m➔e➔
➔ ➔ ➔ ➔ ➔c➔o➔n➔f➔i➔g➔M➔a➔p➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔c➔m➔1➔
➔1➔3➔.➔ ➔S➔e➔c➔r➔e➔t➔s➔ ➔—➔ ➔C➔o➔m➔p➔l➔e➔t➔e➔ ➔G➔u➔i➔d➔e➔
➔D➔e➔f➔i➔n➔i➔t➔i➔o➔n➔:➔ ➔L➔i➔k➔e➔ ➔C➔o➔n➔f➔i➔g➔M➔a➔p➔ ➔b➔u➔t➔ ➔f➔o➔r➔ ➔s➔e➔n➔s➔i➔t➔i➔v➔e➔ ➔d➔a➔t➔a➔ ➔(➔p➔a➔s➔s➔w➔o➔r➔d➔s➔,➔ ➔A➔P➔I➔ ➔k➔e➔y➔s➔,➔ ➔t➔o➔k➔e➔n➔s➔)➔.➔ ➔V➔a➔l➔u➔e➔s➔ ➔a➔r➔e➔ ➔b➔a➔s➔e➔6➔4➔ ➔e➔n➔c➔o➔d➔e➔d➔.➔
➔C➔a➔n➔ ➔b➔e➔ ➔e➔n➔c➔r➔y➔p➔t➔e➔d➔ ➔a➔t➔ ➔r➔e➔s➔t➔.➔
➔I➔m➔p➔e➔r➔a➔t➔i➔v➔e➔ ➔W➔a➔y➔
➔#➔ ➔C➔r➔e➔a➔t➔e➔ ➔f➔r➔o➔m➔ ➔l➔i➔t➔e➔r➔a➔l➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔c➔r➔e➔a➔t➔e➔ ➔s➔e➔c➔r➔e➔t➔ ➔g➔e➔n➔e➔r➔i➔c➔ ➔s➔1➔ ➔\➔
➔ ➔ ➔-➔-➔f➔r➔o➔m➔-➔l➔i➔t➔e➔r➔a➔l➔=➔u➔s➔e➔r➔n➔a➔m➔e➔=➔a➔d➔m➔i➔n➔ ➔\➔
➔ ➔ ➔-➔-➔f➔r➔o➔m➔-➔l➔i➔t➔e➔r➔a➔l➔=➔p➔a➔s➔s➔w➔o➔r➔d➔=➔M➔y➔S➔e➔c➔r➔e➔t➔P➔a➔s➔s➔1➔2➔3➔
➔#➔ ➔C➔r➔e➔a➔t➔e➔ ➔f➔r➔o➔m➔ ➔f➔i➔l➔e➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔c➔r➔e➔a➔t➔e➔ ➔s➔e➔c➔r➔e➔t➔ ➔g➔e➔n➔e➔r➔i➔c➔ ➔s➔1➔ ➔-➔-➔f➔r➔o➔m➔-➔f➔i➔l➔e➔=➔c➔r➔e➔d➔e➔n➔t➔i➔a➔l➔s➔.➔t➔x➔t➔
➔#➔ ➔C➔r➔e➔a➔t➔e➔ ➔T➔L➔S➔ ➔s➔e➔c➔r➔e➔t➔ ➔(➔f➔o➔r➔ ➔H➔T➔T➔P➔S➔)➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔c➔r➔e➔a➔t➔e➔ ➔s➔e➔c➔r➔e➔t➔ ➔t➔l➔s➔ ➔t➔l➔s➔-➔s➔e➔c➔r➔e➔t➔ ➔\➔
➔ ➔ ➔-➔-➔c➔e➔r➔t➔=➔s➔e➔r➔v➔e➔r➔.➔c➔r➔t➔ ➔\➔
➔ ➔ ➔-➔-➔k➔e➔y➔=➔s➔e➔r➔v➔e➔r➔.➔k➔e➔y➔
➔#➔ ➔C➔r➔e➔a➔t➔e➔ ➔D➔o➔c➔k➔e➔r➔ ➔r➔e➔g➔i➔s➔t➔r➔y➔ ➔s➔e➔c➔r➔e➔t➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔c➔r➔e➔a➔t➔e➔ ➔s➔e➔c➔r➔e➔t➔ ➔d➔o➔c➔k➔e➔r➔-➔r➔e➔g➔i➔s➔t➔r➔y➔ ➔r➔e➔g➔c➔r➔e➔d➔ ➔\➔
➔ ➔ ➔-➔-➔d➔o➔c➔k➔e➔r➔-➔s➔e➔r➔v➔e➔r➔=➔d➔o➔c➔k➔e➔r➔.➔i➔o➔ ➔\➔
➔ ➔ ➔-➔-➔d➔o➔c➔k➔e➔r➔-➔u➔s➔e➔r➔n➔a➔m➔e➔=➔a➔k➔h➔i➔l➔ ➔\➔
➔ ➔ ➔-➔-➔d➔o➔c➔k➔e➔r➔-➔p➔a➔s➔s➔w➔o➔r➔d➔=➔m➔y➔p➔a➔s➔s➔w➔o➔r➔d➔
➔
➔
➔
➔
➔#➔ ➔V➔i➔e➔w➔ ➔s➔e➔c➔r➔e➔t➔s➔ ➔(➔v➔a➔l➔u➔e➔s➔ ➔a➔r➔e➔ ➔b➔a➔s➔e➔6➔4➔ ➔e➔n➔c➔o➔d➔e➔d➔)➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔s➔e➔c➔r➔e➔t➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔s➔e➔c➔r➔e➔t➔ ➔s➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔s➔ ➔k➔e➔y➔s➔ ➔b➔u➔t➔ ➔N➔O➔T➔ ➔v➔a➔l➔u➔e➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔s➔e➔c➔r➔e➔t➔ ➔s➔1➔ ➔-➔o➔ ➔y➔a➔m➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔s➔ ➔b➔a➔s➔e➔6➔4➔ ➔e➔n➔c➔o➔d➔e➔d➔ ➔v➔a➔l➔u➔e➔s➔
➔#➔ ➔D➔e➔c➔o➔d➔e➔ ➔a➔ ➔s➔e➔c➔r➔e➔t➔ ➔v➔a➔l➔u➔e➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔s➔e➔c➔r➔e➔t➔ ➔s➔1➔ ➔-➔o➔ ➔j➔s➔o➔n➔p➔a➔t➔h➔=➔'➔{➔.➔d➔a➔t➔a➔.➔p➔a➔s➔s➔w➔o➔r➔d➔}➔'➔ ➔|➔ ➔b➔a➔s➔e➔6➔4➔ ➔-➔-➔d➔e➔c➔o➔d➔e➔
➔D➔e➔c➔l➔a➔r➔a➔t➔i➔v➔e➔ ➔W➔a➔y➔
➔#➔ ➔s➔e➔c➔r➔e➔t➔.➔y➔a➔m➔l➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔S➔e➔c➔r➔e➔t➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔s➔1➔
➔t➔y➔p➔e➔:➔ ➔O➔p➔a➔q➔u➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔g➔e➔n➔e➔r➔i➔c➔ ➔s➔e➔c➔r➔e➔t➔ ➔t➔y➔p➔e➔
➔d➔a➔t➔a➔:➔
➔ ➔ ➔u➔s➔e➔r➔n➔a➔m➔e➔:➔ ➔Y➔W➔R➔t➔a➔W➔4➔=➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔b➔a➔s➔e➔6➔4➔ ➔e➔n➔c➔o➔d➔e➔d➔ ➔v➔a➔l➔u➔e➔ ➔o➔f➔ ➔"➔a➔d➔m➔i➔n➔"➔
➔ ➔ ➔p➔a➔s➔s➔w➔o➔r➔d➔:➔ ➔T➔X➔l➔T➔Z➔W➔N➔y➔Z➔X➔R➔Q➔Y➔X➔N➔z➔M➔T➔I➔z➔ ➔ ➔#➔ ➔b➔a➔s➔e➔6➔4➔ ➔o➔f➔ ➔"➔M➔y➔S➔e➔c➔r➔e➔t➔P➔a➔s➔s➔1➔2➔3➔"➔
➔#➔ ➔E➔n➔c➔o➔d➔e➔ ➔v➔a➔l➔u➔e➔s➔:➔ ➔e➔c➔h➔o➔ ➔-➔n➔ ➔"➔a➔d➔m➔i➔n➔"➔ ➔|➔ ➔b➔a➔s➔e➔6➔4➔
➔#➔ ➔D➔e➔c➔o➔d➔e➔ ➔v➔a➔l➔u➔e➔s➔:➔ ➔e➔c➔h➔o➔ ➔"➔Y➔W➔R➔t➔a➔W➔4➔=➔"➔ ➔|➔ ➔b➔a➔s➔e➔6➔4➔ ➔-➔-➔d➔e➔c➔o➔d➔e➔
➔U➔s➔i➔n➔g➔ ➔S➔e➔c➔r➔e➔t➔s➔ ➔i➔n➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔
➔M➔e➔t➔h➔o➔d➔ ➔1➔:➔ ➔A➔l➔l➔ ➔k➔e➔y➔s➔ ➔a➔s➔ ➔e➔n➔v➔ ➔v➔a➔r➔s➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔
➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔c➔1➔
➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔h➔t➔t➔p➔d➔
➔ ➔ ➔ ➔ ➔e➔n➔v➔F➔r➔o➔m➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔s➔e➔c➔r➔e➔t➔R➔e➔f➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔s➔1➔
➔M➔e➔t➔h➔o➔d➔ ➔2➔:➔ ➔S➔p➔e➔c➔i➔f➔i➔c➔ ➔k➔e➔y➔ ➔a➔s➔ ➔e➔n➔v➔ ➔v➔a➔r➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔
➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔c➔1➔
➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔h➔t➔t➔p➔d➔
➔ ➔ ➔ ➔ ➔e➔n➔v➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔D➔B➔_➔P➔A➔S➔S➔W➔O➔R➔D➔
➔
➔
➔
➔
➔ ➔ ➔ ➔ ➔ ➔ ➔v➔a➔l➔u➔e➔F➔r➔o➔m➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔e➔c➔r➔e➔t➔K➔e➔y➔R➔e➔f➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔s➔1➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔k➔e➔y➔:➔ ➔p➔a➔s➔s➔w➔o➔r➔d➔
➔M➔e➔t➔h➔o➔d➔ ➔3➔:➔ ➔M➔o➔u➔n➔t➔ ➔a➔s➔ ➔f➔i➔l➔e➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔
➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔c➔1➔
➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔h➔t➔t➔p➔d➔
➔ ➔ ➔ ➔ ➔v➔o➔l➔u➔m➔e➔M➔o➔u➔n➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔s➔e➔c➔r➔e➔t➔-➔v➔o➔l➔u➔m➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔m➔o➔u➔n➔t➔P➔a➔t➔h➔:➔ ➔/➔e➔t➔c➔/➔s➔e➔c➔r➔e➔t➔s➔
➔ ➔ ➔ ➔ ➔ ➔ ➔r➔e➔a➔d➔O➔n➔l➔y➔:➔ ➔t➔r➔u➔e➔
➔ ➔ ➔v➔o➔l➔u➔m➔e➔s➔:➔
➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔s➔e➔c➔r➔e➔t➔-➔v➔o➔l➔u➔m➔e➔
➔ ➔ ➔ ➔ ➔s➔e➔c➔r➔e➔t➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔s➔e➔c➔r➔e➔t➔N➔a➔m➔e➔:➔ ➔s➔1➔
➔1➔4➔.➔ ➔R➔B➔A➔C➔ ➔—➔ ➔R➔o➔l➔e➔ ➔B➔a➔s➔e➔d➔ ➔A➔c➔c➔e➔s➔s➔ ➔C➔o➔n➔t➔r➔o➔l➔ ➔(➔C➔o➔m➔p➔l➔e➔t➔e➔)➔
➔D➔e➔f➔i➔n➔i➔t➔i➔o➔n➔:➔ ➔R➔B➔A➔C➔ ➔c➔o➔n➔t➔r➔o➔l➔s➔ ➔W➔H➔O➔ ➔c➔a➔n➔ ➔d➔o➔ ➔W➔H➔A➔T➔ ➔i➔n➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔.➔ ➔I➔t➔'➔s➔ ➔h➔o➔w➔ ➔y➔o➔u➔ ➔m➔a➔n➔a➔g➔e➔ ➔a➔c➔c➔e➔s➔s➔ ➔a➔n➔d➔ ➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔.➔
➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔R➔B➔A➔C➔ ➔D➔I➔A➔G➔R➔A➔M➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔W➔H➔O➔?➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔W➔H➔A➔T➔?➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔W➔H➔E➔R➔E➔?➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔ ➔ ➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔ ➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔U➔s➔e➔r➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔R➔o➔l➔e➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔ ➔│➔ ➔ ➔N➔a➔m➔e➔s➔p➔a➔c➔e➔ ➔ ➔ ➔│➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔G➔r➔o➔u➔p➔ ➔ ➔ ➔│➔─➔─➔─➔─➔ ➔▶➔ ➔│➔ ➔(➔r➔u➔l➔e➔s➔)➔ ➔ ➔│➔─➔─➔─➔─➔ ➔▶➔ ➔ ➔ ➔(➔l➔i➔m➔i➔t➔e➔d➔)➔ ➔ ➔ ➔│➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔S➔e➔r➔v➔i➔c➔e➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔ ➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔A➔c➔c➔o➔u➔n➔t➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔└➔─➔─➔─➔─➔┬➔─➔─➔─➔─➔─➔┘➔ ➔ ➔ ➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔ ➔│➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔C➔l➔u➔s➔t➔e➔r➔R➔o➔l➔e➔ ➔│➔ ➔ ➔│➔ ➔ ➔ ➔C➔l➔u➔s➔t➔e➔r➔ ➔ ➔ ➔│➔ ➔ ➔│➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔ ➔▶➔ ➔│➔ ➔ ➔(➔r➔u➔l➔e➔s➔)➔ ➔ ➔ ➔ ➔│➔─➔─➔ ➔▶➔ ➔ ➔ ➔(➔w➔i➔d➔e➔)➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔│➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔ ➔│➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔R➔o➔l➔e➔B➔i➔n➔d➔i➔n➔g➔ ➔c➔o➔n➔n➔e➔c➔t➔s➔ ➔U➔s➔e➔r➔ ➔←➔→➔ ➔R➔o➔l➔e➔ ➔(➔n➔a➔m➔e➔s➔p➔a➔c➔e➔)➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔C➔l➔u➔s➔t➔e➔r➔R➔o➔l➔e➔B➔i➔n➔d➔i➔n➔g➔ ➔c➔o➔n➔n➔e➔c➔t➔s➔ ➔U➔s➔e➔r➔ ➔←➔→➔ ➔C➔l➔u➔s➔t➔e➔r➔R➔o➔l➔e➔ ➔ ➔ ➔ ➔│➔
➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔
➔
➔
➔
➔
➔R➔B➔A➔C➔ ➔M➔e➔m➔o➔r➔y➔ ➔F➔o➔r➔m➔u➔l➔a➔
➔S➔e➔r➔v➔i➔c➔e➔A➔c➔c➔o➔u➔n➔t➔ ➔ ➔=➔ ➔W➔H➔O➔ ➔(➔i➔d➔e➔n➔t➔i➔t➔y➔)➔
➔R➔o➔l➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔W➔H➔A➔T➔ ➔(➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔,➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔ ➔l➔e➔v➔e➔l➔)➔
➔R➔o➔l➔e➔B➔i➔n➔d➔i➔n➔g➔ ➔ ➔ ➔ ➔ ➔=➔ ➔C➔O➔N➔N➔E➔C➔T➔S➔ ➔W➔H➔O➔ ➔t➔o➔ ➔W➔H➔A➔T➔ ➔(➔n➔a➔m➔e➔s➔p➔a➔c➔e➔)➔
➔C➔l➔u➔s➔t➔e➔r➔R➔o➔l➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔W➔H➔A➔T➔ ➔(➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔,➔ ➔c➔l➔u➔s➔t➔e➔r➔-➔w➔i➔d➔e➔)➔
➔C➔l➔u➔s➔t➔e➔r➔R➔o➔l➔e➔B➔i➔n➔d➔i➔n➔g➔ ➔ ➔=➔ ➔C➔O➔N➔N➔E➔C➔T➔S➔ ➔W➔H➔O➔ ➔t➔o➔ ➔W➔H➔A➔T➔ ➔(➔c➔l➔u➔s➔t➔e➔r➔-➔w➔i➔d➔e➔)➔
➔S➔t➔e➔p➔ ➔1➔:➔ ➔S➔e➔r➔v➔i➔c➔e➔A➔c➔c➔o➔u➔n➔t➔ ➔(➔W➔H➔O➔)➔
➔#➔ ➔s➔e➔r➔v➔i➔c➔e➔a➔c➔c➔o➔u➔n➔t➔.➔y➔a➔m➔l➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔S➔e➔r➔v➔i➔c➔e➔A➔c➔c➔o➔u➔n➔t➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔d➔e➔v➔-➔u➔s➔e➔r➔
➔ ➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔:➔ ➔d➔e➔f➔a➔u➔l➔t➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔a➔p➔p➔l➔y➔ ➔-➔f➔ ➔s➔e➔r➔v➔i➔c➔e➔a➔c➔c➔o➔u➔n➔t➔.➔y➔a➔m➔l➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔s➔e➔r➔v➔i➔c➔e➔a➔c➔c➔o➔u➔n➔t➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔s➔a➔
➔S➔t➔e➔p➔ ➔2➔:➔ ➔R➔o➔l➔e➔ ➔(➔W➔H➔A➔T➔ ➔—➔ ➔N➔a➔m➔e➔s➔p➔a➔c➔e➔ ➔L➔e➔v➔e➔l➔)➔
➔#➔ ➔r➔o➔l➔e➔.➔y➔a➔m➔l➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔r➔b➔a➔c➔.➔a➔u➔t➔h➔o➔r➔i➔z➔a➔t➔i➔o➔n➔.➔k➔8➔s➔.➔i➔o➔/➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔R➔o➔l➔e➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔p➔o➔d➔-➔r➔e➔a➔d➔e➔r➔
➔ ➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔:➔ ➔d➔e➔f➔a➔u➔l➔t➔
➔r➔u➔l➔e➔s➔:➔
➔-➔ ➔a➔p➔i➔G➔r➔o➔u➔p➔s➔:➔ ➔[➔"➔"➔]➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔"➔"➔ ➔=➔ ➔c➔o➔r➔e➔ ➔A➔P➔I➔ ➔g➔r➔o➔u➔p➔
➔ ➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔s➔:➔ ➔[➔"➔p➔o➔d➔s➔"➔]➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔w➔h➔a➔t➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔
➔ ➔ ➔v➔e➔r➔b➔s➔:➔ ➔[➔"➔g➔e➔t➔"➔,➔ ➔"➔l➔i➔s➔t➔"➔,➔ ➔"➔w➔a➔t➔c➔h➔"➔]➔ ➔ ➔#➔ ➔w➔h➔a➔t➔ ➔a➔c➔t➔i➔o➔n➔s➔ ➔a➔l➔l➔o➔w➔e➔d➔
➔C➔o➔m➔m➔o➔n➔ ➔v➔e➔r➔b➔s➔:➔ ➔g➔e➔t➔ ➔,➔ ➔l➔i➔s➔t➔ ➔,➔ ➔w➔a➔t➔c➔h➔ ➔,➔ ➔c➔r➔e➔a➔t➔e➔ ➔,➔ ➔u➔p➔d➔a➔t➔e➔ ➔,➔ ➔p➔a➔t➔c➔h➔ ➔,➔ ➔d➔e➔l➔e➔t➔e➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔a➔p➔p➔l➔y➔ ➔-➔f➔ ➔r➔o➔l➔e➔.➔y➔a➔m➔l➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔r➔o➔l➔e➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔r➔o➔l➔e➔ ➔p➔o➔d➔-➔r➔e➔a➔d➔e➔r➔
➔
➔
➔
➔
➔S➔t➔e➔p➔ ➔3➔:➔ ➔R➔o➔l➔e➔B➔i➔n➔d➔i➔n➔g➔ ➔(➔C➔O➔N➔N➔E➔C➔T➔)➔
➔#➔ ➔r➔o➔l➔e➔b➔i➔n➔d➔i➔n➔g➔.➔y➔a➔m➔l➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔r➔b➔a➔c➔.➔a➔u➔t➔h➔o➔r➔i➔z➔a➔t➔i➔o➔n➔.➔k➔8➔s➔.➔i➔o➔/➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔R➔o➔l➔e➔B➔i➔n➔d➔i➔n➔g➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔r➔e➔a➔d➔-➔p➔o➔d➔s➔-➔b➔i➔n➔d➔i➔n➔g➔
➔ ➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔:➔ ➔d➔e➔f➔a➔u➔l➔t➔
➔s➔u➔b➔j➔e➔c➔t➔s➔:➔
➔-➔ ➔k➔i➔n➔d➔:➔ ➔S➔e➔r➔v➔i➔c➔e➔A➔c➔c➔o➔u➔n➔t➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔d➔e➔v➔-➔u➔s➔e➔r➔
➔ ➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔:➔ ➔d➔e➔f➔a➔u➔l➔t➔
➔r➔o➔l➔e➔R➔e➔f➔:➔
➔ ➔ ➔k➔i➔n➔d➔:➔ ➔R➔o➔l➔e➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔p➔o➔d➔-➔r➔e➔a➔d➔e➔r➔
➔ ➔ ➔a➔p➔i➔G➔r➔o➔u➔p➔:➔ ➔r➔b➔a➔c➔.➔a➔u➔t➔h➔o➔r➔i➔z➔a➔t➔i➔o➔n➔.➔k➔8➔s➔.➔i➔o➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔a➔p➔p➔l➔y➔ ➔-➔f➔ ➔r➔o➔l➔e➔b➔i➔n➔d➔i➔n➔g➔.➔y➔a➔m➔l➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔r➔o➔l➔e➔b➔i➔n➔d➔i➔n➔g➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔r➔o➔l➔e➔b➔i➔n➔d➔i➔n➔g➔ ➔r➔e➔a➔d➔-➔p➔o➔d➔s➔-➔b➔i➔n➔d➔i➔n➔g➔
➔#➔ ➔T➔e➔s➔t➔ ➔i➔f➔ ➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔ ➔w➔o➔r➔k➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔a➔u➔t➔h➔ ➔c➔a➔n➔-➔i➔ ➔l➔i➔s➔t➔ ➔p➔o➔d➔s➔ ➔\➔
➔ ➔ ➔-➔-➔a➔s➔=➔s➔y➔s➔t➔e➔m➔:➔s➔e➔r➔v➔i➔c➔e➔a➔c➔c➔o➔u➔n➔t➔:➔d➔e➔f➔a➔u➔l➔t➔:➔d➔e➔v➔-➔u➔s➔e➔r➔ ➔\➔
➔ ➔ ➔-➔n➔ ➔d➔e➔f➔a➔u➔l➔t➔
➔S➔t➔e➔p➔ ➔4➔:➔ ➔C➔l➔u➔s➔t➔e➔r➔R➔o➔l➔e➔ ➔(➔W➔H➔A➔T➔ ➔—➔ ➔C➔l➔u➔s➔t➔e➔r➔ ➔W➔i➔d➔e➔)➔
➔#➔ ➔c➔l➔u➔s➔t➔e➔r➔r➔o➔l➔e➔.➔y➔a➔m➔l➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔r➔b➔a➔c➔.➔a➔u➔t➔h➔o➔r➔i➔z➔a➔t➔i➔o➔n➔.➔k➔8➔s➔.➔i➔o➔/➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔C➔l➔u➔s➔t➔e➔r➔R➔o➔l➔e➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔n➔o➔d➔e➔-➔r➔e➔a➔d➔e➔r➔
➔r➔u➔l➔e➔s➔:➔
➔-➔ ➔a➔p➔i➔G➔r➔o➔u➔p➔s➔:➔ ➔[➔"➔"➔]➔
➔ ➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔s➔:➔ ➔[➔"➔n➔o➔d➔e➔s➔"➔,➔ ➔"➔n➔a➔m➔e➔s➔p➔a➔c➔e➔s➔"➔,➔ ➔"➔p➔e➔r➔s➔i➔s➔t➔e➔n➔t➔v➔o➔l➔u➔m➔e➔s➔"➔]➔
➔ ➔ ➔v➔e➔r➔b➔s➔:➔ ➔[➔"➔g➔e➔t➔"➔,➔ ➔"➔l➔i➔s➔t➔"➔,➔ ➔"➔w➔a➔t➔c➔h➔"➔]➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔a➔p➔p➔l➔y➔ ➔-➔f➔ ➔c➔l➔u➔s➔t➔e➔r➔r➔o➔l➔e➔.➔y➔a➔m➔l➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔c➔l➔u➔s➔t➔e➔r➔r➔o➔l➔e➔s➔
➔
➔
➔
➔
➔S➔t➔e➔p➔ ➔5➔:➔ ➔C➔l➔u➔s➔t➔e➔r➔R➔o➔l➔e➔B➔i➔n➔d➔i➔n➔g➔ ➔(➔C➔O➔N➔N➔E➔C➔T➔ ➔—➔ ➔C➔l➔u➔s➔t➔e➔r➔ ➔W➔i➔d➔e➔)➔
➔#➔ ➔c➔l➔u➔s➔t➔e➔r➔r➔o➔l➔e➔b➔i➔n➔d➔i➔n➔g➔.➔y➔a➔m➔l➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔r➔b➔a➔c➔.➔a➔u➔t➔h➔o➔r➔i➔z➔a➔t➔i➔o➔n➔.➔k➔8➔s➔.➔i➔o➔/➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔C➔l➔u➔s➔t➔e➔r➔R➔o➔l➔e➔B➔i➔n➔d➔i➔n➔g➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔n➔o➔d➔e➔-➔r➔e➔a➔d➔e➔r➔-➔b➔i➔n➔d➔i➔n➔g➔
➔s➔u➔b➔j➔e➔c➔t➔s➔:➔
➔-➔ ➔k➔i➔n➔d➔:➔ ➔S➔e➔r➔v➔i➔c➔e➔A➔c➔c➔o➔u➔n➔t➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔d➔e➔v➔-➔u➔s➔e➔r➔
➔ ➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔:➔ ➔d➔e➔f➔a➔u➔l➔t➔
➔r➔o➔l➔e➔R➔e➔f➔:➔
➔ ➔ ➔k➔i➔n➔d➔:➔ ➔C➔l➔u➔s➔t➔e➔r➔R➔o➔l➔e➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔n➔o➔d➔e➔-➔r➔e➔a➔d➔e➔r➔
➔ ➔ ➔a➔p➔i➔G➔r➔o➔u➔p➔:➔ ➔r➔b➔a➔c➔.➔a➔u➔t➔h➔o➔r➔i➔z➔a➔t➔i➔o➔n➔.➔k➔8➔s➔.➔i➔o➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔a➔p➔p➔l➔y➔ ➔-➔f➔ ➔c➔l➔u➔s➔t➔e➔r➔r➔o➔l➔e➔b➔i➔n➔d➔i➔n➔g➔.➔y➔a➔m➔l➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔c➔l➔u➔s➔t➔e➔r➔r➔o➔l➔e➔b➔i➔n➔d➔i➔n➔g➔s➔
➔#➔ ➔T➔e➔s➔t➔ ➔c➔l➔u➔s➔t➔e➔r➔ ➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔a➔u➔t➔h➔ ➔c➔a➔n➔-➔i➔ ➔l➔i➔s➔t➔ ➔n➔o➔d➔e➔s➔ ➔\➔
➔ ➔ ➔-➔-➔a➔s➔=➔s➔y➔s➔t➔e➔m➔:➔s➔e➔r➔v➔i➔c➔e➔a➔c➔c➔o➔u➔n➔t➔:➔d➔e➔f➔a➔u➔l➔t➔:➔d➔e➔v➔-➔u➔s➔e➔r➔
➔#➔ ➔C➔l➔e➔a➔n➔u➔p➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔l➔e➔t➔e➔ ➔-➔f➔ ➔s➔e➔r➔v➔i➔c➔e➔a➔c➔c➔o➔u➔n➔t➔.➔y➔a➔m➔l➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔l➔e➔t➔e➔ ➔-➔f➔ ➔r➔o➔l➔e➔.➔y➔a➔m➔l➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔l➔e➔t➔e➔ ➔-➔f➔ ➔r➔o➔l➔e➔b➔i➔n➔d➔i➔n➔g➔.➔y➔a➔m➔l➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔l➔e➔t➔e➔ ➔-➔f➔ ➔c➔l➔u➔s➔t➔e➔r➔r➔o➔l➔e➔.➔y➔a➔m➔l➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔l➔e➔t➔e➔ ➔-➔f➔ ➔c➔l➔u➔s➔t➔e➔r➔r➔o➔l➔e➔b➔i➔n➔d➔i➔n➔g➔.➔y➔a➔m➔l➔
➔1➔5➔.➔ ➔J➔o➔b➔s➔ ➔a➔n➔d➔ ➔C➔r➔o➔n➔J➔o➔b➔s➔
➔J➔o➔b➔ ➔—➔ ➔R➔u➔n➔ ➔t➔o➔ ➔C➔o➔m➔p➔l➔e➔t➔i➔o➔n➔
➔D➔e➔f➔i➔n➔i➔t➔i➔o➔n➔:➔ ➔A➔ ➔J➔o➔b➔ ➔c➔r➔e➔a➔t➔e➔s➔ ➔p➔o➔d➔s➔ ➔t➔h➔a➔t➔ ➔r➔u➔n➔ ➔u➔n➔t➔i➔l➔ ➔s➔u➔c➔c➔e➔s➔s➔f➔u➔l➔ ➔c➔o➔m➔p➔l➔e➔t➔i➔o➔n➔.➔ ➔U➔s➔e➔d➔ ➔f➔o➔r➔ ➔b➔a➔t➔c➔h➔ ➔t➔a➔s➔k➔s➔,➔ ➔m➔i➔g➔r➔a➔t➔i➔o➔n➔s➔,➔ ➔b➔a➔c➔k➔u➔p➔s➔.➔
➔#➔ ➔j➔o➔b➔.➔y➔a➔m➔l➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔b➔a➔t➔c➔h➔/➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔J➔o➔b➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔b➔a➔t➔c➔h➔-➔j➔o➔b➔
➔
➔
➔
➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔c➔o➔m➔p➔l➔e➔t➔i➔o➔n➔s➔:➔ ➔3➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔u➔n➔ ➔3➔ ➔s➔u➔c➔c➔e➔s➔s➔f➔u➔l➔ ➔c➔o➔m➔p➔l➔e➔t➔i➔o➔n➔s➔
➔ ➔ ➔p➔a➔r➔a➔l➔l➔e➔l➔i➔s➔m➔:➔ ➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔u➔n➔ ➔1➔ ➔p➔o➔d➔ ➔a➔t➔ ➔a➔ ➔t➔i➔m➔e➔
➔ ➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔:➔
➔ ➔ ➔ ➔ ➔s➔p➔e➔c➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔w➔o➔r➔k➔e➔r➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔b➔u➔s➔y➔b➔o➔x➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔m➔m➔a➔n➔d➔:➔ ➔[➔"➔s➔h➔"➔,➔ ➔"➔-➔c➔"➔,➔ ➔"➔e➔c➔h➔o➔ ➔P➔r➔o➔c➔e➔s➔s➔i➔n➔g➔ ➔t➔a➔s➔k➔ ➔&➔&➔ ➔s➔l➔e➔e➔p➔ ➔5➔"➔]➔
➔ ➔ ➔ ➔ ➔ ➔ ➔r➔e➔s➔t➔a➔r➔t➔P➔o➔l➔i➔c➔y➔:➔ ➔O➔n➔F➔a➔i➔l➔u➔r➔e➔ ➔ ➔ ➔#➔ ➔r➔e➔s➔t➔a➔r➔t➔ ➔o➔n➔ ➔f➔a➔i➔l➔u➔r➔e➔,➔ ➔N➔e➔v➔e➔r➔ ➔=➔ ➔d➔o➔n➔'➔t➔ ➔r➔e➔s➔t➔a➔r➔t➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔a➔p➔p➔l➔y➔ ➔-➔f➔ ➔j➔o➔b➔.➔y➔a➔m➔l➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔j➔o➔b➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔j➔o➔b➔ ➔b➔a➔t➔c➔h➔-➔j➔o➔b➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔p➔o➔d➔s➔ ➔-➔-➔s➔e➔l➔e➔c➔t➔o➔r➔=➔j➔o➔b➔-➔n➔a➔m➔e➔=➔b➔a➔t➔c➔h➔-➔j➔o➔b➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔l➔o➔g➔s➔ ➔<➔p➔o➔d➔-➔n➔a➔m➔e➔>➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔l➔e➔t➔e➔ ➔j➔o➔b➔ ➔b➔a➔t➔c➔h➔-➔j➔o➔b➔
➔C➔r➔o➔n➔J➔o➔b➔ ➔—➔ ➔S➔c➔h➔e➔d➔u➔l➔e➔d➔ ➔J➔o➔b➔s➔
➔D➔e➔f➔i➔n➔i➔t➔i➔o➔n➔:➔ ➔R➔u➔n➔s➔ ➔J➔o➔b➔s➔ ➔o➔n➔ ➔a➔ ➔s➔c➔h➔e➔d➔u➔l➔e➔ ➔(➔l➔i➔k➔e➔ ➔L➔i➔n➔u➔x➔ ➔c➔r➔o➔n➔)➔.➔ ➔U➔s➔e➔d➔ ➔f➔o➔r➔ ➔s➔c➔h➔e➔d➔u➔l➔e➔d➔ ➔b➔a➔c➔k➔u➔p➔s➔,➔ ➔c➔l➔e➔a➔n➔u➔p➔ ➔t➔a➔s➔k➔s➔,➔ ➔r➔e➔p➔o➔r➔t➔s➔.➔
➔#➔ ➔c➔r➔o➔n➔j➔o➔b➔.➔y➔a➔m➔l➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔b➔a➔t➔c➔h➔/➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔C➔r➔o➔n➔J➔o➔b➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔h➔e➔l➔l➔o➔-➔c➔r➔o➔n➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔s➔c➔h➔e➔d➔u➔l➔e➔:➔ ➔"➔*➔ ➔*➔ ➔*➔ ➔*➔ ➔*➔"➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔v➔e➔r➔y➔ ➔m➔i➔n➔u➔t➔e➔
➔ ➔ ➔#➔ ➔s➔c➔h➔e➔d➔u➔l➔e➔:➔ ➔"➔0➔ ➔2➔ ➔*➔ ➔*➔ ➔*➔"➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔a➔i➔l➔y➔ ➔a➔t➔ ➔2➔a➔m➔
➔ ➔ ➔#➔ ➔s➔c➔h➔e➔d➔u➔l➔e➔:➔ ➔"➔0➔ ➔0➔ ➔*➔ ➔*➔ ➔0➔"➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔v➔e➔r➔y➔ ➔S➔u➔n➔d➔a➔y➔ ➔m➔i➔d➔n➔i➔g➔h➔t➔
➔ ➔ ➔j➔o➔b➔T➔e➔m➔p➔l➔a➔t➔e➔:➔
➔ ➔ ➔ ➔ ➔s➔p➔e➔c➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔p➔e➔c➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔h➔e➔l➔l➔o➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔b➔u➔s➔y➔b➔o➔x➔:➔1➔.➔2➔8➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔m➔m➔a➔n➔d➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔/➔b➔i➔n➔/➔s➔h➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔-➔c➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔d➔a➔t➔e➔;➔ ➔e➔c➔h➔o➔ ➔"➔B➔a➔c➔k➔e➔n➔d➔ ➔i➔s➔ ➔h➔e➔a➔l➔t➔h➔y➔ ➔a➔n➔d➔ ➔r➔u➔n➔n➔i➔n➔g➔ ➔i➔n➔ ➔B➔e➔n➔g➔a➔l➔u➔r➔u➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔r➔e➔s➔t➔a➔r➔t➔P➔o➔l➔i➔c➔y➔:➔ ➔O➔n➔F➔a➔i➔l➔u➔r➔e➔
➔
➔
➔
➔
➔C➔r➔o➔n➔ ➔S➔c➔h➔e➔d➔u➔l➔e➔ ➔F➔o➔r➔m➔a➔t➔:➔
➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔ ➔m➔i➔n➔u➔t➔e➔ ➔(➔0➔-➔5➔9➔)➔
➔│➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔ ➔h➔o➔u➔r➔ ➔(➔0➔-➔2➔3➔)➔
➔│➔ ➔│➔ ➔┌➔─➔─➔─➔─➔─➔ ➔d➔a➔y➔ ➔o➔f➔ ➔m➔o➔n➔t➔h➔ ➔(➔1➔-➔3➔1➔)➔
➔│➔ ➔│➔ ➔│➔ ➔┌➔─➔─➔─➔ ➔m➔o➔n➔t➔h➔ ➔(➔1➔-➔1➔2➔)➔
➔│➔ ➔│➔ ➔│➔ ➔│➔ ➔┌➔─➔ ➔d➔a➔y➔ ➔o➔f➔ ➔w➔e➔e➔k➔ ➔(➔0➔-➔6➔,➔ ➔S➔u➔n➔=➔0➔)➔
➔│➔ ➔│➔ ➔│➔ ➔│➔ ➔│➔
➔*➔ ➔*➔ ➔*➔ ➔*➔ ➔*➔
➔E➔x➔a➔m➔p➔l➔e➔s➔:➔
➔"➔*➔/➔5➔ ➔*➔ ➔*➔ ➔*➔ ➔*➔"➔ ➔ ➔ ➔e➔v➔e➔r➔y➔ ➔5➔ ➔m➔i➔n➔u➔t➔e➔s➔
➔"➔0➔ ➔*➔ ➔*➔ ➔*➔ ➔*➔"➔ ➔ ➔ ➔ ➔ ➔e➔v➔e➔r➔y➔ ➔h➔o➔u➔r➔
➔"➔0➔ ➔2➔ ➔*➔ ➔*➔ ➔*➔"➔ ➔ ➔ ➔ ➔ ➔d➔a➔i➔l➔y➔ ➔a➔t➔ ➔2➔a➔m➔
➔"➔0➔ ➔0➔ ➔*➔ ➔*➔ ➔1➔"➔ ➔ ➔ ➔ ➔ ➔e➔v➔e➔r➔y➔ ➔M➔o➔n➔d➔a➔y➔ ➔m➔i➔d➔n➔i➔g➔h➔t➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔c➔r➔o➔n➔j➔o➔b➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔c➔j➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔c➔j➔ ➔h➔e➔l➔l➔o➔-➔c➔r➔o➔n➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔l➔e➔t➔e➔ ➔c➔j➔ ➔h➔e➔l➔l➔o➔-➔c➔r➔o➔n➔
➔#➔ ➔M➔a➔n➔u➔a➔l➔l➔y➔ ➔t➔r➔i➔g➔g➔e➔r➔ ➔a➔ ➔c➔r➔o➔n➔j➔o➔b➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔c➔r➔e➔a➔t➔e➔ ➔j➔o➔b➔ ➔m➔a➔n➔u➔a➔l➔-➔r➔u➔n➔ ➔-➔-➔f➔r➔o➔m➔=➔c➔r➔o➔n➔j➔o➔b➔/➔h➔e➔l➔l➔o➔-➔c➔r➔o➔n➔
➔1➔6➔.➔ ➔S➔t➔a➔t➔e➔f➔u➔l➔S➔e➔t➔ ➔—➔ ➔C➔o➔m➔p➔l➔e➔t➔e➔ ➔G➔u➔i➔d➔e➔
➔D➔e➔f➔i➔n➔i➔t➔i➔o➔n➔:➔ ➔A➔ ➔S➔t➔a➔t➔e➔f➔u➔l➔S➔e➔t➔ ➔m➔a➔n➔a➔g➔e➔s➔ ➔s➔t➔a➔t➔e➔f➔u➔l➔ ➔a➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔s➔.➔ ➔U➔n➔l➔i➔k➔e➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔s➔,➔ ➔e➔a➔c➔h➔ ➔p➔o➔d➔ ➔g➔e➔t➔s➔ ➔a➔ ➔s➔t➔a➔b➔l➔e➔,➔ ➔u➔n➔i➔q➔u➔e➔
➔i➔d➔e➔n➔t➔i➔t➔y➔ ➔t➔h➔a➔t➔ ➔p➔e➔r➔s➔i➔s➔t➔s➔ ➔a➔c➔r➔o➔s➔s➔ ➔r➔e➔s➔c➔h➔e➔d➔u➔l➔i➔n➔g➔.➔
➔S➔t➔a➔t➔e➔f➔u➔l➔S➔e➔t➔ ➔v➔s➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔
➔F➔e➔a➔t➔u➔r➔e➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔S➔t➔a➔t➔e➔f➔u➔l➔S➔e➔t➔
➔P➔o➔d➔ ➔n➔a➔m➔e➔s➔ ➔R➔a➔n➔d➔o➔m➔ ➔(➔d➔p➔1➔-➔a➔b➔c➔1➔2➔3➔)➔ ➔S➔t➔a➔b➔l➔e➔ ➔o➔r➔d➔e➔r➔e➔d➔ ➔(➔n➔g➔i➔n➔x➔-➔0➔,➔ ➔n➔g➔i➔n➔x➔-➔1➔,➔ ➔n➔g➔i➔n➔x➔-➔2➔)➔
➔P➔o➔d➔ ➔o➔r➔d➔e➔r➔ ➔C➔r➔e➔a➔t➔e➔d➔/➔d➔e➔l➔e➔t➔e➔d➔ ➔r➔a➔n➔d➔o➔m➔l➔y➔ ➔C➔r➔e➔a➔t➔e➔d➔ ➔i➔n➔ ➔o➔r➔d➔e➔r➔ ➔(➔0➔,➔1➔,➔2➔)➔,➔ ➔d➔e➔l➔e➔t➔e➔d➔ ➔i➔n➔ ➔r➔e➔v➔e➔r➔s➔e➔
➔S➔t➔o➔r➔a➔g➔e➔ ➔S➔h➔a➔r➔e➔d➔ ➔o➔r➔ ➔n➔o➔ ➔P➔V➔C➔ ➔E➔a➔c➔h➔ ➔p➔o➔d➔ ➔g➔e➔t➔s➔ ➔i➔t➔s➔ ➔O➔W➔N➔ ➔P➔V➔C➔
➔N➔e➔t➔w➔o➔r➔k➔ ➔i➔d➔e➔n➔t➔i➔t➔y➔ ➔R➔a➔n➔d➔o➔m➔ ➔I➔P➔ ➔S➔t➔a➔b➔l➔e➔ ➔h➔o➔s➔t➔n➔a➔m➔e➔ ➔v➔i➔a➔ ➔h➔e➔a➔d➔l➔e➔s➔s➔ ➔s➔e➔r➔v➔i➔c➔e➔
➔U➔s➔e➔ ➔c➔a➔s➔e➔ ➔S➔t➔a➔t➔e➔l➔e➔s➔s➔ ➔(➔w➔e➔b➔,➔ ➔A➔P➔I➔)➔ ➔S➔t➔a➔t➔e➔f➔u➔l➔ ➔(➔d➔a➔t➔a➔b➔a➔s➔e➔s➔,➔ ➔K➔a➔f➔k➔a➔,➔ ➔E➔l➔a➔s➔t➔i➔c➔s➔e➔a➔r➔c➔h➔)➔
➔
➔
➔
➔
➔S➔c➔a➔l➔i➔n➔g➔ ➔A➔n➔y➔ ➔o➔r➔d➔e➔r➔ ➔O➔r➔d➔e➔r➔e➔d➔ ➔(➔o➔n➔e➔ ➔a➔t➔ ➔a➔ ➔t➔i➔m➔e➔)➔
➔S➔t➔a➔t➔e➔f➔u➔l➔S➔e➔t➔ ➔Y➔A➔M➔L➔
➔#➔ ➔h➔e➔a➔d➔l➔e➔s➔s➔-➔s➔e➔r➔v➔i➔c➔e➔.➔y➔a➔m➔l➔ ➔(➔R➔E➔Q➔U➔I➔R➔E➔D➔ ➔f➔o➔r➔ ➔S➔t➔a➔t➔e➔f➔u➔l➔S➔e➔t➔)➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔S➔e➔r➔v➔i➔c➔e➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔n➔g➔i➔n➔x➔-➔h➔e➔a➔d➔l➔e➔s➔s➔
➔ ➔ ➔l➔a➔b➔e➔l➔s➔:➔
➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔n➔g➔i➔n➔x➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔c➔l➔u➔s➔t➔e➔r➔I➔P➔:➔ ➔N➔o➔n➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔h➔e➔a➔d➔l➔e➔s➔s➔ ➔—➔ ➔n➔o➔ ➔s➔i➔n➔g➔l➔e➔ ➔I➔P➔,➔ ➔e➔a➔c➔h➔ ➔p➔o➔d➔ ➔g➔e➔t➔s➔ ➔i➔t➔s➔ ➔o➔w➔n➔ ➔D➔N➔S➔
➔ ➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔:➔
➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔n➔g➔i➔n➔x➔
➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔ ➔ ➔-➔ ➔p➔o➔r➔t➔:➔ ➔8➔0➔
➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔w➔e➔b➔
➔-➔-➔-➔
➔#➔ ➔s➔t➔a➔t➔e➔f➔u➔l➔s➔e➔t➔.➔y➔a➔m➔l➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔a➔p➔p➔s➔/➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔S➔t➔a➔t➔e➔f➔u➔l➔S➔e➔t➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔n➔g➔i➔n➔x➔-➔s➔t➔a➔t➔e➔f➔u➔l➔s➔e➔t➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔s➔e➔r➔v➔i➔c➔e➔N➔a➔m➔e➔:➔ ➔"➔n➔g➔i➔n➔x➔-➔h➔e➔a➔d➔l➔e➔s➔s➔"➔ ➔ ➔ ➔#➔ ➔m➔u➔s➔t➔ ➔r➔e➔f➔e➔r➔e➔n➔c➔e➔ ➔h➔e➔a➔d➔l➔e➔s➔s➔ ➔s➔e➔r➔v➔i➔c➔e➔
➔ ➔ ➔r➔e➔p➔l➔i➔c➔a➔s➔:➔ ➔3➔
➔ ➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔:➔
➔ ➔ ➔ ➔ ➔m➔a➔t➔c➔h➔L➔a➔b➔e➔l➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔n➔g➔i➔n➔x➔
➔ ➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔:➔
➔ ➔ ➔ ➔ ➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔l➔a➔b➔e➔l➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔n➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔s➔p➔e➔c➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔n➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔n➔g➔i➔n➔x➔:➔l➔a➔t➔e➔s➔t➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔P➔o➔r➔t➔:➔ ➔8➔0➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔w➔e➔b➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔v➔o➔l➔u➔m➔e➔M➔o➔u➔n➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔n➔g➔i➔n➔x➔-➔s➔t➔o➔r➔a➔g➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔m➔o➔u➔n➔t➔P➔a➔t➔h➔:➔ ➔/➔u➔s➔r➔/➔s➔h➔a➔r➔e➔/➔n➔g➔i➔n➔x➔/➔h➔t➔m➔l➔
➔ ➔ ➔v➔o➔l➔u➔m➔e➔C➔l➔a➔i➔m➔T➔e➔m➔p➔l➔a➔t➔e➔s➔:➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔a➔c➔h➔ ➔p➔o➔d➔ ➔g➔e➔t➔s➔ ➔i➔t➔s➔ ➔O➔W➔N➔ ➔P➔V➔C➔ ➔a➔u➔t➔o➔m➔a➔t➔i➔c➔a➔l➔l➔y➔
➔
➔
➔
➔
➔ ➔ ➔-➔ ➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔n➔g➔i➔n➔x➔-➔s➔t➔o➔r➔a➔g➔e➔
➔ ➔ ➔ ➔ ➔s➔p➔e➔c➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔a➔c➔c➔e➔s➔s➔M➔o➔d➔e➔s➔:➔ ➔[➔"➔R➔e➔a➔d➔W➔r➔i➔t➔e➔O➔n➔c➔e➔"➔]➔
➔ ➔ ➔ ➔ ➔ ➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔r➔e➔q➔u➔e➔s➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔o➔r➔a➔g➔e➔:➔ ➔1➔G➔i➔
➔H➔o➔w➔ ➔S➔t➔a➔t➔e➔f➔u➔l➔S➔e➔t➔ ➔D➔N➔S➔ ➔W➔o➔r➔k➔s➔
➔n➔g➔i➔n➔x➔-➔0➔.➔n➔g➔i➔n➔x➔-➔h➔e➔a➔d➔l➔e➔s➔s➔.➔d➔e➔f➔a➔u➔l➔t➔.➔s➔v➔c➔.➔c➔l➔u➔s➔t➔e➔r➔.➔l➔o➔c➔a➔l➔
➔n➔g➔i➔n➔x➔-➔1➔.➔n➔g➔i➔n➔x➔-➔h➔e➔a➔d➔l➔e➔s➔s➔.➔d➔e➔f➔a➔u➔l➔t➔.➔s➔v➔c➔.➔c➔l➔u➔s➔t➔e➔r➔.➔l➔o➔c➔a➔l➔
➔n➔g➔i➔n➔x➔-➔2➔.➔n➔g➔i➔n➔x➔-➔h➔e➔a➔d➔l➔e➔s➔s➔.➔d➔e➔f➔a➔u➔l➔t➔.➔s➔v➔c➔.➔c➔l➔u➔s➔t➔e➔r➔.➔l➔o➔c➔a➔l➔
➔F➔o➔r➔m➔a➔t➔:➔ ➔<➔p➔o➔d➔-➔n➔a➔m➔e➔>➔.➔<➔s➔e➔r➔v➔i➔c➔e➔-➔n➔a➔m➔e➔>➔.➔<➔n➔a➔m➔e➔s➔p➔a➔c➔e➔>➔.➔s➔v➔c➔.➔c➔l➔u➔s➔t➔e➔r➔.➔l➔o➔c➔a➔l➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔s➔t➔a➔t➔e➔f➔u➔l➔s➔e➔t➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔s➔t➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔s➔c➔a➔l➔e➔ ➔s➔t➔s➔ ➔n➔g➔i➔n➔x➔-➔s➔t➔a➔t➔e➔f➔u➔l➔s➔e➔t➔ ➔-➔-➔r➔e➔p➔l➔i➔c➔a➔s➔=➔5➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔l➔e➔t➔e➔ ➔s➔t➔s➔ ➔n➔g➔i➔n➔x➔-➔s➔t➔a➔t➔e➔f➔u➔l➔s➔e➔t➔
➔1➔7➔.➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔S➔t➔r➔a➔t➔e➔g➔i➔e➔s➔
➔S➔t➔r➔a➔t➔e➔g➔y➔ ➔1➔:➔ ➔R➔e➔c➔r➔e➔a➔t➔e➔
➔H➔o➔w➔ ➔i➔t➔ ➔w➔o➔r➔k➔s➔:➔ ➔K➔i➔l➔l➔ ➔A➔L➔L➔ ➔o➔l➔d➔ ➔p➔o➔d➔s➔,➔ ➔t➔h➔e➔n➔ ➔c➔r➔e➔a➔t➔e➔ ➔a➔l➔l➔ ➔n➔e➔w➔ ➔p➔o➔d➔s➔.➔ ➔S➔i➔m➔p➔l➔e➔ ➔b➔u➔t➔ ➔c➔a➔u➔s➔e➔s➔ ➔d➔o➔w➔n➔t➔i➔m➔e➔.➔
➔B➔e➔f➔o➔r➔e➔:➔ ➔[➔v➔1➔]➔[➔v➔1➔]➔[➔v➔1➔]➔
➔D➔u➔r➔i➔n➔g➔:➔ ➔[➔ ➔ ➔]➔[➔ ➔ ➔]➔[➔ ➔ ➔]➔ ➔ ➔←➔ ➔D➔O➔W➔N➔T➔I➔M➔E➔
➔A➔f➔t➔e➔r➔:➔ ➔ ➔[➔v➔2➔]➔[➔v➔2➔]➔[➔v➔2➔]➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔s➔t➔r➔a➔t➔e➔g➔y➔:➔
➔ ➔ ➔ ➔ ➔t➔y➔p➔e➔:➔ ➔R➔e➔c➔r➔e➔a➔t➔e➔
➔U➔s➔e➔ ➔w➔h➔e➔n➔:➔ ➔D➔e➔v➔e➔l➔o➔p➔m➔e➔n➔t➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔s➔,➔ ➔o➔r➔ ➔w➔h➔e➔n➔ ➔o➔l➔d➔ ➔a➔n➔d➔ ➔n➔e➔w➔ ➔v➔e➔r➔s➔i➔o➔n➔s➔ ➔C➔A➔N➔N➔O➔T➔ ➔r➔u➔n➔ ➔t➔o➔g➔e➔t➔h➔e➔r➔
➔D➔o➔w➔n➔t➔i➔m➔e➔:➔ ➔Y➔E➔S➔
➔
➔
➔
➔
➔➔ ➔➔
➔R➔i➔s➔k➔:➔ ➔H➔i➔g➔h➔ ➔(➔i➔f➔ ➔n➔e➔w➔ ➔v➔e➔r➔s➔i➔o➔n➔ ➔f➔a➔i➔l➔s➔,➔ ➔d➔o➔w➔n➔t➔i➔m➔e➔ ➔c➔o➔n➔t➔i➔n➔u➔e➔s➔)➔
➔S➔t➔r➔a➔t➔e➔g➔y➔ ➔2➔:➔ ➔R➔o➔l➔l➔i➔n➔g➔ ➔U➔p➔d➔a➔t➔e➔ ➔(➔D➔e➔f➔a➔u➔l➔t➔)➔
➔H➔o➔w➔ ➔i➔t➔ ➔w➔o➔r➔k➔s➔:➔ ➔G➔r➔a➔d➔u➔a➔l➔l➔y➔ ➔r➔e➔p➔l➔a➔c➔e➔s➔ ➔o➔l➔d➔ ➔p➔o➔d➔s➔ ➔w➔i➔t➔h➔ ➔n➔e➔w➔ ➔o➔n➔e➔s➔.➔ ➔Z➔e➔r➔o➔ ➔d➔o➔w➔n➔t➔i➔m➔e➔.➔
➔S➔t➔a➔r➔t➔:➔ ➔ ➔[➔v➔1➔]➔[➔v➔1➔]➔[➔v➔1➔]➔
➔S➔t➔e➔p➔ ➔1➔:➔ ➔[➔v➔2➔]➔[➔v➔1➔]➔[➔v➔1➔]➔
➔S➔t➔e➔p➔ ➔2➔:➔ ➔[➔v➔2➔]➔[➔v➔2➔]➔[➔v➔1➔]➔
➔S➔t➔e➔p➔ ➔3➔:➔ ➔[➔v➔2➔]➔[➔v➔2➔]➔[➔v➔2➔]➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔s➔t➔r➔a➔t➔e➔g➔y➔:➔
➔ ➔ ➔ ➔ ➔t➔y➔p➔e➔:➔ ➔R➔o➔l➔l➔i➔n➔g➔U➔p➔d➔a➔t➔e➔
➔ ➔ ➔ ➔ ➔r➔o➔l➔l➔i➔n➔g➔U➔p➔d➔a➔t➔e➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔m➔a➔x➔S➔u➔r➔g➔e➔:➔ ➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔m➔a➔x➔ ➔E➔X➔T➔R➔A➔ ➔p➔o➔d➔s➔ ➔d➔u➔r➔i➔n➔g➔ ➔u➔p➔d➔a➔t➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔m➔a➔x➔U➔n➔a➔v➔a➔i➔l➔a➔b➔l➔e➔:➔ ➔1➔ ➔ ➔ ➔#➔ ➔m➔a➔x➔ ➔p➔o➔d➔s➔ ➔D➔O➔W➔N➔ ➔d➔u➔r➔i➔n➔g➔ ➔u➔p➔d➔a➔t➔e➔
➔U➔s➔e➔ ➔w➔h➔e➔n➔:➔ ➔M➔o➔s➔t➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔s➔
➔D➔o➔w➔n➔t➔i➔m➔e➔:➔ ➔N➔O➔
➔R➔o➔l➔l➔b➔a➔c➔k➔:➔ ➔k➔u➔b➔e➔c➔t➔l➔ ➔r➔o➔l➔l➔o➔u➔t➔ ➔u➔n➔d➔o➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔/➔d➔p➔1➔
➔S➔t➔r➔a➔t➔e➔g➔y➔ ➔3➔:➔ ➔B➔l➔u➔e➔-➔G➔r➔e➔e➔n➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔
➔H➔o➔w➔ ➔i➔t➔ ➔w➔o➔r➔k➔s➔:➔ ➔T➔w➔o➔ ➔i➔d➔e➔n➔t➔i➔c➔a➔l➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔s➔.➔ ➔B➔l➔u➔e➔ ➔=➔ ➔l➔i➔v➔e➔.➔ ➔G➔r➔e➔e➔n➔ ➔=➔ ➔n➔e➔w➔.➔ ➔S➔w➔i➔t➔c➔h➔ ➔t➔r➔a➔f➔f➔i➔c➔ ➔b➔y➔ ➔u➔p➔d➔a➔t➔i➔n➔g➔ ➔S➔e➔r➔v➔i➔c➔e➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔.➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔U➔s➔e➔r➔s➔ ➔→➔ ➔│➔ ➔ ➔ ➔S➔e➔r➔v➔i➔c➔e➔ ➔ ➔ ➔│➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔┬➔─➔─➔─➔─➔─➔─➔┘➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔ ➔ ➔ ➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔:➔ ➔v➔e➔r➔s➔i➔o➔n➔=➔b➔l➔u➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔ ➔ ➔ ➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔▼➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔B➔L➔U➔E➔ ➔(➔v➔1➔)➔ ➔—➔ ➔L➔I➔V➔E➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔[➔v➔1➔-➔p➔o➔d➔]➔[➔v➔1➔-➔p➔o➔d➔]➔[➔v➔1➔-➔p➔o➔d➔]➔ ➔ ➔│➔
➔ ➔ ➔ ➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔
➔ ➔ ➔ ➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔G➔R➔E➔E➔N➔ ➔(➔v➔2➔)➔ ➔—➔ ➔S➔T➔A➔N➔D➔B➔Y➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔[➔v➔2➔-➔p➔o➔d➔]➔[➔v➔2➔-➔p➔o➔d➔]➔[➔v➔2➔-➔p➔o➔d➔]➔ ➔ ➔│➔
➔ ➔ ➔ ➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔
➔A➔f➔t➔e➔r➔ ➔s➔w➔i➔t➔c➔h➔ ➔(➔s➔e➔l➔e➔c➔t➔o➔r➔:➔ ➔v➔e➔r➔s➔i➔o➔n➔=➔g➔r➔e➔e➔n➔)➔:➔
➔
➔
➔
➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔U➔s➔e➔r➔s➔ ➔→➔ ➔│➔ ➔ ➔ ➔S➔e➔r➔v➔i➔c➔e➔ ➔ ➔ ➔│➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔┬➔─➔─➔─➔─➔─➔─➔┘➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔ ➔ ➔ ➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔:➔ ➔v➔e➔r➔s➔i➔o➔n➔=➔g➔r➔e➔e➔n➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔ ➔ ➔ ➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔▼➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔G➔R➔E➔E➔N➔ ➔(➔v➔2➔)➔ ➔—➔ ➔N➔O➔W➔ ➔L➔I➔V➔E➔ ➔ ➔ ➔ ➔ ➔│➔
➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔[➔v➔2➔-➔p➔o➔d➔]➔[➔v➔2➔-➔p➔o➔d➔]➔[➔v➔2➔-➔p➔o➔d➔]➔ ➔ ➔│➔
➔ ➔ ➔ ➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔
➔#➔ ➔b➔l➔u➔e➔-➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔.➔y➔a➔m➔l➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔a➔p➔p➔s➔/➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔m➔y➔a➔p➔p➔-➔b➔l➔u➔e➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔r➔e➔p➔l➔i➔c➔a➔s➔:➔ ➔3➔
➔ ➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔:➔
➔ ➔ ➔ ➔ ➔m➔a➔t➔c➔h➔L➔a➔b➔e➔l➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔ ➔ ➔v➔e➔r➔s➔i➔o➔n➔:➔ ➔b➔l➔u➔e➔
➔ ➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔:➔
➔ ➔ ➔ ➔ ➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔l➔a➔b➔e➔l➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔v➔e➔r➔s➔i➔o➔n➔:➔ ➔b➔l➔u➔e➔
➔ ➔ ➔ ➔ ➔s➔p➔e➔c➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔m➔y➔a➔p➔p➔:➔1➔.➔0➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔P➔o➔r➔t➔:➔ ➔8➔0➔
➔-➔-➔-➔
➔#➔ ➔g➔r➔e➔e➔n➔-➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔.➔y➔a➔m➔l➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔a➔p➔p➔s➔/➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔m➔y➔a➔p➔p➔-➔g➔r➔e➔e➔n➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔r➔e➔p➔l➔i➔c➔a➔s➔:➔ ➔3➔
➔ ➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔:➔
➔ ➔ ➔ ➔ ➔m➔a➔t➔c➔h➔L➔a➔b➔e➔l➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔ ➔ ➔v➔e➔r➔s➔i➔o➔n➔:➔ ➔g➔r➔e➔e➔n➔
➔
➔
➔
➔
➔➔ ➔➔
➔ ➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔:➔
➔ ➔ ➔ ➔ ➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔l➔a➔b➔e➔l➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔v➔e➔r➔s➔i➔o➔n➔:➔ ➔g➔r➔e➔e➔n➔
➔ ➔ ➔ ➔ ➔s➔p➔e➔c➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔m➔y➔a➔p➔p➔:➔2➔.➔0➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔P➔o➔r➔t➔:➔ ➔8➔0➔
➔-➔-➔-➔
➔#➔ ➔s➔e➔r➔v➔i➔c➔e➔.➔y➔a➔m➔l➔ ➔—➔ ➔s➔w➔i➔t➔c➔h➔ ➔t➔r➔a➔f➔f➔i➔c➔ ➔b➔y➔ ➔c➔h➔a➔n➔g➔i➔n➔g➔ ➔v➔e➔r➔s➔i➔o➔n➔:➔ ➔b➔l➔u➔e➔ ➔→➔ ➔g➔r➔e➔e➔n➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔S➔e➔r➔v➔i➔c➔e➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔m➔y➔a➔p➔p➔-➔s➔e➔r➔v➔i➔c➔e➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔:➔
➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔v➔e➔r➔s➔i➔o➔n➔:➔ ➔b➔l➔u➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔←➔ ➔c➔h➔a➔n➔g➔e➔ ➔t➔o➔ ➔'➔g➔r➔e➔e➔n➔'➔ ➔t➔o➔ ➔s➔w➔i➔t➔c➔h➔ ➔t➔r➔a➔f➔f➔i➔c➔
➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔ ➔ ➔-➔ ➔p➔o➔r➔t➔:➔ ➔8➔0➔
➔ ➔ ➔ ➔ ➔t➔a➔r➔g➔e➔t➔P➔o➔r➔t➔:➔ ➔8➔0➔
➔#➔ ➔B➔l➔u➔e➔-➔G➔r➔e➔e➔n➔ ➔w➔o➔r➔k➔f➔l➔o➔w➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔a➔p➔p➔l➔y➔ ➔-➔f➔ ➔b➔l➔u➔e➔-➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔.➔y➔a➔m➔l➔ ➔ ➔ ➔ ➔#➔ ➔S➔t➔e➔p➔ ➔1➔:➔ ➔D➔e➔p➔l➔o➔y➔ ➔b➔l➔u➔e➔ ➔(➔l➔i➔v➔e➔)➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔a➔p➔p➔l➔y➔ ➔-➔f➔ ➔s➔e➔r➔v➔i➔c➔e➔.➔y➔a➔m➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔S➔t➔e➔p➔ ➔2➔:➔ ➔S➔e➔r➔v➔i➔c➔e➔ ➔p➔o➔i➔n➔t➔s➔ ➔t➔o➔ ➔b➔l➔u➔e➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔a➔p➔p➔l➔y➔ ➔-➔f➔ ➔g➔r➔e➔e➔n➔-➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔.➔y➔a➔m➔l➔ ➔ ➔ ➔#➔ ➔S➔t➔e➔p➔ ➔3➔:➔ ➔D➔e➔p➔l➔o➔y➔ ➔g➔r➔e➔e➔n➔ ➔(➔s➔t➔a➔n➔d➔b➔y➔)➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔p➔o➔r➔t➔-➔f➔o➔r➔w➔a➔r➔d➔ ➔d➔e➔p➔l➔o➔y➔/➔m➔y➔a➔p➔p➔-➔g➔r➔e➔e➔n➔ ➔8➔0➔8➔0➔:➔8➔0➔ ➔ ➔#➔ ➔S➔t➔e➔p➔ ➔4➔:➔ ➔T➔e➔s➔t➔ ➔g➔r➔e➔e➔n➔
➔#➔ ➔S➔t➔e➔p➔ ➔5➔:➔ ➔U➔p➔d➔a➔t➔e➔ ➔s➔e➔r➔v➔i➔c➔e➔.➔y➔a➔m➔l➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔ ➔t➔o➔ ➔v➔e➔r➔s➔i➔o➔n➔:➔ ➔g➔r➔e➔e➔n➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔a➔p➔p➔l➔y➔ ➔-➔f➔ ➔s➔e➔r➔v➔i➔c➔e➔.➔y➔a➔m➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔S➔t➔e➔p➔ ➔6➔:➔ ➔F➔l➔i➔p➔ ➔—➔ ➔t➔r➔a➔f➔f➔i➔c➔ ➔n➔o➔w➔ ➔g➔o➔e➔s➔ ➔t➔o➔ ➔g➔r➔e➔e➔n➔
➔#➔ ➔R➔o➔l➔l➔b➔a➔c➔k➔:➔ ➔c➔h➔a➔n➔g➔e➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔ ➔b➔a➔c➔k➔ ➔t➔o➔ ➔b➔l➔u➔e➔,➔ ➔k➔u➔b➔e➔c➔t➔l➔ ➔a➔p➔p➔l➔y➔ ➔-➔f➔ ➔s➔e➔r➔v➔i➔c➔e➔.➔y➔a➔m➔l➔
➔D➔o➔w➔n➔t➔i➔m➔e➔:➔ ➔N➔O➔ ➔(➔i➔n➔s➔t➔a➔n➔t➔ ➔s➔w➔i➔t➔c➔h➔)➔
➔R➔o➔l➔l➔b➔a➔c➔k➔:➔ ➔I➔n➔s➔t➔a➔n➔t➔ ➔(➔j➔u➔s➔t➔ ➔c➔h➔a➔n➔g➔e➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔ ➔b➔a➔c➔k➔)➔
➔C➔o➔s➔t➔:➔ ➔D➔o➔u➔b➔l➔e➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔s➔ ➔(➔b➔o➔t➔h➔ ➔v➔e➔r➔s➔i➔o➔n➔s➔ ➔r➔u➔n➔n➔i➔n➔g➔)➔
➔S➔t➔r➔a➔t➔e➔g➔y➔ ➔4➔:➔ ➔C➔a➔n➔a➔r➔y➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔
➔H➔o➔w➔ ➔i➔t➔ ➔w➔o➔r➔k➔s➔:➔ ➔S➔e➔n➔d➔ ➔a➔ ➔s➔m➔a➔l➔l➔ ➔p➔e➔r➔c➔e➔n➔t➔a➔g➔e➔ ➔o➔f➔ ➔t➔r➔a➔f➔f➔i➔c➔ ➔t➔o➔ ➔n➔e➔w➔ ➔v➔e➔r➔s➔i➔o➔n➔.➔ ➔G➔r➔a➔d➔u➔a➔l➔l➔y➔ ➔i➔n➔c➔r➔e➔a➔s➔e➔ ➔i➔f➔ ➔s➔t➔a➔b➔l➔e➔.➔
➔
➔
➔
➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔U➔s➔e➔r➔s➔ ➔→➔ ➔│➔ ➔ ➔ ➔S➔e➔r➔v➔i➔c➔e➔ ➔ ➔ ➔│➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔┬➔─➔─➔─➔─➔─➔─➔┘➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔ ➔ ➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┴➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔ ➔ ➔ ➔ ➔▼➔ ➔ ➔(➔9➔0➔%➔ ➔t➔r➔a➔f➔f➔i➔c➔)➔ ➔ ➔ ➔ ➔ ➔ ➔▼➔ ➔ ➔(➔1➔0➔%➔ ➔t➔r➔a➔f➔f➔i➔c➔)➔
➔[➔v➔1➔]➔[➔v➔1➔]➔[➔v➔1➔]➔[➔v➔1➔]➔[➔v➔1➔]➔ ➔ ➔ ➔ ➔[➔v➔2➔]➔
➔ ➔S➔T➔A➔B➔L➔E➔ ➔(➔5➔ ➔p➔o➔d➔s➔)➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔C➔A➔N➔A➔R➔Y➔ ➔(➔1➔ ➔p➔o➔d➔)➔
➔#➔ ➔s➔t➔a➔b➔l➔e➔-➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔.➔y➔a➔m➔l➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔a➔p➔p➔s➔/➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔m➔y➔a➔p➔p➔-➔s➔t➔a➔b➔l➔e➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔r➔e➔p➔l➔i➔c➔a➔s➔:➔ ➔9➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔9➔0➔%➔ ➔o➔f➔ ➔t➔r➔a➔f➔f➔i➔c➔
➔ ➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔:➔
➔ ➔ ➔ ➔ ➔m➔a➔t➔c➔h➔L➔a➔b➔e➔l➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔:➔
➔ ➔ ➔ ➔ ➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔l➔a➔b➔e➔l➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔v➔e➔r➔s➔i➔o➔n➔:➔ ➔s➔t➔a➔b➔l➔e➔
➔ ➔ ➔ ➔ ➔s➔p➔e➔c➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔m➔y➔a➔p➔p➔:➔1➔.➔0➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔P➔o➔r➔t➔:➔ ➔8➔0➔
➔-➔-➔-➔
➔#➔ ➔c➔a➔n➔a➔r➔y➔-➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔.➔y➔a➔m➔l➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔a➔p➔p➔s➔/➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔m➔y➔a➔p➔p➔-➔c➔a➔n➔a➔r➔y➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔r➔e➔p➔l➔i➔c➔a➔s➔:➔ ➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔1➔0➔%➔ ➔o➔f➔ ➔t➔r➔a➔f➔f➔i➔c➔
➔ ➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔:➔
➔ ➔ ➔ ➔ ➔m➔a➔t➔c➔h➔L➔a➔b➔e➔l➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔:➔
➔ ➔ ➔ ➔ ➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔l➔a➔b➔e➔l➔s➔:➔
➔
➔
➔
➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔v➔e➔r➔s➔i➔o➔n➔:➔ ➔c➔a➔n➔a➔r➔y➔
➔ ➔ ➔ ➔ ➔s➔p➔e➔c➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔m➔y➔a➔p➔p➔:➔2➔.➔0➔ ➔ ➔ ➔#➔ ➔N➔E➔W➔ ➔v➔e➔r➔s➔i➔o➔n➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔P➔o➔r➔t➔:➔ ➔8➔0➔
➔-➔-➔-➔
➔#➔ ➔s➔e➔r➔v➔i➔c➔e➔.➔y➔a➔m➔l➔ ➔—➔ ➔r➔o➔u➔t➔e➔s➔ ➔t➔o➔ ➔B➔O➔T➔H➔ ➔(➔s➔e➔l➔e➔c➔t➔o➔r➔ ➔o➔n➔l➔y➔ ➔u➔s➔e➔s➔ ➔'➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔'➔)➔
➔a➔p➔i➔V➔e➔r➔s➔i➔o➔n➔:➔ ➔v➔1➔
➔k➔i➔n➔d➔:➔ ➔S➔e➔r➔v➔i➔c➔e➔
➔m➔e➔t➔a➔d➔a➔t➔a➔:➔
➔ ➔ ➔n➔a➔m➔e➔:➔ ➔m➔y➔a➔p➔p➔-➔s➔e➔r➔v➔i➔c➔e➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔:➔
➔ ➔ ➔ ➔ ➔a➔p➔p➔:➔ ➔m➔y➔a➔p➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔m➔a➔t➔c➔h➔e➔s➔ ➔B➔O➔T➔H➔ ➔s➔t➔a➔b➔l➔e➔ ➔a➔n➔d➔ ➔c➔a➔n➔a➔r➔y➔ ➔p➔o➔d➔s➔
➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔ ➔ ➔-➔ ➔p➔o➔r➔t➔:➔ ➔8➔0➔
➔ ➔ ➔ ➔ ➔t➔a➔r➔g➔e➔t➔P➔o➔r➔t➔:➔ ➔8➔0➔
➔D➔o➔w➔n➔t➔i➔m➔e➔:➔ ➔N➔O➔
➔R➔i➔s➔k➔:➔ ➔L➔o➔w➔ ➔(➔o➔n➔l➔y➔ ➔s➔m➔a➔l➔l➔ ➔%➔ ➔o➔f➔ ➔u➔s➔e➔r➔s➔ ➔s➔e➔e➔ ➔n➔e➔w➔ ➔v➔e➔r➔s➔i➔o➔n➔)➔
➔R➔o➔l➔l➔b➔a➔c➔k➔:➔ ➔S➔c➔a➔l➔e➔ ➔c➔a➔n➔a➔r➔y➔ ➔t➔o➔ ➔0➔,➔ ➔s➔c➔a➔l➔e➔ ➔s➔t➔a➔b➔l➔e➔ ➔b➔a➔c➔k➔ ➔u➔p➔
➔U➔s➔e➔ ➔w➔h➔e➔n➔:➔ ➔A➔/➔B➔ ➔t➔e➔s➔t➔i➔n➔g➔,➔ ➔g➔r➔a➔d➔u➔a➔l➔ ➔r➔o➔l➔l➔o➔u➔t➔ ➔t➔o➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔S➔t➔r➔a➔t➔e➔g➔y➔ ➔C➔o➔m➔p➔a➔r➔i➔s➔o➔n➔
➔S➔t➔r➔a➔t➔e➔g➔y➔ ➔D➔o➔w➔n➔t➔i➔m➔e➔ ➔R➔o➔l➔l➔b➔a➔c➔k➔ ➔S➔p➔e➔e➔d➔ ➔R➔e➔s➔o➔u➔r➔c➔e➔ ➔C➔o➔s➔t➔ ➔U➔s➔e➔ ➔C➔a➔s➔e➔
➔R➔e➔c➔r➔e➔a➔t➔e➔ ➔Y➔E➔S➔ ➔S➔l➔o➔w➔ ➔N➔o➔r➔m➔a➔l➔ ➔D➔e➔v➔/➔s➔i➔m➔p➔l➔e➔ ➔a➔p➔p➔s➔
➔R➔o➔l➔l➔i➔n➔g➔ ➔U➔p➔d➔a➔t➔e➔ ➔N➔O➔ ➔F➔a➔s➔t➔ ➔N➔o➔r➔m➔a➔l➔+➔s➔l➔i➔g➔h➔t➔ ➔M➔o➔s➔t➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔a➔p➔p➔s➔
➔B➔l➔u➔e➔-➔G➔r➔e➔e➔n➔ ➔N➔O➔ ➔I➔n➔s➔t➔a➔n➔t➔ ➔D➔o➔u➔b➔l➔e➔ ➔C➔r➔i➔t➔i➔c➔a➔l➔ ➔a➔p➔p➔s➔,➔ ➔i➔n➔s➔t➔a➔n➔t➔ ➔r➔o➔l➔l➔b➔a➔c➔k➔
➔C➔a➔n➔a➔r➔y➔ ➔N➔O➔ ➔F➔a➔s➔t➔ ➔N➔o➔r➔m➔a➔l➔+➔s➔m➔a➔l➔l➔ ➔R➔i➔s➔k➔-➔a➔v➔e➔r➔s➔e➔,➔ ➔A➔/➔B➔ ➔t➔e➔s➔t➔i➔n➔g➔
➔1➔8➔.➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔ ➔T➔r➔o➔u➔b➔l➔e➔s➔h➔o➔o➔t➔i➔n➔g➔ ➔G➔u➔i➔d➔e➔
➔
➔
➔
➔
➔M➔o➔s➔t➔ ➔I➔m➔p➔o➔r➔t➔a➔n➔t➔ ➔D➔e➔b➔u➔g➔g➔i➔n➔g➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔
➔#➔ ➔C➔h➔e➔c➔k➔ ➔e➔v➔e➔r➔y➔t➔h➔i➔n➔g➔ ➔a➔t➔ ➔o➔n➔c➔e➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔a➔l➔l➔ ➔-➔n➔ ➔<➔n➔a➔m➔e➔s➔p➔a➔c➔e➔>➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔e➔v➔e➔n➔t➔s➔ ➔-➔-➔s➔o➔r➔t➔-➔b➔y➔=➔'➔.➔l➔a➔s➔t➔T➔i➔m➔e➔s➔t➔a➔m➔p➔'➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔o➔r➔t➔e➔d➔ ➔e➔v➔e➔n➔t➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔e➔v➔e➔n➔t➔s➔ ➔-➔n➔ ➔d➔e➔f➔a➔u➔l➔t➔ ➔|➔ ➔g➔r➔e➔p➔ ➔-➔i➔ ➔w➔a➔r➔n➔i➔n➔g➔ ➔ ➔ ➔#➔ ➔o➔n➔l➔y➔ ➔w➔a➔r➔n➔i➔n➔g➔s➔
➔#➔ ➔P➔o➔d➔ ➔d➔e➔b➔u➔g➔g➔i➔n➔g➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔p➔o➔d➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔e➔c➔k➔ ➔p➔o➔d➔ ➔s➔t➔a➔t➔u➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔p➔o➔d➔ ➔<➔p➔o➔d➔-➔n➔a➔m➔e➔>➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔M➔O➔S➔T➔ ➔U➔S➔E➔F➔U➔L➔ ➔—➔ ➔e➔v➔e➔n➔t➔s➔ ➔+➔ ➔d➔e➔t➔a➔i➔l➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔l➔o➔g➔s➔ ➔<➔p➔o➔d➔-➔n➔a➔m➔e➔>➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔l➔o➔g➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔l➔o➔g➔s➔ ➔<➔p➔o➔d➔-➔n➔a➔m➔e➔>➔ ➔-➔c➔ ➔<➔c➔o➔n➔t➔a➔i➔n➔e➔r➔-➔n➔a➔m➔e➔>➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔l➔o➔g➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔l➔o➔g➔s➔ ➔<➔p➔o➔d➔-➔n➔a➔m➔e➔>➔ ➔-➔-➔p➔r➔e➔v➔i➔o➔u➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔o➔g➔s➔ ➔f➔r➔o➔m➔ ➔c➔r➔a➔s➔h➔e➔d➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔l➔o➔g➔s➔ ➔<➔p➔o➔d➔-➔n➔a➔m➔e➔>➔ ➔-➔f➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔l➔l➔o➔w➔ ➔l➔i➔v➔e➔ ➔l➔o➔g➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔e➔x➔e➔c➔ ➔-➔i➔t➔ ➔<➔p➔o➔d➔-➔n➔a➔m➔e➔>➔ ➔-➔-➔ ➔/➔b➔i➔n➔/➔b➔a➔s➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔e➔l➔l➔ ➔i➔n➔t➔o➔ ➔p➔o➔d➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔e➔x➔e➔c➔ ➔-➔i➔t➔ ➔<➔p➔o➔d➔-➔n➔a➔m➔e➔>➔ ➔-➔-➔ ➔/➔b➔i➔n➔/➔s➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔i➔f➔ ➔b➔a➔s➔h➔ ➔n➔o➔t➔ ➔a➔v➔a➔i➔l➔a➔b➔l➔e➔
➔#➔ ➔N➔o➔d➔e➔ ➔d➔e➔b➔u➔g➔g➔i➔n➔g➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔n➔o➔d➔e➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔n➔o➔d➔e➔ ➔s➔t➔a➔t➔u➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔n➔o➔d➔e➔ ➔<➔n➔o➔d➔e➔-➔n➔a➔m➔e➔>➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔n➔o➔d➔e➔ ➔d➔e➔t➔a➔i➔l➔s➔ ➔+➔ ➔c➔o➔n➔d➔i➔t➔i➔o➔n➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔t➔o➔p➔ ➔n➔o➔d➔e➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔C➔P➔U➔/➔m➔e➔m➔o➔r➔y➔ ➔u➔s➔a➔g➔e➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔t➔o➔p➔ ➔p➔o➔d➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔o➔d➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔u➔s➔a➔g➔e➔
➔E➔r➔r➔o➔r➔ ➔1➔:➔ ➔C➔r➔a➔s➔h➔L➔o➔o➔p➔B➔a➔c➔k➔O➔f➔f➔
➔W➔h➔a➔t➔ ➔i➔t➔ ➔m➔e➔a➔n➔s➔:➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔k➔e➔e➔p➔s➔ ➔s➔t➔a➔r➔t➔i➔n➔g➔ ➔a➔n➔d➔ ➔c➔r➔a➔s➔h➔i➔n➔g➔ ➔r➔e➔p➔e➔a➔t➔e➔d➔l➔y➔.➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔ ➔k➔e➔e➔p➔s➔ ➔t➔r➔y➔i➔n➔g➔ ➔(➔b➔a➔c➔k➔i➔n➔g➔ ➔o➔f➔f➔ ➔w➔i➔t➔h➔
➔i➔n➔c➔r➔e➔a➔s➔i➔n➔g➔ ➔d➔e➔l➔a➔y➔)➔.➔
➔S➔T➔A➔T➔U➔S➔:➔ ➔C➔r➔a➔s➔h➔L➔o➔o➔p➔B➔a➔c➔k➔O➔f➔f➔
➔H➔o➔w➔ ➔t➔o➔ ➔d➔i➔a➔g➔n➔o➔s➔e➔:➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔p➔o➔d➔ ➔<➔p➔o➔d➔-➔n➔a➔m➔e➔>➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔e➔c➔k➔ ➔E➔v➔e➔n➔t➔s➔ ➔s➔e➔c➔t➔i➔o➔n➔ ➔f➔o➔r➔ ➔e➔r➔r➔o➔r➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔l➔o➔g➔s➔ ➔<➔p➔o➔d➔-➔n➔a➔m➔e➔>➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔l➔o➔g➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔l➔o➔g➔s➔ ➔<➔p➔o➔d➔-➔n➔a➔m➔e➔>➔ ➔-➔-➔p➔r➔e➔v➔i➔o➔u➔s➔ ➔ ➔ ➔#➔ ➔l➔o➔g➔s➔ ➔f➔r➔o➔m➔ ➔C➔R➔A➔S➔H➔E➔D➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔(➔m➔o➔s➔t➔ ➔u➔s➔e➔f➔u➔l➔)➔
➔C➔o➔m➔m➔o➔n➔ ➔c➔a➔u➔s➔e➔s➔ ➔a➔n➔d➔ ➔f➔i➔x➔e➔s➔:➔
➔C➔a➔u➔s➔e➔ ➔F➔i➔x➔
➔A➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔ ➔e➔r➔r➔o➔r➔ ➔o➔n➔ ➔s➔t➔a➔r➔t➔u➔p➔ ➔F➔i➔x➔ ➔b➔u➔g➔ ➔i➔n➔ ➔y➔o➔u➔r➔ ➔a➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔ ➔c➔o➔d➔e➔
➔
➔
➔
➔
➔W➔r➔o➔n➔g➔ ➔c➔o➔m➔m➔a➔n➔d➔/➔e➔n➔t➔r➔y➔p➔o➔i➔n➔t➔ ➔i➔n➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔ ➔F➔i➔x➔ ➔C➔M➔D➔ ➔o➔r➔ ➔E➔N➔T➔R➔Y➔P➔O➔I➔N➔T➔
➔M➔i➔s➔s➔i➔n➔g➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔ ➔A➔d➔d➔ ➔r➔e➔q➔u➔i➔r➔e➔d➔ ➔e➔n➔v➔ ➔v➔a➔r➔ ➔t➔o➔ ➔p➔o➔d➔ ➔s➔p➔e➔c➔
➔M➔i➔s➔s➔i➔n➔g➔ ➔C➔o➔n➔f➔i➔g➔M➔a➔p➔ ➔o➔r➔ ➔S➔e➔c➔r➔e➔t➔ ➔C➔r➔e➔a➔t➔e➔ ➔t➔h➔e➔ ➔C➔o➔n➔f➔i➔g➔M➔a➔p➔/➔S➔e➔c➔r➔e➔t➔
➔W➔r➔o➔n➔g➔ ➔p➔o➔r➔t➔ ➔i➔n➔ ➔l➔i➔v➔e➔n➔e➔s➔s➔ ➔p➔r➔o➔b➔e➔ ➔F➔i➔x➔ ➔p➔r➔o➔b➔e➔ ➔p➔o➔r➔t➔ ➔t➔o➔ ➔m➔a➔t➔c➔h➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔p➔o➔r➔t➔
➔O➔u➔t➔ ➔o➔f➔ ➔m➔e➔m➔o➔r➔y➔ ➔I➔n➔c➔r➔e➔a➔s➔e➔ ➔m➔e➔m➔o➔r➔y➔ ➔l➔i➔m➔i➔t➔s➔
➔C➔o➔n➔f➔i➔g➔ ➔f➔i➔l➔e➔ ➔m➔i➔s➔s➔i➔n➔g➔ ➔M➔o➔u➔n➔t➔ ➔c➔o➔r➔r➔e➔c➔t➔ ➔C➔o➔n➔f➔i➔g➔M➔a➔p➔/➔v➔o➔l➔u➔m➔e➔
➔#➔ ➔D➔e➔b➔u➔g➔:➔ ➔s➔t➔a➔r➔t➔ ➔w➔i➔t➔h➔ ➔l➔o➔g➔ ➔f➔r➔o➔m➔ ➔p➔r➔e➔v➔i➔o➔u➔s➔ ➔c➔r➔a➔s➔h➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔l➔o➔g➔s➔ ➔<➔p➔o➔d➔-➔n➔a➔m➔e➔>➔ ➔-➔-➔p➔r➔e➔v➔i➔o➔u➔s➔
➔#➔ ➔I➔f➔ ➔l➔o➔g➔s➔ ➔a➔r➔e➔ ➔e➔m➔p➔t➔y➔ ➔(➔c➔r➔a➔s➔h➔ ➔b➔e➔f➔o➔r➔e➔ ➔l➔o➔g➔g➔i➔n➔g➔)➔,➔ ➔o➔v➔e➔r➔r➔i➔d➔e➔ ➔e➔n➔t➔r➔y➔p➔o➔i➔n➔t➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔r➔u➔n➔ ➔d➔e➔b➔u➔g➔ ➔-➔-➔i➔m➔a➔g➔e➔=➔m➔y➔a➔p➔p➔:➔1➔.➔0➔ ➔-➔-➔c➔o➔m➔m➔a➔n➔d➔ ➔-➔-➔ ➔s➔l➔e➔e➔p➔ ➔3➔6➔0➔0➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔e➔x➔e➔c➔ ➔-➔i➔t➔ ➔d➔e➔b➔u➔g➔ ➔-➔-➔ ➔/➔b➔i➔n➔/➔s➔h➔ ➔ ➔ ➔ ➔#➔ ➔m➔a➔n➔u➔a➔l➔l➔y➔ ➔e➔x➔p➔l➔o➔r➔e➔ ➔w➔h➔a➔t➔'➔s➔ ➔w➔r➔o➔n➔g➔
➔E➔r➔r➔o➔r➔ ➔2➔:➔ ➔I➔m➔a➔g➔e➔P➔u➔l➔l➔B➔a➔c➔k➔O➔f➔f➔ ➔/➔ ➔E➔r➔r➔I➔m➔a➔g➔e➔P➔u➔l➔l➔
➔W➔h➔a➔t➔ ➔i➔t➔ ➔m➔e➔a➔n➔s➔:➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔ ➔c➔a➔n➔'➔t➔ ➔p➔u➔l➔l➔ ➔t➔h➔e➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔i➔m➔a➔g➔e➔ ➔f➔r➔o➔m➔ ➔t➔h➔e➔ ➔r➔e➔g➔i➔s➔t➔r➔y➔.➔
➔S➔T➔A➔T➔U➔S➔:➔ ➔I➔m➔a➔g➔e➔P➔u➔l➔l➔B➔a➔c➔k➔O➔f➔f➔ ➔o➔r➔ ➔E➔r➔r➔I➔m➔a➔g➔e➔P➔u➔l➔l➔
➔H➔o➔w➔ ➔t➔o➔ ➔d➔i➔a➔g➔n➔o➔s➔e➔:➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔p➔o➔d➔ ➔<➔p➔o➔d➔-➔n➔a➔m➔e➔>➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔e➔c➔k➔ ➔E➔v➔e➔n➔t➔s➔ ➔—➔ ➔w➔i➔l➔l➔ ➔s➔h➔o➔w➔ ➔p➔u➔l➔l➔ ➔e➔r➔r➔o➔r➔
➔C➔o➔m➔m➔o➔n➔ ➔c➔a➔u➔s➔e➔s➔ ➔a➔n➔d➔ ➔f➔i➔x➔e➔s➔:➔
➔C➔a➔u➔s➔e➔ ➔F➔i➔x➔
➔W➔r➔o➔n➔g➔ ➔i➔m➔a➔g➔e➔ ➔n➔a➔m➔e➔ ➔F➔i➔x➔ ➔i➔m➔a➔g➔e➔ ➔n➔a➔m➔e➔ ➔i➔n➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔Y➔A➔M➔L➔
➔W➔r➔o➔n➔g➔ ➔t➔a➔g➔ ➔F➔i➔x➔ ➔i➔m➔a➔g➔e➔ ➔t➔a➔g➔ ➔(➔c➔h➔e➔c➔k➔ ➔i➔f➔ ➔i➔t➔ ➔e➔x➔i➔s➔t➔s➔ ➔i➔n➔ ➔r➔e➔g➔i➔s➔t➔r➔y➔)➔
➔I➔m➔a➔g➔e➔ ➔d➔o➔e➔s➔n➔'➔t➔ ➔e➔x➔i➔s➔t➔ ➔P➔u➔s➔h➔ ➔i➔m➔a➔g➔e➔ ➔t➔o➔ ➔r➔e➔g➔i➔s➔t➔r➔y➔ ➔f➔i➔r➔s➔t➔
➔P➔r➔i➔v➔a➔t➔e➔ ➔r➔e➔g➔i➔s➔t➔r➔y➔ ➔—➔ ➔n➔o➔ ➔c➔r➔e➔d➔e➔n➔t➔i➔a➔l➔s➔ ➔C➔r➔e➔a➔t➔e➔ ➔d➔o➔c➔k➔e➔r➔-➔r➔e➔g➔i➔s➔t➔r➔y➔ ➔s➔e➔c➔r➔e➔t➔ ➔a➔n➔d➔ ➔a➔d➔d➔ ➔i➔m➔a➔g➔e➔P➔u➔l➔l➔S➔e➔c➔r➔e➔t➔s➔
➔
➔
➔
➔
➔➔ ➔➔
➔R➔e➔g➔i➔s➔t➔r➔y➔ ➔d➔o➔w➔n➔ ➔W➔a➔i➔t➔ ➔o➔r➔ ➔s➔w➔i➔t➔c➔h➔ ➔t➔o➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔t➔ ➔t➔a➔g➔
➔#➔ ➔F➔i➔x➔ ➔f➔o➔r➔ ➔p➔r➔i➔v➔a➔t➔e➔ ➔r➔e➔g➔i➔s➔t➔r➔y➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔c➔r➔e➔a➔t➔e➔ ➔s➔e➔c➔r➔e➔t➔ ➔d➔o➔c➔k➔e➔r➔-➔r➔e➔g➔i➔s➔t➔r➔y➔ ➔r➔e➔g➔c➔r➔e➔d➔ ➔\➔
➔ ➔ ➔-➔-➔d➔o➔c➔k➔e➔r➔-➔s➔e➔r➔v➔e➔r➔=➔d➔o➔c➔k➔e➔r➔.➔i➔o➔ ➔\➔
➔ ➔ ➔-➔-➔d➔o➔c➔k➔e➔r➔-➔u➔s➔e➔r➔n➔a➔m➔e➔=➔a➔k➔h➔i➔l➔ ➔\➔
➔ ➔ ➔-➔-➔d➔o➔c➔k➔e➔r➔-➔p➔a➔s➔s➔w➔o➔r➔d➔=➔m➔y➔p➔a➔s➔s➔w➔o➔r➔d➔
➔#➔ ➔A➔d➔d➔ ➔t➔o➔ ➔p➔o➔d➔ ➔s➔p➔e➔c➔:➔
➔s➔p➔e➔c➔:➔
➔ ➔ ➔i➔m➔a➔g➔e➔P➔u➔l➔l➔S➔e➔c➔r➔e➔t➔s➔:➔
➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔r➔e➔g➔c➔r➔e➔d➔
➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔
➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔c➔1➔
➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔p➔r➔i➔v➔a➔t➔e➔-➔r➔e➔p➔o➔/➔m➔y➔a➔p➔p➔:➔1➔.➔0➔
➔E➔r➔r➔o➔r➔ ➔3➔:➔ ➔P➔e➔n➔d➔i➔n➔g➔ ➔P➔o➔d➔s➔
➔W➔h➔a➔t➔ ➔i➔t➔ ➔m➔e➔a➔n➔s➔:➔ ➔P➔o➔d➔ ➔i➔s➔ ➔w➔a➔i➔t➔i➔n➔g➔ ➔t➔o➔ ➔b➔e➔ ➔s➔c➔h➔e➔d➔u➔l➔e➔d➔ ➔b➔u➔t➔ ➔c➔a➔n➔'➔t➔ ➔b➔e➔ ➔p➔l➔a➔c➔e➔d➔ ➔o➔n➔ ➔a➔n➔y➔ ➔n➔o➔d➔e➔.➔
➔S➔T➔A➔T➔U➔S➔:➔ ➔P➔e➔n➔d➔i➔n➔g➔
➔H➔o➔w➔ ➔t➔o➔ ➔d➔i➔a➔g➔n➔o➔s➔e➔:➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔p➔o➔d➔ ➔<➔p➔o➔d➔-➔n➔a➔m➔e➔>➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔o➔o➔k➔ ➔a➔t➔ ➔E➔v➔e➔n➔t➔s➔ ➔—➔ ➔s➔h➔o➔w➔s➔ ➔w➔h➔y➔ ➔s➔c➔h➔e➔d➔u➔l➔i➔n➔g➔ ➔f➔a➔i➔l➔e➔d➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔n➔o➔d➔e➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔e➔c➔k➔ ➔n➔o➔d➔e➔ ➔s➔t➔a➔t➔u➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔n➔o➔d➔e➔ ➔<➔n➔o➔d➔e➔-➔n➔a➔m➔e➔>➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔e➔c➔k➔ ➔n➔o➔d➔e➔ ➔c➔o➔n➔d➔i➔t➔i➔o➔n➔s➔ ➔a➔n➔d➔ ➔c➔a➔p➔a➔c➔i➔t➔y➔
➔C➔o➔m➔m➔o➔n➔ ➔c➔a➔u➔s➔e➔s➔ ➔a➔n➔d➔ ➔f➔i➔x➔e➔s➔:➔
➔C➔a➔u➔s➔e➔ ➔F➔i➔x➔
➔N➔o➔t➔ ➔e➔n➔o➔u➔g➔h➔ ➔C➔P➔U➔/➔m➔e➔m➔o➔r➔y➔ ➔o➔n➔ ➔a➔n➔y➔ ➔n➔o➔d➔e➔ ➔A➔d➔d➔ ➔m➔o➔r➔e➔ ➔n➔o➔d➔e➔s➔ ➔o➔r➔ ➔r➔e➔d➔u➔c➔e➔ ➔p➔o➔d➔ ➔r➔e➔q➔u➔e➔s➔t➔s➔
➔N➔o➔d➔e➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔ ➔d➔o➔e➔s➔n➔'➔t➔ ➔m➔a➔t➔c➔h➔ ➔a➔n➔y➔ ➔n➔o➔d➔e➔ ➔F➔i➔x➔ ➔n➔o➔d➔e➔S➔e➔l➔e➔c➔t➔o➔r➔ ➔o➔r➔ ➔n➔o➔d➔e➔ ➔l➔a➔b➔e➔l➔s➔
➔T➔a➔i➔n➔t➔ ➔o➔n➔ ➔a➔l➔l➔ ➔n➔o➔d➔e➔s➔,➔ ➔n➔o➔ ➔t➔o➔l➔e➔r➔a➔t➔i➔o➔n➔ ➔A➔d➔d➔ ➔t➔o➔l➔e➔r➔a➔t➔i➔o➔n➔ ➔o➔r➔ ➔r➔e➔m➔o➔v➔e➔ ➔t➔a➔i➔n➔t➔
➔P➔V➔C➔ ➔n➔o➔t➔ ➔b➔o➔u➔n➔d➔ ➔(➔s➔t➔o➔r➔a➔g➔e➔ ➔i➔s➔s➔u➔e➔)➔ ➔F➔i➔x➔ ➔P➔V➔/➔P➔V➔C➔ ➔—➔ ➔c➔h➔e➔c➔k➔ ➔s➔t➔o➔r➔a➔g➔e➔ ➔c➔l➔a➔s➔s➔
➔
➔
➔
➔
➔A➔l➔l➔ ➔n➔o➔d➔e➔s➔ ➔a➔r➔e➔ ➔f➔u➔l➔l➔ ➔S➔c➔a➔l➔e➔ ➔u➔p➔ ➔c➔l➔u➔s➔t➔e➔r➔ ➔(➔a➔d➔d➔ ➔n➔o➔d➔e➔s➔)➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔p➔o➔d➔ ➔<➔p➔o➔d➔-➔n➔a➔m➔e➔>➔ ➔|➔ ➔g➔r➔e➔p➔ ➔-➔A➔ ➔1➔0➔ ➔"➔E➔v➔e➔n➔t➔s➔:➔"➔
➔#➔ ➔L➔o➔o➔k➔ ➔f➔o➔r➔:➔ ➔"➔0➔/➔3➔ ➔n➔o➔d➔e➔s➔ ➔a➔r➔e➔ ➔a➔v➔a➔i➔l➔a➔b➔l➔e➔:➔ ➔3➔ ➔I➔n➔s➔u➔f➔f➔i➔c➔i➔e➔n➔t➔ ➔m➔e➔m➔o➔r➔y➔"➔
➔#➔ ➔O➔r➔:➔ ➔"➔0➔/➔3➔ ➔n➔o➔d➔e➔s➔ ➔a➔r➔e➔ ➔a➔v➔a➔i➔l➔a➔b➔l➔e➔:➔ ➔n➔o➔d➔e➔(➔s➔)➔ ➔h➔a➔d➔ ➔t➔a➔i➔n➔t➔"➔
➔E➔r➔r➔o➔r➔ ➔4➔:➔ ➔N➔o➔d➔e➔N➔o➔t➔R➔e➔a➔d➔y➔
➔W➔h➔a➔t➔ ➔i➔t➔ ➔m➔e➔a➔n➔s➔:➔ ➔A➔ ➔n➔o➔d➔e➔ ➔i➔s➔ ➔n➔o➔t➔ ➔a➔c➔c➔e➔p➔t➔i➔n➔g➔ ➔p➔o➔d➔s➔ ➔—➔ ➔i➔t➔'➔s➔ ➔i➔n➔ ➔a➔n➔ ➔u➔n➔h➔e➔a➔l➔t➔h➔y➔ ➔s➔t➔a➔t➔e➔.➔
➔S➔T➔A➔T➔U➔S➔:➔ ➔N➔o➔t➔R➔e➔a➔d➔y➔
➔H➔o➔w➔ ➔t➔o➔ ➔d➔i➔a➔g➔n➔o➔s➔e➔:➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔n➔o➔d➔e➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔e➔ ➔N➔o➔t➔R➔e➔a➔d➔y➔ ➔s➔t➔a➔t➔u➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔n➔o➔d➔e➔ ➔<➔n➔o➔d➔e➔-➔n➔a➔m➔e➔>➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔e➔c➔k➔ ➔C➔o➔n➔d➔i➔t➔i➔o➔n➔s➔ ➔s➔e➔c➔t➔i➔o➔n➔
➔#➔ ➔L➔o➔o➔k➔ ➔f➔o➔r➔:➔ ➔M➔e➔m➔o➔r➔y➔P➔r➔e➔s➔s➔u➔r➔e➔,➔ ➔D➔i➔s➔k➔P➔r➔e➔s➔s➔u➔r➔e➔,➔ ➔P➔I➔D➔P➔r➔e➔s➔s➔u➔r➔e➔,➔ ➔N➔e➔t➔w➔o➔r➔k➔U➔n➔a➔v➔a➔i➔l➔a➔b➔l➔e➔
➔C➔o➔m➔m➔o➔n➔ ➔c➔a➔u➔s➔e➔s➔ ➔a➔n➔d➔ ➔f➔i➔x➔e➔s➔:➔
➔C➔a➔u➔s➔e➔ ➔F➔i➔x➔
➔k➔u➔b➔e➔l➔e➔t➔ ➔n➔o➔t➔ ➔r➔u➔n➔n➔i➔n➔g➔ ➔S➔S➔H➔ ➔t➔o➔ ➔n➔o➔d➔e➔,➔ ➔s➔y➔s➔t➔e➔m➔c➔t➔l➔ ➔r➔e➔s➔t➔a➔r➔t➔ ➔k➔u➔b➔e➔l➔e➔t➔
➔N➔e➔t➔w➔o➔r➔k➔ ➔p➔l➔u➔g➔i➔n➔ ➔(➔C➔N➔I➔)➔ ➔f➔a➔i➔l➔e➔d➔ ➔R➔e➔s➔t➔a➔r➔t➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔p➔l➔u➔g➔i➔n➔ ➔D➔a➔e➔m➔o➔n➔S➔e➔t➔
➔N➔o➔d➔e➔ ➔o➔u➔t➔ ➔o➔f➔ ➔d➔i➔s➔k➔ ➔F➔r➔e➔e➔ ➔d➔i➔s➔k➔ ➔s➔p➔a➔c➔e➔,➔ ➔a➔d➔d➔ ➔s➔t➔o➔r➔a➔g➔e➔
➔N➔o➔d➔e➔ ➔o➔u➔t➔ ➔o➔f➔ ➔m➔e➔m➔o➔r➔y➔ ➔F➔r➔e➔e➔ ➔m➔e➔m➔o➔r➔y➔ ➔o➔r➔ ➔a➔d➔d➔ ➔m➔o➔r➔e➔ ➔R➔A➔M➔
➔N➔o➔d➔e➔ ➔l➔o➔s➔t➔ ➔c➔o➔n➔n➔e➔c➔t➔i➔v➔i➔t➔y➔ ➔C➔h➔e➔c➔k➔ ➔n➔e➔t➔w➔o➔r➔k➔,➔ ➔r➔e➔s➔t➔a➔r➔t➔ ➔n➔o➔d➔e➔
➔#➔ ➔S➔S➔H➔ ➔t➔o➔ ➔t➔h➔e➔ ➔p➔r➔o➔b➔l➔e➔m➔ ➔n➔o➔d➔e➔
➔s➔s➔h➔ ➔e➔c➔2➔-➔u➔s➔e➔r➔@➔<➔n➔o➔d➔e➔-➔i➔p➔>➔
➔s➔y➔s➔t➔e➔m➔c➔t➔l➔ ➔s➔t➔a➔t➔u➔s➔ ➔k➔u➔b➔e➔l➔e➔t➔
➔j➔o➔u➔r➔n➔a➔l➔c➔t➔l➔ ➔-➔u➔ ➔k➔u➔b➔e➔l➔e➔t➔ ➔-➔f➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔k➔u➔b➔e➔l➔e➔t➔ ➔l➔o➔g➔s➔
➔s➔y➔s➔t➔e➔m➔c➔t➔l➔ ➔r➔e➔s➔t➔a➔r➔t➔ ➔k➔u➔b➔e➔l➔e➔t➔
➔
➔
➔
➔
➔E➔r➔r➔o➔r➔ ➔5➔:➔ ➔U➔n➔a➔u➔t➔h➔o➔r➔i➔z➔e➔d➔ ➔E➔r➔r➔o➔r➔
➔W➔h➔a➔t➔ ➔i➔t➔ ➔m➔e➔a➔n➔s➔:➔ ➔Y➔o➔u➔ ➔d➔o➔n➔'➔t➔ ➔h➔a➔v➔e➔ ➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔ ➔t➔o➔ ➔p➔e➔r➔f➔o➔r➔m➔ ➔a➔n➔ ➔a➔c➔t➔i➔o➔n➔.➔
➔E➔r➔r➔o➔r➔:➔ ➔U➔n➔a➔u➔t➔h➔o➔r➔i➔z➔e➔d➔ ➔/➔ ➔F➔o➔r➔b➔i➔d➔d➔e➔n➔
➔H➔o➔w➔ ➔t➔o➔ ➔d➔i➔a➔g➔n➔o➔s➔e➔:➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔a➔u➔t➔h➔ ➔c➔a➔n➔-➔i➔ ➔g➔e➔t➔ ➔p➔o➔d➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔e➔c➔k➔ ➔y➔o➔u➔r➔ ➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔a➔u➔t➔h➔ ➔c➔a➔n➔-➔i➔ ➔g➔e➔t➔ ➔p➔o➔d➔s➔ ➔-➔n➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔i➔n➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔a➔u➔t➔h➔ ➔c➔a➔n➔-➔i➔ ➔-➔-➔l➔i➔s➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔a➔l➔l➔ ➔y➔o➔u➔r➔ ➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔
➔C➔o➔m➔m➔o➔n➔ ➔c➔a➔u➔s➔e➔s➔ ➔a➔n➔d➔ ➔f➔i➔x➔e➔s➔:➔
➔C➔a➔u➔s➔e➔ ➔F➔i➔x➔
➔k➔u➔b➔e➔c➔o➔n➔f➔i➔g➔ ➔w➔r➔o➔n➔g➔ ➔o➔r➔ ➔e➔x➔p➔i➔r➔e➔d➔ ➔R➔e➔-➔d➔o➔w➔n➔l➔o➔a➔d➔/➔r➔e➔f➔r➔e➔s➔h➔ ➔k➔u➔b➔e➔c➔o➔n➔f➔i➔g➔
➔M➔i➔s➔s➔i➔n➔g➔ ➔R➔o➔l➔e➔/➔C➔l➔u➔s➔t➔e➔r➔R➔o➔l➔e➔ ➔C➔r➔e➔a➔t➔e➔ ➔R➔o➔l➔e➔ ➔w➔i➔t➔h➔ ➔n➔e➔e➔d➔e➔d➔ ➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔
➔M➔i➔s➔s➔i➔n➔g➔ ➔R➔o➔l➔e➔B➔i➔n➔d➔i➔n➔g➔ ➔C➔r➔e➔a➔t➔e➔ ➔R➔o➔l➔e➔B➔i➔n➔d➔i➔n➔g➔ ➔t➔o➔ ➔c➔o➔n➔n➔e➔c➔t➔ ➔u➔s➔e➔r➔ ➔t➔o➔ ➔R➔o➔l➔e➔
➔W➔r➔o➔n➔g➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔ ➔C➔h➔e➔c➔k➔ ➔i➔f➔ ➔y➔o➔u➔'➔r➔e➔ ➔i➔n➔ ➔t➔h➔e➔ ➔r➔i➔g➔h➔t➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔
➔S➔e➔r➔v➔i➔c➔e➔A➔c➔c➔o➔u➔n➔t➔ ➔m➔i➔s➔s➔i➔n➔g➔ ➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔ ➔C➔r➔e➔a➔t➔e➔ ➔R➔B➔A➔C➔ ➔f➔o➔r➔ ➔t➔h➔e➔ ➔S➔e➔r➔v➔i➔c➔e➔A➔c➔c➔o➔u➔n➔t➔
➔E➔r➔r➔o➔r➔ ➔6➔:➔ ➔O➔O➔M➔K➔i➔l➔l➔e➔d➔ ➔(➔O➔u➔t➔ ➔o➔f➔ ➔M➔e➔m➔o➔r➔y➔ ➔K➔i➔l➔l➔e➔d➔)➔
➔W➔h➔a➔t➔ ➔i➔t➔ ➔m➔e➔a➔n➔s➔:➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔u➔s➔e➔d➔ ➔m➔o➔r➔e➔ ➔m➔e➔m➔o➔r➔y➔ ➔t➔h➔a➔n➔ ➔i➔t➔s➔ ➔l➔i➔m➔i➔t➔ ➔—➔ ➔L➔i➔n➔u➔x➔ ➔k➔e➔r➔n➔e➔l➔ ➔k➔i➔l➔l➔e➔d➔ ➔i➔t➔.➔
➔S➔T➔A➔T➔U➔S➔:➔ ➔O➔O➔M➔K➔i➔l➔l➔e➔d➔ ➔(➔l➔a➔s➔t➔ ➔s➔t➔a➔t➔e➔ ➔r➔e➔a➔s➔o➔n➔)➔
➔H➔o➔w➔ ➔t➔o➔ ➔d➔i➔a➔g➔n➔o➔s➔e➔:➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔p➔o➔d➔ ➔<➔p➔o➔d➔-➔n➔a➔m➔e➔>➔
➔#➔ ➔L➔o➔o➔k➔ ➔f➔o➔r➔:➔ ➔L➔a➔s➔t➔ ➔S➔t➔a➔t➔e➔:➔ ➔T➔e➔r➔m➔i➔n➔a➔t➔e➔d➔,➔ ➔R➔e➔a➔s➔o➔n➔:➔ ➔O➔O➔M➔K➔i➔l➔l➔e➔d➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔t➔o➔p➔ ➔p➔o➔d➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔e➔c➔k➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔m➔e➔m➔o➔r➔y➔ ➔u➔s➔a➔g➔e➔
➔C➔o➔m➔m➔o➔n➔ ➔c➔a➔u➔s➔e➔s➔ ➔a➔n➔d➔ ➔f➔i➔x➔e➔s➔:➔
➔
➔
➔
➔
➔C➔a➔u➔s➔e➔ ➔F➔i➔x➔
➔M➔e➔m➔o➔r➔y➔ ➔l➔i➔m➔i➔t➔ ➔t➔o➔o➔ ➔l➔o➔w➔ ➔I➔n➔c➔r➔e➔a➔s➔e➔ ➔m➔e➔m➔o➔r➔y➔ ➔l➔i➔m➔i➔t➔s➔
➔M➔e➔m➔o➔r➔y➔ ➔l➔e➔a➔k➔ ➔i➔n➔ ➔a➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔ ➔F➔i➔x➔ ➔a➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔ ➔m➔e➔m➔o➔r➔y➔ ➔l➔e➔a➔k➔
➔S➔u➔d➔d➔e➔n➔ ➔t➔r➔a➔f➔f➔i➔c➔ ➔s➔p➔i➔k➔e➔ ➔S➔e➔t➔ ➔H➔P➔A➔ ➔t➔o➔ ➔s➔c➔a➔l➔e➔ ➔b➔e➔f➔o➔r➔e➔ ➔O➔O➔M➔
➔#➔ ➔F➔i➔x➔:➔ ➔i➔n➔c➔r➔e➔a➔s➔e➔ ➔m➔e➔m➔o➔r➔y➔ ➔l➔i➔m➔i➔t➔
➔r➔e➔s➔o➔u➔r➔c➔e➔s➔:➔
➔ ➔ ➔r➔e➔q➔u➔e➔s➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔m➔e➔m➔o➔r➔y➔:➔ ➔"➔2➔5➔6➔M➔i➔"➔
➔ ➔ ➔l➔i➔m➔i➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔m➔e➔m➔o➔r➔y➔:➔ ➔"➔5➔1➔2➔M➔i➔"➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔i➔n➔c➔r➔e➔a➔s➔e➔ ➔t➔h➔i➔s➔
➔E➔r➔r➔o➔r➔ ➔7➔:➔ ➔F➔a➔i➔l➔e➔d➔S➔c➔h➔e➔d➔u➔l➔i➔n➔g➔
➔W➔h➔a➔t➔ ➔i➔t➔ ➔m➔e➔a➔n➔s➔:➔ ➔S➔c➔h➔e➔d➔u➔l➔e➔r➔ ➔c➔a➔n➔'➔t➔ ➔f➔i➔n➔d➔ ➔a➔ ➔s➔u➔i➔t➔a➔b➔l➔e➔ ➔n➔o➔d➔e➔ ➔f➔o➔r➔ ➔t➔h➔e➔ ➔p➔o➔d➔.➔
➔E➔v➔e➔n➔t➔s➔:➔ ➔F➔a➔i➔l➔e➔d➔S➔c➔h➔e➔d➔u➔l➔i➔n➔g➔
➔D➔i➔a➔g➔n➔o➔s➔i➔s➔:➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔p➔o➔d➔ ➔<➔p➔o➔d➔-➔n➔a➔m➔e➔>➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔E➔v➔e➔n➔t➔s➔ ➔w➔i➔l➔l➔ ➔s➔h➔o➔w➔ ➔e➔x➔a➔c➔t➔ ➔r➔e➔a➔s➔o➔n➔
➔C➔o➔m➔m➔o➔n➔ ➔r➔e➔a➔s➔o➔n➔s➔:➔
➔0➔/➔3➔ ➔n➔o➔d➔e➔s➔ ➔a➔r➔e➔ ➔a➔v➔a➔i➔l➔a➔b➔l➔e➔:➔ ➔3➔ ➔I➔n➔s➔u➔f➔f➔i➔c➔i➔e➔n➔t➔ ➔m➔e➔m➔o➔r➔y➔
➔0➔/➔3➔ ➔n➔o➔d➔e➔s➔ ➔a➔r➔e➔ ➔a➔v➔a➔i➔l➔a➔b➔l➔e➔:➔ ➔3➔ ➔n➔o➔d➔e➔(➔s➔)➔ ➔h➔a➔d➔ ➔t➔a➔i➔n➔t➔
➔0➔/➔3➔ ➔n➔o➔d➔e➔s➔ ➔a➔r➔e➔ ➔a➔v➔a➔i➔l➔a➔b➔l➔e➔:➔ ➔3➔ ➔n➔o➔d➔e➔(➔s➔)➔ ➔d➔i➔d➔n➔'➔t➔ ➔m➔a➔t➔c➔h➔ ➔n➔o➔d➔e➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔
➔F➔i➔x➔:➔ ➔B➔a➔s➔e➔d➔ ➔o➔n➔ ➔t➔h➔e➔ ➔m➔e➔s➔s➔a➔g➔e➔ ➔—➔ ➔a➔d➔d➔ ➔n➔o➔d➔e➔s➔,➔ ➔r➔e➔m➔o➔v➔e➔ ➔t➔a➔i➔n➔t➔s➔,➔ ➔o➔r➔ ➔f➔i➔x➔ ➔n➔o➔d➔e➔ ➔s➔e➔l➔e➔c➔t➔o➔r➔s➔.➔
➔E➔r➔r➔o➔r➔ ➔8➔:➔ ➔E➔r➔r➔o➔r➔ ➔C➔r➔e➔a➔t➔i➔n➔g➔ ➔L➔o➔a➔d➔B➔a➔l➔a➔n➔c➔e➔r➔
➔W➔h➔a➔t➔ ➔i➔t➔ ➔m➔e➔a➔n➔s➔:➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔ ➔c➔o➔u➔l➔d➔n➔'➔t➔ ➔c➔r➔e➔a➔t➔e➔ ➔a➔ ➔c➔l➔o➔u➔d➔ ➔l➔o➔a➔d➔ ➔b➔a➔l➔a➔n➔c➔e➔r➔.➔
➔H➔o➔w➔ ➔t➔o➔ ➔d➔i➔a➔g➔n➔o➔s➔e➔:➔
➔
➔
➔
➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔s➔e➔r➔v➔i➔c➔e➔ ➔<➔s➔e➔r➔v➔i➔c➔e➔-➔n➔a➔m➔e➔>➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔e➔c➔k➔ ➔E➔v➔e➔n➔t➔s➔
➔C➔o➔m➔m➔o➔n➔ ➔c➔a➔u➔s➔e➔s➔ ➔a➔n➔d➔ ➔f➔i➔x➔e➔s➔:➔
➔C➔a➔u➔s➔e➔ ➔F➔i➔x➔
➔I➔n➔s➔u➔f➔f➔i➔c➔i➔e➔n➔t➔ ➔I➔A➔M➔ ➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔ ➔A➔d➔d➔ ➔l➔o➔a➔d➔ ➔b➔a➔l➔a➔n➔c➔e➔r➔ ➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔ ➔t➔o➔ ➔n➔o➔d➔e➔ ➔I➔A➔M➔ ➔r➔o➔l➔e➔
➔C➔l➔o➔u➔d➔ ➔p➔r➔o➔v➔i➔d➔e➔r➔ ➔q➔u➔o➔t➔a➔ ➔e➔x➔c➔e➔e➔d➔e➔d➔ ➔R➔e➔q➔u➔e➔s➔t➔ ➔q➔u➔o➔t➔a➔ ➔i➔n➔c➔r➔e➔a➔s➔e➔
➔W➔r➔o➔n➔g➔ ➔A➔W➔S➔ ➔r➔e➔g➔i➔o➔n➔/➔z➔o➔n➔e➔ ➔c➔o➔n➔f➔i➔g➔ ➔F➔i➔x➔ ➔c➔l➔u➔s➔t➔e➔r➔ ➔c➔o➔n➔f➔i➔g➔ ➔f➔o➔r➔ ➔c➔o➔r➔r➔e➔c➔t➔ ➔r➔e➔g➔i➔o➔n➔
➔S➔e➔c➔u➔r➔i➔t➔y➔ ➔g➔r➔o➔u➔p➔ ➔i➔s➔s➔u➔e➔ ➔C➔h➔e➔c➔k➔ ➔s➔e➔c➔u➔r➔i➔t➔y➔ ➔g➔r➔o➔u➔p➔ ➔a➔l➔l➔o➔w➔s➔ ➔r➔e➔q➔u➔i➔r➔e➔d➔ ➔p➔o➔r➔t➔s➔
➔E➔r➔r➔o➔r➔ ➔9➔:➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔C➔r➔e➔a➔t➔i➔n➔g➔ ➔(➔S➔t➔u➔c➔k➔)➔
➔W➔h➔a➔t➔ ➔i➔t➔ ➔m➔e➔a➔n➔s➔:➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔i➔s➔ ➔s➔t➔u➔c➔k➔ ➔i➔n➔ ➔c➔r➔e➔a➔t➔i➔n➔g➔ ➔s➔t➔a➔t➔e➔.➔
➔S➔T➔A➔T➔U➔S➔:➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔C➔r➔e➔a➔t➔i➔n➔g➔ ➔(➔f➔o➔r➔ ➔t➔o➔o➔ ➔l➔o➔n➔g➔)➔
➔H➔o➔w➔ ➔t➔o➔ ➔d➔i➔a➔g➔n➔o➔s➔e➔:➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔p➔o➔d➔ ➔<➔p➔o➔d➔-➔n➔a➔m➔e➔>➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔e➔c➔k➔ ➔E➔v➔e➔n➔t➔s➔
➔C➔o➔m➔m➔o➔n➔ ➔c➔a➔u➔s➔e➔s➔ ➔a➔n➔d➔ ➔f➔i➔x➔e➔s➔:➔
➔C➔a➔u➔s➔e➔ ➔F➔i➔x➔
➔V➔o➔l➔u➔m➔e➔ ➔m➔o➔u➔n➔t➔ ➔i➔s➔s➔u➔e➔ ➔(➔P➔V➔C➔ ➔n➔o➔t➔ ➔b➔o➔u➔n➔d➔)➔ ➔C➔h➔e➔c➔k➔ ➔P➔V➔C➔ ➔s➔t➔a➔t➔u➔s➔,➔ ➔f➔i➔x➔ ➔s➔t➔o➔r➔a➔g➔e➔
➔C➔o➔n➔f➔i➔g➔M➔a➔p➔/➔S➔e➔c➔r➔e➔t➔ ➔d➔o➔e➔s➔n➔'➔t➔ ➔e➔x➔i➔s➔t➔ ➔C➔r➔e➔a➔t➔e➔ ➔m➔i➔s➔s➔i➔n➔g➔ ➔C➔o➔n➔f➔i➔g➔M➔a➔p➔ ➔o➔r➔ ➔S➔e➔c➔r➔e➔t➔
➔I➔m➔a➔g➔e➔ ➔b➔e➔i➔n➔g➔ ➔p➔u➔l➔l➔e➔d➔ ➔(➔s➔l➔o➔w➔ ➔r➔e➔g➔i➔s➔t➔r➔y➔)➔ ➔W➔a➔i➔t➔,➔ ➔o➔r➔ ➔u➔s➔e➔ ➔i➔m➔a➔g➔e➔ ➔p➔u➔l➔l➔ ➔p➔o➔l➔i➔c➔y➔
➔N➔e➔t➔w➔o➔r➔k➔ ➔p➔l➔u➔g➔i➔n➔ ➔n➔o➔t➔ ➔r➔e➔a➔d➔y➔ ➔R➔e➔s➔t➔a➔r➔t➔ ➔C➔N➔I➔ ➔D➔a➔e➔m➔o➔n➔S➔e➔t➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔p➔v➔c➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔e➔c➔k➔ ➔i➔f➔ ➔P➔V➔C➔ ➔i➔s➔ ➔b➔o➔u➔n➔d➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔c➔o➔n➔f➔i➔g➔m➔a➔p➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔e➔c➔k➔ ➔i➔f➔ ➔C➔M➔ ➔e➔x➔i➔s➔t➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔s➔e➔c➔r➔e➔t➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔e➔c➔k➔ ➔i➔f➔ ➔S➔e➔c➔r➔e➔t➔ ➔e➔x➔i➔s➔t➔s➔
➔
➔
➔
➔
➔G➔e➔n➔e➔r➔a➔l➔ ➔T➔r➔o➔u➔b➔l➔e➔s➔h➔o➔o➔t➔i➔n➔g➔ ➔W➔o➔r➔k➔f➔l➔o➔w➔
➔1➔.➔ ➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔p➔o➔d➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔t➔h➔e➔ ➔S➔T➔A➔T➔U➔S➔?➔
➔2➔.➔ ➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔p➔o➔d➔ ➔<➔n➔a➔m➔e➔>➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔W➔h➔a➔t➔ ➔d➔o➔ ➔E➔V➔E➔N➔T➔S➔ ➔s➔a➔y➔?➔
➔3➔.➔ ➔k➔u➔b➔e➔c➔t➔l➔ ➔l➔o➔g➔s➔ ➔<➔p➔o➔d➔-➔n➔a➔m➔e➔>➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔W➔h➔a➔t➔ ➔d➔o➔e➔s➔ ➔t➔h➔e➔ ➔A➔P➔P➔ ➔s➔a➔y➔?➔
➔4➔.➔ ➔k➔u➔b➔e➔c➔t➔l➔ ➔l➔o➔g➔s➔ ➔<➔n➔a➔m➔e➔>➔ ➔-➔-➔p➔r➔e➔v➔i➔o➔u➔s➔ ➔ ➔ ➔ ➔→➔ ➔W➔h➔a➔t➔ ➔d➔i➔d➔ ➔i➔t➔ ➔s➔a➔y➔ ➔b➔e➔f➔o➔r➔e➔ ➔c➔r➔a➔s➔h➔?➔
➔5➔.➔ ➔k➔u➔b➔e➔c➔t➔l➔ ➔e➔x➔e➔c➔ ➔-➔i➔t➔ ➔<➔n➔a➔m➔e➔>➔ ➔-➔-➔ ➔s➔h➔ ➔ ➔ ➔ ➔ ➔→➔ ➔C➔a➔n➔ ➔I➔ ➔g➔e➔t➔ ➔i➔n➔s➔i➔d➔e➔?➔
➔6➔.➔ ➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔e➔v➔e➔n➔t➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔A➔n➔y➔t➔h➔i➔n➔g➔ ➔u➔n➔u➔s➔u➔a➔l➔?➔
➔7➔.➔ ➔k➔u➔b➔e➔c➔t➔l➔ ➔t➔o➔p➔ ➔p➔o➔d➔s➔ ➔/➔ ➔n➔o➔d➔e➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔R➔e➔s➔o➔u➔r➔c➔e➔ ➔p➔r➔e➔s➔s➔u➔r➔e➔?➔
➔8➔.➔ ➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔n➔o➔d➔e➔ ➔<➔n➔a➔m➔e➔>➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔N➔o➔d➔e➔ ➔h➔e➔a➔l➔t➔h➔y➔?➔
➔1➔9➔.➔ ➔E➔s➔s➔e➔n➔t➔i➔a➔l➔ ➔k➔u➔b➔e➔c➔t➔l➔ ➔Q➔u➔i➔c➔k➔ ➔R➔e➔f➔e➔r➔e➔n➔c➔e➔
➔#➔ ➔G➔E➔T➔ ➔(➔v➔i➔e➔w➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔s➔)➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔p➔o➔d➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔o➔d➔s➔ ➔i➔n➔ ➔d➔e➔f➔a➔u➔l➔t➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔p➔o➔d➔s➔ ➔-➔n➔ ➔k➔u➔b➔e➔-➔s➔y➔s➔t➔e➔m➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔o➔d➔s➔ ➔i➔n➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔p➔o➔d➔s➔ ➔-➔A➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔o➔d➔s➔ ➔i➔n➔ ➔A➔L➔L➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔p➔o➔d➔s➔ ➔-➔o➔ ➔w➔i➔d➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔w➔i➔t➔h➔ ➔I➔P➔ ➔a➔n➔d➔ ➔n➔o➔d➔e➔ ➔i➔n➔f➔o➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔p➔o➔d➔s➔ ➔-➔w➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔w➔a➔t➔c➔h➔ ➔(➔l➔i➔v➔e➔ ➔u➔p➔d➔a➔t➔e➔s➔)➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔a➔l➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔l➔l➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔s➔ ➔i➔n➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔
➔#➔ ➔D➔E➔S➔C➔R➔I➔B➔E➔ ➔(➔d➔e➔t➔a➔i➔l➔e➔d➔ ➔i➔n➔f➔o➔)➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔p➔o➔d➔ ➔<➔n➔a➔m➔e➔>➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔n➔o➔d➔e➔ ➔<➔n➔a➔m➔e➔>➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔s➔e➔r➔v➔i➔c➔e➔ ➔<➔n➔a➔m➔e➔>➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔s➔c➔r➔i➔b➔e➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔<➔n➔a➔m➔e➔>➔
➔#➔ ➔A➔P➔P➔L➔Y➔ ➔/➔ ➔C➔R➔E➔A➔T➔E➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔a➔p➔p➔l➔y➔ ➔-➔f➔ ➔f➔i➔l➔e➔.➔y➔a➔m➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔o➔r➔ ➔u➔p➔d➔a➔t➔e➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔c➔r➔e➔a➔t➔e➔ ➔-➔f➔ ➔f➔i➔l➔e➔.➔y➔a➔m➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔o➔n➔l➔y➔ ➔(➔f➔a➔i➔l➔s➔ ➔i➔f➔ ➔e➔x➔i➔s➔t➔s➔)➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔a➔p➔p➔l➔y➔ ➔-➔f➔ ➔.➔/➔d➔i➔r➔e➔c➔t➔o➔r➔y➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔p➔p➔l➔y➔ ➔a➔l➔l➔ ➔Y➔A➔M➔L➔s➔ ➔i➔n➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔a➔p➔p➔l➔y➔ ➔-➔f➔ ➔h➔t➔t➔p➔s➔:➔/➔/➔u➔r➔l➔/➔f➔i➔l➔e➔.➔y➔a➔m➔l➔ ➔ ➔#➔ ➔a➔p➔p➔l➔y➔ ➔f➔r➔o➔m➔ ➔U➔R➔L➔
➔#➔ ➔D➔E➔L➔E➔T➔E➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔l➔e➔t➔e➔ ➔p➔o➔d➔ ➔<➔n➔a➔m➔e➔>➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔l➔e➔t➔e➔ ➔-➔f➔ ➔f➔i➔l➔e➔.➔y➔a➔m➔l➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔l➔e➔t➔e➔ ➔p➔o➔d➔s➔ ➔-➔-➔a➔l➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔a➔l➔l➔ ➔p➔o➔d➔s➔ ➔i➔n➔ ➔n➔a➔m➔e➔s➔p➔a➔c➔e➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔d➔e➔l➔e➔t➔e➔ ➔p➔o➔d➔s➔ ➔-➔l➔ ➔a➔p➔p➔=➔m➔y➔a➔p➔p➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔b➔y➔ ➔l➔a➔b➔e➔l➔
➔#➔ ➔E➔X➔E➔C➔U➔T➔E➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔e➔x➔e➔c➔ ➔-➔i➔t➔ ➔<➔p➔o➔d➔>➔ ➔-➔-➔ ➔b➔a➔s➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔e➔l➔l➔ ➔i➔n➔t➔o➔ ➔p➔o➔d➔
➔
➔
➔
➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔e➔x➔e➔c➔ ➔-➔i➔t➔ ➔<➔p➔o➔d➔>➔ ➔-➔-➔ ➔c➔a➔t➔ ➔/➔e➔t➔c➔/➔c➔o➔n➔f➔i➔g➔ ➔ ➔#➔ ➔r➔u➔n➔ ➔c➔o➔m➔m➔a➔n➔d➔ ➔i➔n➔ ➔p➔o➔d➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔c➔p➔ ➔l➔o➔c➔a➔l➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔<➔p➔o➔d➔>➔:➔/➔p➔a➔t➔h➔/➔ ➔#➔ ➔c➔o➔p➔y➔ ➔f➔i➔l➔e➔ ➔t➔o➔ ➔p➔o➔d➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔c➔p➔ ➔<➔p➔o➔d➔>➔:➔/➔p➔a➔t➔h➔/➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔.➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔p➔y➔ ➔f➔i➔l➔e➔ ➔f➔r➔o➔m➔ ➔p➔o➔d➔
➔#➔ ➔P➔O➔R➔T➔ ➔F➔O➔R➔W➔A➔R➔D➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔p➔o➔r➔t➔-➔f➔o➔r➔w➔a➔r➔d➔ ➔p➔o➔d➔/➔<➔n➔a➔m➔e➔>➔ ➔8➔0➔8➔0➔:➔8➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔o➔c➔a➔l➔:➔p➔o➔d➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔p➔o➔r➔t➔-➔f➔o➔r➔w➔a➔r➔d➔ ➔s➔e➔r➔v➔i➔c➔e➔/➔<➔n➔a➔m➔e➔>➔ ➔8➔0➔8➔0➔:➔8➔0➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔r➔w➔a➔r➔d➔ ➔s➔e➔r➔v➔i➔c➔e➔ ➔p➔o➔r➔t➔
➔#➔ ➔L➔A➔B➔E➔L➔S➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔l➔a➔b➔e➔l➔ ➔p➔o➔d➔ ➔<➔n➔a➔m➔e➔>➔ ➔e➔n➔v➔=➔p➔r➔o➔d➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔d➔d➔ ➔l➔a➔b➔e➔l➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔p➔o➔d➔s➔ ➔-➔l➔ ➔e➔n➔v➔=➔p➔r➔o➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔l➔t➔e➔r➔ ➔b➔y➔ ➔l➔a➔b➔e➔l➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔g➔e➔t➔ ➔p➔o➔d➔s➔ ➔-➔-➔s➔h➔o➔w➔-➔l➔a➔b➔e➔l➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔a➔l➔l➔ ➔l➔a➔b➔e➔l➔s➔
➔#➔ ➔S➔C➔A➔L➔I➔N➔G➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔s➔c➔a➔l➔e➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔d➔p➔1➔ ➔-➔-➔r➔e➔p➔l➔i➔c➔a➔s➔=➔5➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔a➔u➔t➔o➔s➔c➔a➔l➔e➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔d➔p➔1➔ ➔-➔-➔m➔i➔n➔=➔2➔ ➔-➔-➔m➔a➔x➔=➔1➔0➔ ➔-➔-➔c➔p➔u➔-➔p➔e➔r➔c➔e➔n➔t➔=➔8➔0➔
➔#➔ ➔C➔O➔N➔F➔I➔G➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔c➔o➔n➔f➔i➔g➔ ➔g➔e➔t➔-➔c➔o➔n➔t➔e➔x➔t➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔a➔v➔a➔i➔l➔a➔b➔l➔e➔ ➔c➔l➔u➔s➔t➔e➔r➔s➔/➔c➔o➔n➔t➔e➔x➔t➔s➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔c➔o➔n➔f➔i➔g➔ ➔u➔s➔e➔-➔c➔o➔n➔t➔e➔x➔t➔ ➔<➔n➔a➔m➔e➔>➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔w➔i➔t➔c➔h➔ ➔c➔l➔u➔s➔t➔e➔r➔
➔k➔u➔b➔e➔c➔t➔l➔ ➔c➔o➔n➔f➔i➔g➔ ➔c➔u➔r➔r➔e➔n➔t➔-➔c➔o➔n➔t➔e➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔c➔o➔n➔t➔e➔x➔t➔
➔

---

## 🚀 Modern 2026 Production Kubernetes Blueprint

### 1. Container Runtime: containerd
* `dockershim` is permanently deprecated. Modern Kubernetes nodes communicate directly with **`containerd`** via the Container Runtime Interface (CRI), reducing memory overhead and process hopping.

### 2. Modern Ingress Specification (`networking.k8s.io/v1`)
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: app-ingress
  namespace: production
  annotations:
    kubernetes.io/ingress.class: nginx
    cert-manager.io/cluster-issuer: letsencrypt-prod
spec:
  rules:
    - host: api.cloudvault.net
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: payment-api-svc
                port:
                  number: 80
```
