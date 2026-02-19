Tooling – Build Automation
1. Einordnung & Motivation
   Was ist Software Automation?

Software Automation bezeichnet das Automatisieren wiederkehrender Tätigkeiten im Software-Entwicklungsprozess, z. B.:

Bauen (Build)

Testen

Integrieren

Deployen

Automatisierung kann:

On-Demand (manuell per Befehl),

zeitgesteuert (z. B. Nightly Builds),

ereignisgesteuert (z. B. bei Git-Commit) erfolgen.

Warum ist Automatisierung wichtig?

Manuelle Builds sind fehleranfällig und unzuverlässig:

Unterschiede zwischen Entwicklerumgebungen („läuft nur bei mir“)

Fehlende oder inkonsistente Tests

Unklare Abhängigkeiten und Build-Zustände

Nicht reproduzierbare Ergebnisse

👉 Automation ist gleichzeitig Dokumentation des Build-Prozesses.

2. Ziele von Build Automation
   Hauptziele

Höhere Produktqualität

Automatisierte Tests

Automatisierte Code-Checks

Nachvollziehbare Build-Historie

Schnellere Auslieferung (Time-to-Market)

Schnellere Feedback-Zyklen

Kürzere Innovationszyklen

Risikominimierung

Frühes Erkennen fehlerhafter Builds

Transparenter Projektstatus

Geringere Abhängigkeit von einzelnen Personen

Release-Strategie

Häufige, kleine Releases reduzieren das Risiko:

Weniger Code pro Änderung

Schnellere Bugfixes

Geringere Ausfallzeiten

📌 Bildempfehlung:
Diagramm „Reduce risk by releasing often“ (Vergleich große Releases vs. Continuous Releases, Folie ~6)

3. Software Automation Pipeline
   Grundidee

Automatisierung kann in allen Phasen stattfinden:

Development

Integration

QA

Operation

Ein Schritt wird nur fortgesetzt, wenn Tests erfolgreich sind.
Bei Fehlern:

Prozess stoppt

Verantwortliche werden informiert

Fix → erneuter Durchlauf

👉 Ergebnis: Feedback-Loop

📌 Bildempfehlung:
Pipeline-Diagramm mit Phasen & Feedback-Loops (Folie ~7–8)

Einordnung wichtiger Begriffe

Build Automation: Automatisches Kompilieren & Testen

Continuous Integration (CI): Automatisches Integrieren & Testen bei Änderungen

Continuous Delivery (CD): Software jederzeit auslieferbar

Continuous Deployment: Automatische Auslieferung in Produktion

DevOps: Zusammenarbeit von Entwicklung & Betrieb

4. Anforderungen an Build-Automation-Tools

Ein Build-Tool sollte:

Automatisiert sein (keine manuellen Schritte)

Reproduzierbar & konsistent arbeiten

Inkrementell sein (nur Geändertes neu bauen)

Plattformunabhängig funktionieren

Nahtlos integrierbar sein (lokal & CI-Server)

5. Java Build Tools – Überblick
   ANT

XML-basiert

Sehr flexibel

Keine vordefinierte Struktur

Wird bei großen Projekten schnell komplex

Maven

Deklarative Konfiguration (POM)

Fester Build-Lifecycle

Zentrales Dependency-Management

Viele Plugins, aber schwer zu erweitern

Gradle

Kombiniert Maven-Konzepte mit Skripting (Groovy/Kotlin)

DSL (Domain Specific Language)

Weniger Boilerplate

Sehr flexibel durch Plugins

Standard-Tool für Android

📌 Bildempfehlung:
Vergleichsfolie ANT / Maven / Gradle (Code-Beispiele nebeneinander, Folie ~11–12)

6. Gradle – Grundkonzepte
   Ziel

Ein einzelner Befehl soll alles erledigen:

gradle test


Dabei passiert automatisch:

Abhängigkeiten herunterladen

Code & Tests kompilieren

Unit-Tests ausführen

Tasks

Ein Task = eine atomare Arbeitseinheit

Tasks können voneinander abhängen

Beispiel: build → test → compileJava

📌 Bildempfehlung:
Task-Graph (Abhängigkeiten zwischen Tasks, Folie ~19)

7. Projektstart mit Gradle
   Initialisierung
   gradle init


Gradle:

erstellt Projektstruktur

nutzt Convention over Configuration

erzeugt Beispielcode & Tests

legt Gradle Wrapper an

Wichtige erzeugte Dateien

build.gradle.kts – Build-Konfiguration

settings.gradle.kts – Projektdefinition

gradlew / gradlew.bat – Gradle Wrapper

app/src/main/java – Produktivcode

app/src/test/java – Tests

.gradle/, build/ → nicht ins Git committen

8. Gradle Konfiguration
   Plugins

java → Kompilieren, Testen, JAR-Erstellung

application → ausführbare CLI-App (run-Task)

Dependencies

Abhängigkeiten werden aus Repositories (z. B. Maven Central) geladen:

dependencies {
implementation("...")
testImplementation("...")
}


Scopes:

implementation

runtimeOnly

testImplementation

testRuntimeOnly

Versionsschema

Semantic Versioning:

Major – inkompatible Änderungen

Minor – Erweiterungen

Patch – Bugfixes

⚠️ Versionsbereiche nur mit Vorsicht verwenden.

📌 Bildempfehlung:
Screenshot mvnrepository + Versionsauswahl (Folie ~26–27)

9. Tests & Reports

Tests werden in src/test/java gesucht

Annotation @Test

Ergebnisse als HTML-Report:

app/build/reports/tests/test/

10. Cleanup & Gradle Wrapper

Gradle arbeitet inkrementell

clean entfernt generierte Artefakte

Wrapper stellt sicher:

gleiche Gradle-Version für alle

keine lokale Installation nötig

./gradlew test
./gradlew clean

11. Typische Gradle-Befehle
    Befehl	Zweck
    gradlew tasks	verfügbare Tasks anzeigen
    gradlew dependencies	Abhängigkeiten anzeigen
    gradlew projects	Module anzeigen
    gradlew test	Tests ausführen
    gradlew run	Anwendung starten
    gradlew clean	Build-Artefakte löschen
12. Fazit

Build Automation:

erhöht Qualität & Stabilität

reduziert Risiken

beschleunigt Entwicklung

ist Grundlage für CI/CD & DevOps

Gradle ist ein modernes, flexibles Build-Tool, das sich besonders gut für Java-Projekte eignet und sowohl lokal als auch in CI-Pipelines eingesetzt wird.