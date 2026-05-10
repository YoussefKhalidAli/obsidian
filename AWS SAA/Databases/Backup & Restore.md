## 1. Automated Backups

- **Definition:** AWS RDS automatically creates a daily full backup of your database during your **backup window**.
- **Transaction Logs:** Every 5 minutes, RDS backs up the transaction logs.
  - This allows **point-in-time recovery** (PITR) up to 5 minutes ago.
- **Retention Period:** You can set **1–35 days** of retention.
  - Setting `0` disables automated backups for RDS.
- **Benefits:**
  - Protects against accidental data loss.
  - Enables recovery to any specific point in time within the retention period.

---

## 2. Manual DB Snapshots

- **Definition:** Manually triggered backups created by the user.
- **Retention:** Can be retained **indefinitely** until explicitly deleted.
- **Comparison with Automated Backups:**
  - Automated backups expire automatically.
  - Manual snapshots allow long-term storage.
- **Cost-saving Tip:**
  - If you use an RDS instance infrequently (e.g., 2 hours/month):
    1. Use it, then create a **snapshot**.
    2. Delete the original database to save costs.
    3. Restore from the snapshot when needed.

---

## 3. Aurora Backups

- Similar to RDS backups:
  - **Automated backups**: 1–35 days retention, **cannot be disabled**.
  - **Point-in-time recovery**: Recover to any point in the retention window.
  - **Manual snapshots**: Retained indefinitely.
- **Key Difference:** Automated backups on Aurora cannot be disabled.

---

## 4. Restore Options

### a) Restore into a New Database
- Restoring an **automated backup** or **manual snapshot** always creates a **new database**.

### b) Restore MySQL RDS Database from S3
- Workflow:
  1. Backup your on-premises MySQL database.
  2. Upload backup to **Amazon S3** (object storage).
  3. Restore backup from S3 into a **new RDS MySQL instance**.

### c) Restore Aurora MySQL from S3
- Requires **Percona XtraBackup**:
  1. Backup on-premises MySQL using **Percona XtraBackup**.
  2. Upload backup to **Amazon S3**.
  3. Restore into a **new Aurora MySQL cluster**.
- **Key Difference:** Aurora requires Percona XtraBackup, RDS MySQL does not.

---

## 5. Aurora Database Cloning

- **Definition:** Create a **new Aurora database cluster** from an existing one.
- **Use Case:** Quickly create a **staging/test environment** from production.
- **Advantages:**
  - Faster than snapshot + restore.
  - Efficient and cost-effective.
- **How it works (Copy-on-Write):**
  1. Initially, cloned DB shares the **same data volume** as production → **instant creation**.
  2. Updates to production or staging DB allocate new storage **only for changed data**.
- **Benefits:**
  - No impact on production database.
  - Minimal storage costs until data diverges.

---

## 6. Summary of Backup & Restore Options

| Feature                          | RDS MySQL/PostgreSQL   | Aurora MySQL/PostgreSQL |
|---------------------------------|----------------------|------------------------|
| Automated Backups               | Yes, configurable    | Yes, cannot be disabled |
| Transaction Logs                | Every 5 minutes      | Every 5 minutes        |
| Manual Snapshots                | Yes, indefinite      | Yes, indefinite        |
| Restore from S3                 | Yes                  | Yes, via Percona XtraBackup |
| Point-in-time Recovery (PITR)   | Yes                  | Yes                    |
| Cloning                          | N/A                  | Yes, fast with copy-on-write |
