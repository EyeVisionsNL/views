# views changes made by eyevisions in view-assist dashboards
<h1>Englisch</h1>




<h2>**!!!!You need the view-assist template for all views!!!!**</h2>

<h2>###Feel free to use parts or pieces of scripts.###</h2>
  
   
***No i am not on a Lenovo-thinksmart TSV. I'm on a 10,1inch tablet Teclast P30T***





<h2>https://dinki.github.io/View-Assist/docs/viewassist-setup</h2>

<h3>Made some different dashboard for View-assist. the changes are as follows:</h3>

In each top left corner there is a icon. I have applied this to all the other dashboards, just like in the original weather card. Clicking or holding on this will take you to another dashboard. Here are some examples.

info

![Screenshot_20250225-184650](https://github.com/user-attachments/assets/57f544ef-3757-48a4-9cd5-4be2c4556e89)

mediaplayer dashboard

![Screenshot_20250225-191552](https://github.com/user-attachments/assets/392f098a-85a4-4b36-94d0-968885fe7d29)

intent:

![Screenshot_20250225-203627](https://github.com/user-attachments/assets/57eed1c6-d236-4172-81b3-2498269fb865)


<b>clock:</b>

transition changed, it now goes smoothly to new position instead of jumping to it. The clock also changes color based on the KNMI(dutch weather station that give weather color codes)applicable weather codes. This requires KNMI hacs integration. you can adjust the size of the movement if the clock goes outside your screen. Simply play with the percentages and it should work. NO KNMI simple delete the peace of code and put color to the letters.

<b>Weather:</b>

added shadows to letters and set them to white. background changes with type to reflect what kind of weather is out is there. You can find this card on the orginal view-assist wiki page this one is litlle updated. versie 1.03


<b>thermostat:</b>

Here I have placed mini graphs of the thermostat and a co2 meter. I personally use Apollo MSR-2.

![Screenshot_20250306-161519](https://github.com/user-attachments/assets/cda3e512-13fa-4e33-beda-e65e0442dbff)


<h2>New views not in the orginal view-assist</h2>

<b>Compass rose:</b>

Compass rose card with everything in it want you want to know about the wind. this requires WindRose card from hacs.  (screen shot dutch section)


<b>P2000:</b>

The messages from P2000(dutch police,ambulance,fire codes) from your region will appear here. This will require P2000 from hacs. It show the messages for 15 sec and then go to map view to the location.
The automation uses a chime.  (screen shot dutch section)

<b>Activelights:</b>

This page shows the lights that are on. required custom:auto-entities card from hacs

![Screenshot_20250215-173559](https://github.com/user-attachments/assets/5d86e799-e342-49e0-9dff-78b4f91c0693)

<b>Floor plan:</b>

Plain floor plan in layout/template view-assist. (screen shot dutche section)


<b>Camera:</b>

2 cameras placed next to each other on 1 page.


![Screenshot_20250306-203420](https://github.com/user-attachments/assets/4e3be7ae-4142-4ec7-9123-930e29f74411)




<b>***made some new views like, Agenda, Pollen radar, Lightning radar,more pictures of this in the Dutch section***</b>


![Screenshot_20250306-172344](https://github.com/user-attachments/assets/493cc443-b93b-4f05-a319-82bd625312e6)


files: weatherpictures https://files.fm/u/krd4gzxmwr

Made a dutch wake word "Hey Miep"for those dutch people out there! want to make your own? https://colab.research.google.com/drive/1q1oe2zOyZp7UsB3jJiQ1IFn8z5YfjwEb?usp=sharing#scrollTo=1cbqBebHXjFD

files: hey miep wakeword.



<h1>#Dutch</h1>

<h2>***Je heb voor alle views de template nodig van view-assist!!*** </h2>

<h2>###Voel je vrij om delen of stukken van scripts te gebruiken.###</h2>

****Nee zit niet op lenovo-thinksmart TSV maar tablet 10.1inch teclast p30t***


<h2>https://dinki.github.io/View-Assist/docs/viewassist-setup</h2>

<h3>Ik heb wat verschillende dashboard gemaakt voor View-assist. de wijzigingen zijn als volgt:</h3>

In elke linker boven hoek heb ik een  icon gemaakt net als in de origeneele weather card en dit bij alle andere toegepast. Door hierop te klikken of vast te houden ga je naar een ander dashboard.

clock: transition veranderd deze gaat nu vloeiend naar nieuwe positie ipv ernaar te springen. Ook wijzigd de klok van kleur aan de hand van de KNMI geldende weer codes. Dit vergt KNMI hacs intergratie. 
wat backshadows toegevoegd. je kan formaat van bewegen aanpassen als de clock buiten je scherm gaat. simpel met de procenten spelen dan moet het lukken.  code geel

![Screenshot_20250201-094019](https://github.com/user-attachments/assets/14add1de-846f-4ed1-b691-a08689f39032)


<b>Weather:</b>

schaduwen aangebracht aan de letters en deze naar wit gezet. achtergrond verandert mee met type weer wat er dan is hiervoor zip file met de plaatjes gemaakt weather.zip 

![Screenshot_20250217-193341](https://github.com/user-attachments/assets/a9745e39-18bb-4eb9-aeb1-7bf68b831d48)


<b>thermostaat</b>

Hier heb ik mini graphs van de thermostaat en een co2 meter neergezet. Zelf gebruik ik apollo msr-2.

<h2>***Nieuwe views staan niet in view-assist orgineel***</h2>

<b>Windroos:</b>

Windroos kaart met alles erin. dit vergt WindRose card van hacs.

![Screenshot_20250131-114940](https://github.com/user-attachments/assets/f7865cc3-cc3b-4f0f-9dfb-664b3f611d25)


<b>P2000</b>

Hier komen de berichten van P2000 te staan van je regio of woonplaats Dit vergt P2000 van hacs. Ik heb een helper gemaakt die schakeld tussen de 2 p2000 sensoren
lokaal en regio. Neem aan dat dit zelf wel gaat lukken. Zelf ChimeTTS geluid erbij dedaan die je toch al geinstalleerd had voor view-assist. 
Automatsering kiest ander geluid voor GRIP meldingen en zoomt map in net als bij lokale meldingen

![Screenshot_20250225-192227](https://github.com/user-attachments/assets/c85c5393-a8c5-443f-97a6-04230da67105)

![Screenshot_20250226-191451](https://github.com/user-attachments/assets/38a46366-cbd5-4266-8ead-04d152f73f2c)


<b>activelights:</b>

Deze pagina geeft de lampen weer die aan staan. benodigd custom:auto-entities

![Screenshot_20250215-173559](https://github.com/user-attachments/assets/5d86e799-e342-49e0-9dff-78b4f91c0693)


<b>Floorplan:</b>

Gewoon vloerplan in layout/template view-assist

![Screenshot_20250208-213045](https://github.com/user-attachments/assets/75dd974d-bf43-4fd9-b406-57c280a26337)


<b>Camera:</b>

2 camera's op 1 pagina gezet naast elkaar.


<h3>New/Nieuw:</h3>

<b>Agenda</b>

![Screenshot_20250303-220720](https://github.com/user-attachments/assets/13d6ebb9-e84c-4d88-ae10-5f97b3d94bcd)


<b>Bliksem</b>

![Screenshot_20250303-190523](https://github.com/user-attachments/assets/f0e25934-f406-4ebe-a584-91274291149e)



<b>Pollenradar</b>


![Screenshot_20250306-204236](https://github.com/user-attachments/assets/0fc164d7-d46d-4327-bdb4-8e60ece196a9)



<b>files: weatherpictures https://files.fm/u/krd4gzxmwr

Heb een nederlands wake word gemaakt Hey_Miep gemaakt met Open the wake word training environment. https://colab.research.google.com/drive/1q1oe2zOyZp7UsB3jJiQ1IFn8z5YfjwEb?usp=sharing#scrollTo=1cbqBebHXjFD

files: hey miep wakeword </b>
