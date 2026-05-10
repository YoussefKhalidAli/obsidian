**Amazon Quantum Ledger Database (QLDB)** is a **fully managed ledger database** that provides a **cryptographically verifiable, immutable transaction log**.

---
###  Simple idea

> QLDB = a database where **you cannot change or delete history**, and you can **prove it hasn’t been tampered with**

---

### Key characteristics

|Feature|Description|
|---|---|
|Immutable ledger|Once data is written, it **cannot be altered or deleted**|
|Cryptographic verification|You can **prove data integrity** using hashes|
|Centralized|Managed by AWS (not decentralized like blockchain)|
|Transparent history|Full history of all changes is preserved|
|SQL-like queries|Uses PartiQL (similar to SQL)|

---

### How it works (conceptually)

Every change:

1. Is recorded as a transaction
2. Linked using cryptographic hashes
3. Forms a **chain of trust**
 If someone tries to modify past data → it becomes detectable

---

### Use cases

- Financial transaction records
- Audit logs
- Supply chain tracking
- Insurance claims history
- Compliance systems

---

### QLDB vs Blockchain

|Feature|QLDB|Blockchain|
|---|---|---|
|Control|Centralized (AWS)|Decentralized|
|Performance|Fast|Slower|
|Trust model|Trusted authority|Trustless|
|Complexity|Simple|Complex|

---

### When to use QLDB

Use it when you need:

- **Trusted, tamper-proof records**
- **Auditability**
- **Central authority (no need for decentralization)**