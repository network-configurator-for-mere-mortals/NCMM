# NCMM: Network Configurator for Mere Mortals

**NCMM** is a vendor-agnostic, graphical web interface that lets anyone — not just network engineers — design, validate, and deploy professional-grade networks with confidence.

> Drag. Drop. Define. Deploy. And undo when necessary.

---

## 🚀 What It Does

- Visually design network topologies using **drag-and-drop**
- Define **VLANs**, **WANs**, **SSIDs**, **routing/firewall rules** with click/drag simplicity
- Set up **allowed**, **denied**, **one-way traffic**, **port-limited**, or any other routing/paths
- Automatically back up existing configurations **before** every deployment
- Restore from **failsafe configurations** when needed
- Automatically **deploy configurations** to configured management devices
- Maintain Git-backed history and **AI-generated, user editable documentation**
- Extensive AI assistance/integration [Planned/Future]

---

## 🎯 Target Audience

- 👨‍🔧 Homelab enthusiasts
- 🛠️ IT consultants
- 🏠 Small office/home office users
- 🚚 Small businesses
- 🏢 Corporate IT departments (Future 🚧 Monetization potential)
- 🍼 Beginners curious about real-world networking

If you've ever said, “I just want to block my IoT devices from talking to my main LAN,” — this tool is for you.

---

## 🔑 Key Features (Planned)

### 🖼️ Design Workspace
- Drag and arrange VLANs, routers, firewalls, switches, WAPs, SSIDs, and more - then create connections and rules with click/drag simplicity

### 🧭 Devices/Elements Sidebar
- Organized, expandable sidebar where all devices and segments are grouped:
  - 📁 **Management Devices**
    - 📡 Router(s)
    - 🔥 Firewall(s)
    - 🎛️ Switch(es)
    - 📶 Access Point(s)
    - 🧠 Controller(s) (e.g., Omada Controller)
  - 🌐 **Network Segments**
    - 🌍 WAN
    - 🔀 LAN
    - 🧩 VLANs
    - 📶 SSIDs (Home_WiFi, Guest_WiFi, IoT)
  - 📦 **Nodes**
    - 🗄️ Server
    - 💽 NAS
    - 📱 IoT/Smart Device
    - 📡 WAP (Wireless AP)
    - 📶 SSID (linked to WAP)
    - 🖥️ PC/Laptop
    - 🖨️ Printer
    - 📷 Surveillance Camera

### 🔀 Traffic Type Toolbar
- Instantly create:
  - 🚫 Blocked traffic (default)
  - 🔁 Unrestricted traffic
  - ➡️ One-way or port-limited rules
  - ⏳ Future: QoS/scheduled access control

### 🤖 AI Integration
- Context-aware suggestions (_“Would you like to block IoT devices from LAN?”_)
- Autocomplete rules based on natural language (_“Block internet access for guest VLAN except port 443”_)
- Chatbot assistant for help with terms and best practices
- AI-trained rule validator (_“This rule might break DNS resolution for VLAN 20”_)

### 🧩 Device Profiles
- Define per-device:
  - Export formats (JSON, XML, CLI)
  - Deployment methods (SSH, API, restore-from-backup)
  - Factory-reset instructions (for failsafe restore)
- Import Existing Configurations
  - Parse vendor backup files to prepopulate the GUI
	- Plugin system for extracting values from JSON/XML

### 🚀 One-Click Deployments
- Automatically back up current config
- Push new config using the device's NCMM profile
- Preview CLI/JSON Output
  -	Let users toggle a panel to see the config lines that will be applied
	-	Option to download full backup/config file
- Validation Engine
  - Run pre-checks before exporting:
	-	Duplicate subnets
	-	Invalid VLAN IDs
	-	Unreachable nodes

### 🧯 Failsafe Configurations
- Initial failsafe created during setup
- Add additional failsafes over time
- One-click restore with descriptions

### 📁 Version-Controlled Git History
- Local Git repo for all network data and configs
- Optional GitHub repo sync
- AI-generated, user-editable network documentation

### 📽 Onboarding & Help
- First-run Slideshow or Video introducing:
	-	VLANs, SSIDs, WANs
	-	What a firewall rule is
	-	How NCMM works
-	Inline “?” tooltips next to every major section
-	Context-sensitive help panel in sidebar (auto-populates based on selected element)

### 🧑‍🤝‍🧑 Multi-user & Collaboration (Later Stage)
- Web app allows team collaboration
  - Git-style history or snapshots
  - Comment threads on rules/nodes
- Project Templates & Sharing
    - Users can export projects as templates
    - Community-shared configurations (like Docker Compose templates)

### Virtual Deployment and Testing (Later Stage)
- Integration with Virtual Networking platforms (Netbird, etc.) 

---

## 🖥️ Initial Target Platforms

- **OpenWRT**
- **TP-Link Omada**
- **Ubiquiti UniFi**
- Overall platform/device support determined by Community activity

---

## 💡 Philosophy

Everyone should be able to build and maintain a secure, functional network — regardless of their technical background. NCMM is built for **clarity, control, and confidence**.

---

## 📅 Roadmap

| Phase | Milestone                                  | Status        |
|-------|--------------------------------------------|---------------|
| 1     | UI/UX Design + Core Blueprint               | ✅ In Progress |
| 2     | GitHub/Subreddit Launch                     | 🔜 Soon        |
| 3     | First Vendor Ecosystem Implementation       | 🛠️ Planned     |
| 4     | Drag & Drop Rule Creation                   | 🛠️ Planned     |
| 5     | Config Export/Deploy + Git Integration      | 🛠️ Planned     |
| 6     | AI Helper + Device Profile Wizard           | 🚧 Future      |

---

## 🙋 Get Involved:

- 💻 Developers (Python, Vue/React, YAML/JSON)
- ⚙️ Firmware reverse engineers
- 🧬 AI Experts / Machine Learning Devs
- 🖌️ UI/UX designers
- 💰 Sponsors / Donors
- 🧪 Testers (tech-savvy or not!)
- 📢 Community evangelists
- 🤝 Project partners (e.g., NetBird, Tailscale)

---

## 📎 License

MIT (tentative) — to promote wide adoption and collaboration.

---

## 📬 Contact & Community

- 🐙 GitHub: [github.com/digital-lifestyle-creations/NCMM](https://github.com/digital-lifestyle-creations/NCMM)
- 📣 Subreddit: [r/NCMM](https://reddit.com/r/NCMM) *(coming soon)*
- ✉️ Email: ncmm.dev@DigitalLifestyleCreations.com
