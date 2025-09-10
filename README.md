
# Azure Notes – Stored Points

## Azure Storage – Blob, Security, Access
1. **Azure Blob Storage** is a service that stores unstructured data in the cloud as objects or blobs. Blob stands for Binary Large Object. Blob Storage is also referred to as object storage or container storage.
2. **Azure Blob Storage uses a container resource** to group a set of blobs. A blob can't exist by itself in Blob Storage. A blob must be stored in a container resource.
3. **Access tiers**: You can assign hot, cool, or cold tier to a blob to trigger rehydration.
4. **Lifecycle management**: Transition blobs to cooler tiers using policy rules (Hot→Cool, Hot→Archive, Cool→Archive).
5. Expand knowledge in the **Manage the Azure Blob storage lifecycle training module**.
6. **Blob versioning** maintains previous versions, allowing recovery of modified or deleted data.
7. Every file is ultimately a sequence of 0s and 1s.
8. **Azure Storage Explorer**: Upload, download, manage blobs/files/queues/tables, preview data, and configure permissions.
9. Exercise: Provide storage for the public website.
10. Enable version-level immutability.
11. Configure a shared access signature (SAS), including URI and parameters.
12. **Azure Storage Security – Quick Recap**:
   - Encryption at Rest: AES-256, BitLocker/dm-crypt
   - Encryption in Transit: HTTPS, SMB 3.0
   - Encryption Models: service-managed, customer-managed (Key Vault/HSM), client-side
   - Shared Key Authorization: risky, avoid
   - Shared Access Signatures (SAS): scoped, temporary
   - Microsoft Entra ID + Managed Identity: best practice
   - RBAC: role-based fine-grained access
   - Storage Analytics: logging for tracing/diagnosis
13. **Role-Based Access Control (RBAC)** integrates with Entra ID, connection strings, ACLs to secure resources.
14. **Job Skills**: Create/configure storage account, secure blob storage, and file storage.
15. Different ways to secure Azure Storage.
16. How to configure SAS for the Azure storage account.
17. **Locally Redundant Storage (LRS)** replicates data 3 times in the same datacenter.
18. Mount SMB Azure file share on Linux using CIFS, either on-demand or via /etc/fstab.
19. Open port 445 for SMB; use VPN or ExpressRoute if blocked.
20. **Azure Storage Explorer** requires ARM and data permissions via Entra ID.

## Azure File Sync & Storage Analogies
21. **Azure File Sync with cloud tiering** caches files locally and older files in the cloud.
22. **Analogy**: NTFS is like Git’s internal engine tracking files, permissions, and links.
23. **Term Analogies**:
   - MBR → Old filing cabinet
   - GPT → Modern shelf system
   - VHD → Portable disk image
   - SCSI → High-speed disk connector

## Python & Cloud/DevOps
24. Why we use Python in DevOps and Cloud.

## Azure Compute & VM Insights
25. VM pricing varies by size and OS; Linux is cheaper (no license charge), Windows includes OS cost.
26. **Azure Compute Gallery** helps manage and replicate images across regions.
27. **IO-intensive workloads** include SAP HANA, SQL, Oracle, and transaction-heavy systems.
28. Explore and configure resources using **Terraform provider**.
29. **Azure VM I/O Tuning Summary**:
   - blk-mq: parallel access across CPU cores
   - I/O Scheduler: none for blk-mq, noop for older blk
   - LVM Striping: split data across disks for higher performance
30. **LVM Recap**: Manage and resize disk volumes flexibly.
31. Deploy **RHEL in Azure VMs**, controlling OS, apps, and scripts.

## Networking & VM Optimization
32. Support for accelerated networking depends on VM size.
33. Linux VMs fit open-source ecosystems used in cloud-native scenarios.
34. **VM Extensions** are for post-provisioning tasks like installing packages or configuring services.
35. **URN vs UrnAlias**: URN is full image ID, UrnAlias is a shortcut to specify OS images.

## Node.js & Setup
36. Build and run web app with the MEAN stack on the Azure Linux VM.
37. Register Node.js repository using `curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -`; installation takes time.
38. NodeSource provides separate repositories for each Linux distribution.
39. NodeSource distributes Node.js binaries and tools.
40. Node.js provides the runtime environment to run JavaScript outside the browser.

## Azure Availability, Zones & Fault Tolerance
41. **Zonal services** pin resources to specific zones; **Zone-redundant services** replicate automatically.
42. **VM Scale Sets** deploy and manage identical VMs.
43. Need to understand the difference between Layer 7 and Layer 4 Load Balancers.
44. **Spreading algorithm** balances VMs across fault domains; Max spreading is recommended.
45. Availability sets and zones ensure high availability and fault tolerance; need deeper understanding.
46. **Availability Sets analogy**: Servers in different racks ensure uptime during failures.
47. **Availability Zones analogy**: Buildings in different locations ensure work continuity.

## Scaling
48. Ensure maximum and minimum instance counts differ with adequate scale margin for autoscaling.

## Web Apps
49. Create a web app using the Azure portal. [Documentation](https://learn.microsoft.com/en-us/training/modules/configure-azure-app-services/3-create-app-service)
50. **Exercise – Implement Web Apps**: Host PHP apps, use deployment slots, configure autoscaling, and integrate Application Insights.

## Containers
51. **Layered Architecture**: Physical server → Hypervisor → VM → Container runtime → Containers.
52. Port mapping isn't supported as containers share a port namespace.
53. Deleting container groups releases IP addresses and FQDNs.
54. **Azure Files** provide persistent storage mounts across containers.
55. **Why it’s useful**:
   - Persistence survives restarts.
   - Multiple containers share files.
   - Secure access via keys or SAS.
   - Automation using Bash and Azure CLI.
