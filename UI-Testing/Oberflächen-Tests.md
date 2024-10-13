Hier werden mit Oberflächen-Tests die Tests verstanden, welche ein Programm/eine Webseite mit dem Anwender zur Verfügung gestellten Controls/Oberflächenelementen möglich sind.

Es gibt verschiedene Ansätze, wie man diese Tests aufsetzen kann und was man mit diesen Tests testen kann.

## Vorteile
Der Test klickt wie ein echter Anwender. Die grafische Oberfläche wird getestet und es werden Tests mit längeren Workflows möglich. Man kann damit Programme testen, für die die nachträgliche Erstellung von Unit- oder Integrationstests aus Architekturgründen nur schwer möglich ist. Man kann damit fremde Software testen, für die kein Quellcode vorhanden ist.

## Nachteile
Oberflächen-Tests sind nicht sehr zuverlässig. Man muss damit rechnen, dass nur ca. 70 - 80% der Läufe auf onPremise korrekt verlaufen. Bei Oberflächen-Tests von Webseiten kann man damit rechnen, dass annähernd 100% erreicht werden. Win32-Anwendungen sind nur schwer zu automatisieren, weil die einzelnen Controls nur mit Zahlen adressierbar sind.

# Ansatz1 - Alle Tests sind in Unittests aus Funktionen zusammen programmiert
Dieser Ansatz basiert darauf, dass jeder Testfall als Unittest separat programmiert wird und die Testfälle rufen direkt Funktionen auf, welche die UI-Controls ansprechen. 
**Vorteile:** Diese Tests laufen sehr schnell und haben für UI-Tests einen sehr geringen Overhead.
**Nachteile:** Die Tests können sehr schnell sehr unübersichtlich werden. Sie können nur von einem Softwareentwickler gewartet werden. Die Erstellung neuer Tests bedarf immer der Tätigkeit eines Softwareentwicklers. 

# Ansatz2 - Alle Tests werden aus kleinen Codeschnipseln zusammen konfiguriert
Dieser Ansatz basiert darauf, dass mit diesen Tests möglichst fachliche Tests durchgeführt werden sollen, z.B. BDD-Tests. Dafür werden die Tests so in einzelne elementare Abschnitte (Action/Step) unterteilt, dass sie in mehreren Tests an geeigneten Stellen wiederverwendet werden können. Man muss sich dabei einzelnen Testfall immer wie das Untereinanderstapeln von Bauklötzen/Noppenbausteinen vorstellen. 
**Wichtig**: Da die Testfälle immer aus vielen kleinen Codeschnipseln, den Actions/Steps, bestehen, müssen die Codeschnipsel immer das gleiche Interface unterstützen. Man muss sich dabei streng an das [Command Pattern](https://de.wikipedia.org/wiki/Kommando_(Entwurfsmuster)) halten. Jede Action/Step implementiert ein Interface aus einer immer gleichen Anzahl von parameterlosen Methoden, die auch immer die gleiche Aufgaben haben - die wichtigste Methode führt immer diese Action/Step aus. Wenn man Daten in diese Action/Step geben will, muss dieses über Properties der Action/Step implementiert werden. Um einen guten Überblick über die Bibliothek der Actions/Steps zu haben, sollte man sehr auf das Naming achten.

### Vorteile
Der Wissensaufwand zur Erstellung neuer Tests aus vorhandenen Actions/Steps ist sehr gering. Man kann sich voll auf die fachlichen Zusammenhänge konzentrieren. Werteänderungen / Anpassungen vorhandener Testfälle sind relativ leicht. Die einzelnen Actions/Steps sind meistens relativ klein und überschaubar. Nur für die Erstellung von neuen Actions/Steps bzw. Anpassung/Fehlerkorrektur vorhandener Actions/Steps wird ein Softwareentwickler benötigt. Die Actions/Steps sind wieder verwendbar und man kann dadurch relativ schnell neue Tests erstellen.
### Nachteile
Die Tests laufen etwas langsamer als Ansatz1. Der fachliche Entwickler eines Tests muss sich Gedanken machen, wie die einzelnen Actions/Steps geschnitten werden sollen.  Man muss für die Verwaltung der Actions/Steps und zur Ablaufsteuerung einen gewissen Aufwand betreiben.
Mögliche Lösungen für die Ablaufsteuerung sind:
- selbst implementieren mit einer Datenhaltung in XML- oder JSON-Dateien
- Verwenden von [Cucumber](https://de.wikipedia.org/wiki/Cucumber_(Software)) oder ähnlich
- Implementierung mit einer eigenen Software, die die Daten in einer DB oder JSON-/XML-Datei speichert.

### Implementierungsansätze für die Ablaufsteuerung
Die Cucumber-Lösung ist im Online-Bereich vorzuziehen. Für .Net-Lösungen kann man auch sehr einfach mit XML arbeiten, wenn man zur XML-Datei eine XSD-Datei erzeugt, da hiermit sehr einfach zur XML-Datei ein Objektbaum erzeugt werden kann.

# Ansätze zur Adressierung der Oberflächen-Controls
Die einzelnen Elemente der grafischen Oberfläche müssen einzeln adressiert werden, damit man auf sie zugreifen können. Es gibt dazu verschiedene Ansätze, wie man vorgehen kann:
- bei jedem Aufruf wird das Control erneut adressiert
- Anlegen einer Map mit den Controls einer View
- Arbeiten nach dem [[Model-Page-Object]] mit objektorientierten Methoden

## Erneutes Adressieren jedes einzelnen Controls bei Aufruf
Für jeden Aufruf wird das einzelne Control erneut adressiert.
**Vorteile:** Kein unnötiger Code bei einmaliger Verwendung
**Nachteile: ** Sehr schnelle Unübersichtlichkeit und extrem langsame Verwendung bei häufigem Aufruf

## Anlegen einer Map mit den Controls einer View
Für jede View wird eine neue Datei angelegt, welche alle Controls einer View enthalten - egal, wie die grafische Oberfläche strukturiert ist.
**Vorteile:** Sehr einfach zu implementieren
**Nachteile:** Schnell unübersichtlich, wenn es sehr viele Controls auf einer View gibt.

# Wichtige Links für onPremise
https://learn.microsoft.com/de-de/dotnet/framework/ui-automation/ui-automation-fundamentals


# Wichtige Links für Online-Anwendungen
https://www.cypress.io/
https://de.wikipedia.org/wiki/Selenium
https://playwright.dev/