Mutation Tests funktionieren nach folgendem Vorgehen: Man nimmt vorhandene Unit Tests und ändert in den Tests alle Operatoren und zwar werden alle Operatoren negiert, wobei aber nicht jeder Operator negiert wird, sondern nur pro Iteration eines Tests einer. Dadurch erreicht man extrem viele Kombinationen und eine extrem lange Laufzeit des Tests. Deshalb eignen sich die Tests gar nicht für die CI-CD-Pipeline, sondern eher für nightly Läufe oder für einen speziellen lokalen Lauf. Außerdem bedürfen Mutation Tests für sinnvolle Ergebnisse ein gewisses Finetuning. Man kann bestimmte Dateien ausschließen
Insgesamt gibt es drei Arten von Mutation Strategien:
- mutate Source Code
- mutate Byte Code
- mutate Schema

Mögliches Tool:
https://stryker-mutator.io/docs/
[pitest.org](pitest.org)

stryker-mutator ermöglicht eine Ausgabe in HTML, die übersichtlich ist und in der man serfen kann.

Mutation Tests sind nicht invasive Tests. Sie sind gut zum Finden von kleinen, fiesen Fehlern. Mutation Tests sind ein gutes Test-Tool zur Ergänzung von anderen Tools wie 
- TDD
- Approval Testing
- Property Based Testing

Vorraussetzung dieses Tools:
- hohe Testabdeckung
- stabile Tests / keine Flaky Tests

Wichtig ist, dass man sich bei einem Mutation Tests immer den Report genau anschaut, um zu sehen, ob ein Testcase sinn macht. Beim Schreiben von neuen UnitTests kann man diese Testklasse mutieren lassen, was ein weiteres Argument für TDD ist. 
TDD und Mutation Tests ergänzen sich an dieser Stelle perfekt.