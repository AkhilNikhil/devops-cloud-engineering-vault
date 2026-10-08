# 🌿 Git Version Control: The Definitive Master Engineering Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers Git Architecture, The Three Trees (Working Dir, Staging, Repository), Git Object Model (Blobs, Trees, Commits), Merge vs Rebase, Disaster Recovery (Reflog, Detached HEAD), and Branch Governance.

---

## 📑 Table of Contents
- [What is Version Control & Why Git?](#why-git)
- [The Three Trees: Working Directory, Staging Index, Local Repository](#the-three-trees)
- [Git Internal Architecture & Object Model](#git-internals)
- [Branching & Merging: Fast-Forward vs 3-Way Merge](#branching--merging)
- [Git Merge vs Git Rebase Deep Dive](#merge-vs-rebase)
- [Emergency Recovery Playbook (git reflog, git revert, detached HEAD)](#emergency-recovery)
- [GitFlow Branch Governance & Pull Request Policies](#gitflow-governance)
- [Production Command Cheat Sheet & Interview Q&A](#command-cheatsheet--qa)

---

➔S➔E➔C➔T➔I➔O➔N➔ ➔5➔:➔ ➔G➔I➔T➔ ➔—➔ ➔C➔O➔M➔P➔L➔E➔T➔E➔ ➔G➔U➔I➔D➔E➔
➔
➔
➔
➔
➔F➔l➔o➔w➔:➔ ➔V➔C➔S➔ ➔B➔a➔s➔i➔c➔s➔ ➔→➔ ➔G➔i➔t➔ ➔B➔a➔s➔i➔c➔s➔ ➔→➔ ➔W➔o➔r➔k➔i➔n➔g➔ ➔A➔r➔e➔a➔s➔ ➔→➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔ ➔→➔ ➔B➔r➔a➔n➔c➔h➔i➔n➔g➔ ➔→➔ ➔M➔e➔r➔g➔i➔n➔g➔ ➔→➔ ➔R➔e➔m➔o➔t➔e➔ ➔R➔e➔p➔o➔s➔ ➔→➔
➔U➔n➔d➔o➔i➔n➔g➔ ➔C➔h➔a➔n➔g➔e➔s➔ ➔→➔ ➔A➔d➔v➔a➔n➔c➔e➔d➔
➔1➔.➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔V➔e➔r➔s➔i➔o➔n➔ ➔C➔o➔n➔t➔r➔o➔l➔ ➔S➔y➔s➔t➔e➔m➔ ➔(➔V➔C➔S➔)➔?➔
➔D➔e➔f➔i➔n➔i➔t➔i➔o➔n➔:➔
➔A➔ ➔V➔e➔r➔s➔i➔o➔n➔ ➔C➔o➔n➔t➔r➔o➔l➔ ➔S➔y➔s➔t➔e➔m➔ ➔t➔r➔a➔c➔k➔s➔ ➔a➔n➔d➔ ➔m➔a➔n➔a➔g➔e➔s➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔t➔o➔ ➔f➔i➔l➔e➔s➔ ➔o➔v➔e➔r➔ ➔t➔i➔m➔e➔.➔ ➔I➔t➔ ➔a➔l➔l➔o➔w➔s➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔d➔e➔v➔e➔l➔o➔p➔e➔r➔s➔ ➔t➔o➔
➔c➔o➔l➔l➔a➔b➔o➔r➔a➔t➔e➔ ➔o➔n➔ ➔t➔h➔e➔ ➔s➔a➔m➔e➔ ➔c➔o➔d➔e➔b➔a➔s➔e➔,➔ ➔k➔e➔e➔p➔ ➔h➔i➔s➔t➔o➔r➔y➔ ➔o➔f➔ ➔e➔v➔e➔r➔y➔ ➔c➔h➔a➔n➔g➔e➔,➔ ➔a➔n➔d➔ ➔r➔e➔v➔e➔r➔t➔ ➔t➔o➔ ➔a➔n➔y➔ ➔p➔r➔e➔v➔i➔o➔u➔s➔ ➔s➔t➔a➔t➔e➔.➔
➔W➔h➔y➔ ➔D➔e➔v➔O➔p➔s➔ ➔n➔e➔e➔d➔s➔ ➔V➔C➔S➔:➔
➔E➔v➔e➔r➔y➔ ➔c➔o➔d➔e➔ ➔c➔h➔a➔n➔g➔e➔ ➔i➔s➔ ➔t➔r➔a➔c➔k➔e➔d➔ ➔w➔i➔t➔h➔ ➔w➔h➔o➔ ➔m➔a➔d➔e➔ ➔i➔t➔,➔ ➔w➔h➔e➔n➔,➔ ➔a➔n➔d➔ ➔w➔h➔y➔
➔M➔u➔l➔t➔i➔p➔l➔e➔ ➔d➔e➔v➔e➔l➔o➔p➔e➔r➔s➔ ➔c➔a➔n➔ ➔w➔o➔r➔k➔ ➔o➔n➔ ➔s➔a➔m➔e➔ ➔p➔r➔o➔j➔e➔c➔t➔ ➔w➔i➔t➔h➔o➔u➔t➔ ➔o➔v➔e➔r➔w➔r➔i➔t➔i➔n➔g➔ ➔e➔a➔c➔h➔ ➔o➔t➔h➔e➔r➔'➔s➔ ➔w➔o➔r➔k➔
➔R➔o➔l➔l➔ ➔b➔a➔c➔k➔ ➔t➔o➔ ➔a➔ ➔s➔t➔a➔b➔l➔e➔ ➔v➔e➔r➔s➔i➔o➔n➔ ➔i➔f➔ ➔s➔o➔m➔e➔t➔h➔i➔n➔g➔ ➔b➔r➔e➔a➔k➔s➔
➔F➔o➔u➔n➔d➔a➔t➔i➔o➔n➔ ➔o➔f➔ ➔C➔I➔/➔C➔D➔ ➔—➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔s➔ ➔t➔r➔i➔g➔g➔e➔r➔ ➔f➔r➔o➔m➔ ➔c➔o➔d➔e➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔i➔n➔ ➔V➔C➔S➔
➔2➔.➔ ➔T➔y➔p➔e➔s➔ ➔o➔f➔ ➔V➔C➔S➔
➔A➔)➔ ➔L➔o➔c➔a➔l➔ ➔V➔C➔S➔
➔T➔r➔a➔c➔k➔s➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔o➔n➔l➔y➔ ➔o➔n➔ ➔y➔o➔u➔r➔ ➔l➔o➔c➔a➔l➔ ➔m➔a➔c➔h➔i➔n➔e➔
➔N➔o➔ ➔c➔o➔l➔l➔a➔b➔o➔r➔a➔t➔i➔o➔n➔ ➔p➔o➔s➔s➔i➔b➔l➔e➔
➔E➔x➔a➔m➔p➔l➔e➔:➔ ➔R➔C➔S➔ ➔(➔o➔l➔d➔,➔ ➔r➔a➔r➔e➔l➔y➔ ➔u➔s➔e➔d➔)➔
➔P➔r➔o➔b➔l➔e➔m➔:➔ ➔I➔f➔ ➔y➔o➔u➔r➔ ➔m➔a➔c➔h➔i➔n➔e➔ ➔d➔i➔e➔s➔,➔ ➔e➔v➔e➔r➔y➔t➔h➔i➔n➔g➔ ➔i➔s➔ ➔l➔o➔s➔t➔
➔B➔)➔ ➔C➔e➔n➔t➔r➔a➔l➔i➔z➔e➔d➔ ➔V➔C➔S➔ ➔(➔C➔V➔C➔S➔)➔
➔O➔n➔e➔ ➔c➔e➔n➔t➔r➔a➔l➔ ➔s➔e➔r➔v➔e➔r➔ ➔s➔t➔o➔r➔e➔s➔ ➔a➔l➔l➔ ➔v➔e➔r➔s➔i➔o➔n➔s➔
➔D➔e➔v➔e➔l➔o➔p➔e➔r➔s➔ ➔p➔u➔l➔l➔ ➔f➔r➔o➔m➔ ➔a➔n➔d➔ ➔p➔u➔s➔h➔ ➔t➔o➔ ➔t➔h➔a➔t➔ ➔s➔i➔n➔g➔l➔e➔ ➔s➔e➔r➔v➔e➔r➔
➔E➔x➔a➔m➔p➔l➔e➔:➔ ➔S➔V➔N➔ ➔(➔S➔u➔b➔v➔e➔r➔s➔i➔o➔n➔)➔,➔ ➔C➔V➔S➔
➔P➔r➔o➔s➔:➔ ➔S➔i➔m➔p➔l➔e➔,➔ ➔s➔i➔n➔g➔l➔e➔ ➔s➔o➔u➔r➔c➔e➔ ➔o➔f➔ ➔t➔r➔u➔t➔h➔
➔C➔o➔n➔s➔:➔ ➔S➔i➔n➔g➔l➔e➔ ➔p➔o➔i➔n➔t➔ ➔o➔f➔ ➔f➔a➔i➔l➔u➔r➔e➔ ➔—➔ ➔i➔f➔ ➔s➔e➔r➔v➔e➔r➔ ➔g➔o➔e➔s➔ ➔d➔o➔w➔n➔,➔ ➔n➔o➔ ➔o➔n➔e➔ ➔c➔a➔n➔ ➔w➔o➔r➔k➔.➔ ➔N➔o➔ ➔o➔f➔f➔l➔i➔n➔e➔ ➔w➔o➔r➔k➔.➔
➔C➔)➔ ➔D➔i➔s➔t➔r➔i➔b➔u➔t➔e➔d➔ ➔V➔C➔S➔ ➔(➔D➔V➔C➔S➔)➔
➔E➔v➔e➔r➔y➔ ➔d➔e➔v➔e➔l➔o➔p➔e➔r➔ ➔h➔a➔s➔ ➔a➔ ➔f➔u➔l➔l➔ ➔c➔o➔p➔y➔ ➔o➔f➔ ➔t➔h➔e➔ ➔r➔e➔p➔o➔s➔i➔t➔o➔r➔y➔ ➔i➔n➔c➔l➔u➔d➔i➔n➔g➔ ➔c➔o➔m➔p➔l➔e➔t➔e➔ ➔h➔i➔s➔t➔o➔r➔y➔
➔
➔
➔
➔
➔E➔x➔a➔m➔p➔l➔e➔:➔ ➔G➔i➔t➔,➔ ➔M➔e➔r➔c➔u➔r➔i➔a➔l➔
➔P➔r➔o➔s➔:➔ ➔W➔o➔r➔k➔ ➔o➔f➔f➔l➔i➔n➔e➔,➔ ➔n➔o➔ ➔s➔i➔n➔g➔l➔e➔ ➔p➔o➔i➔n➔t➔ ➔o➔f➔ ➔f➔a➔i➔l➔u➔r➔e➔,➔ ➔f➔a➔s➔t➔e➔r➔ ➔o➔p➔e➔r➔a➔t➔i➔o➔n➔s➔,➔ ➔f➔u➔l➔l➔ ➔h➔i➔s➔t➔o➔r➔y➔ ➔l➔o➔c➔a➔l➔l➔y➔
➔C➔o➔n➔s➔:➔ ➔S➔l➔i➔g➔h➔t➔l➔y➔ ➔m➔o➔r➔e➔ ➔c➔o➔m➔p➔l➔e➔x➔ ➔t➔o➔ ➔l➔e➔a➔r➔n➔
➔G➔i➔t➔ ➔i➔s➔ ➔a➔ ➔D➔i➔s➔t➔r➔i➔b➔u➔t➔e➔d➔ ➔V➔C➔S➔ ➔—➔ ➔t➔h➔i➔s➔ ➔i➔s➔ ➔w➔h➔y➔ ➔i➔t➔'➔s➔ ➔t➔h➔e➔ ➔i➔n➔d➔u➔s➔t➔r➔y➔ ➔s➔t➔a➔n➔d➔a➔r➔d➔.➔
➔3➔.➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔G➔i➔t➔?➔
➔D➔e➔f➔i➔n➔i➔t➔i➔o➔n➔:➔
➔G➔i➔t➔ ➔i➔s➔ ➔a➔ ➔f➔r➔e➔e➔,➔ ➔o➔p➔e➔n➔-➔s➔o➔u➔r➔c➔e➔ ➔D➔i➔s➔t➔r➔i➔b➔u➔t➔e➔d➔ ➔V➔e➔r➔s➔i➔o➔n➔ ➔C➔o➔n➔t➔r➔o➔l➔ ➔S➔y➔s➔t➔e➔m➔ ➔c➔r➔e➔a➔t➔e➔d➔ ➔b➔y➔ ➔L➔i➔n➔u➔s➔ ➔T➔o➔r➔v➔a➔l➔d➔s➔ ➔i➔n➔ ➔2➔0➔0➔5➔.➔ ➔I➔t➔ ➔t➔r➔a➔c➔k➔s➔
➔c➔h➔a➔n➔g➔e➔s➔ ➔i➔n➔ ➔s➔o➔u➔r➔c➔e➔ ➔c➔o➔d➔e➔,➔ ➔s➔u➔p➔p➔o➔r➔t➔s➔ ➔n➔o➔n➔-➔l➔i➔n➔e➔a➔r➔ ➔d➔e➔v➔e➔l➔o➔p➔m➔e➔n➔t➔ ➔t➔h➔r➔o➔u➔g➔h➔ ➔b➔r➔a➔n➔c➔h➔i➔n➔g➔,➔ ➔a➔n➔d➔ ➔e➔n➔a➔b➔l➔e➔s➔ ➔t➔e➔a➔m➔ ➔c➔o➔l➔l➔a➔b➔o➔r➔a➔t➔i➔o➔n➔.➔
➔K➔e➔y➔ ➔c➔o➔n➔c➔e➔p➔t➔s➔:➔
➔E➔v➔e➔r➔y➔ ➔c➔h➔a➔n➔g➔e➔ ➔i➔s➔ ➔a➔ ➔c➔o➔m➔m➔i➔t➔ ➔(➔a➔ ➔s➔n➔a➔p➔s➔h➔o➔t➔ ➔o➔f➔ ➔y➔o➔u➔r➔ ➔c➔o➔d➔e➔ ➔a➔t➔ ➔t➔h➔a➔t➔ ➔p➔o➔i➔n➔t➔)➔
➔B➔r➔a➔n➔c➔h➔e➔s➔ ➔l➔e➔t➔ ➔y➔o➔u➔ ➔w➔o➔r➔k➔ ➔o➔n➔ ➔f➔e➔a➔t➔u➔r➔e➔s➔ ➔w➔i➔t➔h➔o➔u➔t➔ ➔a➔f➔f➔e➔c➔t➔i➔n➔g➔ ➔m➔a➔i➔n➔ ➔c➔o➔d➔e➔
➔G➔i➔t➔ ➔i➔s➔ ➔l➔o➔c➔a➔l➔ ➔f➔i➔r➔s➔t➔ ➔—➔ ➔m➔o➔s➔t➔ ➔o➔p➔e➔r➔a➔t➔i➔o➔n➔s➔ ➔h➔a➔p➔p➔e➔n➔ ➔o➔n➔ ➔y➔o➔u➔r➔ ➔m➔a➔c➔h➔i➔n➔e➔ ➔w➔i➔t➔h➔o➔u➔t➔ ➔i➔n➔t➔e➔r➔n➔e➔t➔
➔4➔.➔ ➔G➔i➔t➔ ➔W➔o➔r➔k➔f➔l➔o➔w➔ ➔—➔ ➔T➔h➔e➔ ➔F➔o➔u➔r➔ ➔A➔r➔e➔a➔s➔
➔U➔n➔d➔e➔r➔s➔t➔a➔n➔d➔i➔n➔g➔ ➔t➔h➔e➔s➔e➔ ➔f➔o➔u➔r➔ ➔a➔r➔e➔a➔s➔ ➔i➔s➔ ➔t➔h➔e➔ ➔m➔o➔s➔t➔ ➔i➔m➔p➔o➔r➔t➔a➔n➔t➔ ➔c➔o➔n➔c➔e➔p➔t➔ ➔i➔n➔ ➔G➔i➔t➔:➔
➔W➔o➔r➔k➔i➔n➔g➔ ➔D➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔ ➔→➔ ➔ ➔S➔t➔a➔g➔i➔n➔g➔ ➔A➔r➔e➔a➔ ➔ ➔→➔ ➔ ➔L➔o➔c➔a➔l➔ ➔R➔e➔p➔o➔s➔i➔t➔o➔r➔y➔ ➔ ➔→➔ ➔ ➔R➔e➔m➔o➔t➔e➔ ➔R➔e➔p➔o➔s➔i➔t➔o➔r➔y➔
➔ ➔ ➔ ➔(➔y➔o➔u➔r➔ ➔f➔i➔l➔e➔s➔)➔ ➔ ➔ ➔ ➔ ➔ ➔(➔g➔i➔t➔ ➔a➔d➔d➔)➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔(➔g➔i➔t➔ ➔c➔o➔m➔m➔i➔t➔)➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔(➔g➔i➔t➔ ➔p➔u➔s➔h➔)➔
➔A➔)➔ ➔W➔o➔r➔k➔i➔n➔g➔ ➔D➔i➔r➔e➔c➔t➔o➔r➔y➔
➔W➔h➔e➔r➔e➔ ➔y➔o➔u➔ ➔a➔c➔t➔u➔a➔l➔l➔y➔ ➔w➔r➔i➔t➔e➔ ➔a➔n➔d➔ ➔e➔d➔i➔t➔ ➔y➔o➔u➔r➔ ➔f➔i➔l➔e➔s➔
➔F➔i➔l➔e➔s➔ ➔h➔e➔r➔e➔ ➔a➔r➔e➔ ➔e➔i➔t➔h➔e➔r➔ ➔t➔r➔a➔c➔k➔e➔d➔ ➔(➔G➔i➔t➔ ➔k➔n➔o➔w➔s➔ ➔a➔b➔o➔u➔t➔ ➔t➔h➔e➔m➔)➔ ➔o➔r➔ ➔u➔n➔t➔r➔a➔c➔k➔e➔d➔ ➔(➔n➔e➔w➔ ➔f➔i➔l➔e➔s➔ ➔G➔i➔t➔ ➔h➔a➔s➔n➔'➔t➔ ➔s➔e➔e➔n➔)➔
➔C➔h➔a➔n➔g➔e➔s➔ ➔h➔e➔r➔e➔ ➔a➔r➔e➔ ➔n➔o➔t➔ ➔s➔a➔v➔e➔d➔ ➔t➔o➔ ➔G➔i➔t➔ ➔y➔e➔t➔
➔B➔)➔ ➔S➔t➔a➔g➔i➔n➔g➔ ➔A➔r➔e➔a➔ ➔(➔I➔n➔d➔e➔x➔)➔
➔A➔ ➔p➔r➔e➔p➔a➔r➔a➔t➔i➔o➔n➔ ➔z➔o➔n➔e➔ ➔b➔e➔f➔o➔r➔e➔ ➔c➔o➔m➔m➔i➔t➔t➔i➔n➔g➔
➔Y➔o➔u➔ ➔c➔h➔o➔o➔s➔e➔ ➔w➔h➔i➔c➔h➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔t➔o➔ ➔i➔n➔c➔l➔u➔d➔e➔ ➔i➔n➔ ➔t➔h➔e➔ ➔n➔e➔x➔t➔ ➔c➔o➔m➔m➔i➔t➔
➔U➔s➔e➔ ➔g➔i➔t➔ ➔a➔d➔d➔ ➔ ➔t➔o➔ ➔m➔o➔v➔e➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔f➔r➔o➔m➔ ➔w➔o➔r➔k➔i➔n➔g➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔t➔o➔ ➔s➔t➔a➔g➔i➔n➔g➔ ➔a➔r➔e➔a➔
➔
➔
➔
➔
➔A➔l➔l➔o➔w➔s➔ ➔y➔o➔u➔ ➔t➔o➔ ➔c➔o➔m➔m➔i➔t➔ ➔o➔n➔l➔y➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔c➔h➔a➔n➔g➔e➔s➔,➔ ➔n➔o➔t➔ ➔e➔v➔e➔r➔y➔t➔h➔i➔n➔g➔
➔C➔)➔ ➔L➔o➔c➔a➔l➔ ➔R➔e➔p➔o➔s➔i➔t➔o➔r➔y➔
➔Y➔o➔u➔r➔ ➔l➔o➔c➔a➔l➔ ➔G➔i➔t➔ ➔d➔a➔t➔a➔b➔a➔s➔e➔ ➔s➔t➔o➔r➔e➔d➔ ➔i➔n➔ ➔t➔h➔e➔ ➔.➔g➔i➔t➔ ➔ ➔f➔o➔l➔d➔e➔r➔
➔W➔h➔e➔n➔ ➔y➔o➔u➔ ➔g➔i➔t➔ ➔c➔o➔m➔m➔i➔t➔ ➔,➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔m➔o➔v➔e➔ ➔f➔r➔o➔m➔ ➔s➔t➔a➔g➔i➔n➔g➔ ➔t➔o➔ ➔l➔o➔c➔a➔l➔ ➔r➔e➔p➔o➔
➔C➔o➔n➔t➔a➔i➔n➔s➔ ➔f➔u➔l➔l➔ ➔h➔i➔s➔t➔o➔r➔y➔ ➔o➔f➔ ➔a➔l➔l➔ ➔c➔o➔m➔m➔i➔t➔s➔
➔W➔o➔r➔k➔s➔ ➔c➔o➔m➔p➔l➔e➔t➔e➔l➔y➔ ➔o➔f➔f➔l➔i➔n➔e➔
➔D➔)➔ ➔R➔e➔m➔o➔t➔e➔ ➔R➔e➔p➔o➔s➔i➔t➔o➔r➔y➔
➔A➔ ➔r➔e➔p➔o➔s➔i➔t➔o➔r➔y➔ ➔h➔o➔s➔t➔e➔d➔ ➔o➔n➔ ➔a➔ ➔s➔e➔r➔v➔e➔r➔ ➔—➔ ➔G➔i➔t➔H➔u➔b➔,➔ ➔G➔i➔t➔L➔a➔b➔,➔ ➔B➔i➔t➔b➔u➔c➔k➔e➔t➔,➔ ➔A➔z➔u➔r➔e➔ ➔R➔e➔p➔o➔s➔
➔U➔s➔e➔ ➔g➔i➔t➔ ➔p➔u➔s➔h➔ ➔ ➔t➔o➔ ➔s➔e➔n➔d➔ ➔y➔o➔u➔r➔ ➔l➔o➔c➔a➔l➔ ➔c➔o➔m➔m➔i➔t➔s➔ ➔t➔o➔ ➔r➔e➔m➔o➔t➔e➔
➔U➔s➔e➔ ➔g➔i➔t➔ ➔p➔u➔l➔l➔ ➔ ➔t➔o➔ ➔g➔e➔t➔ ➔o➔t➔h➔e➔r➔s➔'➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔f➔r➔o➔m➔ ➔r➔e➔m➔o➔t➔e➔
➔T➔h➔e➔ ➔c➔e➔n➔t➔r➔a➔l➔ ➔c➔o➔l➔l➔a➔b➔o➔r➔a➔t➔i➔o➔n➔ ➔p➔o➔i➔n➔t➔ ➔f➔o➔r➔ ➔t➔e➔a➔m➔s➔
➔5➔.➔ ➔G➔i➔t➔ ➔S➔e➔t➔u➔p➔ ➔—➔ ➔F➔i➔r➔s➔t➔ ➔T➔i➔m➔e➔ ➔C➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔
➔#➔ ➔S➔e➔t➔ ➔y➔o➔u➔r➔ ➔i➔d➔e➔n➔t➔i➔t➔y➔ ➔(➔r➔e➔q➔u➔i➔r➔e➔d➔ ➔b➔e➔f➔o➔r➔e➔ ➔f➔i➔r➔s➔t➔ ➔c➔o➔m➔m➔i➔t➔)➔
➔g➔i➔t➔ ➔c➔o➔n➔f➔i➔g➔ ➔-➔-➔g➔l➔o➔b➔a➔l➔ ➔u➔s➔e➔r➔.➔n➔a➔m➔e➔ ➔"➔A➔k➔h➔i➔l➔ ➔B➔ ➔M➔"➔
➔g➔i➔t➔ ➔c➔o➔n➔f➔i➔g➔ ➔-➔-➔g➔l➔o➔b➔a➔l➔ ➔u➔s➔e➔r➔.➔e➔m➔a➔i➔l➔ ➔"➔a➔k➔h➔i➔l➔b➔m➔1➔3➔@➔g➔m➔a➔i➔l➔.➔c➔o➔m➔"➔
➔#➔ ➔S➔e➔t➔ ➔d➔e➔f➔a➔u➔l➔t➔ ➔e➔d➔i➔t➔o➔r➔
➔g➔i➔t➔ ➔c➔o➔n➔f➔i➔g➔ ➔-➔-➔g➔l➔o➔b➔a➔l➔ ➔c➔o➔r➔e➔.➔e➔d➔i➔t➔o➔r➔ ➔v➔i➔m➔
➔#➔ ➔C➔h➔e➔c➔k➔ ➔a➔l➔l➔ ➔c➔o➔n➔f➔i➔g➔
➔g➔i➔t➔ ➔c➔o➔n➔f➔i➔g➔ ➔-➔-➔l➔i➔s➔t➔
➔#➔ ➔I➔n➔i➔t➔i➔a➔l➔i➔z➔e➔ ➔a➔ ➔n➔e➔w➔ ➔G➔i➔t➔ ➔r➔e➔p➔o➔ ➔i➔n➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔g➔i➔t➔ ➔i➔n➔i➔t➔
➔#➔ ➔C➔l➔o➔n➔e➔ ➔a➔n➔ ➔e➔x➔i➔s➔t➔i➔n➔g➔ ➔r➔e➔m➔o➔t➔e➔ ➔r➔e➔p➔o➔ ➔t➔o➔ ➔y➔o➔u➔r➔ ➔m➔a➔c➔h➔i➔n➔e➔
➔g➔i➔t➔ ➔c➔l➔o➔n➔e➔ ➔h➔t➔t➔p➔s➔:➔/➔/➔g➔i➔t➔h➔u➔b➔.➔c➔o➔m➔/➔u➔s➔e➔r➔n➔a➔m➔e➔/➔r➔e➔p➔o➔.➔g➔i➔t➔
➔#➔ ➔C➔l➔o➔n➔e➔ ➔i➔n➔t➔o➔ ➔a➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔f➔o➔l➔d➔e➔r➔ ➔n➔a➔m➔e➔
➔g➔i➔t➔ ➔c➔l➔o➔n➔e➔ ➔h➔t➔t➔p➔s➔:➔/➔/➔g➔i➔t➔h➔u➔b➔.➔c➔o➔m➔/➔u➔s➔e➔r➔n➔a➔m➔e➔/➔r➔e➔p➔o➔.➔g➔i➔t➔ ➔m➔y➔-➔f➔o➔l➔d➔e➔r➔
➔
➔
➔
➔
➔➔ ➔➔
➔➔ ➔➔
➔6➔.➔ ➔B➔a➔s➔i➔c➔ ➔G➔i➔t➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔ ➔—➔ ➔W➔o➔r➔k➔i➔n➔g➔ ➔D➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔t➔o➔ ➔L➔o➔c➔a➔l➔ ➔R➔e➔p➔o➔
➔C➔h➔e➔c➔k➔i➔n➔g➔ ➔S➔t➔a➔t➔u➔s➔
➔g➔i➔t➔ ➔s➔t➔a➔t➔u➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔e➔ ➔w➔h➔i➔c➔h➔ ➔f➔i➔l➔e➔s➔ ➔a➔r➔e➔ ➔m➔o➔d➔i➔f➔i➔e➔d➔,➔ ➔s➔t➔a➔g➔e➔d➔,➔ ➔o➔r➔ ➔u➔n➔t➔r➔a➔c➔k➔e➔d➔
➔g➔i➔t➔ ➔s➔t➔a➔t➔u➔s➔ ➔-➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔r➔t➔ ➔s➔t➔a➔t➔u➔s➔ ➔v➔i➔e➔w➔
➔T➔r➔a➔c➔k➔i➔n➔g➔ ➔F➔i➔l➔e➔s➔ ➔—➔ ➔g➔i➔t➔ ➔a➔d➔d➔ ➔(➔W➔o➔r➔k➔i➔n➔g➔ ➔D➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔→➔ ➔S➔t➔a➔g➔i➔n➔g➔ ➔A➔r➔e➔a➔)➔
➔g➔i➔t➔ ➔a➔d➔d➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔t➔a➔g➔e➔ ➔a➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔f➔i➔l➔e➔
➔g➔i➔t➔ ➔a➔d➔d➔ ➔.➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔t➔a➔g➔e➔ ➔A➔L➔L➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔i➔n➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔g➔i➔t➔ ➔a➔d➔d➔ ➔*➔.➔j➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔t➔a➔g➔e➔ ➔a➔l➔l➔ ➔J➔S➔ ➔f➔i➔l➔e➔s➔
➔g➔i➔t➔ ➔a➔d➔d➔ ➔s➔r➔c➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔t➔a➔g➔e➔ ➔a➔l➔l➔ ➔f➔i➔l➔e➔s➔ ➔i➔n➔ ➔s➔r➔c➔ ➔f➔o➔l➔d➔e➔r➔
➔g➔i➔t➔ ➔a➔d➔d➔ ➔-➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔i➔n➔t➔e➔r➔a➔c➔t➔i➔v➔e➔l➔y➔ ➔c➔h➔o➔o➔s➔e➔ ➔w➔h➔i➔c➔h➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔t➔o➔ ➔s➔t➔a➔g➔e➔ ➔(➔p➔a➔t➔c➔h➔ ➔m➔o➔d➔
➔C➔o➔m➔m➔i➔t➔t➔i➔n➔g➔ ➔—➔ ➔g➔i➔t➔ ➔c➔o➔m➔m➔i➔t➔ ➔(➔S➔t➔a➔g➔i➔n➔g➔ ➔A➔r➔e➔a➔ ➔→➔ ➔L➔o➔c➔a➔l➔ ➔R➔e➔p➔o➔)➔
➔g➔i➔t➔ ➔c➔o➔m➔m➔i➔t➔ ➔-➔m➔ ➔"➔A➔d➔d➔ ➔l➔o➔g➔i➔n➔ ➔f➔e➔a➔t➔u➔r➔e➔"➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔m➔m➔i➔t➔ ➔w➔i➔t➔h➔ ➔m➔e➔s➔s➔a➔g➔e➔
➔g➔i➔t➔ ➔c➔o➔m➔m➔i➔t➔ ➔-➔a➔m➔ ➔"➔F➔i➔x➔ ➔b➔u➔g➔"➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔d➔d➔ ➔+➔ ➔c➔o➔m➔m➔i➔t➔ ➔t➔r➔a➔c➔k➔e➔d➔ ➔f➔i➔l➔e➔s➔ ➔i➔n➔ ➔o➔n➔e➔ ➔s➔t➔e➔p➔
➔g➔i➔t➔ ➔c➔o➔m➔m➔i➔t➔ ➔-➔-➔a➔m➔e➔n➔d➔ ➔-➔m➔ ➔"➔N➔e➔w➔ ➔m➔e➔s➔s➔a➔g➔e➔"➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔x➔ ➔l➔a➔s➔t➔ ➔c➔o➔m➔m➔i➔t➔ ➔m➔e➔s➔s➔a➔g➔e➔ ➔(➔b➔e➔f➔o➔r➔e➔ ➔p➔u➔s➔h➔)➔
➔g➔i➔t➔ ➔c➔o➔m➔m➔i➔t➔ ➔-➔-➔a➔m➔e➔n➔d➔ ➔-➔-➔n➔o➔-➔e➔d➔i➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔d➔d➔ ➔f➔o➔r➔g➔o➔t➔t➔e➔n➔ ➔f➔i➔l➔e➔ ➔t➔o➔ ➔l➔a➔s➔t➔ ➔c➔o➔m➔m➔i➔t➔
➔V➔i➔e➔w➔i➔n➔g➔ ➔H➔i➔s➔t➔o➔r➔y➔
➔g➔i➔t➔ ➔l➔o➔g➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔u➔l➔l➔ ➔c➔o➔m➔m➔i➔t➔ ➔h➔i➔s➔t➔o➔r➔y➔
➔g➔i➔t➔ ➔l➔o➔g➔ ➔-➔-➔o➔n➔e➔l➔i➔n➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔m➔p➔a➔c➔t➔ ➔o➔n➔e➔-➔l➔i➔n➔e➔ ➔v➔i➔e➔w➔
➔g➔i➔t➔ ➔l➔o➔g➔ ➔-➔-➔o➔n➔e➔l➔i➔n➔e➔ ➔-➔-➔g➔r➔a➔p➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔v➔i➔s➔u➔a➔l➔ ➔b➔r➔a➔n➔c➔h➔ ➔g➔r➔a➔p➔h➔
➔g➔i➔t➔ ➔l➔o➔g➔ ➔-➔-➔o➔n➔e➔l➔i➔n➔e➔ ➔-➔5➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔a➔s➔t➔ ➔5➔ ➔c➔o➔m➔m➔i➔t➔s➔
➔g➔i➔t➔ ➔l➔o➔g➔ ➔-➔-➔a➔u➔t➔h➔o➔r➔=➔"➔A➔k➔h➔i➔l➔"➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔m➔m➔i➔t➔s➔ ➔b➔y➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔a➔u➔t➔h➔o➔r➔
➔g➔i➔t➔ ➔l➔o➔g➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔h➔i➔s➔t➔o➔r➔y➔ ➔o➔f➔ ➔a➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔f➔i➔l➔e➔
➔g➔i➔t➔ ➔s➔h➔o➔w➔ ➔<➔c➔o➔m➔m➔i➔t➔-➔i➔d➔>➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔d➔e➔t➔a➔i➔l➔s➔ ➔o➔f➔ ➔a➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔c➔o➔m➔m➔i➔t➔
➔V➔i➔e➔w➔i➔n➔g➔ ➔D➔i➔f➔f➔e➔r➔e➔n➔c➔e➔s➔
➔g➔i➔t➔ ➔d➔i➔f➔f➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔i➔n➔ ➔w➔o➔r➔k➔i➔n➔g➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔(➔n➔o➔t➔ ➔s➔t➔a➔g➔e➔d➔)➔
➔g➔i➔t➔ ➔d➔i➔f➔f➔ ➔-➔-➔s➔t➔a➔g➔e➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔i➔n➔ ➔s➔t➔a➔g➔i➔n➔g➔ ➔a➔r➔e➔a➔ ➔(➔r➔e➔a➔d➔y➔ ➔t➔o➔ ➔c➔o➔m➔m➔i➔t➔)➔
➔
➔
➔
➔
➔g➔i➔t➔ ➔d➔i➔f➔f➔ ➔m➔a➔i➔n➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔b➔r➔a➔n➔c➔h➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔m➔p➔a➔r➔e➔ ➔t➔w➔o➔ ➔b➔r➔a➔n➔c➔h➔e➔s➔
➔g➔i➔t➔ ➔d➔i➔f➔f➔ ➔<➔c➔o➔m➔m➔i➔t➔1➔>➔ ➔<➔c➔o➔m➔m➔i➔t➔2➔>➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔m➔p➔a➔r➔e➔ ➔t➔w➔o➔ ➔c➔o➔m➔m➔i➔t➔s➔
➔7➔.➔ ➔B➔r➔a➔n➔c➔h➔i➔n➔g➔ ➔—➔ ➔W➔o➔r➔k➔i➔n➔g➔ ➔i➔n➔ ➔I➔s➔o➔l➔a➔t➔i➔o➔n➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔ ➔B➔r➔a➔n➔c➔h➔?➔
➔A➔ ➔b➔r➔a➔n➔c➔h➔ ➔i➔s➔ ➔a➔n➔ ➔i➔n➔d➔e➔p➔e➔n➔d➔e➔n➔t➔ ➔l➔i➔n➔e➔ ➔o➔f➔ ➔d➔e➔v➔e➔l➔o➔p➔m➔e➔n➔t➔.➔ ➔Y➔o➔u➔ ➔c➔r➔e➔a➔t➔e➔ ➔a➔ ➔b➔r➔a➔n➔c➔h➔ ➔t➔o➔ ➔w➔o➔r➔k➔ ➔o➔n➔ ➔a➔ ➔f➔e➔a➔t➔u➔r➔e➔ ➔o➔r➔ ➔b➔u➔g➔ ➔f➔i➔x➔ ➔w➔i➔t➔h➔o➔u➔t➔
➔a➔f➔f➔e➔c➔t➔i➔n➔g➔ ➔t➔h➔e➔ ➔m➔a➔i➔n➔ ➔c➔o➔d➔e➔b➔a➔s➔e➔.➔ ➔W➔h➔e➔n➔ ➔d➔o➔n➔e➔,➔ ➔y➔o➔u➔ ➔m➔e➔r➔g➔e➔ ➔i➔t➔ ➔b➔a➔c➔k➔.➔
➔D➔e➔f➔a➔u➔l➔t➔ ➔b➔r➔a➔n➔c➔h➔:➔ ➔m➔a➔i➔n➔ ➔ ➔o➔r➔ ➔m➔a➔s➔t➔e➔r➔
➔B➔r➔a➔n➔c➔h➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔
➔#➔ ➔V➔i➔e➔w➔ ➔b➔r➔a➔n➔c➔h➔e➔s➔
➔g➔i➔t➔ ➔b➔r➔a➔n➔c➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔l➔o➔c➔a➔l➔ ➔b➔r➔a➔n➔c➔h➔e➔s➔
➔g➔i➔t➔ ➔b➔r➔a➔n➔c➔h➔ ➔-➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔r➔e➔m➔o➔t➔e➔ ➔b➔r➔a➔n➔c➔h➔e➔s➔
➔g➔i➔t➔ ➔b➔r➔a➔n➔c➔h➔ ➔-➔a➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔a➔l➔l➔ ➔b➔r➔a➔n➔c➔h➔e➔s➔ ➔(➔l➔o➔c➔a➔l➔ ➔+➔ ➔r➔e➔m➔o➔t➔e➔)➔
➔#➔ ➔C➔r➔e➔a➔t➔e➔ ➔b➔r➔a➔n➔c➔h➔
➔g➔i➔t➔ ➔b➔r➔a➔n➔c➔h➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔l➔o➔g➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔n➔e➔w➔ ➔b➔r➔a➔n➔c➔h➔
➔g➔i➔t➔ ➔c➔h➔e➔c➔k➔o➔u➔t➔ ➔-➔b➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔l➔o➔g➔i➔n➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔A➔N➔D➔ ➔s➔w➔i➔t➔c➔h➔ ➔t➔o➔ ➔n➔e➔w➔ ➔b➔r➔a➔n➔c➔h➔ ➔(➔o➔l➔d➔ ➔w➔a➔y➔)➔
➔g➔i➔t➔ ➔s➔w➔i➔t➔c➔h➔ ➔-➔c➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔l➔o➔g➔i➔n➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔A➔N➔D➔ ➔s➔w➔i➔t➔c➔h➔ ➔t➔o➔ ➔n➔e➔w➔ ➔b➔r➔a➔n➔c➔h➔ ➔(➔n➔e➔w➔ ➔w➔a➔y➔)➔
➔#➔ ➔S➔w➔i➔t➔c➔h➔ ➔b➔r➔a➔n➔c➔h➔
➔g➔i➔t➔ ➔c➔h➔e➔c➔k➔o➔u➔t➔ ➔m➔a➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔w➔i➔t➔c➔h➔ ➔t➔o➔ ➔m➔a➔i➔n➔ ➔b➔r➔a➔n➔c➔h➔ ➔(➔o➔l➔d➔ ➔w➔a➔y➔)➔
➔g➔i➔t➔ ➔s➔w➔i➔t➔c➔h➔ ➔m➔a➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔w➔i➔t➔c➔h➔ ➔t➔o➔ ➔m➔a➔i➔n➔ ➔b➔r➔a➔n➔c➔h➔ ➔(➔n➔e➔w➔ ➔w➔a➔y➔)➔
➔#➔ ➔R➔e➔n➔a➔m➔e➔ ➔b➔r➔a➔n➔c➔h➔
➔g➔i➔t➔ ➔b➔r➔a➔n➔c➔h➔ ➔-➔m➔ ➔o➔l➔d➔-➔n➔a➔m➔e➔ ➔n➔e➔w➔-➔n➔a➔m➔e➔
➔#➔ ➔D➔e➔l➔e➔t➔e➔ ➔b➔r➔a➔n➔c➔h➔
➔g➔i➔t➔ ➔b➔r➔a➔n➔c➔h➔ ➔-➔d➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔l➔o➔g➔i➔n➔ ➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔b➔r➔a➔n➔c➔h➔ ➔(➔s➔a➔f➔e➔ ➔—➔ ➔o➔n➔l➔y➔ ➔i➔f➔ ➔m➔e➔r➔g➔e➔d➔)➔
➔g➔i➔t➔ ➔b➔r➔a➔n➔c➔h➔ ➔-➔D➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔l➔o➔g➔i➔n➔ ➔ ➔ ➔#➔ ➔f➔o➔r➔c➔e➔ ➔d➔e➔l➔e➔t➔e➔ ➔b➔r➔a➔n➔c➔h➔ ➔(➔e➔v➔e➔n➔ ➔i➔f➔ ➔n➔o➔t➔ ➔m➔e➔r➔g➔e➔d➔)➔
➔#➔ ➔D➔e➔l➔e➔t➔e➔ ➔r➔e➔m➔o➔t➔e➔ ➔b➔r➔a➔n➔c➔h➔
➔g➔i➔t➔ ➔p➔u➔s➔h➔ ➔o➔r➔i➔g➔i➔n➔ ➔-➔-➔d➔e➔l➔e➔t➔e➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔l➔o➔g➔i➔n➔
➔B➔r➔a➔n➔c➔h➔ ➔W➔o➔r➔k➔f➔l➔o➔w➔ ➔E➔x➔a➔m➔p➔l➔e➔
➔#➔ ➔1➔.➔ ➔C➔r➔e➔a➔t➔e➔ ➔f➔e➔a➔t➔u➔r➔e➔ ➔b➔r➔a➔n➔c➔h➔ ➔f➔r➔o➔m➔ ➔m➔a➔i➔n➔
➔g➔i➔t➔ ➔s➔w➔i➔t➔c➔h➔ ➔m➔a➔i➔n➔
➔
➔
➔
➔
➔g➔i➔t➔ ➔p➔u➔l➔l➔ ➔o➔r➔i➔g➔i➔n➔ ➔m➔a➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔m➔a➔k➔e➔ ➔s➔u➔r➔e➔ ➔m➔a➔i➔n➔ ➔i➔s➔ ➔u➔p➔ ➔t➔o➔ ➔d➔a➔t➔e➔
➔g➔i➔t➔ ➔s➔w➔i➔t➔c➔h➔ ➔-➔c➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔l➔o➔g➔i➔n➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔f➔e➔a➔t➔u➔r➔e➔ ➔b➔r➔a➔n➔c➔h➔
➔#➔ ➔2➔.➔ ➔W➔o➔r➔k➔ ➔o➔n➔ ➔f➔e➔a➔t➔u➔r➔e➔
➔#➔ ➔.➔.➔.➔ ➔e➔d➔i➔t➔ ➔f➔i➔l➔e➔s➔ ➔.➔.➔.➔
➔g➔i➔t➔ ➔a➔d➔d➔ ➔.➔
➔g➔i➔t➔ ➔c➔o➔m➔m➔i➔t➔ ➔-➔m➔ ➔"➔A➔d➔d➔ ➔l➔o➔g➔i➔n➔ ➔p➔a➔g➔e➔"➔
➔g➔i➔t➔ ➔c➔o➔m➔m➔i➔t➔ ➔-➔m➔ ➔"➔A➔d➔d➔ ➔l➔o➔g➔i➔n➔ ➔A➔P➔I➔"➔
➔#➔ ➔3➔.➔ ➔P➔u➔s➔h➔ ➔f➔e➔a➔t➔u➔r➔e➔ ➔b➔r➔a➔n➔c➔h➔ ➔t➔o➔ ➔r➔e➔m➔o➔t➔e➔
➔g➔i➔t➔ ➔p➔u➔s➔h➔ ➔o➔r➔i➔g➔i➔n➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔l➔o➔g➔i➔n➔
➔#➔ ➔4➔.➔ ➔C➔r➔e➔a➔t➔e➔ ➔P➔u➔l➔l➔ ➔R➔e➔q➔u➔e➔s➔t➔ ➔o➔n➔ ➔G➔i➔t➔H➔u➔b➔/➔G➔i➔t➔L➔a➔b➔
➔#➔ ➔5➔.➔ ➔A➔f➔t➔e➔r➔ ➔r➔e➔v➔i➔e➔w➔,➔ ➔m➔e➔r➔g➔e➔ ➔t➔o➔ ➔m➔a➔i➔n➔
➔8➔.➔ ➔M➔e➔r➔g➔i➔n➔g➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔M➔e➔r➔g➔i➔n➔g➔?➔
➔M➔e➔r➔g➔i➔n➔g➔ ➔c➔o➔m➔b➔i➔n➔e➔s➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔f➔r➔o➔m➔ ➔o➔n➔e➔ ➔b➔r➔a➔n➔c➔h➔ ➔i➔n➔t➔o➔ ➔a➔n➔o➔t➔h➔e➔r➔.➔ ➔Y➔o➔u➔ ➔t➔y➔p➔i➔c➔a➔l➔l➔y➔ ➔m➔e➔r➔g➔e➔ ➔a➔ ➔f➔e➔a➔t➔u➔r➔e➔ ➔b➔r➔a➔n➔c➔h➔ ➔i➔n➔t➔o➔ ➔m➔a➔i➔n➔ ➔w➔h➔e➔n➔
➔t➔h➔e➔ ➔f➔e➔a➔t➔u➔r➔e➔ ➔i➔s➔ ➔c➔o➔m➔p➔l➔e➔t➔e➔.➔
➔T➔y➔p➔e➔s➔ ➔o➔f➔ ➔M➔e➔r➔g➔e➔s➔
➔A➔)➔ ➔F➔a➔s➔t➔-➔F➔o➔r➔w➔a➔r➔d➔ ➔M➔e➔r➔g➔e➔
➔H➔a➔p➔p➔e➔n➔s➔ ➔w➔h➔e➔n➔ ➔t➔h➔e➔ ➔t➔a➔r➔g➔e➔t➔ ➔b➔r➔a➔n➔c➔h➔ ➔h➔a➔s➔ ➔n➔o➔ ➔n➔e➔w➔ ➔c➔o➔m➔m➔i➔t➔s➔ ➔s➔i➔n➔c➔e➔ ➔t➔h➔e➔ ➔f➔e➔a➔t➔u➔r➔e➔ ➔b➔r➔a➔n➔c➔h➔ ➔w➔a➔s➔ ➔c➔r➔e➔a➔t➔e➔d➔.➔ ➔G➔i➔t➔ ➔s➔i➔m➔p➔l➔y➔ ➔m➔o➔v➔e➔s➔
➔t➔h➔e➔ ➔p➔o➔i➔n➔t➔e➔r➔ ➔f➔o➔r➔w➔a➔r➔d➔.➔ ➔N➔o➔ ➔m➔e➔r➔g➔e➔ ➔c➔o➔m➔m➔i➔t➔ ➔c➔r➔e➔a➔t➔e➔d➔.➔ ➔C➔l➔e➔a➔n➔,➔ ➔l➔i➔n➔e➔a➔r➔ ➔h➔i➔s➔t➔o➔r➔y➔.➔
➔g➔i➔t➔ ➔s➔w➔i➔t➔c➔h➔ ➔m➔a➔i➔n➔
➔g➔i➔t➔ ➔m➔e➔r➔g➔e➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔l➔o➔g➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔a➔s➔t➔-➔f➔o➔r➔w➔a➔r➔d➔ ➔i➔f➔ ➔p➔o➔s➔s➔i➔b➔l➔e➔
➔B➔e➔f➔o➔r➔e➔:➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔A➔f➔t➔e➔r➔:➔
➔m➔a➔i➔n➔:➔ ➔A➔-➔B➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔m➔a➔i➔n➔:➔ ➔A➔-➔B➔-➔C➔-➔D➔
➔f➔e➔a➔t➔u➔r➔e➔:➔ ➔ ➔ ➔C➔-➔D➔
➔B➔)➔ ➔T➔h➔r➔e➔e➔-➔W➔a➔y➔ ➔M➔e➔r➔g➔e➔ ➔(➔2➔-➔W➔a➔y➔ ➔M➔e➔r➔g➔e➔ ➔/➔ ➔R➔e➔c➔u➔r➔s➔i➔v➔e➔ ➔M➔e➔r➔g➔e➔)➔
➔H➔a➔p➔p➔e➔n➔s➔ ➔w➔h➔e➔n➔ ➔b➔o➔t➔h➔ ➔b➔r➔a➔n➔c➔h➔e➔s➔ ➔h➔a➔v➔e➔ ➔d➔i➔v➔e➔r➔g➔e➔d➔ ➔—➔ ➔b➔o➔t➔h➔ ➔h➔a➔v➔e➔ ➔n➔e➔w➔ ➔c➔o➔m➔m➔i➔t➔s➔.➔ ➔G➔i➔t➔ ➔f➔i➔n➔d➔s➔ ➔t➔h➔e➔ ➔c➔o➔m➔m➔o➔n➔ ➔a➔n➔c➔e➔s➔t➔o➔r➔
➔c➔o➔m➔m➔i➔t➔ ➔a➔n➔d➔ ➔c➔r➔e➔a➔t➔e➔s➔ ➔a➔ ➔n➔e➔w➔ ➔m➔e➔r➔g➔e➔ ➔c➔o➔m➔m➔i➔t➔ ➔t➔h➔a➔t➔ ➔c➔o➔m➔b➔i➔n➔e➔s➔ ➔b➔o➔t➔h➔.➔
➔
➔
➔
➔
➔➔ ➔➔
➔g➔i➔t➔ ➔s➔w➔i➔t➔c➔h➔ ➔m➔a➔i➔n➔
➔g➔i➔t➔ ➔m➔e➔r➔g➔e➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔l➔o➔g➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔s➔ ➔a➔ ➔m➔e➔r➔g➔e➔ ➔c➔o➔m➔m➔i➔t➔
➔g➔i➔t➔ ➔m➔e➔r➔g➔e➔ ➔-➔-➔n➔o➔-➔f➔f➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔l➔o➔g➔i➔n➔ ➔ ➔#➔ ➔f➔o➔r➔c➔e➔ ➔m➔e➔r➔g➔e➔ ➔c➔o➔m➔m➔i➔t➔ ➔e➔v➔e➔n➔ ➔i➔f➔ ➔f➔a➔s➔t➔-➔f➔o➔r➔w➔a➔r➔d➔ ➔p➔o➔s➔s➔i➔b➔l➔e➔
➔B➔e➔f➔o➔r➔e➔:➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔A➔f➔t➔e➔r➔:➔
➔m➔a➔i➔n➔:➔ ➔A➔-➔B➔-➔E➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔m➔a➔i➔n➔:➔ ➔A➔-➔B➔-➔E➔-➔-➔-➔M➔ ➔ ➔(➔M➔ ➔=➔ ➔m➔e➔r➔g➔e➔ ➔c➔o➔m➔m➔i➔t➔)➔
➔f➔e➔a➔t➔u➔r➔e➔:➔ ➔ ➔ ➔C➔-➔D➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔\➔ ➔ ➔ ➔C➔-➔D➔-➔/➔
➔C➔)➔ ➔S➔q➔u➔a➔s➔h➔ ➔M➔e➔r➔g➔e➔
➔C➔o➔m➔b➔i➔n➔e➔s➔ ➔a➔l➔l➔ ➔f➔e➔a➔t➔u➔r➔e➔ ➔b➔r➔a➔n➔c➔h➔ ➔c➔o➔m➔m➔i➔t➔s➔ ➔i➔n➔t➔o➔ ➔a➔ ➔s➔i➔n➔g➔l➔e➔ ➔c➔o➔m➔m➔i➔t➔ ➔o➔n➔ ➔m➔a➔i➔n➔.➔ ➔K➔e➔e➔p➔s➔ ➔h➔i➔s➔t➔o➔r➔y➔ ➔c➔l➔e➔a➔n➔.➔
➔g➔i➔t➔ ➔m➔e➔r➔g➔e➔ ➔-➔-➔s➔q➔u➔a➔s➔h➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔l➔o➔g➔i➔n➔
➔g➔i➔t➔ ➔c➔o➔m➔m➔i➔t➔ ➔-➔m➔ ➔"➔A➔d➔d➔ ➔l➔o➔g➔i➔n➔ ➔f➔e➔a➔t➔u➔r➔e➔"➔ ➔ ➔ ➔#➔ ➔o➔n➔e➔ ➔c➔l➔e➔a➔n➔ ➔c➔o➔m➔m➔i➔t➔
➔9➔.➔ ➔M➔e➔r➔g➔e➔ ➔C➔o➔n➔f➔l➔i➔c➔t➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔ ➔M➔e➔r➔g➔e➔ ➔C➔o➔n➔f➔l➔i➔c➔t➔?➔
➔A➔ ➔m➔e➔r➔g➔e➔ ➔c➔o➔n➔f➔l➔i➔c➔t➔ ➔h➔a➔p➔p➔e➔n➔s➔ ➔w➔h➔e➔n➔ ➔t➔w➔o➔ ➔b➔r➔a➔n➔c➔h➔e➔s➔ ➔m➔o➔d➔i➔f➔y➔ ➔t➔h➔e➔ ➔s➔a➔m➔e➔ ➔l➔i➔n➔e➔ ➔o➔f➔ ➔t➔h➔e➔ ➔s➔a➔m➔e➔ ➔f➔i➔l➔e➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔t➔l➔y➔.➔ ➔G➔i➔t➔ ➔c➔a➔n➔'➔t➔ ➔d➔e➔c➔i➔d➔e➔
➔w➔h➔i➔c➔h➔ ➔c➔h➔a➔n➔g➔e➔ ➔t➔o➔ ➔k➔e➔e➔p➔,➔ ➔s➔o➔ ➔i➔t➔ ➔a➔s➔k➔s➔ ➔y➔o➔u➔ ➔t➔o➔ ➔r➔e➔s➔o➔l➔v➔e➔ ➔i➔t➔ ➔m➔a➔n➔u➔a➔l➔l➔y➔.➔
➔W➔h➔e➔n➔ ➔d➔o➔e➔s➔ ➔i➔t➔ ➔h➔a➔p➔p➔e➔n➔?➔
➔T➔w➔o➔ ➔d➔e➔v➔e➔l➔o➔p➔e➔r➔s➔ ➔e➔d➔i➔t➔ ➔t➔h➔e➔ ➔s➔a➔m➔e➔ ➔l➔i➔n➔e➔ ➔i➔n➔ ➔t➔h➔e➔ ➔s➔a➔m➔e➔ ➔f➔i➔l➔e➔
➔O➔n➔e➔ ➔d➔e➔v➔e➔l➔o➔p➔e➔r➔ ➔d➔e➔l➔e➔t➔e➔s➔ ➔a➔ ➔f➔i➔l➔e➔ ➔a➔n➔o➔t➔h➔e➔r➔ ➔d➔e➔v➔e➔l➔o➔p➔e➔r➔ ➔m➔o➔d➔i➔f➔i➔e➔d➔
➔B➔o➔t➔h➔ ➔b➔r➔a➔n➔c➔h➔e➔s➔ ➔r➔e➔n➔a➔m➔e➔ ➔t➔h➔e➔ ➔s➔a➔m➔e➔ ➔f➔i➔l➔e➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔t➔l➔y➔
➔H➔o➔w➔ ➔t➔o➔ ➔R➔e➔s➔o➔l➔v➔e➔ ➔a➔ ➔M➔e➔r➔g➔e➔ ➔C➔o➔n➔f➔l➔i➔c➔t➔
➔#➔ ➔S➔t➔e➔p➔ ➔1➔:➔ ➔T➔r➔y➔ ➔t➔o➔ ➔m➔e➔r➔g➔e➔
➔g➔i➔t➔ ➔m➔e➔r➔g➔e➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔l➔o➔g➔i➔n➔
➔#➔ ➔O➔U➔T➔P➔U➔T➔:➔ ➔C➔O➔N➔F➔L➔I➔C➔T➔ ➔(➔c➔o➔n➔t➔e➔n➔t➔)➔:➔ ➔M➔e➔r➔g➔e➔ ➔c➔o➔n➔f➔l➔i➔c➔t➔ ➔i➔n➔ ➔a➔p➔p➔.➔j➔s➔
➔#➔ ➔S➔t➔e➔p➔ ➔2➔:➔ ➔O➔p➔e➔n➔ ➔t➔h➔e➔ ➔c➔o➔n➔f➔l➔i➔c➔t➔e➔d➔ ➔f➔i➔l➔e➔ ➔—➔ ➔G➔i➔t➔ ➔m➔a➔r➔k➔s➔ ➔c➔o➔n➔f➔l➔i➔c➔t➔s➔ ➔l➔i➔k➔e➔ ➔t➔h➔i➔s➔:➔
➔<➔<➔<➔<➔<➔<➔<➔ ➔H➔E➔A➔D➔ ➔(➔y➔o➔u➔r➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔b➔r➔a➔n➔c➔h➔ ➔-➔ ➔m➔a➔i➔n➔)➔
➔c➔o➔n➔s➔t➔ ➔p➔o➔r➔t➔ ➔=➔ ➔3➔0➔0➔0➔;➔
➔=➔=➔=➔=➔=➔=➔=➔
➔c➔o➔n➔s➔t➔ ➔p➔o➔r➔t➔ ➔=➔ ➔8➔0➔8➔0➔;➔
➔
➔
➔
➔
➔>➔>➔>➔>➔>➔>➔>➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔l➔o➔g➔i➔n➔ ➔(➔i➔n➔c➔o➔m➔i➔n➔g➔ ➔b➔r➔a➔n➔c➔h➔)➔
➔#➔ ➔S➔t➔e➔p➔ ➔3➔:➔ ➔M➔a➔n➔u➔a➔l➔l➔y➔ ➔e➔d➔i➔t➔ ➔t➔h➔e➔ ➔f➔i➔l➔e➔ ➔t➔o➔ ➔k➔e➔e➔p➔ ➔w➔h➔a➔t➔ ➔y➔o➔u➔ ➔w➔a➔n➔t➔:➔
➔c➔o➔n➔s➔t➔ ➔p➔o➔r➔t➔ ➔=➔ ➔3➔0➔0➔0➔;➔ ➔ ➔ ➔#➔ ➔k➔e➔e➔p➔ ➔m➔a➔i➔n➔'➔s➔ ➔v➔e➔r➔s➔i➔o➔n➔
➔#➔ ➔O➔R➔
➔c➔o➔n➔s➔t➔ ➔p➔o➔r➔t➔ ➔=➔ ➔8➔0➔8➔0➔;➔ ➔ ➔ ➔#➔ ➔k➔e➔e➔p➔ ➔f➔e➔a➔t➔u➔r➔e➔'➔s➔ ➔v➔e➔r➔s➔i➔o➔n➔
➔#➔ ➔O➔R➔ ➔c➔o➔m➔b➔i➔n➔e➔ ➔b➔o➔t➔h➔ ➔i➔f➔ ➔n➔e➔e➔d➔e➔d➔
➔#➔ ➔S➔t➔e➔p➔ ➔4➔:➔ ➔R➔e➔m➔o➔v➔e➔ ➔t➔h➔e➔ ➔c➔o➔n➔f➔l➔i➔c➔t➔ ➔m➔a➔r➔k➔e➔r➔s➔ ➔<➔<➔<➔<➔<➔<➔<➔,➔ ➔=➔=➔=➔=➔=➔=➔=➔,➔ ➔>➔>➔>➔>➔>➔>➔>➔
➔#➔ ➔S➔t➔e➔p➔ ➔5➔:➔ ➔S➔t➔a➔g➔e➔ ➔t➔h➔e➔ ➔r➔e➔s➔o➔l➔v➔e➔d➔ ➔f➔i➔l➔e➔
➔g➔i➔t➔ ➔a➔d➔d➔ ➔a➔p➔p➔.➔j➔s➔
➔#➔ ➔S➔t➔e➔p➔ ➔6➔:➔ ➔C➔o➔m➔p➔l➔e➔t➔e➔ ➔t➔h➔e➔ ➔m➔e➔r➔g➔e➔
➔g➔i➔t➔ ➔c➔o➔m➔m➔i➔t➔ ➔-➔m➔ ➔"➔M➔e➔r➔g➔e➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔l➔o➔g➔i➔n➔ ➔—➔ ➔r➔e➔s➔o➔l➔v➔e➔d➔ ➔p➔o➔r➔t➔ ➔c➔o➔n➔f➔l➔i➔c➔t➔"➔
➔#➔ ➔T➔o➔ ➔a➔b➔o➔r➔t➔ ➔a➔ ➔m➔e➔r➔g➔e➔ ➔a➔n➔d➔ ➔g➔o➔ ➔b➔a➔c➔k➔ ➔t➔o➔ ➔b➔e➔f➔o➔r➔e➔
➔g➔i➔t➔ ➔m➔e➔r➔g➔e➔ ➔-➔-➔a➔b➔o➔r➔t➔
➔1➔0➔.➔ ➔C➔o➔n➔n➔e➔c➔t➔i➔n➔g➔ ➔t➔o➔ ➔R➔e➔m➔o➔t➔e➔ ➔R➔e➔p➔o➔s➔i➔t➔o➔r➔y➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔ ➔R➔e➔m➔o➔t➔e➔?➔
➔A➔ ➔r➔e➔m➔o➔t➔e➔ ➔i➔s➔ ➔a➔ ➔v➔e➔r➔s➔i➔o➔n➔ ➔o➔f➔ ➔y➔o➔u➔r➔ ➔r➔e➔p➔o➔s➔i➔t➔o➔r➔y➔ ➔h➔o➔s➔t➔e➔d➔ ➔o➔n➔ ➔a➔ ➔s➔e➔r➔v➔e➔r➔ ➔(➔G➔i➔t➔H➔u➔b➔,➔ ➔G➔i➔t➔L➔a➔b➔,➔ ➔A➔z➔u➔r➔e➔ ➔R➔e➔p➔o➔s➔)➔.➔ ➔o➔r➔i➔g➔i➔n➔ ➔ ➔i➔s➔ ➔t➔h➔e➔
➔d➔e➔f➔a➔u➔l➔t➔ ➔n➔a➔m➔e➔ ➔f➔o➔r➔ ➔y➔o➔u➔r➔ ➔r➔e➔m➔o➔t➔e➔.➔
➔R➔e➔m➔o➔t➔e➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔
➔#➔ ➔V➔i➔e➔w➔ ➔r➔e➔m➔o➔t➔e➔s➔
➔g➔i➔t➔ ➔r➔e➔m➔o➔t➔e➔ ➔-➔v➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔r➔e➔m➔o➔t➔e➔s➔ ➔w➔i➔t➔h➔ ➔U➔R➔L➔s➔
➔g➔i➔t➔ ➔r➔e➔m➔o➔t➔e➔ ➔s➔h➔o➔w➔ ➔o➔r➔i➔g➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔t➔a➔i➔l➔s➔ ➔a➔b➔o➔u➔t➔ ➔o➔r➔i➔g➔i➔n➔
➔#➔ ➔A➔d➔d➔ ➔r➔e➔m➔o➔t➔e➔
➔g➔i➔t➔ ➔r➔e➔m➔o➔t➔e➔ ➔a➔d➔d➔ ➔o➔r➔i➔g➔i➔n➔ ➔h➔t➔t➔p➔s➔:➔/➔/➔g➔i➔t➔h➔u➔b➔.➔c➔o➔m➔/➔a➔k➔h➔i➔l➔/➔r➔e➔p➔o➔.➔g➔i➔t➔
➔#➔ ➔C➔h➔a➔n➔g➔e➔ ➔r➔e➔m➔o➔t➔e➔ ➔U➔R➔L➔
➔g➔i➔t➔ ➔r➔e➔m➔o➔t➔e➔ ➔s➔e➔t➔-➔u➔r➔l➔ ➔o➔r➔i➔g➔i➔n➔ ➔h➔t➔t➔p➔s➔:➔/➔/➔g➔i➔t➔h➔u➔b➔.➔c➔o➔m➔/➔a➔k➔h➔i➔l➔/➔n➔e➔w➔-➔r➔e➔p➔o➔.➔g➔i➔t➔
➔#➔ ➔R➔e➔m➔o➔v➔e➔ ➔r➔e➔m➔o➔t➔e➔
➔g➔i➔t➔ ➔r➔e➔m➔o➔t➔e➔ ➔r➔e➔m➔o➔v➔e➔ ➔o➔r➔i➔g➔i➔n➔
➔
➔
➔
➔
➔➔ ➔➔
➔1➔1➔.➔ ➔P➔u➔s➔h➔,➔ ➔P➔u➔l➔l➔,➔ ➔F➔e➔t➔c➔h➔ ➔—➔ ➔S➔y➔n➔c➔i➔n➔g➔ ➔w➔i➔t➔h➔ ➔R➔e➔m➔o➔t➔e➔
➔g➔i➔t➔ ➔p➔u➔s➔h➔ ➔—➔ ➔L➔o➔c➔a➔l➔ ➔R➔e➔p➔o➔ ➔→➔ ➔R➔e➔m➔o➔t➔e➔
➔g➔i➔t➔ ➔p➔u➔s➔h➔ ➔o➔r➔i➔g➔i➔n➔ ➔m➔a➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔u➔s➔h➔ ➔m➔a➔i➔n➔ ➔b➔r➔a➔n➔c➔h➔ ➔t➔o➔ ➔o➔r➔i➔g➔i➔n➔
➔g➔i➔t➔ ➔p➔u➔s➔h➔ ➔o➔r➔i➔g➔i➔n➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔l➔o➔g➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔u➔s➔h➔ ➔f➔e➔a➔t➔u➔r➔e➔ ➔b➔r➔a➔n➔c➔h➔
➔g➔i➔t➔ ➔p➔u➔s➔h➔ ➔-➔u➔ ➔o➔r➔i➔g➔i➔n➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔l➔o➔g➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔u➔s➔h➔ ➔a➔n➔d➔ ➔s➔e➔t➔ ➔u➔p➔s➔t➔r➔e➔a➔m➔ ➔(➔t➔r➔a➔c➔k➔ ➔r➔e➔m➔o➔t➔e➔ ➔b➔r➔a➔n➔c➔h➔)➔
➔g➔i➔t➔ ➔p➔u➔s➔h➔ ➔-➔-➔f➔o➔r➔c➔e➔ ➔o➔r➔i➔g➔i➔n➔ ➔m➔a➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔r➔c➔e➔ ➔p➔u➔s➔h➔ ➔(➔D➔A➔N➔G➔E➔R➔O➔U➔S➔ ➔—➔ ➔o➔v➔e➔r➔w➔r➔i➔t➔e➔s➔ ➔r➔e➔m➔o➔t➔e➔)➔
➔g➔i➔t➔ ➔p➔u➔s➔h➔ ➔-➔-➔f➔o➔r➔c➔e➔-➔w➔i➔t➔h➔-➔l➔e➔a➔s➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔a➔f➔e➔r➔ ➔f➔o➔r➔c➔e➔ ➔p➔u➔s➔h➔ ➔(➔f➔a➔i➔l➔s➔ ➔i➔f➔ ➔r➔e➔m➔o➔t➔e➔ ➔h➔a➔s➔ ➔n➔e➔w➔ ➔c➔o➔m➔
➔g➔i➔t➔ ➔p➔u➔s➔h➔ ➔o➔r➔i➔g➔i➔n➔ ➔-➔-➔d➔e➔l➔e➔t➔e➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔l➔o➔g➔i➔n➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔r➔e➔m➔o➔t➔e➔ ➔b➔r➔a➔n➔c➔h➔
➔g➔i➔t➔ ➔p➔u➔s➔h➔ ➔-➔-➔t➔a➔g➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔u➔s➔h➔ ➔a➔l➔l➔ ➔t➔a➔g➔s➔
➔g➔i➔t➔ ➔p➔u➔l➔l➔ ➔—➔ ➔R➔e➔m➔o➔t➔e➔ ➔→➔ ➔L➔o➔c➔a➔l➔ ➔(➔f➔e➔t➔c➔h➔ ➔+➔ ➔m➔e➔r➔g➔e➔ ➔i➔n➔ ➔o➔n➔e➔ ➔s➔t➔e➔p➔)➔
➔g➔i➔t➔ ➔p➔u➔l➔l➔ ➔o➔r➔i➔g➔i➔n➔ ➔m➔a➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔u➔l➔l➔ ➔l➔a➔t➔e➔s➔t➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔f➔r➔o➔m➔ ➔m➔a➔i➔n➔
➔g➔i➔t➔ ➔p➔u➔l➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔u➔l➔l➔ ➔f➔r➔o➔m➔ ➔t➔r➔a➔c➔k➔e➔d➔ ➔u➔p➔s➔t➔r➔e➔a➔m➔ ➔b➔r➔a➔n➔c➔h➔
➔g➔i➔t➔ ➔p➔u➔l➔l➔ ➔-➔-➔r➔e➔b➔a➔s➔e➔ ➔o➔r➔i➔g➔i➔n➔ ➔m➔a➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔u➔l➔l➔ ➔a➔n➔d➔ ➔r➔e➔b➔a➔s➔e➔ ➔i➔n➔s➔t➔e➔a➔d➔ ➔o➔f➔ ➔m➔e➔r➔g➔e➔
➔g➔i➔t➔ ➔f➔e➔t➔c➔h➔ ➔—➔ ➔D➔o➔w➔n➔l➔o➔a➔d➔ ➔w➔i➔t➔h➔o➔u➔t➔ ➔M➔e➔r➔g➔i➔n➔g➔
➔g➔i➔t➔ ➔f➔e➔t➔c➔h➔ ➔o➔r➔i➔g➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔o➔w➔n➔l➔o➔a➔d➔ ➔a➔l➔l➔ ➔r➔e➔m➔o➔t➔e➔ ➔c➔h➔a➔n➔g➔e➔s➔,➔ ➔d➔o➔n➔'➔t➔ ➔m➔e➔r➔g➔e➔
➔g➔i➔t➔ ➔f➔e➔t➔c➔h➔ ➔o➔r➔i➔g➔i➔n➔ ➔m➔a➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔e➔t➔c➔h➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔b➔r➔a➔n➔c➔h➔
➔g➔i➔t➔ ➔f➔e➔t➔c➔h➔ ➔-➔-➔a➔l➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔e➔t➔c➔h➔ ➔f➔r➔o➔m➔ ➔a➔l➔l➔ ➔r➔e➔m➔o➔t➔e➔s➔
➔#➔ ➔A➔f➔t➔e➔r➔ ➔f➔e➔t➔c➔h➔,➔ ➔y➔o➔u➔ ➔c➔a➔n➔ ➔c➔o➔m➔p➔a➔r➔e➔:➔
➔g➔i➔t➔ ➔d➔i➔f➔f➔ ➔m➔a➔i➔n➔ ➔o➔r➔i➔g➔i➔n➔/➔m➔a➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔e➔ ➔w➔h➔a➔t➔ ➔c➔h➔a➔n➔g➔e➔d➔ ➔o➔n➔ ➔r➔e➔m➔o➔t➔e➔
➔g➔i➔t➔ ➔m➔e➔r➔g➔e➔ ➔o➔r➔i➔g➔i➔n➔/➔m➔a➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔t➔h➔e➔n➔ ➔m➔a➔n➔u➔a➔l➔l➔y➔ ➔m➔e➔r➔g➔e➔ ➔w➔h➔e➔n➔ ➔r➔e➔a➔d➔y➔
➔K➔e➔y➔ ➔D➔i➔f➔f➔e➔r➔e➔n➔c➔e➔:➔
➔g➔i➔t➔ ➔p➔u➔l➔l➔ ➔ ➔=➔ ➔g➔i➔t➔ ➔f➔e➔t➔c➔h➔ ➔ ➔+➔ ➔g➔i➔t➔ ➔m➔e➔r➔g➔e➔ ➔ ➔—➔ ➔d➔o➔w➔n➔l➔o➔a➔d➔s➔ ➔A➔N➔D➔ ➔m➔e➔r➔g➔e➔s➔ ➔a➔u➔t➔o➔m➔a➔t➔i➔c➔a➔l➔l➔y➔
➔g➔i➔t➔ ➔f➔e➔t➔c➔h➔ ➔ ➔=➔ ➔d➔o➔w➔n➔l➔o➔a➔d➔s➔ ➔o➔n➔l➔y➔,➔ ➔y➔o➔u➔ ➔d➔e➔c➔i➔d➔e➔ ➔w➔h➔e➔n➔ ➔t➔o➔ ➔m➔e➔r➔g➔e➔ ➔—➔ ➔s➔a➔f➔e➔r➔
➔g➔i➔t➔ ➔c➔l➔o➔n➔e➔ ➔—➔ ➔C➔o➔p➔y➔ ➔R➔e➔m➔o➔t➔e➔ ➔R➔e➔p➔o➔ ➔t➔o➔ ➔L➔o➔c➔a➔l➔
➔g➔i➔t➔ ➔c➔l➔o➔n➔e➔ ➔h➔t➔t➔p➔s➔:➔/➔/➔g➔i➔t➔h➔u➔b➔.➔c➔o➔m➔/➔a➔k➔h➔i➔l➔/➔r➔e➔p➔o➔.➔g➔i➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔l➔o➔n➔e➔ ➔r➔e➔p➔o➔
➔g➔i➔t➔ ➔c➔l➔o➔n➔e➔ ➔h➔t➔t➔p➔s➔:➔/➔/➔g➔i➔t➔h➔u➔b➔.➔c➔o➔m➔/➔a➔k➔h➔i➔l➔/➔r➔e➔p➔o➔.➔g➔i➔t➔ ➔m➔y➔a➔p➔p➔ ➔ ➔#➔ ➔c➔l➔o➔n➔e➔ ➔i➔n➔t➔o➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔f➔o➔l➔d➔e➔r➔
➔
➔
➔
➔
➔➔ ➔➔
➔➔ ➔➔
➔g➔i➔t➔ ➔c➔l➔o➔n➔e➔ ➔-➔-➔b➔r➔a➔n➔c➔h➔ ➔d➔e➔v➔e➔l➔o➔p➔ ➔r➔e➔p➔o➔.➔g➔i➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔l➔o➔n➔e➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔b➔r➔a➔n➔c➔h➔
➔g➔i➔t➔ ➔c➔l➔o➔n➔e➔ ➔-➔-➔d➔e➔p➔t➔h➔ ➔1➔ ➔r➔e➔p➔o➔.➔g➔i➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔a➔l➔l➔o➔w➔ ➔c➔l➔o➔n➔e➔ ➔(➔l➔a➔t➔e➔s➔t➔ ➔c➔o➔m➔m➔i➔t➔ ➔o➔n➔l➔y➔
➔1➔2➔.➔ ➔U➔n➔d➔o➔i➔n➔g➔ ➔C➔h➔a➔n➔g➔e➔s➔
➔T➔h➔i➔s➔ ➔i➔s➔ ➔o➔n➔e➔ ➔o➔f➔ ➔t➔h➔e➔ ➔m➔o➔s➔t➔ ➔i➔m➔p➔o➔r➔t➔a➔n➔t➔ ➔t➔o➔p➔i➔c➔s➔ ➔i➔n➔ ➔G➔i➔t➔ ➔i➔n➔t➔e➔r➔v➔i➔e➔w➔s➔.➔
➔A➔)➔ ➔g➔i➔t➔ ➔c➔h➔e➔c➔k➔o➔u➔t➔ ➔—➔ ➔D➔i➔s➔c➔a➔r➔d➔ ➔W➔o➔r➔k➔i➔n➔g➔ ➔D➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔C➔h➔a➔n➔g➔e➔s➔
➔g➔i➔t➔ ➔c➔h➔e➔c➔k➔o➔u➔t➔ ➔-➔-➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔i➔s➔c➔a➔r➔d➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔i➔n➔ ➔w➔o➔r➔k➔i➔n➔g➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔(➔o➔l➔d➔ ➔w➔a➔y➔)➔
➔g➔i➔t➔ ➔r➔e➔s➔t➔o➔r➔e➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔i➔s➔c➔a➔r➔d➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔i➔n➔ ➔w➔o➔r➔k➔i➔n➔g➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔(➔n➔e➔w➔ ➔w➔a➔y➔)➔
➔g➔i➔t➔ ➔r➔e➔s➔t➔o➔r➔e➔ ➔.➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔i➔s➔c➔a➔r➔d➔ ➔A➔L➔L➔ ➔w➔o➔r➔k➔i➔n➔g➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔c➔h➔a➔n➔g➔e➔s➔
➔⚠➔ ➔ ➔W➔a➔r➔n➔i➔n➔g➔:➔ ➔T➔h➔i➔s➔ ➔i➔s➔ ➔p➔e➔r➔m➔a➔n➔e➔n➔t➔ ➔—➔ ➔y➔o➔u➔ ➔l➔o➔s➔e➔ ➔y➔o➔u➔r➔ ➔u➔n➔s➔a➔v➔e➔d➔ ➔c➔h➔a➔n➔g➔e➔s➔.➔
➔B➔)➔ ➔g➔i➔t➔ ➔r➔e➔s➔e➔t➔ ➔—➔ ➔U➔n➔s➔t➔a➔g➔e➔ ➔o➔r➔ ➔G➔o➔ ➔B➔a➔c➔k➔ ➔i➔n➔ ➔H➔i➔s➔t➔o➔r➔y➔
➔T➔h➔r➔e➔e➔ ➔m➔o➔d➔e➔s➔:➔
➔#➔ ➔1➔.➔ ➔g➔i➔t➔ ➔r➔e➔s➔e➔t➔ ➔-➔-➔s➔o➔f➔t➔ ➔<➔c➔o➔m➔m➔i➔t➔>➔
➔#➔ ➔M➔o➔v➔e➔s➔ ➔H➔E➔A➔D➔ ➔b➔a➔c➔k➔ ➔t➔o➔ ➔t➔h➔a➔t➔ ➔c➔o➔m➔m➔i➔t➔
➔#➔ ➔C➔h➔a➔n➔g➔e➔s➔ ➔g➔o➔ ➔b➔a➔c➔k➔ ➔t➔o➔ ➔S➔T➔A➔G➔I➔N➔G➔ ➔A➔R➔E➔A➔ ➔(➔s➔t➔a➔g➔e➔d➔,➔ ➔r➔e➔a➔d➔y➔ ➔t➔o➔ ➔r➔e➔c➔o➔m➔m➔i➔t➔)➔
➔g➔i➔t➔ ➔r➔e➔s➔e➔t➔ ➔-➔-➔s➔o➔f➔t➔ ➔H➔E➔A➔D➔~➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔u➔n➔d➔o➔ ➔l➔a➔s➔t➔ ➔c➔o➔m➔m➔i➔t➔,➔ ➔k➔e➔e➔p➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔s➔t➔a➔g➔e➔d➔
➔g➔i➔t➔ ➔r➔e➔s➔e➔t➔ ➔-➔-➔s➔o➔f➔t➔ ➔<➔c➔o➔m➔m➔i➔t➔-➔i➔d➔>➔
➔#➔ ➔2➔.➔ ➔g➔i➔t➔ ➔r➔e➔s➔e➔t➔ ➔-➔-➔m➔i➔x➔e➔d➔ ➔<➔c➔o➔m➔m➔i➔t➔>➔ ➔(➔D➔E➔F➔A➔U➔L➔T➔)➔
➔#➔ ➔M➔o➔v➔e➔s➔ ➔H➔E➔A➔D➔ ➔b➔a➔c➔k➔ ➔t➔o➔ ➔t➔h➔a➔t➔ ➔c➔o➔m➔m➔i➔t➔
➔#➔ ➔C➔h➔a➔n➔g➔e➔s➔ ➔g➔o➔ ➔b➔a➔c➔k➔ ➔t➔o➔ ➔W➔O➔R➔K➔I➔N➔G➔ ➔D➔I➔R➔E➔C➔T➔O➔R➔Y➔ ➔(➔u➔n➔s➔t➔a➔g➔e➔d➔)➔
➔g➔i➔t➔ ➔r➔e➔s➔e➔t➔ ➔H➔E➔A➔D➔~➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔u➔n➔d➔o➔ ➔l➔a➔s➔t➔ ➔c➔o➔m➔m➔i➔t➔,➔ ➔u➔n➔s➔t➔a➔g➔e➔ ➔c➔h➔a➔n➔g➔e➔s➔
➔g➔i➔t➔ ➔r➔e➔s➔e➔t➔ ➔H➔E➔A➔D➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔u➔n➔s➔t➔a➔g➔e➔ ➔a➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔f➔i➔l➔e➔
➔#➔ ➔3➔.➔ ➔g➔i➔t➔ ➔r➔e➔s➔e➔t➔ ➔-➔-➔h➔a➔r➔d➔ ➔<➔c➔o➔m➔m➔i➔t➔>➔
➔#➔ ➔M➔o➔v➔e➔s➔ ➔H➔E➔A➔D➔ ➔b➔a➔c➔k➔ ➔t➔o➔ ➔t➔h➔a➔t➔ ➔c➔o➔m➔m➔i➔t➔
➔#➔ ➔A➔L➔L➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔a➔r➔e➔ ➔D➔E➔L➔E➔T➔E➔D➔ ➔p➔e➔r➔m➔a➔n➔e➔n➔t➔l➔y➔
➔g➔i➔t➔ ➔r➔e➔s➔e➔t➔ ➔-➔-➔h➔a➔r➔d➔ ➔H➔E➔A➔D➔~➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔u➔n➔d➔o➔ ➔l➔a➔s➔t➔ ➔c➔o➔m➔m➔i➔t➔,➔ ➔D➔E➔L➔E➔T➔E➔ ➔a➔l➔l➔ ➔c➔h➔a➔n➔g➔e➔s➔
➔g➔i➔t➔ ➔r➔e➔s➔e➔t➔ ➔-➔-➔h➔a➔r➔d➔ ➔<➔c➔o➔m➔m➔i➔t➔-➔i➔d➔>➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔g➔o➔ ➔b➔a➔c➔k➔ ➔t➔o➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔c➔o➔m➔m➔i➔t➔,➔ ➔d➔e➔l➔e➔t➔e➔ ➔e➔v➔e➔r➔y➔t➔h➔i➔n➔g➔ ➔a➔f➔t➔e➔
➔⚠➔ ➔ ➔W➔a➔r➔n➔i➔n➔g➔:➔ ➔-➔-➔h➔a➔r➔d➔ ➔ ➔d➔e➔l➔e➔t➔e➔s➔ ➔y➔o➔u➔r➔ ➔w➔o➔r➔k➔ ➔p➔e➔r➔m➔a➔n➔e➔n➔t➔l➔y➔.➔ ➔U➔s➔e➔ ➔w➔i➔t➔h➔ ➔c➔a➔u➔t➔i➔o➔n➔.➔
➔W➔h➔e➔n➔ ➔t➔o➔ ➔u➔s➔e➔ ➔w➔h➔i➔c➔h➔:➔
➔
➔
➔
➔
➔➔ ➔➔
➔➔ ➔➔
➔M➔o➔d➔e➔ ➔C➔h➔a➔n➔g➔e➔s➔ ➔g➔o➔ ➔t➔o➔ ➔U➔s➔e➔ ➔w➔h➔e➔n➔
➔-➔-➔s➔o➔f➔t➔ ➔S➔t➔a➔g➔i➔n➔g➔ ➔a➔r➔e➔a➔ ➔W➔a➔n➔t➔ ➔t➔o➔ ➔r➔e➔c➔o➔m➔m➔i➔t➔ ➔w➔i➔t➔h➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔t➔ ➔m➔e➔s➔s➔a➔g➔e➔
➔-➔-➔m➔i➔x➔e➔d➔ ➔W➔o➔r➔k➔i➔n➔g➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔W➔a➔n➔t➔ ➔t➔o➔ ➔r➔e➔-➔e➔d➔i➔t➔ ➔b➔e➔f➔o➔r➔e➔ ➔s➔t➔a➔g➔i➔n➔g➔
➔-➔-➔h➔a➔r➔d➔ ➔D➔E➔L➔E➔T➔E➔D➔ ➔W➔a➔n➔t➔ ➔t➔o➔ ➔c➔o➔m➔p➔l➔e➔t➔e➔l➔y➔ ➔u➔n➔d➔o➔,➔ ➔n➔o➔ ➔g➔o➔i➔n➔g➔ ➔b➔a➔c➔k➔
➔C➔)➔ ➔g➔i➔t➔ ➔r➔e➔v➔e➔r➔t➔ ➔—➔ ➔S➔a➔f➔e➔l➔y➔ ➔U➔n➔d➔o➔ ➔a➔ ➔C➔o➔m➔m➔i➔t➔
➔g➔i➔t➔ ➔r➔e➔v➔e➔r➔t➔ ➔<➔c➔o➔m➔m➔i➔t➔-➔i➔d➔>➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔a➔ ➔N➔E➔W➔ ➔c➔o➔m➔m➔i➔t➔ ➔t➔h➔a➔t➔ ➔u➔n➔d➔o➔e➔s➔ ➔t➔h➔e➔ ➔s➔p➔e➔c➔i➔f➔i➔e➔d➔ ➔c➔o➔m➔m➔
➔g➔i➔t➔ ➔r➔e➔v➔e➔r➔t➔ ➔H➔E➔A➔D➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔v➔e➔r➔t➔ ➔l➔a➔s➔t➔ ➔c➔o➔m➔m➔i➔t➔
➔g➔i➔t➔ ➔r➔e➔v➔e➔r➔t➔ ➔H➔E➔A➔D➔~➔3➔.➔.➔H➔E➔A➔D➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔v➔e➔r➔t➔ ➔l➔a➔s➔t➔ ➔3➔ ➔c➔o➔m➔m➔i➔t➔s➔
➔g➔i➔t➔ ➔r➔e➔v➔e➔r➔t➔ ➔-➔-➔n➔o➔-➔c➔o➔m➔m➔i➔t➔ ➔<➔c➔o➔m➔m➔i➔t➔-➔i➔d➔>➔ ➔#➔ ➔r➔e➔v➔e➔r➔t➔ ➔w➔i➔t➔h➔o➔u➔t➔ ➔a➔u➔t➔o➔-➔c➔o➔m➔m➔i➔t➔t➔i➔n➔g➔
➔K➔e➔y➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔c➔e➔ ➔f➔r➔o➔m➔ ➔r➔e➔s➔e➔t➔:➔
➔g➔i➔t➔ ➔r➔e➔s➔e➔t➔ ➔ ➔—➔ ➔r➔e➔w➔r➔i➔t➔e➔s➔ ➔h➔i➔s➔t➔o➔r➔y➔ ➔(➔d➔a➔n➔g➔e➔r➔o➔u➔s➔ ➔i➔f➔ ➔a➔l➔r➔e➔a➔d➔y➔ ➔p➔u➔s➔h➔e➔d➔)➔
➔g➔i➔t➔ ➔r➔e➔v➔e➔r➔t➔ ➔ ➔—➔ ➔a➔d➔d➔s➔ ➔a➔ ➔n➔e➔w➔ ➔c➔o➔m➔m➔i➔t➔ ➔t➔h➔a➔t➔ ➔u➔n➔d➔o➔e➔s➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔(➔s➔a➔f➔e➔,➔ ➔p➔r➔e➔s➔e➔r➔v➔e➔s➔ ➔h➔i➔s➔t➔o➔r➔y➔)➔
➔R➔u➔l➔e➔:➔ ➔U➔s➔e➔ ➔r➔e➔v➔e➔r➔t➔ ➔ ➔f➔o➔r➔ ➔c➔o➔m➔m➔i➔t➔s➔ ➔a➔l➔r➔e➔a➔d➔y➔ ➔p➔u➔s➔h➔e➔d➔ ➔t➔o➔ ➔r➔e➔m➔o➔t➔e➔.➔ ➔U➔s➔e➔ ➔r➔e➔s➔e➔t➔ ➔ ➔o➔n➔l➔y➔ ➔f➔o➔r➔ ➔l➔o➔c➔a➔l➔ ➔c➔o➔m➔m➔i➔t➔s➔ ➔n➔o➔t➔ ➔y➔e➔t➔
➔p➔u➔s➔h➔e➔d➔.➔
➔D➔)➔ ➔g➔i➔t➔ ➔r➔m➔ ➔—➔ ➔R➔e➔m➔o➔v➔e➔ ➔F➔i➔l➔e➔s➔ ➔f➔r➔o➔m➔ ➔G➔i➔t➔
➔g➔i➔t➔ ➔r➔m➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔f➔i➔l➔e➔ ➔f➔r➔o➔m➔ ➔w➔o➔r➔k➔i➔n➔g➔ ➔d➔i➔r➔ ➔A➔N➔D➔ ➔s➔t➔a➔g➔i➔n➔g➔
➔g➔i➔t➔ ➔r➔m➔ ➔-➔-➔c➔a➔c➔h➔e➔d➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔f➔r➔o➔m➔ ➔G➔i➔t➔ ➔t➔r➔a➔c➔k➔i➔n➔g➔ ➔o➔n➔l➔y➔,➔ ➔k➔e➔e➔p➔ ➔f➔i➔l➔e➔ ➔l➔o➔c➔a➔l➔l➔y➔
➔g➔i➔t➔ ➔r➔m➔ ➔-➔r➔ ➔f➔o➔l➔d➔e➔r➔n➔a➔m➔e➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔e➔n➔t➔i➔r➔e➔ ➔f➔o➔l➔d➔e➔r➔
➔#➔ ➔C➔o➔m➔m➔o➔n➔ ➔u➔s➔e➔:➔ ➔s➔t➔o➔p➔ ➔t➔r➔a➔c➔k➔i➔n➔g➔ ➔a➔ ➔f➔i➔l➔e➔ ➔(➔e➔.➔g➔.➔,➔ ➔a➔c➔c➔i➔d➔e➔n➔t➔a➔l➔l➔y➔ ➔c➔o➔m➔m➔i➔t➔t➔e➔d➔ ➔.➔e➔n➔v➔)➔
➔g➔i➔t➔ ➔r➔m➔ ➔-➔-➔c➔a➔c➔h➔e➔d➔ ➔.➔e➔n➔v➔
➔e➔c➔h➔o➔ ➔"➔.➔e➔n➔v➔"➔ ➔>➔>➔ ➔.➔g➔i➔t➔i➔g➔n➔o➔r➔e➔
➔g➔i➔t➔ ➔c➔o➔m➔m➔i➔t➔ ➔-➔m➔ ➔"➔R➔e➔m➔o➔v➔e➔ ➔.➔e➔n➔v➔ ➔f➔r➔o➔m➔ ➔t➔r➔a➔c➔k➔i➔n➔g➔"➔
➔1➔3➔.➔ ➔g➔i➔t➔ ➔s➔t➔a➔s➔h➔ ➔—➔ ➔S➔a➔v➔e➔ ➔W➔o➔r➔k➔ ➔T➔e➔m➔p➔o➔r➔a➔r➔i➔l➔y➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔S➔t➔a➔s➔h➔?➔
➔
➔
➔
➔
➔S➔t➔a➔s➔h➔ ➔t➔e➔m➔p➔o➔r➔a➔r➔i➔l➔y➔ ➔s➔a➔v➔e➔s➔ ➔y➔o➔u➔r➔ ➔u➔n➔c➔o➔m➔m➔i➔t➔t➔e➔d➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔s➔o➔ ➔y➔o➔u➔ ➔c➔a➔n➔ ➔s➔w➔i➔t➔c➔h➔ ➔b➔r➔a➔n➔c➔h➔e➔s➔ ➔o➔r➔ ➔d➔o➔ ➔s➔o➔m➔e➔t➔h➔i➔n➔g➔ ➔e➔l➔s➔e➔,➔ ➔t➔h➔e➔n➔
➔c➔o➔m➔e➔ ➔b➔a➔c➔k➔ ➔t➔o➔ ➔y➔o➔u➔r➔ ➔w➔o➔r➔k➔.➔
➔g➔i➔t➔ ➔s➔t➔a➔s➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔t➔a➔s➔h➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔c➔h➔a➔n➔g➔e➔s➔
➔g➔i➔t➔ ➔s➔t➔a➔s➔h➔ ➔p➔u➔s➔h➔ ➔-➔m➔ ➔"➔l➔o➔g➔i➔n➔ ➔w➔o➔r➔k➔"➔ ➔ ➔ ➔#➔ ➔s➔t➔a➔s➔h➔ ➔w➔i➔t➔h➔ ➔a➔ ➔n➔a➔m➔e➔
➔g➔i➔t➔ ➔s➔t➔a➔s➔h➔ ➔l➔i➔s➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔a➔l➔l➔ ➔s➔t➔a➔s➔h➔e➔s➔
➔g➔i➔t➔ ➔s➔t➔a➔s➔h➔ ➔p➔o➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔p➔p➔l➔y➔ ➔l➔a➔s➔t➔ ➔s➔t➔a➔s➔h➔ ➔a➔n➔d➔ ➔r➔e➔m➔o➔v➔e➔ ➔i➔t➔ ➔f➔r➔o➔m➔ ➔s➔t➔a➔s➔h➔ ➔l➔i➔s➔t➔
➔g➔i➔t➔ ➔s➔t➔a➔s➔h➔ ➔a➔p➔p➔l➔y➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔p➔p➔l➔y➔ ➔l➔a➔s➔t➔ ➔s➔t➔a➔s➔h➔ ➔b➔u➔t➔ ➔k➔e➔e➔p➔ ➔i➔t➔ ➔i➔n➔ ➔s➔t➔a➔s➔h➔ ➔l➔i➔s➔t➔
➔g➔i➔t➔ ➔s➔t➔a➔s➔h➔ ➔a➔p➔p➔l➔y➔ ➔s➔t➔a➔s➔h➔@➔{➔2➔}➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔p➔p➔l➔y➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔s➔t➔a➔s➔h➔
➔g➔i➔t➔ ➔s➔t➔a➔s➔h➔ ➔d➔r➔o➔p➔ ➔s➔t➔a➔s➔h➔@➔{➔0➔}➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔s➔t➔a➔s➔h➔
➔g➔i➔t➔ ➔s➔t➔a➔s➔h➔ ➔c➔l➔e➔a➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔a➔l➔l➔ ➔s➔t➔a➔s➔h➔e➔s➔
➔E➔x➔a➔m➔p➔l➔e➔:➔
➔#➔ ➔Y➔o➔u➔'➔r➔e➔ ➔w➔o➔r➔k➔i➔n➔g➔ ➔o➔n➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔l➔o➔g➔i➔n➔ ➔w➔h➔e➔n➔ ➔u➔r➔g➔e➔n➔t➔ ➔b➔u➔g➔ ➔f➔i➔x➔ ➔i➔s➔ ➔n➔e➔e➔d➔e➔d➔
➔g➔i➔t➔ ➔s➔t➔a➔s➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔a➔v➔e➔ ➔y➔o➔u➔r➔ ➔w➔o➔r➔k➔
➔g➔i➔t➔ ➔s➔w➔i➔t➔c➔h➔ ➔m➔a➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔w➔i➔t➔c➔h➔ ➔t➔o➔ ➔m➔a➔i➔n➔
➔g➔i➔t➔ ➔s➔w➔i➔t➔c➔h➔ ➔-➔c➔ ➔h➔o➔t➔f➔i➔x➔-➔b➔u➔g➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔x➔ ➔t➔h➔e➔ ➔b➔u➔g➔
➔g➔i➔t➔ ➔c➔o➔m➔m➔i➔t➔ ➔-➔m➔ ➔"➔F➔i➔x➔ ➔c➔r➔i➔t➔i➔c➔a➔l➔ ➔b➔u➔g➔"➔
➔g➔i➔t➔ ➔s➔w➔i➔t➔c➔h➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔l➔o➔g➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔g➔o➔ ➔b➔a➔c➔k➔
➔g➔i➔t➔ ➔s➔t➔a➔s➔h➔ ➔p➔o➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔s➔t➔o➔r➔e➔ ➔y➔o➔u➔r➔ ➔s➔a➔v➔e➔d➔ ➔w➔o➔r➔k➔
➔1➔4➔.➔ ➔g➔i➔t➔ ➔c➔h➔e➔r➔r➔y➔-➔p➔i➔c➔k➔ ➔—➔ ➔P➔i➔c➔k➔ ➔S➔p➔e➔c➔i➔f➔i➔c➔ ➔C➔o➔m➔m➔i➔t➔s➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔C➔h➔e➔r➔r➔y➔-➔p➔i➔c➔k➔?➔
➔C➔h➔e➔r➔r➔y➔-➔p➔i➔c➔k➔ ➔a➔p➔p➔l➔i➔e➔s➔ ➔a➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔c➔o➔m➔m➔i➔t➔ ➔f➔r➔o➔m➔ ➔o➔n➔e➔ ➔b➔r➔a➔n➔c➔h➔ ➔t➔o➔ ➔a➔n➔o➔t➔h➔e➔r➔.➔ ➔Y➔o➔u➔ ➔p➔i➔c➔k➔ ➔o➔n➔l➔y➔ ➔t➔h➔e➔ ➔c➔o➔m➔m➔i➔t➔ ➔y➔o➔u➔ ➔w➔a➔n➔t➔,➔ ➔n➔o➔t➔ ➔t➔h➔e➔
➔e➔n➔t➔i➔r➔e➔ ➔b➔r➔a➔n➔c➔h➔.➔
➔g➔i➔t➔ ➔c➔h➔e➔r➔r➔y➔-➔p➔i➔c➔k➔ ➔<➔c➔o➔m➔m➔i➔t➔-➔i➔d➔>➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔p➔p➔l➔y➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔c➔o➔m➔m➔i➔t➔ ➔t➔o➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔b➔r➔a➔n➔c➔h➔
➔g➔i➔t➔ ➔c➔h➔e➔r➔r➔y➔-➔p➔i➔c➔k➔ ➔<➔c➔o➔m➔m➔i➔t➔1➔>➔ ➔<➔c➔o➔m➔m➔i➔t➔2➔>➔ ➔ ➔ ➔ ➔#➔ ➔a➔p➔p➔l➔y➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔c➔o➔m➔m➔i➔t➔s➔
➔g➔i➔t➔ ➔c➔h➔e➔r➔r➔y➔-➔p➔i➔c➔k➔ ➔A➔.➔.➔B➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔p➔p➔l➔y➔ ➔r➔a➔n➔g➔e➔ ➔o➔f➔ ➔c➔o➔m➔m➔i➔t➔s➔
➔g➔i➔t➔ ➔c➔h➔e➔r➔r➔y➔-➔p➔i➔c➔k➔ ➔-➔-➔n➔o➔-➔c➔o➔m➔m➔i➔t➔ ➔<➔c➔o➔m➔m➔i➔t➔-➔i➔d➔>➔ ➔#➔ ➔a➔p➔p➔l➔y➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔w➔i➔t➔h➔o➔u➔t➔ ➔c➔o➔m➔m➔i➔t➔t➔i➔n➔g➔
➔g➔i➔t➔ ➔c➔h➔e➔r➔r➔y➔-➔p➔i➔c➔k➔ ➔-➔-➔a➔b➔o➔r➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔b➔o➔r➔t➔ ➔c➔h➔e➔r➔r➔y➔-➔p➔i➔c➔k➔ ➔i➔f➔ ➔c➔o➔n➔f➔l➔i➔c➔t➔
➔E➔x➔a➔m➔p➔l➔e➔:➔
➔#➔ ➔Y➔o➔u➔ ➔f➔i➔x➔e➔d➔ ➔a➔ ➔b➔u➔g➔ ➔i➔n➔ ➔f➔e➔a➔t➔u➔r➔e➔ ➔b➔r➔a➔n➔c➔h➔ ➔a➔n➔d➔ ➔w➔a➔n➔t➔ ➔t➔h➔a➔t➔ ➔f➔i➔x➔ ➔i➔n➔ ➔m➔a➔i➔n➔ ➔t➔o➔o➔
➔g➔i➔t➔ ➔l➔o➔g➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔b➔r➔a➔n➔c➔h➔ ➔-➔-➔o➔n➔e➔l➔i➔n➔e➔
➔#➔ ➔a➔b➔c➔1➔2➔3➔4➔ ➔F➔i➔x➔ ➔n➔u➔l➔l➔ ➔p➔o➔i➔n➔t➔e➔r➔ ➔b➔u➔g➔
➔#➔ ➔d➔e➔f➔5➔6➔7➔8➔ ➔A➔d➔d➔ ➔n➔e➔w➔ ➔f➔e➔a➔t➔u➔r➔e➔
➔
➔
➔
➔
➔g➔i➔t➔ ➔s➔w➔i➔t➔c➔h➔ ➔m➔a➔i➔n➔
➔g➔i➔t➔ ➔c➔h➔e➔r➔r➔y➔-➔p➔i➔c➔k➔ ➔a➔b➔c➔1➔2➔3➔4➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔p➔p➔l➔y➔ ➔o➔n➔l➔y➔ ➔t➔h➔e➔ ➔b➔u➔g➔ ➔f➔i➔x➔ ➔t➔o➔ ➔m➔a➔i➔n➔,➔ ➔n➔o➔t➔ ➔t➔h➔e➔ ➔f➔e➔a➔t➔u➔r➔e➔
➔W➔h➔e➔n➔ ➔t➔o➔ ➔u➔s➔e➔:➔
➔B➔u➔g➔ ➔f➔i➔x➔ ➔i➔n➔ ➔o➔n➔e➔ ➔b➔r➔a➔n➔c➔h➔ ➔n➔e➔e➔d➔e➔d➔ ➔i➔n➔ ➔a➔n➔o➔t➔h➔e➔r➔
➔P➔i➔c➔k➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔f➔e➔a➔t➔u➔r➔e➔s➔ ➔w➔i➔t➔h➔o➔u➔t➔ ➔m➔e➔r➔g➔i➔n➔g➔ ➔e➔n➔t➔i➔r➔e➔ ➔b➔r➔a➔n➔c➔h➔
➔B➔a➔c➔k➔p➔o➔r➔t➔i➔n➔g➔ ➔f➔i➔x➔e➔s➔ ➔t➔o➔ ➔o➔l➔d➔e➔r➔ ➔r➔e➔l➔e➔a➔s➔e➔ ➔b➔r➔a➔n➔c➔h➔e➔s➔
➔1➔5➔.➔ ➔g➔i➔t➔ ➔r➔e➔b➔a➔s➔e➔ ➔—➔ ➔R➔e➔w➔r➔i➔t➔e➔ ➔H➔i➔s➔t➔o➔r➔y➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔R➔e➔b➔a➔s➔e➔?➔
➔R➔e➔b➔a➔s➔e➔ ➔m➔o➔v➔e➔s➔ ➔o➔r➔ ➔r➔e➔p➔l➔a➔y➔s➔ ➔y➔o➔u➔r➔ ➔c➔o➔m➔m➔i➔t➔s➔ ➔o➔n➔ ➔t➔o➔p➔ ➔o➔f➔ ➔a➔n➔o➔t➔h➔e➔r➔ ➔b➔r➔a➔n➔c➔h➔.➔ ➔C➔r➔e➔a➔t➔e➔s➔ ➔a➔ ➔c➔l➔e➔a➔n➔e➔r➔,➔ ➔l➔i➔n➔e➔a➔r➔ ➔h➔i➔s➔t➔o➔r➔y➔ ➔c➔o➔m➔p➔a➔r➔e➔d➔ ➔t➔o➔
➔m➔e➔r➔g➔e➔ ➔c➔o➔m➔m➔i➔t➔s➔.➔
➔g➔i➔t➔ ➔r➔e➔b➔a➔s➔e➔ ➔m➔a➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔b➔a➔s➔e➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔b➔r➔a➔n➔c➔h➔ ➔o➔n➔t➔o➔ ➔m➔a➔i➔n➔
➔g➔i➔t➔ ➔r➔e➔b➔a➔s➔e➔ ➔-➔-➔i➔n➔t➔e➔r➔a➔c➔t➔i➔v➔e➔ ➔H➔E➔A➔D➔~➔3➔ ➔ ➔#➔ ➔i➔n➔t➔e➔r➔a➔c➔t➔i➔v➔e➔ ➔r➔e➔b➔a➔s➔e➔ ➔—➔ ➔e➔d➔i➔t➔ ➔l➔a➔s➔t➔ ➔3➔ ➔c➔o➔m➔m➔i➔t➔s➔
➔g➔i➔t➔ ➔r➔e➔b➔a➔s➔e➔ ➔-➔-➔a➔b➔o➔r➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔b➔o➔r➔t➔ ➔r➔e➔b➔a➔s➔e➔
➔g➔i➔t➔ ➔r➔e➔b➔a➔s➔e➔ ➔-➔-➔c➔o➔n➔t➔i➔n➔u➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔n➔t➔i➔n➔u➔e➔ ➔a➔f➔t➔e➔r➔ ➔r➔e➔s➔o➔l➔v➔i➔n➔g➔ ➔c➔o➔n➔f➔l➔i➔c➔t➔
➔I➔n➔t➔e➔r➔a➔c➔t➔i➔v➔e➔ ➔r➔e➔b➔a➔s➔e➔ ➔o➔p➔t➔i➔o➔n➔s➔:➔
➔g➔i➔t➔ ➔r➔e➔b➔a➔s➔e➔ ➔-➔i➔ ➔H➔E➔A➔D➔~➔3➔
➔#➔ ➔O➔p➔e➔n➔s➔ ➔e➔d➔i➔t➔o➔r➔ ➔w➔i➔t➔h➔:➔
➔#➔ ➔p➔i➔c➔k➔ ➔a➔b➔c➔1➔2➔3➔4➔ ➔F➔i➔r➔s➔t➔ ➔c➔o➔m➔m➔i➔t➔
➔#➔ ➔p➔i➔c➔k➔ ➔d➔e➔f➔5➔6➔7➔8➔ ➔S➔e➔c➔o➔n➔d➔ ➔c➔o➔m➔m➔i➔t➔
➔#➔ ➔p➔i➔c➔k➔ ➔g➔h➔i➔9➔0➔1➔2➔ ➔T➔h➔i➔r➔d➔ ➔c➔o➔m➔m➔i➔t➔
➔#➔ ➔C➔h➔a➔n➔g➔e➔ ➔'➔p➔i➔c➔k➔'➔ ➔t➔o➔:➔
➔#➔ ➔s➔q➔u➔a➔s➔h➔ ➔ ➔—➔ ➔c➔o➔m➔b➔i➔n➔e➔ ➔w➔i➔t➔h➔ ➔p➔r➔e➔v➔i➔o➔u➔s➔ ➔c➔o➔m➔m➔i➔t➔
➔#➔ ➔r➔e➔w➔o➔r➔d➔ ➔ ➔—➔ ➔e➔d➔i➔t➔ ➔c➔o➔m➔m➔i➔t➔ ➔m➔e➔s➔s➔a➔g➔e➔
➔#➔ ➔d➔r➔o➔p➔ ➔ ➔ ➔ ➔—➔ ➔d➔e➔l➔e➔t➔e➔ ➔c➔o➔m➔m➔i➔t➔
➔#➔ ➔e➔d➔i➔t➔ ➔ ➔ ➔ ➔—➔ ➔p➔a➔u➔s➔e➔ ➔t➔o➔ ➔a➔m➔e➔n➔d➔
➔M➔e➔r➔g➔e➔ ➔v➔s➔ ➔R➔e➔b➔a➔s➔e➔:➔
➔M➔e➔r➔g➔e➔ ➔R➔e➔b➔a➔s➔e➔
➔H➔i➔s➔t➔o➔r➔y➔ ➔P➔r➔e➔s➔e➔r➔v➔e➔s➔ ➔f➔u➔l➔l➔ ➔h➔i➔s➔t➔o➔r➔y➔ ➔w➔i➔t➔h➔ ➔m➔e➔r➔g➔e➔ ➔c➔o➔m➔m➔i➔t➔s➔ ➔C➔r➔e➔a➔t➔e➔s➔ ➔c➔l➔e➔a➔n➔ ➔l➔i➔n➔e➔a➔r➔ ➔h➔i➔s➔t➔o➔r➔y➔
➔
➔
➔
➔
➔S➔a➔f➔e➔t➔y➔ ➔S➔a➔f➔e➔ ➔f➔o➔r➔ ➔s➔h➔a➔r➔e➔d➔ ➔b➔r➔a➔n➔c➔h➔e➔s➔ ➔N➔e➔v➔e➔r➔ ➔r➔e➔b➔a➔s➔e➔ ➔s➔h➔a➔r➔e➔d➔/➔p➔u➔b➔l➔i➔c➔ ➔b➔r➔a➔n➔c➔h➔e➔s➔
➔U➔s➔e➔ ➔w➔h➔e➔n➔ ➔M➔e➔r➔g➔i➔n➔g➔ ➔f➔e➔a➔t➔u➔r➔e➔ ➔t➔o➔ ➔m➔a➔i➔n➔ ➔K➔e➔e➔p➔i➔n➔g➔ ➔f➔e➔a➔t➔u➔r➔e➔ ➔b➔r➔a➔n➔c➔h➔ ➔u➔p➔ ➔t➔o➔ ➔d➔a➔t➔e➔ ➔w➔i➔t➔h➔ ➔m➔a➔i➔n➔
➔R➔u➔l➔e➔:➔ ➔N➔e➔v➔e➔r➔ ➔r➔e➔b➔a➔s➔e➔ ➔c➔o➔m➔m➔i➔t➔s➔ ➔t➔h➔a➔t➔ ➔h➔a➔v➔e➔ ➔b➔e➔e➔n➔ ➔p➔u➔s➔h➔e➔d➔ ➔t➔o➔ ➔a➔ ➔s➔h➔a➔r➔e➔d➔ ➔r➔e➔m➔o➔t➔e➔ ➔b➔r➔a➔n➔c➔h➔.➔
➔1➔6➔.➔ ➔g➔i➔t➔ ➔t➔a➔g➔ ➔—➔ ➔M➔a➔r➔k➔i➔n➔g➔ ➔R➔e➔l➔e➔a➔s➔e➔s➔
➔g➔i➔t➔ ➔t➔a➔g➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔a➔l➔l➔ ➔t➔a➔g➔s➔
➔g➔i➔t➔ ➔t➔a➔g➔ ➔v➔1➔.➔0➔.➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔l➔i➔g➔h➔t➔w➔e➔i➔g➔h➔t➔ ➔t➔a➔g➔
➔g➔i➔t➔ ➔t➔a➔g➔ ➔-➔a➔ ➔v➔1➔.➔0➔.➔0➔ ➔-➔m➔ ➔"➔R➔e➔l➔e➔a➔s➔e➔ ➔1➔.➔0➔.➔0➔"➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔a➔n➔n➔o➔t➔a➔t➔e➔d➔ ➔t➔a➔g➔ ➔(➔r➔e➔c➔o➔m➔m➔e➔n➔d➔e➔d➔)➔
➔g➔i➔t➔ ➔t➔a➔g➔ ➔-➔a➔ ➔v➔1➔.➔0➔.➔0➔ ➔<➔c➔o➔m➔m➔i➔t➔-➔i➔d➔>➔ ➔ ➔ ➔ ➔#➔ ➔t➔a➔g➔ ➔a➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔c➔o➔m➔m➔i➔t➔
➔g➔i➔t➔ ➔p➔u➔s➔h➔ ➔o➔r➔i➔g➔i➔n➔ ➔v➔1➔.➔0➔.➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔u➔s➔h➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔t➔a➔g➔
➔g➔i➔t➔ ➔p➔u➔s➔h➔ ➔o➔r➔i➔g➔i➔n➔ ➔-➔-➔t➔a➔g➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔u➔s➔h➔ ➔a➔l➔l➔ ➔t➔a➔g➔s➔
➔g➔i➔t➔ ➔t➔a➔g➔ ➔-➔d➔ ➔v➔1➔.➔0➔.➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔l➔o➔c➔a➔l➔ ➔t➔a➔g➔
➔g➔i➔t➔ ➔p➔u➔s➔h➔ ➔o➔r➔i➔g➔i➔n➔ ➔-➔-➔d➔e➔l➔e➔t➔e➔ ➔v➔1➔.➔0➔.➔0➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔r➔e➔m➔o➔t➔e➔ ➔t➔a➔g➔
➔U➔s➔e➔ ➔i➔n➔ ➔D➔e➔v➔O➔p➔s➔:➔ ➔T➔a➔g➔ ➔r➔e➔l➔e➔a➔s➔e➔s➔ ➔i➔n➔ ➔C➔I➔/➔C➔D➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔s➔.➔ ➔W➔h➔e➔n➔ ➔y➔o➔u➔ ➔t➔a➔g➔ ➔a➔ ➔c➔o➔m➔m➔i➔t➔,➔ ➔t➔h➔e➔ ➔p➔i➔p➔e➔l➔i➔n➔e➔ ➔a➔u➔t➔o➔m➔a➔t➔i➔c➔a➔l➔l➔y➔ ➔b➔u➔i➔l➔d➔s➔ ➔a➔n➔d➔
➔d➔e➔p➔l➔o➔y➔s➔ ➔t➔h➔a➔t➔ ➔v➔e➔r➔s➔i➔o➔n➔.➔
➔1➔7➔.➔ ➔.➔g➔i➔t➔i➔g➔n➔o➔r➔e➔ ➔—➔ ➔E➔x➔c➔l➔u➔d➔i➔n➔g➔ ➔F➔i➔l➔e➔s➔ ➔f➔r➔o➔m➔ ➔G➔i➔t➔
➔.➔g➔i➔t➔i➔g➔n➔o➔r➔e➔ ➔t➔e➔l➔l➔s➔ ➔G➔i➔t➔ ➔w➔h➔i➔c➔h➔ ➔f➔i➔l➔e➔s➔ ➔t➔o➔ ➔n➔e➔v➔e➔r➔ ➔t➔r➔a➔c➔k➔.➔
➔#➔ ➔E➔x➔a➔m➔p➔l➔e➔ ➔.➔g➔i➔t➔i➔g➔n➔o➔r➔e➔ ➔f➔i➔l➔e➔:➔
➔n➔o➔d➔e➔_➔m➔o➔d➔u➔l➔e➔s➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔p➔e➔n➔d➔e➔n➔c➔y➔ ➔f➔o➔l➔d➔e➔r➔s➔
➔.➔e➔n➔v➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔ ➔(➔N➔E➔V➔E➔R➔ ➔c➔o➔m➔m➔i➔t➔ ➔s➔e➔c➔r➔e➔t➔s➔)➔
➔*➔.➔l➔o➔g➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔o➔g➔ ➔f➔i➔l➔e➔s➔
➔d➔i➔s➔t➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔b➔u➔i➔l➔d➔ ➔o➔u➔t➔p➔u➔t➔
➔.➔D➔S➔_➔S➔t➔o➔r➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔M➔a➔c➔ ➔s➔y➔s➔t➔e➔m➔ ➔f➔i➔l➔e➔s➔
➔*➔.➔j➔a➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔m➔p➔i➔l➔e➔d➔ ➔J➔a➔v➔a➔ ➔f➔i➔l➔e➔s➔
➔t➔a➔r➔g➔e➔t➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔M➔a➔v➔e➔n➔ ➔b➔u➔i➔l➔d➔ ➔f➔o➔l➔d➔e➔r➔
➔_➔_➔p➔y➔c➔a➔c➔h➔e➔_➔_➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔P➔y➔t➔h➔o➔n➔ ➔c➔a➔c➔h➔e➔
➔#➔ ➔C➔h➔e➔c➔k➔ ➔w➔h➔a➔t➔'➔s➔ ➔b➔e➔i➔n➔g➔ ➔i➔g➔n➔o➔r➔e➔d➔
➔g➔i➔t➔ ➔s➔t➔a➔t➔u➔s➔ ➔-➔-➔i➔g➔n➔o➔r➔e➔d➔
➔#➔ ➔I➔f➔ ➔y➔o➔u➔ ➔a➔c➔c➔i➔d➔e➔n➔t➔a➔l➔l➔y➔ ➔c➔o➔m➔m➔i➔t➔t➔e➔d➔ ➔s➔o➔m➔e➔t➔h➔i➔n➔g➔:➔
➔
➔
➔
➔
➔g➔i➔t➔ ➔r➔m➔ ➔-➔-➔c➔a➔c➔h➔e➔d➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔
➔e➔c➔h➔o➔ ➔"➔f➔i➔l➔e➔n➔a➔m➔e➔"➔ ➔>➔>➔ ➔.➔g➔i➔t➔i➔g➔n➔o➔r➔e➔
➔g➔i➔t➔ ➔c➔o➔m➔m➔i➔t➔ ➔-➔m➔ ➔"➔R➔e➔m➔o➔v➔e➔ ➔a➔c➔c➔i➔d➔e➔n➔t➔a➔l➔l➔y➔ ➔c➔o➔m➔m➔i➔t➔t➔e➔d➔ ➔f➔i➔l➔e➔"➔
➔1➔8➔.➔ ➔G➔i➔t➔ ➔B➔r➔a➔n➔c➔h➔i➔n➔g➔ ➔S➔t➔r➔a➔t➔e➔g➔i➔e➔s➔
➔A➔)➔ ➔G➔i➔t➔f➔l➔o➔w➔
➔C➔l➔a➔s➔s➔i➔c➔ ➔s➔t➔r➔a➔t➔e➔g➔y➔ ➔w➔i➔t➔h➔ ➔l➔o➔n➔g➔-➔l➔i➔v➔e➔d➔ ➔b➔r➔a➔n➔c➔h➔e➔s➔:➔
➔m➔a➔i➔n➔ ➔ ➔—➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔c➔o➔d➔e➔ ➔o➔n➔l➔y➔
➔d➔e➔v➔e➔l➔o➔p➔ ➔ ➔—➔ ➔i➔n➔t➔e➔g➔r➔a➔t➔i➔o➔n➔ ➔b➔r➔a➔n➔c➔h➔
➔f➔e➔a➔t➔u➔r➔e➔/➔*➔ ➔ ➔—➔ ➔n➔e➔w➔ ➔f➔e➔a➔t➔u➔r➔e➔s➔
➔r➔e➔l➔e➔a➔s➔e➔/➔*➔ ➔ ➔—➔ ➔r➔e➔l➔e➔a➔s➔e➔ ➔p➔r➔e➔p➔a➔r➔a➔t➔i➔o➔n➔
➔h➔o➔t➔f➔i➔x➔/➔*➔ ➔ ➔—➔ ➔u➔r➔g➔e➔n➔t➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔f➔i➔x➔e➔s➔
➔B➔)➔ ➔G➔i➔t➔H➔u➔b➔ ➔F➔l➔o➔w➔ ➔(➔R➔e➔c➔o➔m➔m➔e➔n➔d➔e➔d➔ ➔f➔o➔r➔ ➔D➔e➔v➔O➔p➔s➔)➔
➔S➔i➔m➔p➔l➔e➔r➔,➔ ➔f➔a➔s➔t➔e➔r➔:➔
➔m➔a➔i➔n➔ ➔ ➔—➔ ➔a➔l➔w➔a➔y➔s➔ ➔d➔e➔p➔l➔o➔y➔a➔b➔l➔e➔
➔f➔e➔a➔t➔u➔r➔e➔/➔*➔ ➔ ➔—➔ ➔s➔h➔o➔r➔t➔-➔l➔i➔v➔e➔d➔ ➔f➔e➔a➔t➔u➔r➔e➔ ➔b➔r➔a➔n➔c➔h➔e➔s➔
➔C➔r➔e➔a➔t➔e➔ ➔P➔R➔ ➔→➔ ➔r➔e➔v➔i➔e➔w➔ ➔→➔ ➔m➔e➔r➔g➔e➔ ➔t➔o➔ ➔m➔a➔i➔n➔ ➔→➔ ➔d➔e➔p➔l➔o➔y➔
➔C➔)➔ ➔T➔r➔u➔n➔k➔ ➔B➔a➔s➔e➔d➔ ➔D➔e➔v➔e➔l➔o➔p➔m➔e➔n➔t➔
➔E➔v➔e➔r➔y➔o➔n➔e➔ ➔c➔o➔m➔m➔i➔t➔s➔ ➔d➔i➔r➔e➔c➔t➔l➔y➔ ➔t➔o➔ ➔m➔a➔i➔n➔ ➔ ➔(➔t➔r➔u➔n➔k➔)➔
➔V➔e➔r➔y➔ ➔s➔h➔o➔r➔t➔-➔l➔i➔v➔e➔d➔ ➔b➔r➔a➔n➔c➔h➔e➔s➔ ➔(➔h➔o➔u➔r➔s➔,➔ ➔n➔o➔t➔ ➔d➔a➔y➔s➔)➔
➔H➔e➔a➔v➔y➔ ➔u➔s➔e➔ ➔o➔f➔ ➔f➔e➔a➔t➔u➔r➔e➔ ➔f➔l➔a➔g➔s➔
➔U➔s➔e➔d➔ ➔b➔y➔ ➔h➔i➔g➔h➔-➔v➔e➔l➔o➔c➔i➔t➔y➔ ➔t➔e➔a➔m➔s➔ ➔l➔i➔k➔e➔ ➔G➔o➔o➔g➔l➔e➔
➔1➔9➔.➔ ➔P➔u➔l➔l➔ ➔R➔e➔q➔u➔e➔s➔t➔ ➔(➔P➔R➔)➔ ➔W➔o➔r➔k➔f➔l➔o➔w➔
➔#➔ ➔1➔.➔ ➔C➔r➔e➔a➔t➔e➔ ➔f➔e➔a➔t➔u➔r➔e➔ ➔b➔r➔a➔n➔c➔h➔
➔g➔i➔t➔ ➔s➔w➔i➔t➔c➔h➔ ➔-➔c➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔p➔a➔y➔m➔e➔n➔t➔
➔#➔ ➔2➔.➔ ➔M➔a➔k➔e➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔a➔n➔d➔ ➔c➔o➔m➔m➔i➔t➔
➔
➔
➔
➔
➔g➔i➔t➔ ➔a➔d➔d➔ ➔.➔
➔g➔i➔t➔ ➔c➔o➔m➔m➔i➔t➔ ➔-➔m➔ ➔"➔A➔d➔d➔ ➔p➔a➔y➔m➔e➔n➔t➔ ➔g➔a➔t➔e➔w➔a➔y➔"➔
➔#➔ ➔3➔.➔ ➔P➔u➔s➔h➔ ➔t➔o➔ ➔r➔e➔m➔o➔t➔e➔
➔g➔i➔t➔ ➔p➔u➔s➔h➔ ➔-➔u➔ ➔o➔r➔i➔g➔i➔n➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔p➔a➔y➔m➔e➔n➔t➔
➔#➔ ➔4➔.➔ ➔C➔r➔e➔a➔t➔e➔ ➔P➔R➔ ➔o➔n➔ ➔G➔i➔t➔H➔u➔b➔/➔G➔i➔t➔L➔a➔b➔/➔A➔z➔u➔r➔e➔ ➔R➔e➔p➔o➔s➔
➔#➔ ➔—➔ ➔A➔d➔d➔ ➔d➔e➔s➔c➔r➔i➔p➔t➔i➔o➔n➔ ➔o➔f➔ ➔w➔h➔a➔t➔ ➔c➔h➔a➔n➔g➔e➔d➔ ➔a➔n➔d➔ ➔w➔h➔y➔
➔#➔ ➔—➔ ➔L➔i➔n➔k➔ ➔t➔o➔ ➔t➔a➔s➔k➔/➔t➔i➔c➔k➔e➔t➔ ➔(➔i➔n➔ ➔y➔o➔u➔r➔ ➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔ ➔p➔r➔o➔j➔e➔c➔t➔ ➔y➔o➔u➔ ➔u➔s➔e➔d➔ ➔P➔R➔ ➔t➔e➔m➔p➔l➔a➔t➔e➔s➔)➔
➔#➔ ➔—➔ ➔R➔e➔q➔u➔e➔s➔t➔ ➔r➔e➔v➔i➔e➔w➔e➔r➔s➔
➔#➔ ➔5➔.➔ ➔A➔f➔t➔e➔r➔ ➔r➔e➔v➔i➔e➔w➔ ➔a➔n➔d➔ ➔a➔p➔p➔r➔o➔v➔a➔l➔ ➔—➔ ➔m➔e➔r➔g➔e➔ ➔t➔o➔ ➔m➔a➔i➔n➔
➔#➔ ➔6➔.➔ ➔D➔e➔l➔e➔t➔e➔ ➔f➔e➔a➔t➔u➔r➔e➔ ➔b➔r➔a➔n➔c➔h➔
➔g➔i➔t➔ ➔b➔r➔a➔n➔c➔h➔ ➔-➔d➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔p➔a➔y➔m➔e➔n➔t➔
➔g➔i➔t➔ ➔p➔u➔s➔h➔ ➔o➔r➔i➔g➔i➔n➔ ➔-➔-➔d➔e➔l➔e➔t➔e➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔p➔a➔y➔m➔e➔n➔t➔
➔2➔0➔.➔ ➔C➔o➔m➔m➔o➔n➔ ➔G➔i➔t➔ ➔I➔n➔t➔e➔r➔v➔i➔e➔w➔ ➔Q➔u➔e➔s➔t➔i➔o➔n➔s➔
➔Q➔:➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔H➔E➔A➔D➔ ➔i➔n➔ ➔G➔i➔t➔?➔
➔H➔E➔A➔D➔ ➔i➔s➔ ➔a➔ ➔p➔o➔i➔n➔t➔e➔r➔ ➔t➔o➔ ➔t➔h➔e➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔c➔o➔m➔m➔i➔t➔ ➔y➔o➔u➔'➔r➔e➔ ➔o➔n➔.➔ ➔U➔s➔u➔a➔l➔l➔y➔ ➔p➔o➔i➔n➔t➔s➔ ➔t➔o➔ ➔t➔h➔e➔ ➔t➔i➔p➔ ➔o➔f➔ ➔y➔o➔u➔r➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔b➔r➔a➔n➔c➔h➔.➔ ➔W➔h➔e➔n➔ ➔y➔o➔u➔
➔c➔h➔e➔c➔k➔o➔u➔t➔ ➔a➔ ➔b➔r➔a➔n➔c➔h➔,➔ ➔H➔E➔A➔D➔ ➔m➔o➔v➔e➔s➔ ➔t➔o➔ ➔t➔h➔a➔t➔ ➔b➔r➔a➔n➔c➔h➔'➔s➔ ➔l➔a➔t➔e➔s➔t➔ ➔c➔o➔m➔m➔i➔t➔.➔
➔Q➔:➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔d➔e➔t➔a➔c➔h➔e➔d➔ ➔H➔E➔A➔D➔?➔
➔W➔h➔e➔n➔ ➔H➔E➔A➔D➔ ➔p➔o➔i➔n➔t➔s➔ ➔d➔i➔r➔e➔c➔t➔l➔y➔ ➔t➔o➔ ➔a➔ ➔c➔o➔m➔m➔i➔t➔ ➔i➔n➔s➔t➔e➔a➔d➔ ➔o➔f➔ ➔a➔ ➔b➔r➔a➔n➔c➔h➔.➔ ➔H➔a➔p➔p➔e➔n➔s➔ ➔w➔h➔e➔n➔ ➔y➔o➔u➔ ➔g➔i➔t➔ ➔c➔h➔e➔c➔k➔o➔u➔t➔ ➔.➔ ➔A➔n➔y➔
➔c➔o➔m➔m➔i➔t➔s➔ ➔m➔a➔d➔e➔ ➔i➔n➔ ➔d➔e➔t➔a➔c➔h➔e➔d➔ ➔H➔E➔A➔D➔ ➔s➔t➔a➔t➔e➔ ➔c➔a➔n➔ ➔b➔e➔ ➔l➔o➔s➔t➔.➔ ➔C➔r➔e➔a➔t➔e➔ ➔a➔ ➔b➔r➔a➔n➔c➔h➔ ➔t➔o➔ ➔s➔a➔v➔e➔ ➔w➔o➔r➔k➔:➔ ➔g➔i➔t➔ ➔s➔w➔i➔t➔c➔h➔ ➔-➔c➔ ➔n➔e➔w➔-➔
➔b➔r➔a➔n➔c➔h➔
➔Q➔:➔ ➔D➔i➔f➔f➔e➔r➔e➔n➔c➔e➔ ➔b➔e➔t➔w➔e➔e➔n➔ ➔g➔i➔t➔ ➔p➔u➔l➔l➔ ➔a➔n➔d➔ ➔g➔i➔t➔ ➔f➔e➔t➔c➔h➔?➔
➔g➔i➔t➔ ➔f➔e➔t➔c➔h➔ ➔ ➔d➔o➔w➔n➔l➔o➔a➔d➔s➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔b➔u➔t➔ ➔d➔o➔e➔s➔n➔'➔t➔ ➔m➔e➔r➔g➔e➔.➔ ➔g➔i➔t➔ ➔p➔u➔l➔l➔ ➔ ➔d➔o➔w➔n➔l➔o➔a➔d➔s➔ ➔A➔N➔D➔ ➔m➔e➔r➔g➔e➔s➔.➔ ➔U➔s➔e➔ ➔f➔e➔t➔c➔h➔ ➔w➔h➔e➔n➔
➔y➔o➔u➔ ➔w➔a➔n➔t➔ ➔t➔o➔ ➔r➔e➔v➔i➔e➔w➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔b➔e➔f➔o➔r➔e➔ ➔m➔e➔r➔g➔i➔n➔g➔.➔
➔Q➔:➔ ➔H➔o➔w➔ ➔d➔o➔ ➔y➔o➔u➔ ➔s➔q➔u➔a➔s➔h➔ ➔c➔o➔m➔m➔i➔t➔s➔?➔
➔g➔i➔t➔ ➔r➔e➔b➔a➔s➔e➔ ➔-➔i➔ ➔H➔E➔A➔D➔~➔3➔ ➔ ➔ ➔ ➔#➔ ➔i➔n➔t➔e➔r➔a➔c➔t➔i➔v➔e➔l➔y➔ ➔s➔q➔u➔a➔s➔h➔ ➔l➔a➔s➔t➔ ➔3➔ ➔c➔o➔m➔m➔i➔t➔s➔
➔#➔ ➔c➔h➔a➔n➔g➔e➔ ➔'➔p➔i➔c➔k➔'➔ ➔t➔o➔ ➔'➔s➔q➔u➔a➔s➔h➔'➔ ➔f➔o➔r➔ ➔c➔o➔m➔m➔i➔t➔s➔ ➔t➔o➔ ➔c➔o➔m➔b➔i➔n➔e➔
➔Q➔:➔ ➔H➔o➔w➔ ➔d➔o➔ ➔y➔o➔u➔ ➔f➔i➔n➔d➔ ➔w➔h➔i➔c➔h➔ ➔c➔o➔m➔m➔i➔t➔ ➔i➔n➔t➔r➔o➔d➔u➔c➔e➔d➔ ➔a➔ ➔b➔u➔g➔?➔
➔g➔i➔t➔ ➔b➔i➔s➔e➔c➔t➔ ➔s➔t➔a➔r➔t➔
➔g➔i➔t➔ ➔b➔i➔s➔e➔c➔t➔ ➔b➔a➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔c➔o➔m➔m➔i➔t➔ ➔i➔s➔ ➔b➔a➔d➔
➔g➔i➔t➔ ➔b➔i➔s➔e➔c➔t➔ ➔g➔o➔o➔d➔ ➔<➔c➔o➔m➔m➔i➔t➔-➔i➔d➔>➔ ➔#➔ ➔l➔a➔s➔t➔ ➔k➔n➔o➔w➔n➔ ➔g➔o➔o➔d➔ ➔c➔o➔m➔m➔i➔t➔
➔
➔
➔
➔
➔#➔ ➔G➔i➔t➔ ➔c➔h➔e➔c➔k➔s➔ ➔o➔u➔t➔ ➔c➔o➔m➔m➔i➔t➔s➔ ➔b➔e➔t➔w➔e➔e➔n➔ ➔—➔ ➔y➔o➔u➔ ➔t➔e➔s➔t➔ ➔e➔a➔c➔h➔ ➔o➔n➔e➔
➔g➔i➔t➔ ➔b➔i➔s➔e➔c➔t➔ ➔g➔o➔o➔d➔/➔b➔a➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔m➔a➔r➔k➔ ➔e➔a➔c➔h➔ ➔u➔n➔t➔i➔l➔ ➔b➔u➔g➔ ➔i➔s➔ ➔f➔o➔u➔n➔d➔
➔g➔i➔t➔ ➔b➔i➔s➔e➔c➔t➔ ➔r➔e➔s➔e➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔n➔d➔ ➔b➔i➔s➔e➔c➔t➔
➔2➔1➔.➔ ➔Q➔u➔i➔c➔k➔ ➔R➔e➔f➔e➔r➔e➔n➔c➔e➔ ➔—➔ ➔M➔o➔s➔t➔ ➔U➔s➔e➔d➔ ➔G➔i➔t➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔
➔#➔ ➔D➔A➔I➔L➔Y➔ ➔W➔O➔R➔K➔F➔L➔O➔W➔
➔g➔i➔t➔ ➔s➔t➔a➔t➔u➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔e➔c➔k➔ ➔w➔h➔a➔t➔'➔s➔ ➔c➔h➔a➔n➔g➔e➔d➔
➔g➔i➔t➔ ➔a➔d➔d➔ ➔.➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔t➔a➔g➔e➔ ➔a➔l➔l➔ ➔c➔h➔a➔n➔g➔e➔s➔
➔g➔i➔t➔ ➔c➔o➔m➔m➔i➔t➔ ➔-➔m➔ ➔"➔m➔e➔s➔s➔a➔g➔e➔"➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔m➔m➔i➔t➔
➔g➔i➔t➔ ➔p➔u➔s➔h➔ ➔o➔r➔i➔g➔i➔n➔ ➔b➔r➔a➔n➔c➔h➔-➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔u➔s➔h➔ ➔t➔o➔ ➔r➔e➔m➔o➔t➔e➔
➔g➔i➔t➔ ➔p➔u➔l➔l➔ ➔o➔r➔i➔g➔i➔n➔ ➔m➔a➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔g➔e➔t➔ ➔l➔a➔t➔e➔s➔t➔ ➔c➔h➔a➔n➔g➔e➔s➔
➔#➔ ➔B➔R➔A➔N➔C➔H➔I➔N➔G➔
➔g➔i➔t➔ ➔s➔w➔i➔t➔c➔h➔ ➔-➔c➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔a➔n➔d➔ ➔s➔w➔i➔t➔c➔h➔ ➔t➔o➔ ➔n➔e➔w➔ ➔b➔r➔a➔n➔c➔h➔
➔g➔i➔t➔ ➔s➔w➔i➔t➔c➔h➔ ➔m➔a➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔g➔o➔ ➔b➔a➔c➔k➔ ➔t➔o➔ ➔m➔a➔i➔n➔
➔g➔i➔t➔ ➔m➔e➔r➔g➔e➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔m➔e➔r➔g➔e➔ ➔f➔e➔a➔t➔u➔r➔e➔ ➔i➔n➔t➔o➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔b➔r➔a➔n➔c➔h➔
➔g➔i➔t➔ ➔b➔r➔a➔n➔c➔h➔ ➔-➔d➔ ➔f➔e➔a➔t➔u➔r➔e➔-➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔b➔r➔a➔n➔c➔h➔ ➔a➔f➔t➔e➔r➔ ➔m➔e➔r➔g➔e➔
➔#➔ ➔U➔N➔D➔O➔I➔N➔G➔
➔g➔i➔t➔ ➔r➔e➔s➔t➔o➔r➔e➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔i➔s➔c➔a➔r➔d➔ ➔w➔o➔r➔k➔i➔n➔g➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔c➔h➔a➔n➔g➔e➔s➔
➔g➔i➔t➔ ➔r➔e➔s➔e➔t➔ ➔H➔E➔A➔D➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔u➔n➔s➔t➔a➔g➔e➔ ➔a➔ ➔f➔i➔l➔e➔
➔g➔i➔t➔ ➔r➔e➔s➔e➔t➔ ➔-➔-➔s➔o➔f➔t➔ ➔H➔E➔A➔D➔~➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔u➔n➔d➔o➔ ➔l➔a➔s➔t➔ ➔c➔o➔m➔m➔i➔t➔,➔ ➔k➔e➔e➔p➔ ➔c➔h➔a➔n➔g➔e➔s➔ ➔s➔t➔a➔g➔e➔d➔
➔g➔i➔t➔ ➔r➔e➔s➔e➔t➔ ➔-➔-➔h➔a➔r➔d➔ ➔H➔E➔A➔D➔~➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔u➔n➔d➔o➔ ➔l➔a➔s➔t➔ ➔c➔o➔m➔m➔i➔t➔,➔ ➔D➔E➔L➔E➔T➔E➔ ➔c➔h➔a➔n➔g➔e➔s➔
➔g➔i➔t➔ ➔r➔e➔v➔e➔r➔t➔ ➔<➔c➔o➔m➔m➔i➔t➔-➔i➔d➔>➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔a➔f➔e➔l➔y➔ ➔u➔n➔d➔o➔ ➔p➔u➔s➔h➔e➔d➔ ➔c➔o➔m➔m➔i➔t➔
➔#➔ ➔R➔E➔M➔O➔T➔E➔
➔g➔i➔t➔ ➔r➔e➔m➔o➔t➔e➔ ➔-➔v➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔v➔i➔e➔w➔ ➔r➔e➔m➔o➔t➔e➔s➔
➔g➔i➔t➔ ➔f➔e➔t➔c➔h➔ ➔o➔r➔i➔g➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔o➔w➔n➔l➔o➔a➔d➔ ➔w➔i➔t➔h➔o➔u➔t➔ ➔m➔e➔r➔g➔i➔n➔g➔
➔g➔i➔t➔ ➔p➔u➔l➔l➔ ➔o➔r➔i➔g➔i➔n➔ ➔m➔a➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔o➔w➔n➔l➔o➔a➔d➔ ➔a➔n➔d➔ ➔m➔e➔r➔g➔e➔
➔g➔i➔t➔ ➔p➔u➔s➔h➔ ➔o➔r➔i➔g➔i➔n➔ ➔b➔r➔a➔n➔c➔h➔-➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔u➔p➔l➔o➔a➔d➔ ➔t➔o➔ ➔r➔e➔m➔o➔t➔e➔
➔g➔i➔t➔ ➔c➔l➔o➔n➔e➔ ➔<➔u➔r➔l➔>➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔p➔y➔ ➔r➔e➔m➔o➔t➔e➔ ➔r➔e➔p➔o➔ ➔l➔o➔c➔a➔l➔l➔y➔
➔#➔ ➔I➔N➔S➔P➔E➔C➔T➔I➔O➔N➔
➔g➔i➔t➔ ➔l➔o➔g➔ ➔-➔-➔o➔n➔e➔l➔i➔n➔e➔ ➔-➔-➔g➔r➔a➔p➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔v➔i➔s➔u➔a➔l➔ ➔h➔i➔s➔t➔o➔r➔y➔
➔g➔i➔t➔ ➔d➔i➔f➔f➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔e➔ ➔u➔n➔s➔t➔a➔g➔e➔d➔ ➔c➔h➔a➔n➔g➔e➔s➔
➔g➔i➔t➔ ➔s➔h➔o➔w➔ ➔<➔c➔o➔m➔m➔i➔t➔-➔i➔d➔>➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔e➔ ➔c➔o➔m➔m➔i➔t➔ ➔d➔e➔t➔a➔i➔l➔s➔
➔g➔i➔t➔ ➔b➔l➔a➔m➔e➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔w➔h➔o➔ ➔c➔h➔a➔n➔g➔e➔d➔ ➔e➔a➔c➔h➔ ➔l➔i➔n➔e➔
➔#➔ ➔A➔D➔V➔A➔N➔C➔E➔D➔
➔g➔i➔t➔ ➔s➔t➔a➔s➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔a➔v➔e➔ ➔w➔o➔r➔k➔ ➔t➔e➔m➔p➔o➔r➔a➔r➔i➔l➔y➔
➔g➔i➔t➔ ➔s➔t➔a➔s➔h➔ ➔p➔o➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔s➔t➔o➔r➔e➔ ➔s➔a➔v➔e➔d➔ ➔w➔o➔r➔k➔
➔g➔i➔t➔ ➔c➔h➔e➔r➔r➔y➔-➔p➔i➔c➔k➔ ➔<➔c➔o➔m➔m➔i➔t➔-➔i➔d➔>➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔p➔p➔l➔y➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔c➔o➔m➔m➔i➔t➔
➔
➔
➔
➔
➔g➔i➔t➔ ➔r➔e➔b➔a➔s➔e➔ ➔m➔a➔i➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔b➔a➔s➔e➔ ➔o➔n➔t➔o➔ ➔m➔a➔i➔n➔
➔g➔i➔t➔ ➔t➔a➔g➔ ➔-➔a➔ ➔v➔1➔.➔0➔.➔0➔ ➔-➔m➔ ➔"➔R➔e➔l➔e➔a➔s➔e➔"➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔r➔e➔l➔e➔a➔s➔e➔ ➔t➔a➔g➔
➔
