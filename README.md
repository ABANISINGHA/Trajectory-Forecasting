# Trajectory-Forecasting

Conference Paper submitted in 16th ICCCNT 2025: [link](https://drive.google.com/file/d/1DN9Fm6LfY6LFSSxkDiC4ZIL2E9_9n4uq/view?usp=sharing)


This repository contains the full implementation of a **spatio-temporal trajectory forecasting model** for autonomous vehicles using a **Graph Attention Network (GAT)** and **GRU-based encoder-decoder architecture**. The model is evaluated on the real-world **NGSIM US-101 highway dataset**, and incorporates **social pooling** and **temporal attention** for improved interaction modeling.

---

## 🔍 Project Overview

- **Task**: Predict future coordinates of an ego vehicle based on its past motion and nearby vehicles' interactions.
- **Input**: Sequence of 5 graph-structured traffic scenes (5 seconds of past frames).
- **Output**: 4 future position predictions (3 seconds ahead).
- **Approach**:
  - Spatial encoding via **Graph Attention Network (GAT)**.
  - Interaction context captured using **learned social pooling**.
  - Temporal modeling using **GRU** with **attention over encoder history**.
  - Decoder uses **teacher forcing** and outputs future 2D coordinates.

---

## 🧠 Model Architecture

- `GATConv`: Encodes per-frame spatial graph.
- `MLP`: Pools features from neighbor nodes.
- `GRU Encoder`: Processes ego-social history.
- `Multihead Attention`: Adds focus to relevant past steps.
- `GRU Decoder`: Autoregressively predicts future trajectory.
- `Linear`: Final coordinate regression.

![Model Diagram](docs/model_architecture.png)

---

## 📁 Dataset

We use the [NGSIM US-101](https://ops.fhwa.dot.gov/trafficanalysistools/ngsim.htm) dataset, which contains detailed freeway traffic data.
![Alt Text]([https://example.com/path/to/image.png](https://www.fhwa.dot.gov/publications/research/operations/07030/images/07030fig1.jpg))

### 🛠 Data Processing

- CSV converted to graph sequences per ego vehicle.
- Each graph:
  - Nodes: Vehicles (features: `Local_X`, `Local_Y`, `v_Vel`, `v_Acc`, `Lane_ID`)
  - Edges: Binary proximity-based (no edge features yet)
- Output: `[past_graphs, adjacency_matrices, future_coordinates]`

---

## ⚙️ Installation

```bash
git clone https://github.com/yourusername/trajectory-forecasting-gatgru.git
cd trajectory-forecasting-gatgru
pip install -r requirements.txt

