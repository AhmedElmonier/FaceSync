# PRD: Multi-Modal Edge-to-Cloud Attendance SaaS (v2.6)

**Project Lead:** Ahmed El Monier
**System Status:** Architecture Locked – Bilingual Edition (AR/EN)

## 1. Project Vision & Bilingual Success Metrics
An enterprise-grade attendance ecosystem engineered for the Egyptian market, providing seamless transitions between Arabic (RTL) and English (LTR) across all touchpoints.

### Core Success KPIs
| Category | Metric | Target Objective |
| :--- | :--- | :--- |
| User Experience | Inference Latency | $< 200\text{ms}$ (using HNSW index). |
| User Experience | Language Switch | Instant (No page reload for Dashboard/Kiosk). |
| AI Accuracy | $FAR$ (False Acceptance) | $< 0.001\%$ (High-security threshold). |
| AI Accuracy | $FRR$ (Face) | $< 1\%$ (Standard pose/lighting). |
| AI Accuracy | $FRR$ (Periocular) | $< 5\%$ (Specialized Niqab/Mask module). |

## 2. Bilingual UI/UX & Localization (i18n)
### 2.1 The RTL (Right-to-Left) Mandate
*   **Directional Mirroring:** The Dashboard must detect the `ar` locale and wrap the UI in a `<div dir="rtl">`. Sidebar, icons, and text alignment must flip 180°.
*   **Logical CSS:** Use Tailwind CSS Logical Properties (e.g., `ps-4` for padding-start instead of `pl-4`) to ensure layout integrity across both scripts.
*   **Typography:** Optimized dual-font stack (**IBM Plex Sans Arabic** for Arabic; **Inter** for English).

### 2.2 Edge Kiosk Localization
*   **Bilingual Audio:** Localized audio prompts (e.g., "Identity Confirmed" vs "تم تأكيد الهوية").
*   **Visual Cues:** Heavy reliance on universal iconography (Green Check / Red X).
*   **Dual-Language Enrollment:** Fully bilingual guided wizard to ensure workers understand head-pose instructions.

## 3. The AI Pipeline & Enrollment UX
### 3.1 Enrollment "Genesis" Flow
*   **Guided Capture:** 5-angle high-res capture (Center, $\pm 30^\circ$ Yaw, $\pm 15^\circ$ Pitch). AI auto-captures based on specific Euler angles.
*   **Search Engine:** HNSW (Hierarchical Navigable Small World) indexing for $O(\log N)$ speed.
*   **Mesh Sync:** Encrypted vector blobs synced via a Blind Cloud Relay with a 60-second SLA.

### 3.2 Decision Boundary
*   **Green Zone ($C \ge 0.85$):** Auto-commit.
*   **Gray Zone ($0.75 \le C < 0.85$):** Log-and-continue with "Unverified" flag for Manager review.
*   **Red Zone ($C < 0.75$):** Instant rejection; trigger Hard Fallback (RFID/Manual).

## 4. Technical Architecture & Resilience
### 4.1 Connectivity & Data Sync
*   **Telemetry (MQTT):** Real-time heartbeat and OTA triggers via AWS IoT Core.
*   **Data Sync (HTTPS):** Batch logs via HTTPS POST with Exponential Backoff.
*   **Offline Blackout:** 30-day storage. At 90% capacity, prioritize Clock-In events over telemetry. Warning at 80% (8GB) capacity.

### 4.2 Temporal Integrity
*   **NTP Guard:** Mandatory sync every 60 mins.
*   **Drift Rejection:** Cloud rejects syncs $>\pm 5\text{ mins}$ from Server Time.

## 5. Governance & Security
### 5.1 Bilingual Maker-Checker Workflow
*   **Maker:** Manager initiates edit; system records original vs. proposed data.
*   **Checker:** Admin receives alerts in their `preferred_language`. The Approvals Inbox displays the reason for change with a 1-click **[Translate]** toggle.
*   **Alerting:** WhatsApp/Email alerts follow the user's stored language preference.

### 5.2 Deletion & Failsafes
*   **Individual Purge:** Confirmed "Wipe Vector" broadcast across the mesh.
*   **Tenant Deletion:** Text-match challenge (Type Company Name to Confirm) + 30-day "Soft-Delete" tombstone period.
*   **No-Trap Backups:** AES-256 keys derived via Argon2id from Admin Password + Tenant UUID.

## 6. Tech Stack Summary
*   **Edge:** Python (OpenCV, PyTorch, HNSW, SQLite).
*   **Backend:** FastAPI (Babel i18n), PostgreSQL (Row-Level Security).
*   **Frontend:** Next.js, TypeScript, Tailwind CSS, `next-intl`.
*   **Mobile:** Flutter (i18n-ready + TFLite).
