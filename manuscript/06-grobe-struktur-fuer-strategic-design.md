# VI Grobe Struktur für Strategic Design

Wenn in einem großen System ein übergreifendes Prinzip fehlt, mit dem
Elemente in Bezug auf ihre Rolle anhand für das gesamte Design gültigen
Pattern interpretiert werden können, dann können Entwickler den Wald
vor den Bäumen nicht sehen. Wir müssen in der Lage sein, die Rolle
eines einzelnen Teils im Ganzen zu verstehen, ohne uns mit den Details
des Ganzen zu befassen.

Eine "grobe Struktur" ist eine Sprache, mit der man das System im
Großen diskutieren und verstehen kann.  Ein Satz von übergeordneten
Konzepten oder Regeln oder beidem legt ein Pattern für das Design des
ganzen Systems fest.  Dieses Gestaltungssprinzip kann sowohl das
Design als auch das Verständnis fördern.  Es hilft, selbständige
Arbeiten zu koordinieren, denn es gibt ein gemeinsames Konzept für das
Gesamtbildes, nämlich wie die Rollen der verschiedenen Teile das Ganze
prägen.

Daher:

**Entwickel ein Pattern von Regeln oder Rollen und Beziehungen, das
das gesamte System umfasst und ein gewisses Verständnis der Position
jedes Teils im Ganzen ermöglicht, auch ohne detaillierte Kenntnis der
Verantwortung des Teils.**

## Evolving Order {#evolving-order}

*Dt.: Sich entwickelnde Ordnung*

Design ohne Regeln bringt Systeme hervor, die niemand als Ganzes
verstehen kann und die sehr schwer zu warten sind.  Aber Architekturen
können ein Projekt durch die ursprünglichen Annahmen für das Design zu
sehr einschränken und den Entwicklern/Designern der einzelnen Teile
der Anwendung zu viel Macht entziehen.  Entwickler werden die
Entwickler die Anwendung künstlich vereinfachen, um sie an die
geforderte Struktur anzupassen, oder sie werden die Architektur
untergraben und haben überhaupt keine Struktur, was die Probleme der
unkoordinierten Entwicklung wieder aufwirft.

Daher:

**Sorge dafür, dass sich diese konzeptionelle grobe Struktur mit der
Anwendung weiterentwickelt und sich dabei möglicherweise in eine ganz
andere Struktur verwandelt.  Beschränke die detaillierten Design- und
Modellentscheidungen nicht zu sehr, die mit Wissen über die Details
getroffen werden müssen.**

**Eine grobe Struktur sollte angewendet werden, wenn eine Struktur
gefunden werden kann, die das System wesentlich klarer macht, ohne
dabei widernatürliche Einschränkungen bei der Modellentwicklung zu
erzwingen.  Da eine schlecht passende Struktur schlechter ist als
keine, ist es am besten, nicht auf Vollständigkeit zu achten, sondern
eine minimale Menge zu finden, die die aufgetretenen Probleme löst.
Weniger ist mehr.**

**Was folgt, ist eine Reihe von vier speziellen Mustern für die grobe
Struktur, die bei einigen Projekten entstehen und für diese Art von
Pattern repräsentativ sind.**

## System Metaphor {#system-metaphor}

*Dt.: System-Metapher*

Metaphorisches Denken ist in der Softwareentwicklung weit verbreitet,
insbesondere bei Modellen.  Aber die Extreme-Programming-Praktik der
"Metapher" ist mittlerweile zu einer besonderen Art geworden, eine
Metapher zu nutzen, um Ordnung in die Entwicklung eines ganzen Systems
zu bringen.

Software-Designs sind in der Regel sehr abstrakt und schwer zu
verstehen. Sowohl Entwickler als auch Benutzer benötigen konkrete
Möglichkeiten, das System zu verstehen und eine gemeinsame Sichtweise
auf das Gesamtsystem zu entwickeln.

Deshalb:

