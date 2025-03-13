# $${\color{red}Views\space changes\space made \space \color{white}by\space EyeVisionsNL\space for\space \color{blue}{ViewAssist\space dashboards}}$$


![Version](https://img.shields.io/badge/version-1.03-blue)
![HACS](https://img.shields.io/badge/HACS-Required-red)

---

# English

## 📌 Important: You need the ViewAssist dashboard.yaml for all views!

🔗 **[ViewAssist Setup Guide](https://dinki.github.io/View-Assist/docs/viewassist-setup)**

### Feel free to use parts or pieces of these scripts.

💡 *"No, I am not on a Lenovo ThinkSmart TSV. I'm using a 10.1-inch Teclast P30T tablet."*

## 🏠 Dashboard Changes

Each top-left corner now has an icon, just like the original weather card. Clicking or holding this icon navigates to another dashboard.
add back shadows to icons and letters in all the dashboards and template. And swipe to navigate!
Here are some examples:

### 📏 dashboard.yaml
- all changes back shadows are in template.yaml
- Requires **Home Assistant Swipe Navigation** from HACS. If you want to use swiping between dashboards
```javascript
add on row 525
        - filter: drop-shadow(2px 2px 2px black)



swipe_nav:
  wrap: true
  enable_mouse_swipe: true
  enable_on_subviews: true
  animate: flip
  prevent_default: true
  swipe_amount: 10
```

### 📊 Info View
![Screenshot](https://github.com/user-attachments/assets/57f544ef-3757-48a4-9cd5-4be2c4556e89)

### 🎵 Media Player Dashboard
![Screenshot](https://github.com/user-attachments/assets/392f098a-85a4-4b36-94d0-968885fe7d29)

### 🕒 Clock
- The transition is now smooth instead of jumping.
- The clock color changes based on **KNMI weather warnings** (requires KNMI HACS integration).
- You can adjust the movement size if the clock moves outside the screen.
- If no KNMI integration is available, remove the color-changing code and set a static color.

### ☁️ Weather
- Added shadows to letters and set them to white.
- Background changes dynamically to reflect the current weather.
- You can find this updated version (**1.03**) on the original ViewAssist wiki.
  
![Screenshot_20250313-084106](https://github.com/user-attachments/assets/353cc437-f4cd-46cf-909e-7ecbc8958c60)


### 🌡️ Thermostat
- Added **mini graphs** for the thermostat and a CO₂ meter.
- Personally tested with **Apollo MSR-2**.

![Screenshot](https://github.com/user-attachments/assets/cda3e512-13fa-4e33-beda-e65e0442dbff)

## 🔥 New Views (Not in Original ViewAssist)

### 🧭 Compass Rose
- Displays all wind-related information.
- Requires **WindRose card** from HACS.

### 🚨 P2000 (Emergency Alerts)
- Displays P2000 messages for your region.
- Requires **P2000 HACS integration**.
- Messages show for **15 seconds**, then switch to a map view of the location.
- Includes a chime sound for alerts.
- Requires **P2000-sensor** from HACS.

### 💡 Active Lights
- Shows currently active lights.
- Requires **custom:auto-entities** card from HACS.

![Screenshot](https://github.com/user-attachments/assets/5d86e799-e342-49e0-9dff-78b4f91c0693)

### 🏠 Floor Plan
- Simple floor plan layout in ViewAssist.

### 🎥 Camera View
- Displays **two cameras** side by side.

![Screenshot](https://github.com/user-attachments/assets/4e3be7ae-4142-4ec7-9123-930e29f74411)

### 📅 Agenda
- 2 made 1 static background other dynamic like the clock background.
- Requires **Week planner card** from HACS. 
![Screenshot](https://github.com/user-attachments/assets/13d6ebb9-e84c-4d88-ae10-5f97b3d94bcd)

### ⚡ Lightning Radar
- Alerts when lightning is **within 30 km**.
- Switches to a map view for better visualization.
- Dynamic message updates based on distance:
- Requires **Blitzortung.org Lightning_Detector** from HACS.

```javascript
if (strikes > 0) {
    message = `⚡️ ${strikes} strikes detected ${distance} km away.`;
} else {
    message = "✅ No lightning detected.";
}

if (distance <= 10 && strikes > 0) {
    message += " ⚠️ Lightning is very close. Close windows and doors!";
} else if (distance <= 30 && strikes > 0) {
    message += " 🌩️ Lightning nearby. Stay safe!";
}
```

![Screenshot](https://github.com/user-attachments/assets/f0e25934-f406-4ebe-a584-91274291149e)

### 🤧 Pollen Radar
- Displays pollen levels (requires **PollenRadar HACS integration**).

![Screenshot](https://github.com/user-attachments/assets/e547f99a-372b-408c-bd89-8cc421d4aaff)

### 🚗💨 Vehicle dashboard
- Displays the status of your vehicle.
- Requires **Ultra Vehicle Card** from HACS.


![Screenshot_20250313-172654](https://github.com/user-attachments/assets/fa2ee55a-ab7f-422f-9ef8-9879aafe8f6f)


---

# Dutch (Nederlands)

## 📌 Belangrijk: Je hebt de ViewAssist-template nodig voor alle views!

🔗 **[ViewAssist Installatiegids](https://dinki.github.io/View-Assist/docs/viewassist-setup)**

### Voel je vrij om delen van deze scripts te gebruiken.

💡 *"Nee, ik zit niet op een Lenovo ThinkSmart TSV, maar op een 10.1-inch Teclast P30T tablet."*

## 🏠 Wijzigingen in Dashboards

Elke linker bovenhoek bevat nu een **icoon**, net als in de originele weerkaart. Klikken of vasthouden brengt je naar een ander dashboard.

### 🕒 Klok
- **Vloeiende overgang** bij positieverandering.
- Kleur verandert afhankelijk van **KNMI-waarschuwingen**.
- Pas de bewegingsgrootte aan als de klok buiten het scherm komt.

![Screenshot](https://github.com/user-attachments/assets/14add1de-846f-4ed1-b691-a08689f39032)

### 🌡️ Thermostaat
- Mini-grafieken voor thermostaat en CO₂-meter.
- Persoonlijk getest met **Apollo MSR-2**.

### 🌍 Windroos
- Alle windinformatie op één plek.
- Vereist **WindRose kaart** van HACS.

![Screenshot](https://github.com/user-attachments/assets/f7865cc3-cc3b-4f0f-9dfb-664b3f611d25)

### 🚨 P2000
- Weergave van **P2000-meldingen** uit jouw regio.
- Helper schakelt tussen **lokale en regionale** sensoren.
- Speciale **chime-geluiden** voor GRIP-meldingen.

![Screenshot](https://github.com/user-attachments/assets/c85c5393-a8c5-443f-97a6-04230da67105)

### ⚡ Bliksemwaarschuwingen
- Meldingen bij **bliksem binnen 30 km**.
- Kaartweergave met inslagen en waarschuwingen en detectoren in beeld.

![Screenshot](https://github.com/user-attachments/assets/ca891a29-0c04-4e24-9149-b6fbbe3db9de)

### 🤧 Pollenradar
- Handig voor hooikoortspatiënten.
- Vereist **PollenRadar HACS integratie**.

![Screenshot](https://github.com/user-attachments/assets/e547f99a-372b-408c-bd89-8cc421d4aaff)

### 🚗💨 Vehicle dashboard
- Laat de status zien van je voertuig.
- Vereist **Ultra Vehicle Card** van HACS.


![Screenshot_20250313-172654](https://github.com/user-attachments/assets/0c372a5d-bf21-4ad5-b203-3566ae60d08c)

---

## 📂 Download Links
- **Weerafbeeldingen**: [weatherpictures.zip](https://files.fm/u/scc8pg78pk)
- **Nederlands Wake Word - "Hey Miep"**: [Train je eigen wake word](https://colab.research.google.com/drive/1q1oe2zOyZp7UsB3jJiQ1IFn8z5YfjwEb?usp=sharing#scrollTo=1cbqBebHXjFD)
- **wil je miep proberen die staat er bij als zip file**

---


