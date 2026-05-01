===========================================
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

INSTALLATION GUIDE
------------------
If the required tools are not yet installed on your machine:

Java Development Kit (JDK) 21 Installation:
1. Visit https://www.oracle.com/java/technologies/downloads/
2. Download the Windows x64 Installer version (JDK 21)
3. Run the installer and follow the instructions
4. Verify the installation: java -version

Apache Maven Installation:
1. Visit https://maven.apache.org/download.cgi
2. Download the Binary zip archive file
3. Extract it to e.g. C:\Program Files\Maven
4. Add to the PATH environment variable: C:\Program Files\Maven\bin
5. Verify the installation: mvn -version

IntelliJ IDEA Installation:
1. Visit https://www.jetbrains.com/idea/download/
2. Download the Community (free) version
3. Run the installer and follow the instructions

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


SETTINGS REQUIRED FOR RUNNING THE EXE
---------------------------------------
If you only want to use the executable EXE (without a development environment):
- Required: Java 21 or newer must be installed on your machine
- The Java path must be added to the system PATH variable:
  1. Find the Java installation folder, e.g.: C:\Program Files\Java\jdk-21\bin
  2. Open: Control Panel > System > Advanced system settings >
     Environment Variables
  3. Under "System variables" find the "Path" variable
  4. Click Edit > New, and add the path to the Java bin folder

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
