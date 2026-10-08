# 🐳 Docker Containerization: The Definitive Master Engineering Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers Container Architecture, Virtual Machines vs Containers, Image Layering, Multi-Stage Builds, Security Hardening, Docker Compose, Production CLI, and Real-World Troubleshooting.

---

## 📑 Table of Contents
- [Docker Architecture & Core Workflow](#docker-architecture--core-workflow)
- [Core Concepts & Foundations](#core-concepts--foundations)
- [Dockerfile Instructions Deep Dive](#dockerfile-instructions-deep-dive)
- [Multi-Stage Production Dockerfile](#multi-stage-production-dockerfile)
- [Docker Networking Deep Dive](#docker-networking-deep-dive)
- [Docker Storage: Volumes vs Bind Mounts](#docker-storage-volumes-vs-bind-mounts)
- [Multi-Container Orchestration with Docker Compose](#multi-container-orchestration-with-docker-compose)
- [Production Command Cheat Sheet](#production-command-cheat-sheet)
- [Production Troubleshooting & Debugging](#production-troubleshooting--debugging)
- [High-Yield Technical Interview Q&A](#high-yield-technical-interview-qa)

---

➔S➔E➔C➔T➔I➔O➔N➔ ➔3➔:➔ ➔D➔O➔C➔K➔E➔R➔ ➔—➔ ➔C➔O➔M➔P➔L➔E➔T➔E➔ ➔G➔U➔I➔D➔E➔
➔D➔o➔c➔k➔e➔r➔ ➔A➔r➔c➔h➔i➔t➔e➔c➔t➔u➔r➔e➔
➔D➔o➔c➔k➔e➔r➔ ➔h➔a➔s➔ ➔t➔h➔r➔e➔e➔ ➔m➔a➔i➔n➔ ➔c➔o➔m➔p➔o➔n➔e➔n➔t➔s➔:➔
➔1➔.➔ ➔D➔o➔c➔k➔e➔r➔ ➔C➔l➔i➔e➔n➔t➔ ➔—➔ ➔t➔h➔e➔ ➔C➔L➔I➔ ➔y➔o➔u➔ ➔u➔s➔e➔.➔ ➔d➔o➔c➔k➔e➔r➔ ➔b➔u➔i➔l➔d➔ ➔,➔ ➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔,➔ ➔d➔o➔c➔k➔e➔r➔ ➔p➔u➔s➔h➔ ➔ ➔e➔t➔c➔.➔ ➔S➔e➔n➔d➔s➔ ➔c➔o➔m➔m➔a➔n➔d➔s➔
➔t➔o➔ ➔t➔h➔e➔ ➔d➔a➔e➔m➔o➔n➔ ➔v➔i➔a➔ ➔R➔E➔S➔T➔ ➔A➔P➔I➔.➔
➔2➔.➔ ➔D➔o➔c➔k➔e➔r➔ ➔D➔a➔e➔m➔o➔n➔ ➔—➔ ➔b➔a➔c➔k➔g➔r➔o➔u➔n➔d➔ ➔s➔e➔r➔v➔i➔c➔e➔ ➔t➔h➔a➔t➔ ➔d➔o➔e➔s➔ ➔a➔l➔l➔ ➔t➔h➔e➔ ➔a➔c➔t➔u➔a➔l➔ ➔w➔o➔r➔k➔ ➔—➔ ➔b➔u➔i➔l➔d➔i➔n➔g➔ ➔i➔m➔a➔g➔e➔s➔,➔ ➔r➔u➔n➔n➔i➔n➔g➔
➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔,➔ ➔m➔a➔n➔a➔g➔i➔n➔g➔ ➔n➔e➔t➔w➔o➔r➔k➔i➔n➔g➔ ➔a➔n➔d➔ ➔s➔t➔o➔r➔a➔g➔e➔.➔
➔3➔.➔ ➔D➔o➔c➔k➔e➔r➔ ➔R➔e➔g➔i➔s➔t➔r➔y➔ ➔—➔ ➔s➔t➔o➔r➔e➔s➔ ➔i➔m➔a➔g➔e➔s➔.➔ ➔D➔o➔c➔k➔e➔r➔ ➔H➔u➔b➔ ➔(➔p➔u➔b➔l➔i➔c➔)➔,➔ ➔A➔m➔a➔z➔o➔n➔ ➔E➔C➔R➔,➔ ➔A➔z➔u➔r➔e➔ ➔A➔C➔R➔ ➔(➔p➔r➔i➔v➔a➔t➔e➔)➔.➔
➔W➔o➔r➔k➔f➔l➔o➔w➔:➔
➔
➔
➔
➔
➔Y➔o➔u➔ ➔w➔r➔i➔t➔e➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔
➔→➔ ➔d➔o➔c➔k➔e➔r➔ ➔b➔u➔i➔l➔d➔ ➔(➔c➔l➔i➔e➔n➔t➔ ➔s➔e➔n➔d➔s➔ ➔t➔o➔ ➔d➔a➔e➔m➔o➔n➔)➔
➔→➔ ➔d➔a➔e➔m➔o➔n➔ ➔b➔u➔i➔l➔d➔s➔ ➔i➔m➔a➔g➔e➔
➔→➔ ➔d➔o➔c➔k➔e➔r➔ ➔p➔u➔s➔h➔ ➔(➔p➔u➔s➔h➔ ➔t➔o➔ ➔r➔e➔g➔i➔s➔t➔r➔y➔)➔
➔→➔ ➔o➔t➔h➔e➔r➔s➔ ➔p➔u➔l➔l➔ ➔a➔n➔d➔ ➔r➔u➔n➔ ➔t➔h➔e➔ ➔i➔m➔a➔g➔e➔
➔Q➔1➔.➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔D➔o➔c➔k➔e➔r➔ ➔a➔n➔d➔ ➔w➔h➔y➔ ➔d➔o➔e➔s➔ ➔a➔ ➔D➔e➔v➔O➔p➔s➔ ➔e➔n➔g➔i➔n➔e➔e➔r➔ ➔u➔s➔e➔ ➔i➔t➔?➔
➔A➔n➔s➔w➔e➔r➔:➔
➔D➔o➔c➔k➔e➔r➔ ➔i➔s➔ ➔a➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔i➔z➔a➔t➔i➔o➔n➔ ➔p➔l➔a➔t➔f➔o➔r➔m➔ ➔t➔h➔a➔t➔ ➔p➔a➔c➔k➔a➔g➔e➔s➔ ➔y➔o➔u➔r➔ ➔a➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔,➔ ➔d➔e➔p➔e➔n➔d➔e➔n➔c➔i➔e➔s➔,➔ ➔a➔n➔d➔ ➔r➔u➔n➔t➔i➔m➔e➔ ➔i➔n➔t➔o➔ ➔a➔
➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔—➔ ➔a➔ ➔l➔i➔g➔h➔t➔w➔e➔i➔g➔h➔t➔,➔ ➔i➔s➔o➔l➔a➔t➔e➔d➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔.➔ ➔I➔n➔s➔t➔e➔a➔d➔ ➔o➔f➔ ➔s➔h➔i➔p➔p➔i➔n➔g➔ ➔y➔o➔u➔r➔ ➔w➔h➔o➔l➔e➔ ➔s➔e➔r➔v➔e➔r➔ ➔s➔e➔t➔u➔p➔,➔ ➔y➔o➔u➔ ➔s➔h➔i➔p➔ ➔a➔
➔D➔o➔c➔k➔e➔r➔ ➔i➔m➔a➔g➔e➔ ➔t➔h➔a➔t➔ ➔r➔u➔n➔s➔ ➔t➔h➔e➔ ➔s➔a➔m➔e➔ ➔e➔v➔e➔r➔y➔w➔h➔e➔r➔e➔ ➔—➔ ➔l➔a➔p➔t➔o➔p➔,➔ ➔s➔t➔a➔g➔i➔n➔g➔,➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔.➔
➔W➔h➔y➔ ➔b➔e➔t➔t➔e➔r➔ ➔t➔h➔a➔n➔ ➔V➔M➔s➔:➔
➔F➔e➔a➔t➔u➔r➔e➔ ➔V➔i➔r➔t➔u➔a➔l➔ ➔M➔a➔c➔h➔i➔n➔e➔ ➔D➔o➔c➔k➔e➔r➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔
➔O➔S➔ ➔F➔u➔l➔l➔ ➔O➔S➔ ➔p➔e➔r➔ ➔V➔M➔ ➔S➔h➔a➔r➔e➔s➔ ➔h➔o➔s➔t➔ ➔O➔S➔ ➔k➔e➔r➔n➔e➔l➔
➔S➔t➔a➔r➔t➔u➔p➔ ➔M➔i➔n➔u➔t➔e➔s➔ ➔S➔e➔c➔o➔n➔d➔s➔
➔S➔i➔z➔e➔ ➔G➔B➔s➔ ➔M➔B➔s➔
➔P➔o➔r➔t➔a➔b➔i➔l➔i➔t➔y➔ ➔L➔o➔w➔ ➔H➔i➔g➔h➔
➔P➔e➔r➔f➔o➔r➔m➔a➔n➔c➔e➔ ➔H➔e➔a➔v➔y➔ ➔L➔i➔g➔h➔t➔w➔e➔i➔g➔h➔t➔
➔K➔e➔y➔ ➔b➔e➔n➔e➔f➔i➔t➔:➔ ➔E➔l➔i➔m➔i➔n➔a➔t➔e➔s➔ ➔"➔w➔o➔r➔k➔s➔ ➔o➔n➔ ➔m➔y➔ ➔m➔a➔c➔h➔i➔n➔e➔"➔ ➔p➔r➔o➔b➔l➔e➔m➔.➔ ➔S➔a➔m➔e➔ ➔i➔m➔a➔g➔e➔ ➔r➔u➔n➔s➔ ➔i➔d➔e➔n➔t➔i➔c➔a➔l➔l➔y➔ ➔e➔v➔e➔r➔y➔w➔h➔e➔r➔e➔.➔
➔Q➔2➔.➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔t➔h➔e➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔c➔e➔ ➔b➔e➔t➔w➔e➔e➔n➔ ➔a➔ ➔D➔o➔c➔k➔e➔r➔ ➔I➔m➔a➔g➔e➔ ➔a➔n➔d➔ ➔a➔ ➔D➔o➔c➔k➔e➔r➔
➔C➔o➔n➔t➔a➔i➔n➔e➔r➔?➔
➔A➔n➔s➔w➔e➔r➔:➔
➔D➔o➔c➔k➔e➔r➔ ➔I➔m➔a➔g➔e➔ ➔—➔ ➔a➔ ➔r➔e➔a➔d➔-➔o➔n➔l➔y➔ ➔b➔l➔u➔e➔p➔r➔i➔n➔t➔/➔t➔e➔m➔p➔l➔a➔t➔e➔ ➔w➔i➔t➔h➔ ➔a➔l➔l➔ ➔t➔h➔e➔ ➔c➔o➔d➔e➔,➔ ➔d➔e➔p➔e➔n➔d➔e➔n➔c➔i➔e➔s➔,➔ ➔a➔n➔d➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔.➔ ➔B➔u➔i➔l➔t➔
➔f➔r➔o➔m➔ ➔a➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔.➔ ➔S➔t➔o➔r➔e➔d➔ ➔i➔n➔ ➔a➔ ➔r➔e➔g➔i➔s➔t➔r➔y➔.➔
➔D➔o➔c➔k➔e➔r➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔—➔ ➔a➔ ➔r➔u➔n➔n➔i➔n➔g➔ ➔i➔n➔s➔t➔a➔n➔c➔e➔ ➔o➔f➔ ➔a➔n➔ ➔i➔m➔a➔g➔e➔.➔ ➔T➔h➔e➔ ➔a➔c➔t➔u➔a➔l➔ ➔e➔x➔e➔c➔u➔t➔i➔n➔g➔ ➔p➔r➔o➔c➔e➔s➔s➔ ➔w➔i➔t➔h➔ ➔i➔t➔s➔ ➔o➔w➔n➔ ➔w➔r➔i➔t➔a➔b➔l➔e➔
➔l➔a➔y➔e➔r➔.➔
➔
➔
➔
➔
➔➔ ➔➔
➔E➔x➔a➔m➔p➔l➔e➔:➔
➔d➔o➔c➔k➔e➔r➔ ➔p➔u➔l➔l➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔u➔l➔l➔ ➔i➔m➔a➔g➔e➔ ➔f➔r➔o➔m➔ ➔D➔o➔c➔k➔e➔r➔ ➔H➔u➔b➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔p➔ ➔8➔0➔:➔8➔0➔ ➔-➔-➔n➔a➔m➔e➔ ➔m➔y➔n➔g➔i➔n➔x➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔a➔n➔d➔ ➔r➔u➔n➔ ➔a➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔f➔r➔o➔m➔ ➔i➔m➔a➔g➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔p➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔e➔ ➔r➔u➔n➔n➔i➔n➔g➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔
➔Y➔o➔u➔ ➔c➔a➔n➔ ➔r➔u➔n➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔f➔r➔o➔m➔ ➔o➔n➔e➔ ➔i➔m➔a➔g➔e➔ ➔—➔ ➔t➔h➔e➔y➔'➔r➔e➔ ➔a➔l➔l➔ ➔i➔s➔o➔l➔a➔t➔e➔d➔ ➔f➔r➔o➔m➔ ➔e➔a➔c➔h➔ ➔o➔t➔h➔e➔r➔.➔
➔Q➔3➔.➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔ ➔a➔n➔d➔ ➔w➔h➔a➔t➔ ➔a➔r➔e➔ ➔t➔h➔e➔ ➔k➔e➔y➔ ➔i➔n➔s➔t➔r➔u➔c➔t➔i➔o➔n➔s➔?➔
➔A➔n➔s➔w➔e➔r➔:➔
➔A➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔ ➔i➔s➔ ➔a➔ ➔t➔e➔x➔t➔ ➔f➔i➔l➔e➔ ➔w➔i➔t➔h➔ ➔i➔n➔s➔t➔r➔u➔c➔t➔i➔o➔n➔s➔ ➔t➔o➔ ➔b➔u➔i➔l➔d➔ ➔a➔ ➔D➔o➔c➔k➔e➔r➔ ➔i➔m➔a➔g➔e➔.➔
➔I➔n➔s➔t➔r➔u➔c➔t➔i➔o➔n➔ ➔P➔u➔r➔p➔o➔s➔e➔ ➔E➔x➔a➔m➔p➔l➔e➔
➔F➔R➔O➔M➔ ➔B➔a➔s➔e➔ ➔i➔m➔a➔g➔e➔ ➔t➔o➔ ➔s➔t➔a➔r➔t➔ ➔w➔i➔t➔h➔ ➔F➔R➔O➔M➔ ➔n➔o➔d➔e➔:➔1➔8➔-➔a➔l➔p➔i➔n➔e➔
➔R➔U➔N➔ ➔E➔x➔e➔c➔u➔t➔e➔ ➔c➔o➔m➔m➔a➔n➔d➔s➔ ➔d➔u➔r➔i➔n➔g➔ ➔b➔u➔i➔l➔d➔ ➔R➔U➔N➔ ➔n➔p➔m➔ ➔i➔n➔s➔t➔a➔l➔l➔
➔C➔O➔P➔Y➔ ➔C➔o➔p➔y➔ ➔f➔i➔l➔e➔s➔ ➔f➔r➔o➔m➔ ➔h➔o➔s➔t➔ ➔i➔n➔t➔o➔ ➔i➔m➔a➔g➔e➔ ➔C➔O➔P➔Y➔ ➔.➔ ➔/➔a➔p➔p➔
➔W➔O➔R➔K➔D➔I➔R➔ ➔S➔e➔t➔ ➔w➔o➔r➔k➔i➔n➔g➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔W➔O➔R➔K➔D➔I➔R➔ ➔/➔a➔p➔p➔
➔E➔X➔P➔O➔S➔E➔ ➔D➔e➔c➔l➔a➔r➔e➔ ➔p➔o➔r➔t➔ ➔t➔h➔e➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔l➔i➔s➔t➔e➔n➔s➔ ➔o➔n➔ ➔E➔X➔P➔O➔S➔E➔ ➔3➔0➔0➔0➔
➔C➔M➔D➔ ➔D➔e➔f➔a➔u➔l➔t➔ ➔c➔o➔m➔m➔a➔n➔d➔ ➔w➔h➔e➔n➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔s➔t➔a➔r➔t➔s➔ ➔C➔M➔D➔ ➔[➔"➔n➔o➔d➔e➔"➔,➔ ➔"➔a➔p➔p➔.➔j➔s➔"➔]➔
➔E➔N➔V➔ ➔S➔e➔t➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔ ➔E➔N➔V➔ ➔N➔O➔D➔E➔_➔E➔N➔V➔=➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔U➔S➔E➔R➔ ➔S➔e➔t➔ ➔n➔o➔n➔-➔r➔o➔o➔t➔ ➔u➔s➔e➔r➔ ➔f➔o➔r➔ ➔s➔e➔c➔u➔r➔i➔t➔y➔ ➔U➔S➔E➔R➔ ➔n➔o➔d➔e➔
➔E➔x➔a➔m➔p➔l➔e➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔ ➔f➔o➔r➔ ➔a➔ ➔N➔o➔d➔e➔.➔j➔s➔ ➔a➔p➔p➔:➔
➔F➔R➔O➔M➔ ➔n➔o➔d➔e➔:➔1➔8➔-➔a➔l➔p➔i➔n➔e➔
➔W➔O➔R➔K➔D➔I➔R➔ ➔/➔a➔p➔p➔
➔C➔O➔P➔Y➔ ➔p➔a➔c➔k➔a➔g➔e➔*➔.➔j➔s➔o➔n➔ ➔.➔/➔
➔R➔U➔N➔ ➔n➔p➔m➔ ➔i➔n➔s➔t➔a➔l➔l➔
➔C➔O➔P➔Y➔ ➔.➔ ➔.➔
➔E➔X➔P➔O➔S➔E➔ ➔3➔0➔0➔0➔
➔
➔
➔
➔
➔U➔S➔E➔R➔ ➔n➔o➔d➔e➔
➔C➔M➔D➔ ➔[➔"➔n➔o➔d➔e➔"➔,➔ ➔"➔a➔p➔p➔.➔j➔s➔"➔]➔
➔Q➔4➔.➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔t➔h➔e➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔c➔e➔ ➔b➔e➔t➔w➔e➔e➔n➔ ➔C➔O➔P➔Y➔ ➔a➔n➔d➔ ➔A➔D➔D➔?➔
➔A➔n➔s➔w➔e➔r➔:➔
➔C➔O➔P➔Y➔ ➔—➔ ➔s➔i➔m➔p➔l➔y➔ ➔c➔o➔p➔i➔e➔s➔ ➔f➔i➔l➔e➔s➔ ➔f➔r➔o➔m➔ ➔h➔o➔s➔t➔ ➔i➔n➔t➔o➔ ➔t➔h➔e➔ ➔i➔m➔a➔g➔e➔.➔ ➔N➔o➔t➔h➔i➔n➔g➔ ➔e➔x➔t➔r➔a➔.➔ ➔P➔r➔e➔f➔e➔r➔r➔e➔d➔.➔
➔A➔D➔D➔ ➔—➔ ➔d➔o➔e➔s➔ ➔e➔v➔e➔r➔y➔t➔h➔i➔n➔g➔ ➔C➔O➔P➔Y➔ ➔d➔o➔e➔s➔,➔ ➔p➔l➔u➔s➔ ➔e➔x➔t➔r➔a➔c➔t➔s➔ ➔t➔a➔r➔ ➔f➔i➔l➔e➔s➔ ➔a➔u➔t➔o➔m➔a➔t➔i➔c➔a➔l➔l➔y➔ ➔a➔n➔d➔ ➔c➔a➔n➔ ➔f➔e➔t➔c➔h➔ ➔f➔r➔o➔m➔ ➔U➔R➔L➔s➔.➔
➔B➔e➔s➔t➔ ➔p➔r➔a➔c➔t➔i➔c➔e➔:➔ ➔A➔l➔w➔a➔y➔s➔ ➔u➔s➔e➔ ➔C➔O➔P➔Y➔.➔ ➔U➔s➔e➔ ➔A➔D➔D➔ ➔o➔n➔l➔y➔ ➔w➔h➔e➔n➔ ➔y➔o➔u➔ ➔n➔e➔e➔d➔ ➔t➔a➔r➔ ➔e➔x➔t➔r➔a➔c➔t➔i➔o➔n➔.➔
➔C➔O➔P➔Y➔ ➔.➔/➔a➔p➔p➔ ➔/➔a➔p➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔r➔e➔f➔e➔r➔r➔e➔d➔ ➔-➔ ➔s➔i➔m➔p➔l➔e➔ ➔a➔n➔d➔ ➔p➔r➔e➔d➔i➔c➔t➔a➔b➔l➔e➔
➔A➔D➔D➔ ➔a➔r➔c➔h➔i➔v➔e➔.➔t➔a➔r➔.➔g➔z➔ ➔/➔a➔p➔p➔ ➔ ➔#➔ ➔u➔s➔e➔ ➔o➔n➔l➔y➔ ➔w➔h➔e➔n➔ ➔y➔o➔u➔ ➔n➔e➔e➔d➔ ➔a➔u➔t➔o➔-➔e➔x➔t➔r➔a➔c➔t➔i➔o➔n➔
➔Q➔5➔.➔ ➔W➔h➔a➔t➔ ➔a➔r➔e➔ ➔D➔o➔c➔k➔e➔r➔ ➔L➔a➔y➔e➔r➔s➔ ➔a➔n➔d➔ ➔w➔h➔y➔ ➔d➔o➔ ➔t➔h➔e➔y➔ ➔m➔a➔t➔t➔e➔r➔?➔
➔A➔n➔s➔w➔e➔r➔:➔
➔E➔a➔c➔h➔ ➔i➔n➔s➔t➔r➔u➔c➔t➔i➔o➔n➔ ➔i➔n➔ ➔a➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔ ➔c➔r➔e➔a➔t➔e➔s➔ ➔a➔ ➔r➔e➔a➔d➔-➔o➔n➔l➔y➔ ➔l➔a➔y➔e➔r➔.➔ ➔L➔a➔y➔e➔r➔s➔ ➔s➔t➔a➔c➔k➔ ➔o➔n➔ ➔t➔o➔p➔ ➔o➔f➔ ➔e➔a➔c➔h➔ ➔o➔t➔h➔e➔r➔ ➔t➔o➔ ➔f➔o➔r➔m➔ ➔t➔h➔e➔ ➔f➔i➔n➔a➔l➔
➔i➔m➔a➔g➔e➔.➔
➔H➔o➔w➔ ➔c➔a➔c➔h➔i➔n➔g➔ ➔w➔o➔r➔k➔s➔:➔
➔F➔R➔O➔M➔ ➔n➔o➔d➔e➔:➔1➔8➔-➔a➔l➔p➔i➔n➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔L➔a➔y➔e➔r➔ ➔1➔ ➔—➔ ➔c➔a➔c➔h➔e➔d➔ ➔u➔n➔l➔e➔s➔s➔ ➔b➔a➔s➔e➔ ➔i➔m➔a➔g➔e➔ ➔c➔h➔a➔n➔g➔e➔s➔
➔W➔O➔R➔K➔D➔I➔R➔ ➔/➔a➔p➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔L➔a➔y➔e➔r➔ ➔2➔ ➔—➔ ➔c➔a➔c➔h➔e➔d➔
➔C➔O➔P➔Y➔ ➔p➔a➔c➔k➔a➔g➔e➔*➔.➔j➔s➔o➔n➔ ➔.➔/➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔L➔a➔y➔e➔r➔ ➔3➔ ➔—➔ ➔c➔a➔c➔h➔e➔d➔ ➔u➔n➔l➔e➔s➔s➔ ➔p➔a➔c➔k➔a➔g➔e➔.➔j➔s➔o➔n➔ ➔c➔h➔a➔n➔g➔e➔s➔
➔R➔U➔N➔ ➔n➔p➔m➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔L➔a➔y➔e➔r➔ ➔4➔ ➔—➔ ➔c➔a➔c➔h➔e➔d➔ ➔u➔n➔l➔e➔s➔s➔ ➔l➔a➔y➔e➔r➔ ➔3➔ ➔c➔h➔a➔n➔g➔e➔s➔
➔C➔O➔P➔Y➔ ➔.➔ ➔.➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔L➔a➔y➔e➔r➔ ➔5➔ ➔—➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔e➔v➔e➔r➔y➔ ➔t➔i➔m➔e➔ ➔c➔o➔d➔e➔ ➔c➔h➔a➔n➔g➔e➔s➔
➔C➔M➔D➔ ➔[➔"➔n➔o➔d➔e➔"➔,➔ ➔"➔a➔p➔p➔.➔j➔s➔"➔]➔ ➔ ➔ ➔ ➔ ➔#➔ ➔L➔a➔y➔e➔r➔ ➔6➔
➔O➔p➔t➔i➔m➔i➔z➔a➔t➔i➔o➔n➔ ➔t➔i➔p➔:➔ ➔P➔u➔t➔ ➔r➔a➔r➔e➔l➔y➔ ➔c➔h➔a➔n➔g➔i➔n➔g➔ ➔i➔n➔s➔t➔r➔u➔c➔t➔i➔o➔n➔s➔ ➔a➔t➔ ➔t➔o➔p➔,➔ ➔f➔r➔e➔q➔u➔e➔n➔t➔l➔y➔ ➔c➔h➔a➔n➔g➔i➔n➔g➔ ➔a➔t➔ ➔b➔o➔t➔t➔o➔m➔.➔ ➔T➔h➔i➔s➔ ➔w➔a➔y➔ ➔n➔p➔m➔
➔i➔n➔s➔t➔a➔l➔l➔ ➔ ➔i➔s➔ ➔c➔a➔c➔h➔e➔d➔ ➔a➔n➔d➔ ➔d➔o➔e➔s➔n➔'➔t➔ ➔r➔e➔-➔r➔u➔n➔ ➔e➔v➔e➔r➔y➔ ➔t➔i➔m➔e➔ ➔y➔o➔u➔ ➔c➔h➔a➔n➔g➔e➔ ➔y➔o➔u➔r➔ ➔c➔o➔d➔e➔.➔
➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔w➔r➔i➔t➔a➔b➔l➔e➔ ➔l➔a➔y➔e➔r➔:➔ ➔W➔h➔e➔n➔ ➔y➔o➔u➔ ➔r➔u➔n➔ ➔a➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔,➔ ➔D➔o➔c➔k➔e➔r➔ ➔a➔d➔d➔s➔ ➔a➔ ➔w➔r➔i➔t➔a➔b➔l➔e➔ ➔l➔a➔y➔e➔r➔ ➔o➔n➔ ➔t➔o➔p➔.➔ ➔M➔u➔l➔t➔i➔p➔l➔e➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔
➔f➔r➔o➔m➔ ➔o➔n➔e➔ ➔i➔m➔a➔g➔e➔ ➔e➔a➔c➔h➔ ➔g➔e➔t➔ ➔t➔h➔e➔i➔r➔ ➔o➔w➔n➔ ➔w➔r➔i➔t➔a➔b➔l➔e➔ ➔l➔a➔y➔e➔r➔.➔
➔
➔
➔
➔
➔Q➔6➔.➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔t➔h➔e➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔c➔e➔ ➔b➔e➔t➔w➔e➔e➔n➔ ➔R➔U➔N➔,➔ ➔C➔M➔D➔,➔ ➔a➔n➔d➔ ➔E➔N➔T➔R➔Y➔P➔O➔I➔N➔T➔?➔
➔A➔n➔s➔w➔e➔r➔:➔
➔I➔n➔s➔t➔r➔u➔c➔t➔i➔o➔n➔ ➔W➔h➔e➔n➔ ➔i➔t➔ ➔r➔u➔n➔s➔ ➔C➔a➔n➔ ➔b➔e➔ ➔o➔v➔e➔r➔r➔i➔d➔d➔e➔n➔?➔ ➔U➔s➔e➔ ➔f➔o➔r➔
➔R➔U➔N➔ ➔B➔u➔i➔l➔d➔ ➔t➔i➔m➔e➔ ➔N➔/➔A➔ ➔I➔n➔s➔t➔a➔l➔l➔i➔n➔g➔ ➔p➔a➔c➔k➔a➔g➔e➔s➔
➔C➔M➔D➔ ➔R➔u➔n➔t➔i➔m➔e➔ ➔(➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔s➔t➔a➔r➔t➔)➔ ➔Y➔e➔s➔,➔ ➔e➔a➔s➔i➔l➔y➔ ➔D➔e➔f➔a➔u➔l➔t➔ ➔a➔r➔g➔u➔m➔e➔n➔t➔s➔
➔E➔N➔T➔R➔Y➔P➔O➔I➔N➔T➔ ➔R➔u➔n➔t➔i➔m➔e➔ ➔(➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔s➔t➔a➔r➔t➔)➔ ➔O➔n➔l➔y➔ ➔w➔i➔t➔h➔ ➔-➔-➔e➔n➔t➔r➔y➔p➔o➔i➔n➔t➔ ➔f➔l➔a➔g➔ ➔M➔a➔i➔n➔ ➔e➔x➔e➔c➔u➔t➔a➔b➔l➔e➔
➔E➔x➔a➔m➔p➔l➔e➔:➔
➔R➔U➔N➔ ➔a➔p➔t➔-➔g➔e➔t➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔-➔y➔ ➔c➔u➔r➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔u➔n➔s➔ ➔d➔u➔r➔i➔n➔g➔ ➔b➔u➔i➔l➔d➔,➔ ➔i➔n➔s➔t➔a➔l➔l➔s➔ ➔c➔u➔r➔l➔
➔E➔N➔T➔R➔Y➔P➔O➔I➔N➔T➔ ➔[➔"➔p➔y➔t➔h➔o➔n➔3➔"➔,➔ ➔"➔a➔p➔p➔.➔p➔y➔"➔]➔ ➔ ➔ ➔#➔ ➔a➔l➔w➔a➔y➔s➔ ➔r➔u➔n➔s➔ ➔p➔y➔t➔h➔o➔n➔3➔ ➔a➔p➔p➔.➔p➔y➔
➔C➔M➔D➔ ➔[➔"➔-➔-➔d➔e➔b➔u➔g➔"➔]➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔f➔a➔u➔l➔t➔ ➔a➔r➔g➔u➔m➔e➔n➔t➔,➔ ➔c➔a➔n➔ ➔b➔e➔ ➔o➔v➔e➔r➔r➔i➔d➔d➔e➔n➔
➔#➔ ➔R➔u➔n➔n➔i➔n➔g➔:➔ ➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔m➔y➔i➔m➔a➔g➔e➔ ➔-➔-➔p➔r➔o➔d➔
➔#➔ ➔R➔e➔s➔u➔l➔t➔:➔ ➔p➔y➔t➔h➔o➔n➔3➔ ➔a➔p➔p➔.➔p➔y➔ ➔-➔-➔p➔r➔o➔d➔ ➔ ➔ ➔(➔C➔M➔D➔ ➔o➔v➔e➔r➔r➔i➔d➔d➔e➔n➔,➔ ➔E➔N➔T➔R➔Y➔P➔O➔I➔N➔T➔ ➔s➔t➔a➔y➔s➔)➔
➔Q➔7➔.➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔D➔o➔c➔k➔e➔r➔ ➔C➔o➔m➔p➔o➔s➔e➔?➔
➔A➔n➔s➔w➔e➔r➔:➔
➔D➔o➔c➔k➔e➔r➔ ➔C➔o➔m➔p➔o➔s➔e➔ ➔l➔e➔t➔s➔ ➔y➔o➔u➔ ➔d➔e➔f➔i➔n➔e➔ ➔a➔n➔d➔ ➔r➔u➔n➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔t➔o➔g➔e➔t➔h➔e➔r➔ ➔a➔s➔ ➔a➔ ➔s➔i➔n➔g➔l➔e➔ ➔a➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔ ➔u➔s➔i➔n➔g➔ ➔a➔ ➔d➔o➔c➔k➔e➔r➔-➔
➔c➔o➔m➔p➔o➔s➔e➔.➔y➔m➔l➔ ➔ ➔f➔i➔l➔e➔.➔
➔E➔x➔a➔m➔p➔l➔e➔ ➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔.➔y➔m➔l➔ ➔(➔F➔r➔o➔n➔t➔e➔n➔d➔ ➔+➔ ➔B➔a➔c➔k➔e➔n➔d➔ ➔+➔ ➔D➔a➔t➔a➔b➔a➔s➔e➔)➔:➔
➔v➔e➔r➔s➔i➔o➔n➔:➔ ➔'➔3➔.➔8➔'➔
➔s➔e➔r➔v➔i➔c➔e➔s➔:➔
➔ ➔ ➔f➔r➔o➔n➔t➔e➔n➔d➔:➔
➔ ➔ ➔ ➔ ➔b➔u➔i➔l➔d➔:➔ ➔.➔/➔f➔r➔o➔n➔t➔e➔n➔d➔
➔ ➔ ➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔"➔8➔0➔:➔8➔0➔"➔
➔ ➔ ➔ ➔ ➔d➔e➔p➔e➔n➔d➔s➔_➔o➔n➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔b➔a➔c➔k➔e➔n➔d➔
➔ ➔ ➔b➔a➔c➔k➔e➔n➔d➔:➔
➔ ➔ ➔ ➔ ➔b➔u➔i➔l➔d➔:➔ ➔.➔/➔b➔a➔c➔k➔e➔n➔d➔
➔ ➔ ➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔
➔
➔
➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔"➔3➔0➔0➔0➔:➔3➔0➔0➔0➔"➔
➔ ➔ ➔ ➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔D➔B➔_➔H➔O➔S➔T➔=➔d➔a➔t➔a➔b➔a➔s➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔D➔B➔_➔P➔O➔R➔T➔=➔5➔4➔3➔2➔
➔ ➔ ➔ ➔ ➔d➔e➔p➔e➔n➔d➔s➔_➔o➔n➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔d➔a➔t➔a➔b➔a➔s➔e➔
➔ ➔ ➔d➔a➔t➔a➔b➔a➔s➔e➔:➔
➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔p➔o➔s➔t➔g➔r➔e➔s➔:➔1➔4➔
➔ ➔ ➔ ➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔P➔O➔S➔T➔G➔R➔E➔S➔_➔D➔B➔=➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔P➔O➔S➔T➔G➔R➔E➔S➔_➔P➔A➔S➔S➔W➔O➔R➔D➔=➔s➔e➔c➔r➔e➔t➔
➔ ➔ ➔ ➔ ➔v➔o➔l➔u➔m➔e➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔d➔b➔-➔d➔a➔t➔a➔:➔/➔v➔a➔r➔/➔l➔i➔b➔/➔p➔o➔s➔t➔g➔r➔e➔s➔q➔l➔/➔d➔a➔t➔a➔
➔v➔o➔l➔u➔m➔e➔s➔:➔
➔ ➔ ➔d➔b➔-➔d➔a➔t➔a➔:➔
➔K➔e➔y➔ ➔c➔o➔m➔m➔a➔n➔d➔s➔:➔
➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔ ➔u➔p➔ ➔-➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔t➔a➔r➔t➔ ➔a➔l➔l➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔i➔n➔ ➔b➔a➔c➔k➔g➔r➔o➔u➔n➔d➔
➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔ ➔d➔o➔w➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔t➔o➔p➔ ➔a➔n➔d➔ ➔r➔e➔m➔o➔v➔e➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔
➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔ ➔l➔o➔g➔s➔ ➔-➔f➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔l➔l➔o➔w➔ ➔l➔o➔g➔s➔ ➔o➔f➔ ➔a➔l➔l➔ ➔s➔e➔r➔v➔i➔c➔e➔s➔
➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔ ➔p➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔r➔u➔n➔n➔i➔n➔g➔ ➔s➔e➔r➔v➔i➔c➔e➔s➔
➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔ ➔b➔u➔i➔l➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔b➔u➔i➔l➔d➔ ➔i➔m➔a➔g➔e➔s➔
➔U➔s➔e➔ ➔c➔a➔s➔e➔:➔ ➔P➔e➔r➔f➔e➔c➔t➔ ➔f➔o➔r➔ ➔l➔o➔c➔a➔l➔ ➔d➔e➔v➔e➔l➔o➔p➔m➔e➔n➔t➔.➔ ➔I➔n➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔,➔ ➔u➔s➔e➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔.➔
➔Q➔8➔.➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔D➔o➔c➔k➔e➔r➔ ➔N➔e➔t➔w➔o➔r➔k➔i➔n➔g➔?➔
➔A➔n➔s➔w➔e➔r➔:➔
➔D➔o➔c➔k➔e➔r➔ ➔n➔e➔t➔w➔o➔r➔k➔i➔n➔g➔ ➔c➔o➔n➔t➔r➔o➔l➔s➔ ➔h➔o➔w➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔c➔o➔m➔m➔u➔n➔i➔c➔a➔t➔e➔ ➔w➔i➔t➔h➔ ➔e➔a➔c➔h➔ ➔o➔t➔h➔e➔r➔ ➔a➔n➔d➔ ➔t➔h➔e➔ ➔o➔u➔t➔s➔i➔d➔e➔ ➔w➔o➔r➔l➔d➔.➔
➔N➔e➔t➔w➔o➔r➔k➔ ➔T➔y➔p➔e➔ ➔D➔e➔s➔c➔r➔i➔p➔t➔i➔o➔n➔ ➔U➔s➔e➔ ➔c➔a➔s➔e➔
➔B➔r➔i➔d➔g➔e➔ ➔D➔e➔f➔a➔u➔l➔t➔.➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔o➔n➔ ➔s➔a➔m➔e➔ ➔b➔r➔i➔d➔g➔e➔ ➔c➔a➔n➔ ➔t➔a➔l➔k➔ ➔t➔o➔ ➔e➔a➔c➔h➔ ➔o➔t➔h➔e➔r➔ ➔M➔o➔s➔t➔ ➔c➔o➔m➔m➔o➔n➔,➔ ➔s➔i➔n➔g➔l➔e➔ ➔h➔o➔s➔t➔
➔H➔o➔s➔t➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔u➔s➔e➔s➔ ➔h➔o➔s➔t➔ ➔m➔a➔c➔h➔i➔n➔e➔'➔s➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔d➔i➔r➔e➔c➔t➔l➔y➔ ➔H➔i➔g➔h➔ ➔p➔e➔r➔f➔o➔r➔m➔a➔n➔c➔e➔,➔ ➔n➔o➔ ➔i➔s➔o➔l➔a➔t➔i➔o➔n➔
➔O➔v➔e➔r➔l➔a➔y➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔a➔c➔r➔o➔s➔s➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔t➔ ➔m➔a➔c➔h➔i➔n➔e➔s➔ ➔c➔o➔m➔m➔u➔n➔i➔c➔a➔t➔e➔ ➔D➔o➔c➔k➔e➔r➔ ➔S➔w➔a➔r➔m➔,➔ ➔m➔u➔l➔t➔i➔-➔h➔o➔s➔t➔
➔N➔o➔n➔e➔ ➔N➔o➔ ➔n➔e➔t➔w➔o➔r➔k➔i➔n➔g➔ ➔C➔o➔m➔p➔l➔e➔t➔e➔ ➔i➔s➔o➔l➔a➔t➔i➔o➔n➔
➔
➔
➔
➔
➔C➔o➔m➔m➔a➔n➔d➔s➔:➔
➔d➔o➔c➔k➔e➔r➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔l➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔n➔e➔t➔w➔o➔r➔k➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔c➔r➔e➔a➔t➔e➔ ➔m➔y➔n➔e➔t➔w➔o➔r➔k➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔c➔u➔s➔t➔o➔m➔ ➔b➔r➔i➔d➔g➔e➔ ➔n➔e➔t➔w➔o➔r➔k➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔-➔n➔e➔t➔w➔o➔r➔k➔ ➔m➔y➔n➔e➔t➔w➔o➔r➔k➔ ➔m➔y➔a➔p➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔u➔n➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔o➔n➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔n➔e➔t➔w➔o➔r➔k➔
➔d➔o➔c➔k➔e➔r➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔i➔n➔s➔p➔e➔c➔t➔ ➔m➔y➔n➔e➔t➔w➔o➔r➔k➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔i➔n➔s➔p➔e➔c➔t➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔d➔e➔t➔a➔i➔l➔s➔
➔E➔x➔a➔m➔p➔l➔e➔:➔ ➔T➔w➔o➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔o➔n➔ ➔s➔a➔m➔e➔ ➔b➔r➔i➔d➔g➔e➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔c➔a➔n➔ ➔c➔o➔m➔m➔u➔n➔i➔c➔a➔t➔e➔ ➔b➔y➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔n➔a➔m➔e➔:➔
➔#➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔1➔:➔ ➔b➔a➔c➔k➔e➔n➔d➔
➔#➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔2➔:➔ ➔d➔a➔t➔a➔b➔a➔s➔e➔
➔#➔ ➔b➔a➔c➔k➔e➔n➔d➔ ➔c➔a➔n➔ ➔r➔e➔a➔c➔h➔ ➔d➔a➔t➔a➔b➔a➔s➔e➔ ➔u➔s➔i➔n➔g➔:➔ ➔p➔o➔s➔t➔g➔r➔e➔s➔:➔/➔/➔d➔a➔t➔a➔b➔a➔s➔e➔:➔5➔4➔3➔2➔
➔Q➔9➔.➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔ ➔D➔o➔c➔k➔e➔r➔ ➔V➔o➔l➔u➔m➔e➔?➔
➔A➔n➔s➔w➔e➔r➔:➔
➔A➔ ➔D➔o➔c➔k➔e➔r➔ ➔v➔o➔l➔u➔m➔e➔ ➔i➔s➔ ➔p➔e➔r➔s➔i➔s➔t➔e➔n➔t➔ ➔s➔t➔o➔r➔a➔g➔e➔ ➔t➔h➔a➔t➔ ➔s➔u➔r➔v➔i➔v➔e➔s➔ ➔e➔v➔e➔n➔ ➔a➔f➔t➔e➔r➔ ➔a➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔i➔s➔ ➔d➔e➔l➔e➔t➔e➔d➔.➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔a➔r➔e➔ ➔e➔p➔h➔e➔m➔e➔r➔a➔l➔
➔—➔ ➔w➔h➔e➔n➔ ➔t➔h➔e➔y➔ ➔s➔t➔o➔p➔,➔ ➔d➔a➔t➔a➔ ➔i➔n➔s➔i➔d➔e➔ ➔i➔s➔ ➔l➔o➔s➔t➔.➔ ➔V➔o➔l➔u➔m➔e➔s➔ ➔s➔t➔o➔r➔e➔ ➔d➔a➔t➔a➔ ➔o➔u➔t➔s➔i➔d➔e➔ ➔t➔h➔e➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔.➔
➔T➔y➔p➔e➔s➔:➔
➔N➔a➔m➔e➔d➔ ➔V➔o➔l➔u➔m➔e➔ ➔—➔ ➔m➔a➔n➔a➔g➔e➔d➔ ➔b➔y➔ ➔D➔o➔c➔k➔e➔r➔,➔ ➔s➔t➔o➔r➔e➔d➔ ➔i➔n➔ ➔D➔o➔c➔k➔e➔r➔'➔s➔ ➔m➔a➔n➔a➔g➔e➔d➔ ➔l➔o➔c➔a➔t➔i➔o➔n➔.➔ ➔B➔e➔s➔t➔ ➔f➔o➔r➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔.➔
➔B➔i➔n➔d➔ ➔M➔o➔u➔n➔t➔ ➔—➔ ➔m➔o➔u➔n➔t➔s➔ ➔a➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔h➔o➔s➔t➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔i➔n➔t➔o➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔.➔ ➔G➔o➔o➔d➔ ➔f➔o➔r➔ ➔d➔e➔v➔e➔l➔o➔p➔m➔e➔n➔t➔.➔
➔C➔o➔m➔m➔a➔n➔d➔s➔:➔
➔d➔o➔c➔k➔e➔r➔ ➔v➔o➔l➔u➔m➔e➔ ➔c➔r➔e➔a➔t➔e➔ ➔m➔y➔v➔o➔l➔u➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔n➔a➔m➔e➔d➔ ➔v➔o➔l➔u➔m➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔v➔o➔l➔u➔m➔e➔ ➔l➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔v➔o➔l➔u➔m➔e➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔v➔o➔l➔u➔m➔e➔ ➔i➔n➔s➔p➔e➔c➔t➔ ➔m➔y➔v➔o➔l➔u➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔i➔n➔s➔p➔e➔c➔t➔ ➔v➔o➔l➔u➔m➔e➔ ➔d➔e➔t➔a➔i➔l➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔v➔o➔l➔u➔m➔e➔ ➔r➔m➔ ➔m➔y➔v➔o➔l➔u➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔v➔o➔l➔u➔m➔e➔
➔#➔ ➔R➔u➔n➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔w➔i➔t➔h➔ ➔v➔o➔l➔u➔m➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔v➔ ➔m➔y➔v➔o➔l➔u➔m➔e➔:➔/➔v➔a➔r➔/➔l➔i➔b➔/➔p➔o➔s➔t➔g➔r➔e➔s➔q➔l➔/➔d➔a➔t➔a➔ ➔p➔o➔s➔t➔g➔r➔e➔s➔ ➔ ➔ ➔#➔ ➔n➔a➔m➔e➔d➔ ➔v➔o➔l➔u➔m➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔v➔ ➔/➔h➔o➔m➔e➔/➔a➔k➔h➔i➔l➔/➔a➔p➔p➔:➔/➔a➔p➔p➔ ➔m➔y➔a➔p➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔b➔i➔n➔d➔ ➔m➔o➔u➔n➔t➔
➔E➔x➔a➔m➔p➔l➔e➔:➔ ➔P➔o➔s➔t➔g➔r➔e➔S➔Q➔L➔ ➔d➔a➔t➔a➔b➔a➔s➔e➔ ➔w➔i➔t➔h➔ ➔p➔e➔r➔s➔i➔s➔t➔e➔n➔t➔ ➔v➔o➔l➔u➔m➔e➔:➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔\➔
➔ ➔ ➔-➔-➔n➔a➔m➔e➔ ➔p➔o➔s➔t➔g➔r➔e➔s➔ ➔\➔
➔ ➔ ➔-➔e➔ ➔P➔O➔S➔T➔G➔R➔E➔S➔_➔P➔A➔S➔S➔W➔O➔R➔D➔=➔s➔e➔c➔r➔e➔t➔ ➔\➔
➔ ➔ ➔-➔v➔ ➔p➔g➔d➔a➔t➔a➔:➔/➔v➔a➔r➔/➔l➔i➔b➔/➔p➔o➔s➔t➔g➔r➔e➔s➔q➔l➔/➔d➔a➔t➔a➔ ➔\➔
➔
➔
➔
➔
➔ ➔ ➔p➔o➔s➔t➔g➔r➔e➔s➔:➔1➔4➔
➔#➔ ➔E➔v➔e➔n➔ ➔i➔f➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔i➔s➔ ➔d➔e➔l➔e➔t➔e➔d➔,➔ ➔d➔a➔t➔a➔ ➔i➔n➔ ➔p➔g➔d➔a➔t➔a➔ ➔v➔o➔l➔u➔m➔e➔ ➔r➔e➔m➔a➔i➔n➔s➔
➔Q➔1➔0➔.➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔ ➔D➔o➔c➔k➔e➔r➔ ➔R➔e➔g➔i➔s➔t➔r➔y➔ ➔a➔n➔d➔ ➔t➔y➔p➔e➔s➔?➔
➔A➔n➔s➔w➔e➔r➔:➔
➔A➔ ➔D➔o➔c➔k➔e➔r➔ ➔r➔e➔g➔i➔s➔t➔r➔y➔ ➔i➔s➔ ➔a➔ ➔c➔e➔n➔t➔r➔a➔l➔i➔z➔e➔d➔ ➔r➔e➔p➔o➔s➔i➔t➔o➔r➔y➔ ➔t➔o➔ ➔s➔t➔o➔r➔e➔ ➔a➔n➔d➔ ➔m➔a➔n➔a➔g➔e➔ ➔D➔o➔c➔k➔e➔r➔ ➔i➔m➔a➔g➔e➔s➔.➔
➔R➔e➔g➔i➔s➔t➔r➔y➔ ➔T➔y➔p➔e➔ ➔U➔s➔e➔ ➔c➔a➔s➔e➔
➔D➔o➔c➔k➔e➔r➔ ➔H➔u➔b➔ ➔P➔u➔b➔l➔i➔c➔ ➔O➔p➔e➔n➔ ➔s➔o➔u➔r➔c➔e➔ ➔p➔r➔o➔j➔e➔c➔t➔s➔,➔ ➔b➔a➔s➔e➔ ➔i➔m➔a➔g➔e➔s➔
➔A➔m➔a➔z➔o➔n➔ ➔E➔C➔R➔ ➔P➔r➔i➔v➔a➔t➔e➔ ➔A➔W➔S➔-➔b➔a➔s➔e➔d➔ ➔p➔r➔o➔j➔e➔c➔t➔s➔
➔A➔z➔u➔r➔e➔ ➔A➔C➔R➔ ➔P➔r➔i➔v➔a➔t➔e➔ ➔A➔z➔u➔r➔e➔-➔b➔a➔s➔e➔d➔ ➔p➔r➔o➔j➔e➔c➔t➔s➔
➔H➔a➔r➔b➔o➔r➔ ➔S➔e➔l➔f➔-➔h➔o➔s➔t➔e➔d➔ ➔O➔n➔-➔p➔r➔e➔m➔i➔s➔e➔ ➔e➔n➔t➔e➔r➔p➔r➔i➔s➔e➔
➔C➔o➔m➔m➔a➔n➔d➔s➔:➔
➔d➔o➔c➔k➔e➔r➔ ➔l➔o➔g➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔o➔g➔i➔n➔ ➔t➔o➔ ➔D➔o➔c➔k➔e➔r➔ ➔H➔u➔b➔
➔d➔o➔c➔k➔e➔r➔ ➔l➔o➔g➔i➔n➔ ➔<➔r➔e➔g➔i➔s➔t➔r➔y➔-➔u➔r➔l➔>➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔o➔g➔i➔n➔ ➔t➔o➔ ➔p➔r➔i➔v➔a➔t➔e➔ ➔r➔e➔g➔i➔s➔t➔r➔y➔
➔d➔o➔c➔k➔e➔r➔ ➔t➔a➔g➔ ➔m➔y➔a➔p➔p➔:➔1➔.➔0➔ ➔m➔y➔r➔e➔p➔o➔/➔m➔y➔a➔p➔p➔:➔1➔.➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔t➔a➔g➔ ➔i➔m➔a➔g➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔p➔u➔s➔h➔ ➔m➔y➔r➔e➔p➔o➔/➔m➔y➔a➔p➔p➔:➔1➔.➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔u➔s➔h➔ ➔t➔o➔ ➔r➔e➔g➔i➔s➔t➔r➔y➔
➔d➔o➔c➔k➔e➔r➔ ➔p➔u➔l➔l➔ ➔m➔y➔r➔e➔p➔o➔/➔m➔y➔a➔p➔p➔:➔1➔.➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔u➔l➔l➔ ➔f➔r➔o➔m➔ ➔r➔e➔g➔i➔s➔t➔r➔y➔
➔Q➔1➔1➔.➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔ ➔M➔u➔l➔t➔i➔-➔S➔t➔a➔g➔e➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔?➔
➔A➔n➔s➔w➔e➔r➔:➔
➔M➔u➔l➔t➔i➔-➔s➔t➔a➔g➔e➔ ➔b➔u➔i➔l➔d➔s➔ ➔u➔s➔e➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔F➔R➔O➔M➔ ➔s➔t➔a➔t➔e➔m➔e➔n➔t➔s➔ ➔—➔ ➔a➔ ➔b➔u➔i➔l➔d➔ ➔s➔t➔a➔g➔e➔ ➔a➔n➔d➔ ➔a➔ ➔r➔u➔n➔t➔i➔m➔e➔ ➔s➔t➔a➔g➔e➔.➔ ➔B➔u➔i➔l➔d➔ ➔s➔t➔a➔g➔e➔ ➔c➔o➔m➔p➔i➔l➔e➔s➔
➔c➔o➔d➔e➔ ➔w➔i➔t➔h➔ ➔a➔l➔l➔ ➔d➔e➔v➔ ➔t➔o➔o➔l➔s➔.➔ ➔R➔u➔n➔t➔i➔m➔e➔ ➔s➔t➔a➔g➔e➔ ➔c➔o➔p➔i➔e➔s➔ ➔o➔n➔l➔y➔ ➔t➔h➔e➔ ➔b➔u➔i➔l➔t➔ ➔a➔r➔t➔i➔f➔a➔c➔t➔s➔,➔ ➔k➔e➔e➔p➔i➔n➔g➔ ➔t➔h➔e➔ ➔f➔i➔n➔a➔l➔ ➔i➔m➔a➔g➔e➔ ➔s➔m➔a➔l➔l➔ ➔a➔n➔d➔ ➔s➔e➔c➔u➔r➔e➔.➔
➔E➔x➔a➔m➔p➔l➔e➔:➔
➔#➔ ➔S➔t➔a➔g➔e➔ ➔1➔ ➔-➔ ➔B➔u➔i➔l➔d➔
➔F➔R➔O➔M➔ ➔n➔o➔d➔e➔:➔1➔8➔ ➔A➔S➔ ➔b➔u➔i➔l➔d➔e➔r➔
➔W➔O➔R➔K➔D➔I➔R➔ ➔/➔a➔p➔p➔
➔
➔
➔
➔
➔C➔O➔P➔Y➔ ➔p➔a➔c➔k➔a➔g➔e➔*➔.➔j➔s➔o➔n➔ ➔.➔/➔
➔R➔U➔N➔ ➔n➔p➔m➔ ➔i➔n➔s➔t➔a➔l➔l➔
➔C➔O➔P➔Y➔ ➔.➔ ➔.➔
➔R➔U➔N➔ ➔n➔p➔m➔ ➔r➔u➔n➔ ➔b➔u➔i➔l➔d➔
➔#➔ ➔S➔t➔a➔g➔e➔ ➔2➔ ➔-➔ ➔R➔u➔n➔t➔i➔m➔e➔ ➔(➔o➔n➔l➔y➔ ➔a➔r➔t➔i➔f➔a➔c➔t➔s➔,➔ ➔n➔o➔ ➔d➔e➔v➔ ➔t➔o➔o➔l➔s➔)➔
➔F➔R➔O➔M➔ ➔n➔o➔d➔e➔:➔1➔8➔-➔a➔l➔p➔i➔n➔e➔
➔W➔O➔R➔K➔D➔I➔R➔ ➔/➔a➔p➔p➔
➔C➔O➔P➔Y➔ ➔-➔-➔f➔r➔o➔m➔=➔b➔u➔i➔l➔d➔e➔r➔ ➔/➔a➔p➔p➔/➔d➔i➔s➔t➔ ➔.➔/➔d➔i➔s➔t➔
➔C➔O➔P➔Y➔ ➔-➔-➔f➔r➔o➔m➔=➔b➔u➔i➔l➔d➔e➔r➔ ➔/➔a➔p➔p➔/➔n➔o➔d➔e➔_➔m➔o➔d➔u➔l➔e➔s➔ ➔.➔/➔n➔o➔d➔e➔_➔m➔o➔d➔u➔l➔e➔s➔
➔E➔X➔P➔O➔S➔E➔ ➔3➔0➔0➔0➔
➔C➔M➔D➔ ➔[➔"➔n➔o➔d➔e➔"➔,➔ ➔"➔d➔i➔s➔t➔/➔a➔p➔p➔.➔j➔s➔"➔]➔
➔R➔e➔s➔u➔l➔t➔:➔ ➔F➔i➔n➔a➔l➔ ➔i➔m➔a➔g➔e➔ ➔i➔s➔ ➔t➔i➔n➔y➔ ➔—➔ ➔n➔o➔ ➔b➔u➔i➔l➔d➔ ➔t➔o➔o➔l➔s➔,➔ ➔n➔o➔ ➔s➔o➔u➔r➔c➔e➔ ➔c➔o➔d➔e➔,➔ ➔j➔u➔s➔t➔ ➔w➔h➔a➔t➔'➔s➔ ➔n➔e➔e➔d➔e➔d➔ ➔t➔o➔ ➔r➔u➔n➔.➔
➔Q➔1➔2➔.➔ ➔D➔o➔c➔k➔e➔r➔ ➔S➔e➔c➔u➔r➔i➔t➔y➔ ➔B➔e➔s➔t➔ ➔P➔r➔a➔c➔t➔i➔c➔e➔s➔
➔A➔n➔s➔w➔e➔r➔:➔
➔#➔ ➔1➔.➔ ➔N➔e➔v➔e➔r➔ ➔r➔u➔n➔ ➔a➔s➔ ➔r➔o➔o➔t➔ ➔—➔ ➔u➔s➔e➔ ➔n➔o➔n➔-➔r➔o➔o➔t➔ ➔u➔s➔e➔r➔
➔U➔S➔E➔R➔ ➔n➔o➔d➔e➔
➔#➔ ➔2➔.➔ ➔U➔s➔e➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔b➔a➔s➔e➔ ➔i➔m➔a➔g➔e➔ ➔v➔e➔r➔s➔i➔o➔n➔s➔,➔ ➔n➔o➔t➔ ➔l➔a➔t➔e➔s➔t➔
➔F➔R➔O➔M➔ ➔n➔o➔d➔e➔:➔1➔8➔-➔a➔l➔p➔i➔n➔e➔ ➔ ➔ ➔#➔ ➔g➔o➔o➔d➔
➔F➔R➔O➔M➔ ➔n➔o➔d➔e➔:➔l➔a➔t➔e➔s➔t➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔b➔a➔d➔
➔#➔ ➔3➔.➔ ➔U➔s➔e➔ ➔.➔d➔o➔c➔k➔e➔r➔i➔g➔n➔o➔r➔e➔ ➔t➔o➔ ➔e➔x➔c➔l➔u➔d➔e➔ ➔u➔n➔n➔e➔c➔e➔s➔s➔a➔r➔y➔ ➔f➔i➔l➔e➔s➔
➔#➔ ➔.➔d➔o➔c➔k➔e➔r➔i➔g➔n➔o➔r➔e➔ ➔f➔i➔l➔e➔:➔
➔n➔o➔d➔e➔_➔m➔o➔d➔u➔l➔e➔s➔
➔.➔g➔i➔t➔
➔*➔.➔l➔o➔g➔
➔.➔e➔n➔v➔
➔#➔ ➔4➔.➔ ➔D➔o➔n➔'➔t➔ ➔h➔a➔r➔d➔c➔o➔d➔e➔ ➔s➔e➔c➔r➔e➔t➔s➔
➔E➔N➔V➔ ➔D➔B➔_➔P➔A➔S➔S➔W➔O➔R➔D➔=➔s➔e➔c➔r➔e➔t➔1➔2➔3➔ ➔ ➔ ➔#➔ ➔B➔A➔D➔ ➔—➔ ➔v➔i➔s➔i➔b➔l➔e➔ ➔i➔n➔ ➔i➔m➔a➔g➔e➔ ➔h➔i➔s➔t➔o➔r➔y➔
➔#➔ ➔U➔s➔e➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔ ➔a➔t➔ ➔r➔u➔n➔t➔i➔m➔e➔ ➔i➔n➔s➔t➔e➔a➔d➔:➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔e➔ ➔D➔B➔_➔P➔A➔S➔S➔W➔O➔R➔D➔=➔s➔e➔c➔r➔e➔t➔1➔2➔3➔ ➔m➔y➔a➔p➔p➔
➔#➔ ➔5➔.➔ ➔U➔s➔e➔ ➔m➔u➔l➔t➔i➔-➔s➔t➔a➔g➔e➔ ➔b➔u➔i➔l➔d➔s➔ ➔t➔o➔ ➔r➔e➔d➔u➔c➔e➔ ➔a➔t➔t➔a➔c➔k➔ ➔s➔u➔r➔f➔a➔c➔e➔
➔#➔ ➔6➔.➔ ➔S➔c➔a➔n➔ ➔i➔m➔a➔g➔e➔s➔ ➔f➔o➔r➔ ➔v➔u➔l➔n➔e➔r➔a➔b➔i➔l➔i➔t➔i➔e➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔s➔c➔a➔n➔ ➔m➔y➔a➔p➔p➔:➔1➔.➔0➔
➔
➔
➔
➔
➔#➔ ➔7➔.➔ ➔S➔e➔t➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔l➔i➔m➔i➔t➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔-➔m➔e➔m➔o➔r➔y➔=➔"➔2➔5➔6➔m➔"➔ ➔-➔-➔c➔p➔u➔s➔=➔"➔0➔.➔5➔"➔ ➔m➔y➔a➔p➔p➔
➔Q➔1➔3➔.➔ ➔D➔o➔c➔k➔e➔r➔ ➔T➔r➔o➔u➔b➔l➔e➔s➔h➔o➔o➔t➔i➔n➔g➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔
➔A➔n➔s➔w➔e➔r➔:➔
➔#➔ ➔V➔i➔e➔w➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔l➔o➔g➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔l➔o➔g➔s➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔v➔i➔e➔w➔ ➔l➔o➔g➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔l➔o➔g➔s➔ ➔-➔f➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔l➔l➔o➔w➔ ➔l➔o➔g➔s➔ ➔i➔n➔ ➔r➔e➔a➔l➔ ➔t➔i➔m➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔l➔o➔g➔s➔ ➔-➔-➔t➔a➔i➔l➔ ➔5➔0➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔ ➔ ➔#➔ ➔l➔a➔s➔t➔ ➔5➔0➔ ➔l➔i➔n➔e➔s➔
➔#➔ ➔I➔n➔s➔p➔e➔c➔t➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔d➔o➔c➔k➔e➔r➔ ➔i➔n➔s➔p➔e➔c➔t➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔u➔l➔l➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔d➔e➔t➔a➔i➔l➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔s➔t➔a➔t➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔v➔e➔ ➔C➔P➔U➔,➔ ➔m➔e➔m➔o➔r➔y➔ ➔u➔s➔a➔g➔e➔ ➔o➔f➔ ➔a➔l➔l➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔t➔o➔p➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔r➔o➔c➔e➔s➔s➔e➔s➔ ➔r➔u➔n➔n➔i➔n➔g➔ ➔i➔n➔s➔i➔d➔e➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔#➔ ➔D➔e➔b➔u➔g➔ ➔i➔n➔s➔i➔d➔e➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔d➔o➔c➔k➔e➔r➔ ➔e➔x➔e➔c➔ ➔-➔i➔t➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔b➔a➔s➔h➔ ➔ ➔ ➔ ➔#➔ ➔o➔p➔e➔n➔ ➔b➔a➔s➔h➔ ➔s➔h➔e➔l➔l➔ ➔i➔n➔s➔i➔d➔e➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔d➔o➔c➔k➔e➔r➔ ➔e➔x➔e➔c➔ ➔-➔i➔t➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔s➔h➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔u➔s➔e➔ ➔s➔h➔ ➔i➔f➔ ➔b➔a➔s➔h➔ ➔n➔o➔t➔ ➔a➔v➔a➔i➔l➔a➔b➔l➔e➔
➔#➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔l➔i➔f➔e➔c➔y➔c➔l➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔p➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔r➔u➔n➔n➔i➔n➔g➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔p➔s➔ ➔-➔a➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔a➔l➔l➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔(➔i➔n➔c➔l➔u➔d➔i➔n➔g➔ ➔s➔t➔o➔p➔p➔e➔d➔)➔
➔d➔o➔c➔k➔e➔r➔ ➔s➔t➔o➔p➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔t➔o➔p➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔d➔o➔c➔k➔e➔r➔ ➔s➔t➔a➔r➔t➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔t➔a➔r➔t➔ ➔s➔t➔o➔p➔p➔e➔d➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔e➔s➔t➔a➔r➔t➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔s➔t➔a➔r➔t➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔m➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔s➔t➔o➔p➔p➔e➔d➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔m➔ ➔-➔f➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔r➔c➔e➔ ➔r➔e➔m➔o➔v➔e➔ ➔r➔u➔n➔n➔i➔n➔g➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔#➔ ➔I➔m➔a➔g➔e➔ ➔m➔a➔n➔a➔g➔e➔m➔e➔n➔t➔
➔d➔o➔c➔k➔e➔r➔ ➔i➔m➔a➔g➔e➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔a➔l➔l➔ ➔i➔m➔a➔g➔e➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔m➔i➔ ➔m➔y➔i➔m➔a➔g➔e➔:➔1➔.➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔i➔m➔a➔g➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔i➔m➔a➔g➔e➔ ➔p➔r➔u➔n➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔u➔n➔u➔s➔e➔d➔ ➔i➔m➔a➔g➔e➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔s➔y➔s➔t➔e➔m➔ ➔p➔r➔u➔n➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔l➔e➔a➔n➔ ➔u➔p➔ ➔e➔v➔e➔r➔y➔t➔h➔i➔n➔g➔ ➔u➔n➔u➔s➔e➔d➔
➔Q➔1➔4➔.➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔t➔h➔e➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔c➔e➔ ➔b➔e➔t➔w➔e➔e➔n➔ ➔D➔o➔c➔k➔e➔r➔ ➔a➔n➔d➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔d➔?➔
➔A➔n➔s➔w➔e➔r➔:➔
➔
➔
➔
➔
➔D➔o➔c➔k➔e➔r➔ ➔—➔ ➔c➔o➔m➔p➔l➔e➔t➔e➔ ➔p➔l➔a➔t➔f➔o➔r➔m➔.➔ ➔I➔n➔c➔l➔u➔d➔e➔s➔ ➔C➔L➔I➔,➔ ➔b➔u➔i➔l➔d➔ ➔t➔o➔o➔l➔s➔,➔ ➔i➔m➔a➔g➔e➔ ➔m➔a➔n➔a➔g➔e➔m➔e➔n➔t➔,➔ ➔n➔e➔t➔w➔o➔r➔k➔i➔n➔g➔,➔ ➔s➔t➔o➔r➔a➔g➔e➔,➔ ➔a➔n➔d➔
➔c➔o➔n➔t➔a➔i➔n➔e➔r➔d➔ ➔u➔n➔d➔e➔r➔n➔e➔a➔t➔h➔.➔
➔c➔o➔n➔t➔a➔i➔n➔e➔r➔d➔ ➔—➔ ➔l➔i➔g➔h➔t➔w➔e➔i➔g➔h➔t➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔r➔u➔n➔t➔i➔m➔e➔.➔ ➔J➔u➔s➔t➔ ➔t➔h➔e➔ ➔c➔o➔r➔e➔ ➔e➔n➔g➔i➔n➔e➔ ➔t➔h➔a➔t➔ ➔r➔u➔n➔s➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔.➔ ➔N➔o➔ ➔C➔L➔I➔,➔ ➔n➔o➔ ➔b➔u➔i➔l➔d➔
➔t➔o➔o➔l➔s➔.➔
➔D➔o➔c➔k➔e➔r➔ ➔u➔s➔e➔s➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔d➔ ➔u➔n➔d➔e➔r➔ ➔t➔h➔e➔ ➔h➔o➔o➔d➔.➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔ ➔m➔o➔v➔e➔d➔ ➔a➔w➔a➔y➔ ➔f➔r➔o➔m➔ ➔D➔o➔c➔k➔e➔r➔ ➔a➔n➔d➔ ➔n➔o➔w➔ ➔u➔s➔e➔s➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔d➔
➔d➔i➔r➔e➔c➔t➔l➔y➔ ➔a➔s➔ ➔i➔t➔s➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔r➔u➔n➔t➔i➔m➔e➔ ➔—➔ ➔s➔i➔m➔p➔l➔e➔r➔,➔ ➔f➔a➔s➔t➔e➔r➔,➔ ➔l➔e➔s➔s➔ ➔o➔v➔e➔r➔h➔e➔a➔d➔.➔
➔F➔o➔r➔ ➔i➔n➔t➔e➔r➔v➔i➔e➔w➔s➔:➔ ➔D➔o➔c➔k➔e➔r➔ ➔i➔s➔ ➔t➔h➔e➔ ➔f➔u➔l➔l➔ ➔t➔o➔o➔l➔s➔e➔t➔ ➔f➔o➔r➔ ➔d➔e➔v➔e➔l➔o➔p➔e➔r➔s➔.➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔d➔ ➔i➔s➔ ➔t➔h➔e➔ ➔l➔e➔a➔n➔e➔r➔ ➔r➔u➔n➔t➔i➔m➔e➔ ➔t➔h➔a➔t➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔
➔p➔r➔e➔f➔e➔r➔s➔ ➔i➔n➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔.➔
➔Q➔1➔5➔.➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔O➔r➔c➔h➔e➔s➔t➔r➔a➔t➔i➔o➔n➔ ➔a➔n➔d➔ ➔w➔h➔y➔ ➔d➔o➔ ➔y➔o➔u➔ ➔n➔e➔e➔d➔ ➔i➔t➔?➔
➔A➔n➔s➔w➔e➔r➔:➔
➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔o➔r➔c➔h➔e➔s➔t➔r➔a➔t➔i➔o➔n➔ ➔a➔u➔t➔o➔m➔a➔t➔e➔s➔ ➔d➔e➔p➔l➔o➔y➔i➔n➔g➔,➔ ➔s➔c➔a➔l➔i➔n➔g➔,➔ ➔a➔n➔d➔ ➔m➔a➔n➔a➔g➔i➔n➔g➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔a➔c➔r➔o➔s➔s➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔m➔a➔c➔h➔i➔n➔e➔s➔.➔
➔W➔i➔t➔h➔o➔u➔t➔ ➔i➔t➔,➔ ➔y➔o➔u➔'➔d➔ ➔m➔a➔n➔u➔a➔l➔l➔y➔ ➔m➔a➔n➔a➔g➔e➔ ➔e➔a➔c➔h➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔—➔ ➔i➔m➔p➔o➔s➔s➔i➔b➔l➔e➔ ➔a➔t➔ ➔s➔c➔a➔l➔e➔.➔
➔W➔h➔a➔t➔ ➔o➔r➔c➔h➔e➔s➔t➔r➔a➔t➔i➔o➔n➔ ➔h➔a➔n➔d➔l➔e➔s➔:➔
➔D➔e➔p➔l➔o➔y➔i➔n➔g➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔a➔c➔r➔o➔s➔s➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔n➔o➔d➔e➔s➔
➔S➔c➔a➔l➔i➔n➔g➔ ➔u➔p➔/➔d➔o➔w➔n➔ ➔b➔a➔s➔e➔d➔ ➔o➔n➔ ➔d➔e➔m➔a➔n➔d➔
➔R➔e➔s➔t➔a➔r➔t➔i➔n➔g➔ ➔f➔a➔i➔l➔e➔d➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔(➔s➔e➔l➔f➔-➔h➔e➔a➔l➔i➔n➔g➔)➔
➔Z➔e➔r➔o➔-➔d➔o➔w➔n➔t➔i➔m➔e➔ ➔u➔p➔d➔a➔t➔e➔s➔
➔L➔o➔a➔d➔ ➔b➔a➔l➔a➔n➔c➔i➔n➔g➔ ➔t➔r➔a➔f➔f➔i➔c➔
➔N➔e➔t➔w➔o➔r➔k➔i➔n➔g➔ ➔b➔e➔t➔w➔e➔e➔n➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔
➔P➔e➔r➔s➔i➔s➔t➔e➔n➔t➔ ➔s➔t➔o➔r➔a➔g➔e➔ ➔m➔a➔n➔a➔g➔e➔m➔e➔n➔t➔
➔T➔o➔o➔l➔s➔:➔
➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔ ➔—➔ ➔i➔n➔d➔u➔s➔t➔r➔y➔ ➔s➔t➔a➔n➔d➔a➔r➔d➔,➔ ➔m➔o➔s➔t➔ ➔p➔o➔w➔e➔r➔f➔u➔l➔
➔D➔o➔c➔k➔e➔r➔ ➔S➔w➔a➔r➔m➔ ➔—➔ ➔s➔i➔m➔p➔l➔e➔r➔,➔ ➔b➔u➔i➔l➔t➔ ➔i➔n➔t➔o➔ ➔D➔o➔c➔k➔e➔r➔,➔ ➔l➔e➔s➔s➔ ➔f➔e➔a➔t➔u➔r➔e➔s➔
➔F➔o➔r➔ ➔i➔n➔t➔e➔r➔v➔i➔e➔w➔s➔:➔ ➔A➔l➔w➔a➔y➔s➔ ➔s➔a➔y➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔.➔ ➔I➔t➔'➔s➔ ➔w➔h➔a➔t➔ ➔e➔n➔t➔e➔r➔p➔r➔i➔s➔e➔ ➔D➔e➔v➔O➔p➔s➔ ➔t➔e➔a➔m➔s➔ ➔u➔s➔e➔.➔
➔D➔o➔c➔k➔e➔r➔ ➔—➔ ➔D➔e➔e➔p➔ ➔D➔i➔v➔e➔ ➔&➔ ➔A➔d➔d➔i➔t➔i➔o➔n➔a➔l➔ ➔T➔o➔p➔i➔c➔s➔
➔A➔l➔l➔ ➔n➔e➔w➔ ➔c➔o➔n➔t➔e➔n➔t➔.➔ ➔N➔o➔ ➔d➔u➔p➔l➔i➔c➔a➔t➔i➔o➔n➔ ➔w➔i➔t➔h➔ ➔e➔x➔i➔s➔t➔i➔n➔g➔ ➔D➔o➔c➔k➔e➔r➔ ➔s➔e➔c➔t➔i➔o➔n➔ ➔a➔b➔o➔v➔e➔.➔
➔
➔
➔
➔
➔A➔.➔ ➔V➔M➔ ➔v➔s➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔s➔
➔V➔i➔r➔t➔u➔a➔l➔ ➔M➔a➔c➔h➔i➔n➔e➔ ➔(➔V➔M➔)➔
➔A➔ ➔V➔M➔ ➔i➔s➔ ➔a➔ ➔f➔u➔l➔l➔ ➔c➔o➔m➔p➔u➔t➔e➔r➔ ➔r➔u➔n➔n➔i➔n➔g➔ ➔i➔n➔s➔i➔d➔e➔ ➔y➔o➔u➔r➔ ➔c➔o➔m➔p➔u➔t➔e➔r➔.➔ ➔I➔t➔ ➔h➔a➔s➔ ➔i➔t➔s➔ ➔o➔w➔n➔ ➔O➔S➔,➔ ➔k➔e➔r➔n➔e➔l➔,➔ ➔m➔e➔m➔o➔r➔y➔,➔ ➔C➔P➔U➔ ➔a➔l➔l➔o➔c➔a➔t➔i➔o➔n➔ ➔—➔
➔e➔v➔e➔r➔y➔t➔h➔i➔n➔g➔.➔
➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔Y➔o➔u➔r➔ ➔M➔a➔c➔h➔i➔n➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔H➔y➔p➔e➔r➔v➔i➔s➔o➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔(➔V➔M➔w➔a➔r➔e➔,➔ ➔V➔i➔r➔t➔u➔a➔l➔B➔o➔x➔,➔ ➔K➔V➔M➔)➔ ➔ ➔ ➔│➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔ ➔│➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔│➔ ➔ ➔ ➔V➔M➔ ➔1➔ ➔ ➔ ➔│➔ ➔│➔ ➔ ➔ ➔V➔M➔ ➔2➔ ➔ ➔ ➔│➔ ➔ ➔│➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔│➔ ➔G➔u➔e➔s➔t➔ ➔O➔S➔ ➔│➔ ➔│➔ ➔G➔u➔e➔s➔t➔ ➔O➔S➔ ➔│➔ ➔ ➔│➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔│➔ ➔ ➔A➔p➔p➔ ➔A➔ ➔ ➔ ➔│➔ ➔│➔ ➔ ➔A➔p➔p➔ ➔B➔ ➔ ➔ ➔│➔ ➔ ➔│➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔ ➔│➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔H➔o➔s➔t➔ ➔O➔S➔ ➔+➔ ➔K➔e➔r➔n➔e➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔H➔a➔r➔d➔w➔a➔r➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔
➔C➔o➔n➔t➔a➔i➔n➔e➔r➔
➔A➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔s➔h➔a➔r➔e➔s➔ ➔t➔h➔e➔ ➔h➔o➔s➔t➔ ➔O➔S➔ ➔k➔e➔r➔n➔e➔l➔.➔ ➔I➔t➔ ➔o➔n➔l➔y➔ ➔p➔a➔c➔k➔a➔g➔e➔s➔ ➔t➔h➔e➔ ➔a➔p➔p➔ ➔a➔n➔d➔ ➔i➔t➔s➔ ➔d➔e➔p➔e➔n➔d➔e➔n➔c➔i➔e➔s➔ ➔—➔ ➔n➔o➔ ➔f➔u➔l➔l➔ ➔O➔S➔ ➔n➔e➔e➔d➔e➔d➔.➔
➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔Y➔o➔u➔r➔ ➔M➔a➔c➔h➔i➔n➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔D➔o➔c➔k➔e➔r➔ ➔E➔n➔g➔i➔n➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔ ➔│➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔│➔C➔o➔n➔t➔a➔i➔n➔e➔r➔1➔│➔ ➔│➔C➔o➔n➔t➔a➔i➔n➔e➔r➔2➔│➔ ➔ ➔│➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔│➔ ➔ ➔A➔p➔p➔ ➔A➔ ➔ ➔ ➔│➔ ➔│➔ ➔ ➔A➔p➔p➔ ➔B➔ ➔ ➔ ➔│➔ ➔ ➔│➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔│➔ ➔ ➔L➔i➔b➔s➔ ➔ ➔ ➔ ➔│➔ ➔│➔ ➔ ➔L➔i➔b➔s➔ ➔ ➔ ➔ ➔│➔ ➔ ➔│➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔ ➔│➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔H➔o➔s➔t➔ ➔O➔S➔ ➔+➔ ➔K➔e➔r➔n➔e➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔H➔a➔r➔d➔w➔a➔r➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔
➔V➔M➔ ➔v➔s➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔C➔o➔m➔p➔a➔r➔i➔s➔o➔n➔
➔
➔
➔
➔
➔F➔e➔a➔t➔u➔r➔e➔ ➔V➔i➔r➔t➔u➔a➔l➔ ➔M➔a➔c➔h➔i➔n➔e➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔
➔S➔i➔z➔e➔ ➔G➔B➔s➔ ➔(➔f➔u➔l➔l➔ ➔O➔S➔)➔ ➔M➔B➔s➔ ➔(➔j➔u➔s➔t➔ ➔a➔p➔p➔ ➔+➔ ➔l➔i➔b➔s➔)➔
➔S➔t➔a➔r➔t➔u➔p➔ ➔t➔i➔m➔e➔ ➔M➔i➔n➔u➔t➔e➔s➔ ➔S➔e➔c➔o➔n➔d➔s➔
➔O➔S➔ ➔O➔w➔n➔ ➔f➔u➔l➔l➔ ➔O➔S➔ ➔S➔h➔a➔r➔e➔s➔ ➔h➔o➔s➔t➔ ➔O➔S➔ ➔k➔e➔r➔n➔e➔l➔
➔I➔s➔o➔l➔a➔t➔i➔o➔n➔ ➔S➔t➔r➔o➔n➔g➔ ➔(➔h➔a➔r➔d➔w➔a➔r➔e➔ ➔l➔e➔v➔e➔l➔)➔ ➔G➔o➔o➔d➔ ➔(➔p➔r➔o➔c➔e➔s➔s➔ ➔l➔e➔v➔e➔l➔)➔
➔P➔e➔r➔f➔o➔r➔m➔a➔n➔c➔e➔ ➔S➔l➔o➔w➔e➔r➔ ➔(➔o➔v➔e➔r➔h➔e➔a➔d➔)➔ ➔N➔e➔a➔r➔ ➔n➔a➔t➔i➔v➔e➔ ➔s➔p➔e➔e➔d➔
➔P➔o➔r➔t➔a➔b➔i➔l➔i➔t➔y➔ ➔L➔e➔s➔s➔ ➔p➔o➔r➔t➔a➔b➔l➔e➔ ➔H➔i➔g➔h➔l➔y➔ ➔p➔o➔r➔t➔a➔b➔l➔e➔
➔R➔e➔s➔o➔u➔r➔c➔e➔ ➔u➔s➔a➔g➔e➔ ➔H➔e➔a➔v➔y➔ ➔L➔i➔g➔h➔t➔w➔e➔i➔g➔h➔t➔
➔S➔e➔c➔u➔r➔i➔t➔y➔ ➔M➔o➔r➔e➔ ➔i➔s➔o➔l➔a➔t➔e➔d➔ ➔L➔e➔s➔s➔ ➔i➔s➔o➔l➔a➔t➔e➔d➔
➔U➔s➔e➔ ➔c➔a➔s➔e➔ ➔F➔u➔l➔l➔ ➔O➔S➔ ➔n➔e➔e➔d➔e➔d➔,➔ ➔s➔t➔r➔o➔n➔g➔ ➔i➔s➔o➔l➔a➔t➔i➔o➔n➔ ➔M➔i➔c➔r➔o➔s➔e➔r➔v➔i➔c➔e➔s➔,➔ ➔C➔I➔/➔C➔D➔
➔P➔r➔o➔s➔ ➔o➔f➔ ➔V➔M➔s➔:➔
➔S➔t➔r➔o➔n➔g➔ ➔i➔s➔o➔l➔a➔t➔i➔o➔n➔ ➔—➔ ➔o➔n➔e➔ ➔V➔M➔ ➔c➔r➔a➔s➔h➔ ➔d➔o➔e➔s➔n➔'➔t➔ ➔a➔f➔f➔e➔c➔t➔ ➔o➔t➔h➔e➔r➔s➔
➔R➔u➔n➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔t➔ ➔O➔S➔ ➔(➔W➔i➔n➔d➔o➔w➔s➔ ➔V➔M➔ ➔o➔n➔ ➔L➔i➔n➔u➔x➔ ➔h➔o➔s➔t➔)➔
➔B➔e➔t➔t➔e➔r➔ ➔s➔e➔c➔u➔r➔i➔t➔y➔ ➔b➔o➔u➔n➔d➔a➔r➔i➔e➔s➔
➔G➔o➔o➔d➔ ➔f➔o➔r➔ ➔s➔t➔a➔t➔e➔f➔u➔l➔,➔ ➔l➔o➔n➔g➔-➔r➔u➔n➔n➔i➔n➔g➔ ➔a➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔s➔
➔C➔o➔n➔s➔ ➔o➔f➔ ➔V➔M➔s➔:➔
➔H➔e➔a➔v➔y➔ ➔—➔ ➔e➔a➔c➔h➔ ➔V➔M➔ ➔n➔e➔e➔d➔s➔ ➔f➔u➔l➔l➔ ➔O➔S➔ ➔(➔G➔B➔s➔)➔
➔S➔l➔o➔w➔ ➔t➔o➔ ➔s➔t➔a➔r➔t➔
➔W➔a➔s➔t➔e➔s➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔s➔
➔H➔a➔r➔d➔ ➔t➔o➔ ➔s➔c➔a➔l➔e➔ ➔q➔u➔i➔c➔k➔l➔y➔
➔P➔r➔o➔s➔ ➔o➔f➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔
➔L➔i➔g➔h➔t➔w➔e➔i➔g➔h➔t➔ ➔—➔ ➔M➔B➔s➔ ➔n➔o➔t➔ ➔G➔B➔s➔
➔S➔t➔a➔r➔t➔ ➔i➔n➔ ➔s➔e➔c➔o➔n➔d➔s➔
➔C➔o➔n➔s➔i➔s➔t➔e➔n➔t➔ ➔a➔c➔r➔o➔s➔s➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔s➔
➔E➔a➔s➔y➔ ➔t➔o➔ ➔s➔c➔a➔l➔e➔
➔P➔e➔r➔f➔e➔c➔t➔ ➔f➔o➔r➔ ➔m➔i➔c➔r➔o➔s➔e➔r➔v➔i➔c➔e➔s➔ ➔a➔n➔d➔ ➔C➔I➔/➔C➔D➔
➔C➔o➔n➔s➔ ➔o➔f➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔
➔W➔e➔a➔k➔e➔r➔ ➔i➔s➔o➔l➔a➔t➔i➔o➔n➔ ➔t➔h➔a➔n➔ ➔V➔M➔s➔
➔A➔l➔l➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔s➔h➔a➔r➔e➔ ➔h➔o➔s➔t➔ ➔k➔e➔r➔n➔e➔l➔ ➔—➔ ➔k➔e➔r➔n➔e➔l➔ ➔v➔u➔l➔n➔e➔r➔a➔b➔i➔l➔i➔t➔y➔ ➔a➔f➔f➔e➔c➔t➔s➔ ➔a➔l➔l➔
➔S➔t➔a➔t➔e➔f➔u➔l➔ ➔a➔p➔p➔s➔ ➔n➔e➔e➔d➔ ➔e➔x➔t➔r➔a➔ ➔s➔e➔t➔u➔p➔ ➔(➔v➔o➔l➔u➔m➔e➔s➔)➔
➔
➔
➔
➔
➔N➔e➔t➔w➔o➔r➔k➔i➔n➔g➔ ➔m➔o➔r➔e➔ ➔c➔o➔m➔p➔l➔e➔x➔ ➔a➔t➔ ➔s➔c➔a➔l➔e➔
➔B➔.➔ ➔D➔o➔c➔k➔e➔r➔ ➔A➔r➔c➔h➔i➔t➔e➔c➔t➔u➔r➔e➔ ➔(➔D➔e➔t➔a➔i➔l➔e➔d➔)➔
➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔D➔o➔c➔k➔e➔r➔ ➔C➔l➔i➔e➔n➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔(➔d➔o➔c➔k➔e➔r➔ ➔b➔u➔i➔l➔d➔,➔ ➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔,➔ ➔d➔o➔c➔k➔e➔r➔ ➔p➔u➔s➔h➔)➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┬➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔R➔E➔S➔T➔ ➔A➔P➔I➔
➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔▼➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔D➔o➔c➔k➔e➔r➔ ➔D➔a➔e➔m➔o➔n➔ ➔(➔d➔o➔c➔k➔e➔r➔d➔)➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔ ➔I➔m➔a➔g➔e➔s➔ ➔ ➔ ➔ ➔│➔ ➔ ➔│➔C➔o➔n➔t➔a➔i➔n➔e➔r➔s➔│➔ ➔ ➔│➔ ➔ ➔ ➔ ➔N➔e➔t➔w➔o➔r➔k➔s➔ ➔ ➔ ➔ ➔│➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔(➔s➔t➔o➔r➔e➔d➔ ➔ ➔ ➔ ➔│➔ ➔ ➔│➔(➔r➔u➔n➔n➔i➔n➔g➔ ➔ ➔│➔ ➔ ➔│➔ ➔ ➔(➔b➔r➔i➔d➔g➔e➔,➔h➔o➔s➔t➔,➔ ➔│➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔l➔o➔c➔a➔l➔l➔y➔)➔ ➔ ➔ ➔│➔ ➔ ➔│➔i➔n➔s➔t➔a➔n➔c➔e➔s➔)➔│➔ ➔ ➔│➔ ➔ ➔ ➔o➔v➔e➔r➔l➔a➔y➔)➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔│➔
➔│➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔ ➔│➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔d➔ ➔(➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔r➔u➔n➔t➔i➔m➔e➔)➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔ ➔ ➔│➔
➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┬➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔p➔u➔s➔h➔/➔p➔u➔l➔l➔
➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔▼➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔D➔o➔c➔k➔e➔r➔ ➔R➔e➔g➔i➔s➔t➔r➔y➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔(➔D➔o➔c➔k➔e➔r➔ ➔H➔u➔b➔,➔ ➔E➔C➔R➔,➔ ➔A➔C➔R➔,➔ ➔H➔a➔r➔b➔o➔r➔)➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔
➔T➔h➔r➔e➔e➔ ➔m➔a➔i➔n➔ ➔c➔o➔m➔p➔o➔n➔e➔n➔t➔s➔:➔
➔D➔o➔c➔k➔e➔r➔ ➔C➔l➔i➔e➔n➔t➔ ➔—➔ ➔C➔L➔I➔ ➔y➔o➔u➔ ➔u➔s➔e➔.➔ ➔S➔e➔n➔d➔s➔ ➔c➔o➔m➔m➔a➔n➔d➔s➔ ➔t➔o➔ ➔d➔a➔e➔m➔o➔n➔ ➔v➔i➔a➔ ➔R➔E➔S➔T➔ ➔A➔P➔I➔.➔
➔D➔o➔c➔k➔e➔r➔ ➔D➔a➔e➔m➔o➔n➔ ➔(➔d➔o➔c➔k➔e➔r➔d➔)➔ ➔—➔ ➔b➔a➔c➔k➔g➔r➔o➔u➔n➔d➔ ➔s➔e➔r➔v➔i➔c➔e➔.➔ ➔D➔o➔e➔s➔ ➔a➔l➔l➔ ➔t➔h➔e➔ ➔w➔o➔r➔k➔ ➔—➔ ➔b➔u➔i➔l➔d➔s➔ ➔i➔m➔a➔g➔e➔s➔,➔ ➔r➔u➔n➔s➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔,➔
➔m➔a➔n➔a➔g➔e➔s➔ ➔n➔e➔t➔w➔o➔r➔k➔s➔ ➔a➔n➔d➔ ➔v➔o➔l➔u➔m➔e➔s➔.➔
➔D➔o➔c➔k➔e➔r➔ ➔R➔e➔g➔i➔s➔t➔r➔y➔ ➔—➔ ➔s➔t➔o➔r➔e➔s➔ ➔a➔n➔d➔ ➔d➔i➔s➔t➔r➔i➔b➔u➔t➔e➔s➔ ➔i➔m➔a➔g➔e➔s➔.➔
➔C➔.➔ ➔D➔o➔c➔k➔e➔r➔ ➔I➔m➔a➔g➔e➔ ➔—➔ ➔D➔e➔e➔p➔ ➔D➔i➔v➔e➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔ ➔D➔o➔c➔k➔e➔r➔ ➔I➔m➔a➔g➔e➔?➔
➔A➔ ➔D➔o➔c➔k➔e➔r➔ ➔i➔m➔a➔g➔e➔ ➔i➔s➔ ➔a➔ ➔r➔e➔a➔d➔-➔o➔n➔l➔y➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔ ➔u➔s➔e➔d➔ ➔t➔o➔ ➔c➔r➔e➔a➔t➔e➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔.➔ ➔I➔t➔'➔s➔ ➔b➔u➔i➔l➔t➔ ➔i➔n➔ ➔l➔a➔y➔e➔r➔s➔ ➔—➔ ➔e➔a➔c➔h➔ ➔i➔n➔s➔t➔r➔u➔c➔t➔i➔o➔n➔ ➔i➔n➔ ➔t➔h➔e➔
➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔ ➔c➔r➔e➔a➔t➔e➔s➔ ➔o➔n➔e➔ ➔l➔a➔y➔e➔r➔.➔
➔
➔
➔
➔
➔L➔a➔y➔e➔r➔ ➔4➔:➔ ➔C➔O➔P➔Y➔ ➔a➔p➔p➔ ➔f➔i➔l➔e➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔←➔ ➔y➔o➔u➔r➔ ➔c➔o➔d➔e➔
➔L➔a➔y➔e➔r➔ ➔3➔:➔ ➔R➔U➔N➔ ➔n➔p➔m➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔←➔ ➔d➔e➔p➔e➔n➔d➔e➔n➔c➔i➔e➔s➔
➔L➔a➔y➔e➔r➔ ➔2➔:➔ ➔W➔O➔R➔K➔D➔I➔R➔ ➔/➔a➔p➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔←➔ ➔s➔e➔t➔ ➔w➔o➔r➔k➔i➔n➔g➔ ➔d➔i➔r➔
➔L➔a➔y➔e➔r➔ ➔1➔:➔ ➔F➔R➔O➔M➔ ➔n➔o➔d➔e➔:➔1➔8➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔←➔ ➔b➔a➔s➔e➔ ➔O➔S➔ ➔+➔ ➔N➔o➔d➔e➔
➔I➔m➔a➔g➔e➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔:➔
➔d➔o➔c➔k➔e➔r➔ ➔i➔m➔a➔g➔e➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔a➔l➔l➔ ➔l➔o➔c➔a➔l➔ ➔i➔m➔a➔g➔e➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔i➔m➔a➔g➔e➔s➔ ➔-➔a➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔i➔n➔c➔l➔u➔d➔e➔ ➔i➔n➔t➔e➔r➔m➔e➔d➔i➔a➔t➔e➔ ➔i➔m➔a➔g➔e➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔p➔u➔l➔l➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔u➔l➔l➔ ➔f➔r➔o➔m➔ ➔D➔o➔c➔k➔e➔r➔ ➔H➔u➔b➔
➔d➔o➔c➔k➔e➔r➔ ➔p➔u➔l➔l➔ ➔n➔g➔i➔n➔x➔:➔1➔.➔2➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔u➔l➔l➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔v➔e➔r➔s➔i➔o➔n➔
➔d➔o➔c➔k➔e➔r➔ ➔p➔u➔l➔l➔ ➔m➔y➔r➔e➔p➔o➔/➔m➔y➔a➔p➔p➔:➔1➔.➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔u➔l➔l➔ ➔f➔r➔o➔m➔ ➔p➔r➔i➔v➔a➔t➔e➔ ➔r➔e➔g➔i➔s➔t➔r➔y➔
➔d➔o➔c➔k➔e➔r➔ ➔i➔n➔s➔p➔e➔c➔t➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔t➔a➔i➔l➔e➔d➔ ➔i➔m➔a➔g➔e➔ ➔i➔n➔f➔o➔
➔d➔o➔c➔k➔e➔r➔ ➔h➔i➔s➔t➔o➔r➔y➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔l➔a➔y➔e➔r➔s➔ ➔o➔f➔ ➔i➔m➔a➔g➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔i➔m➔a➔g➔e➔ ➔l➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔a➔m➔e➔ ➔a➔s➔ ➔d➔o➔c➔k➔e➔r➔ ➔i➔m➔a➔g➔e➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔i➔m➔a➔g➔e➔ ➔r➔m➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔i➔m➔a➔g➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔m➔i➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔a➔m➔e➔ ➔a➔s➔ ➔a➔b➔o➔v➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔m➔i➔ ➔-➔f➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔r➔c➔e➔ ➔r➔e➔m➔o➔v➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔i➔m➔a➔g➔e➔ ➔p➔r➔u➔n➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔u➔n➔u➔s➔e➔d➔ ➔i➔m➔a➔g➔e➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔i➔m➔a➔g➔e➔ ➔p➔r➔u➔n➔e➔ ➔-➔a➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔A➔L➔L➔ ➔u➔n➔u➔s➔e➔d➔ ➔i➔m➔a➔g➔e➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔t➔a➔g➔ ➔n➔g➔i➔n➔x➔:➔l➔a➔t➔e➔s➔t➔ ➔m➔y➔r➔e➔p➔o➔/➔n➔g➔i➔n➔x➔:➔v➔1➔ ➔ ➔#➔ ➔t➔a➔g➔ ➔i➔m➔a➔g➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔s➔a➔v➔e➔ ➔n➔g➔i➔n➔x➔ ➔>➔ ➔n➔g➔i➔n➔x➔.➔t➔a➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔a➔v➔e➔ ➔i➔m➔a➔g➔e➔ ➔t➔o➔ ➔f➔i➔l➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔l➔o➔a➔d➔ ➔<➔ ➔n➔g➔i➔n➔x➔.➔t➔a➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔o➔a➔d➔ ➔i➔m➔a➔g➔e➔ ➔f➔r➔o➔m➔ ➔f➔i➔l➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔e➔x➔p➔o➔r➔t➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔1➔ ➔>➔ ➔a➔p➔p➔.➔t➔a➔r➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔x➔p➔o➔r➔t➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔f➔i➔l➔e➔s➔y➔s➔t➔e➔m➔
➔d➔o➔c➔k➔e➔r➔ ➔i➔m➔p➔o➔r➔t➔ ➔a➔p➔p➔.➔t➔a➔r➔ ➔m➔y➔i➔m➔a➔g➔e➔:➔v➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔i➔m➔p➔o➔r➔t➔ ➔a➔s➔ ➔i➔m➔a➔g➔e➔
➔D➔.➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔ ➔—➔ ➔A➔l➔l➔ ➔I➔n➔s➔t➔r➔u➔c➔t➔i➔o➔n➔s➔
➔#➔ ➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔
➔#➔ ➔D➔O➔C➔K➔E➔R➔F➔I➔L➔E➔ ➔C➔O➔M➔P➔L➔E➔T➔E➔ ➔I➔N➔S➔T➔R➔U➔C➔T➔I➔O➔N➔S➔ ➔G➔U➔I➔D➔E➔
➔#➔ ➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔
➔#➔ ➔F➔R➔O➔M➔ ➔—➔ ➔b➔a➔s➔e➔ ➔i➔m➔a➔g➔e➔ ➔(➔R➔E➔Q➔U➔I➔R➔E➔D➔,➔ ➔m➔u➔s➔t➔ ➔b➔e➔ ➔f➔i➔r➔s➔t➔)➔
➔F➔R➔O➔M➔ ➔u➔b➔u➔n➔t➔u➔:➔2➔2➔.➔0➔4➔
➔F➔R➔O➔M➔ ➔n➔o➔d➔e➔:➔1➔8➔-➔a➔l➔p➔i➔n➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔l➔p➔i➔n➔e➔ ➔=➔ ➔t➔i➔n➔y➔ ➔b➔a➔s➔e➔ ➔i➔m➔a➔g➔e➔
➔F➔R➔O➔M➔ ➔s➔c➔r➔a➔t➔c➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔m➔p➔t➔y➔ ➔b➔a➔s➔e➔ ➔(➔f➔o➔r➔ ➔c➔o➔m➔p➔i➔l➔e➔d➔ ➔b➔i➔n➔a➔r➔i➔e➔s➔)➔
➔#➔ ➔M➔A➔I➔N➔T➔A➔I➔N➔E➔R➔ ➔—➔ ➔a➔u➔t➔h➔o➔r➔ ➔i➔n➔f➔o➔ ➔(➔d➔e➔p➔r➔e➔c➔a➔t➔e➔d➔,➔ ➔u➔s➔e➔ ➔L➔A➔B➔E➔L➔ ➔i➔n➔s➔t➔e➔a➔d➔)➔
➔M➔A➔I➔N➔T➔A➔I➔N➔E➔R➔ ➔A➔k➔h➔i➔l➔ ➔<➔a➔k➔h➔i➔l➔b➔m➔1➔3➔@➔g➔m➔a➔i➔l➔.➔c➔o➔m➔>➔
➔#➔ ➔L➔A➔B➔E➔L➔ ➔—➔ ➔m➔e➔t➔a➔d➔a➔t➔a➔ ➔k➔e➔y➔-➔v➔a➔l➔u➔e➔ ➔p➔a➔i➔r➔s➔
➔L➔A➔B➔E➔L➔ ➔m➔a➔i➔n➔t➔a➔i➔n➔e➔r➔=➔"➔a➔k➔h➔i➔l➔b➔m➔1➔3➔@➔g➔m➔a➔i➔l➔.➔c➔o➔m➔"➔
➔
➔
➔
➔
➔L➔A➔B➔E➔L➔ ➔v➔e➔r➔s➔i➔o➔n➔=➔"➔1➔.➔0➔"➔
➔L➔A➔B➔E➔L➔ ➔d➔e➔s➔c➔r➔i➔p➔t➔i➔o➔n➔=➔"➔M➔y➔ ➔N➔o➔d➔e➔.➔j➔s➔ ➔A➔p➔p➔"➔
➔#➔ ➔R➔U➔N➔ ➔—➔ ➔e➔x➔e➔c➔u➔t➔e➔ ➔c➔o➔m➔m➔a➔n➔d➔ ➔d➔u➔r➔i➔n➔g➔ ➔B➔U➔I➔L➔D➔ ➔t➔i➔m➔e➔ ➔(➔c➔r➔e➔a➔t➔e➔s➔ ➔a➔ ➔l➔a➔y➔e➔r➔)➔
➔R➔U➔N➔ ➔a➔p➔t➔-➔g➔e➔t➔ ➔u➔p➔d➔a➔t➔e➔ ➔&➔&➔ ➔a➔p➔t➔-➔g➔e➔t➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔-➔y➔ ➔c➔u➔r➔l➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔m➔b➔i➔n➔e➔ ➔t➔o➔ ➔r➔e➔d➔u➔c➔e➔ ➔l➔a➔y➔e➔r➔s➔
➔R➔U➔N➔ ➔n➔p➔m➔ ➔i➔n➔s➔t➔a➔l➔l➔
➔R➔U➔N➔ ➔m➔k➔d➔i➔r➔ ➔-➔p➔ ➔/➔a➔p➔p➔/➔l➔o➔g➔s➔
➔#➔ ➔C➔O➔P➔Y➔ ➔—➔ ➔c➔o➔p➔y➔ ➔f➔i➔l➔e➔s➔ ➔f➔r➔o➔m➔ ➔h➔o➔s➔t➔ ➔t➔o➔ ➔i➔m➔a➔g➔e➔
➔C➔O➔P➔Y➔ ➔p➔a➔c➔k➔a➔g➔e➔.➔j➔s➔o➔n➔ ➔/➔a➔p➔p➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔p➔y➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔f➔i➔l➔e➔
➔C➔O➔P➔Y➔ ➔s➔r➔c➔/➔ ➔/➔a➔p➔p➔/➔s➔r➔c➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔p➔y➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔C➔O➔P➔Y➔ ➔.➔ ➔/➔a➔p➔p➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔p➔y➔ ➔e➔v➔e➔r➔y➔t➔h➔i➔n➔g➔
➔#➔ ➔A➔D➔D➔ ➔—➔ ➔l➔i➔k➔e➔ ➔C➔O➔P➔Y➔ ➔b➔u➔t➔ ➔w➔i➔t➔h➔ ➔e➔x➔t➔r➔a➔ ➔p➔o➔w➔e➔r➔s➔
➔A➔D➔D➔ ➔a➔p➔p➔.➔t➔a➔r➔.➔g➔z➔ ➔/➔a➔p➔p➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔u➔t➔o➔-➔e➔x➔t➔r➔a➔c➔t➔s➔ ➔t➔a➔r➔ ➔f➔i➔l➔e➔s➔
➔A➔D➔D➔ ➔h➔t➔t➔p➔s➔:➔/➔/➔e➔x➔a➔m➔p➔l➔e➔.➔c➔o➔m➔/➔f➔i➔l➔e➔ ➔/➔a➔p➔p➔/➔ ➔ ➔ ➔#➔ ➔d➔o➔w➔n➔l➔o➔a➔d➔ ➔f➔r➔o➔m➔ ➔U➔R➔L➔
➔#➔ ➔R➔u➔l➔e➔:➔ ➔U➔s➔e➔ ➔C➔O➔P➔Y➔ ➔u➔n➔l➔e➔s➔s➔ ➔y➔o➔u➔ ➔n➔e➔e➔d➔ ➔A➔D➔D➔'➔s➔ ➔e➔x➔t➔r➔a➔ ➔f➔e➔a➔t➔u➔r➔e➔s➔
➔#➔ ➔W➔O➔R➔K➔D➔I➔R➔ ➔—➔ ➔s➔e➔t➔ ➔w➔o➔r➔k➔i➔n➔g➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔(➔c➔r➔e➔a➔t➔e➔s➔ ➔i➔t➔ ➔i➔f➔ ➔d➔o➔e➔s➔n➔'➔t➔ ➔e➔x➔i➔s➔t➔)➔
➔W➔O➔R➔K➔D➔I➔R➔ ➔/➔a➔p➔p➔
➔#➔ ➔A➔l➔l➔ ➔f➔o➔l➔l➔o➔w➔i➔n➔g➔ ➔c➔o➔m➔m➔a➔n➔d➔s➔ ➔r➔u➔n➔ ➔f➔r➔o➔m➔ ➔/➔a➔p➔p➔
➔#➔ ➔E➔N➔V➔ ➔—➔ ➔s➔e➔t➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔ ➔(➔a➔v➔a➔i➔l➔a➔b➔l➔e➔ ➔a➔t➔ ➔r➔u➔n➔t➔i➔m➔e➔ ➔t➔o➔o➔)➔
➔E➔N➔V➔ ➔N➔O➔D➔E➔_➔E➔N➔V➔=➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔E➔N➔V➔ ➔P➔O➔R➔T➔=➔3➔0➔0➔0➔
➔E➔N➔V➔ ➔D➔B➔_➔H➔O➔S➔T➔=➔p➔o➔s➔t➔g➔r➔e➔s➔-➔s➔e➔r➔v➔i➔c➔e➔
➔#➔ ➔A➔R➔G➔ ➔—➔ ➔b➔u➔i➔l➔d➔-➔t➔i➔m➔e➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔ ➔(➔N➔O➔T➔ ➔a➔v➔a➔i➔l➔a➔b➔l➔e➔ ➔a➔t➔ ➔r➔u➔n➔t➔i➔m➔e➔)➔
➔A➔R➔G➔ ➔V➔E➔R➔S➔I➔O➔N➔=➔1➔.➔0➔
➔A➔R➔G➔ ➔B➔U➔I➔L➔D➔_➔D➔A➔T➔E➔
➔#➔ ➔U➔s➔a➔g➔e➔:➔ ➔d➔o➔c➔k➔e➔r➔ ➔b➔u➔i➔l➔d➔ ➔-➔-➔b➔u➔i➔l➔d➔-➔a➔r➔g➔ ➔V➔E➔R➔S➔I➔O➔N➔=➔2➔.➔0➔ ➔.➔
➔#➔ ➔E➔X➔P➔O➔S➔E➔ ➔—➔ ➔d➔o➔c➔u➔m➔e➔n➔t➔ ➔w➔h➔i➔c➔h➔ ➔p➔o➔r➔t➔ ➔t➔h➔e➔ ➔a➔p➔p➔ ➔l➔i➔s➔t➔e➔n➔s➔ ➔o➔n➔ ➔(➔d➔o➔e➔s➔n➔'➔t➔ ➔a➔c➔t➔u➔a➔l➔l➔y➔ ➔p➔u➔b➔l➔i➔s➔h➔)➔
➔E➔X➔P➔O➔S➔E➔ ➔3➔0➔0➔0➔
➔E➔X➔P➔O➔S➔E➔ ➔8➔0➔ ➔4➔4➔3➔
➔#➔ ➔V➔O➔L➔U➔M➔E➔ ➔—➔ ➔c➔r➔e➔a➔t➔e➔ ➔m➔o➔u➔n➔t➔ ➔p➔o➔i➔n➔t➔ ➔f➔o➔r➔ ➔e➔x➔t➔e➔r➔n➔a➔l➔ ➔v➔o➔l➔u➔m➔e➔s➔
➔V➔O➔L➔U➔M➔E➔ ➔[➔"➔/➔d➔a➔t➔a➔"➔]➔
➔V➔O➔L➔U➔M➔E➔ ➔/➔v➔a➔r➔/➔l➔o➔g➔/➔a➔p➔p➔
➔#➔ ➔U➔S➔E➔R➔ ➔—➔ ➔s➔e➔t➔ ➔u➔s➔e➔r➔ ➔f➔o➔r➔ ➔f➔o➔l➔l➔o➔w➔i➔n➔g➔ ➔R➔U➔N➔/➔C➔M➔D➔/➔E➔N➔T➔R➔Y➔P➔O➔I➔N➔T➔ ➔(➔s➔e➔c➔u➔r➔i➔t➔y➔ ➔b➔e➔s➔t➔ ➔p➔r➔a➔c➔t➔i➔c➔e➔)➔
➔R➔U➔N➔ ➔u➔s➔e➔r➔a➔d➔d➔ ➔-➔m➔ ➔a➔p➔p➔u➔s➔e➔r➔
➔U➔S➔E➔R➔ ➔a➔p➔p➔u➔s➔e➔r➔
➔#➔ ➔N➔e➔v➔e➔r➔ ➔r➔u➔n➔ ➔a➔s➔ ➔r➔o➔o➔t➔ ➔i➔n➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔#➔ ➔C➔M➔D➔ ➔—➔ ➔d➔e➔f➔a➔u➔l➔t➔ ➔c➔o➔m➔m➔a➔n➔d➔ ➔w➔h➔e➔n➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔s➔t➔a➔r➔t➔s➔ ➔(➔c➔a➔n➔ ➔b➔e➔ ➔o➔v➔e➔r➔r➔i➔d➔d➔e➔n➔)➔
➔C➔M➔D➔ ➔[➔"➔n➔o➔d➔e➔"➔,➔ ➔"➔a➔p➔p➔.➔j➔s➔"➔]➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔x➔e➔c➔ ➔f➔o➔r➔m➔ ➔(➔p➔r➔e➔f➔e➔r➔r➔e➔d➔)➔
➔C➔M➔D➔ ➔n➔o➔d➔e➔ ➔a➔p➔p➔.➔j➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔e➔l➔l➔ ➔f➔o➔r➔m➔
➔C➔M➔D➔ ➔[➔"➔n➔p➔m➔"➔,➔ ➔"➔s➔t➔a➔r➔t➔"➔]➔
➔
➔
➔
➔
➔#➔ ➔E➔N➔T➔R➔Y➔P➔O➔I➔N➔T➔ ➔—➔ ➔m➔a➔i➔n➔ ➔e➔x➔e➔c➔u➔t➔a➔b➔l➔e➔ ➔(➔h➔a➔r➔d➔e➔r➔ ➔t➔o➔ ➔o➔v➔e➔r➔r➔i➔d➔e➔)➔
➔E➔N➔T➔R➔Y➔P➔O➔I➔N➔T➔ ➔[➔"➔n➔o➔d➔e➔"➔]➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔x➔e➔c➔ ➔f➔o➔r➔m➔
➔E➔N➔T➔R➔Y➔P➔O➔I➔N➔T➔ ➔n➔o➔d➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔e➔l➔l➔ ➔f➔o➔r➔m➔
➔#➔ ➔C➔o➔m➔b➔i➔n➔e➔d➔ ➔w➔i➔t➔h➔ ➔C➔M➔D➔:➔
➔E➔N➔T➔R➔Y➔P➔O➔I➔N➔T➔ ➔[➔"➔n➔o➔d➔e➔"➔]➔
➔C➔M➔D➔ ➔[➔"➔a➔p➔p➔.➔j➔s➔"➔]➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔u➔n➔s➔:➔ ➔n➔o➔d➔e➔ ➔a➔p➔p➔.➔j➔s➔
➔#➔ ➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔m➔y➔i➔m➔a➔g➔e➔ ➔s➔e➔r➔v➔e➔r➔.➔j➔s➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔u➔n➔s➔:➔ ➔n➔o➔d➔e➔ ➔s➔e➔r➔v➔e➔r➔.➔j➔s➔ ➔(➔C➔M➔D➔ ➔o➔v➔e➔r➔r➔i➔d➔d➔e➔n➔)➔
➔#➔ ➔H➔E➔A➔L➔T➔H➔C➔H➔E➔C➔K➔ ➔—➔ ➔h➔o➔w➔ ➔D➔o➔c➔k➔e➔r➔ ➔c➔h➔e➔c➔k➔s➔ ➔i➔f➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔i➔s➔ ➔h➔e➔a➔l➔t➔h➔y➔
➔H➔E➔A➔L➔T➔H➔C➔H➔E➔C➔K➔ ➔-➔-➔i➔n➔t➔e➔r➔v➔a➔l➔=➔3➔0➔s➔ ➔-➔-➔t➔i➔m➔e➔o➔u➔t➔=➔1➔0➔s➔ ➔-➔-➔r➔e➔t➔r➔i➔e➔s➔=➔3➔ ➔\➔
➔ ➔ ➔C➔M➔D➔ ➔c➔u➔r➔l➔ ➔-➔f➔ ➔h➔t➔t➔p➔:➔/➔/➔l➔o➔c➔a➔l➔h➔o➔s➔t➔:➔3➔0➔0➔0➔/➔h➔e➔a➔l➔t➔h➔ ➔|➔|➔ ➔e➔x➔i➔t➔ ➔1➔
➔#➔ ➔O➔N➔B➔U➔I➔L➔D➔ ➔—➔ ➔t➔r➔i➔g➔g➔e➔r➔ ➔i➔n➔s➔t➔r➔u➔c➔t➔i➔o➔n➔s➔ ➔f➔o➔r➔ ➔c➔h➔i➔l➔d➔ ➔i➔m➔a➔g➔e➔s➔
➔O➔N➔B➔U➔I➔L➔D➔ ➔C➔O➔P➔Y➔ ➔.➔ ➔/➔a➔p➔p➔
➔O➔N➔B➔U➔I➔L➔D➔ ➔R➔U➔N➔ ➔n➔p➔m➔ ➔i➔n➔s➔t➔a➔l➔l➔
➔#➔ ➔S➔T➔O➔P➔S➔I➔G➔N➔A➔L➔ ➔—➔ ➔s➔i➔g➔n➔a➔l➔ ➔t➔o➔ ➔s➔t➔o➔p➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔S➔T➔O➔P➔S➔I➔G➔N➔A➔L➔ ➔S➔I➔G➔T➔E➔R➔M➔
➔#➔ ➔S➔H➔E➔L➔L➔ ➔—➔ ➔c➔h➔a➔n➔g➔e➔ ➔d➔e➔f➔a➔u➔l➔t➔ ➔s➔h➔e➔l➔l➔
➔S➔H➔E➔L➔L➔ ➔[➔"➔/➔b➔i➔n➔/➔b➔a➔s➔h➔"➔,➔ ➔"➔-➔c➔"➔]➔
➔C➔o➔m➔p➔l➔e➔t➔e➔ ➔P➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔ ➔E➔x➔a➔m➔p➔l➔e➔:➔
➔#➔ ➔S➔t➔a➔g➔e➔ ➔1➔ ➔-➔ ➔B➔u➔i➔l➔d➔
➔F➔R➔O➔M➔ ➔n➔o➔d➔e➔:➔1➔8➔ ➔A➔S➔ ➔b➔u➔i➔l➔d➔e➔r➔
➔L➔A➔B➔E➔L➔ ➔m➔a➔i➔n➔t➔a➔i➔n➔e➔r➔=➔"➔a➔k➔h➔i➔l➔b➔m➔1➔3➔@➔g➔m➔a➔i➔l➔.➔c➔o➔m➔"➔
➔W➔O➔R➔K➔D➔I➔R➔ ➔/➔a➔p➔p➔
➔C➔O➔P➔Y➔ ➔p➔a➔c➔k➔a➔g➔e➔*➔.➔j➔s➔o➔n➔ ➔.➔/➔
➔R➔U➔N➔ ➔n➔p➔m➔ ➔c➔i➔ ➔-➔-➔o➔n➔l➔y➔=➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔#➔ ➔S➔t➔a➔g➔e➔ ➔2➔ ➔-➔ ➔R➔u➔n➔t➔i➔m➔e➔
➔F➔R➔O➔M➔ ➔n➔o➔d➔e➔:➔1➔8➔-➔a➔l➔p➔i➔n➔e➔
➔E➔N➔V➔ ➔N➔O➔D➔E➔_➔E➔N➔V➔=➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔E➔N➔V➔ ➔P➔O➔R➔T➔=➔3➔0➔0➔0➔
➔W➔O➔R➔K➔D➔I➔R➔ ➔/➔a➔p➔p➔
➔C➔O➔P➔Y➔ ➔-➔-➔f➔r➔o➔m➔=➔b➔u➔i➔l➔d➔e➔r➔ ➔/➔a➔p➔p➔/➔n➔o➔d➔e➔_➔m➔o➔d➔u➔l➔e➔s➔ ➔.➔/➔n➔o➔d➔e➔_➔m➔o➔d➔u➔l➔e➔s➔
➔C➔O➔P➔Y➔ ➔.➔ ➔.➔
➔R➔U➔N➔ ➔u➔s➔e➔r➔a➔d➔d➔ ➔-➔m➔ ➔a➔p➔p➔u➔s➔e➔r➔
➔U➔S➔E➔R➔ ➔a➔p➔p➔u➔s➔e➔r➔
➔E➔X➔P➔O➔S➔E➔ ➔3➔0➔0➔0➔
➔H➔E➔A➔L➔T➔H➔C➔H➔E➔C➔K➔ ➔-➔-➔i➔n➔t➔e➔r➔v➔a➔l➔=➔3➔0➔s➔ ➔C➔M➔D➔ ➔c➔u➔r➔l➔ ➔-➔f➔ ➔h➔t➔t➔p➔:➔/➔/➔l➔o➔c➔a➔l➔h➔o➔s➔t➔:➔3➔0➔0➔0➔/➔h➔e➔a➔l➔t➔h➔ ➔|➔|➔ ➔e➔x➔i➔t➔ ➔1➔
➔C➔M➔D➔ ➔[➔"➔n➔o➔d➔e➔"➔,➔ ➔"➔a➔p➔p➔.➔j➔s➔"➔]➔
➔
➔
➔
➔
➔E➔.➔ ➔D➔o➔c➔k➔e➔r➔ ➔R➔e➔g➔i➔s➔t➔r➔y➔ ➔—➔ ➔C➔o➔m➔p➔l➔e➔t➔e➔ ➔G➔u➔i➔d➔e➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔ ➔D➔o➔c➔k➔e➔r➔ ➔R➔e➔g➔i➔s➔t➔r➔y➔?➔
➔A➔ ➔r➔e➔g➔i➔s➔t➔r➔y➔ ➔i➔s➔ ➔a➔ ➔s➔e➔r➔v➔e➔r➔ ➔t➔h➔a➔t➔ ➔s➔t➔o➔r➔e➔s➔ ➔a➔n➔d➔ ➔d➔i➔s➔t➔r➔i➔b➔u➔t➔e➔s➔ ➔D➔o➔c➔k➔e➔r➔ ➔i➔m➔a➔g➔e➔s➔.➔ ➔T➔h➔i➔n➔k➔ ➔o➔f➔ ➔i➔t➔ ➔l➔i➔k➔e➔ ➔G➔i➔t➔H➔u➔b➔ ➔b➔u➔t➔ ➔f➔o➔r➔ ➔D➔o➔c➔k➔e➔r➔ ➔i➔m➔a➔g➔e➔s➔.➔
➔T➔y➔p➔e➔s➔:➔
➔R➔e➔g➔i➔s➔t➔r➔y➔ ➔T➔y➔p➔e➔ ➔U➔R➔L➔
➔D➔o➔c➔k➔e➔r➔ ➔H➔u➔b➔ ➔P➔u➔b➔l➔i➔c➔/➔P➔r➔i➔v➔a➔t➔e➔ ➔h➔u➔b➔.➔d➔o➔c➔k➔e➔r➔.➔c➔o➔m➔
➔A➔m➔a➔z➔o➔n➔ ➔E➔C➔R➔ ➔P➔r➔i➔v➔a➔t➔e➔ ➔(➔A➔W➔S➔)➔ ➔A➔W➔S➔ ➔C➔o➔n➔s➔o➔l➔e➔
➔A➔z➔u➔r➔e➔ ➔A➔C➔R➔ ➔P➔r➔i➔v➔a➔t➔e➔ ➔(➔A➔z➔u➔r➔e➔)➔ ➔A➔z➔u➔r➔e➔ ➔P➔o➔r➔t➔a➔l➔
➔G➔i➔t➔H➔u➔b➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔R➔e➔g➔i➔s➔t➔r➔y➔ ➔P➔r➔i➔v➔a➔t➔e➔ ➔g➔h➔c➔r➔.➔i➔o➔
➔H➔a➔r➔b➔o➔r➔ ➔S➔e➔l➔f➔-➔h➔o➔s➔t➔e➔d➔ ➔Y➔o➔u➔r➔ ➔s➔e➔r➔v➔e➔r➔
➔D➔o➔c➔k➔e➔r➔ ➔H➔u➔b➔ ➔—➔ ➔A➔l➔l➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔:➔
➔#➔ ➔L➔o➔g➔i➔n➔ ➔/➔ ➔L➔o➔g➔o➔u➔t➔
➔d➔o➔c➔k➔e➔r➔ ➔l➔o➔g➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔o➔g➔i➔n➔ ➔t➔o➔ ➔D➔o➔c➔k➔e➔r➔ ➔H➔u➔b➔
➔d➔o➔c➔k➔e➔r➔ ➔l➔o➔g➔i➔n➔ ➔-➔u➔ ➔a➔k➔h➔i➔l➔ ➔-➔p➔ ➔m➔y➔p➔a➔s➔s➔w➔o➔r➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔w➔i➔t➔h➔ ➔c➔r➔e➔d➔e➔n➔t➔i➔a➔l➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔l➔o➔g➔i➔n➔ ➔r➔e➔g➔i➔s➔t➔r➔y➔.➔e➔x➔a➔m➔p➔l➔e➔.➔c➔o➔m➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔o➔g➔i➔n➔ ➔t➔o➔ ➔p➔r➔i➔v➔a➔t➔e➔ ➔r➔e➔g➔i➔s➔t➔r➔y➔
➔d➔o➔c➔k➔e➔r➔ ➔l➔o➔g➔o➔u➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔o➔g➔o➔u➔t➔
➔#➔ ➔S➔e➔a➔r➔c➔h➔
➔d➔o➔c➔k➔e➔r➔ ➔s➔e➔a➔r➔c➔h➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔a➔r➔c➔h➔ ➔D➔o➔c➔k➔e➔r➔ ➔H➔u➔b➔
➔d➔o➔c➔k➔e➔r➔ ➔s➔e➔a➔r➔c➔h➔ ➔-➔-➔f➔i➔l➔t➔e➔r➔=➔s➔t➔a➔r➔s➔=➔1➔0➔0➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔l➔t➔e➔r➔ ➔b➔y➔ ➔s➔t➔a➔r➔s➔
➔#➔ ➔P➔u➔l➔l➔
➔d➔o➔c➔k➔e➔r➔ ➔p➔u➔l➔l➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔a➔t➔e➔s➔t➔ ➔t➔a➔g➔
➔d➔o➔c➔k➔e➔r➔ ➔p➔u➔l➔l➔ ➔n➔g➔i➔n➔x➔:➔1➔.➔2➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔v➔e➔r➔s➔i➔o➔n➔
➔d➔o➔c➔k➔e➔r➔ ➔p➔u➔l➔l➔ ➔u➔b➔u➔n➔t➔u➔:➔2➔2➔.➔0➔4➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔O➔S➔ ➔v➔e➔r➔s➔i➔o➔n➔
➔#➔ ➔T➔a➔g➔
➔d➔o➔c➔k➔e➔r➔ ➔t➔a➔g➔ ➔m➔y➔a➔p➔p➔:➔l➔a➔t➔e➔s➔t➔ ➔a➔k➔h➔i➔l➔/➔m➔y➔a➔p➔p➔:➔1➔.➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔t➔a➔g➔ ➔f➔o➔r➔ ➔D➔o➔c➔k➔e➔r➔ ➔H➔u➔b➔
➔d➔o➔c➔k➔e➔r➔ ➔t➔a➔g➔ ➔m➔y➔a➔p➔p➔:➔l➔a➔t➔e➔s➔t➔ ➔1➔2➔3➔4➔5➔6➔.➔d➔k➔r➔.➔e➔c➔r➔.➔u➔s➔-➔e➔a➔s➔t➔-➔1➔.➔a➔m➔a➔z➔o➔n➔a➔w➔s➔.➔c➔o➔m➔/➔m➔y➔a➔p➔p➔:➔1➔.➔0➔ ➔ ➔#➔ ➔f➔o➔r➔ ➔E➔C➔R➔
➔#➔ ➔P➔u➔s➔h➔
➔d➔o➔c➔k➔e➔r➔ ➔p➔u➔s➔h➔ ➔a➔k➔h➔i➔l➔/➔m➔y➔a➔p➔p➔:➔1➔.➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔u➔s➔h➔ ➔t➔o➔ ➔D➔o➔c➔k➔e➔r➔ ➔H➔u➔b➔
➔d➔o➔c➔k➔e➔r➔ ➔p➔u➔s➔h➔ ➔1➔2➔3➔4➔5➔6➔.➔d➔k➔r➔.➔e➔c➔r➔.➔u➔s➔-➔e➔a➔s➔t➔-➔1➔.➔a➔m➔a➔z➔o➔n➔a➔w➔s➔.➔c➔o➔m➔/➔m➔y➔a➔p➔p➔:➔1➔.➔0➔ ➔ ➔#➔ ➔p➔u➔s➔h➔ ➔t➔o➔ ➔E➔C➔R➔
➔#➔ ➔L➔o➔g➔i➔n➔ ➔t➔o➔ ➔A➔W➔S➔ ➔E➔C➔R➔
➔a➔w➔s➔ ➔e➔c➔r➔ ➔g➔e➔t➔-➔l➔o➔g➔i➔n➔-➔p➔a➔s➔s➔w➔o➔r➔d➔ ➔-➔-➔r➔e➔g➔i➔o➔n➔ ➔u➔s➔-➔e➔a➔s➔t➔-➔1➔ ➔|➔ ➔\➔
➔
➔
➔
➔
➔➔ ➔➔
➔ ➔ ➔d➔o➔c➔k➔e➔r➔ ➔l➔o➔g➔i➔n➔ ➔-➔-➔u➔s➔e➔r➔n➔a➔m➔e➔ ➔A➔W➔S➔ ➔-➔-➔p➔a➔s➔s➔w➔o➔r➔d➔-➔s➔t➔d➔i➔n➔ ➔\➔
➔ ➔ ➔1➔2➔3➔4➔5➔6➔7➔8➔9➔.➔d➔k➔r➔.➔e➔c➔r➔.➔u➔s➔-➔e➔a➔s➔t➔-➔1➔.➔a➔m➔a➔z➔o➔n➔a➔w➔s➔.➔c➔o➔m➔
➔F➔.➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔L➔i➔f➔e➔c➔y➔c➔l➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔ ➔c➔r➔e➔a➔t➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔↓➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔C➔R➔E➔A➔T➔E➔D➔ ➔ ➔ ➔│➔ ➔←➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔c➔r➔e➔a➔t➔e➔d➔ ➔b➔u➔t➔ ➔n➔o➔t➔ ➔s➔t➔a➔r➔t➔e➔d➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔┬➔─➔─➔─➔─➔─➔─➔┘➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔d➔o➔c➔k➔e➔r➔ ➔s➔t➔a➔r➔t➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔↓➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔R➔U➔N➔N➔I➔N➔G➔ ➔ ➔ ➔│➔ ➔←➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔i➔s➔ ➔e➔x➔e➔c➔u➔t➔i➔n➔g➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔┬➔─➔─➔─➔─➔─➔─➔┘➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔┴➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔ ➔p➔a➔u➔s➔e➔ ➔ ➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔ ➔s➔t➔o➔p➔/➔k➔i➔l➔l➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔▼➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔▼➔
➔ ➔ ➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔ ➔P➔A➔U➔S➔E➔D➔ ➔ ➔ ➔ ➔│➔ ➔ ➔│➔ ➔ ➔ ➔S➔T➔O➔P➔P➔E➔D➔ ➔ ➔ ➔│➔ ➔←➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔s➔t➔o➔p➔p➔e➔d➔
➔ ➔ ➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔┬➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔┬➔─➔─➔─➔─➔─➔─➔┘➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔ ➔u➔n➔p➔a➔u➔s➔e➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔ ➔s➔t➔a➔r➔t➔ ➔(➔r➔e➔s➔t➔a➔r➔t➔)➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔┬➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔↓➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔R➔U➔N➔N➔I➔N➔G➔ ➔ ➔ ➔│➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔ ➔r➔m➔ ➔→➔ ➔D➔E➔L➔E➔T➔E➔D➔
➔L➔i➔f➔e➔c➔y➔c➔l➔e➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔:➔
➔#➔ ➔C➔r➔e➔a➔t➔e➔ ➔(➔w➔i➔t➔h➔o➔u➔t➔ ➔s➔t➔a➔r➔t➔i➔n➔g➔)➔
➔d➔o➔c➔k➔e➔r➔ ➔c➔r➔e➔a➔t➔e➔ ➔-➔-➔n➔a➔m➔e➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔n➔g➔i➔n➔x➔
➔#➔ ➔S➔t➔a➔r➔t➔
➔d➔o➔c➔k➔e➔r➔ ➔s➔t➔a➔r➔t➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔#➔ ➔R➔u➔n➔ ➔(➔c➔r➔e➔a➔t➔e➔ ➔+➔ ➔s➔t➔a➔r➔t➔ ➔i➔n➔ ➔o➔n➔e➔ ➔s➔t➔e➔p➔ ➔—➔ ➔m➔o➔s➔t➔ ➔c➔o➔m➔m➔o➔n➔)➔
➔
➔
➔
➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔u➔n➔s➔ ➔i➔n➔ ➔f➔o➔r➔e➔g➔r➔o➔u➔n➔d➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔t➔a➔c➔h➔e➔d➔ ➔(➔b➔a➔c➔k➔g➔r➔o➔u➔n➔d➔)➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔-➔n➔a➔m➔e➔ ➔w➔e➔b➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔w➔i➔t➔h➔ ➔n➔a➔m➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔p➔ ➔8➔0➔8➔0➔:➔8➔0➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔w➔i➔t➔h➔ ➔p➔o➔r➔t➔ ➔m➔a➔p➔p➔i➔n➔g➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔e➔ ➔E➔N➔V➔=➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔m➔y➔a➔p➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔w➔i➔t➔h➔ ➔e➔n➔v➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔v➔ ➔m➔y➔v➔o➔l➔u➔m➔e➔:➔/➔d➔a➔t➔a➔ ➔m➔y➔a➔p➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔w➔i➔t➔h➔ ➔v➔o➔l➔u➔m➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔-➔r➔m➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔u➔t➔o➔-➔r➔e➔m➔o➔v➔e➔ ➔w➔h➔e➔n➔ ➔s➔t➔o➔p➔p➔e➔d➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔i➔t➔ ➔u➔b➔u➔n➔t➔u➔ ➔b➔a➔s➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔i➔n➔t➔e➔r➔a➔c➔t➔i➔v➔e➔ ➔t➔e➔r➔m➔i➔n➔a➔l➔
➔#➔ ➔S➔t➔o➔p➔ ➔(➔g➔r➔a➔c➔e➔f➔u➔l➔ ➔—➔ ➔s➔e➔n➔d➔s➔ ➔S➔I➔G➔T➔E➔R➔M➔,➔ ➔w➔a➔i➔t➔s➔,➔ ➔t➔h➔e➔n➔ ➔S➔I➔G➔K➔I➔L➔L➔)➔
➔d➔o➔c➔k➔e➔r➔ ➔s➔t➔o➔p➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔d➔o➔c➔k➔e➔r➔ ➔s➔t➔o➔p➔ ➔-➔t➔ ➔3➔0➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔w➔a➔i➔t➔ ➔3➔0➔ ➔s➔e➔c➔o➔n➔d➔s➔ ➔b➔e➔f➔o➔r➔e➔ ➔k➔i➔l➔l➔
➔#➔ ➔K➔i➔l➔l➔ ➔(➔i➔m➔m➔e➔d➔i➔a➔t➔e➔ ➔—➔ ➔s➔e➔n➔d➔s➔ ➔S➔I➔G➔K➔I➔L➔L➔)➔
➔d➔o➔c➔k➔e➔r➔ ➔k➔i➔l➔l➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔#➔ ➔R➔e➔s➔t➔a➔r➔t➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔e➔s➔t➔a➔r➔t➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔#➔ ➔P➔a➔u➔s➔e➔ ➔/➔ ➔U➔n➔p➔a➔u➔s➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔p➔a➔u➔s➔e➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔d➔o➔c➔k➔e➔r➔ ➔u➔n➔p➔a➔u➔s➔e➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔#➔ ➔R➔e➔m➔o➔v➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔m➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔s➔t➔o➔p➔p➔e➔d➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔m➔ ➔-➔f➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔r➔c➔e➔ ➔r➔e➔m➔o➔v➔e➔ ➔r➔u➔n➔n➔i➔n➔g➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔m➔ ➔$➔(➔d➔o➔c➔k➔e➔r➔ ➔p➔s➔ ➔-➔a➔q➔)➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔A➔L➔L➔ ➔s➔t➔o➔p➔p➔e➔d➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔p➔r➔u➔n➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔a➔l➔l➔ ➔s➔t➔o➔p➔p➔e➔d➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔
➔#➔ ➔V➔i➔e➔w➔
➔d➔o➔c➔k➔e➔r➔ ➔p➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔u➔n➔n➔i➔n➔g➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔p➔s➔ ➔-➔a➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔l➔l➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔(➔i➔n➔c➔l➔u➔d➔i➔n➔g➔ ➔s➔t➔o➔p➔p➔e➔d➔)➔
➔d➔o➔c➔k➔e➔r➔ ➔p➔s➔ ➔-➔q➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔o➔n➔l➔y➔ ➔I➔D➔s➔
➔#➔ ➔I➔n➔s➔p➔e➔c➔t➔ ➔a➔n➔d➔ ➔D➔e➔b➔u➔g➔
➔d➔o➔c➔k➔e➔r➔ ➔i➔n➔s➔p➔e➔c➔t➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔u➔l➔l➔ ➔J➔S➔O➔N➔ ➔d➔e➔t➔a➔i➔l➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔l➔o➔g➔s➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔o➔g➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔l➔o➔g➔s➔ ➔-➔f➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔l➔l➔o➔w➔ ➔l➔o➔g➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔l➔o➔g➔s➔ ➔-➔-➔t➔a➔i➔l➔ ➔5➔0➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔a➔s➔t➔ ➔5➔0➔ ➔l➔i➔n➔e➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔e➔x➔e➔c➔ ➔-➔i➔t➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔b➔a➔s➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔e➔l➔l➔ ➔i➔n➔s➔i➔d➔e➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔d➔o➔c➔k➔e➔r➔ ➔e➔x➔e➔c➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔l➔s➔ ➔/➔a➔p➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔u➔n➔ ➔c➔o➔m➔m➔a➔n➔d➔ ➔w➔i➔t➔h➔o➔u➔t➔ ➔s➔h➔e➔l➔l➔
➔d➔o➔c➔k➔e➔r➔ ➔t➔o➔p➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔r➔o➔c➔e➔s➔s➔e➔s➔ ➔i➔n➔s➔i➔d➔e➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔d➔o➔c➔k➔e➔r➔ ➔s➔t➔a➔t➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔v➔e➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔u➔s➔a➔g➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔s➔t➔a➔t➔s➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔s➔t➔a➔t➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔d➔i➔f➔f➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔l➔e➔s➔ ➔c➔h➔a➔n➔g➔e➔d➔ ➔v➔s➔ ➔i➔m➔a➔g➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔c➔p➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔:➔/➔a➔p➔p➔/➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔.➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔p➔y➔ ➔f➔i➔l➔e➔ ➔f➔r➔o➔m➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔d➔o➔c➔k➔e➔r➔ ➔c➔p➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔:➔/➔a➔p➔p➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔p➔y➔ ➔f➔i➔l➔e➔ ➔t➔o➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔
➔
➔
➔
➔G➔.➔ ➔P➔o➔r➔t➔ ➔M➔a➔p➔p➔i➔n➔g➔
➔W➔h➔y➔ ➔p➔o➔r➔t➔ ➔m➔a➔p➔p➔i➔n➔g➔?➔
➔C➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔r➔u➔n➔ ➔i➔n➔ ➔t➔h➔e➔i➔r➔ ➔o➔w➔n➔ ➔i➔s➔o➔l➔a➔t➔e➔d➔ ➔n➔e➔t➔w➔o➔r➔k➔.➔ ➔P➔o➔r➔t➔ ➔m➔a➔p➔p➔i➔n➔g➔ ➔c➔o➔n➔n➔e➔c➔t➔s➔ ➔a➔ ➔p➔o➔r➔t➔ ➔o➔n➔ ➔y➔o➔u➔r➔ ➔h➔o➔s➔t➔ ➔m➔a➔c➔h➔i➔n➔e➔ ➔t➔o➔ ➔a➔ ➔p➔o➔r➔t➔
➔i➔n➔s➔i➔d➔e➔ ➔t➔h➔e➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔.➔
➔H➔o➔s➔t➔ ➔M➔a➔c➔h➔i➔n➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔
➔ ➔ ➔ ➔:➔8➔0➔8➔0➔ ➔ ➔ ➔ ➔─➔─➔─➔─➔─➔─➔─➔─➔ ➔▶➔ ➔ ➔ ➔ ➔:➔3➔0➔0➔0➔
➔ ➔ ➔ ➔:➔8➔0➔8➔1➔ ➔ ➔ ➔ ➔─➔─➔─➔─➔─➔─➔─➔─➔ ➔▶➔ ➔ ➔ ➔ ➔:➔3➔0➔0➔0➔ ➔ ➔(➔t➔w➔o➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔,➔ ➔s➔a➔m➔e➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔p➔o➔r➔t➔)➔
➔ ➔ ➔ ➔:➔5➔4➔3➔2➔ ➔ ➔ ➔ ➔─➔─➔─➔─➔─➔─➔─➔─➔ ➔▶➔ ➔ ➔ ➔ ➔:➔5➔4➔3➔2➔
➔#➔ ➔-➔p➔ ➔h➔o➔s➔t➔P➔o➔r➔t➔:➔c➔o➔n➔t➔a➔i➔n➔e➔r➔P➔o➔r➔t➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔p➔ ➔8➔0➔8➔0➔:➔3➔0➔0➔0➔ ➔m➔y➔a➔p➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔h➔o➔s➔t➔ ➔8➔0➔8➔0➔ ➔→➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔3➔0➔0➔0➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔p➔ ➔8➔0➔:➔8➔0➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔h➔o➔s➔t➔ ➔8➔0➔ ➔→➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔8➔0➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔p➔ ➔5➔4➔3➔2➔:➔5➔4➔3➔2➔ ➔p➔o➔s➔t➔g➔r➔e➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔a➔t➔a➔b➔a➔s➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔p➔ ➔8➔0➔8➔0➔:➔8➔0➔ ➔-➔p➔ ➔8➔4➔4➔3➔:➔4➔4➔3➔ ➔n➔g➔i➔n➔x➔ ➔#➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔p➔o➔r➔t➔s➔
➔#➔ ➔-➔P➔ ➔(➔c➔a➔p➔i➔t➔a➔l➔ ➔P➔)➔ ➔—➔ ➔p➔u➔b➔l➔i➔s➔h➔ ➔A➔L➔L➔ ➔e➔x➔p➔o➔s➔e➔d➔ ➔p➔o➔r➔t➔s➔ ➔t➔o➔ ➔r➔a➔n➔d➔o➔m➔ ➔h➔o➔s➔t➔ ➔p➔o➔r➔t➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔P➔ ➔n➔g➔i➔n➔x➔
➔#➔ ➔C➔h➔e➔c➔k➔ ➔p➔o➔r➔t➔ ➔m➔a➔p➔p➔i➔n➔g➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔p➔o➔r➔t➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔e➔ ➔a➔l➔l➔ ➔p➔o➔r➔t➔ ➔m➔a➔p➔p➔i➔n➔g➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔p➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔s➔ ➔p➔o➔r➔t➔s➔ ➔i➔n➔ ➔o➔u➔t➔p➔u➔t➔
➔#➔ ➔B➔i➔n➔d➔ ➔t➔o➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔h➔o➔s➔t➔ ➔I➔P➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔p➔ ➔1➔2➔7➔.➔0➔.➔0➔.➔1➔:➔8➔0➔8➔0➔:➔8➔0➔ ➔n➔g➔i➔n➔x➔ ➔ ➔#➔ ➔o➔n➔l➔y➔ ➔l➔o➔c➔a➔l➔h➔o➔s➔t➔ ➔c➔a➔n➔ ➔a➔c➔c➔e➔s➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔p➔ ➔0➔.➔0➔.➔0➔.➔0➔:➔8➔0➔8➔0➔:➔8➔0➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔#➔ ➔a➔n➔y➔ ➔I➔P➔ ➔c➔a➔n➔ ➔a➔c➔c➔e➔s➔s➔ ➔(➔d➔e➔f➔a➔u➔l➔t➔)➔
➔H➔.➔ ➔C➔r➔e➔a➔t➔i➔n➔g➔ ➔I➔m➔a➔g➔e➔ ➔f➔r➔o➔m➔ ➔a➔ ➔R➔u➔n➔n➔i➔n➔g➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔
➔S➔o➔m➔e➔t➔i➔m➔e➔s➔ ➔y➔o➔u➔ ➔m➔a➔k➔e➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔i➔n➔s➔i➔d➔e➔ ➔a➔ ➔r➔u➔n➔n➔i➔n➔g➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔a➔n➔d➔ ➔w➔a➔n➔t➔ ➔t➔o➔ ➔s➔a➔v➔e➔ ➔t➔h➔a➔t➔ ➔a➔s➔ ➔a➔ ➔n➔e➔w➔ ➔i➔m➔a➔g➔e➔.➔
➔#➔ ➔S➔t➔e➔p➔ ➔1➔ ➔—➔ ➔R➔u➔n➔ ➔a➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔a➔n➔d➔ ➔m➔a➔k➔e➔ ➔c➔h➔a➔n➔g➔e➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔i➔t➔ ➔u➔b➔u➔n➔t➔u➔ ➔b➔a➔s➔h➔
➔#➔ ➔I➔n➔s➔i➔d➔e➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔:➔
➔a➔p➔t➔-➔g➔e➔t➔ ➔u➔p➔d➔a➔t➔e➔ ➔&➔&➔ ➔a➔p➔t➔-➔g➔e➔t➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔-➔y➔ ➔n➔g➔i➔n➔x➔
➔e➔x➔i➔t➔
➔#➔ ➔S➔t➔e➔p➔ ➔2➔ ➔—➔ ➔C➔o➔m➔m➔i➔t➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔a➔s➔ ➔n➔e➔w➔ ➔i➔m➔a➔g➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔c➔o➔m➔m➔i➔t➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔_➔n➔a➔m➔e➔ ➔m➔y➔i➔m➔a➔g➔e➔:➔v➔1➔
➔
➔
➔
➔
➔d➔o➔c➔k➔e➔r➔ ➔c➔o➔m➔m➔i➔t➔ ➔-➔m➔ ➔"➔A➔d➔d➔e➔d➔ ➔n➔g➔i➔n➔x➔"➔ ➔-➔a➔ ➔"➔A➔k➔h➔i➔l➔"➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔_➔n➔a➔m➔e➔ ➔m➔y➔i➔m➔a➔g➔e➔:➔v➔1➔
➔#➔ ➔S➔t➔e➔p➔ ➔3➔ ➔—➔ ➔V➔e➔r➔i➔f➔y➔
➔d➔o➔c➔k➔e➔r➔ ➔i➔m➔a➔g➔e➔s➔ ➔ ➔ ➔ ➔#➔ ➔y➔o➔u➔'➔l➔l➔ ➔s➔e➔e➔ ➔m➔y➔i➔m➔a➔g➔e➔:➔v➔1➔
➔#➔ ➔N➔o➔t➔e➔:➔ ➔T➔h➔i➔s➔ ➔i➔s➔ ➔N➔O➔T➔ ➔b➔e➔s➔t➔ ➔p➔r➔a➔c➔t➔i➔c➔e➔ ➔—➔ ➔a➔l➔w➔a➔y➔s➔ ➔u➔s➔e➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔ ➔f➔o➔r➔ ➔r➔e➔p➔r➔o➔d➔u➔c➔i➔b➔i➔l➔i➔t➔y➔
➔#➔ ➔U➔s➔e➔ ➔c➔o➔m➔m➔i➔t➔ ➔o➔n➔l➔y➔ ➔f➔o➔r➔ ➔q➔u➔i➔c➔k➔ ➔d➔e➔b➔u➔g➔g➔i➔n➔g➔ ➔o➔r➔ ➔t➔e➔s➔t➔i➔n➔g➔
➔I➔.➔ ➔F➔u➔l➔l➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔W➔o➔r➔k➔f➔l➔o➔w➔ ➔—➔ ➔D➔o➔c➔k➔e➔r➔ ➔O➔n➔l➔y➔
➔S➔c➔e➔n➔a➔r➔i➔o➔:➔ ➔Y➔o➔u➔ ➔h➔a➔v➔e➔ ➔a➔ ➔N➔o➔d➔e➔.➔j➔s➔ ➔a➔p➔p➔.➔ ➔D➔e➔p➔l➔o➔y➔ ➔i➔t➔ ➔u➔s➔i➔n➔g➔ ➔D➔o➔c➔k➔e➔r➔.➔
➔#➔ ➔─➔─➔ ➔S➔T➔E➔P➔ ➔1➔:➔ ➔C➔l➔o➔n➔e➔ ➔y➔o➔u➔r➔ ➔c➔o➔d➔e➔ ➔─➔─➔
➔g➔i➔t➔ ➔c➔l➔o➔n➔e➔ ➔h➔t➔t➔p➔s➔:➔/➔/➔g➔i➔t➔h➔u➔b➔.➔c➔o➔m➔/➔a➔k➔h➔i➔l➔/➔m➔y➔a➔p➔p➔.➔g➔i➔t➔
➔c➔d➔ ➔m➔y➔a➔p➔p➔
➔#➔ ➔─➔─➔ ➔S➔T➔E➔P➔ ➔2➔:➔ ➔W➔r➔i➔t➔e➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔ ➔─➔─➔
➔c➔a➔t➔ ➔>➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔ ➔<➔<➔ ➔'➔E➔O➔F➔'➔
➔F➔R➔O➔M➔ ➔n➔o➔d➔e➔:➔1➔8➔-➔a➔l➔p➔i➔n➔e➔
➔W➔O➔R➔K➔D➔I➔R➔ ➔/➔a➔p➔p➔
➔C➔O➔P➔Y➔ ➔p➔a➔c➔k➔a➔g➔e➔*➔.➔j➔s➔o➔n➔ ➔.➔/➔
➔R➔U➔N➔ ➔n➔p➔m➔ ➔i➔n➔s➔t➔a➔l➔l➔
➔C➔O➔P➔Y➔ ➔.➔ ➔.➔
➔E➔X➔P➔O➔S➔E➔ ➔3➔0➔0➔0➔
➔C➔M➔D➔ ➔[➔"➔n➔o➔d➔e➔"➔,➔ ➔"➔a➔p➔p➔.➔j➔s➔"➔]➔
➔E➔O➔F➔
➔#➔ ➔─➔─➔ ➔S➔T➔E➔P➔ ➔3➔:➔ ➔B➔u➔i➔l➔d➔ ➔D➔o➔c➔k➔e➔r➔ ➔i➔m➔a➔g➔e➔ ➔─➔─➔
➔d➔o➔c➔k➔e➔r➔ ➔b➔u➔i➔l➔d➔ ➔-➔t➔ ➔m➔y➔a➔p➔p➔:➔1➔.➔0➔ ➔.➔
➔d➔o➔c➔k➔e➔r➔ ➔b➔u➔i➔l➔d➔ ➔-➔t➔ ➔m➔y➔a➔p➔p➔:➔1➔.➔0➔ ➔-➔f➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔.➔p➔r➔o➔d➔ ➔.➔ ➔ ➔ ➔#➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔d➔o➔c➔k➔e➔r➔f➔i➔l➔e➔
➔#➔ ➔─➔─➔ ➔S➔T➔E➔P➔ ➔4➔:➔ ➔T➔e➔s➔t➔ ➔l➔o➔c➔a➔l➔l➔y➔ ➔─➔─➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔p➔ ➔3➔0➔0➔0➔:➔3➔0➔0➔0➔ ➔-➔-➔n➔a➔m➔e➔ ➔m➔y➔a➔p➔p➔ ➔m➔y➔a➔p➔p➔:➔1➔.➔0➔
➔c➔u➔r➔l➔ ➔h➔t➔t➔p➔:➔/➔/➔l➔o➔c➔a➔l➔h➔o➔s➔t➔:➔3➔0➔0➔0➔ ➔ ➔ ➔ ➔#➔ ➔v➔e➔r➔i➔f➔y➔ ➔i➔t➔ ➔w➔o➔r➔k➔s➔
➔#➔ ➔─➔─➔ ➔S➔T➔E➔P➔ ➔5➔:➔ ➔T➔a➔g➔ ➔f➔o➔r➔ ➔D➔o➔c➔k➔e➔r➔ ➔H➔u➔b➔ ➔─➔─➔
➔d➔o➔c➔k➔e➔r➔ ➔t➔a➔g➔ ➔m➔y➔a➔p➔p➔:➔1➔.➔0➔ ➔a➔k➔h➔i➔l➔/➔m➔y➔a➔p➔p➔:➔1➔.➔0➔
➔#➔ ➔─➔─➔ ➔S➔T➔E➔P➔ ➔6➔:➔ ➔L➔o➔g➔i➔n➔ ➔a➔n➔d➔ ➔P➔u➔s➔h➔ ➔─➔─➔
➔d➔o➔c➔k➔e➔r➔ ➔l➔o➔g➔i➔n➔
➔d➔o➔c➔k➔e➔r➔ ➔p➔u➔s➔h➔ ➔a➔k➔h➔i➔l➔/➔m➔y➔a➔p➔p➔:➔1➔.➔0➔
➔#➔ ➔─➔─➔ ➔S➔T➔E➔P➔ ➔7➔:➔ ➔O➔n➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔s➔e➔r➔v➔e➔r➔ ➔—➔ ➔p➔u➔l➔l➔ ➔a➔n➔d➔ ➔r➔u➔n➔ ➔─➔─➔
➔
➔
➔
➔
➔d➔o➔c➔k➔e➔r➔ ➔p➔u➔l➔l➔ ➔a➔k➔h➔i➔l➔/➔m➔y➔a➔p➔p➔:➔1➔.➔0➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔p➔ ➔8➔0➔:➔3➔0➔0➔0➔ ➔-➔-➔n➔a➔m➔e➔ ➔m➔y➔a➔p➔p➔ ➔a➔k➔h➔i➔l➔/➔m➔y➔a➔p➔p➔:➔1➔.➔0➔
➔J➔.➔ ➔F➔u➔l➔l➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔W➔o➔r➔k➔f➔l➔o➔w➔ ➔—➔ ➔D➔o➔c➔k➔e➔r➔ ➔+➔ ➔J➔e➔n➔k➔i➔n➔s➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔
➔C➔o➔m➔p➔l➔e➔t➔e➔ ➔J➔e➔n➔k➔i➔n➔s➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔f➔o➔r➔ ➔D➔o➔c➔k➔e➔r➔:➔
➔/➔/➔ ➔J➔e➔n➔k➔i➔n➔s➔f➔i➔l➔e➔
➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔{➔
➔ ➔ ➔ ➔ ➔a➔g➔e➔n➔t➔ ➔a➔n➔y➔
➔ ➔ ➔ ➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔D➔O➔C➔K➔E➔R➔_➔H➔U➔B➔_➔C➔R➔E➔D➔S➔ ➔=➔ ➔c➔r➔e➔d➔e➔n➔t➔i➔a➔l➔s➔(➔'➔d➔o➔c➔k➔e➔r➔-➔h➔u➔b➔-➔c➔r➔e➔d➔e➔n➔t➔i➔a➔l➔s➔'➔)➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔I➔M➔A➔G➔E➔_➔N➔A➔M➔E➔ ➔=➔ ➔"➔a➔k➔h➔i➔l➔/➔m➔y➔a➔p➔p➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔I➔M➔A➔G➔E➔_➔T➔A➔G➔ ➔=➔ ➔"➔$➔{➔B➔U➔I➔L➔D➔_➔N➔U➔M➔B➔E➔R➔}➔"➔ ➔ ➔ ➔ ➔ ➔/➔/➔ ➔u➔s➔e➔ ➔J➔e➔n➔k➔i➔n➔s➔ ➔b➔u➔i➔l➔d➔ ➔n➔u➔m➔b➔e➔r➔ ➔a➔s➔ ➔t➔a➔g➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔S➔O➔N➔A➔R➔_➔T➔O➔K➔E➔N➔ ➔=➔ ➔c➔r➔e➔d➔e➔n➔t➔i➔a➔l➔s➔(➔'➔s➔o➔n➔a➔r➔-➔t➔o➔k➔e➔n➔'➔)➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔N➔E➔X➔U➔S➔_➔C➔R➔E➔D➔S➔ ➔=➔ ➔c➔r➔e➔d➔e➔n➔t➔i➔a➔l➔s➔(➔'➔n➔e➔x➔u➔s➔-➔c➔r➔e➔d➔e➔n➔t➔i➔a➔l➔s➔'➔)➔
➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔s➔t➔a➔g➔e➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔/➔/➔ ➔─➔─➔ ➔S➔T➔A➔G➔E➔ ➔1➔:➔ ➔C➔l➔o➔n➔e➔ ➔C➔o➔d➔e➔ ➔─➔─➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔g➔e➔(➔'➔C➔l➔o➔n➔e➔ ➔C➔o➔d➔e➔'➔)➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔g➔i➔t➔ ➔b➔r➔a➔n➔c➔h➔:➔ ➔'➔m➔a➔i➔n➔'➔,➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔u➔r➔l➔:➔ ➔'➔h➔t➔t➔p➔s➔:➔/➔/➔g➔i➔t➔h➔u➔b➔.➔c➔o➔m➔/➔a➔k➔h➔i➔l➔/➔m➔y➔a➔p➔p➔.➔g➔i➔t➔'➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔/➔/➔ ➔─➔─➔ ➔S➔T➔A➔G➔E➔ ➔2➔:➔ ➔B➔u➔i➔l➔d➔ ➔C➔o➔d➔e➔ ➔─➔─➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔g➔e➔(➔'➔B➔u➔i➔l➔d➔ ➔C➔o➔d➔e➔'➔)➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔h➔ ➔'➔n➔p➔m➔ ➔i➔n➔s➔t➔a➔l➔l➔'➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔h➔ ➔'➔n➔p➔m➔ ➔r➔u➔n➔ ➔b➔u➔i➔l➔d➔'➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔/➔/➔ ➔─➔─➔ ➔S➔T➔A➔G➔E➔ ➔3➔:➔ ➔S➔o➔n➔a➔r➔Q➔u➔b➔e➔ ➔A➔n➔a➔l➔y➔s➔i➔s➔ ➔─➔─➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔g➔e➔(➔'➔S➔o➔n➔a➔r➔Q➔u➔b➔e➔ ➔A➔n➔a➔l➔y➔s➔i➔s➔'➔)➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔w➔i➔t➔h➔S➔o➔n➔a➔r➔Q➔u➔b➔e➔E➔n➔v➔(➔'➔S➔o➔n➔a➔r➔Q➔u➔b➔e➔'➔)➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔h➔ ➔'➔'➔'➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔o➔n➔a➔r➔-➔s➔c➔a➔n➔n➔e➔r➔ ➔\➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔D➔s➔o➔n➔a➔r➔.➔p➔r➔o➔j➔e➔c➔t➔K➔e➔y➔=➔m➔y➔a➔p➔p➔ ➔\➔
➔
➔
➔
➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔D➔s➔o➔n➔a➔r➔.➔s➔o➔u➔r➔c➔e➔s➔=➔.➔ ➔\➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔D➔s➔o➔n➔a➔r➔.➔h➔o➔s➔t➔.➔u➔r➔l➔=➔h➔t➔t➔p➔:➔/➔/➔s➔o➔n➔a➔r➔q➔u➔b➔e➔:➔9➔0➔0➔0➔ ➔\➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔D➔s➔o➔n➔a➔r➔.➔l➔o➔g➔i➔n➔=➔$➔{➔S➔O➔N➔A➔R➔_➔T➔O➔K➔E➔N➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔'➔'➔'➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔/➔/➔ ➔─➔─➔ ➔S➔T➔A➔G➔E➔ ➔4➔:➔ ➔Q➔u➔a➔l➔i➔t➔y➔ ➔G➔a➔t➔e➔ ➔─➔─➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔g➔e➔(➔'➔Q➔u➔a➔l➔i➔t➔y➔ ➔G➔a➔t➔e➔'➔)➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔w➔a➔i➔t➔F➔o➔r➔Q➔u➔a➔l➔i➔t➔y➔G➔a➔t➔e➔ ➔a➔b➔o➔r➔t➔P➔i➔p➔e➔l➔i➔n➔e➔:➔ ➔t➔r➔u➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔/➔/➔ ➔─➔─➔ ➔S➔T➔A➔G➔E➔ ➔5➔:➔ ➔U➔p➔l➔o➔a➔d➔ ➔t➔o➔ ➔N➔e➔x➔u➔s➔ ➔─➔─➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔g➔e➔(➔'➔U➔p➔l➔o➔a➔d➔ ➔A➔r➔t➔i➔f➔a➔c➔t➔ ➔t➔o➔ ➔N➔e➔x➔u➔s➔'➔)➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔h➔ ➔'➔'➔'➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔c➔u➔r➔l➔ ➔-➔u➔ ➔$➔{➔N➔E➔X➔U➔S➔_➔C➔R➔E➔D➔S➔_➔U➔S➔R➔}➔:➔$➔{➔N➔E➔X➔U➔S➔_➔C➔R➔E➔D➔S➔_➔P➔S➔W➔}➔ ➔\➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔-➔u➔p➔l➔o➔a➔d➔-➔f➔i➔l➔e➔ ➔t➔a➔r➔g➔e➔t➔/➔m➔y➔a➔p➔p➔.➔j➔a➔r➔ ➔\➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔h➔t➔t➔p➔:➔/➔/➔n➔e➔x➔u➔s➔:➔8➔0➔8➔1➔/➔r➔e➔p➔o➔s➔i➔t➔o➔r➔y➔/➔m➔y➔a➔p➔p➔-➔r➔e➔l➔e➔a➔s➔e➔s➔/➔m➔y➔a➔p➔p➔-➔$➔{➔B➔U➔I➔L➔D➔_➔N➔U➔M➔B➔E➔R➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔'➔'➔'➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔/➔/➔ ➔─➔─➔ ➔S➔T➔A➔G➔E➔ ➔6➔:➔ ➔B➔u➔i➔l➔d➔ ➔D➔o➔c➔k➔e➔r➔ ➔I➔m➔a➔g➔e➔ ➔─➔─➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔g➔e➔(➔'➔B➔u➔i➔l➔d➔ ➔D➔o➔c➔k➔e➔r➔ ➔I➔m➔a➔g➔e➔'➔)➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔h➔ ➔"➔d➔o➔c➔k➔e➔r➔ ➔b➔u➔i➔l➔d➔ ➔-➔t➔ ➔$➔{➔I➔M➔A➔G➔E➔_➔N➔A➔M➔E➔}➔:➔$➔{➔I➔M➔A➔G➔E➔_➔T➔A➔G➔}➔ ➔.➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔h➔ ➔"➔d➔o➔c➔k➔e➔r➔ ➔t➔a➔g➔ ➔$➔{➔I➔M➔A➔G➔E➔_➔N➔A➔M➔E➔}➔:➔$➔{➔I➔M➔A➔G➔E➔_➔T➔A➔G➔}➔ ➔$➔{➔I➔M➔A➔G➔E➔_➔N➔A➔M➔E➔}➔:➔l➔a➔t➔e➔s➔t➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔/➔/➔ ➔─➔─➔ ➔S➔T➔A➔G➔E➔ ➔7➔:➔ ➔P➔u➔s➔h➔ ➔t➔o➔ ➔D➔o➔c➔k➔e➔r➔ ➔H➔u➔b➔ ➔─➔─➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔g➔e➔(➔'➔P➔u➔s➔h➔ ➔D➔o➔c➔k➔e➔r➔ ➔I➔m➔a➔g➔e➔'➔)➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔h➔ ➔'➔'➔'➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔e➔c➔h➔o➔ ➔$➔{➔D➔O➔C➔K➔E➔R➔_➔H➔U➔B➔_➔C➔R➔E➔D➔S➔_➔P➔S➔W➔}➔ ➔|➔ ➔\➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔ ➔l➔o➔g➔i➔n➔ ➔-➔u➔ ➔$➔{➔D➔O➔C➔K➔E➔R➔_➔H➔U➔B➔_➔C➔R➔E➔D➔S➔_➔U➔S➔R➔}➔ ➔-➔-➔p➔a➔s➔s➔w➔o➔r➔d➔-➔s➔t➔d➔i➔n➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔ ➔p➔u➔s➔h➔ ➔$➔{➔I➔M➔A➔G➔E➔_➔N➔A➔M➔E➔}➔:➔$➔{➔I➔M➔A➔G➔E➔_➔T➔A➔G➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔ ➔p➔u➔s➔h➔ ➔$➔{➔I➔M➔A➔G➔E➔_➔N➔A➔M➔E➔}➔:➔l➔a➔t➔e➔s➔t➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔'➔'➔'➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔/➔/➔ ➔─➔─➔ ➔S➔T➔A➔G➔E➔ ➔8➔:➔ ➔D➔e➔p➔l➔o➔y➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔─➔─➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔g➔e➔(➔'➔D➔e➔p➔l➔o➔y➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔'➔)➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔ ➔{➔
➔
➔
➔
➔
➔➔ ➔➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔h➔ ➔'➔'➔'➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔ ➔s➔t➔o➔p➔ ➔m➔y➔a➔p➔p➔ ➔|➔|➔ ➔t➔r➔u➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔ ➔r➔m➔ ➔m➔y➔a➔p➔p➔ ➔|➔|➔ ➔t➔r➔u➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔ ➔p➔u➔l➔l➔ ➔$➔{➔I➔M➔A➔G➔E➔_➔N➔A➔M➔E➔}➔:➔$➔{➔I➔M➔A➔G➔E➔_➔T➔A➔G➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔\➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔-➔n➔a➔m➔e➔ ➔m➔y➔a➔p➔p➔ ➔\➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔p➔ ➔8➔0➔:➔3➔0➔0➔0➔ ➔\➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔-➔r➔e➔s➔t➔a➔r➔t➔=➔a➔l➔w➔a➔y➔s➔ ➔\➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔e➔ ➔N➔O➔D➔E➔_➔E➔N➔V➔=➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔\➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔$➔{➔I➔M➔A➔G➔E➔_➔N➔A➔M➔E➔}➔:➔$➔{➔I➔M➔A➔G➔E➔_➔T➔A➔G➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔'➔'➔'➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔p➔o➔s➔t➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔u➔c➔c➔e➔s➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔e➔c➔h➔o➔ ➔"➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔ ➔s➔u➔c➔c➔e➔s➔s➔f➔u➔l➔!➔ ➔A➔p➔p➔ ➔r➔u➔n➔n➔i➔n➔g➔ ➔o➔n➔ ➔p➔o➔r➔t➔ ➔8➔0➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔f➔a➔i➔l➔u➔r➔e➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔e➔c➔h➔o➔ ➔"➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔f➔a➔i➔l➔e➔d➔!➔ ➔C➔h➔e➔c➔k➔ ➔l➔o➔g➔s➔.➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔/➔/➔ ➔S➔e➔n➔d➔ ➔e➔m➔a➔i➔l➔/➔S➔l➔a➔c➔k➔ ➔n➔o➔t➔i➔f➔i➔c➔a➔t➔i➔o➔n➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔a➔l➔w➔a➔y➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔h➔ ➔'➔d➔o➔c➔k➔e➔r➔ ➔i➔m➔a➔g➔e➔ ➔p➔r➔u➔n➔e➔ ➔-➔f➔'➔ ➔ ➔ ➔ ➔/➔/➔ ➔c➔l➔e➔a➔n➔u➔p➔ ➔u➔n➔u➔s➔e➔d➔ ➔i➔m➔a➔g➔e➔s➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔}➔
➔}➔
➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔F➔l➔o➔w➔:➔
➔C➔l➔o➔n➔e➔ ➔C➔o➔d➔e➔ ➔→➔ ➔B➔u➔i➔l➔d➔ ➔C➔o➔d➔e➔ ➔→➔ ➔S➔o➔n➔a➔r➔Q➔u➔b➔e➔ ➔→➔ ➔Q➔u➔a➔l➔i➔t➔y➔ ➔G➔a➔t➔e➔ ➔→➔ ➔N➔e➔x➔u➔s➔ ➔→➔ ➔D➔o➔c➔k➔e➔r➔ ➔B➔u➔i➔l➔d➔ ➔→➔ ➔D➔o➔c➔k➔e➔r➔ ➔P➔u➔s➔
➔K➔.➔ ➔D➔o➔c➔k➔e➔r➔ ➔C➔o➔m➔p➔o➔s➔e➔ ➔—➔ ➔C➔o➔m➔p➔l➔e➔t➔e➔ ➔G➔u➔i➔d➔e➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔D➔o➔c➔k➔e➔r➔ ➔C➔o➔m➔p➔o➔s➔e➔?➔
➔A➔ ➔t➔o➔o➔l➔ ➔t➔o➔ ➔d➔e➔f➔i➔n➔e➔ ➔a➔n➔d➔ ➔r➔u➔n➔ ➔m➔u➔l➔t➔i➔-➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔a➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔s➔ ➔u➔s➔i➔n➔g➔ ➔a➔ ➔s➔i➔n➔g➔l➔e➔ ➔Y➔A➔M➔L➔ ➔f➔i➔l➔e➔.➔
➔T➔y➔p➔e➔ ➔1➔ ➔—➔ ➔M➔u➔l➔t➔i➔p➔l➔e➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔f➔r➔o➔m➔ ➔E➔x➔i➔s➔t➔i➔n➔g➔ ➔I➔m➔a➔g➔e➔s➔
➔
➔
➔
➔
➔#➔ ➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔.➔y➔m➔l➔
➔v➔e➔r➔s➔i➔o➔n➔:➔ ➔'➔3➔.➔8➔'➔
➔s➔e➔r➔v➔i➔c➔e➔s➔:➔
➔ ➔ ➔#➔ ➔F➔r➔o➔n➔t➔e➔n➔d➔
➔ ➔ ➔f➔r➔o➔n➔t➔e➔n➔d➔:➔
➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔n➔g➔i➔n➔x➔:➔l➔a➔t➔e➔s➔t➔
➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔_➔n➔a➔m➔e➔:➔ ➔f➔r➔o➔n➔t➔e➔n➔d➔
➔ ➔ ➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔"➔8➔0➔:➔8➔0➔"➔
➔ ➔ ➔ ➔ ➔v➔o➔l➔u➔m➔e➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔.➔/➔f➔r➔o➔n➔t➔e➔n➔d➔:➔/➔u➔s➔r➔/➔s➔h➔a➔r➔e➔/➔n➔g➔i➔n➔x➔/➔h➔t➔m➔l➔
➔ ➔ ➔ ➔ ➔n➔e➔t➔w➔o➔r➔k➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔a➔p➔p➔n➔e➔t➔w➔o➔r➔k➔
➔ ➔ ➔ ➔ ➔d➔e➔p➔e➔n➔d➔s➔_➔o➔n➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔b➔a➔c➔k➔e➔n➔d➔
➔ ➔ ➔#➔ ➔B➔a➔c➔k➔e➔n➔d➔
➔ ➔ ➔b➔a➔c➔k➔e➔n➔d➔:➔
➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔n➔o➔d➔e➔:➔1➔8➔
➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔_➔n➔a➔m➔e➔:➔ ➔b➔a➔c➔k➔e➔n➔d➔
➔ ➔ ➔ ➔ ➔w➔o➔r➔k➔i➔n➔g➔_➔d➔i➔r➔:➔ ➔/➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔c➔o➔m➔m➔a➔n➔d➔:➔ ➔n➔o➔d➔e➔ ➔a➔p➔p➔.➔j➔s➔
➔ ➔ ➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔"➔3➔0➔0➔0➔:➔3➔0➔0➔0➔"➔
➔ ➔ ➔ ➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔N➔O➔D➔E➔_➔E➔N➔V➔=➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔D➔B➔_➔H➔O➔S➔T➔=➔d➔a➔t➔a➔b➔a➔s➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔D➔B➔_➔P➔O➔R➔T➔=➔5➔4➔3➔2➔
➔ ➔ ➔ ➔ ➔n➔e➔t➔w➔o➔r➔k➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔a➔p➔p➔n➔e➔t➔w➔o➔r➔k➔
➔ ➔ ➔ ➔ ➔d➔e➔p➔e➔n➔d➔s➔_➔o➔n➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔d➔a➔t➔a➔b➔a➔s➔e➔
➔ ➔ ➔#➔ ➔D➔a➔t➔a➔b➔a➔s➔e➔
➔ ➔ ➔d➔a➔t➔a➔b➔a➔s➔e➔:➔
➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔p➔o➔s➔t➔g➔r➔e➔s➔:➔1➔4➔
➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔_➔n➔a➔m➔e➔:➔ ➔d➔a➔t➔a➔b➔a➔s➔e➔
➔ ➔ ➔ ➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔P➔O➔S➔T➔G➔R➔E➔S➔_➔D➔B➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔ ➔ ➔P➔O➔S➔T➔G➔R➔E➔S➔_➔U➔S➔E➔R➔:➔ ➔a➔d➔m➔i➔n➔
➔ ➔ ➔ ➔ ➔ ➔ ➔P➔O➔S➔T➔G➔R➔E➔S➔_➔P➔A➔S➔S➔W➔O➔R➔D➔:➔ ➔s➔e➔c➔r➔e➔t➔
➔ ➔ ➔ ➔ ➔v➔o➔l➔u➔m➔e➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔p➔g➔d➔a➔t➔a➔:➔/➔v➔a➔r➔/➔l➔i➔b➔/➔p➔o➔s➔t➔g➔r➔e➔s➔q➔l➔/➔d➔a➔t➔a➔
➔ ➔ ➔ ➔ ➔n➔e➔t➔w➔o➔r➔k➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔a➔p➔p➔n➔e➔t➔w➔o➔r➔k➔
➔
➔
➔
➔
➔v➔o➔l➔u➔m➔e➔s➔:➔
➔ ➔ ➔p➔g➔d➔a➔t➔a➔:➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔n➔a➔m➔e➔d➔ ➔v➔o➔l➔u➔m➔e➔ ➔f➔o➔r➔ ➔d➔a➔t➔a➔b➔a➔s➔e➔ ➔p➔e➔r➔s➔i➔s➔t➔e➔n➔c➔e➔
➔n➔e➔t➔w➔o➔r➔k➔s➔:➔
➔ ➔ ➔a➔p➔p➔n➔e➔t➔w➔o➔r➔k➔:➔
➔ ➔ ➔ ➔ ➔d➔r➔i➔v➔e➔r➔:➔ ➔b➔r➔i➔d➔g➔e➔
➔T➔y➔p➔e➔ ➔2➔ ➔—➔ ➔M➔u➔l➔t➔i➔p➔l➔e➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔w➔i➔t➔h➔ ➔C➔u➔s➔t➔o➔m➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔s➔
➔#➔ ➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔.➔y➔m➔l➔ ➔(➔b➔u➔i➔l➔d➔s➔ ➔f➔r➔o➔m➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔s➔)➔
➔v➔e➔r➔s➔i➔o➔n➔:➔ ➔'➔3➔.➔8➔'➔
➔s➔e➔r➔v➔i➔c➔e➔s➔:➔
➔ ➔ ➔f➔r➔o➔n➔t➔e➔n➔d➔:➔
➔ ➔ ➔ ➔ ➔b➔u➔i➔l➔d➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔e➔x➔t➔:➔ ➔.➔/➔f➔r➔o➔n➔t➔e➔n➔d➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔l➔d➔e➔r➔ ➔c➔o➔n➔t➔a➔i➔n➔i➔n➔g➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔f➔i➔l➔e➔:➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔ ➔ ➔ ➔#➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔ ➔n➔a➔m➔e➔
➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔_➔n➔a➔m➔e➔:➔ ➔f➔r➔o➔n➔t➔e➔n➔d➔
➔ ➔ ➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔"➔8➔0➔:➔8➔0➔"➔
➔ ➔ ➔ ➔ ➔n➔e➔t➔w➔o➔r➔k➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔a➔p➔p➔n➔e➔t➔w➔o➔r➔k➔
➔ ➔ ➔b➔a➔c➔k➔e➔n➔d➔:➔
➔ ➔ ➔ ➔ ➔b➔u➔i➔l➔d➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔e➔x➔t➔:➔ ➔.➔/➔b➔a➔c➔k➔e➔n➔d➔
➔ ➔ ➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔f➔i➔l➔e➔:➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔.➔p➔r➔o➔d➔ ➔ ➔ ➔ ➔#➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔ ➔n➔a➔m➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔a➔r➔g➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔N➔O➔D➔E➔_➔E➔N➔V➔=➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔b➔u➔i➔l➔d➔ ➔a➔r➔g➔u➔m➔e➔n➔t➔s➔
➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔_➔n➔a➔m➔e➔:➔ ➔b➔a➔c➔k➔e➔n➔d➔
➔ ➔ ➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔"➔3➔0➔0➔0➔:➔3➔0➔0➔0➔"➔
➔ ➔ ➔ ➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔D➔B➔_➔H➔O➔S➔T➔=➔d➔a➔t➔a➔b➔a➔s➔e➔
➔ ➔ ➔ ➔ ➔n➔e➔t➔w➔o➔r➔k➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔a➔p➔p➔n➔e➔t➔w➔o➔r➔k➔
➔ ➔ ➔ ➔ ➔d➔e➔p➔e➔n➔d➔s➔_➔o➔n➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔d➔a➔t➔a➔b➔a➔s➔e➔
➔ ➔ ➔d➔a➔t➔a➔b➔a➔s➔e➔:➔
➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔p➔o➔s➔t➔g➔r➔e➔s➔:➔1➔4➔
➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔_➔n➔a➔m➔e➔:➔ ➔d➔a➔t➔a➔b➔a➔s➔e➔
➔ ➔ ➔ ➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔P➔O➔S➔T➔G➔R➔E➔S➔_➔D➔B➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔ ➔ ➔P➔O➔S➔T➔G➔R➔E➔S➔_➔U➔S➔E➔R➔:➔ ➔a➔d➔m➔i➔n➔
➔ ➔ ➔ ➔ ➔ ➔ ➔P➔O➔S➔T➔G➔R➔E➔S➔_➔P➔A➔S➔S➔W➔O➔R➔D➔:➔ ➔s➔e➔c➔r➔e➔t➔
➔
➔
➔
➔
➔ ➔ ➔ ➔ ➔v➔o➔l➔u➔m➔e➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔p➔g➔d➔a➔t➔a➔:➔/➔v➔a➔r➔/➔l➔i➔b➔/➔p➔o➔s➔t➔g➔r➔e➔s➔q➔l➔/➔d➔a➔t➔a➔
➔ ➔ ➔ ➔ ➔n➔e➔t➔w➔o➔r➔k➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔a➔p➔p➔n➔e➔t➔w➔o➔r➔k➔
➔v➔o➔l➔u➔m➔e➔s➔:➔
➔ ➔ ➔p➔g➔d➔a➔t➔a➔:➔
➔n➔e➔t➔w➔o➔r➔k➔s➔:➔
➔ ➔ ➔a➔p➔p➔n➔e➔t➔w➔o➔r➔k➔:➔
➔ ➔ ➔ ➔ ➔d➔r➔i➔v➔e➔r➔:➔ ➔b➔r➔i➔d➔g➔e➔
➔D➔o➔c➔k➔e➔r➔ ➔C➔o➔m➔p➔o➔s➔e➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔:➔
➔#➔ ➔S➔t➔a➔r➔t➔
➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔ ➔u➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔t➔a➔r➔t➔ ➔a➔l➔l➔ ➔(➔f➔o➔r➔e➔g➔r➔o➔u➔n➔d➔)➔
➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔ ➔u➔p➔ ➔-➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔t➔a➔r➔t➔ ➔a➔l➔l➔ ➔(➔b➔a➔c➔k➔g➔r➔o➔u➔n➔d➔/➔d➔e➔t➔a➔c➔h➔e➔d➔)➔
➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔ ➔u➔p➔ ➔-➔-➔b➔u➔i➔l➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔b➔u➔i➔l➔d➔ ➔i➔m➔a➔g➔e➔s➔ ➔b➔e➔f➔o➔r➔e➔ ➔s➔t➔a➔r➔t➔i➔n➔g➔
➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔ ➔u➔p➔ ➔-➔d➔ ➔-➔-➔b➔u➔i➔l➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔b➔u➔i➔l➔d➔ ➔+➔ ➔d➔e➔t➔a➔c➔h➔e➔d➔
➔#➔ ➔S➔t➔o➔p➔
➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔ ➔s➔t➔o➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔t➔o➔p➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔(➔k➔e➔e➔p➔ ➔t➔h➔e➔m➔)➔
➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔ ➔d➔o➔w➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔t➔o➔p➔ ➔+➔ ➔r➔e➔m➔o➔v➔e➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔
➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔ ➔d➔o➔w➔n➔ ➔-➔v➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔t➔o➔p➔ ➔+➔ ➔r➔e➔m➔o➔v➔e➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔+➔ ➔v➔o➔l➔u➔m➔e➔s➔
➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔ ➔d➔o➔w➔n➔ ➔-➔-➔r➔m➔i➔ ➔a➔l➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔+➔ ➔i➔m➔a➔g➔e➔s➔ ➔t➔o➔o➔
➔#➔ ➔V➔i➔e➔w➔
➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔ ➔p➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔
➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔ ➔l➔o➔g➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔l➔l➔ ➔l➔o➔g➔s➔
➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔ ➔l➔o➔g➔s➔ ➔-➔f➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔l➔l➔o➔w➔ ➔a➔l➔l➔ ➔l➔o➔g➔s➔
➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔ ➔l➔o➔g➔s➔ ➔b➔a➔c➔k➔e➔n➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔s➔e➔r➔v➔i➔c➔e➔ ➔l➔o➔g➔s➔
➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔ ➔l➔o➔g➔s➔ ➔-➔f➔ ➔b➔a➔c➔k➔e➔n➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔l➔l➔o➔w➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔s➔e➔r➔v➔i➔c➔e➔
➔#➔ ➔S➔c➔a➔l➔e➔
➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔ ➔u➔p➔ ➔-➔d➔ ➔-➔-➔s➔c➔a➔l➔e➔ ➔b➔a➔c➔k➔e➔n➔d➔=➔3➔ ➔ ➔#➔ ➔r➔u➔n➔ ➔3➔ ➔b➔a➔c➔k➔e➔n➔d➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔
➔#➔ ➔E➔x➔e➔c➔u➔t➔e➔
➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔ ➔e➔x➔e➔c➔ ➔b➔a➔c➔k➔e➔n➔d➔ ➔b➔a➔s➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔e➔l➔l➔ ➔i➔n➔t➔o➔ ➔s➔e➔r➔v➔i➔c➔e➔
➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔ ➔e➔x➔e➔c➔ ➔d➔a➔t➔a➔b➔a➔s➔e➔ ➔p➔s➔q➔l➔ ➔-➔U➔ ➔a➔d➔m➔i➔n➔ ➔ ➔#➔ ➔r➔u➔n➔ ➔c➔o➔m➔m➔a➔n➔d➔ ➔i➔n➔ ➔s➔e➔r➔v➔i➔c➔e➔
➔#➔ ➔B➔u➔i➔l➔d➔ ➔o➔n➔l➔y➔
➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔ ➔b➔u➔i➔l➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔b➔u➔i➔l➔d➔ ➔a➔l➔l➔ ➔i➔m➔a➔g➔e➔s➔
➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔ ➔b➔u➔i➔l➔d➔ ➔b➔a➔c➔k➔e➔n➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔b➔u➔i➔l➔d➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔s➔e➔r➔v➔i➔c➔e➔
➔#➔ ➔P➔u➔l➔l➔ ➔l➔a➔t➔e➔s➔t➔ ➔i➔m➔a➔g➔e➔s➔
➔d➔o➔c➔k➔e➔r➔-➔c➔o➔m➔p➔o➔s➔e➔ ➔p➔u➔l➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔u➔l➔l➔ ➔a➔l➔l➔ ➔i➔m➔a➔g➔e➔s➔
➔
➔
➔
➔
➔L➔.➔ ➔D➔o➔c➔k➔e➔r➔ ➔V➔o➔l➔u➔m➔e➔s➔ ➔—➔ ➔C➔o➔m➔p➔l➔e➔t➔e➔ ➔G➔u➔i➔d➔e➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔ ➔D➔o➔c➔k➔e➔r➔ ➔V➔o➔l➔u➔m➔e➔?➔
➔V➔o➔l➔u➔m➔e➔s➔ ➔p➔r➔o➔v➔i➔d➔e➔ ➔p➔e➔r➔s➔i➔s➔t➔e➔n➔t➔ ➔s➔t➔o➔r➔a➔g➔e➔ ➔f➔o➔r➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔.➔ ➔D➔a➔t➔a➔ ➔i➔n➔ ➔v➔o➔l➔u➔m➔e➔s➔ ➔s➔u➔r➔v➔i➔v➔e➔s➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔r➔e➔s➔t➔a➔r➔t➔s➔ ➔a➔n➔d➔ ➔d➔e➔l➔e➔t➔i➔o➔n➔s➔.➔
➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔(➔e➔p➔h➔e➔m➔e➔r➔a➔l➔)➔
➔ ➔ ➔ ➔ ➔↓➔ ➔w➔r➔i➔t➔e➔s➔ ➔t➔o➔
➔V➔o➔l➔u➔m➔e➔ ➔(➔p➔e➔r➔s➔i➔s➔t➔e➔n➔t➔)➔ ➔←➔ ➔s➔u➔r➔v➔i➔v➔e➔s➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔d➔e➔l➔e➔t➔i➔o➔n➔
➔T➔y➔p➔e➔s➔ ➔o➔f➔ ➔S➔t➔o➔r➔a➔g➔e➔
➔1➔.➔ ➔N➔a➔m➔e➔d➔ ➔V➔o➔l➔u➔m➔e➔ ➔(➔M➔a➔n➔a➔g➔e➔d➔ ➔b➔y➔ ➔D➔o➔c➔k➔e➔r➔ ➔—➔ ➔R➔e➔c➔o➔m➔m➔e➔n➔d➔e➔d➔)➔
➔#➔ ➔D➔o➔c➔k➔e➔r➔ ➔m➔a➔n➔a➔g➔e➔s➔ ➔w➔h➔e➔r➔e➔ ➔d➔a➔t➔a➔ ➔i➔s➔ ➔s➔t➔o➔r➔e➔d➔
➔d➔o➔c➔k➔e➔r➔ ➔v➔o➔l➔u➔m➔e➔ ➔c➔r➔e➔a➔t➔e➔ ➔m➔y➔v➔o➔l➔u➔m➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔v➔ ➔m➔y➔v➔o➔l➔u➔m➔e➔:➔/➔d➔a➔t➔a➔ ➔m➔y➔a➔p➔p➔
➔#➔ ➔D➔a➔t➔a➔ ➔l➔i➔v➔e➔s➔ ➔i➔n➔:➔ ➔/➔v➔a➔r➔/➔l➔i➔b➔/➔d➔o➔c➔k➔e➔r➔/➔v➔o➔l➔u➔m➔e➔s➔/➔m➔y➔v➔o➔l➔u➔m➔e➔/➔_➔d➔a➔t➔a➔
➔2➔.➔ ➔B➔i➔n➔d➔ ➔M➔o➔u➔n➔t➔ ➔(➔H➔o➔s➔t➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔)➔
➔#➔ ➔Y➔o➔u➔ ➔c➔o➔n➔t➔r➔o➔l➔ ➔w➔h➔e➔r➔e➔ ➔d➔a➔t➔a➔ ➔l➔i➔v➔e➔s➔ ➔o➔n➔ ➔h➔o➔s➔t➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔v➔ ➔/➔h➔o➔m➔e➔/➔a➔k➔h➔i➔l➔/➔d➔a➔t➔a➔:➔/➔d➔a➔t➔a➔ ➔m➔y➔a➔p➔p➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔v➔ ➔$➔(➔p➔w➔d➔)➔:➔/➔a➔p➔p➔ ➔m➔y➔a➔p➔p➔ ➔ ➔ ➔ ➔#➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔3➔.➔ ➔t➔m➔p➔f➔s➔ ➔M➔o➔u➔n➔t➔ ➔(➔I➔n➔-➔m➔e➔m➔o➔r➔y➔,➔ ➔n➔o➔t➔ ➔p➔e➔r➔s➔i➔s➔t➔e➔n➔t➔)➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔-➔t➔m➔p➔f➔s➔ ➔/➔t➔m➔p➔ ➔m➔y➔a➔p➔p➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔t➔o➔r➔e➔d➔ ➔i➔n➔ ➔h➔o➔s➔t➔ ➔m➔e➔m➔o➔r➔y➔ ➔o➔n➔l➔y➔
➔V➔o➔l➔u➔m➔e➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔:➔
➔#➔ ➔C➔r➔e➔a➔t➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔v➔o➔l➔u➔m➔e➔ ➔c➔r➔e➔a➔t➔e➔ ➔m➔y➔v➔o➔l➔u➔m➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔v➔o➔l➔u➔m➔e➔ ➔c➔r➔e➔a➔t➔e➔ ➔-➔-➔d➔r➔i➔v➔e➔r➔ ➔l➔o➔c➔a➔l➔ ➔m➔y➔v➔o➔l➔u➔m➔e➔
➔#➔ ➔L➔i➔s➔t➔
➔d➔o➔c➔k➔e➔r➔ ➔v➔o➔l➔u➔m➔e➔ ➔l➔s➔
➔#➔ ➔I➔n➔s➔p➔e➔c➔t➔
➔d➔o➔c➔k➔e➔r➔ ➔v➔o➔l➔u➔m➔e➔ ➔i➔n➔s➔p➔e➔c➔t➔ ➔m➔y➔v➔o➔l➔u➔m➔e➔
➔
➔
➔
➔
➔#➔ ➔S➔h➔o➔w➔s➔ ➔m➔o➔u➔n➔t➔p➔o➔i➔n➔t➔,➔ ➔d➔r➔i➔v➔e➔r➔,➔ ➔l➔a➔b➔e➔l➔s➔
➔#➔ ➔R➔e➔m➔o➔v➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔v➔o➔l➔u➔m➔e➔ ➔r➔m➔ ➔m➔y➔v➔o➔l➔u➔m➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔v➔o➔l➔u➔m➔e➔ ➔p➔r➔u➔n➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔a➔l➔l➔ ➔u➔n➔u➔s➔e➔d➔ ➔v➔o➔l➔u➔m➔e➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔v➔o➔l➔u➔m➔e➔ ➔p➔r➔u➔n➔e➔ ➔-➔f➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔r➔c➔e➔ ➔(➔n➔o➔ ➔c➔o➔n➔f➔i➔r➔m➔a➔t➔i➔o➔n➔)➔
➔#➔ ➔U➔s➔e➔ ➔i➔n➔ ➔r➔u➔n➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔v➔ ➔m➔y➔v➔o➔l➔u➔m➔e➔:➔/➔a➔p➔p➔/➔d➔a➔t➔a➔ ➔m➔y➔a➔p➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔n➔a➔m➔e➔d➔ ➔v➔o➔l➔u➔m➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔v➔ ➔/➔h➔o➔s➔t➔/➔p➔a➔t➔h➔:➔/➔c➔o➔n➔t➔a➔i➔n➔e➔r➔/➔p➔a➔t➔h➔ ➔m➔y➔a➔p➔p➔ ➔ ➔ ➔#➔ ➔b➔i➔n➔d➔ ➔m➔o➔u➔n➔t➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔v➔ ➔m➔y➔v➔o➔l➔u➔m➔e➔:➔/➔d➔a➔t➔a➔:➔r➔o➔ ➔m➔y➔a➔p➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔a➔d➔-➔o➔n➔l➔y➔ ➔v➔o➔l➔u➔m➔e➔
➔#➔ ➔B➔a➔c➔k➔u➔p➔ ➔a➔ ➔v➔o➔l➔u➔m➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔-➔r➔m➔ ➔\➔
➔ ➔ ➔-➔v➔ ➔m➔y➔v➔o➔l➔u➔m➔e➔:➔/➔d➔a➔t➔a➔ ➔\➔
➔ ➔ ➔-➔v➔ ➔$➔(➔p➔w➔d➔)➔:➔/➔b➔a➔c➔k➔u➔p➔ ➔\➔
➔ ➔ ➔u➔b➔u➔n➔t➔u➔ ➔t➔a➔r➔ ➔c➔v➔f➔ ➔/➔b➔a➔c➔k➔u➔p➔/➔b➔a➔c➔k➔u➔p➔.➔t➔a➔r➔ ➔/➔d➔a➔t➔a➔
➔#➔ ➔R➔e➔s➔t➔o➔r➔e➔ ➔a➔ ➔v➔o➔l➔u➔m➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔-➔r➔m➔ ➔\➔
➔ ➔ ➔-➔v➔ ➔m➔y➔v➔o➔l➔u➔m➔e➔:➔/➔d➔a➔t➔a➔ ➔\➔
➔ ➔ ➔-➔v➔ ➔$➔(➔p➔w➔d➔)➔:➔/➔b➔a➔c➔k➔u➔p➔ ➔\➔
➔ ➔ ➔u➔b➔u➔n➔t➔u➔ ➔t➔a➔r➔ ➔x➔v➔f➔ ➔/➔b➔a➔c➔k➔u➔p➔/➔b➔a➔c➔k➔u➔p➔.➔t➔a➔r➔ ➔-➔C➔ ➔/➔
➔M➔.➔ ➔D➔o➔c➔k➔e➔r➔ ➔N➔e➔t➔w➔o➔r➔k➔i➔n➔g➔ ➔—➔ ➔A➔l➔l➔ ➔T➔y➔p➔e➔s➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔D➔o➔c➔k➔e➔r➔ ➔N➔e➔t➔w➔o➔r➔k➔i➔n➔g➔?➔
➔D➔o➔c➔k➔e➔r➔ ➔n➔e➔t➔w➔o➔r➔k➔i➔n➔g➔ ➔c➔o➔n➔t➔r➔o➔l➔s➔ ➔h➔o➔w➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔c➔o➔m➔m➔u➔n➔i➔c➔a➔t➔e➔ ➔w➔i➔t➔h➔ ➔e➔a➔c➔h➔ ➔o➔t➔h➔e➔r➔ ➔a➔n➔d➔ ➔t➔h➔e➔ ➔o➔u➔t➔s➔i➔d➔e➔ ➔w➔o➔r➔l➔d➔.➔
➔1➔.➔ ➔B➔r➔i➔d➔g➔e➔ ➔N➔e➔t➔w➔o➔r➔k➔ ➔(➔D➔e➔f➔a➔u➔l➔t➔)➔
➔H➔o➔s➔t➔ ➔M➔a➔c➔h➔i➔n➔e➔
➔├➔─➔─➔ ➔d➔o➔c➔k➔e➔r➔0➔ ➔(➔b➔r➔i➔d➔g➔e➔ ➔i➔n➔t➔e➔r➔f➔a➔c➔e➔,➔ ➔1➔7➔2➔.➔1➔7➔.➔0➔.➔1➔)➔
➔│➔ ➔ ➔ ➔├➔─➔─➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔1➔ ➔(➔1➔7➔2➔.➔1➔7➔.➔0➔.➔2➔)➔
➔│➔ ➔ ➔ ➔├➔─➔─➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔2➔ ➔(➔1➔7➔2➔.➔1➔7➔.➔0➔.➔3➔)➔
➔│➔ ➔ ➔ ➔└➔─➔─➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔3➔ ➔(➔1➔7➔2➔.➔1➔7➔.➔0➔.➔4➔)➔
➔└➔─➔─➔ ➔e➔t➔h➔0➔ ➔(➔h➔o➔s➔t➔ ➔n➔e➔t➔w➔o➔r➔k➔,➔ ➔c➔o➔n➔n➔e➔c➔t➔e➔d➔ ➔t➔o➔ ➔i➔n➔t➔e➔r➔n➔e➔t➔)➔
➔D➔e➔f➔a➔u➔l➔t➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔f➔o➔r➔ ➔a➔l➔l➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔
➔C➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔o➔n➔ ➔s➔a➔m➔e➔ ➔b➔r➔i➔d➔g➔e➔ ➔c➔a➔n➔ ➔c➔o➔m➔m➔u➔n➔i➔c➔a➔t➔e➔ ➔b➔y➔ ➔I➔P➔
➔C➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔o➔n➔ ➔c➔u➔s➔t➔o➔m➔ ➔b➔r➔i➔d➔g➔e➔ ➔c➔a➔n➔ ➔c➔o➔m➔m➔u➔n➔i➔c➔a➔t➔e➔ ➔b➔y➔ ➔n➔a➔m➔e➔
➔
➔
➔
➔
➔I➔s➔o➔l➔a➔t➔e➔d➔ ➔f➔r➔o➔m➔ ➔o➔t➔h➔e➔r➔ ➔b➔r➔i➔d➔g➔e➔ ➔n➔e➔t➔w➔o➔r➔k➔s➔
➔#➔ ➔D➔e➔f➔a➔u➔l➔t➔ ➔b➔r➔i➔d➔g➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔u➔s➔e➔s➔ ➔d➔e➔f➔a➔u➔l➔t➔ ➔b➔r➔i➔d➔g➔e➔
➔#➔ ➔C➔u➔s➔t➔o➔m➔ ➔b➔r➔i➔d➔g➔e➔ ➔(➔r➔e➔c➔o➔m➔m➔e➔n➔d➔e➔d➔ ➔—➔ ➔a➔l➔l➔o➔w➔s➔ ➔D➔N➔S➔ ➔b➔y➔ ➔n➔a➔m➔e➔)➔
➔d➔o➔c➔k➔e➔r➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔c➔r➔e➔a➔t➔e➔ ➔m➔y➔b➔r➔i➔d➔g➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔-➔n➔e➔t➔w➔o➔r➔k➔ ➔m➔y➔b➔r➔i➔d➔g➔e➔ ➔-➔-➔n➔a➔m➔e➔ ➔w➔e➔b➔ ➔n➔g➔i➔n➔x➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔-➔n➔e➔t➔w➔o➔r➔k➔ ➔m➔y➔b➔r➔i➔d➔g➔e➔ ➔-➔-➔n➔a➔m➔e➔ ➔a➔p➔p➔ ➔m➔y➔a➔p➔p➔
➔#➔ ➔N➔o➔w➔ ➔'➔a➔p➔p➔'➔ ➔c➔a➔n➔ ➔r➔e➔a➔c➔h➔ ➔'➔w➔e➔b➔'➔ ➔b➔y➔ ➔n➔a➔m➔e➔:➔ ➔h➔t➔t➔p➔:➔/➔/➔w➔e➔b➔:➔8➔0➔
➔2➔.➔ ➔H➔o➔s➔t➔ ➔N➔e➔t➔w➔o➔r➔k➔
➔H➔o➔s➔t➔ ➔M➔a➔c➔h➔i➔n➔e➔ ➔(➔1➔9➔2➔.➔1➔6➔8➔.➔1➔.➔1➔0➔)➔
➔└➔─➔─➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔(➔s➔h➔a➔r➔e➔s➔ ➔h➔o➔s➔t➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔s➔t➔a➔c➔k➔)➔
➔ ➔ ➔ ➔ ➔└➔─➔─➔ ➔U➔s➔e➔s➔ ➔h➔o➔s➔t➔'➔s➔ ➔I➔P➔ ➔a➔n➔d➔ ➔p➔o➔r➔t➔s➔ ➔d➔i➔r➔e➔c➔t➔l➔y➔
➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔u➔s➔e➔s➔ ➔h➔o➔s➔t➔'➔s➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔d➔i➔r➔e➔c➔t➔l➔y➔
➔N➔o➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔i➔s➔o➔l➔a➔t➔i➔o➔n➔
➔F➔a➔s➔t➔e➔s➔t➔ ➔p➔e➔r➔f➔o➔r➔m➔a➔n➔c➔e➔ ➔(➔n➔o➔ ➔N➔A➔T➔ ➔o➔v➔e➔r➔h➔e➔a➔d➔)➔
➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔p➔o➔r➔t➔ ➔=➔ ➔h➔o➔s➔t➔ ➔p➔o➔r➔t➔ ➔(➔n➔o➔ ➔-➔p➔ ➔n➔e➔e➔d➔e➔d➔)➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔-➔n➔e➔t➔w➔o➔r➔k➔ ➔h➔o➔s➔t➔ ➔n➔g➔i➔n➔x➔
➔#➔ ➔n➔g➔i➔n➔x➔ ➔n➔o➔w➔ ➔a➔c➔c➔e➔s➔s➔i➔b➔l➔e➔ ➔o➔n➔ ➔h➔o➔s➔t➔'➔s➔ ➔p➔o➔r➔t➔ ➔8➔0➔ ➔d➔i➔r➔e➔c➔t➔l➔y➔
➔#➔ ➔C➔a➔n➔n➔o➔t➔ ➔u➔s➔e➔ ➔-➔p➔ ➔w➔i➔t➔h➔ ➔h➔o➔s➔t➔ ➔n➔e➔t➔w➔o➔r➔k➔
➔3➔.➔ ➔N➔o➔n➔e➔ ➔N➔e➔t➔w➔o➔r➔k➔
➔N➔o➔ ➔n➔e➔t➔w➔o➔r➔k➔i➔n➔g➔ ➔a➔t➔ ➔a➔l➔l➔
➔C➔o➔m➔p➔l➔e➔t➔e➔l➔y➔ ➔i➔s➔o➔l➔a➔t➔e➔d➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔U➔s➔e➔ ➔f➔o➔r➔ ➔m➔a➔x➔i➔m➔u➔m➔ ➔s➔e➔c➔u➔r➔i➔t➔y➔ ➔o➔r➔ ➔b➔a➔t➔c➔h➔ ➔p➔r➔o➔c➔e➔s➔s➔i➔n➔g➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔-➔n➔e➔t➔w➔o➔r➔k➔ ➔n➔o➔n➔e➔ ➔m➔y➔a➔p➔p➔
➔#➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔h➔a➔s➔ ➔n➔o➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔a➔c➔c➔e➔s➔s➔
➔4➔.➔ ➔O➔v➔e➔r➔l➔a➔y➔ ➔N➔e➔t➔w➔o➔r➔k➔
➔H➔o➔s➔t➔ ➔1➔ ➔(➔S➔w➔a➔r➔m➔ ➔M➔a➔n➔a➔g➔e➔r➔)➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔H➔o➔s➔t➔ ➔2➔ ➔(➔S➔w➔a➔r➔m➔ ➔W➔o➔r➔k➔e➔r➔)➔
➔├➔─➔─➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔├➔─➔─➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔3➔
➔
➔
➔
➔
➔└➔─➔─➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔2➔ ➔ ➔←➔─➔─➔─➔ ➔o➔v➔e➔r➔l➔a➔y➔ ➔─➔─➔ ➔▶➔ ➔ ➔└➔─➔─➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔4➔
➔ ➔ ➔ ➔ ➔ ➔(➔a➔l➔l➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔c➔a➔n➔ ➔c➔o➔m➔m➔u➔n➔i➔c➔a➔t➔e➔ ➔a➔c➔r➔o➔s➔s➔ ➔h➔o➔s➔t➔s➔)➔
➔U➔s➔e➔d➔ ➔i➔n➔ ➔D➔o➔c➔k➔e➔r➔ ➔S➔w➔a➔r➔m➔ ➔f➔o➔r➔ ➔m➔u➔l➔t➔i➔-➔h➔o➔s➔t➔ ➔n➔e➔t➔w➔o➔r➔k➔i➔n➔g➔
➔C➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔o➔n➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔t➔ ➔p➔h➔y➔s➔i➔c➔a➔l➔ ➔h➔o➔s➔t➔s➔ ➔c➔o➔m➔m➔u➔n➔i➔c➔a➔t➔e➔ ➔s➔e➔a➔m➔l➔e➔s➔s➔l➔y➔
➔E➔n➔c➔r➔y➔p➔t➔e➔d➔ ➔t➔r➔a➔f➔f➔i➔c➔ ➔b➔e➔t➔w➔e➔e➔n➔ ➔h➔o➔s➔t➔s➔
➔#➔ ➔C➔r➔e➔a➔t➔e➔ ➔o➔v➔e➔r➔l➔a➔y➔ ➔(➔r➔e➔q➔u➔i➔r➔e➔s➔ ➔S➔w➔a➔r➔m➔ ➔m➔o➔d➔e➔)➔
➔d➔o➔c➔k➔e➔r➔ ➔s➔w➔a➔r➔m➔ ➔i➔n➔i➔t➔
➔d➔o➔c➔k➔e➔r➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔c➔r➔e➔a➔t➔e➔ ➔-➔d➔ ➔o➔v➔e➔r➔l➔a➔y➔ ➔m➔y➔o➔v➔e➔r➔l➔a➔y➔
➔d➔o➔c➔k➔e➔r➔ ➔s➔e➔r➔v➔i➔c➔e➔ ➔c➔r➔e➔a➔t➔e➔ ➔-➔-➔n➔e➔t➔w➔o➔r➔k➔ ➔m➔y➔o➔v➔e➔r➔l➔a➔y➔ ➔n➔g➔i➔n➔x➔
➔5➔.➔ ➔M➔a➔c➔v➔l➔a➔n➔ ➔N➔e➔t➔w➔o➔r➔k➔
➔A➔s➔s➔i➔g➔n➔s➔ ➔a➔ ➔r➔e➔a➔l➔ ➔M➔A➔C➔ ➔a➔d➔d➔r➔e➔s➔s➔ ➔t➔o➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔a➔p➔p➔e➔a➔r➔s➔ ➔a➔s➔ ➔p➔h➔y➔s➔i➔c➔a➔l➔ ➔d➔e➔v➔i➔c➔e➔ ➔o➔n➔ ➔n➔e➔t➔w➔o➔r➔k➔
➔D➔i➔r➔e➔c➔t➔ ➔c➔o➔n➔n➔e➔c➔t➔i➔o➔n➔ ➔t➔o➔ ➔p➔h➔y➔s➔i➔c➔a➔l➔ ➔n➔e➔t➔w➔o➔r➔k➔
➔U➔s➔e➔d➔ ➔w➔h➔e➔n➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔n➔e➔e➔d➔ ➔t➔o➔ ➔b➔e➔ ➔o➔n➔ ➔p➔h➔y➔s➔i➔c➔a➔l➔ ➔L➔A➔N➔
➔d➔o➔c➔k➔e➔r➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔c➔r➔e➔a➔t➔e➔ ➔-➔d➔ ➔m➔a➔c➔v➔l➔a➔n➔ ➔\➔
➔ ➔ ➔-➔-➔s➔u➔b➔n➔e➔t➔=➔1➔9➔2➔.➔1➔6➔8➔.➔1➔.➔0➔/➔2➔4➔ ➔\➔
➔ ➔ ➔-➔-➔g➔a➔t➔e➔w➔a➔y➔=➔1➔9➔2➔.➔1➔6➔8➔.➔1➔.➔1➔ ➔\➔
➔ ➔ ➔-➔o➔ ➔p➔a➔r➔e➔n➔t➔=➔e➔t➔h➔0➔ ➔\➔
➔ ➔ ➔m➔y➔m➔a➔c➔v➔l➔a➔n➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔-➔n➔e➔t➔w➔o➔r➔k➔ ➔m➔y➔m➔a➔c➔v➔l➔a➔n➔ ➔-➔-➔i➔p➔=➔1➔9➔2➔.➔1➔6➔8➔.➔1➔.➔1➔0➔0➔ ➔n➔g➔i➔n➔x➔
➔N➔e➔t➔w➔o➔r➔k➔i➔n➔g➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔:➔
➔#➔ ➔L➔i➔s➔t➔ ➔n➔e➔t➔w➔o➔r➔k➔s➔
➔d➔o➔c➔k➔e➔r➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔l➔s➔
➔#➔ ➔C➔r➔e➔a➔t➔e➔ ➔n➔e➔t➔w➔o➔r➔k➔
➔d➔o➔c➔k➔e➔r➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔c➔r➔e➔a➔t➔e➔ ➔m➔y➔n➔e➔t➔w➔o➔r➔k➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔b➔r➔i➔d➔g➔e➔ ➔b➔y➔ ➔d➔e➔f➔a➔u➔l➔t➔
➔d➔o➔c➔k➔e➔r➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔c➔r➔e➔a➔t➔e➔ ➔-➔-➔d➔r➔i➔v➔e➔r➔ ➔b➔r➔i➔d➔g➔e➔ ➔m➔y➔b➔r➔i➔d➔g➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔c➔r➔e➔a➔t➔e➔ ➔-➔-➔d➔r➔i➔v➔e➔r➔ ➔o➔v➔e➔r➔l➔a➔y➔ ➔m➔y➔o➔v➔e➔r➔l➔a➔y➔
➔d➔o➔c➔k➔e➔r➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔c➔r➔e➔a➔t➔e➔ ➔-➔-➔s➔u➔b➔n➔e➔t➔=➔1➔7➔2➔.➔2➔0➔.➔0➔.➔0➔/➔1➔6➔ ➔m➔y➔n➔e➔t➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔u➔s➔t➔o➔m➔ ➔s➔u➔b➔n➔e➔t➔
➔#➔ ➔I➔n➔s➔p➔e➔c➔t➔
➔d➔o➔c➔k➔e➔r➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔i➔n➔s➔p➔e➔c➔t➔ ➔m➔y➔n➔e➔t➔w➔o➔r➔k➔
➔d➔o➔c➔k➔e➔r➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔i➔n➔s➔p➔e➔c➔t➔ ➔b➔r➔i➔d➔g➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔f➔a➔u➔l➔t➔ ➔b➔r➔i➔d➔g➔e➔ ➔i➔n➔f➔o➔
➔
➔
➔
➔
➔#➔ ➔C➔o➔n➔n➔e➔c➔t➔/➔D➔i➔s➔c➔o➔n➔n➔e➔c➔t➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔t➔o➔ ➔n➔e➔t➔w➔o➔r➔k➔
➔d➔o➔c➔k➔e➔r➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔c➔o➔n➔n➔e➔c➔t➔ ➔m➔y➔n➔e➔t➔w➔o➔r➔k➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔d➔o➔c➔k➔e➔r➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔d➔i➔s➔c➔o➔n➔n➔e➔c➔t➔ ➔m➔y➔n➔e➔t➔w➔o➔r➔k➔ ➔m➔y➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔#➔ ➔R➔e➔m➔o➔v➔e➔
➔d➔o➔c➔k➔e➔r➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔r➔m➔ ➔m➔y➔n➔e➔t➔w➔o➔r➔k➔
➔d➔o➔c➔k➔e➔r➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔p➔r➔u➔n➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔u➔n➔u➔s➔e➔d➔ ➔n➔e➔t➔w➔o➔r➔k➔s➔
➔#➔ ➔R➔u➔n➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔o➔n➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔n➔e➔t➔w➔o➔r➔k➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔-➔n➔e➔t➔w➔o➔r➔k➔ ➔m➔y➔n➔e➔t➔w➔o➔r➔k➔ ➔-➔-➔n➔a➔m➔e➔ ➔w➔e➔b➔ ➔n➔g➔i➔n➔x➔
➔d➔o➔c➔k➔e➔r➔ ➔r➔u➔n➔ ➔-➔d➔ ➔-➔-➔n➔e➔t➔w➔o➔r➔k➔ ➔m➔y➔n➔e➔t➔w➔o➔r➔k➔ ➔-➔-➔n➔a➔m➔e➔ ➔a➔p➔p➔ ➔m➔y➔a➔p➔p➔
➔#➔ ➔a➔p➔p➔ ➔c➔a➔n➔ ➔r➔e➔a➔c➔h➔ ➔w➔e➔b➔ ➔u➔s➔i➔n➔g➔:➔ ➔h➔t➔t➔p➔:➔/➔/➔w➔e➔b➔ ➔(➔b➔y➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔n➔a➔m➔e➔)➔
➔N➔e➔t➔w➔o➔r➔k➔ ➔C➔o➔m➔p➔a➔r➔i➔s➔o➔n➔:➔
➔N➔e➔t➔w➔o➔r➔k➔ ➔I➔s➔o➔l➔a➔t➔i➔o➔n➔ ➔C➔o➔m➔m➔u➔n➔i➔c➔a➔t➔i➔o➔n➔ ➔U➔s➔e➔ ➔C➔a➔s➔e➔
➔B➔r➔i➔d➔g➔e➔ ➔Y➔e➔s➔ ➔B➔y➔ ➔I➔P➔ ➔o➔r➔ ➔n➔a➔m➔e➔ ➔(➔c➔u➔s➔t➔o➔m➔)➔ ➔D➔e➔f➔a➔u➔l➔t➔,➔ ➔s➔i➔n➔g➔l➔e➔ ➔h➔o➔s➔t➔
➔H➔o➔s➔t➔ ➔N➔o➔ ➔S➔h➔a➔r➔e➔s➔ ➔h➔o➔s➔t➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔P➔e➔r➔f➔o➔r➔m➔a➔n➔c➔e➔ ➔c➔r➔i➔t➔i➔c➔a➔l➔
➔N➔o➔n➔e➔ ➔C➔o➔m➔p➔l➔e➔t➔e➔ ➔N➔o➔ ➔n➔e➔t➔w➔o➔r➔k➔i➔n➔g➔ ➔B➔a➔t➔c➔h➔,➔ ➔s➔e➔c➔u➔r➔i➔t➔y➔
➔O➔v➔e➔r➔l➔a➔y➔ ➔Y➔e➔s➔ ➔A➔c➔r➔o➔s➔s➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔h➔o➔s➔t➔s➔ ➔D➔o➔c➔k➔e➔r➔ ➔S➔w➔a➔r➔m➔
➔M➔a➔c➔v➔l➔a➔n➔ ➔Y➔e➔s➔ ➔D➔i➔r➔e➔c➔t➔ ➔t➔o➔ ➔p➔h➔y➔s➔i➔c➔a➔l➔ ➔L➔A➔N➔ ➔L➔e➔g➔a➔c➔y➔ ➔a➔p➔p➔ ➔i➔n➔t➔e➔g➔r➔a➔t➔i➔o➔n➔
➔N➔.➔ ➔M➔u➔l➔t➔i➔-➔S➔t➔a➔g➔e➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔ ➔(➔A➔l➔r➔e➔a➔d➔y➔ ➔i➔n➔ ➔D➔o➔c➔k➔e➔r➔ ➔S➔e➔c➔t➔i➔o➔n➔ ➔a➔b➔o➔v➔e➔ ➔—➔ ➔s➔e➔e➔ ➔S➔e➔c➔t➔i➔o➔n➔ ➔3➔
➔Q➔1➔1➔)➔
➔R➔e➔f➔e➔r➔ ➔t➔o➔ ➔S➔e➔c➔t➔i➔o➔n➔ ➔3➔:➔ ➔Q➔1➔1➔ ➔—➔ ➔M➔u➔l➔t➔i➔-➔S➔t➔a➔g➔e➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔ ➔f➔o➔r➔ ➔c➔o➔m➔p➔l➔e➔t➔e➔ ➔e➔x➔p➔l➔a➔n➔a➔t➔i➔o➔n➔ ➔a➔n➔d➔ ➔e➔x➔a➔m➔p➔l➔e➔.➔
➔

---

## 🚀 Modern 2026 Production Standards & Hardening

### 1. Modern Docker Compose Specification (`compose.yaml`)
*Note: In modern Docker Compose, the top-level `version: '3.8'` attribute is obsolete. Compose now follows the unified Compose Specification:*

```yaml
services:
  web-app:
    build:
      context: .
      dockerfile: Dockerfile
    container_name: web-production
    restart: unless-stopped
    ports:
      - "80:8080"
    environment:
      NODE_ENV: production
      DATABASE_URL: postgresql://dbuser:${DB_PASSWORD}@database:5432/appdb
    depends_on:
      database:
        condition: service_healthy
    networks:
      - internal-net

  database:
    image: postgres:16-alpine
    container_name: db-production
    restart: unless-stopped
    environment:
      POSTGRES_DB: appdb
      POSTGRES_USER: dbuser
      POSTGRES_PASSWORD: ${DB_PASSWORD}
    volumes:
      - postgres_data:/var/lib/postgresql/data
    networks:
      - internal-net
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U dbuser -d appdb"]
      interval: 10s
      timeout: 5s
      retries: 5

volumes:
  postgres_data:

networks:
  internal-net:
    driver: bridge
```

### 2. Multi-Stage Production React / Node.js Template
```dockerfile
# STAGE 1: Build
FROM node:20-alpine AS builder
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci --prefer-offline
COPY . .
RUN npm run build

# STAGE 2: Secure Production Runtime
FROM nginx:1.25-alpine-slim AS runner
RUN addgroup -g 10001 -S appgroup && adduser -u 10001 -S appuser -G appgroup
COPY --from=builder --chown=appuser:appgroup /app/dist /usr/share/nginx/html
USER 10001
EXPOSE 8080
HEALTHCHECK --interval=30s --timeout=5s --retries=3 CMD wget --quiet --tries=1 --spider http://localhost:8080/health || exit 1
CMD ["nginx", "-g", "daemon off;"]
```
