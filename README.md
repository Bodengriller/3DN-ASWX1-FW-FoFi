# 3DN-ASWX1-FW-FoFi
MEINE Änderungen an der 3D-Nexus-Firmware für den Artillery Sidewinder X1


## Zu diesem Repo
Earl Miller von 3D Nexus bietet auf
https://3d-nexus.com/resources/file-archives/download/5-printer-firmware/11-artillery-swx1-marlin-1-1-9-advanced-firmware-and-gui
seine Firmware-Modifikation von Marlin 1.1.9 an.

Er hat in seiner Firmware Mesh Bed Leveling (MBL) aktiviert und sich mit seiner Arbeit sehr viel Mühe gegeben.
Seine Firmware wird von vielen Leuten genutzt und ist daher als "erprobt und für gut befunden" anzuerkennen.

Es gab ein paar Kleinigkeiten, die **mir persönlich** nicht 100%ig passten, darum habe ich diese angepasst.

Ich nutze dieses Repo ausdrücklich nur als Speicher- Ablage- und Dokumentations-Ort für meine eigenen Änderungen.
Dies ist auch der Grund, wieso ich dies hier nur sporadisch und auf Deutsch dokumentiere.
Diese Änderungen dürfen natürlich von jedermann mit-benutzt werden, allerdings **wird es hier keinen Support geben!**

Bei Fragen zur Firmware wendet euch bitte an Earl Miller von 3D Nexus auf seiner Seite.


## Änderungen
Änderungen in den Configs wurden mit "FoFi" gekennzeichnet.
Dies hier sind einige Erläuterungen (als Gedankenstütze an mich selbst):


**Zeile:**	333  
**3DN:**	#define TEMP_HYSTERESIS 5  
**FoFi:**	#define TEMP_HYSTERESIS 3  
**Grund:**	Ich habe liebe eine stabile Temperatur als eine Zeitersparnis von wenigen Sekunden  
  
**Zeile:**	355  
**3DN:**	#define HEATER_0_MAXTEMP 250  
**FoFi:**	#define HEATER_0_MAXTEMP 275  
**Grund:**	Bei Temp-Towers mit PETG (220 - 265°C) hatte ich massive Probleme im oberen Bereich.  
Marlin rechnet sowieso immer 15°C "Sicherheit" ein. bei 250°C erreicht man also effektig nur eine stabile Temperatur von 235 - 240°C.   Alles darüber ist ein ständiges Ein-Aus und mit Pech läuft man in den "Heating failed"-Fehler obwohl man "nur" 265°C ansteuerte.  
  
**Zeile:**	361  
**3DN:**	#define BED_MAXTEMP 120  
**FoFi:**	#define BED_MAXTEMP 150  
**Grund:**	Ich bin der Ansicht, dass mein Alu-Bett mit der Silikonmatte auch mehr als 120°C (abzgl. Sicherheit) ab kann. Ich brauche es nicht, will es aber nutzen können. (Original steht hier auch 150)  
  
**Zeile:**	390  
**3DN:**	#define DEFAULT_Kp 11.92  
		#define DEFAULT_Ki 0.87  
		#define DEFAULT_Kd 40.97  
**FoFi:**  //FoFi Sidewinder X1 at 205°C  
		#define DEFAULT_Kp 10.85  
		#define DEFAULT_Ki 0.75  
		#define DEFAULT_Kd 39.12  
**Grund:**	Persönliche Mittelwerte - Müssen natürlich übers PID-Tuning neu ermittelt werden!  
  
**Zeile:**	446  
**3DN:**	#define DEFAULT_bedKp 57.71  
		#define DEFAULT_bedKi 8.81  
		#define DEFAULT_bedKd 252.09  
**FoFi:**	//FoFi Sidewinder X1 at 60°C  
		#define DEFAULT_bedKp 83.48  
		#define DEFAULT_bedKi 8.15  
		#define DEFAULT_bedKd 213.72  
**Grund:**	Persönliche Mittelwerte - Müssen natürlich übers PID-Tuning neu ermittelt werden!  
  
**Zeile:**	625  
**3DN:**	#define DEFAULT_AXIS_STEPS_PER_UNIT   { 80, 80, 400, 445 }  
**FoFi:**	#define DEFAULT_AXIS_STEPS_PER_UNIT   { 80.121, 80.121, 399.778, 445 }  
**Grund:**	Diese Werte werden in der Artillery-FW verwendet und ich habe nichts daran auszusetzen! (Einige nutzer mügen die glatten Werte lieber!)  
  
**Zeile:**	897 & 901  
**3DN:**	#define Y_BED_SIZE 310  
		#define X_MIN_POS -2  
**FoFi:**	#define Y_BED_SIZE 300  
		#define X_MIN_POS 0  
**Grund:**	Für mich waren diese Werte einfach falsch! Man konnte mit der Nozzle nach hinten und rechts über den Druckbereich fahren (jedoch nicht in einen mechanischen Anschlag). Ich habe diese Werte ermittelt und so rundherum ca. 5mm Software-Limit um den Druckbereich.  
  
**Zeile:**	1168 & 1170  
**3DN:**	#define HOMING_FEEDRATE_XY (80\*60)  
		#define HOMING_FEEDRATE_Z  (20\*60)  
**FoFi:**	#define HOMING_FEEDRATE_XY (60\*60)  
		#define HOMING_FEEDRATE_Z  (10\*60)  
**Grund:**	Ich habe es lieber, wenn die Achsen beim homen etwas sanfter vor die Inis fahren.  
  
**Zeile:**	1176 & 1178  
**3DN:**	#define PREHEAT_1_TEMP_HOTEND 180  
		#define PREHEAT_1_TEMP_BED     70  
**FoFi:**	#define PREHEAT_1_TEMP_HOTEND 200  
		#define PREHEAT_1_TEMP_BED     65  
**Grund:**	Persönlicher Geschmack  
  
## Sonstiges  
Kompiliert mit ArduinoIDE 1.8.12 (without Bootloader)  
Board: "Arduino/Genuino Mega or Mega 2560"  
Processor: "ATmega2560 (Mega 2560)"  
  
## Verlauf  
**11.06.2020** - Erste Überarbeitung/Anpassung der 3D-Nexus-Firmware (Marlin 1.1.9)
