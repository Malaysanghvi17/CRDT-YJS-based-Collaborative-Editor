# CRDT-RGA-based-Collaborative-Editor

Real-time collaborative text editor built from scratch using **RGA(Replicated Growable Array) (CRDT)** with WebSocket-based synchronization, live cursor presence, and a **HTML-TS + Node.js** architecture. Designed for conflict-free distributed editing and low-latency multi-user collaboration.

---

## Live Project

**Application URL**
[https://collab-ot-project-latest.onrender.com/canvas?doc=default](https://collab-ot-project-latest.onrender.com/canvas?doc=default)

---

## Overview

This project uses an implementation of Replicated Growable Array (RGA) — a sequence-based CRDT (Conflict-free Replicated Data Type) designed for real-time collaborative editing.

RGA represents a document as a linked structure where:

* Each character (or element) has a unique ID
* Insert operations reference a parent element
* Concurrent inserts are deterministically ordered using unique IDs (e.g., Lamport timestamps)
* Deletions are handled using tombstones to preserve consistency across replicas
Because operations are commutative and deterministic, all replicas eventually converge to the same state without requiring central coordination.

This makes RGA well-suited for distributed, real-time text collaboration systems.

The project demonstrates a fully functional collaborative text editor where multiple users can:

* Edit the same document simultaneously
* See each other's cursor positions in real time
* Continue editing while offline
* Automatically synchronize document state after reconnection

The system ensures deterministic conflict resolution using CRDT principles via RGA, eliminating the need for manual merge handling.

---

## Technology Stack

**Frontend**

* HTML + TS(vannila project)
* TypeScript
* CRDT based RGA algo

**Backend**

* Node.js
* WebSocket server

**Core Synchronization**

* RGA CRDT document model
* Structured operation-based update propagation
* Custom presence tracking for live cursor synchronization

---

## Demo Screenshots

### 1. Basic User Interface

<img width="1919" height="856" alt="image" src="https://github.com/user-attachments/assets/91927789-95d7-42a2-8c7c-f8a55eddf2c2" />

---

### 2. Live In-Sync Editing with Cursor Position

Multiple users editing simultaneously with real-time cursor presence tracking.

<img width="1918" height="853" alt="image" src="https://github.com/user-attachments/assets/7568fccc-b2ba-4f78-93ee-c82e813de211" />

---

### 3. Offline Editing Scenario
One user disconnects from the internet while both continue typing locally.

<div align="center"> 
  <table> 
    <tr> 
      <td align="center">
        <strong>User 1 (Online State)</strong>
      </td> 
      <td align="center">
        <strong>User 2 (Offline State)</strong>
      </td> 
    </tr> 
    <tr> 
      <td> 
        <img width="500" src="https://github.com/user-attachments/assets/c61c7953-ffc1-4dfc-b982-15a33aca3467" /> 
      </td>
      <td> 
        <img width="350" src="https://github.com/user-attachments/assets/6642dd46-1537-4d87-97ab-75cd8e84668f" />
      </td>
    </tr> 
  </table> 
</div>

---

### 4. Automatic State Synchronization After Reconnection
When the offline user reconnects to the internet, both document states merge automatically and converge to the same consistent version.

<div align="center"> 
  <table> 
    <tr>
      <td align="center">
        <strong>
          User 1 (After Sync)
        </strong>
      </td> 
      <td align="center">
        <strong>User 2 (After Reconnection)</strong>
      </td> 
    </tr>
    <tr> 
      <td>
        <img width="500" src="https://github.com/user-attachments/assets/91c4ea16-db99-4259-8f6a-32d1a1520659" /> 
      </td>
      <td> 
        <img width="350" src="https://github.com/user-attachments/assets/47dd3dc4-9d47-4661-9e8b-a9b456e701fc" /> 
      </td> 
    </tr> 
  </table> 
</div>

---

## Key Characteristics

* Conflict-free replicated data type (CRDT) based architecture
* Deterministic merge guarantees
* Strong eventual consistency
* Stateless WebSocket relay server
* Offline-first editing capability
* Real-time cursor awareness

---

## Architectural Concept

Each client maintains its own local RGA document instance.

All updates are:

* Commutative
* Associative
* Idempotent

This guarantees convergence regardless of:

* Network delays
* Message ordering
* Temporary disconnections

The backend acts only as an update relay and does not perform conflict resolution logic.
