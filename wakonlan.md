Verslag: Wake on LAN via Home AssistantDit verslag beschrijft de stapsgewijze procedure die is gevolgd om een Ubuntu Server op afstand te kunnen starten vanuit Home Assistant, specifiek voor het inschakelen van Wake on LAN (WOL).Benodigde ComponentenUbuntu Server: De doel-pc die op afstand moet worden gestart.Home Assistant: Het automatiseringsplatform dat de commando's zal versturen.Netwerk: Een lokaal netwerk waarin beide apparaten zich bevinden.PuTTY / Terminal: Voor het uitvoeren van commando's op de Ubuntu Server en Home Assistant.Stapsgewijze Procedure1. Ubuntu Server voorbereiden voor Wake on LAN (WOL)Om de server via het netwerk te kunnen starten, moet Wake on LAN ingeschakeld zijn.BIOS/UEFI-instellingen:De server is opnieuw opgestart en het BIOS/UEFI-menu is geopend (meestal via Del, F2, F12 of Esc).In de energiebeheerinstellingen (bijv. "Power Management" of "APM Configuration") is de optie "Wake on LAN" of "Power On By LAN/Ethernet" ingeschakeld."Deep Sleep" of vergelijkbare energiebesparende opties zijn uitgeschakeld om te voorkomen dat de netwerkadapter volledig wordt uitgeschakeld.De wijzigingen zijn opgeslagen en de server is opnieuw opgestart.Ubuntu OS-instellingen (met ethtool):Het ethtool-programma is geïnstalleerd op de Ubuntu Server:sudo apt update
sudo apt install ethtool

De naam van de Ethernet-interface is geïdentificeerd als enp3s0 met ip a.De WOL-ondersteuning van de interface is gecontroleerd met sudo ethtool enp3s0 | grep Wake-on om te bevestigen dat 'g' (magic packet) wordt ondersteund.WOL is tijdelijk ingeschakeld met sudo ethtool -s enp3s0 wol g.Om WOL permanent te maken na herstarts, is een systemd service aangemaakt en ingeschakeld:Bestand /etc/systemd/system/wakeonlan@enp3s0.service is aangemaakt met de volgende inhoud:[Unit]
Description=Enable Wake On LAN for enp3s0
After=network.target

[Service]
Type=oneshot
ExecStart=/usr/sbin/ethtool -s %i wol g
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target

De service is ingeschakeld en gestart:sudo systemctl enable wakeonlan@enp3s0.service
sudo systemctl start wakeonlan@enp3s0.service
sudo systemctl daemon-reload

2. Home Assistant configuratieDe configuration.yaml van Home Assistant is aangepast om de wake_on_lan integratie toe te voegen.Voor het starten (Wake on LAN):Het MAC-adres (50:eb:f6:bb:61:ac) en IP-adres (192.168.2.6) van de enp3s0 interface zijn gebruikt.wake_on_lan:
  - mac_address: "50:eb:f6:bb:61:ac"
    name: "Ubuntu Server"
    host: "192.168.2.6"

Home Assistant is opnieuw opgestart na de configuratiewijzigingen.3. Knop in Home Assistant UIEen knop is toegevoegd aan het Home Assistant dashboard:"Start Ubuntu Server" knop: Roept de dienst wake_on_lan.send_packet aan met het doel wake_on_lan.ubuntu_server.ResultaatNa het doorlopen van alle stappen en het oplossen van de geïdentificeerde problemen, is de functionaliteit succesvol getest. De Ubuntu Server kan nu via Wake on LAN worden opgestart via de knop in de Home Assistant gebruikersinterface.Deze procedure heeft gezorgd voor een geautomatiseerde en efficiënte controle over de opstartstatus van de Ubuntu Server vanuit Home Assistant.
