# 🚀 Advanced Azure Monitoring Lab

## 🎯 Scenario
**Contoso Corporation** needs centralized monitoring for their Azure Virtual Machines to detect performance issues, generate alerts, and improve operational visibility using Azure Monitor.

---

# 🏗️ Architecture

![Architecture](./diagrams/architecture.png)

---

# 📋 Lab Objectives

By completing this lab, you will learn how to:

- Deploy a virtual machine
- Configure Log Analytics Workspace
- Enable VM Insights
- Monitor CPU and performance metrics
- Create metric alerts
- Create activity log alerts
- Query logs using KQL
- Build monitoring dashboards

---

# 🔹 STEP 1 — Create Resource Group

- **Name:** `rg-monitoring-lab`
- **Region:** `UAE North`

---

# 🔹 STEP 2 — Create Virtual Machine

## Configuration

| Setting | Value |
|---|---|
| VM Name | `vm-monitor` |
| Image | Windows Server 2022 Datacenter |
| Size | Standard B2s |
| Region | UAE North |

---

# 🔹 STEP 3 — Create Log Analytics Workspace

| Setting | Value |
|---|---|
| Workspace Name | `law-contoso-monitor` |
| Region | UAE North |

---

# 🔹 STEP 4 — Enable VM Insights

1. Go to the virtual machine (`vm-monitor`)
2. Open **Insights**
3. Click **Enable**
4. Select the **Log Analytics Workspace**
   - `law-contoso-monitor`

---

# 🔹 STEP 5 — Generate CPU Load (Testing)

On the VM, open **PowerShell** and run:

```powershell
while ($true) { }
```

⚠️ This simulates high CPU usage for monitoring tests.

---

# 🔹 STEP 6 — Explore Metrics

1. Go to **Azure Monitor**
2. Select **Metrics**
3. Set scope to:
   - `vm-monitor`

## Add Metrics

- Percentage CPU
- Memory Percentage
- Disk I/O / Requests

---

# 🔹 STEP 7 — Create Metric Alert

1. Go to **Azure Monitor → Alerts**
2. Click **+ Create → Alert rule**

## Configuration

| Setting | Value |
|---|---|
| Scope | `vm-monitor` |
| Condition | CPU Percentage > 70% |

3. Create **Action Group**
   - Add email notification

4. Save alert rule

---

# 🔹 STEP 8 — Create Activity Log Alert

1. Go to **Azure Monitor → Alerts**
2. Select **Activity Log Alert**

## Configuration

| Setting | Value |
|---|---|
| Event | Virtual Machine Delete |
| Scope | Subscription / Resource Group |

3. Attach Action Group (Email notification)

---

# 🔹 STEP 9 — Query Logs (KQL)

1. Open **Log Analytics Workspace**
2. Go to **Logs**

## KQL Queries

### Heartbeat Logs
```kql
Heartbeat
| summarize count() by Computer
```

---

### CPU Performance
```kql
Perf
| where CounterName == "% Processor Time"
| summarize avg(CounterValue) by bin(TimeGenerated, 5m)
```

---

# 🔹 STEP 10 — Create Dashboard

1. Search for **Dashboard**
2. Click **+ New Dashboard**
3. Name it:
   - `Contoso Monitoring Dashboard`

## Pin Items

- CPU Metrics Chart
- VM Insights Overview
- Alerts Status
- Log Analytics Queries

4. Click **Save**

---

# 🎉 Lab Completed Successfully!

## ✅ Skills Learned

- Azure Monitor setup
- Log Analytics configuration
- VM Insights monitoring
- Metric alerts creation
- Activity log alerts
- KQL log querying
- Dashboard creation

---

# 📌 Real-World Use Cases

This monitoring setup is used in:

- Enterprise IT operations
- Cloud infrastructure monitoring
- Security operations (SOC)
- Performance optimization
- Incident detection and response

---

# 🔐 Best Practices

- Enable diagnostics on all production VMs
- Use multiple alert conditions
- Avoid infinite CPU test commands in production
- Set proper retention for logs
- Use action groups for automation

---
```
