# Federated AI-driven Energy Services

Orchestrator component for managing and optimizing Federated Learning (FL) processes across distributed edge nodes.

The Orchestrator FL API enables:

* Node registration (resources, energy profile, data stats)
* Node clustering for optimized FL execution
* Collection of training metrics
---

## Prerequisites

* A set of nodes running Federated Learning workloads
* `Docker` and `Docker Compose` installed
* Network connectivity between nodes and orchestrator
---

## Setup

### 1. Clone the Orchestrator UC2 Repository

```bash
git clone https://github.com/HEDGE-IoT/orchestrator-blueprint_orch_components_uc2
cd orchestrator-blueprint_orch_components_uc2/orchestrator_fl_api
```

---

### 2. Configure Deployment (Optional)

Edit `docker-compose.yaml` if needed:

```yaml
  ports:
    - "8000:8000"
```

---

### 3. Deploy the Orchestrator

```bash
docker-compose up -d
```

Verify service is running:

```bash
docker ps
```

---

## API Access

Open Swagger UI for a detailed documentation over the exposed methods, body, responses and expected formats:

```
http://<HOST_IP>:<APP_PORT>/hedge/orch-fl-p2p/docs
```

---

## Usage

### 1. Register Federated Learning Nodes

Endpoint:

```
POST /node/register
```

Provide:

* CPU / RAM (optional)
* Energy profile (optional)
* Software: Hierarchical or Peer-to-Peer (P2P by default)
---

### 2. Perform Node Clustering

Endpoint:

```
POST /cluster/agglomerative
```

The orchestrator:

* Groups nodes with similar computational characteristics and energy profiles

Output:

* List of clusters for training coordination

---

### 3. Execute Federated Learning

Use the clustering output to:

* Assign nodes to groups
* Optimize communication overhead
* Run training rounds

---

### 4. Send Training Metrics

Endpoint:

```
POST /metrics/node 
```
or
```
POST /metrics/cluster
```
Examples of metrics:

* Exchange Data Size
* Transmission Time
* Communication Blocking Time
* CPU Mean Usage Percent
* Memory Usage
* Power Consumption
* Accuracy

---
## Validation

* Verify nodes are registered:

```bash
GET /node/all
```

* Verify clusters are generated:

```bash
GET /cluster/all
```

* Check metrics ingestion:

```bash
GET /metrics/cluster/{cluster_id}
```

---
