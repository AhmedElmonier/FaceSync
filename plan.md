# Implementation Plan: Multi-Modal Edge-to-Cloud Attendance SaaS

## Executive Summary
This implementation plan outlines the development of a high-resilience, bilingual (Arabic/English) attendance ecosystem engineered for the Egyptian market. The system leverages a hybrid Edge-to-Cloud architecture to ensure 100% data integrity during internet blackouts and sub-200ms inference latency on local edge nodes. By integrating state-of-the-art AI (RetinaFace/ArcFace) with a robust "Maker-Checker" governance workflow, the solution eliminates buddy-punching and manual payroll errors while ensuring full localization across all user touchpoints.

## Summary
The project is divided into five distinct phases, moving from the core AI inference on the edge to the high-level fleet management operations in the cloud. Each phase builds upon the previous one, ensuring a solid foundation for scalability, security, and bilingual user experience.

---

## Phase 1: The AI Edge Inference Core
**Spec Name:** `spec-edge-ai-core.md`  
**Focus:** Turning a video stream into a verified identity on a local machine.

*   **Objective:** Implement the $RetinaFace$ + $ArcFace$ pipeline and the Periocular module.
*   **Key Deliverable:** A local Python script that captures RTSP frames, detects faces, generates embeddings, and matches them against a local HNSW index.
*   **Success Metric:** Under 200ms latency for a single frame with 5+ faces.
*   **Bilingual Scope:** Localized audio/visual "Success/Fail" feedback on the terminal/mock-UI.

---

## Phase 2: The Resilient SQLite & Sync Engine
**Spec Name:** `spec-sync-persistence.md`  
**Focus:** Handling the "Internet Blackout" and the "Blind Relay."

*   **Objective:** Build the local SQLite schema and the HTTPS batch-sync worker with exponential backoff.
*   **Key Deliverable:** A background process that queues attendance logs and only clears them upon receiving a cryptographic 200 OK from a (mocked) Cloud API.
*   **Success Metric:** 100% data integrity after a simulated 24-hour internet blackout.

---

## Phase 3: The Multilingual Cloud API (SaaS Brain)
**Spec Name:** `spec-cloud-api-i18n.md`  
**Focus:** The FastAPI backend, PostgreSQL RLS, and the Bilingual Alert Engine.

*   **Objective:** Set up the multi-tenant database and the REST/MQTT endpoints.
*   **Key Deliverable:** A secure API that accepts batch logs, performs Row-Level Security checks, and triggers WhatsApp/Email alerts in the recipient's preferred language.
*   **Success Metric:** Successful authenticated sync from Phase 2 to Phase 3 with sub-second DB write time.

---

## Phase 4: The Bilingual HR Dashboard (Client UI)
**Spec Name:** `spec-dashboard-rtl-ltr.md`  
**Focus:** The Next.js frontend, RTL mirroring, and the Maker-Checker inbox.

*   **Objective:** Build the HR Director's view with full Arabic/English toggling.
*   **Key Deliverable:** A dashboard that flips layout based on locale, featuring the Live Operations Hub and the "Pending Approvals" widget for manual time edits.
*   **Success Metric:** Pixel-perfect RTL rendering and working "Maker-Checker" status updates.

---

## Phase 5: Fleet Management & Super Admin
**Spec Name:** `spec-super-admin-ops.md`  
**Focus:** The "God Mode" view and the Argon2id security layer.

*   **Objective:** Implement the fleet heartbeat monitoring, OTA update triggers, and the "Nuclear Delete" failsafes.
*   **Key Deliverable:** A dark-mode dashboard for managing multiple tenants and monitoring Edge PC temperatures/storage.
*   **Success Metric:** Successful remote "Reboot Service" command sent via MQTT to a Phase 1 Edge device.
