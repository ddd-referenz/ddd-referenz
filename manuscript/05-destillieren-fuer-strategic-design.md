# Destillieren für Strategic Design

Wie kann man sich auf das zentrale Problem konzentrieren und
verhindern, dass man in einem Meer von Nebensächlichkeiten ertrinkt?

Destillation bezeichnet einen Prozess, um die Bestandteile einer
Mischung trennen und so die Essenz in einer Form zu extrahieren, die
sie wertvoller und nützlicher macht.  Ein Modell ist eine Destillation
von Wissen.  Mit jedem [Refactoring Towards Deeper Knowledge](#refactoring-towards-deeper-insight) abstrahieren wir
entscheidende Aspekte des Domänenwissens und der Prioritäten in der
Domäne.  Um auf eine strategische Perspektive zurückzukommen,
beschäftigt sich dieses Kapitel mit Möglichkeiten, die größten
Bestandteile des Modells zu unterscheiden und das Domänenmodell als
Ganzes zu destillieren.

## Core Domain {#core-domain}

*Dt.: Kerndomäne*

In einem großen System gibt es so viele Komponenten, die alle
kompliziert und absolut notwendig für den Erfolg sind, dass die Essenz
des Domänenmodells, der eigentliche Unternehmenswert, unklar sein kann
und dann vernachlässigt werden kann.

Die harte Realität ist, dass nicht alle Teile des Designs gleich
ausgefeilt sein werden.  Es müssen Prioritäten gesetzt werden.  Um das
Domänenmodell zu einem Asset zu machen, muss der kritische Kern dieses
Modells schlank sein und vollständig genutzt werden, um
Anwendungsfunktionalitäten zu erstellen.  Aber die wenigen
hochqualifizierte Entwickler neigen dazu, sich auf die technische
Infrastruktur oder gut definierbare Domänenprobleme zu konzentrieren,
die ohne spezielle Domänenkenntnisse verstanden werden können.

Daher:

**Dampfe das Modell auf das Wesentliche ein.  Definiere eine
Kerndomäne und biete eine Möglichkeit, sie leicht von der großen
Anzahl unterstützender Modelle und Codes zu unterscheiden. Bringe die
wertvollsten und spezialisiertesten Konzepte auf den Punkt. Mache den
Kern klein.

Nutze die besten Talente für die [Core Domain](#core-domain) und
rekrutiere entsprechend.  Investiere genügend Aufwände, um ein
tiefgreifendes Modell zu finden und ein flexibles Design zu
entwickeln, das ausreicht, um die Vision des Systems zu erfüllen.

Rechtfertige die Investition in andere Teile, indem du betrachtest,
wie er den destillierten Kern unterstützt.**

## Generic Subdomains {#generic-subdomains}

*Dt.: Generische Subdomänen*

Einige Teile des Modells erhöhen die Komplexität, ohne Spezialwissen
zu erfassen oder zu vermitteln.  Alles, was nicht relevant ist, macht
die [Core Domain](#core-domain) schwieriger zu erkennen und zu
verstehen.  Das Modell wird blockiert mit allgemeinen Prinzipien, die
jeder kennt oder Details, die zu Spezialitäten gehören, die nicht das
Hauptaugenmerk sind, sondern eine unterstützende Rolle spielen. Doch
wie allgemein auch immer sie sind, diese anderen Elemente sind für das
Funktionieren des Systems und die vollständige Ausprägung des Modells
von wesentlicher Bedeutung.

Daher:

**Identifiziere zusammenhängende Subdomains, die nicht die Motivation
für Ihr Projekt sind.  Berücksichtigen Sie generische Modelle dieser
Subdomains und stellen Sie sie in separate Module.  Hinterlasse keine
Spuren deiner Spezialitäten in ihnen.

Sobald sie getrennt wurden, geben Sie ihrer weiteren Entwicklung eine
niedrigere Priorität als der [Core Domain](#core-domain) und vermeiden
es, Kernentwickler den Aufgaben zuzuordnen (da sie von ihnen wenig
Domänenwissen erhalten).  Erwägen Sie auch Standardlösungen oder
öffentlich verfügbare Modelle für diese [Generic
Subdomains](#generic-subdomains).

## Domain Vision Statement {#domain-vision-statement}

*Dt.: Darstellung der Domänenvision*

Zu Beginn eines Projekts existiert das Modell in der Regel noch gar
nicht, aber seine Entwicklung muss schon fokussiert werden.  In
späteren Entwicklungsstadien muss der Wert des Systems erklärt werden,
ohne dass man dazu das Modells eingehend untersuchen muss. Auch können
sich kritische Aspekte des Domänenmodells über mehrere [Bounded
Context](#bounded-context) erstrecken, aber per Definition können
diese unterschiedlichen Modelle nicht so strukturiert werden, dass sie ihren
gemeinsamen Fokus zeigen.

Daker:

**Schreiben Sie eine kurze Beschreibung (etwa eine Seite) der [Core
Domain](#core-domain)und den Wert, den sie bringen wird, das
"Leistungsversprechen".  Ignoriere Aspekte, die dieses Domänenmodell
nicht von anderen unterscheiden.  Zeige, wie das Domänenmodell
verschiedenen Interessen dient und sie ausgleicht.  Halten das
Statement kurz. Schreibe dieses Statement frühzeitig und überarbeite,
wenn du neue Erkenntnisse gewinnst.**

## Highlighted Core {#highlighted-core}

*Dt.: Hervorgehobener Kern*

*Ein [Domain Vision Statement](#domain-vision-statement) beschreibt
die [Core Domain](#core-domain) grob, aber überlässt die Definition
der spezifischen Elemente des Kernmodells den Ungenauigkeiten einer
individuellen Interpretation.  Ohne ein außergewöhnlich hohes Maß an
Kommunikation im Team hat das [Domain Vision
Statement](#domain-vision-statement) alleine wenig Einfluss.*

Auch wenn die Teammitglieder im Großen und Ganzen wissen, was zur
[Core Domain](#core-domain) gehört, werden verschiedene Personen nicht
immer die gleichen Elemente herausgreifen, und selbst die gleiche
Person wird nicht von einem Tag auf den anderen konsistente Aussagen
dazu machen. Der mentale Aufwand, das Modell ständig zu filtern, um
die wesentlichen Teile zu identifizieren, benötigt die volle
Konzentration, die besser für das Nachdenken über das Design
aufgewendet werden sollte, und erfordert detaillierte Kenntnisse über
das Model.  Die [Core Domain](#core-domain) muss leichter erkennbar
werden.

Signifikante strukturelle Änderungen am Code sind der ideale Weg, um
die [Core Domain](#core-domain) zu identifizieren, aber sie sind nicht
immer kurzfristig praktikabel.  Tatsächlich sind solche großen
Code-Änderungen nur schwer durchführbar, ohne die Sichtweise, die dem
Team fehlt.

Daher (eine Form des [Highlighted Core](#highlighted-core)):

**Schreibe ein sehr kurzes Dokument (drei bis sieben kurze Seiten), das
die [Core Domain](#core-domain) und die primären Interaktionen
zwischen den Kernelementen beschreibt.**

und/oder (als eine weitere Form des [Highlighted Core](#highlighted-core)):

**Markiere die Elemente der [Core Domain](#core-domain) im primären
Repository des Modells, ohne besonders seine Rolle besonders zu
erklären.  Mache es Entwicklern leicht herauszufinden, was im Kern ist
oder nicht.**

Wenn das Destillationsdokument die Grundzüge der Kerndomäne
beschreibt, dann dient es als pragmatischer Indikator für die
Bedeutung einer Modelländerung.  Wenn eine Modell- oder Code-Änderung
Auswirkungen auf das Destillationsdokument hat, muss mit anderen
Teammitgliedern Rücksprache gehalten werden.  Wenn die Änderung
vorgenommen wird, erfordert das eine sofortige Benachrichtigung aller
Teammitglieder und die Veröffentlichung einer neuen Version des
Dokuments. Änderungen außerhalb des Kerns oder an Details, die nicht
im Destillationsdokument enthalten sind, können ohne Rücksprache oder
Benachrichtigung vorgenommen werden und werden von anderen Mitgliedern
im Laufe ihrer Arbeit wahrgenommen.  So haben Entwickler die volle
Unabhängigkeit, die die meisten agilen Prozesse vorschlagen.

*Obwohl das [Domain Vision Statement](#domain-vision-statement) und der
[Highlighted Core](#highlighted-core) informiert und leitet, ändern
sie nicht wirklich das Modell oder den Code selbst.  [Generic
Subdomains](#generic-subdomain) aufzuteilen entfernt tatsächlich
einige störende Elemente.  Als nächstes werden wir uns andere
Möglichkeiten ansehen, das Modell und das Design selbst strukturell zu
ändern, um die [Core Domain](#core-domain) sichtbarer und
überschaubarer zu machen...*

# Cohesive Mechanisms {#cohesive-mechanism}

Berechnungen erreichen manchmal eine Komplexität, die das Design
aufzublähen beginnt.  Das konzeptuelle "Was" wird vom mechanistischen
"Wie" überflutet.  Eine große Anzahl von Methoden, die Algorithmen zur
Lösung des Problems bereitstellen, verdecken die Methoden, die das
Problem ausdrücken.

