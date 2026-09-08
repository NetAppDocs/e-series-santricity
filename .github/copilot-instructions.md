## Copilot instructions for SANtricity software documentation

### Repository overview
Product: SANtricity software

SANtricity software provides web-based management for NetApp *E-Series* and *EF-Series* storage arrays through two interfaces: *System Manager* for a single array and *Unified Manager* for multiple arrays. Repository content focuses on provisioning storage, data protection, hardware operations, access/security settings, support workflows, and multi-array administration.

### Repository structure
- `san-getstarted/` – Getting-started flows for accessing interfaces and setting up System Manager or Unified Manager.
- `sm-interface/` – System Manager interface behavior, dashboard/navigation, notifications, and day-to-day UI tasks.
- `sm-storage/` – Storage provisioning and operations (hosts, pools, volume groups, volumes, snapshots, remote storage, performance).
- `sm-hardware/` – Hardware component status and operations for controllers, drives, shelves, and related hardware views.
- `sm-settings/` – System Manager configuration for alerts, access management, certificates, system settings, and add-on features.
- `sm-mirroring/` – Asynchronous and synchronous mirroring concepts, requirements, and management tasks.
- `sm-support/` – Support and diagnostics tasks, event logs, AutoSupport, upgrades, and recovery data collection.
- `system-manager/` – Landing-page navigation content for single-array management documentation.
- `um-admin/` – Unified Manager interface administration and core UI operations for managing multiple arrays.
- `um-manage/` – Unified Manager workflows for discovery, grouping arrays, batch operations, and importing settings.
- `um-certificates/` – Unified Manager certificate and authentication configuration, including directory-service access controls.
- `unified-manager/` – Landing-page navigation content for multi-array management documentation.
- `_include/` – Shared include snippets reused across AsciiDoc topics.
- `redirect/` – Redirect target pages (mostly FAQ-style topics) used to preserve legacy links.
- `media/` – Shared images and UI graphics referenced by AsciiDoc pages.

### Product-specific context
**Architecture and components:**
- *System Manager* is embedded on each storage-array controller and is accessed directly by browser to manage one array.
- *Unified Manager* runs on a management server with *Web Services Proxy* and provides centralized management for multiple arrays.
- Unified Manager can discover arrays, run batch operations (for example import settings), and launch System Manager for array-specific operations.
- Initial configuration for both *asynchronous mirroring* and *synchronous mirroring* is done in Unified Manager, while ongoing mirrored-resource management is done in System Manager.

**Key concepts:**
- A *pool* is a logical group of drives, while a *volume group* is a container for volumes with shared characteristics; both provide capacity for host-accessible volumes.
- A *workload* is a storage object tied to an application context and is used during volume creation and performance grouping.
- *Asynchronous mirroring* replicates changed data between arrays over time as bandwidth permits; it is managed at group level with mirrored volumes.
- *Synchronous mirroring* replicates writes in real time between arrays for high availability and disaster-recovery continuity.
- *Remote Storage* maps a remote source volume to a local E-Series target volume for import-based migration, using iSCSI connectivity.
- Feature availability is platform-dependent across storage-system types; do not assume every array supports every data-protection or volume feature.

**Naming conventions and terminology:**
- Use *storage array* (not generic “server”) for managed systems, and distinguish *local storage array* versus *remote storage array* in replication/migration contexts.
- Use exact UI product names: *SANtricity System Manager* and *SANtricity Unified Manager*.
- Mirroring terms are specific: *mirrored pair*, *mirror consistency group*, *primary volume*, and *secondary volume*.
- Remote-storage setup uses *IQN* (*iSCSI Qualified Name*) and *LUN* identifiers when defining source/target mappings.
- UI path notation appears as `menu:Section[Subsection]` in source topics and should map to actual SANtricity navigation labels.

### Typical user workflows
**Initial single-array setup:** Access controller IP in browser → Open SANtricity System Manager → Run setup/configuration tasks (passwords, alerts, support options) → Create pools/volume groups and volumes for hosts

**Multi-array onboarding:** Install SANtricity Unified Manager with Web Services Proxy → Discover storage arrays on the network → Organize arrays and import shared settings in batch → Launch System Manager for per-array operations

**Mirroring setup and operations:** Use Unified Manager to establish inter-array mirroring configuration → Create mirrored pairs or consistency groups → Manage mirrored resources in System Manager → Monitor mirror status and synchronization

**Remote storage migration:** Prepare iSCSI connectivity and local destination volume → Register local E-Series system as a host on the remote system using IQN → Create remote storage object in System Manager to map source-to-target volumes → Start and monitor import, then keep or break the mapping
