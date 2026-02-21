# Tooling: Build-Automatisierung

### 1. Grundlagen der Software-Automatisierung

   Software-Automatisierung beschreibt das Skripten oder Automatisieren täglicher Aufgaben von Entwicklern und Operatoren.

   • **Ausführungsarten**: Sie kann auf Abruf `On-Demand`, nach Zeitplan `Scheduled, z. B. Nightly Builds` oder ereignisbasiert `Triggered, z. B. bei einem Push ins VCS` erfolgen.
   • **Ziele**: Hauptziele sind die Verbesserung der Produktqualität (durch `automatisierte Tests` und `Audits`), ein schnelleres **Time-to-Market** durch kurze Innovationszyklen und die Minimierung von Risiken (schnelles Finden kaputter Builds).
   • **Vorteile**: Automatisierung dient gleichzeitig als Dokumentation und verhindert Fehler, die bei manueller Arbeit entstehen (z. B. "Auf meinem PC läuft es!").
 
### 2. Die Automatisierungspipeline

   Automatisierung kann in jeder Phase des Softwareprozesses (`Entwicklung`, `Integration`, `QA`, `Betrieb`) implementiert werden.

   • **Feedback-Loop**: Ein Schritt in der Pipeline wird nur ausgeführt, wenn der vorherige erfolgreich war. Bei Fehlern wird der Prozess gestoppt und die Verantwortlichen sofort benachrichtigt.
   ![[Pasted image 20260221102111.png]]
   • **Konzepte*: Wichtige Begriffe in diesem Kontext sind `Continuous Integration (CI)`, `Continuous Delivery (CD)` und `DevOps`. Durch häufige kleine Updates wird das Risiko von Ausfällen und die Komplexität von Fehlerbehebungen reduziert.
   ![[Pasted image 20260221101933.png]]

### 3. Build-Automatisierung

   Build-Automatisierungstools müssen bestimmte Anforderungen erfüllen:
   - Sie sollten ohne manuelle Interaktion laufen, reproduzierbar (gleiche Ergebnisse bei gleicher Ausgangslage) und plattformunabhängig sein.
   - Zudem sollten sie inkrementell arbeiten (nur geänderte Teile neu bauen).
   
Vergleich der `Java-Build-Tools`:
   • `ANT (+ IVY)`: `XML`-basiertes Skripting. Es ist sehr flexibel, hat aber keinen vordefinierten Lebenszyklus, was bei grossen Projekten schnell komplex wird.
   • `Maven`: Setzt auf ein deklaratives Modell `XML` mit einer festen Projektstruktur und einem Standard-Lebenszyklus. Es führte das `Dependency Management` und zentrale Repositories `Maven Central` ein.
   • `Gradle`: Kombiniert die Konzepte von `Maven` mit der Flexibilität von Skripting `Groovy oder Kotlin`. Es nutzt eine `Domain Specific Language (DSL)`, was die Build-Files kürzer und lesbarer macht.

### 4. Fokus Gradle

   Gradle nutzt einen Convention-over-Configuration-Ansatz und ist das Standard-Build-Tool für Android.
   
**Projektstruktur & Setup**
   Mit dem Befehl `gradle init` lässt sich eine Standard-Projektstruktur erstellen.
   
• **Wichtige Dateien**:
   ◦ `build.gradle.kts`: Zentrale Konfigurationsdatei `Build-Definition`.
   ◦ `settings.gradle.kts`: Definiert den Projektnamen und inkludierte Module.
   ◦ Gradle Wrapper `gradlew`: Ermöglicht die Nutzung von Gradle, ohne dass es lokal auf dem System installiert sein muss. Dies garantiert konsistente Versionen im Team.
   ◦ `src/main/java & src/test/java`: Standardverzeichnisse für Quellcode und Tests.

•Konfigurationsbereiche in `build.gradle.kts`
   • `Plugins`: Erweitern die Funktionalität. Das `java-Plugin` stellt Tasks zum Kompilieren und Testen bereit; das `application-Plugin` ermöglicht die Ausführung der Anwendung via `CLI`.
   • `Repositories`: Definieren, woher externe Bibliotheken bezogen werden (z. B. `mavenCentral()`).
   • `Dependencies`: Bibliotheken werden mit einem `Scope` deklariert:
   ◦ `implementation`: Erforderlich zum Kompilieren und Ausführen.
   ◦ `testImplementation`: Nur für Tests erforderlich.
   ◦ `runtimeOnly`: Nur zur Laufzeit erforderlich.
   • `Tasks`: Repräsentieren atomare Arbeitsschritte (z. B. `compileJava`, `test`, `jar`). Sie können voneinander abhängen und bilden einen `Task-Graphen`.

•Versionierung & Tests
   • `Semantic Versioning`: Versionen folgen dem Schema `Major.Minor.Patch`.
   • `Testing`: Gradle sucht automatisch nach `@Test-Annotationen` und generiert `HTML-Reports` der Testergebnisse unter `app/build/reports/tests/test/`.

### 5. Wichtige Gradle-Befehle für die Praxis
   • `./gradlew clean`: Löscht generierte Dateien `Ordner build/`.
   • `./gradlew test`: Führt die `Unit-Tests` aus.
   • `./gradlew run`: Startet die Anwendung `benötigt application-Plugin`.
   • `./gradlew tasks`: Zeigt alle verfügbaren Tasks an.
   • `./gradlew dependencies`: Listet den Abhängigkeitsbaum auf.