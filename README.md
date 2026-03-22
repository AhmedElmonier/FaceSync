# FaceSync: Multi-Modal Edge-to-Cloud Attendance SaaS

FaceSync is an enterprise-grade attendance ecosystem engineered for high resilience and bilingual (Arabic/English) environments, specifically optimized for the Egyptian market.

## 🚀 Project Vision
To provide a seamless, AI-driven attendance experience with 100% data integrity, even during internet blackouts, through a hybrid Edge-to-Cloud architecture.

### Key Success Metrics
- **Performance:** < 200ms inference latency on edge nodes.
- **Accuracy:** < 0.001% False Acceptance Rate.
- **Multimodal:** Specialized periocular module for Niqab/Mask detection.
- **Localization:** Full RTL/LTR support without page reloads.

## ✨ Core Features
- **Bilingual UI/UX:** Instant seamless switching between Arabic and English (RTL/LTR).
- **Edge-First Resilience:** 30-day offline storage with automated batch synchronization.
- **Advanced AI Pipeline:** RetinaFace + ArcFace embeddings with HNSW indexing.
- **Maker-Checker Governance:** Secure administrative oversight for manual adjustments.
- **Fleet Management:** Real-time health monitoring and OTA updates for edge devices.

## 🛠 Tech Stack
- **Edge:** Python, OpenCV, PyTorch, SQLite, HNSW.
- **Backend:** FastAPI, PostgreSQL (RLS), MQTT (AWS IoT Core).
- **Frontend:** Next.js (TypeScript), Tailwind CSS, `next-intl`.
- **Mobile:** Flutter (TFLite).

## 📅 Implementation Roadmap
1. **Phase 1:** AI Edge Inference Core
2. **Phase 2:** Resilient SQLite & Sync Engine
3. **Phase 3:** Multilingual Cloud API (SaaS Brain)
4. **Phase 4:** Bilingual HR Dashboard (Client UI)
5. **Phase 5:** Fleet Management & Super Admin

---
*Lead: Ahmed El Monier*
