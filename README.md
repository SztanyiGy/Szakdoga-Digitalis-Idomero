=============================================
DIGITÁLIS IDŐMÉRŐ - OLVASÁSI ÚTMUTATÓ
=============================================

ALKALMAZÁS LEÍRÁSA
------------------
A Digitális Időmérő egy Windows alapú asztali alkalmazás, amely
nyomon követi a felhasználó digitális eszközhasználatát. Az alkalmazás
rögzíti az aktív ablakok használati idejét, statisztikákat készít,
valamint időzítő funkcióval is rendelkezik.

Főbb funkciók:
- Aktív alkalmazások és ablakok figyelése
- Használati idő rögzítése és kategorizálása
- Napi és heti statisztikák megjelenítése
- Adatok exportálása CSV és Excel formátumban
- Időzítő funkció értesítéssel
- Inaktivitás kezelése (5 perc után automatikus szüneteltetés)


RENDSZERKÖVETELMÉNYEK
---------------------
- Operációs rendszer: Windows 10 vagy Windows 11 (64 bit)
- Java Development Kit (JDK) 21 vagy újabb verzió
- Apache Maven 3.8 vagy újabb verzió
- Minimális RAM: 512 MB
- Ajánlott RAM: 1 GB vagy több
- Szabad lemezterület: minimum 200 MB


A PROJEKT IMPORTÁLÁSA INTELLIJ IDEA-BA
---------------------------------------
1. Csomagold ki a zip fájlt egy tetszőleges mappába
2. Nyisd meg az IntelliJ IDEA fejlesztői környezetet
3. Válaszd a File > Open menüpontot
4. Navigálj a kicsomagolt "Szakdoga-Digitalis-Idomero-main" mappába
5. Kattints az OK gombra
6. Az IntelliJ IDEA automatikusan felismeri a Maven projektet
7. Várd meg amíg a Maven letölti a szükséges függőségeket
   (ez első alkalommal néhány percet vehet igénybe)
8. Ha a Maven szinkronizálás nem indul el automatikusan:
   jobb klikk a pom.xml fájlra > Maven > Reload Project


AZ ALKALMAZÁS FUTTATÁSA FEJLESZTŐI KÖRNYEZETBŐL
-------------------------------------------------
1. A projekt betöltése után keresd meg a Launcher.java osztályt:
   src/main/java/org/example/digitalisidomero/Launcher.java
2. Jobb klikk a fájlra > Run 'Launcher.main()'
   VAGY
   Nyisd meg a fájlt és kattints a zöld nyíl ikonra a szerkesztő mellett


LEFORDÍTOTT JAR FÁJL LÉTREHOZÁSA
---------------------------------
1. Nyisd meg a terminált a projekt gyökérmappájában
   (IntelliJ IDEA-ban: View > Tool Windows > Terminal)
2. Futtasd le a következő parancsot:

   mvn clean package

3. A lefordított JAR fájl a target/ mappában jön létre:
   target/DigitalisIdomero.jar


EXE FÁJL ÉS FUTTATHATÓ MAPPA LÉTREHOZÁSA
------------------------------------------
A jpackage eszköz segítségével önálló, futtatható alkalmazásmappa
hozható létre, amely Java telepítés nélkül is futtatható.

1. Először futtasd le a JAR létrehozását:
   mvn clean package

2. Majd futtasd le a következő parancsot a projekt gyökérmappájában:

   jpackage --input target --name DigitalisIdomero --main-jar DigitalisIdomero.jar --main-class org.example.digitalisidomero.Launcher --type app-image --win-console

3. A parancs lefutása után létrejön egy "DigitalisIdomero" nevű mappa,
   amelyben megtalálható az alkalmazás futtatható állománya.

4. Az alkalmazás elindításához nyisd meg a mappát és futtasd:
   DigitalisIdomero.exe


