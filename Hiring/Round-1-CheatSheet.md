# Trybo — Screening Criteria Brief for JobTwine
**Confidential | Hiring Bar Document | Feb 2026**

We are hiring for **three distinct profiles**. Each has a per-skill verification gates that must be tested in Round 1. A candidate who cannot pass the verification question for a skill they claim on their resume should **not be cleared**, regardless of general impression.

Please choose accordingly from below cheatsheet for round 1 verifications.

***

## Profile 1 — Full-Stack Junior Engineer (2–4 years)
**Bar:** 0→1 builder. Learns fast, not afraid of new tech, can own features end-to-end across mobile and backend.

### Mandatory Resume Skill Verifications

**React Native** → *OS Lifecycle & Background Behavior*
Ask: *"A user triggers a 5-minute background job from your app. The app gets killed by the OS mid-job. How does the backend notify the user when it completes?"*
Pass: Must reach FCM/APNs as the answer without prompting. Must understand that threads die with the app process. Must not suggest polling from a killed app or background Java threads.

**Node.js / Express** → *Event Loop & Concurrency Model*
Ask: *"Node.js is single-threaded. How does it handle 10,000 simultaneous requests without blocking?"*
Pass: Must explain async I/O, the event loop, and libuv offloading — not "we add more servers" or "load balancer."

**MongoDB** → *Indexing & Query Performance*
Ask: *"Your notifications collection has 10 million documents. Queries are slow. Walk me through how you'd diagnose and fix it."*
Pass: Must mention `explain()`, compound vs single-field indexes, and cardinality tradeoffs. Surface-level "add an index" is insufficient.

**PostgreSQL / Supabase** → *Transactions & Consistency*
Ask: *"Two concurrent requests try to deduct from the same user's balance at the same time. How do you prevent a race condition?"*
Pass: Must mention transactions, `SELECT FOR UPDATE`, or optimistic locking. "We just don't allow it" is a fail.

**Redis** → *Pub/Sub Durability & Eviction*
Ask: *"You're using Redis pub/sub for real-time events. A subscriber goes offline for 30 seconds. What happens to messages published during that time?"*
Pass: Must know pub/sub has no persistence — missed messages are lost. Must suggest Redis Streams or a persistent queue as the fix.

**Docker / Kubernetes** → *Real Usage vs Resume Padding*
Ask: *"Walk me through the last Dockerfile you wrote. What's the difference between CMD and ENTRYPOINT? What's a liveness probe?"*
Pass: Must answer CMD/ENTRYPOINT correctly and have a concrete Docker story. Kubernetes without knowing liveness probes = resume padding.

**JWT / Auth** → *Token Invalidation*
Ask: *"A user logs out. How do you invalidate their JWT before it expires?"*
Pass: Must acknowledge JWTs are stateless and explain a blocklist (Redis TTL), short-lived tokens + refresh rotation, or session revocation. "You can't" or "just delete it client-side" is a fail.

**WebSockets** → *Reconnection & State Recovery*
Ask: *"Your WebSocket connection drops mid-session. How does the client recover without losing state?"*
Pass: Must discuss reconnect logic, exponential backoff, and server-side session/message resumption. Not just "the client reconnects."

***

## Profile 2 — Senior Agentic Backend Engineer
**Bar:** Has built or operated a production agentic system. Understands orchestration, durable execution, and trust/safety at the infra level — not just LLM wrappers.

### Mandatory Resume Skill Verifications

**Durable Execution (Temporal / LangGraph / equivalent)** → *Resumability & Compensation*
Ask: *"A multi-step agent workflow is mid-execution when the process crashes. How do you resume it exactly where it left off? What happens to a step that had already sent an email before the crash?"*
Pass: Must discuss checkpointing to persistent storage, idempotency keys, and compensation/saga patterns for non-reversible side effects. "Restart from the beginning" is a fail.

**ReAct / Agent Orchestration** → *Dynamic Replanning*
Ask: *"Your agent is mid-plan and discovers that the tool it needs for step 3 is unavailable. What does the orchestration engine do? How is this different from a fixed workflow?"*
Pass: Must describe partial replanning, fallback skill selection from a registry, and graph re-compilation from the failure point — not a full restart.

**DAG-based Task Planning** → *Cycle Detection & Parallel Execution*
Ask: *"How do you detect a circular dependency in a task graph at plan validation time, before execution starts? And how do you identify which nodes can run in parallel?"*
Pass: Must describe topological sort / DFS cycle detection. Parallel nodes = nodes with no dependency edge between them (fan-out). Vague "we validate it" is a fail.

**MCP (Model Context Protocol)** → *Protocol Depth*
Ask: *"What transport mechanisms does MCP support? If you're adding a new MCP server to a production system, what do you validate before routing live traffic to it?"*
Pass: Must know stdio and HTTP/SSE transports. Validation should include: tool schema conformance, health check/canary, auth scope verification. "I've used it" without protocol knowledge is a fail.

**Global Intent Detection (GID) / Semantic Routing** → *Hallucination Control*
Ask: *"Your LLM planner produces a plan that references a tool that doesn't exist in your registry. How do you catch and handle this before it reaches the executor?"*
Pass: Must describe schema validation against a registry, re-prompt with error context on failure, graceful degradation (remove the node, cascade-remove dependents). No answer about "trusting the LLM" passes.

