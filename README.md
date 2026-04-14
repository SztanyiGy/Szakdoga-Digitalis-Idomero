# Szakdoga-Digitális-Időmérő
📌 Leírás

Ez az alkalmazás a felhasználó számítógépes alkalmazáshasználatát figyeli, és rögzíti, hogy mennyi időt tölt különböző programokban.
Célja a digitális eszközhasználat tudatosabbá tétele.

⚙️ Követelmények

A projekt futtatásához az alábbiak szükségesek:

Java 21
IntelliJ IDEA 2025.3.1 (vagy frissebb)
Maven (a projekt függőségeinek kezeléséhez)
Internetkapcsolat a függőségek letöltéséhez

A szükséges függőségek a pom.xml fájlban találhatók, és Maven segítségével automatikusan letöltésre kerülnek.

🚀 Futtatás
1. Klónozás
git clone <repo_link>
2. Projekt megnyitása

Nyisd meg a projektet IntelliJ IDEA-ban.

3. Függőségek letöltése

A projekt megnyitásakor az IntelliJ automatikusan letölti a szükséges artifacteket a pom.xml alapján.
Ha ez nem történik meg, futtasd:

mvn clean install
4. Indítás

A Main osztály futtatásával elindítható az alkalmazás.

🧠 Használat

A program elindítása után automatikusan figyeli az aktív alkalmazásokat, és rögzíti az azokban eltöltött időt.

⚠️ Korlátok
jelenleg csak egy gépen működik
nincs felhő alapú mentés
az alkalmazások felismerése nem minden esetben pontos
