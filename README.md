# Firewall-Log-Analysis


## Overview
This project demonstrates how to detect suspicious firewall activity using Splunk. It focuses on identifying repeated blocked attempts, port scan behavior, and general traffic visibility from firewall logs.

## Data Source
- **File:** `firewall_logs_sample.csv`
- **Fields:** `time, src_ip, dest_ip, dest_port, action`

## Splunk Setup
1. Upload the log file into Splunk.
2. Assign it to index: `firewall`
3. Use sourcetype: `csv` (or custom: `firewall_logs`)

## Key Searches
- Top blocked IPs:
  ```spl
  index=firewall sourcetype=csv action="blocked"
  | stats count by src_ip , dest_port
  | where count > 10
  | sort - count