PROJEKT STRUKTÚRA
-----------------
Szakdoga-Digitalis-Idomero-main/
│
├── pom.xml                          - Maven konfiguráció és függőségek
├── config.properties                - Alkalmazás konfigurációs fájl
├── timetracker.db                   - SQLite adatbázis fájl
├── readme.txt                       - Ez a fájl
│
├── src/main/java/org/example/digitalisidomero/
│   │
│   ├── Launcher.java                - Alkalmazás belépési pontja
│   ├── Main.java                    - Főosztály
│   ├── module-info.java             - Java modul konfiguráció
│   │
│   ├── config/
│   │   ├── AppConfig.java           - Alkalmazás konfiguráció kezelése
│   │   └── Constants.java           - Alkalmazás konstansok
│   │
│   ├── database/
│   │   ├── DatabaseConnection.java  - Adatbázis kapcsolat kezelése
│   │   ├── DatabaseInitializer.java - Adatbázis táblák inicializálása
│   │   └── dao/
│   │       ├── ApplicationDAO.java  - Alkalmazás adatok kezelése
│   │       ├── CategoryDAO.java     - Kategória adatok kezelése
│   │       └── SessionDAO.java      - Munkamenet adatok kezelése
│   │
│   ├── model/
│   │   ├── Application.java         - Alkalmazás adatmodell
│   │   ├── Category.java            - Kategória adatmodell
│   │   └── Session.java             - Munkamenet adatmodell
│   │
│   ├── monitor/
│   │   ├── ActivityDetector.java    - Felhasználói inaktivitás figyelése
│   │   ├── MonitorService.java      - Ablakfigyelés koordinálása
│   │   └── WindowMonitor.java       - Aktív ablak lekérdezése (JNA)
│   │
│   ├── service/
│   │   ├── CategoryService.java     - Kategória üzleti logika
│   │   ├── ExportService.java       - CSV és Excel export
│   │   ├── MonitorService.java      - Figyelési szolgáltatás
│   │   ├── NotificationService.java - Értesítések kezelése
│   │   ├── StatisticsService.java   - Statisztikák számítása
│   │   ├── TimeLimitService.java    - Időkorlát kezelése
│   │   └── TrackingService.java     - Nyomkövetési logika
│   │
│   ├── ui/
│   │   ├── MainController.java      - Főképernyő kontroller
│   │   ├── StatisticsController.java- Statisztika képernyő kontroller
│   │   └── TimerController.java     - Időzítő képernyő kontroller
│   │
│   └── util/
│       ├── DateUtils.java           - Dátum segédeszközök
│       └── TimeFormatter.java       - Idő formázó segédeszközök
│
└── src/main/resources/org/example/digitalisidomero/
    ├── main-view.fxml               - Főképernyő felület leíró
    ├── statistics-view.fxml         - Statisztika képernyő felület leíró
    ├── timer-view.fxml              - Időzítő képernyő felület leíró
    ├── styles.css                   - Főstíluslap
    └── statistics.css               - Statisztika oldal stíluslap


FELHASZNÁLT TECHNOLÓGIÁK
-------------------------
- Java 21
- JavaFX 21 (grafikus felhasználói felület)
- SQLite (helyi adatbázis)
- JNA / JNA-Platform 5.14.0 (Windows API hívások)
- Apache POI 5.2.5 (Excel export)
- Apache Maven (projekt menedzsment)
- Log4j 2.22.1 (naplózás)


MEGJEGYZÉSEK
------------
- Az alkalmazás kizárólag Windows operációs rendszeren működik,
  mivel az aktív ablak figyeléséhez Windows API hívásokat használ (JNA).
- Az adatok helyi SQLite adatbázisban tárolódnak (timetracker.db),
  amely az alkalmazás első indításakor automatikusan létrejön.
- Az alkalmazás fejlesztője: Sztányi György
- Fejlesztői környezet: IntelliJ IDEA, Java 21, Maven


=============================================
DIGITAL TIME TRACKER - README
=============================================

APPLICATION DESCRIPTION
------------------------
Digital Time Tracker is a Windows-based desktop application that
monitors the user's digital device usage. The application records
active window usage time, generates statistics, and includes a
timer function.

Main features:
- Monitoring active applications and windows
- Recording and categorizing usage time
- Displaying daily and weekly statistics
- Exporting data in CSV and Excel format
- Timer function with notifications
- Inactivity handling (automatic pause after 5 minutes)


SYSTEM REQUIREMENTS
-------------------
- Operating System: Windows 10 or Windows 11 (64-bit)
- Java Development Kit (JDK) 21 or newer
- Apache Maven 3.8 or newer
- Minimum RAM: 512 MB
- Recommended RAM: 1 GB or more
- Free disk space: minimum 200 MB


IMPORTING THE PROJECT INTO INTELLIJ IDEA
-----------------------------------------
1. Extract the zip file to any folder
2. Open IntelliJ IDEA
3. Select File > Open
4. Navigate to the extracted "Szakdoga-Digitalis-Idomero-main" folder
5. Click OK
6. IntelliJ IDEA will automatically recognize the Maven project
7. Wait for Maven to download the required dependencies
   (this may take a few minutes the first time)