**RAG Pipelines** → *Retrieval Quality & Failure Modes*
Ask: *"Your RAG pipeline is returning semantically similar but factually wrong chunks. What are the three most likely causes and how do you fix each?"*
Pass: Must cover: chunking strategy (too coarse/fine), embedding model mismatch, and retrieval scoring threshold. Bonus: re-ranking, metadata filtering, hybrid search.

**PII Redaction / Audit Logging** → *Production Trust*
Ask: *"An agent accidentally logs a user's phone number in a task audit entry. How does your system prevent this, and what's your remediation path after the fact?"*
Pass: Must mention pre-write PII scanning (regex + NER), field-level redaction before persistence, and a retroactive scrub pipeline. "We're careful" is a fail.

**Consent / HITL State Management** → *Interruption Mechanics*
Ask: *"A user approves an action, the graph resumes, but the external API call fails. The action was non-idempotent (e.g., a payment). What does your system do?"*
Pass: Must discuss idempotency keys, distinguishing retriable vs non-retriable failures, re-asking consent if re-execution risk is high, and surfacing a structured failure artifact to the user.

***

## Profile 3 — Lead Frontend Engineer (React Native, Product Owner)
**Bar:** 6+ years. Owns the full client-side architecture. Has built real-time, agentic, and voice UIs — not just screens.

### Mandatory Resume Skill Verifications

**React Native (6+ years claimed)** → *JS-Native Bridge & Custom Modules*
Ask: *"You need to access a native Android API that has no React Native library. Walk me through how you'd build a custom native module — what files, what bridge mechanism, and how does the JS side call it?"*
Pass: Must describe `@ReactMethod`, `ReactContextBaseJavaModule`, `NativeModules` on JS side, and Promise/callback patterns. Expo-only candidates who can't go native are a fail for this role.

**Expo** → *Managed vs Bare Workflow Tradeoffs*
Ask: *"When would you eject from Expo's managed workflow, and what breaks when you do?"*
Pass: Must articulate: native module requirements, OTA update constraints, build configuration control as eject triggers. Must know EAS Build as the modern alternative to ejecting fully.

**TanStack Query / Zustand** → *Real-Time State & Optimistic UI*
Ask: *"You have a chat message that the user sends. You want it to appear instantly in the UI before the server confirms it. Then the server returns an error. Walk through the full state cycle."*
Pass: Must describe optimistic update → rollback on error → cache invalidation. Must know `onMutate`, `onError`, `onSettled` or equivalent pattern. "Just set state and call API" is a fail.

**SSE / WebSocket for Streaming LLM** → *Streaming Architecture*
Ask: *"You're streaming an LLM response token by token from the backend via SSE. The stream drops mid-response. How do you handle reconnection and partial state on the client?"*
Pass: Must discuss `EventSource` reconnect with `Last-Event-ID`, partial message buffering, and UI state for "streaming" vs "complete" vs "error." Must not suggest polling as a substitute.

**Generative UI / JSON-Driven Layouts** → *Renderer Architecture*
Ask: *"The backend sends a JSON payload describing a UI card — type: 'flight_card', fields: [...]. How do you architect the renderer on the React Native side so that adding a new card type requires zero changes to existing code?"*
Pass: Must describe a renderer registry (map of type → component), dynamic component lookup, and prop schema validation. Hard-coded switch/if-else chains are a fail.

**Resume-from-Kill / Offline-First** → *App Lifecycle Architecture*
Ask: *"Your app was killed mid-flow while waiting for an agent task to complete. The user reopens the app 10 minutes later. How does the app know there's a pending task, load its state, and resume the UI correctly?"*
Pass: Must describe: push notification delivery on kill, local persistence (SQLite/WatermelonDB/AsyncStorage) of task state, hydration on app launch from persisted state, and reconciliation with server state. No local persistence = fail.

**WebRTC / Audio** → *Low-Latency Voice Architecture*
Ask: *"You're building a real-time voice room. How do you handle Voice Activity Detection (VAD), and what happens when the app is backgrounded mid-call on iOS?"*
Pass: Must know VAD libraries (e.g., `@livekit/react-native`, WebRTC-native VAD), iOS `AVAudioSession` background mode requirements, and `Background Modes: audio` entitlement. "It just keeps running" without knowing the entitlement is a fail.

**WatermelonDB / SQLite (Offline Sync)** → *Sync Architecture*
Ask: *"You have local data in WatermelonDB and server data in Postgres. A user edits the same record offline and then comes back online — another user edited the same record server-side in the meantime. How do you resolve this?"*
Pass: Must describe: conflict resolution strategy (last-write-wins, server-wins, or merge with vector clocks), sync queue design, and optimistic local writes with server reconciliation. No answer on conflict strategy = fail.

***

## General Instructions for JobTwine Panel

1. **Do not pass on general impression alone.** Pick any skill from the resume and verify using above cheatsheet to guage the proficiency. We want to eliminate resume Skill Padding. We have seen many resumes now mentioning things like RAG/NodeJs/Cloud without having any experience in such fields.
2. **Reject confident wrong answers harder than honest gaps.** A candidate who says "I'm not sure, but here's how I'd approach it" is better than one who confidently gives an architecturally incorrect answer and defends it under challenge.
3. **The bar is not "has used the technology." The bar is "can reason correctly about its failure modes."**