**Wenn eine konkrete Analogie zum System entsteht, die die Phantasie
der Teammitglieder einfängt und das Denken in eine nützliche Richtung
zu lenken scheint, nehmen Sie es als grobe Struktur an.  Organisiere
das Design um diese Metapher herum und nimm es in die [Ubiquituous
Language](#ubiquituous-language).  Die System-Metapher sollte sowohl
die Kommunikation über das System erleichtern als auch die Entwicklung
des Systems leiten.  Dies erhöht die Konsistenz in verschiedenen
Teilen des Systems, möglicherweise sogar über verschiedene [Bounded
Contexts](#bounded-context) hinweg.  Aber da alle Metaphern ungenau
sind, überprüfe die Metapher ständig auf Übertreibungen oder
Ungeeignetheit und sei bereit, sie fallen zu lassen, wenn sie dir im
Weg steht.**

## Responsibility Layer {#responsibility-layer}

*Dt.: Schichten nach Zuständigkeiten*

Bei objekt-orientierten Design werden den einzelnen Objekten kleine
Mengen zusammenhängender Zuständigkeiten zugewiesen.  Das Design nach
Zuständigkeiten betrifft auch größere Einheiten.

Wenn jedes einzelne Objekt manuell zugewiesene Verantwortlichkeiten
hat, dann gibt es keine Richtlinien, keine Einheitlichkeit und keine
Möglichkeiten, große Teile der Domäne zusammen zu bearbeiten.  Um
einem großen Modell Zusammenhalt zu verleihen, ist es sinnvoll, der
Zuweisung von Verantwortlichkeiten eine gewisse Struktur aufzuerlegen.

Daher:

**Betrachte die konzeptionellen Abhängigkeiten im Modell und die
unterschiedlichen Änderungsgeschwindigkeiten und -quellen der
verschiedenen Teile der Domäne.  Wenn du natürliche Schichten in der
Domäne identifizierst, dann entwerfe sie als grobe und abstrakte
Verantwortlichkeiten.  Diese Verantwortlichkeiten sollten eine
Geschichte über den Zweck und das Design deines Systems auf grober
Ebene erzählen.  Refactoriere das Modell so, dass die
Verantwortlichkeiten der einzelnen Domänenobjekte,
[Aggregate](#aggregate) und Module genau in die Verantwortung einer
Schicht passen.**

## Knowledge Level {#knowledge-level}

*Dt.: Wissensebene*

*Eine Gruppe von Objekten, die beschreiben, wie sich eine andere
Gruppe von Objekten verhalten soll.*

In einer Anwendung, in der die Rollen und Beziehungen zwischen den
Einheiten in verschiedenen Situationen unterschiedlich sind, kann die
Komplexität explodieren. Weder ganz allgemeine noch sehr individuelle
Modelle erfüllen die Bedürfnisse der Anwender.  Am Ende haben Objekte
Referenzen auf andere Typen, um eine Vielzahl von Fällen abzudecken,
oder mit Attributen, die in verschiedenen Situationen unterschiedlich
verwendet werden.  Klassen, die die gleichen Daten und das gleiche
Verhalten haben, können kopiert werden, nur um unterschiedliche Regeln
bei der Zusammensetzung der Objekte zu berücksichtigen.

Daher:

**Erstellen eine eigene Gruppe von Objekten, welche die Struktur und
das Verhalten des Basismodells beschreiben und einschränken können.
Halte diese Belange als zwei "Ebenen" getrennt: eine sehr
konkrete, die andere spiegelt Regeln und Wissen wider, die ein
Benutzer oder Superuser anpassen kann.

(siehe Fowler, M. 1997.  Analysis Patterns: Reusable Object Models,
Addison-Wesley.)

## Pluggable Component Framework {#pluggable-knowledge-framework}

*Dt.: Steckbares Komponentent-Framework*

Gute Möglichkeiten ergeben sich aus einem sehr ausgereiften Modell,
das tief und destilliert ist. Ein [Pluggable Component
Framework](#pluggable-knowledge-framework) kommt in der Regel erst ins
Spiel, wenn bereits einige Anwendungen in der gleichen Domäne
implementiert wurden.

Wenn eine Vielzahl von Anwendungen zusammenarbeiten müssen, die alle
auf den gleichen Abstraktionen basieren, aber unabhängig voneinander
konzipiert sind, schränken Übersetzungen zwischen mehreren [Bounded
Contexts](#bounded-context) die Integration ein.  Ein [Shared
Kernel](#shared-kerbnel) ist nicht realisierbar für Teams, die nicht
eng zusammenarbeiten.  Doppelte Arbeit und Fragmentierung erhöhen die
Kosten für Entwicklung und Installation, und die Interoperabilität
wird sehr schwierig.

Daher:

**Destilliere einen abstrakten Kern von Schnittstellen und
Interaktionen und entwickel ein Framework, das es ermöglicht,
verschiedene Implementierungen dieser Schnittstellen zu ersetzen.
Ebenso solltest du jeder Anwendung erlauben, diese Komponenten zu
verwenden, solange sie ausschließlich über die Schnittstellen des
abstrakten Kerns arbeitet.**
