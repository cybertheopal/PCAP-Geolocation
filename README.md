# PCAP-Geolocation

# 🌐 Using Wireshark and MaxMind to Analyze PCAP Files with Geolocation

This guide walks you through how to use Wireshark to analyze packet capture (PCAP) files, map IP addresses to geographic locations using the MaxMind GeoIP database, and visualize the data to spot potential security threats like distributed denial-of-service (DDoS) attacks.

---

## 1. 🗂️ Set Up MaxMind for Geolocation

### 🔐 Create a MaxMind Account  
1. Go to [maxmind.com](https://www.maxmind.com/) and sign up for a free account.  
2. No credit card required—just basic info.

### 📦 Download GeoIP Databases  
After logging in:
- Navigate to **Download Databases**
- Download the following in ZIP format:
  - **GeoLite2 ASN**
  - **GeoLite2 City**
  - **GeoLite2 Country**
- Extract all files to a folder you'll use in Wireshark.

---

## 2. ⚙️ Configure Wireshark

### 📁 Point Wireshark to the GeoIP Database  
1. Open Wireshark.  
2. Go to `Edit > Preferences` (on macOS, it's under `Wireshark > Preferences`).  
3. Navigate to `Name Resolution`.  
4. Under `MaxMind database directories`, click **Edit** and select the folder with the extracted files.  
5. Restart Wireshark to apply changes.

---

## 3. 🕵️ Analyze Your Packet Capture

### 📂 Load the PCAP File  
Open your `.pcap` file in Wireshark.

### 🧠 Identify Suspicious Patterns  
- Look for repeated SYN packets from many IPs (possible scans or attacks).  
- Expand the `IPv4` section in the packet details to view country, latitude, and longitude.

### 🗺️ Visualize IP Data  
- Go to `Statistics > Endpoints`, select `IPv4`, and browse the IP list with geo info.  
- Click `Map > Open in Browser` to generate a heat map of the IP sources.

---

## 4. 🔍 Filter and Investigate Further

### 🌍 Filter by Country  
To isolate traffic from a specific country (e.g., China), use:
```wireshark
ip.geoip.country == "CN"
