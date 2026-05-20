# 🚀 Advanced Azure Monitoring Lab

## 🎯 Scenario
**Contoso Corporation** needs centralized monitoring for their Azure Virtual Machines to detect performance issues, generate alerts, and improve operational visibility using Azure Monitor.

---

# 🏗️ Architecture

![Architecture](./diagrams/architecture.png)

---

# 📋 Lab Objectives

- Deploy and monitor a Virtual Machine
- Enable VM Insights
- View metrics directly from VM
- Create metric alerts from VM
- Create activity log alerts from Azure Monitor
- Query logs using KQL
- Build dashboards

---

# 🔹 STEP 1 — Create Resource Group

- **Name:** `rg-monitoring-lab`
- **Region:** `UAE North`

---

# 🔹 STEP 2 — Create Virtual Machine

| Setting | Value |
|---|---|
| Name | `vm-monitor` |
| Image | Windows Server 2022 Datacenter |
| Size | Standard B2s |
| Region | UAE North |

---

# 🔹 STEP 3 — Create Log Analytics Workspace

| Setting | Value |
|---|---|
| Name | `law-contoso-monitor` |
| Region | UAE North |

---

# 🔹 STEP 4 — Enable VM Insights

1. Open the VM: `vm-monitor`
2. Go to **Insights**
3. Click **Enable**
4. Select workspace:
   - `law-contoso-monitor`

---

# 🔹 STEP 5 — Generate CPU Load (Testing)

On the VM, open **PowerShell**:

```powershell
while ($true) { }
```

⚠️ This creates high CPU load for monitoring tests.

---

# 🔹 STEP 6 — Monitor Metrics (FROM VM)

1. Go to the VM: `vm-monitor`
2. In the left menu, select:
   - **Monitoring → Metrics**
3. Click **Add metric**

## Add Metrics:

- Percentage CPU
- Memory Percentage
- Disk Read/Write

4. Set time range (Last 1 hour)

📊 You can now visually monitor VM performance directly from the VM blade.

---

# 🔹 STEP 7 — Create Metric Alert (FROM VM)

1. Stay inside the VM: `vm-monitor`
2. Go to:
   - **Monitoring → Alerts**
3. Click **+ Create alert rule**

## Configuration

| Setting | Value |
|---|---|
| Scope | This VM (`vm-monitor`) |
| Condition | CPU Percentage > 70% |

4. Create **Action Group**
   - Add email notification

5. Click **Create alert rule**

📌 This alert is now created directly from the VM resource.

---

# 🔹 STEP 8 — Create Activity Log Alert (FROM AZURE MONITOR)

1. Go to **Azure Monitor**
2. Open **Alerts**
3. Click **+ Create → Alert rule**

## Configuration

| Setting | Value |
|---|---|
| Signal type | Activity Log |
| Event | Virtual Machine Delete |
| Scope | Subscription or Resource Group |

4. Create or select **Action Group**
   - Email notification

5. Click **Create alert rule**

📌 This ensures monitoring at the Azure platform level (not VM-level).

---

# 🔹 STEP 9 — Query Logs (KQL)

1. Open **Log Analytics Workspace**
2. Go to **Logs**

## KQL Queries

### Heartbeat

```kql id="k8q1aa"
Heartbeat
| summarize count() by Computer
```

---

### CPU Performance

```kql id="m4x2bb"
Perf
| where CounterName == "% Processor Time"
| summarize avg(CounterValue) by bin(TimeGenerated, 5m)
```

---

# 🔹 STEP 10 — Create Dashboard

1. Search **Dashboard**
2. Click **+ New dashboard**
3. Name it:
   - `Contoso Monitoring Dashboard`

## Pin Items

- VM CPU Metrics
- VM Insights
- Alerts status
- Log Analytics queries

4. Click **Save**

---

# 🎉 Lab Completed Successfully!

## ✅ Skills Practiced

- VM-level monitoring (Metrics + Alerts)
- Azure Monitor platform alerts
- Log Analytics (KQL queries)
- VM Insights integration
- Dashboard creation

---

# 🔐 Best Practices

- Always create alerts from VM for resource-level monitoring
- Use Azure Monitor for subscription-wide events
- Avoid infinite loops in production CPU tests
- Enable VM Insights for deep diagnostics
- Centralize logs in Log Analytics Workspace

---
```
