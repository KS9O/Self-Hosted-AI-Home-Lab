# Hermes Agent Environment Breakdown

This document provides a technical overview of the Hermes Agent environment as of May 4, 2026.

## Architectural Philosophy & Use Cases

This environment utilizes a **Tiered Intelligence Architecture**. By using **Gemini 3.1 Pro** (accessed via TUI) as the State of the Art (SOTA) orchestrator, I strategically delegate tasks to local agents (Benson and Ronald) to minimize token consumption, maintain data sovereignty, and optimize resource usage.

### **Why I run this setup:**
- **Resource Efficiency:** I offload high-volume, iterative development tasks to local models, reserving SOTA cloud credits for complex architectural decisions.
- **Latency Optimization:** Real-time Discord interactions and local file system operations are handled with near-zero latency via local inference.
- **Privacy & Security:** Sensitive system audits and internal code refactoring are performed locally, ensuring proprietary data never leaves the network.

### **Proven Use Cases:**
1.  **Iterative UI/UX Development:** Benson handles the hundreds of small CSS/JS tweaks in the [project-monolith](ackursyns.com) workspace. At the same time, Gemini 3.1 Pro is tasked with reviewing the final architectural integrity.
2.  **Continuous Security Auditing:** Ronald performs 24/7 log analysis and dependency scanning (Gemma-4 4B), alerting the human operator only when a high-probability threat is detected.
3.  **Automated Skill Synthesis:** When a new workflow is discovered, local agents document and "save" the skill, which can then be indexed and utilized by the SOTA model in future sessions.

![alt text](<assets/Benson Daily Cyberheadlines.png>)

**Here is a use case that I use daily, Benson, will scrape the internet and give me a daily Cybersecurity headline report at 7 AM (EST) everyday! Its a great and convenient way to stay up to date on emerging threats and news**

---

## Delegation & Logic Flow
```
    Me(user)([My Request]) --> SOTA[Gemini 3.1 Pro<br>TUI Orchestrator]
    
    "Local Execution Layer (WSL2)"
        SOTA -- "Software Dev / API Integration" --> Benson[Benson Profile<br>Qwen 27B Uncensored]
        SOTA -- "System Audit / Security" --> Ronald[Ronald Profile<br>Gemma-4 4B]
        
        Benson --> B_Tools[Terminal / Files / Discord]
        Ronald --> R_Tools[Log Scrapers / Netstat / Webhooks]
    
    B_Tools --> Success([Task Completed])
    R_Tools --> Success
    Success --> Feedback[Update Persistent Memory]
```

---

## Active AI Models

### **Primary Model: Qwen 3.6 27B Uncensored**
- **Status:** **Active** (Serving the **Benson** Profile)
- **Host:** Dedicated Inference Server (Local Network)
- **Capabilities:** 100,000 token context window optimized for dense codebases.

![alt text](<assets/Benson Agent.jpg>)

### **Secondary Model: Gemma-4 4B**
- **Status:** **Standby** (Assigned to the **Ronald** Profile)
- **Host:** Local Gateway Node (Standby)
- **Capabilities:** Lightweight, high-speed inference for security telemetry.

![alt text](<assets/Ronald-Local Hermes agent.jpg>)

---

## Hardware & Infrastructure

### **1. Inference Server (Benson's Engine)**
- **CPU:** AMD Ryzen 7 7800X3D
- **GPU:** NVIDIA RTX 3090 Ti (24GB VRAM)
- **Memory:** 32GB DDR5 RAM

### **2. Local Gateway Node (Ronald's Host)**
- **Environment:** **WSL2 (Ubuntu)**
- **CPU:** Intel(R) Core(TM) i7-8700
- **Memory:** 8GB Allocated RAM
- **Storage:** 1TB Dedicated NVMe

---

## Messaging Gateway & Profiles

### **Profile Architecture**
Hermes utilizes isolated profiles to maintain distinct "Souls" and memory banks. This prevents context contamination between software development (Benson) and system security (Ronald).

### **Discord Connectivity**
- **Gateway:** Persistent WebSocket connection via WSL2.
- **Auth:** Whitelisted access via `DISCORD_ALLOWED_USERS`.
- **Interface:** Supports Slash commands and rich-media thread management.

---

## Profile Breakdown

| Profile | Model | Primary Domain | Personality |
| :--- | :--- | :--- | :--- |
| **Benson** | **Qwen 3.6 27B** | Software Dev / Architecture | Professional Tech Specialist |
| **Ronald** | **Gemma-4 4B** | SysAdmin / Security | Methodical Security Expert |

