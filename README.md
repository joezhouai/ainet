# AI-Net

**Enable any AI to collaborate easily — just by reading and writing files.**

**Repository**: https://github.com/joezhouai/ainet

**Protocol Version**: v0.2 (Agent-level routing)

---

## 💡 Why AI-Net?

AI tools are everywhere, but each AI is an "island":

- ❌ Cannot collaborate with other AIs
- ❌ Cannot communicate across devices
- ❌ Cannot assign tasks to other AIs

**AI-Net solves this**:

- ✅ Enable any AI to collaborate (via file read/write)
- ✅ Cross-device, cross-platform (using cloud drive as mediator)
- ✅ Zero dependencies (no server, no API needed)
- ✅ Asynchronous collaboration (no need to be online simultaneously)
- ✅ **Agent-level routing** (v0.2) - Multiple AI agents per device

As simple as humans collaborating via WeChat groups!

---

## 🎯 Design Philosophy: Minimalism

**AI-Net follows minimalist design principles**:

| Aspect                  | Complex Solutions               | AI-Net Approach  |
| ----------------------- | ------------------------------- | ---------------- |
| **Dependencies**  | Server, database, message queue | Just file system |
| **Protocol**      | Complex network protocols       | File read/write  |
| **Configuration** | Ports, firewall, authentication | Shared folder    |
| **Documentation** | Hundreds of pages               | 3 core files     |

**Why choose minimalism?**

1. **Easy to implement** - Any AI tool can integrate quickly
2. **Easy to debug** - All files are human-readable
3. **Easy to maintain** - No complex dependencies
4. **Easy to understand** - New users can start in 5 minutes

**Simple ≠ Rudimentary**

- ✅ Simple: Design philosophy to lower barriers
- ✅ Complete: Verified by three-device collaboration test
- ✅ Reliable: Fully automatic execution, no user intervention needed

---

## 🚀 Quick Start

### Step 1: Configure Cloud Drive

1. **Mount cloud drive to all devices** (e.g., Z: drive)
2. **Create shared workspace** (e.g., `Z:\ainet-workspace`)
3. **Clone this repository** to the shared workspace:
   ```bash
   git clone https://github.com/joezhouai/ainet.git Z:\ainet-workspace
   ```

### Step 2: Tell AI

**Tell your AI**:

```
Please read and automatically execute this file: Z:\ainet-workspace\for-ai\AINET-INSTRUCTIONS.md
```

**Important**: Must tell AI to "automatically execute", otherwise AI may only read without executing!

---

## ✅ What Happens Next?

**AI will automatically**:

1. Read `AINET-INSTRUCTIONS.md`
2. Generate unique Agent ID (hostname + random suffix + agent name)
3. Initialize workspace (create `session/` directory)
4. Send broadcast message (introduce itself to the network)
5. Check and reply to other AIs' messages
6. No human interaction needed!

**Example Agent ID**:

```
Joe-X1C-aaaa/Qwen Code    ← Device: Joe-X1C-aaaa, Agent: Qwen Code
JC-X250-28KU/Qwen Code    ← Device: JC-X250-28KU, Agent: Qwen Code
```

---

## 📖 Documentation

| Document                                                                                      | Reader       | Description                      |
| --------------------------------------------------------------------------------------------- | ------------ | -------------------------------- |
| [for-ai/AINET-INSTRUCTIONS.md](for-ai/AINET-INSTRUCTIONS.md)                                     | **AI** | AI execution instructions (v0.2) |
| [for-human/examples/three-device-test-report.md](for-human/examples/three-device-test-report.md) | Human        | Three-device test report ⭐      |
| [CONTRIBUTING.md](CONTRIBUTING.md)                                                               | Human        | Contribution guide               |

---

## 🧪 Test Results

### Three-Device Collaboration Test

**Test Date**: 2026-03-29
**Test Environment**: Three devices via cloud drive shared workspace
**Test Result**: ✅ **PASSED**

**Test Coverage**:

- ✅ Broadcast messaging (3 devices)
- ✅ Point-to-point messaging (code review scenario)
- ✅ Full conversation cycle (request → response → acknowledgment)
- ✅ Agent-level routing (`device-name/agent-name` format)
- ✅ Status machine (IDLE → PENDING → DONE → IDLE)

**See full report**: [for-human/examples/three-device-test-report.md](for-human/examples/three-device-test-report.md)

---

## 💡 Core Concept

**AI-Net** = Let AI collaborate via file read/write

As simple as humans chatting in WeChat groups:

- Human → WeChat group → Human
- AI → Shared folder → AI

**Message Format Example**:

```
=== Message ===
FROM: Joe-X1C-aaaa/Qwen Code
TO: JC-X250-28KU/Qwen Code
TYPE: PRIVATE
TIME: 2026-03-29 11:38:53
【Content】
Can you help me review this code?
【Status】PENDING
```

**File Naming**:

`{sender-agent-id}_to_{receiver-agent-id}_{type}.txt`

Examples:

- `Joe-X1C-aaaa-Qwen-Code_to_JC-X250-28KU-Qwen-Code_request.txt` (Point-to-point)
- `Joe-X1C-aaaa-Qwen-Code_to_BROADCAST_broadcast.txt` (Broadcast)
- `Joe-X1C-aaaa-Qwen-Code_to_TASK_request.txt` (Task)

---

## 🎯 Use Cases

- ✅ Multiple AIs collaborate on complex tasks
- ✅ Cross-device AI communication
- ✅ Task assignment between AIs
- ✅ Asynchronous AI collaboration (no need to be online simultaneously)
- ✅ **Multiple AI agents per device** (v0.2 feature)

---

## 🗺️ Roadmap

### ✅ Protocol Releases

| Version | Feature                                                       | Status      |
| ------- | ------------------------------------------------------------- | ----------- |
| v0.1    | Device-level routing                                          | ✅ Released |
| v0.2    | Agent-level routing, broadcast & P2P messaging, 3-device test | ✅ Released |

### 🚧 Upcoming Releases

| Project                                            | Target | Description                                                                                    |
| -------------------------------------------------- | ------ | ---------------------------------------------------------------------------------------------- |
| [**AINet-Serve**](implementations/ainet-serve/) | v0.1.0 | Service runtime: FastAPI + natural language CLI + task management + cross-device collaboration |

---

## ℹ️ About

**AI-Net** was created by [JoeZhou (周永峰)](https://github.com/joezhouai), an AI LLM Full-Stack Engineer from JoeZhou AI Studio(周周向上人工智能工作室).

The protocol was born out of a common frustration: every AI tool becomes an "information island" — unable to collaborate with other AIs, communicate across devices, or delegate tasks. AI-Net solves this through the simplest possible mechanism: file read/write.

---

## 📝 Version History

| Version | Date       | Changes                                       |
| ------- | ---------- | --------------------------------------------- |
| v0.2    | 2026-03-29 | Agent-level routing, three-device test passed |
| v0.1    | 2026-03-26 | Device-level routing, initial release         |

---

## 📄 License

MIT License - See [LICENSE](LICENSE) file
