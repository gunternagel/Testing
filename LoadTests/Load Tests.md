	Unter Load Tests versteht man Tests zur Performance-Messung vom Backend. Ein Load Test besteht aus den einzelnen Requests sowie deren jeweiligen Payloads gegenüber dem Backend. 

# Erstellung von Load Tests
1. Testcases überlegen, für die Load Tests angelegt werden sollen.
2. Jeder Testcase ist manuell durchzuklicken und dabei müssen alle wichtigen Requests in den Dev-Tools des Browsers genau analysiert werden. Jede Payload des Requests ist für eine jeweilige Nutzdaten-Datei des Requests zu erfassen. Bei allen Results ist der Rückgabewert zu erfassen und die Payload des Results ist auf wichtige, zu übernehmende Werte zu überprüfen.
3. Alle den jeweiligen Test benötigte Daten sind aus den Datenbanken zu kopieren und müssen vor jedem Test eingespielt werden.
4. Die erstellten Load Tests sollten möglichst regelmäßig - am besten bei jedem Build ausgeführt werden.

# Load Test Tools
## [[JMeter]]

## Silk Performer
Für die Test sind die Payloads in JSON-Dateien zu erfassen.
Es gibt eine Sprache, in der man die Logik hinter diesen Tests erstellen kann.
https://www.microfocus.com/documentation/silk-performer/205/en/silkperformer-205-webhelp-en/SILKPERF-92292CEF-INTROSP-CON.html


## Load Runner
- Tests werden gescriptet oder werden über eine UI konfiguriert. Die gescripteten Tests können mit C-Script oder JavaScript angelegt werden.
- Die Tests können mittels Jenkins-Build-Steps in den Jenkins-Build eingefügt werden.
https://www.opentext.com/de-de/produkte/loadrunner-professional
[[LoadRunner]]
