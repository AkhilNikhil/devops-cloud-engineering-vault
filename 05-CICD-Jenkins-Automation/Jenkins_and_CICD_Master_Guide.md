# 🔄 CI/CD & Configuration Automation: Jenkins & Ansible Master Engineering Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers Continuous Integration & Delivery, Jenkins Controller-Agent Architecture, Declarative Pipelines, SonarQube & Nexus Integration, and Ansible Agentless Configuration Management.

---

## 📑 Table of Contents
- [PART 1: JENKINS CI/CD AUTOMATION](#part-1-jenkins-cicd-automation)
  - [Why Jenkins & CI/CD Foundations](#why-jenkins)
  - [Jenkins Controller-Agent Distributed Architecture](#jenkins-architecture)
  - [Declarative Pipeline Syntax & Best Practices](#declarative-pipelines)
  - [Quality & Artifact Governance (SonarQube & Nexus)](#sonarqube--nexus)
  - [Complete Production Jenkinsfile Blueprint](#production-jenkinsfile)
- [PART 2: ANSIBLE CONFIGURATION MANAGEMENT](#part-2-ansible-configuration-management)
  - [Why Ansible? (Agentless Architecture over SSH)](#why-ansible)
  - [Ansible Inventory & Host Management](#ansible-inventory)
  - [Playbooks, Tasks, Modules & Idempotency](#ansible-playbooks)
  - [Ansible Roles & Reusability](#ansible-roles)
- [Production Troubleshooting & Interview Q&A](#troubleshooting--interview-qa)

---

# PART 1: JENKINS CI/CD AUTOMATION

➔S➔E➔C➔T➔I➔O➔N➔ ➔4➔:➔ ➔J➔E➔N➔K➔I➔N➔S➔
➔
➔
➔
➔
➔Q➔1➔.➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔J➔e➔n➔k➔i➔n➔s➔ ➔a➔n➔d➔ ➔w➔h➔y➔ ➔d➔o➔e➔s➔ ➔a➔ ➔D➔e➔v➔O➔p➔s➔ ➔e➔n➔g➔i➔n➔e➔e➔r➔ ➔u➔s➔e➔ ➔i➔t➔?➔
➔A➔n➔s➔w➔e➔r➔:➔
➔J➔e➔n➔k➔i➔n➔s➔ ➔i➔s➔ ➔a➔n➔ ➔o➔p➔e➔n➔-➔s➔o➔u➔r➔c➔e➔ ➔a➔u➔t➔o➔m➔a➔t➔i➔o➔n➔ ➔s➔e➔r➔v➔e➔r➔ ➔u➔s➔e➔d➔ ➔t➔o➔ ➔b➔u➔i➔l➔d➔ ➔C➔I➔/➔C➔D➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔s➔.➔ ➔I➔t➔ ➔a➔u➔t➔o➔m➔a➔t➔i➔c➔a➔l➔l➔y➔ ➔t➔r➔i➔g➔g➔e➔r➔s➔ ➔b➔u➔i➔l➔d➔s➔ ➔w➔h➔e➔n➔
➔c➔o➔d➔e➔ ➔i➔s➔ ➔p➔u➔s➔h➔e➔d➔,➔ ➔r➔u➔n➔s➔ ➔t➔e➔s➔t➔s➔,➔ ➔b➔u➔i➔l➔d➔s➔ ➔a➔r➔t➔i➔f➔a➔c➔t➔s➔,➔ ➔a➔n➔d➔ ➔d➔e➔p➔l➔o➔y➔s➔ ➔t➔o➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔s➔ ➔—➔ ➔w➔i➔t➔h➔o➔u➔t➔ ➔m➔a➔n➔u➔a➔l➔ ➔i➔n➔t➔e➔r➔v➔e➔n➔t➔i➔o➔n➔.➔
➔I➔n➔t➔e➔g➔r➔a➔t➔i➔o➔n➔s➔:➔ ➔G➔i➔t➔,➔ ➔D➔o➔c➔k➔e➔r➔,➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔,➔ ➔N➔e➔x➔u➔s➔,➔ ➔A➔r➔t➔i➔f➔a➔c➔t➔o➔r➔y➔,➔ ➔S➔o➔n➔a➔r➔Q➔u➔b➔e➔,➔ ➔S➔l➔a➔c➔k➔
➔W➔h➔y➔ ➔D➔e➔v➔O➔p➔s➔ ➔u➔s➔e➔s➔ ➔i➔t➔:➔
➔A➔u➔t➔o➔m➔a➔t➔e➔s➔ ➔t➔h➔e➔ ➔e➔n➔t➔i➔r➔e➔ ➔r➔e➔l➔e➔a➔s➔e➔ ➔p➔r➔o➔c➔e➔s➔s➔
➔C➔a➔t➔c➔h➔e➔s➔ ➔b➔u➔g➔s➔ ➔e➔a➔r➔l➔y➔ ➔v➔i➔a➔ ➔a➔u➔t➔o➔m➔a➔t➔e➔d➔ ➔t➔e➔s➔t➔i➔n➔g➔
➔C➔o➔n➔s➔i➔s➔t➔e➔n➔t➔,➔ ➔r➔e➔p➔e➔a➔t➔a➔b➔l➔e➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔s➔
➔S➔a➔v➔e➔s➔ ➔t➔i➔m➔e➔ ➔—➔ ➔n➔o➔ ➔m➔a➔n➔u➔a➔l➔ ➔b➔u➔i➔l➔d➔/➔d➔e➔p➔l➔o➔y➔ ➔s➔t➔e➔p➔s➔
➔Q➔2➔.➔ ➔W➔h➔a➔t➔ ➔a➔r➔e➔ ➔J➔e➔n➔k➔i➔n➔s➔ ➔J➔o➔b➔ ➔T➔y➔p➔e➔s➔?➔
➔A➔n➔s➔w➔e➔r➔:➔
➔J➔o➔b➔ ➔T➔y➔p➔e➔ ➔D➔e➔s➔c➔r➔i➔p➔t➔i➔o➔n➔ ➔U➔s➔e➔ ➔c➔a➔s➔e➔
➔F➔r➔e➔e➔s➔t➔y➔l➔e➔ ➔M➔a➔n➔u➔a➔l➔ ➔U➔I➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔,➔ ➔b➔u➔i➔l➔d➔ ➔s➔t➔e➔p➔s➔ ➔d➔e➔f➔i➔n➔e➔d➔ ➔i➔n➔ ➔U➔I➔ ➔S➔i➔m➔p➔l➔e➔,➔ ➔l➔e➔g➔a➔c➔y➔ ➔j➔o➔b➔s➔
➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔J➔e➔n➔k➔i➔n➔s➔f➔i➔l➔e➔ ➔w➔r➔i➔t➔t➔e➔n➔ ➔i➔n➔ ➔G➔r➔o➔o➔v➔y➔,➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔a➔s➔ ➔C➔o➔d➔e➔ ➔M➔o➔d➔e➔r➔n➔ ➔s➔t➔a➔n➔d➔a➔r➔d➔
➔M➔u➔l➔t➔i➔b➔r➔a➔n➔c➔h➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔A➔u➔t➔o➔-➔c➔r➔e➔a➔t➔e➔s➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔s➔ ➔f➔o➔r➔ ➔e➔a➔c➔h➔ ➔G➔i➔t➔ ➔b➔r➔a➔n➔c➔h➔ ➔F➔e➔a➔t➔u➔r➔e➔ ➔b➔r➔a➔n➔c➔h➔ ➔w➔o➔r➔k➔f➔l➔o➔w➔s➔
➔F➔o➔r➔ ➔i➔n➔t➔e➔r➔v➔i➔e➔w➔s➔:➔ ➔A➔l➔w➔a➔y➔s➔ ➔t➔a➔l➔k➔ ➔a➔b➔o➔u➔t➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔j➔o➔b➔s➔ ➔w➔i➔t➔h➔ ➔J➔e➔n➔k➔i➔n➔s➔f➔i➔l➔e➔ ➔—➔ ➔t➔h➔a➔t➔'➔s➔ ➔t➔h➔e➔ ➔i➔n➔d➔u➔s➔t➔r➔y➔ ➔s➔t➔a➔n➔d➔a➔r➔d➔.➔
➔Q➔3➔.➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔ ➔J➔e➔n➔k➔i➔n➔s➔f➔i➔l➔e➔?➔
➔A➔n➔s➔w➔e➔r➔:➔
➔A➔ ➔J➔e➔n➔k➔i➔n➔s➔f➔i➔l➔e➔ ➔i➔s➔ ➔a➔ ➔t➔e➔x➔t➔ ➔f➔i➔l➔e➔ ➔w➔r➔i➔t➔t➔e➔n➔ ➔i➔n➔ ➔G➔r➔o➔o➔v➔y➔ ➔t➔h➔a➔t➔ ➔d➔e➔f➔i➔n➔e➔s➔ ➔y➔o➔u➔r➔ ➔e➔n➔t➔i➔r➔e➔ ➔C➔I➔/➔C➔D➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔a➔s➔ ➔c➔o➔d➔e➔.➔ ➔I➔t➔ ➔l➔i➔v➔e➔s➔ ➔i➔n➔ ➔y➔o➔u➔r➔ ➔G➔i➔t➔
➔r➔e➔p➔o➔ ➔a➔l➔o➔n➔g➔s➔i➔d➔e➔ ➔y➔o➔u➔r➔ ➔a➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔ ➔c➔o➔d➔e➔.➔ ➔T➔h➔i➔s➔ ➔m➔e➔a➔n➔s➔ ➔y➔o➔u➔r➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔i➔s➔ ➔v➔e➔r➔s➔i➔o➔n➔ ➔c➔o➔n➔t➔r➔o➔l➔l➔e➔d➔.➔
➔E➔x➔a➔m➔p➔l➔e➔ ➔J➔e➔n➔k➔i➔n➔s➔f➔i➔l➔e➔:➔
➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔{➔
➔ ➔ ➔ ➔ ➔a➔g➔e➔n➔t➔ ➔a➔n➔y➔
➔
➔
➔
➔
➔ ➔ ➔ ➔ ➔s➔t➔a➔g➔e➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔g➔e➔(➔'➔C➔h➔e➔c➔k➔o➔u➔t➔'➔)➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔g➔i➔t➔ ➔'➔h➔t➔t➔p➔s➔:➔/➔/➔g➔i➔t➔h➔u➔b➔.➔c➔o➔m➔/➔A➔k➔h➔i➔l➔N➔i➔k➔h➔i➔l➔/➔m➔y➔a➔p➔p➔.➔g➔i➔t➔'➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔g➔e➔(➔'➔B➔u➔i➔l➔d➔'➔)➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔h➔ ➔'➔m➔v➔n➔ ➔c➔l➔e➔a➔n➔ ➔p➔a➔c➔k➔a➔g➔e➔'➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔g➔e➔(➔'➔T➔e➔s➔t➔'➔)➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔h➔ ➔'➔m➔v➔n➔ ➔t➔e➔s➔t➔'➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔g➔e➔(➔'➔D➔o➔c➔k➔e➔r➔ ➔B➔u➔i➔l➔d➔ ➔&➔ ➔P➔u➔s➔h➔'➔)➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔h➔ ➔'➔d➔o➔c➔k➔e➔r➔ ➔b➔u➔i➔l➔d➔ ➔-➔t➔ ➔m➔y➔a➔p➔p➔:➔1➔.➔0➔ ➔.➔'➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔h➔ ➔'➔d➔o➔c➔k➔e➔r➔ ➔p➔u➔s➔h➔ ➔m➔y➔r➔e➔p➔o➔/➔m➔y➔a➔p➔p➔:➔1➔.➔0➔'➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔g➔e➔(➔'➔D➔e➔p➔l➔o➔y➔ ➔t➔o➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔'➔)➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔h➔ ➔'➔k➔u➔b➔e➔c➔t➔l➔ ➔a➔p➔p➔l➔y➔ ➔-➔f➔ ➔k➔8➔s➔/➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔.➔y➔a➔m➔l➔'➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔p➔o➔s➔t➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔u➔c➔c➔e➔s➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔e➔c➔h➔o➔ ➔'➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔s➔u➔c➔c➔e➔e➔d➔e➔d➔!➔'➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔f➔a➔i➔l➔u➔r➔e➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔e➔c➔h➔o➔ ➔'➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔f➔a➔i➔l➔e➔d➔!➔'➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔}➔
➔}➔
➔B➔e➔n➔e➔f➔i➔t➔s➔:➔ ➔V➔e➔r➔s➔i➔o➔n➔ ➔c➔o➔n➔t➔r➔o➔l➔l➔e➔d➔,➔ ➔r➔e➔v➔i➔e➔w➔a➔b➔l➔e➔,➔ ➔c➔o➔n➔s➔i➔s➔t➔e➔n➔t➔,➔ ➔r➔e➔u➔s➔a➔b➔l➔e➔.➔
➔
➔
➔
➔
➔Q➔4➔.➔ ➔W➔h➔a➔t➔ ➔a➔r➔e➔ ➔C➔o➔m➔m➔o➔n➔ ➔C➔I➔/➔C➔D➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔S➔t➔a➔g➔e➔s➔?➔
➔A➔n➔s➔w➔e➔r➔:➔
➔S➔t➔a➔g➔e➔ ➔W➔h➔a➔t➔ ➔i➔t➔ ➔d➔o➔e➔s➔
➔C➔h➔e➔c➔k➔o➔u➔t➔ ➔P➔u➔l➔l➔ ➔l➔a➔t➔e➔s➔t➔ ➔c➔o➔d➔e➔ ➔f➔r➔o➔m➔ ➔G➔i➔t➔
➔B➔u➔i➔l➔d➔ ➔C➔o➔m➔p➔i➔l➔e➔ ➔c➔o➔d➔e➔,➔ ➔c➔r➔e➔a➔t➔e➔ ➔J➔A➔R➔/➔W➔A➔R➔/➔b➔i➔n➔a➔r➔y➔
➔T➔e➔s➔t➔ ➔R➔u➔n➔ ➔u➔n➔i➔t➔ ➔t➔e➔s➔t➔s➔,➔ ➔i➔n➔t➔e➔g➔r➔a➔t➔i➔o➔n➔ ➔t➔e➔s➔t➔s➔
➔C➔o➔d➔e➔ ➔Q➔u➔a➔l➔i➔t➔y➔ ➔S➔o➔n➔a➔r➔Q➔u➔b➔e➔ ➔s➔c➔a➔n➔ ➔f➔o➔r➔ ➔c➔o➔d➔e➔ ➔s➔m➔e➔l➔l➔s➔,➔ ➔b➔u➔g➔s➔
➔S➔e➔c➔u➔r➔i➔t➔y➔ ➔S➔c➔a➔n➔ ➔C➔h➔e➔c➔k➔ ➔f➔o➔r➔ ➔v➔u➔l➔n➔e➔r➔a➔b➔i➔l➔i➔t➔i➔e➔s➔
➔D➔o➔c➔k➔e➔r➔ ➔B➔u➔i➔l➔d➔ ➔B➔u➔i➔l➔d➔ ➔D➔o➔c➔k➔e➔r➔ ➔i➔m➔a➔g➔e➔
➔P➔u➔s➔h➔ ➔t➔o➔ ➔R➔e➔g➔i➔s➔t➔r➔y➔ ➔P➔u➔s➔h➔ ➔i➔m➔a➔g➔e➔ ➔t➔o➔ ➔E➔C➔R➔/➔A➔C➔R➔/➔D➔o➔c➔k➔e➔r➔ ➔H➔u➔b➔
➔D➔e➔p➔l➔o➔y➔ ➔t➔o➔ ➔S➔t➔a➔g➔i➔n➔g➔ ➔D➔e➔p➔l➔o➔y➔ ➔t➔o➔ ➔t➔e➔s➔t➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔
➔D➔e➔p➔l➔o➔y➔ ➔t➔o➔ ➔P➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔D➔e➔p➔l➔o➔y➔ ➔t➔o➔ ➔l➔i➔v➔e➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔
➔Q➔5➔.➔ ➔W➔h➔a➔t➔ ➔a➔r➔e➔ ➔J➔e➔n➔k➔i➔n➔s➔ ➔T➔r➔i➔g➔g➔e➔r➔s➔?➔
➔A➔n➔s➔w➔e➔r➔:➔
➔T➔r➔i➔g➔g➔e➔r➔s➔ ➔t➔e➔l➔l➔ ➔J➔e➔n➔k➔i➔n➔s➔ ➔w➔h➔e➔n➔ ➔t➔o➔ ➔r➔u➔n➔ ➔a➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔a➔u➔t➔o➔m➔a➔t➔i➔c➔a➔l➔l➔y➔.➔
➔T➔r➔i➔g➔g➔e➔r➔ ➔H➔o➔w➔ ➔i➔t➔ ➔w➔o➔r➔k➔s➔ ➔B➔e➔s➔t➔ ➔f➔o➔r➔
➔W➔e➔b➔h➔o➔o➔k➔ ➔G➔i➔t➔ ➔s➔e➔n➔d➔s➔ ➔n➔o➔t➔i➔f➔i➔c➔a➔t➔i➔o➔n➔ ➔t➔o➔ ➔J➔e➔n➔k➔i➔n➔s➔ ➔o➔n➔ ➔c➔o➔d➔e➔ ➔p➔u➔s➔h➔.➔ ➔I➔n➔s➔t➔a➔n➔t➔.➔ ➔P➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔—➔ ➔f➔a➔s➔t➔e➔s➔t➔
➔P➔o➔l➔l➔ ➔S➔C➔M➔ ➔J➔e➔n➔k➔i➔n➔s➔ ➔c➔h➔e➔c➔k➔s➔ ➔G➔i➔t➔ ➔r➔e➔p➔o➔ ➔e➔v➔e➔r➔y➔ ➔X➔ ➔m➔i➔n➔u➔t➔e➔s➔ ➔f➔o➔r➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔L➔e➔g➔a➔c➔y➔ ➔s➔y➔s➔t➔e➔m➔s➔
➔S➔c➔h➔e➔d➔u➔l➔e➔d➔ ➔R➔u➔n➔s➔ ➔o➔n➔ ➔c➔r➔o➔n➔ ➔s➔c➔h➔e➔d➔u➔l➔e➔ ➔(➔e➔.➔g➔.➔,➔ ➔e➔v➔e➔r➔y➔ ➔n➔i➔g➔h➔t➔ ➔a➔t➔ ➔2➔a➔m➔)➔ ➔N➔i➔g➔h➔t➔l➔y➔ ➔b➔u➔i➔l➔d➔s➔
➔M➔a➔n➔u➔a➔l➔ ➔C➔l➔i➔c➔k➔ ➔"➔B➔u➔i➔l➔d➔ ➔N➔o➔w➔"➔ ➔i➔n➔ ➔J➔e➔n➔k➔i➔n➔s➔ ➔U➔I➔ ➔O➔n➔-➔d➔e➔m➔a➔n➔d➔
➔U➔p➔s➔t➔r➔e➔a➔m➔ ➔J➔o➔b➔ ➔O➔n➔e➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔t➔r➔i➔g➔g➔e➔r➔s➔ ➔a➔n➔o➔t➔h➔e➔r➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔c➔h➔a➔i➔n➔i➔n➔g➔
➔E➔x➔a➔m➔p➔l➔e➔ ➔W➔e➔b➔h➔o➔o➔k➔ ➔t➔r➔i➔g➔g➔e➔r➔ ➔i➔n➔ ➔J➔e➔n➔k➔i➔n➔s➔f➔i➔l➔e➔:➔
➔
➔
➔
➔
➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔{➔
➔ ➔ ➔ ➔ ➔a➔g➔e➔n➔t➔ ➔a➔n➔y➔
➔ ➔ ➔ ➔ ➔t➔r➔i➔g➔g➔e➔r➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔g➔i➔t➔h➔u➔b➔P➔u➔s➔h➔(➔)➔ ➔ ➔ ➔/➔/➔ ➔t➔r➔i➔g➔g➔e➔r➔s➔ ➔o➔n➔ ➔e➔v➔e➔r➔y➔ ➔G➔i➔t➔H➔u➔b➔ ➔p➔u➔s➔h➔
➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔s➔t➔a➔g➔e➔s➔ ➔{➔ ➔.➔.➔.➔ ➔}➔
➔}➔
➔B➔e➔s➔t➔ ➔p➔r➔a➔c➔t➔i➔c➔e➔:➔ ➔A➔l➔w➔a➔y➔s➔ ➔u➔s➔e➔ ➔W➔e➔b➔h➔o➔o➔k➔s➔ ➔—➔ ➔i➔n➔s➔t➔a➔n➔t➔ ➔r➔e➔s➔p➔o➔n➔s➔e➔ ➔w➔h➔e➔n➔ ➔c➔o➔d➔e➔ ➔i➔s➔ ➔p➔u➔s➔h➔e➔d➔.➔
➔Q➔6➔.➔ ➔D➔e➔c➔l➔a➔r➔a➔t➔i➔v➔e➔ ➔v➔s➔ ➔S➔c➔r➔i➔p➔t➔e➔d➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔
➔A➔n➔s➔w➔e➔r➔:➔
➔F➔e➔a➔t➔u➔r➔e➔ ➔D➔e➔c➔l➔a➔r➔a➔t➔i➔v➔e➔ ➔S➔c➔r➔i➔p➔t➔e➔d➔
➔S➔y➔n➔t➔a➔x➔ ➔S➔t➔r➔u➔c➔t➔u➔r➔e➔d➔,➔ ➔f➔i➔x➔e➔d➔ ➔f➔o➔r➔m➔a➔t➔ ➔F➔u➔l➔l➔ ➔G➔r➔o➔o➔v➔y➔ ➔p➔r➔o➔g➔r➔a➔m➔m➔i➔n➔g➔
➔R➔e➔a➔d➔a➔b➔i➔l➔i➔t➔y➔ ➔E➔a➔s➔y➔ ➔t➔o➔ ➔r➔e➔a➔d➔ ➔C➔o➔m➔p➔l➔e➔x➔
➔F➔l➔e➔x➔i➔b➔i➔l➔i➔t➔y➔ ➔L➔i➔m➔i➔t➔e➔d➔ ➔V➔e➔r➔y➔ ➔f➔l➔e➔x➔i➔b➔l➔e➔
➔S➔t➔a➔n➔d➔a➔r➔d➔ ➔M➔o➔d➔e➔r➔n➔ ➔s➔t➔a➔n➔d➔a➔r➔d➔ ➔✅➔ ➔L➔e➔g➔a➔c➔y➔
➔D➔e➔c➔l➔a➔r➔a➔t➔i➔v➔e➔ ➔E➔x➔a➔m➔p➔l➔e➔:➔
➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔{➔
➔ ➔ ➔ ➔ ➔a➔g➔e➔n➔t➔ ➔a➔n➔y➔
➔ ➔ ➔ ➔ ➔s➔t➔a➔g➔e➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔g➔e➔(➔'➔B➔u➔i➔l➔d➔'➔)➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔h➔ ➔'➔m➔v➔n➔ ➔b➔u➔i➔l➔d➔'➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔}➔
➔}➔
➔S➔c➔r➔i➔p➔t➔e➔d➔ ➔E➔x➔a➔m➔p➔l➔e➔:➔
➔n➔o➔d➔e➔ ➔{➔
➔ ➔ ➔ ➔ ➔s➔t➔a➔g➔e➔(➔'➔B➔u➔i➔l➔d➔'➔)➔ ➔{➔
➔
➔
➔
➔
➔➔ ➔➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔i➔f➔ ➔(➔e➔n➔v➔.➔B➔R➔A➔N➔C➔H➔_➔N➔A➔M➔E➔ ➔=➔=➔ ➔'➔m➔a➔s➔t➔e➔r➔'➔)➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔h➔ ➔'➔m➔v➔n➔ ➔b➔u➔i➔l➔d➔'➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔}➔
➔}➔
➔F➔o➔r➔ ➔i➔n➔t➔e➔r➔v➔i➔e➔w➔s➔:➔ ➔A➔l➔w➔a➔y➔s➔ ➔s➔a➔y➔ ➔D➔e➔c➔l➔a➔r➔a➔t➔i➔v➔e➔ ➔i➔s➔ ➔b➔e➔t➔t➔e➔r➔ ➔—➔ ➔m➔o➔d➔e➔r➔n➔ ➔s➔t➔a➔n➔d➔a➔r➔d➔,➔ ➔e➔a➔s➔i➔e➔r➔ ➔t➔o➔ ➔m➔a➔i➔n➔t➔a➔i➔n➔.➔
➔Q➔7➔.➔ ➔H➔o➔w➔ ➔t➔o➔ ➔M➔a➔n➔a➔g➔e➔ ➔S➔e➔c➔r➔e➔t➔s➔ ➔i➔n➔ ➔J➔e➔n➔k➔i➔n➔s➔?➔
➔A➔n➔s➔w➔e➔r➔:➔
➔N➔e➔v➔e➔r➔ ➔h➔a➔r➔d➔c➔o➔d➔e➔ ➔s➔e➔c➔r➔e➔t➔s➔ ➔i➔n➔ ➔J➔e➔n➔k➔i➔n➔s➔f➔i➔l➔e➔.➔ ➔U➔s➔e➔ ➔J➔e➔n➔k➔i➔n➔s➔ ➔C➔r➔e➔d➔e➔n➔t➔i➔a➔l➔s➔ ➔S➔t➔o➔r➔e➔.➔
➔T➔y➔p➔e➔s➔ ➔o➔f➔ ➔c➔r➔e➔d➔e➔n➔t➔i➔a➔l➔s➔:➔
➔U➔s➔e➔r➔n➔a➔m➔e➔/➔P➔a➔s➔s➔w➔o➔r➔d➔ ➔—➔ ➔D➔o➔c➔k➔e➔r➔ ➔H➔u➔b➔,➔ ➔G➔i➔t➔
➔S➔S➔H➔ ➔K➔e➔y➔ ➔—➔ ➔s➔e➔r➔v➔e➔r➔ ➔a➔c➔c➔e➔s➔s➔
➔S➔e➔c➔r➔e➔t➔ ➔T➔e➔x➔t➔ ➔—➔ ➔A➔P➔I➔ ➔t➔o➔k➔e➔n➔s➔,➔ ➔k➔e➔y➔s➔
➔C➔e➔r➔t➔i➔f➔i➔c➔a➔t➔e➔ ➔—➔ ➔S➔S➔L➔ ➔c➔e➔r➔t➔s➔
➔E➔x➔a➔m➔p➔l➔e➔ ➔u➔s➔i➔n➔g➔ ➔c➔r➔e➔d➔e➔n➔t➔i➔a➔l➔s➔ ➔i➔n➔ ➔J➔e➔n➔k➔i➔n➔s➔f➔i➔l➔e➔:➔
➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔{➔
➔ ➔ ➔ ➔ ➔a➔g➔e➔n➔t➔ ➔a➔n➔y➔
➔ ➔ ➔ ➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔D➔O➔C➔K➔E➔R➔_➔C➔R➔E➔D➔S➔ ➔=➔ ➔c➔r➔e➔d➔e➔n➔t➔i➔a➔l➔s➔(➔'➔d➔o➔c➔k➔e➔r➔-➔h➔u➔b➔-➔c➔r➔e➔d➔e➔n➔t➔i➔a➔l➔s➔'➔)➔
➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔s➔t➔a➔g➔e➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔g➔e➔(➔'➔P➔u➔s➔h➔ ➔I➔m➔a➔g➔e➔'➔)➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔h➔ ➔'➔'➔'➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔e➔c➔h➔o➔ ➔$➔D➔O➔C➔K➔E➔R➔_➔C➔R➔E➔D➔S➔_➔P➔S➔W➔ ➔|➔ ➔d➔o➔c➔k➔e➔r➔ ➔l➔o➔g➔i➔n➔ ➔-➔u➔ ➔$➔D➔O➔C➔K➔E➔R➔_➔C➔R➔E➔D➔S➔_➔U➔S➔R➔ ➔-➔-➔p➔a➔s➔s➔w➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔ ➔p➔u➔s➔h➔ ➔m➔y➔r➔e➔p➔o➔/➔m➔y➔a➔p➔p➔:➔1➔.➔0➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔'➔'➔'➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔}➔
➔}➔
➔R➔u➔l➔e➔:➔ ➔C➔r➔e➔d➔e➔n➔t➔i➔a➔l➔s➔ ➔a➔r➔e➔ ➔i➔n➔j➔e➔c➔t➔e➔d➔ ➔a➔t➔ ➔r➔u➔n➔t➔i➔m➔e➔ ➔—➔ ➔n➔e➔v➔e➔r➔ ➔v➔i➔s➔i➔b➔l➔e➔ ➔i➔n➔ ➔l➔o➔g➔s➔ ➔o➔r➔ ➔G➔i➔t➔ ➔h➔i➔s➔t➔o➔r➔y➔.➔
➔
➔
➔
➔
➔Q➔8➔.➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔J➔e➔n➔k➔i➔n➔s➔ ➔M➔a➔s➔t➔e➔r➔ ➔a➔n➔d➔ ➔A➔g➔e➔n➔t➔?➔
➔A➔n➔s➔w➔e➔r➔:➔
➔M➔a➔s➔t➔e➔r➔ ➔(➔C➔o➔n➔t➔r➔o➔l➔l➔e➔r➔)➔ ➔—➔ ➔m➔a➔n➔a➔g➔e➔s➔ ➔j➔o➔b➔s➔,➔ ➔s➔c➔h➔e➔d➔u➔l➔e➔s➔ ➔b➔u➔i➔l➔d➔s➔,➔ ➔s➔t➔o➔r➔e➔s➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔s➔,➔ ➔s➔e➔r➔v➔e➔s➔ ➔t➔h➔e➔ ➔U➔I➔.➔ ➔D➔o➔e➔s➔ ➔N➔O➔T➔ ➔r➔u➔n➔
➔b➔u➔i➔l➔d➔s➔ ➔i➔t➔s➔e➔l➔f➔.➔
➔A➔g➔e➔n➔t➔ ➔(➔W➔o➔r➔k➔e➔r➔)➔ ➔—➔ ➔e➔x➔e➔c➔u➔t➔e➔s➔ ➔t➔h➔e➔ ➔a➔c➔t➔u➔a➔l➔ ➔b➔u➔i➔l➔d➔ ➔j➔o➔b➔s➔.➔ ➔C➔a➔n➔ ➔h➔a➔v➔e➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔a➔g➔e➔n➔t➔s➔ ➔w➔i➔t➔h➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔t➔ ➔s➔e➔t➔u➔p➔s➔.➔
➔W➔h➔y➔ ➔u➔s➔e➔ ➔a➔g➔e➔n➔t➔s➔:➔
➔M➔a➔s➔t➔e➔r➔ ➔s➔t➔a➔y➔s➔ ➔l➔i➔g➔h➔t➔w➔e➔i➔g➔h➔t➔
➔S➔c➔a➔l➔e➔ ➔b➔y➔ ➔a➔d➔d➔i➔n➔g➔ ➔m➔o➔r➔e➔ ➔a➔g➔e➔n➔t➔s➔
➔D➔i➔f➔f➔e➔r➔e➔n➔t➔ ➔a➔g➔e➔n➔t➔s➔ ➔f➔o➔r➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔t➔ ➔j➔o➔b➔s➔ ➔(➔D➔o➔c➔k➔e➔r➔ ➔a➔g➔e➔n➔t➔,➔ ➔J➔a➔v➔a➔ ➔a➔g➔e➔n➔t➔,➔ ➔e➔t➔c➔.➔)➔
➔E➔x➔a➔m➔p➔l➔e➔ ➔i➔n➔ ➔J➔e➔n➔k➔i➔n➔s➔f➔i➔l➔e➔:➔
➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔{➔
➔ ➔ ➔ ➔ ➔a➔g➔e➔n➔t➔ ➔{➔ ➔l➔a➔b➔e➔l➔ ➔'➔d➔o➔c➔k➔e➔r➔'➔ ➔}➔ ➔ ➔ ➔/➔/➔ ➔r➔u➔n➔ ➔o➔n➔l➔y➔ ➔o➔n➔ ➔a➔g➔e➔n➔t➔ ➔l➔a➔b➔e➔l➔l➔e➔d➔ ➔'➔d➔o➔c➔k➔e➔r➔'➔
➔ ➔ ➔ ➔ ➔s➔t➔a➔g➔e➔s➔ ➔{➔ ➔.➔.➔.➔ ➔}➔
➔}➔
➔/➔/➔ ➔O➔R➔
➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔{➔
➔ ➔ ➔ ➔ ➔a➔g➔e➔n➔t➔ ➔a➔n➔y➔ ➔ ➔ ➔ ➔/➔/➔ ➔r➔u➔n➔ ➔o➔n➔ ➔a➔n➔y➔ ➔a➔v➔a➔i➔l➔a➔b➔l➔e➔ ➔a➔g➔e➔n➔t➔
➔ ➔ ➔ ➔ ➔s➔t➔a➔g➔e➔s➔ ➔{➔ ➔.➔.➔.➔ ➔}➔
➔}➔
➔Q➔9➔.➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔ ➔J➔e➔n➔k➔i➔n➔s➔ ➔S➔h➔a➔r➔e➔d➔ ➔L➔i➔b➔r➔a➔r➔y➔?➔
➔A➔n➔s➔w➔e➔r➔:➔
➔R➔e➔u➔s➔a➔b➔l➔e➔ ➔G➔r➔o➔o➔v➔y➔ ➔c➔o➔d➔e➔ ➔s➔h➔a➔r➔e➔d➔ ➔a➔c➔r➔o➔s➔s➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔s➔.➔ ➔W➔r➔i➔t➔e➔ ➔o➔n➔c➔e➔,➔ ➔u➔s➔e➔ ➔e➔v➔e➔r➔y➔w➔h➔e➔r➔e➔.➔
➔S➔t➔r➔u➔c➔t➔u➔r➔e➔:➔
➔s➔h➔a➔r➔e➔d➔-➔l➔i➔b➔r➔a➔r➔y➔/➔
➔ ➔ ➔v➔a➔r➔s➔/➔
➔ ➔ ➔ ➔ ➔d➔e➔p➔l➔o➔y➔.➔g➔r➔o➔o➔v➔y➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔u➔s➔a➔b➔l➔e➔ ➔d➔e➔p➔l➔o➔y➔ ➔f➔u➔n➔c➔t➔i➔o➔n➔
➔ ➔ ➔ ➔ ➔t➔e➔s➔t➔.➔g➔r➔o➔o➔v➔y➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔u➔s➔a➔b➔l➔e➔ ➔t➔e➔s➔t➔ ➔f➔u➔n➔c➔t➔i➔o➔n➔
➔U➔s➔a➔g➔e➔ ➔i➔n➔ ➔J➔e➔n➔k➔i➔n➔s➔f➔i➔l➔e➔:➔
➔
➔
➔
➔
➔@➔L➔i➔b➔r➔a➔r➔y➔(➔'➔m➔y➔-➔s➔h➔a➔r➔e➔d➔-➔l➔i➔b➔r➔a➔r➔y➔'➔)➔ ➔_➔
➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔{➔
➔ ➔ ➔ ➔ ➔a➔g➔e➔n➔t➔ ➔a➔n➔y➔
➔ ➔ ➔ ➔ ➔s➔t➔a➔g➔e➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔g➔e➔(➔'➔D➔e➔p➔l➔o➔y➔'➔)➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔e➔p➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔c➔r➔i➔p➔t➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔e➔p➔l➔o➔y➔(➔'➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔'➔)➔ ➔ ➔ ➔/➔/➔ ➔c➔a➔l➔l➔ ➔s➔h➔a➔r➔e➔d➔ ➔f➔u➔n➔c➔t➔i➔o➔n➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔}➔
➔}➔
➔B➔e➔n➔e➔f➔i➔t➔s➔:➔ ➔N➔o➔ ➔c➔o➔d➔e➔ ➔d➔u➔p➔l➔i➔c➔a➔t➔i➔o➔n➔,➔ ➔u➔p➔d➔a➔t➔e➔ ➔i➔n➔ ➔o➔n➔e➔ ➔p➔l➔a➔c➔e➔,➔ ➔c➔o➔n➔s➔i➔s➔t➔e➔n➔t➔ ➔a➔c➔r➔o➔s➔s➔ ➔a➔l➔l➔ ➔t➔e➔a➔m➔s➔.➔
➔Q➔1➔0➔.➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔B➔l➔u➔e➔ ➔O➔c➔e➔a➔n➔ ➔i➔n➔ ➔J➔e➔n➔k➔i➔n➔s➔?➔
➔A➔n➔s➔w➔e➔r➔:➔
➔B➔l➔u➔e➔ ➔O➔c➔e➔a➔n➔ ➔i➔s➔ ➔J➔e➔n➔k➔i➔n➔s➔'➔s➔ ➔m➔o➔d➔e➔r➔n➔ ➔U➔I➔ ➔f➔o➔r➔ ➔v➔i➔s➔u➔a➔l➔i➔z➔i➔n➔g➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔s➔.➔ ➔T➔r➔a➔d➔i➔t➔i➔o➔n➔a➔l➔ ➔J➔e➔n➔k➔i➔n➔s➔ ➔U➔I➔ ➔i➔s➔ ➔c➔l➔u➔t➔t➔e➔r➔e➔d➔ ➔a➔n➔d➔ ➔h➔a➔r➔d➔ ➔t➔o➔ ➔r➔e➔a➔d➔.➔
➔B➔l➔u➔e➔ ➔O➔c➔e➔a➔n➔ ➔s➔h➔o➔w➔s➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔s➔ ➔a➔s➔ ➔a➔ ➔v➔i➔s➔u➔a➔l➔ ➔f➔l➔o➔w➔c➔h➔a➔r➔t➔.➔
➔F➔e➔a➔t➔u➔r➔e➔s➔:➔
➔V➔i➔s➔u➔a➔l➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔v➔i➔e➔w➔ ➔—➔ ➔e➔a➔c➔h➔ ➔s➔t➔a➔g➔e➔ ➔a➔s➔ ➔a➔ ➔b➔o➔x➔
➔G➔r➔e➔e➔n➔ ➔=➔ ➔s➔u➔c➔c➔e➔s➔s➔,➔ ➔R➔e➔d➔ ➔=➔ ➔f➔a➔i➔l➔e➔d➔
➔S➔e➔e➔ ➔e➔x➔a➔c➔t➔l➔y➔ ➔w➔h➔i➔c➔h➔ ➔s➔t➔a➔g➔e➔ ➔f➔a➔i➔l➔e➔d➔ ➔i➔n➔s➔t➔a➔n➔t➔l➔y➔
➔I➔n➔l➔i➔n➔e➔ ➔l➔o➔g➔s➔ ➔p➔e➔r➔ ➔s➔t➔a➔g➔e➔
➔P➔u➔l➔l➔ ➔r➔e➔q➔u➔e➔s➔t➔ ➔i➔n➔t➔e➔g➔r➔a➔t➔i➔o➔n➔
➔F➔o➔r➔ ➔i➔n➔t➔e➔r➔v➔i➔e➔w➔s➔:➔ ➔M➔e➔n➔t➔i➔o➔n➔ ➔i➔t➔ ➔a➔s➔ ➔t➔h➔e➔ ➔m➔o➔d➔e➔r➔n➔ ➔J➔e➔n➔k➔i➔n➔s➔ ➔U➔I➔ ➔t➔h➔a➔t➔ ➔i➔m➔p➔r➔o➔v➔e➔s➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔v➔i➔s➔i➔b➔i➔l➔i➔t➔y➔ ➔a➔n➔d➔ ➔t➔r➔o➔u➔b➔l➔e➔s➔h➔o➔o➔t➔i➔n➔g➔.➔
➔

---

# PART 2: ANSIBLE CONFIGURATION MANAGEMENT

➔S➔E➔C➔T➔I➔O➔N➔ ➔9➔:➔ ➔A➔N➔S➔I➔B➔L➔E➔ ➔—➔ ➔C➔O➔M➔P➔L➔E➔T➔E➔ ➔G➔U➔I➔D➔E➔
➔C➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔ ➔M➔a➔n➔a➔g➔e➔m➔e➔n➔t➔ ➔t➔o➔o➔l➔.➔ ➔W➔r➔i➔t➔e➔ ➔o➔n➔c➔e➔,➔ ➔a➔p➔p➔l➔y➔ ➔t➔o➔ ➔h➔u➔n➔d➔r➔e➔d➔s➔ ➔o➔f➔ ➔s➔e➔r➔v➔e➔r➔s➔.➔
➔
➔
➔
➔
➔1➔.➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔A➔n➔s➔i➔b➔l➔e➔?➔
➔D➔e➔f➔i➔n➔i➔t➔i➔o➔n➔:➔
➔A➔n➔s➔i➔b➔l➔e➔ ➔i➔s➔ ➔a➔n➔ ➔o➔p➔e➔n➔-➔s➔o➔u➔r➔c➔e➔ ➔a➔u➔t➔o➔m➔a➔t➔i➔o➔n➔ ➔t➔o➔o➔l➔ ➔f➔o➔r➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔ ➔m➔a➔n➔a➔g➔e➔m➔e➔n➔t➔,➔ ➔a➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔ ➔d➔e➔p➔l➔o➔y➔m➔e➔n➔t➔,➔ ➔a➔n➔d➔ ➔t➔a➔s➔k➔
➔a➔u➔t➔o➔m➔a➔t➔i➔o➔n➔.➔ ➔Y➔o➔u➔ ➔w➔r➔i➔t➔e➔ ➔s➔i➔m➔p➔l➔e➔ ➔Y➔A➔M➔L➔ ➔f➔i➔l➔e➔s➔ ➔c➔a➔l➔l➔e➔d➔ ➔P➔l➔a➔y➔b➔o➔o➔k➔s➔ ➔a➔n➔d➔ ➔A➔n➔s➔i➔b➔l➔e➔ ➔e➔x➔e➔c➔u➔t➔e➔s➔ ➔t➔h➔e➔m➔ ➔o➔n➔ ➔r➔e➔m➔o➔t➔e➔ ➔s➔e➔r➔v➔e➔r➔s➔.➔
➔W➔h➔y➔ ➔A➔n➔s➔i➔b➔l➔e➔?➔
➔B➔e➔f➔o➔r➔e➔ ➔A➔n➔s➔i➔b➔l➔e➔:➔ ➔S➔S➔H➔ ➔i➔n➔t➔o➔ ➔e➔a➔c➔h➔ ➔s➔e➔r➔v➔e➔r➔ ➔m➔a➔n➔u➔a➔l➔l➔y➔,➔ ➔r➔u➔n➔ ➔c➔o➔m➔m➔a➔n➔d➔s➔ ➔o➔n➔e➔ ➔b➔y➔ ➔o➔n➔e➔.➔ ➔W➔i➔t➔h➔ ➔1➔0➔0➔ ➔s➔e➔r➔v➔e➔r➔s➔,➔ ➔i➔t➔'➔s➔ ➔a➔
➔n➔i➔g➔h➔t➔m➔a➔r➔e➔.➔
➔W➔i➔t➔h➔ ➔A➔n➔s➔i➔b➔l➔e➔:➔ ➔W➔r➔i➔t➔e➔ ➔a➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔ ➔o➔n➔c➔e➔.➔ ➔R➔u➔n➔ ➔i➔t➔ ➔o➔n➔ ➔a➔l➔l➔ ➔1➔0➔0➔ ➔s➔e➔r➔v➔e➔r➔s➔ ➔s➔i➔m➔u➔l➔t➔a➔n➔e➔o➔u➔s➔l➔y➔.➔
➔K➔e➔y➔ ➔F➔e➔a➔t➔u➔r➔e➔s➔:➔
➔A➔g➔e➔n➔t➔l➔e➔s➔s➔ ➔—➔ ➔n➔o➔ ➔s➔o➔f➔t➔w➔a➔r➔e➔ ➔t➔o➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔o➔n➔ ➔t➔a➔r➔g➔e➔t➔ ➔s➔e➔r➔v➔e➔r➔s➔.➔ ➔U➔s➔e➔s➔ ➔S➔S➔H➔.➔
➔I➔d➔e➔m➔p➔o➔t➔e➔n➔t➔ ➔—➔ ➔r➔u➔n➔n➔i➔n➔g➔ ➔t➔h➔e➔ ➔s➔a➔m➔e➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔ ➔t➔w➔i➔c➔e➔ ➔g➔i➔v➔e➔s➔ ➔t➔h➔e➔ ➔s➔a➔m➔e➔ ➔r➔e➔s➔u➔l➔t➔.➔ ➔W➔o➔n➔'➔t➔ ➔b➔r➔e➔a➔k➔ ➔t➔h➔i➔n➔g➔s➔.➔
➔S➔i➔m➔p➔l➔e➔ ➔Y➔A➔M➔L➔ ➔—➔ ➔e➔a➔s➔y➔ ➔t➔o➔ ➔r➔e➔a➔d➔ ➔a➔n➔d➔ ➔w➔r➔i➔t➔e➔
➔P➔u➔s➔h➔-➔b➔a➔s➔e➔d➔ ➔—➔ ➔A➔n➔s➔i➔b➔l➔e➔ ➔c➔o➔n➔t➔r➔o➔l➔l➔e➔r➔ ➔p➔u➔s➔h➔e➔s➔ ➔c➔o➔m➔m➔a➔n➔d➔s➔ ➔t➔o➔ ➔s➔e➔r➔v➔e➔r➔s➔
➔L➔a➔r➔g➔e➔ ➔c➔o➔m➔m➔u➔n➔i➔t➔y➔ ➔—➔ ➔t➔h➔o➔u➔s➔a➔n➔d➔s➔ ➔o➔f➔ ➔p➔r➔e➔-➔b➔u➔i➔l➔t➔ ➔m➔o➔d➔u➔l➔e➔s➔
➔2➔.➔ ➔H➔o➔w➔ ➔A➔n➔s➔i➔b➔l➔e➔ ➔W➔o➔r➔k➔s➔
➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔A➔n➔s➔i➔b➔l➔e➔ ➔C➔o➔n➔t➔r➔o➔l➔ ➔N➔o➔d➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔(➔y➔o➔u➔r➔ ➔m➔a➔c➔h➔i➔n➔e➔ ➔/➔ ➔J➔e➔n➔k➔i➔n➔s➔ ➔s➔e➔r➔v➔e➔r➔)➔ ➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔I➔n➔v➔e➔n➔t➔o➔r➔y➔ ➔f➔i➔l➔e➔ ➔ ➔←➔ ➔l➔i➔s➔t➔ ➔o➔f➔ ➔s➔e➔r➔v➔e➔r➔s➔ ➔ ➔│➔
➔│➔ ➔ ➔P➔l➔a➔y➔b➔o➔o➔k➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔←➔ ➔w➔h➔a➔t➔ ➔t➔o➔ ➔d➔o➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔a➔n➔s➔i➔b➔l➔e➔ ➔c➔o➔m➔m➔a➔n➔d➔ ➔←➔ ➔e➔x➔e➔c➔u➔t➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┬➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔S➔S➔H➔ ➔(➔n➔o➔ ➔a➔g➔e➔n➔t➔ ➔n➔e➔e➔d➔e➔d➔)➔
➔ ➔ ➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┼➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔ ➔ ➔ ➔ ➔▼➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔▼➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔▼➔
➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔│➔S➔e➔r➔v➔e➔r➔ ➔1➔│➔ ➔│➔S➔e➔r➔v➔e➔r➔ ➔2➔│➔ ➔ ➔ ➔ ➔.➔.➔.➔ ➔ ➔ ➔ ➔│➔S➔e➔r➔v➔e➔r➔ ➔N➔│➔
➔│➔(➔t➔a➔r➔g➔e➔t➔)➔│➔ ➔│➔(➔t➔a➔r➔g➔e➔t➔)➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔(➔t➔a➔r➔g➔e➔t➔)➔│➔
➔└➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔
➔A➔n➔s➔i➔b➔l➔e➔ ➔P➔u➔s➔h➔ ➔v➔s➔ ➔C➔h➔e➔f➔/➔P➔u➔p➔p➔e➔t➔ ➔P➔u➔l➔l➔:➔
➔A➔n➔s➔i➔b➔l➔e➔ ➔C➔h➔e➔f➔/➔P➔u➔p➔p➔e➔t➔
➔
➔
➔
➔
➔A➔r➔c➔h➔i➔t➔e➔c➔t➔u➔r➔e➔ ➔P➔u➔s➔h➔ ➔(➔c➔o➔n➔t➔r➔o➔l➔ ➔→➔ ➔n➔o➔d➔e➔s➔)➔ ➔P➔u➔l➔l➔ ➔(➔n➔o➔d➔e➔s➔ ➔f➔e➔t➔c➔h➔ ➔c➔o➔n➔f➔i➔g➔)➔
➔A➔g➔e➔n➔t➔ ➔N➔o➔ ➔a➔g➔e➔n➔t➔ ➔n➔e➔e➔d➔e➔d➔ ➔A➔g➔e➔n➔t➔ ➔r➔e➔q➔u➔i➔r➔e➔d➔ ➔o➔n➔ ➔e➔a➔c➔h➔ ➔n➔o➔d➔e➔
➔L➔a➔n➔g➔u➔a➔g➔e➔ ➔Y➔A➔M➔L➔ ➔R➔u➔b➔y➔ ➔D➔S➔L➔
➔L➔e➔a➔r➔n➔i➔n➔g➔ ➔c➔u➔r➔v➔e➔ ➔E➔a➔s➔y➔ ➔S➔t➔e➔e➔p➔e➔r➔
➔3➔.➔ ➔A➔n➔s➔i➔b➔l➔e➔ ➔K➔e➔y➔ ➔C➔o➔m➔p➔o➔n➔e➔n➔t➔s➔
➔C➔o➔m➔p➔o➔n➔e➔n➔t➔ ➔D➔e➔s➔c➔r➔i➔p➔t➔i➔o➔n➔
➔C➔o➔n➔t➔r➔o➔l➔ ➔N➔o➔d➔e➔ ➔M➔a➔c➔h➔i➔n➔e➔ ➔w➔h➔e➔r➔e➔ ➔A➔n➔s➔i➔b➔l➔e➔ ➔i➔s➔ ➔i➔n➔s➔t➔a➔l➔l➔e➔d➔ ➔a➔n➔d➔ ➔r➔u➔n➔ ➔f➔r➔o➔m➔
➔M➔a➔n➔a➔g➔e➔d➔ ➔N➔o➔d➔e➔s➔ ➔T➔a➔r➔g➔e➔t➔ ➔s➔e➔r➔v➔e➔r➔s➔ ➔A➔n➔s➔i➔b➔l➔e➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔e➔s➔ ➔(➔n➔o➔ ➔A➔n➔s➔i➔b➔l➔e➔ ➔n➔e➔e➔d➔e➔d➔)➔
➔I➔n➔v➔e➔n➔t➔o➔r➔y➔ ➔L➔i➔s➔t➔ ➔o➔f➔ ➔m➔a➔n➔a➔g➔e➔d➔ ➔n➔o➔d➔e➔s➔ ➔(➔I➔P➔/➔h➔o➔s➔t➔n➔a➔m➔e➔)➔
➔P➔l➔a➔y➔b➔o➔o➔k➔ ➔Y➔A➔M➔L➔ ➔f➔i➔l➔e➔ ➔c➔o➔n➔t➔a➔i➔n➔i➔n➔g➔ ➔a➔u➔t➔o➔m➔a➔t➔i➔o➔n➔ ➔t➔a➔s➔k➔s➔
➔P➔l➔a➔y➔ ➔A➔ ➔s➔e➔t➔ ➔o➔f➔ ➔t➔a➔s➔k➔s➔ ➔t➔a➔r➔g➔e➔t➔i➔n➔g➔ ➔a➔ ➔g➔r➔o➔u➔p➔ ➔o➔f➔ ➔h➔o➔s➔t➔s➔
➔T➔a➔s➔k➔ ➔A➔ ➔s➔i➔n➔g➔l➔e➔ ➔u➔n➔i➔t➔ ➔o➔f➔ ➔w➔o➔r➔k➔ ➔(➔i➔n➔s➔t➔a➔l➔l➔ ➔n➔g➔i➔n➔x➔,➔ ➔c➔o➔p➔y➔ ➔f➔i➔l➔e➔)➔
➔M➔o➔d➔u➔l➔e➔ ➔P➔r➔e➔-➔b➔u➔i➔l➔t➔ ➔f➔u➔n➔c➔t➔i➔o➔n➔ ➔f➔o➔r➔ ➔a➔ ➔t➔a➔s➔k➔ ➔(➔a➔p➔t➔,➔ ➔y➔u➔m➔,➔ ➔c➔o➔p➔y➔,➔ ➔s➔e➔r➔v➔i➔c➔e➔)➔
➔R➔o➔l➔e➔ ➔R➔e➔u➔s➔a➔b➔l➔e➔,➔ ➔o➔r➔g➔a➔n➔i➔z➔e➔d➔ ➔c➔o➔l➔l➔e➔c➔t➔i➔o➔n➔ ➔o➔f➔ ➔t➔a➔s➔k➔s➔
➔H➔a➔n➔d➔l➔e➔r➔ ➔T➔a➔s➔k➔ ➔t➔h➔a➔t➔ ➔r➔u➔n➔s➔ ➔o➔n➔l➔y➔ ➔w➔h➔e➔n➔ ➔n➔o➔t➔i➔f➔i➔e➔d➔ ➔(➔r➔e➔s➔t➔a➔r➔t➔ ➔s➔e➔r➔v➔i➔c➔e➔)➔
➔V➔a➔r➔i➔a➔b➔l➔e➔ ➔D➔y➔n➔a➔m➔i➔c➔ ➔v➔a➔l➔u➔e➔s➔ ➔u➔s➔e➔d➔ ➔i➔n➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔s➔
➔T➔e➔m➔p➔l➔a➔t➔e➔ ➔J➔i➔n➔j➔a➔2➔ ➔f➔i➔l➔e➔s➔ ➔w➔i➔t➔h➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔ ➔f➔o➔r➔ ➔c➔o➔n➔f➔i➔g➔ ➔f➔i➔l➔e➔s➔
➔V➔a➔u➔l➔t➔ ➔E➔n➔c➔r➔y➔p➔t➔e➔d➔ ➔s➔t➔o➔r➔a➔g➔e➔ ➔f➔o➔r➔ ➔s➔e➔c➔r➔e➔t➔s➔
➔G➔a➔l➔a➔x➔y➔ ➔C➔o➔m➔m➔u➔n➔i➔t➔y➔ ➔r➔e➔p➔o➔s➔i➔t➔o➔r➔y➔ ➔f➔o➔r➔ ➔r➔o➔l➔e➔s➔
➔4➔.➔ ➔I➔n➔s➔t➔a➔l➔l➔a➔t➔i➔o➔n➔
➔
➔
➔
➔
➔#➔ ➔I➔n➔s➔t➔a➔l➔l➔ ➔A➔n➔s➔i➔b➔l➔e➔ ➔o➔n➔ ➔C➔o➔n➔t➔r➔o➔l➔ ➔N➔o➔d➔e➔ ➔(➔U➔b➔u➔n➔t➔u➔)➔
➔s➔u➔d➔o➔ ➔a➔p➔t➔ ➔u➔p➔d➔a➔t➔e➔
➔s➔u➔d➔o➔ ➔a➔p➔t➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔a➔n➔s➔i➔b➔l➔e➔ ➔-➔y➔
➔#➔ ➔V➔e➔r➔i➔f➔y➔
➔a➔n➔s➔i➔b➔l➔e➔ ➔-➔-➔v➔e➔r➔s➔i➔o➔n➔
➔#➔ ➔I➔n➔s➔t➔a➔l➔l➔ ➔o➔n➔ ➔R➔H➔E➔L➔/➔C➔e➔n➔t➔O➔S➔
➔s➔u➔d➔o➔ ➔y➔u➔m➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔e➔p➔e➔l➔-➔r➔e➔l➔e➔a➔s➔e➔ ➔-➔y➔
➔s➔u➔d➔o➔ ➔y➔u➔m➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔a➔n➔s➔i➔b➔l➔e➔ ➔-➔y➔
➔#➔ ➔I➔n➔s➔t➔a➔l➔l➔ ➔v➔i➔a➔ ➔p➔i➔p➔
➔p➔i➔p➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔a➔n➔s➔i➔b➔l➔e➔
➔#➔ ➔K➔e➔y➔ ➔f➔i➔l➔e➔s➔
➔/➔e➔t➔c➔/➔a➔n➔s➔i➔b➔l➔e➔/➔h➔o➔s➔t➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔f➔a➔u➔l➔t➔ ➔i➔n➔v➔e➔n➔t➔o➔r➔y➔ ➔f➔i➔l➔e➔
➔/➔e➔t➔c➔/➔a➔n➔s➔i➔b➔l➔e➔/➔a➔n➔s➔i➔b➔l➔e➔.➔c➔f➔g➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔f➔a➔u➔l➔t➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔
➔5➔.➔ ➔I➔n➔v➔e➔n➔t➔o➔r➔y➔ ➔—➔ ➔D➔e➔f➔i➔n➔e➔ ➔Y➔o➔u➔r➔ ➔S➔e➔r➔v➔e➔r➔s➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔I➔n➔v➔e➔n➔t➔o➔r➔y➔?➔
➔A➔ ➔f➔i➔l➔e➔ ➔l➔i➔s➔t➔i➔n➔g➔ ➔a➔l➔l➔ ➔t➔h➔e➔ ➔s➔e➔r➔v➔e➔r➔s➔ ➔A➔n➔s➔i➔b➔l➔e➔ ➔m➔a➔n➔a➔g➔e➔s➔.➔ ➔C➔a➔n➔ ➔b➔e➔ ➔a➔ ➔s➔i➔m➔p➔l➔e➔ ➔t➔e➔x➔t➔ ➔f➔i➔l➔e➔ ➔o➔r➔ ➔d➔y➔n➔a➔m➔i➔c➔ ➔(➔f➔r➔o➔m➔ ➔A➔W➔S➔,➔ ➔A➔z➔u➔r➔e➔)➔.➔
➔S➔t➔a➔t➔i➔c➔ ➔I➔n➔v➔e➔n➔t➔o➔r➔y➔ ➔(➔h➔o➔s➔t➔s➔ ➔f➔i➔l➔e➔)➔:➔
➔#➔ ➔/➔e➔t➔c➔/➔a➔n➔s➔i➔b➔l➔e➔/➔h➔o➔s➔t➔s➔ ➔ ➔O➔R➔ ➔ ➔i➔n➔v➔e➔n➔t➔o➔r➔y➔.➔i➔n➔i➔
➔#➔ ➔S➔i➔m➔p➔l➔e➔ ➔l➔i➔s➔t➔
➔1➔9➔2➔.➔1➔6➔8➔.➔1➔.➔1➔0➔
➔1➔9➔2➔.➔1➔6➔8➔.➔1➔.➔1➔1➔
➔s➔e➔r➔v➔e➔r➔1➔.➔e➔x➔a➔m➔p➔l➔e➔.➔c➔o➔m➔
➔#➔ ➔G➔r➔o➔u➔p➔s➔
➔[➔w➔e➔b➔s➔e➔r➔v➔e➔r➔s➔]➔
➔w➔e➔b➔1➔.➔e➔x➔a➔m➔p➔l➔e➔.➔c➔o➔m➔
➔w➔e➔b➔2➔.➔e➔x➔a➔m➔p➔l➔e➔.➔c➔o➔m➔
➔1➔9➔2➔.➔1➔6➔8➔.➔1➔.➔2➔0➔
➔[➔d➔b➔s➔e➔r➔v➔e➔r➔s➔]➔
➔d➔b➔1➔.➔e➔x➔a➔m➔p➔l➔e➔.➔c➔o➔m➔
➔d➔b➔2➔.➔e➔x➔a➔m➔p➔l➔e➔.➔c➔o➔m➔
➔[➔a➔p➔p➔s➔e➔r➔v➔e➔r➔s➔]➔
➔
➔
➔
➔
➔a➔p➔p➔1➔.➔e➔x➔a➔m➔p➔l➔e➔.➔c➔o➔m➔ ➔a➔n➔s➔i➔b➔l➔e➔_➔u➔s➔e➔r➔=➔u➔b➔u➔n➔t➔u➔ ➔a➔n➔s➔i➔b➔l➔e➔_➔p➔o➔r➔t➔=➔2➔2➔
➔#➔ ➔G➔r➔o➔u➔p➔ ➔o➔f➔ ➔g➔r➔o➔u➔p➔s➔
➔[➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔:➔c➔h➔i➔l➔d➔r➔e➔n➔]➔
➔w➔e➔b➔s➔e➔r➔v➔e➔r➔s➔
➔d➔b➔s➔e➔r➔v➔e➔r➔s➔
➔#➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔s➔ ➔f➔o➔r➔ ➔g➔r➔o➔u➔p➔
➔[➔w➔e➔b➔s➔e➔r➔v➔e➔r➔s➔:➔v➔a➔r➔s➔]➔
➔a➔n➔s➔i➔b➔l➔e➔_➔u➔s➔e➔r➔=➔u➔b➔u➔n➔t➔u➔
➔a➔n➔s➔i➔b➔l➔e➔_➔s➔s➔h➔_➔p➔r➔i➔v➔a➔t➔e➔_➔k➔e➔y➔_➔f➔i➔l➔e➔=➔~➔/➔.➔s➔s➔h➔/➔i➔d➔_➔r➔s➔a➔
➔h➔t➔t➔p➔_➔p➔o➔r➔t➔=➔8➔0➔
➔Y➔A➔M➔L➔ ➔I➔n➔v➔e➔n➔t➔o➔r➔y➔:➔
➔#➔ ➔i➔n➔v➔e➔n➔t➔o➔r➔y➔.➔y➔m➔l➔
➔a➔l➔l➔:➔
➔ ➔ ➔c➔h➔i➔l➔d➔r➔e➔n➔:➔
➔ ➔ ➔ ➔ ➔w➔e➔b➔s➔e➔r➔v➔e➔r➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔h➔o➔s➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔w➔e➔b➔1➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔a➔n➔s➔i➔b➔l➔e➔_➔h➔o➔s➔t➔:➔ ➔1➔9➔2➔.➔1➔6➔8➔.➔1➔.➔1➔0➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔a➔n➔s➔i➔b➔l➔e➔_➔u➔s➔e➔r➔:➔ ➔u➔b➔u➔n➔t➔u➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔w➔e➔b➔2➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔a➔n➔s➔i➔b➔l➔e➔_➔h➔o➔s➔t➔:➔ ➔1➔9➔2➔.➔1➔6➔8➔.➔1➔.➔1➔1➔
➔ ➔ ➔ ➔ ➔d➔b➔s➔e➔r➔v➔e➔r➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔h➔o➔s➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔b➔1➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔a➔n➔s➔i➔b➔l➔e➔_➔h➔o➔s➔t➔:➔ ➔1➔9➔2➔.➔1➔6➔8➔.➔1➔.➔2➔0➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔a➔n➔s➔i➔b➔l➔e➔_➔u➔s➔e➔r➔:➔ ➔u➔b➔u➔n➔t➔u➔
➔I➔n➔v➔e➔n➔t➔o➔r➔y➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔:➔
➔a➔n➔s➔i➔b➔l➔e➔-➔i➔n➔v➔e➔n➔t➔o➔r➔y➔ ➔-➔-➔l➔i➔s➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔a➔l➔l➔ ➔h➔o➔s➔t➔s➔
➔a➔n➔s➔i➔b➔l➔e➔-➔i➔n➔v➔e➔n➔t➔o➔r➔y➔ ➔-➔-➔g➔r➔a➔p➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔t➔r➔e➔e➔ ➔v➔i➔e➔w➔
➔a➔n➔s➔i➔b➔l➔e➔ ➔a➔l➔l➔ ➔-➔-➔l➔i➔s➔t➔-➔h➔o➔s➔t➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔h➔o➔s➔t➔s➔
➔a➔n➔s➔i➔b➔l➔e➔ ➔w➔e➔b➔s➔e➔r➔v➔e➔r➔s➔ ➔-➔-➔l➔i➔s➔t➔-➔h➔o➔s➔t➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔h➔o➔s➔t➔s➔ ➔i➔n➔ ➔g➔r➔o➔u➔p➔
➔6➔.➔ ➔A➔d➔-➔H➔o➔c➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔
➔W➔h➔a➔t➔ ➔a➔r➔e➔ ➔A➔d➔-➔H➔o➔c➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔?➔
➔
➔
➔
➔
➔Q➔u➔i➔c➔k➔ ➔o➔n➔e➔-➔l➔i➔n➔e➔r➔ ➔c➔o➔m➔m➔a➔n➔d➔s➔ ➔t➔o➔ ➔r➔u➔n➔ ➔a➔ ➔t➔a➔s➔k➔ ➔o➔n➔ ➔s➔e➔r➔v➔e➔r➔s➔ ➔w➔i➔t➔h➔o➔u➔t➔ ➔w➔r➔i➔t➔i➔n➔g➔ ➔a➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔.➔
➔#➔ ➔S➔y➔n➔t➔a➔x➔
➔a➔n➔s➔i➔b➔l➔e➔ ➔<➔h➔o➔s➔t➔s➔/➔g➔r➔o➔u➔p➔>➔ ➔-➔m➔ ➔<➔m➔o➔d➔u➔l➔e➔>➔ ➔-➔a➔ ➔"➔<➔a➔r➔g➔u➔m➔e➔n➔t➔s➔>➔"➔
➔#➔ ➔T➔e➔s➔t➔ ➔c➔o➔n➔n➔e➔c➔t➔i➔v➔i➔t➔y➔ ➔(➔p➔i➔n➔g➔ ➔a➔l➔l➔ ➔s➔e➔r➔v➔e➔r➔s➔)➔
➔a➔n➔s➔i➔b➔l➔e➔ ➔a➔l➔l➔ ➔-➔m➔ ➔p➔i➔n➔g➔
➔a➔n➔s➔i➔b➔l➔e➔ ➔w➔e➔b➔s➔e➔r➔v➔e➔r➔s➔ ➔-➔m➔ ➔p➔i➔n➔g➔
➔#➔ ➔R➔u➔n➔ ➔s➔h➔e➔l➔l➔ ➔c➔o➔m➔m➔a➔n➔d➔
➔a➔n➔s➔i➔b➔l➔e➔ ➔a➔l➔l➔ ➔-➔m➔ ➔s➔h➔e➔l➔l➔ ➔-➔a➔ ➔"➔u➔p➔t➔i➔m➔e➔"➔
➔a➔n➔s➔i➔b➔l➔e➔ ➔w➔e➔b➔s➔e➔r➔v➔e➔r➔s➔ ➔-➔m➔ ➔s➔h➔e➔l➔l➔ ➔-➔a➔ ➔"➔d➔f➔ ➔-➔h➔"➔
➔a➔n➔s➔i➔b➔l➔e➔ ➔d➔b➔s➔e➔r➔v➔e➔r➔s➔ ➔-➔m➔ ➔s➔h➔e➔l➔l➔ ➔-➔a➔ ➔"➔f➔r➔e➔e➔ ➔-➔h➔"➔
➔#➔ ➔I➔n➔s➔t➔a➔l➔l➔ ➔p➔a➔c➔k➔a➔g➔e➔
➔a➔n➔s➔i➔b➔l➔e➔ ➔w➔e➔b➔s➔e➔r➔v➔e➔r➔s➔ ➔-➔m➔ ➔a➔p➔t➔ ➔-➔a➔ ➔"➔n➔a➔m➔e➔=➔n➔g➔i➔n➔x➔ ➔s➔t➔a➔t➔e➔=➔p➔r➔e➔s➔e➔n➔t➔"➔ ➔-➔-➔b➔e➔c➔o➔m➔e➔
➔a➔n➔s➔i➔b➔l➔e➔ ➔w➔e➔b➔s➔e➔r➔v➔e➔r➔s➔ ➔-➔m➔ ➔y➔u➔m➔ ➔-➔a➔ ➔"➔n➔a➔m➔e➔=➔n➔g➔i➔n➔x➔ ➔s➔t➔a➔t➔e➔=➔p➔r➔e➔s➔e➔n➔t➔"➔ ➔-➔-➔b➔e➔c➔o➔m➔e➔
➔#➔ ➔C➔o➔p➔y➔ ➔f➔i➔l➔e➔
➔a➔n➔s➔i➔b➔l➔e➔ ➔w➔e➔b➔s➔e➔r➔v➔e➔r➔s➔ ➔-➔m➔ ➔c➔o➔p➔y➔ ➔-➔a➔ ➔"➔s➔r➔c➔=➔/➔l➔o➔c➔a➔l➔/➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔d➔e➔s➔t➔=➔/➔r➔e➔m➔o➔t➔e➔/➔f➔i➔l➔e➔.➔t➔x➔t➔"➔
➔#➔ ➔C➔r➔e➔a➔t➔e➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔a➔n➔s➔i➔b➔l➔e➔ ➔a➔l➔l➔ ➔-➔m➔ ➔f➔i➔l➔e➔ ➔-➔a➔ ➔"➔p➔a➔t➔h➔=➔/➔o➔p➔t➔/➔m➔y➔a➔p➔p➔ ➔s➔t➔a➔t➔e➔=➔d➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔m➔o➔d➔e➔=➔0➔7➔5➔5➔"➔
➔#➔ ➔R➔e➔s➔t➔a➔r➔t➔ ➔s➔e➔r➔v➔i➔c➔e➔
➔a➔n➔s➔i➔b➔l➔e➔ ➔w➔e➔b➔s➔e➔r➔v➔e➔r➔s➔ ➔-➔m➔ ➔s➔e➔r➔v➔i➔c➔e➔ ➔-➔a➔ ➔"➔n➔a➔m➔e➔=➔n➔g➔i➔n➔x➔ ➔s➔t➔a➔t➔e➔=➔r➔e➔s➔t➔a➔r➔t➔e➔d➔"➔ ➔-➔-➔b➔e➔c➔o➔m➔e➔
➔#➔ ➔G➔a➔t➔h➔e➔r➔ ➔f➔a➔c➔t➔s➔ ➔a➔b➔o➔u➔t➔ ➔s➔e➔r➔v➔e➔r➔s➔
➔a➔n➔s➔i➔b➔l➔e➔ ➔a➔l➔l➔ ➔-➔m➔ ➔s➔e➔t➔u➔p➔
➔a➔n➔s➔i➔b➔l➔e➔ ➔w➔e➔b➔1➔ ➔-➔m➔ ➔s➔e➔t➔u➔p➔ ➔-➔a➔ ➔"➔f➔i➔l➔t➔e➔r➔=➔a➔n➔s➔i➔b➔l➔e➔_➔o➔s➔_➔f➔a➔m➔i➔l➔y➔"➔
➔#➔ ➔C➔h➔e➔c➔k➔ ➔f➔r➔e➔e➔ ➔m➔e➔m➔o➔r➔y➔
➔a➔n➔s➔i➔b➔l➔e➔ ➔a➔l➔l➔ ➔-➔m➔ ➔s➔e➔t➔u➔p➔ ➔-➔a➔ ➔"➔f➔i➔l➔t➔e➔r➔=➔a➔n➔s➔i➔b➔l➔e➔_➔m➔e➔m➔f➔r➔e➔e➔_➔m➔b➔"➔
➔#➔ ➔O➔p➔t➔i➔o➔n➔s➔
➔-➔i➔ ➔i➔n➔v➔e➔n➔t➔o➔r➔y➔.➔i➔n➔i➔ ➔ ➔ ➔ ➔#➔ ➔s➔p➔e➔c➔i➔f➔y➔ ➔i➔n➔v➔e➔n➔t➔o➔r➔y➔ ➔f➔i➔l➔e➔
➔-➔-➔b➔e➔c➔o➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔u➔d➔o➔ ➔(➔r➔u➔n➔ ➔a➔s➔ ➔r➔o➔o➔t➔)➔
➔-➔u➔ ➔u➔b➔u➔n➔t➔u➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔p➔e➔c➔i➔f➔y➔ ➔u➔s➔e➔r➔n➔a➔m➔e➔
➔-➔k➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔s➔k➔ ➔f➔o➔r➔ ➔p➔a➔s➔s➔w➔o➔r➔d➔
➔-➔-➔p➔r➔i➔v➔a➔t➔e➔-➔k➔e➔y➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔S➔S➔H➔ ➔k➔e➔y➔ ➔f➔i➔l➔e➔
➔-➔v➔ ➔/➔ ➔-➔v➔v➔ ➔/➔ ➔-➔v➔v➔v➔ ➔ ➔ ➔ ➔#➔ ➔v➔e➔r➔b➔o➔s➔e➔ ➔o➔u➔t➔p➔u➔t➔
➔7➔.➔ ➔P➔l➔a➔y➔b➔o➔o➔k➔s➔ ➔—➔ ➔T➔h➔e➔ ➔H➔e➔a➔r➔t➔ ➔o➔f➔ ➔A➔n➔s➔i➔b➔l➔e➔
➔
➔
➔
➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔ ➔P➔l➔a➔y➔b➔o➔o➔k➔?➔
➔A➔ ➔Y➔A➔M➔L➔ ➔f➔i➔l➔e➔ ➔c➔o➔n➔t➔a➔i➔n➔i➔n➔g➔ ➔o➔n➔e➔ ➔o➔r➔ ➔m➔o➔r➔e➔ ➔p➔l➔a➔y➔s➔.➔ ➔E➔a➔c➔h➔ ➔p➔l➔a➔y➔ ➔t➔a➔r➔g➔e➔t➔s➔ ➔a➔ ➔g➔r➔o➔u➔p➔ ➔o➔f➔ ➔h➔o➔s➔t➔s➔ ➔a➔n➔d➔ ➔r➔u➔n➔s➔ ➔a➔ ➔s➔e➔r➔i➔e➔s➔ ➔o➔f➔ ➔t➔a➔s➔k➔s➔.➔
➔B➔a➔s➔i➔c➔ ➔P➔l➔a➔y➔b➔o➔o➔k➔ ➔S➔t➔r➔u➔c➔t➔u➔r➔e➔
➔-➔-➔-➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔M➔y➔ ➔F➔i➔r➔s➔t➔ ➔P➔l➔a➔y➔b➔o➔o➔k➔
➔ ➔ ➔h➔o➔s➔t➔s➔:➔ ➔w➔e➔b➔s➔e➔r➔v➔e➔r➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔t➔a➔r➔g➔e➔t➔ ➔g➔r➔o➔u➔p➔ ➔f➔r➔o➔m➔ ➔i➔n➔v➔e➔n➔t➔o➔r➔y➔
➔ ➔ ➔b➔e➔c➔o➔m➔e➔:➔ ➔y➔e➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔u➔d➔o➔
➔ ➔ ➔v➔a➔r➔s➔:➔
➔ ➔ ➔ ➔ ➔h➔t➔t➔p➔_➔p➔o➔r➔t➔:➔ ➔8➔0➔
➔ ➔ ➔ ➔ ➔a➔p➔p➔_➔n➔a➔m➔e➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔t➔a➔s➔k➔s➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔I➔n➔s➔t➔a➔l➔l➔ ➔n➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔t➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔n➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔p➔r➔e➔s➔e➔n➔t➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔u➔p➔d➔a➔t➔e➔_➔c➔a➔c➔h➔e➔:➔ ➔y➔e➔s➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔S➔t➔a➔r➔t➔ ➔n➔g➔i➔n➔x➔ ➔s➔e➔r➔v➔i➔c➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔s➔e➔r➔v➔i➔c➔e➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔n➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔s➔t➔a➔r➔t➔e➔d➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔e➔n➔a➔b➔l➔e➔d➔:➔ ➔y➔e➔s➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔C➔r➔e➔a➔t➔e➔ ➔w➔e➔b➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔ ➔ ➔ ➔ ➔ ➔ ➔f➔i➔l➔e➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔a➔t➔h➔:➔ ➔/➔v➔a➔r➔/➔w➔w➔w➔/➔{➔{➔ ➔a➔p➔p➔_➔n➔a➔m➔e➔ ➔}➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔m➔o➔d➔e➔:➔ ➔'➔0➔7➔5➔5➔'➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔C➔o➔p➔y➔ ➔i➔n➔d➔e➔x➔.➔h➔t➔m➔l➔
➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔p➔y➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔r➔c➔:➔ ➔f➔i➔l➔e➔s➔/➔i➔n➔d➔e➔x➔.➔h➔t➔m➔l➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔e➔s➔t➔:➔ ➔/➔v➔a➔r➔/➔w➔w➔w➔/➔{➔{➔ ➔a➔p➔p➔_➔n➔a➔m➔e➔ ➔}➔}➔/➔i➔n➔d➔e➔x➔.➔h➔t➔m➔l➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔m➔o➔d➔e➔:➔ ➔'➔0➔6➔4➔4➔'➔
➔R➔u➔n➔ ➔P➔l➔a➔y➔b➔o➔o➔k➔:➔
➔a➔n➔s➔i➔b➔l➔e➔-➔p➔l➔a➔y➔b➔o➔o➔k➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔.➔y➔m➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔u➔n➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔
➔a➔n➔s➔i➔b➔l➔e➔-➔p➔l➔a➔y➔b➔o➔o➔k➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔.➔y➔m➔l➔ ➔-➔i➔ ➔i➔n➔v➔e➔n➔t➔o➔r➔y➔.➔i➔n➔i➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔u➔s➔t➔o➔m➔ ➔i➔n➔v➔e➔n➔t➔o➔r➔y➔
➔a➔n➔s➔i➔b➔l➔e➔-➔p➔l➔a➔y➔b➔o➔o➔k➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔.➔y➔m➔l➔ ➔-➔-➔c➔h➔e➔c➔k➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔r➔y➔ ➔r➔u➔n➔ ➔(➔n➔o➔ ➔c➔h➔a➔n➔g➔e➔s➔)➔
➔a➔n➔s➔i➔b➔l➔e➔-➔p➔l➔a➔y➔b➔o➔o➔k➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔.➔y➔m➔l➔ ➔-➔-➔d➔i➔f➔f➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔w➔h➔a➔t➔ ➔c➔h➔a➔n➔g➔e➔d➔
➔a➔n➔s➔i➔b➔l➔e➔-➔p➔l➔a➔y➔b➔o➔o➔k➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔.➔y➔m➔l➔ ➔-➔v➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔v➔e➔r➔b➔o➔s➔e➔
➔a➔n➔s➔i➔b➔l➔e➔-➔p➔l➔a➔y➔b➔o➔o➔k➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔.➔y➔m➔l➔ ➔-➔-➔t➔a➔g➔s➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔u➔n➔ ➔o➔n➔l➔y➔ ➔t➔a➔g➔g➔e➔d➔ ➔t➔a➔s➔k➔s➔
➔
➔
➔
➔
➔a➔n➔s➔i➔b➔l➔e➔-➔p➔l➔a➔y➔b➔o➔o➔k➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔.➔y➔m➔l➔ ➔-➔-➔s➔k➔i➔p➔-➔t➔a➔g➔s➔ ➔r➔e➔s➔t➔a➔r➔t➔ ➔ ➔ ➔ ➔#➔ ➔s➔k➔i➔p➔ ➔t➔a➔g➔g➔e➔d➔ ➔t➔a➔s➔k➔s➔
➔a➔n➔s➔i➔b➔l➔e➔-➔p➔l➔a➔y➔b➔o➔o➔k➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔.➔y➔m➔l➔ ➔-➔-➔l➔i➔m➔i➔t➔ ➔w➔e➔b➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔u➔n➔ ➔o➔n➔l➔y➔ ➔o➔n➔ ➔w➔e➔b➔1➔
➔8➔.➔ ➔C➔o➔m➔m➔o➔n➔ ➔A➔n➔s➔i➔b➔l➔e➔ ➔M➔o➔d➔u➔l➔e➔s➔
➔#➔ ➔─➔─➔ ➔P➔A➔C➔K➔A➔G➔E➔ ➔M➔A➔N➔A➔G➔E➔M➔E➔N➔T➔ ➔─➔─➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔I➔n➔s➔t➔a➔l➔l➔ ➔p➔a➔c➔k➔a➔g➔e➔ ➔(➔U➔b➔u➔n➔t➔u➔/➔D➔e➔b➔i➔a➔n➔)➔
➔ ➔ ➔a➔p➔t➔:➔
➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔n➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔p➔r➔e➔s➔e➔n➔t➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔r➔e➔s➔e➔n➔t➔/➔a➔b➔s➔e➔n➔t➔/➔l➔a➔t➔e➔s➔t➔
➔ ➔ ➔ ➔ ➔u➔p➔d➔a➔t➔e➔_➔c➔a➔c➔h➔e➔:➔ ➔y➔e➔s➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔I➔n➔s➔t➔a➔l➔l➔ ➔p➔a➔c➔k➔a➔g➔e➔ ➔(➔R➔H➔E➔L➔/➔C➔e➔n➔t➔O➔S➔)➔
➔ ➔ ➔y➔u➔m➔:➔
➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔n➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔p➔r➔e➔s➔e➔n➔t➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔I➔n➔s➔t➔a➔l➔l➔ ➔p➔i➔p➔ ➔p➔a➔c➔k➔a➔g➔e➔
➔ ➔ ➔p➔i➔p➔:➔
➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔f➔l➔a➔s➔k➔
➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔p➔r➔e➔s➔e➔n➔t➔
➔#➔ ➔─➔─➔ ➔F➔I➔L➔E➔ ➔O➔P➔E➔R➔A➔T➔I➔O➔N➔S➔ ➔─➔─➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔C➔r➔e➔a➔t➔e➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔ ➔ ➔f➔i➔l➔e➔:➔
➔ ➔ ➔ ➔ ➔p➔a➔t➔h➔:➔ ➔/➔o➔p➔t➔/➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔ ➔ ➔ ➔ ➔m➔o➔d➔e➔:➔ ➔'➔0➔7➔5➔5➔'➔
➔ ➔ ➔ ➔ ➔o➔w➔n➔e➔r➔:➔ ➔u➔b➔u➔n➔t➔u➔
➔ ➔ ➔ ➔ ➔g➔r➔o➔u➔p➔:➔ ➔u➔b➔u➔n➔t➔u➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔C➔r➔e➔a➔t➔e➔ ➔f➔i➔l➔e➔
➔ ➔ ➔f➔i➔l➔e➔:➔
➔ ➔ ➔ ➔ ➔p➔a➔t➔h➔:➔ ➔/➔o➔p➔t➔/➔m➔y➔a➔p➔p➔/➔a➔p➔p➔.➔p➔y➔
➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔t➔o➔u➔c➔h➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔D➔e➔l➔e➔t➔e➔ ➔f➔i➔l➔e➔
➔ ➔ ➔f➔i➔l➔e➔:➔
➔ ➔ ➔ ➔ ➔p➔a➔t➔h➔:➔ ➔/➔t➔m➔p➔/➔o➔l➔d➔f➔i➔l➔e➔.➔t➔x➔t➔
➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔a➔b➔s➔e➔n➔t➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔C➔o➔p➔y➔ ➔f➔i➔l➔e➔ ➔f➔r➔o➔m➔ ➔c➔o➔n➔t➔r➔o➔l➔ ➔t➔o➔ ➔m➔a➔n➔a➔g➔e➔d➔
➔ ➔ ➔c➔o➔p➔y➔:➔
➔ ➔ ➔ ➔ ➔s➔r➔c➔:➔ ➔f➔i➔l➔e➔s➔/➔n➔g➔i➔n➔x➔.➔c➔o➔n➔f➔
➔
➔
➔
➔
➔ ➔ ➔ ➔ ➔d➔e➔s➔t➔:➔ ➔/➔e➔t➔c➔/➔n➔g➔i➔n➔x➔/➔n➔g➔i➔n➔x➔.➔c➔o➔n➔f➔
➔ ➔ ➔ ➔ ➔m➔o➔d➔e➔:➔ ➔'➔0➔6➔4➔4➔'➔
➔ ➔ ➔ ➔ ➔b➔a➔c➔k➔u➔p➔:➔ ➔y➔e➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔b➔a➔c➔k➔u➔p➔ ➔e➔x➔i➔s➔t➔i➔n➔g➔ ➔f➔i➔l➔e➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔C➔o➔p➔y➔ ➔i➔n➔l➔i➔n➔e➔ ➔c➔o➔n➔t➔e➔n➔t➔ ➔t➔o➔ ➔f➔i➔l➔e➔
➔ ➔ ➔c➔o➔p➔y➔:➔
➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔e➔n➔t➔:➔ ➔"➔H➔e➔l➔l➔o➔ ➔W➔o➔r➔l➔d➔"➔
➔ ➔ ➔ ➔ ➔d➔e➔s➔t➔:➔ ➔/➔v➔a➔r➔/➔w➔w➔w➔/➔h➔t➔m➔l➔/➔i➔n➔d➔e➔x➔.➔h➔t➔m➔l➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔D➔o➔w➔n➔l➔o➔a➔d➔ ➔f➔i➔l➔e➔ ➔f➔r➔o➔m➔ ➔U➔R➔L➔
➔ ➔ ➔g➔e➔t➔_➔u➔r➔l➔:➔
➔ ➔ ➔ ➔ ➔u➔r➔l➔:➔ ➔h➔t➔t➔p➔s➔:➔/➔/➔e➔x➔a➔m➔p➔l➔e➔.➔c➔o➔m➔/➔f➔i➔l➔e➔.➔z➔i➔p➔
➔ ➔ ➔ ➔ ➔d➔e➔s➔t➔:➔ ➔/➔o➔p➔t➔/➔f➔i➔l➔e➔.➔z➔i➔p➔
➔#➔ ➔─➔─➔ ➔S➔E➔R➔V➔I➔C➔E➔ ➔M➔A➔N➔A➔G➔E➔M➔E➔N➔T➔ ➔─➔─➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔S➔t➔a➔r➔t➔ ➔a➔n➔d➔ ➔e➔n➔a➔b➔l➔e➔ ➔s➔e➔r➔v➔i➔c➔e➔
➔ ➔ ➔s➔e➔r➔v➔i➔c➔e➔:➔
➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔n➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔s➔t➔a➔r➔t➔e➔d➔
➔ ➔ ➔ ➔ ➔e➔n➔a➔b➔l➔e➔d➔:➔ ➔y➔e➔s➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔R➔e➔s➔t➔a➔r➔t➔ ➔s➔e➔r➔v➔i➔c➔e➔
➔ ➔ ➔s➔e➔r➔v➔i➔c➔e➔:➔
➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔n➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔r➔e➔s➔t➔a➔r➔t➔e➔d➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔S➔t➔o➔p➔ ➔s➔e➔r➔v➔i➔c➔e➔
➔ ➔ ➔s➔e➔r➔v➔i➔c➔e➔:➔
➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔n➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔s➔t➔o➔p➔p➔e➔d➔
➔#➔ ➔─➔─➔ ➔C➔O➔M➔M➔A➔N➔D➔ ➔E➔X➔E➔C➔U➔T➔I➔O➔N➔ ➔─➔─➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔R➔u➔n➔ ➔s➔h➔e➔l➔l➔ ➔c➔o➔m➔m➔a➔n➔d➔
➔ ➔ ➔s➔h➔e➔l➔l➔:➔ ➔e➔c➔h➔o➔ ➔"➔H➔e➔l➔l➔o➔"➔ ➔>➔ ➔/➔t➔m➔p➔/➔h➔e➔l➔l➔o➔.➔t➔x➔t➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔R➔u➔n➔ ➔c➔o➔m➔m➔a➔n➔d➔ ➔(➔s➔a➔f➔e➔r➔,➔ ➔n➔o➔ ➔s➔h➔e➔l➔l➔ ➔f➔e➔a➔t➔u➔r➔e➔s➔)➔
➔ ➔ ➔c➔o➔m➔m➔a➔n➔d➔:➔ ➔l➔s➔ ➔-➔l➔a➔ ➔/➔o➔p➔t➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔R➔u➔n➔ ➔s➔c➔r➔i➔p➔t➔
➔ ➔ ➔s➔c➔r➔i➔p➔t➔:➔ ➔s➔c➔r➔i➔p➔t➔s➔/➔s➔e➔t➔u➔p➔.➔s➔h➔
➔#➔ ➔─➔─➔ ➔U➔S➔E➔R➔ ➔M➔A➔N➔A➔G➔E➔M➔E➔N➔T➔ ➔─➔─➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔C➔r➔e➔a➔t➔e➔ ➔u➔s➔e➔r➔
➔ ➔ ➔u➔s➔e➔r➔:➔
➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔d➔e➔p➔l➔o➔y➔
➔ ➔ ➔ ➔ ➔s➔h➔e➔l➔l➔:➔ ➔/➔b➔i➔n➔/➔b➔a➔s➔h➔
➔ ➔ ➔ ➔ ➔h➔o➔m➔e➔:➔ ➔/➔h➔o➔m➔e➔/➔d➔e➔p➔l➔o➔y➔
➔ ➔ ➔ ➔ ➔c➔r➔e➔a➔t➔e➔_➔h➔o➔m➔e➔:➔ ➔y➔e➔s➔
➔ ➔ ➔ ➔ ➔g➔r➔o➔u➔p➔s➔:➔ ➔s➔u➔d➔o➔
➔
➔
➔
➔
➔ ➔ ➔ ➔ ➔a➔p➔p➔e➔n➔d➔:➔ ➔y➔e➔s➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔D➔e➔l➔e➔t➔e➔ ➔u➔s➔e➔r➔
➔ ➔ ➔u➔s➔e➔r➔:➔
➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔o➔l➔d➔u➔s➔e➔r➔
➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔a➔b➔s➔e➔n➔t➔
➔ ➔ ➔ ➔ ➔r➔e➔m➔o➔v➔e➔:➔ ➔y➔e➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔s➔ ➔h➔o➔m➔e➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔#➔ ➔─➔─➔ ➔G➔I➔T➔ ➔─➔─➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔C➔l➔o➔n➔e➔ ➔g➔i➔t➔ ➔r➔e➔p➔o➔s➔i➔t➔o➔r➔y➔
➔ ➔ ➔g➔i➔t➔:➔
➔ ➔ ➔ ➔ ➔r➔e➔p➔o➔:➔ ➔h➔t➔t➔p➔s➔:➔/➔/➔g➔i➔t➔h➔u➔b➔.➔c➔o➔m➔/➔a➔k➔h➔i➔l➔/➔m➔y➔a➔p➔p➔.➔g➔i➔t➔
➔ ➔ ➔ ➔ ➔d➔e➔s➔t➔:➔ ➔/➔o➔p➔t➔/➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔v➔e➔r➔s➔i➔o➔n➔:➔ ➔m➔a➔i➔n➔
➔#➔ ➔─➔─➔ ➔T➔E➔M➔P➔L➔A➔T➔E➔ ➔─➔─➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔D➔e➔p➔l➔o➔y➔ ➔c➔o➔n➔f➔i➔g➔ ➔f➔r➔o➔m➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔
➔ ➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔:➔
➔ ➔ ➔ ➔ ➔s➔r➔c➔:➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔s➔/➔n➔g➔i➔n➔x➔.➔c➔o➔n➔f➔.➔j➔2➔
➔ ➔ ➔ ➔ ➔d➔e➔s➔t➔:➔ ➔/➔e➔t➔c➔/➔n➔g➔i➔n➔x➔/➔n➔g➔i➔n➔x➔.➔c➔o➔n➔f➔
➔ ➔ ➔ ➔ ➔m➔o➔d➔e➔:➔ ➔'➔0➔6➔4➔4➔'➔
➔#➔ ➔─➔─➔ ➔D➔O➔C➔K➔E➔R➔ ➔─➔─➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔P➔u➔l➔l➔ ➔D➔o➔c➔k➔e➔r➔ ➔i➔m➔a➔g➔e➔
➔ ➔ ➔d➔o➔c➔k➔e➔r➔_➔i➔m➔a➔g➔e➔:➔
➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔n➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔t➔a➔g➔:➔ ➔l➔a➔t➔e➔s➔t➔
➔ ➔ ➔ ➔ ➔s➔o➔u➔r➔c➔e➔:➔ ➔p➔u➔l➔l➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔R➔u➔n➔ ➔D➔o➔c➔k➔e➔r➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔ ➔ ➔d➔o➔c➔k➔e➔r➔_➔c➔o➔n➔t➔a➔i➔n➔e➔r➔:➔
➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔n➔g➔i➔n➔x➔:➔l➔a➔t➔e➔s➔t➔
➔ ➔ ➔ ➔ ➔p➔o➔r➔t➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔"➔8➔0➔:➔8➔0➔"➔
➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔s➔t➔a➔r➔t➔e➔d➔
➔#➔ ➔─➔─➔ ➔D➔E➔B➔U➔G➔ ➔─➔─➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔P➔r➔i➔n➔t➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔
➔ ➔ ➔d➔e➔b➔u➔g➔:➔
➔ ➔ ➔ ➔ ➔m➔s➔g➔:➔ ➔"➔T➔h➔e➔ ➔v➔a➔l➔u➔e➔ ➔i➔s➔ ➔{➔{➔ ➔m➔y➔_➔v➔a➔r➔i➔a➔b➔l➔e➔ ➔}➔}➔"➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔P➔r➔i➔n➔t➔ ➔a➔l➔l➔ ➔f➔a➔c➔t➔s➔
➔ ➔ ➔d➔e➔b➔u➔g➔:➔
➔ ➔ ➔ ➔ ➔v➔a➔r➔:➔ ➔a➔n➔s➔i➔b➔l➔e➔_➔f➔a➔c➔t➔s➔
➔
➔
➔
➔
➔9➔.➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔s➔ ➔i➔n➔ ➔A➔n➔s➔i➔b➔l➔e➔
➔#➔ ➔─➔─➔ ➔I➔N➔L➔I➔N➔E➔ ➔V➔A➔R➔I➔A➔B➔L➔E➔S➔ ➔─➔─➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔D➔e➔p➔l➔o➔y➔ ➔A➔p➔p➔
➔ ➔ ➔h➔o➔s➔t➔s➔:➔ ➔w➔e➔b➔s➔e➔r➔v➔e➔r➔s➔
➔ ➔ ➔v➔a➔r➔s➔:➔
➔ ➔ ➔ ➔ ➔a➔p➔p➔_➔n➔a➔m➔e➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔a➔p➔p➔_➔p➔o➔r➔t➔:➔ ➔3➔0➔0➔0➔
➔ ➔ ➔ ➔ ➔a➔p➔p➔_➔v➔e➔r➔s➔i➔o➔n➔:➔ ➔"➔1➔.➔0➔"➔
➔ ➔ ➔t➔a➔s➔k➔s➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔P➔r➔i➔n➔t➔ ➔a➔p➔p➔ ➔i➔n➔f➔o➔
➔ ➔ ➔ ➔ ➔ ➔ ➔d➔e➔b➔u➔g➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔m➔s➔g➔:➔ ➔"➔D➔e➔p➔l➔o➔y➔i➔n➔g➔ ➔{➔{➔ ➔a➔p➔p➔_➔n➔a➔m➔e➔ ➔}➔}➔ ➔v➔{➔{➔ ➔a➔p➔p➔_➔v➔e➔r➔s➔i➔o➔n➔ ➔}➔}➔ ➔o➔n➔ ➔p➔o➔r➔t➔ ➔{➔{➔ ➔a➔p➔p➔_➔p➔o➔r➔t➔ ➔}➔}➔"➔
➔#➔ ➔─➔─➔ ➔V➔A➔R➔I➔A➔B➔L➔E➔ ➔F➔I➔L➔E➔S➔ ➔─➔─➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔D➔e➔p➔l➔o➔y➔ ➔A➔p➔p➔
➔ ➔ ➔h➔o➔s➔t➔s➔:➔ ➔w➔e➔b➔s➔e➔r➔v➔e➔r➔s➔
➔ ➔ ➔v➔a➔r➔s➔_➔f➔i➔l➔e➔s➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔v➔a➔r➔s➔/➔m➔a➔i➔n➔.➔y➔m➔l➔
➔ ➔ ➔ ➔ ➔-➔ ➔v➔a➔r➔s➔/➔s➔e➔c➔r➔e➔t➔s➔.➔y➔m➔l➔
➔#➔ ➔v➔a➔r➔s➔/➔m➔a➔i➔n➔.➔y➔m➔l➔
➔a➔p➔p➔_➔n➔a➔m➔e➔:➔ ➔m➔y➔a➔p➔p➔
➔a➔p➔p➔_➔p➔o➔r➔t➔:➔ ➔3➔0➔0➔0➔
➔d➔b➔_➔h➔o➔s➔t➔:➔ ➔p➔o➔s➔t➔g➔r➔e➔s➔-➔s➔e➔r➔v➔e➔r➔
➔d➔b➔_➔p➔o➔r➔t➔:➔ ➔5➔4➔3➔2➔
➔#➔ ➔v➔a➔r➔s➔/➔s➔e➔c➔r➔e➔t➔s➔.➔y➔m➔l➔ ➔(➔u➔s➔e➔ ➔A➔n➔s➔i➔b➔l➔e➔ ➔V➔a➔u➔l➔t➔ ➔t➔o➔ ➔e➔n➔c➔r➔y➔p➔t➔ ➔t➔h➔i➔s➔)➔
➔d➔b➔_➔p➔a➔s➔s➔w➔o➔r➔d➔:➔ ➔s➔u➔p➔e➔r➔s➔e➔c➔r➔e➔t➔
➔a➔p➔i➔_➔k➔e➔y➔:➔ ➔a➔b➔c➔1➔2➔3➔x➔y➔z➔
➔V➔a➔r➔i➔a➔b➔l➔e➔ ➔P➔r➔e➔c➔e➔d➔e➔n➔c➔e➔ ➔(➔h➔i➔g➔h➔e➔s➔t➔ ➔t➔o➔ ➔l➔o➔w➔e➔s➔t➔)➔:➔
➔1➔.➔ ➔C➔o➔m➔m➔a➔n➔d➔ ➔l➔i➔n➔e➔ ➔(➔-➔e➔ ➔"➔v➔a➔r➔=➔v➔a➔l➔u➔e➔"➔)➔
➔2➔.➔ ➔T➔a➔s➔k➔ ➔v➔a➔r➔s➔
➔3➔.➔ ➔B➔l➔o➔c➔k➔ ➔v➔a➔r➔s➔
➔4➔.➔ ➔R➔o➔l➔e➔ ➔a➔n➔d➔ ➔i➔n➔c➔l➔u➔d➔e➔ ➔v➔a➔r➔s➔
➔5➔.➔ ➔P➔l➔a➔y➔ ➔v➔a➔r➔s➔_➔f➔i➔l➔e➔s➔
➔6➔.➔ ➔P➔l➔a➔y➔ ➔v➔a➔r➔s➔
➔7➔.➔ ➔H➔o➔s➔t➔ ➔f➔a➔c➔t➔s➔
➔8➔.➔ ➔I➔n➔v➔e➔n➔t➔o➔r➔y➔ ➔h➔o➔s➔t➔ ➔v➔a➔r➔s➔
➔
➔
➔
➔
➔9➔.➔ ➔I➔n➔v➔e➔n➔t➔o➔r➔y➔ ➔g➔r➔o➔u➔p➔ ➔v➔a➔r➔s➔
➔1➔0➔.➔ ➔R➔o➔l➔e➔ ➔d➔e➔f➔a➔u➔l➔t➔s➔
➔1➔0➔.➔ ➔H➔a➔n➔d➔l➔e➔r➔s➔ ➔—➔ ➔R➔u➔n➔ ➔o➔n➔ ➔N➔o➔t➔i➔f➔i➔c➔a➔t➔i➔o➔n➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔ ➔H➔a➔n➔d➔l➔e➔r➔?➔
➔A➔ ➔t➔a➔s➔k➔ ➔t➔h➔a➔t➔ ➔r➔u➔n➔s➔ ➔O➔N➔L➔Y➔ ➔w➔h➔e➔n➔ ➔n➔o➔t➔i➔f➔i➔e➔d➔ ➔b➔y➔ ➔a➔n➔o➔t➔h➔e➔r➔ ➔t➔a➔s➔k➔.➔ ➔P➔r➔e➔v➔e➔n➔t➔s➔ ➔u➔n➔n➔e➔c➔e➔s➔s➔a➔r➔y➔ ➔r➔e➔s➔t➔a➔r➔t➔s➔.➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔C➔o➔n➔f➔i➔g➔u➔r➔e➔ ➔N➔g➔i➔n➔x➔
➔ ➔ ➔h➔o➔s➔t➔s➔:➔ ➔w➔e➔b➔s➔e➔r➔v➔e➔r➔s➔
➔ ➔ ➔b➔e➔c➔o➔m➔e➔:➔ ➔y➔e➔s➔
➔ ➔ ➔t➔a➔s➔k➔s➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔C➔o➔p➔y➔ ➔n➔g➔i➔n➔x➔ ➔c➔o➔n➔f➔i➔g➔
➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔p➔y➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔r➔c➔:➔ ➔f➔i➔l➔e➔s➔/➔n➔g➔i➔n➔x➔.➔c➔o➔n➔f➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔e➔s➔t➔:➔ ➔/➔e➔t➔c➔/➔n➔g➔i➔n➔x➔/➔n➔g➔i➔n➔x➔.➔c➔o➔n➔f➔
➔ ➔ ➔ ➔ ➔ ➔ ➔n➔o➔t➔i➔f➔y➔:➔ ➔R➔e➔s➔t➔a➔r➔t➔ ➔N➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔t➔r➔i➔g➔g➔e➔r➔s➔ ➔h➔a➔n➔d➔l➔e➔r➔ ➔o➔n➔l➔y➔ ➔i➔f➔ ➔f➔i➔l➔e➔ ➔c➔h➔a➔n➔g➔e➔d➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔I➔n➔s➔t➔a➔l➔l➔ ➔n➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔t➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔n➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔p➔r➔e➔s➔e➔n➔t➔
➔ ➔ ➔ ➔ ➔ ➔ ➔n➔o➔t➔i➔f➔y➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔S➔t➔a➔r➔t➔ ➔N➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔E➔n➔a➔b➔l➔e➔ ➔N➔g➔i➔n➔x➔
➔ ➔ ➔h➔a➔n➔d➔l➔e➔r➔s➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔R➔e➔s➔t➔a➔r➔t➔ ➔N➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔ ➔ ➔s➔e➔r➔v➔i➔c➔e➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔n➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔r➔e➔s➔t➔a➔r➔t➔e➔d➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔S➔t➔a➔r➔t➔ ➔N➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔ ➔ ➔s➔e➔r➔v➔i➔c➔e➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔n➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔s➔t➔a➔r➔t➔e➔d➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔E➔n➔a➔b➔l➔e➔ ➔N➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔ ➔ ➔s➔e➔r➔v➔i➔c➔e➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔n➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔e➔n➔a➔b➔l➔e➔d➔:➔ ➔y➔e➔s➔
➔
➔
➔
➔
➔K➔e➔y➔ ➔p➔o➔i➔n➔t➔:➔ ➔H➔a➔n➔d➔l➔e➔r➔ ➔r➔u➔n➔s➔ ➔O➔N➔C➔E➔ ➔e➔v➔e➔n➔ ➔i➔f➔ ➔n➔o➔t➔i➔f➔i➔e➔d➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔t➔i➔m➔e➔s➔.➔ ➔A➔n➔d➔ ➔r➔u➔n➔s➔ ➔a➔t➔ ➔E➔N➔D➔ ➔o➔f➔ ➔p➔l➔a➔y➔.➔
➔1➔1➔.➔ ➔C➔o➔n➔d➔i➔t➔i➔o➔n➔a➔l➔s➔ ➔a➔n➔d➔ ➔L➔o➔o➔p➔s➔
➔t➔a➔s➔k➔s➔:➔
➔ ➔ ➔#➔ ➔─➔─➔ ➔C➔O➔N➔D➔I➔T➔I➔O➔N➔A➔L➔S➔ ➔(➔w➔h➔e➔n➔)➔ ➔─➔─➔
➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔I➔n➔s➔t➔a➔l➔l➔ ➔o➔n➔ ➔U➔b➔u➔n➔t➔u➔ ➔o➔n➔l➔y➔
➔ ➔ ➔ ➔ ➔a➔p➔t➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔n➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔p➔r➔e➔s➔e➔n➔t➔
➔ ➔ ➔ ➔ ➔w➔h➔e➔n➔:➔ ➔a➔n➔s➔i➔b➔l➔e➔_➔o➔s➔_➔f➔a➔m➔i➔l➔y➔ ➔=➔=➔ ➔"➔D➔e➔b➔i➔a➔n➔"➔
➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔I➔n➔s➔t➔a➔l➔l➔ ➔o➔n➔ ➔R➔H➔E➔L➔ ➔o➔n➔l➔y➔
➔ ➔ ➔ ➔ ➔y➔u➔m➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔n➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔p➔r➔e➔s➔e➔n➔t➔
➔ ➔ ➔ ➔ ➔w➔h➔e➔n➔:➔ ➔a➔n➔s➔i➔b➔l➔e➔_➔o➔s➔_➔f➔a➔m➔i➔l➔y➔ ➔=➔=➔ ➔"➔R➔e➔d➔H➔a➔t➔"➔
➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔O➔n➔l➔y➔ ➔r➔u➔n➔ ➔i➔n➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔ ➔ ➔ ➔ ➔s➔h➔e➔l➔l➔:➔ ➔d➔e➔p➔l➔o➔y➔.➔s➔h➔
➔ ➔ ➔ ➔ ➔w➔h➔e➔n➔:➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔=➔=➔ ➔"➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔"➔
➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔M➔u➔l➔t➔i➔p➔l➔e➔ ➔c➔o➔n➔d➔i➔t➔i➔o➔n➔s➔
➔ ➔ ➔ ➔ ➔a➔p➔t➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔n➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔p➔r➔e➔s➔e➔n➔t➔
➔ ➔ ➔ ➔ ➔w➔h➔e➔n➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔a➔n➔s➔i➔b➔l➔e➔_➔o➔s➔_➔f➔a➔m➔i➔l➔y➔ ➔=➔=➔ ➔"➔D➔e➔b➔i➔a➔n➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔a➔n➔s➔i➔b➔l➔e➔_➔d➔i➔s➔t➔r➔i➔b➔u➔t➔i➔o➔n➔_➔m➔a➔j➔o➔r➔_➔v➔e➔r➔s➔i➔o➔n➔ ➔=➔=➔ ➔"➔2➔0➔"➔
➔ ➔ ➔#➔ ➔─➔─➔ ➔L➔O➔O➔P➔S➔ ➔─➔─➔
➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔I➔n➔s➔t➔a➔l➔l➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔p➔a➔c➔k➔a➔g➔e➔s➔
➔ ➔ ➔ ➔ ➔a➔p➔t➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔"➔{➔{➔ ➔i➔t➔e➔m➔ ➔}➔}➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔p➔r➔e➔s➔e➔n➔t➔
➔ ➔ ➔ ➔ ➔l➔o➔o➔p➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔n➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔g➔i➔t➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔c➔u➔r➔l➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔v➔i➔m➔
➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔C➔r➔e➔a➔t➔e➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔u➔s➔e➔r➔s➔
➔ ➔ ➔ ➔ ➔u➔s➔e➔r➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔"➔{➔{➔ ➔i➔t➔e➔m➔.➔n➔a➔m➔e➔ ➔}➔}➔"➔
➔
➔
➔
➔
➔ ➔ ➔ ➔ ➔ ➔ ➔g➔r➔o➔u➔p➔s➔:➔ ➔"➔{➔{➔ ➔i➔t➔e➔m➔.➔g➔r➔o➔u➔p➔ ➔}➔}➔"➔
➔ ➔ ➔ ➔ ➔l➔o➔o➔p➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔{➔ ➔n➔a➔m➔e➔:➔ ➔a➔l➔i➔c➔e➔,➔ ➔g➔r➔o➔u➔p➔:➔ ➔s➔u➔d➔o➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔{➔ ➔n➔a➔m➔e➔:➔ ➔b➔o➔b➔,➔ ➔g➔r➔o➔u➔p➔:➔ ➔d➔o➔c➔k➔e➔r➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔{➔ ➔n➔a➔m➔e➔:➔ ➔c➔h➔a➔r➔l➔i➔e➔,➔ ➔g➔r➔o➔u➔p➔:➔ ➔d➔e➔v➔ ➔}➔
➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔C➔r➔e➔a➔t➔e➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔i➔e➔s➔
➔ ➔ ➔ ➔ ➔f➔i➔l➔e➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔p➔a➔t➔h➔:➔ ➔"➔{➔{➔ ➔i➔t➔e➔m➔ ➔}➔}➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔ ➔ ➔ ➔ ➔l➔o➔o➔p➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔/➔o➔p➔t➔/➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔/➔o➔p➔t➔/➔l➔o➔g➔s➔
➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔/➔o➔p➔t➔/➔c➔o➔n➔f➔i➔g➔
➔1➔2➔.➔ ➔T➔e➔m➔p➔l➔a➔t➔e➔s➔ ➔—➔ ➔J➔i➔n➔j➔a➔2➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔ ➔T➔e➔m➔p➔l➔a➔t➔e➔?➔
➔A➔ ➔f➔i➔l➔e➔ ➔w➔i➔t➔h➔ ➔p➔l➔a➔c➔e➔h➔o➔l➔d➔e➔r➔s➔ ➔(➔v➔a➔r➔i➔a➔b➔l➔e➔s➔)➔ ➔t➔h➔a➔t➔ ➔A➔n➔s➔i➔b➔l➔e➔ ➔f➔i➔l➔l➔s➔ ➔i➔n➔.➔ ➔U➔s➔e➔d➔ ➔f➔o➔r➔ ➔c➔o➔n➔f➔i➔g➔ ➔f➔i➔l➔e➔s➔ ➔t➔h➔a➔t➔ ➔d➔i➔f➔f➔e➔r➔ ➔p➔e➔r➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔.➔
➔{➔#➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔s➔/➔n➔g➔i➔n➔x➔.➔c➔o➔n➔f➔.➔j➔2➔ ➔#➔}➔
➔s➔e➔r➔v➔e➔r➔ ➔{➔
➔ ➔ ➔ ➔ ➔l➔i➔s➔t➔e➔n➔ ➔{➔{➔ ➔h➔t➔t➔p➔_➔p➔o➔r➔t➔ ➔}➔}➔;➔
➔ ➔ ➔ ➔ ➔s➔e➔r➔v➔e➔r➔_➔n➔a➔m➔e➔ ➔{➔{➔ ➔s➔e➔r➔v➔e➔r➔_➔n➔a➔m➔e➔ ➔}➔}➔;➔
➔ ➔ ➔ ➔ ➔
➔ ➔ ➔ ➔ ➔l➔o➔c➔a➔t➔i➔o➔n➔ ➔/➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔r➔o➔x➔y➔_➔p➔a➔s➔s➔ ➔h➔t➔t➔p➔:➔/➔/➔{➔{➔ ➔a➔p➔p➔_➔h➔o➔s➔t➔ ➔}➔}➔:➔{➔{➔ ➔a➔p➔p➔_➔p➔o➔r➔t➔ ➔}➔}➔;➔
➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔
➔ ➔ ➔ ➔ ➔a➔c➔c➔e➔s➔s➔_➔l➔o➔g➔ ➔/➔v➔a➔r➔/➔l➔o➔g➔/➔n➔g➔i➔n➔x➔/➔{➔{➔ ➔a➔p➔p➔_➔n➔a➔m➔e➔ ➔}➔}➔_➔a➔c➔c➔e➔s➔s➔.➔l➔o➔g➔;➔
➔}➔
➔{➔#➔ ➔C➔o➔n➔d➔i➔t➔i➔o➔n➔a➔l➔ ➔i➔n➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔ ➔#➔}➔
➔{➔%➔ ➔i➔f➔ ➔e➔n➔a➔b➔l➔e➔_➔s➔s➔l➔ ➔%➔}➔
➔ ➔ ➔ ➔ ➔l➔i➔s➔t➔e➔n➔ ➔4➔4➔3➔ ➔s➔s➔l➔;➔
➔ ➔ ➔ ➔ ➔s➔s➔l➔_➔c➔e➔r➔t➔i➔f➔i➔c➔a➔t➔e➔ ➔/➔e➔t➔c➔/➔s➔s➔l➔/➔{➔{➔ ➔a➔p➔p➔_➔n➔a➔m➔e➔ ➔}➔}➔.➔c➔r➔t➔;➔
➔{➔%➔ ➔e➔n➔d➔i➔f➔ ➔%➔}➔
➔{➔#➔ ➔L➔o➔o➔p➔ ➔i➔n➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔ ➔#➔}➔
➔u➔p➔s➔t➔r➔e➔a➔m➔ ➔b➔a➔c➔k➔e➔n➔d➔ ➔{➔
➔{➔%➔ ➔f➔o➔r➔ ➔s➔e➔r➔v➔e➔r➔ ➔i➔n➔ ➔b➔a➔c➔k➔e➔n➔d➔_➔s➔e➔r➔v➔e➔r➔s➔ ➔%➔}➔
➔ ➔ ➔ ➔ ➔s➔e➔r➔v➔e➔r➔ ➔{➔{➔ ➔s➔e➔r➔v➔e➔r➔ ➔}➔}➔:➔{➔{➔ ➔a➔p➔p➔_➔p➔o➔r➔t➔ ➔}➔}➔;➔
➔
➔
➔
➔
➔{➔%➔ ➔e➔n➔d➔f➔o➔r➔ ➔%➔}➔
➔}➔
➔#➔ ➔U➔s➔e➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔ ➔i➔n➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔D➔e➔p➔l➔o➔y➔ ➔n➔g➔i➔n➔x➔ ➔c➔o➔n➔f➔i➔g➔
➔ ➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔:➔
➔ ➔ ➔ ➔ ➔s➔r➔c➔:➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔s➔/➔n➔g➔i➔n➔x➔.➔c➔o➔n➔f➔.➔j➔2➔
➔ ➔ ➔ ➔ ➔d➔e➔s➔t➔:➔ ➔/➔e➔t➔c➔/➔n➔g➔i➔n➔x➔/➔s➔i➔t➔e➔s➔-➔a➔v➔a➔i➔l➔a➔b➔l➔e➔/➔{➔{➔ ➔a➔p➔p➔_➔n➔a➔m➔e➔ ➔}➔}➔.➔c➔o➔n➔f➔
➔ ➔ ➔v➔a➔r➔s➔:➔
➔ ➔ ➔ ➔ ➔h➔t➔t➔p➔_➔p➔o➔r➔t➔:➔ ➔8➔0➔
➔ ➔ ➔ ➔ ➔s➔e➔r➔v➔e➔r➔_➔n➔a➔m➔e➔:➔ ➔m➔y➔a➔p➔p➔.➔e➔x➔a➔m➔p➔l➔e➔.➔c➔o➔m➔
➔ ➔ ➔ ➔ ➔a➔p➔p➔_➔h➔o➔s➔t➔:➔ ➔l➔o➔c➔a➔l➔h➔o➔s➔t➔
➔ ➔ ➔ ➔ ➔a➔p➔p➔_➔p➔o➔r➔t➔:➔ ➔3➔0➔0➔0➔
➔ ➔ ➔n➔o➔t➔i➔f➔y➔:➔ ➔R➔e➔s➔t➔a➔r➔t➔ ➔N➔g➔i➔n➔x➔
➔1➔3➔.➔ ➔R➔o➔l➔e➔s➔ ➔—➔ ➔R➔e➔u➔s➔a➔b➔l➔e➔ ➔A➔n➔s➔i➔b➔l➔e➔ ➔C➔o➔d➔e➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔ ➔R➔o➔l➔e➔?➔
➔A➔ ➔s➔t➔r➔u➔c➔t➔u➔r➔e➔d➔ ➔w➔a➔y➔ ➔t➔o➔ ➔o➔r➔g➔a➔n➔i➔z➔e➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔s➔ ➔i➔n➔t➔o➔ ➔r➔e➔u➔s➔a➔b➔l➔e➔ ➔c➔o➔m➔p➔o➔n➔e➔n➔t➔s➔.➔ ➔L➔i➔k➔e➔ ➔a➔ ➔m➔o➔d➔u➔l➔e➔.➔
➔R➔o➔l➔e➔ ➔D➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔S➔t➔r➔u➔c➔t➔u➔r➔e➔:➔
➔r➔o➔l➔e➔s➔/➔
➔└➔─➔─➔ ➔n➔g➔i➔n➔x➔/➔
➔ ➔ ➔ ➔ ➔├➔─➔─➔ ➔t➔a➔s➔k➔s➔/➔
➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔└➔─➔─➔ ➔m➔a➔i➔n➔.➔y➔m➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔m➔a➔i➔n➔ ➔t➔a➔s➔k➔s➔
➔ ➔ ➔ ➔ ➔├➔─➔─➔ ➔h➔a➔n➔d➔l➔e➔r➔s➔/➔
➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔└➔─➔─➔ ➔m➔a➔i➔n➔.➔y➔m➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔h➔a➔n➔d➔l➔e➔r➔s➔
➔ ➔ ➔ ➔ ➔├➔─➔─➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔s➔/➔
➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔└➔─➔─➔ ➔n➔g➔i➔n➔x➔.➔c➔o➔n➔f➔.➔j➔2➔ ➔ ➔#➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔s➔
➔ ➔ ➔ ➔ ➔├➔─➔─➔ ➔f➔i➔l➔e➔s➔/➔
➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔└➔─➔─➔ ➔i➔n➔d➔e➔x➔.➔h➔t➔m➔l➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔t➔a➔t➔i➔c➔ ➔f➔i➔l➔e➔s➔
➔ ➔ ➔ ➔ ➔├➔─➔─➔ ➔v➔a➔r➔s➔/➔
➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔└➔─➔─➔ ➔m➔a➔i➔n➔.➔y➔m➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔
➔ ➔ ➔ ➔ ➔├➔─➔─➔ ➔d➔e➔f➔a➔u➔l➔t➔s➔/➔
➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔└➔─➔─➔ ➔m➔a➔i➔n➔.➔y➔m➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔f➔a➔u➔l➔t➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔ ➔(➔l➔o➔w➔e➔s➔t➔ ➔p➔r➔i➔o➔r➔i➔t➔y➔)➔
➔ ➔ ➔ ➔ ➔└➔─➔─➔ ➔m➔e➔t➔a➔/➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔└➔─➔─➔ ➔m➔a➔i➔n➔.➔y➔m➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔o➔l➔e➔ ➔m➔e➔t➔a➔d➔a➔t➔a➔,➔ ➔d➔e➔p➔e➔n➔d➔e➔n➔c➔i➔e➔s➔
➔C➔r➔e➔a➔t➔e➔ ➔R➔o➔l➔e➔:➔
➔
➔
➔
➔
➔a➔n➔s➔i➔b➔l➔e➔-➔g➔a➔l➔a➔x➔y➔ ➔i➔n➔i➔t➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔s➔ ➔r➔o➔l➔e➔ ➔s➔t➔r➔u➔c➔t➔u➔r➔e➔
➔a➔n➔s➔i➔b➔l➔e➔-➔g➔a➔l➔a➔x➔y➔ ➔i➔n➔i➔t➔ ➔d➔o➔c➔k➔e➔r➔
➔a➔n➔s➔i➔b➔l➔e➔-➔g➔a➔l➔a➔x➔y➔ ➔i➔n➔i➔t➔ ➔d➔e➔p➔l➔o➔y➔-➔a➔p➔p➔
➔U➔s➔e➔ ➔R➔o➔l➔e➔ ➔i➔n➔ ➔P➔l➔a➔y➔b➔o➔o➔k➔:➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔S➔e➔t➔u➔p➔ ➔W➔e➔b➔ ➔S➔e➔r➔v➔e➔r➔
➔ ➔ ➔h➔o➔s➔t➔s➔:➔ ➔w➔e➔b➔s➔e➔r➔v➔e➔r➔s➔
➔ ➔ ➔b➔e➔c➔o➔m➔e➔:➔ ➔y➔e➔s➔
➔ ➔ ➔r➔o➔l➔e➔s➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔p➔p➔l➔y➔ ➔n➔g➔i➔n➔x➔ ➔r➔o➔l➔e➔
➔ ➔ ➔ ➔ ➔-➔ ➔d➔o➔c➔k➔e➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔p➔p➔l➔y➔ ➔d➔o➔c➔k➔e➔r➔ ➔r➔o➔l➔e➔
➔ ➔ ➔ ➔ ➔-➔ ➔{➔ ➔r➔o➔l➔e➔:➔ ➔d➔e➔p➔l➔o➔y➔-➔a➔p➔p➔,➔ ➔a➔p➔p➔_➔n➔a➔m➔e➔:➔ ➔m➔y➔a➔p➔p➔ ➔}➔ ➔ ➔ ➔#➔ ➔w➔i➔t➔h➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔
➔I➔n➔s➔t➔a➔l➔l➔ ➔C➔o➔m➔m➔u➔n➔i➔t➔y➔ ➔R➔o➔l➔e➔s➔:➔
➔a➔n➔s➔i➔b➔l➔e➔-➔g➔a➔l➔a➔x➔y➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔g➔e➔e➔r➔l➔i➔n➔g➔g➔u➔y➔.➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔f➔r➔o➔m➔ ➔G➔a➔l➔a➔x➔y➔
➔a➔n➔s➔i➔b➔l➔e➔-➔g➔a➔l➔a➔x➔y➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔-➔r➔ ➔r➔e➔q➔u➔i➔r➔e➔m➔e➔n➔t➔s➔.➔y➔m➔l➔ ➔ ➔ ➔ ➔#➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔f➔r➔o➔m➔ ➔f➔i➔l➔e➔
➔a➔n➔s➔i➔b➔l➔e➔-➔g➔a➔l➔a➔x➔y➔ ➔l➔i➔s➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔i➔n➔s➔t➔a➔l➔l➔e➔d➔ ➔r➔o➔l➔e➔s➔
➔1➔4➔.➔ ➔A➔n➔s➔i➔b➔l➔e➔ ➔V➔a➔u➔l➔t➔ ➔—➔ ➔S➔e➔c➔r➔e➔t➔s➔ ➔M➔a➔n➔a➔g➔e➔m➔e➔n➔t➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔V➔a➔u➔l➔t➔?➔
➔E➔n➔c➔r➔y➔p➔t➔s➔ ➔s➔e➔n➔s➔i➔t➔i➔v➔e➔ ➔f➔i➔l➔e➔s➔ ➔(➔p➔a➔s➔s➔w➔o➔r➔d➔s➔,➔ ➔k➔e➔y➔s➔)➔ ➔s➔o➔ ➔y➔o➔u➔ ➔c➔a➔n➔ ➔s➔a➔f➔e➔l➔y➔ ➔s➔t➔o➔r➔e➔ ➔t➔h➔e➔m➔ ➔i➔n➔ ➔G➔i➔t➔.➔
➔#➔ ➔C➔r➔e➔a➔t➔e➔ ➔e➔n➔c➔r➔y➔p➔t➔e➔d➔ ➔f➔i➔l➔e➔
➔a➔n➔s➔i➔b➔l➔e➔-➔v➔a➔u➔l➔t➔ ➔c➔r➔e➔a➔t➔e➔ ➔s➔e➔c➔r➔e➔t➔s➔.➔y➔m➔l➔
➔#➔ ➔E➔d➔i➔t➔ ➔e➔n➔c➔r➔y➔p➔t➔e➔d➔ ➔f➔i➔l➔e➔
➔a➔n➔s➔i➔b➔l➔e➔-➔v➔a➔u➔l➔t➔ ➔e➔d➔i➔t➔ ➔s➔e➔c➔r➔e➔t➔s➔.➔y➔m➔l➔
➔#➔ ➔E➔n➔c➔r➔y➔p➔t➔ ➔e➔x➔i➔s➔t➔i➔n➔g➔ ➔f➔i➔l➔e➔
➔a➔n➔s➔i➔b➔l➔e➔-➔v➔a➔u➔l➔t➔ ➔e➔n➔c➔r➔y➔p➔t➔ ➔v➔a➔r➔s➔/➔s➔e➔c➔r➔e➔t➔s➔.➔y➔m➔l➔
➔#➔ ➔D➔e➔c➔r➔y➔p➔t➔ ➔f➔i➔l➔e➔
➔a➔n➔s➔i➔b➔l➔e➔-➔v➔a➔u➔l➔t➔ ➔d➔e➔c➔r➔y➔p➔t➔ ➔v➔a➔r➔s➔/➔s➔e➔c➔r➔e➔t➔s➔.➔y➔m➔l➔
➔#➔ ➔V➔i➔e➔w➔ ➔e➔n➔c➔r➔y➔p➔t➔e➔d➔ ➔f➔i➔l➔e➔
➔a➔n➔s➔i➔b➔l➔e➔-➔v➔a➔u➔l➔t➔ ➔v➔i➔e➔w➔ ➔s➔e➔c➔r➔e➔t➔s➔.➔y➔m➔l➔
➔
➔
➔
➔
➔#➔ ➔C➔h➔a➔n➔g➔e➔ ➔v➔a➔u➔l➔t➔ ➔p➔a➔s➔s➔w➔o➔r➔d➔
➔a➔n➔s➔i➔b➔l➔e➔-➔v➔a➔u➔l➔t➔ ➔r➔e➔k➔e➔y➔ ➔s➔e➔c➔r➔e➔t➔s➔.➔y➔m➔l➔
➔#➔ ➔R➔u➔n➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔ ➔w➔i➔t➔h➔ ➔v➔a➔u➔l➔t➔
➔a➔n➔s➔i➔b➔l➔e➔-➔p➔l➔a➔y➔b➔o➔o➔k➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔.➔y➔m➔l➔ ➔-➔-➔a➔s➔k➔-➔v➔a➔u➔l➔t➔-➔p➔a➔s➔s➔
➔a➔n➔s➔i➔b➔l➔e➔-➔p➔l➔a➔y➔b➔o➔o➔k➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔.➔y➔m➔l➔ ➔-➔-➔v➔a➔u➔l➔t➔-➔p➔a➔s➔s➔w➔o➔r➔d➔-➔f➔i➔l➔e➔ ➔~➔/➔.➔v➔a➔u➔l➔t➔_➔p➔a➔s➔s➔
➔1➔5➔.➔ ➔C➔o➔m➔p➔l➔e➔t➔e➔ ➔P➔l➔a➔y➔b➔o➔o➔k➔ ➔—➔ ➔D➔e➔p➔l➔o➔y➔ ➔F➔u➔l➔l➔ ➔S➔t➔a➔c➔k➔ ➔A➔p➔p➔
➔-➔-➔-➔
➔#➔ ➔d➔e➔p➔l➔o➔y➔-➔a➔p➔p➔.➔y➔m➔l➔ ➔—➔ ➔D➔e➔p➔l➔o➔y➔ ➔N➔o➔d➔e➔.➔j➔s➔ ➔a➔p➔p➔ ➔w➔i➔t➔h➔ ➔N➔g➔i➔n➔x➔ ➔o➔n➔ ➔U➔b➔u➔n➔t➔u➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔D➔e➔p➔l➔o➔y➔ ➔F➔u➔l➔l➔ ➔S➔t➔a➔c➔k➔ ➔A➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔
➔ ➔ ➔h➔o➔s➔t➔s➔:➔ ➔w➔e➔b➔s➔e➔r➔v➔e➔r➔s➔
➔ ➔ ➔b➔e➔c➔o➔m➔e➔:➔ ➔y➔e➔s➔
➔ ➔ ➔v➔a➔r➔s➔_➔f➔i➔l➔e➔s➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔v➔a➔r➔s➔/➔m➔a➔i➔n➔.➔y➔m➔l➔
➔ ➔ ➔ ➔ ➔-➔ ➔v➔a➔r➔s➔/➔s➔e➔c➔r➔e➔t➔s➔.➔y➔m➔l➔
➔ ➔ ➔v➔a➔r➔s➔:➔
➔ ➔ ➔ ➔ ➔a➔p➔p➔_➔n➔a➔m➔e➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔a➔p➔p➔_➔d➔i➔r➔:➔ ➔/➔o➔p➔t➔/➔{➔{➔ ➔a➔p➔p➔_➔n➔a➔m➔e➔ ➔}➔}➔
➔ ➔ ➔ ➔ ➔a➔p➔p➔_➔p➔o➔r➔t➔:➔ ➔3➔0➔0➔0➔
➔ ➔ ➔ ➔ ➔n➔g➔i➔n➔x➔_➔p➔o➔r➔t➔:➔ ➔8➔0➔
➔ ➔ ➔ ➔ ➔n➔o➔d➔e➔_➔v➔e➔r➔s➔i➔o➔n➔:➔ ➔"➔1➔8➔"➔
➔ ➔ ➔ ➔ ➔g➔i➔t➔_➔r➔e➔p➔o➔:➔ ➔h➔t➔t➔p➔s➔:➔/➔/➔g➔i➔t➔h➔u➔b➔.➔c➔o➔m➔/➔a➔k➔h➔i➔l➔/➔m➔y➔a➔p➔p➔.➔g➔i➔t➔
➔ ➔ ➔t➔a➔s➔k➔s➔:➔
➔ ➔ ➔ ➔ ➔#➔ ➔─➔─➔ ➔S➔Y➔S➔T➔E➔M➔ ➔S➔E➔T➔U➔P➔ ➔─➔─➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔U➔p➔d➔a➔t➔e➔ ➔a➔p➔t➔ ➔c➔a➔c➔h➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔t➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔u➔p➔d➔a➔t➔e➔_➔c➔a➔c➔h➔e➔:➔ ➔y➔e➔s➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔c➔a➔c➔h➔e➔_➔v➔a➔l➔i➔d➔_➔t➔i➔m➔e➔:➔ ➔3➔6➔0➔0➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔I➔n➔s➔t➔a➔l➔l➔ ➔s➔y➔s➔t➔e➔m➔ ➔d➔e➔p➔e➔n➔d➔e➔n➔c➔i➔e➔s➔
➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔t➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔c➔u➔r➔l➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔g➔i➔t➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔n➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔-➔ ➔u➔f➔w➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔p➔r➔e➔s➔e➔n➔t➔
➔
➔
➔
➔
➔ ➔ ➔ ➔ ➔#➔ ➔─➔─➔ ➔N➔O➔D➔E➔.➔J➔S➔ ➔─➔─➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔A➔d➔d➔ ➔N➔o➔d➔e➔S➔o➔u➔r➔c➔e➔ ➔r➔e➔p➔o➔s➔i➔t➔o➔r➔y➔
➔ ➔ ➔ ➔ ➔ ➔ ➔s➔h➔e➔l➔l➔:➔ ➔c➔u➔r➔l➔ ➔-➔f➔s➔S➔L➔ ➔h➔t➔t➔p➔s➔:➔/➔/➔d➔e➔b➔.➔n➔o➔d➔e➔s➔o➔u➔r➔c➔e➔.➔c➔o➔m➔/➔s➔e➔t➔u➔p➔_➔{➔{➔ ➔n➔o➔d➔e➔_➔v➔e➔r➔s➔i➔o➔n➔ ➔}➔}➔.➔x➔ ➔|➔ ➔b➔a➔s➔h➔ ➔-➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔I➔n➔s➔t➔a➔l➔l➔ ➔N➔o➔d➔e➔.➔j➔s➔
➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔t➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔n➔o➔d➔e➔j➔s➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔p➔r➔e➔s➔e➔n➔t➔
➔ ➔ ➔ ➔ ➔#➔ ➔─➔─➔ ➔A➔P➔P➔L➔I➔C➔A➔T➔I➔O➔N➔ ➔─➔─➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔C➔r➔e➔a➔t➔e➔ ➔a➔p➔p➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔ ➔ ➔ ➔ ➔ ➔ ➔f➔i➔l➔e➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔a➔t➔h➔:➔ ➔"➔{➔{➔ ➔a➔p➔p➔_➔d➔i➔r➔ ➔}➔}➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔o➔w➔n➔e➔r➔:➔ ➔u➔b➔u➔n➔t➔u➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔m➔o➔d➔e➔:➔ ➔'➔0➔7➔5➔5➔'➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔C➔l➔o➔n➔e➔ ➔a➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔ ➔c➔o➔d➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔g➔i➔t➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔r➔e➔p➔o➔:➔ ➔"➔{➔{➔ ➔g➔i➔t➔_➔r➔e➔p➔o➔ ➔}➔}➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔e➔s➔t➔:➔ ➔"➔{➔{➔ ➔a➔p➔p➔_➔d➔i➔r➔ ➔}➔}➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔v➔e➔r➔s➔i➔o➔n➔:➔ ➔m➔a➔i➔n➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔f➔o➔r➔c➔e➔:➔ ➔y➔e➔s➔
➔ ➔ ➔ ➔ ➔ ➔ ➔b➔e➔c➔o➔m➔e➔_➔u➔s➔e➔r➔:➔ ➔u➔b➔u➔n➔t➔u➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔I➔n➔s➔t➔a➔l➔l➔ ➔n➔p➔m➔ ➔d➔e➔p➔e➔n➔d➔e➔n➔c➔i➔e➔s➔
➔ ➔ ➔ ➔ ➔ ➔ ➔n➔p➔m➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔a➔t➔h➔:➔ ➔"➔{➔{➔ ➔a➔p➔p➔_➔d➔i➔r➔ ➔}➔}➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔b➔e➔c➔o➔m➔e➔_➔u➔s➔e➔r➔:➔ ➔u➔b➔u➔n➔t➔u➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔S➔e➔t➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔
➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔p➔y➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔c➔o➔n➔t➔e➔n➔t➔:➔ ➔|➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔N➔O➔D➔E➔_➔E➔N➔V➔=➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔P➔O➔R➔T➔=➔{➔{➔ ➔a➔p➔p➔_➔p➔o➔r➔t➔ ➔}➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔D➔B➔_➔H➔O➔S➔T➔=➔{➔{➔ ➔d➔b➔_➔h➔o➔s➔t➔ ➔}➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔D➔B➔_➔P➔A➔S➔S➔W➔O➔R➔D➔=➔{➔{➔ ➔d➔b➔_➔p➔a➔s➔s➔w➔o➔r➔d➔ ➔}➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔e➔s➔t➔:➔ ➔"➔{➔{➔ ➔a➔p➔p➔_➔d➔i➔r➔ ➔}➔}➔/➔.➔e➔n➔v➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔m➔o➔d➔e➔:➔ ➔'➔0➔6➔0➔0➔'➔
➔ ➔ ➔ ➔ ➔#➔ ➔─➔─➔ ➔N➔G➔I➔N➔X➔ ➔─➔─➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔D➔e➔p➔l➔o➔y➔ ➔n➔g➔i➔n➔x➔ ➔c➔o➔n➔f➔i➔g➔
➔ ➔ ➔ ➔ ➔ ➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔r➔c➔:➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔s➔/➔n➔g➔i➔n➔x➔.➔c➔o➔n➔f➔.➔j➔2➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔e➔s➔t➔:➔ ➔/➔e➔t➔c➔/➔n➔g➔i➔n➔x➔/➔s➔i➔t➔e➔s➔-➔a➔v➔a➔i➔l➔a➔b➔l➔e➔/➔{➔{➔ ➔a➔p➔p➔_➔n➔a➔m➔e➔ ➔}➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔n➔o➔t➔i➔f➔y➔:➔ ➔R➔e➔s➔t➔a➔r➔t➔ ➔N➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔E➔n➔a➔b➔l➔e➔ ➔n➔g➔i➔n➔x➔ ➔s➔i➔t➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔f➔i➔l➔e➔:➔
➔
➔
➔
➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔r➔c➔:➔ ➔/➔e➔t➔c➔/➔n➔g➔i➔n➔x➔/➔s➔i➔t➔e➔s➔-➔a➔v➔a➔i➔l➔a➔b➔l➔e➔/➔{➔{➔ ➔a➔p➔p➔_➔n➔a➔m➔e➔ ➔}➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔e➔s➔t➔:➔ ➔/➔e➔t➔c➔/➔n➔g➔i➔n➔x➔/➔s➔i➔t➔e➔s➔-➔e➔n➔a➔b➔l➔e➔d➔/➔{➔{➔ ➔a➔p➔p➔_➔n➔a➔m➔e➔ ➔}➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔l➔i➔n➔k➔
➔ ➔ ➔ ➔ ➔ ➔ ➔n➔o➔t➔i➔f➔y➔:➔ ➔R➔e➔s➔t➔a➔r➔t➔ ➔N➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔R➔e➔m➔o➔v➔e➔ ➔d➔e➔f➔a➔u➔l➔t➔ ➔n➔g➔i➔n➔x➔ ➔s➔i➔t➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔f➔i➔l➔e➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔a➔t➔h➔:➔ ➔/➔e➔t➔c➔/➔n➔g➔i➔n➔x➔/➔s➔i➔t➔e➔s➔-➔e➔n➔a➔b➔l➔e➔d➔/➔d➔e➔f➔a➔u➔l➔t➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔a➔b➔s➔e➔n➔t➔
➔ ➔ ➔ ➔ ➔ ➔ ➔n➔o➔t➔i➔f➔y➔:➔ ➔R➔e➔s➔t➔a➔r➔t➔ ➔N➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔#➔ ➔─➔─➔ ➔F➔I➔R➔E➔W➔A➔L➔L➔ ➔─➔─➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔A➔l➔l➔o➔w➔ ➔H➔T➔T➔P➔
➔ ➔ ➔ ➔ ➔ ➔ ➔u➔f➔w➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔r➔u➔l➔e➔:➔ ➔a➔l➔l➔o➔w➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔o➔r➔t➔:➔ ➔"➔8➔0➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔r➔o➔t➔o➔:➔ ➔t➔c➔p➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔A➔l➔l➔o➔w➔ ➔S➔S➔H➔
➔ ➔ ➔ ➔ ➔ ➔ ➔u➔f➔w➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔r➔u➔l➔e➔:➔ ➔a➔l➔l➔o➔w➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔o➔r➔t➔:➔ ➔"➔2➔2➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔r➔o➔t➔o➔:➔ ➔t➔c➔p➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔E➔n➔a➔b➔l➔e➔ ➔U➔F➔W➔
➔ ➔ ➔ ➔ ➔ ➔ ➔u➔f➔w➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔e➔n➔a➔b➔l➔e➔d➔
➔ ➔ ➔ ➔ ➔#➔ ➔─➔─➔ ➔S➔T➔A➔R➔T➔ ➔A➔P➔P➔ ➔─➔─➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔I➔n➔s➔t➔a➔l➔l➔ ➔P➔M➔2➔ ➔(➔p➔r➔o➔c➔e➔s➔s➔ ➔m➔a➔n➔a➔g➔e➔r➔)➔
➔ ➔ ➔ ➔ ➔ ➔ ➔n➔p➔m➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔p➔m➔2➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔g➔l➔o➔b➔a➔l➔:➔ ➔y➔e➔s➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔S➔t➔a➔r➔t➔ ➔a➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔ ➔w➔i➔t➔h➔ ➔P➔M➔2➔
➔ ➔ ➔ ➔ ➔ ➔ ➔s➔h➔e➔l➔l➔:➔ ➔p➔m➔2➔ ➔s➔t➔a➔r➔t➔ ➔a➔p➔p➔.➔j➔s➔ ➔-➔-➔n➔a➔m➔e➔ ➔{➔{➔ ➔a➔p➔p➔_➔n➔a➔m➔e➔ ➔}➔}➔ ➔|➔|➔ ➔p➔m➔2➔ ➔r➔e➔s➔t➔a➔r➔t➔ ➔{➔{➔ ➔a➔p➔p➔_➔n➔a➔m➔e➔ ➔}➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔a➔r➔g➔s➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔c➔h➔d➔i➔r➔:➔ ➔"➔{➔{➔ ➔a➔p➔p➔_➔d➔i➔r➔ ➔}➔}➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔b➔e➔c➔o➔m➔e➔_➔u➔s➔e➔r➔:➔ ➔u➔b➔u➔n➔t➔u➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔S➔a➔v➔e➔ ➔P➔M➔2➔ ➔c➔o➔n➔f➔i➔g➔
➔ ➔ ➔ ➔ ➔ ➔ ➔s➔h➔e➔l➔l➔:➔ ➔p➔m➔2➔ ➔s➔a➔v➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔b➔e➔c➔o➔m➔e➔_➔u➔s➔e➔r➔:➔ ➔u➔b➔u➔n➔t➔u➔
➔ ➔ ➔h➔a➔n➔d➔l➔e➔r➔s➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔R➔e➔s➔t➔a➔r➔t➔ ➔N➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔ ➔ ➔s➔e➔r➔v➔i➔c➔e➔:➔
➔
➔
➔
➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔n➔g➔i➔n➔x➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔r➔e➔s➔t➔a➔r➔t➔e➔d➔
➔1➔6➔.➔ ➔A➔n➔s➔i➔b➔l➔e➔ ➔f➔o➔r➔ ➔D➔e➔v➔O➔p➔s➔ ➔—➔ ➔K➔e➔y➔ ➔U➔s➔e➔ ➔C➔a➔s➔e➔s➔
➔1➔.➔ ➔P➔r➔o➔v➔i➔s➔i➔o➔n➔ ➔a➔n➔d➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔e➔ ➔E➔C➔2➔ ➔i➔n➔s➔t➔a➔n➔c➔e➔s➔:➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔C➔o➔n➔f➔i➔g➔u➔r➔e➔ ➔E➔C➔2➔ ➔i➔n➔s➔t➔a➔n➔c➔e➔s➔
➔ ➔ ➔h➔o➔s➔t➔s➔:➔ ➔a➔w➔s➔_➔e➔c➔2➔
➔ ➔ ➔t➔a➔s➔k➔s➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔I➔n➔s➔t➔a➔l➔l➔ ➔D➔o➔c➔k➔e➔r➔
➔ ➔ ➔ ➔ ➔ ➔ ➔a➔p➔t➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔d➔o➔c➔k➔e➔r➔.➔i➔o➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔p➔r➔e➔s➔e➔n➔t➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔S➔t➔a➔r➔t➔ ➔D➔o➔c➔k➔e➔r➔
➔ ➔ ➔ ➔ ➔ ➔ ➔s➔e➔r➔v➔i➔c➔e➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔d➔o➔c➔k➔e➔r➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔s➔t➔a➔r➔t➔e➔d➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔e➔n➔a➔b➔l➔e➔d➔:➔ ➔y➔e➔s➔
➔2➔.➔ ➔D➔e➔p➔l➔o➔y➔ ➔D➔o➔c➔k➔e➔r➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔:➔
➔-➔ ➔n➔a➔m➔e➔:➔ ➔D➔e➔p➔l➔o➔y➔ ➔A➔p➔p➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔
➔ ➔ ➔h➔o➔s➔t➔s➔:➔ ➔a➔l➔l➔
➔ ➔ ➔t➔a➔s➔k➔s➔:➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔P➔u➔l➔l➔ ➔l➔a➔t➔e➔s➔t➔ ➔i➔m➔a➔g➔e➔
➔ ➔ ➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔_➔i➔m➔a➔g➔e➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔a➔k➔h➔i➔l➔/➔m➔y➔a➔p➔p➔:➔l➔a➔t➔e➔s➔t➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔o➔u➔r➔c➔e➔:➔ ➔p➔u➔l➔l➔
➔ ➔ ➔ ➔ ➔-➔ ➔n➔a➔m➔e➔:➔ ➔R➔u➔n➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔
➔ ➔ ➔ ➔ ➔ ➔ ➔d➔o➔c➔k➔e➔r➔_➔c➔o➔n➔t➔a➔i➔n➔e➔r➔:➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔:➔ ➔m➔y➔a➔p➔p➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔i➔m➔a➔g➔e➔:➔ ➔a➔k➔h➔i➔l➔/➔m➔y➔a➔p➔p➔:➔l➔a➔t➔e➔s➔t➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔o➔r➔t➔s➔:➔ ➔[➔"➔8➔0➔:➔3➔0➔0➔0➔"➔]➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔r➔e➔s➔t➔a➔r➔t➔_➔p➔o➔l➔i➔c➔y➔:➔ ➔a➔l➔w➔a➔y➔s➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔t➔e➔:➔ ➔s➔t➔a➔r➔t➔e➔d➔
➔3➔.➔ ➔C➔o➔n➔f➔i➔g➔u➔r➔e➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔s➔e➔r➔v➔e➔r➔s➔ ➔a➔t➔ ➔o➔n➔c➔e➔:➔
➔#➔ ➔A➔p➔p➔l➔y➔ ➔t➔o➔ ➔a➔l➔l➔ ➔1➔0➔0➔ ➔s➔e➔r➔v➔e➔r➔s➔ ➔s➔i➔m➔u➔l➔t➔a➔n➔e➔o➔u➔s➔l➔y➔
➔
➔
➔
➔
➔a➔n➔s➔i➔b➔l➔e➔-➔p➔l➔a➔y➔b➔o➔o➔k➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔e➔-➔s➔e➔r➔v➔e➔r➔s➔.➔y➔m➔l➔ ➔-➔i➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔-➔i➔n➔v➔e➔n➔t➔o➔r➔y➔.➔i➔n➔i➔
➔1➔7➔.➔ ➔A➔n➔s➔i➔b➔l➔e➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔ ➔Q➔u➔i➔c➔k➔ ➔R➔e➔f➔e➔r➔e➔n➔c➔e➔
➔#➔ ➔─➔─➔ ➔A➔D➔-➔H➔O➔C➔ ➔─➔─➔
➔a➔n➔s➔i➔b➔l➔e➔ ➔a➔l➔l➔ ➔-➔m➔ ➔p➔i➔n➔g➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔t➔e➔s➔t➔ ➔c➔o➔n➔n➔e➔c➔t➔i➔v➔i➔t➔y➔
➔a➔n➔s➔i➔b➔l➔e➔ ➔w➔e➔b➔s➔e➔r➔v➔e➔r➔s➔ ➔-➔m➔ ➔s➔h➔e➔l➔l➔ ➔-➔a➔ ➔"➔u➔p➔t➔i➔m➔e➔"➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔u➔n➔ ➔c➔o➔m➔m➔a➔n➔d➔
➔a➔n➔s➔i➔b➔l➔e➔ ➔a➔l➔l➔ ➔-➔m➔ ➔s➔e➔t➔u➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔g➔a➔t➔h➔e➔r➔ ➔f➔a➔c➔t➔s➔
➔a➔n➔s➔i➔b➔l➔e➔ ➔a➔l➔l➔ ➔-➔m➔ ➔a➔p➔t➔ ➔-➔a➔ ➔"➔n➔a➔m➔e➔=➔n➔g➔i➔n➔x➔ ➔s➔t➔a➔t➔e➔=➔p➔r➔e➔s➔e➔n➔t➔"➔ ➔-➔-➔b➔e➔c➔o➔m➔e➔
➔#➔ ➔─➔─➔ ➔P➔L➔A➔Y➔B➔O➔O➔K➔ ➔─➔─➔
➔a➔n➔s➔i➔b➔l➔e➔-➔p➔l➔a➔y➔b➔o➔o➔k➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔.➔y➔m➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔u➔n➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔
➔a➔n➔s➔i➔b➔l➔e➔-➔p➔l➔a➔y➔b➔o➔o➔k➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔.➔y➔m➔l➔ ➔-➔-➔c➔h➔e➔c➔k➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔r➔y➔ ➔r➔u➔n➔
➔a➔n➔s➔i➔b➔l➔e➔-➔p➔l➔a➔y➔b➔o➔o➔k➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔.➔y➔m➔l➔ ➔-➔-➔d➔i➔f➔f➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔c➔h➔a➔n➔g➔e➔s➔
➔a➔n➔s➔i➔b➔l➔e➔-➔p➔l➔a➔y➔b➔o➔o➔k➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔.➔y➔m➔l➔ ➔-➔v➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔v➔e➔r➔b➔o➔s➔e➔
➔a➔n➔s➔i➔b➔l➔e➔-➔p➔l➔a➔y➔b➔o➔o➔k➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔.➔y➔m➔l➔ ➔-➔-➔t➔a➔g➔s➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔u➔n➔ ➔t➔a➔g➔g➔e➔d➔ ➔t➔a➔s➔k➔s➔
➔a➔n➔s➔i➔b➔l➔e➔-➔p➔l➔a➔y➔b➔o➔o➔k➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔.➔y➔m➔l➔ ➔-➔-➔l➔i➔m➔i➔t➔ ➔w➔e➔b➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔t➔a➔r➔g➔e➔t➔ ➔o➔n➔e➔ ➔h➔o➔s➔t➔
➔a➔n➔s➔i➔b➔l➔e➔-➔p➔l➔a➔y➔b➔o➔o➔k➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔.➔y➔m➔l➔ ➔-➔e➔ ➔"➔e➔n➔v➔=➔p➔r➔o➔d➔"➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔x➔t➔r➔a➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔
➔#➔ ➔─➔─➔ ➔I➔N➔V➔E➔N➔T➔O➔R➔Y➔ ➔─➔─➔
➔a➔n➔s➔i➔b➔l➔e➔-➔i➔n➔v➔e➔n➔t➔o➔r➔y➔ ➔-➔-➔l➔i➔s➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔a➔l➔l➔ ➔h➔o➔s➔t➔s➔
➔a➔n➔s➔i➔b➔l➔e➔-➔i➔n➔v➔e➔n➔t➔o➔r➔y➔ ➔-➔-➔g➔r➔a➔p➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔t➔r➔e➔e➔ ➔v➔i➔e➔w➔
➔#➔ ➔─➔─➔ ➔G➔A➔L➔A➔X➔Y➔ ➔(➔R➔O➔L➔E➔S➔)➔ ➔─➔─➔
➔a➔n➔s➔i➔b➔l➔e➔-➔g➔a➔l➔a➔x➔y➔ ➔i➔n➔i➔t➔ ➔m➔y➔r➔o➔l➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔r➔o➔l➔e➔ ➔s➔t➔r➔u➔c➔t➔u➔r➔e➔
➔a➔n➔s➔i➔b➔l➔e➔-➔g➔a➔l➔a➔x➔y➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔g➔e➔e➔r➔l➔i➔n➔g➔g➔u➔y➔.➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔o➔w➔n➔l➔o➔a➔d➔ ➔r➔o➔l➔e➔
➔a➔n➔s➔i➔b➔l➔e➔-➔g➔a➔l➔a➔x➔y➔ ➔l➔i➔s➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔i➔n➔s➔t➔a➔l➔l➔e➔d➔ ➔r➔o➔l➔e➔s➔
➔#➔ ➔─➔─➔ ➔V➔A➔U➔L➔T➔ ➔─➔─➔
➔a➔n➔s➔i➔b➔l➔e➔-➔v➔a➔u➔l➔t➔ ➔c➔r➔e➔a➔t➔e➔ ➔s➔e➔c➔r➔e➔t➔s➔.➔y➔m➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔e➔n➔c➔r➔y➔p➔t➔e➔d➔ ➔f➔i➔l➔e➔
➔a➔n➔s➔i➔b➔l➔e➔-➔v➔a➔u➔l➔t➔ ➔e➔d➔i➔t➔ ➔s➔e➔c➔r➔e➔t➔s➔.➔y➔m➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔d➔i➔t➔ ➔e➔n➔c➔r➔y➔p➔t➔e➔d➔ ➔f➔i➔l➔e➔
➔a➔n➔s➔i➔b➔l➔e➔-➔v➔a➔u➔l➔t➔ ➔e➔n➔c➔r➔y➔p➔t➔ ➔v➔a➔r➔s➔.➔y➔m➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔n➔c➔r➔y➔p➔t➔ ➔e➔x➔i➔s➔t➔i➔n➔g➔ ➔f➔i➔l➔e➔
➔a➔n➔s➔i➔b➔l➔e➔-➔p➔l➔a➔y➔b➔o➔o➔k➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔.➔y➔m➔l➔ ➔-➔-➔a➔s➔k➔-➔v➔a➔u➔l➔t➔-➔p➔a➔s➔s➔ ➔ ➔#➔ ➔r➔u➔n➔ ➔w➔i➔t➔h➔ ➔v➔a➔u➔l➔t➔ ➔p➔a➔s➔s➔w➔o➔r➔d➔
➔#➔ ➔─➔─➔ ➔C➔O➔N➔F➔I➔G➔ ➔─➔─➔
➔a➔n➔s➔i➔b➔l➔e➔ ➔-➔-➔v➔e➔r➔s➔i➔o➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔v➔e➔r➔s➔i➔o➔n➔
➔a➔n➔s➔i➔b➔l➔e➔-➔c➔o➔n➔f➔i➔g➔ ➔l➔i➔s➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔a➔l➔l➔ ➔c➔o➔n➔f➔i➔g➔
➔a➔n➔s➔i➔b➔l➔e➔-➔c➔o➔n➔f➔i➔g➔ ➔d➔u➔m➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔a➔c➔t➔i➔v➔e➔ ➔c➔o➔n➔f➔i➔g➔
➔1➔8➔.➔ ➔A➔n➔s➔i➔b➔l➔e➔ ➔I➔n➔t➔e➔r➔v➔i➔e➔w➔ ➔Q➔&➔A➔
➔
➔
➔
➔
➔Q➔:➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔A➔n➔s➔i➔b➔l➔e➔ ➔a➔n➔d➔ ➔h➔o➔w➔ ➔i➔s➔ ➔i➔t➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔t➔ ➔f➔r➔o➔m➔ ➔C➔h➔e➔f➔/➔P➔u➔p➔p➔e➔t➔?➔
➔A➔n➔s➔i➔b➔l➔e➔ ➔i➔s➔ ➔a➔g➔e➔n➔t➔l➔e➔s➔s➔ ➔—➔ ➔n➔o➔ ➔s➔o➔f➔t➔w➔a➔r➔e➔ ➔n➔e➔e➔d➔e➔d➔ ➔o➔n➔ ➔m➔a➔n➔a➔g➔e➔d➔ ➔n➔o➔d➔e➔s➔.➔ ➔I➔t➔ ➔u➔s➔e➔s➔ ➔S➔S➔H➔ ➔t➔o➔ ➔p➔u➔s➔h➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔s➔.➔ ➔C➔h➔e➔f➔ ➔a➔n➔d➔
➔P➔u➔p➔p➔e➔t➔ ➔u➔s➔e➔ ➔a➔ ➔p➔u➔l➔l➔ ➔m➔o➔d➔e➔l➔ ➔w➔h➔e➔r➔e➔ ➔a➔g➔e➔n➔t➔s➔ ➔o➔n➔ ➔e➔a➔c➔h➔ ➔n➔o➔d➔e➔ ➔f➔e➔t➔c➔h➔ ➔c➔o➔n➔f➔i➔g➔ ➔f➔r➔o➔m➔ ➔a➔ ➔s➔e➔r➔v➔e➔r➔.➔
➔Q➔:➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔i➔d➔e➔m➔p➔o➔t➔e➔n➔c➔y➔ ➔i➔n➔ ➔A➔n➔s➔i➔b➔l➔e➔?➔
➔R➔u➔n➔n➔i➔n➔g➔ ➔t➔h➔e➔ ➔s➔a➔m➔e➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔t➔i➔m➔e➔s➔ ➔p➔r➔o➔d➔u➔c➔e➔s➔ ➔t➔h➔e➔ ➔s➔a➔m➔e➔ ➔r➔e➔s➔u➔l➔t➔.➔ ➔I➔f➔ ➔n➔g➔i➔n➔x➔ ➔i➔s➔ ➔a➔l➔r➔e➔a➔d➔y➔ ➔i➔n➔s➔t➔a➔l➔l➔e➔d➔,➔ ➔A➔n➔s➔i➔b➔l➔e➔ ➔w➔o➔n➔'➔t➔
➔i➔n➔s➔t➔a➔l➔l➔ ➔i➔t➔ ➔a➔g➔a➔i➔n➔.➔ ➔T➔h➔i➔s➔ ➔p➔r➔e➔v➔e➔n➔t➔s➔ ➔u➔n➔i➔n➔t➔e➔n➔d➔e➔d➔ ➔c➔h➔a➔n➔g➔e➔s➔.➔
➔Q➔:➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔t➔h➔e➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔c➔e➔ ➔b➔e➔t➔w➔e➔e➔n➔ ➔a➔ ➔t➔a➔s➔k➔ ➔a➔n➔d➔ ➔a➔ ➔h➔a➔n➔d➔l➔e➔r➔?➔
➔A➔ ➔t➔a➔s➔k➔ ➔a➔l➔w➔a➔y➔s➔ ➔r➔u➔n➔s➔ ➔w➔h➔e➔n➔ ➔t➔h➔e➔ ➔p➔l➔a➔y➔ ➔e➔x➔e➔c➔u➔t➔e➔s➔.➔ ➔A➔ ➔h➔a➔n➔d➔l➔e➔r➔ ➔o➔n➔l➔y➔ ➔r➔u➔n➔s➔ ➔w➔h➔e➔n➔ ➔n➔o➔t➔i➔f➔i➔e➔d➔ ➔b➔y➔ ➔a➔ ➔t➔a➔s➔k➔,➔ ➔a➔n➔d➔ ➔o➔n➔l➔y➔ ➔i➔f➔ ➔t➔h➔a➔t➔ ➔t➔a➔s➔k➔
➔m➔a➔d➔e➔ ➔a➔ ➔c➔h➔a➔n➔g➔e➔.➔ ➔U➔s➔e➔d➔ ➔f➔o➔r➔ ➔t➔h➔i➔n➔g➔s➔ ➔l➔i➔k➔e➔ ➔r➔e➔s➔t➔a➔r➔t➔i➔n➔g➔ ➔s➔e➔r➔v➔i➔c➔e➔s➔.➔
➔Q➔:➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔A➔n➔s➔i➔b➔l➔e➔ ➔V➔a➔u➔l➔t➔?➔
➔A➔ ➔f➔e➔a➔t➔u➔r➔e➔ ➔t➔o➔ ➔e➔n➔c➔r➔y➔p➔t➔ ➔s➔e➔n➔s➔i➔t➔i➔v➔e➔ ➔d➔a➔t➔a➔ ➔l➔i➔k➔e➔ ➔p➔a➔s➔s➔w➔o➔r➔d➔s➔ ➔a➔n➔d➔ ➔A➔P➔I➔ ➔k➔e➔y➔s➔ ➔s➔o➔ ➔t➔h➔e➔y➔ ➔c➔a➔n➔ ➔b➔e➔ ➔s➔a➔f➔e➔l➔y➔ ➔s➔t➔o➔r➔e➔d➔ ➔i➔n➔ ➔v➔e➔r➔s➔i➔o➔n➔ ➔c➔o➔n➔t➔r➔o➔l➔.➔
➔Q➔:➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔n➔ ➔A➔n➔s➔i➔b➔l➔e➔ ➔R➔o➔l➔e➔?➔
➔A➔ ➔s➔t➔r➔u➔c➔t➔u➔r➔e➔d➔,➔ ➔r➔e➔u➔s➔a➔b➔l➔e➔ ➔w➔a➔y➔ ➔t➔o➔ ➔o➔r➔g➔a➔n➔i➔z➔e➔ ➔t➔a➔s➔k➔s➔,➔ ➔h➔a➔n➔d➔l➔e➔r➔s➔,➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔s➔,➔ ➔a➔n➔d➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔.➔ ➔L➔i➔k➔e➔ ➔a➔ ➔f➔u➔n➔c➔t➔i➔o➔n➔ ➔i➔n➔ ➔p➔r➔o➔g➔r➔a➔m➔m➔i➔n➔g➔
➔—➔ ➔w➔r➔i➔t➔e➔ ➔o➔n➔c➔e➔,➔ ➔u➔s➔e➔ ➔m➔a➔n➔y➔ ➔t➔i➔m➔e➔s➔.➔
➔Q➔:➔ ➔H➔o➔w➔ ➔d➔o➔ ➔y➔o➔u➔ ➔h➔a➔n➔d➔l➔e➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔t➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔s➔ ➔i➔n➔ ➔A➔n➔s➔i➔b➔l➔e➔?➔
➔U➔s➔e➔ ➔s➔e➔p➔a➔r➔a➔t➔e➔ ➔i➔n➔v➔e➔n➔t➔o➔r➔y➔ ➔f➔i➔l➔e➔s➔ ➔(➔d➔e➔v➔-➔i➔n➔v➔e➔n➔t➔o➔r➔y➔.➔i➔n➔i➔,➔ ➔p➔r➔o➔d➔-➔i➔n➔v➔e➔n➔t➔o➔r➔y➔.➔i➔n➔i➔)➔ ➔a➔n➔d➔ ➔s➔e➔p➔a➔r➔a➔t➔e➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔ ➔f➔i➔l➔e➔s➔.➔ ➔R➔u➔n➔:➔ ➔a➔n➔s➔i➔b➔l➔e➔-➔
➔p➔l➔a➔y➔b➔o➔o➔k➔ ➔p➔l➔a➔y➔b➔o➔o➔k➔.➔y➔m➔l➔ ➔-➔i➔ ➔p➔r➔o➔d➔-➔i➔n➔v➔e➔n➔t➔o➔r➔y➔.➔i➔n➔i➔
➔D➔O➔C➔U➔M➔E➔N➔T➔ ➔S➔T➔A➔T➔U➔S➔ ➔&➔ ➔S➔T➔U➔D➔Y➔ ➔P➔L➔A➔N➔
➔✅➔ ➔ ➔W➔h➔a➔t➔'➔s➔ ➔C➔o➔v➔e➔r➔e➔d➔ ➔i➔n➔ ➔T➔h➔i➔s➔ ➔D➔o➔c➔u➔m➔e➔n➔t➔
➔#➔ ➔S➔e➔c➔t➔i➔o➔n➔ ➔T➔o➔p➔i➔c➔s➔ ➔C➔o➔v➔e➔r➔e➔d➔ ➔S➔t➔a➔t➔u➔s➔
➔1➔ ➔A➔W➔S➔ ➔C➔o➔r➔e➔ ➔I➔A➔M➔,➔ ➔R➔e➔g➔i➔o➔n➔s➔,➔ ➔A➔Z➔s➔,➔ ➔S➔e➔c➔u➔r➔i➔t➔y➔ ➔G➔r➔o➔u➔p➔s➔,➔ ➔A➔C➔L➔s➔,➔ ➔A➔u➔t➔o➔ ➔S➔c➔a➔l➔i➔n➔g➔,➔ ➔A➔L➔B➔ ➔v➔s➔ ➔N➔L➔B➔,➔
➔C➔l➔o➔u➔d➔W➔a➔t➔c➔h➔,➔ ➔R➔D➔S➔ ➔v➔s➔ ➔D➔y➔n➔a➔m➔o➔D➔B➔,➔ ➔S➔3➔ ➔v➔s➔ ➔E➔B➔S➔,➔ ➔V➔P➔C➔,➔ ➔S➔u➔b➔n➔e➔t➔s➔,➔ ➔E➔l➔a➔s➔t➔i➔c➔ ➔I➔P➔
➔✅➔
➔C➔o➔m➔p➔l➔e➔t➔e➔
➔2➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔ ➔D➔o➔c➔k➔e➔r➔ ➔d➔r➔a➔w➔b➔a➔c➔k➔s➔,➔ ➔S➔w➔a➔r➔m➔ ➔v➔s➔ ➔K➔8➔s➔,➔ ➔K➔8➔s➔ ➔f➔e➔a➔t➔u➔r➔e➔s➔,➔ ➔A➔r➔c➔h➔i➔t➔e➔c➔t➔u➔r➔e➔,➔ ➔k➔O➔p➔s➔,➔ ➔R➔C➔ ➔v➔s➔ ➔R➔S➔,➔
➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔s➔,➔ ➔S➔e➔r➔v➔i➔c➔e➔s➔ ➔(➔C➔l➔u➔s➔t➔e➔r➔I➔P➔/➔N➔o➔d➔e➔P➔o➔r➔t➔/➔L➔B➔)➔,➔ ➔V➔o➔l➔u➔m➔e➔s➔
➔(➔e➔m➔p➔t➔y➔D➔i➔r➔/➔h➔o➔s➔t➔P➔a➔t➔h➔/➔P➔V➔/➔P➔V➔C➔)➔,➔ ➔N➔a➔m➔e➔s➔p➔a➔c➔e➔s➔,➔ ➔D➔a➔e➔m➔o➔n➔S➔e➔t➔,➔ ➔C➔o➔n➔f➔i➔g➔M➔a➔p➔,➔
➔✅➔
➔C➔o➔m➔p➔l➔e➔t➔e➔
➔
➔
➔
➔
➔S➔e➔c➔r➔e➔t➔s➔,➔ ➔R➔B➔A➔C➔,➔ ➔J➔o➔b➔s➔,➔ ➔C➔r➔o➔n➔J➔o➔b➔s➔,➔ ➔T➔r➔o➔u➔b➔l➔e➔s➔h➔o➔o➔t➔i➔n➔g➔ ➔(➔9➔ ➔e➔r➔r➔o➔r➔s➔)➔,➔ ➔D➔e➔p➔l➔o➔y➔m➔e➔n➔t➔
➔S➔t➔r➔a➔t➔e➔g➔i➔e➔s➔ ➔(➔R➔e➔c➔r➔e➔a➔t➔e➔/➔R➔o➔l➔l➔i➔n➔g➔/➔B➔l➔u➔e➔-➔G➔r➔e➔e➔n➔/➔C➔a➔n➔a➔r➔y➔)➔,➔ ➔S➔t➔a➔t➔e➔f➔u➔l➔S➔e➔t➔
➔3➔ ➔D➔o➔c➔k➔e➔r➔ ➔V➔M➔ ➔v➔s➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔,➔ ➔D➔o➔c➔k➔e➔r➔ ➔A➔r➔c➔h➔i➔t➔e➔c➔t➔u➔r➔e➔,➔ ➔I➔m➔a➔g➔e➔s➔,➔ ➔D➔o➔c➔k➔e➔r➔f➔i➔l➔e➔ ➔(➔a➔l➔l➔ ➔i➔n➔s➔t➔r➔u➔c➔t➔i➔o➔n➔s➔)➔,➔
➔R➔e➔g➔i➔s➔t➔r➔y➔,➔ ➔C➔o➔n➔t➔a➔i➔n➔e➔r➔ ➔L➔i➔f➔e➔c➔y➔c➔l➔e➔,➔ ➔P➔o➔r➔t➔ ➔M➔a➔p➔p➔i➔n➔g➔,➔ ➔C➔o➔m➔p➔o➔s➔e➔ ➔(➔2➔ ➔t➔y➔p➔e➔s➔)➔,➔ ➔V➔o➔l➔u➔m➔e➔s➔ ➔(➔3➔
➔t➔y➔p➔e➔s➔)➔,➔ ➔N➔e➔t➔w➔o➔r➔k➔i➔n➔g➔ ➔(➔B➔r➔i➔d➔g➔e➔/➔H➔o➔s➔t➔/➔N➔o➔n➔e➔/➔O➔v➔e➔r➔l➔a➔y➔/➔M➔a➔c➔v➔l➔a➔n➔)➔,➔ ➔M➔u➔l➔t➔i➔-➔s➔t➔a➔g➔e➔,➔
➔J➔e➔n➔k➔i➔n➔s➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔,➔ ➔S➔e➔c➔u➔r➔i➔t➔y➔
➔✅➔
➔C➔o➔m➔p➔l➔e➔t➔e➔
➔4➔ ➔J➔e➔n➔k➔i➔n➔s➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔J➔e➔n➔k➔i➔n➔s➔,➔ ➔J➔o➔b➔ ➔t➔y➔p➔e➔s➔,➔ ➔J➔e➔n➔k➔i➔n➔s➔f➔i➔l➔e➔,➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔ ➔s➔t➔a➔g➔e➔s➔,➔ ➔T➔r➔i➔g➔g➔e➔r➔s➔,➔ ➔D➔e➔c➔l➔a➔r➔a➔t➔i➔v➔e➔
➔v➔s➔ ➔S➔c➔r➔i➔p➔t➔e➔d➔,➔ ➔C➔r➔e➔d➔e➔n➔t➔i➔a➔l➔s➔,➔ ➔M➔a➔s➔t➔e➔r➔/➔A➔g➔e➔n➔t➔,➔ ➔S➔h➔a➔r➔e➔d➔ ➔L➔i➔b➔r➔a➔r➔i➔e➔s➔,➔ ➔B➔l➔u➔e➔ ➔O➔c➔e➔a➔n➔
➔✅➔
➔C➔o➔m➔p➔l➔e➔t➔e➔
➔5➔ ➔G➔i➔t➔ ➔V➔C➔S➔ ➔t➔y➔p➔e➔s➔,➔ ➔G➔i➔t➔ ➔w➔o➔r➔k➔f➔l➔o➔w➔,➔ ➔4➔ ➔w➔o➔r➔k➔i➔n➔g➔ ➔a➔r➔e➔a➔s➔,➔ ➔S➔e➔t➔u➔p➔,➔ ➔B➔a➔s➔i➔c➔ ➔c➔o➔m➔m➔a➔n➔d➔s➔,➔
➔B➔r➔a➔n➔c➔h➔i➔n➔g➔,➔ ➔M➔e➔r➔g➔i➔n➔g➔ ➔(➔3➔ ➔t➔y➔p➔e➔s➔)➔,➔ ➔M➔e➔r➔g➔e➔ ➔c➔o➔n➔f➔l➔i➔c➔t➔s➔,➔ ➔R➔e➔m➔o➔t➔e➔ ➔r➔e➔p➔o➔,➔
➔P➔u➔s➔h➔/➔P➔u➔l➔l➔/➔F➔e➔t➔c➔h➔/➔C➔l➔o➔n➔e➔,➔ ➔U➔n➔d➔o➔i➔n➔g➔ ➔c➔h➔a➔n➔g➔e➔s➔,➔ ➔S➔t➔a➔s➔h➔,➔ ➔C➔h➔e➔r➔r➔y➔-➔p➔i➔c➔k➔,➔ ➔R➔e➔b➔a➔s➔e➔,➔ ➔T➔a➔g➔s➔,➔
➔.➔g➔i➔t➔i➔g➔n➔o➔r➔e➔,➔ ➔B➔r➔a➔n➔c➔h➔i➔n➔g➔ ➔s➔t➔r➔a➔t➔e➔g➔i➔e➔s➔,➔ ➔P➔R➔ ➔w➔o➔r➔k➔f➔l➔o➔w➔
➔✅➔
➔C➔o➔m➔p➔l➔e➔t➔e➔
➔6➔ ➔L➔i➔n➔u➔x➔ ➔F➔e➔a➔t➔u➔r➔e➔s➔,➔ ➔D➔i➔s➔t➔r➔o➔s➔,➔ ➔A➔r➔c➔h➔i➔t➔e➔c➔t➔u➔r➔e➔,➔ ➔S➔h➔e➔l➔l➔ ➔t➔y➔p➔e➔s➔,➔ ➔F➔i➔l➔e➔ ➔s➔y➔s➔t➔e➔m➔ ➔s➔t➔r➔u➔c➔t➔u➔r➔e➔,➔ ➔F➔i➔l➔e➔ ➔s➔y➔s➔t➔e➔m➔
➔t➔y➔p➔e➔s➔,➔ ➔A➔b➔s➔o➔l➔u➔t➔e➔/➔R➔e➔l➔a➔t➔i➔v➔e➔ ➔p➔a➔t➔h➔,➔ ➔F➔i➔l➔e➔ ➔c➔o➔m➔m➔a➔n➔d➔s➔,➔ ➔V➔o➔l➔u➔m➔e➔ ➔o➔n➔ ➔E➔C➔2➔,➔ ➔S➔y➔s➔t➔e➔m➔
➔c➔o➔m➔m➔a➔n➔d➔s➔,➔ ➔U➔s➔e➔r➔ ➔m➔a➔n➔a➔g➔e➔m➔e➔n➔t➔,➔ ➔G➔r➔o➔u➔p➔ ➔m➔a➔n➔a➔g➔e➔m➔e➔n➔t➔,➔ ➔F➔i➔l➔e➔ ➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔,➔ ➔A➔C➔L➔
➔(➔s➔e➔t➔f➔a➔c➔l➔/➔g➔e➔t➔f➔a➔c➔l➔)➔,➔ ➔C➔o➔m➔p➔r➔e➔s➔s➔i➔o➔n➔,➔ ➔F➔i➔l➔t➔e➔r➔ ➔c➔o➔m➔m➔a➔n➔d➔s➔ ➔+➔ ➔R➔e➔g➔e➔x➔,➔
➔f➔i➔n➔d➔/➔l➔o➔c➔a➔t➔e➔/➔u➔p➔d➔a➔t➔e➔d➔b➔,➔ ➔P➔i➔p➔i➔n➔g➔/➔R➔e➔d➔i➔r➔e➔c➔t➔i➔o➔n➔,➔ ➔N➔e➔t➔w➔o➔r➔k➔i➔n➔g➔ ➔c➔o➔m➔m➔a➔n➔d➔s➔
➔✅➔
➔C➔o➔m➔p➔l➔e➔t➔e➔
➔7➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔,➔ ➔H➔o➔w➔ ➔i➔t➔ ➔w➔o➔r➔k➔s➔,➔ ➔F➔i➔l➔e➔s➔,➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔,➔ ➔P➔r➔o➔v➔i➔d➔e➔r➔s➔,➔ ➔R➔e➔s➔o➔u➔r➔c➔e➔
➔b➔l➔o➔c➔k➔s➔,➔ ➔V➔P➔C➔ ➔c➔r➔e➔a➔t➔i➔o➔n➔,➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔s➔ ➔(➔a➔l➔l➔ ➔t➔y➔p➔e➔s➔)➔,➔ ➔O➔u➔t➔p➔u➔t➔s➔,➔ ➔S➔t➔a➔t➔e➔ ➔(➔l➔o➔c➔a➔l➔ ➔v➔s➔ ➔r➔e➔m➔o➔t➔e➔)➔,➔
➔W➔o➔r➔k➔s➔p➔a➔c➔e➔s➔,➔ ➔M➔o➔d➔u➔l➔e➔s➔,➔ ➔M➔e➔t➔a➔-➔a➔r➔g➔u➔m➔e➔n➔t➔s➔,➔ ➔D➔a➔t➔a➔ ➔s➔o➔u➔r➔c➔e➔s➔,➔ ➔L➔o➔c➔a➔l➔s➔,➔ ➔I➔n➔t➔e➔r➔v➔i➔e➔w➔
➔Q➔&➔A➔
➔✅➔
➔C➔o➔m➔p➔l➔e➔t➔e➔
➔8➔ ➔A➔z➔u➔r➔e➔
➔D➔e➔v➔O➔p➔s➔
➔D➔e➔v➔O➔p➔s➔ ➔c➔u➔l➔t➔u➔r➔e➔,➔ ➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔ ➔5➔ ➔s➔e➔r➔v➔i➔c➔e➔s➔,➔ ➔B➔o➔a➔r➔d➔s➔
➔(➔E➔p➔i➔c➔s➔/➔F➔e➔a➔t➔u➔r➔e➔s➔/➔S➔t➔o➔r➔i➔e➔s➔/➔T➔a➔s➔k➔s➔)➔,➔ ➔R➔e➔p➔o➔s➔,➔ ➔B➔r➔a➔n➔c➔h➔ ➔p➔o➔l➔i➔c➔i➔e➔s➔,➔ ➔P➔R➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔s➔,➔ ➔S➔e➔l➔f➔-➔
➔h➔o➔s➔t➔e➔d➔ ➔a➔g➔e➔n➔t➔ ➔s➔e➔t➔u➔p➔,➔ ➔Y➔A➔M➔L➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔s➔,➔ ➔T➔r➔i➔g➔g➔e➔r➔s➔,➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔s➔,➔ ➔M➔u➔l➔t➔i➔-➔s➔t➔a➔g➔e➔
➔p➔i➔p➔e➔l➔i➔n➔e➔s➔,➔ ➔E➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔s➔,➔ ➔A➔p➔p➔r➔o➔v➔a➔l➔s➔,➔ ➔D➔O➔R➔A➔ ➔m➔e➔t➔r➔i➔c➔s➔,➔ ➔Y➔o➔u➔r➔ ➔P➔r➔o➔j➔e➔c➔t➔ ➔1➔ ➔(➔T➔o➔m➔c➔a➔t➔
➔C➔I➔/➔C➔D➔)➔,➔ ➔Y➔o➔u➔r➔ ➔P➔r➔o➔j➔e➔c➔t➔ ➔2➔ ➔(➔R➔e➔v➔e➔r➔s➔e➔ ➔P➔r➔o➔x➔y➔ ➔+➔ ➔L➔G➔T➔M➔)➔
➔✅➔
➔C➔o➔m➔p➔l➔e➔t➔e➔
➔9➔ ➔A➔n➔s➔i➔b➔l➔e➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔A➔n➔s➔i➔b➔l➔e➔,➔ ➔A➔r➔c➔h➔i➔t➔e➔c➔t➔u➔r➔e➔,➔ ➔C➔o➔m➔p➔o➔n➔e➔n➔t➔s➔,➔ ➔I➔n➔s➔t➔a➔l➔l➔a➔t➔i➔o➔n➔,➔ ➔I➔n➔v➔e➔n➔t➔o➔r➔y➔,➔ ➔A➔d➔-➔h➔o➔c➔
➔c➔o➔m➔m➔a➔n➔d➔s➔,➔ ➔P➔l➔a➔y➔b➔o➔o➔k➔s➔,➔ ➔C➔o➔m➔m➔o➔n➔ ➔m➔o➔d➔u➔l➔e➔s➔,➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔s➔,➔ ➔H➔a➔n➔d➔l➔e➔r➔s➔,➔
➔C➔o➔n➔d➔i➔t➔i➔o➔n➔a➔l➔s➔/➔L➔o➔o➔p➔s➔,➔ ➔T➔e➔m➔p➔l➔a➔t➔e➔s➔ ➔(➔J➔i➔n➔j➔a➔2➔)➔,➔ ➔R➔o➔l➔e➔s➔,➔ ➔V➔a➔u➔l➔t➔,➔ ➔C➔o➔m➔p➔l➔e➔t➔e➔ ➔d➔e➔p➔l➔o➔y➔
➔p➔l➔a➔y➔b➔o➔o➔k➔,➔ ➔D➔e➔v➔O➔p➔s➔ ➔u➔s➔e➔ ➔c➔a➔s➔e➔s➔,➔ ➔I➔n➔t➔e➔r➔v➔i➔e➔w➔ ➔Q➔&➔A➔
➔✅➔
➔C➔o➔m➔p➔l➔e➔t➔e➔
➔❌➔ ➔ ➔T➔h➔i➔n➔g➔s➔ ➔S➔t➔i➔l➔l➔ ➔M➔i➔s➔s➔i➔n➔g➔ ➔/➔ ➔T➔o➔ ➔A➔d➔d➔ ➔L➔a➔t➔e➔r➔
➔T➔o➔p➔i➔c➔ ➔P➔r➔i➔o➔r➔i➔t➔y➔ ➔W➔h➔y➔ ➔I➔m➔p➔o➔r➔t➔a➔n➔t➔
➔A➔W➔S➔ ➔S➔c➔e➔n➔a➔r➔i➔o➔-➔b➔a➔s➔e➔d➔ ➔q➔u➔e➔s➔t➔i➔o➔n➔s➔ ➔🔴➔ ➔ ➔H➔i➔g➔h➔ ➔I➔n➔t➔e➔r➔v➔i➔e➔w➔e➔r➔s➔ ➔l➔o➔v➔e➔ ➔s➔c➔e➔n➔a➔r➔i➔o➔s➔
➔
➔
➔
➔
➔A➔W➔S➔ ➔L➔a➔m➔b➔d➔a➔ ➔b➔a➔s➔i➔c➔s➔ ➔🟡➔ ➔ ➔M➔e➔d➔i➔u➔m➔ ➔S➔e➔r➔v➔e➔r➔l➔e➔s➔s➔ ➔t➔r➔e➔n➔d➔i➔n➔g➔
➔A➔W➔S➔ ➔E➔K➔S➔ ➔(➔m➔a➔n➔a➔g➔e➔d➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔)➔ ➔🟡➔ ➔ ➔M➔e➔d➔i➔u➔m➔ ➔A➔l➔t➔e➔r➔n➔a➔t➔i➔v➔e➔ ➔t➔o➔ ➔k➔O➔p➔s➔
➔N➔e➔t➔w➔o➔r➔k➔i➔n➔g➔ ➔d➔e➔e➔p➔ ➔d➔i➔v➔e➔ ➔(➔O➔S➔I➔,➔ ➔D➔N➔S➔,➔ ➔T➔C➔P➔/➔I➔P➔)➔ ➔🟡➔ ➔ ➔M➔e➔d➔i➔u➔m➔ ➔D➔e➔v➔O➔p➔s➔ ➔f➔u➔n➔d➔a➔m➔e➔n➔t➔a➔l➔s➔
➔S➔o➔n➔a➔r➔Q➔u➔b➔e➔ ➔b➔a➔s➔i➔c➔s➔ ➔🟡➔ ➔ ➔M➔e➔d➔i➔u➔m➔ ➔O➔n➔ ➔y➔o➔u➔r➔ ➔J➔e➔n➔k➔i➔n➔s➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔
➔N➔e➔x➔u➔s➔ ➔b➔a➔s➔i➔c➔s➔ ➔🟡➔ ➔ ➔M➔e➔d➔i➔u➔m➔ ➔A➔r➔t➔i➔f➔a➔c➔t➔ ➔m➔a➔n➔a➔g➔e➔m➔e➔n➔t➔
➔G➔i➔t➔H➔u➔b➔ ➔A➔c➔t➔i➔o➔n➔s➔ ➔v➔s➔ ➔J➔e➔n➔k➔i➔n➔s➔ ➔v➔s➔ ➔A➔z➔u➔r➔e➔ ➔P➔i➔p➔e➔l➔i➔n➔e➔s➔ ➔🟡➔ ➔ ➔M➔e➔d➔i➔u➔m➔ ➔C➔o➔m➔m➔o➔n➔ ➔i➔n➔t➔e➔r➔v➔i➔e➔w➔ ➔c➔o➔m➔p➔a➔r➔i➔s➔o➔n➔
➔P➔o➔s➔t➔g➔r➔e➔S➔Q➔L➔ ➔b➔a➔s➔i➔c➔s➔ ➔🟢➔ ➔ ➔L➔o➔w➔ ➔O➔n➔ ➔y➔o➔u➔r➔ ➔r➔e➔s➔u➔m➔e➔
➔A➔p➔a➔c➔h➔e➔ ➔T➔o➔m➔c➔a➔t➔ ➔d➔e➔e➔p➔ ➔d➔i➔v➔e➔ ➔🟢➔ ➔ ➔L➔o➔w➔ ➔Y➔o➔u➔r➔ ➔p➔r➔o➔j➔e➔c➔t➔ ➔e➔x➔p➔e➔r➔i➔e➔n➔c➔e➔ ➔c➔o➔v➔e➔r➔s➔ ➔i➔t➔
➔M➔o➔c➔k➔ ➔i➔n➔t➔e➔r➔v➔i➔e➔w➔ ➔q➔u➔e➔s➔t➔i➔o➔n➔s➔ ➔(➔a➔l➔l➔ ➔t➔o➔p➔i➔c➔s➔)➔ ➔🔴➔ ➔ ➔H➔i➔g➔h➔ ➔P➔r➔a➔c➔t➔i➔c➔e➔ ➔m➔a➔k➔e➔s➔ ➔p➔e➔r➔f➔e➔c➔t➔
➔📊➔ ➔ ➔D➔o➔c➔u➔m➔e➔n➔t➔ ➔S➔t➔a➔t➔i➔s➔t➔i➔c➔s➔
➔M➔e➔t➔r➔i➔c➔ ➔V➔a➔l➔u➔e➔
➔T➔o➔t➔a➔l➔ ➔S➔e➔c➔t➔i➔o➔n➔s➔ ➔9➔
➔E➔s➔t➔i➔m➔a➔t➔e➔d➔ ➔P➔a➔g➔e➔s➔ ➔1➔9➔0➔-➔2➔0➔0➔ ➔p➔a➔g➔e➔s➔
➔T➔o➔p➔i➔c➔s➔ ➔C➔o➔v➔e➔r➔e➔d➔ ➔1➔5➔0➔+➔
➔C➔o➔m➔m➔a➔n➔d➔s➔ ➔I➔n➔c➔l➔u➔d➔e➔d➔ ➔5➔0➔0➔+➔
➔Y➔A➔M➔L➔ ➔E➔x➔a➔m➔p➔l➔e➔s➔ ➔4➔0➔+➔
➔B➔a➔s➔e➔d➔ ➔o➔n➔ ➔Y➔o➔u➔r➔ ➔R➔e➔s➔u➔m➔e➔ ➔✅➔ ➔ ➔Y➔e➔s➔
➔📅➔ ➔ ➔S➔u➔g➔g➔e➔s➔t➔e➔d➔ ➔S➔t➔u➔d➔y➔ ➔P➔l➔a➔n➔
➔P➔h➔a➔s➔e➔ ➔1➔ ➔—➔ ➔F➔o➔u➔n➔d➔a➔t➔i➔o➔n➔ ➔(➔W➔e➔e➔k➔ ➔1➔)➔
➔G➔o➔ ➔t➔h➔r➔o➔u➔g➔h➔ ➔t➔h➔e➔s➔e➔ ➔f➔i➔r➔s➔t➔ ➔—➔ ➔y➔o➔u➔ ➔h➔a➔v➔e➔ ➔h➔a➔n➔d➔s➔-➔o➔n➔ ➔e➔x➔p➔e➔r➔i➔e➔n➔c➔e➔:➔
➔
➔
➔
➔
➔D➔a➔y➔ ➔1➔:➔ ➔G➔i➔t➔ ➔(➔S➔e➔c➔t➔i➔o➔n➔ ➔5➔)➔ ➔—➔ ➔y➔o➔u➔ ➔u➔s➔e➔d➔ ➔t➔h➔i➔s➔ ➔d➔a➔i➔l➔y➔
➔D➔a➔y➔ ➔2➔:➔ ➔L➔i➔n➔u➔x➔ ➔(➔S➔e➔c➔t➔i➔o➔n➔ ➔6➔)➔ ➔—➔ ➔y➔o➔u➔ ➔d➔i➔d➔ ➔s➔y➔s➔t➔e➔m➔ ➔h➔a➔r➔d➔e➔n➔i➔n➔g➔
➔D➔a➔y➔ ➔3➔:➔ ➔D➔o➔c➔k➔e➔r➔ ➔(➔S➔e➔c➔t➔i➔o➔n➔ ➔3➔)➔ ➔—➔ ➔y➔o➔u➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔i➔z➔e➔d➔ ➔a➔p➔p➔s➔
➔D➔a➔y➔ ➔4➔:➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔ ➔(➔S➔e➔c➔t➔i➔o➔n➔ ➔2➔)➔ ➔—➔ ➔y➔o➔u➔r➔ ➔k➔O➔p➔s➔ ➔p➔r➔o➔j➔e➔c➔t➔
➔D➔a➔y➔ ➔5➔:➔ ➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔ ➔(➔S➔e➔c➔t➔i➔o➔n➔ ➔8➔)➔ ➔—➔ ➔y➔o➔u➔r➔ ➔s➔t➔r➔o➔n➔g➔e➔s➔t➔ ➔p➔r➔o➔j➔e➔c➔t➔
➔D➔a➔y➔ ➔6➔-➔7➔:➔ ➔R➔e➔v➔i➔s➔e➔ ➔e➔v➔e➔r➔y➔t➔h➔i➔n➔g➔ ➔f➔r➔o➔m➔ ➔W➔e➔e➔k➔ ➔1➔
➔P➔h➔a➔s➔e➔ ➔2➔ ➔—➔ ➔T➔o➔o➔l➔s➔ ➔(➔W➔e➔e➔k➔ ➔2➔)➔
➔D➔a➔y➔ ➔8➔:➔ ➔ ➔J➔e➔n➔k➔i➔n➔s➔ ➔(➔S➔e➔c➔t➔i➔o➔n➔ ➔4➔)➔
➔D➔a➔y➔ ➔9➔:➔ ➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔(➔S➔e➔c➔t➔i➔o➔n➔ ➔7➔)➔
➔D➔a➔y➔ ➔1➔0➔:➔ ➔A➔n➔s➔i➔b➔l➔e➔ ➔(➔S➔e➔c➔t➔i➔o➔n➔ ➔9➔)➔
➔D➔a➔y➔ ➔1➔1➔:➔ ➔A➔W➔S➔ ➔(➔S➔e➔c➔t➔i➔o➔n➔ ➔1➔)➔
➔D➔a➔y➔ ➔1➔2➔:➔ ➔P➔r➔a➔c➔t➔i➔c➔e➔ ➔e➔x➔p➔l➔a➔i➔n➔i➔n➔g➔ ➔y➔o➔u➔r➔ ➔3➔ ➔p➔r➔o➔j➔e➔c➔t➔s➔ ➔o➔u➔t➔ ➔l➔o➔u➔d➔
➔D➔a➔y➔ ➔1➔3➔-➔1➔4➔:➔ ➔M➔o➔c➔k➔ ➔i➔n➔t➔e➔r➔v➔i➔e➔w➔ ➔q➔u➔e➔s➔t➔i➔o➔n➔s➔
➔P➔h➔a➔s➔e➔ ➔3➔ ➔—➔ ➔I➔n➔t➔e➔r➔v➔i➔e➔w➔ ➔P➔r➔e➔p➔ ➔(➔W➔e➔e➔k➔ ➔3➔)➔
➔D➔a➔y➔ ➔1➔5➔:➔ ➔P➔r➔a➔c➔t➔i➔c➔e➔ ➔p➔r➔o➔j➔e➔c➔t➔ ➔e➔x➔p➔l➔a➔n➔a➔t➔i➔o➔n➔s➔ ➔(➔r➔e➔c➔o➔r➔d➔ ➔y➔o➔u➔r➔s➔e➔l➔f➔)➔
➔D➔a➔y➔ ➔1➔6➔:➔ ➔S➔c➔e➔n➔a➔r➔i➔o➔-➔b➔a➔s➔e➔d➔ ➔q➔u➔e➔s➔t➔i➔o➔n➔s➔ ➔(➔A➔W➔S➔,➔ ➔K➔8➔s➔)➔
➔D➔a➔y➔ ➔1➔7➔:➔ ➔C➔o➔m➔m➔o➔n➔ ➔D➔e➔v➔O➔p➔s➔ ➔i➔n➔t➔e➔r➔v➔i➔e➔w➔ ➔p➔a➔t➔t➔e➔r➔n➔s➔
➔D➔a➔y➔ ➔1➔8➔:➔ ➔H➔R➔ ➔q➔u➔e➔s➔t➔i➔o➔n➔s➔ ➔+➔ ➔s➔a➔l➔a➔r➔y➔ ➔n➔e➔g➔o➔t➔i➔a➔t➔i➔o➔n➔
➔D➔a➔y➔ ➔1➔9➔:➔ ➔A➔p➔p➔l➔y➔ ➔f➔o➔r➔ ➔j➔o➔b➔s➔
➔D➔a➔y➔ ➔2➔0➔:➔ ➔K➔e➔e➔p➔ ➔a➔p➔p➔l➔y➔i➔n➔g➔,➔ ➔k➔e➔e➔p➔ ➔p➔r➔a➔c➔t➔i➔c➔i➔n➔g➔
➔💡➔ ➔ ➔H➔o➔w➔ ➔t➔o➔ ➔U➔s➔e➔ ➔T➔h➔i➔s➔ ➔D➔o➔c➔u➔m➔e➔n➔t➔
➔S➔t➔e➔p➔ ➔1➔:➔ ➔R➔e➔a➔d➔ ➔e➔a➔c➔h➔ ➔s➔e➔c➔t➔i➔o➔n➔ ➔o➔n➔c➔e➔ ➔(➔d➔o➔n➔'➔t➔ ➔m➔e➔m➔o➔r➔i➔z➔e➔ ➔y➔e➔t➔)➔
➔S➔t➔e➔p➔ ➔2➔:➔ ➔R➔e➔a➔d➔ ➔a➔g➔a➔i➔n➔,➔ ➔h➔i➔g➔h➔l➔i➔g➔h➔t➔ ➔c➔o➔m➔m➔a➔n➔d➔s➔ ➔y➔o➔u➔ ➔d➔o➔n➔'➔t➔ ➔k➔n➔o➔w➔
➔S➔t➔e➔p➔ ➔3➔:➔ ➔P➔r➔a➔c➔t➔i➔c➔e➔ ➔c➔o➔m➔m➔a➔n➔d➔s➔ ➔i➔n➔ ➔t➔e➔r➔m➔i➔n➔a➔l➔
➔S➔t➔e➔p➔ ➔4➔:➔ ➔T➔r➔y➔ ➔t➔o➔ ➔e➔x➔p➔l➔a➔i➔n➔ ➔e➔a➔c➔h➔ ➔c➔o➔n➔c➔e➔p➔t➔ ➔o➔u➔t➔ ➔l➔o➔u➔d➔ ➔(➔l➔i➔k➔e➔ ➔i➔n➔ ➔a➔n➔ ➔i➔n➔t➔e➔r➔v➔i➔e➔w➔)➔
➔S➔t➔e➔p➔ ➔5➔:➔ ➔F➔o➔c➔u➔s➔ ➔o➔n➔ ➔y➔o➔u➔r➔ ➔P➔R➔O➔J➔E➔C➔T➔ ➔e➔x➔p➔l➔a➔n➔a➔t➔i➔o➔n➔s➔ ➔—➔ ➔i➔n➔t➔e➔r➔v➔i➔e➔w➔e➔r➔s➔ ➔w➔i➔l➔l➔ ➔g➔o➔ ➔d➔e➔e➔p➔
➔S➔t➔e➔p➔ ➔6➔:➔ ➔G➔o➔ ➔t➔h➔r➔o➔u➔g➔h➔ ➔t➔h➔i➔s➔ ➔d➔o➔c➔u➔m➔e➔n➔t➔ ➔3➔-➔4➔ ➔t➔i➔m➔e➔s➔ ➔m➔i➔n➔i➔m➔u➔m➔
➔🎯➔ ➔ ➔I➔n➔t➔e➔r➔v➔i➔e➔w➔ ➔P➔r➔e➔p➔a➔r➔a➔t➔i➔o➔n➔ ➔T➔i➔p➔s➔
➔
➔
➔
➔
➔T➔o➔p➔ ➔5➔ ➔t➔h➔i➔n➔g➔s➔ ➔i➔n➔t➔e➔r➔v➔i➔e➔w➔e➔r➔s➔ ➔a➔s➔k➔ ➔f➔o➔r➔ ➔D➔e➔v➔O➔p➔s➔ ➔r➔o➔l➔e➔s➔:➔
➔1➔.➔ ➔"➔T➔e➔l➔l➔ ➔m➔e➔ ➔a➔b➔o➔u➔t➔ ➔y➔o➔u➔r➔ ➔p➔r➔o➔j➔e➔c➔t➔s➔"➔ ➔—➔ ➔P➔r➔a➔c➔t➔i➔c➔e➔ ➔t➔h➔i➔s➔ ➔1➔0➔ ➔t➔i➔m➔e➔s➔ ➔o➔u➔t➔ ➔l➔o➔u➔d➔
➔2➔.➔ ➔"➔W➔h➔a➔t➔ ➔h➔a➔p➔p➔e➔n➔s➔ ➔w➔h➔e➔n➔ ➔a➔ ➔P➔o➔d➔ ➔c➔r➔a➔s➔h➔e➔s➔?➔"➔ ➔—➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔ ➔t➔r➔o➔u➔b➔l➔e➔s➔h➔o➔o➔t➔i➔n➔g➔
➔3➔.➔ ➔"➔H➔o➔w➔ ➔d➔o➔e➔s➔ ➔y➔o➔u➔r➔ ➔C➔I➔/➔C➔D➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔w➔o➔r➔k➔?➔"➔ ➔—➔ ➔E➔n➔d➔ ➔t➔o➔ ➔e➔n➔d➔ ➔e➔x➔p➔l➔a➔n➔a➔t➔i➔o➔n➔
➔4➔.➔ ➔"➔W➔h➔a➔t➔ ➔i➔s➔ ➔t➔h➔e➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔c➔e➔ ➔b➔e➔t➔w➔e➔e➔n➔.➔.➔.➔"➔ ➔—➔ ➔c➔o➔m➔p➔a➔r➔i➔s➔o➔n➔ ➔q➔u➔e➔s➔t➔i➔o➔n➔s➔
➔5➔.➔ ➔"➔H➔o➔w➔ ➔w➔o➔u➔l➔d➔ ➔y➔o➔u➔ ➔h➔a➔n➔d➔l➔e➔ ➔[➔s➔c➔e➔n➔a➔r➔i➔o➔]➔?➔"➔ ➔—➔ ➔p➔r➔o➔b➔l➔e➔m➔ ➔s➔o➔l➔v➔i➔n➔g➔
➔Y➔o➔u➔r➔ ➔S➔t➔r➔o➔n➔g➔e➔s➔t➔ ➔C➔a➔r➔d➔s➔ ➔t➔o➔ ➔P➔l➔a➔y➔:➔
➔✅➔ ➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔ ➔c➔l➔u➔s➔t➔e➔r➔ ➔u➔s➔i➔n➔g➔ ➔k➔O➔p➔s➔ ➔o➔n➔ ➔A➔W➔S➔ ➔(➔r➔a➔r➔e➔ ➔e➔x➔p➔e➔r➔i➔e➔n➔c➔e➔)➔
➔✅➔ ➔ ➔M➔u➔l➔t➔i➔-➔t➔i➔e➔r➔ ➔a➔p➔p➔ ➔(➔N➔o➔d➔e➔.➔j➔s➔ ➔+➔ ➔A➔p➔a➔c➔h➔e➔ ➔+➔ ➔P➔o➔s➔t➔g➔r➔e➔S➔Q➔L➔)➔ ➔o➔n➔ ➔K➔8➔s➔
➔✅➔ ➔ ➔L➔G➔T➔M➔ ➔s➔t➔a➔c➔k➔ ➔m➔o➔n➔i➔t➔o➔r➔i➔n➔g➔ ➔(➔s➔h➔o➔w➔s➔ ➔y➔o➔u➔ ➔g➔o➔ ➔b➔e➔y➔o➔n➔d➔ ➔b➔a➔s➔i➔c➔s➔)➔
➔✅➔ ➔ ➔M➔u➔l➔t➔i➔-➔p➔o➔r➔t➔ ➔r➔e➔v➔e➔r➔s➔e➔ ➔p➔r➔o➔x➔y➔ ➔w➔i➔t➔h➔ ➔A➔p➔a➔c➔h➔e➔ ➔(➔m➔i➔d➔d➔l➔e➔w➔a➔r➔e➔ ➔k➔n➔o➔w➔l➔e➔d➔g➔e➔)➔
➔✅➔ ➔ ➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔ ➔f➔u➔l➔l➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔w➔i➔t➔h➔ ➔s➔e➔l➔f➔-➔h➔o➔s➔t➔e➔d➔ ➔a➔g➔e➔n➔t➔
➔W➔h➔a➔t➔ ➔t➔o➔ ➔s➔a➔y➔ ➔w➔h➔e➔n➔ ➔y➔o➔u➔ ➔d➔o➔n➔'➔t➔ ➔k➔n➔o➔w➔ ➔s➔o➔m➔e➔t➔h➔i➔n➔g➔:➔
➔"➔I➔ ➔h➔a➔v➔e➔n➔'➔t➔ ➔w➔o➔r➔k➔e➔d➔ ➔w➔i➔t➔h➔ ➔t➔h➔a➔t➔ ➔d➔i➔r➔e➔c➔t➔l➔y➔,➔ ➔b➔u➔t➔ ➔b➔a➔s➔e➔d➔ ➔o➔n➔ ➔m➔y➔ ➔e➔x➔p➔e➔r➔i➔e➔n➔c➔e➔ ➔w➔i➔t➔h➔ ➔[➔s➔i➔m➔i➔l➔a➔r➔ ➔t➔h➔i➔n➔g➔]➔,➔ ➔I➔ ➔u➔n➔d➔e➔r➔s➔t➔a➔n➔d➔ ➔i➔t➔ ➔w➔o➔r➔k➔s➔
➔b➔y➔.➔.➔.➔"➔
➔🚀➔ ➔ ➔Y➔o➔u➔'➔r➔e➔ ➔D➔o➔i➔n➔g➔ ➔G➔r➔e➔a➔t➔,➔ ➔A➔k➔h➔i➔l➔!➔
➔T➔h➔i➔s➔ ➔d➔o➔c➔u➔m➔e➔n➔t➔ ➔i➔s➔ ➔y➔o➔u➔r➔ ➔c➔o➔m➔p➔l➔e➔t➔e➔ ➔D➔e➔v➔O➔p➔s➔ ➔p➔r➔e➔p➔a➔r➔a➔t➔i➔o➔n➔ ➔b➔i➔b➔l➔e➔.➔
➔G➔o➔ ➔t➔h➔r➔o➔u➔g➔h➔ ➔i➔t➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔t➔i➔m➔e➔s➔,➔ ➔p➔r➔a➔c➔t➔i➔c➔e➔ ➔o➔u➔t➔ ➔l➔o➔u➔d➔,➔ ➔a➔n➔d➔ ➔y➔o➔u➔'➔l➔l➔ ➔b➔e➔ ➔r➔e➔a➔d➔y➔.➔
➔R➔e➔m➔e➔m➔b➔e➔r➔:➔ ➔C➔o➔n➔s➔i➔s➔t➔e➔n➔c➔y➔ ➔b➔e➔a➔t➔s➔ ➔i➔n➔t➔e➔n➔s➔i➔t➔y➔.➔ ➔2➔ ➔h➔o➔u➔r➔s➔ ➔e➔v➔e➔r➔y➔ ➔d➔a➔y➔ ➔b➔e➔a➔t➔s➔ ➔1➔4➔ ➔h➔o➔u➔r➔s➔ ➔o➔n➔ ➔S➔u➔n➔d➔a➔y➔.➔
➔D➔o➔c➔u➔m➔e➔n➔t➔ ➔p➔r➔e➔p➔a➔r➔e➔d➔ ➔b➔y➔ ➔C➔l➔a➔u➔d➔e➔ ➔f➔o➔r➔ ➔A➔k➔h➔i➔l➔ ➔B➔ ➔M➔ ➔—➔ ➔D➔e➔v➔O➔p➔s➔ ➔&➔ ➔C➔l➔o➔u➔d➔ ➔E➔n➔g➔i➔n➔e➔e➔r➔
➔K➔e➔e➔p➔ ➔g➔o➔i➔n➔g➔.➔ ➔Y➔o➔u➔'➔v➔e➔ ➔g➔o➔t➔ ➔t➔h➔i➔s➔!➔ ➔💪➔
➔
➔
➔
➔
➔
