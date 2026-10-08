# 🐧 Linux Systems & Networking: The Definitive Master Engineering Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers OS Kernel Architecture, Process Hierarchy, File Permissions, Modern Networking (`ss`/`ip`), Computer Networking Fundamentals (OSI, TCP/IP, DNS), Bash Strict Mode, and Performance Triage.

---

## 📑 Table of Contents
- [Linux Operating System Architecture](#linux-architecture)
- [File System Hierarchy & Permissions (Octal 755/644, SUID/SGID)](#file-system--permissions)
- [Process Management & Lifecycle (Zombies vs Orphans, Signals)](#process-management)
- [System Performance Diagnosis (CPU Load, Available RAM, Disk I/O)](#system-performance)
- [Modern System Administration & systemd Services](#systemd-services)
- [Computer Networking Fundamentals (OSI 7 Layers, TCP 3-Way Handshake, DNS)](#networking-fundamentals)
- [Modern Networking Command Cheat Sheet (`ss` vs `netstat`)](#networking-commands)
- [Production Bash Shell Scripting Blueprint](#bash-scripting)
- [Troubleshooting Playbook & Senior Interview Q&A](#troubleshooting-playbook)

---

# PART 1: LINUX SYSTEMS ADMINISTRATION

➔S➔E➔C➔T➔I➔O➔N➔ ➔6➔:➔ ➔L➔I➔N➔U➔X➔ ➔—➔ ➔C➔O➔M➔P➔L➔E➔T➔E➔ ➔G➔U➔I➔D➔E➔
➔F➔l➔o➔w➔:➔ ➔I➔n➔t➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔→➔ ➔D➔i➔s➔t➔r➔i➔b➔u➔t➔i➔o➔n➔s➔ ➔→➔ ➔S➔t➔r➔u➔c➔t➔u➔r➔e➔ ➔→➔ ➔S➔h➔e➔l➔l➔ ➔→➔ ➔F➔i➔l➔e➔ ➔S➔y➔s➔t➔e➔m➔ ➔→➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔ ➔→➔ ➔U➔s➔e➔r➔s➔ ➔&➔ ➔G➔r➔o➔u➔p➔s➔ ➔→➔
➔P➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔ ➔→➔ ➔C➔o➔m➔p➔r➔e➔s➔s➔i➔o➔n➔ ➔→➔ ➔F➔i➔l➔t➔e➔r➔s➔ ➔→➔ ➔N➔e➔t➔w➔o➔r➔k➔i➔n➔g➔ ➔→➔ ➔A➔d➔v➔a➔n➔c➔e➔d➔
➔1➔.➔ ➔W➔h➔a➔t➔ ➔i➔s➔ ➔L➔i➔n➔u➔x➔?➔
➔D➔e➔f➔i➔n➔i➔t➔i➔o➔n➔:➔
➔L➔i➔n➔u➔x➔ ➔i➔s➔ ➔a➔ ➔f➔r➔e➔e➔,➔ ➔o➔p➔e➔n➔-➔s➔o➔u➔r➔c➔e➔ ➔U➔n➔i➔x➔-➔l➔i➔k➔e➔ ➔o➔p➔e➔r➔a➔t➔i➔n➔g➔ ➔s➔y➔s➔t➔e➔m➔ ➔k➔e➔r➔n➔e➔l➔ ➔c➔r➔e➔a➔t➔e➔d➔ ➔b➔y➔ ➔L➔i➔n➔u➔s➔ ➔T➔o➔r➔v➔a➔l➔d➔s➔ ➔i➔n➔ ➔1➔9➔9➔1➔.➔ ➔I➔t➔ ➔i➔s➔ ➔t➔h➔e➔
➔f➔o➔u➔n➔d➔a➔t➔i➔o➔n➔ ➔o➔f➔ ➔m➔o➔s➔t➔ ➔s➔e➔r➔v➔e➔r➔s➔,➔ ➔c➔l➔o➔u➔d➔ ➔i➔n➔f➔r➔a➔s➔t➔r➔u➔c➔t➔u➔r➔e➔,➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔,➔ ➔a➔n➔d➔ ➔D➔e➔v➔O➔p➔s➔ ➔t➔o➔o➔l➔i➔n➔g➔ ➔i➔n➔ ➔t➔h➔e➔ ➔w➔o➔r➔l➔d➔.➔
➔K➔e➔y➔ ➔F➔e➔a➔t➔u➔r➔e➔s➔:➔
➔O➔p➔e➔n➔ ➔S➔o➔u➔r➔c➔e➔ ➔—➔ ➔s➔o➔u➔r➔c➔e➔ ➔c➔o➔d➔e➔ ➔i➔s➔ ➔f➔r➔e➔e➔l➔y➔ ➔a➔v➔a➔i➔l➔a➔b➔l➔e➔,➔ ➔a➔n➔y➔o➔n➔e➔ ➔c➔a➔n➔ ➔m➔o➔d➔i➔f➔y➔ ➔a➔n➔d➔ ➔d➔i➔s➔t➔r➔i➔b➔u➔t➔e➔
➔M➔u➔l➔t➔i➔-➔u➔s➔e➔r➔ ➔—➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔u➔s➔e➔r➔s➔ ➔c➔a➔n➔ ➔l➔o➔g➔ ➔i➔n➔ ➔a➔n➔d➔ ➔w➔o➔r➔k➔ ➔s➔i➔m➔u➔l➔t➔a➔n➔e➔o➔u➔s➔l➔y➔
➔M➔u➔l➔t➔i➔-➔t➔a➔s➔k➔i➔n➔g➔ ➔—➔ ➔r➔u➔n➔s➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔p➔r➔o➔c➔e➔s➔s➔e➔s➔ ➔a➔t➔ ➔t➔h➔e➔ ➔s➔a➔m➔e➔ ➔t➔i➔m➔e➔
➔S➔e➔c➔u➔r➔e➔ ➔—➔ ➔s➔t➔r➔o➔n➔g➔ ➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔ ➔m➔o➔d➔e➔l➔,➔ ➔l➔e➔s➔s➔ ➔v➔u➔l➔n➔e➔r➔a➔b➔l➔e➔ ➔t➔o➔ ➔v➔i➔r➔u➔s➔e➔s➔
➔S➔t➔a➔b➔l➔e➔ ➔—➔ ➔s➔e➔r➔v➔e➔r➔s➔ ➔r➔u➔n➔ ➔f➔o➔r➔ ➔y➔e➔a➔r➔s➔ ➔w➔i➔t➔h➔o➔u➔t➔ ➔r➔e➔b➔o➔o➔t➔i➔n➔g➔
➔P➔o➔r➔t➔a➔b➔l➔e➔ ➔—➔ ➔r➔u➔n➔s➔ ➔o➔n➔ ➔a➔l➔m➔o➔s➔t➔ ➔a➔n➔y➔ ➔h➔a➔r➔d➔w➔a➔r➔e➔
➔S➔h➔e➔l➔l➔/➔C➔L➔I➔ ➔—➔ ➔p➔o➔w➔e➔r➔f➔u➔l➔ ➔c➔o➔m➔m➔a➔n➔d➔-➔l➔i➔n➔e➔ ➔i➔n➔t➔e➔r➔f➔a➔c➔e➔ ➔f➔o➔r➔ ➔a➔u➔t➔o➔m➔a➔t➔i➔o➔n➔
➔F➔r➔e➔e➔ ➔—➔ ➔n➔o➔ ➔l➔i➔c➔e➔n➔s➔i➔n➔g➔ ➔c➔o➔s➔t➔ ➔(➔h➔u➔g➔e➔ ➔f➔o➔r➔ ➔D➔e➔v➔O➔p➔s➔ ➔a➔t➔ ➔s➔c➔a➔l➔e➔)➔
➔W➔h➔y➔ ➔D➔e➔v➔O➔p➔s➔ ➔u➔s➔e➔s➔ ➔L➔i➔n➔u➔x➔:➔
➔M➔o➔s➔t➔ ➔c➔l➔o➔u➔d➔ ➔s➔e➔r➔v➔e➔r➔s➔ ➔(➔A➔W➔S➔ ➔E➔C➔2➔,➔ ➔A➔z➔u➔r➔e➔ ➔V➔M➔s➔)➔ ➔r➔u➔n➔ ➔L➔i➔n➔u➔x➔
➔D➔o➔c➔k➔e➔r➔ ➔c➔o➔n➔t➔a➔i➔n➔e➔r➔s➔ ➔u➔s➔e➔ ➔L➔i➔n➔u➔x➔ ➔k➔e➔r➔n➔e➔l➔
➔M➔o➔s➔t➔ ➔D➔e➔v➔O➔p➔s➔ ➔t➔o➔o➔l➔s➔ ➔(➔J➔e➔n➔k➔i➔n➔s➔,➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔,➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔)➔ ➔r➔u➔n➔ ➔n➔a➔t➔i➔v➔e➔l➔y➔ ➔o➔n➔ ➔L➔i➔n➔u➔x➔
➔S➔h➔e➔l➔l➔ ➔s➔c➔r➔i➔p➔t➔i➔n➔g➔ ➔e➔n➔a➔b➔l➔e➔s➔ ➔p➔o➔w➔e➔r➔f➔u➔l➔ ➔a➔u➔t➔o➔m➔a➔t➔i➔o➔n➔
➔
➔
➔
➔
➔2➔.➔ ➔L➔i➔n➔u➔x➔ ➔D➔i➔s➔t➔r➔i➔b➔u➔t➔i➔o➔n➔s➔ ➔(➔D➔i➔s➔t➔r➔o➔s➔)➔
➔A➔ ➔L➔i➔n➔u➔x➔ ➔d➔i➔s➔t➔r➔i➔b➔u➔t➔i➔o➔n➔ ➔=➔ ➔L➔i➔n➔u➔x➔ ➔k➔e➔r➔n➔e➔l➔ ➔+➔ ➔p➔a➔c➔k➔a➔g➔e➔ ➔m➔a➔n➔a➔g➔e➔r➔ ➔+➔ ➔d➔e➔f➔a➔u➔l➔t➔ ➔s➔o➔f➔t➔w➔a➔r➔e➔ ➔+➔ ➔U➔I➔
➔D➔i➔s➔t➔r➔i➔b➔u➔t➔i➔o➔n➔ ➔P➔a➔c➔k➔a➔g➔e➔ ➔M➔a➔n➔a➔g➔e➔r➔ ➔U➔s➔e➔d➔ ➔F➔o➔r➔
➔U➔b➔u➔n➔t➔u➔ ➔a➔p➔t➔ ➔M➔o➔s➔t➔ ➔p➔o➔p➔u➔l➔a➔r➔,➔ ➔D➔e➔v➔O➔p➔s➔,➔ ➔b➔e➔g➔i➔n➔n➔e➔r➔s➔
➔R➔H➔E➔L➔ ➔(➔R➔e➔d➔ ➔H➔a➔t➔)➔ ➔y➔u➔m➔ ➔/➔ ➔d➔n➔f➔ ➔E➔n➔t➔e➔r➔p➔r➔i➔s➔e➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔ ➔s➔e➔r➔v➔e➔r➔s➔
➔C➔e➔n➔t➔O➔S➔ ➔y➔u➔m➔ ➔/➔ ➔d➔n➔f➔ ➔F➔r➔e➔e➔ ➔R➔H➔E➔L➔ ➔a➔l➔t➔e➔r➔n➔a➔t➔i➔v➔e➔ ➔(➔d➔e➔p➔r➔e➔c➔a➔t➔e➔d➔)➔
➔A➔m➔a➔z➔o➔n➔ ➔L➔i➔n➔u➔x➔ ➔y➔u➔m➔ ➔/➔ ➔d➔n➔f➔ ➔A➔W➔S➔ ➔E➔C➔2➔ ➔i➔n➔s➔t➔a➔n➔c➔e➔s➔
➔D➔e➔b➔i➔a➔n➔ ➔a➔p➔t➔ ➔S➔t➔a➔b➔l➔e➔ ➔s➔e➔r➔v➔e➔r➔s➔
➔A➔l➔p➔i➔n➔e➔ ➔a➔p➔k➔ ➔D➔o➔c➔k➔e➔r➔ ➔b➔a➔s➔e➔ ➔i➔m➔a➔g➔e➔s➔ ➔(➔t➔i➔n➔y➔,➔ ➔~➔5➔M➔B➔)➔
➔K➔a➔l➔i➔ ➔L➔i➔n➔u➔x➔ ➔a➔p➔t➔ ➔S➔e➔c➔u➔r➔i➔t➔y➔/➔p➔e➔n➔e➔t➔r➔a➔t➔i➔o➔n➔ ➔t➔e➔s➔t➔i➔n➔g➔
➔F➔e➔d➔o➔r➔a➔ ➔d➔n➔f➔ ➔C➔u➔t➔t➔i➔n➔g➔ ➔e➔d➔g➔e➔ ➔f➔e➔a➔t➔u➔r➔e➔s➔
➔F➔o➔r➔ ➔y➔o➔u➔r➔ ➔r➔e➔s➔u➔m➔e➔:➔ ➔Y➔o➔u➔ ➔u➔s➔e➔d➔ ➔U➔b➔u➔n➔t➔u➔ ➔a➔n➔d➔ ➔R➔H➔E➔L➔ ➔—➔ ➔m➔e➔n➔t➔i➔o➔n➔ ➔b➔o➔t➔h➔ ➔i➔n➔ ➔i➔n➔t➔e➔r➔v➔i➔e➔w➔s➔.➔
➔3➔.➔ ➔L➔i➔n➔u➔x➔ ➔A➔r➔c➔h➔i➔t➔e➔c➔t➔u➔r➔e➔ ➔/➔ ➔S➔t➔r➔u➔c➔t➔u➔r➔e➔
➔H➔a➔r➔d➔w➔a➔r➔e➔ ➔(➔C➔P➔U➔,➔ ➔R➔A➔M➔,➔ ➔D➔i➔s➔k➔,➔ ➔N➔e➔t➔w➔o➔r➔k➔)➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔↑➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔K➔e➔r➔n➔e➔l➔ ➔ ➔(➔c➔o➔r➔e➔ ➔o➔f➔ ➔O➔S➔ ➔—➔ ➔m➔a➔n➔a➔g➔e➔s➔ ➔h➔a➔r➔d➔w➔a➔r➔e➔,➔ ➔m➔e➔m➔o➔r➔y➔,➔ ➔p➔r➔o➔c➔e➔s➔s➔e➔s➔)➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔↑➔
➔ ➔ ➔ ➔S➔y➔s➔t➔e➔m➔ ➔L➔i➔b➔r➔a➔r➔i➔e➔s➔ ➔(➔g➔l➔i➔b➔c➔,➔ ➔e➔t➔c➔.➔)➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔↑➔
➔ ➔ ➔ ➔ ➔ ➔ ➔S➔h➔e➔l➔l➔ ➔ ➔(➔c➔o➔m➔m➔a➔n➔d➔ ➔i➔n➔t➔e➔r➔p➔r➔e➔t➔e➔r➔ ➔—➔ ➔b➔a➔s➔h➔,➔ ➔s➔h➔,➔ ➔z➔s➔h➔)➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔↑➔
➔ ➔ ➔ ➔A➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔s➔ ➔/➔ ➔U➔s➔e➔r➔ ➔P➔r➔o➔g➔r➔a➔m➔s➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔↑➔
➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔U➔s➔e➔r➔
➔C➔o➔m➔p➔o➔n➔e➔n➔t➔s➔ ➔e➔x➔p➔l➔a➔i➔n➔e➔d➔:➔
➔
➔
➔
➔
➔K➔e➔r➔n➔e➔l➔ ➔—➔ ➔t➔h➔e➔ ➔b➔r➔a➔i➔n➔ ➔o➔f➔ ➔L➔i➔n➔u➔x➔.➔ ➔M➔a➔n➔a➔g➔e➔s➔ ➔C➔P➔U➔,➔ ➔m➔e➔m➔o➔r➔y➔,➔ ➔I➔/➔O➔,➔ ➔p➔r➔o➔c➔e➔s➔s➔e➔s➔,➔ ➔n➔e➔t➔w➔o➔r➔k➔i➔n➔g➔.➔ ➔Y➔o➔u➔ ➔n➔e➔v➔e➔r➔ ➔i➔n➔t➔e➔r➔a➔c➔t➔ ➔w➔i➔t➔h➔ ➔i➔t➔
➔d➔i➔r➔e➔c➔t➔l➔y➔.➔
➔S➔h➔e➔l➔l➔ ➔—➔ ➔t➔h➔e➔ ➔i➔n➔t➔e➔r➔f➔a➔c➔e➔ ➔b➔e➔t➔w➔e➔e➔n➔ ➔y➔o➔u➔ ➔a➔n➔d➔ ➔t➔h➔e➔ ➔k➔e➔r➔n➔e➔l➔.➔ ➔Y➔o➔u➔ ➔t➔y➔p➔e➔ ➔c➔o➔m➔m➔a➔n➔d➔s➔ ➔→➔ ➔s➔h➔e➔l➔l➔ ➔i➔n➔t➔e➔r➔p➔r➔e➔t➔s➔ ➔→➔ ➔k➔e➔r➔n➔e➔l➔
➔e➔x➔e➔c➔u➔t➔e➔s➔.➔
➔S➔y➔s➔t➔e➔m➔ ➔L➔i➔b➔r➔a➔r➔i➔e➔s➔ ➔—➔ ➔p➔r➔e➔-➔w➔r➔i➔t➔t➔e➔n➔ ➔f➔u➔n➔c➔t➔i➔o➔n➔s➔ ➔t➔h➔a➔t➔ ➔p➔r➔o➔g➔r➔a➔m➔s➔ ➔u➔s➔e➔ ➔t➔o➔ ➔t➔a➔l➔k➔ ➔t➔o➔ ➔t➔h➔e➔ ➔k➔e➔r➔n➔e➔l➔.➔
➔U➔s➔e➔r➔ ➔S➔p➔a➔c➔e➔ ➔—➔ ➔w➔h➔e➔r➔e➔ ➔a➔l➔l➔ ➔a➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔s➔ ➔r➔u➔n➔ ➔(➔y➔o➔u➔r➔ ➔p➔r➔o➔g➔r➔a➔m➔s➔,➔ ➔s➔e➔r➔v➔i➔c➔e➔s➔,➔ ➔t➔o➔o➔l➔s➔)➔.➔
➔4➔.➔ ➔L➔i➔n➔u➔x➔ ➔S➔h➔e➔l➔l➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔ ➔S➔h➔e➔l➔l➔?➔
➔A➔ ➔s➔h➔e➔l➔l➔ ➔i➔s➔ ➔a➔ ➔c➔o➔m➔m➔a➔n➔d➔-➔l➔i➔n➔e➔ ➔i➔n➔t➔e➔r➔p➔r➔e➔t➔e➔r➔.➔ ➔Y➔o➔u➔ ➔t➔y➔p➔e➔ ➔c➔o➔m➔m➔a➔n➔d➔s➔,➔ ➔i➔t➔ ➔p➔a➔s➔s➔e➔s➔ ➔t➔h➔e➔m➔ ➔t➔o➔ ➔t➔h➔e➔ ➔k➔e➔r➔n➔e➔l➔ ➔f➔o➔r➔ ➔e➔x➔e➔c➔u➔t➔i➔o➔n➔.➔
➔T➔y➔p➔e➔s➔ ➔o➔f➔ ➔S➔h➔e➔l➔l➔s➔:➔
➔S➔h➔e➔l➔l➔ ➔D➔e➔s➔c➔r➔i➔p➔t➔i➔o➔n➔
➔b➔a➔s➔h➔ ➔B➔o➔u➔r➔n➔e➔ ➔A➔g➔a➔i➔n➔ ➔S➔h➔e➔l➔l➔ ➔—➔ ➔m➔o➔s➔t➔ ➔c➔o➔m➔m➔o➔n➔,➔ ➔d➔e➔f➔a➔u➔l➔t➔ ➔o➔n➔ ➔U➔b➔u➔n➔t➔u➔/➔R➔H➔E➔L➔
➔s➔h➔ ➔O➔r➔i➔g➔i➔n➔a➔l➔ ➔B➔o➔u➔r➔n➔e➔ ➔S➔h➔e➔l➔l➔
➔z➔s➔h➔ ➔E➔x➔t➔e➔n➔d➔e➔d➔ ➔b➔a➔s➔h➔ ➔w➔i➔t➔h➔ ➔b➔e➔t➔t➔e➔r➔ ➔f➔e➔a➔t➔u➔r➔e➔s➔,➔ ➔p➔o➔p➔u➔l➔a➔r➔ ➔o➔n➔ ➔M➔a➔c➔
➔f➔i➔s➔h➔ ➔U➔s➔e➔r➔-➔f➔r➔i➔e➔n➔d➔l➔y➔ ➔s➔h➔e➔l➔l➔ ➔w➔i➔t➔h➔ ➔a➔u➔t➔o➔c➔o➔m➔p➔l➔e➔t➔e➔
➔k➔s➔h➔ ➔K➔o➔r➔n➔ ➔S➔h➔e➔l➔l➔ ➔—➔ ➔u➔s➔e➔d➔ ➔i➔n➔ ➔s➔o➔m➔e➔ ➔e➔n➔t➔e➔r➔p➔r➔i➔s➔e➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔s➔
➔C➔h➔e➔c➔k➔ ➔y➔o➔u➔r➔ ➔s➔h➔e➔l➔l➔:➔
➔e➔c➔h➔o➔ ➔$➔S➔H➔E➔L➔L➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔s➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔s➔h➔e➔l➔l➔ ➔p➔a➔t➔h➔
➔e➔c➔h➔o➔ ➔$➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔s➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔s➔h➔e➔l➔l➔ ➔n➔a➔m➔e➔
➔c➔a➔t➔ ➔/➔e➔t➔c➔/➔s➔h➔e➔l➔l➔s➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔a➔l➔l➔ ➔i➔n➔s➔t➔a➔l➔l➔e➔d➔ ➔s➔h➔e➔l➔l➔s➔
➔c➔h➔s➔h➔ ➔-➔s➔ ➔/➔b➔i➔n➔/➔z➔s➔h➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔a➔n➔g➔e➔ ➔d➔e➔f➔a➔u➔l➔t➔ ➔s➔h➔e➔l➔l➔
➔S➔h➔e➔l➔l➔ ➔P➔r➔o➔m➔p➔t➔:➔
➔a➔k➔h➔i➔l➔@➔s➔e➔r➔v➔e➔r➔:➔~➔$➔
➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔ ➔│➔ ➔└➔─➔─➔ ➔$➔ ➔=➔ ➔n➔o➔r➔m➔a➔l➔ ➔u➔s➔e➔r➔,➔ ➔#➔ ➔=➔ ➔r➔o➔o➔t➔ ➔u➔s➔e➔r➔
➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔│➔ ➔ ➔ ➔ ➔└➔─➔─➔─➔─➔ ➔~➔ ➔=➔ ➔h➔o➔m➔e➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔ ➔h➔o➔s➔t➔n➔a➔m➔e➔
➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔ ➔u➔s➔e➔r➔n➔a➔m➔e➔
➔
➔
➔
➔
➔5➔.➔ ➔L➔i➔n➔u➔x➔ ➔F➔i➔l➔e➔ ➔S➔y➔s➔t➔e➔m➔ ➔S➔t➔r➔u➔c➔t➔u➔r➔e➔
➔E➔v➔e➔r➔y➔t➔h➔i➔n➔g➔ ➔i➔n➔ ➔L➔i➔n➔u➔x➔ ➔i➔s➔ ➔a➔ ➔f➔i➔l➔e➔.➔ ➔T➔h➔e➔ ➔f➔i➔l➔e➔s➔y➔s➔t➔e➔m➔ ➔s➔t➔a➔r➔t➔s➔ ➔f➔r➔o➔m➔ ➔r➔o➔o➔t➔ ➔/➔ ➔.➔
➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔←➔ ➔R➔o➔o➔t➔ ➔—➔ ➔t➔o➔p➔ ➔o➔f➔ ➔e➔n➔t➔i➔r➔e➔ ➔f➔i➔l➔e➔s➔y➔s➔t➔e➔m➔
➔├➔─➔─➔ ➔b➔i➔n➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔←➔ ➔E➔s➔s➔e➔n➔t➔i➔a➔l➔ ➔b➔i➔n➔a➔r➔i➔e➔s➔ ➔(➔l➔s➔,➔ ➔c➔p➔,➔ ➔m➔v➔,➔ ➔c➔a➔t➔)➔
➔├➔─➔─➔ ➔s➔b➔i➔n➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔←➔ ➔S➔y➔s➔t➔e➔m➔ ➔b➔i➔n➔a➔r➔i➔e➔s➔ ➔(➔o➔n➔l➔y➔ ➔r➔o➔o➔t➔ ➔u➔s➔e➔s➔:➔ ➔f➔d➔i➔s➔k➔,➔ ➔m➔o➔u➔n➔t➔)➔
➔├➔─➔─➔ ➔e➔t➔c➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔←➔ ➔C➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔ ➔f➔i➔l➔e➔s➔ ➔(➔n➔g➔i➔n➔x➔.➔c➔o➔n➔f➔,➔ ➔p➔a➔s➔s➔w➔d➔,➔ ➔h➔o➔s➔t➔s➔)➔
➔├➔─➔─➔ ➔h➔o➔m➔e➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔←➔ ➔U➔s➔e➔r➔ ➔h➔o➔m➔e➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔i➔e➔s➔ ➔(➔/➔h➔o➔m➔e➔/➔a➔k➔h➔i➔l➔)➔
➔├➔─➔─➔ ➔r➔o➔o➔t➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔←➔ ➔R➔o➔o➔t➔ ➔u➔s➔e➔r➔'➔s➔ ➔h➔o➔m➔e➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔├➔─➔─➔ ➔v➔a➔r➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔←➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔ ➔d➔a➔t➔a➔ ➔(➔l➔o➔g➔s➔,➔ ➔d➔a➔t➔a➔b➔a➔s➔e➔s➔,➔ ➔m➔a➔i➔l➔)➔
➔│➔ ➔ ➔ ➔└➔─➔─➔ ➔l➔o➔g➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔←➔ ➔S➔y➔s➔t➔e➔m➔ ➔a➔n➔d➔ ➔a➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔ ➔l➔o➔g➔s➔
➔├➔─➔─➔ ➔t➔m➔p➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔←➔ ➔T➔e➔m➔p➔o➔r➔a➔r➔y➔ ➔f➔i➔l➔e➔s➔ ➔(➔c➔l➔e➔a➔r➔e➔d➔ ➔o➔n➔ ➔r➔e➔b➔o➔o➔t➔)➔
➔├➔─➔─➔ ➔u➔s➔r➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔←➔ ➔U➔s➔e➔r➔ ➔p➔r➔o➔g➔r➔a➔m➔s➔ ➔a➔n➔d➔ ➔u➔t➔i➔l➔i➔t➔i➔e➔s➔
➔│➔ ➔ ➔ ➔├➔─➔─➔ ➔b➔i➔n➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔←➔ ➔M➔o➔s➔t➔ ➔u➔s➔e➔r➔ ➔c➔o➔m➔m➔a➔n➔d➔s➔
➔│➔ ➔ ➔ ➔└➔─➔─➔ ➔l➔o➔c➔a➔l➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔←➔ ➔L➔o➔c➔a➔l➔l➔y➔ ➔i➔n➔s➔t➔a➔l➔l➔e➔d➔ ➔s➔o➔f➔t➔w➔a➔r➔e➔
➔├➔─➔─➔ ➔o➔p➔t➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔←➔ ➔O➔p➔t➔i➔o➔n➔a➔l➔/➔t➔h➔i➔r➔d➔-➔p➔a➔r➔t➔y➔ ➔s➔o➔f➔t➔w➔a➔r➔e➔
➔├➔─➔─➔ ➔d➔e➔v➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔←➔ ➔D➔e➔v➔i➔c➔e➔ ➔f➔i➔l➔e➔s➔ ➔(➔d➔i➔s➔k➔s➔,➔ ➔t➔e➔r➔m➔i➔n➔a➔l➔s➔)➔
➔├➔─➔─➔ ➔p➔r➔o➔c➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔←➔ ➔V➔i➔r➔t➔u➔a➔l➔ ➔f➔i➔l➔e➔s➔y➔s➔t➔e➔m➔ ➔—➔ ➔r➔u➔n➔n➔i➔n➔g➔ ➔p➔r➔o➔c➔e➔s➔s➔e➔s➔ ➔i➔n➔f➔o➔
➔├➔─➔─➔ ➔s➔y➔s➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔←➔ ➔V➔i➔r➔t➔u➔a➔l➔ ➔f➔i➔l➔e➔s➔y➔s➔t➔e➔m➔ ➔—➔ ➔k➔e➔r➔n➔e➔l➔/➔h➔a➔r➔d➔w➔a➔r➔e➔ ➔i➔n➔f➔o➔
➔├➔─➔─➔ ➔m➔n➔t➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔←➔ ➔T➔e➔m➔p➔o➔r➔a➔r➔y➔ ➔m➔o➔u➔n➔t➔ ➔p➔o➔i➔n➔t➔s➔
➔├➔─➔─➔ ➔m➔e➔d➔i➔a➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔←➔ ➔R➔e➔m➔o➔v➔a➔b➔l➔e➔ ➔m➔e➔d➔i➔a➔ ➔(➔U➔S➔B➔,➔ ➔C➔D➔)➔
➔├➔─➔─➔ ➔b➔o➔o➔t➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔←➔ ➔B➔o➔o➔t➔ ➔l➔o➔a➔d➔e➔r➔ ➔f➔i➔l➔e➔s➔ ➔(➔k➔e➔r➔n➔e➔l➔,➔ ➔g➔r➔u➔b➔)➔
➔└➔─➔─➔ ➔l➔i➔b➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔←➔ ➔S➔h➔a➔r➔e➔d➔ ➔l➔i➔b➔r➔a➔r➔i➔e➔s➔
➔K➔e➔y➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔i➔e➔s➔ ➔t➔o➔ ➔r➔e➔m➔e➔m➔b➔e➔r➔:➔
➔/➔e➔t➔c➔ ➔ ➔—➔ ➔A➔L➔L➔ ➔c➔o➔n➔f➔i➔g➔ ➔f➔i➔l➔e➔s➔ ➔l➔i➔v➔e➔ ➔h➔e➔r➔e➔
➔/➔v➔a➔r➔/➔l➔o➔g➔ ➔ ➔—➔ ➔A➔L➔L➔ ➔l➔o➔g➔s➔ ➔l➔i➔v➔e➔ ➔h➔e➔r➔e➔
➔/➔h➔o➔m➔e➔ ➔ ➔—➔ ➔u➔s➔e➔r➔ ➔f➔i➔l➔e➔s➔
➔/➔t➔m➔p➔ ➔ ➔—➔ ➔t➔e➔m➔p➔o➔r➔a➔r➔y➔,➔ ➔c➔l➔e➔a➔r➔e➔d➔ ➔o➔n➔ ➔r➔e➔b➔o➔o➔t➔
➔/➔p➔r➔o➔c➔ ➔ ➔—➔ ➔r➔e➔a➔l➔-➔t➔i➔m➔e➔ ➔s➔y➔s➔t➔e➔m➔ ➔i➔n➔f➔o➔ ➔(➔n➔o➔t➔ ➔r➔e➔a➔l➔ ➔f➔i➔l➔e➔s➔)➔
➔6➔.➔ ➔T➔y➔p➔e➔s➔ ➔o➔f➔ ➔F➔i➔l➔e➔ ➔S➔y➔s➔t➔e➔m➔s➔
➔F➔i➔l➔e➔ ➔S➔y➔s➔t➔e➔m➔ ➔D➔e➔s➔c➔r➔i➔p➔t➔i➔o➔n➔ ➔U➔s➔e➔d➔ ➔O➔n➔
➔e➔x➔t➔4➔ ➔M➔o➔s➔t➔ ➔c➔o➔m➔m➔o➔n➔ ➔L➔i➔n➔u➔x➔ ➔f➔i➔l➔e➔s➔y➔s➔t➔e➔m➔,➔ ➔j➔o➔u➔r➔n➔a➔l➔i➔n➔g➔ ➔U➔b➔u➔n➔t➔u➔,➔ ➔D➔e➔b➔i➔a➔n➔ ➔E➔C➔2➔
➔
➔
➔
➔
➔x➔f➔s➔ ➔H➔i➔g➔h➔ ➔p➔e➔r➔f➔o➔r➔m➔a➔n➔c➔e➔,➔ ➔l➔a➔r➔g➔e➔ ➔f➔i➔l➔e➔s➔ ➔R➔H➔E➔L➔,➔ ➔A➔m➔a➔z➔o➔n➔ ➔L➔i➔n➔u➔x➔ ➔E➔C➔2➔
➔b➔t➔r➔f➔s➔ ➔M➔o➔d➔e➔r➔n➔,➔ ➔s➔n➔a➔p➔s➔h➔o➔t➔s➔,➔ ➔R➔A➔I➔D➔ ➔s➔u➔p➔p➔o➔r➔t➔ ➔A➔d➔v➔a➔n➔c➔e➔d➔ ➔L➔i➔n➔u➔x➔
➔N➔T➔F➔S➔ ➔W➔i➔n➔d➔o➔w➔s➔ ➔f➔i➔l➔e➔s➔y➔s➔t➔e➔m➔ ➔W➔i➔n➔d➔o➔w➔s➔ ➔(➔r➔e➔a➔d➔a➔b➔l➔e➔ ➔o➔n➔ ➔L➔i➔n➔u➔x➔)➔
➔F➔A➔T➔3➔2➔ ➔U➔n➔i➔v➔e➔r➔s➔a➔l➔,➔ ➔U➔S➔B➔ ➔d➔r➔i➔v➔e➔s➔ ➔U➔S➔B➔ ➔d➔r➔i➔v➔e➔s➔
➔t➔m➔p➔f➔s➔ ➔I➔n➔-➔m➔e➔m➔o➔r➔y➔ ➔f➔i➔l➔e➔s➔y➔s➔t➔e➔m➔ ➔/➔t➔m➔p➔ ➔o➔n➔ ➔m➔o➔d➔e➔r➔n➔ ➔L➔i➔n➔u➔x➔
➔N➔F➔S➔ ➔N➔e➔t➔w➔o➔r➔k➔ ➔F➔i➔l➔e➔ ➔S➔y➔s➔t➔e➔m➔ ➔—➔ ➔s➔h➔a➔r➔e➔ ➔f➔i➔l➔e➔s➔ ➔o➔v➔e➔r➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔S➔h➔a➔r➔e➔d➔ ➔s➔t➔o➔r➔a➔g➔e➔
➔E➔F➔S➔ ➔A➔W➔S➔ ➔E➔l➔a➔s➔t➔i➔c➔ ➔F➔i➔l➔e➔ ➔S➔y➔s➔t➔e➔m➔ ➔(➔N➔F➔S➔-➔b➔a➔s➔e➔d➔)➔ ➔A➔W➔S➔ ➔s➔h➔a➔r➔e➔d➔ ➔s➔t➔o➔r➔a➔g➔e➔
➔7➔.➔ ➔A➔b➔s➔o➔l➔u➔t➔e➔ ➔P➔a➔t➔h➔ ➔v➔s➔ ➔R➔e➔l➔a➔t➔i➔v➔e➔ ➔P➔a➔t➔h➔
➔A➔b➔s➔o➔l➔u➔t➔e➔ ➔P➔a➔t➔h➔:➔
➔A➔l➔w➔a➔y➔s➔ ➔s➔t➔a➔r➔t➔s➔ ➔f➔r➔o➔m➔ ➔r➔o➔o➔t➔ ➔/➔
➔F➔u➔l➔l➔ ➔p➔a➔t➔h➔ ➔r➔e➔g➔a➔r➔d➔l➔e➔s➔s➔ ➔o➔f➔ ➔w➔h➔e➔r➔e➔ ➔y➔o➔u➔ ➔a➔r➔e➔
➔E➔x➔a➔m➔p➔l➔e➔:➔ ➔/➔h➔o➔m➔e➔/➔a➔k➔h➔i➔l➔/➔p➔r➔o➔j➔e➔c➔t➔s➔/➔a➔p➔p➔.➔j➔s➔
➔R➔e➔l➔a➔t➔i➔v➔e➔ ➔P➔a➔t➔h➔:➔
➔S➔t➔a➔r➔t➔s➔ ➔f➔r➔o➔m➔ ➔y➔o➔u➔r➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔l➔o➔c➔a➔t➔i➔o➔n➔
➔U➔s➔e➔s➔ ➔.➔ ➔ ➔(➔c➔u➔r➔r➔e➔n➔t➔ ➔d➔i➔r➔)➔ ➔a➔n➔d➔ ➔.➔.➔ ➔ ➔(➔p➔a➔r➔e➔n➔t➔ ➔d➔i➔r➔)➔
➔E➔x➔a➔m➔p➔l➔e➔:➔ ➔.➔/➔p➔r➔o➔j➔e➔c➔t➔s➔/➔a➔p➔p➔.➔j➔s➔ ➔ ➔o➔r➔ ➔.➔.➔/➔e➔t➔c➔/➔n➔g➔i➔n➔x➔.➔c➔o➔n➔f➔
➔#➔ ➔Y➔o➔u➔ ➔a➔r➔e➔ ➔i➔n➔ ➔/➔h➔o➔m➔e➔/➔a➔k➔h➔i➔l➔/➔
➔c➔d➔ ➔/➔e➔t➔c➔/➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔b➔s➔o➔l➔u➔t➔e➔ ➔—➔ ➔g➔o➔e➔s➔ ➔f➔r➔o➔m➔ ➔r➔o➔o➔t➔
➔c➔d➔ ➔.➔.➔/➔e➔t➔c➔/➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔l➔a➔t➔i➔v➔e➔ ➔—➔ ➔g➔o➔e➔s➔ ➔u➔p➔ ➔o➔n➔e➔ ➔l➔e➔v➔e➔l➔ ➔t➔h➔e➔n➔ ➔t➔o➔ ➔e➔t➔c➔/➔n➔g➔i➔n➔x➔
➔c➔d➔ ➔.➔/➔p➔r➔o➔j➔e➔c➔t➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔l➔a➔t➔i➔v➔e➔ ➔—➔ ➔g➔o➔e➔s➔ ➔i➔n➔t➔o➔ ➔p➔r➔o➔j➔e➔c➔t➔s➔ ➔i➔n➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔d➔i➔r➔
➔#➔ ➔S➔p➔e➔c➔i➔a➔l➔ ➔s➔y➔m➔b➔o➔l➔s➔
➔.➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔.➔.➔ ➔ ➔ ➔ ➔#➔ ➔p➔a➔r➔e➔n➔t➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔~➔ ➔ ➔ ➔ ➔ ➔#➔ ➔h➔o➔m➔e➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔o➔f➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔u➔s➔e➔r➔
➔-➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔r➔e➔v➔i➔o➔u➔s➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔/➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔o➔o➔t➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔#➔ ➔E➔x➔a➔m➔p➔l➔e➔s➔
➔c➔d➔ ➔~➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔g➔o➔ ➔t➔o➔ ➔h➔o➔m➔e➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔
➔
➔
➔
➔c➔d➔ ➔-➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔g➔o➔ ➔t➔o➔ ➔p➔r➔e➔v➔i➔o➔u➔s➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔c➔d➔ ➔.➔.➔/➔.➔.➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔g➔o➔ ➔u➔p➔ ➔t➔w➔o➔ ➔l➔e➔v➔e➔l➔s➔
➔8➔.➔ ➔F➔i➔l➔e➔ ➔S➔y➔s➔t➔e➔m➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔
➔N➔a➔v➔i➔g➔a➔t➔i➔o➔n➔
➔p➔w➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔r➔i➔n➔t➔ ➔w➔o➔r➔k➔i➔n➔g➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔(➔w➔h➔e➔r➔e➔ ➔a➔m➔ ➔I➔?➔)➔
➔l➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔f➔i➔l➔e➔s➔
➔l➔s➔ ➔-➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔o➔n➔g➔ ➔f➔o➔r➔m➔a➔t➔ ➔(➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔,➔ ➔o➔w➔n➔e➔r➔,➔ ➔s➔i➔z➔e➔,➔ ➔d➔a➔t➔e➔)➔
➔l➔s➔ ➔-➔a➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔h➔i➔d➔d➔e➔n➔ ➔f➔i➔l➔e➔s➔ ➔(➔s➔t➔a➔r➔t➔i➔n➔g➔ ➔w➔i➔t➔h➔ ➔.➔)➔
➔l➔s➔ ➔-➔l➔a➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔o➔n➔g➔ ➔f➔o➔r➔m➔a➔t➔ ➔+➔ ➔h➔i➔d➔d➔e➔n➔ ➔f➔i➔l➔e➔s➔
➔l➔s➔ ➔-➔l➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔h➔u➔m➔a➔n➔ ➔r➔e➔a➔d➔a➔b➔l➔e➔ ➔f➔i➔l➔e➔ ➔s➔i➔z➔e➔s➔
➔l➔s➔ ➔-➔l➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔o➔r➔t➔ ➔b➔y➔ ➔m➔o➔d➔i➔f➔i➔c➔a➔t➔i➔o➔n➔ ➔t➔i➔m➔e➔
➔l➔s➔ ➔-➔R➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔r➔e➔c➔u➔r➔s➔i➔v➔e➔l➔y➔
➔C➔r➔e➔a➔t➔e➔ ➔F➔i➔l➔e➔s➔ ➔a➔n➔d➔ ➔D➔i➔r➔e➔c➔t➔o➔r➔i➔e➔s➔
➔t➔o➔u➔c➔h➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔e➔m➔p➔t➔y➔ ➔f➔i➔l➔e➔ ➔o➔r➔ ➔u➔p➔d➔a➔t➔e➔ ➔t➔i➔m➔e➔s➔t➔a➔m➔p➔
➔t➔o➔u➔c➔h➔ ➔f➔i➔l➔e➔1➔ ➔f➔i➔l➔e➔2➔ ➔f➔i➔l➔e➔3➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔f➔i➔l➔e➔s➔
➔m➔k➔d➔i➔r➔ ➔d➔i➔r➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔m➔k➔d➔i➔r➔ ➔-➔p➔ ➔a➔/➔b➔/➔c➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔n➔e➔s➔t➔e➔d➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔i➔e➔s➔ ➔(➔p➔a➔r➔e➔n➔t➔s➔)➔
➔m➔k➔d➔i➔r➔ ➔-➔p➔ ➔p➔r➔o➔j➔e➔c➔t➔/➔{➔s➔r➔c➔,➔t➔e➔s➔t➔s➔,➔d➔o➔c➔s➔}➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔s➔u➔b➔d➔i➔r➔s➔ ➔a➔t➔ ➔o➔n➔c➔e➔
➔C➔o➔p➔y➔ ➔—➔ ➔c➔p➔
➔c➔p➔ ➔f➔i➔l➔e➔1➔ ➔f➔i➔l➔e➔2➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔p➔y➔ ➔f➔i➔l➔e➔1➔ ➔t➔o➔ ➔f➔i➔l➔e➔2➔
➔c➔p➔ ➔f➔i➔l➔e➔1➔ ➔/➔p➔a➔t➔h➔/➔t➔o➔/➔d➔i➔r➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔p➔y➔ ➔f➔i➔l➔e➔ ➔t➔o➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔c➔p➔ ➔-➔r➔ ➔d➔i➔r➔1➔ ➔d➔i➔r➔2➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔p➔y➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔r➔e➔c➔u➔r➔s➔i➔v➔e➔l➔y➔
➔c➔p➔ ➔-➔p➔ ➔f➔i➔l➔e➔1➔ ➔f➔i➔l➔e➔2➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔p➔y➔ ➔a➔n➔d➔ ➔p➔r➔e➔s➔e➔r➔v➔e➔ ➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔/➔t➔i➔m➔e➔s➔t➔a➔m➔p➔s➔
➔c➔p➔ ➔-➔i➔ ➔f➔i➔l➔e➔1➔ ➔f➔i➔l➔e➔2➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔i➔n➔t➔e➔r➔a➔c➔t➔i➔v➔e➔ ➔—➔ ➔a➔s➔k➔ ➔b➔e➔f➔o➔r➔e➔ ➔o➔v➔e➔r➔w➔r➔i➔t➔e➔
➔c➔p➔ ➔-➔v➔ ➔f➔i➔l➔e➔1➔ ➔f➔i➔l➔e➔2➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔v➔e➔r➔b➔o➔s➔e➔ ➔—➔ ➔s➔h➔o➔w➔ ➔w➔h➔a➔t➔'➔s➔ ➔b➔e➔i➔n➔g➔ ➔c➔o➔p➔i➔e➔d➔
➔c➔p➔ ➔*➔.➔t➔x➔t➔ ➔/➔b➔a➔c➔k➔u➔p➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔p➔y➔ ➔a➔l➔l➔ ➔t➔x➔t➔ ➔f➔i➔l➔e➔s➔ ➔t➔o➔ ➔b➔a➔c➔k➔u➔p➔
➔M➔o➔v➔e➔ ➔/➔ ➔R➔e➔n➔a➔m➔e➔ ➔—➔ ➔m➔v➔
➔
➔
➔
➔
➔m➔v➔ ➔f➔i➔l➔e➔1➔ ➔f➔i➔l➔e➔2➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔n➔a➔m➔e➔ ➔f➔i➔l➔e➔1➔ ➔t➔o➔ ➔f➔i➔l➔e➔2➔
➔m➔v➔ ➔f➔i➔l➔e➔1➔ ➔/➔p➔a➔t➔h➔/➔t➔o➔/➔d➔i➔r➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔m➔o➔v➔e➔ ➔f➔i➔l➔e➔ ➔t➔o➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔m➔v➔ ➔d➔i➔r➔1➔ ➔d➔i➔r➔2➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔n➔a➔m➔e➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔m➔v➔ ➔-➔i➔ ➔f➔i➔l➔e➔1➔ ➔f➔i➔l➔e➔2➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔s➔k➔ ➔b➔e➔f➔o➔r➔e➔ ➔o➔v➔e➔r➔w➔r➔i➔t➔e➔
➔m➔v➔ ➔-➔v➔ ➔f➔i➔l➔e➔1➔ ➔f➔i➔l➔e➔2➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔v➔e➔r➔b➔o➔s➔e➔
➔m➔v➔ ➔*➔.➔l➔o➔g➔ ➔/➔v➔a➔r➔/➔l➔o➔g➔/➔a➔r➔c➔h➔i➔v➔e➔/➔ ➔ ➔ ➔#➔ ➔m➔o➔v➔e➔ ➔a➔l➔l➔ ➔l➔o➔g➔ ➔f➔i➔l➔e➔s➔
➔D➔e➔l➔e➔t➔e➔ ➔—➔ ➔r➔m➔
➔r➔m➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔f➔i➔l➔e➔
➔r➔m➔ ➔-➔i➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔s➔k➔ ➔b➔e➔f➔o➔r➔e➔ ➔d➔e➔l➔e➔t➔e➔
➔r➔m➔ ➔-➔f➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔r➔c➔e➔ ➔d➔e➔l➔e➔t➔e➔,➔ ➔n➔o➔ ➔p➔r➔o➔m➔p➔t➔
➔r➔m➔ ➔-➔r➔ ➔d➔i➔r➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔r➔e➔c➔u➔r➔s➔i➔v➔e➔l➔y➔
➔r➔m➔ ➔-➔r➔f➔ ➔d➔i➔r➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔r➔c➔e➔ ➔d➔e➔l➔e➔t➔e➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔(➔D➔A➔N➔G➔E➔R➔O➔U➔S➔ ➔—➔ ➔n➔o➔ ➔u➔n➔d➔o➔)➔
➔r➔m➔ ➔*➔.➔t➔m➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔a➔l➔l➔ ➔.➔t➔m➔p➔ ➔f➔i➔l➔e➔s➔
➔V➔i➔e➔w➔ ➔F➔i➔l➔e➔ ➔C➔o➔n➔t➔e➔n➔t➔
➔c➔a➔t➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔r➔i➔n➔t➔ ➔e➔n➔t➔i➔r➔e➔ ➔f➔i➔l➔e➔
➔c➔a➔t➔ ➔-➔n➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔w➔i➔t➔h➔ ➔l➔i➔n➔e➔ ➔n➔u➔m➔b➔e➔r➔s➔
➔l➔e➔s➔s➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔c➔r➔o➔l➔l➔ ➔t➔h➔r➔o➔u➔g➔h➔ ➔f➔i➔l➔e➔ ➔(➔q➔ ➔t➔o➔ ➔q➔u➔i➔t➔)➔
➔m➔o➔r➔e➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔a➔g➔e➔ ➔t➔h➔r➔o➔u➔g➔h➔ ➔f➔i➔l➔e➔
➔h➔e➔a➔d➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔r➔s➔t➔ ➔1➔0➔ ➔l➔i➔n➔e➔s➔
➔h➔e➔a➔d➔ ➔-➔n➔ ➔2➔0➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔r➔s➔t➔ ➔2➔0➔ ➔l➔i➔n➔e➔s➔
➔t➔a➔i➔l➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔a➔s➔t➔ ➔1➔0➔ ➔l➔i➔n➔e➔s➔
➔t➔a➔i➔l➔ ➔-➔n➔ ➔2➔0➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔a➔s➔t➔ ➔2➔0➔ ➔l➔i➔n➔e➔s➔
➔t➔a➔i➔l➔ ➔-➔f➔ ➔/➔v➔a➔r➔/➔l➔o➔g➔/➔s➔y➔s➔l➔o➔g➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔l➔l➔o➔w➔ ➔l➔o➔g➔ ➔i➔n➔ ➔r➔e➔a➔l➔ ➔t➔i➔m➔e➔ ➔(➔V➔E➔R➔Y➔ ➔u➔s➔e➔f➔u➔l➔ ➔f➔o➔r➔ ➔D➔e➔v➔O➔p➔s➔)➔
➔F➔i➔l➔e➔ ➔I➔n➔f➔o➔r➔m➔a➔t➔i➔o➔n➔
➔f➔i➔l➔e➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔w➔h➔a➔t➔ ➔t➔y➔p➔e➔ ➔o➔f➔ ➔f➔i➔l➔e➔ ➔i➔s➔ ➔i➔t➔?➔
➔s➔t➔a➔t➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔t➔a➔i➔l➔e➔d➔ ➔f➔i➔l➔e➔ ➔i➔n➔f➔o➔ ➔(➔s➔i➔z➔e➔,➔ ➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔,➔ ➔t➔i➔m➔e➔s➔t➔a➔m➔p➔s➔)➔
➔w➔c➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔u➔n➔t➔ ➔l➔i➔n➔e➔s➔,➔ ➔w➔o➔r➔d➔s➔,➔ ➔c➔h➔a➔r➔a➔c➔t➔e➔r➔s➔
➔w➔c➔ ➔-➔l➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔u➔n➔t➔ ➔l➔i➔n➔e➔s➔ ➔o➔n➔l➔y➔
➔d➔u➔ ➔-➔s➔h➔ ➔d➔i➔r➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔i➔s➔k➔ ➔u➔s➔a➔g➔e➔ ➔o➔f➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔(➔h➔u➔m➔a➔n➔ ➔r➔e➔a➔d➔a➔b➔l➔e➔)➔
➔d➔u➔ ➔-➔s➔h➔ ➔*➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔i➔s➔k➔ ➔u➔s➔a➔g➔e➔ ➔o➔f➔ ➔a➔l➔l➔ ➔i➔t➔e➔m➔s➔ ➔i➔n➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔d➔i➔r➔
➔d➔f➔ ➔-➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔i➔s➔k➔ ➔s➔p➔a➔c➔e➔ ➔o➔f➔ ➔a➔l➔l➔ ➔m➔o➔u➔n➔t➔e➔d➔ ➔f➔i➔l➔e➔s➔y➔s➔t➔e➔m➔s➔
➔L➔i➔n➔k➔s➔
➔
➔
➔
➔
➔➔ ➔➔
➔l➔n➔ ➔f➔i➔l➔e➔1➔ ➔h➔a➔r➔d➔l➔i➔n➔k➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔h➔a➔r➔d➔ ➔l➔i➔n➔k➔ ➔(➔s➔a➔m➔e➔ ➔i➔n➔o➔d➔e➔)➔
➔l➔n➔ ➔-➔s➔ ➔f➔i➔l➔e➔1➔ ➔s➔y➔m➔l➔i➔n➔k➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔s➔y➔m➔b➔o➔l➔i➔c➔ ➔(➔s➔o➔f➔t➔)➔ ➔l➔i➔n➔k➔ ➔(➔l➔i➔k➔e➔ ➔a➔ ➔s➔h➔o➔r➔t➔c➔u➔t➔)➔
➔l➔s➔ ➔-➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔y➔m➔l➔i➔n➔k➔s➔ ➔s➔h➔o➔w➔n➔ ➔w➔i➔t➔h➔ ➔-➔>➔
➔r➔e➔a➔d➔l➔i➔n➔k➔ ➔s➔y➔m➔l➔i➔n➔k➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔w➔h➔e➔r➔e➔ ➔s➔y➔m➔l➔i➔n➔k➔ ➔p➔o➔i➔n➔t➔s➔
➔9➔.➔ ➔H➔o➔w➔ ➔t➔o➔ ➔A➔d➔d➔ ➔a➔ ➔V➔o➔l➔u➔m➔e➔ ➔t➔o➔ ➔a➔n➔ ➔E➔C➔2➔ ➔I➔n➔s➔t➔a➔n➔c➔e➔
➔T➔h➔i➔s➔ ➔i➔s➔ ➔a➔ ➔c➔o➔m➔m➔o➔n➔ ➔D➔e➔v➔O➔p➔s➔ ➔t➔a➔s➔k➔ ➔—➔ ➔a➔d➔d➔i➔n➔g➔ ➔e➔x➔t➔r➔a➔ ➔s➔t➔o➔r➔a➔g➔e➔ ➔t➔o➔ ➔y➔o➔u➔r➔ ➔E➔C➔2➔ ➔i➔n➔s➔t➔a➔n➔c➔e➔.➔
➔S➔t➔e➔p➔ ➔1➔ ➔—➔ ➔C➔r➔e➔a➔t➔e➔ ➔a➔n➔d➔ ➔A➔t➔t➔a➔c➔h➔ ➔E➔B➔S➔ ➔V➔o➔l➔u➔m➔e➔ ➔(➔A➔W➔S➔ ➔C➔o➔n➔s➔o➔l➔e➔ ➔o➔r➔ ➔C➔L➔I➔)➔
➔#➔ ➔U➔s➔i➔n➔g➔ ➔A➔W➔S➔ ➔C➔L➔I➔:➔
➔a➔w➔s➔ ➔e➔c➔2➔ ➔c➔r➔e➔a➔t➔e➔-➔v➔o➔l➔u➔m➔e➔ ➔-➔-➔s➔i➔z➔e➔ ➔2➔0➔ ➔-➔-➔a➔v➔a➔i➔l➔a➔b➔i➔l➔i➔t➔y➔-➔z➔o➔n➔e➔ ➔u➔s➔-➔e➔a➔s➔t➔-➔1➔a➔ ➔-➔-➔v➔o➔l➔u➔m➔e➔-➔t➔y➔p➔e➔ ➔g➔p➔3➔
➔a➔w➔s➔ ➔e➔c➔2➔ ➔a➔t➔t➔a➔c➔h➔-➔v➔o➔l➔u➔m➔e➔ ➔-➔-➔v➔o➔l➔u➔m➔e➔-➔i➔d➔ ➔v➔o➔l➔-➔x➔x➔x➔x➔x➔x➔x➔x➔ ➔-➔-➔i➔n➔s➔t➔a➔n➔c➔e➔-➔i➔d➔ ➔i➔-➔x➔x➔x➔x➔x➔x➔x➔x➔ ➔-➔-➔d➔e➔v➔i➔c➔e➔ ➔/➔d➔e➔v➔/➔
➔S➔t➔e➔p➔ ➔2➔ ➔—➔ ➔S➔S➔H➔ ➔i➔n➔t➔o➔ ➔y➔o➔u➔r➔ ➔E➔C➔2➔ ➔i➔n➔s➔t➔a➔n➔c➔e➔ ➔a➔n➔d➔ ➔v➔e➔r➔i➔f➔y➔ ➔d➔i➔s➔k➔ ➔i➔s➔ ➔a➔t➔t➔a➔c➔h➔e➔d➔
➔l➔s➔b➔l➔k➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔a➔l➔l➔ ➔b➔l➔o➔c➔k➔ ➔d➔e➔v➔i➔c➔e➔s➔ ➔—➔ ➔y➔o➔u➔ ➔s➔h➔o➔u➔l➔d➔ ➔s➔e➔e➔ ➔x➔v➔d➔f➔
➔f➔d➔i➔s➔k➔ ➔-➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔t➔a➔i➔l➔e➔d➔ ➔d➔i➔s➔k➔ ➔i➔n➔f➔o➔
➔S➔t➔e➔p➔ ➔3➔ ➔—➔ ➔F➔o➔r➔m➔a➔t➔ ➔t➔h➔e➔ ➔V➔o➔l➔u➔m➔e➔ ➔w➔i➔t➔h➔ ➔a➔ ➔F➔i➔l➔e➔ ➔S➔y➔s➔t➔e➔m➔
➔m➔k➔f➔s➔.➔e➔x➔t➔4➔ ➔/➔d➔e➔v➔/➔x➔v➔d➔f➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔r➔m➔a➔t➔ ➔w➔i➔t➔h➔ ➔e➔x➔t➔4➔
➔#➔ ➔O➔R➔
➔m➔k➔f➔s➔.➔x➔f➔s➔ ➔/➔d➔e➔v➔/➔x➔v➔d➔f➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔r➔m➔a➔t➔ ➔w➔i➔t➔h➔ ➔x➔f➔s➔ ➔(➔f➔o➔r➔ ➔R➔H➔E➔L➔/➔A➔m➔a➔z➔o➔n➔ ➔L➔i➔n➔u➔x➔)➔
➔S➔t➔e➔p➔ ➔4➔ ➔—➔ ➔C➔r➔e➔a➔t➔e➔ ➔a➔ ➔M➔o➔u➔n➔t➔ ➔P➔o➔i➔n➔t➔ ➔a➔n➔d➔ ➔M➔o➔u➔n➔t➔
➔m➔k➔d➔i➔r➔ ➔/➔d➔a➔t➔a➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔t➔o➔ ➔m➔o➔u➔n➔t➔ ➔t➔o➔
➔m➔o➔u➔n➔t➔ ➔/➔d➔e➔v➔/➔x➔v➔d➔f➔ ➔/➔d➔a➔t➔a➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔m➔o➔u➔n➔t➔ ➔v➔o➔l➔u➔m➔e➔ ➔t➔o➔ ➔/➔d➔a➔t➔a➔
➔d➔f➔ ➔-➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔v➔e➔r➔i➔f➔y➔ ➔i➔t➔'➔s➔ ➔m➔o➔u➔n➔t➔e➔d➔
➔S➔t➔e➔p➔ ➔5➔ ➔—➔ ➔M➔a➔k➔e➔ ➔i➔t➔ ➔P➔e➔r➔s➔i➔s➔t➔e➔n➔t➔ ➔(➔s➔u➔r➔v➔i➔v➔e➔ ➔r➔e➔b➔o➔o➔t➔s➔)➔
➔
➔
➔
➔
➔#➔ ➔G➔e➔t➔ ➔U➔U➔I➔D➔ ➔o➔f➔ ➔t➔h➔e➔ ➔v➔o➔l➔u➔m➔e➔
➔b➔l➔k➔i➔d➔ ➔/➔d➔e➔v➔/➔x➔v➔d➔f➔
➔#➔ ➔O➔u➔t➔p➔u➔t➔:➔ ➔/➔d➔e➔v➔/➔x➔v➔d➔f➔:➔ ➔U➔U➔I➔D➔=➔"➔a➔b➔c➔1➔2➔3➔.➔.➔.➔"➔ ➔T➔Y➔P➔E➔=➔"➔e➔x➔t➔4➔"➔
➔#➔ ➔A➔d➔d➔ ➔t➔o➔ ➔/➔e➔t➔c➔/➔f➔s➔t➔a➔b➔ ➔f➔o➔r➔ ➔a➔u➔t➔o➔-➔m➔o➔u➔n➔t➔ ➔o➔n➔ ➔r➔e➔b➔o➔o➔t➔
➔e➔c➔h➔o➔ ➔"➔U➔U➔I➔D➔=➔a➔b➔c➔1➔2➔3➔.➔.➔.➔ ➔ ➔/➔d➔a➔t➔a➔ ➔ ➔e➔x➔t➔4➔ ➔ ➔d➔e➔f➔a➔u➔l➔t➔s➔,➔n➔o➔f➔s➔ ➔ ➔0➔ ➔ ➔2➔"➔ ➔>➔>➔ ➔/➔e➔t➔c➔/➔f➔s➔t➔a➔b➔
➔#➔ ➔T➔e➔s➔t➔ ➔f➔s➔t➔a➔b➔ ➔e➔n➔t➔r➔y➔
➔m➔o➔u➔n➔t➔ ➔-➔a➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔m➔o➔u➔n➔t➔ ➔a➔l➔l➔ ➔e➔n➔t➔r➔i➔e➔s➔ ➔i➔n➔ ➔f➔s➔t➔a➔b➔
➔d➔f➔ ➔-➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔v➔e➔r➔i➔f➔y➔
➔U➔n➔m➔o➔u➔n➔t➔
➔u➔m➔o➔u➔n➔t➔ ➔/➔d➔a➔t➔a➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔u➔n➔m➔o➔u➔n➔t➔ ➔v➔o➔l➔u➔m➔e➔
➔u➔m➔o➔u➔n➔t➔ ➔-➔l➔ ➔/➔d➔a➔t➔a➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔a➔z➔y➔ ➔u➔n➔m➔o➔u➔n➔t➔ ➔(➔i➔f➔ ➔b➔u➔s➔y➔)➔
➔1➔0➔.➔ ➔S➔y➔s➔t➔e➔m➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔
➔S➔y➔s➔t➔e➔m➔ ➔I➔n➔f➔o➔r➔m➔a➔t➔i➔o➔n➔
➔u➔n➔a➔m➔e➔ ➔-➔a➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔l➔l➔ ➔s➔y➔s➔t➔e➔m➔ ➔i➔n➔f➔o➔ ➔(➔k➔e➔r➔n➔e➔l➔,➔ ➔h➔o➔s➔t➔n➔a➔m➔e➔,➔ ➔a➔r➔c➔h➔)➔
➔u➔n➔a➔m➔e➔ ➔-➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔k➔e➔r➔n➔e➔l➔ ➔v➔e➔r➔s➔i➔o➔n➔ ➔o➔n➔l➔y➔
➔h➔o➔s➔t➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔h➔o➔s➔t➔n➔a➔m➔e➔
➔h➔o➔s➔t➔n➔a➔m➔e➔c➔t➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔t➔a➔i➔l➔e➔d➔ ➔h➔o➔s➔t➔n➔a➔m➔e➔ ➔a➔n➔d➔ ➔O➔S➔ ➔i➔n➔f➔o➔
➔h➔o➔s➔t➔n➔a➔m➔e➔c➔t➔l➔ ➔s➔e➔t➔-➔h➔o➔s➔t➔n➔a➔m➔e➔ ➔n➔e➔w➔n➔a➔m➔e➔ ➔ ➔ ➔#➔ ➔c➔h➔a➔n➔g➔e➔ ➔h➔o➔s➔t➔n➔a➔m➔e➔ ➔p➔e➔r➔m➔a➔n➔e➔n➔t➔l➔y➔
➔c➔a➔t➔ ➔/➔e➔t➔c➔/➔o➔s➔-➔r➔e➔l➔e➔a➔s➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔O➔S➔ ➔d➔e➔t➔a➔i➔l➔s➔ ➔(➔n➔a➔m➔e➔,➔ ➔v➔e➔r➔s➔i➔o➔n➔)➔
➔l➔s➔c➔p➔u➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔C➔P➔U➔ ➔i➔n➔f➔o➔
➔f➔r➔e➔e➔ ➔-➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔R➔A➔M➔ ➔u➔s➔a➔g➔e➔ ➔(➔h➔u➔m➔a➔n➔ ➔r➔e➔a➔d➔a➔b➔l➔e➔)➔
➔u➔p➔t➔i➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔h➔o➔w➔ ➔l➔o➔n➔g➔ ➔s➔y➔s➔t➔e➔m➔ ➔h➔a➔s➔ ➔b➔e➔e➔n➔ ➔r➔u➔n➔n➔i➔n➔g➔
➔w➔h➔o➔a➔m➔i➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔l➔o➔g➔g➔e➔d➔ ➔i➔n➔ ➔u➔s➔e➔r➔
➔i➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔u➔s➔e➔r➔ ➔I➔D➔,➔ ➔g➔r➔o➔u➔p➔ ➔I➔D➔,➔ ➔g➔r➔o➔u➔p➔s➔
➔w➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔w➔h➔o➔ ➔i➔s➔ ➔l➔o➔g➔g➔e➔d➔ ➔i➔n➔ ➔a➔n➔d➔ ➔w➔h➔a➔t➔ ➔t➔h➔e➔y➔'➔r➔e➔ ➔d➔o➔i➔n➔g➔
➔l➔a➔s➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔o➔g➔i➔n➔ ➔h➔i➔s➔t➔o➔r➔y➔
➔D➔a➔t➔e➔ ➔a➔n➔d➔ ➔T➔i➔m➔e➔ ➔—➔ ➔t➔i➔m➔e➔d➔a➔t➔e➔c➔t➔l➔
➔d➔a➔t➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔d➔a➔t➔e➔ ➔a➔n➔d➔ ➔t➔i➔m➔e➔
➔d➔a➔t➔e➔ ➔"➔+➔%➔Y➔-➔%➔m➔-➔%➔d➔ ➔%➔H➔:➔%➔M➔:➔%➔S➔"➔ ➔ ➔ ➔#➔ ➔f➔o➔r➔m➔a➔t➔t➔e➔d➔ ➔d➔a➔t➔e➔
➔
➔
➔
➔
➔➔ ➔➔
➔t➔i➔m➔e➔d➔a➔t➔e➔c➔t➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔t➔a➔i➔l➔e➔d➔ ➔t➔i➔m➔e➔ ➔i➔n➔f➔o➔ ➔i➔n➔c➔l➔u➔d➔i➔n➔g➔ ➔t➔i➔m➔e➔z➔o➔n➔e➔
➔t➔i➔m➔e➔d➔a➔t➔e➔c➔t➔l➔ ➔l➔i➔s➔t➔-➔t➔i➔m➔e➔z➔o➔n➔e➔s➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔a➔l➔l➔ ➔t➔i➔m➔e➔z➔o➔n➔e➔s➔
➔t➔i➔m➔e➔d➔a➔t➔e➔c➔t➔l➔ ➔s➔e➔t➔-➔t➔i➔m➔e➔z➔o➔n➔e➔ ➔A➔s➔i➔a➔/➔K➔o➔l➔k➔a➔t➔a➔ ➔ ➔ ➔#➔ ➔s➔e➔t➔ ➔t➔i➔m➔e➔z➔o➔n➔e➔ ➔(➔f➔o➔r➔ ➔I➔n➔d➔i➔a➔)➔
➔t➔i➔m➔e➔d➔a➔t➔e➔c➔t➔l➔ ➔s➔e➔t➔-➔n➔t➔p➔ ➔t➔r➔u➔e➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔n➔a➔b➔l➔e➔ ➔N➔T➔P➔ ➔t➔i➔m➔e➔ ➔s➔y➔n➔c➔
➔h➔w➔c➔l➔o➔c➔k➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔h➔a➔r➔d➔w➔a➔r➔e➔ ➔c➔l➔o➔c➔k➔ ➔t➔i➔m➔e➔
➔P➔r➔o➔c➔e➔s➔s➔ ➔M➔a➔n➔a➔g➔e➔m➔e➔n➔t➔
➔p➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔r➔o➔c➔e➔s➔s➔e➔s➔ ➔o➔f➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔t➔e➔r➔m➔i➔n➔a➔l➔
➔p➔s➔ ➔a➔u➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔l➔l➔ ➔r➔u➔n➔n➔i➔n➔g➔ ➔p➔r➔o➔c➔e➔s➔s➔e➔s➔ ➔(➔a➔=➔a➔l➔l➔,➔ ➔u➔=➔u➔s➔e➔r➔,➔ ➔x➔=➔n➔o➔ ➔t➔e➔r➔m➔i➔n➔a➔l➔)➔
➔p➔s➔ ➔a➔u➔x➔ ➔|➔ ➔g➔r➔e➔p➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔n➔d➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔p➔r➔o➔c➔e➔s➔s➔
➔t➔o➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔v➔e➔ ➔p➔r➔o➔c➔e➔s➔s➔ ➔m➔o➔n➔i➔t➔o➔r➔ ➔(➔q➔ ➔t➔o➔ ➔q➔u➔i➔t➔)➔
➔h➔t➔o➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔b➔e➔t➔t➔e➔r➔ ➔l➔i➔v➔e➔ ➔m➔o➔n➔i➔t➔o➔r➔ ➔(➔i➔n➔s➔t➔a➔l➔l➔ ➔s➔e➔p➔a➔r➔a➔t➔e➔l➔y➔)➔
➔k➔i➔l➔l➔ ➔P➔I➔D➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔n➔d➔ ➔S➔I➔G➔T➔E➔R➔M➔ ➔(➔g➔r➔a➔c➔e➔f➔u➔l➔ ➔s➔t➔o➔p➔)➔ ➔t➔o➔ ➔p➔r➔o➔c➔e➔s➔s➔
➔k➔i➔l➔l➔ ➔-➔9➔ ➔P➔I➔D➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔n➔d➔ ➔S➔I➔G➔K➔I➔L➔L➔ ➔(➔f➔o➔r➔c➔e➔ ➔s➔t➔o➔p➔)➔ ➔—➔ ➔c➔a➔n➔n➔o➔t➔ ➔b➔e➔ ➔i➔g➔n➔o➔r➔e➔d➔
➔k➔i➔l➔l➔ ➔-➔1➔5➔ ➔P➔I➔D➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔n➔d➔ ➔S➔I➔G➔T➔E➔R➔M➔ ➔e➔x➔p➔l➔i➔c➔i➔t➔l➔y➔
➔k➔i➔l➔l➔a➔l➔l➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔k➔i➔l➔l➔ ➔a➔l➔l➔ ➔p➔r➔o➔c➔e➔s➔s➔e➔s➔ ➔n➔a➔m➔e➔d➔ ➔n➔g➔i➔n➔x➔
➔p➔k➔i➔l➔l➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔k➔i➔l➔l➔ ➔b➔y➔ ➔n➔a➔m➔e➔ ➔p➔a➔t➔t➔e➔r➔n➔
➔p➔g➔r➔e➔p➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔n➔d➔ ➔P➔I➔D➔ ➔o➔f➔ ➔p➔r➔o➔c➔e➔s➔s➔ ➔b➔y➔ ➔n➔a➔m➔e➔
➔n➔o➔h➔u➔p➔ ➔c➔o➔m➔m➔a➔n➔d➔ ➔&➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔u➔n➔ ➔c➔o➔m➔m➔a➔n➔d➔ ➔t➔h➔a➔t➔ ➔s➔u➔r➔v➔i➔v➔e➔s➔ ➔l➔o➔g➔o➔u➔t➔
➔j➔o➔b➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔b➔a➔c➔k➔g➔r➔o➔u➔n➔d➔ ➔j➔o➔b➔s➔
➔b➔g➔ ➔%➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔u➔t➔ ➔j➔o➔b➔ ➔1➔ ➔i➔n➔ ➔b➔a➔c➔k➔g➔r➔o➔u➔n➔d➔
➔f➔g➔ ➔%➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔b➔r➔i➔n➔g➔ ➔j➔o➔b➔ ➔1➔ ➔t➔o➔ ➔f➔o➔r➔e➔g➔r➔o➔u➔n➔d➔
➔S➔e➔r➔v➔i➔c➔e➔ ➔M➔a➔n➔a➔g➔e➔m➔e➔n➔t➔ ➔—➔ ➔s➔y➔s➔t➔e➔m➔c➔t➔l➔
➔s➔y➔s➔t➔e➔m➔c➔t➔l➔ ➔s➔t➔a➔r➔t➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔t➔a➔r➔t➔ ➔s➔e➔r➔v➔i➔c➔e➔
➔s➔y➔s➔t➔e➔m➔c➔t➔l➔ ➔s➔t➔o➔p➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔t➔o➔p➔ ➔s➔e➔r➔v➔i➔c➔e➔
➔s➔y➔s➔t➔e➔m➔c➔t➔l➔ ➔r➔e➔s➔t➔a➔r➔t➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔s➔t➔a➔r➔t➔ ➔s➔e➔r➔v➔i➔c➔e➔
➔s➔y➔s➔t➔e➔m➔c➔t➔l➔ ➔r➔e➔l➔o➔a➔d➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔l➔o➔a➔d➔ ➔c➔o➔n➔f➔i➔g➔ ➔w➔i➔t➔h➔o➔u➔t➔ ➔r➔e➔s➔t➔a➔r➔t➔
➔s➔y➔s➔t➔e➔m➔c➔t➔l➔ ➔s➔t➔a➔t➔u➔s➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔e➔c➔k➔ ➔s➔e➔r➔v➔i➔c➔e➔ ➔s➔t➔a➔t➔u➔s➔
➔s➔y➔s➔t➔e➔m➔c➔t➔l➔ ➔e➔n➔a➔b➔l➔e➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔t➔a➔r➔t➔ ➔o➔n➔ ➔b➔o➔o➔t➔
➔s➔y➔s➔t➔e➔m➔c➔t➔l➔ ➔d➔i➔s➔a➔b➔l➔e➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔o➔n➔'➔t➔ ➔s➔t➔a➔r➔t➔ ➔o➔n➔ ➔b➔o➔o➔t➔
➔s➔y➔s➔t➔e➔m➔c➔t➔l➔ ➔i➔s➔-➔a➔c➔t➔i➔v➔e➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔#➔ ➔i➔s➔ ➔i➔t➔ ➔r➔u➔n➔n➔i➔n➔g➔?➔
➔s➔y➔s➔t➔e➔m➔c➔t➔l➔ ➔i➔s➔-➔e➔n➔a➔b➔l➔e➔d➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔#➔ ➔i➔s➔ ➔i➔t➔ ➔e➔n➔a➔b➔l➔e➔d➔ ➔o➔n➔ ➔b➔o➔o➔t➔?➔
➔s➔y➔s➔t➔e➔m➔c➔t➔l➔ ➔l➔i➔s➔t➔-➔u➔n➔i➔t➔s➔ ➔-➔-➔t➔y➔p➔e➔=➔s➔e➔r➔v➔i➔c➔e➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔a➔l➔l➔ ➔s➔e➔r➔v➔i➔c➔e➔s➔
➔j➔o➔u➔r➔n➔a➔l➔c➔t➔l➔ ➔-➔u➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔v➔i➔e➔w➔ ➔l➔o➔g➔s➔ ➔f➔o➔r➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔s➔e➔r➔v➔i➔c➔e➔
➔j➔o➔u➔r➔n➔a➔l➔c➔t➔l➔ ➔-➔u➔ ➔n➔g➔i➔n➔x➔ ➔-➔f➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔l➔l➔o➔w➔ ➔l➔o➔g➔s➔ ➔f➔o➔r➔ ➔s➔e➔r➔v➔i➔c➔e➔
➔j➔o➔u➔r➔n➔a➔l➔c➔t➔l➔ ➔-➔n➔ ➔5➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔a➔s➔t➔ ➔5➔0➔ ➔l➔o➔g➔ ➔l➔i➔n➔e➔s➔
➔P➔a➔c➔k➔a➔g➔e➔ ➔M➔a➔n➔a➔g➔e➔m➔e➔n➔t➔
➔
➔
➔
➔
➔#➔ ➔U➔b➔u➔n➔t➔u➔/➔D➔e➔b➔i➔a➔n➔ ➔(➔a➔p➔t➔)➔
➔a➔p➔t➔ ➔u➔p➔d➔a➔t➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔u➔p➔d➔a➔t➔e➔ ➔p➔a➔c➔k➔a➔g➔e➔ ➔l➔i➔s➔t➔
➔a➔p➔t➔ ➔u➔p➔g➔r➔a➔d➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔u➔p➔g➔r➔a➔d➔e➔ ➔a➔l➔l➔ ➔p➔a➔c➔k➔a➔g➔e➔s➔
➔a➔p➔t➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔p➔a➔c➔k➔a➔g➔e➔
➔a➔p➔t➔ ➔r➔e➔m➔o➔v➔e➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔p➔a➔c➔k➔a➔g➔e➔
➔a➔p➔t➔ ➔p➔u➔r➔g➔e➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔p➔a➔c➔k➔a➔g➔e➔ ➔+➔ ➔c➔o➔n➔f➔i➔g➔ ➔f➔i➔l➔e➔s➔
➔a➔p➔t➔ ➔s➔e➔a➔r➔c➔h➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔a➔r➔c➔h➔ ➔f➔o➔r➔ ➔p➔a➔c➔k➔a➔g➔e➔
➔d➔p➔k➔g➔ ➔-➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔i➔n➔s➔t➔a➔l➔l➔e➔d➔ ➔p➔a➔c➔k➔a➔g➔e➔s➔
➔#➔ ➔R➔H➔E➔L➔/➔C➔e➔n➔t➔O➔S➔/➔A➔m➔a➔z➔o➔n➔ ➔L➔i➔n➔u➔x➔ ➔(➔y➔u➔m➔/➔d➔n➔f➔)➔
➔y➔u➔m➔ ➔u➔p➔d➔a➔t➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔u➔p➔d➔a➔t➔e➔ ➔a➔l➔l➔ ➔p➔a➔c➔k➔a➔g➔e➔s➔
➔y➔u➔m➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔p➔a➔c➔k➔a➔g➔e➔
➔y➔u➔m➔ ➔r➔e➔m➔o➔v➔e➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔p➔a➔c➔k➔a➔g➔e➔
➔y➔u➔m➔ ➔s➔e➔a➔r➔c➔h➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔a➔r➔c➔h➔ ➔p➔a➔c➔k➔a➔g➔e➔
➔y➔u➔m➔ ➔l➔i➔s➔t➔ ➔i➔n➔s➔t➔a➔l➔l➔e➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔i➔n➔s➔t➔a➔l➔l➔e➔d➔ ➔p➔a➔c➔k➔a➔g➔e➔s➔
➔d➔n➔f➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔a➔m➔e➔ ➔b➔u➔t➔ ➔n➔e➔w➔e➔r➔ ➔(➔d➔n➔f➔ ➔r➔e➔p➔l➔a➔c➔e➔s➔ ➔y➔u➔m➔)➔
➔1➔1➔.➔ ➔U➔s➔e➔r➔ ➔M➔a➔n➔a➔g➔e➔m➔e➔n➔t➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔
➔L➔i➔n➔u➔x➔ ➔h➔a➔s➔ ➔t➔h➔r➔e➔e➔ ➔t➔y➔p➔e➔s➔ ➔o➔f➔ ➔u➔s➔e➔r➔s➔:➔
➔R➔o➔o➔t➔ ➔—➔ ➔s➔u➔p➔e➔r➔u➔s➔e➔r➔,➔ ➔U➔I➔D➔ ➔0➔,➔ ➔f➔u➔l➔l➔ ➔a➔c➔c➔e➔s➔s➔
➔S➔y➔s➔t➔e➔m➔ ➔u➔s➔e➔r➔s➔ ➔—➔ ➔c➔r➔e➔a➔t➔e➔d➔ ➔b➔y➔ ➔s➔e➔r➔v➔i➔c➔e➔s➔ ➔(➔n➔g➔i➔n➔x➔,➔ ➔m➔y➔s➔q➔l➔)➔,➔ ➔U➔I➔D➔ ➔1➔-➔9➔9➔9➔
➔R➔e➔g➔u➔l➔a➔r➔ ➔u➔s➔e➔r➔s➔ ➔—➔ ➔h➔u➔m➔a➔n➔ ➔u➔s➔e➔r➔s➔,➔ ➔U➔I➔D➔ ➔1➔0➔0➔0➔+➔
➔#➔ ➔U➔s➔e➔r➔ ➔i➔n➔f➔o➔ ➔f➔i➔l➔e➔s➔
➔c➔a➔t➔ ➔/➔e➔t➔c➔/➔p➔a➔s➔s➔w➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔o➔f➔ ➔a➔l➔l➔ ➔u➔s➔e➔r➔s➔ ➔(➔u➔s➔e➔r➔n➔a➔m➔e➔:➔x➔:➔U➔I➔D➔:➔G➔I➔D➔:➔i➔n➔f➔o➔:➔h➔o➔m➔e➔:➔s➔h➔e➔l➔l➔)➔
➔c➔a➔t➔ ➔/➔e➔t➔c➔/➔s➔h➔a➔d➔o➔w➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔n➔c➔r➔y➔p➔t➔e➔d➔ ➔p➔a➔s➔s➔w➔o➔r➔d➔s➔ ➔(➔r➔o➔o➔t➔ ➔o➔n➔l➔y➔)➔
➔#➔ ➔C➔r➔e➔a➔t➔e➔ ➔u➔s➔e➔r➔
➔u➔s➔e➔r➔a➔d➔d➔ ➔a➔k➔h➔i➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔u➔s➔e➔r➔ ➔(➔n➔o➔ ➔h➔o➔m➔e➔ ➔d➔i➔r➔ ➔b➔y➔ ➔d➔e➔f➔a➔u➔l➔t➔ ➔o➔n➔ ➔s➔o➔m➔e➔ ➔d➔
➔u➔s➔e➔r➔a➔d➔d➔ ➔-➔m➔ ➔a➔k➔h➔i➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔u➔s➔e➔r➔ ➔W➔I➔T➔H➔ ➔h➔o➔m➔e➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔u➔s➔e➔r➔a➔d➔d➔ ➔-➔m➔ ➔-➔s➔ ➔/➔b➔i➔n➔/➔b➔a➔s➔h➔ ➔a➔k➔h➔i➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔w➔i➔t➔h➔ ➔h➔o➔m➔e➔ ➔d➔i➔r➔ ➔a➔n➔d➔ ➔b➔a➔s➔h➔ ➔s➔h➔e➔l➔l➔
➔u➔s➔e➔r➔a➔d➔d➔ ➔-➔m➔ ➔-➔u➔ ➔1➔5➔0➔0➔ ➔a➔k➔h➔i➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔w➔i➔t➔h➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔U➔I➔D➔
➔u➔s➔e➔r➔a➔d➔d➔ ➔-➔m➔ ➔-➔g➔ ➔d➔e➔v➔o➔p➔s➔ ➔a➔k➔h➔i➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔w➔i➔t➔h➔ ➔p➔r➔i➔m➔a➔r➔y➔ ➔g➔r➔o➔u➔p➔
➔u➔s➔e➔r➔a➔d➔d➔ ➔-➔m➔ ➔-➔G➔ ➔d➔o➔c➔k➔e➔r➔,➔s➔u➔d➔o➔ ➔a➔k➔h➔i➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔w➔i➔t➔h➔ ➔s➔u➔p➔p➔l➔e➔m➔e➔n➔t➔a➔r➔y➔ ➔g➔r➔o➔u➔p➔s➔
➔#➔ ➔S➔e➔t➔/➔c➔h➔a➔n➔g➔e➔ ➔p➔a➔s➔s➔w➔o➔r➔d➔
➔p➔a➔s➔s➔w➔d➔ ➔a➔k➔h➔i➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔t➔ ➔p➔a➔s➔s➔w➔o➔r➔d➔ ➔f➔o➔r➔ ➔u➔s➔e➔r➔
➔p➔a➔s➔s➔w➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔a➔n➔g➔e➔ ➔y➔o➔u➔r➔ ➔o➔w➔n➔ ➔p➔a➔s➔s➔w➔o➔r➔d➔
➔p➔a➔s➔s➔w➔d➔ ➔-➔l➔ ➔a➔k➔h➔i➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔o➔c➔k➔ ➔u➔s➔e➔r➔ ➔a➔c➔c➔o➔u➔n➔t➔
➔p➔a➔s➔s➔w➔d➔ ➔-➔u➔ ➔a➔k➔h➔i➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔u➔n➔l➔o➔c➔k➔ ➔u➔s➔e➔r➔ ➔a➔c➔c➔o➔u➔n➔t➔
➔p➔a➔s➔s➔w➔d➔ ➔-➔e➔ ➔a➔k➔h➔i➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔r➔c➔e➔ ➔p➔a➔s➔s➔w➔o➔r➔d➔ ➔c➔h➔a➔n➔g➔e➔ ➔o➔n➔ ➔n➔e➔x➔t➔ ➔l➔o➔g➔i➔n➔
➔
➔
➔
➔
➔➔ ➔➔
➔#➔ ➔M➔o➔d➔i➔f➔y➔ ➔u➔s➔e➔r➔
➔u➔s➔e➔r➔m➔o➔d➔ ➔-➔s➔ ➔/➔b➔i➔n➔/➔z➔s➔h➔ ➔a➔k➔h➔i➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔a➔n➔g➔e➔ ➔s➔h➔e➔l➔l➔
➔u➔s➔e➔r➔m➔o➔d➔ ➔-➔d➔ ➔/➔h➔o➔m➔e➔/➔n➔e➔w➔d➔i➔r➔ ➔a➔k➔h➔i➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔a➔n➔g➔e➔ ➔h➔o➔m➔e➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔u➔s➔e➔r➔m➔o➔d➔ ➔-➔a➔G➔ ➔d➔o➔c➔k➔e➔r➔ ➔a➔k➔h➔i➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔d➔d➔ ➔u➔s➔e➔r➔ ➔t➔o➔ ➔d➔o➔c➔k➔e➔r➔ ➔g➔r➔o➔u➔p➔ ➔(➔a➔ ➔=➔ ➔a➔p➔p➔e➔n➔d➔,➔ ➔G➔ ➔=➔ ➔g➔r➔o➔u➔
➔u➔s➔e➔r➔m➔o➔d➔ ➔-➔a➔G➔ ➔s➔u➔d➔o➔ ➔a➔k➔h➔i➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔g➔i➔v➔e➔ ➔u➔s➔e➔r➔ ➔s➔u➔d➔o➔ ➔a➔c➔c➔e➔s➔s➔
➔u➔s➔e➔r➔m➔o➔d➔ ➔-➔L➔ ➔a➔k➔h➔i➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔o➔c➔k➔ ➔u➔s➔e➔r➔
➔#➔ ➔D➔e➔l➔e➔t➔e➔ ➔u➔s➔e➔r➔
➔u➔s➔e➔r➔d➔e➔l➔ ➔a➔k➔h➔i➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔u➔s➔e➔r➔ ➔(➔k➔e➔e➔p➔s➔ ➔h➔o➔m➔e➔ ➔d➔i➔r➔)➔
➔u➔s➔e➔r➔d➔e➔l➔ ➔-➔r➔ ➔a➔k➔h➔i➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔u➔s➔e➔r➔ ➔A➔N➔D➔ ➔h➔o➔m➔e➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔#➔ ➔S➔w➔i➔t➔c➔h➔ ➔u➔s➔e➔r➔
➔s➔u➔ ➔a➔k➔h➔i➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔w➔i➔t➔c➔h➔ ➔t➔o➔ ➔a➔k➔h➔i➔l➔ ➔(➔n➔e➔e➔d➔ ➔a➔k➔h➔i➔l➔'➔s➔ ➔p➔a➔s➔s➔w➔o➔r➔d➔)➔
➔s➔u➔ ➔-➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔w➔i➔t➔c➔h➔ ➔t➔o➔ ➔r➔o➔o➔t➔
➔s➔u➔d➔o➔ ➔c➔o➔m➔m➔a➔n➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔u➔n➔ ➔s➔i➔n➔g➔l➔e➔ ➔c➔o➔m➔m➔a➔n➔d➔ ➔a➔s➔ ➔r➔o➔o➔t➔
➔s➔u➔d➔o➔ ➔s➔u➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔b➔e➔c➔o➔m➔e➔ ➔r➔o➔o➔t➔ ➔u➔s➔i➔n➔g➔ ➔y➔o➔u➔r➔ ➔p➔a➔s➔s➔w➔o➔r➔d➔
➔s➔u➔d➔o➔ ➔-➔u➔ ➔a➔k➔h➔i➔l➔ ➔c➔o➔m➔m➔a➔n➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔u➔n➔ ➔c➔o➔m➔m➔a➔n➔d➔ ➔a➔s➔ ➔a➔n➔o➔t➔h➔e➔r➔ ➔u➔s➔e➔r➔
➔#➔ ➔V➔i➔e➔w➔ ➔w➔h➔o➔ ➔i➔s➔ ➔l➔o➔g➔g➔e➔d➔ ➔i➔n➔
➔w➔h➔o➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔o➔g➔g➔e➔d➔ ➔i➔n➔ ➔u➔s➔e➔r➔s➔
➔w➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔o➔g➔g➔e➔d➔ ➔i➔n➔ ➔u➔s➔e➔r➔s➔ ➔+➔ ➔w➔h➔a➔t➔ ➔t➔h➔e➔y➔'➔r➔e➔ ➔d➔o➔i➔n➔g➔
➔i➔d➔ ➔a➔k➔h➔i➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔U➔I➔D➔,➔ ➔G➔I➔D➔,➔ ➔g➔r➔o➔u➔p➔s➔ ➔o➔f➔ ➔u➔s➔e➔r➔
➔f➔i➔n➔g➔e➔r➔ ➔a➔k➔h➔i➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔u➔s➔e➔r➔ ➔i➔n➔f➔o➔ ➔(➔i➔f➔ ➔i➔n➔s➔t➔a➔l➔l➔e➔d➔)➔
➔1➔2➔.➔ ➔G➔r➔o➔u➔p➔ ➔M➔a➔n➔a➔g➔e➔m➔e➔n➔t➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔
➔G➔r➔o➔u➔p➔s➔ ➔a➔l➔l➔o➔w➔ ➔y➔o➔u➔ ➔t➔o➔ ➔m➔a➔n➔a➔g➔e➔ ➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔ ➔f➔o➔r➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔u➔s➔e➔r➔s➔ ➔a➔t➔ ➔o➔n➔c➔e➔.➔
➔#➔ ➔G➔r➔o➔u➔p➔ ➔i➔n➔f➔o➔ ➔f➔i➔l➔e➔
➔c➔a➔t➔ ➔/➔e➔t➔c➔/➔g➔r➔o➔u➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔a➔l➔l➔ ➔g➔r➔o➔u➔p➔s➔ ➔(➔g➔r➔o➔u➔p➔n➔a➔m➔e➔:➔x➔:➔G➔I➔D➔:➔m➔e➔m➔b➔e➔r➔s➔)➔
➔#➔ ➔C➔r➔e➔a➔t➔e➔ ➔g➔r➔o➔u➔p➔
➔g➔r➔o➔u➔p➔a➔d➔d➔ ➔d➔e➔v➔o➔p➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔g➔r➔o➔u➔p➔
➔g➔r➔o➔u➔p➔a➔d➔d➔ ➔-➔g➔ ➔2➔0➔0➔0➔ ➔d➔e➔v➔o➔p➔s➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔g➔r➔o➔u➔p➔ ➔w➔i➔t➔h➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔G➔I➔D➔
➔#➔ ➔M➔o➔d➔i➔f➔y➔ ➔g➔r➔o➔u➔p➔
➔g➔r➔o➔u➔p➔m➔o➔d➔ ➔-➔n➔ ➔n➔e➔w➔n➔a➔m➔e➔ ➔d➔e➔v➔o➔p➔s➔ ➔ ➔ ➔#➔ ➔r➔e➔n➔a➔m➔e➔ ➔g➔r➔o➔u➔p➔
➔g➔r➔o➔u➔p➔m➔o➔d➔ ➔-➔g➔ ➔2➔0➔0➔1➔ ➔d➔e➔v➔o➔p➔s➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔a➔n➔g➔e➔ ➔G➔I➔D➔
➔#➔ ➔D➔e➔l➔e➔t➔e➔ ➔g➔r➔o➔u➔p➔
➔g➔r➔o➔u➔p➔d➔e➔l➔ ➔d➔e➔v➔o➔p➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔g➔r➔o➔u➔p➔
➔#➔ ➔A➔d➔d➔/➔r➔e➔m➔o➔v➔e➔ ➔u➔s➔e➔r➔ ➔f➔r➔o➔m➔ ➔g➔r➔o➔u➔p➔
➔
➔
➔
➔
➔u➔s➔e➔r➔m➔o➔d➔ ➔-➔a➔G➔ ➔d➔e➔v➔o➔p➔s➔ ➔a➔k➔h➔i➔l➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔d➔d➔ ➔a➔k➔h➔i➔l➔ ➔t➔o➔ ➔d➔e➔v➔o➔p➔s➔ ➔g➔r➔o➔u➔p➔
➔g➔p➔a➔s➔s➔w➔d➔ ➔-➔a➔ ➔a➔k➔h➔i➔l➔ ➔d➔e➔v➔o➔p➔s➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔d➔d➔ ➔a➔k➔h➔i➔l➔ ➔t➔o➔ ➔d➔e➔v➔o➔p➔s➔ ➔g➔r➔o➔u➔p➔
➔g➔p➔a➔s➔s➔w➔d➔ ➔-➔d➔ ➔a➔k➔h➔i➔l➔ ➔d➔e➔v➔o➔p➔s➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔a➔k➔h➔i➔l➔ ➔f➔r➔o➔m➔ ➔d➔e➔v➔o➔p➔s➔ ➔g➔r➔o➔u➔p➔
➔#➔ ➔V➔i➔e➔w➔ ➔g➔r➔o➔u➔p➔s➔
➔g➔r➔o➔u➔p➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔g➔r➔o➔u➔p➔s➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔u➔s➔e➔r➔ ➔b➔e➔l➔o➔n➔g➔s➔ ➔t➔o➔
➔g➔r➔o➔u➔p➔s➔ ➔a➔k➔h➔i➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔g➔r➔o➔u➔p➔s➔ ➔a➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔u➔s➔e➔r➔ ➔b➔e➔l➔o➔n➔g➔s➔ ➔t➔o➔
➔i➔d➔ ➔a➔k➔h➔i➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔U➔I➔D➔,➔ ➔G➔I➔D➔,➔ ➔a➔l➔l➔ ➔g➔r➔o➔u➔p➔s➔
➔#➔ ➔P➔r➔i➔m➔a➔r➔y➔ ➔v➔s➔ ➔S➔e➔c➔o➔n➔d➔a➔r➔y➔ ➔g➔r➔o➔u➔p➔s➔
➔#➔ ➔P➔r➔i➔m➔a➔r➔y➔ ➔g➔r➔o➔u➔p➔:➔ ➔d➔e➔f➔a➔u➔l➔t➔ ➔g➔r➔o➔u➔p➔ ➔a➔s➔s➔i➔g➔n➔e➔d➔ ➔w➔h➔e➔n➔ ➔u➔s➔e➔r➔ ➔c➔r➔e➔a➔t➔e➔s➔ ➔f➔i➔l➔e➔s➔
➔#➔ ➔S➔e➔c➔o➔n➔d➔a➔r➔y➔ ➔g➔r➔o➔u➔p➔s➔:➔ ➔a➔d➔d➔i➔t➔i➔o➔n➔a➔l➔ ➔g➔r➔o➔u➔p➔s➔ ➔f➔o➔r➔ ➔e➔x➔t➔r➔a➔ ➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔
➔1➔3➔.➔ ➔F➔i➔l➔e➔ ➔P➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔
➔E➔v➔e➔r➔y➔ ➔f➔i➔l➔e➔ ➔h➔a➔s➔ ➔t➔h➔r➔e➔e➔ ➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔ ➔s➔e➔t➔s➔:➔
➔-➔r➔w➔x➔r➔w➔x➔r➔w➔x➔ ➔ ➔1➔ ➔ ➔a➔k➔h➔i➔l➔ ➔ ➔d➔e➔v➔o➔p➔s➔ ➔ ➔4➔0➔9➔6➔ ➔ ➔J➔a➔n➔ ➔1➔ ➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔
➔│➔└➔─➔─➔┘➔└➔─➔─➔┘➔└➔─➔─➔┘➔
➔│➔ ➔ ➔│➔ ➔ ➔ ➔│➔ ➔ ➔ ➔└➔─➔─➔ ➔o➔t➔h➔e➔r➔s➔ ➔(➔e➔v➔e➔r➔y➔o➔n➔e➔ ➔e➔l➔s➔e➔)➔
➔│➔ ➔ ➔│➔ ➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔ ➔g➔r➔o➔u➔p➔
➔│➔ ➔ ➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔ ➔o➔w➔n➔e➔r➔ ➔(➔u➔s➔e➔r➔)➔
➔└➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔ ➔f➔i➔l➔e➔ ➔t➔y➔p➔e➔ ➔(➔-➔ ➔=➔ ➔f➔i➔l➔e➔,➔ ➔d➔ ➔=➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔,➔ ➔l➔ ➔=➔ ➔s➔y➔m➔l➔i➔n➔k➔)➔
➔P➔e➔r➔m➔i➔s➔s➔i➔o➔n➔ ➔t➔y➔p➔e➔s➔:➔
➔S➔y➔m➔b➔o➔l➔ ➔N➔u➔m➔b➔e➔r➔ ➔M➔e➔a➔n➔i➔n➔g➔ ➔O➔n➔ ➔F➔i➔l➔e➔ ➔O➔n➔ ➔D➔i➔r➔e➔c➔t➔o➔r➔y➔
➔r➔ ➔4➔ ➔r➔e➔a➔d➔ ➔v➔i➔e➔w➔ ➔c➔o➔n➔t➔e➔n➔t➔ ➔l➔i➔s➔t➔ ➔f➔i➔l➔e➔s➔
➔w➔ ➔2➔ ➔w➔r➔i➔t➔e➔ ➔m➔o➔d➔i➔f➔y➔ ➔c➔o➔n➔t➔e➔n➔t➔ ➔c➔r➔e➔a➔t➔e➔/➔d➔e➔l➔e➔t➔e➔ ➔f➔i➔l➔e➔s➔
➔x➔ ➔1➔ ➔e➔x➔e➔c➔u➔t➔e➔ ➔r➔u➔n➔ ➔a➔s➔ ➔p➔r➔o➔g➔r➔a➔m➔ ➔e➔n➔t➔e➔r➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔(➔c➔d➔)➔
➔-➔ ➔0➔ ➔n➔o➔ ➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔ ➔—➔ ➔—➔
➔N➔u➔m➔e➔r➔i➔c➔ ➔(➔O➔c➔t➔a➔l➔)➔ ➔r➔e➔p➔r➔e➔s➔e➔n➔t➔a➔t➔i➔o➔n➔:➔
➔r➔w➔x➔ ➔=➔ ➔4➔+➔2➔+➔1➔ ➔=➔ ➔7➔
➔r➔w➔-➔ ➔=➔ ➔4➔+➔2➔+➔0➔ ➔=➔ ➔6➔
➔r➔-➔x➔ ➔=➔ ➔4➔+➔0➔+➔1➔ ➔=➔ ➔5➔
➔r➔-➔-➔ ➔=➔ ➔4➔+➔0➔+➔0➔ ➔=➔ ➔4➔
➔
➔
➔
➔
➔➔ ➔➔
➔-➔-➔-➔ ➔=➔ ➔0➔+➔0➔+➔0➔ ➔=➔ ➔0➔
➔#➔ ➔E➔x➔a➔m➔p➔l➔e➔s➔:➔
➔7➔5➔5➔ ➔=➔ ➔r➔w➔x➔r➔-➔x➔r➔-➔x➔ ➔ ➔(➔o➔w➔n➔e➔r➔:➔ ➔a➔l➔l➔,➔ ➔g➔r➔o➔u➔p➔:➔ ➔r➔e➔a➔d➔+➔e➔x➔e➔c➔u➔t➔e➔,➔ ➔o➔t➔h➔e➔r➔s➔:➔ ➔r➔e➔a➔d➔+➔e➔x➔e➔c➔u➔t➔e➔)➔
➔6➔4➔4➔ ➔=➔ ➔r➔w➔-➔r➔-➔-➔r➔-➔-➔ ➔ ➔(➔o➔w➔n➔e➔r➔:➔ ➔r➔e➔a➔d➔+➔w➔r➔i➔t➔e➔,➔ ➔g➔r➔o➔u➔p➔:➔ ➔r➔e➔a➔d➔,➔ ➔o➔t➔h➔e➔r➔s➔:➔ ➔r➔e➔a➔d➔)➔
➔6➔0➔0➔ ➔=➔ ➔r➔w➔-➔-➔-➔-➔-➔-➔-➔ ➔ ➔(➔o➔w➔n➔e➔r➔:➔ ➔r➔e➔a➔d➔+➔w➔r➔i➔t➔e➔,➔ ➔n➔o➔b➔o➔d➔y➔ ➔e➔l➔s➔e➔)➔
➔7➔7➔7➔ ➔=➔ ➔r➔w➔x➔r➔w➔x➔r➔w➔x➔ ➔ ➔(➔e➔v➔e➔r➔y➔o➔n➔e➔ ➔f➔u➔l➔l➔ ➔a➔c➔c➔e➔s➔s➔ ➔—➔ ➔D➔A➔N➔G➔E➔R➔O➔U➔S➔,➔ ➔a➔v➔o➔i➔d➔ ➔i➔n➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔)➔
➔c➔h➔m➔o➔d➔ ➔—➔ ➔C➔h➔a➔n➔g➔e➔ ➔P➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔
➔#➔ ➔N➔u➔m➔e➔r➔i➔c➔ ➔m➔o➔d➔e➔
➔c➔h➔m➔o➔d➔ ➔7➔5➔5➔ ➔s➔c➔r➔i➔p➔t➔.➔s➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔w➔x➔r➔-➔x➔r➔-➔x➔
➔c➔h➔m➔o➔d➔ ➔6➔4➔4➔ ➔c➔o➔n➔f➔i➔g➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔w➔-➔r➔-➔-➔r➔-➔-➔
➔c➔h➔m➔o➔d➔ ➔6➔0➔0➔ ➔p➔r➔i➔v➔a➔t➔e➔.➔k➔e➔y➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔w➔-➔-➔-➔-➔-➔-➔-➔ ➔(➔S➔S➔H➔ ➔k➔e➔y➔s➔ ➔m➔u➔s➔t➔ ➔b➔e➔ ➔6➔0➔0➔)➔
➔c➔h➔m➔o➔d➔ ➔7➔7➔7➔ ➔f➔i➔l➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔A➔V➔O➔I➔D➔ ➔i➔n➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔c➔h➔m➔o➔d➔ ➔-➔R➔ ➔7➔5➔5➔ ➔/➔v➔a➔r➔/➔w➔w➔w➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔c➔u➔r➔s➔i➔v➔e➔ ➔—➔ ➔a➔p➔p➔l➔y➔ ➔t➔o➔ ➔a➔l➔l➔ ➔f➔i➔l➔e➔s➔ ➔i➔n➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔#➔ ➔S➔y➔m➔b➔o➔l➔i➔c➔ ➔m➔o➔d➔e➔
➔c➔h➔m➔o➔d➔ ➔u➔+➔x➔ ➔s➔c➔r➔i➔p➔t➔.➔s➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔d➔d➔ ➔e➔x➔e➔c➔u➔t➔e➔ ➔f➔o➔r➔ ➔o➔w➔n➔e➔r➔ ➔(➔u➔=➔u➔s➔e➔r➔,➔ ➔g➔=➔g➔r➔o➔u➔p➔,➔ ➔o➔=➔o➔t➔h➔e➔r➔s➔,➔ ➔a➔=➔a➔l➔l➔
➔c➔h➔m➔o➔d➔ ➔g➔+➔w➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔d➔d➔ ➔w➔r➔i➔t➔e➔ ➔f➔o➔r➔ ➔g➔r➔o➔u➔p➔
➔c➔h➔m➔o➔d➔ ➔o➔-➔r➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔r➔e➔a➔d➔ ➔f➔o➔r➔ ➔o➔t➔h➔e➔r➔s➔
➔c➔h➔m➔o➔d➔ ➔a➔+➔r➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔d➔d➔ ➔r➔e➔a➔d➔ ➔f➔o➔r➔ ➔e➔v➔e➔r➔y➔o➔n➔e➔
➔c➔h➔m➔o➔d➔ ➔u➔=➔r➔w➔x➔,➔g➔=➔r➔x➔,➔o➔=➔r➔ ➔f➔i➔l➔e➔ ➔ ➔ ➔#➔ ➔s➔e➔t➔ ➔e➔x➔a➔c➔t➔ ➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔
➔c➔h➔o➔w➔n➔ ➔—➔ ➔C➔h➔a➔n➔g➔e➔ ➔O➔w➔n➔e➔r➔
➔c➔h➔o➔w➔n➔ ➔a➔k➔h➔i➔l➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔a➔n➔g➔e➔ ➔o➔w➔n➔e➔r➔ ➔t➔o➔ ➔a➔k➔h➔i➔l➔
➔c➔h➔o➔w➔n➔ ➔a➔k➔h➔i➔l➔:➔d➔e➔v➔o➔p➔s➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔a➔n➔g➔e➔ ➔o➔w➔n➔e➔r➔ ➔A➔N➔D➔ ➔g➔r➔o➔u➔p➔
➔c➔h➔o➔w➔n➔ ➔:➔d➔e➔v➔o➔p➔s➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔a➔n➔g➔e➔ ➔g➔r➔o➔u➔p➔ ➔o➔n➔l➔y➔
➔c➔h➔o➔w➔n➔ ➔-➔R➔ ➔a➔k➔h➔i➔l➔:➔d➔e➔v➔o➔p➔s➔ ➔/➔v➔a➔r➔/➔w➔w➔w➔/➔ ➔ ➔#➔ ➔r➔e➔c➔u➔r➔s➔i➔v➔e➔ ➔c➔h➔a➔n➔g➔e➔
➔c➔h➔g➔r➔p➔ ➔—➔ ➔C➔h➔a➔n➔g➔e➔ ➔G➔r➔o➔u➔p➔
➔c➔h➔g➔r➔p➔ ➔d➔e➔v➔o➔p➔s➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔a➔n➔g➔e➔ ➔g➔r➔o➔u➔p➔ ➔o➔f➔ ➔f➔i➔l➔e➔
➔c➔h➔g➔r➔p➔ ➔-➔R➔ ➔d➔e➔v➔o➔p➔s➔ ➔/➔p➔r➔o➔j➔e➔c➔t➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔c➔u➔r➔s➔i➔v➔e➔
➔u➔m➔a➔s➔k➔ ➔—➔ ➔D➔e➔f➔a➔u➔l➔t➔ ➔P➔e➔r➔m➔i➔s➔s➔i➔o➔n➔ ➔M➔a➔s➔k➔
➔
➔
➔
➔
➔u➔m➔a➔s➔k➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔u➔m➔a➔s➔k➔ ➔(➔u➔s➔u➔a➔l➔l➔y➔ ➔0➔2➔2➔)➔
➔u➔m➔a➔s➔k➔ ➔0➔2➔2➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔t➔ ➔u➔m➔a➔s➔k➔
➔#➔ ➔u➔m➔a➔s➔k➔ ➔0➔2➔2➔ ➔m➔e➔a➔n➔s➔ ➔n➔e➔w➔ ➔f➔i➔l➔e➔s➔ ➔g➔e➔t➔ ➔6➔4➔4➔,➔ ➔n➔e➔w➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔i➔e➔s➔ ➔g➔e➔t➔ ➔7➔5➔5➔
➔#➔ ➔6➔6➔6➔ ➔(➔f➔i➔l➔e➔ ➔d➔e➔f➔a➔u➔l➔t➔)➔ ➔-➔ ➔0➔2➔2➔ ➔=➔ ➔6➔4➔4➔
➔#➔ ➔7➔7➔7➔ ➔(➔d➔i➔r➔ ➔d➔e➔f➔a➔u➔l➔t➔)➔ ➔ ➔-➔ ➔0➔2➔2➔ ➔=➔ ➔7➔5➔5➔
➔S➔p➔e➔c➔i➔a➔l➔ ➔P➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔
➔#➔ ➔S➔U➔I➔D➔ ➔(➔S➔e➔t➔ ➔U➔s➔e➔r➔ ➔I➔D➔)➔ ➔—➔ ➔r➔u➔n➔ ➔f➔i➔l➔e➔ ➔a➔s➔ ➔o➔w➔n➔e➔r➔,➔ ➔n➔o➔t➔ ➔a➔s➔ ➔e➔x➔e➔c➔u➔t➔o➔r➔
➔c➔h➔m➔o➔d➔ ➔u➔+➔s➔ ➔s➔c➔r➔i➔p➔t➔.➔s➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔t➔s➔ ➔S➔U➔I➔D➔
➔c➔h➔m➔o➔d➔ ➔4➔7➔5➔5➔ ➔s➔c➔r➔i➔p➔t➔.➔s➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔n➔u➔m➔e➔r➔i➔c➔
➔#➔ ➔S➔G➔I➔D➔ ➔(➔S➔e➔t➔ ➔G➔r➔o➔u➔p➔ ➔I➔D➔)➔ ➔—➔ ➔f➔i➔l➔e➔s➔ ➔i➔n➔h➔e➔r➔i➔t➔ ➔g➔r➔o➔u➔p➔ ➔o➔f➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔c➔h➔m➔o➔d➔ ➔g➔+➔s➔ ➔/➔s➔h➔a➔r➔e➔d➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔t➔s➔ ➔S➔G➔I➔D➔ ➔o➔n➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔c➔h➔m➔o➔d➔ ➔2➔7➔5➔5➔ ➔/➔s➔h➔a➔r➔e➔d➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔n➔u➔m➔e➔r➔i➔c➔
➔#➔ ➔S➔t➔i➔c➔k➔y➔ ➔B➔i➔t➔ ➔—➔ ➔o➔n➔l➔y➔ ➔o➔w➔n➔e➔r➔ ➔c➔a➔n➔ ➔d➔e➔l➔e➔t➔e➔ ➔t➔h➔e➔i➔r➔ ➔f➔i➔l➔e➔s➔ ➔i➔n➔ ➔s➔h➔a➔r➔e➔d➔ ➔d➔i➔r➔ ➔(➔l➔i➔k➔e➔ ➔/➔t➔m➔p➔)➔
➔c➔h➔m➔o➔d➔ ➔+➔t➔ ➔/➔s➔h➔a➔r➔e➔d➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔t➔s➔ ➔s➔t➔i➔c➔k➔y➔ ➔b➔i➔t➔
➔c➔h➔m➔o➔d➔ ➔1➔7➔7➔7➔ ➔/➔t➔m➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔n➔u➔m➔e➔r➔i➔c➔ ➔(➔t➔ ➔s➔h➔o➔w➔n➔ ➔a➔s➔ ➔T➔ ➔i➔f➔ ➔n➔o➔ ➔e➔x➔e➔c➔u➔t➔e➔)➔
➔#➔ ➔V➔i➔e➔w➔ ➔s➔p➔e➔c➔i➔a➔l➔ ➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔
➔l➔s➔ ➔-➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔ ➔i➔n➔ ➔e➔x➔e➔c➔u➔t➔e➔ ➔p➔o➔s➔i➔t➔i➔o➔n➔ ➔=➔ ➔S➔U➔I➔D➔/➔S➔G➔I➔D➔,➔ ➔t➔ ➔=➔ ➔s➔t➔i➔c➔k➔y➔
➔1➔4➔.➔ ➔A➔C➔L➔ ➔—➔ ➔s➔e➔t➔f➔a➔c➔l➔ ➔a➔n➔d➔ ➔g➔e➔t➔f➔a➔c➔l➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔A➔C➔L➔?➔
➔S➔t➔a➔n➔d➔a➔r➔d➔ ➔L➔i➔n➔u➔x➔ ➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔ ➔o➔n➔l➔y➔ ➔a➔l➔l➔o➔w➔ ➔o➔n➔e➔ ➔o➔w➔n➔e➔r➔ ➔a➔n➔d➔ ➔o➔n➔e➔ ➔g➔r➔o➔u➔p➔ ➔p➔e➔r➔ ➔f➔i➔l➔e➔.➔ ➔A➔C➔L➔ ➔(➔A➔c➔c➔e➔s➔s➔ ➔C➔o➔n➔t➔r➔o➔l➔ ➔L➔i➔s➔t➔)➔ ➔g➔i➔v➔e➔s➔ ➔y➔o➔u➔
➔f➔i➔n➔e➔-➔g➔r➔a➔i➔n➔e➔d➔ ➔c➔o➔n➔t➔r➔o➔l➔ ➔—➔ ➔s➔e➔t➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔t➔ ➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔ ➔f➔o➔r➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔u➔s➔e➔r➔s➔ ➔a➔n➔d➔ ➔g➔r➔o➔u➔p➔s➔ ➔o➔n➔ ➔t➔h➔e➔ ➔s➔a➔m➔e➔ ➔f➔i➔l➔e➔.➔
➔#➔ ➔I➔n➔s➔t➔a➔l➔l➔ ➔A➔C➔L➔ ➔i➔f➔ ➔n➔e➔e➔d➔e➔d➔
➔a➔p➔t➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔a➔c➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔U➔b➔u➔n➔t➔u➔
➔y➔u➔m➔ ➔i➔n➔s➔t➔a➔l➔l➔ ➔a➔c➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔R➔H➔E➔L➔
➔#➔ ➔C➔h➔e➔c➔k➔ ➔i➔f➔ ➔A➔C➔L➔ ➔i➔s➔ ➔s➔u➔p➔p➔o➔r➔t➔e➔d➔
➔m➔o➔u➔n➔t➔ ➔|➔ ➔g➔r➔e➔p➔ ➔a➔c➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔o➔o➔k➔ ➔f➔o➔r➔ ➔'➔a➔c➔l➔'➔ ➔i➔n➔ ➔m➔o➔u➔n➔t➔ ➔o➔p➔t➔i➔o➔n➔s➔
➔#➔ ➔g➔e➔t➔f➔a➔c➔l➔ ➔—➔ ➔v➔i➔e➔w➔ ➔A➔C➔L➔ ➔o➔f➔ ➔a➔ ➔f➔i➔l➔e➔
➔g➔e➔t➔f➔a➔c➔l➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔.➔t➔x➔t➔
➔#➔ ➔O➔u➔t➔p➔u➔t➔:➔
➔#➔ ➔f➔i➔l➔e➔:➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔.➔t➔x➔t➔
➔
➔
➔
➔
➔#➔ ➔o➔w➔n➔e➔r➔:➔ ➔a➔k➔h➔i➔l➔
➔#➔ ➔g➔r➔o➔u➔p➔:➔ ➔d➔e➔v➔o➔p➔s➔
➔#➔ ➔u➔s➔e➔r➔:➔:➔r➔w➔-➔
➔#➔ ➔g➔r➔o➔u➔p➔:➔:➔r➔-➔-➔
➔#➔ ➔o➔t➔h➔e➔r➔:➔:➔r➔-➔-➔
➔#➔ ➔s➔e➔t➔f➔a➔c➔l➔ ➔—➔ ➔s➔e➔t➔ ➔A➔C➔L➔
➔s➔e➔t➔f➔a➔c➔l➔ ➔-➔m➔ ➔u➔:➔j➔o➔h➔n➔:➔r➔w➔x➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔g➔i➔v➔e➔ ➔j➔o➔h➔n➔ ➔r➔w➔x➔ ➔o➔n➔ ➔f➔i➔l➔e➔
➔s➔e➔t➔f➔a➔c➔l➔ ➔-➔m➔ ➔u➔:➔j➔a➔n➔e➔:➔r➔-➔-➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔g➔i➔v➔e➔ ➔j➔a➔n➔e➔ ➔r➔e➔a➔d➔ ➔o➔n➔l➔y➔
➔s➔e➔t➔f➔a➔c➔l➔ ➔-➔m➔ ➔g➔:➔q➔a➔:➔r➔x➔ ➔/➔t➔e➔s➔t➔d➔i➔r➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔g➔i➔v➔e➔ ➔q➔a➔ ➔g➔r➔o➔u➔p➔ ➔r➔x➔ ➔o➔n➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔s➔e➔t➔f➔a➔c➔l➔ ➔-➔R➔ ➔-➔m➔ ➔u➔:➔j➔o➔h➔n➔:➔r➔w➔x➔ ➔/➔p➔r➔o➔j➔e➔c➔t➔/➔ ➔ ➔#➔ ➔r➔e➔c➔u➔r➔s➔i➔v➔e➔ ➔A➔C➔L➔
➔s➔e➔t➔f➔a➔c➔l➔ ➔-➔x➔ ➔u➔:➔j➔o➔h➔n➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔A➔C➔L➔ ➔f➔o➔r➔ ➔j➔o➔h➔n➔
➔s➔e➔t➔f➔a➔c➔l➔ ➔-➔b➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔A➔L➔L➔ ➔A➔C➔L➔s➔ ➔f➔r➔o➔m➔ ➔f➔i➔l➔e➔
➔#➔ ➔D➔e➔f➔a➔u➔l➔t➔ ➔A➔C➔L➔ ➔(➔i➔n➔h➔e➔r➔i➔t➔e➔d➔ ➔b➔y➔ ➔n➔e➔w➔ ➔f➔i➔l➔e➔s➔ ➔i➔n➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔)➔
➔s➔e➔t➔f➔a➔c➔l➔ ➔-➔d➔ ➔-➔m➔ ➔u➔:➔j➔o➔h➔n➔:➔r➔w➔x➔ ➔/➔s➔h➔a➔r➔e➔d➔/➔ ➔ ➔ ➔#➔ ➔a➔n➔y➔ ➔n➔e➔w➔ ➔f➔i➔l➔e➔ ➔i➔n➔ ➔/➔s➔h➔a➔r➔e➔d➔ ➔g➔e➔t➔s➔ ➔j➔o➔h➔n➔'➔s➔ ➔A➔C➔L➔
➔#➔ ➔M➔a➔s➔k➔ ➔—➔ ➔l➔i➔m➔i➔t➔s➔ ➔e➔f➔f➔e➔c➔t➔i➔v➔e➔ ➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔
➔s➔e➔t➔f➔a➔c➔l➔ ➔-➔m➔ ➔m➔:➔r➔x➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔t➔ ➔m➔a➔s➔k➔ ➔t➔o➔ ➔r➔x➔ ➔(➔l➔i➔m➔i➔t➔s➔ ➔g➔r➔o➔u➔p➔ ➔+➔ ➔n➔a➔m➔e➔d➔ ➔u➔s➔e➔r➔s➔)➔
➔1➔5➔.➔ ➔F➔i➔l➔e➔ ➔C➔o➔m➔p➔r➔e➔s➔s➔i➔o➔n➔ ➔a➔n➔d➔ ➔A➔r➔c➔h➔i➔v➔i➔n➔g➔
➔t➔a➔r➔ ➔—➔ ➔T➔a➔p➔e➔ ➔A➔r➔c➔h➔i➔v➔e➔ ➔(➔m➔o➔s➔t➔ ➔c➔o➔m➔m➔o➔n➔ ➔i➔n➔ ➔L➔i➔n➔u➔x➔)➔
➔#➔ ➔C➔r➔e➔a➔t➔e➔ ➔a➔r➔c➔h➔i➔v➔e➔
➔t➔a➔r➔ ➔-➔c➔v➔f➔ ➔a➔r➔c➔h➔i➔v➔e➔.➔t➔a➔r➔ ➔f➔i➔l➔e➔s➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔t➔a➔r➔ ➔(➔c➔=➔c➔r➔e➔a➔t➔e➔,➔ ➔v➔=➔v➔e➔r➔b➔o➔s➔e➔,➔ ➔f➔=➔f➔i➔l➔e➔)➔
➔t➔a➔r➔ ➔-➔c➔z➔v➔f➔ ➔a➔r➔c➔h➔i➔v➔e➔.➔t➔a➔r➔.➔g➔z➔ ➔f➔i➔l➔e➔s➔/➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔c➔o➔m➔p➔r➔e➔s➔s➔e➔d➔ ➔t➔a➔r➔.➔g➔z➔ ➔(➔z➔=➔g➔z➔i➔p➔)➔
➔t➔a➔r➔ ➔-➔c➔j➔v➔f➔ ➔a➔r➔c➔h➔i➔v➔e➔.➔t➔a➔r➔.➔b➔z➔2➔ ➔f➔i➔l➔e➔s➔/➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔c➔o➔m➔p➔r➔e➔s➔s➔e➔d➔ ➔t➔a➔r➔.➔b➔z➔2➔ ➔(➔j➔=➔b➔z➔i➔p➔2➔)➔
➔t➔a➔r➔ ➔-➔c➔J➔v➔f➔ ➔a➔r➔c➔h➔i➔v➔e➔.➔t➔a➔r➔.➔x➔z➔ ➔f➔i➔l➔e➔s➔/➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔r➔e➔a➔t➔e➔ ➔c➔o➔m➔p➔r➔e➔s➔s➔e➔d➔ ➔t➔a➔r➔.➔x➔z➔ ➔(➔J➔=➔x➔z➔)➔
➔#➔ ➔E➔x➔t➔r➔a➔c➔t➔ ➔a➔r➔c➔h➔i➔v➔e➔
➔t➔a➔r➔ ➔-➔x➔v➔f➔ ➔a➔r➔c➔h➔i➔v➔e➔.➔t➔a➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔x➔t➔r➔a➔c➔t➔ ➔t➔a➔r➔
➔t➔a➔r➔ ➔-➔x➔z➔v➔f➔ ➔a➔r➔c➔h➔i➔v➔e➔.➔t➔a➔r➔.➔g➔z➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔x➔t➔r➔a➔c➔t➔ ➔t➔a➔r➔.➔g➔z➔
➔t➔a➔r➔ ➔-➔x➔z➔v➔f➔ ➔a➔r➔c➔h➔i➔v➔e➔.➔t➔a➔r➔.➔g➔z➔ ➔-➔C➔ ➔/➔p➔a➔t➔h➔/➔ ➔ ➔#➔ ➔e➔x➔t➔r➔a➔c➔t➔ ➔t➔o➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔#➔ ➔V➔i➔e➔w➔ ➔c➔o➔n➔t➔e➔n➔t➔s➔ ➔w➔i➔t➔h➔o➔u➔t➔ ➔e➔x➔t➔r➔a➔c➔t➔i➔n➔g➔
➔t➔a➔r➔ ➔-➔t➔v➔f➔ ➔a➔r➔c➔h➔i➔v➔e➔.➔t➔a➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔c➔o➔n➔t➔e➔n➔t➔s➔
➔#➔ ➔A➔d➔d➔ ➔t➔o➔ ➔e➔x➔i➔s➔t➔i➔n➔g➔ ➔a➔r➔c➔h➔i➔v➔e➔
➔t➔a➔r➔ ➔-➔r➔v➔f➔ ➔a➔r➔c➔h➔i➔v➔e➔.➔t➔a➔r➔ ➔n➔e➔w➔f➔i➔l➔e➔.➔t➔x➔t➔
➔#➔ ➔M➔e➔m➔o➔r➔y➔ ➔t➔r➔i➔c➔k➔:➔ ➔c➔=➔c➔r➔e➔a➔t➔e➔,➔ ➔x➔=➔e➔x➔t➔r➔a➔c➔t➔,➔ ➔t➔=➔l➔i➔s➔t➔,➔ ➔v➔=➔v➔e➔r➔b➔o➔s➔e➔,➔ ➔f➔=➔f➔i➔l➔e➔n➔a➔m➔e➔,➔ ➔z➔=➔g➔z➔i➔p➔
➔
➔
➔
➔
➔➔ ➔➔
➔g➔z➔i➔p➔ ➔/➔ ➔g➔u➔n➔z➔i➔p➔
➔g➔z➔i➔p➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔m➔p➔r➔e➔s➔s➔ ➔—➔ ➔c➔r➔e➔a➔t➔e➔s➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔.➔g➔z➔,➔ ➔r➔e➔m➔o➔v➔e➔s➔ ➔o➔r➔i➔g➔i➔n➔a➔
➔g➔z➔i➔p➔ ➔-➔k➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔m➔p➔r➔e➔s➔s➔,➔ ➔k➔e➔e➔p➔ ➔o➔r➔i➔g➔i➔n➔a➔l➔
➔g➔z➔i➔p➔ ➔-➔d➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔.➔g➔z➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔c➔o➔m➔p➔r➔e➔s➔s➔
➔g➔u➔n➔z➔i➔p➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔.➔g➔z➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔c➔o➔m➔p➔r➔e➔s➔s➔ ➔(➔s➔a➔m➔e➔ ➔a➔s➔ ➔g➔z➔i➔p➔ ➔-➔d➔)➔
➔g➔z➔i➔p➔ ➔-➔l➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔.➔g➔z➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔c➔o➔m➔p➔r➔e➔s➔s➔i➔o➔n➔ ➔s➔t➔a➔t➔s➔
➔g➔z➔i➔p➔ ➔-➔9➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔m➔a➔x➔i➔m➔u➔m➔ ➔c➔o➔m➔p➔r➔e➔s➔s➔i➔o➔n➔
➔z➔i➔p➔ ➔/➔ ➔u➔n➔z➔i➔p➔
➔z➔i➔p➔ ➔a➔r➔c➔h➔i➔v➔e➔.➔z➔i➔p➔ ➔f➔i➔l➔e➔1➔ ➔f➔i➔l➔e➔2➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔z➔i➔p➔ ➔f➔i➔l➔e➔s➔
➔z➔i➔p➔ ➔-➔r➔ ➔a➔r➔c➔h➔i➔v➔e➔.➔z➔i➔p➔ ➔f➔o➔l➔d➔e➔r➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔z➔i➔p➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔r➔e➔c➔u➔r➔s➔i➔v➔e➔l➔y➔
➔u➔n➔z➔i➔p➔ ➔a➔r➔c➔h➔i➔v➔e➔.➔z➔i➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔x➔t➔r➔a➔c➔t➔ ➔z➔i➔p➔
➔u➔n➔z➔i➔p➔ ➔a➔r➔c➔h➔i➔v➔e➔.➔z➔i➔p➔ ➔-➔d➔ ➔/➔p➔a➔t➔h➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔x➔t➔r➔a➔c➔t➔ ➔t➔o➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔u➔n➔z➔i➔p➔ ➔-➔l➔ ➔a➔r➔c➔h➔i➔v➔e➔.➔z➔i➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔c➔o➔n➔t➔e➔n➔t➔s➔
➔O➔t➔h➔e➔r➔ ➔c➔o➔m➔p➔r➔e➔s➔s➔i➔o➔n➔
➔b➔z➔i➔p➔2➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔m➔p➔r➔e➔s➔s➔ ➔w➔i➔t➔h➔ ➔b➔z➔i➔p➔2➔ ➔(➔b➔e➔t➔t➔e➔r➔ ➔r➔a➔t➔i➔o➔,➔ ➔s➔l➔o➔w➔e➔r➔)➔
➔b➔u➔n➔z➔i➔p➔2➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔.➔b➔z➔2➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔c➔o➔m➔p➔r➔e➔s➔s➔
➔x➔z➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔m➔p➔r➔e➔s➔s➔ ➔w➔i➔t➔h➔ ➔x➔z➔ ➔(➔b➔e➔s➔t➔ ➔r➔a➔t➔i➔o➔,➔ ➔s➔l➔o➔w➔e➔s➔t➔)➔
➔u➔n➔x➔z➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔.➔x➔z➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔c➔o➔m➔p➔r➔e➔s➔s➔
➔1➔6➔.➔ ➔F➔i➔l➔t➔e➔r➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔ ➔a➔n➔d➔ ➔R➔e➔g➔u➔l➔a➔r➔ ➔E➔x➔p➔r➔e➔s➔s➔i➔o➔n➔s➔
➔g➔r➔e➔p➔ ➔—➔ ➔S➔e➔a➔r➔c➔h➔ ➔T➔e➔x➔t➔
➔g➔r➔e➔p➔ ➔"➔p➔a➔t➔t➔e➔r➔n➔"➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔a➔r➔c➔h➔ ➔f➔o➔r➔ ➔p➔a➔t➔t➔e➔r➔n➔ ➔i➔n➔ ➔f➔i➔l➔e➔
➔g➔r➔e➔p➔ ➔-➔i➔ ➔"➔p➔a➔t➔t➔e➔r➔n➔"➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔a➔s➔e➔ ➔i➔n➔s➔e➔n➔s➔i➔t➔i➔v➔e➔
➔g➔r➔e➔p➔ ➔-➔r➔ ➔"➔p➔a➔t➔t➔e➔r➔n➔"➔ ➔/➔v➔a➔r➔/➔l➔o➔g➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔c➔u➔r➔s➔i➔v➔e➔ ➔s➔e➔a➔r➔c➔h➔ ➔i➔n➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔g➔r➔e➔p➔ ➔-➔n➔ ➔"➔p➔a➔t➔t➔e➔r➔n➔"➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔l➔i➔n➔e➔ ➔n➔u➔m➔b➔e➔r➔s➔
➔g➔r➔e➔p➔ ➔-➔v➔ ➔"➔p➔a➔t➔t➔e➔r➔n➔"➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔i➔n➔v➔e➔r➔t➔ ➔—➔ ➔s➔h➔o➔w➔ ➔l➔i➔n➔e➔s➔ ➔t➔h➔a➔t➔ ➔D➔O➔N➔'➔T➔ ➔m➔a➔t➔c➔h➔
➔g➔r➔e➔p➔ ➔-➔c➔ ➔"➔p➔a➔t➔t➔e➔r➔n➔"➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔u➔n➔t➔ ➔m➔a➔t➔c➔h➔i➔n➔g➔ ➔l➔i➔n➔e➔s➔
➔g➔r➔e➔p➔ ➔-➔l➔ ➔"➔p➔a➔t➔t➔e➔r➔n➔"➔ ➔*➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔f➔i➔l➔e➔s➔ ➔t➔h➔a➔t➔ ➔c➔o➔n➔t➔a➔i➔n➔ ➔p➔a➔t➔t➔e➔r➔n➔
➔g➔r➔e➔p➔ ➔-➔w➔ ➔"➔w➔o➔r➔d➔"➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔m➔a➔t➔c➔h➔ ➔w➔h➔o➔l➔e➔ ➔w➔o➔r➔d➔ ➔o➔n➔l➔y➔
➔g➔r➔e➔p➔ ➔-➔A➔ ➔3➔ ➔"➔p➔a➔t➔t➔e➔r➔n➔"➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔3➔ ➔l➔i➔n➔e➔s➔ ➔A➔f➔t➔e➔r➔ ➔m➔a➔t➔c➔h➔
➔
➔
➔
➔
➔g➔r➔e➔p➔ ➔-➔B➔ ➔3➔ ➔"➔p➔a➔t➔t➔e➔r➔n➔"➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔3➔ ➔l➔i➔n➔e➔s➔ ➔B➔e➔f➔o➔r➔e➔ ➔m➔a➔t➔c➔h➔
➔g➔r➔e➔p➔ ➔-➔E➔ ➔"➔p➔a➔t➔t➔e➔r➔n➔1➔|➔p➔a➔t➔t➔e➔r➔n➔2➔"➔ ➔f➔i➔l➔e➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔x➔t➔e➔n➔d➔e➔d➔ ➔r➔e➔g➔e➔x➔ ➔(➔O➔R➔)➔
➔g➔r➔e➔p➔ ➔"➔^➔s➔t➔a➔r➔t➔"➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔n➔e➔s➔ ➔s➔t➔a➔r➔t➔i➔n➔g➔ ➔w➔i➔t➔h➔ ➔"➔s➔t➔a➔r➔t➔"➔
➔g➔r➔e➔p➔ ➔"➔e➔n➔d➔$➔"➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔n➔e➔s➔ ➔e➔n➔d➔i➔n➔g➔ ➔w➔i➔t➔h➔ ➔"➔e➔n➔d➔"➔
➔g➔r➔e➔p➔ ➔"➔^➔$➔"➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔m➔p➔t➔y➔ ➔l➔i➔n➔e➔s➔
➔#➔ ➔R➔e➔a➔l➔ ➔D➔e➔v➔O➔p➔s➔ ➔e➔x➔a➔m➔p➔l➔e➔s➔:➔
➔g➔r➔e➔p➔ ➔"➔E➔R➔R➔O➔R➔"➔ ➔/➔v➔a➔r➔/➔l➔o➔g➔/➔a➔p➔p➔.➔l➔o➔g➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔n➔d➔ ➔e➔r➔r➔o➔r➔s➔ ➔i➔n➔ ➔l➔o➔g➔
➔g➔r➔e➔p➔ ➔-➔i➔ ➔"➔f➔a➔i➔l➔e➔d➔"➔ ➔/➔v➔a➔r➔/➔l➔o➔g➔/➔s➔y➔s➔l➔o➔g➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔n➔d➔ ➔f➔a➔i➔l➔u➔r➔e➔s➔
➔p➔s➔ ➔a➔u➔x➔ ➔|➔ ➔g➔r➔e➔p➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔n➔d➔ ➔n➔g➔i➔n➔x➔ ➔p➔r➔o➔c➔e➔s➔s➔
➔c➔a➔t➔ ➔/➔e➔t➔c➔/➔p➔a➔s➔s➔w➔d➔ ➔|➔ ➔g➔r➔e➔p➔ ➔"➔/➔b➔i➔n➔/➔b➔a➔s➔h➔"➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔u➔s➔e➔r➔s➔ ➔w➔i➔t➔h➔ ➔b➔a➔s➔h➔ ➔s➔h➔e➔l➔l➔
➔R➔e➔g➔u➔l➔a➔r➔ ➔E➔x➔p➔r➔e➔s➔s➔i➔o➔n➔s➔ ➔(➔R➔e➔g➔e➔x➔)➔ ➔Q➔u➔i➔c➔k➔ ➔R➔e➔f➔e➔r➔e➔n➔c➔e➔
➔.➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔a➔n➔y➔ ➔s➔i➔n➔g➔l➔e➔ ➔c➔h➔a➔r➔a➔c➔t➔e➔r➔
➔*➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔z➔e➔r➔o➔ ➔o➔r➔ ➔m➔o➔r➔e➔ ➔o➔f➔ ➔p➔r➔e➔v➔i➔o➔u➔s➔
➔+➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔o➔n➔e➔ ➔o➔r➔ ➔m➔o➔r➔e➔ ➔o➔f➔ ➔p➔r➔e➔v➔i➔o➔u➔s➔ ➔(➔u➔s➔e➔ ➔w➔i➔t➔h➔ ➔-➔E➔)➔
➔?➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔z➔e➔r➔o➔ ➔o➔r➔ ➔o➔n➔e➔ ➔o➔f➔ ➔p➔r➔e➔v➔i➔o➔u➔s➔ ➔(➔u➔s➔e➔ ➔w➔i➔t➔h➔ ➔-➔E➔)➔
➔^➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔t➔a➔r➔t➔ ➔o➔f➔ ➔l➔i➔n➔e➔
➔$➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔e➔n➔d➔ ➔o➔f➔ ➔l➔i➔n➔e➔
➔[➔]➔ ➔ ➔ ➔ ➔ ➔ ➔c➔h➔a➔r➔a➔c➔t➔e➔r➔ ➔c➔l➔a➔s➔s➔ ➔[➔a➔b➔c➔]➔ ➔=➔ ➔a➔,➔ ➔b➔,➔ ➔o➔r➔ ➔c➔
➔[➔^➔]➔ ➔ ➔ ➔ ➔ ➔n➔e➔g➔a➔t➔e➔d➔ ➔c➔l➔a➔s➔s➔ ➔[➔^➔a➔b➔c➔]➔ ➔=➔ ➔n➔o➔t➔ ➔a➔,➔ ➔b➔,➔ ➔o➔r➔ ➔c➔
➔|➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔O➔R➔ ➔(➔u➔s➔e➔ ➔w➔i➔t➔h➔ ➔-➔E➔)➔
➔\➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔e➔s➔c➔a➔p➔e➔ ➔s➔p➔e➔c➔i➔a➔l➔ ➔c➔h➔a➔r➔a➔c➔t➔e➔r➔
➔{➔n➔}➔ ➔ ➔ ➔ ➔ ➔e➔x➔a➔c➔t➔l➔y➔ ➔n➔ ➔t➔i➔m➔e➔s➔
➔{➔n➔,➔m➔}➔ ➔ ➔ ➔b➔e➔t➔w➔e➔e➔n➔ ➔n➔ ➔a➔n➔d➔ ➔m➔ ➔t➔i➔m➔e➔s➔
➔#➔ ➔E➔x➔a➔m➔p➔l➔e➔s➔:➔
➔g➔r➔e➔p➔ ➔"➔^➔[➔0➔-➔9➔]➔"➔ ➔f➔i➔l➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔n➔e➔s➔ ➔s➔t➔a➔r➔t➔i➔n➔g➔ ➔w➔i➔t➔h➔ ➔d➔i➔g➔i➔t➔
➔g➔r➔e➔p➔ ➔"➔[➔0➔-➔9➔]➔\➔{➔3➔\➔}➔"➔ ➔f➔i➔l➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔x➔a➔c➔t➔l➔y➔ ➔3➔ ➔d➔i➔g➔i➔t➔s➔
➔g➔r➔e➔p➔ ➔-➔E➔ ➔"➔e➔r➔r➔o➔r➔|➔f➔a➔i➔l➔"➔ ➔f➔i➔l➔e➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔n➔e➔s➔ ➔w➔i➔t➔h➔ ➔e➔r➔r➔o➔r➔ ➔O➔R➔ ➔f➔a➔i➔l➔
➔g➔r➔e➔p➔ ➔"➔\➔.➔"➔ ➔f➔i➔l➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔t➔e➔r➔a➔l➔ ➔d➔o➔t➔
➔a➔w➔k➔ ➔—➔ ➔P➔a➔t➔t➔e➔r➔n➔ ➔S➔c➔a➔n➔n➔i➔n➔g➔ ➔a➔n➔d➔ ➔P➔r➔o➔c➔e➔s➔s➔i➔n➔g➔
➔a➔w➔k➔ ➔'➔{➔p➔r➔i➔n➔t➔ ➔$➔1➔}➔'➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔r➔i➔n➔t➔ ➔f➔i➔r➔s➔t➔ ➔c➔o➔l➔u➔m➔n➔
➔a➔w➔k➔ ➔'➔{➔p➔r➔i➔n➔t➔ ➔$➔1➔,➔ ➔$➔3➔}➔'➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔r➔i➔n➔t➔ ➔c➔o➔l➔u➔m➔n➔s➔ ➔1➔ ➔a➔n➔d➔ ➔3➔
➔a➔w➔k➔ ➔-➔F➔:➔ ➔'➔{➔p➔r➔i➔n➔t➔ ➔$➔1➔}➔'➔ ➔/➔e➔t➔c➔/➔p➔a➔s➔s➔w➔d➔ ➔ ➔ ➔ ➔#➔ ➔u➔s➔e➔ ➔:➔ ➔a➔s➔ ➔d➔e➔l➔i➔m➔i➔t➔e➔r➔,➔ ➔p➔r➔i➔n➔t➔ ➔f➔i➔r➔s➔t➔ ➔f➔i➔e➔l➔d➔
➔a➔w➔k➔ ➔'➔N➔R➔=➔=➔5➔'➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔r➔i➔n➔t➔ ➔l➔i➔n➔e➔ ➔5➔
➔a➔w➔k➔ ➔'➔N➔R➔>➔=➔5➔ ➔&➔&➔ ➔N➔R➔<➔=➔1➔0➔'➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔r➔i➔n➔t➔ ➔l➔i➔n➔e➔s➔ ➔5➔ ➔t➔o➔ ➔1➔0➔
➔a➔w➔k➔ ➔'➔/➔p➔a➔t➔t➔e➔r➔n➔/➔ ➔{➔p➔r➔i➔n➔t➔}➔'➔ ➔f➔i➔l➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔r➔i➔n➔t➔ ➔l➔i➔n➔e➔s➔ ➔m➔a➔t➔c➔h➔i➔n➔g➔ ➔p➔a➔t➔t➔e➔r➔n➔
➔a➔w➔k➔ ➔'➔{➔p➔r➔i➔n➔t➔ ➔N➔R➔,➔ ➔$➔0➔}➔'➔ ➔f➔i➔l➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔r➔i➔n➔t➔ ➔w➔i➔t➔h➔ ➔l➔i➔n➔e➔ ➔n➔u➔m➔b➔e➔r➔s➔
➔a➔w➔k➔ ➔'➔{➔s➔u➔m➔+➔=➔$➔1➔}➔ ➔E➔N➔D➔ ➔{➔p➔r➔i➔n➔t➔ ➔s➔u➔m➔}➔'➔ ➔f➔ ➔ ➔ ➔#➔ ➔s➔u➔m➔ ➔f➔i➔r➔s➔t➔ ➔c➔o➔l➔u➔m➔n➔
➔d➔f➔ ➔-➔h➔ ➔|➔ ➔a➔w➔k➔ ➔'➔{➔p➔r➔i➔n➔t➔ ➔$➔1➔,➔ ➔$➔5➔}➔'➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔r➔i➔n➔t➔ ➔d➔i➔s➔k➔ ➔n➔a➔m➔e➔ ➔a➔n➔d➔ ➔u➔s➔a➔g➔e➔ ➔%➔
➔
➔
➔
➔
➔#➔ ➔R➔e➔a➔l➔ ➔e➔x➔a➔m➔p➔l➔e➔ ➔—➔ ➔g➔e➔t➔ ➔u➔s➔e➔r➔n➔a➔m➔e➔s➔ ➔f➔r➔o➔m➔ ➔/➔e➔t➔c➔/➔p➔a➔s➔s➔w➔d➔
➔a➔w➔k➔ ➔-➔F➔:➔ ➔'➔{➔p➔r➔i➔n➔t➔ ➔$➔1➔}➔'➔ ➔/➔e➔t➔c➔/➔p➔a➔s➔s➔w➔d➔
➔s➔e➔d➔ ➔—➔ ➔S➔t➔r➔e➔a➔m➔ ➔E➔d➔i➔t➔o➔r➔
➔s➔e➔d➔ ➔'➔s➔/➔o➔l➔d➔/➔n➔e➔w➔/➔'➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔p➔l➔a➔c➔e➔ ➔f➔i➔r➔s➔t➔ ➔o➔c➔c➔u➔r➔r➔e➔n➔c➔e➔ ➔p➔e➔r➔ ➔l➔i➔n➔e➔
➔s➔e➔d➔ ➔'➔s➔/➔o➔l➔d➔/➔n➔e➔w➔/➔g➔'➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔p➔l➔a➔c➔e➔ ➔A➔L➔L➔ ➔o➔c➔c➔u➔r➔r➔e➔n➔c➔e➔s➔
➔s➔e➔d➔ ➔'➔s➔/➔o➔l➔d➔/➔n➔e➔w➔/➔g➔i➔'➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔p➔l➔a➔c➔e➔ ➔a➔l➔l➔,➔ ➔c➔a➔s➔e➔ ➔i➔n➔s➔e➔n➔s➔i➔t➔i➔v➔e➔
➔s➔e➔d➔ ➔-➔i➔ ➔'➔s➔/➔o➔l➔d➔/➔n➔e➔w➔/➔g➔'➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔d➔i➔t➔ ➔f➔i➔l➔e➔ ➔I➔N➔ ➔P➔L➔A➔C➔E➔ ➔(➔m➔o➔d➔i➔f➔i➔e➔s➔ ➔a➔c➔t➔u➔a➔l➔ ➔f➔i➔l➔e➔)➔
➔s➔e➔d➔ ➔-➔i➔.➔b➔a➔k➔ ➔'➔s➔/➔o➔l➔d➔/➔n➔e➔w➔/➔g➔'➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔#➔ ➔i➔n➔ ➔p➔l➔a➔c➔e➔ ➔w➔i➔t➔h➔ ➔b➔a➔c➔k➔u➔p➔ ➔(➔.➔b➔a➔k➔)➔
➔s➔e➔d➔ ➔'➔5➔d➔'➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔l➔i➔n➔e➔ ➔5➔
➔s➔e➔d➔ ➔'➔/➔p➔a➔t➔t➔e➔r➔n➔/➔d➔'➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔l➔i➔n➔e➔s➔ ➔m➔a➔t➔c➔h➔i➔n➔g➔ ➔p➔a➔t➔t➔e➔r➔n➔
➔s➔e➔d➔ ➔-➔n➔ ➔'➔5➔,➔1➔0➔p➔'➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔r➔i➔n➔t➔ ➔l➔i➔n➔e➔s➔ ➔5➔ ➔t➔o➔ ➔1➔0➔ ➔o➔n➔l➔y➔
➔s➔e➔d➔ ➔'➔5➔i➔\➔n➔e➔w➔ ➔l➔i➔n➔e➔'➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔i➔n➔s➔e➔r➔t➔ ➔l➔i➔n➔e➔ ➔b➔e➔f➔o➔r➔e➔ ➔l➔i➔n➔e➔ ➔5➔
➔s➔e➔d➔ ➔'➔5➔a➔\➔n➔e➔w➔ ➔l➔i➔n➔e➔'➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔p➔p➔e➔n➔d➔ ➔l➔i➔n➔e➔ ➔a➔f➔t➔e➔r➔ ➔l➔i➔n➔e➔ ➔5➔
➔s➔e➔d➔ ➔'➔s➔/➔^➔/➔p➔r➔e➔f➔i➔x➔/➔'➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔d➔d➔ ➔p➔r➔e➔f➔i➔x➔ ➔t➔o➔ ➔e➔v➔e➔r➔y➔ ➔l➔i➔n➔e➔
➔s➔e➔d➔ ➔'➔s➔/➔$➔/➔ ➔s➔u➔f➔f➔i➔x➔/➔'➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔d➔d➔ ➔s➔u➔f➔f➔i➔x➔ ➔t➔o➔ ➔e➔v➔e➔r➔y➔ ➔l➔i➔n➔e➔
➔#➔ ➔R➔e➔a➔l➔ ➔D➔e➔v➔O➔p➔s➔ ➔e➔x➔a➔m➔p➔l➔e➔ ➔—➔ ➔u➔p➔d➔a➔t➔e➔ ➔c➔o➔n➔f➔i➔g➔ ➔f➔i➔l➔e➔
➔s➔e➔d➔ ➔-➔i➔ ➔'➔s➔/➔p➔o➔r➔t➔=➔8➔0➔8➔0➔/➔p➔o➔r➔t➔=➔8➔0➔/➔'➔ ➔/➔e➔t➔c➔/➔a➔p➔p➔.➔c➔o➔n➔f➔
➔c➔u➔t➔ ➔—➔ ➔C➔u➔t➔ ➔C➔o➔l➔u➔m➔n➔s➔ ➔f➔r➔o➔m➔ ➔T➔e➔x➔t➔
➔c➔u➔t➔ ➔-➔d➔:➔ ➔-➔f➔1➔ ➔/➔e➔t➔c➔/➔p➔a➔s➔s➔w➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔u➔t➔ ➔f➔i➔e➔l➔d➔ ➔1➔ ➔u➔s➔i➔n➔g➔ ➔:➔ ➔a➔s➔ ➔d➔e➔l➔i➔m➔i➔t➔e➔r➔
➔c➔u➔t➔ ➔-➔d➔,➔ ➔-➔f➔2➔,➔4➔ ➔d➔a➔t➔a➔.➔c➔s➔v➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔u➔t➔ ➔f➔i➔e➔l➔d➔s➔ ➔2➔ ➔a➔n➔d➔ ➔4➔ ➔f➔r➔o➔m➔ ➔C➔S➔V➔
➔c➔u➔t➔ ➔-➔c➔1➔-➔1➔0➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔u➔t➔ ➔f➔i➔r➔s➔t➔ ➔1➔0➔ ➔c➔h➔a➔r➔a➔c➔t➔e➔r➔s➔
➔c➔u➔t➔ ➔-➔d➔'➔ ➔'➔ ➔-➔f➔1➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔u➔t➔ ➔f➔i➔r➔s➔t➔ ➔w➔o➔r➔d➔
➔s➔o➔r➔t➔ ➔—➔ ➔S➔o➔r➔t➔ ➔L➔i➔n➔e➔s➔
➔s➔o➔r➔t➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔l➔p➔h➔a➔b➔e➔t➔i➔c➔a➔l➔ ➔s➔o➔r➔t➔
➔s➔o➔r➔t➔ ➔-➔r➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔v➔e➔r➔s➔e➔ ➔s➔o➔r➔t➔
➔s➔o➔r➔t➔ ➔-➔n➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔n➔u➔m➔e➔r➔i➔c➔a➔l➔ ➔s➔o➔r➔t➔
➔s➔o➔r➔t➔ ➔-➔u➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔o➔r➔t➔ ➔a➔n➔d➔ ➔r➔e➔m➔o➔v➔e➔ ➔d➔u➔p➔l➔i➔c➔a➔t➔e➔s➔
➔s➔o➔r➔t➔ ➔-➔k➔2➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔o➔r➔t➔ ➔b➔y➔ ➔s➔e➔c➔o➔n➔d➔ ➔c➔o➔l➔u➔m➔n➔
➔s➔o➔r➔t➔ ➔-➔t➔:➔ ➔-➔k➔3➔ ➔-➔n➔ ➔/➔e➔t➔c➔/➔p➔a➔s➔s➔w➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔o➔r➔t➔ ➔p➔a➔s➔s➔w➔d➔ ➔b➔y➔ ➔U➔I➔D➔ ➔(➔f➔i➔e➔l➔d➔ ➔3➔,➔ ➔n➔u➔m➔e➔r➔i➔c➔)➔
➔u➔n➔i➔q➔ ➔—➔ ➔R➔e➔m➔o➔v➔e➔ ➔D➔u➔p➔l➔i➔c➔a➔t➔e➔s➔
➔
➔
➔
➔
➔u➔n➔i➔q➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔c➔o➔n➔s➔e➔c➔u➔t➔i➔v➔e➔ ➔d➔u➔p➔l➔i➔c➔a➔t➔e➔s➔
➔u➔n➔i➔q➔ ➔-➔c➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔u➔n➔t➔ ➔o➔c➔c➔u➔r➔r➔e➔n➔c➔e➔s➔
➔u➔n➔i➔q➔ ➔-➔d➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔o➔n➔l➔y➔ ➔d➔u➔p➔l➔i➔c➔a➔t➔e➔s➔
➔s➔o➔r➔t➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔|➔ ➔u➔n➔i➔q➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔o➔r➔t➔ ➔f➔i➔r➔s➔t➔,➔ ➔t➔h➔e➔n➔ ➔r➔e➔m➔o➔v➔e➔ ➔a➔l➔l➔ ➔d➔u➔p➔l➔i➔c➔a➔t➔e➔s➔
➔s➔o➔r➔t➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔|➔ ➔u➔n➔i➔q➔ ➔-➔c➔ ➔|➔ ➔s➔o➔r➔t➔ ➔-➔r➔n➔ ➔ ➔#➔ ➔c➔o➔u➔n➔t➔ ➔a➔n➔d➔ ➔s➔o➔r➔t➔ ➔b➔y➔ ➔f➔r➔e➔q➔u➔e➔n➔c➔y➔
➔t➔r➔ ➔—➔ ➔T➔r➔a➔n➔s➔l➔a➔t➔e➔ ➔C➔h➔a➔r➔a➔c➔t➔e➔r➔s➔
➔t➔r➔ ➔'➔a➔-➔z➔'➔ ➔'➔A➔-➔Z➔'➔ ➔<➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔o➔w➔e➔r➔c➔a➔s➔e➔ ➔t➔o➔ ➔u➔p➔p➔e➔r➔c➔a➔s➔e➔
➔t➔r➔ ➔-➔d➔ ➔'➔\➔n➔'➔ ➔<➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔n➔e➔w➔l➔i➔n➔e➔s➔
➔t➔r➔ ➔-➔s➔ ➔'➔ ➔'➔ ➔<➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔q➔u➔e➔e➔z➔e➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔s➔p➔a➔c➔e➔s➔ ➔i➔n➔t➔o➔ ➔o➔n➔e➔
➔e➔c➔h➔o➔ ➔"➔h➔e➔l➔l➔o➔"➔ ➔|➔ ➔t➔r➔ ➔'➔a➔-➔z➔'➔ ➔'➔A➔-➔Z➔'➔ ➔ ➔ ➔ ➔ ➔#➔ ➔H➔E➔L➔L➔O➔
➔w➔c➔ ➔—➔ ➔W➔o➔r➔d➔ ➔C➔o➔u➔n➔t➔
➔w➔c➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔n➔e➔s➔,➔ ➔w➔o➔r➔d➔s➔,➔ ➔c➔h➔a➔r➔a➔c➔t➔e➔r➔s➔
➔w➔c➔ ➔-➔l➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔u➔n➔t➔ ➔l➔i➔n➔e➔s➔ ➔o➔n➔l➔y➔
➔w➔c➔ ➔-➔w➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔u➔n➔t➔ ➔w➔o➔r➔d➔s➔ ➔o➔n➔l➔y➔
➔w➔c➔ ➔-➔c➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔u➔n➔t➔ ➔b➔y➔t➔e➔s➔
➔l➔s➔ ➔|➔ ➔w➔c➔ ➔-➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔u➔n➔t➔ ➔f➔i➔l➔e➔s➔ ➔i➔n➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔1➔7➔.➔ ➔F➔i➔n➔d➔ ➔a➔n➔d➔ ➔L➔o➔c➔a➔t➔e➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔
➔f➔i➔n➔d➔ ➔—➔ ➔S➔e➔a➔r➔c➔h➔ ➔F➔i➔l➔e➔s➔ ➔i➔n➔ ➔R➔e➔a➔l➔ ➔T➔i➔m➔e➔
➔#➔ ➔B➔a➔s➔i➔c➔ ➔f➔i➔n➔d➔
➔f➔i➔n➔d➔ ➔/➔p➔a➔t➔h➔ ➔-➔n➔a➔m➔e➔ ➔"➔f➔i➔l➔e➔n➔a➔m➔e➔"➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔n➔d➔ ➔b➔y➔ ➔e➔x➔a➔c➔t➔ ➔n➔a➔m➔e➔
➔f➔i➔n➔d➔ ➔/➔p➔a➔t➔h➔ ➔-➔n➔a➔m➔e➔ ➔"➔*➔.➔l➔o➔g➔"➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔n➔d➔ ➔b➔y➔ ➔p➔a➔t➔t➔e➔r➔n➔
➔f➔i➔n➔d➔ ➔/➔p➔a➔t➔h➔ ➔-➔i➔n➔a➔m➔e➔ ➔"➔*➔.➔L➔o➔g➔"➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔a➔s➔e➔ ➔i➔n➔s➔e➔n➔s➔i➔t➔i➔v➔e➔ ➔n➔a➔m➔e➔
➔f➔i➔n➔d➔ ➔.➔ ➔-➔n➔a➔m➔e➔ ➔"➔*➔.➔t➔x➔t➔"➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔n➔d➔ ➔i➔n➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔#➔ ➔F➔i➔n➔d➔ ➔b➔y➔ ➔t➔y➔p➔e➔
➔f➔i➔n➔d➔ ➔/➔p➔a➔t➔h➔ ➔-➔t➔y➔p➔e➔ ➔f➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔l➔e➔s➔ ➔o➔n➔l➔y➔
➔f➔i➔n➔d➔ ➔/➔p➔a➔t➔h➔ ➔-➔t➔y➔p➔e➔ ➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔i➔e➔s➔ ➔o➔n➔l➔y➔
➔f➔i➔n➔d➔ ➔/➔p➔a➔t➔h➔ ➔-➔t➔y➔p➔e➔ ➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔y➔m➔b➔o➔l➔i➔c➔ ➔l➔i➔n➔k➔s➔ ➔o➔n➔l➔y➔
➔#➔ ➔F➔i➔n➔d➔ ➔b➔y➔ ➔s➔i➔z➔e➔
➔f➔i➔n➔d➔ ➔/➔ ➔-➔s➔i➔z➔e➔ ➔+➔1➔0➔0➔M➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔l➔e➔s➔ ➔l➔a➔r➔g➔e➔r➔ ➔t➔h➔a➔n➔ ➔1➔0➔0➔M➔B➔
➔
➔
➔
➔
➔➔ ➔➔
➔➔ ➔➔
➔f➔i➔n➔d➔ ➔/➔ ➔-➔s➔i➔z➔e➔ ➔-➔1➔k➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔l➔e➔s➔ ➔s➔m➔a➔l➔l➔e➔r➔ ➔t➔h➔a➔n➔ ➔1➔K➔B➔
➔f➔i➔n➔d➔ ➔/➔ ➔-➔s➔i➔z➔e➔ ➔5➔0➔M➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔l➔e➔s➔ ➔e➔x➔a➔c➔t➔l➔y➔ ➔5➔0➔M➔B➔
➔#➔ ➔F➔i➔n➔d➔ ➔b➔y➔ ➔t➔i➔m➔e➔
➔f➔i➔n➔d➔ ➔/➔ ➔-➔m➔t➔i➔m➔e➔ ➔-➔7➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔m➔o➔d➔i➔f➔i➔e➔d➔ ➔i➔n➔ ➔l➔a➔s➔t➔ ➔7➔ ➔d➔a➔y➔s➔
➔f➔i➔n➔d➔ ➔/➔ ➔-➔m➔t➔i➔m➔e➔ ➔+➔3➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔m➔o➔d➔i➔f➔i➔e➔d➔ ➔m➔o➔r➔e➔ ➔t➔h➔a➔n➔ ➔3➔0➔ ➔d➔a➔y➔s➔ ➔a➔g➔o➔
➔f➔i➔n➔d➔ ➔/➔ ➔-➔a➔t➔i➔m➔e➔ ➔-➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔c➔c➔e➔s➔s➔e➔d➔ ➔i➔n➔ ➔l➔a➔s➔t➔ ➔2➔4➔ ➔h➔o➔u➔r➔s➔
➔f➔i➔n➔d➔ ➔/➔ ➔-➔n➔e➔w➔e➔r➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔l➔e➔s➔ ➔n➔e➔w➔e➔r➔ ➔t➔h➔a➔n➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔
➔#➔ ➔F➔i➔n➔d➔ ➔b➔y➔ ➔p➔e➔r➔m➔i➔s➔s➔i➔o➔n➔s➔
➔f➔i➔n➔d➔ ➔/➔ ➔-➔p➔e➔r➔m➔ ➔7➔7➔7➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔l➔e➔s➔ ➔w➔i➔t➔h➔ ➔e➔x➔a➔c➔t➔l➔y➔ ➔7➔7➔7➔
➔f➔i➔n➔d➔ ➔/➔ ➔-➔p➔e➔r➔m➔ ➔/➔u➔+➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔l➔e➔s➔ ➔w➔i➔t➔h➔ ➔S➔U➔I➔D➔ ➔s➔e➔t➔
➔#➔ ➔F➔i➔n➔d➔ ➔b➔y➔ ➔o➔w➔n➔e➔r➔
➔f➔i➔n➔d➔ ➔/➔h➔o➔m➔e➔ ➔-➔u➔s➔e➔r➔ ➔a➔k➔h➔i➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔l➔e➔s➔ ➔o➔w➔n➔e➔d➔ ➔b➔y➔ ➔a➔k➔h➔i➔l➔
➔f➔i➔n➔d➔ ➔/➔h➔o➔m➔e➔ ➔-➔g➔r➔o➔u➔p➔ ➔d➔e➔v➔o➔p➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔l➔e➔s➔ ➔o➔w➔n➔e➔d➔ ➔b➔y➔ ➔d➔e➔v➔o➔p➔s➔ ➔g➔r➔o➔u➔p➔
➔#➔ ➔F➔i➔n➔d➔ ➔a➔n➔d➔ ➔e➔x➔e➔c➔u➔t➔e➔ ➔a➔c➔t➔i➔o➔n➔
➔f➔i➔n➔d➔ ➔/➔t➔m➔p➔ ➔-➔n➔a➔m➔e➔ ➔"➔*➔.➔t➔m➔p➔"➔ ➔-➔d➔e➔l➔e➔t➔e➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔n➔d➔ ➔a➔n➔d➔ ➔d➔e➔l➔e➔t➔e➔
➔f➔i➔n➔d➔ ➔/➔v➔a➔r➔/➔l➔o➔g➔ ➔-➔n➔a➔m➔e➔ ➔"➔*➔.➔l➔o➔g➔"➔ ➔-➔e➔x➔e➔c➔ ➔l➔s➔ ➔-➔l➔h➔ ➔{➔}➔ ➔\➔;➔ ➔ ➔ ➔#➔ ➔f➔i➔n➔d➔ ➔a➔n➔d➔ ➔r➔u➔n➔ ➔l➔s➔
➔f➔i➔n➔d➔ ➔.➔ ➔-➔n➔a➔m➔e➔ ➔"➔*➔.➔t➔x➔t➔"➔ ➔-➔e➔x➔e➔c➔ ➔g➔r➔e➔p➔ ➔"➔e➔r➔r➔o➔r➔"➔ ➔{➔}➔ ➔\➔;➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔n➔d➔ ➔t➔x➔t➔ ➔f➔i➔l➔e➔s➔ ➔a➔n➔d➔ ➔g➔r➔e➔p➔ ➔i➔n➔s➔i➔d➔e➔ ➔t➔h➔e➔m➔
➔#➔ ➔R➔e➔a➔l➔ ➔D➔e➔v➔O➔p➔s➔ ➔e➔x➔a➔m➔p➔l➔e➔s➔:➔
➔f➔i➔n➔d➔ ➔/➔ ➔-➔n➔a➔m➔e➔ ➔"➔n➔g➔i➔n➔x➔.➔c➔o➔n➔f➔"➔ ➔2➔>➔/➔d➔e➔v➔/➔n➔u➔l➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔n➔d➔ ➔n➔g➔i➔n➔x➔ ➔c➔o➔n➔f➔i➔g➔
➔f➔i➔n➔d➔ ➔/➔v➔a➔r➔/➔l➔o➔g➔ ➔-➔n➔a➔m➔e➔ ➔"➔*➔.➔l➔o➔g➔"➔ ➔-➔m➔t➔i➔m➔e➔ ➔+➔7➔ ➔-➔d➔e➔l➔e➔t➔e➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔l➔o➔g➔s➔ ➔o➔l➔d➔e➔r➔ ➔t➔h➔a➔n➔ ➔7➔ ➔d➔a➔y➔s➔
➔f➔i➔n➔d➔ ➔/➔ ➔-➔p➔e➔r➔m➔ ➔/➔u➔+➔s➔ ➔-➔t➔y➔p➔e➔ ➔f➔ ➔2➔>➔/➔d➔e➔v➔/➔n➔u➔l➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔n➔d➔ ➔a➔l➔l➔ ➔S➔U➔I➔D➔ ➔f➔i➔l➔e➔s➔ ➔(➔s➔e➔c➔u➔r➔i➔t➔y➔ ➔c➔h➔e➔c➔k➔)➔
➔l➔o➔c➔a➔t➔e➔ ➔—➔ ➔F➔a➔s➔t➔ ➔F➔i➔l➔e➔ ➔S➔e➔a➔r➔c➔h➔ ➔(➔u➔s➔e➔s➔ ➔d➔a➔t➔a➔b➔a➔s➔e➔)➔
➔l➔o➔c➔a➔t➔e➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔a➔s➔t➔ ➔s➔e➔a➔r➔c➔h➔ ➔u➔s➔i➔n➔g➔ ➔p➔r➔e➔-➔b➔u➔i➔l➔t➔ ➔d➔a➔t➔a➔b➔a➔s➔e➔
➔l➔o➔c➔a➔t➔e➔ ➔"➔*➔.➔c➔o➔n➔f➔"➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔a➔r➔c➔h➔ ➔b➔y➔ ➔p➔a➔t➔t➔e➔r➔n➔
➔l➔o➔c➔a➔t➔e➔ ➔-➔i➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔a➔s➔e➔ ➔i➔n➔s➔e➔n➔s➔i➔t➔i➔v➔e➔
➔l➔o➔c➔a➔t➔e➔ ➔-➔c➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔u➔n➔t➔ ➔r➔e➔s➔u➔l➔t➔s➔ ➔o➔n➔l➔y➔
➔l➔o➔c➔a➔t➔e➔ ➔-➔n➔ ➔1➔0➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔o➔n➔l➔y➔ ➔1➔0➔ ➔r➔e➔s➔u➔l➔t➔s➔
➔u➔p➔d➔a➔t➔e➔d➔b➔ ➔—➔ ➔U➔p➔d➔a➔t➔e➔ ➔l➔o➔c➔a➔t➔e➔ ➔D➔a➔t➔a➔b➔a➔s➔e➔
➔u➔p➔d➔a➔t➔e➔d➔b➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔u➔p➔d➔a➔t➔e➔ ➔t➔h➔e➔ ➔l➔o➔c➔a➔t➔e➔ ➔d➔a➔t➔a➔b➔a➔s➔e➔ ➔(➔r➔u➔n➔ ➔a➔s➔ ➔r➔o➔o➔t➔)➔
➔#➔ ➔l➔o➔c➔a➔t➔e➔ ➔u➔s➔e➔s➔ ➔a➔ ➔d➔a➔t➔a➔b➔a➔s➔e➔ ➔b➔u➔i➔l➔t➔ ➔b➔y➔ ➔u➔p➔d➔a➔t➔e➔d➔b➔ ➔—➔ ➔r➔u➔n➔ ➔t➔h➔i➔s➔ ➔b➔e➔f➔o➔r➔e➔ ➔l➔o➔c➔a➔t➔e➔ ➔i➔f➔ ➔f➔i➔l➔e➔s➔ ➔a➔r➔e➔ ➔n➔e➔w➔
➔#➔ ➔u➔p➔d➔a➔t➔e➔d➔b➔ ➔r➔u➔n➔s➔ ➔a➔u➔t➔o➔m➔a➔t➔i➔c➔a➔l➔l➔y➔ ➔a➔s➔ ➔a➔ ➔c➔r➔o➔n➔ ➔j➔o➔b➔ ➔d➔a➔i➔l➔y➔
➔
➔
➔
➔
➔1➔8➔.➔ ➔P➔i➔p➔i➔n➔g➔ ➔a➔n➔d➔ ➔R➔e➔d➔i➔r➔e➔c➔t➔i➔o➔n➔
➔P➔i➔p➔i➔n➔g➔ ➔—➔ ➔|➔ ➔(➔p➔a➔s➔s➔ ➔o➔u➔t➔p➔u➔t➔ ➔o➔f➔ ➔o➔n➔e➔ ➔c➔o➔m➔m➔a➔n➔d➔ ➔t➔o➔ ➔a➔n➔o➔t➔h➔e➔r➔)➔
➔#➔ ➔P➔i➔p➔e➔ ➔t➔a➔k➔e➔s➔ ➔s➔t➔d➔o➔u➔t➔ ➔o➔f➔ ➔l➔e➔f➔t➔ ➔c➔o➔m➔m➔a➔n➔d➔ ➔a➔n➔d➔ ➔f➔e➔e➔d➔s➔ ➔i➔t➔ ➔a➔s➔ ➔s➔t➔d➔i➔n➔ ➔t➔o➔ ➔r➔i➔g➔h➔t➔ ➔c➔o➔m➔m➔a➔n➔d➔
➔l➔s➔ ➔-➔l➔ ➔|➔ ➔g➔r➔e➔p➔ ➔"➔.➔t➔x➔t➔"➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔f➔i➔l➔e➔s➔,➔ ➔f➔i➔l➔t➔e➔r➔ ➔f➔o➔r➔ ➔.➔t➔x➔t➔
➔p➔s➔ ➔a➔u➔x➔ ➔|➔ ➔g➔r➔e➔p➔ ➔n➔g➔i➔n➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔n➔d➔ ➔n➔g➔i➔n➔x➔ ➔p➔r➔o➔c➔e➔s➔s➔e➔s➔
➔c➔a➔t➔ ➔/➔e➔t➔c➔/➔p➔a➔s➔s➔w➔d➔ ➔|➔ ➔g➔r➔e➔p➔ ➔"➔/➔b➔i➔n➔/➔b➔a➔s➔h➔"➔ ➔ ➔ ➔#➔ ➔u➔s➔e➔r➔s➔ ➔w➔i➔t➔h➔ ➔b➔a➔s➔h➔ ➔s➔h➔e➔l➔l➔
➔d➔f➔ ➔-➔h➔ ➔|➔ ➔g➔r➔e➔p➔ ➔"➔/➔d➔e➔v➔/➔x➔v➔d➔a➔"➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔n➔d➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔d➔i➔s➔k➔
➔c➔a➔t➔ ➔a➔c➔c➔e➔s➔s➔.➔l➔o➔g➔ ➔|➔ ➔g➔r➔e➔p➔ ➔"➔E➔R➔R➔O➔R➔"➔ ➔|➔ ➔w➔c➔ ➔-➔l➔ ➔ ➔ ➔#➔ ➔c➔o➔u➔n➔t➔ ➔e➔r➔r➔o➔r➔s➔ ➔i➔n➔ ➔l➔o➔g➔
➔c➔a➔t➔ ➔/➔e➔t➔c➔/➔p➔a➔s➔s➔w➔d➔ ➔|➔ ➔c➔u➔t➔ ➔-➔d➔:➔ ➔-➔f➔1➔ ➔|➔ ➔s➔o➔r➔t➔ ➔ ➔ ➔ ➔#➔ ➔s➔o➔r➔t➔e➔d➔ ➔l➔i➔s➔t➔ ➔o➔f➔ ➔u➔s➔e➔r➔n➔a➔m➔e➔s➔
➔p➔s➔ ➔a➔u➔x➔ ➔|➔ ➔s➔o➔r➔t➔ ➔-➔k➔3➔ ➔-➔r➔n➔ ➔|➔ ➔h➔e➔a➔d➔ ➔-➔5➔ ➔ ➔ ➔ ➔ ➔#➔ ➔t➔o➔p➔ ➔5➔ ➔C➔P➔U➔-➔c➔o➔n➔s➔u➔m➔i➔n➔g➔ ➔p➔r➔o➔c➔e➔s➔s➔e➔s➔
➔R➔e➔d➔i➔r➔e➔c➔t➔i➔o➔n➔
➔#➔ ➔O➔u➔t➔p➔u➔t➔ ➔r➔e➔d➔i➔r➔e➔c➔t➔i➔o➔n➔
➔c➔o➔m➔m➔a➔n➔d➔ ➔>➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔d➔i➔r➔e➔c➔t➔ ➔s➔t➔d➔o➔u➔t➔ ➔t➔o➔ ➔f➔i➔l➔e➔ ➔(➔O➔V➔E➔R➔W➔R➔I➔T➔E➔S➔)➔
➔c➔o➔m➔m➔a➔n➔d➔ ➔>➔>➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔d➔i➔r➔e➔c➔t➔ ➔s➔t➔d➔o➔u➔t➔ ➔t➔o➔ ➔f➔i➔l➔e➔ ➔(➔A➔P➔P➔E➔N➔D➔S➔)➔
➔c➔o➔m➔m➔a➔n➔d➔ ➔2➔>➔ ➔e➔r➔r➔o➔r➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔d➔i➔r➔e➔c➔t➔ ➔s➔t➔d➔e➔r➔r➔ ➔t➔o➔ ➔f➔i➔l➔e➔
➔c➔o➔m➔m➔a➔n➔d➔ ➔2➔>➔>➔ ➔e➔r➔r➔o➔r➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔p➔p➔e➔n➔d➔ ➔s➔t➔d➔e➔r➔r➔ ➔t➔o➔ ➔f➔i➔l➔e➔
➔c➔o➔m➔m➔a➔n➔d➔ ➔>➔ ➔o➔u➔t➔p➔u➔t➔.➔t➔x➔t➔ ➔2➔>➔&➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔d➔i➔r➔e➔c➔t➔ ➔b➔o➔t➔h➔ ➔s➔t➔d➔o➔u➔t➔ ➔a➔n➔d➔ ➔s➔t➔d➔e➔r➔r➔ ➔t➔o➔ ➔f➔i➔l➔e➔
➔c➔o➔m➔m➔a➔n➔d➔ ➔&➔>➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔d➔i➔r➔e➔c➔t➔ ➔b➔o➔t➔h➔ ➔(➔s➔h➔o➔r➔t➔h➔a➔n➔d➔)➔
➔c➔o➔m➔m➔a➔n➔d➔ ➔>➔ ➔/➔d➔e➔v➔/➔n➔u➔l➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔i➔s➔c➔a➔r➔d➔ ➔o➔u➔t➔p➔u➔t➔ ➔(➔s➔e➔n➔d➔ ➔t➔o➔ ➔n➔u➔l➔l➔)➔
➔c➔o➔m➔m➔a➔n➔d➔ ➔>➔ ➔/➔d➔e➔v➔/➔n➔u➔l➔l➔ ➔2➔>➔&➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔i➔s➔c➔a➔r➔d➔ ➔a➔l➔l➔ ➔o➔u➔t➔p➔u➔t➔
➔#➔ ➔I➔n➔p➔u➔t➔ ➔r➔e➔d➔i➔r➔e➔c➔t➔i➔o➔n➔
➔c➔o➔m➔m➔a➔n➔d➔ ➔<➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔u➔s➔e➔ ➔f➔i➔l➔e➔ ➔a➔s➔ ➔i➔n➔p➔u➔t➔
➔m➔y➔s➔q➔l➔ ➔-➔u➔ ➔r➔o➔o➔t➔ ➔-➔p➔ ➔d➔b➔n➔a➔m➔e➔ ➔<➔ ➔d➔u➔m➔p➔.➔s➔q➔l➔ ➔ ➔ ➔#➔ ➔i➔m➔p➔o➔r➔t➔ ➔S➔Q➔L➔ ➔d➔u➔m➔p➔
➔#➔ ➔H➔e➔r➔e➔ ➔d➔o➔c➔u➔m➔e➔n➔t➔
➔c➔a➔t➔ ➔<➔<➔ ➔E➔O➔F➔ ➔>➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔
➔T➔h➔i➔s➔ ➔i➔s➔ ➔l➔i➔n➔e➔ ➔1➔
➔T➔h➔i➔s➔ ➔i➔s➔ ➔l➔i➔n➔e➔ ➔2➔
➔E➔O➔F➔
➔#➔ ➔P➔i➔p➔e➔ ➔a➔n➔d➔ ➔r➔e➔d➔i➔r➔e➔c➔t➔i➔o➔n➔ ➔c➔o➔m➔b➔i➔n➔e➔d➔
➔g➔r➔e➔p➔ ➔"➔E➔R➔R➔O➔R➔"➔ ➔/➔v➔a➔r➔/➔l➔o➔g➔/➔a➔p➔p➔.➔l➔o➔g➔ ➔|➔ ➔t➔a➔i➔l➔ ➔-➔1➔0➔0➔ ➔>➔ ➔e➔r➔r➔o➔r➔s➔.➔t➔x➔t➔ ➔ ➔ ➔#➔ ➔s➔a➔v➔e➔ ➔l➔a➔s➔t➔ ➔1➔0➔0➔ ➔e➔r➔r➔o➔r➔s➔
➔p➔s➔ ➔a➔u➔x➔ ➔|➔ ➔g➔r➔e➔p➔ ➔n➔g➔i➔n➔x➔ ➔|➔ ➔a➔w➔k➔ ➔'➔{➔p➔r➔i➔n➔t➔ ➔$➔2➔}➔'➔ ➔|➔ ➔x➔a➔r➔g➔s➔ ➔k➔i➔l➔l➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔k➔i➔l➔l➔ ➔n➔g➔i➔n➔x➔ ➔p➔r➔o➔c➔e➔s➔s➔e➔s➔
➔1➔9➔.➔ ➔N➔e➔t➔w➔o➔r➔k➔i➔n➔g➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔
➔
➔
➔
➔
➔#➔ ➔I➔n➔t➔e➔r➔f➔a➔c➔e➔ ➔a➔n➔d➔ ➔I➔P➔ ➔i➔n➔f➔o➔
➔i➔p➔ ➔a➔d➔d➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔a➔l➔l➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔i➔n➔t➔e➔r➔f➔a➔c➔e➔s➔ ➔a➔n➔d➔ ➔I➔P➔s➔
➔i➔p➔ ➔a➔d➔d➔r➔ ➔s➔h➔o➔w➔ ➔e➔t➔h➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔i➔n➔t➔e➔r➔f➔a➔c➔e➔
➔i➔f➔c➔o➔n➔f➔i➔g➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔o➔l➔d➔e➔r➔ ➔c➔o➔m➔m➔a➔n➔d➔ ➔(➔m➔a➔y➔ ➔n➔e➔e➔d➔ ➔n➔e➔t➔-➔t➔o➔o➔l➔s➔)➔
➔i➔p➔ ➔l➔i➔n➔k➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔l➔i➔n➔k➔ ➔l➔a➔y➔e➔r➔ ➔i➔n➔f➔o➔
➔i➔p➔ ➔l➔i➔n➔k➔ ➔s➔e➔t➔ ➔e➔t➔h➔0➔ ➔u➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔b➔r➔i➔n➔g➔ ➔i➔n➔t➔e➔r➔f➔a➔c➔e➔ ➔u➔p➔
➔i➔p➔ ➔l➔i➔n➔k➔ ➔s➔e➔t➔ ➔e➔t➔h➔0➔ ➔d➔o➔w➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔b➔r➔i➔n➔g➔ ➔i➔n➔t➔e➔r➔f➔a➔c➔e➔ ➔d➔o➔w➔n➔
➔#➔ ➔R➔o➔u➔t➔i➔n➔g➔
➔i➔p➔ ➔r➔o➔u➔t➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔r➔o➔u➔t➔i➔n➔g➔ ➔t➔a➔b➔l➔e➔
➔i➔p➔ ➔r➔o➔u➔t➔e➔ ➔s➔h➔o➔w➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔a➔m➔e➔
➔r➔o➔u➔t➔e➔ ➔-➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔r➔o➔u➔t➔i➔n➔g➔ ➔t➔a➔b➔l➔e➔ ➔(➔o➔l➔d➔e➔r➔)➔
➔i➔p➔ ➔r➔o➔u➔t➔e➔ ➔a➔d➔d➔ ➔1➔9➔2➔.➔1➔6➔8➔.➔1➔.➔0➔/➔2➔4➔ ➔v➔i➔a➔ ➔1➔0➔.➔0➔.➔0➔.➔1➔ ➔ ➔ ➔#➔ ➔a➔d➔d➔ ➔s➔t➔a➔t➔i➔c➔ ➔r➔o➔u➔t➔e➔
➔i➔p➔ ➔r➔o➔u➔t➔e➔ ➔d➔e➔l➔ ➔1➔9➔2➔.➔1➔6➔8➔.➔1➔.➔0➔/➔2➔4➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔r➔o➔u➔t➔e➔
➔#➔ ➔D➔N➔S➔
➔n➔s➔l➔o➔o➔k➔u➔p➔ ➔g➔o➔o➔g➔l➔e➔.➔c➔o➔m➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔D➔N➔S➔ ➔l➔o➔o➔k➔u➔p➔
➔d➔i➔g➔ ➔g➔o➔o➔g➔l➔e➔.➔c➔o➔m➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔t➔a➔i➔l➔e➔d➔ ➔D➔N➔S➔ ➔l➔o➔o➔k➔u➔p➔
➔d➔i➔g➔ ➔g➔o➔o➔g➔l➔e➔.➔c➔o➔m➔ ➔A➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔o➔o➔k➔u➔p➔ ➔A➔ ➔r➔e➔c➔o➔r➔d➔
➔d➔i➔g➔ ➔g➔o➔o➔g➔l➔e➔.➔c➔o➔m➔ ➔M➔X➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔o➔o➔k➔u➔p➔ ➔m➔a➔i➔l➔ ➔r➔e➔c➔o➔r➔d➔s➔
➔c➔a➔t➔ ➔/➔e➔t➔c➔/➔r➔e➔s➔o➔l➔v➔.➔c➔o➔n➔f➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔D➔N➔S➔ ➔s➔e➔r➔v➔e➔r➔ ➔c➔o➔n➔f➔i➔g➔
➔c➔a➔t➔ ➔/➔e➔t➔c➔/➔h➔o➔s➔t➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔o➔c➔a➔l➔ ➔h➔o➔s➔t➔n➔a➔m➔e➔ ➔r➔e➔s➔o➔l➔u➔t➔i➔o➔n➔
➔#➔ ➔C➔o➔n➔n➔e➔c➔t➔i➔v➔i➔t➔y➔
➔p➔i➔n➔g➔ ➔g➔o➔o➔g➔l➔e➔.➔c➔o➔m➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔t➔e➔s➔t➔ ➔c➔o➔n➔n➔e➔c➔t➔i➔v➔i➔t➔y➔ ➔(➔s➔e➔n➔d➔s➔ ➔I➔C➔M➔P➔)➔
➔p➔i➔n➔g➔ ➔-➔c➔ ➔4➔ ➔g➔o➔o➔g➔l➔e➔.➔c➔o➔m➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔i➔n➔g➔ ➔4➔ ➔t➔i➔m➔e➔s➔ ➔t➔h➔e➔n➔ ➔s➔t➔o➔p➔
➔p➔i➔n➔g➔ ➔-➔i➔ ➔0➔.➔5➔ ➔g➔o➔o➔g➔l➔e➔.➔c➔o➔m➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔i➔n➔g➔ ➔e➔v➔e➔r➔y➔ ➔0➔.➔5➔ ➔s➔e➔c➔o➔n➔d➔s➔
➔t➔r➔a➔c➔e➔r➔o➔u➔t➔e➔ ➔g➔o➔o➔g➔l➔e➔.➔c➔o➔m➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔t➔r➔a➔c➔e➔ ➔p➔a➔t➔h➔ ➔t➔o➔ ➔d➔e➔s➔t➔i➔n➔a➔t➔i➔o➔n➔
➔m➔t➔r➔ ➔g➔o➔o➔g➔l➔e➔.➔c➔o➔m➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔n➔t➔i➔n➔u➔o➔u➔s➔ ➔t➔r➔a➔c➔e➔r➔o➔u➔t➔e➔
➔#➔ ➔P➔o➔r➔t➔s➔ ➔a➔n➔d➔ ➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔s➔
➔n➔e➔t➔s➔t➔a➔t➔ ➔-➔t➔u➔l➔p➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔e➔n➔i➔n➔g➔ ➔p➔o➔r➔t➔s➔ ➔(➔t➔=➔t➔c➔p➔,➔ ➔u➔=➔u➔d➔p➔,➔ ➔l➔=➔l➔i➔s➔t➔e➔n➔i➔n➔g➔,➔ ➔p➔=➔p➔
➔s➔s➔ ➔-➔t➔u➔l➔p➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔a➔m➔e➔ ➔b➔u➔t➔ ➔f➔a➔s➔t➔e➔r➔ ➔(➔m➔o➔d➔e➔r➔n➔ ➔r➔e➔p➔l➔a➔c➔e➔m➔e➔n➔t➔ ➔f➔o➔r➔ ➔n➔e➔t➔s➔t➔a➔t➔
➔s➔s➔ ➔-➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔o➔c➔k➔e➔t➔ ➔s➔t➔a➔t➔i➔s➔t➔i➔c➔s➔ ➔s➔u➔m➔m➔a➔r➔y➔
➔l➔s➔o➔f➔ ➔-➔i➔ ➔:➔8➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔w➔h➔a➔t➔ ➔p➔r➔o➔c➔e➔s➔s➔ ➔i➔s➔ ➔u➔s➔i➔n➔g➔ ➔p➔o➔r➔t➔ ➔8➔0➔
➔l➔s➔o➔f➔ ➔-➔i➔ ➔:➔8➔0➔8➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔e➔c➔k➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔p➔o➔r➔t➔
➔n➔e➔t➔s➔t➔a➔t➔ ➔-➔a➔n➔ ➔|➔ ➔g➔r➔e➔p➔ ➔E➔S➔T➔A➔B➔L➔I➔S➔H➔E➔D➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔c➔t➔i➔v➔e➔ ➔c➔o➔n➔n➔e➔c➔t➔i➔o➔n➔s➔
➔#➔ ➔H➔T➔T➔P➔ ➔R➔e➔q➔u➔e➔s➔t➔s➔
➔c➔u➔r➔l➔ ➔h➔t➔t➔p➔:➔/➔/➔e➔x➔a➔m➔p➔l➔e➔.➔c➔o➔m➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔b➔a➔s➔i➔c➔ ➔H➔T➔T➔P➔ ➔G➔E➔T➔
➔c➔u➔r➔l➔ ➔-➔I➔ ➔h➔t➔t➔p➔:➔/➔/➔e➔x➔a➔m➔p➔l➔e➔.➔c➔o➔m➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔h➔e➔a➔d➔e➔r➔s➔ ➔o➔n➔l➔y➔
➔c➔u➔r➔l➔ ➔-➔X➔ ➔P➔O➔S➔T➔ ➔-➔d➔ ➔'➔{➔"➔k➔e➔y➔"➔:➔"➔v➔a➔l➔"➔}➔'➔ ➔-➔H➔ ➔"➔C➔o➔n➔t➔e➔n➔t➔-➔T➔y➔p➔e➔:➔ ➔a➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔/➔j➔s➔o➔n➔"➔ ➔h➔t➔t➔p➔:➔/➔/➔a➔p➔i➔
➔c➔u➔r➔l➔ ➔-➔o➔ ➔f➔i➔l➔e➔.➔z➔i➔p➔ ➔h➔t➔t➔p➔:➔/➔/➔e➔x➔a➔m➔p➔l➔e➔.➔c➔o➔m➔/➔f➔i➔l➔e➔.➔z➔i➔p➔ ➔ ➔ ➔#➔ ➔d➔o➔w➔n➔l➔o➔a➔d➔ ➔f➔i➔l➔e➔
➔c➔u➔r➔l➔ ➔-➔L➔ ➔h➔t➔t➔p➔:➔/➔/➔e➔x➔a➔m➔p➔l➔e➔.➔c➔o➔m➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔l➔l➔o➔w➔ ➔r➔e➔d➔i➔r➔e➔c➔t➔s➔
➔c➔u➔r➔l➔ ➔-➔u➔ ➔u➔s➔e➔r➔n➔a➔m➔e➔:➔p➔a➔s➔s➔w➔o➔r➔d➔ ➔h➔t➔t➔p➔:➔/➔/➔a➔p➔i➔ ➔#➔ ➔b➔a➔s➔i➔c➔ ➔a➔u➔t➔h➔
➔w➔g➔e➔t➔ ➔h➔t➔t➔p➔:➔/➔/➔e➔x➔a➔m➔p➔l➔e➔.➔c➔o➔m➔/➔f➔i➔l➔e➔.➔z➔i➔p➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔o➔w➔n➔l➔o➔a➔d➔ ➔f➔i➔l➔e➔
➔w➔g➔e➔t➔ ➔-➔r➔ ➔h➔t➔t➔p➔:➔/➔/➔e➔x➔a➔m➔p➔l➔e➔.➔c➔o➔m➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔c➔u➔r➔s➔i➔v➔e➔ ➔d➔o➔w➔n➔l➔o➔a➔d➔
➔
➔
➔
➔
➔#➔ ➔F➔i➔r➔e➔w➔a➔l➔l➔ ➔—➔ ➔U➔F➔W➔ ➔(➔U➔b➔u➔n➔t➔u➔)➔
➔u➔f➔w➔ ➔s➔t➔a➔t➔u➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔h➔e➔c➔k➔ ➔f➔i➔r➔e➔w➔a➔l➔l➔ ➔s➔t➔a➔t➔u➔s➔
➔u➔f➔w➔ ➔e➔n➔a➔b➔l➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔n➔a➔b➔l➔e➔ ➔f➔i➔r➔e➔w➔a➔l➔l➔
➔u➔f➔w➔ ➔d➔i➔s➔a➔b➔l➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔i➔s➔a➔b➔l➔e➔ ➔f➔i➔r➔e➔w➔a➔l➔l➔
➔u➔f➔w➔ ➔a➔l➔l➔o➔w➔ ➔2➔2➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔l➔l➔o➔w➔ ➔S➔S➔H➔
➔u➔f➔w➔ ➔a➔l➔l➔o➔w➔ ➔8➔0➔/➔t➔c➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔l➔l➔o➔w➔ ➔H➔T➔T➔P➔
➔u➔f➔w➔ ➔a➔l➔l➔o➔w➔ ➔4➔4➔3➔/➔t➔c➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔l➔l➔o➔w➔ ➔H➔T➔T➔P➔S➔
➔u➔f➔w➔ ➔d➔e➔n➔y➔ ➔8➔0➔8➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔n➔y➔ ➔p➔o➔r➔t➔ ➔8➔0➔8➔0➔
➔u➔f➔w➔ ➔d➔e➔l➔e➔t➔e➔ ➔a➔l➔l➔o➔w➔ ➔8➔0➔8➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔m➔o➔v➔e➔ ➔r➔u➔l➔e➔
➔u➔f➔w➔ ➔a➔l➔l➔o➔w➔ ➔f➔r➔o➔m➔ ➔1➔9➔2➔.➔1➔6➔8➔.➔1➔.➔0➔/➔2➔4➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔l➔l➔o➔w➔ ➔f➔r➔o➔m➔ ➔s➔u➔b➔n➔e➔t➔
➔#➔ ➔F➔i➔r➔e➔w➔a➔l➔l➔ ➔—➔ ➔i➔p➔t➔a➔b➔l➔e➔s➔ ➔(➔l➔o➔w➔e➔r➔ ➔l➔e➔v➔e➔l➔)➔
➔i➔p➔t➔a➔b➔l➔e➔s➔ ➔-➔L➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔i➔s➔t➔ ➔a➔l➔l➔ ➔r➔u➔l➔e➔s➔
➔i➔p➔t➔a➔b➔l➔e➔s➔ ➔-➔A➔ ➔I➔N➔P➔U➔T➔ ➔-➔p➔ ➔t➔c➔p➔ ➔-➔-➔d➔p➔o➔r➔t➔ ➔8➔0➔ ➔-➔j➔ ➔A➔C➔C➔E➔P➔T➔ ➔ ➔ ➔ ➔#➔ ➔a➔l➔l➔o➔w➔ ➔p➔o➔r➔t➔ ➔8➔0➔ ➔i➔n➔
➔i➔p➔t➔a➔b➔l➔e➔s➔ ➔-➔A➔ ➔I➔N➔P➔U➔T➔ ➔-➔p➔ ➔t➔c➔p➔ ➔-➔-➔d➔p➔o➔r➔t➔ ➔2➔2➔ ➔-➔j➔ ➔A➔C➔C➔E➔P➔T➔ ➔ ➔ ➔ ➔#➔ ➔a➔l➔l➔o➔w➔ ➔S➔S➔H➔
➔i➔p➔t➔a➔b➔l➔e➔s➔ ➔-➔A➔ ➔I➔N➔P➔U➔T➔ ➔-➔j➔ ➔D➔R➔O➔P➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔r➔o➔p➔ ➔e➔v➔e➔r➔y➔t➔h➔i➔n➔g➔ ➔e➔l➔s➔e➔
➔i➔p➔t➔a➔b➔l➔e➔s➔ ➔-➔F➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔l➔u➔s➔h➔ ➔(➔d➔e➔l➔e➔t➔e➔)➔ ➔a➔l➔l➔ ➔r➔u➔l➔e➔s➔
➔#➔ ➔S➔S➔H➔
➔s➔s➔h➔ ➔a➔k➔h➔i➔l➔@➔1➔9➔2➔.➔1➔6➔8➔.➔1➔.➔1➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔S➔S➔H➔ ➔t➔o➔ ➔s➔e➔r➔v➔e➔r➔
➔s➔s➔h➔ ➔-➔i➔ ➔k➔e➔y➔.➔p➔e➔m➔ ➔e➔c➔2➔-➔u➔s➔e➔r➔@➔i➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔S➔S➔H➔ ➔w➔i➔t➔h➔ ➔k➔e➔y➔ ➔(➔A➔W➔S➔ ➔E➔C➔2➔)➔
➔s➔s➔h➔ ➔-➔p➔ ➔2➔2➔2➔2➔ ➔u➔s➔e➔r➔@➔h➔o➔s➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔S➔S➔H➔ ➔o➔n➔ ➔c➔u➔s➔t➔o➔m➔ ➔p➔o➔r➔t➔
➔s➔c➔p➔ ➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔u➔s➔e➔r➔@➔h➔o➔s➔t➔:➔/➔p➔a➔t➔h➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔p➔y➔ ➔f➔i➔l➔e➔ ➔t➔o➔ ➔r➔e➔m➔o➔t➔e➔ ➔s➔e➔r➔v➔e➔r➔
➔s➔c➔p➔ ➔u➔s➔e➔r➔@➔h➔o➔s➔t➔:➔/➔p➔a➔t➔h➔/➔f➔i➔l➔e➔.➔t➔x➔t➔ ➔.➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔p➔y➔ ➔f➔i➔l➔e➔ ➔f➔r➔o➔m➔ ➔r➔e➔m➔o➔t➔e➔ ➔s➔e➔r➔v➔e➔r➔
➔s➔c➔p➔ ➔-➔r➔ ➔f➔o➔l➔d➔e➔r➔/➔ ➔u➔s➔e➔r➔@➔h➔o➔s➔t➔:➔/➔p➔a➔t➔h➔/➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔p➔y➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔ ➔t➔o➔ ➔r➔e➔m➔o➔t➔e➔
➔s➔s➔h➔-➔k➔e➔y➔g➔e➔n➔ ➔-➔t➔ ➔r➔s➔a➔ ➔-➔b➔ ➔4➔0➔9➔6➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔g➔e➔n➔e➔r➔a➔t➔e➔ ➔S➔S➔H➔ ➔k➔e➔y➔ ➔p➔a➔i➔r➔
➔s➔s➔h➔-➔c➔o➔p➔y➔-➔i➔d➔ ➔u➔s➔e➔r➔@➔h➔o➔s➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔p➔y➔ ➔p➔u➔b➔l➔i➔c➔ ➔k➔e➔y➔ ➔t➔o➔ ➔r➔e➔m➔o➔t➔e➔ ➔s➔e➔r➔v➔e➔r➔
➔#➔ ➔N➔e➔t➔w➔o➔r➔k➔ ➔p➔e➔r➔f➔o➔r➔m➔a➔n➔c➔e➔
➔i➔p➔e➔r➔f➔3➔ ➔-➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔t➔a➔r➔t➔ ➔i➔p➔e➔r➔f➔ ➔s➔e➔r➔v➔e➔r➔
➔i➔p➔e➔r➔f➔3➔ ➔-➔c➔ ➔s➔e➔r➔v➔e➔r➔-➔i➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔t➔e➔s➔t➔ ➔b➔a➔n➔d➔w➔i➔d➔t➔h➔ ➔t➔o➔ ➔s➔e➔r➔v➔e➔r➔
➔n➔l➔o➔a➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔a➔l➔-➔t➔i➔m➔e➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔t➔r➔a➔f➔f➔i➔c➔ ➔m➔o➔n➔i➔t➔o➔r➔
➔n➔e➔t➔h➔o➔g➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔u➔s➔a➔g➔e➔ ➔p➔e➔r➔ ➔p➔r➔o➔c➔e➔s➔s➔
➔2➔0➔.➔ ➔E➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔s➔
➔#➔ ➔V➔i➔e➔w➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔
➔e➔n➔v➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔a➔l➔l➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔
➔p➔r➔i➔n➔t➔e➔n➔v➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔a➔m➔e➔
➔p➔r➔i➔n➔t➔e➔n➔v➔ ➔P➔A➔T➔H➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔
➔e➔c➔h➔o➔ ➔$➔H➔O➔M➔E➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔r➔i➔n➔t➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔ ➔v➔a➔l➔u➔e➔
➔e➔c➔h➔o➔ ➔$➔P➔A➔T➔H➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔r➔i➔n➔t➔ ➔P➔A➔T➔H➔
➔#➔ ➔S➔e➔t➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔
➔
➔
➔
➔
➔➔ ➔➔
➔e➔x➔p➔o➔r➔t➔ ➔M➔Y➔V➔A➔R➔=➔"➔h➔e➔l➔l➔o➔"➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔t➔ ➔a➔n➔d➔ ➔e➔x➔p➔o➔r➔t➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔ ➔(➔a➔v➔a➔i➔l➔a➔b➔l➔e➔ ➔t➔o➔ ➔c➔h➔i➔l➔d➔ ➔p➔r➔o➔
➔M➔Y➔V➔A➔R➔=➔"➔h➔e➔l➔l➔o➔"➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔t➔ ➔b➔u➔t➔ ➔N➔O➔T➔ ➔e➔x➔p➔o➔r➔t➔e➔d➔ ➔(➔o➔n➔l➔y➔ ➔i➔n➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔s➔h➔e➔l➔l➔)➔
➔e➔x➔p➔o➔r➔t➔ ➔P➔A➔T➔H➔=➔$➔P➔A➔T➔H➔:➔/➔n➔e➔w➔/➔p➔a➔t➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔d➔d➔ ➔t➔o➔ ➔P➔A➔T➔H➔
➔#➔ ➔P➔e➔r➔m➔a➔n➔e➔n➔t➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔ ➔—➔ ➔a➔d➔d➔ ➔t➔o➔ ➔~➔/➔.➔b➔a➔s➔h➔r➔c➔ ➔o➔r➔ ➔/➔e➔t➔c➔/➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔
➔e➔c➔h➔o➔ ➔'➔e➔x➔p➔o➔r➔t➔ ➔M➔Y➔V➔A➔R➔=➔"➔h➔e➔l➔l➔o➔"➔'➔ ➔>➔>➔ ➔~➔/➔.➔b➔a➔s➔h➔r➔c➔
➔s➔o➔u➔r➔c➔e➔ ➔~➔/➔.➔b➔a➔s➔h➔r➔c➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔l➔o➔a➔d➔ ➔b➔a➔s➔h➔r➔c➔
➔#➔ ➔C➔o➔m➔m➔o➔n➔ ➔e➔n➔v➔i➔r➔o➔n➔m➔e➔n➔t➔ ➔v➔a➔r➔i➔a➔b➔l➔e➔s➔
➔$➔H➔O➔M➔E➔ ➔ ➔ ➔ ➔#➔ ➔u➔s➔e➔r➔'➔s➔ ➔h➔o➔m➔e➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔$➔P➔A➔T➔H➔ ➔ ➔ ➔ ➔#➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔i➔e➔s➔ ➔t➔o➔ ➔s➔e➔a➔r➔c➔h➔ ➔f➔o➔r➔ ➔c➔o➔m➔m➔a➔n➔d➔s➔
➔$➔U➔S➔E➔R➔ ➔ ➔ ➔ ➔#➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔u➔s➔e➔r➔n➔a➔m➔e➔
➔$➔S➔H➔E➔L➔L➔ ➔ ➔ ➔#➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔s➔h➔e➔l➔l➔
➔$➔P➔W➔D➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔w➔o➔r➔k➔i➔n➔g➔ ➔d➔i➔r➔e➔c➔t➔o➔r➔y➔
➔$➔E➔D➔I➔T➔O➔R➔ ➔ ➔#➔ ➔d➔e➔f➔a➔u➔l➔t➔ ➔t➔e➔x➔t➔ ➔e➔d➔i➔t➔o➔r➔
➔$➔L➔A➔N➔G➔ ➔ ➔ ➔ ➔#➔ ➔s➔y➔s➔t➔e➔m➔ ➔l➔a➔n➔g➔u➔a➔g➔e➔
➔2➔1➔.➔ ➔T➔e➔x➔t➔ ➔E➔d➔i➔t➔o➔r➔s➔
➔#➔ ➔v➔i➔m➔ ➔(➔m➔o➔s➔t➔ ➔i➔m➔p➔o➔r➔t➔a➔n➔t➔ ➔f➔o➔r➔ ➔D➔e➔v➔O➔p➔s➔)➔
➔v➔i➔m➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔o➔p➔e➔n➔ ➔f➔i➔l➔e➔ ➔i➔n➔ ➔v➔i➔m➔
➔#➔ ➔v➔i➔m➔ ➔m➔o➔d➔e➔s➔:➔
➔#➔ ➔N➔o➔r➔m➔a➔l➔ ➔m➔o➔d➔e➔ ➔ ➔—➔ ➔d➔e➔f➔a➔u➔l➔t➔,➔ ➔n➔a➔v➔i➔g➔a➔t➔e➔ ➔a➔n➔d➔ ➔r➔u➔n➔ ➔c➔o➔m➔m➔a➔n➔d➔s➔
➔#➔ ➔I➔n➔s➔e➔r➔t➔ ➔m➔o➔d➔e➔ ➔ ➔—➔ ➔p➔r➔e➔s➔s➔ ➔'➔i➔'➔ ➔t➔o➔ ➔e➔n➔t➔e➔r➔,➔ ➔t➔y➔p➔e➔ ➔t➔e➔x➔t➔
➔#➔ ➔C➔o➔m➔m➔a➔n➔d➔ ➔m➔o➔d➔e➔ ➔—➔ ➔p➔r➔e➔s➔s➔ ➔'➔:➔'➔ ➔t➔o➔ ➔e➔n➔t➔e➔r➔ ➔c➔o➔m➔m➔a➔n➔d➔s➔
➔#➔ ➔E➔s➔s➔e➔n➔t➔i➔a➔l➔ ➔v➔i➔m➔ ➔c➔o➔m➔m➔a➔n➔d➔s➔:➔
➔i➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔n➔t➔e➔r➔ ➔i➔n➔s➔e➔r➔t➔ ➔m➔o➔d➔e➔
➔E➔s➔c➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔g➔o➔ ➔b➔a➔c➔k➔ ➔t➔o➔ ➔n➔o➔r➔m➔a➔l➔ ➔m➔o➔d➔e➔
➔:➔w➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔a➔v➔e➔ ➔f➔i➔l➔e➔
➔:➔q➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔q➔u➔i➔t➔ ➔(➔f➔a➔i➔l➔s➔ ➔i➔f➔ ➔u➔n➔s➔a➔v➔e➔d➔ ➔c➔h➔a➔n➔g➔e➔s➔)➔
➔:➔w➔q➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔a➔v➔e➔ ➔a➔n➔d➔ ➔q➔u➔i➔t➔
➔:➔q➔!➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔q➔u➔i➔t➔ ➔w➔i➔t➔h➔o➔u➔t➔ ➔s➔a➔v➔i➔n➔g➔ ➔(➔f➔o➔r➔c➔e➔)➔
➔:➔w➔q➔!➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔a➔v➔e➔ ➔a➔n➔d➔ ➔q➔u➔i➔t➔ ➔(➔f➔o➔r➔c➔e➔)➔
➔d➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔l➔e➔t➔e➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔l➔i➔n➔e➔
➔y➔y➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔p➔y➔ ➔(➔y➔a➔n➔k➔)➔ ➔c➔u➔r➔r➔e➔n➔t➔ ➔l➔i➔n➔e➔
➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔a➔s➔t➔e➔
➔u➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔u➔n➔d➔o➔
➔C➔t➔r➔l➔+➔r➔ ➔ ➔ ➔ ➔ ➔#➔ ➔r➔e➔d➔o➔
➔/➔p➔a➔t➔t➔e➔r➔n➔ ➔ ➔ ➔#➔ ➔s➔e➔a➔r➔c➔h➔ ➔f➔o➔r➔w➔a➔r➔d➔
➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔n➔e➔x➔t➔ ➔s➔e➔a➔r➔c➔h➔ ➔r➔e➔s➔u➔l➔t➔
➔:➔%➔s➔/➔o➔l➔d➔/➔n➔e➔w➔/➔g➔ ➔ ➔#➔ ➔r➔e➔p➔l➔a➔c➔e➔ ➔a➔l➔l➔ ➔o➔c➔c➔u➔r➔r➔e➔n➔c➔e➔s➔ ➔i➔n➔ ➔f➔i➔l➔e➔
➔g➔g➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔g➔o➔ ➔t➔o➔ ➔t➔o➔p➔ ➔o➔f➔ ➔f➔i➔l➔e➔
➔
➔
➔
➔
➔G➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔g➔o➔ ➔t➔o➔ ➔b➔o➔t➔t➔o➔m➔ ➔o➔f➔ ➔f➔i➔l➔e➔
➔:➔s➔e➔t➔ ➔n➔u➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔o➔w➔ ➔l➔i➔n➔e➔ ➔n➔u➔m➔b➔e➔r➔s➔
➔#➔ ➔n➔a➔n➔o➔ ➔(➔s➔i➔m➔p➔l➔e➔r➔ ➔e➔d➔i➔t➔o➔r➔)➔
➔n➔a➔n➔o➔ ➔f➔i➔l➔e➔n➔a➔m➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔o➔p➔e➔n➔ ➔f➔i➔l➔e➔
➔C➔t➔r➔l➔+➔O➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔a➔v➔e➔
➔C➔t➔r➔l➔+➔X➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔x➔i➔t➔
➔C➔t➔r➔l➔+➔W➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔e➔a➔r➔c➔h➔
➔C➔t➔r➔l➔+➔K➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔c➔u➔t➔ ➔l➔i➔n➔e➔
➔C➔t➔r➔l➔+➔U➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔a➔s➔t➔e➔
➔2➔2➔.➔ ➔L➔o➔g➔ ➔M➔a➔n➔a➔g➔e➔m➔e➔n➔t➔
➔#➔ ➔I➔m➔p➔o➔r➔t➔a➔n➔t➔ ➔l➔o➔g➔ ➔f➔i➔l➔e➔s➔
➔/➔v➔a➔r➔/➔l➔o➔g➔/➔s➔y➔s➔l➔o➔g➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔g➔e➔n➔e➔r➔a➔l➔ ➔s➔y➔s➔t➔e➔m➔ ➔l➔o➔g➔s➔ ➔(➔U➔b➔u➔n➔t➔u➔)➔
➔/➔v➔a➔r➔/➔l➔o➔g➔/➔m➔e➔s➔s➔a➔g➔e➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔g➔e➔n➔e➔r➔a➔l➔ ➔s➔y➔s➔t➔e➔m➔ ➔l➔o➔g➔s➔ ➔(➔R➔H➔E➔L➔)➔
➔/➔v➔a➔r➔/➔l➔o➔g➔/➔a➔u➔t➔h➔.➔l➔o➔g➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔u➔t➔h➔e➔n➔t➔i➔c➔a➔t➔i➔o➔n➔ ➔l➔o➔g➔s➔ ➔(➔U➔b➔u➔n➔t➔u➔)➔
➔/➔v➔a➔r➔/➔l➔o➔g➔/➔s➔e➔c➔u➔r➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔u➔t➔h➔e➔n➔t➔i➔c➔a➔t➔i➔o➔n➔ ➔l➔o➔g➔s➔ ➔(➔R➔H➔E➔L➔)➔
➔/➔v➔a➔r➔/➔l➔o➔g➔/➔k➔e➔r➔n➔.➔l➔o➔g➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔k➔e➔r➔n➔e➔l➔ ➔l➔o➔g➔s➔
➔/➔v➔a➔r➔/➔l➔o➔g➔/➔d➔m➔e➔s➔g➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔b➔o➔o➔t➔ ➔m➔e➔s➔s➔a➔g➔e➔s➔
➔/➔v➔a➔r➔/➔l➔o➔g➔/➔n➔g➔i➔n➔x➔/➔a➔c➔c➔e➔s➔s➔.➔l➔o➔g➔ ➔ ➔ ➔ ➔#➔ ➔n➔g➔i➔n➔x➔ ➔a➔c➔c➔e➔s➔s➔ ➔l➔o➔g➔
➔/➔v➔a➔r➔/➔l➔o➔g➔/➔n➔g➔i➔n➔x➔/➔e➔r➔r➔o➔r➔.➔l➔o➔g➔ ➔ ➔ ➔ ➔ ➔#➔ ➔n➔g➔i➔n➔x➔ ➔e➔r➔r➔o➔r➔ ➔l➔o➔g➔
➔/➔v➔a➔r➔/➔l➔o➔g➔/➔a➔p➔a➔c➔h➔e➔2➔/➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔a➔p➔a➔c➔h➔e➔ ➔l➔o➔g➔s➔
➔#➔ ➔V➔i➔e➔w➔ ➔l➔o➔g➔s➔
➔t➔a➔i➔l➔ ➔-➔f➔ ➔/➔v➔a➔r➔/➔l➔o➔g➔/➔s➔y➔s➔l➔o➔g➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔l➔l➔o➔w➔ ➔l➔i➔v➔e➔ ➔l➔o➔g➔
➔t➔a➔i➔l➔ ➔-➔1➔0➔0➔ ➔/➔v➔a➔r➔/➔l➔o➔g➔/➔n➔g➔i➔n➔x➔/➔e➔r➔r➔o➔r➔.➔l➔o➔g➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔a➔s➔t➔ ➔1➔0➔0➔ ➔l➔i➔n➔e➔s➔
➔g➔r➔e➔p➔ ➔"➔E➔R➔R➔O➔R➔"➔ ➔/➔v➔a➔r➔/➔l➔o➔g➔/➔a➔p➔p➔.➔l➔o➔g➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔i➔l➔t➔e➔r➔ ➔e➔r➔r➔o➔r➔s➔
➔g➔r➔e➔p➔ ➔"➔E➔R➔R➔O➔R➔"➔ ➔/➔v➔a➔r➔/➔l➔o➔g➔/➔a➔p➔p➔.➔l➔o➔g➔ ➔|➔ ➔w➔c➔ ➔-➔l➔ ➔ ➔ ➔#➔ ➔c➔o➔u➔n➔t➔ ➔e➔r➔r➔o➔r➔s➔
➔j➔o➔u➔r➔n➔a➔l➔c➔t➔l➔ ➔-➔f➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔f➔o➔l➔l➔o➔w➔ ➔s➔y➔s➔t➔e➔m➔d➔ ➔j➔o➔u➔r➔n➔a➔l➔
➔j➔o➔u➔r➔n➔a➔l➔c➔t➔l➔ ➔-➔u➔ ➔n➔g➔i➔n➔x➔ ➔-➔-➔s➔i➔n➔c➔e➔ ➔"➔1➔ ➔h➔o➔u➔r➔ ➔a➔g➔o➔"➔ ➔#➔ ➔n➔g➔i➔n➔x➔ ➔l➔o➔g➔s➔ ➔f➔r➔o➔m➔ ➔l➔a➔s➔t➔ ➔h➔o➔u➔r➔
➔j➔o➔u➔r➔n➔a➔l➔c➔t➔l➔ ➔-➔-➔s➔i➔n➔c➔e➔ ➔"➔2➔0➔2➔4➔-➔0➔1➔-➔0➔1➔"➔ ➔-➔-➔u➔n➔t➔i➔l➔ ➔"➔2➔0➔2➔4➔-➔0➔1➔-➔0➔2➔"➔ ➔ ➔#➔ ➔d➔a➔t➔e➔ ➔r➔a➔n➔g➔e➔
➔2➔3➔.➔ ➔S➔h➔e➔l➔l➔ ➔S➔c➔r➔i➔p➔t➔i➔n➔g➔ ➔B➔a➔s➔i➔c➔s➔
➔#➔!➔/➔b➔i➔n➔/➔b➔a➔s➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔s➔h➔e➔b➔a➔n➔g➔ ➔—➔ ➔t➔e➔l➔l➔s➔ ➔s➔y➔s➔t➔e➔m➔ ➔t➔o➔ ➔u➔s➔e➔ ➔b➔a➔s➔h➔
➔#➔ ➔V➔a➔r➔i➔a➔b➔l➔e➔s➔
➔N➔A➔M➔E➔=➔"➔A➔k➔h➔i➔l➔"➔
➔
➔
➔
➔
➔e➔c➔h➔o➔ ➔"➔H➔e➔l➔l➔o➔,➔ ➔$➔N➔A➔M➔E➔"➔
➔#➔ ➔I➔n➔p➔u➔t➔
➔r➔e➔a➔d➔ ➔-➔p➔ ➔"➔E➔n➔t➔e➔r➔ ➔n➔a➔m➔e➔:➔ ➔"➔ ➔N➔A➔M➔E➔
➔#➔ ➔C➔o➔n➔d➔i➔t➔i➔o➔n➔s➔
➔i➔f➔ ➔[➔ ➔$➔N➔A➔M➔E➔ ➔=➔=➔ ➔"➔A➔k➔h➔i➔l➔"➔ ➔]➔;➔ ➔t➔h➔e➔n➔
➔ ➔ ➔ ➔ ➔e➔c➔h➔o➔ ➔"➔W➔e➔l➔c➔o➔m➔e➔ ➔A➔k➔h➔i➔l➔"➔
➔e➔l➔i➔f➔ ➔[➔ ➔$➔N➔A➔M➔E➔ ➔=➔=➔ ➔"➔J➔o➔h➔n➔"➔ ➔]➔;➔ ➔t➔h➔e➔n➔
➔ ➔ ➔ ➔ ➔e➔c➔h➔o➔ ➔"➔W➔e➔l➔c➔o➔m➔e➔ ➔J➔o➔h➔n➔"➔
➔e➔l➔s➔e➔
➔ ➔ ➔ ➔ ➔e➔c➔h➔o➔ ➔"➔U➔n➔k➔n➔o➔w➔n➔ ➔u➔s➔e➔r➔"➔
➔f➔i➔
➔#➔ ➔L➔o➔o➔p➔s➔
➔f➔o➔r➔ ➔i➔ ➔i➔n➔ ➔1➔ ➔2➔ ➔3➔ ➔4➔ ➔5➔;➔ ➔d➔o➔
➔ ➔ ➔ ➔ ➔e➔c➔h➔o➔ ➔"➔N➔u➔m➔b➔e➔r➔:➔ ➔$➔i➔"➔
➔d➔o➔n➔e➔
➔f➔o➔r➔ ➔f➔i➔l➔e➔ ➔i➔n➔ ➔*➔.➔t➔x➔t➔;➔ ➔d➔o➔
➔ ➔ ➔ ➔ ➔e➔c➔h➔o➔ ➔"➔P➔r➔o➔c➔e➔s➔s➔i➔n➔g➔:➔ ➔$➔f➔i➔l➔e➔"➔
➔d➔o➔n➔e➔
➔w➔h➔i➔l➔e➔ ➔[➔ ➔c➔o➔n➔d➔i➔t➔i➔o➔n➔ ➔]➔;➔ ➔d➔o➔
➔ ➔ ➔ ➔ ➔#➔ ➔c➔o➔m➔m➔a➔n➔d➔s➔
➔d➔o➔n➔e➔
➔#➔ ➔F➔u➔n➔c➔t➔i➔o➔n➔s➔
➔g➔r➔e➔e➔t➔(➔)➔ ➔{➔
➔ ➔ ➔ ➔ ➔e➔c➔h➔o➔ ➔"➔H➔e➔l➔l➔o➔,➔ ➔$➔1➔"➔ ➔ ➔ ➔ ➔#➔ ➔$➔1➔ ➔=➔ ➔f➔i➔r➔s➔t➔ ➔a➔r➔g➔u➔m➔e➔n➔t➔
➔}➔
➔g➔r➔e➔e➔t➔ ➔"➔A➔k➔h➔i➔l➔"➔
➔#➔ ➔E➔x➔i➔t➔ ➔c➔o➔d➔e➔s➔
➔e➔c➔h➔o➔ ➔$➔?➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔0➔ ➔=➔ ➔s➔u➔c➔c➔e➔s➔s➔,➔ ➔n➔o➔n➔-➔z➔e➔r➔o➔ ➔=➔ ➔f➔a➔i➔l➔u➔r➔e➔
➔e➔x➔i➔t➔ ➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔x➔i➔t➔ ➔s➔c➔r➔i➔p➔t➔ ➔w➔i➔t➔h➔ ➔s➔u➔c➔c➔e➔s➔s➔
➔e➔x➔i➔t➔ ➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔e➔x➔i➔t➔ ➔s➔c➔r➔i➔p➔t➔ ➔w➔i➔t➔h➔ ➔f➔a➔i➔l➔u➔r➔e➔
➔#➔ ➔M➔a➔k➔e➔ ➔s➔c➔r➔i➔p➔t➔ ➔e➔x➔e➔c➔u➔t➔a➔b➔l➔e➔ ➔a➔n➔d➔ ➔r➔u➔n➔
➔c➔h➔m➔o➔d➔ ➔+➔x➔ ➔s➔c➔r➔i➔p➔t➔.➔s➔h➔
➔.➔/➔s➔c➔r➔i➔p➔t➔.➔s➔h➔
➔b➔a➔s➔h➔ ➔s➔c➔r➔i➔p➔t➔.➔s➔h➔
➔2➔4➔.➔ ➔Q➔u➔i➔c➔k➔ ➔R➔e➔f➔e➔r➔e➔n➔c➔e➔ ➔—➔ ➔M➔o➔s➔t➔ ➔U➔s➔e➔d➔ ➔L➔i➔n➔u➔x➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔
➔
➔
➔
➔
➔#➔ ➔N➔A➔V➔I➔G➔A➔T➔I➔O➔N➔
➔p➔w➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔c➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔l➔s➔ ➔-➔l➔a➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔c➔d➔ ➔~➔
➔#➔ ➔F➔I➔L➔E➔ ➔O➔P➔E➔R➔A➔T➔I➔O➔N➔S➔
➔t➔o➔u➔c➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔m➔k➔d➔i➔r➔ ➔-➔p➔ ➔ ➔ ➔ ➔ ➔c➔p➔ ➔-➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔m➔v➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔r➔m➔ ➔-➔r➔f➔
➔c➔a➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔l➔e➔s➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔h➔e➔a➔d➔ ➔-➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔t➔a➔i➔l➔ ➔-➔f➔ ➔ ➔ ➔ ➔ ➔ ➔f➔i➔l➔e➔
➔#➔ ➔P➔E➔R➔M➔I➔S➔S➔I➔O➔N➔S➔
➔c➔h➔m➔o➔d➔ ➔7➔5➔5➔ ➔ ➔ ➔ ➔ ➔c➔h➔o➔w➔n➔ ➔u➔s➔e➔r➔:➔g➔r➔o➔u➔p➔ ➔ ➔ ➔ ➔s➔e➔t➔f➔a➔c➔l➔ ➔-➔m➔ ➔u➔:➔u➔s➔e➔r➔:➔r➔w➔x➔ ➔ ➔ ➔ ➔g➔e➔t➔f➔a➔c➔l➔
➔#➔ ➔U➔S➔E➔R➔ ➔M➔A➔N➔A➔G➔E➔M➔E➔N➔T➔
➔u➔s➔e➔r➔a➔d➔d➔ ➔-➔m➔ ➔ ➔ ➔ ➔p➔a➔s➔s➔w➔d➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔u➔s➔e➔r➔m➔o➔d➔ ➔-➔a➔G➔ ➔ ➔ ➔ ➔u➔s➔e➔r➔d➔e➔l➔ ➔-➔r➔
➔g➔r➔o➔u➔p➔a➔d➔d➔ ➔ ➔ ➔ ➔ ➔ ➔g➔p➔a➔s➔s➔w➔d➔ ➔-➔a➔ ➔ ➔ ➔ ➔g➔r➔o➔u➔p➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔i➔d➔
➔#➔ ➔P➔R➔O➔C➔E➔S➔S➔E➔S➔
➔p➔s➔ ➔a➔u➔x➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔t➔o➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔k➔i➔l➔l➔ ➔-➔9➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔y➔s➔t➔e➔m➔c➔t➔l➔ ➔s➔t➔a➔t➔u➔s➔
➔s➔y➔s➔t➔e➔m➔c➔t➔l➔ ➔s➔t➔a➔r➔t➔/➔s➔t➔o➔p➔/➔r➔e➔s➔t➔a➔r➔t➔/➔e➔n➔a➔b➔l➔e➔
➔#➔ ➔N➔E➔T➔W➔O➔R➔K➔I➔N➔G➔
➔i➔p➔ ➔a➔d➔d➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔p➔i➔n➔g➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔c➔u➔r➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔s➔ ➔-➔t➔u➔l➔p➔n➔
➔u➔f➔w➔ ➔a➔l➔l➔o➔w➔ ➔ ➔ ➔ ➔ ➔s➔s➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔c➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔i➔g➔
➔#➔ ➔S➔E➔A➔R➔C➔H➔
➔g➔r➔e➔p➔ ➔-➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔f➔i➔n➔d➔ ➔/➔ ➔-➔n➔a➔m➔e➔ ➔ ➔l➔o➔c➔a➔t➔e➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔g➔r➔e➔p➔ ➔-➔i➔ ➔-➔n➔
➔a➔w➔k➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔e➔d➔ ➔-➔i➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔c➔u➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔s➔o➔r➔t➔ ➔|➔ ➔u➔n➔i➔q➔
➔#➔ ➔C➔O➔M➔P➔R➔E➔S➔S➔I➔O➔N➔
➔t➔a➔r➔ ➔-➔c➔z➔v➔f➔ ➔ ➔ ➔ ➔ ➔t➔a➔r➔ ➔-➔x➔z➔v➔f➔ ➔ ➔ ➔ ➔ ➔z➔i➔p➔ ➔-➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔u➔n➔z➔i➔p➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔g➔z➔i➔p➔
➔#➔ ➔D➔I➔S➔K➔
➔d➔f➔ ➔-➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔d➔u➔ ➔-➔s➔h➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔l➔s➔b➔l➔k➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔m➔o➔u➔n➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔u➔m➔o➔u➔n➔t➔
➔m➔k➔f➔s➔.➔e➔x➔t➔4➔ ➔ ➔ ➔ ➔ ➔b➔l➔k➔i➔d➔
➔#➔ ➔L➔O➔G➔S➔
➔t➔a➔i➔l➔ ➔-➔f➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔j➔o➔u➔r➔n➔a➔l➔c➔t➔l➔ ➔-➔u➔ ➔ ➔ ➔ ➔g➔r➔e➔p➔ ➔"➔E➔R➔R➔O➔R➔"➔ ➔ ➔ ➔ ➔/➔v➔a➔r➔/➔l➔o➔g➔/➔
➔T➔O➔P➔I➔C➔S➔ ➔T➔O➔ ➔A➔D➔D➔ ➔N➔E➔X➔T➔
➔[➔ ➔]➔ ➔T➔e➔r➔r➔a➔f➔o➔r➔m➔ ➔—➔ ➔c➔o➔m➔p➔l➔e➔t➔e➔ ➔g➔u➔i➔d➔e➔
➔[➔ ➔]➔ ➔A➔z➔u➔r➔e➔ ➔D➔e➔v➔O➔p➔s➔ ➔—➔ ➔c➔o➔m➔p➔l➔e➔t➔e➔ ➔g➔u➔i➔d➔e➔
➔
➔
➔
➔
➔[➔ ➔]➔ ➔A➔n➔s➔i➔b➔l➔e➔ ➔—➔ ➔c➔o➔m➔p➔l➔e➔t➔e➔ ➔g➔u➔i➔d➔e➔
➔[➔ ➔]➔ ➔A➔W➔S➔ ➔S➔c➔e➔n➔a➔r➔i➔o➔-➔b➔a➔s➔e➔d➔ ➔q➔u➔e➔s➔t➔i➔o➔n➔s➔
➔[➔ ➔]➔ ➔N➔e➔t➔w➔o➔r➔k➔i➔n➔g➔ ➔d➔e➔e➔p➔ ➔d➔i➔v➔e➔
➔P➔r➔e➔p➔a➔r➔e➔d➔ ➔f➔o➔r➔:➔ ➔A➔k➔h➔i➔l➔ ➔B➔ ➔M➔ ➔|➔ ➔D➔e➔v➔O➔p➔s➔ ➔&➔ ➔C➔l➔o➔u➔d➔ ➔E➔n➔g➔i➔n➔e➔e➔r➔
➔K➔e➔e➔p➔ ➔g➔o➔i➔n➔g➔ ➔—➔ ➔y➔o➔u➔'➔r➔e➔ ➔d➔o➔i➔n➔g➔ ➔g➔r➔e➔a➔t➔!➔
➔

---

# PART 2: COMPUTER NETWORKING FUNDAMENTALS

➔S➔E➔C➔T➔I➔O➔N➔ ➔1➔0➔:➔ ➔N➔E➔T➔W➔O➔R➔K➔I➔N➔G➔ ➔F➔U➔N➔D➔A➔M➔E➔N➔T➔A➔L➔S➔ ➔—➔
➔C➔O➔M➔P➔L➔E➔T➔E➔ ➔G➔U➔I➔D➔E➔
➔E➔s➔s➔e➔n➔t➔i➔a➔l➔ ➔n➔e➔t➔w➔o➔r➔k➔i➔n➔g➔ ➔k➔n➔o➔w➔l➔e➔d➔g➔e➔ ➔f➔o➔r➔ ➔D➔e➔v➔O➔p➔s➔ ➔i➔n➔t➔e➔r➔v➔i➔e➔w➔s➔.➔ ➔C➔o➔v➔e➔r➔s➔ ➔O➔S➔I➔,➔ ➔T➔C➔P➔/➔I➔P➔,➔ ➔D➔N➔S➔,➔ ➔D➔H➔C➔P➔,➔ ➔I➔P➔ ➔a➔d➔d➔r➔e➔s➔s➔i➔n➔g➔,➔ ➔a➔n➔d➔
➔m➔o➔r➔e➔.➔
➔1➔.➔ ➔W➔h➔y➔ ➔N➔e➔t➔w➔o➔r➔k➔i➔n➔g➔ ➔M➔a➔t➔t➔e➔r➔s➔ ➔f➔o➔r➔ ➔D➔e➔v➔O➔p➔s➔
➔A➔s➔ ➔a➔ ➔D➔e➔v➔O➔p➔s➔ ➔e➔n➔g➔i➔n➔e➔e➔r➔ ➔y➔o➔u➔ ➔d➔e➔a➔l➔ ➔w➔i➔t➔h➔ ➔n➔e➔t➔w➔o➔r➔k➔i➔n➔g➔ ➔e➔v➔e➔r➔y➔ ➔d➔a➔y➔ ➔—➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔i➔n➔g➔ ➔V➔P➔C➔s➔,➔ ➔s➔e➔t➔t➔i➔n➔g➔ ➔u➔p➔ ➔l➔o➔a➔d➔ ➔b➔a➔l➔a➔n➔c➔e➔r➔s➔,➔
➔t➔r➔o➔u➔b➔l➔e➔s➔h➔o➔o➔t➔i➔n➔g➔ ➔w➔h➔y➔ ➔s➔e➔r➔v➔i➔c➔e➔s➔ ➔c➔a➔n➔'➔t➔ ➔c➔o➔m➔m➔u➔n➔i➔c➔a➔t➔e➔,➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔i➔n➔g➔ ➔s➔e➔c➔u➔r➔i➔t➔y➔ ➔g➔r➔o➔u➔p➔s➔.➔ ➔U➔n➔d➔e➔r➔s➔t➔a➔n➔d➔i➔n➔g➔ ➔n➔e➔t➔w➔o➔r➔k➔i➔n➔g➔
➔f➔u➔n➔d➔a➔m➔e➔n➔t➔a➔l➔s➔ ➔m➔a➔k➔e➔s➔ ➔y➔o➔u➔ ➔a➔ ➔m➔u➔c➔h➔ ➔s➔t➔r➔o➔n➔g➔e➔r➔ ➔e➔n➔g➔i➔n➔e➔e➔r➔.➔
➔2➔.➔ ➔O➔S➔I➔ ➔M➔o➔d➔e➔l➔ ➔—➔ ➔7➔ ➔L➔a➔y➔e➔r➔s➔
➔O➔S➔I➔ ➔(➔O➔p➔e➔n➔ ➔S➔y➔s➔t➔e➔m➔s➔ ➔I➔n➔t➔e➔r➔c➔o➔n➔n➔e➔c➔t➔i➔o➔n➔)➔ ➔—➔ ➔a➔ ➔c➔o➔n➔c➔e➔p➔t➔u➔a➔l➔ ➔f➔r➔a➔m➔e➔w➔o➔r➔k➔ ➔t➔h➔a➔t➔ ➔b➔r➔e➔a➔k➔s➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔c➔o➔m➔m➔u➔n➔i➔c➔a➔t➔i➔o➔n➔ ➔i➔n➔t➔o➔ ➔7➔
➔l➔a➔y➔e➔r➔s➔,➔ ➔e➔a➔c➔h➔ ➔w➔i➔t➔h➔ ➔a➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔f➔u➔n➔c➔t➔i➔o➔n➔.➔
➔L➔a➔y➔e➔r➔ ➔7➔ ➔—➔ ➔A➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔ ➔ ➔ ➔ ➔→➔ ➔H➔T➔T➔P➔,➔ ➔F➔T➔P➔,➔ ➔S➔M➔T➔P➔,➔ ➔T➔e➔l➔n➔e➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔D➔a➔t➔a➔
➔L➔a➔y➔e➔r➔ ➔6➔ ➔—➔ ➔P➔r➔e➔s➔e➔n➔t➔a➔t➔i➔o➔n➔ ➔ ➔ ➔→➔ ➔J➔P➔E➔G➔,➔ ➔G➔I➔F➔,➔ ➔M➔P➔E➔G➔,➔ ➔A➔S➔C➔I➔I➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔D➔a➔t➔a➔
➔L➔a➔y➔e➔r➔ ➔5➔ ➔—➔ ➔S➔e➔s➔s➔i➔o➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔S➔e➔s➔s➔i➔o➔n➔ ➔s➔e➔t➔u➔p➔/➔t➔e➔a➔r➔d➔o➔w➔n➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔D➔a➔t➔a➔
➔L➔a➔y➔e➔r➔ ➔4➔ ➔—➔ ➔T➔r➔a➔n➔s➔p➔o➔r➔t➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔T➔C➔P➔,➔ ➔U➔D➔P➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔S➔e➔g➔m➔e➔n➔t➔
➔L➔a➔y➔e➔r➔ ➔3➔ ➔—➔ ➔N➔e➔t➔w➔o➔r➔k➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔I➔P➔,➔ ➔I➔C➔M➔P➔,➔ ➔A➔R➔P➔,➔ ➔O➔S➔P➔F➔,➔ ➔R➔I➔P➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔P➔a➔c➔k➔e➔t➔
➔L➔a➔y➔e➔r➔ ➔2➔ ➔—➔ ➔D➔a➔t➔a➔ ➔L➔i➔n➔k➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔E➔t➔h➔e➔r➔n➔e➔t➔,➔ ➔P➔P➔P➔,➔ ➔M➔A➔C➔ ➔a➔d➔d➔r➔e➔s➔s➔e➔s➔ ➔ ➔ ➔→➔ ➔F➔r➔a➔m➔e➔
➔L➔a➔y➔e➔r➔ ➔1➔ ➔—➔ ➔P➔h➔y➔s➔i➔c➔a➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔C➔a➔b➔l➔e➔s➔,➔ ➔f➔i➔b➔e➔r➔,➔ ➔h➔u➔b➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔B➔i➔t➔
➔E➔a➔s➔y➔ ➔m➔e➔m➔o➔r➔y➔ ➔t➔r➔i➔c➔k➔ ➔(➔t➔o➔p➔ ➔t➔o➔ ➔b➔o➔t➔t➔o➔m➔)➔:➔ ➔A➔l➔l➔ ➔P➔e➔o➔p➔l➔e➔ ➔S➔e➔e➔m➔ ➔T➔o➔ ➔N➔e➔e➔d➔ ➔D➔a➔t➔a➔ ➔P➔r➔o➔c➔e➔s➔s➔i➔n➔g➔
➔L➔a➔y➔e➔r➔ ➔N➔a➔m➔e➔ ➔P➔u➔r➔p➔o➔s➔e➔ ➔K➔e➔y➔ ➔P➔r➔o➔t➔o➔c➔o➔l➔s➔
➔7➔ ➔A➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔ ➔I➔n➔t➔e➔r➔f➔a➔c➔e➔ ➔f➔o➔r➔ ➔a➔p➔p➔s➔ ➔t➔o➔ ➔a➔c➔c➔e➔s➔s➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔H➔T➔T➔P➔,➔ ➔F➔T➔P➔,➔ ➔S➔M➔T➔P➔,➔ ➔T➔e➔l➔n➔e➔t➔
➔6➔ ➔P➔r➔e➔s➔e➔n➔t➔a➔t➔i➔o➔n➔ ➔D➔a➔t➔a➔ ➔f➔o➔r➔m➔a➔t➔t➔i➔n➔g➔,➔ ➔e➔n➔c➔r➔y➔p➔t➔i➔o➔n➔,➔ ➔c➔o➔m➔p➔r➔e➔s➔s➔i➔o➔n➔ ➔J➔P➔E➔G➔,➔ ➔G➔I➔F➔,➔ ➔M➔P➔E➔G➔,➔ ➔A➔S➔C➔I➔I➔
➔5➔ ➔S➔e➔s➔s➔i➔o➔n➔ ➔E➔s➔t➔a➔b➔l➔i➔s➔h➔,➔ ➔m➔a➔n➔a➔g➔e➔,➔ ➔t➔e➔r➔m➔i➔n➔a➔t➔e➔ ➔s➔e➔s➔s➔i➔o➔n➔s➔ ➔N➔e➔t➔B➔I➔O➔S➔,➔ ➔R➔P➔C➔
➔4➔ ➔T➔r➔a➔n➔s➔p➔o➔r➔t➔ ➔R➔e➔l➔i➔a➔b➔l➔e➔/➔u➔n➔r➔e➔l➔i➔a➔b➔l➔e➔ ➔d➔e➔l➔i➔v➔e➔r➔y➔,➔ ➔s➔e➔g➔m➔e➔n➔t➔a➔t➔i➔o➔n➔ ➔T➔C➔P➔,➔ ➔U➔D➔P➔
➔
➔
➔
➔
➔3➔ ➔N➔e➔t➔w➔o➔r➔k➔ ➔L➔o➔g➔i➔c➔a➔l➔ ➔a➔d➔d➔r➔e➔s➔s➔i➔n➔g➔,➔ ➔r➔o➔u➔t➔i➔n➔g➔ ➔p➔a➔c➔k➔e➔t➔s➔ ➔I➔P➔,➔ ➔I➔C➔M➔P➔,➔ ➔A➔R➔P➔,➔ ➔O➔S➔P➔F➔
➔2➔ ➔D➔a➔t➔a➔ ➔L➔i➔n➔k➔ ➔N➔o➔d➔e➔-➔t➔o➔-➔n➔o➔d➔e➔ ➔t➔r➔a➔n➔s➔f➔e➔r➔,➔ ➔M➔A➔C➔ ➔a➔d➔d➔r➔e➔s➔s➔i➔n➔g➔ ➔E➔t➔h➔e➔r➔n➔e➔t➔,➔ ➔P➔P➔P➔
➔1➔ ➔P➔h➔y➔s➔i➔c➔a➔l➔ ➔P➔h➔y➔s➔i➔c➔a➔l➔ ➔t➔r➔a➔n➔s➔m➔i➔s➔s➔i➔o➔n➔ ➔o➔f➔ ➔b➔i➔t➔s➔ ➔C➔a➔b➔l➔e➔s➔,➔ ➔f➔i➔b➔e➔r➔,➔ ➔h➔u➔b➔s➔
➔D➔e➔v➔O➔p➔s➔ ➔r➔e➔l➔e➔v➔a➔n➔c➔e➔:➔
➔L➔a➔y➔e➔r➔ ➔4➔ ➔—➔ ➔L➔o➔a➔d➔ ➔B➔a➔l➔a➔n➔c➔e➔r➔s➔ ➔(➔A➔L➔B➔ ➔=➔ ➔L➔a➔y➔e➔r➔ ➔7➔,➔ ➔N➔L➔B➔ ➔=➔ ➔L➔a➔y➔e➔r➔ ➔4➔)➔
➔L➔a➔y➔e➔r➔ ➔3➔ ➔—➔ ➔R➔o➔u➔t➔i➔n➔g➔ ➔t➔a➔b➔l➔e➔s➔,➔ ➔V➔P➔C➔ ➔r➔o➔u➔t➔i➔n➔g➔
➔L➔a➔y➔e➔r➔ ➔7➔ ➔—➔ ➔H➔T➔T➔P➔/➔H➔T➔T➔P➔S➔,➔ ➔a➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔-➔l➔e➔v➔e➔l➔ ➔f➔i➔r➔e➔w➔a➔l➔l➔s➔
➔3➔.➔ ➔T➔C➔P➔/➔I➔P➔ ➔M➔o➔d➔e➔l➔ ➔—➔ ➔4➔ ➔L➔a➔y➔e➔r➔s➔
➔A➔ ➔s➔i➔m➔p➔l➔i➔f➔i➔e➔d➔,➔ ➔p➔r➔a➔c➔t➔i➔c➔a➔l➔ ➔m➔o➔d➔e➔l➔ ➔u➔s➔e➔d➔ ➔i➔n➔ ➔r➔e➔a➔l➔ ➔n➔e➔t➔w➔o➔r➔k➔i➔n➔g➔.➔ ➔M➔a➔p➔s➔ ➔t➔o➔ ➔O➔S➔I➔ ➔l➔a➔y➔e➔r➔s➔.➔
➔T➔C➔P➔/➔I➔P➔ ➔L➔a➔y➔e➔r➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔O➔S➔I➔ ➔L➔a➔y➔e➔r➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔D➔a➔t➔a➔ ➔N➔a➔m➔e➔
➔A➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔ ➔ ➔ ➔ ➔=➔ ➔ ➔A➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔ ➔+➔ ➔P➔r➔e➔s➔e➔n➔t➔a➔t➔i➔o➔n➔ ➔+➔ ➔S➔e➔s➔s➔i➔o➔n➔ ➔ ➔ ➔→➔ ➔D➔a➔t➔a➔
➔T➔r➔a➔n➔s➔p➔o➔r➔t➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔ ➔T➔r➔a➔n➔s➔p➔o➔r➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔S➔e➔g➔m➔e➔n➔t➔
➔I➔n➔t➔e➔r➔n➔e➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔ ➔N➔e➔t➔w➔o➔r➔k➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔P➔a➔c➔k➔e➔t➔
➔N➔e➔t➔w➔o➔r➔k➔ ➔A➔c➔c➔e➔s➔s➔ ➔=➔ ➔ ➔D➔a➔t➔a➔ ➔L➔i➔n➔k➔ ➔+➔ ➔P➔h➔y➔s➔i➔c➔a➔l➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔→➔ ➔F➔r➔a➔m➔e➔ ➔/➔ ➔B➔i➔t➔
➔T➔C➔P➔/➔I➔P➔ ➔L➔a➔y➔e➔r➔ ➔K➔e➔y➔ ➔P➔r➔o➔t➔o➔c➔o➔l➔s➔ ➔F➔u➔n➔c➔t➔i➔o➔n➔
➔A➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔ ➔H➔T➔T➔P➔,➔ ➔F➔T➔P➔,➔ ➔D➔N➔S➔,➔ ➔S➔M➔T➔P➔ ➔U➔s➔e➔r➔-➔f➔a➔c➔i➔n➔g➔ ➔s➔e➔r➔v➔i➔c➔e➔s➔
➔T➔r➔a➔n➔s➔p➔o➔r➔t➔ ➔T➔C➔P➔,➔ ➔U➔D➔P➔ ➔E➔n➔d➔-➔t➔o➔-➔e➔n➔d➔ ➔d➔e➔l➔i➔v➔e➔r➔y➔
➔I➔n➔t➔e➔r➔n➔e➔t➔ ➔I➔P➔,➔ ➔A➔R➔P➔,➔ ➔I➔C➔M➔P➔ ➔R➔o➔u➔t➔i➔n➔g➔,➔ ➔l➔o➔g➔i➔c➔a➔l➔ ➔a➔d➔d➔r➔e➔s➔s➔i➔n➔g➔
➔N➔e➔t➔w➔o➔r➔k➔ ➔A➔c➔c➔e➔s➔s➔ ➔E➔t➔h➔e➔r➔n➔e➔t➔,➔ ➔M➔A➔C➔ ➔P➔h➔y➔s➔i➔c➔a➔l➔ ➔t➔r➔a➔n➔s➔m➔i➔s➔s➔i➔o➔n➔
➔4➔.➔ ➔T➔C➔P➔ ➔v➔s➔ ➔U➔D➔P➔
➔B➔o➔t➔h➔ ➔o➔p➔e➔r➔a➔t➔e➔ ➔a➔t➔ ➔L➔a➔y➔e➔r➔ ➔4➔ ➔(➔T➔r➔a➔n➔s➔p➔o➔r➔t➔ ➔L➔a➔y➔e➔r➔)➔.➔ ➔T➔h➔i➔n➔k➔ ➔o➔f➔ ➔d➔a➔t➔a➔ ➔a➔s➔ ➔c➔a➔r➔s➔ ➔c➔a➔r➔r➔y➔i➔n➔g➔ ➔p➔a➔c➔k➔a➔g➔e➔s➔ ➔—➔ ➔t➔h➔e➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔c➔e➔ ➔i➔s➔ ➔H➔O➔W➔
➔t➔h➔e➔y➔ ➔e➔n➔s➔u➔r➔e➔ ➔d➔e➔l➔i➔v➔e➔r➔y➔.➔
➔F➔e➔a➔t➔u➔r➔e➔ ➔T➔C➔P➔ ➔U➔D➔P➔
➔
➔
➔
➔
➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔ ➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔-➔o➔r➔i➔e➔n➔t➔e➔d➔ ➔(➔e➔s➔t➔a➔b➔l➔i➔s➔h➔e➔s➔ ➔c➔o➔n➔n➔e➔c➔t➔i➔o➔n➔
➔f➔i➔r➔s➔t➔)➔
➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔l➔e➔s➔s➔ ➔(➔n➔o➔ ➔s➔e➔t➔u➔p➔ ➔n➔e➔e➔d➔e➔d➔)➔
➔R➔e➔l➔i➔a➔b➔i➔l➔i➔t➔y➔ ➔R➔e➔l➔i➔a➔b➔l➔e➔ ➔—➔ ➔g➔u➔a➔r➔a➔n➔t➔e➔e➔s➔ ➔d➔e➔l➔i➔v➔e➔r➔y➔ ➔i➔n➔ ➔o➔r➔d➔e➔r➔ ➔U➔n➔r➔e➔l➔i➔a➔b➔l➔e➔ ➔—➔ ➔n➔o➔ ➔g➔u➔a➔r➔a➔n➔t➔e➔e➔
➔A➔c➔k➔n➔o➔w➔l➔e➔d➔g➔e➔m➔e➔n➔t➔ ➔Y➔e➔s➔ ➔—➔ ➔c➔o➔n➔f➔i➔r➔m➔s➔ ➔d➔a➔t➔a➔ ➔r➔e➔c➔e➔i➔v➔e➔d➔ ➔N➔o➔
➔S➔p➔e➔e➔d➔ ➔S➔l➔o➔w➔e➔r➔ ➔(➔o➔v➔e➔r➔h➔e➔a➔d➔ ➔f➔o➔r➔ ➔r➔e➔l➔i➔a➔b➔i➔l➔i➔t➔y➔)➔ ➔F➔a➔s➔t➔e➔r➔ ➔(➔n➔o➔ ➔o➔v➔e➔r➔h➔e➔a➔d➔)➔
➔P➔r➔o➔t➔o➔c➔o➔l➔ ➔n➔u➔m➔b➔e➔r➔ ➔6➔ ➔1➔7➔
➔U➔s➔e➔ ➔c➔a➔s➔e➔ ➔H➔T➔T➔P➔,➔ ➔F➔T➔P➔,➔ ➔S➔M➔T➔P➔,➔ ➔S➔S➔H➔ ➔D➔N➔S➔,➔ ➔D➔H➔C➔P➔,➔ ➔v➔i➔d➔e➔o➔ ➔s➔t➔r➔e➔a➔m➔i➔n➔g➔,➔
➔g➔a➔m➔i➔n➔g➔
➔W➔h➔y➔ ➔T➔C➔P➔ ➔i➔s➔ ➔R➔e➔l➔i➔a➔b➔l➔e➔:➔
➔1➔.➔ ➔A➔c➔k➔n➔o➔w➔l➔e➔d➔g➔e➔m➔e➔n➔t➔ ➔—➔ ➔r➔e➔c➔e➔i➔v➔e➔r➔ ➔c➔o➔n➔f➔i➔r➔m➔s➔ ➔d➔a➔t➔a➔ ➔r➔e➔c➔e➔i➔v➔e➔d➔
➔2➔.➔ ➔S➔e➔q➔u➔e➔n➔c➔i➔n➔g➔ ➔—➔ ➔d➔a➔t➔a➔ ➔d➔i➔v➔i➔d➔e➔d➔ ➔i➔n➔t➔o➔ ➔n➔u➔m➔b➔e➔r➔e➔d➔ ➔s➔e➔g➔m➔e➔n➔t➔s➔,➔ ➔r➔e➔c➔e➔i➔v➔e➔r➔ ➔d➔e➔t➔e➔c➔t➔s➔ ➔m➔i➔s➔s➔i➔n➔g➔ ➔s➔e➔g➔m➔e➔n➔t➔s➔
➔3➔.➔ ➔C➔h➔e➔c➔k➔s➔u➔m➔ ➔—➔ ➔d➔e➔t➔e➔c➔t➔s➔ ➔c➔o➔r➔r➔u➔p➔t➔i➔o➔n➔ ➔d➔u➔r➔i➔n➔g➔ ➔t➔r➔a➔n➔s➔m➔i➔s➔s➔i➔o➔n➔
➔W➔h➔y➔ ➔U➔D➔P➔ ➔i➔s➔ ➔U➔n➔r➔e➔l➔i➔a➔b➔l➔e➔ ➔b➔u➔t➔ ➔F➔a➔s➔t➔:➔
➔N➔o➔ ➔c➔o➔n➔n➔e➔c➔t➔i➔o➔n➔ ➔s➔e➔t➔u➔p➔
➔N➔o➔ ➔a➔c➔k➔n➔o➔w➔l➔e➔d➔g➔e➔m➔e➔n➔t➔s➔
➔N➔o➔ ➔r➔e➔t➔r➔a➔n➔s➔m➔i➔s➔s➔i➔o➔n➔
➔P➔e➔r➔f➔e➔c➔t➔ ➔f➔o➔r➔ ➔r➔e➔a➔l➔-➔t➔i➔m➔e➔ ➔s➔t➔r➔e➔a➔m➔i➔n➔g➔,➔ ➔g➔a➔m➔i➔n➔g➔,➔ ➔D➔N➔S➔ ➔w➔h➔e➔r➔e➔ ➔s➔p➔e➔e➔d➔ ➔>➔ ➔a➔c➔c➔u➔r➔a➔c➔y➔
➔5➔.➔ ➔T➔C➔P➔ ➔T➔h➔r➔e➔e➔-➔W➔a➔y➔ ➔H➔a➔n➔d➔s➔h➔a➔k➔e➔
➔P➔r➔o➔c➔e➔s➔s➔ ➔t➔o➔ ➔e➔s➔t➔a➔b➔l➔i➔s➔h➔ ➔a➔ ➔c➔o➔n➔n➔e➔c➔t➔i➔o➔n➔ ➔b➔e➔t➔w➔e➔e➔n➔ ➔c➔l➔i➔e➔n➔t➔ ➔a➔n➔d➔ ➔s➔e➔r➔v➔e➔r➔ ➔B➔E➔F➔O➔R➔E➔ ➔d➔a➔t➔a➔ ➔i➔s➔ ➔s➔e➔n➔t➔.➔
➔C➔l➔i➔e➔n➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔S➔e➔r➔v➔e➔r➔
➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔ ➔ ➔│➔─➔─➔─➔─➔ ➔S➔Y➔N➔ ➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔ ➔▶➔ ➔│➔ ➔ ➔S➔t➔e➔p➔ ➔1➔:➔ ➔C➔l➔i➔e➔n➔t➔ ➔s➔a➔y➔s➔ ➔"➔I➔ ➔w➔a➔n➔t➔ ➔t➔o➔ ➔c➔o➔n➔n➔e➔c➔t➔"➔
➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔ ➔ ➔│➔ ➔◀➔ ➔─➔─➔─➔ ➔S➔Y➔N➔-➔A➔C➔K➔ ➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔│➔ ➔ ➔S➔t➔e➔p➔ ➔2➔:➔ ➔S➔e➔r➔v➔e➔r➔ ➔s➔a➔y➔s➔ ➔"➔O➔K➔,➔ ➔I➔'➔m➔ ➔r➔e➔a➔d➔y➔"➔
➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔ ➔ ➔│➔─➔─➔─➔─➔ ➔A➔C➔K➔ ➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔ ➔▶➔ ➔│➔ ➔ ➔S➔t➔e➔p➔ ➔3➔:➔ ➔C➔l➔i➔e➔n➔t➔ ➔c➔o➔n➔f➔i➔r➔m➔s➔ ➔"➔L➔e➔t➔'➔s➔ ➔g➔o➔"➔
➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔ ➔ ➔│➔ ➔←➔─➔─➔─➔─➔ ➔D➔A➔T➔A➔ ➔F➔L➔O➔W➔S➔ ➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔ ➔▶➔ ➔│➔ ➔ ➔C➔o➔n➔n➔e➔c➔t➔i➔o➔n➔ ➔e➔s➔t➔a➔b➔l➔i➔s➔h➔e➔d➔!➔
➔S➔Y➔N➔ ➔—➔ ➔S➔y➔n➔c➔h➔r➔o➔n➔i➔z➔e➔ ➔—➔ ➔c➔l➔i➔e➔n➔t➔ ➔r➔e➔q➔u➔e➔s➔t➔s➔ ➔c➔o➔n➔n➔e➔c➔t➔i➔o➔n➔
➔S➔Y➔N➔-➔A➔C➔K➔ ➔—➔ ➔S➔y➔n➔c➔h➔r➔o➔n➔i➔z➔e➔-➔A➔c➔k➔n➔o➔w➔l➔e➔d➔g➔e➔ ➔—➔ ➔s➔e➔r➔v➔e➔r➔ ➔a➔c➔k➔n➔o➔w➔l➔e➔d➔g➔e➔s➔ ➔a➔n➔d➔ ➔s➔i➔g➔n➔a➔l➔s➔ ➔r➔e➔a➔d➔i➔n➔e➔s➔s➔
➔
➔
➔
➔
➔➔ ➔➔
➔A➔C➔K➔ ➔—➔ ➔A➔c➔k➔n➔o➔w➔l➔e➔d➔g➔e➔ ➔—➔ ➔c➔l➔i➔e➔n➔t➔ ➔c➔o➔n➔f➔i➔r➔m➔s➔,➔ ➔c➔o➔n➔n➔e➔c➔t➔i➔o➔n➔ ➔e➔s➔t➔a➔b➔l➔i➔s➔h➔e➔d➔
➔6➔.➔ ➔D➔N➔S➔ ➔—➔ ➔D➔o➔m➔a➔i➔n➔ ➔N➔a➔m➔e➔ ➔S➔y➔s➔t➔e➔m➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔D➔N➔S➔?➔
➔D➔N➔S➔ ➔t➔r➔a➔n➔s➔l➔a➔t➔e➔s➔ ➔h➔u➔m➔a➔n➔-➔r➔e➔a➔d➔a➔b➔l➔e➔ ➔d➔o➔m➔a➔i➔n➔ ➔n➔a➔m➔e➔s➔ ➔(➔l➔i➔k➔e➔ ➔g➔o➔o➔g➔l➔e➔.➔c➔o➔m➔)➔ ➔i➔n➔t➔o➔ ➔I➔P➔ ➔a➔d➔d➔r➔e➔s➔s➔e➔s➔ ➔(➔l➔i➔k➔e➔ ➔1➔4➔2➔.➔2➔5➔0➔.➔6➔4➔.➔4➔6➔)➔ ➔t➔h➔a➔t➔
➔c➔o➔m➔p➔u➔t➔e➔r➔s➔ ➔u➔s➔e➔ ➔t➔o➔ ➔c➔o➔m➔m➔u➔n➔i➔c➔a➔t➔e➔.➔
➔Y➔o➔u➔ ➔t➔y➔p➔e➔:➔ ➔g➔o➔o➔g➔l➔e➔.➔c➔o➔m➔
➔D➔N➔S➔ ➔r➔e➔s➔o➔l➔v➔e➔s➔:➔ ➔1➔4➔2➔.➔2➔5➔0➔.➔6➔4➔.➔4➔6➔
➔B➔r➔o➔w➔s➔e➔r➔ ➔c➔o➔n➔n➔e➔c➔t➔s➔ ➔t➔o➔ ➔t➔h➔a➔t➔ ➔I➔P➔
➔D➔N➔S➔ ➔R➔e➔s➔o➔l➔u➔t➔i➔o➔n➔ ➔F➔l➔o➔w➔:➔
➔B➔r➔o➔w➔s➔e➔r➔ ➔→➔ ➔L➔o➔c➔a➔l➔ ➔C➔a➔c➔h➔e➔ ➔→➔ ➔H➔o➔s➔t➔s➔ ➔f➔i➔l➔e➔ ➔→➔ ➔D➔N➔S➔ ➔R➔e➔s➔o➔l➔v➔e➔r➔ ➔→➔ ➔R➔o➔o➔t➔ ➔S➔e➔r➔v➔e➔r➔ ➔→➔ ➔T➔L➔D➔ ➔S➔e➔r➔v➔e➔r➔ ➔→➔ ➔A➔u➔t➔h➔o➔r➔i➔
➔K➔e➔y➔ ➔D➔N➔S➔ ➔C➔o➔m➔m➔a➔n➔d➔s➔:➔
➔n➔s➔l➔o➔o➔k➔u➔p➔ ➔g➔o➔o➔g➔l➔e➔.➔c➔o➔m➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔D➔N➔S➔ ➔l➔o➔o➔k➔u➔p➔
➔d➔i➔g➔ ➔g➔o➔o➔g➔l➔e➔.➔c➔o➔m➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔d➔e➔t➔a➔i➔l➔e➔d➔ ➔D➔N➔S➔ ➔l➔o➔o➔k➔u➔p➔
➔d➔i➔g➔ ➔g➔o➔o➔g➔l➔e➔.➔c➔o➔m➔ ➔A➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔o➔o➔k➔u➔p➔ ➔A➔ ➔r➔e➔c➔o➔r➔d➔ ➔(➔I➔P➔v➔4➔)➔
➔d➔i➔g➔ ➔g➔o➔o➔g➔l➔e➔.➔c➔o➔m➔ ➔M➔X➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔o➔o➔k➔u➔p➔ ➔m➔a➔i➔l➔ ➔r➔e➔c➔o➔r➔d➔s➔
➔c➔a➔t➔ ➔/➔e➔t➔c➔/➔r➔e➔s➔o➔l➔v➔.➔c➔o➔n➔f➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔D➔N➔S➔ ➔s➔e➔r➔v➔e➔r➔ ➔c➔o➔n➔f➔i➔g➔
➔c➔a➔t➔ ➔/➔e➔t➔c➔/➔h➔o➔s➔t➔s➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔l➔o➔c➔a➔l➔ ➔h➔o➔s➔t➔n➔a➔m➔e➔ ➔r➔e➔s➔o➔l➔u➔t➔i➔o➔n➔
➔7➔.➔ ➔A➔R➔P➔ ➔—➔ ➔A➔d➔d➔r➔e➔s➔s➔ ➔R➔e➔s➔o➔l➔u➔t➔i➔o➔n➔ ➔P➔r➔o➔t➔o➔c➔o➔l➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔A➔R➔P➔?➔
➔A➔R➔P➔ ➔m➔a➔p➔s➔ ➔a➔ ➔d➔e➔v➔i➔c➔e➔'➔s➔ ➔I➔P➔ ➔a➔d➔d➔r➔e➔s➔s➔ ➔(➔L➔a➔y➔e➔r➔ ➔3➔)➔ ➔t➔o➔ ➔i➔t➔s➔ ➔M➔A➔C➔ ➔a➔d➔d➔r➔e➔s➔s➔ ➔(➔L➔a➔y➔e➔r➔ ➔2➔)➔.➔ ➔W➔h➔e➔n➔ ➔a➔ ➔d➔e➔v➔i➔c➔e➔ ➔w➔a➔n➔t➔s➔ ➔t➔o➔ ➔c➔o➔m➔m➔u➔n➔i➔c➔a➔t➔e➔
➔o➔n➔ ➔t➔h➔e➔ ➔s➔a➔m➔e➔ ➔l➔o➔c➔a➔l➔ ➔n➔e➔t➔w➔o➔r➔k➔,➔ ➔i➔t➔ ➔u➔s➔e➔s➔ ➔A➔R➔P➔ ➔t➔o➔ ➔f➔i➔n➔d➔ ➔t➔h➔e➔ ➔r➔e➔c➔i➔p➔i➔e➔n➔t➔'➔s➔ ➔M➔A➔C➔ ➔a➔d➔d➔r➔e➔s➔s➔.➔
➔D➔e➔v➔i➔c➔e➔ ➔A➔ ➔w➔a➔n➔t➔s➔ ➔t➔o➔ ➔t➔a➔l➔k➔ ➔t➔o➔ ➔1➔9➔2➔.➔1➔6➔8➔.➔1➔.➔1➔0➔
➔A➔R➔P➔ ➔b➔r➔o➔a➔d➔c➔a➔s➔t➔:➔ ➔"➔W➔h➔o➔ ➔h➔a➔s➔ ➔1➔9➔2➔.➔1➔6➔8➔.➔1➔.➔1➔0➔?➔"➔
➔
➔
➔
➔
➔D➔e➔v➔i➔c➔e➔ ➔B➔ ➔r➔e➔p➔l➔i➔e➔s➔:➔ ➔"➔I➔ ➔d➔o➔!➔ ➔M➔y➔ ➔M➔A➔C➔ ➔i➔s➔ ➔A➔A➔:➔B➔B➔:➔C➔C➔:➔D➔D➔:➔E➔E➔:➔F➔F➔"➔
➔D➔e➔v➔i➔c➔e➔ ➔A➔ ➔s➔e➔n➔d➔s➔ ➔d➔a➔t➔a➔ ➔t➔o➔ ➔t➔h➔a➔t➔ ➔M➔A➔C➔
➔8➔.➔ ➔P➔I➔N➔G➔
➔P➔I➔N➔G➔ ➔u➔s➔e➔s➔ ➔I➔C➔M➔P➔ ➔(➔I➔n➔t➔e➔r➔n➔e➔t➔ ➔C➔o➔n➔t➔r➔o➔l➔ ➔M➔e➔s➔s➔a➔g➔e➔ ➔P➔r➔o➔t➔o➔c➔o➔l➔)➔ ➔t➔o➔ ➔t➔e➔s➔t➔ ➔r➔e➔a➔c➔h➔a➔b➔i➔l➔i➔t➔y➔ ➔o➔f➔ ➔a➔ ➔h➔o➔s➔t➔.➔
➔S➔e➔n➔d➔s➔ ➔e➔c➔h➔o➔ ➔r➔e➔q➔u➔e➔s➔t➔ ➔→➔ ➔w➔a➔i➔t➔s➔ ➔f➔o➔r➔ ➔e➔c➔h➔o➔ ➔r➔e➔p➔l➔y➔
➔M➔e➔a➔s➔u➔r➔e➔s➔ ➔r➔o➔u➔n➔d➔ ➔t➔r➔i➔p➔ ➔t➔i➔m➔e➔ ➔(➔R➔T➔T➔)➔
➔T➔e➔s➔t➔s➔ ➔c➔o➔n➔n➔e➔c➔t➔i➔v➔i➔t➔y➔ ➔a➔n➔d➔ ➔l➔a➔t➔e➔n➔c➔y➔
➔p➔i➔n➔g➔ ➔g➔o➔o➔g➔l➔e➔.➔c➔o➔m➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔t➔e➔s➔t➔ ➔c➔o➔n➔n➔e➔c➔t➔i➔v➔i➔t➔y➔
➔p➔i➔n➔g➔ ➔-➔c➔ ➔4➔ ➔g➔o➔o➔g➔l➔e➔.➔c➔o➔m➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔i➔n➔g➔ ➔4➔ ➔t➔i➔m➔e➔s➔ ➔o➔n➔l➔y➔
➔p➔i➔n➔g➔ ➔-➔i➔ ➔0➔.➔5➔ ➔g➔o➔o➔g➔l➔e➔.➔c➔o➔m➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔#➔ ➔p➔i➔n➔g➔ ➔e➔v➔e➔r➔y➔ ➔0➔.➔5➔ ➔s➔e➔c➔o➔n➔d➔s➔
➔9➔.➔ ➔D➔H➔C➔P➔ ➔—➔ ➔D➔y➔n➔a➔m➔i➔c➔ ➔H➔o➔s➔t➔ ➔C➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔ ➔P➔r➔o➔t➔o➔c➔o➔l➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔D➔H➔C➔P➔?➔
➔D➔H➔C➔P➔ ➔a➔u➔t➔o➔m➔a➔t➔i➔c➔a➔l➔l➔y➔ ➔a➔s➔s➔i➔g➔n➔s➔ ➔I➔P➔ ➔a➔d➔d➔r➔e➔s➔s➔e➔s➔ ➔a➔n➔d➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔ ➔(➔s➔u➔b➔n➔e➔t➔ ➔m➔a➔s➔k➔,➔ ➔g➔a➔t➔e➔w➔a➔y➔,➔ ➔D➔N➔S➔)➔ ➔t➔o➔ ➔d➔e➔v➔i➔c➔e➔s➔.➔
➔E➔l➔i➔m➔i➔n➔a➔t➔e➔s➔ ➔m➔a➔n➔u➔a➔l➔ ➔c➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔.➔
➔D➔O➔R➔A➔ ➔P➔r➔o➔c➔e➔s➔s➔ ➔(➔h➔o➔w➔ ➔D➔H➔C➔P➔ ➔w➔o➔r➔k➔s➔)➔:➔
➔C➔l➔i➔e➔n➔t➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔D➔H➔C➔P➔ ➔S➔e➔r➔v➔e➔r➔
➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔ ➔ ➔│➔─➔─➔ ➔D➔I➔S➔C➔O➔V➔E➔R➔ ➔(➔b➔r➔o➔a➔d➔c➔a➔s➔t➔)➔ ➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔ ➔▶➔ ➔│➔ ➔ ➔"➔I➔ ➔n➔e➔e➔d➔ ➔a➔n➔ ➔I➔P➔ ➔a➔d➔d➔r➔e➔s➔s➔!➔"➔
➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔ ➔ ➔│➔ ➔◀➔ ➔─➔─➔ ➔O➔F➔F➔E➔R➔ ➔(➔u➔n➔i➔c➔a➔s➔t➔)➔ ➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔│➔ ➔ ➔"➔H➔o➔w➔ ➔a➔b➔o➔u➔t➔ ➔1➔9➔2➔.➔1➔6➔8➔.➔1➔.➔1➔0➔0➔?➔"➔
➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔ ➔ ➔│➔─➔─➔ ➔R➔E➔Q➔U➔E➔S➔T➔ ➔(➔b➔r➔o➔a➔d➔c➔a➔s➔t➔)➔ ➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔ ➔▶➔ ➔│➔ ➔ ➔"➔Y➔e➔s➔,➔ ➔I➔'➔l➔l➔ ➔t➔a➔k➔e➔ ➔t➔h➔a➔t➔ ➔I➔P➔"➔
➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔ ➔ ➔│➔ ➔◀➔ ➔─➔─➔ ➔A➔C➔K➔ ➔(➔u➔n➔i➔c➔a➔s➔t➔)➔ ➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔─➔│➔ ➔ ➔"➔I➔t➔'➔s➔ ➔y➔o➔u➔r➔s➔!➔ ➔H➔e➔r➔e➔'➔s➔ ➔y➔o➔u➔r➔ ➔c➔o➔n➔f➔i➔g➔"➔
➔ ➔ ➔│➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔ ➔ ➔│➔ ➔ ➔I➔P➔ ➔a➔s➔s➔i➔g➔n➔e➔d➔!➔ ➔ ➔1➔9➔2➔.➔1➔6➔8➔.➔1➔.➔1➔0➔0➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔│➔
➔D➔O➔R➔A➔ ➔=➔ ➔D➔i➔s➔c➔o➔v➔e➔r➔ ➔→➔ ➔O➔f➔f➔e➔r➔ ➔→➔ ➔R➔e➔q➔u➔e➔s➔t➔ ➔→➔ ➔A➔c➔k➔n➔o➔w➔l➔e➔d➔g➔e➔
➔W➔h➔y➔ ➔D➔H➔C➔P➔?➔
➔
➔
➔
➔
➔A➔u➔t➔o➔m➔a➔t➔i➔o➔n➔ ➔—➔ ➔n➔o➔ ➔m➔a➔n➔u➔a➔l➔ ➔I➔P➔ ➔a➔s➔s➔i➔g➔n➔m➔e➔n➔t➔
➔E➔r➔r➔o➔r➔ ➔P➔r➔e➔v➔e➔n➔t➔i➔o➔n➔ ➔—➔ ➔n➔o➔ ➔d➔u➔p➔l➔i➔c➔a➔t➔e➔ ➔I➔P➔s➔
➔C➔e➔n➔t➔r➔a➔l➔ ➔M➔a➔n➔a➔g➔e➔m➔e➔n➔t➔ ➔—➔ ➔m➔a➔n➔a➔g➔e➔ ➔a➔l➔l➔ ➔I➔P➔s➔ ➔f➔r➔o➔m➔ ➔o➔n➔e➔ ➔p➔l➔a➔c➔e➔
➔1➔0➔.➔ ➔N➔e➔t➔w➔o➔r➔k➔ ➔P➔e➔r➔f➔o➔r➔m➔a➔n➔c➔e➔ ➔M➔e➔t➔r➔i➔c➔s➔
➔M➔e➔t➔r➔i➔c➔ ➔D➔e➔f➔i➔n➔i➔t➔i➔o➔n➔
➔B➔a➔n➔d➔w➔i➔d➔t➔h➔ ➔M➔a➔x➔i➔m➔u➔m➔ ➔r➔a➔t➔e➔ ➔d➔a➔t➔a➔ ➔c➔a➔n➔ ➔t➔r➔a➔n➔s➔f➔e➔r➔ ➔(➔b➔i➔t➔s➔ ➔p➔e➔r➔ ➔s➔e➔c➔o➔n➔d➔)➔.➔ ➔C➔a➔p➔a➔c➔i➔t➔y➔ ➔o➔f➔ ➔t➔h➔e➔ ➔c➔o➔n➔n➔e➔c➔t➔i➔o➔n➔.➔
➔L➔a➔t➔e➔n➔c➔y➔ ➔T➔i➔m➔e➔ ➔f➔o➔r➔ ➔d➔a➔t➔a➔ ➔t➔o➔ ➔t➔r➔a➔v➔e➔l➔ ➔f➔r➔o➔m➔ ➔s➔o➔u➔r➔c➔e➔ ➔t➔o➔ ➔d➔e➔s➔t➔i➔n➔a➔t➔i➔o➔n➔.➔ ➔L➔o➔w➔e➔r➔ ➔=➔ ➔f➔a➔s➔t➔e➔r➔.➔
➔R➔T➔T➔ ➔(➔R➔o➔u➔n➔d➔ ➔T➔r➔i➔p➔ ➔T➔i➔m➔e➔)➔ ➔T➔i➔m➔e➔ ➔f➔o➔r➔ ➔p➔a➔c➔k➔e➔t➔ ➔t➔o➔ ➔g➔o➔ ➔t➔o➔ ➔d➔e➔s➔t➔i➔n➔a➔t➔i➔o➔n➔ ➔A➔N➔D➔ ➔c➔o➔m➔e➔ ➔b➔a➔c➔k➔.➔
➔M➔T➔U➔ ➔(➔M➔a➔x➔ ➔T➔r➔a➔n➔s➔m➔i➔s➔s➔i➔o➔n➔ ➔U➔n➔i➔t➔)➔ ➔L➔a➔r➔g➔e➔s➔t➔ ➔p➔a➔c➔k➔e➔t➔ ➔s➔i➔z➔e➔ ➔t➔h➔a➔t➔ ➔c➔a➔n➔ ➔b➔e➔ ➔t➔r➔a➔n➔s➔m➔i➔t➔t➔e➔d➔ ➔(➔t➔y➔p➔i➔c➔a➔l➔l➔y➔ ➔1➔5➔0➔0➔ ➔b➔y➔t➔e➔s➔ ➔o➔n➔ ➔E➔t➔h➔e➔r➔n➔e➔t➔)➔.➔
➔T➔h➔r➔o➔u➔g➔h➔p➔u➔t➔ ➔A➔c➔t➔u➔a➔l➔ ➔d➔a➔t➔a➔ ➔t➔r➔a➔n➔s➔f➔e➔r➔r➔e➔d➔ ➔i➔n➔ ➔a➔ ➔g➔i➔v➔e➔n➔ ➔t➔i➔m➔e➔ ➔(➔v➔s➔ ➔b➔a➔n➔d➔w➔i➔d➔t➔h➔ ➔w➔h➔i➔c➔h➔ ➔i➔s➔ ➔m➔a➔x➔i➔m➔u➔m➔)➔.➔
➔J➔i➔t➔t➔e➔r➔ ➔V➔a➔r➔i➔a➔t➔i➔o➔n➔ ➔i➔n➔ ➔l➔a➔t➔e➔n➔c➔y➔ ➔o➔v➔e➔r➔ ➔t➔i➔m➔e➔.➔ ➔H➔i➔g➔h➔ ➔j➔i➔t➔t➔e➔r➔ ➔c➔a➔u➔s➔e➔s➔ ➔c➔h➔o➔p➔p➔y➔ ➔a➔u➔d➔i➔o➔/➔v➔i➔d➔e➔o➔.➔
➔1➔1➔.➔ ➔I➔P➔v➔4➔ ➔v➔s➔ ➔I➔P➔v➔6➔
➔I➔P➔v➔4➔ ➔—➔ ➔3➔2➔-➔b➔i➔t➔ ➔a➔d➔d➔r➔e➔s➔s➔e➔s➔,➔ ➔~➔4➔.➔3➔ ➔b➔i➔l➔l➔i➔o➔n➔ ➔a➔d➔d➔r➔e➔s➔s➔e➔s➔.➔ ➔R➔u➔n➔n➔i➔n➔g➔ ➔o➔u➔t➔!➔
➔I➔P➔v➔6➔ ➔—➔ ➔1➔2➔8➔-➔b➔i➔t➔ ➔a➔d➔d➔r➔e➔s➔s➔e➔s➔,➔ ➔~➔3➔4➔0➔ ➔u➔n➔d➔e➔c➔i➔l➔l➔i➔o➔n➔ ➔a➔d➔d➔r➔e➔s➔s➔e➔s➔.➔ ➔T➔h➔e➔ ➔f➔u➔t➔u➔r➔e➔.➔
➔F➔e➔a➔t➔u➔r➔e➔ ➔I➔P➔v➔4➔ ➔I➔P➔v➔6➔
➔A➔d➔d➔r➔e➔s➔s➔ ➔L➔e➔n➔g➔t➔h➔ ➔3➔2➔ ➔b➔i➔t➔s➔ ➔(➔4➔ ➔o➔c➔t➔e➔t➔s➔)➔ ➔1➔2➔8➔ ➔b➔i➔t➔s➔ ➔(➔8➔ ➔o➔c➔t➔e➔t➔s➔)➔
➔F➔o➔r➔m➔a➔t➔ ➔D➔e➔c➔i➔m➔a➔l➔ ➔d➔o➔t➔s➔ ➔(➔1➔9➔2➔.➔1➔6➔8➔.➔0➔.➔1➔)➔ ➔H➔e➔x➔ ➔c➔o➔l➔o➔n➔s➔ ➔(➔2➔0➔0➔1➔:➔0➔d➔b➔8➔:➔:➔7➔3➔3➔4➔)➔
➔T➔o➔t➔a➔l➔ ➔A➔d➔d➔r➔e➔s➔s➔e➔s➔ ➔~➔4➔.➔3➔ ➔b➔i➔l➔l➔i➔o➔n➔ ➔~➔3➔4➔0➔ ➔u➔n➔d➔e➔c➔i➔l➔l➔i➔o➔n➔ ➔(➔2➔^➔1➔2➔8➔)➔
➔N➔A➔T➔ ➔R➔e➔q➔u➔i➔r➔e➔d➔ ➔Y➔e➔s➔ ➔(➔t➔o➔ ➔e➔x➔t➔e➔n➔d➔ ➔a➔d➔d➔r➔e➔s➔s➔ ➔s➔p➔a➔c➔e➔)➔ ➔N➔o➔ ➔(➔e➔n➔o➔u➔g➔h➔ ➔a➔d➔d➔r➔e➔s➔s➔e➔s➔ ➔f➔o➔r➔ ➔a➔l➔l➔)➔
➔S➔e➔c➔u➔r➔i➔t➔y➔ ➔N➔o➔ ➔b➔u➔i➔l➔t➔-➔i➔n➔ ➔(➔n➔e➔e➔d➔s➔ ➔I➔P➔s➔e➔c➔)➔ ➔B➔u➔i➔l➔t➔-➔i➔n➔ ➔I➔P➔s➔e➔c➔ ➔s➔u➔p➔p➔o➔r➔t➔
➔C➔o➔n➔f➔i➔g➔u➔r➔a➔t➔i➔o➔n➔ ➔M➔a➔n➔u➔a➔l➔ ➔o➔r➔ ➔D➔H➔C➔P➔ ➔A➔u➔t➔o➔-➔c➔o➔n➔f➔i➔g➔ ➔(➔S➔L➔A➔A➔C➔)➔ ➔o➔r➔ ➔D➔H➔C➔P➔v➔6➔
➔B➔r➔o➔a➔d➔c➔a➔s➔t➔ ➔S➔u➔p➔p➔o➔r➔t➔e➔d➔ ➔N➔o➔ ➔b➔r➔o➔a➔d➔c➔a➔s➔t➔ ➔(➔u➔s➔e➔s➔ ➔M➔u➔l➔t➔i➔c➔a➔s➔t➔/➔A➔n➔y➔c➔a➔s➔t➔)➔
➔
➔
➔
➔
➔➔ ➔➔
➔H➔e➔a➔d➔e➔r➔ ➔C➔o➔m➔p➔l➔e➔x➔ ➔S➔i➔m➔p➔l➔i➔f➔i➔e➔d➔ ➔(➔f➔a➔s➔t➔e➔r➔ ➔p➔r➔o➔c➔e➔s➔s➔i➔n➔g➔)➔
➔1➔2➔.➔ ➔I➔P➔ ➔A➔d➔d➔r➔e➔s➔s➔ ➔C➔l➔a➔s➔s➔e➔s➔
➔C➔l➔a➔s➔s➔ ➔A➔:➔ ➔1➔.➔0➔.➔0➔.➔0➔ ➔ ➔ ➔ ➔–➔ ➔1➔2➔6➔.➔0➔.➔0➔.➔0➔ ➔ ➔ ➔ ➔M➔a➔s➔k➔:➔ ➔2➔5➔5➔.➔0➔.➔0➔.➔0➔ ➔ ➔ ➔ ➔ ➔N➔e➔t➔w➔o➔r➔k➔s➔:➔ ➔1➔2➔6➔ ➔ ➔ ➔ ➔ ➔ ➔H➔o➔s➔t➔s➔:➔ ➔1➔6➔,➔7➔7➔
➔C➔l➔a➔s➔s➔ ➔B➔:➔ ➔1➔2➔8➔.➔0➔.➔0➔.➔0➔ ➔ ➔–➔ ➔1➔9➔1➔.➔0➔.➔0➔.➔0➔ ➔ ➔ ➔ ➔M➔a➔s➔k➔:➔ ➔2➔5➔5➔.➔2➔5➔5➔.➔0➔.➔0➔ ➔ ➔ ➔N➔e➔t➔w➔o➔r➔k➔s➔:➔ ➔1➔6➔,➔3➔8➔4➔ ➔ ➔ ➔H➔o➔s➔t➔s➔:➔ ➔6➔5➔,➔5➔3➔
➔C➔l➔a➔s➔s➔ ➔C➔:➔ ➔1➔9➔2➔.➔0➔.➔0➔.➔0➔ ➔ ➔–➔ ➔2➔2➔3➔.➔0➔.➔0➔.➔0➔ ➔ ➔ ➔ ➔M➔a➔s➔k➔:➔ ➔2➔5➔5➔.➔2➔5➔5➔.➔2➔5➔5➔.➔0➔ ➔N➔e➔t➔w➔o➔r➔k➔s➔:➔ ➔2➔,➔0➔9➔7➔,➔1➔5➔2➔ ➔H➔o➔s➔t➔s➔:➔ ➔2➔5➔4➔
➔S➔p➔e➔c➔i➔a➔l➔:➔
➔1➔2➔7➔.➔0➔.➔0➔.➔1➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔ ➔=➔ ➔L➔o➔o➔p➔b➔a➔c➔k➔ ➔(➔l➔o➔c➔a➔l➔h➔o➔s➔t➔)➔
➔2➔5➔5➔.➔2➔5➔5➔.➔2➔5➔5➔.➔2➔5➔5➔ ➔ ➔=➔ ➔B➔r➔o➔a➔d➔c➔a➔s➔t➔
➔P➔r➔i➔v➔a➔t➔e➔ ➔I➔P➔ ➔R➔a➔n➔g➔e➔s➔ ➔(➔n➔o➔t➔ ➔r➔o➔u➔t➔a➔b➔l➔e➔ ➔o➔n➔ ➔i➔n➔t➔e➔r➔n➔e➔t➔)➔:➔
➔C➔l➔a➔s➔s➔ ➔A➔:➔ ➔1➔0➔.➔0➔.➔0➔.➔0➔ ➔ ➔ ➔ ➔–➔ ➔1➔0➔.➔2➔5➔5➔.➔2➔5➔5➔.➔2➔5➔5➔
➔C➔l➔a➔s➔s➔ ➔B➔:➔ ➔1➔7➔2➔.➔1➔6➔.➔0➔.➔0➔ ➔ ➔–➔ ➔1➔7➔2➔.➔3➔1➔.➔2➔5➔5➔.➔2➔5➔5➔
➔C➔l➔a➔s➔s➔ ➔C➔:➔ ➔1➔9➔2➔.➔1➔6➔8➔.➔0➔.➔0➔ ➔–➔ ➔1➔9➔2➔.➔1➔6➔8➔.➔2➔5➔5➔.➔2➔5➔5➔
➔A➔P➔I➔P➔A➔ ➔(➔A➔u➔t➔o➔m➔a➔t➔i➔c➔ ➔P➔r➔i➔v➔a➔t➔e➔ ➔I➔P➔ ➔A➔d➔d➔r➔e➔s➔s➔i➔n➔g➔)➔:➔
➔I➔f➔ ➔a➔ ➔d➔e➔v➔i➔c➔e➔ ➔f➔a➔i➔l➔s➔ ➔t➔o➔ ➔g➔e➔t➔ ➔a➔n➔ ➔I➔P➔ ➔f➔r➔o➔m➔ ➔D➔H➔C➔P➔,➔ ➔i➔t➔ ➔a➔s➔s➔i➔g➔n➔s➔ ➔i➔t➔s➔e➔l➔f➔ ➔a➔n➔ ➔a➔d➔d➔r➔e➔s➔s➔ ➔i➔n➔ ➔t➔h➔e➔ ➔1➔6➔9➔.➔2➔5➔4➔.➔0➔.➔0➔/➔1➔6➔ ➔r➔a➔n➔g➔e➔.➔ ➔T➔h➔i➔s➔ ➔a➔l➔l➔o➔w➔s➔
➔l➔o➔c➔a➔l➔ ➔c➔o➔m➔m➔u➔n➔i➔c➔a➔t➔i➔o➔n➔ ➔b➔u➔t➔ ➔N➔O➔T➔ ➔i➔n➔t➔e➔r➔n➔e➔t➔ ➔a➔c➔c➔e➔s➔s➔.➔
➔1➔3➔.➔ ➔C➔o➔m➔m➔o➔n➔ ➔P➔o➔r➔t➔s➔ ➔a➔n➔d➔ ➔P➔r➔o➔t➔o➔c➔o➔l➔s➔
➔P➔o➔r➔t➔ ➔P➔r➔o➔t➔o➔c➔o➔l➔ ➔S➔e➔r➔v➔i➔c➔e➔
➔2➔2➔ ➔T➔C➔P➔ ➔S➔S➔H➔ ➔—➔ ➔s➔e➔c➔u➔r➔e➔ ➔r➔e➔m➔o➔t➔e➔ ➔a➔c➔c➔e➔s➔s➔
➔2➔3➔ ➔T➔C➔P➔ ➔T➔e➔l➔n➔e➔t➔ ➔—➔ ➔i➔n➔s➔e➔c➔u➔r➔e➔ ➔r➔e➔m➔o➔t➔e➔ ➔a➔c➔c➔e➔s➔s➔
➔2➔5➔ ➔T➔C➔P➔ ➔S➔M➔T➔P➔ ➔—➔ ➔e➔m➔a➔i➔l➔ ➔s➔e➔n➔d➔i➔n➔g➔
➔5➔3➔ ➔T➔C➔P➔/➔U➔D➔P➔ ➔D➔N➔S➔ ➔—➔ ➔d➔o➔m➔a➔i➔n➔ ➔n➔a➔m➔e➔ ➔r➔e➔s➔o➔l➔u➔t➔i➔o➔n➔
➔6➔7➔/➔6➔8➔ ➔U➔D➔P➔ ➔D➔H➔C➔P➔ ➔—➔ ➔I➔P➔ ➔a➔d➔d➔r➔e➔s➔s➔ ➔a➔s➔s➔i➔g➔n➔m➔e➔n➔t➔
➔8➔0➔ ➔T➔C➔P➔ ➔H➔T➔T➔P➔ ➔—➔ ➔w➔e➔b➔ ➔t➔r➔a➔f➔f➔i➔c➔
➔4➔4➔3➔ ➔T➔C➔P➔ ➔H➔T➔T➔P➔S➔ ➔—➔ ➔s➔e➔c➔u➔r➔e➔ ➔w➔e➔b➔ ➔t➔r➔a➔f➔f➔i➔c➔
➔
➔
➔
➔
➔3➔3➔0➔6➔ ➔T➔C➔P➔ ➔M➔y➔S➔Q➔L➔ ➔d➔a➔t➔a➔b➔a➔s➔e➔
➔5➔4➔3➔2➔ ➔T➔C➔P➔ ➔P➔o➔s➔t➔g➔r➔e➔S➔Q➔L➔ ➔d➔a➔t➔a➔b➔a➔s➔e➔
➔6➔4➔4➔3➔ ➔T➔C➔P➔ ➔K➔u➔b➔e➔r➔n➔e➔t➔e➔s➔ ➔A➔P➔I➔ ➔s➔e➔r➔v➔e➔r➔
➔2➔3➔7➔9➔/➔2➔3➔8➔0➔ ➔T➔C➔P➔ ➔e➔t➔c➔d➔
➔1➔0➔2➔5➔0➔ ➔T➔C➔P➔ ➔k➔u➔b➔e➔l➔e➔t➔ ➔A➔P➔I➔
➔8➔0➔8➔0➔ ➔T➔C➔P➔ ➔H➔T➔T➔P➔ ➔a➔l➔t➔e➔r➔n➔a➔t➔e➔ ➔(➔T➔o➔m➔c➔a➔t➔,➔ ➔J➔e➔n➔k➔i➔n➔s➔)➔
➔S➔S➔H➔ ➔v➔s➔ ➔T➔e➔l➔n➔e➔t➔:➔
➔S➔S➔H➔ ➔T➔e➔l➔n➔e➔t➔
➔P➔o➔r➔t➔ ➔2➔2➔ ➔2➔3➔
➔E➔n➔c➔r➔y➔p➔t➔i➔o➔n➔ ➔Y➔e➔s➔ ➔N➔o➔ ➔(➔p➔l➔a➔i➔n➔ ➔t➔e➔x➔t➔)➔
➔S➔e➔c➔u➔r➔i➔t➔y➔ ➔S➔e➔c➔u➔r➔e➔ ➔I➔n➔s➔e➔c➔u➔r➔e➔
➔U➔s➔e➔ ➔t➔o➔d➔a➔y➔ ➔A➔l➔w➔a➔y➔s➔ ➔p➔r➔e➔f➔e➔r➔r➔e➔d➔ ➔N➔e➔v➔e➔r➔ ➔i➔n➔ ➔p➔r➔o➔d➔u➔c➔t➔i➔o➔n➔
➔1➔4➔.➔ ➔N➔e➔t➔w➔o➔r➔k➔ ➔D➔e➔v➔i➔c➔e➔s➔
➔D➔e➔v➔i➔c➔e➔ ➔O➔S➔I➔ ➔L➔a➔y➔e➔r➔ ➔H➔o➔w➔ ➔i➔t➔ ➔w➔o➔r➔k➔s➔
➔H➔u➔b➔ ➔L➔a➔y➔e➔r➔ ➔1➔ ➔(➔P➔h➔y➔s➔i➔c➔a➔l➔)➔ ➔B➔r➔o➔a➔d➔c➔a➔s➔t➔s➔ ➔a➔l➔l➔ ➔d➔a➔t➔a➔ ➔t➔o➔ ➔A➔L➔L➔ ➔p➔o➔r➔t➔s➔.➔ ➔D➔u➔m➔b➔,➔ ➔n➔o➔ ➔i➔n➔t➔e➔l➔l➔i➔g➔e➔n➔c➔e➔.➔
➔S➔w➔i➔t➔c➔h➔ ➔L➔a➔y➔e➔r➔ ➔2➔ ➔(➔D➔a➔t➔a➔ ➔L➔i➔n➔k➔)➔ ➔F➔o➔r➔w➔a➔r➔d➔s➔ ➔d➔a➔t➔a➔ ➔t➔o➔ ➔S➔P➔E➔C➔I➔F➔I➔C➔ ➔d➔e➔v➔i➔c➔e➔ ➔u➔s➔i➔n➔g➔ ➔M➔A➔C➔ ➔a➔d➔d➔r➔e➔s➔s➔.➔ ➔I➔n➔t➔e➔l➔l➔i➔g➔e➔n➔t➔.➔
➔R➔o➔u➔t➔e➔r➔ ➔L➔a➔y➔e➔r➔ ➔3➔ ➔(➔N➔e➔t➔w➔o➔r➔k➔)➔ ➔R➔o➔u➔t➔e➔s➔ ➔p➔a➔c➔k➔e➔t➔s➔ ➔b➔e➔t➔w➔e➔e➔n➔ ➔D➔I➔F➔F➔E➔R➔E➔N➔T➔ ➔n➔e➔t➔w➔o➔r➔k➔s➔ ➔u➔s➔i➔n➔g➔ ➔I➔P➔ ➔a➔d➔d➔r➔e➔s➔s➔e➔s➔.➔
➔F➔i➔r➔e➔w➔a➔l➔l➔ ➔L➔a➔y➔e➔r➔ ➔3➔-➔7➔ ➔F➔i➔l➔t➔e➔r➔s➔ ➔t➔r➔a➔f➔f➔i➔c➔ ➔b➔a➔s➔e➔d➔ ➔o➔n➔ ➔r➔u➔l➔e➔s➔.➔ ➔P➔e➔r➔m➔i➔t➔s➔ ➔o➔r➔ ➔d➔e➔n➔i➔e➔s➔ ➔b➔a➔s➔e➔d➔ ➔o➔n➔ ➔p➔o➔l➔i➔c➔i➔e➔s➔.➔
➔H➔u➔b➔ ➔v➔s➔ ➔S➔w➔i➔t➔c➔h➔ ➔v➔s➔ ➔R➔o➔u➔t➔e➔r➔:➔
➔H➔u➔b➔:➔ ➔ ➔ ➔ ➔ ➔A➔ ➔s➔h➔o➔u➔t➔s➔ ➔→➔ ➔e➔v➔e➔r➔y➔o➔n➔e➔ ➔h➔e➔a➔r➔s➔ ➔(➔b➔r➔o➔a➔d➔c➔a➔s➔t➔ ➔t➔o➔ ➔a➔l➔l➔)➔
➔S➔w➔i➔t➔c➔h➔:➔ ➔ ➔A➔ ➔s➔h➔o➔u➔t➔s➔ ➔→➔ ➔o➔n➔l➔y➔ ➔B➔ ➔h➔e➔a➔r➔s➔ ➔(➔t➔a➔r➔g➔e➔t➔e➔d➔ ➔b➔y➔ ➔M➔A➔C➔)➔
➔R➔o➔u➔t➔e➔r➔:➔ ➔ ➔A➔ ➔s➔e➔n➔d➔s➔ ➔t➔o➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔t➔ ➔c➔i➔t➔y➔ ➔→➔ ➔r➔o➔u➔t➔e➔r➔ ➔f➔i➔n➔d➔s➔ ➔t➔h➔e➔ ➔p➔a➔t➔h➔ ➔(➔r➔o➔u➔t➔i➔n➔g➔ ➔b➔y➔ ➔I➔P➔)➔
➔C➔a➔n➔ ➔y➔o➔u➔ ➔r➔e➔p➔l➔a➔c➔e➔ ➔a➔ ➔R➔o➔u➔t➔e➔r➔ ➔w➔i➔t➔h➔ ➔a➔ ➔S➔w➔i➔t➔c➔h➔?➔
➔
➔
➔
➔
➔N➔o➔.➔ ➔T➔h➔e➔y➔ ➔s➔e➔r➔v➔e➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔t➔ ➔p➔u➔r➔p➔o➔s➔e➔s➔.➔ ➔R➔o➔u➔t➔e➔r➔ ➔=➔ ➔b➔e➔t➔w➔e➔e➔n➔ ➔n➔e➔t➔w➔o➔r➔k➔s➔ ➔(➔L➔a➔y➔e➔r➔ ➔3➔)➔.➔ ➔S➔w➔i➔t➔c➔h➔ ➔=➔ ➔w➔i➔t➔h➔i➔n➔ ➔a➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔(➔L➔a➔y➔e➔r➔ ➔2➔)➔.➔
➔S➔o➔m➔e➔ ➔L➔a➔y➔e➔r➔ ➔3➔ ➔s➔w➔i➔t➔c➔h➔e➔s➔ ➔c➔a➔n➔ ➔d➔o➔ ➔l➔i➔m➔i➔t➔e➔d➔ ➔r➔o➔u➔t➔i➔n➔g➔ ➔b➔u➔t➔ ➔d➔o➔n➔'➔t➔ ➔r➔e➔p➔l➔a➔c➔e➔ ➔a➔ ➔f➔u➔l➔l➔ ➔r➔o➔u➔t➔e➔r➔.➔
➔1➔5➔.➔ ➔N➔A➔T➔ ➔—➔ ➔N➔e➔t➔w➔o➔r➔k➔ ➔A➔d➔d➔r➔e➔s➔s➔ ➔T➔r➔a➔n➔s➔l➔a➔t➔i➔o➔n➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔N➔A➔T➔?➔
➔C➔o➔n➔v➔e➔r➔t➔s➔ ➔p➔r➔i➔v➔a➔t➔e➔ ➔I➔P➔ ➔a➔d➔d➔r➔e➔s➔s➔e➔s➔ ➔t➔o➔ ➔p➔u➔b➔l➔i➔c➔ ➔I➔P➔ ➔a➔d➔d➔r➔e➔s➔s➔e➔s➔ ➔f➔o➔r➔ ➔i➔n➔t➔e➔r➔n➔e➔t➔ ➔a➔c➔c➔e➔s➔s➔.➔ ➔C➔o➔n➔s➔e➔r➔v➔e➔s➔ ➔p➔u➔b➔l➔i➔c➔ ➔I➔P➔s➔ ➔a➔n➔d➔ ➔a➔d➔d➔s➔ ➔s➔e➔c➔u➔r➔i➔t➔y➔
➔b➔y➔ ➔h➔i➔d➔i➔n➔g➔ ➔i➔n➔t➔e➔r➔n➔a➔l➔ ➔a➔d➔d➔r➔e➔s➔s➔e➔s➔.➔
➔T➔y➔p➔e➔s➔ ➔o➔f➔ ➔N➔A➔T➔:➔
➔T➔y➔p➔e➔ ➔H➔o➔w➔ ➔i➔t➔ ➔w➔o➔r➔k➔s➔
➔S➔t➔a➔t➔i➔c➔ ➔N➔A➔T➔ ➔O➔n➔e➔ ➔p➔r➔i➔v➔a➔t➔e➔ ➔I➔P➔ ➔→➔ ➔o➔n➔e➔ ➔p➔u➔b➔l➔i➔c➔ ➔I➔P➔ ➔(➔1➔:➔1➔ ➔m➔a➔p➔p➔i➔n➔g➔)➔
➔D➔y➔n➔a➔m➔i➔c➔ ➔N➔A➔T➔ ➔M➔u➔l➔t➔i➔p➔l➔e➔ ➔p➔r➔i➔v➔a➔t➔e➔ ➔I➔P➔s➔ ➔→➔ ➔p➔o➔o➔l➔ ➔o➔f➔ ➔p➔u➔b➔l➔i➔c➔ ➔I➔P➔s➔
➔P➔A➔T➔ ➔(➔P➔o➔r➔t➔ ➔A➔d➔d➔r➔e➔s➔s➔
➔T➔r➔a➔n➔s➔l➔a➔t➔i➔o➔n➔)➔
➔M➔u➔l➔t➔i➔p➔l➔e➔ ➔p➔r➔i➔v➔a➔t➔e➔ ➔I➔P➔s➔ ➔→➔ ➔O➔N➔E➔ ➔p➔u➔b➔l➔i➔c➔ ➔I➔P➔ ➔u➔s➔i➔n➔g➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔t➔ ➔p➔o➔r➔t➔s➔.➔ ➔A➔l➔s➔o➔ ➔c➔a➔l➔l➔e➔d➔ ➔N➔A➔T➔
➔o➔v➔e➔r➔l➔o➔a➔d➔.➔ ➔M➔o➔s➔t➔ ➔c➔o➔m➔m➔o➔n➔.➔
➔A➔W➔S➔ ➔N➔A➔T➔ ➔G➔a➔t➔e➔w➔a➔y➔ ➔w➔o➔r➔k➔s➔ ➔e➔x➔a➔c➔t➔l➔y➔ ➔l➔i➔k➔e➔ ➔P➔A➔T➔ ➔—➔ ➔a➔l➔l➔o➔w➔s➔ ➔p➔r➔i➔v➔a➔t➔e➔ ➔s➔u➔b➔n➔e➔t➔ ➔i➔n➔s➔t➔a➔n➔c➔e➔s➔ ➔t➔o➔ ➔a➔c➔c➔e➔s➔s➔ ➔i➔n➔t➔e➔r➔n➔e➔t➔ ➔w➔h➔i➔l➔e➔ ➔b➔l➔o➔c➔k➔i➔n➔g➔
➔i➔n➔b➔o➔u➔n➔d➔ ➔c➔o➔n➔n➔e➔c➔t➔i➔o➔n➔s➔.➔
➔1➔6➔.➔ ➔V➔L➔A➔N➔ ➔—➔ ➔V➔i➔r➔t➔u➔a➔l➔ ➔L➔o➔c➔a➔l➔ ➔A➔r➔e➔a➔ ➔N➔e➔t➔w➔o➔r➔k➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔V➔L➔A➔N➔?➔
➔L➔o➔g➔i➔c➔a➔l➔l➔y➔ ➔s➔e➔g➔m➔e➔n➔t➔s➔ ➔a➔ ➔p➔h➔y➔s➔i➔c➔a➔l➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔i➔n➔t➔o➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔v➔i➔r➔t➔u➔a➔l➔ ➔n➔e➔t➔w➔o➔r➔k➔s➔.➔ ➔D➔e➔v➔i➔c➔e➔s➔ ➔i➔n➔ ➔d➔i➔f➔f➔e➔r➔e➔n➔t➔ ➔V➔L➔A➔N➔s➔ ➔c➔a➔n➔'➔t➔
➔c➔o➔m➔m➔u➔n➔i➔c➔a➔t➔e➔ ➔d➔i➔r➔e➔c➔t➔l➔y➔ ➔w➔i➔t➔h➔o➔u➔t➔ ➔r➔o➔u➔t➔i➔n➔g➔.➔
➔W➔h➔y➔ ➔u➔s➔e➔ ➔V➔L➔A➔N➔s➔?➔
➔S➔e➔c➔u➔r➔i➔t➔y➔ ➔—➔ ➔i➔s➔o➔l➔a➔t➔e➔ ➔s➔e➔n➔s➔i➔t➔i➔v➔e➔ ➔d➔e➔v➔i➔c➔e➔s➔ ➔(➔H➔R➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔s➔e➔p➔a➔r➔a➔t➔e➔ ➔f➔r➔o➔m➔ ➔D➔e➔v➔ ➔n➔e➔t➔w➔o➔r➔k➔)➔
➔P➔e➔r➔f➔o➔r➔m➔a➔n➔c➔e➔ ➔—➔ ➔r➔e➔d➔u➔c➔e➔ ➔b➔r➔o➔a➔d➔c➔a➔s➔t➔ ➔t➔r➔a➔f➔f➔i➔c➔ ➔b➔y➔ ➔l➔i➔m➔i➔t➔i➔n➔g➔ ➔t➔o➔ ➔s➔p➔e➔c➔i➔f➔i➔c➔ ➔V➔L➔A➔N➔s➔
➔O➔r➔g➔a➔n➔i➔z➔a➔t➔i➔o➔n➔ ➔—➔ ➔l➔o➔g➔i➔c➔a➔l➔l➔y➔ ➔s➔t➔r➔u➔c➔t➔u➔r➔e➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔r➔e➔g➔a➔r➔d➔l➔e➔s➔s➔ ➔o➔f➔ ➔p➔h➔y➔s➔i➔c➔a➔l➔ ➔l➔o➔c➔a➔t➔i➔o➔n➔
➔V➔L➔A➔N➔ ➔r➔e➔d➔u➔c➔e➔s➔ ➔b➔r➔o➔a➔d➔c➔a➔s➔t➔ ➔t➔r➔a➔f➔f➔i➔c➔ ➔b➔y➔ ➔d➔i➔v➔i➔d➔i➔n➔g➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔i➔n➔t➔o➔ ➔s➔m➔a➔l➔l➔e➔r➔ ➔b➔r➔o➔a➔d➔c➔a➔s➔t➔ ➔d➔o➔m➔a➔i➔n➔s➔.➔ ➔T➔r➔a➔f➔f➔i➔c➔ ➔i➔n➔ ➔V➔L➔A➔N➔ ➔1➔0➔
➔d➔o➔e➔s➔n➔'➔t➔ ➔r➔e➔a➔c➔h➔ ➔V➔L➔A➔N➔ ➔2➔0➔.➔
➔A➔c➔c➔e➔s➔s➔ ➔P➔o➔r➔t➔ ➔v➔s➔ ➔T➔r➔u➔n➔k➔ ➔P➔o➔r➔t➔:➔
➔
➔
➔
➔
➔A➔c➔c➔e➔s➔s➔ ➔P➔o➔r➔t➔ ➔T➔r➔u➔n➔k➔ ➔P➔o➔r➔t➔
➔V➔L➔A➔N➔s➔ ➔C➔a➔r➔r➔i➔e➔s➔ ➔O➔N➔E➔ ➔V➔L➔A➔N➔ ➔C➔a➔r➔r➔i➔e➔s➔ ➔M➔U➔L➔T➔I➔P➔L➔E➔ ➔V➔L➔A➔N➔s➔
➔U➔s➔e➔ ➔C➔o➔n➔n➔e➔c➔t➔ ➔e➔n➔d➔ ➔d➔e➔v➔i➔c➔e➔s➔ ➔(➔P➔C➔s➔)➔ ➔C➔o➔n➔n➔e➔c➔t➔ ➔s➔w➔i➔t➔c➔h➔e➔s➔ ➔t➔o➔ ➔s➔w➔i➔t➔c➔h➔e➔s➔/➔r➔o➔u➔t➔e➔r➔s➔
➔V➔L➔A➔N➔ ➔t➔a➔g➔g➔i➔n➔g➔ ➔R➔e➔m➔o➔v➔e➔d➔ ➔b➔e➔f➔o➔r➔e➔ ➔s➔e➔n➔d➔i➔n➔g➔ ➔t➔o➔ ➔d➔e➔v➔i➔c➔e➔ ➔M➔a➔i➔n➔t➔a➔i➔n➔s➔ ➔V➔L➔A➔N➔ ➔t➔a➔g➔s➔
➔1➔7➔.➔ ➔V➔P➔N➔ ➔—➔ ➔V➔i➔r➔t➔u➔a➔l➔ ➔P➔r➔i➔v➔a➔t➔e➔ ➔N➔e➔t➔w➔o➔r➔k➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔V➔P➔N➔?➔
➔E➔x➔t➔e➔n➔d➔s➔ ➔a➔ ➔p➔r➔i➔v➔a➔t➔e➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔o➔v➔e➔r➔ ➔a➔ ➔p➔u➔b➔l➔i➔c➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔(➔i➔n➔t➔e➔r➔n➔e➔t➔)➔ ➔u➔s➔i➔n➔g➔ ➔a➔n➔ ➔e➔n➔c➔r➔y➔p➔t➔e➔d➔ ➔t➔u➔n➔n➔e➔l➔.➔ ➔A➔l➔l➔o➔w➔s➔ ➔s➔e➔c➔u➔r➔e➔
➔c➔o➔m➔m➔u➔n➔i➔c➔a➔t➔i➔o➔n➔ ➔o➔v➔e➔r➔ ➔u➔n➔t➔r➔u➔s➔t➔e➔d➔ ➔n➔e➔t➔w➔o➔r➔k➔s➔.➔
➔V➔P➔N➔ ➔u➔s➔e➔s➔:➔
➔E➔n➔c➔r➔y➔p➔t➔i➔o➔n➔ ➔—➔ ➔p➔r➔o➔t➔e➔c➔t➔s➔ ➔d➔a➔t➔a➔ ➔i➔n➔ ➔t➔r➔a➔n➔s➔i➔t➔
➔A➔u➔t➔h➔e➔n➔t➔i➔c➔a➔t➔i➔o➔n➔ ➔—➔ ➔v➔e➔r➔i➔f➔i➔e➔s➔ ➔i➔d➔e➔n➔t➔i➔t➔i➔e➔s➔
➔T➔u➔n➔n➔e➔l➔i➔n➔g➔ ➔p➔r➔o➔t➔o➔c➔o➔l➔s➔ ➔—➔ ➔s➔e➔c➔u➔r➔e➔l➔y➔ ➔t➔r➔a➔n➔s➔p➔o➔r➔t➔ ➔d➔a➔t➔a➔
➔V➔P➔N➔ ➔v➔s➔ ➔V➔L➔A➔N➔:➔
➔V➔P➔N➔ ➔V➔L➔A➔N➔
➔P➔u➔r➔p➔o➔s➔e➔ ➔S➔e➔c➔u➔r➔e➔ ➔t➔u➔n➔n➔e➔l➔ ➔o➔v➔e➔r➔ ➔i➔n➔t➔e➔r➔n➔e➔t➔ ➔L➔o➔g➔i➔c➔a➔l➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔s➔e➔g➔m➔e➔n➔t➔a➔t➔i➔o➔n➔
➔L➔o➔c➔a➔t➔i➔o➔n➔ ➔B➔e➔t➔w➔e➔e➔n➔ ➔s➔i➔t➔e➔s➔/➔u➔s➔e➔r➔s➔ ➔o➔v➔e➔r➔ ➔p➔u➔b➔l➔i➔c➔ ➔i➔n➔t➔e➔r➔n➔e➔t➔ ➔W➔i➔t➔h➔i➔n➔ ➔l➔o➔c➔a➔l➔ ➔n➔e➔t➔w➔o➔r➔k➔
➔S➔e➔c➔u➔r➔i➔t➔y➔ ➔E➔n➔c➔r➔y➔p➔t➔i➔o➔n➔ ➔+➔ ➔a➔u➔t➔h➔e➔n➔t➔i➔c➔a➔t➔i➔o➔n➔ ➔T➔r➔a➔f➔f➔i➔c➔ ➔i➔s➔o➔l➔a➔t➔i➔o➔n➔
➔C➔o➔s➔t➔ ➔L➔o➔w➔ ➔(➔u➔s➔e➔s➔ ➔e➔x➔i➔s➔t➔i➔n➔g➔ ➔i➔n➔t➔e➔r➔n➔e➔t➔)➔ ➔L➔o➔w➔ ➔(➔c➔o➔n➔f➔i➔g➔u➔r➔e➔d➔ ➔o➔n➔ ➔s➔w➔i➔t➔c➔h➔)➔
➔1➔8➔.➔ ➔F➔i➔r➔e➔w➔a➔l➔l➔
➔W➔h➔a➔t➔ ➔i➔s➔ ➔a➔ ➔F➔i➔r➔e➔w➔a➔l➔l➔?➔
➔A➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔s➔e➔c➔u➔r➔i➔t➔y➔ ➔d➔e➔v➔i➔c➔e➔ ➔t➔h➔a➔t➔ ➔f➔i➔l➔t➔e➔r➔s➔ ➔t➔r➔a➔f➔f➔i➔c➔ ➔b➔e➔t➔w➔e➔e➔n➔ ➔t➔r➔u➔s➔t➔e➔d➔ ➔(➔i➔n➔t➔e➔r➔n➔a➔l➔)➔ ➔a➔n➔d➔ ➔u➔n➔t➔r➔u➔s➔t➔e➔d➔ ➔(➔e➔x➔t➔e➔r➔n➔a➔l➔)➔ ➔n➔e➔t➔w➔o➔r➔k➔s➔.➔
➔P➔e➔r➔m➔i➔t➔s➔ ➔o➔r➔ ➔d➔e➔n➔i➔e➔s➔ ➔t➔r➔a➔f➔f➔i➔c➔ ➔b➔a➔s➔e➔d➔ ➔o➔n➔ ➔p➔r➔e➔d➔e➔f➔i➔n➔e➔d➔ ➔r➔u➔l➔e➔s➔.➔
➔F➔i➔r➔e➔w➔a➔l➔l➔ ➔f➔u➔n➔c➔t➔i➔o➔n➔s➔:➔
➔1➔.➔ ➔T➔r➔a➔f➔f➔i➔c➔ ➔F➔i➔l➔t➔e➔r➔i➔n➔g➔ ➔—➔ ➔a➔l➔l➔o➔w➔ ➔o➔n➔l➔y➔ ➔l➔e➔g➔i➔t➔i➔m➔a➔t➔e➔ ➔t➔r➔a➔f➔f➔i➔c➔
➔
➔
➔
➔
➔2➔.➔ ➔N➔e➔t➔w➔o➔r➔k➔ ➔S➔e➔g➔m➔e➔n➔t➔a➔t➔i➔o➔n➔ ➔—➔ ➔i➔s➔o➔l➔a➔t➔e➔ ➔p➔a➔r➔t➔s➔ ➔o➔f➔ ➔n➔e➔t➔w➔o➔r➔k➔
➔3➔.➔ ➔P➔r➔o➔t➔e➔c➔t➔i➔o➔n➔ ➔—➔ ➔s➔h➔i➔e➔l➔d➔ ➔i➔n➔t➔e➔r➔n➔a➔l➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔f➔r➔o➔m➔ ➔t➔h➔r➔e➔a➔t➔s➔
➔I➔n➔ ➔A➔W➔S➔:➔
➔S➔e➔c➔u➔r➔i➔t➔y➔ ➔G➔r➔o➔u➔p➔s➔ ➔=➔ ➔i➔n➔s➔t➔a➔n➔c➔e➔-➔l➔e➔v➔e➔l➔ ➔f➔i➔r➔e➔w➔a➔l➔l➔ ➔(➔s➔t➔a➔t➔e➔f➔u➔l➔)➔
➔N➔e➔t➔w➔o➔r➔k➔ ➔A➔C➔L➔s➔ ➔=➔ ➔s➔u➔b➔n➔e➔t➔-➔l➔e➔v➔e➔l➔ ➔f➔i➔r➔e➔w➔a➔l➔l➔ ➔(➔s➔t➔a➔t➔e➔l➔e➔s➔s➔)➔
➔1➔9➔.➔ ➔N➔e➔t➔w➔o➔r➔k➔ ➔T➔o➔p➔o➔l➔o➔g➔i➔e➔s➔
➔T➔o➔p➔o➔l➔o➔g➔y➔ ➔S➔t➔r➔u➔c➔t➔u➔r➔e➔ ➔P➔r➔o➔s➔ ➔C➔o➔n➔s➔ ➔U➔s➔e➔ ➔C➔a➔s➔e➔
➔B➔u➔s➔ ➔A➔l➔l➔ ➔n➔o➔d➔e➔s➔ ➔o➔n➔ ➔s➔i➔n➔g➔l➔e➔
➔c➔a➔b➔l➔e➔
➔S➔i➔m➔p➔l➔e➔,➔ ➔c➔h➔e➔a➔p➔ ➔O➔n➔e➔ ➔f➔a➔i➔l➔u➔r➔e➔ ➔=➔ ➔a➔l➔l➔
➔d➔o➔w➔n➔
➔S➔m➔a➔l➔l➔/➔t➔e➔m➔p➔o➔r➔a➔r➔y➔
➔n➔e➔t➔w➔o➔r➔k➔s➔
➔S➔t➔a➔r➔ ➔A➔l➔l➔ ➔d➔e➔v➔i➔c➔e➔s➔ ➔c➔o➔n➔n➔e➔c➔t➔
➔t➔o➔ ➔c➔e➔n➔t➔r➔a➔l➔
➔h➔u➔b➔/➔s➔w➔i➔t➔c➔h➔
➔E➔a➔s➔y➔ ➔t➔r➔o➔u➔b➔l➔e➔s➔h➔o➔o➔t➔,➔ ➔o➔n➔e➔
➔l➔i➔n➔k➔ ➔f➔a➔i➔l➔u➔r➔e➔ ➔d➔o➔e➔s➔n➔'➔t➔ ➔a➔f➔f➔e➔c➔t➔
➔o➔t➔h➔e➔r➔s➔
➔C➔e➔n➔t➔r➔a➔l➔ ➔h➔u➔b➔
➔f➔a➔i➔l➔u➔r➔e➔ ➔=➔ ➔a➔l➔l➔ ➔d➔o➔w➔n➔
➔H➔o➔m➔e➔s➔,➔ ➔o➔f➔f➔i➔c➔e➔s➔
➔R➔i➔n➔g➔ ➔E➔a➔c➔h➔ ➔n➔o➔d➔e➔ ➔c➔o➔n➔n➔e➔c➔t➔s➔
➔t➔o➔ ➔e➔x➔a➔c➔t➔l➔y➔ ➔t➔w➔o➔ ➔o➔t➔h➔e➔r➔s➔
➔S➔i➔m➔p➔l➔e➔ ➔d➔a➔t➔a➔ ➔f➔l➔o➔w➔ ➔S➔i➔n➔g➔l➔e➔ ➔n➔o➔d➔e➔
➔f➔a➔i➔l➔u➔r➔e➔ ➔b➔r➔e➔a➔k➔s➔
➔r➔i➔n➔g➔
➔T➔o➔k➔e➔n➔ ➔r➔i➔n➔g➔
➔n➔e➔t➔w➔o➔r➔k➔s➔
➔M➔e➔s➔h➔ ➔E➔v➔e➔r➔y➔ ➔n➔o➔d➔e➔ ➔c➔o➔n➔n➔e➔c➔t➔s➔
➔t➔o➔ ➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔o➔t➔h➔e➔r➔s➔
➔H➔i➔g➔h➔l➔y➔ ➔r➔e➔d➔u➔n➔d➔a➔n➔t➔,➔
➔m➔u➔l➔t➔i➔p➔l➔e➔ ➔p➔a➔t➔h➔s➔
➔E➔x➔p➔e➔n➔s➔i➔v➔e➔,➔
➔c➔o➔m➔p➔l➔e➔x➔
➔M➔i➔l➔i➔t➔a➔r➔y➔,➔ ➔d➔a➔t➔a➔
➔c➔e➔n➔t➔e➔r➔s➔
➔T➔r➔e➔e➔ ➔S➔t➔a➔r➔ ➔n➔e➔t➔w➔o➔r➔k➔s➔
➔c➔o➔n➔n➔e➔c➔t➔e➔d➔ ➔v➔i➔a➔
➔c➔e➔n➔t➔r➔a➔l➔ ➔b➔u➔s➔
➔S➔c➔a➔l➔a➔b➔l➔e➔,➔ ➔h➔i➔e➔r➔a➔r➔c➔h➔i➔c➔a➔l➔ ➔M➔a➔i➔n➔ ➔b➔u➔s➔ ➔f➔a➔i➔l➔u➔r➔e➔
➔=➔ ➔a➔l➔l➔ ➔s➔e➔g➔m➔e➔n➔t➔s➔
➔d➔o➔w➔n➔
➔S➔c➔h➔o➔o➔l➔s➔,➔
➔u➔n➔i➔v➔e➔r➔s➔i➔t➔i➔e➔s➔
➔H➔y➔b➔r➔i➔d➔ ➔C➔o➔m➔b➔i➔n➔a➔t➔i➔o➔n➔ ➔o➔f➔
➔t➔o➔p➔o➔l➔o➔g➔i➔e➔s➔
➔F➔l➔e➔x➔i➔b➔l➔e➔,➔ ➔c➔u➔s➔t➔o➔m➔i➔z➔a➔b➔l➔e➔ ➔C➔o➔m➔p➔l➔e➔x➔ ➔a➔n➔d➔
➔e➔x➔p➔e➔n➔s➔i➔v➔e➔
➔L➔a➔r➔g➔e➔ ➔c➔o➔r➔p➔o➔r➔a➔t➔e➔
➔n➔e➔t➔w➔o➔r➔k➔s➔
➔2➔0➔.➔ ➔N➔e➔t➔w➔o➔r➔k➔i➔n➔g➔ ➔Q➔u➔i➔c➔k➔ ➔R➔e➔f➔e➔r➔e➔n➔c➔e➔ ➔f➔o➔r➔ ➔D➔e➔v➔O➔p➔s➔ ➔I➔n➔t➔e➔r➔v➔i➔e➔w➔s➔
➔O➔S➔I➔ ➔M➔o➔d➔e➔l➔ ➔(➔7➔ ➔l➔a➔y➔e➔r➔s➔,➔ ➔t➔o➔p➔ ➔t➔o➔ ➔b➔o➔t➔t➔o➔m➔)➔:➔
➔A➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔ ➔→➔ ➔P➔r➔e➔s➔e➔n➔t➔a➔t➔i➔o➔n➔ ➔→➔ ➔S➔e➔s➔s➔i➔o➔n➔ ➔→➔ ➔T➔r➔a➔n➔s➔p➔o➔r➔t➔ ➔→➔ ➔N➔e➔t➔w➔o➔r➔k➔ ➔→➔ ➔D➔a➔t➔a➔ ➔L➔i➔n➔k➔ ➔→➔ ➔P➔h➔y➔s➔i➔c➔a➔l➔
➔D➔a➔t➔a➔ ➔n➔a➔m➔e➔s➔ ➔b➔y➔ ➔l➔a➔y➔e➔r➔:➔
➔A➔p➔p➔l➔i➔c➔a➔t➔i➔o➔n➔/➔P➔r➔e➔s➔e➔n➔t➔a➔t➔i➔o➔n➔/➔S➔e➔s➔s➔i➔o➔n➔ ➔=➔ ➔D➔a➔t➔a➔
➔T➔r➔a➔n➔s➔p➔o➔r➔t➔ ➔=➔ ➔S➔e➔g➔m➔e➔n➔t➔
➔
➔
➔
➔
➔N➔e➔t➔w➔o➔r➔k➔ ➔=➔ ➔P➔a➔c➔k➔e➔t➔
➔D➔a➔t➔a➔ ➔L➔i➔n➔k➔ ➔=➔ ➔F➔r➔a➔m➔e➔
➔P➔h➔y➔s➔i➔c➔a➔l➔ ➔=➔ ➔B➔i➔t➔
➔T➔C➔P➔ ➔=➔ ➔r➔e➔l➔i➔a➔b➔l➔e➔,➔ ➔c➔o➔n➔n➔e➔c➔t➔i➔o➔n➔-➔o➔r➔i➔e➔n➔t➔e➔d➔,➔ ➔p➔o➔r➔t➔ ➔6➔
➔U➔D➔P➔ ➔=➔ ➔u➔n➔r➔e➔l➔i➔a➔b➔l➔e➔,➔ ➔c➔o➔n➔n➔e➔c➔t➔i➔o➔n➔l➔e➔s➔s➔,➔ ➔p➔o➔r➔t➔ ➔1➔7➔
➔T➔h➔r➔e➔e➔-➔w➔a➔y➔ ➔h➔a➔n➔d➔s➔h➔a➔k➔e➔ ➔=➔ ➔S➔Y➔N➔ ➔→➔ ➔S➔Y➔N➔-➔A➔C➔K➔ ➔→➔ ➔A➔C➔K➔
➔D➔N➔S➔ ➔=➔ ➔d➔o➔m➔a➔i➔n➔ ➔→➔ ➔I➔P➔ ➔t➔r➔a➔n➔s➔l➔a➔t➔i➔o➔n➔ ➔(➔p➔o➔r➔t➔ ➔5➔3➔)➔
➔D➔H➔C➔P➔ ➔=➔ ➔a➔u➔t➔o➔ ➔I➔P➔ ➔a➔s➔s➔i➔g➔n➔m➔e➔n➔t➔ ➔→➔ ➔D➔O➔R➔A➔ ➔p➔r➔o➔c➔e➔s➔s➔
➔A➔R➔P➔ ➔=➔ ➔I➔P➔ ➔→➔ ➔M➔A➔C➔ ➔a➔d➔d➔r➔e➔s➔s➔ ➔m➔a➔p➔p➔i➔n➔g➔
➔P➔I➔N➔G➔ ➔=➔ ➔I➔C➔M➔P➔ ➔e➔c➔h➔o➔ ➔r➔e➔q➔u➔e➔s➔t➔/➔r➔e➔p➔l➔y➔
➔I➔P➔v➔4➔ ➔=➔ ➔3➔2➔-➔b➔i➔t➔,➔ ➔4➔.➔3➔B➔ ➔a➔d➔d➔r➔e➔s➔s➔e➔s➔
➔I➔P➔v➔6➔ ➔=➔ ➔1➔2➔8➔-➔b➔i➔t➔,➔ ➔3➔4➔0➔ ➔u➔n➔d➔e➔c➔i➔l➔l➔i➔o➔n➔ ➔a➔d➔d➔r➔e➔s➔s➔e➔s➔
➔P➔r➔i➔v➔a➔t➔e➔ ➔r➔a➔n➔g➔e➔s➔:➔ ➔1➔0➔.➔x➔,➔ ➔1➔7➔2➔.➔1➔6➔-➔3➔1➔.➔x➔,➔ ➔1➔9➔2➔.➔1➔6➔8➔.➔x➔
➔L➔o➔o➔p➔b➔a➔c➔k➔:➔ ➔1➔2➔7➔.➔0➔.➔0➔.➔1➔
➔A➔P➔I➔P➔A➔:➔ ➔1➔6➔9➔.➔2➔5➔4➔.➔x➔.➔x➔ ➔(➔n➔o➔ ➔D➔H➔C➔P➔ ➔a➔v➔a➔i➔l➔a➔b➔l➔e➔)➔
➔N➔A➔T➔ ➔=➔ ➔p➔r➔i➔v➔a➔t➔e➔ ➔I➔P➔ ➔→➔ ➔p➔u➔b➔l➔i➔c➔ ➔I➔P➔ ➔(➔P➔A➔T➔ ➔=➔ ➔m➔o➔s➔t➔ ➔c➔o➔m➔m➔o➔n➔)➔
➔V➔L➔A➔N➔ ➔=➔ ➔l➔o➔g➔i➔c➔a➔l➔ ➔n➔e➔t➔w➔o➔r➔k➔ ➔s➔e➔g➔m➔e➔n➔t➔a➔t➔i➔o➔n➔
➔V➔P➔N➔ ➔=➔ ➔e➔n➔c➔r➔y➔p➔t➔e➔d➔ ➔t➔u➔n➔n➔e➔l➔ ➔o➔v➔e➔r➔ ➔i➔n➔t➔e➔r➔n➔e➔t➔
➔F➔i➔r➔e➔w➔a➔l➔l➔ ➔=➔ ➔t➔r➔a➔f➔f➔i➔c➔ ➔f➔i➔l➔t➔e➔r➔ ➔b➔y➔ ➔r➔u➔l➔e➔s➔
➔H➔u➔b➔ ➔=➔ ➔L➔a➔y➔e➔r➔ ➔1➔,➔ ➔b➔r➔o➔a➔d➔c➔a➔s➔t➔s➔ ➔a➔l➔l➔
➔S➔w➔i➔t➔c➔h➔ ➔=➔ ➔L➔a➔y➔e➔r➔ ➔2➔,➔ ➔f➔o➔r➔w➔a➔r➔d➔s➔ ➔b➔y➔ ➔M➔A➔C➔
➔R➔o➔u➔t➔e➔r➔ ➔=➔ ➔L➔a➔y➔e➔r➔ ➔3➔,➔ ➔r➔o➔u➔t➔e➔s➔ ➔b➔y➔ ➔I➔P➔
➔S➔S➔H➔ ➔(➔p➔o➔r➔t➔ ➔2➔2➔)➔ ➔=➔ ➔s➔e➔c➔u➔r➔e➔,➔ ➔e➔n➔c➔r➔y➔p➔t➔e➔d➔
➔T➔e➔l➔n➔e➔t➔ ➔(➔p➔o➔r➔t➔ ➔2➔3➔)➔ ➔=➔ ➔i➔n➔s➔e➔c➔u➔r➔e➔,➔ ➔p➔l➔a➔i➔n➔ ➔t➔e➔x➔t➔
➔
