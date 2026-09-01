# SENTINEL // Temporal-Heterogeneous Graph Forensic Intelligence Platform

> **Continuous-Time Inductive TH-GAT & Subgraph-Based XAI Platform for Bitcoin Network & Blockchain Surveillance**  
> **Smart India Hackathon (SIH) 2026** | **Problem Statement ID:** `26146`  
> **Organization:** National Technical Research Organisation (**NTRO**) | **Theme:** Blockchain & Cybersecurity  
> **Environment:** 100% Offline / Air-Gapped Workstation & Linux Forensic Ready  

---

## Overview
**SENTINEL** is a state-of-the-art forensic intelligence platform that correlates **P2P network-layer telemetry** (IPs, ASNs, propagation timings, Tor/VPN flags) with **on-chain blockchain UTXO transactions** (wallet scripts, fee rates, change mechanisms).

It models the entire ecosystem as a **Dynamic Heterogeneous Temporal Graph** $G = (V, E, \mathcal{T})$ and executes an **Inductive Continuous-Time Temporal-Heterogeneous Graph Attention Network (TH-GAT)** with **Bochner's Theorem Continuous Fourier Time Encoding**, **Graph Contrastive Learning (GraphCL)**, and **Subgraph-based XAI (PGExplainer / GNNExplainer)** to detect, isolate, and explain money laundering, ransomware campaigns, and mixer services in sub-second latency.

---

## Quickstart Guide

### 1. Prerequisites & Installation
Ensure you have Python 3.10+ installed. Install the self-contained dependencies:
```bash
pip install -r requirements.txt
```

### 2. Launch Tactical Web Dashboard & REST API
```bash
python main.py
```
Open **`http://127.0.0.1:8000`** in your browser to access the interactive link-analysis graph, real-time threat queue, DuckDB SQL console, and automated case dossier generator.

### 3. Headless Multi-Format Ingestion & Analysis (CSV, JSON, XML)
Execute command-line forensic analysis on any standard telemetry stream:
```bash
# Ingest and analyze a master JSON dataset:
python main.py --input data/transactions.json

# Ingest and analyze a CSV transaction stream:
python main.py --input sample_feed.csv

# Ingest and analyze an XML telemetry payload:
python main.py --input network_capture.xml
```

### 4. Synthetic Adversarial Dataset Generation
Generate high-fidelity synthetic Bitcoin transactions with ground-truth adversarial typologies (Ransomware, CoinJoin mixers, Peel Chains, Smurfing):
```bash
# Generate and immediately analyze 200 synthetic transactions:
python main.py --generate 200
```

### 5. Automated Court-Ready Dossier Export
Generate markdown forensic dossiers with SHA-256 cryptographic seals for top-ranked investigative leads:
```bash
python main.py --input data/transactions.json --export data/exported_dossiers
```

---

## End-to-End System Architecture

```
+-----------------------------------------------------------------------------------+
|            MULTI-FORMAT HIGH-THROUGHPUT INGESTION (CSV / JSON / XML)              |
|   - Zero-Copy In-Memory Storage  - Vectorized SQL Filtering  - Sub-ms Aggregations|
+------------------------------------------+----------------------------------------+
                                           |
                                           v
+-----------------------------------------------------------------------------------+
|               OFFLINE NETWORK & GEOIP ENRICHMENT ENGINE (AIR-GAPPED)              |
|   - Interval Tree IP Resolver   - ASN Registry   - Tor/VPN & Bulletproof Detector |
+------------------------------------------+----------------------------------------+
                                           |
                                           v
+-----------------------------------------------------------------------------------+
|               DUAL-LAYER DYNAMIC HETEROGENEOUS GRAPH ENGINE                       |
|   - Network Layer: (IP) ──[BROADCASTS / PORT / ASN]──> (TX)                       |
|   - Financial Layer: (Wallet) ──[SPENT_IN / OUTPUTS_TO]──> (TX)                   |
|   - Common-Input Ownership Heuristic (CIOH / DSU) & Peel Chain Tracing            |
+------------------------------------------+----------------------------------------+
                                           |
                                           v
+-----------------------------------------------------------------------------------+
|            TEMPORAL HETEROGENEOUS GRAPH ATTENTION NETWORK (TH-GAT)                |
|   - Continuous Fourier Time Encodings via Bochner's Theorem: Phi_k(dt)            |
|   - Relation-Specific Multi-Head Attention modulated by Financial Volumes         |
|   - Graph Contrastive Learning (GraphCL) for Zero-Day Topological Anomaly Scoring |
+------------------------------------------+----------------------------------------+
                                           |
                                           v
+-----------------------------------------------------------------------------------+
|             SUBGRAPH-BASED EXPLAINABLE AI (PGEXPLAINER / GNNEXPLAINER)            |
|   - Extraction of Minimal 2-to-3 Hop Causal Subgraphs                             |
|   - Evidence-Backed Synthesized Findings & SHAP Feature Attributions             |
|   - Court-Ready Forensic Case Dossier Generator with SHA-256 Digital Seals        |
+------------------------------------------+----------------------------------------+
                                           |
                                           v
+-----------------------------------------------------------------------------------+
|                TACTICAL DEFENSE DASHBOARD & LINK-ANALYSIS CANVAS                  |
|   - Force-Directed Graph  - Causal Subgraph Inspector  - Live Threat Matrix       |
|   - In-Memory DuckDB SQL Console  - Multi-Hop Flow Tracer  - One-Click Exports    |
+-----------------------------------------------------------------------------------+
```

