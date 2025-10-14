# 🧩 Kasten K10 – API Resources Reference (OpenShift Cluster)

_Last update: October 2025_  
_All API groups provided by Veeam Kasten K10 and their corresponding CRDs, kinds, and purposes._

---

## ⚙️ actions.kio.kasten.io

| NAME | NAMESPACED | KIND | COMMENT |
|------|-------------|------|----------|
| `backupactions` | ✅ | BackupAction | Launches an on-demand **backup** or snapshot of an application (namespaced). |
| `backupclusteractions` | ❌ | BackupClusterAction | Backs up **cluster-scoped resources** (CRDs, ClusterRoles, etc.). |
| `batchrestoreactions` | ✅ | BatchRestoreAction | Performs **mass restores** of multiple applications in one operation. |
| `cancelactions` | ✅ | CancelAction | Cancels a running backup/export/restore operation gracefully. |
| `exportactions` | ✅ | ExportAction | Triggers **export** of restore points to external repositories (S3, NFS, etc.). |
| `importactions` | ✅ | ImportAction | Imports **restore points** or metadata from an external repository. |
| `migratefcdactions` | ✅ | MigrateFCDAction | Handles migration of **vSphere First-Class Disks (FCD)** to CSI-based volumes (legacy support). |
| `reportactions` | ✅ | ReportAction | Generates **K10 reports** (backup summaries, compliance data). |
| `restoreactions` | ✅ | RestoreAction | Launches a **restore** of an application from a restore point. |
| `restoreclusteractions` | ❌ | RestoreClusterAction | Restores **cluster-scoped resources** (ClusterRoles, CRDs, etc.). |
| `retireactions` | ❌ | RetireAction | Deletes or retires restore points and associated artifacts. |
| `runactions` | ✅ | RunAction | Triggers the execution of a **Policy** (Backup, Export, Restore, Validate). |
| `stageactions` | ✅ | StageAction | Used for **staged restores** — pre-deploy app manifests before full restore. |
| `upgradeactions` | ✅ | UpgradeAction | Performs internal **data/model upgrades** within K10. |
| `validateactions` | ✅ | ValidateAction | Validates **restore point integrity** in repositories (added in K10 8.0.7). |

---

## 📦 apps.kio.kasten.io

| NAME | NAMESPACED | KIND | COMMENT |
|------|-------------|------|----------|
| `applications` | ✅ | Application | Represents an **application object** detected and protected by K10. |
| `clusterrestorepoints` | ❌ | ClusterRestorePoint | Stores restore points for **cluster-scoped resources** (non-namespaced). |
| `restorepointcontents` | ❌ | RestorePointContent | Backend object describing the **snapshot/export data** behind a RestorePoint. |
| `restorepoints` | ✅ | RestorePoint | Logical **restore points** for apps/namespaces; references export data and snapshots. |

---

## 🧰 config.kio.kasten.io

| NAME | NAMESPACED | KIND | COMMENT |
|------|-------------|------|----------|
| `actionpodspecbindings` | ✅ | ActionPodSpecBinding | Associates an `ActionPodSpec` with a workload or namespace. |
| `actionpodspecs` | ✅ | ActionPodSpec | Defines the **Pod template** used by K10 for executing actions (resources, tolerations, etc.). |
| `auditconfigs` | ✅ | AuditConfig | Configures **audit log export** to external storage for compliance. |
| `blueprintbindings` | ✅ | BlueprintBinding | Automatically binds **Kanister blueprints** to workloads using selectors. |
| `policies` | ✅ | Policy | Defines **scheduled backup/export/restore policies** and their parameters. |
| `policypresets` | ✅ | PolicyPreset | Provides reusable templates for Policies (frequency, retention, export profiles). |
| `profiles` | ✅ | Profile | Defines **storage/export/import credentials** (S3, Azure, NFS, Vault, etc.). |
| `storagesecuritycontextbindings` | ✅ | StorageSecurityContextBinding | Binds a StorageSecurityContext to a specific StorageClass or volume. |
| `storagesecuritycontexts` | ✅ | StorageSecurityContext | Defines UID/GID/group context for accessing secured file systems. |
| `transformsets` | ✅ | TransformSet | Declares reusable **manifest transformations** applied during restores. |

---

## 🗄️ repositories.kio.kasten.io

| NAME | NAMESPACED | KIND | COMMENT |
|------|-------------|------|----------|
| `storagerepositories` | ✅ | StorageRepository | Represents a **Kopia repository** managed by K10 (location, health, retention). |

---

## 📊 reporting.kio.kasten.io

| NAME | NAMESPACED | KIND | COMMENT |
|------|-------------|------|----------|
| `reports` | ✅ | Report | Stores generated **K10 reports** (from ReportAction or scheduled jobs). |

---

## 🧠 Operational Notes

- Most resources under `actions.*` are **namespaced**, except `*clusteractions` and `retireactions` (cluster-scoped).  
- `apps.*` resources track **state and metadata** — they’re created or consumed by actions.  
- `config.*` defines governance, storage profiles, security contexts, and blueprints.  
- `repositories.*` handles Kopia repositories and data plane metadata.  
- `reporting.*` enables reporting, audit, and compliance exports.  
- Use `oc api-resources --api-group=<group>` to confirm active versions and availability.  
