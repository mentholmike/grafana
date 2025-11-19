# Hyper-V Metrics Dashboard for Grafana

A comprehensive Grafana dashboard for monitoring Hyper-V hosts and related infrastructure. This dashboard provides real-time insights into service status, CPU, memory, disk space, and network bandwidth using Prometheus as the data source.

![Dashboard Preview](https://via.placeholder.com/1200x600?text=Hyper-V+Metrics+Dashboard)  
*(Add a screenshot of your imported dashboard here for better visualization.)*

## Features

- **Service Monitoring**: Check if critical services are running.
- **Resource Utilization**: Track CPU logical processors, available memory, disk free space.
- **Network Bandwidth**: Visualize bandwidth usage for primary Hyper-V NICs and network adapters.
- **Multi-Host Support**: Panels for Hyper-V host and VMs on your machine
- **Library Panels**: Reusable panels for your VMS
- **Visualizations**: Uses Stat, Gauge, Bar Gauge, and Time Series panels with thresholds for alerts (e.g., CPU >70% orange, >85% red; memory/disk in bytes).
- **Auto-Refresh**: Set to auto-refresh for live monitoring.
- **Annotations & Alerts**: Built-in support for Grafana annotations.

The dashboard is tagged with `HyperV` and includes a dashboard link for easy navigation.

## Prerequisites

- **Grafana**: Version 12.3.0 or later (tested with plugin version `12.3.0-18723771502`).
- **Prometheus**: As the data source, configured with Windows exporters (e.g., `windows_exporter` for metrics like `windows_service_state`, `windows_cpu_logical_processor`, `windows_memory_available_bytes`, `windows_logical_disk_free_bytes`, `windows_net_current_bandwidth_bytes`).
- **Windows Exporter**: Install on Windows hosts to expose metrics (e.g., via [Prometheus Windows Exporter](https://github.com/prometheus-community/windows_exporter)).
- **Datasources**: Ensure Prometheus UIDs match your setup:

## Installation

1. **Import the Dashboard**:
   - In Grafana, go to **Dashboards > New > Import**.
   - Copy the JSON from `dashboard.json` (or paste the provided JSON directly).
   - Set the folder (optional) and import.

2. **Configure Datasources**:
   - Verify or create Prometheus datasources matching the UIDs in the JSON.
   - Update queries if host IPs or jobs change (e.g., regex filters like `/^\\{__name__=\"windows_service_state\".../`).

3. **Library Panels**:
   - The dashboard references library panels:
   - Import these separately if not already in your Grafana instance.

4. **Time Range**:
   - Defaults to last 5 minutes; adjust via the time picker.

5. **Alerts**:
   - Configure Grafana alerts based on thresholds (e.g., Hyper-V service state != running triggers red).

## Usage

- **Layout**:
  - Top: Hyper-V service status (Stat panel).
  - Row 1: CPU processors (Gauge) | Unallocated Memory (Gauge).
  - Row 2: VM Free Space (Bar Gauge) | Primary Network Bandwidth (Time Series).
  - Row 3: VM RAM & Disk (Stat).
  - Row 4: VM (Time Series) | APC Gateway Service (Stat).
  - Row 5: VM RAM & Disk (Stat).
  - Row 6: VM (Time Series).
  - Bottom: Library panels for CC-ActiveDirectory.

- **Customization**:
  - Edit panels to adjust thresholds (e.g., add more steps for disk space).
  - Units: Bytes for memory/disk/bandwidth; bool for services; percentage for CPU.
  - Variables: No templating variables defined; add via Grafana if needed for multi-instance support.

- **Example Queries**:
  - Service State: `windows_service_state{state="running"}`
  - Memory: `windows_memory_available_bytes{job="hyperv_metrics"}`
  - Bandwidth: `windows_net_current_bandwidth_bytes{nic="..."}`

## Screenshots

Add screenshots of key panels here:
- [Hyper-V Status and Resources](path/to/screenshot1.png)
- [Network Bandwidth Time Series](path/to/screenshot2.png)
- [APC-Gateway and CC Panels](path/to/screenshot3.png)

## Contributing

Feel free to fork this repo, update the JSON for new metrics, or add features like variables for dynamic host selection. Pull requests welcome!

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.  
*(If you haven't added one, create a `LICENSE` file in your repo.)*

## Support

- Grafana Documentation: [Importing Dashboards](https://grafana.com/docs/grafana/latest/dashboards/build-dashboards/import-dashboard/)
- Windows Exporter: [GitHub Repo](https://github.com/prometheus-community/windows_exporter)
- Issues: Open a GitHub issue for bugs or enhancements.

