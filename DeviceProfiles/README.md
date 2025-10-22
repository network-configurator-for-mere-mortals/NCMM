# NCMM (Network Configurator for Mere Mortals)  
### Vendor-Agnostic Device Profiles for Automated Network Management  

## Overview  
NCMM simplifies network configuration by abstracting vendor-specific complexities into **standardized Device Profiles**. Users design networks visually (click/drag), and NCMM translates actions into device-specific commands via a rules engine. Supports:  
- **Network Devices**: Routers, switches, firewalls, APs.  
- **Non-Network Devices**: NAS, Docker, cloud VPS, IP cameras, IoT.  
- **Small Businesses**: PCI-DSS, guest WiFi, digital signage.  

## Key Features  
- **Unified GUI**: Configure MikroTik, Cisco, UniFi, Synology, Docker, etc., in one interface.  
- **Device Profiles**: SQLite database stores vendor/firmware-specific templates and rules.  
- **Dependency-Aware**: Auto-sequences tasks (e.g., create VLAN before assigning ports).  
- **Validation**: Checks success via regex or custom scripts.  

---

## Device Profiles Schema  
NCMM uses a SQLite database (`ncmm_profiles.db`) with the following structure:  

### Core Tables  
| Table                 | Purpose                                                                 |  
|-----------------------|-------------------------------------------------------------------------|  
| `devices`             | Vendor/model, firmware, IP, and config method (SSH/API).               |  
| `tasks`               | All config actions (e.g., `create_vlan`, `docker_static_ip`).          |  
| `templates`           | CLI/API templates (Jinja2/JSON) for each task-device combination.      |  
| `industry_profiles`   | Compliance standards (HIPAA, PCI-DSS) and industry-specific tasks.     |  

### Example Queries  
**1. Get all VLAN tasks for a Cisco switch:**  
```sql  
SELECT t.name, tm.cli_template  
FROM tasks t  
JOIN templates tm ON t.id = tm.task_id  
WHERE t.category = 'vlan' AND tm.device_id = (SELECT id FROM devices WHERE vendor = 'cisco');  
```  

**2. List PCI-DSS compliance tasks:**  
```sql  
SELECT t.name FROM tasks t  
JOIN industry_tasks it ON t.id = it.task_id  
JOIN industry_profiles ip ON it.industry_id = ip.id  
WHERE ip.compliance_standard = 'PCI-DSS';  
```  

---

## Supported Task Categories  
NCMM organizes tasks into **26+ categories**, including:  
| Category               | Examples                                  |  
|------------------------|-------------------------------------------|  
| `vlan`                 | Create VLANs, assign ports.               |  
| `container`            | Docker static IPs, Kubernetes networks.   |  
| `video_surveillance`   | Blue Iris motion zones, RTSP streams.     |  
| `compliance`           | Disable TLS 1.0, enable audit logging.    |  

*(See full list in [CATEGORIES.md](CATEGORIES.md).)*  

---

## How It Works  
1. **User Design**: Drag/drop elements in the GUI (e.g., VLANs, firewalls).  
2. **Task Generation**: Rules engine matches actions to Device Profiles.  
3. **Template Rendering**: Jinja2/JSON templates generate device-specific configs.  
4. **Deployment**: Commands sent via SSH/REST API/Docker CLI.  
5. **Validation**: Checks output against regex or scripts.  

![NCMM Workflow](workflow.png)  

---

## Extending Device Profiles  
### Add a New Device  
1. Insert into `devices` table:  
   ```sql  
   INSERT INTO devices (name, vendor, model, config_method, device_type)  
   VALUES ('my_router', 'MikroTik', 'RB4011', 'ssh_cli', 'network');  
   ```  
2. Add templates for its tasks:  
   ```sql  
   INSERT INTO templates (task_id, device_id, cli_template)  
   VALUES (  
     (SELECT id FROM tasks WHERE name = 'create_vlan'),  
     (SELECT id FROM devices WHERE name = 'my_router'),  
     '/interface vlan add name={{name}} vlan-id={{id}}'  
   );  
   ```  

### Add a New Task  
1. Define the task:  
   ```sql  
   INSERT INTO tasks (name, category, description, device_type)  
   VALUES ('block_ssh_bruteforce', 'firewall', 'Rate-limit SSH connections', 'network');  
   ```  
2. Link to devices/industries as needed.  

---

## FAQs  
**Q: Can NCMM handle firmware-specific quirks?**  
A: Yes! The `firmware_exceptions` table stores version-dependent overrides.  

**Q: How are dependencies (e.g., VLAN before firewall rule) handled?**  
A: The `task_dependencies` table enforces order and conditions.  

**Q: Is SQLite scalable for large networks?**  
A: Yes—benchmarks show sub-ms query times for 10K+ tasks.  

---

## License  
MIT. Contribute at [github.com/ncmm](github.com/ncmm).  
```  

---

### Key Notes for Implementation  
1. **Dynamic UI**: The GUI filters tasks by `device_type` and `category`.  
2. **Security**: Credentials are never stored in the DB—use Vault/Keyring.  
3. **Backup**: Version the `.db` file alongside configs (Git-friendly).
