# Nikto Web Vulnerability Scanner Implementation

This project demonstrates the use of the Nikto web vulnerability scanner in Kali Linux to identify security weaknesses in web servers. The process includes network scanning, extracting active hosts, and running Nikto on the discovered targets.

## Prerequisites
- Kali Linux installed
- Basic understanding of Linux commands
- Network access to the target systems
- Nikto and other utilities pre-installed (ifconfig, ipcalc, nmap, awk, cat)

## Commands Used
### Step 1: Identify Network Configuration
```sh
ifconfig
```
This command displays the network configuration, including the IP address and subnet.

### Step 2: Calculate Network Range
```sh
ipcalc 10.0.2.15
```
This command calculates the network details for the given IP address.

### Step 3: Scan the Network for Active Hosts on Port 80
```sh
nmap -p 80 10.0.2.0/24 -oG nullbyte.txt
```
This command scans the subnet `10.0.2.0/24` for hosts with port 80 open and saves the output in `nullbyte.txt`.

### Step 4: Extract Active Hosts
```sh
cat nullbyte.txt | awk '/Up$/{print $2}' | cat >> targetIP.txt
```
This extracts IP addresses of active hosts and appends them to `targetIP.txt`.

### Step 5: Verify Extracted IPs
```sh
cat targetIP.txt
```
Displays the list of extracted target IPs.

### Step 6: Run Nikto on Extracted Targets
```sh
nikto -h targetIP.txt
```
Runs Nikto on all the identified active hosts.

### Step 7: Run Nikto on a Specific Website and Save Output
```sh
nikto -h www.espn.com -output output.txt
```
Scans `www.espn.com` and saves the results in `output.txt`.

## Notes
- Ensure you have legal permission before scanning any network or website.
- Nikto helps identify vulnerabilities but does not exploit them.
- Modify the subnet and target as per your requirement.

## Disclaimer
This tool should only be used for ethical security testing on systems you own or have permission to scan. Unauthorized scanning may lead to legal consequences.

