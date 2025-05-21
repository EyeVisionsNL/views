Stappenplan: Server in Slaapstand Zetten vanuit Home Assistant
Dit document beschrijft de stappen om een server in slaapstand te zetten via een shell_command in Home Assistant, inclusief de benodigde SSH-configuratie.

Open de Terminal & SSH add-on in Home Assistant.
Navigeer naar de configuratiemap:
```javascript
cd /config
```
Maak een verborgen map voor SSH-sleutels aan en stel de juiste permissies in:
```javascript
mkdir -p .ssh
chmod 700 .ssh
```
Genereer het SSH-sleutelpaar. Druk op Enter voor de standaardlocatie (/config/.ssh/id_rsa) en druk nogmaals op Enter voor een lege wachtwoordzin. Een lege wachtwoordzin is cruciaal voor geautomatiseerde scripts.
```javascript
ssh-keygen -t rsa -b 4096 -f /config/.ssh/id_rsa -N ""
```
Dit maakt twee bestanden aan: /config/.ssh/id_rsa (de privé sleutel) en /config/.ssh/id_rsa.pub (de publieke sleutel).

Stap 2: Voeg de Publieke Sleutel toe aan je Server
De publieke sleutel moet op de server worden geplaatst zodat de gebruiker eyevisions zonder wachtwoord kan inloggen vanaf Home Assistant.

Bekijk de inhoud van de zojuist gegenereerde publieke sleutel in de Home Assistant Terminal:
```javascript
cat /config/.ssh/id_rsa.pub
```
Kopieer de hele output van dit commando. Dit is je publieke sleutel.
Log in op je server als gebruiker :
```javascript
ssh eyevisions@nothomeassistant
```
Maak op de server een .ssh map aan en stel de juiste permissies in, als deze nog niet bestaan:
```javascript
mkdir -p ~/.ssh
chmod 700 ~/.ssh
```
Voeg de gekopieerde publieke sleutel toe aan het authorized_keys bestand van de gebruiker eyevisions. Vervang PLAK_HIER_DE_INHOUD_VAN_ID_RSA.PUB door de tekst die je in stap 2 hebt gekopieerd.
```javascript
echo "PLAK_HIER_DE_INHOUD_VAN_ID_RSA.PUB" >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```
Log uit van de server.

Stap 3: Configureer het shell_command in Home Assistant
Nu we zeker weten dat de SSH-sleutels correct staan, passen we het shell_command aan om de SSH-verbinding correct te initiëren, zelfs in een niet-interactieve omgeving.

Open je configuration.yaml bestand in Home Assistant (bijv. via de File Editor add-on).

Voeg het volgende shell_command toe aan je configuratie.yaml file:
```javascript
shell_command:
  hibernate_server: "/usr/bin/ssh -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null -i /config/.ssh/id_rsa eyevisions@192.168.2.6 'sudo systemctl hibernate'"
```
Ga in Home Assistant naar Instellingen > Systeem > Herstarten.
Kies Volledige herstart.
Stap 5: Test het Commando
Na de herstart kun je testen of het shell_command nu correct werkt.

