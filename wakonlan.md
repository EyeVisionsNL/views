# Wake on LAN via Home Assistant

Dit document beschrijft de stappen om een **server-129 op afstand te starten via Wake on LAN (WOL)**, gestuurd vanuit **Home Assistant**.

## 🔧 Benodigde Componenten

- **server-129**: De pc die op afstand gestart moet worden.
- **Home Assistant**: Het automatiseringsplatform dat het commando verzendt.
- **Lokaal netwerk**: Beide apparaten moeten zich in hetzelfde netwerk bevinden.
- **PuTTY / Terminal**: Voor het uitvoeren van commando's op de server en Home Assistant.

---

## 📝 Stapsgewijze Procedure

### 1. server-129 voorbereiden voor Wake on LAN

#### BIOS/UEFI-instellingen

1. Start de server opnieuw op en open het BIOS/UEFI-menu (vaak via `Del`, `F2`, `F12` of `Esc`).
2. Navigeer naar de energiebeheerinstellingen (bijv. *Power Management* of *APM Configuration*).
3. Schakel de optie **"Wake on LAN"** of **"Power On By LAN/Ethernet"** in.
4. Schakel opties zoals **"Deep Sleep"** uit, zodat de netwerkadapter actief blijft.
5. Sla de instellingen op en herstart de server.

#### Ubuntu OS-instellingen

1. Installeer `ethtool`:

   ```bash
   sudo apt update
   sudo apt install ethtool
   ```

2. Zoek de naam van de netwerkinterface (bijv. `enp3s0`):

   ```bash
   ip a
   ```

3. Controleer of WOL wordt ondersteund:

   ```bash
   sudo ethtool enp3s0 | grep Wake-on
   ```

4. Activeer WOL tijdelijk:

   ```bash
   sudo ethtool -s enp3s0 wol g
   ```

5. Maak WOL permanent via een systemd-service:

   Maak het volgende bestand aan:  
   **`/etc/systemd/system/wakeonlan@enp3s0.service`**

   ```ini
   [Unit]
   Description=Enable Wake On LAN for enp3s0
   After=network.target

   [Service]
   Type=oneshot
   ExecStart=/usr/sbin/ethtool -s %i wol g
   RemainAfterExit=yes

   [Install]
   WantedBy=multi-user.target
   ```

6. Activeer en start de service:

   ```bash
   sudo systemctl daemon-reload
   sudo systemctl enable wakeonlan@enp3s0.service
   sudo systemctl start wakeonlan@enp3s0.service
   ```

---

### 2. Home Assistant configureren

Voeg in `configuration.yaml` de integratie toe:

```yaml
wake_on_lan:

switch:
  - platform: wake_on_lan
    mac_address: "52:b7:d3:03:76:c0"
    name: "server-129"
    host: "192.168.198.35"
```

> ✅ Herstart Home Assistant na het aanpassen van de configuratie.

---

### 3. Knop in de Home Assistant UI

Voeg een knop toe aan je dashboard die een WOL-pakket verzendt:

```yaml
type: button
name: Start server-129
icon: mdi:power
tap_action:
  action: call-service
  service: wake_on_lan.send_magic_packet
  service_data:
    mac: "52:b7:d3:03:76:c0"
    broadcast_address: "192.168.2.255"
```

Zorg dat het broadcast-adres overeenkomt met je netwerkconfiguratie.

---

## ✅ Resultaat

Na het uitvoeren van deze stappen is de server-129 met succes op afstand op te starten via Home Assistant. De server reageert betrouwbaar op de knop *"Start server-129"* in de gebruikersinterface.

Deze aanpak zorgt voor een geautomatiseerde, energiezuinige oplossing om servers enkel aan te zetten wanneer nodig.

---

## 📎 Referenties

- [Ubuntu manpage ethtool](https://manpages.ubuntu.com/manpages/jammy/en/man8/ethtool.8.html)
- [Home Assistant Wake on LAN Docs](https://www.home-assistant.io/integrations/wake_on_lan/)
