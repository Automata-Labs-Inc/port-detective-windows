# PortDetective: The Active Port Guard for Windows

[![Download from Microsoft Store](https://img.shields.io/badge/Microsoft_Store-Download-0078D4?style=for-the-badge&logo=windows&logoColor=white)](https://apps.microsoft.com/store/detail/9P3N1R131WDZ?cid=GitHub)
[![Rust](https://img.shields.io/badge/built_with-Rust-orange?style=for-the-badge&logo=rust)](https://www.rust-lang.org/)
[![Tauri](https://img.shields.io/badge/powered_by-Tauri-24C8D8?style=for-the-badge&logo=tauri)](https://tauri.app/)

**Stop hunting zombie processes. Start coding.**

**PortDetective** is a lightweight, Windows desktop utility designed to eliminate the friction of `EADDRINUSE` errors and local port conflicts. Unlike passive diagnostic tools (like Resource Monitor or TCPView), PortDetective acts as an active guard dog for your local development environment.

## 🚀 The Problem
You run `npm start`, `docker-compose up`, or `cargo run`, only to be met with a fatal crash:
`Error: listen EADDRINUSE: address already in use :::3000`

The standard Windows workflow to fix this is tedious:
1. Open PowerShell.
2. Run `netstat -ano | findstr :3000`.
3. Locate the PID.
4. Open Task Manager.
5. Search for the PID and terminate the tree.

## ✅ The Solution
**PortDetective** automates the triage. It sits silently in your Windows system tray and actively monitors your stack's vital signs.

* **Active Watchlist:** Add your vital dev ports (e.g., `3000`, `5432`, `8080`). Get a native OS notification the **exact millisecond** a rogue background process hijacks them.
* **Zero-Idle Overhead:** Built with an edge-triggered **Tokio** watcher thread in Rust. It consumes ~0% CPU while minimized to the tray.
* **Native Win32 Integration:** No slow CLI wrappers. The backend interfaces directly with `GetExtendedTcpTable` via memory-safe Rust for near-instant network snapshots.
* **1-Click Safe Kill:** Instantly terminate rogue processes directly from the UI. PortDetective validates process tokens before execution to prevent accidental termination of reused PIDs.

---

### 📸 Visual Proof
![PortDetective in Action](YOUR_GIF_URL_HERE)
*Fixing an EADDRINUSE error in 2 seconds without leaving your IDE.*

---

## 🛠 Technical Architecture
PortDetective is built for speed and low memory footprint.
* **Backend Core:** Rust (utilizing `windows-sys` for native APIs and `tokio` for async daemon tasks).
* **Frontend UI:** React + Tailwind CSS + Zustand, rendered via the Tauri WebView.
* **OS Integration:** Deep integration with Windows internals, including synchronous UAC elevation (`ShellExecuteW`) to securely unlock system-level processes.

## 💎 PortDetective Pro
While the core local triage features are completely free, we offer a one-time **Pro** unlock in the Microsoft Store aimed at DevOps engineers and Sysadmins:
* **Remote Port Scanner:** A highly concurrent, GUI-based remote scanning engine for rapid network triage (powered by optimized Rust networking primitives).
* **Enterprise Audit Logging:** 1-click export of your live network snapshot to CSV/JSON, including deep-level data like **Absolute Executable Paths** and **Exact Remote IP Mappings** for compliance documentation.

## 🛡️ Privacy & Security
* **Local-First Processing:** PortDetective operates entirely offline. No telemetry, no cloud processing, and no data ever leaves your machine.
* **Closed Source for Sustainability:** To support independent development at **Automata Labs**, the core application binary is closed-source. However, we use this public GitHub repository for all community bug tracking, feature requests, and roadmapping.

---

## 🙋 Getting Help & Roadmap
We use GitHub Issues to track everything. We'd love to hear your feedback!
* [**Report a Bug**](../../issues/new)
* [**Request a Feature**](../../issues/new)
* [**View the Public Roadmap**](../../issues)

---

### **[👉 Download PortDetective Free from the Microsoft Store](https://apps.microsoft.com/store/detail/9P3N1R131WDZ?cid=GitHub)**
