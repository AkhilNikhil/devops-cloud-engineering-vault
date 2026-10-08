# 🏗️ Terraform Infrastructure as Code: The Definitive Master Engineering Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers Declarative IaC Principles, HCL Syntax, S3 Remote Backend with DynamoDB State Locking, Terraform 1.5+ Features (`import`, `moved`), AWS Provider v5.x Decoupled Resources, Modules, and Disaster Recovery.

---

## 📑 Table of Contents
- [What is Terraform & Why Do We Use It?](#1-what-is-terraform)
- [How Terraform Works (Desired State Architecture)](#2-how-terraform-works)
- [Terraform Workflow: Init, Plan, Apply, Destroy](#terraform-workflow)
- [State File Governance & S3 + DynamoDB Remote Backend](#state-file-architecture)
- [HCL Syntax & Core Blocks (Providers, Resources, Variables, Outputs)](#hcl-syntax)
- [Modern Terraform 1.5+ Features: import, moved, check](#modern-terraform-features)
- [Modular Architecture Best Practices](#modules-architecture)
- [Production Disaster Recovery & Troubleshooting](#troubleshooting-playbook)

---

➔S➔E➔C➔T➔I➔O➔N➔ ➔7➔:➔ ➔T➔E➔R➔R➔A➔F➔O➔R➔M➔ ➔—➔ ➔C➔O➔M➔P➔L➔E➔T➔E➔ ➔G➔U➔I➔D➔E➔
➔I➔n➔f➔r➔a➔s➔t➔r➔u➔c➔t➔u➔r➔e➔ ➔a➔s➔ ➔C➔o➔d➔e➔ ➔(➔I➔a➔C➔)➔ ➔t➔o➔o➔l➔ ➔b➔y➔ ➔H➔a➔s➔h➔i➔C➔o➔r➔p➔.➔ ➔W➔r➔i➔t➔e➔ ➔c➔o➔d➔e➔ ➔t➔o➔ ➔c➔r➔e➔a➔t➔e➔ ➔c➔l➔o➔u➔d➔ ➔i➔n➔f➔r➔a➔s➔t➔r➔u➔c➔t➔u➔r➔e➔.➔
➔1➔.➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔?➔
➔D➔e➔f➔i➔n➔i➔t➔i➔o➔n➔:➔
➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔i➔s➔ ➔a➔n➔ ➔o➔p➔e➔n➔-➔s➔o➔u➔r➔c➔e➔ ➔I➔n➔f➔r➔a➔s➔t➔r➔u➔c➔t➔u➔r➔e➔ ➔a➔s➔ ➔C➔o➔d➔e➔ ➔(➔I➔a➔C➔)➔ ➔t➔o➔o➔l➔ ➔b➔y➔ ➔H➔a➔s➔h➔i➔C➔o➔r➔p➔.➔ ➔I➔t➔ ➔l➔e➔t➔s➔ ➔y➔o➔u➔ ➔d➔e➔f➔i➔n➔e➔ ➔c➔l➔o➔u➔d➔
➔i➔n➔f➔r➔a➔s➔t➔r➔u➔c➔t➔u➔r➔e➔ ➔(➔E➔C➔2➔,➔ ➔V➔P➔C➔,➔ ➔S➔3➔,➔ ➔e➔t➔c➔.➔)➔ ➔i➔n➔ ➔h➔u➔m➔a➔n➔-➔r➔e➔a➔d➔a➔b➔l➔e➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔ ➔f➔i➔l➔e➔s➔ ➔a➔n➔d➔ ➔m➔a➔n➔a➔g➔e➔ ➔i➔t➔ ➔t➔h➔r➔o➔u➔g➔h➔ ➔c➔o➔d➔e➔.➔
➔W➔h➔y➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔?➔
➔B➔e➔f➔o➔r➔e➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔:➔ ➔C➔l➔i➔c➔k➔ ➔t➔h➔r➔o➔u➔g➔h➔ ➔A➔W➔S➔ ➔C➔o➔n➔s➔o➔l➔e➔ ➔m➔a➔n➔u➔a➔l➔l➔y➔ ➔t➔o➔ ➔c➔r➔e➔a➔t➔e➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔s➔.➔ ➔H➔a➔r➔d➔ ➔t➔o➔ ➔r➔e➔p➔r➔o➔d➔u➔c➔e➔,➔ ➔n➔o➔
➔v➔e➔r➔s➔i➔o➔n➔ ➔c➔o➔n➔t➔r➔o➔l➔,➔ ➔e➔r➔r➔o➔r➔-➔p➔r➔o➔n➔e➔.➔
➔W➔i➔t➔h➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔:➔ ➔W➔r➔i➔t➔e➔ ➔c➔o➔d➔e➔ ➔o➔n➔c➔e➔,➔ ➔r➔u➔n➔ ➔i➔t➔ ➔a➔n➔y➔w➔h➔e➔r➔e➔.➔ ➔V➔e➔r➔s➔i➔o➔n➔ ➔c➔o➔n➔t➔r➔o➔l➔l➔e➔d➔,➔ ➔r➔e➔p➔e➔a➔t➔a➔b➔l➔e➔,➔ ➔c➔o➔n➔s➔i➔s➔t➔e➔n➔t➔.➔
➔K➔e➔y➔ ➔P➔r➔i➔n➔c➔i➔p➔l➔e➔ ➔—➔ ➔D➔e➔s➔i➔r➔e➔d➔ ➔S➔t➔a➔t➔e➔:➔
➔Y➔o➔u➔ ➔d➔e➔c➔l➔a➔r➔e➔ ➔W➔H➔A➔T➔ ➔y➔o➔u➔ ➔w➔a➔n➔t➔ ➔(➔d➔e➔s➔i➔r➔e➔d➔ ➔s➔t➔a➔t➔e➔)➔.➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔f➔i➔g➔u➔r➔e➔s➔ ➔o➔u➔t➔ ➔H➔O➔W➔ ➔t➔o➔ ➔c➔r➔e➔a➔t➔e➔ ➔i➔t➔ ➔a➔n➔d➔ ➔e➔n➔s➔u➔r➔e➔s➔ ➔t➔h➔e➔ ➔a➔c➔t➔u➔a➔l➔ ➔s➔t➔a➔t➔e➔
➔m➔a➔t➔c➔h➔e➔s➔ ➔d➔e➔s➔i➔r➔e➔d➔ ➔s➔t➔a➔t➔e➔.➔
➔Y➔o➔u➔ ➔w➔r➔i➔t➔e➔:➔ ➔ ➔"➔I➔ ➔w➔a➔n➔t➔ ➔3➔ ➔E➔C➔2➔ ➔i➔n➔s➔t➔a➔n➔c➔e➔s➔"➔
➔T➔e➔r➔r➔a➔f➔o➔r➔m➔:➔ ➔ ➔C➔h➔e➔c➔k➔s➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔s➔t➔a➔t➔e➔ ➔→➔ ➔C➔r➔e➔a➔t➔e➔s➔ ➔w➔h➔a➔t➔'➔s➔ ➔m➔i➔s➔s➔i➔n➔g➔ ➔→➔ ➔R➔e➔p➔o➔r➔t➔s➔ ➔c➔h➔a➔n➔g➔e➔s➔
➔
➔
➔
➔
➔2➔.➔ ➔H➔o➔w➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔W➔o➔r➔k➔s➔
➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔Y➔o➔u➔ ➔(➔D➔e➔v➔e➔l➔o➔p➔e➔r➔)➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔W➔r➔i➔t➔e➔ ➔.➔t➔f➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔ ➔f➔i➔l➔e➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┬➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔▼➔
➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔C➔o➔r➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔│➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔ ➔ ➔ ➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔ ➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔ ➔S➔t➔a➔t➔e➔ ➔F➔i➔l➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔ ➔ ➔p➔l➔a➔n➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔(➔t➔e➔r➔r➔a➔f➔o➔r➔m➔.➔t➔f➔s➔t➔a➔t➔e➔)➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔ ➔a➔p➔p➔l➔y➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔t➔r➔a➔c➔k➔s➔ ➔w➔h➔a➔t➔ ➔e➔x➔i➔s➔t➔s➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔│➔
➔│➔ ➔ ➔│➔ ➔ ➔ ➔d➔e➔s➔t➔r➔o➔y➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔ ➔│➔
➔│➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┬➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┘➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔A➔P➔I➔ ➔c➔a➔l➔l➔s➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┼➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔▼➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔▼➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔▼➔
➔ ➔ ➔ ➔ ➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔ ➔ ➔ ➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔┐➔ ➔ ➔ ➔ ➔ ➔ ➔┌➔─➔─➔─➔─➔─➔─➔─➔┐➔
➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔A➔W➔S➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔A➔z➔u➔r➔e➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔G➔C➔P➔ ➔ ➔│➔
➔ ➔ ➔ ➔ ➔ ➔ ➔│➔P➔r➔o➔v➔i➔d➔e➔r➔│➔ ➔ ➔ ➔ ➔ ➔│➔P➔r➔o➔v➔i➔d➔e➔r➔│➔ ➔ ➔ ➔ ➔ ➔│➔P➔r➔o➔v➔i➔d➔e➔r➔│➔
➔ ➔ ➔ ➔ ➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔ ➔ ➔ ➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔┘➔ ➔ ➔ ➔ ➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔┘➔
➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔W➔o➔r➔k➔f➔l➔o➔w➔:➔
➔W➔r➔i➔t➔e➔ ➔(➔.➔t➔f➔ ➔f➔i➔l➔e➔s➔)➔ ➔→➔ ➔I➔n➔i➔t➔ ➔→➔ ➔P➔l➔a➔n➔ ➔→➔ ➔A➔p➔p➔l➔y➔ ➔→➔ ➔D➔e➔s➔t➔r➔o➔y➔
➔1➔.➔ ➔W➔r➔i➔t➔e➔ ➔—➔ ➔c➔r➔e➔a➔t➔e➔ ➔.➔t➔f➔ ➔ ➔f➔i➔l➔e➔s➔ ➔d➔e➔c➔l➔a➔r➔i➔n➔g➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔s➔
➔2➔.➔ ➔I➔n➔i➔t➔ ➔—➔ ➔d➔o➔w➔n➔l➔o➔a➔d➔ ➔p➔r➔o➔v➔i➔d➔e➔r➔ ➔p➔l➔u➔g➔i➔n➔s➔
➔3➔.➔ ➔P➔l➔a➔n➔ ➔—➔ ➔p➔r➔e➔v➔i➔e➔w➔ ➔w➔h➔a➔t➔ ➔w➔i➔l➔l➔ ➔b➔e➔ ➔c➔r➔e➔a➔t➔e➔d➔/➔c➔h➔a➔n➔g➔e➔d➔/➔d➔e➔s➔t➔r➔o➔y➔e➔d➔
➔4➔.➔ ➔A➔p➔p➔l➔y➔ ➔—➔ ➔a➔c➔t➔u➔a➔l➔l➔y➔ ➔c➔r➔e➔a➔t➔e➔ ➔t➔h➔e➔ ➔i➔n➔f➔r➔a➔s➔t➔r➔u➔c➔t➔u➔r➔e➔
➔5➔.➔ ➔D➔e➔s➔t➔r➔o➔y➔ ➔—➔ ➔t➔e➔a➔r➔ ➔d➔o➔w➔n➔ ➔e➔v➔e➔r➔y➔t➔h➔i➔n➔g➔
➔3➔.➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔F➔i➔l➔e➔s➔
➔F➔i➔l➔e➔ ➔P➔u➔r➔p➔o➔s➔e➔
➔
➔
➔
➔
➔m➔a➔i➔n➔.➔t➔f➔ ➔M➔a➔i➔n➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔d➔e➔f➔i➔n➔i➔t➔i➔o➔n➔s➔
➔v➔a➔r➔i➔a➔b➔l➔e➔s➔.➔t➔f➔ ➔I➔n➔p➔u➔t➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔ ➔d➔e➔c➔l➔a➔r➔a➔t➔i➔o➔n➔s➔
➔o➔u➔t➔p➔u➔t➔s➔.➔t➔f➔ ➔O➔u➔t➔p➔u➔t➔ ➔v➔a➔l➔u➔e➔ ➔d➔e➔f➔i➔n➔i➔t➔i➔o➔n➔s➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔.➔t➔f➔v➔a➔r➔s➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔ ➔v➔a➔l➔u➔e➔s➔
➔p➔r➔o➔v➔i➔d➔e➔r➔s➔.➔t➔f➔ ➔P➔r➔o➔v➔i➔d➔e➔r➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔
➔b➔a➔c➔k➔e➔n➔d➔.➔t➔f➔ ➔R➔e➔m➔o➔t➔e➔ ➔s➔t➔a➔t➔e➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔.➔t➔f➔s➔t➔a➔t➔e➔ ➔S➔t➔a➔t➔e➔ ➔f➔i➔l➔e➔ ➔(➔a➔u➔t➔o➔-➔g➔e➔n➔e➔r➔a➔t➔e➔d➔,➔ ➔d➔o➔n➔'➔t➔ ➔e➔d➔i➔t➔)➔
➔.➔t➔e➔r➔r➔a➔f➔o➔r➔m➔/➔ ➔D➔o➔w➔n➔l➔o➔a➔d➔e➔d➔ ➔p➔r➔o➔v➔i➔d➔e➔r➔s➔ ➔(➔a➔u➔t➔o➔-➔g➔e➔n➔e➔r➔a➔t➔e➔d➔)➔
➔.➔t➔e➔r➔r➔a➔f➔o➔r➔m➔.➔l➔o➔c➔k➔.➔h➔c➔l➔ ➔P➔r➔o➔v➔i➔d➔e➔r➔ ➔v➔e➔r➔s➔i➔o➔n➔ ➔l➔o➔c➔k➔ ➔f➔i➔l➔e➔
➔4➔.➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔
➔#➔ ➔─➔─➔ ➔S➔E➔T➔U➔P➔ ➔─➔─➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔i➔n➔i➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔i➔n➔i➔t➔i➔a➔l➔i➔z➔e➔ ➔—➔ ➔d➔o➔w➔n➔l➔o➔a➔d➔ ➔p➔r➔o➔v➔i➔d➔e➔r➔s➔,➔ ➔s➔e➔t➔u➔p➔ ➔b➔a➔c➔k➔e➔n➔d➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔i➔n➔i➔t➔ ➔-➔u➔p➔g➔r➔a➔d➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔u➔p➔g➔r➔a➔d➔e➔ ➔p➔r➔o➔v➔i➔d➔e➔r➔s➔ ➔t➔o➔ ➔l➔a➔t➔e➔s➔t➔ ➔v➔e➔r➔s➔i➔o➔n➔s➔
➔#➔ ➔─➔─➔ ➔P➔R➔E➔V➔I➔E➔W➔ ➔─➔─➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔p➔l➔a➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔w➔h➔a➔t➔ ➔w➔i➔l➔l➔ ➔b➔e➔ ➔c➔r➔e➔a➔t➔e➔d➔/➔c➔h➔a➔n➔g➔e➔d➔/➔d➔e➔s➔t➔r➔o➔y➔e➔d➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔p➔l➔a➔n➔ ➔-➔o➔u➔t➔=➔t➔f➔p➔l➔a➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔a➔v➔e➔ ➔p➔l➔a➔n➔ ➔t➔o➔ ➔f➔i➔l➔e➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔p➔l➔a➔n➔ ➔-➔v➔a➔r➔=➔"➔e➔n➔v➔=➔p➔r➔o➔d➔"➔ ➔ ➔ ➔ ➔#➔ ➔p➔a➔s➔s➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔ ➔o➔n➔ ➔c➔o➔m➔m➔a➔n➔d➔ ➔l➔i➔n➔e➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔p➔l➔a➔n➔ ➔-➔d➔e➔s➔t➔r➔o➔y➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔r➔e➔v➔i➔e➔w➔ ➔d➔e➔s➔t➔r➔o➔y➔
➔#➔ ➔─➔─➔ ➔A➔P➔P➔L➔Y➔ ➔─➔─➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔a➔p➔p➔l➔y➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔p➔p➔l➔y➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔(➔a➔s➔k➔s➔ ➔f➔o➔r➔ ➔c➔o➔n➔f➔i➔r➔m➔a➔t➔i➔o➔n➔)➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔a➔p➔p➔l➔y➔ ➔-➔a➔u➔t➔o➔-➔a➔p➔p➔r➔o➔v➔e➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔p➔p➔l➔y➔ ➔w➔i➔t➔h➔o➔u➔t➔ ➔c➔o➔n➔f➔i➔r➔m➔a➔t➔i➔o➔n➔ ➔(➔C➔I➔/➔C➔D➔)➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔a➔p➔p➔l➔y➔ ➔t➔f➔p➔l➔a➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔p➔p➔l➔y➔ ➔s➔a➔v➔e➔d➔ ➔p➔l➔a➔n➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔a➔p➔p➔l➔y➔ ➔-➔v➔a➔r➔=➔"➔e➔n➔v➔=➔p➔r➔o➔d➔"➔ ➔ ➔ ➔#➔ ➔a➔p➔p➔l➔y➔ ➔w➔i➔t➔h➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔
➔#➔ ➔─➔─➔ ➔D➔E➔S➔T➔R➔O➔Y➔ ➔─➔─➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔d➔e➔s➔t➔r➔o➔y➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔s➔t➔r➔o➔y➔ ➔a➔l➔l➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔s➔ ➔(➔a➔s➔k➔s➔ ➔c➔o➔n➔f➔i➔r➔m➔a➔t➔i➔o➔n➔)➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔d➔e➔s➔t➔r➔o➔y➔ ➔-➔a➔u➔t➔o➔-➔a➔p➔p➔r➔o➔v➔e➔ ➔ ➔ ➔#➔ ➔d➔e➔s➔t➔r➔o➔y➔ ➔w➔i➔t➔h➔o➔u➔t➔ ➔c➔o➔n➔f➔i➔r➔m➔a➔t➔i➔o➔n➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔d➔e➔s➔t➔r➔o➔y➔ ➔-➔t➔a➔r➔g➔e➔t➔=➔a➔w➔s➔_➔i➔n➔s➔t➔a➔n➔c➔e➔.➔w➔e➔b➔ ➔ ➔#➔ ➔d➔e➔s➔t➔r➔o➔y➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔
➔#➔ ➔─➔─➔ ➔S➔T➔A➔T➔E➔ ➔─➔─➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔s➔h➔o➔w➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔s➔t➔a➔t➔e➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔s➔t➔a➔t➔e➔ ➔l➔i➔s➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔a➔l➔l➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔s➔ ➔i➔n➔ ➔s➔t➔a➔t➔e➔
➔
➔
➔
➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔s➔t➔a➔t➔e➔ ➔s➔h➔o➔w➔ ➔a➔w➔s➔_➔i➔n➔s➔t➔a➔n➔c➔e➔.➔w➔e➔b➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔s➔t➔a➔t➔e➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔s➔t➔a➔t➔e➔ ➔r➔m➔ ➔a➔w➔s➔_➔i➔n➔s➔t➔a➔n➔c➔e➔.➔w➔e➔b➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔f➔r➔o➔m➔ ➔s➔t➔a➔t➔e➔ ➔(➔w➔i➔t➔h➔o➔u➔t➔ ➔d➔e➔s➔t➔r➔o➔y➔i➔n➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔s➔t➔a➔t➔e➔ ➔m➔v➔ ➔a➔w➔s➔_➔i➔n➔s➔t➔a➔n➔c➔e➔.➔o➔l➔d➔ ➔a➔w➔s➔_➔i➔n➔s➔t➔a➔n➔c➔e➔.➔n➔e➔w➔ ➔ ➔#➔ ➔r➔e➔n➔a➔m➔e➔ ➔i➔n➔ ➔s➔t➔a➔t➔e➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔r➔e➔f➔r➔e➔s➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔y➔n➔c➔ ➔s➔t➔a➔t➔e➔ ➔w➔i➔t➔h➔ ➔r➔e➔a➔l➔ ➔i➔n➔f➔r➔a➔s➔t➔r➔u➔c➔t➔u➔r➔e➔
➔#➔ ➔─➔─➔ ➔I➔M➔P➔O➔R➔T➔ ➔─➔─➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔i➔m➔p➔o➔r➔t➔ ➔a➔w➔s➔_➔i➔n➔s➔t➔a➔n➔c➔e➔.➔w➔e➔b➔ ➔i➔-➔1➔2➔3➔4➔5➔6➔7➔8➔9➔0➔ ➔ ➔#➔ ➔i➔m➔p➔o➔r➔t➔ ➔e➔x➔i➔s➔t➔i➔n➔g➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔i➔n➔t➔o➔ ➔s➔t➔a➔t➔e➔
➔#➔ ➔─➔─➔ ➔V➔A➔L➔I➔D➔A➔T➔E➔ ➔&➔ ➔F➔O➔R➔M➔A➔T➔ ➔─➔─➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔v➔a➔l➔i➔d➔a➔t➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔e➔c➔k➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔ ➔s➔y➔n➔t➔a➔x➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔f➔m➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔r➔m➔a➔t➔ ➔.➔t➔f➔ ➔f➔i➔l➔e➔s➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔f➔m➔t➔ ➔-➔r➔e➔c➔u➔r➔s➔i➔v➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔r➔m➔a➔t➔ ➔a➔l➔l➔ ➔f➔i➔l➔e➔s➔ ➔r➔e➔c➔u➔r➔s➔i➔v➔e➔l➔y➔
➔#➔ ➔─➔─➔ ➔W➔O➔R➔K➔S➔P➔A➔C➔E➔ ➔─➔─➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔ ➔l➔i➔s➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔s➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔ ➔n➔e➔w➔ ➔d➔e➔v➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔n➔e➔w➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔ ➔s➔e➔l➔e➔c➔t➔ ➔p➔r➔o➔d➔ ➔ ➔ ➔#➔ ➔s➔w➔i➔t➔c➔h➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔ ➔s➔h➔o➔w➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔ ➔d➔e➔l➔e➔t➔e➔ ➔d➔e➔v➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔
➔#➔ ➔─➔─➔ ➔O➔U➔T➔P➔U➔T➔ ➔─➔─➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔o➔u➔t➔p➔u➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔a➔l➔l➔ ➔o➔u➔t➔p➔u➔t➔s➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔o➔u➔t➔p➔u➔t➔ ➔v➔p➔c➔_➔i➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔o➔u➔t➔p➔u➔t➔
➔#➔ ➔─➔─➔ ➔G➔R➔A➔P➔H➔ ➔─➔─➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔g➔r➔a➔p➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔g➔e➔n➔e➔r➔a➔t➔e➔ ➔d➔e➔p➔e➔n➔d➔e➔n➔c➔y➔ ➔g➔r➔a➔p➔h➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔g➔r➔a➔p➔h➔ ➔|➔ ➔d➔o➔t➔ ➔-➔T➔p➔n➔g➔ ➔>➔ ➔g➔r➔a➔p➔h➔.➔p➔n➔g➔ ➔ ➔#➔ ➔v➔i➔s➔u➔a➔l➔i➔z➔e➔ ➔a➔s➔ ➔i➔m➔a➔g➔e➔
➔5➔.➔ ➔P➔r➔o➔v➔i➔d➔e➔r➔ ➔C➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔
➔#➔ ➔p➔r➔o➔v➔i➔d➔e➔r➔s➔.➔t➔f➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔{➔
➔ ➔ ➔r➔e➔q➔u➔i➔r➔e➔d➔_➔v➔e➔r➔s➔i➔o➔n➔ ➔=➔ ➔"➔>➔=➔ ➔1➔.➔0➔"➔
➔ ➔ ➔r➔e➔q➔u➔i➔r➔e➔d➔_➔p➔r➔o➔v➔i➔d➔e➔r➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔a➔w➔s➔ ➔=➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔s➔o➔u➔r➔c➔e➔ ➔ ➔=➔ ➔"➔h➔a➔s➔h➔i➔c➔o➔r➔p➔/➔a➔w➔s➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔v➔e➔r➔s➔i➔o➔n➔ ➔=➔ ➔"➔~➔>➔ ➔5➔.➔0➔"➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔n➔y➔ ➔5➔.➔x➔ ➔v➔e➔r➔s➔i➔o➔n➔
➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔a➔z➔u➔r➔e➔r➔m➔ ➔=➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔s➔o➔u➔r➔c➔e➔ ➔ ➔=➔ ➔"➔h➔a➔s➔h➔i➔c➔o➔r➔p➔/➔a➔z➔u➔r➔e➔r➔m➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔v➔e➔r➔s➔i➔o➔n➔ ➔=➔ ➔"➔~➔>➔ ➔3➔.➔0➔"➔
➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔}➔
➔
➔
➔
➔
➔ ➔ ➔#➔ ➔R➔e➔m➔o➔t➔e➔ ➔s➔t➔a➔t➔e➔ ➔i➔n➔ ➔S➔3➔ ➔(➔f➔o➔r➔ ➔t➔e➔a➔m➔s➔)➔
➔ ➔ ➔b➔a➔c➔k➔e➔n➔d➔ ➔"➔s➔3➔"➔ ➔{➔
➔ ➔ ➔ ➔ ➔b➔u➔c➔k➔e➔t➔ ➔=➔ ➔"➔m➔y➔-➔t➔e➔r➔r➔a➔f➔o➔r➔m➔-➔s➔t➔a➔t➔e➔"➔
➔ ➔ ➔ ➔ ➔k➔e➔y➔ ➔ ➔ ➔ ➔=➔ ➔"➔p➔r➔o➔d➔/➔t➔e➔r➔r➔a➔f➔o➔r➔m➔.➔t➔f➔s➔t➔a➔t➔e➔"➔
➔ ➔ ➔ ➔ ➔r➔e➔g➔i➔o➔n➔ ➔=➔ ➔"➔u➔s➔-➔e➔a➔s➔t➔-➔1➔"➔
➔ ➔ ➔}➔
➔}➔
➔#➔ ➔A➔W➔S➔ ➔P➔r➔o➔v➔i➔d➔e➔r➔
➔p➔r➔o➔v➔i➔d➔e➔r➔ ➔"➔a➔w➔s➔"➔ ➔{➔
➔ ➔ ➔r➔e➔g➔i➔o➔n➔ ➔ ➔ ➔ ➔ ➔=➔ ➔"➔u➔s➔-➔e➔a➔s➔t➔-➔1➔"➔
➔ ➔ ➔a➔c➔c➔e➔s➔s➔_➔k➔e➔y➔ ➔=➔ ➔v➔a➔r➔.➔a➔w➔s➔_➔a➔c➔c➔e➔s➔s➔_➔k➔e➔y➔ ➔ ➔ ➔ ➔#➔ ➔f➔r➔o➔m➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔
➔ ➔ ➔s➔e➔c➔r➔e➔t➔_➔k➔e➔y➔ ➔=➔ ➔v➔a➔r➔.➔a➔w➔s➔_➔s➔e➔c➔r➔e➔t➔_➔k➔e➔y➔ ➔ ➔ ➔ ➔#➔ ➔f➔r➔o➔m➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔
➔ ➔ ➔#➔ ➔B➔e➔t➔t➔e➔r➔:➔ ➔u➔s➔e➔ ➔A➔W➔S➔ ➔C➔L➔I➔ ➔p➔r➔o➔f➔i➔l➔e➔ ➔o➔r➔ ➔I➔A➔M➔ ➔r➔o➔l➔e➔
➔ ➔ ➔#➔ ➔p➔r➔o➔f➔i➔l➔e➔ ➔=➔ ➔"➔d➔e➔f➔a➔u➔l➔t➔"➔
➔}➔
➔6➔.➔ ➔R➔e➔s➔o➔u➔r➔c➔e➔ ➔B➔l➔o➔c➔k➔ ➔—➔ ➔H➔o➔w➔ ➔t➔o➔ ➔C➔r➔e➔a➔t➔e➔ ➔I➔n➔f➔r➔a➔s➔t➔r➔u➔c➔t➔u➔r➔e➔
➔S➔y➔n➔t➔a➔x➔:➔
➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔"➔p➔r➔o➔v➔i➔d➔e➔r➔_➔r➔e➔s➔o➔u➔r➔c➔e➔t➔y➔p➔e➔"➔ ➔"➔l➔o➔c➔a➔l➔_➔n➔a➔m➔e➔"➔ ➔{➔
➔ ➔ ➔a➔r➔g➔u➔m➔e➔n➔t➔1➔ ➔=➔ ➔v➔a➔l➔u➔e➔1➔
➔ ➔ ➔a➔r➔g➔u➔m➔e➔n➔t➔2➔ ➔=➔ ➔v➔a➔l➔u➔e➔2➔
➔}➔
➔E➔x➔a➔m➔p➔l➔e➔s➔:➔
➔#➔ ➔E➔C➔2➔ ➔I➔n➔s➔t➔a➔n➔c➔e➔
➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔"➔a➔w➔s➔_➔i➔n➔s➔t➔a➔n➔c➔e➔"➔ ➔"➔w➔e➔b➔"➔ ➔{➔
➔ ➔ ➔a➔m➔i➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔"➔a➔m➔i➔-➔0➔c➔5➔5➔b➔1➔5➔9➔c➔b➔f➔a➔f➔e➔1➔f➔0➔"➔
➔ ➔ ➔i➔n➔s➔t➔a➔n➔c➔e➔_➔t➔y➔p➔e➔ ➔=➔ ➔"➔t➔2➔.➔m➔i➔c➔r➔o➔"➔
➔ ➔ ➔k➔e➔y➔_➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔"➔m➔y➔-➔k➔e➔y➔"➔
➔ ➔ ➔t➔a➔g➔s➔ ➔=➔ ➔{➔
➔ ➔ ➔ ➔ ➔N➔a➔m➔e➔ ➔=➔ ➔"➔W➔e➔b➔S➔e➔r➔v➔e➔r➔"➔
➔ ➔ ➔ ➔ ➔E➔n➔v➔ ➔ ➔=➔ ➔"➔P➔r➔o➔d➔u➔c➔t➔i➔o➔n➔"➔
➔ ➔ ➔}➔
➔}➔
➔#➔ ➔S➔3➔ ➔B➔u➔c➔k➔e➔t➔
➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔"➔a➔w➔s➔_➔s➔3➔_➔b➔u➔c➔k➔e➔t➔"➔ ➔"➔m➔y➔b➔u➔c➔k➔e➔t➔"➔ ➔{➔
➔
➔
➔
➔
➔ ➔ ➔b➔u➔c➔k➔e➔t➔ ➔=➔ ➔"➔a➔k➔h➔i➔l➔-➔m➔y➔-➔b➔u➔c➔k➔e➔t➔-➔2➔0➔2➔4➔"➔
➔ ➔ ➔t➔a➔g➔s➔ ➔=➔ ➔{➔
➔ ➔ ➔ ➔ ➔N➔a➔m➔e➔ ➔=➔ ➔"➔M➔y➔B➔u➔c➔k➔e➔t➔"➔
➔ ➔ ➔}➔
➔}➔
➔#➔ ➔S➔e➔c➔u➔r➔i➔t➔y➔ ➔G➔r➔o➔u➔p➔
➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔"➔a➔w➔s➔_➔s➔e➔c➔u➔r➔i➔t➔y➔_➔g➔r➔o➔u➔p➔"➔ ➔"➔w➔e➔b➔_➔s➔g➔"➔ ➔{➔
➔ ➔ ➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔"➔w➔e➔b➔-➔s➔g➔"➔
➔ ➔ ➔d➔e➔s➔c➔r➔i➔p➔t➔i➔o➔n➔ ➔=➔ ➔"➔A➔l➔l➔o➔w➔ ➔H➔T➔T➔P➔ ➔a➔n➔d➔ ➔S➔S➔H➔"➔
➔ ➔ ➔v➔p➔c➔_➔i➔d➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔a➔w➔s➔_➔v➔p➔c➔.➔m➔a➔i➔n➔.➔i➔d➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔f➔e➔r➔e➔n➔c➔e➔ ➔a➔n➔o➔t➔h➔e➔r➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔
➔ ➔ ➔i➔n➔g➔r➔e➔s➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔f➔r➔o➔m➔_➔p➔o➔r➔t➔ ➔ ➔ ➔=➔ ➔8➔0➔
➔ ➔ ➔ ➔ ➔t➔o➔_➔p➔o➔r➔t➔ ➔ ➔ ➔ ➔ ➔=➔ ➔8➔0➔
➔ ➔ ➔ ➔ ➔p➔r➔o➔t➔o➔c➔o➔l➔ ➔ ➔ ➔ ➔=➔ ➔"➔t➔c➔p➔"➔
➔ ➔ ➔ ➔ ➔c➔i➔d➔r➔_➔b➔l➔o➔c➔k➔s➔ ➔=➔ ➔[➔"➔0➔.➔0➔.➔0➔.➔0➔/➔0➔"➔]➔
➔ ➔ ➔}➔
➔ ➔ ➔i➔n➔g➔r➔e➔s➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔f➔r➔o➔m➔_➔p➔o➔r➔t➔ ➔ ➔ ➔=➔ ➔2➔2➔
➔ ➔ ➔ ➔ ➔t➔o➔_➔p➔o➔r➔t➔ ➔ ➔ ➔ ➔ ➔=➔ ➔2➔2➔
➔ ➔ ➔ ➔ ➔p➔r➔o➔t➔o➔c➔o➔l➔ ➔ ➔ ➔ ➔=➔ ➔"➔t➔c➔p➔"➔
➔ ➔ ➔ ➔ ➔c➔i➔d➔r➔_➔b➔l➔o➔c➔k➔s➔ ➔=➔ ➔[➔"➔0➔.➔0➔.➔0➔.➔0➔/➔0➔"➔]➔
➔ ➔ ➔}➔
➔ ➔ ➔e➔g➔r➔e➔s➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔f➔r➔o➔m➔_➔p➔o➔r➔t➔ ➔ ➔ ➔=➔ ➔0➔
➔ ➔ ➔ ➔ ➔t➔o➔_➔p➔o➔r➔t➔ ➔ ➔ ➔ ➔ ➔=➔ ➔0➔
➔ ➔ ➔ ➔ ➔p➔r➔o➔t➔o➔c➔o➔l➔ ➔ ➔ ➔ ➔=➔ ➔"➔-➔1➔"➔
➔ ➔ ➔ ➔ ➔c➔i➔d➔r➔_➔b➔l➔o➔c➔k➔s➔ ➔=➔ ➔[➔"➔0➔.➔0➔.➔0➔.➔0➔/➔0➔"➔]➔
➔ ➔ ➔}➔
➔}➔
➔7➔.➔ ➔C➔r➔e➔a➔t➔i➔n➔g➔ ➔a➔ ➔V➔P➔C➔ ➔—➔ ➔C➔o➔m➔p➔l➔e➔t➔e➔ ➔E➔x➔a➔m➔p➔l➔e➔
➔#➔ ➔m➔a➔i➔n➔.➔t➔f➔ ➔—➔ ➔C➔o➔m➔p➔l➔e➔t➔e➔ ➔V➔P➔C➔ ➔S➔e➔t➔u➔p➔
➔#➔ ➔─➔─➔ ➔V➔P➔C➔ ➔─➔─➔
➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔"➔a➔w➔s➔_➔v➔p➔c➔"➔ ➔"➔m➔a➔i➔n➔"➔ ➔{➔
➔ ➔ ➔c➔i➔d➔r➔_➔b➔l➔o➔c➔k➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔"➔1➔0➔.➔0➔.➔0➔.➔0➔/➔1➔6➔"➔
➔ ➔ ➔e➔n➔a➔b➔l➔e➔_➔d➔n➔s➔_➔h➔o➔s➔t➔n➔a➔m➔e➔s➔ ➔=➔ ➔t➔r➔u➔e➔
➔ ➔ ➔e➔n➔a➔b➔l➔e➔_➔d➔n➔s➔_➔s➔u➔p➔p➔o➔r➔t➔ ➔ ➔ ➔=➔ ➔t➔r➔u➔e➔
➔
➔
➔
➔
➔ ➔ ➔t➔a➔g➔s➔ ➔=➔ ➔{➔
➔ ➔ ➔ ➔ ➔N➔a➔m➔e➔ ➔=➔ ➔"➔m➔a➔i➔n➔-➔v➔p➔c➔"➔
➔ ➔ ➔}➔
➔}➔
➔#➔ ➔─➔─➔ ➔P➔U➔B➔L➔I➔C➔ ➔S➔U➔B➔N➔E➔T➔ ➔─➔─➔
➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔"➔a➔w➔s➔_➔s➔u➔b➔n➔e➔t➔"➔ ➔"➔p➔u➔b➔l➔i➔c➔"➔ ➔{➔
➔ ➔ ➔v➔p➔c➔_➔i➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔a➔w➔s➔_➔v➔p➔c➔.➔m➔a➔i➔n➔.➔i➔d➔
➔ ➔ ➔c➔i➔d➔r➔_➔b➔l➔o➔c➔k➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔"➔1➔0➔.➔0➔.➔1➔.➔0➔/➔2➔4➔"➔
➔ ➔ ➔a➔v➔a➔i➔l➔a➔b➔i➔l➔i➔t➔y➔_➔z➔o➔n➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔"➔u➔s➔-➔e➔a➔s➔t➔-➔1➔a➔"➔
➔ ➔ ➔m➔a➔p➔_➔p➔u➔b➔l➔i➔c➔_➔i➔p➔_➔o➔n➔_➔l➔a➔u➔n➔c➔h➔ ➔=➔ ➔t➔r➔u➔e➔ ➔ ➔ ➔ ➔#➔ ➔a➔u➔t➔o➔-➔a➔s➔s➔i➔g➔n➔ ➔p➔u➔b➔l➔i➔c➔ ➔I➔P➔
➔ ➔ ➔t➔a➔g➔s➔ ➔=➔ ➔{➔
➔ ➔ ➔ ➔ ➔N➔a➔m➔e➔ ➔=➔ ➔"➔p➔u➔b➔l➔i➔c➔-➔s➔u➔b➔n➔e➔t➔"➔
➔ ➔ ➔}➔
➔}➔
➔#➔ ➔─➔─➔ ➔P➔R➔I➔V➔A➔T➔E➔ ➔S➔U➔B➔N➔E➔T➔ ➔─➔─➔
➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔"➔a➔w➔s➔_➔s➔u➔b➔n➔e➔t➔"➔ ➔"➔p➔r➔i➔v➔a➔t➔e➔"➔ ➔{➔
➔ ➔ ➔v➔p➔c➔_➔i➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔a➔w➔s➔_➔v➔p➔c➔.➔m➔a➔i➔n➔.➔i➔d➔
➔ ➔ ➔c➔i➔d➔r➔_➔b➔l➔o➔c➔k➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔"➔1➔0➔.➔0➔.➔2➔.➔0➔/➔2➔4➔"➔
➔ ➔ ➔a➔v➔a➔i➔l➔a➔b➔i➔l➔i➔t➔y➔_➔z➔o➔n➔e➔ ➔=➔ ➔"➔u➔s➔-➔e➔a➔s➔t➔-➔1➔b➔"➔
➔ ➔ ➔t➔a➔g➔s➔ ➔=➔ ➔{➔
➔ ➔ ➔ ➔ ➔N➔a➔m➔e➔ ➔=➔ ➔"➔p➔r➔i➔v➔a➔t➔e➔-➔s➔u➔b➔n➔e➔t➔"➔
➔ ➔ ➔}➔
➔}➔
➔#➔ ➔─➔─➔ ➔I➔N➔T➔E➔R➔N➔E➔T➔ ➔G➔A➔T➔E➔W➔A➔Y➔ ➔─➔─➔
➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔"➔a➔w➔s➔_➔i➔n➔t➔e➔r➔n➔e➔t➔_➔g➔a➔t➔e➔w➔a➔y➔"➔ ➔"➔i➔g➔w➔"➔ ➔{➔
➔ ➔ ➔v➔p➔c➔_➔i➔d➔ ➔=➔ ➔a➔w➔s➔_➔v➔p➔c➔.➔m➔a➔i➔n➔.➔i➔d➔
➔ ➔ ➔t➔a➔g➔s➔ ➔=➔ ➔{➔
➔ ➔ ➔ ➔ ➔N➔a➔m➔e➔ ➔=➔ ➔"➔m➔a➔i➔n➔-➔i➔g➔w➔"➔
➔ ➔ ➔}➔
➔}➔
➔#➔ ➔─➔─➔ ➔R➔O➔U➔T➔E➔ ➔T➔A➔B➔L➔E➔ ➔(➔f➔o➔r➔ ➔p➔u➔b➔l➔i➔c➔ ➔s➔u➔b➔n➔e➔t➔)➔ ➔─➔─➔
➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔"➔a➔w➔s➔_➔r➔o➔u➔t➔e➔_➔t➔a➔b➔l➔e➔"➔ ➔"➔p➔u➔b➔l➔i➔c➔_➔r➔t➔"➔ ➔{➔
➔ ➔ ➔v➔p➔c➔_➔i➔d➔ ➔=➔ ➔a➔w➔s➔_➔v➔p➔c➔.➔m➔a➔i➔n➔.➔i➔d➔
➔ ➔ ➔r➔o➔u➔t➔e➔ ➔{➔
➔ ➔ ➔ ➔ ➔c➔i➔d➔r➔_➔b➔l➔o➔c➔k➔ ➔=➔ ➔"➔0➔.➔0➔.➔0➔.➔0➔/➔0➔"➔
➔ ➔ ➔ ➔ ➔g➔a➔t➔e➔w➔a➔y➔_➔i➔d➔ ➔=➔ ➔a➔w➔s➔_➔i➔n➔t➔e➔r➔n➔e➔t➔_➔g➔a➔t➔e➔w➔a➔y➔.➔i➔g➔w➔.➔i➔d➔
➔ ➔ ➔}➔
➔ ➔ ➔t➔a➔g➔s➔ ➔=➔ ➔{➔
➔ ➔ ➔ ➔ ➔N➔a➔m➔e➔ ➔=➔ ➔"➔p➔u➔b➔l➔i➔c➔-➔r➔t➔"➔
➔
➔
➔
➔
➔ ➔ ➔}➔
➔}➔
➔#➔ ➔─➔─➔ ➔A➔S➔S➔O➔C➔I➔A➔T➔E➔ ➔R➔O➔U➔T➔E➔ ➔T➔A➔B➔L➔E➔ ➔W➔I➔T➔H➔ ➔P➔U➔B➔L➔I➔C➔ ➔S➔U➔B➔N➔E➔T➔ ➔─➔─➔
➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔"➔a➔w➔s➔_➔r➔o➔u➔t➔e➔_➔t➔a➔b➔l➔e➔_➔a➔s➔s➔o➔c➔i➔a➔t➔i➔o➔n➔"➔ ➔"➔p➔u➔b➔l➔i➔c➔_➔r➔t➔a➔"➔ ➔{➔
➔ ➔ ➔s➔u➔b➔n➔e➔t➔_➔i➔d➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔a➔w➔s➔_➔s➔u➔b➔n➔e➔t➔.➔p➔u➔b➔l➔i➔c➔.➔i➔d➔
➔ ➔ ➔r➔o➔u➔t➔e➔_➔t➔a➔b➔l➔e➔_➔i➔d➔ ➔=➔ ➔a➔w➔s➔_➔r➔o➔u➔t➔e➔_➔t➔a➔b➔l➔e➔.➔p➔u➔b➔l➔i➔c➔_➔r➔t➔.➔i➔d➔
➔}➔
➔#➔ ➔─➔─➔ ➔S➔E➔C➔U➔R➔I➔T➔Y➔ ➔G➔R➔O➔U➔P➔ ➔─➔─➔
➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔"➔a➔w➔s➔_➔s➔e➔c➔u➔r➔i➔t➔y➔_➔g➔r➔o➔u➔p➔"➔ ➔"➔w➔e➔b➔_➔s➔g➔"➔ ➔{➔
➔ ➔ ➔n➔a➔m➔e➔ ➔ ➔ ➔=➔ ➔"➔w➔e➔b➔-➔s➔g➔"➔
➔ ➔ ➔v➔p➔c➔_➔i➔d➔ ➔=➔ ➔a➔w➔s➔_➔v➔p➔c➔.➔m➔a➔i➔n➔.➔i➔d➔
➔ ➔ ➔i➔n➔g➔r➔e➔s➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔f➔r➔o➔m➔_➔p➔o➔r➔t➔ ➔ ➔ ➔=➔ ➔8➔0➔
➔ ➔ ➔ ➔ ➔t➔o➔_➔p➔o➔r➔t➔ ➔ ➔ ➔ ➔ ➔=➔ ➔8➔0➔
➔ ➔ ➔ ➔ ➔p➔r➔o➔t➔o➔c➔o➔l➔ ➔ ➔ ➔ ➔=➔ ➔"➔t➔c➔p➔"➔
➔ ➔ ➔ ➔ ➔c➔i➔d➔r➔_➔b➔l➔o➔c➔k➔s➔ ➔=➔ ➔[➔"➔0➔.➔0➔.➔0➔.➔0➔/➔0➔"➔]➔
➔ ➔ ➔}➔
➔ ➔ ➔i➔n➔g➔r➔e➔s➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔f➔r➔o➔m➔_➔p➔o➔r➔t➔ ➔ ➔ ➔=➔ ➔2➔2➔
➔ ➔ ➔ ➔ ➔t➔o➔_➔p➔o➔r➔t➔ ➔ ➔ ➔ ➔ ➔=➔ ➔2➔2➔
➔ ➔ ➔ ➔ ➔p➔r➔o➔t➔o➔c➔o➔l➔ ➔ ➔ ➔ ➔=➔ ➔"➔t➔c➔p➔"➔
➔ ➔ ➔ ➔ ➔c➔i➔d➔r➔_➔b➔l➔o➔c➔k➔s➔ ➔=➔ ➔[➔"➔0➔.➔0➔.➔0➔.➔0➔/➔0➔"➔]➔
➔ ➔ ➔}➔
➔ ➔ ➔e➔g➔r➔e➔s➔s➔ ➔{➔
➔ ➔ ➔ ➔ ➔f➔r➔o➔m➔_➔p➔o➔r➔t➔ ➔ ➔ ➔=➔ ➔0➔
➔ ➔ ➔ ➔ ➔t➔o➔_➔p➔o➔r➔t➔ ➔ ➔ ➔ ➔ ➔=➔ ➔0➔
➔ ➔ ➔ ➔ ➔p➔r➔o➔t➔o➔c➔o➔l➔ ➔ ➔ ➔ ➔=➔ ➔"➔-➔1➔"➔
➔ ➔ ➔ ➔ ➔c➔i➔d➔r➔_➔b➔l➔o➔c➔k➔s➔ ➔=➔ ➔[➔"➔0➔.➔0➔.➔0➔.➔0➔/➔0➔"➔]➔
➔ ➔ ➔}➔
➔ ➔ ➔t➔a➔g➔s➔ ➔=➔ ➔{➔
➔ ➔ ➔ ➔ ➔N➔a➔m➔e➔ ➔=➔ ➔"➔w➔e➔b➔-➔s➔g➔"➔
➔ ➔ ➔}➔
➔}➔
➔#➔ ➔─➔─➔ ➔E➔C➔2➔ ➔I➔N➔S➔T➔A➔N➔C➔E➔ ➔I➔N➔ ➔P➔U➔B➔L➔I➔C➔ ➔S➔U➔B➔N➔E➔T➔ ➔─➔─➔
➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔"➔a➔w➔s➔_➔i➔n➔s➔t➔a➔n➔c➔e➔"➔ ➔"➔w➔e➔b➔"➔ ➔{➔
➔ ➔ ➔a➔m➔i➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔v➔a➔r➔.➔a➔m➔i➔_➔i➔d➔
➔ ➔ ➔i➔n➔s➔t➔a➔n➔c➔e➔_➔t➔y➔p➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔v➔a➔r➔.➔i➔n➔s➔t➔a➔n➔c➔e➔_➔t➔y➔p➔e➔
➔ ➔ ➔s➔u➔b➔n➔e➔t➔_➔i➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔a➔w➔s➔_➔s➔u➔b➔n➔e➔t➔.➔p➔u➔b➔l➔i➔c➔.➔i➔d➔
➔ ➔ ➔v➔p➔c➔_➔s➔e➔c➔u➔r➔i➔t➔y➔_➔g➔r➔o➔u➔p➔_➔i➔d➔s➔ ➔=➔ ➔[➔a➔w➔s➔_➔s➔e➔c➔u➔r➔i➔t➔y➔_➔g➔r➔o➔u➔p➔.➔w➔e➔b➔_➔s➔g➔.➔i➔d➔]➔
➔ ➔ ➔k➔e➔y➔_➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔v➔a➔r➔.➔k➔e➔y➔_➔n➔a➔m➔e➔
➔ ➔ ➔t➔a➔g➔s➔ ➔=➔ ➔{➔
➔
➔
➔
➔
➔ ➔ ➔ ➔ ➔N➔a➔m➔e➔ ➔=➔ ➔"➔w➔e➔b➔-➔s➔e➔r➔v➔e➔r➔"➔
➔ ➔ ➔}➔
➔}➔
➔8➔.➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔s➔
➔W➔h➔y➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔?➔
➔A➔v➔o➔i➔d➔ ➔h➔a➔r➔d➔c➔o➔d➔i➔n➔g➔ ➔v➔a➔l➔u➔e➔s➔.➔ ➔R➔e➔u➔s➔e➔ ➔s➔a➔m➔e➔ ➔c➔o➔d➔e➔ ➔f➔o➔r➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔t➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔s➔ ➔(➔d➔e➔v➔,➔ ➔s➔t➔a➔g➔i➔n➔g➔,➔ ➔p➔r➔o➔d➔)➔.➔
➔D➔e➔c➔l➔a➔r➔i➔n➔g➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔s➔ ➔(➔v➔a➔r➔i➔a➔b➔l➔e➔s➔.➔t➔f➔)➔
➔#➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔.➔t➔f➔
➔v➔a➔r➔i➔a➔b➔l➔e➔ ➔"➔r➔e➔g➔i➔o➔n➔"➔ ➔{➔
➔ ➔ ➔d➔e➔s➔c➔r➔i➔p➔t➔i➔o➔n➔ ➔=➔ ➔"➔A➔W➔S➔ ➔r➔e➔g➔i➔o➔n➔"➔
➔ ➔ ➔t➔y➔p➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔s➔t➔r➔i➔n➔g➔
➔ ➔ ➔d➔e➔f➔a➔u➔l➔t➔ ➔ ➔ ➔ ➔ ➔=➔ ➔"➔u➔s➔-➔e➔a➔s➔t➔-➔1➔"➔
➔}➔
➔v➔a➔r➔i➔a➔b➔l➔e➔ ➔"➔i➔n➔s➔t➔a➔n➔c➔e➔_➔t➔y➔p➔e➔"➔ ➔{➔
➔ ➔ ➔d➔e➔s➔c➔r➔i➔p➔t➔i➔o➔n➔ ➔=➔ ➔"➔E➔C➔2➔ ➔i➔n➔s➔t➔a➔n➔c➔e➔ ➔t➔y➔p➔e➔"➔
➔ ➔ ➔t➔y➔p➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔s➔t➔r➔i➔n➔g➔
➔ ➔ ➔d➔e➔f➔a➔u➔l➔t➔ ➔ ➔ ➔ ➔ ➔=➔ ➔"➔t➔2➔.➔m➔i➔c➔r➔o➔"➔
➔}➔
➔v➔a➔r➔i➔a➔b➔l➔e➔ ➔"➔a➔m➔i➔_➔i➔d➔"➔ ➔{➔
➔ ➔ ➔d➔e➔s➔c➔r➔i➔p➔t➔i➔o➔n➔ ➔=➔ ➔"➔A➔M➔I➔ ➔I➔D➔ ➔f➔o➔r➔ ➔E➔C➔2➔"➔
➔ ➔ ➔t➔y➔p➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔s➔t➔r➔i➔n➔g➔
➔ ➔ ➔#➔ ➔n➔o➔ ➔d➔e➔f➔a➔u➔l➔t➔ ➔—➔ ➔m➔u➔s➔t➔ ➔b➔e➔ ➔p➔r➔o➔v➔i➔d➔e➔d➔
➔}➔
➔v➔a➔r➔i➔a➔b➔l➔e➔ ➔"➔k➔e➔y➔_➔n➔a➔m➔e➔"➔ ➔{➔
➔ ➔ ➔d➔e➔s➔c➔r➔i➔p➔t➔i➔o➔n➔ ➔=➔ ➔"➔S➔S➔H➔ ➔k➔e➔y➔ ➔p➔a➔i➔r➔ ➔n➔a➔m➔e➔"➔
➔ ➔ ➔t➔y➔p➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔s➔t➔r➔i➔n➔g➔
➔}➔
➔v➔a➔r➔i➔a➔b➔l➔e➔ ➔"➔a➔l➔l➔o➔w➔e➔d➔_➔p➔o➔r➔t➔s➔"➔ ➔{➔
➔ ➔ ➔d➔e➔s➔c➔r➔i➔p➔t➔i➔o➔n➔ ➔=➔ ➔"➔L➔i➔s➔t➔ ➔o➔f➔ ➔a➔l➔l➔o➔w➔e➔d➔ ➔p➔o➔r➔t➔s➔"➔
➔ ➔ ➔t➔y➔p➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔l➔i➔s➔t➔(➔n➔u➔m➔b➔e➔r➔)➔
➔ ➔ ➔d➔e➔f➔a➔u➔l➔t➔ ➔ ➔ ➔ ➔ ➔=➔ ➔[➔8➔0➔,➔ ➔4➔4➔3➔,➔ ➔2➔2➔]➔
➔}➔
➔v➔a➔r➔i➔a➔b➔l➔e➔ ➔"➔t➔a➔g➔s➔"➔ ➔{➔
➔
➔
➔
➔
➔ ➔ ➔d➔e➔s➔c➔r➔i➔p➔t➔i➔o➔n➔ ➔=➔ ➔"➔C➔o➔m➔m➔o➔n➔ ➔t➔a➔g➔s➔"➔
➔ ➔ ➔t➔y➔p➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔m➔a➔p➔(➔s➔t➔r➔i➔n➔g➔)➔
➔ ➔ ➔d➔e➔f➔a➔u➔l➔t➔ ➔=➔ ➔{➔
➔ ➔ ➔ ➔ ➔P➔r➔o➔j➔e➔c➔t➔ ➔ ➔ ➔ ➔ ➔=➔ ➔"➔M➔y➔A➔p➔p➔"➔
➔ ➔ ➔ ➔ ➔E➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔=➔ ➔"➔d➔e➔v➔"➔
➔ ➔ ➔ ➔ ➔O➔w➔n➔e➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔"➔A➔k➔h➔i➔l➔"➔
➔ ➔ ➔}➔
➔}➔
➔v➔a➔r➔i➔a➔b➔l➔e➔ ➔"➔d➔b➔_➔p➔a➔s➔s➔w➔o➔r➔d➔"➔ ➔{➔
➔ ➔ ➔d➔e➔s➔c➔r➔i➔p➔t➔i➔o➔n➔ ➔=➔ ➔"➔D➔a➔t➔a➔b➔a➔s➔e➔ ➔p➔a➔s➔s➔w➔o➔r➔d➔"➔
➔ ➔ ➔t➔y➔p➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔s➔t➔r➔i➔n➔g➔
➔ ➔ ➔s➔e➔n➔s➔i➔t➔i➔v➔e➔ ➔ ➔ ➔=➔ ➔t➔r➔u➔e➔ ➔ ➔ ➔ ➔#➔ ➔w➔o➔n➔'➔t➔ ➔s➔h➔o➔w➔ ➔i➔n➔ ➔l➔o➔g➔s➔ ➔o➔r➔ ➔o➔u➔t➔p➔u➔t➔
➔}➔
➔V➔a➔r➔i➔a➔b➔l➔e➔ ➔T➔y➔p➔e➔s➔
➔T➔y➔p➔e➔ ➔E➔x➔a➔m➔p➔l➔e➔
➔s➔t➔r➔i➔n➔g➔ ➔"➔u➔s➔-➔e➔a➔s➔t➔-➔1➔"➔
➔n➔u➔m➔b➔e➔r➔ ➔3➔
➔b➔o➔o➔l➔ ➔t➔r➔u➔e➔
➔l➔i➔s➔t➔(➔s➔t➔r➔i➔n➔g➔)➔ ➔[➔"➔a➔"➔,➔ ➔"➔b➔"➔,➔ ➔"➔c➔"➔]➔
➔m➔a➔p➔(➔s➔t➔r➔i➔n➔g➔)➔ ➔{➔k➔e➔y➔ ➔=➔ ➔"➔v➔a➔l➔u➔e➔"➔}➔
➔o➔b➔j➔e➔c➔t➔ ➔c➔o➔m➔p➔l➔e➔x➔ ➔t➔y➔p➔e➔
➔U➔s➔i➔n➔g➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔s➔ ➔(➔m➔a➔i➔n➔.➔t➔f➔)➔
➔p➔r➔o➔v➔i➔d➔e➔r➔ ➔"➔a➔w➔s➔"➔ ➔{➔
➔ ➔ ➔r➔e➔g➔i➔o➔n➔ ➔=➔ ➔v➔a➔r➔.➔r➔e➔g➔i➔o➔n➔
➔}➔
➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔"➔a➔w➔s➔_➔i➔n➔s➔t➔a➔n➔c➔e➔"➔ ➔"➔w➔e➔b➔"➔ ➔{➔
➔ ➔ ➔a➔m➔i➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔v➔a➔r➔.➔a➔m➔i➔_➔i➔d➔
➔ ➔ ➔i➔n➔s➔t➔a➔n➔c➔e➔_➔t➔y➔p➔e➔ ➔=➔ ➔v➔a➔r➔.➔i➔n➔s➔t➔a➔n➔c➔e➔_➔t➔y➔p➔e➔
➔ ➔ ➔k➔e➔y➔_➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔v➔a➔r➔.➔k➔e➔y➔_➔n➔a➔m➔e➔
➔ ➔ ➔t➔a➔g➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔v➔a➔r➔.➔t➔a➔g➔s➔
➔}➔
➔
➔
➔
➔
➔P➔r➔o➔v➔i➔d➔i➔n➔g➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔ ➔V➔a➔l➔u➔e➔s➔
➔M➔e➔t➔h➔o➔d➔ ➔1➔ ➔—➔ ➔t➔e➔r➔r➔a➔f➔o➔r➔m➔.➔t➔f➔v➔a➔r➔s➔ ➔f➔i➔l➔e➔ ➔(➔m➔o➔s➔t➔ ➔c➔o➔m➔m➔o➔n➔)➔:➔
➔#➔ ➔t➔e➔r➔r➔a➔f➔o➔r➔m➔.➔t➔f➔v➔a➔r➔s➔
➔r➔e➔g➔i➔o➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔"➔u➔s➔-➔e➔a➔s➔t➔-➔1➔"➔
➔i➔n➔s➔t➔a➔n➔c➔e➔_➔t➔y➔p➔e➔ ➔=➔ ➔"➔t➔3➔.➔m➔e➔d➔i➔u➔m➔"➔
➔a➔m➔i➔_➔i➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔"➔a➔m➔i➔-➔0➔c➔5➔5➔b➔1➔5➔9➔c➔b➔f➔a➔f➔e➔1➔f➔0➔"➔
➔k➔e➔y➔_➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔"➔m➔y➔-➔k➔e➔y➔p➔a➔i➔r➔"➔
➔d➔b➔_➔p➔a➔s➔s➔w➔o➔r➔d➔ ➔ ➔ ➔=➔ ➔"➔s➔u➔p➔e➔r➔s➔e➔c➔r➔e➔t➔"➔
➔M➔e➔t➔h➔o➔d➔ ➔2➔ ➔—➔ ➔C➔o➔m➔m➔a➔n➔d➔ ➔l➔i➔n➔e➔:➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔a➔p➔p➔l➔y➔ ➔-➔v➔a➔r➔=➔"➔r➔e➔g➔i➔o➔n➔=➔u➔s➔-➔e➔a➔s➔t➔-➔1➔"➔ ➔-➔v➔a➔r➔=➔"➔i➔n➔s➔t➔a➔n➔c➔e➔_➔t➔y➔p➔e➔=➔t➔3➔.➔m➔e➔d➔i➔u➔m➔"➔
➔M➔e➔t➔h➔o➔d➔ ➔3➔ ➔—➔ ➔E➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔:➔
➔e➔x➔p➔o➔r➔t➔ ➔T➔F➔_➔V➔A➔R➔_➔r➔e➔g➔i➔o➔n➔=➔"➔u➔s➔-➔e➔a➔s➔t➔-➔1➔"➔
➔e➔x➔p➔o➔r➔t➔ ➔T➔F➔_➔V➔A➔R➔_➔i➔n➔s➔t➔a➔n➔c➔e➔_➔t➔y➔p➔e➔=➔"➔t➔3➔.➔m➔e➔d➔i➔u➔m➔"➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔a➔p➔p➔l➔y➔
➔M➔e➔t➔h➔o➔d➔ ➔4➔ ➔—➔ ➔D➔i➔f➔f➔e➔r➔e➔n➔t➔ ➔.➔t➔f➔v➔a➔r➔s➔ ➔f➔o➔r➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔s➔:➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔a➔p➔p➔l➔y➔ ➔-➔v➔a➔r➔-➔f➔i➔l➔e➔=➔"➔d➔e➔v➔.➔t➔f➔v➔a➔r➔s➔"➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔a➔p➔p➔l➔y➔ ➔-➔v➔a➔r➔-➔f➔i➔l➔e➔=➔"➔p➔r➔o➔d➔.➔t➔f➔v➔a➔r➔s➔"➔
➔9➔.➔ ➔O➔u➔t➔p➔u➔t➔s➔
➔W➔h➔y➔ ➔o➔u➔t➔p➔u➔t➔s➔?➔
➔D➔i➔s➔p➔l➔a➔y➔ ➔u➔s➔e➔f➔u➔l➔ ➔i➔n➔f➔o➔r➔m➔a➔t➔i➔o➔n➔ ➔a➔f➔t➔e➔r➔ ➔a➔p➔p➔l➔y➔.➔ ➔S➔h➔a➔r➔e➔ ➔v➔a➔l➔u➔e➔s➔ ➔b➔e➔t➔w➔e➔e➔n➔ ➔m➔o➔d➔u➔l➔e➔s➔.➔
➔#➔ ➔o➔u➔t➔p➔u➔t➔s➔.➔t➔f➔
➔o➔u➔t➔p➔u➔t➔ ➔"➔v➔p➔c➔_➔i➔d➔"➔ ➔{➔
➔ ➔ ➔d➔e➔s➔c➔r➔i➔p➔t➔i➔o➔n➔ ➔=➔ ➔"➔I➔D➔ ➔o➔f➔ ➔t➔h➔e➔ ➔V➔P➔C➔"➔
➔ ➔ ➔v➔a➔l➔u➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔a➔w➔s➔_➔v➔p➔c➔.➔m➔a➔i➔n➔.➔i➔d➔
➔}➔
➔o➔u➔t➔p➔u➔t➔ ➔"➔p➔u➔b➔l➔i➔c➔_➔s➔u➔b➔n➔e➔t➔_➔i➔d➔"➔ ➔{➔
➔
➔
➔
➔
➔ ➔ ➔d➔e➔s➔c➔r➔i➔p➔t➔i➔o➔n➔ ➔=➔ ➔"➔I➔D➔ ➔o➔f➔ ➔p➔u➔b➔l➔i➔c➔ ➔s➔u➔b➔n➔e➔t➔"➔
➔ ➔ ➔v➔a➔l➔u➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔a➔w➔s➔_➔s➔u➔b➔n➔e➔t➔.➔p➔u➔b➔l➔i➔c➔.➔i➔d➔
➔}➔
➔o➔u➔t➔p➔u➔t➔ ➔"➔i➔n➔s➔t➔a➔n➔c➔e➔_➔p➔u➔b➔l➔i➔c➔_➔i➔p➔"➔ ➔{➔
➔ ➔ ➔d➔e➔s➔c➔r➔i➔p➔t➔i➔o➔n➔ ➔=➔ ➔"➔P➔u➔b➔l➔i➔c➔ ➔I➔P➔ ➔o➔f➔ ➔w➔e➔b➔ ➔s➔e➔r➔v➔e➔r➔"➔
➔ ➔ ➔v➔a➔l➔u➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔a➔w➔s➔_➔i➔n➔s➔t➔a➔n➔c➔e➔.➔w➔e➔b➔.➔p➔u➔b➔l➔i➔c➔_➔i➔p➔
➔}➔
➔o➔u➔t➔p➔u➔t➔ ➔"➔i➔n➔s➔t➔a➔n➔c➔e➔_➔d➔n➔s➔"➔ ➔{➔
➔ ➔ ➔d➔e➔s➔c➔r➔i➔p➔t➔i➔o➔n➔ ➔=➔ ➔"➔P➔u➔b➔l➔i➔c➔ ➔D➔N➔S➔ ➔o➔f➔ ➔w➔e➔b➔ ➔s➔e➔r➔v➔e➔r➔"➔
➔ ➔ ➔v➔a➔l➔u➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔a➔w➔s➔_➔i➔n➔s➔t➔a➔n➔c➔e➔.➔w➔e➔b➔.➔p➔u➔b➔l➔i➔c➔_➔d➔n➔s➔
➔}➔
➔o➔u➔t➔p➔u➔t➔ ➔"➔d➔b➔_➔p➔a➔s➔s➔w➔o➔r➔d➔"➔ ➔{➔
➔ ➔ ➔v➔a➔l➔u➔e➔ ➔ ➔ ➔ ➔ ➔=➔ ➔v➔a➔r➔.➔d➔b➔_➔p➔a➔s➔s➔w➔o➔r➔d➔
➔ ➔ ➔s➔e➔n➔s➔i➔t➔i➔v➔e➔ ➔=➔ ➔t➔r➔u➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔w➔o➔n➔'➔t➔ ➔s➔h➔o➔w➔ ➔i➔n➔ ➔t➔e➔r➔m➔i➔n➔a➔l➔
➔}➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔o➔u➔t➔p➔u➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔a➔l➔l➔ ➔o➔u➔t➔p➔u➔t➔s➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔o➔u➔t➔p➔u➔t➔ ➔v➔p➔c➔_➔i➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔o➔u➔t➔p➔u➔t➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔o➔u➔t➔p➔u➔t➔ ➔-➔j➔s➔o➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔o➔u➔t➔p➔u➔t➔ ➔a➔s➔ ➔J➔S➔O➔N➔
➔1➔0➔.➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔S➔t➔a➔t➔e➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔S➔t➔a➔t➔e➔?➔
➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔k➔e➔e➔p➔s➔ ➔a➔ ➔s➔t➔a➔t➔e➔ ➔f➔i➔l➔e➔ ➔(➔ ➔t➔e➔r➔r➔a➔f➔o➔r➔m➔.➔t➔f➔s➔t➔a➔t➔e➔ ➔)➔ ➔t➔h➔a➔t➔ ➔m➔a➔p➔s➔ ➔y➔o➔u➔r➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔ ➔t➔o➔ ➔r➔e➔a➔l➔ ➔i➔n➔f➔r➔a➔s➔t➔r➔u➔c➔t➔u➔r➔e➔.➔ ➔I➔t➔
➔t➔r➔a➔c➔k➔s➔ ➔w➔h➔a➔t➔ ➔e➔x➔i➔s➔t➔s➔ ➔s➔o➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔k➔n➔o➔w➔s➔ ➔w➔h➔a➔t➔ ➔t➔o➔ ➔c➔r➔e➔a➔t➔e➔,➔ ➔u➔p➔d➔a➔t➔e➔,➔ ➔o➔r➔ ➔d➔e➔l➔e➔t➔e➔.➔
➔/➔/➔ ➔t➔e➔r➔r➔a➔f➔o➔r➔m➔.➔t➔f➔s➔t➔a➔t➔e➔ ➔(➔s➔i➔m➔p➔l➔i➔f➔i➔e➔d➔)➔
➔{➔
➔ ➔ ➔"➔r➔e➔s➔o➔u➔r➔c➔e➔s➔"➔:➔ ➔[➔
➔ ➔ ➔ ➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔"➔t➔y➔p➔e➔"➔:➔ ➔"➔a➔w➔s➔_➔i➔n➔s➔t➔a➔n➔c➔e➔"➔,➔
➔ ➔ ➔ ➔ ➔ ➔ ➔"➔n➔a➔m➔e➔"➔:➔ ➔"➔w➔e➔b➔"➔,➔
➔ ➔ ➔ ➔ ➔ ➔ ➔"➔i➔n➔s➔t➔a➔n➔c➔e➔s➔"➔:➔ ➔[➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔"➔a➔t➔t➔r➔i➔b➔u➔t➔e➔s➔"➔:➔ ➔{➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔"➔i➔d➔"➔:➔ ➔"➔i➔-➔1➔2➔3➔4➔5➔6➔7➔8➔9➔0➔"➔,➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔"➔a➔m➔i➔"➔:➔ ➔"➔a➔m➔i➔-➔0➔c➔5➔5➔b➔1➔5➔9➔c➔b➔f➔a➔f➔e➔1➔f➔0➔"➔,➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔"➔p➔u➔b➔l➔i➔c➔_➔i➔p➔"➔:➔ ➔"➔5➔4➔.➔1➔2➔3➔.➔4➔5➔6➔.➔7➔8➔9➔"➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔
➔
➔
➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔ ➔ ➔ ➔ ➔]➔
➔ ➔ ➔ ➔ ➔}➔
➔ ➔ ➔]➔
➔}➔
➔L➔o➔c➔a➔l➔ ➔S➔t➔a➔t➔e➔ ➔v➔s➔ ➔R➔e➔m➔o➔t➔e➔ ➔S➔t➔a➔t➔e➔:➔
➔L➔o➔c➔a➔l➔ ➔S➔t➔a➔t➔e➔ ➔R➔e➔m➔o➔t➔e➔ ➔S➔t➔a➔t➔e➔
➔L➔o➔c➔a➔t➔i➔o➔n➔ ➔t➔e➔r➔r➔a➔f➔o➔r➔m➔.➔t➔f➔s➔t➔a➔t➔e➔ ➔o➔n➔ ➔y➔o➔u➔r➔ ➔m➔a➔c➔h➔i➔n➔e➔ ➔S➔3➔,➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔C➔l➔o➔u➔d➔
➔T➔e➔a➔m➔ ➔u➔s➔e➔ ➔❌➔ ➔ ➔N➔o➔t➔ ➔s➔a➔f➔e➔ ➔f➔o➔r➔ ➔t➔e➔a➔m➔s➔ ➔✅➔ ➔ ➔M➔u➔l➔t➔i➔p➔l➔e➔ ➔p➔e➔o➔p➔l➔e➔ ➔c➔a➔n➔ ➔w➔o➔r➔k➔
➔L➔o➔c➔k➔i➔n➔g➔ ➔N➔o➔ ➔Y➔e➔s➔ ➔(➔p➔r➔e➔v➔e➔n➔t➔s➔ ➔c➔o➔n➔f➔l➔i➔c➔t➔s➔)➔
➔B➔a➔c➔k➔u➔p➔ ➔M➔a➔n➔u➔a➔l➔ ➔A➔u➔t➔o➔m➔a➔t➔i➔c➔
➔R➔e➔m➔o➔t➔e➔ ➔S➔t➔a➔t➔e➔ ➔i➔n➔ ➔S➔3➔ ➔(➔f➔o➔r➔ ➔t➔e➔a➔m➔s➔)➔:➔
➔#➔ ➔b➔a➔c➔k➔e➔n➔d➔.➔t➔f➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔{➔
➔ ➔ ➔b➔a➔c➔k➔e➔n➔d➔ ➔"➔s➔3➔"➔ ➔{➔
➔ ➔ ➔ ➔ ➔b➔u➔c➔k➔e➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔"➔m➔y➔-➔t➔e➔r➔r➔a➔f➔o➔r➔m➔-➔s➔t➔a➔t➔e➔-➔b➔u➔c➔k➔e➔t➔"➔
➔ ➔ ➔ ➔ ➔k➔e➔y➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔"➔p➔r➔o➔d➔/➔v➔p➔c➔/➔t➔e➔r➔r➔a➔f➔o➔r➔m➔.➔t➔f➔s➔t➔a➔t➔e➔"➔
➔ ➔ ➔ ➔ ➔r➔e➔g➔i➔o➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔"➔u➔s➔-➔e➔a➔s➔t➔-➔1➔"➔
➔ ➔ ➔ ➔ ➔e➔n➔c➔r➔y➔p➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔t➔r➔u➔e➔
➔ ➔ ➔ ➔ ➔d➔y➔n➔a➔m➔o➔d➔b➔_➔t➔a➔b➔l➔e➔ ➔=➔ ➔"➔t➔e➔r➔r➔a➔f➔o➔r➔m➔-➔l➔o➔c➔k➔s➔"➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔r➔ ➔s➔t➔a➔t➔e➔ ➔l➔o➔c➔k➔i➔n➔g➔
➔ ➔ ➔}➔
➔}➔
➔1➔1➔.➔ ➔W➔o➔r➔k➔s➔p➔a➔c➔e➔s➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔ ➔W➔o➔r➔k➔s➔p➔a➔c➔e➔?➔
➔W➔o➔r➔k➔s➔p➔a➔c➔e➔s➔ ➔l➔e➔t➔ ➔y➔o➔u➔ ➔m➔a➔n➔a➔g➔e➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔s➔ ➔(➔d➔e➔v➔,➔ ➔s➔t➔a➔g➔i➔n➔g➔,➔ ➔p➔r➔o➔d➔)➔ ➔w➔i➔t➔h➔ ➔t➔h➔e➔ ➔s➔a➔m➔e➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔ ➔b➔u➔t➔
➔s➔e➔p➔a➔r➔a➔t➔e➔ ➔s➔t➔a➔t➔e➔ ➔f➔i➔l➔e➔s➔.➔
➔d➔e➔f➔a➔u➔l➔t➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔ ➔ ➔→➔ ➔t➔e➔r➔r➔a➔f➔o➔r➔m➔.➔t➔f➔s➔t➔a➔t➔e➔
➔d➔e➔v➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔t➔e➔r➔r➔a➔f➔o➔r➔m➔.➔t➔f➔s➔t➔a➔t➔e➔.➔d➔/➔d➔e➔v➔/➔t➔e➔r➔r➔a➔f➔o➔r➔m➔.➔t➔f➔s➔t➔a➔t➔e➔
➔p➔r➔o➔d➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔ ➔ ➔ ➔ ➔ ➔→➔ ➔t➔e➔r➔r➔a➔f➔o➔r➔m➔.➔t➔f➔s➔t➔a➔t➔e➔.➔d➔/➔p➔r➔o➔d➔/➔t➔e➔r➔r➔a➔f➔o➔r➔m➔.➔t➔f➔s➔t➔a➔t➔e➔
➔
➔
➔
➔
➔#➔ ➔W➔o➔r➔k➔s➔p➔a➔c➔e➔ ➔c➔o➔m➔m➔a➔n➔d➔s➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔ ➔l➔i➔s➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔a➔l➔l➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔s➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔ ➔n➔e➔w➔ ➔d➔e➔v➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔d➔e➔v➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔ ➔n➔e➔w➔ ➔s➔t➔a➔g➔i➔n➔g➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔s➔t➔a➔g➔i➔n➔g➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔ ➔n➔e➔w➔ ➔p➔r➔o➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔p➔r➔o➔d➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔ ➔s➔e➔l➔e➔c➔t➔ ➔d➔e➔v➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔w➔i➔t➔c➔h➔ ➔t➔o➔ ➔d➔e➔v➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔ ➔s➔h➔o➔w➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔ ➔d➔e➔l➔e➔t➔e➔ ➔d➔e➔v➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔
➔U➔s➔i➔n➔g➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔ ➔i➔n➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔:➔
➔#➔ ➔U➔s➔e➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔ ➔n➔a➔m➔e➔ ➔t➔o➔ ➔s➔e➔t➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔t➔ ➔v➔a➔l➔u➔e➔s➔
➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔"➔a➔w➔s➔_➔i➔n➔s➔t➔a➔n➔c➔e➔"➔ ➔"➔w➔e➔b➔"➔ ➔{➔
➔ ➔ ➔i➔n➔s➔t➔a➔n➔c➔e➔_➔t➔y➔p➔e➔ ➔=➔ ➔t➔e➔r➔r➔a➔f➔o➔r➔m➔.➔w➔o➔r➔k➔s➔p➔a➔c➔e➔ ➔=➔=➔ ➔"➔p➔r➔o➔d➔"➔ ➔?➔ ➔"➔t➔3➔.➔l➔a➔r➔g➔e➔"➔ ➔:➔ ➔"➔t➔2➔.➔m➔i➔c➔r➔o➔"➔
➔ ➔ ➔t➔a➔g➔s➔ ➔=➔ ➔{➔
➔ ➔ ➔ ➔ ➔N➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔"➔w➔e➔b➔-➔$➔{➔t➔e➔r➔r➔a➔f➔o➔r➔m➔.➔w➔o➔r➔k➔s➔p➔a➔c➔e➔}➔"➔
➔ ➔ ➔ ➔ ➔E➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔=➔ ➔t➔e➔r➔r➔a➔f➔o➔r➔m➔.➔w➔o➔r➔k➔s➔p➔a➔c➔e➔
➔ ➔ ➔}➔
➔}➔
➔#➔ ➔O➔r➔ ➔u➔s➔e➔ ➔l➔o➔c➔a➔l➔s➔
➔l➔o➔c➔a➔l➔s➔ ➔{➔
➔ ➔ ➔i➔n➔s➔t➔a➔n➔c➔e➔_➔t➔y➔p➔e➔ ➔=➔ ➔{➔
➔ ➔ ➔ ➔ ➔d➔e➔v➔ ➔ ➔ ➔ ➔ ➔=➔ ➔"➔t➔2➔.➔m➔i➔c➔r➔o➔"➔
➔ ➔ ➔ ➔ ➔s➔t➔a➔g➔i➔n➔g➔ ➔=➔ ➔"➔t➔2➔.➔m➔e➔d➔i➔u➔m➔"➔
➔ ➔ ➔ ➔ ➔p➔r➔o➔d➔ ➔ ➔ ➔ ➔=➔ ➔"➔t➔3➔.➔l➔a➔r➔g➔e➔"➔
➔ ➔ ➔}➔
➔}➔
➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔"➔a➔w➔s➔_➔i➔n➔s➔t➔a➔n➔c➔e➔"➔ ➔"➔w➔e➔b➔"➔ ➔{➔
➔ ➔ ➔i➔n➔s➔t➔a➔n➔c➔e➔_➔t➔y➔p➔e➔ ➔=➔ ➔l➔o➔c➔a➔l➔.➔i➔n➔s➔t➔a➔n➔c➔e➔_➔t➔y➔p➔e➔[➔t➔e➔r➔r➔a➔f➔o➔r➔m➔.➔w➔o➔r➔k➔s➔p➔a➔c➔e➔]➔
➔}➔
➔W➔o➔r➔k➔s➔p➔a➔c➔e➔ ➔w➔o➔r➔k➔f➔l➔o➔w➔:➔
➔#➔ ➔D➔e➔p➔l➔o➔y➔ ➔t➔o➔ ➔d➔e➔v➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔ ➔s➔e➔l➔e➔c➔t➔ ➔d➔e➔v➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔a➔p➔p➔l➔y➔ ➔-➔v➔a➔r➔-➔f➔i➔l➔e➔=➔"➔d➔e➔v➔.➔t➔f➔v➔a➔r➔s➔"➔
➔#➔ ➔D➔e➔p➔l➔o➔y➔ ➔t➔o➔ ➔p➔r➔o➔d➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔ ➔s➔e➔l➔e➔c➔t➔ ➔p➔r➔o➔d➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔a➔p➔p➔l➔y➔ ➔-➔v➔a➔r➔-➔f➔i➔l➔e➔=➔"➔p➔r➔o➔d➔.➔t➔f➔v➔a➔r➔s➔"➔
➔
➔
➔
➔
➔1➔2➔.➔ ➔M➔o➔d➔u➔l➔e➔s➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔ ➔M➔o➔d➔u➔l➔e➔?➔
➔A➔ ➔m➔o➔d➔u➔l➔e➔ ➔i➔s➔ ➔a➔ ➔r➔e➔u➔s➔a➔b➔l➔e➔ ➔p➔a➔c➔k➔a➔g➔e➔ ➔o➔f➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔c➔o➔d➔e➔.➔ ➔I➔n➔s➔t➔e➔a➔d➔ ➔o➔f➔ ➔r➔e➔w➔r➔i➔t➔i➔n➔g➔ ➔t➔h➔e➔ ➔s➔a➔m➔e➔ ➔V➔P➔C➔ ➔c➔o➔d➔e➔ ➔f➔o➔r➔ ➔e➔v➔e➔r➔y➔ ➔p➔r➔o➔j➔e➔c➔t➔,➔
➔w➔r➔i➔t➔e➔ ➔i➔t➔ ➔o➔n➔c➔e➔ ➔a➔s➔ ➔a➔ ➔m➔o➔d➔u➔l➔e➔ ➔a➔n➔d➔ ➔u➔s➔e➔ ➔i➔t➔ ➔e➔v➔e➔r➔y➔w➔h➔e➔r➔e➔.➔
➔W➔i➔t➔h➔o➔u➔t➔ ➔m➔o➔d➔u➔l➔e➔s➔:➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔W➔i➔t➔h➔ ➔m➔o➔d➔u➔l➔e➔s➔:➔
➔p➔r➔o➔j➔e➔c➔t➔1➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔m➔o➔d➔u➔l➔e➔s➔/➔
➔ ➔ ➔m➔a➔i➔n➔.➔t➔f➔ ➔(➔v➔p➔c➔ ➔c➔o➔d➔e➔)➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔v➔p➔c➔/➔
➔ ➔ ➔m➔a➔i➔n➔.➔t➔f➔ ➔(➔e➔c➔2➔ ➔c➔o➔d➔e➔)➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔m➔a➔i➔n➔.➔t➔f➔
➔p➔r➔o➔j➔e➔c➔t➔2➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔.➔t➔f➔
➔ ➔ ➔m➔a➔i➔n➔.➔t➔f➔ ➔(➔v➔p➔c➔ ➔c➔o➔d➔e➔ ➔A➔G➔A➔I➔N➔)➔ ➔ ➔ ➔ ➔ ➔o➔u➔t➔p➔u➔t➔s➔.➔t➔f➔
➔ ➔ ➔m➔a➔i➔n➔.➔t➔f➔ ➔(➔e➔c➔2➔ ➔c➔o➔d➔e➔ ➔A➔G➔A➔I➔N➔)➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔r➔o➔j➔e➔c➔t➔1➔/➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔m➔a➔i➔n➔.➔t➔f➔ ➔(➔c➔a➔l➔l➔s➔ ➔v➔p➔c➔ ➔m➔o➔d➔u➔l➔e➔)➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔r➔o➔j➔e➔c➔t➔2➔/➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔m➔a➔i➔n➔.➔t➔f➔ ➔(➔c➔a➔l➔l➔s➔ ➔v➔p➔c➔ ➔m➔o➔d➔u➔l➔e➔)➔
➔C➔r➔e➔a➔t➔i➔n➔g➔ ➔a➔ ➔M➔o➔d➔u➔l➔e➔
➔#➔ ➔m➔o➔d➔u➔l➔e➔s➔/➔v➔p➔c➔/➔m➔a➔i➔n➔.➔t➔f➔
➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔"➔a➔w➔s➔_➔v➔p➔c➔"➔ ➔"➔m➔a➔i➔n➔"➔ ➔{➔
➔ ➔ ➔c➔i➔d➔r➔_➔b➔l➔o➔c➔k➔ ➔=➔ ➔v➔a➔r➔.➔c➔i➔d➔r➔_➔b➔l➔o➔c➔k➔
➔ ➔ ➔t➔a➔g➔s➔ ➔=➔ ➔{➔
➔ ➔ ➔ ➔ ➔N➔a➔m➔e➔ ➔=➔ ➔v➔a➔r➔.➔v➔p➔c➔_➔n➔a➔m➔e➔
➔ ➔ ➔}➔
➔}➔
➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔"➔a➔w➔s➔_➔s➔u➔b➔n➔e➔t➔"➔ ➔"➔p➔u➔b➔l➔i➔c➔"➔ ➔{➔
➔ ➔ ➔v➔p➔c➔_➔i➔d➔ ➔ ➔ ➔ ➔ ➔=➔ ➔a➔w➔s➔_➔v➔p➔c➔.➔m➔a➔i➔n➔.➔i➔d➔
➔ ➔ ➔c➔i➔d➔r➔_➔b➔l➔o➔c➔k➔ ➔=➔ ➔v➔a➔r➔.➔p➔u➔b➔l➔i➔c➔_➔s➔u➔b➔n➔e➔t➔_➔c➔i➔d➔r➔
➔}➔
➔#➔ ➔m➔o➔d➔u➔l➔e➔s➔/➔v➔p➔c➔/➔v➔a➔r➔i➔a➔b➔l➔e➔s➔.➔t➔f➔
➔v➔a➔r➔i➔a➔b➔l➔e➔ ➔"➔c➔i➔d➔r➔_➔b➔l➔o➔c➔k➔"➔ ➔{➔
➔ ➔ ➔t➔y➔p➔e➔ ➔=➔ ➔s➔t➔r➔i➔n➔g➔
➔}➔
➔v➔a➔r➔i➔a➔b➔l➔e➔ ➔"➔v➔p➔c➔_➔n➔a➔m➔e➔"➔ ➔{➔
➔ ➔ ➔t➔y➔p➔e➔ ➔=➔ ➔s➔t➔r➔i➔n➔g➔
➔}➔
➔v➔a➔r➔i➔a➔b➔l➔e➔ ➔"➔p➔u➔b➔l➔i➔c➔_➔s➔u➔b➔n➔e➔t➔_➔c➔i➔d➔r➔"➔ ➔{➔
➔
➔
➔
➔
➔ ➔ ➔t➔y➔p➔e➔ ➔=➔ ➔s➔t➔r➔i➔n➔g➔
➔}➔
➔#➔ ➔m➔o➔d➔u➔l➔e➔s➔/➔v➔p➔c➔/➔o➔u➔t➔p➔u➔t➔s➔.➔t➔f➔
➔o➔u➔t➔p➔u➔t➔ ➔"➔v➔p➔c➔_➔i➔d➔"➔ ➔{➔
➔ ➔ ➔v➔a➔l➔u➔e➔ ➔=➔ ➔a➔w➔s➔_➔v➔p➔c➔.➔m➔a➔i➔n➔.➔i➔d➔
➔}➔
➔o➔u➔t➔p➔u➔t➔ ➔"➔s➔u➔b➔n➔e➔t➔_➔i➔d➔"➔ ➔{➔
➔ ➔ ➔v➔a➔l➔u➔e➔ ➔=➔ ➔a➔w➔s➔_➔s➔u➔b➔n➔e➔t➔.➔p➔u➔b➔l➔i➔c➔.➔i➔d➔
➔}➔
➔U➔s➔i➔n➔g➔ ➔a➔ ➔M➔o➔d➔u➔l➔e➔
➔#➔ ➔m➔a➔i➔n➔.➔t➔f➔ ➔(➔i➔n➔ ➔y➔o➔u➔r➔ ➔p➔r➔o➔j➔e➔c➔t➔)➔
➔#➔ ➔L➔o➔c➔a➔l➔ ➔m➔o➔d➔u➔l➔e➔
➔m➔o➔d➔u➔l➔e➔ ➔"➔v➔p➔c➔"➔ ➔{➔
➔ ➔ ➔s➔o➔u➔r➔c➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔"➔.➔/➔m➔o➔d➔u➔l➔e➔s➔/➔v➔p➔c➔"➔ ➔ ➔ ➔ ➔#➔ ➔p➔a➔t➔h➔ ➔t➔o➔ ➔m➔o➔d➔u➔l➔e➔
➔ ➔ ➔c➔i➔d➔r➔_➔b➔l➔o➔c➔k➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔"➔1➔0➔.➔0➔.➔0➔.➔0➔/➔1➔6➔"➔
➔ ➔ ➔v➔p➔c➔_➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔"➔p➔r➔o➔d➔-➔v➔p➔c➔"➔
➔ ➔ ➔p➔u➔b➔l➔i➔c➔_➔s➔u➔b➔n➔e➔t➔_➔c➔i➔d➔r➔ ➔=➔ ➔"➔1➔0➔.➔0➔.➔1➔.➔0➔/➔2➔4➔"➔
➔}➔
➔#➔ ➔P➔u➔b➔l➔i➔c➔ ➔r➔e➔g➔i➔s➔t➔r➔y➔ ➔m➔o➔d➔u➔l➔e➔ ➔(➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔R➔e➔g➔i➔s➔t➔r➔y➔)➔
➔m➔o➔d➔u➔l➔e➔ ➔"➔v➔p➔c➔"➔ ➔{➔
➔ ➔ ➔s➔o➔u➔r➔c➔e➔ ➔ ➔=➔ ➔"➔t➔e➔r➔r➔a➔f➔o➔r➔m➔-➔a➔w➔s➔-➔m➔o➔d➔u➔l➔e➔s➔/➔v➔p➔c➔/➔a➔w➔s➔"➔
➔ ➔ ➔v➔e➔r➔s➔i➔o➔n➔ ➔=➔ ➔"➔5➔.➔0➔.➔0➔"➔
➔ ➔ ➔n➔a➔m➔e➔ ➔=➔ ➔"➔m➔y➔-➔v➔p➔c➔"➔
➔ ➔ ➔c➔i➔d➔r➔ ➔=➔ ➔"➔1➔0➔.➔0➔.➔0➔.➔0➔/➔1➔6➔"➔
➔ ➔ ➔a➔z➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔[➔"➔u➔s➔-➔e➔a➔s➔t➔-➔1➔a➔"➔,➔ ➔"➔u➔s➔-➔e➔a➔s➔t➔-➔1➔b➔"➔]➔
➔ ➔ ➔p➔r➔i➔v➔a➔t➔e➔_➔s➔u➔b➔n➔e➔t➔s➔ ➔=➔ ➔[➔"➔1➔0➔.➔0➔.➔1➔.➔0➔/➔2➔4➔"➔,➔ ➔"➔1➔0➔.➔0➔.➔2➔.➔0➔/➔2➔4➔"➔]➔
➔ ➔ ➔p➔u➔b➔l➔i➔c➔_➔s➔u➔b➔n➔e➔t➔s➔ ➔ ➔=➔ ➔[➔"➔1➔0➔.➔0➔.➔4➔.➔0➔/➔2➔4➔"➔,➔ ➔"➔1➔0➔.➔0➔.➔5➔.➔0➔/➔2➔4➔"➔]➔
➔ ➔ ➔e➔n➔a➔b➔l➔e➔_➔n➔a➔t➔_➔g➔a➔t➔e➔w➔a➔y➔ ➔=➔ ➔t➔r➔u➔e➔
➔}➔
➔#➔ ➔U➔s➔e➔ ➔m➔o➔d➔u➔l➔e➔ ➔o➔u➔t➔p➔u➔t➔s➔
➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔"➔a➔w➔s➔_➔i➔n➔s➔t➔a➔n➔c➔e➔"➔ ➔"➔w➔e➔b➔"➔ ➔{➔
➔ ➔ ➔s➔u➔b➔n➔e➔t➔_➔i➔d➔ ➔=➔ ➔m➔o➔d➔u➔l➔e➔.➔v➔p➔c➔.➔s➔u➔b➔n➔e➔t➔_➔i➔d➔
➔}➔
➔
➔
➔
➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔i➔n➔i➔t➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔o➔w➔n➔l➔o➔a➔d➔s➔ ➔m➔o➔d➔u➔l➔e➔s➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔p➔l➔a➔n➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔a➔p➔p➔l➔y➔
➔1➔3➔.➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔M➔e➔t➔a➔-➔A➔r➔g➔u➔m➔e➔n➔t➔s➔
➔#➔ ➔c➔o➔u➔n➔t➔ ➔—➔ ➔c➔r➔e➔a➔t➔e➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔s➔
➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔"➔a➔w➔s➔_➔i➔n➔s➔t➔a➔n➔c➔e➔"➔ ➔"➔w➔e➔b➔"➔ ➔{➔
➔ ➔ ➔c➔o➔u➔n➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔3➔
➔ ➔ ➔a➔m➔i➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔v➔a➔r➔.➔a➔m➔i➔_➔i➔d➔
➔ ➔ ➔i➔n➔s➔t➔a➔n➔c➔e➔_➔t➔y➔p➔e➔ ➔=➔ ➔"➔t➔2➔.➔m➔i➔c➔r➔o➔"➔
➔ ➔ ➔t➔a➔g➔s➔ ➔=➔ ➔{➔
➔ ➔ ➔ ➔ ➔N➔a➔m➔e➔ ➔=➔ ➔"➔w➔e➔b➔-➔$➔{➔c➔o➔u➔n➔t➔.➔i➔n➔d➔e➔x➔}➔"➔ ➔ ➔ ➔ ➔#➔ ➔w➔e➔b➔-➔0➔,➔ ➔w➔e➔b➔-➔1➔,➔ ➔w➔e➔b➔-➔2➔
➔ ➔ ➔}➔
➔}➔
➔#➔ ➔f➔o➔r➔_➔e➔a➔c➔h➔ ➔—➔ ➔c➔r➔e➔a➔t➔e➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔s➔ ➔f➔r➔o➔m➔ ➔m➔a➔p➔ ➔o➔r➔ ➔s➔e➔t➔
➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔"➔a➔w➔s➔_➔s➔3➔_➔b➔u➔c➔k➔e➔t➔"➔ ➔"➔b➔u➔c➔k➔e➔t➔s➔"➔ ➔{➔
➔ ➔ ➔f➔o➔r➔_➔e➔a➔c➔h➔ ➔=➔ ➔t➔o➔s➔e➔t➔(➔[➔"➔d➔e➔v➔"➔,➔ ➔"➔s➔t➔a➔g➔i➔n➔g➔"➔,➔ ➔"➔p➔r➔o➔d➔"➔]➔)➔
➔ ➔ ➔b➔u➔c➔k➔e➔t➔ ➔ ➔ ➔=➔ ➔"➔m➔y➔a➔p➔p➔-➔$➔{➔e➔a➔c➔h➔.➔k➔e➔y➔}➔"➔
➔}➔
➔#➔ ➔d➔e➔p➔e➔n➔d➔s➔_➔o➔n➔ ➔—➔ ➔e➔x➔p➔l➔i➔c➔i➔t➔ ➔d➔e➔p➔e➔n➔d➔e➔n➔c➔y➔
➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔"➔a➔w➔s➔_➔i➔n➔s➔t➔a➔n➔c➔e➔"➔ ➔"➔w➔e➔b➔"➔ ➔{➔
➔ ➔ ➔d➔e➔p➔e➔n➔d➔s➔_➔o➔n➔ ➔=➔ ➔[➔a➔w➔s➔_➔v➔p➔c➔.➔m➔a➔i➔n➔,➔ ➔a➔w➔s➔_➔s➔u➔b➔n➔e➔t➔.➔p➔u➔b➔l➔i➔c➔]➔
➔ ➔ ➔#➔ ➔.➔.➔.➔
➔}➔
➔#➔ ➔l➔i➔f➔e➔c➔y➔c➔l➔e➔ ➔—➔ ➔c➔o➔n➔t➔r➔o➔l➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔b➔e➔h➔a➔v➔i➔o➔r➔
➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔"➔a➔w➔s➔_➔i➔n➔s➔t➔a➔n➔c➔e➔"➔ ➔"➔w➔e➔b➔"➔ ➔{➔
➔ ➔ ➔#➔ ➔.➔.➔.➔
➔ ➔ ➔l➔i➔f➔e➔c➔y➔c➔l➔e➔ ➔{➔
➔ ➔ ➔ ➔ ➔c➔r➔e➔a➔t➔e➔_➔b➔e➔f➔o➔r➔e➔_➔d➔e➔s➔t➔r➔o➔y➔ ➔=➔ ➔t➔r➔u➔e➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔n➔e➔w➔ ➔b➔e➔f➔o➔r➔e➔ ➔d➔e➔s➔t➔r➔o➔y➔i➔n➔g➔ ➔o➔l➔d➔
➔ ➔ ➔ ➔ ➔p➔r➔e➔v➔e➔n➔t➔_➔d➔e➔s➔t➔r➔o➔y➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔t➔r➔u➔e➔ ➔ ➔ ➔ ➔#➔ ➔n➔e➔v➔e➔r➔ ➔a➔l➔l➔o➔w➔ ➔d➔e➔s➔t➔r➔o➔y➔ ➔(➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔D➔B➔s➔)➔
➔ ➔ ➔ ➔ ➔i➔g➔n➔o➔r➔e➔_➔c➔h➔a➔n➔g➔e➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔[➔t➔a➔g➔s➔]➔ ➔ ➔#➔ ➔i➔g➔n➔o➔r➔e➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔t➔o➔ ➔t➔a➔g➔s➔
➔ ➔ ➔}➔
➔}➔
➔
➔
➔
➔
➔1➔4➔.➔ ➔D➔a➔t➔a➔ ➔S➔o➔u➔r➔c➔e➔s➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔ ➔D➔a➔t➔a➔ ➔S➔o➔u➔r➔c➔e➔?➔
➔D➔a➔t➔a➔ ➔s➔o➔u➔r➔c➔e➔s➔ ➔l➔e➔t➔ ➔y➔o➔u➔ ➔f➔e➔t➔c➔h➔ ➔i➔n➔f➔o➔r➔m➔a➔t➔i➔o➔n➔ ➔a➔b➔o➔u➔t➔ ➔e➔x➔i➔s➔t➔i➔n➔g➔ ➔i➔n➔f➔r➔a➔s➔t➔r➔u➔c➔t➔u➔r➔e➔ ➔(➔n➔o➔t➔ ➔m➔a➔n➔a➔g➔e➔d➔ ➔b➔y➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔)➔ ➔a➔n➔d➔ ➔u➔s➔e➔ ➔i➔t➔ ➔i➔n➔
➔y➔o➔u➔r➔ ➔c➔o➔n➔f➔i➔g➔.➔
➔#➔ ➔F➔e➔t➔c➔h➔ ➔e➔x➔i➔s➔t➔i➔n➔g➔ ➔V➔P➔C➔
➔d➔a➔t➔a➔ ➔"➔a➔w➔s➔_➔v➔p➔c➔"➔ ➔"➔e➔x➔i➔s➔t➔i➔n➔g➔"➔ ➔{➔
➔ ➔ ➔i➔d➔ ➔=➔ ➔"➔v➔p➔c➔-➔1➔2➔3➔4➔5➔6➔7➔8➔"➔
➔}➔
➔#➔ ➔F➔e➔t➔c➔h➔ ➔l➔a➔t➔e➔s➔t➔ ➔A➔m➔a➔z➔o➔n➔ ➔L➔i➔n➔u➔x➔ ➔A➔M➔I➔ ➔a➔u➔t➔o➔m➔a➔t➔i➔c➔a➔l➔l➔y➔
➔d➔a➔t➔a➔ ➔"➔a➔w➔s➔_➔a➔m➔i➔"➔ ➔"➔a➔m➔a➔z➔o➔n➔_➔l➔i➔n➔u➔x➔"➔ ➔{➔
➔ ➔ ➔m➔o➔s➔t➔_➔r➔e➔c➔e➔n➔t➔ ➔=➔ ➔t➔r➔u➔e➔
➔ ➔ ➔o➔w➔n➔e➔r➔s➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔[➔"➔a➔m➔a➔z➔o➔n➔"➔]➔
➔ ➔ ➔f➔i➔l➔t➔e➔r➔ ➔{➔
➔ ➔ ➔ ➔ ➔n➔a➔m➔e➔ ➔ ➔ ➔=➔ ➔"➔n➔a➔m➔e➔"➔
➔ ➔ ➔ ➔ ➔v➔a➔l➔u➔e➔s➔ ➔=➔ ➔[➔"➔a➔m➔z➔n➔2➔-➔a➔m➔i➔-➔h➔v➔m➔-➔*➔-➔x➔8➔6➔_➔6➔4➔-➔g➔p➔2➔"➔]➔
➔ ➔ ➔}➔
➔}➔
➔#➔ ➔U➔s➔e➔ ➔d➔a➔t➔a➔ ➔s➔o➔u➔r➔c➔e➔
➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔"➔a➔w➔s➔_➔i➔n➔s➔t➔a➔n➔c➔e➔"➔ ➔"➔w➔e➔b➔"➔ ➔{➔
➔ ➔ ➔a➔m➔i➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔d➔a➔t➔a➔.➔a➔w➔s➔_➔a➔m➔i➔.➔a➔m➔a➔z➔o➔n➔_➔l➔i➔n➔u➔x➔.➔i➔d➔ ➔ ➔ ➔ ➔#➔ ➔a➔l➔w➔a➔y➔s➔ ➔l➔a➔t➔e➔s➔t➔ ➔A➔M➔I➔
➔ ➔ ➔i➔n➔s➔t➔a➔n➔c➔e➔_➔t➔y➔p➔e➔ ➔=➔ ➔"➔t➔2➔.➔m➔i➔c➔r➔o➔"➔
➔ ➔ ➔s➔u➔b➔n➔e➔t➔_➔i➔d➔ ➔ ➔ ➔ ➔ ➔=➔ ➔d➔a➔t➔a➔.➔a➔w➔s➔_➔v➔p➔c➔.➔e➔x➔i➔s➔t➔i➔n➔g➔.➔i➔d➔
➔}➔
➔1➔5➔.➔ ➔L➔o➔c➔a➔l➔s➔
➔W➔h➔a➔t➔ ➔a➔r➔e➔ ➔L➔o➔c➔a➔l➔s➔?➔
➔L➔o➔c➔a➔l➔ ➔v➔a➔l➔u➔e➔s➔ ➔a➔r➔e➔ ➔l➔i➔k➔e➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔ ➔b➔u➔t➔ ➔c➔o➔m➔p➔u➔t➔e➔d➔ ➔w➔i➔t➔h➔i➔n➔ ➔t➔h➔e➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔.➔ ➔U➔s➔e➔d➔ ➔t➔o➔ ➔a➔v➔o➔i➔d➔ ➔r➔e➔p➔e➔t➔i➔t➔i➔o➔n➔.➔
➔l➔o➔c➔a➔l➔s➔ ➔{➔
➔ ➔ ➔e➔n➔v➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔t➔e➔r➔r➔a➔f➔o➔r➔m➔.➔w➔o➔r➔k➔s➔p➔a➔c➔e➔
➔ ➔ ➔a➔p➔p➔_➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔=➔ ➔"➔m➔y➔a➔p➔p➔"➔
➔ ➔ ➔c➔o➔m➔m➔o➔n➔_➔t➔a➔g➔s➔ ➔=➔ ➔{➔
➔ ➔ ➔ ➔ ➔P➔r➔o➔j➔e➔c➔t➔ ➔ ➔ ➔ ➔ ➔=➔ ➔l➔o➔c➔a➔l➔.➔a➔p➔p➔_➔n➔a➔m➔e➔
➔ ➔ ➔ ➔ ➔E➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔=➔ ➔l➔o➔c➔a➔l➔.➔e➔n➔v➔
➔ ➔ ➔ ➔ ➔O➔w➔n➔e➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔"➔A➔k➔h➔i➔l➔"➔
➔
➔
➔
➔
➔ ➔ ➔ ➔ ➔M➔a➔n➔a➔g➔e➔d➔B➔y➔ ➔ ➔ ➔=➔ ➔"➔T➔e➔r➔r➔a➔f➔o➔r➔m➔"➔
➔ ➔ ➔}➔
➔}➔
➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔"➔a➔w➔s➔_➔i➔n➔s➔t➔a➔n➔c➔e➔"➔ ➔"➔w➔e➔b➔"➔ ➔{➔
➔ ➔ ➔a➔m➔i➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔v➔a➔r➔.➔a➔m➔i➔_➔i➔d➔
➔ ➔ ➔i➔n➔s➔t➔a➔n➔c➔e➔_➔t➔y➔p➔e➔ ➔=➔ ➔"➔t➔2➔.➔m➔i➔c➔r➔o➔"➔
➔ ➔ ➔t➔a➔g➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔l➔o➔c➔a➔l➔.➔c➔o➔m➔m➔o➔n➔_➔t➔a➔g➔s➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔u➔s➔e➔ ➔c➔o➔m➔m➔o➔n➔ ➔t➔a➔g➔s➔ ➔e➔v➔e➔r➔y➔w➔h➔e➔r➔e➔
➔}➔
➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔"➔a➔w➔s➔_➔s➔3➔_➔b➔u➔c➔k➔e➔t➔"➔ ➔"➔d➔a➔t➔a➔"➔ ➔{➔
➔ ➔ ➔b➔u➔c➔k➔e➔t➔ ➔=➔ ➔"➔$➔{➔l➔o➔c➔a➔l➔.➔a➔p➔p➔_➔n➔a➔m➔e➔}➔-➔$➔{➔l➔o➔c➔a➔l➔.➔e➔n➔v➔}➔-➔d➔a➔t➔a➔"➔
➔ ➔ ➔t➔a➔g➔s➔ ➔ ➔ ➔=➔ ➔l➔o➔c➔a➔l➔.➔c➔o➔m➔m➔o➔n➔_➔t➔a➔g➔s➔
➔}➔
➔1➔6➔.➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔I➔n➔t➔e➔r➔v➔i➔e➔w➔ ➔Q➔&➔A➔
➔Q➔:➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔t➔h➔e➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔c➔e➔ ➔b➔e➔t➔w➔e➔e➔n➔ ➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔p➔l➔a➔n➔ ➔a➔n➔d➔ ➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔a➔p➔p➔l➔y➔?➔
➔p➔l➔a➔n➔ ➔ ➔s➔h➔o➔w➔s➔ ➔w➔h➔a➔t➔ ➔W➔I➔L➔L➔ ➔h➔a➔p➔p➔e➔n➔ ➔(➔p➔r➔e➔v➔i➔e➔w➔)➔.➔ ➔a➔p➔p➔l➔y➔ ➔ ➔a➔c➔t➔u➔a➔l➔l➔y➔ ➔m➔a➔k➔e➔s➔ ➔t➔h➔e➔ ➔c➔h➔a➔n➔g➔e➔s➔.➔
➔Q➔:➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔s➔t➔a➔t➔e➔ ➔a➔n➔d➔ ➔w➔h➔y➔ ➔i➔s➔ ➔i➔t➔ ➔i➔m➔p➔o➔r➔t➔a➔n➔t➔?➔
➔S➔t➔a➔t➔e➔ ➔f➔i➔l➔e➔ ➔t➔r➔a➔c➔k➔s➔ ➔t➔h➔e➔ ➔m➔a➔p➔p➔i➔n➔g➔ ➔b➔e➔t➔w➔e➔e➔n➔ ➔y➔o➔u➔r➔ ➔c➔o➔n➔f➔i➔g➔ ➔a➔n➔d➔ ➔r➔e➔a➔l➔ ➔i➔n➔f➔r➔a➔s➔t➔r➔u➔c➔t➔u➔r➔e➔.➔ ➔W➔i➔t➔h➔o➔u➔t➔ ➔i➔t➔,➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔d➔o➔e➔s➔n➔'➔t➔ ➔k➔n➔o➔w➔
➔w➔h➔a➔t➔ ➔e➔x➔i➔s➔t➔s➔ ➔a➔n➔d➔ ➔w➔o➔u➔l➔d➔ ➔t➔r➔y➔ ➔t➔o➔ ➔r➔e➔c➔r➔e➔a➔t➔e➔ ➔e➔v➔e➔r➔y➔t➔h➔i➔n➔g➔.➔
➔Q➔:➔ ➔W➔h➔a➔t➔ ➔h➔a➔p➔p➔e➔n➔s➔ ➔i➔f➔ ➔y➔o➔u➔ ➔d➔e➔l➔e➔t➔e➔ ➔t➔h➔e➔ ➔s➔t➔a➔t➔e➔ ➔f➔i➔l➔e➔?➔
➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔l➔o➔s➔e➔s➔ ➔t➔r➔a➔c➔k➔ ➔o➔f➔ ➔e➔x➔i➔s➔t➔i➔n➔g➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔s➔.➔ ➔R➔u➔n➔n➔i➔n➔g➔ ➔a➔p➔p➔l➔y➔ ➔w➔o➔u➔l➔d➔ ➔t➔r➔y➔ ➔t➔o➔ ➔c➔r➔e➔a➔t➔e➔ ➔d➔u➔p➔l➔i➔c➔a➔t➔e➔s➔.➔ ➔Y➔o➔u➔'➔d➔ ➔n➔e➔e➔d➔ ➔t➔o➔ ➔i➔m➔p➔o➔r➔t➔
➔r➔e➔s➔o➔u➔r➔c➔e➔s➔ ➔b➔a➔c➔k➔ ➔u➔s➔i➔n➔g➔ ➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔i➔m➔p➔o➔r➔t➔ ➔.➔
➔Q➔:➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔t➔h➔e➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔c➔e➔ ➔b➔e➔t➔w➔e➔e➔n➔ ➔c➔o➔u➔n➔t➔ ➔a➔n➔d➔ ➔f➔o➔r➔_➔e➔a➔c➔h➔?➔
➔c➔o➔u➔n➔t➔ ➔ ➔c➔r➔e➔a➔t➔e➔s➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔s➔ ➔b➔y➔ ➔n➔u➔m➔b➔e➔r➔.➔ ➔f➔o➔r➔_➔e➔a➔c➔h➔ ➔ ➔c➔r➔e➔a➔t➔e➔s➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔s➔ ➔f➔r➔o➔m➔ ➔a➔ ➔m➔a➔p➔ ➔o➔r➔ ➔s➔e➔t➔ ➔—➔ ➔b➔e➔t➔t➔e➔r➔ ➔b➔e➔c➔a➔u➔s➔e➔
➔r➔e➔s➔o➔u➔r➔c➔e➔s➔ ➔h➔a➔v➔e➔ ➔m➔e➔a➔n➔i➔n➔g➔f➔u➔l➔ ➔n➔a➔m➔e➔s➔ ➔n➔o➔t➔ ➔j➔u➔s➔t➔ ➔i➔n➔d➔e➔x➔e➔s➔.➔
➔Q➔:➔ ➔H➔o➔w➔ ➔d➔o➔ ➔y➔o➔u➔ ➔m➔a➔n➔a➔g➔e➔ ➔s➔e➔c➔r➔e➔t➔s➔ ➔i➔n➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔?➔
➔U➔s➔e➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔ ➔(➔T➔F➔_➔V➔A➔R➔_➔)➔,➔ ➔m➔a➔r➔k➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔ ➔a➔s➔ ➔s➔e➔n➔s➔i➔t➔i➔v➔e➔=➔t➔r➔u➔e➔,➔ ➔u➔s➔e➔ ➔A➔W➔S➔ ➔S➔e➔c➔r➔e➔t➔s➔ ➔M➔a➔n➔a➔g➔e➔r➔ ➔o➔r➔ ➔H➔a➔s➔h➔i➔C➔o➔r➔p➔
➔V➔a➔u➔l➔t➔,➔ ➔n➔e➔v➔e➔r➔ ➔h➔a➔r➔d➔c➔o➔d➔e➔ ➔i➔n➔ ➔.➔t➔f➔ ➔f➔i➔l➔e➔s➔.➔
➔Q➔:➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔m➔o➔d➔u➔l➔e➔?➔
➔R➔e➔u➔s➔a➔b➔l➔e➔,➔ ➔s➔e➔l➔f➔-➔c➔o➔n➔t➔a➔i➔n➔e➔d➔ ➔p➔a➔c➔k➔a➔g➔e➔ ➔o➔f➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔c➔o➔d➔e➔.➔ ➔L➔i➔k➔e➔ ➔a➔ ➔f➔u➔n➔c➔t➔i➔o➔n➔ ➔i➔n➔ ➔p➔r➔o➔g➔r➔a➔m➔m➔i➔n➔g➔ ➔—➔ ➔w➔r➔i➔t➔e➔ ➔o➔n➔c➔e➔,➔ ➔u➔s➔e➔ ➔m➔a➔n➔y➔
➔t➔i➔m➔e➔s➔.➔
➔Q➔:➔ ➔H➔o➔w➔ ➔d➔o➔e➔s➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔h➔a➔n➔d➔l➔e➔ ➔d➔e➔p➔e➔n➔d➔e➔n➔c➔i➔e➔s➔?➔
➔A➔u➔t➔o➔m➔a➔t➔i➔c➔a➔l➔l➔y➔ ➔t➔h➔r➔o➔u➔g➔h➔ ➔r➔e➔s➔o➔u➔r➔c➔e➔ ➔r➔e➔f➔e➔r➔e➔n➔c➔e➔s➔ ➔(➔i➔m➔p➔l➔i➔c➔i➔t➔ ➔d➔e➔p➔e➔n➔d➔e➔n➔c➔y➔)➔.➔ ➔Y➔o➔u➔ ➔c➔a➔n➔ ➔a➔l➔s➔o➔ ➔u➔s➔e➔ ➔d➔e➔p➔e➔n➔d➔s➔_➔o➔n➔ ➔ ➔f➔o➔r➔ ➔e➔x➔p➔l➔i➔c➔i➔t➔
➔d➔e➔p➔e➔n➔d➔e➔n➔c➔y➔.➔
➔
➔
➔
➔
➔1➔7➔.➔ ➔Q➔u➔i➔c➔k➔ ➔R➔e➔f➔e➔r➔e➔n➔c➔e➔ ➔—➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔
➔#➔ ➔E➔S➔S➔E➔N➔T➔I➔A➔L➔ ➔W➔O➔R➔K➔F➔L➔O➔W➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔i➔n➔i➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔l➔w➔a➔y➔s➔ ➔f➔i➔r➔s➔t➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔f➔m➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔r➔m➔a➔t➔ ➔c➔o➔d➔e➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔v➔a➔l➔i➔d➔a➔t➔e➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔e➔c➔k➔ ➔s➔y➔n➔t➔a➔x➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔p➔l➔a➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔r➔e➔v➔i➔e➔w➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔a➔p➔p➔l➔y➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔/➔u➔p➔d➔a➔t➔e➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔d➔e➔s➔t➔r➔o➔y➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔t➔e➔a➔r➔ ➔d➔o➔w➔n➔
➔#➔ ➔S➔T➔A➔T➔E➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔s➔t➔a➔t➔e➔ ➔l➔i➔s➔t➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔s➔t➔a➔t➔e➔ ➔s➔h➔o➔w➔ ➔<➔r➔e➔s➔o➔u➔r➔c➔e➔>➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔o➔u➔t➔p➔u➔t➔
➔#➔ ➔W➔O➔R➔K➔S➔P➔A➔C➔E➔S➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔ ➔n➔e➔w➔ ➔d➔e➔v➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔ ➔s➔e➔l➔e➔c➔t➔ ➔p➔r➔o➔d➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔w➔o➔r➔k➔s➔p➔a➔c➔e➔ ➔l➔i➔s➔t➔
➔#➔ ➔I➔M➔P➔O➔R➔T➔ ➔E➔X➔I➔S➔T➔I➔N➔G➔ ➔R➔E➔S➔O➔U➔R➔C➔E➔
➔t➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔i➔m➔p➔o➔r➔t➔ ➔a➔w➔s➔_➔i➔n➔s➔t➔a➔n➔c➔e➔.➔w➔e➔b➔ ➔i➔-➔1➔2➔3➔4➔5➔6➔7➔8➔9➔0➔
➔

---

## 🚀 Modern Terraform 1.5+ & AWS Provider v5.x Best Practices

### 1. Decoupled S3 Resources (Provider v5.x)
```hcl
resource "aws_s3_bucket" "vault_storage" {
  bucket = "enterprise-cloud-vault-storage"
}

resource "aws_s3_bucket_versioning" "vault_storage_versioning" {
  bucket = aws_s3_bucket.vault_storage.id
  versioning_configuration {
    status = "Enabled"
  }
}

resource "aws_s3_bucket_server_side_encryption_configuration" "vault_storage_crypto" {
  bucket = aws_s3_bucket.vault_storage.id
  rule {
    apply_server_side_encryption_by_default {
      sse_algorithm = "AES256"
    }
  }
}
```

### 2. Declarative `import` and `moved` Blocks
```hcl
import {
  to = aws_security_group.app_sg
  id = "sg-0123456789abcdef0"
}

moved {
  from = aws_instance.web
  to   = aws_instance.api_server
}
```
