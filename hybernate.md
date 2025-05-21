# Server in Slaapstand Zetten via Home Assistant (Hibernate)

Dit document beschrijft hoe je een server in slaapstand (hibernate) zet via **Home Assistant**, met behulp van een `shell_command` en SSH-sleutels.

---

## 🔧 Benodigde Voorwaarden

- **Home Assistant** geïnstalleerd met toegang tot de **Terminal & SSH** add-on
- **Ubuntu Server** waarop SSH-toegang mogelijk is
- **Gebruiker met sudo-rechten** op de server
- **Geen wachtwoordzin** op de SSH-sleutel vereist voor automatisering

---

## 🛠️ Stap 1: SSH-sleutel genereren in Home Assistant

1. Open de **Terminal & SSH** add-on in Home Assistant.
2. Navigeer naar de configuratiemap:

   ```bash
   cd /config
   ```

3. Maak de `.ssh` map aan en stel de juiste rechten in:

   ```bash
   mkdir -p .ssh
   chmod 700 .ssh
   ```

4. Genereer het SSH-sleutelpaar (druk telkens op `Enter` voor de standaardwaarden):

   ```bash
   ssh-keygen -t rsa -b 4096 -f /config/.ssh/id_rsa -N ""
   ```

   Hiermee worden twee bestanden aangemaakt:
   - `/config/.ssh/id_rsa` (privésleutel)
   - `/config/.ssh/id_rsa.pub` (publieke sleutel)

---

## 📥 Stap 2: Publieke sleutel toevoegen aan je server

1. Bekijk de inhoud van de publieke sleutel:

   ```bash
   cat /config/.ssh/id_rsa.pub
   ```

2. **Kopieer** de volledige output van dit commando.

3. Log in op je server als de juiste gebruiker:

   ```bash
   ssh eyevisions@nothomeassistant
   ```

4. Maak op de server (indien nodig) de `.ssh` map aan en stel de juiste rechten in:

   ```bash
   mkdir -p ~/.ssh
   chmod 700 ~/.ssh
   ```

5. Voeg de gekopieerde publieke sleutel toe aan `authorized_keys`:

   ```bash
   echo "PLAK_HIER_DE_INHOUD_VAN_ID_RSA.PUB" >> ~/.ssh/authorized_keys
   chmod 600 ~/.ssh/authorized_keys
   ```

6. Log uit van de server.

---

## ⚙️ Stap 3: shell_command instellen in Home Assistant

1. Open je `configuration.yaml` bestand in Home Assistant.
2. Voeg de volgende configuratie toe:

   ```yaml
   shell_command:
     hibernate_server: "/usr/bin/ssh -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null -i /config/.ssh/id_rsa eyevisions@192.168.2.6 'sudo systemctl hibernate'"
   ```

3. Ga naar **Instellingen > Systeem > Herstarten**.
4. Kies **Volledige herstart**.

---

## ✅ Stap 4: Test het Commando

Na de herstart kun je het commando testen vanuit Developer Tools of een knop in de UI. Als alles correct is ingesteld, zal de server in slaapstand gaan na het uitvoeren van het `shell_command`.

---

## 🧠 Opmerkingen

- Zorg dat de gebruiker `eyevisions` **sudo mag uitvoeren zonder wachtwoord** voor het `hibernate`-commando. Voeg eventueel toe aan `/etc/sudoers.d/hibernate`:

  ```bash
  eyevisions ALL=NOPASSWD: /bin/systemctl hibernate
  ```

- Test eerst of `sudo systemctl hibernate` werkt op de server zelf voordat je dit via Home Assistant probeert.

---

## 📎 Referenties

- [Home Assistant shell_command Docs](https://www.home-assistant.io/integrations/shell_command/)
- [Ubuntu Hibernate Handleiding](https://wiki.ubuntu.com/PowerManagement/Hibernate)