8. If Maven sync does not start automatically:
   right-click pom.xml > Maven > Reload Project


RUNNING THE APPLICATION FROM THE DEVELOPMENT ENVIRONMENT
---------------------------------------------------------
1. After loading the project, find the Launcher.java class:
   src/main/java/org/example/digitalisidomero/Launcher.java
2. Right-click the file > Run 'Launcher.main()'
   OR
   Open the file and click the green arrow icon next to the editor


CREATING A COMPILED JAR FILE
-----------------------------
1. Open the terminal in the project root folder
   (In IntelliJ IDEA: View > Tool Windows > Terminal)
2. Run the following command:

   mvn clean package

3. The compiled JAR file will be created in the target/ folder:
   target/DigitalisIdomero.jar


CREATING AN EXE FILE AND RUNNABLE FOLDER
-----------------------------------------
Using the jpackage tool, a standalone application folder can be
created that runs without a Java installation.

1. First create the JAR file:
   mvn clean package

2. Then run the following command in the project root folder:

   jpackage --input target --name DigitalisIdomero --main-jar DigitalisIdomero.jar --main-class org.example.digitalisidomero.Launcher --type app-image --win-console

3. After the command completes, a "DigitalisIdomero" folder will be
   created containing the executable application.

4. To start the application, open the folder and run:
   DigitalisIdomero.exe


PROJECT STRUCTURE
-----------------
Szakdoga-Digitalis-Idomero-main/
│
├── pom.xml                          - Maven configuration and dependencies
├── config.properties                - Application configuration file
├── timetracker.db                   - SQLite database file
├── readme.txt                       - This file
│
├── src/main/java/org/example/digitalisidomero/
│   │
│   ├── Launcher.java                - Application entry point
│   ├── Main.java                    - Main class
│   ├── module-info.java             - Java module configuration
│   │
│   ├── config/
│   │   ├── AppConfig.java           - Application configuration management
│   │   └── Constants.java           - Application constants
│   │
│   ├── database/
│   │   ├── DatabaseConnection.java  - Database connection management
│   │   ├── DatabaseInitializer.java - Database table initialization
│   │   └── dao/
│   │       ├── ApplicationDAO.java  - Application data access
│   │       ├── CategoryDAO.java     - Category data access
│   │       └── SessionDAO.java      - Session data access
│   │
│   ├── model/
│   │   ├── Application.java         - Application data model
│   │   ├── Category.java            - Category data model
│   │   └── Session.java             - Session data model
│   │
│   ├── monitor/
│   │   ├── ActivityDetector.java    - User inactivity detection
│   │   ├── MonitorService.java      - Window monitoring coordination
│   │   └── WindowMonitor.java       - Active window querying (JNA)
│   │
│   ├── service/
│   │   ├── CategoryService.java     - Category business logic
│   │   ├── ExportService.java       - CSV and Excel export
│   │   ├── MonitorService.java      - Monitoring service
│   │   ├── NotificationService.java - Notification management
│   │   ├── StatisticsService.java   - Statistics calculation
│   │   ├── TimeLimitService.java    - Time limit management
│   │   └── TrackingService.java     - Tracking logic
│   │
│   ├── ui/
│   │   ├── MainController.java      - Main screen controller
│   │   ├── StatisticsController.java- Statistics screen controller
│   │   └── TimerController.java     - Timer screen controller
│   │
│   └── util/
│       ├── DateUtils.java           - Date utility tools
│       └── TimeFormatter.java       - Time formatting utilities
│
└── src/main/resources/org/example/digitalisidomero/
    ├── main-view.fxml               - Main screen UI descriptor
    ├── statistics-view.fxml         - Statistics screen UI descriptor
    ├── timer-view.fxml              - Timer screen UI descriptor
    ├── styles.css                   - Main stylesheet
    └── statistics.css               - Statistics page stylesheet


TECHNOLOGIES USED
-----------------
- Java 21
- JavaFX 21 (graphical user interface)
- SQLite (local database)
- JNA / JNA-Platform 5.14.0 (Windows API calls)
- Apache POI 5.2.5 (Excel export)
- Apache Maven (project management)
- Log4j 2.22.1 (logging)


NOTES
-----
- The application only works on Windows operating system,
  as it uses Windows API calls (JNA) to monitor the active window.
- Data is stored in a local SQLite database (timetracker.db),
  which is automatically created when the application first starts.
- Developer: Sztányi György
- Development environment: IntelliJ IDEA, Java 21, Maven
