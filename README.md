# 📂 Azure Notes – Structured Stored Points

## 🟠 Azure Storage Concepts

https://share.google/BUANPFLQwlDgKwAPZ

### ✅ Azure Blob Storage
1. Azure Blob Storage is a service that stores unstructured data in the cloud as objects or blobs. Blob stands for Binary Large Object. Blob Storage is also referred to as object storage or container storage.
2. Azure Blob Storage uses a container resource to group a set of blobs. A blob can't exist by itself in Blob Storage. A blob must be stored in a container resource.
3. To access the blob's content, you can assign it to the hot, cool, or cold tier to trigger the process referred to as rehydration.
4. Lifecycle management: Use Azure Blob Storage lifecycle management policy rules. Transition blobs to a cooler storage tier (Hot→Cool, Hot→Archive, Cool→Archive) to optimize for performance and cost.
5. Expand your knowledge in the Manage the Azure Blob storage lifecycle training module.
6. You can enable Blob versioning to maintain previous versions of an object. This allows recovery of modified or deleted data.

### ✅ Storage Tools
7. Every file on your computer—every photo, song, document, and program—is ultimately just a sequence of 0s and 1s.
8. Azure Storage Explorer allows upload, download, and management of blobs, files, queues, tables, Data Lake Storage entities, and managed disks. It also lets you preview data and configure permissions.
9. Exercise: Provide storage for the public website.
10. Enable version-level immutability.
11. Configure a shared access signature (SAS), including the URI and SAS parameters.

### ✅ Storage Security
12. Azure Storage Security — Quick Recap:
   - Encryption at Rest: AES-256, BitLocker/dm-crypt
   - Encryption in Transit: HTTPS, SMB 3.0
   - Encryption Models: service-managed, customer-managed (Key Vault/HSM), client-side
   - Shared Key Authorization: risky, avoid
   - Shared Access Signatures (SAS): scoped, temporary
   - Microsoft Entra ID + Managed Identity: best practice
   - RBAC: role-based fine-grained access
   - Storage Analytics: logging for tracing/diagnosis
13. Role-Based Access Control (RBAC): Azure Storage Insights integrates with RBAC, Entra ID, connection strings, ACLs to ensure secure access.
14. Different ways to secure Azure Storage.
15. How to configure SAS for the Azure storage account.

### ✅ Storage Redundancy
16. Locally Redundant Storage (LRS): Data replicated 3 times on separate racks in the same datacenter. Protects from local failures.

### ✅ File Shares
17. Mount SMB Azure file share on Linux using CIFS client. Mount on-demand or persistently.
18. Open port 445 for SMB. If blocked, use VPN or ExpressRoute with private endpoints.
19. Azure Storage Explorer requires both management and data layer permissions, needing Entra ID permissions for storage accounts and containers.

### ✅ Azure File Sync
20. Azure File Sync with cloud tiering: Windows Server acts as a cache, with frequently used files local and older files stored in the cloud.
21. NTFS is like Git’s internal engine. Azure File Sync leverages NTFS for tiering and recall.

### ✅ Storage Terminology Analogies
22. MBR → Old filing cabinet  
23. GPT → Modern shelf system  
24. VHD → Portable disk image  
25. SCSI → High-speed disk connector  

---

## 🟠 Azure Virtual Machines & Compute

### ✅ VM Pricing and Images
26. Hourly price varies based on VM size and OS. Linux VMs are cheaper due to no OS license charge.
27. Azure Compute Gallery helps manage multiple images and replicate them to needed regions.

### ✅ Workload Types
28. IO-intensive workloads include SAP HANA, SQL, Oracle, and other transaction-heavy workloads.

### ✅ Terraform Integration
29. Azure provides a Terraform provider to configure resources programmatically.

### ✅ VM I/O Tuning
30. blk-mq: Parallel disk access for faster throughput.
31. I/O Scheduler: none for blk-mq, noop for older blk.
32. LVM Striping: Combines multiple disks for better IOPS and speed.

### ✅ LVM Management
33. Logical Volume Manager helps flexibly manage disks by combining and resizing them.

### ✅ RHEL in Azure
34. Deploy RHEL as the OS inside a VM. You control everything within the VM.

### ✅ Accelerated Networking
35. Support depends on the VM size.

