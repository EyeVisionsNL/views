# 💤 Home Assistant ➡️ Server Miep Hibernate via SSH

Deze handleiding beschrijft hoe je vanuit Home Assistant je Linux-server (bijvoorbeeld je voice-server **"Miep"**) via SSH in de **hibernate-stand** zet.  
Ideaal om energie te besparen wanneer je Whisper, Piper en OpenWakeWord even niet nodig hebt! 🔇⚡

---

## 🛠️ Wat heb je nodig?

- 🏠 Home Assistant OS
- 📦 De **Terminal & SSH** add-on in Home Assistant
- 🖥️ Een Linux-server genaamd **Miep**
- 👤 Een gebruiker op Miep (bijv. `eyevisions`) die `sudo systemctl hibernate` mag uitvoeren
- 🔐 Een **wachtwoordloze SSH-verbinding** (met private/public key)

---

## 📜 Stappenplan

### 1️⃣ Genereer een SSH-sleutelpaar in Home Assistant

Open de Terminal in Home Assistant en voer uit:

```bash
ssh-keygen -t rsa -b 4096 -f /config/id_rsa_hass -N ""
```

Dit genereert:
- 🔑 `/config/id_rsa_hass` (private key)
- 🗝️ `/config/id_rsa_hass.pub` (public key)

---

### 2️⃣ Kopieer de publieke sleutel

```bash
cat /config/id_rsa_hass.pub
```

📋 Kopieer de output die begint met `ssh-rsa ...`.

---

### 3️⃣ Log in op je server **Miep**

```bash
ssh eyevisions@192.168.2.6
```

---

### 4️⃣ Maak `.ssh` map aan (indien nodig) en stel juiste rechten in

```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh
```

---

### 5️⃣ Voeg de publieke sleutel toe aan `authorized_keys`

Optioneel: back-up maken van bestaande sleutelbestand:

```bash
mv ~/.ssh/authorized_keys ~/.ssh/authorized_keys_backup
```

Voeg je sleutel toe (vervang onderstaande sleutel door je eigen uit stap 2!):

```bash
echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQC2chdal0FPbTIhNsLonCWwpJQTinHLlYbaLBgIJK3N2Rmb5/..." > ~/.ssh/authorized_keys
```

---

### 6️⃣ Controleer de inhoud van `authorized_keys`

```bash
cat ~/.ssh/authorized_keys
```

✅ Hier moet nu alleen jouw publieke sleutel uit stap 2 staan.

---

### 7️⃣ Stel de juiste rechten in

```bash
chmod 600 ~/.ssh/authorized_keys
```

---

### 8️⃣ Voeg de host key van Miep toe in Home Assistant

In Home Assistant:

```bash
ssh-keyscan 192.168.2.6 > /config/known_hosts_hass
```

🔒 Dit voorkomt interactieve bevestiging bij de eerste verbinding.

---

### 9️⃣ Voeg `shell_command` toe in je `configuration.yaml`

Open `configuration.yaml` in Home Assistant en voeg toe:

```yaml
shell_command:
  hibernate_server: "ssh -o 'StrictHostKeyChecking=yes' -o 'UserKnownHostsFile=/config/known_hosts_hass' -i /config/id_rsa_hass eyevisions@192.168.2.6 'sudo systemctl hibernate'"
```

📌 Herstart Home Assistant na het aanpassen van deze configuratie!

---

## ✅ Gebruik in Home Assistant

Je kunt nu deze `shell_command` gebruiken in:

- 🔁 Automatiseringen
- ▶️ Scripts
- 🎛️ Dashboards (knoppen!)

Bijv. een knop in je dashboard:

```yaml
type: button
name: Hibernate Server Miep
icon: mdi:power-sleep
tap_action:
  action: call-service
  service: shell_command.hibernate_server
```

---

## 🧠 Over Server Miep

**Miep** is jouw lokale slimme voice-server met:

- 🗣️ Whisper (large-v3)
- 🔊 Piper TTS
- 🎤 OpenWakeWord met eigen wake word: **"Hey Miep"**

---

## ❤️ Credits

Met 💡 bedacht en 🛠️ gebouwd door **jou**  
Voor iedereen die zijn slimme huis ook écht slim wil maken 🧠🏡

---

## 🐧 Powered by

- [Home Assistant](https://www.home-assistant.io/)
- Linux
- SSH
- Whisper, Piper & OpenWakeWord