---

## Mathematical Formulations

### 1. Continuous-Time Fourier Time Encoding (Bochner's Theorem)
Instead of discrete time slices (which lose micro-burst laundering patterns), scalar time deltas $\Delta t$ are mapped into continuous harmonic representations:

$$\Phi_k(\Delta t) = \cos(\omega_k \Delta t + \psi_k) \quad \text{where} \quad \omega_k = \frac{1}{10^{k / d_{\text{time}}}}$$

### 2. Relation-Specific Heterogeneous Attention
For node $i$ (e.g. Wallet/IP) and neighbor $j$ (e.g. TXID) under relation $r$:

$$\alpha_{ij}^r = \frac{\exp\left(\text{LeakyReLU}\left(\mathbf{a}_r^T [\mathbf{W}_{\text{src}} h_i \,\|\, \mathbf{W}_{\text{dst}} h_j \,\|\, \mathbf{W}_{\text{edge}} [\log(1 + \text{amount}) \,\|\, \Phi(\Delta t)]]\right)\right)}{\sum_{l \in \mathcal{N}_i^r} \exp\left(\text{LeakyReLU}\left(\mathbf{a}_r^T [\mathbf{W}_{\text{src}} h_i \,\|\, \mathbf{W}_{\text{dst}} h_l \,\|\, \mathbf{W}_{\text{edge}} e_{il}]\right)\right)}$$

Multi-head message aggregation with LayerNorm:

$$h_i^{(l+1)} = \text{LayerNorm}\left(\sigma\left(\mathop{\Big\Vert}_{k=1}^K \sum_{j \in \mathcal{N}_i} \alpha_{ij}^{k, r} \mathbf{W}_{\text{dst}}^k h_j^{(l)}\right) + \mathbf{W}_{\text{res}} h_i^{(l)}\right)$$

### 3. Graph Contrastive Learning (GraphCL) & Anomaly Scoring
Self-supervised topological reconstruction evaluates embedding displacement under temporal edge perturbation:

$$\mathcal{S}_{\text{anomaly}} = \left(1.0 - \text{CosineSimilarity}\left(z_i^{\text{nominal}}, z_i^{\text{perturbed}}\right)\right) \times 50.0$$

### 4. Subgraph Causal Extraction (PGExplainer)
Extracts the minimal subgraph $G_s \subset G$ maximizing mutual information with respect to the neural prediction:

$$\max_{G_s} I(Y; G_s) = H(Y) - H(Y \mid G = G_s)$$

---

## Forensic Heuristics Engine

* **Common Input Ownership Heuristic (CIOH):** Groups distinct wallet addresses participating as inputs in non-CoinJoin transactions into single pseudo-entities using Disjoint Set Union (DSU).
* **Peel Chain Tracer:** Identifies recursive peeling sequences ($\ge 3$ consecutive hops) where an actor disperses small fractions while routing the primary balance to fresh change wallets.
* **Equal-Output CoinJoin Detector:** Flags Wasabi and Whirlpool mixer pools through equal-denomination output frequency clustering and high transaction entropy.
* **Smurfing & Structuring:** Detects 1-to-Many fan-out layering ($\ge 5$ outputs) and Many-to-1 fan-in consolidation structures designed to evade threshold interdiction.

---

## REST API Reference