### ✅ Linux VM Popularity
36. Azure Linux VMs are widely used because they fit open-source ecosystems.

### ✅ VM Extensions
37. Post-provisioning tasks like installing packages, configuring services, and bootstrapping without SSH.
38. Examples: Custom Script Extension, Log Analytics Agent, Security Extensions.

### ✅ Image Identifiers
39. URN = full image ID, UrnAlias = shortcut used to select OS images.

---

## 🟠 Scaling & Availability

### ✅ Spreading Algorithm
40. Max spreading spreads VMs across as many fault domains as possible. Fixed spreading spreads across exactly five.

### ✅ Availability Features
41. Availability sets and zones improve fault tolerance and high availability.
42. Availability sets resemble servers in separate racks.
43. Availability zones resemble buildings in the same city.

### ✅ Scale Margin
44. Ensure maximum and minimum instances are different with an adequate margin. Use autoscaling rules.

---

## 🟠 Web Apps & Development

### ✅ Web App Creation
45. Create a web app using the Azure portal and refer to the documentation:  
https://learn.microsoft.com/en-us/training/modules/configure-azure-app-services/3-create-app-service

---

## 🟠 Backup & Recovery

### ✅ Access Tiers
46. Access tiers categorize data storage based on frequency and retention needs.

### ✅ Azure Backup Vault vs Azure Key Vault
47. Azure Backup Vault stores backups for VMs and databases.
48. Azure Key Vault stores secrets, keys, and certificates securely.
49. Backup Vault = Data locker; Key Vault = Security safe.

### ✅ Backup Recovery Concepts
50. Recovery Time Objective (RTO): Time allowed to restore systems.
51. Recovery Point Objective (RPO): Acceptable data loss in time.
52. Backup frequency, recovery timelines, and real-world scenarios.

### ✅ Backup Automation
53. Automate backups and monitor restore speeds to meet RTO and RPO goals.

### ✅ Tiering in Backup
54. Classifying backup data into tiers based on access and retention.

---

## 🟠 Containers

### ✅ Container Basics
55. Containers offer lightweight isolation with fewer resources than VMs.
56. They can be deployed with Docker or orchestrators like Azure Container Apps.
57. Use Azure Disks or Files for storage.
58. Container groups are collections of containers scheduled on the same host.
59. Containers can be recreated quickly if a node fails.

### ✅ Container Networking
60. Port mapping isn't supported as containers share a port namespace.

### ✅ Persistence with Azure Files
61. Containers can mount Azure Files as volumes for persistent storage.

### ✅ File Sharing Benefits
62. Persistence, sharing between containers, security via SAS or keys, and automation.

---

## 🟠 Frameworks & Tools

### ✅ gRPC
63. gRPC is a high-performance RPC framework used in microservices and mobile apps. It uses HTTP/2 and Protocol Buffers.

### ✅ KEDA
64. Kubernetes Event-Driven Autoscaling (KEDA) scales apps based on external events.

### ✅ ACA Integration
65. Azure Container Apps integrates with Logic Apps, Functions, and Event Grid. AKS integrates with policies, monitoring, and security.

---

## 🟠 CSS & Angular

### ✅ SCSS Extension
66. SCSS is an extension of CSS adding variables, nesting, and mixins.

### ✅ SCSS Features
67. Mixins: reusable styles  
68. Nesting: organized selectors  
69. Variables: reusable values  

### ✅ Bootstrap SCSS
70. A customizable styling framework based on SCSS.

### ✅ Angular SPA
71. Angular’s default SPA structure can be modified with custom components and templates.

---

## ✅ Additional Notes

### ✅ Moderate
72. The term "Moderate."

---

## Recovery Services Vault: Control Plane for Backup

- Acts as a **secure interface** for backup and disaster recovery.
- Stores **metadata**: retention, policies, access control, encryption settings.
- Does **not expose raw data** like a storage account.
- Delegates actual storage to Azure Backup infrastructure.

### Vault Responsibilities
- Define what to back up
- Set how long to retain
- Control who can access/restore
- Apply encryption and redundancy (LRS/GRS/ZRS)

✅ Think of it as a **policy-driven gatekeeper**  
❌ Not a general-purpose data container

## ✅ Azure Backup, Storage & Monitoring (Points 73 → End)

