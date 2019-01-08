# IV Context Mapping für Strategic Design

### Bounded Context

Der [Bounded Context](#bounded-context) (dt.: begrenzter Kontext)
ist eine Beschreibung
einer Grenze (typischerweise ein Subsystem oder die Arbeit eines
bestimmten Teams), innerhalb derer ein bestimmtes Modell definiert und
anwendbar ist.

### Upstream-Downstream {#upstream-downstream}

Eine Beziehung zwischen zwei Gruppen, in der die Handlungen der
"Upstream"-Gruppe den Projekterfolg der "Downstream"-Gruppe
beeinflussen, während die Handlungen der Downstream-Gruppe die
Upstream-Projekte nicht wesentlich beeinflussen. (Wenn zwei Städte am
gleichen Fluss liegen, wirkt sich die Verschmutzung der upstream (dt.:
flussaufwärts) gelegenen Stadt in erster Linie auf die downstream
gelegene Stadt (dt.: flussabwärts) aus).

Das Upstream-Team kann unabhängig vom Schicksal des Downstream-Teams
erfolgreich sein.

### Mutually Dependent {#mutually-dependent}

Mutually Dependent (dt.: wechselseitig abhängig) beschreibt eine Situation,
in der zwei Softwareentwicklungsprojekte in getrennten Kontexten
beide liefern müssen, damit jedes von beiden als erfolgreich angesehen
werden können. 

Wenn zwei Systeme jeweils auf Informationen oder Funktionen des
anderen angewiesen sind - was wir im Allgemeinen vermeiden würden -
sehen wir natürlich die Projekte, die diese Systeme entwickeln, als
wechselseitig miteinander verflochten.  Es gibt aber auch
wechselseitig abhängige
Projekte, bei denen Systemabhängigkeiten nur in eine Richtung
verlaufen.  Wenn ein System ohne ein bestimmtes abhängiges System und
die Integration mit diesem abhängigen System wenig Wert hat -
vielleicht weil dies der einzige Ort ist, an dem es verwendet wird -
dann führt es zu einem Misserfolg beider Projekte, wenn das abhängige
System nicht ausgeliefert wird.

### Free {#free}

Ein Softwareentwicklungskontext ist free (dt.: frei), wenn die
Ausrichtung, der Erfolg oder das Scheitern der Entwicklungsarbeit in
anderen Kontexten wenig Einfluss auf die Auslieferung dieses Konext
hat.

## Context Map {#context-map}

*dt.: Kontext-Karte*

*Um die Strategie zu planen, benötigen wir eine realistische, groß
angelegte Sicht auf die Modellentwicklung, die sich über unser
gesamtes Projekt und andere, in die wir integrieren, erstreckt.*

Ein einzelner [Bounded Context](#bounded-context) hinterlässt einige
Probleme, wenn
keine globale Sichtweise vorhanden ist.  Der Kontext anderer Modelle
kann noch vage und im Fluss sein.

Leute in anderen Teams sind sich der Grenzen der [Bounded
Contexts](#bounded-context) 
nicht sehr bewusst und nehmen unwissentlich Änderungen vor, die die
Übergänge verwischen oder die Zusammenhänge komplizieren.  Wenn
Verbindungen zwischen verschiedenen Kontexten hergestellt werden
müssen, neigen sie dazu, ineinander zu verlaufen.

Selbst wenn die Grenzen klar sind, stellen Beziehungen zu anderen
Kontexten Einschränkungen für die Art des Modells oder das erreichbare
Änderungstempo 
dar.  Diese Einschränkungen manifestieren
sich in erster Linie durch nicht-technische Kanäle, die manchmal
schwer mit den von ihnen betroffenen Designentscheidungen in
Verbindung zu bringen sind.

Daher:

**Identifiziere jedes Modell, das beim Projekt im Spiel ist und
definiere seinen [Bounded Context](#bounded-context).  Dazu gehören
auch die impliziten 
Modelle von nicht-objekt-orientierten Subsystemen.  Benenne jeden
[Bounded Context](#bounded-context) und mache diese Namen zu einem
Teil der 
[Ubiquitous Language](#ubiquitous-language).**

**Beschreibe  die Berührungspunkte zwischen den Modellen, skizziere
die explizite Übersetzung für jede Art der Kommunikation, hebe alle
Austausch-, Isolations- und Einflussmechanismen hervor.**

**Kartografiere das vorhandene Gelände. Nimm Transformationen erst später
vor.**

Diese Karte kann die Grundlage für eine realistische Design-Strategie sein.

Die Charakterisierung von Beziehungen wird auf den folgenden Seiten
konkretisiert, mit einer Reihe von üblichen Pattern für Beziehungen
zwischen [Bounded Contexts](#bounded-context).

## Partnership {#partnership}

*dt.: Partnerschaft*

*Wenn Teams in zwei Kontexten gemeinsam erfolgreich sind oder
scheitern, entsteht oft eine kooperative Beziehung.*

Eine schlechte Koordination voneinander abhängiger Subsysteme in
getrennten Kontexten führt bei beiden Projekten dazu, dass sie nicht
erfolgreich
liefern können.  Ein wichtiges Feature, das in einem System fehlt,
kann dazu führen, dass das andere System nicht liefern
kann. Schnittstellen, die nicht den Erwartungen der Entwickler des
anderen Subsystems entsprechen, können zum Fehlschlagen der
Integration führen.  Eine gemeinsam vereinbarte Schnittstelle kann
sich als so umständlich erweisen, dass sie die Entwicklung des
Client-Systems verlangsamt, oder so schwer zu implementieren, dass sie
die Entwicklung des Server-Subsystems verlangsamt.  Ein Misserfolg
bringt beide Projekte zum Scheitern.

Daher:

**Wenn ein Fehlschlag bei der Entwicklung in einem der beiden Kontexte
zu einem Misserfolg für beide führen würde, solltest du ein
Partnership zwischen den für die beiden Kontexte
zuständigen Teams
etablieren.  Führe einen Prozess zur koordinierten Planung der
Entwicklung und zum gemeinsamen Managements der Integration ein.**

**Die Teams müssen bei der Entwicklung ihrer Schnittstellen
zusammenarbeiten, um die Bedürfnisse bei der Entwicklung beider
Systeme zu befriedigen. Voneinander abhängige Features sollten so
eingeplant werden, dass sie für das gleiche Release abgeschlossen
werden.**

Es ist in den meisten Fällen nicht notwendig, dass Entwickler das
Modell des anderen Subsystems im Detail verstehen, aber sie müssen
ihre Projektplanung koordinieren.  Wenn die Entwicklung in einem
Kontext auf Hindernisse stößt, ist eine gemeinsame Auseinandersetzung
mit dem Thema erforderlich, um eine schnelle Designlösung zu finden,
die beide Kontexte nicht übermäßig negativ beeinträchtigt.

Außerdem ist ein klarer Prozess zur Steuerung der Integration
erforderlich.  So kann beispielsweise eine spezielle Testsuite
definiert werden, die zeigt, dass die Schnittstelle den Erwartungen
des Client-Systems entspricht und die im Rahmen der [Continuous
Integration](#continuous-integration) auf dem Serversystem ausgeführt
werden kann.

*Partnership ist ein neuer Begriff, der nach dem
blauen Buch aus dem Jahre
2004 entstanden ist.*

## Shared Kernel {#shared-kernel}

*dt.: Gemeinsamer Kern*

*Die gemeinsame Nutzung eines Teils des Modells und des zugehörigen
Codes erzeugen eine sehr enge wechselseitige Abhängigkeit, die der
Designarbeit nutzen 
oder sie behindern kann.*

Wenn die funktionale Integration begrenzt ist, kann der Aufwand für
die [Continuous Integration](#continuous-integration) eines großen
Kontextes für zu hoch
gehalten werden.  Das kann insbesondere der Fall sein, wenn das Team
nicht über die Fähigkeit oder die politische Organisation verfügt,
eine [Continuous Integration](#continuous-integration)
aufrechtzuerhalten, oder wenn ein
einzelnes Team einfach zu groß und zu schwer in den Griff zu bekommen
wäre.  So können stattdessen
getrennte [Bounded Contexts](#bounded-context) definiert und mehrere
Teams gebildet 
werden.

Einmal getrennt, können unkoordinierte Teams, die an eng verwandten
Anwendungen arbeiten, eine Weile gut vorankommen, aber was sie
produzieren, passt vielleicht nicht zusammen.  Selbst
partnerschaftliche Teams können am Ende viel für Übersetzungsschichten
und Änderungen ausgeben, während sie Aufwände verdoppeln und die
Vorteile einer gemeinsamen [Ubiquitous
Language](#ubiquitous-language) verlieren.

Daher:

**Markiere eine explizite Grenze für eine Teilmenge des
Domänenmodells, das die Teams gemeinsam nutzen wollen. Halte diesen
Kern klein.**

**Füge innerhalb dieser Grenze neben dieser Teilmenge des Modells die
Teilmenge des Codes oder des Datenbankdesigns hinzu, die mit diesem
Teil des Modells verbunden ist.  Diese explizit geteilten Artefakte
haben einen besonderen Status und sollte nicht ohne Rücksprache mit
dem anderen Team geändert werden.**

Definiere einen
[Continuous-Integration-Prozess](#continuous-integration), der das
Kernmodell
kompakt hält und stimme die [Ubiquitous
Language](#ubiquitous-language) der Teams 
aufeinander ab.  Integriere ein funktionales System häufig, wenn auch
etwas seltener als das Tempo der [Continuous
Integration](#continuous-integration) innerhalb 
der Teams.

## Customer/Supplier Development {#customer-supplier}

*dt.: Kunde / Zulieferer*

*Wenn sich zwei Teams in einer
[Upstream-Downstream-Beziehung](#upstream-downstream)
befinden, in der das Upstream-Team unabhängig vom Schicksal des
Downstream-Teams erfolgreich sein kann, werden die Bedürfnisse des
Downstream-Teams auf verschiedene Arten mit einer vielen unterschiedlichen
Konsequenzen berücksichtigt.*

Ein Downstream-Team kann hilflos sein, wenn es den
Upstream-Prioritäten ausgeliefert ist.  Währenddessen kann das
Upstream-Team blockiert sein, weil es sich Sorgen macht, dass
Upstream-Systeme gebrochen werden.  Die Probleme des Downstream-Teams
werden auch durch umständliche Verfahren zum Anfordern von Änderungen
mit
komplexen Genehmigungsprozessen nicht geringer.  Und die ungehinderte
Entwicklung des Upstream-Teams wird gestoppt, wenn das Downstream-Team
ein Vetorecht bei Änderungen hat.

Daher:

**Etabliere eine klare
Customer-Supplier-Beziehung zwischen den 
beiden Teams, d.h. Downstream-Prioritäten fließen in die
Upstream-Planung ein. Verhandel und budgetiere Aufgaben für die
Downstream-Anforderungen, so dass jeder die Verpflichtungen und den
Zeitplan versteht.**

Agile Teams können dem Downstream-Team bei der Planung die Rolle des
Kunden gegenüber dem Upstream-Team spielen lassen.  Gemeinsam
entwickelte automatisierte Akzeptanztests können die erwartete
Schnittstelle vom Upstream validieren.  Das Hinzufügen dieser Tests
zur Testsuite des Upstream-Teams, die im Rahmen der [Continuous
Integration](#continuous-integration) durchgeführt wird, befreit das
Upstream-Team bei
Änderungen von der Angst, unbeabsichtigte  Auswirkungen auf Downstream
zu haben.

## Conformist {#conformist}

*dt.: Konformist*

Wenn zwei Entwicklungsteams eine Upstream/Downstream-Beziehung haben,
in der Upstream keine Motivation hat, den Bedürfnisse des
Downstream-Teams zu entsprechen, ist das Downstream-Team hilflos.
Altruismus mag Upstream-Entwickler motivieren, Versprechungen zu
machen, aber sie werden wahrscheinlich nicht erfüllt werden.  Der
Glaube an diese guten Absichten führt dazu, dass das
Downstream-Team auf der Grundlage von Features plant, die nie
verfügbar sein werden.  Das Downstream-Projekt wird sich verzögern,
bis
das Team schließlich lernt, mit dem zu leben, was ihm gegeben wird.
Eine auf die Bedürfnisse des Downstream-Teams zugeschnittene
Schnittstelle ist nicht in Sicht.

Daher:

**Eliminiere die Komplexität der Übersetzung zwischen [Bounded
Contexts](#bounded-context), indem du dich sklavisch an das Modell des
Upstream-Teams
hälst.  Obwohl dies den Stil der Downstream-Designer einengt und
wahrscheinlich nicht das ideale Modell für die Anwendung ergibt,
vereinfacht Konformität die Integration enorm.  Außerdem
wirst du dir
eine [Ubiquitous Language](#ubiquitous-language) mit dem
Upstream-Team teilen.  Upstream
hat das Sagen. Daher ist es gut, die Kommunikation für sie
möglichst einfach zu gestalten.  Altruismus kann ausreichen, um sie
dazu zu bringen, Informationen mit dir zu teilen.**

## Anticorruption-Layer {#anticorruption-layer}

*dt.: Antikorruptionsschicht*

Übersetzungsschichten können einfach, ja sogar elegant sein, wenn es
darum geht, gut gestaltete [Bounded Context](#bounded-context)
kooperativer Teams zu
verbinden.  Aber wenn die Kontrolle oder die Kommunikation nicht
ausreicht, um einen [Shared Kernel](#shared-kernel), eine
[Partnership](#partnership) oder [Customer
/ Supplier](#customer-supplier) zu erreichen, wird die Übersetzung
komplexer.  Die
Übersetzungsschicht nimmt eher einen defensiven Charakter an.

Eine große Schnittstelle mit einem Upstream-System kann am Ende
die Absicht des Downstream-Modells insgesamt überfordern, so
dass das Modell ad hoc an das Modell des anderen Systems angeglichen
wird.  Die Modelle von Altsystemen sind in der Regel schwach (wenn
nicht sogar [Big Balls of Mud](#big-ball-of-mud)), und selbst wenn das
Modell
ausnahmsweise gut gestaltet ist, mag es nicht den Anforderungen des
aktuellen Projekts entsprechen, so dass es unpraktisch wäre,
sich an das Upstream-Modell anzupassen.  Dennoch kann die Integration
für das Downstream-Projekt sehr wertvoll oder sogar erforderlich sein.

Daher:

**Erstelle als Downstream-Client eine Isolationsschicht, um deinem
System die Funktionalität des Upstream-Systems in Form deines eigenen
Domänenmodells zur Verfügung zu stellen.  Diese Schicht spricht mit
dem anderen System über seine bestehende Schnittstelle und erfordert
wenig oder gar keine Änderungen am anderen System.  Intern übersetzt
die Schicht je nach Bedarf in eine oder beide Richtungen zwischen
den beiden Modellen.**

## Open-host Service {#open-host-service}

*dt.: Offener Host*

*Typischerweise definierst du für jeden [Bounded
Context](#bounded-context) eine
Übersetzungsschicht für jede Komponente, in die du integrieren musst
und die außerhalb des Kontextes liegt.  Wenn jede Integration anders
ist, vermeidet dieser Ansatz, eine Übersetzungsschicht für jedes
externe System einzufügen, die Korruption der Modelle mit minimalen
Kosten. Wenn dein Subsystem jedoch stark nachgefragt ist, benötigst
du möglicherweise einen flexibleren Ansatz.*

Wenn ein Subsystem mit vielen anderen integriert werden muss, kann die
Anpassung eines Übersetzers für jede einzelne Integration das Team
dazu bringen sich zu verzetteln.  Es gibt immer mehr zu warten und
immer mehr zu beachten, wenn Änderungen vorgenommen werden.

Daher:

**Definiere ein Protokoll, das den Zugriff auf dein Subsystem als eine
Reihe von [Services](#service) ermöglicht.  Öffne das Protokoll, so dass
alle, die sich mit dir integrieren müssen, das Protokoll nutzen
können.  Verbessere
und erweitere das Protokoll, um neue Integrationsanforderungen zu
erfüllen, es sei denn, ein einzelnes Team hat individuelle
Anforderungen.  Verwende dann einen spezifischen Übersetzer, um das
Protokoll für diesen speziellen Fall zu erweitern, so dass das
gemeinsame Protokoll einfach und kohärent bleibt.**

Damit befindet sich der Anbieter des Service in der Upstream-Position.
Jeder Kunde ist Downstream, und typischerweise sind einige von ihnen
[Conformist](#conformist) und andere bilden [Anticorruption
Layer](#anticorruption-layer).  Ein Kontext
mit einem Open Host Service kann jede Art von Beziehung zu anderen
Kontexten haben, die nicht seine Clients sind.

## Published Language {#published-language}

*dt.: veröffentlichte Sprache*

*Die Übersetzung zwischen den Modellen zweier [Bounded
Contexts](#bounded-context)
erfordert eine gemeinsame Sprache.*

Die direkte Übersetzung in und aus den bestehenden Domänenmodellen
ist möglicherweise keine gute Lösung.  Diese Modelle können übermäßig
komplex oder schlecht aufgeteilt sein. Sie sind wahrscheinlich
undokumentiert.  Wenn man ein solches Modell als Datenaustauschsprache
verwendet, 
wird es schlussendlich eingefroren und kann nicht auf neue
Entwicklungsbedürfnisse reagieren.

Deshalb:

**Verwende eine gut dokumentierte gemeinsame Sprache, die notwendigen
Domäneninformationen als gemeinsames Kommunikationsmedium ausdrückt
und bei Bedarf in diese Sprache und aus dieser Sprache übersetzen
kann.**

Viele Branchen definieren Published Languages
in Form von 
Datenaustauschstandards.  Projektteams entwickeln aber auch ihre
eigenen für den Einsatz in ihrem Unternehmen.

Published Language wird oft mit dem [Open Host
Service](#open-host-service) kombiniert.

## Separate Ways {#separate-ways}

*dt.: Getrennte Wege*

Wir müssen rücksichtslos sein, wenn es um die Definition von
Anforderungen geht.  Wenn zwei Mengen von Funktionalitäten keine
signifikante Beziehung zueinander haben, können sie vollständig
voneinander getrennt werden.

Integration ist immer teuer, und manchmal ist ihr Nutzen gering.

Daher:

**Definiere, dass ein [Bounded Context](#bounded-context) gar keine
Verbindung zu den
anderen hat, so dass Entwickler einfache, spezialisierte Lösungen in
diesem kleinen Bereich finden können.**

## Big Ball of Mud {#big-ball-of-mud}

*dt.: Großer Schlammball*

Wenn wir bestehende Softwaresysteme untersuchen und versuchen zu
verstehen, wie unterschiedliche Modelle innerhalb definierter Grenzen
angewendet werden, finden wir Teile von Systemen, oft große, wo
Modelle gemischt sind und Grenzen inkonsistent sind.

Es ist leicht, sich daran festzubeißen, die Kontextgrenzen
von Modellen in Systemen zu beschreiben, in denen es einfach keine
Grenzen gibt.

Gut definierte Kontextgrenzen entstehen erst durch intellektuelle
Entscheidungen und soziale Kräfte (auch wenn die Personen, die die
Systeme schaffen, sich dieser Ursachen zu dem jeweiligen Zeitpunkt
nicht immer bewusst
waren).  Wenn diese Faktoren fehlen oder verschwinden, vermischen sich
mehrere konzeptuelle Systeme und machen Definitionen und Regeln
mehrdeutig oder widersprüchlich.  Die Systeme werden dazu gebracht, 
nach einer unklaren Logik zu funktionieren, wenn Feature hinzugefügt
werden.  Abhängigkeiten durchziehen die Software.  Ursache und Wirkung
werden immer schwieriger nachvollziehbar.  Schließlich erstarrt die
Software zu einem großen Schlammball.

Big Ball of Mud ist für einige Situationen eigentlich recht
praktisch (wie im Originalartikel von Foote und Yoder beschrieben),
aber er verhindert fast vollständig die Subtilität und Präzision, die
für nützliche Modelle erforderlich ist.

Deshalb:

**Zeichne eine Grenze um das gesamte Durcheinander und bezeichne es
als einen Big Ball of Mud. Versuche nicht, in
diesem Kontext eine
ausgeklügelte Modellierung anzuwenden.  Sei auf der Hut vor der
Tendenz, dass sich solche Systeme in andere Kontexte ausbreiten.**

(siehe
  [Big Ball of Mud von Brian Foote und Joseph Yoder](http://www.laputan.org/mud/mud.html))

*Big Ball of Mud ist ein neuer Begriff, der nach
dem blauen Buch aus dem Jahre 2004 entstanden ist.*
