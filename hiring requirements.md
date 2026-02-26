## Hiring Plan & Role Specifications: Trybo Q1 2026

### **Hiring Strategy Overview**

* **Total Target Headcount:** 4 Core Engineers.
* **The "Alex" Profile (P0):** 1x Owner-level Frontend (React Native Veteran).
* **The Backend Owner (P0):** 1x Senior Backend/Infra (Agentic Architecture Specialist).
* **The Implementation Engine:** 2x Full-Stack Juniors (2–4 yrs experience).

---

## **1. Lead Frontend Engineer (Product Owner)**

**Focus:** Real-time Interaction, Consent UX, & WebRTC/Voice Interface.

### **Core Requirements**

* **React Native Mastery:** 6+ years depth. Experience with Expo, Custom Native Modules, and JS-Native bridges.
* **Real-time State & Streaming:** Expert with TanStack Query, Zustand, and WebSocket/SSE for streaming LLM responses and optimistic UI updates.
* **Agentic UI/UX:** Experience building "Generative UI" (JSON-driven layouts) and complex skeletal states for background agent tasks.
* **Reliability:** Architecting resume-from-kill flows, background services, and offline-first sync (SQLite/WatermelonDB).
* **WebRTC/Audio:** Implementation of low-latency voice rooms, VAD (Voice Activity Detection), and background audio constraints.

### **Technical Specifics**

* Performance profiling (Hermes, JSI, FPS optimization).
* Deep-link integration for secure OTP/Auth bypass flows.
* Strict DTO (Data Transfer Object) contract management for AI-to-UI communication.

---

## **2. Senior Backend Engineer (Agentic Infra)**

**Focus:** GID Brain, Task Orchestration, & Execution Substrate.

### **Core Requirements**

* **Durable Execution:** Expert in state machines, resumable task logic, retries/compensation patterns (Temporal or equivalent).
* **Agent Orchestration:** Practical implementation of ReAct patterns, DAG-based task planning, and dynamic subtask replanning.
* **MCP Mastery:** Deep understanding of Model Context Protocol (JSON-RPC 2.0), tool discovery, and resource modeling.
* **Intelligence Layer:** Designing strict JSON Schemas for Global Intent Detection (GID) and managing high-accuracy RAG pipelines.
* **Security & Trust:** Built-in PII redaction, audit logging, and first-class "Consent & Approval" state management.

### **Technical Specifics**

* **Stack:** Go or Python (Async IO), PostgreSQL/Supabase, Vector DBs (Pinecone/Weaviate).
* **Communication:** High-concurrency WebSockets/SSE implementation and event-driven architectures.
* **Voice Integration:** WebRTC-to-SIP bridging and telephony primitives (LiveKit/Twilio).

---

## **3. Full-Stack Engineer (Implementation)**

**Focus:** Feature Delivery, API Plumbing, & Tool Integration.

### **Core Requirements**

* **Experience:** 2–4 years. High growth potential over raw years.
* **Backend:** Building REST/WebSocket endpoints, implementing MCP connectors (Gmail, Calendar, Notion), and writing unit/eval tests for agents.
* **Frontend:** Building clean, reactive UI components based on Figma designs; managing local state and API consumption.
* **Data:** Basic SQL optimization, vector embedding generation, and JSON-schema validation.

### **Technical Specifics**

* Comfortable working across the stack to ship vertical features (e.g., "New Search Primitive").
* Familiarity with LangChain, LangGraph, or similar multi-agent frameworks.
* Strong focus on "shipping-to-learn" and rapid prototyping.

---

### **Success Metrics for New Hires (First 90 Days)**

* **Lead Frontend:** Deliver the "Trybo Link" WebRTC room and the unified "Approval Console" UI.
* **Senior Backend:** Implement the Resumable State Machine and stabilize the GID Intent Schema.
* **Juniors:** Successfully integrate 3+ new MCP tools and maintain 95%+ API uptime.
