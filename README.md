# 🧩 Kasten K10 – API Resources Reference (OpenShift Cluster)

_Last update: October 2025_  
_All API groups provided by Veeam Kasten, including subresources such as `/details`._

---

## ⚙️ actions.kio.kasten.io

| NAME | NAMESPACED | KIND | COMMENT |
|------|-------------|------|----------|
| `backupactions` | ✅ | BackupAction | Launches an on-demand **backup** or snapshot of an application (namespaced). |
| `backupactions/details` | ✅ | — | Read-only **status subresource** giving backup progress, phase, and metrics. |
| `backupclusteractions` | ❌ | BackupClusterAction | Backs up **cluster-scoped resources** (CRDs, ClusterRoles, etc.). |
| `batchrestoreactions` | ✅ | BatchRestoreAction | Performs **mass restores** of multiple applications in one operation. |
| `batchrestoreactions/details` | ✅ | — | Read-only subresource providing detailed per-restore results and progress. |
| `cancelactions` | ✅ | CancelAction | Cancels a running backup/export/restore operation gracefully. |
| `exportactions` | ✅ | ExportAction | Triggers **export** of restore points to external repositories (S3, NFS, etc.). |
| `exportactions/details` | ✅ | — | Shows export transfer progress and throughput metrics. |
| `importactions` | ✅ | ImportAction | Imports **restore points** or metadata from an external repository. |
| `importactions/details` | ✅ | — | Displays import progress and validation results. |
| `migratefcdactions` | ✅ | MigrateFCDAction | Handles migration of **vSphere First-Class Disks (FCD)** to CSI volumes. |
| `reportactions` | ✅ | ReportAction | Generates **K10 reports** (backup summaries, compliance data). |
| `restoreactions` | ✅ | RestoreAction | Launches a **restore** of an application from a restore point. |
| `restoreactions/details` | ✅ | — | Read-only **restore status subresource** (phases, errors, completion time). |
| `restoreclusteractions` | ❌ | RestoreClusterAction | Restores **cluster-scoped resources** (ClusterRoles, CRDs, etc.). |
| `retireactions` | ❌ | RetireAction | Deletes or retires restore points and associated artifacts. |
| `runactions` | ✅ | RunAction | Triggers execution of a **Policy** (Backup, Export, Restore, Validate). |
| `runactions/details` | ✅ | — | Provides summary and execution details of the associated policy run. |
| `stageactions` | ✅ | StageAction | Used for **staged restores** — prepares manifests before restore. |
| `upgradeactions` | ✅ | UpgradeAction | Performs internal **data/model upgrades** within K10. |
| `validateactions` | ✅ | ValidateAction | Validates **restore point integrity** in repositories (added in K10 8.0.7). |

---

## 📦 apps.kio.kasten.io

| NAME | NAMESPACED | KIND | COMMENT |
|------|-------------|------|----------|
| `applications` | ✅ | Application | Represents an **application object** detected and protected by K10. |
| `clusterrestorepoints` | ❌ | ClusterRestorePoint | Stores restore points for **cluster-scoped resources**. |
| `restorepointcontents` | ❌ | RestorePointContent | Backend object describing the **snapshot/export data** behind a RestorePoint. |
| `restorepoints` | ✅ | RestorePoint | Logical **restore points** for apps/namespaces referencing exported data. |

---

## 🧰 config.kio.kasten.io

| NAME | NAMESPACED | KIND | COMMENT |
|------|-------------|------|----------|
| `actionpodspecbindings` | ✅ | ActionPodSpecBinding | Associates an `ActionPodSpec` with a workload or namespace. |
| `actionpodspecs` | ✅ | ActionPodSpec | Defines the **pod template** used by K10 to run actions. |
| `auditconfigs` | ✅ | AuditConfig | Configures **audit log export** to external storage. |
| `blueprintbindings` | ✅ | BlueprintBinding | Automatically binds **Kanister blueprints** to workloads. |
| `policies` | ✅ | Policy | Defines **scheduled backup/export/restore policies** and parameters. |
| `policypresets` | ✅ | PolicyPreset | Reusable policy templates (frequency, retention, profiles). |
| `profiles` | ✅ | Profile | Defines **storage/export/import credentials** (S3, Azure, NFS, Vault…). |
| `storagesecuritycontextbindings` | ✅ | StorageSecurityContextBinding | Binds a StorageSecurityContext to a StorageClass or volume. |
| `storagesecuritycontexts` | ✅ | StorageSecurityContext | Defines UID/GID/group context for pods accessing storage. |
| `transformsets` | ✅ | TransformSet | Reusable **manifest transformations** applied during restore. |

---

## 🗄️ repositories.kio.kasten.io

| NAME | NAMESPACED | KIND | COMMENT |
|------|-------------|------|----------|
| `storagerepositories` | ✅ | StorageRepository | Represents a **Kopia repository** managed by K10. |
| `storagerepositories/details` | ✅ | — | Exposes repository internals, size, snapshots count, and metrics. |

---

## 📊 reporting.kio.kasten.io

| NAME | NAMESPACED | KIND | COMMENT |
|------|-------------|------|----------|
| `reports` | ✅ | Report | Stores generated **K10 reports** (from ReportAction or scheduled reports). |

---

## 🧠 Operational Notes

- `/details` subresources are **read-only** and expose live or historical execution metadata.  
- Most `actions.*` are namespaced except `*clusteractions` and `retireactions`.  
- `apps.*` track application state and restore-point lineage.  
- `config.*` defines operational governance, storage profiles, and blueprints.  
- `repositories.*` manage Kopia repositories and metrics.  
- `reporting.*` provides audit and compliance reporting.  
- Use `oc api-resources --api-group=<group>` to validate live API availability.  