The platform exposes a high-performance REST API (FastAPI) for programmatic integration:

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/api/status` | System health, loaded records count, graph topology size, and DuckDB stats |
| `GET` | `/api/analysis/overview` | Aggregated threat breakdown, total volume analyzed, heuristic summary, and traffic routes |
| `GET` | `/api/leads` | Ranked, explainable threat leads with filters (`tier`, `category`, `limit`) |
| `GET` | `/api/leads/{id}/dossier` | Complete evidence-backed case dossier with SHA-256 digital integrity seal |
| `GET` | `/api/graph` | Full multi-layer graph serialization for interactive Vis.js visualization |
| `GET` | `/api/graph/explain/{target_id}` | Minimal 2-to-3 hop causal subgraph isolating the exact laundering path |
| `GET` | `/api/graph/ego/{entity_id}` | Ego-network neighborhood extraction around a specific wallet/TX/IP |
| `POST` | `/api/graph/trace` | Multi-hop shortest path and fund taint flow discovery between entities |
| `POST` | `/api/columnar/query` | Executes analytical in-memory SQL queries directly against DuckDB |
| `GET` | `/api/columnar/bursts` | IP-level high-frequency broadcast burst detection using SQL window functions |
| `GET` | `/api/columnar/asns` | Autonomous System distribution and proxy volume aggregation |
| `POST` | `/api/ingest/file` | Streaming multipart file upload (`.json`, `.csv`, `.xml`) |
| `POST` | `/api/generate-synthetic` | On-demand generation and pipeline re-analysis of $N$ synthetic transactions |
| `GET` | `/api/export/csv` | One-click export of flagged forensic threat leads as CSV |
| `GET` | `/api/export/json` | Export of normalized, enriched dataset as formatted JSON |

---

## Project Structure

```
├── main.py                           # Single unified entrypoint (Web Platform & CLI)
├── requirements.txt                  # Dependency specifications
├── README.md                         # Complete project documentation & architecture
│
├── core/                             # Ingestion, Columnar DB & Correlation
│   ├── db_engine.py                  # High-Throughput In-Memory DuckDB Columnar Engine
│   ├── parser.py                     # Streaming Multi-Format Parser (CSV/JSON/XML)
│   ├── geoip_resolver.py             # Offline Interval Tree GeoIP & ASN Resolver
│   ├── correlator.py                 # Dual-Layer Network & Blockchain Fusion
│   └── generator.py                  # Realistic Adversarial Synthetic Dataset Generator
│
├── graph_engine/                     # Graph Intelligence & Heuristics
│   ├── entity_graph.py               # Dynamic Heterogeneous Graph Engine
│   ├── heuristics.py                 # CIOH, Peel Chain, CoinJoin Mixer & Smurfing Detectors
│   └── path_tracer.py                # Multi-Hop Shortest Path & Fund Flow Tracer
│
├── ai_models/                        # Multi-Model AI/ML Core
│   ├── th_gat.py                     # Continuous-Time Temporal Heterogeneous GAT (TH-GAT)
│   ├── gnn_detector.py               # TH-GAT Inference & Anomaly Manager
│   ├── feature_extractor.py          # 24-Dimensional Multi-Modal Feature Vectorizer
│   └── ensemble_engine.py            # Calibrated Multi-Factor Threat Scoring (0-100)
│
├── explainability/                   # Explainable AI (XAI) & Causal Subgraphs
│   ├── subgraph_explainer.py         # Minimal Causal Subgraph Extraction (PGExplainer)
│   ├── xai_engine.py                 # SHAP Feature Attribution & Evidence Synthesizer
│   ├── lead_ranker.py                # Actionable P1-P4 Lead Prioritization & Actions
│   └── forensic_dossier.py           # Automated Case Briefs with SHA-256 Digital Seals
│
├── api/                              # REST API Backend
│   ├── app.py                        # FastAPI Application & Static File Mount
│   └── routes.py                     # Analytical Endpoints, Ingestion & Graph Routes
│
├── web/                              # Cyber-Forensic Web Dashboard
│   ├── index.html                    # Single Page Application Dashboard
│   ├── css/style.css                 # Dark Mode Glassmorphism Theme
│   └── js/                           # Graph Visualizer, Causal Subgraph Inspector, Charts
│
└── data/                             # Master Dataset & Offline GeoIP Database
    ├── exported_dossiers/            # Exported forensic case dossiers
    ├── geoip_asn_db.json             # Bundled Offline GeoIP / ASN Intelligence
    └── transactions.json             # Formatted Master Bitcoin Dataset
```

---

## Offline Air-Gapped Operation Guarantees
* **Zero External Network Dependencies**: Embedded offline GeoIP database in `data/geoip_asn_db.json`.
* **Bundled Frontend Assets**: Vis.js and Chart.js are stored locally in `web/js/` to eliminate external CDN calls.
* **Local Model Execution**: PyTorch TH-GAT models execute 100% locally on CPU or CUDA GPU.
* **Air-Gapped Workstation Ready**: Tested and certified for air-gapped Linux forensic workstations without internet access.
