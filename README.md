# PCAP-Geolocation

## Using Wireshark and MaxMind to Analyze PCAP Files with Geolocation

This guide walks you through how to use Wireshark to analyze packet capture (PCAP) files, map IP addresses to geographic locations using the MaxMind GeoIP database, and visualize the data to spot potential security threats like distributed denial-of-service (DDoS) attacks.

---

## 1. Set Up MaxMind for Geolocation

### Create a MaxMind Account

1. Go to [maxmind.com](https://www.maxmind.com/) and sign up for a free account.  
2. No credit card required—just basic info.

### Download GeoIP Databases

After logging in:

- Navigate to **Download Databases**
- Download the following in ZIP format:
  - **GeoLite2 ASN**
  - **GeoLite2 City**
  - **GeoLite2 Country**
- Extract all files to a folder you'll use in Wireshark.

---

## 2. Configure Wireshark

### Point Wireshark to the GeoIP Database

1. Open Wireshark.  
2. Go to `Edit > Preferences` (on macOS, it's under `Wireshark > Preferences`).  
3. Navigate to `Name Resolution`.  
4. Under `MaxMind database directories`, click **Edit** and select the folder with the extracted files.  
5. Restart Wireshark to apply changes.

---

## 3. Analyze Your Packet Capture

### Load the PCAP File

Open your `.pcap` file in Wireshark.

### Identify Suspicious Patterns

- Look for repeated SYN packets from many IPs (possible scans or attacks).  
- Expand the `IPv4` section in the packet details to view country, latitude, and longitude.

### Visualize IP Data

- Go to `Statistics > Endpoints`, select `IPv4`, and browse the IP list with geo info.  
- Click `Map > Open in Browser` to generate a heat map of the IP sources.

---

## 4. Deep Dive: ASN and TTL Analysis

### Check ASN Info

Use the ASN (Autonomous System Number) field in Wireshark to identify the origin of IP traffic.

- This is especially useful for spotting traffic coming from cloud hosting services or known malicious networks.  
- ASN lookups can help determine if the traffic is part of a known organization or a potential threat.

### Inspect TTL Values

Examine **Time To Live (TTL)** values to estimate how far the source IP may be.

- Different operating systems and networks use different starting TTL values.  
- Comparing TTL values can help detect spoofed packets or multiple sources pretending to be one.

---

## 5. Identify Signs of a DDoS Attack

### Look for Red Flags

Watch for these common indicators of a DDoS or scripted attack:

- Repeated or identical **IP ID** values across various source IPs  
- Sequential or patterned **TCP Sequence Numbers**  
- Source IPs that appear randomized or spoofed

These patterns often suggest automated tools or botnets.

### Take Action

Once you've identified potential threats, consider these response steps:

- **Block or blacklist** suspicious IPs or CIDR blocks using your firewall or IDS/IPS  
- **Log and monitor** ongoing activity for escalation or persistence  
- **Report** bad actors to relevant hosting providers, threat intel platforms, or security communities

---

## Conclusion

With Wireshark and the MaxMind GeoIP databases, you can gain deeper insight into where your network traffic is coming from and what it might mean.

By combining traditional packet inspection with geolocation and ASN analysis, you're better equipped to:

- Investigate abnormal patterns  
- Trace malicious behavior  
- Take timely action to protect your systems
