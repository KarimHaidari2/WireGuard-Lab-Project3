# WireGuard Lab – DigitalOcean VPN Setup  
**Project 3 – Secure Networking / WireGuard VPN Deployment**

This project demonstrates the complete setup, configuration, and testing of a secure WireGuard VPN server running on a DigitalOcean Ubuntu Droplet using Docker and Docker Compose.

The goal of this lab was to:
- Deploy a cloud-based WireGuard VPN server  
- Configure Docker + Docker Compose  
- Generate secure peer configuration files  
- Test mobile connectivity (iPhone)  
- Verify encryption and private networking  
- Document the entire process with screenshots

---

## 🔧 Technologies Used
- **DigitalOcean Droplet (Ubuntu 24.04 LTS)**
- **WireGuard VPN**
- **Docker Engine**
- **Docker Compose v2**
- **SSH / Terminal**
- **SCP for file transfers**
- **iOS WireGuard App**

---

## 📦 Project Files
- `WireGuard_Lab_Project3_Report.docx` – Full detailed lab report  
- Configuration folders (peer1, peer2, templates)  
- QR code and terminal screenshots  

---

## 🛠️ Steps Performed (Summary)
 1. Created DigitalOcean Droplet
- Region: *NYC3*
- Size: *1vCPU, 1GB RAM, 25GB SSD*
- OS: *Ubuntu 24.04 LTS*
- Collected public IP: **161.35.132.166**

---

 **2. Connected via SSH**

```bash
ssh root@161.35.132.166
Successfully logged in and updated system packages.

3. Installed Docker + Docker Compose
Verified versions:

pgsql
Copy code
docker --version
docker compose version
4. Created Project Directory
bash
Copy code
mkdir wg
cd wg
5. Built docker-compose.yml
Used LinuxServer WireGuard image:

yaml
Copy code
services:
  wireguard:
    image: linuxserver/wireguard
    container_name: wireguard
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    environment:
      - PUID=0
      - PGID=0
      - TZ=America/Chicago
      - SERVERURL=161.35.132.166
      - SERVERPORT=51820
      - PEERS=2
      - PEERDNS=auto
    volumes:
      - ./config:/config
      - /lib/modules:/lib/modules
    ports:
      - 51820:51820/udp
    sysctls:
      - net.ipv4.conf.all.src_valid_mark=1
    restart: unless-stopped
6. Launched WireGuard Server
nginx
Copy code
docker compose up -d
WireGuard container successfully started.

7. Generated Peer Configurations
bash
Copy code
cd /wg/config/peer1/
cat peer1.conf
Exported QR code:

bash
Copy code
docker exec -it wireguard /app/show-peer 1
Scanned QR code on iPhone → connection successful.

8. Transferred config file to Mac
ruby
Copy code
scp root@161.35.132.166:/wg/config/peer1/peer1.conf ~/Downloads/
9. Tested the VPN on iPhone
Scanned QR code

Connected successfully

Verified encrypted tunnel

🧪 Final Result
✔️ WireGuard Server successfully deployed
✔️ Peer devices configured
✔️ iPhone mobile VPN tested
✔️ Full project documented
✔️ Screenshots included

📎 Author
Karim Haidari
Cybersecurity Student | University of Tulsa

https://github.com/KarimHaidari2/WireGuard-Lab-Project/edit/main/README.md 