### **73. SQL Server & SAP HANA Workload-Aware Backups**
- Stream-based specialized backup solutions for SQL Server and SAP HANA in Azure VMs.
- Support full, differential, and log backups.
- Provide 15-minute RPO and point-in-time recovery.

### **74. Recovery Services Vault (RSV) – Secure Control Plane**
- Stores backup configuration metadata (what, how often, retention, security, access).
- Does not expose raw data directly like a storage account.
- Acts as the policy & access controller for Azure Backup and Site Recovery.

### **75. VSS Snapshot Workflow (for Application-Consistent Backups)**
- Backup requestor (Azure Backup/agent) asks VSS for snapshot.
- VSS coordinates with app writers (SQL, AD, IIS, etc.) → flush in-memory data.
- Snapshot (shadow copy) created.
- Writers resume operations.
- Snapshot moved to vault with retention + encryption policies.
- ✅ Ensures clean, application-consistent backups.

### **76. Snapshot Tier (Instant Restore)**
- Snapshots stored locally up to 5 days.
- Best for fast operational recovery.
- Supports instant restore directly from snapshots.

### **77. Vault Tier**
- Snapshots copied to the vault for long-term retention and security.
- Recovery point type changes to “snapshot + vault”.

### **78. Restore Options**
- Restore from Snapshot Tier → faster, best for operational recovery.
- Restore from Vault Tier → for older recovery points, longer retention.

### **79. Cross-Subscription Restore (CSR)**
- Restore VMs/disks to a different subscription within same tenant.
- Requires CSR property enabled in RSV.
- Works with Cross Region Restore (CRR) and Cross Zonal Restore (CZR).
- Only supported for managed VMs with MSI (Managed System Identity).
- ❌ Not supported for snapshots, unmanaged VMs, or ADE-encrypted VMs.

### **80. Azure Ultra Disks**
- Deliver high throughput, high IOPS, and consistent low latency.
- Support dynamic performance scaling without VM restart.
- Ideal for mission-critical workloads like databases.

### **81. Zone-Redundant Storage (ZRS)**
- Data replicated synchronously across 3 availability zones in the same region.
- Protects against zone-level failures.
- Keeps data accessible even if one AZ is unavailable.

### **82. Disk Bursting**
- Allows VMs/disks to temporarily exceed baseline performance.
- Useful for traffic spikes, batch jobs, or fast boot scenarios.

### **83. VM Disk Resize (Data Safety)**
- You can increase VM disk size while VM is running.
- Must ensure data consistency → resizing doesn’t delete data, but the OS must detect new capacity.
- OS won’t use the new space until you extend the partition inside VM.

### **84. Custom Data Collection Rules (DCRs)**
- Define what monitoring data to collect and where to send it.
- Collect metrics, performance counters, event logs.
- Send data to Azure Monitor Logs or Azure Monitor Metrics.

### **85. Activity Logs (Default in Azure Monitor)**
- Automatically record VM lifecycle events (startup, modifications).
- Can be sent to:
  - Azure Monitor Logs → querying, alerting (retention up to 2 years).
  - Azure Storage → cheap long-term archiving.
  - Azure Event Hubs → stream logs outside Azure.

### **86. VM Client/Guest Monitoring**
- Monitors inside the VM: OS, workloads, apps.
- Requires Azure Monitor Agent (AMA) + configured DCRs.

### **87. DCR Storage Logic**
- Azure Monitor Metrics → can store only metrics.
- Azure Monitor Logs → can store metrics + event logs.
- More flexible for querying and alerting.

### **88. Client Event Log Data Collection**
- VM Insights creates a default DCR for performance counters.
- For event logs, you must create a custom DCR.
- Data stored in Log Analytics Workspace, accessible with Kusto Query Language (KQL).

### **89. Guest/Client Monitoring Purpose**
- Goes beyond VM host monitoring.
- Ensures software, processes, and workloads running inside VM are healthy.

### **90. VM Guest/Client Monitoring (Continued)**
- Besides monitoring your VM host's health, utilization, and performance, you need to monitor the software and processes running on your VM. These are called the VM guest or client.

This structured markdown document aligns with how you’ve been storing points — grouping them logically and assigning sub-points where needed. Let me know if this is ready to be saved as a file for you!
