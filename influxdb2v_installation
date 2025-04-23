# Installing InfluxDB on Rocky Linux

This guide provides step-by-step instructions to install InfluxDB 2.x, an open-source time-series database, on Rocky Linux (tested on Rocky Linux 8 and 9).

## Table of Contents
- [Prerequisites](#prerequisites)
- [Installation Steps](#installation-steps)
  - [Step 1: Update the System](#step-1-update-the-system)
  - [Step 2: Add the InfluxData Repository](#step-2-add-the-influxdata-repository)
  - [Step 3: Install InfluxDB](#step-3-install-influxdb)
  - [Step 4: Start and Enable the InfluxDB Service](#step-4-start-and-enable-the-influxdb-service)
  - [Step 5: Configure InfluxDB](#step-5-configure-influxdb)
  - [Step 6: Configure Firewall (Optional)](#step-6-configure-firewall-optional)
  - [Step 7: Verify Installation](#step-7-verify-installation)
  - [Step 8: Secure InfluxDB (Optional)](#step-8-secure-influxdb-optional)
  - [Step 9: Basic Usage (Optional)](#step-9-basic-usage-optional)
- [Troubleshooting](#troubleshooting)
- [Additional Notes](#additional-notes)
- [References](#references)

## Prerequisites
- Rocky Linux system (e.g., Rocky Linux 8 or 9)
- Root or sudo privileges
- Internet access for downloading packages
- Basic familiarity with terminal commands

## Installation Steps

### Step 1: Update the System
Ensure your system is up to date to avoid package conflicts.

```bash
sudo dnf update -y
```

### Step 2: Add the InfluxData Repository

InfluxDB is not available in the default Rocky Linux repositories. Add the InfluxData repository.

Create a repository file for InfluxData:
```bash
sudo tee /etc/yum.repos.d/influxdata.repo > /dev/null <<EOF
[influxdata]
name = InfluxData Repository
baseurl = https://repos.influxdata.com/centos/\$releasever/\$basearch/stable
enabled = 1
gpgcheck = 1
gpgkey = https://repos.influxdata.com/influxdata-archive_compat.key
EOF
```

Import the InfluxData GPG key:
```bash
sudo rpm --import https://repos.influxdata.com/influxdata-archive_compat.key
```

### Step 3: Install InfluxDB

Install the InfluxDB package:
```bash
sudo dnf install influxdb2 -y
```

### Step 4: Start and Enable the InfluxDB Service

Start the InfluxDB service and enable it to run on boot.

Start the service:
```bash
sudo systemctl start influxdb
```

Enable the service on boot:
```bash
sudo systemctl enable influxdb
```

Verify the service is running:
```bash
sudo systemctl status influxdb
```
Ensure the output shows "active (running)".

### Step 5: Configure InfluxDB

InfluxDB 2.x requires initial setup via the web interface or CLI.

**Web UI Setup:**
- Open a browser and navigate to `http://<your-server-ip>:8086`
- Follow the prompts to:
  - Create an admin user (username and password)
  - Set up an organization and a bucket

**CLI Setup (alternative):**
```bash
influx setup
```
Follow the prompts to configure the admin user, organization, and bucket.

### Step 6: Configure Firewall (Optional)

If firewalld is enabled, allow access to InfluxDB's default port (8086):
```bash
sudo firewall-cmd --permanent --add-port=8086/tcp
sudo firewall-cmd --reload
```

### Step 7: Verify Installation

Confirm that InfluxDB is installed and running.

Check the InfluxDB version:
```bash
influx version
```

Log in to the InfluxDB CLI:
```bash
influx
```
Use the credentials set during setup.

**Test the Web UI:**
- Access `http://<your-server-ip>:8086` and log in with your admin credentials

### Step 8: Secure InfluxDB (Optional)

Enhance security with the following steps:

- Use strong passwords for admin users
- Enable HTTPS using a reverse proxy (e.g., Nginx) or a certificate (e.g., Let's Encrypt)
- Restrict port 8086 access using a firewall or security groups

### Step 9: Basic Usage (Optional)

Get started with InfluxDB:

Create a bucket:
```bash
influx bucket create --name my-bucket
```

Write data using the CLI, API, or client libraries.

Query data using the Web UI's Data Explorer or Flux queries in the CLI:
```
from(bucket:"my-bucket") |> range(start:-1h)
```

## Troubleshooting

**Service not starting:**
- Check logs: `journalctl -u influxdb`
- Ensure port 8086 is free: `sudo netstat -tulnp | grep 8086`

**Repository issues:**
- Verify the repository URL and GPG key
- Clear DNF cache: `sudo dnf clean all`

**Web UI inaccessible:**
- Confirm port 8086 is open in the firewall
- Verify InfluxDB is running: `sudo systemctl status influxdb`

## Additional Notes

- Replace `<your-server-ip>` with your server's IP address or `localhost` for local access
- For InfluxDB 1.x, use the `influxdb` package instead of `influxdb2`, but InfluxDB 2.x is recommended
- For advanced setups (e.g., clustering), refer to the InfluxDB documentation

## References

- [Official InfluxDB Documentation](https://docs.influxdata.com/)
- [InfluxData Repository](https://repos.influxdata.com/)

Last updated: April 23, 2025
