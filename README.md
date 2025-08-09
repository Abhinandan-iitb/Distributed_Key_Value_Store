# Distributed Key-Value Store

##  Overview

This project implements a **distributed key-value store** that supports **multiple cache coherency and prefetching mechanisms**, designed to store and retrieve data efficiently across a cluster of interconnected nodes.
It leverages **consistent hashing** to allow dynamic node additions/removals without costly data reorganization, and uses **JSON-based persistent storage** for durability.

---

##  Features

* **Peer-to-peer server architecture** with consistent hashing
* **Dynamic node management** — nodes can join/leave seamlessly
* **Data replication** for improved fault tolerance
* **JSON-based storage** for persistence across restarts
* **Basic CRUD operations** (Create, Retrieve, Update, Delete)
* **Multithreaded server handling** for concurrent client requests
* **Automatic network scanning** to discover active nodes

---

##  System Design

### **1. Server**

* Uses **consistent hashing** to map keys to nodes
* Supports distributed communication to maintain data consistency
* Stores data on the responsible node and its successors (replication)

### **2. Database**

* Stores key-value pairs in a local JSON file
* Ensures persistence across restarts
* CRUD operations are supported:

  * **Create** — Add new key-value pairs
  * **Search** — Retrieve values by key
  * **Update** — Modify existing values
  * **Delete** — Remove key-value pairs

---

##  Implementation Details

1. **Node Setup**

   * Node determines its position in the consistent hash ring
   * Joins network by contacting known nodes for predecessor/successor info

2. **Key Storage**

   * Hashes the key to find the target node
   * Stores the key-value pair on the node and its successors

3. **Database Management**

   * Each server has an independent JSON file for storage
   * Allows isolation between nodes

4. **Concurrency**

   * Multithreading handles multiple requests in parallel

5. **Error Handling**

   * Detects server unavailability and retries failed operations

---

##  Evaluation

**Tested Metrics:**

* Insertion time
* Retrieval time
* Deletion time

**Observation:**

* Retrieval is faster than deletion (due to I/O overhead in deletion operations).
* System handles multiple concurrent client requests efficiently.

---

##  Limitations & Future Improvements

* Improve **data replication** for higher fault tolerance
* Handle **multiple node failures** more gracefully
* Optimize update & delete operations (Chord algorithm)
* Achieve better **load distribution** across the key space

---

##  Getting Started

1. **Clone the repository:**

```bash
git clone https://github.com/Abhinandan-iitb/Distributed_Key_Value_Store.git
```

2. **Install dependencies** (if applicable):

```bash
pip install -r requirements.txt
```

3. **Run the server:**

```bash
python server.py
```

4. **Run the client:**

```bash
python client.py
```

---

## 👨‍💻 Authors

* **Vishal Kumar Singh** (24M0742)
* **Abhinandan Kumar** (24M0788)

**Guided by:** Prof. **Purushottam (Puru) Kulkarni**, IIT Bombay

