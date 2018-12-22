# II Bestandteil eines modellgetriebenen Designs

Diese Pattern stellen weit verbreitete Best Practices für
objekt-orientiertes Designs im Hinblick auf domain-driven Design dar.
Sie leiten die Entscheidungen zur Präzisierung des Modells und halten
Modell und Implementierung aufeinander abgestimmt, wobei das eine die
Effektivität des anderen verstärkt.  Das sorgfältige Ausarbeiten der
Details der einzelnen Modellelemente gibt den Entwicklern eine solide
Plattform, um Modelle zu erforschen und in enger Abstimmung mit der
Implementierung zu halten.

## Layered Architecture {#layered-architectur}

*Dt.: Geschichte Architektur*

In einem objektorientierten Programm werden Benutzeroberfläche,
Datenbank und anderer unterstützender Code oft direkt in den
Business-Objekte implementiert.  Zusätzliche Geschäftslogik ist in das
Verhalten von UI-Widgets und Datenbankskripten eingebettet.  Dies
geschieht, weil es der einfachste Weg ist, die Dinge schnell zum
Laufen zu bringen.

Wenn der domänenbezogene Code durch eine so große Menge an anderem
Code diffus wird, wird es extrem schwierig, ihn zu identifizieren und
zu verstehen.  Oberflächliche Änderungen an der Benutzeroberfläche
können in Wirklichkeit die Geschäftslogik verändern.  Um eine
Geschäftsregel zu ändern, kann das sorgfältige Prüfung von UI-Code,
Datenbankcode oder anderen Programmelementen erforderlich sein.  Die
Implementierung kohärenter, modellgetriebener Objekte wird
unpraktikabel.  Automatisiertes Testen ist umständlich.  Mit all den
Technologien und der Logik, die in jede einzelne Aktivität involviert
sind, muss ein Programm muss sehr einfach gehalten werden, oder es
wird unmöglich, es zu verstehen.

Daher:

**Isoliere die Umsetzung des Domänenmodells und der Geschäftslogik und
eliminiere alle Abhängigkeiten zur Infrastruktur, zur
Benutzeroberfläche und sogar zu der Anwendungslogik, die keine
Geschäftslogik ist.  Unterteile ein komplexes Programm in Schichten.
Entwickel innerhalb jeder Schicht ein Design, das kohärent ist und nur
von den darunter liegenden Schichten abhängt.  Befolge die üblichen
Architekturmuster, um eine lose Kopplung zu den darüber liegenden
Schichten zu erreichen. Konzentriere den gesamten Code, der sich auf
das Domänenmodell bezieht, in einer Schicht und isoliere es von der
Benutzeroberfläche, der Anwendungscode und dem Infrastrukturcode.  Die
Domänenobjekte können sich auf die Umsetzung des Domänenmodells
konzentrieren und sind frei von der Verantwortlichkeit, sich
anzuzeigen, sich zu speichern, Aufgaben in der Anwendung zu verwalten
usw. .  Dies ermöglicht es dem Modell, sich so zu entwickeln, dass es
reichhaltig genug und klar genug sein kann, um grundlegendes Wissen
über das Geschäft zu erfassen und umzusetzen.**

Das Hauptziel dabei ist die Isolation.  Verwandte Muster, wie
z.B. "Hexagonal Architecture", können ebenso gut oder besser dazu
beitragen, dass unsere Umsetzungen des Domänenmodells Abhängigkeiten
von und Referenzen zu anderen Systembelangen vermeiden.

## Entities {#entity}

*Dt.: Entität, auch bekannt als Reference Objects*

Viele Objekte stellen eine Kontinuität und Identität dar und
durchlaufen einen Lebenszyklus, obwohl sich ihre Attribute ändern
können.

Einige Objekte sind nicht in erster Linie durch ihre Attribute
definiert.  Sie stellen einen Identität dar, die durch die Zeit und
oft durch verschiedene Darstellungen durchläuft.  Manchmal muss ein
solches Objekt mit einem anderen Objekt verglichen werden, obwohl die
Attribute unterschiedlich sind.  Ein Objekt muss von anderen Objekten
unterschieden werden, auch wenn sie die gleichen Eigenschaften haben
können.  Eine falsche Identität kann zu Datenkorruption führen.

Daher:

**Wenn ein Objekt durch seine Identität und nicht durch seine
Attribute unterschieden wird, dann mache das zu einem wichtigen Teil
seiner Definition im Modell.  Halte die Klassendefinition einfach und
konzentriere dich auf die Kontinuität des Lebenszyklus und
Identität.**

**Definiere ein Möglichkeit zur Unterscheidung jedes Objekts
unabhängig von seiner Form oder Geschichte.  Achte auf Anforderungen,
die einen Abgleich von Objekten über Attribute erfordern.  Definiere
eine Operation, die garantiert ein eindeutiges Ergebnis für jedes
Objekt liefert, möglicherweise durch Anhängen eines garantiert
eindeutiges Symbols.  Dieser Identifikationsmechanismus kann von außen
kommen, oder es kann ein beliebiger Identifikator sein, der vom und
für das System erstellt wird, aber es muss der Unterscheidung der
Identität im Modell passen.**

**Das Modell muss definieren, was es bedeutet, dasselbe Ding zu
sein.**

## Value Object {#value-object}

*Dt.: Wertobjekt*

Einige Objekte beschreiben oder berechnen eine Eigenschaft eines Dins.

Viele Objekte haben keine konzeptionelle Identität.

Die Identität von [Entities](#entity) zu verfolgen ist unerlässlich,
aber andere Objekte eine Identität zuzuweisen, kann die Systemleistung
beeinträchtigen, mehr Analysetätigkeiten erwzingen und das Modell
durcheinander bringen, indem alle Objekte gleich aussehen.
Software-Design ist ein ständiger Kampf mit Komplexität.  Wir müssen
differenzieren, damit eine besondere Behandlung nur dann erfolgt, wenn
sie notwendig ist.

Wenn wir diese Kategorie von Objekten jedoch nur als die Abwesenheit
von Identität verstehen, haben wir nicht viel zu unserem
Werkzeugkasten oder Vokabular hinzugefügt.  Tatsächlich haben diese
Objekte eigene Eigenschaften und eine eigene Bedeutung für das Modell.
Dies sind Objekte, die Dinge beschreiben.

Daher:

**Wenn du dich nur um die Attribute und die Logik eines Elements des
Modells kümmern, klassifiziere es als [Value Object](#value-object).
Lass es die Bedeutung der Attribute ausdrücken, die es enthält, und
gib ihm die entsprechende Funktionalität.  Behandel das Wertobjekt als
unveränderlich.  Machen alle Operationen zu [Side-effect-free
Functions](#side-effect-free-functions), die nicht von einem
veränderlichen Zustand abhängig sind.  Gib dem Wertobjekt keine
Identität und vermeide die Designkomplexitäten, die zur Wartung von
Entitäten notwendig sind.**

## Domain Event {#domain-event}

*Dt.: Domänen-Ereignis*

Etwas ist passiert, was für Domänen-Experten wichtig ist.

Eine {Entity}(#entity) ist dafür verantwortlich, ihren Zustand und die
Regeln für ihren Lebenszyklus zu erfassen.  Aber wenn man die
tatsächlichen Ursachen für die Änderung des Zustands kennen muss, ist
das in der Regel nicht explizit in der Entity abgelegt, und es kann
schwierig sein zu erklären, wie das System in den Zustand gekommen
ist, in dem es ist.  Audit-Trails können eine Nachverfolgung
ermöglichen, sind aber in der Regel nicht dazu geeignet, für die Logik
des Programms selbst verwendet zu werden.  Änderungshistorien von
[Entities](#entity) können den Zugriff auf frühere Zustände
ermöglichen, ignorieren aber die Bedeutung dieser Änderungen, so dass
jede Manipulation der Informationen prozedural ist und oft aus der
Domänenebene herausgedrängt wird.

In verteilten Systemen entsteht ein anderer, wenn auch verwandter
Themenkomplex.  Der Zustand eines verteilten Systems kann nicht immer
vollständig konsistent gehalten werden.  Wir halten die Aggregate
intern jederzeit konsistent, während wir andere Änderungen asynchron
vornehmen.  Da sich Änderungen über die Knoten eines Netzwerks
ausbreiten, kann es schwierig sein, mehrere Updates auszuführen, die
nicht in der richtigen Reihenfolge oder aus verschiedenen Quellen
kommen.

Daher:

**Modelliere Informationen über die Aktivität in der Domäne als
eine Reihe von diskreten Ereignissen.  Stelle jedes Ereignis als
Domänenobjekt dar.  Diese unterscheiden sich von Systemereignissen,
die die Aktivität innerhalb der Software selbst widerspiegeln, obwohl
oft ein Systemereignis mit einem Domänenereignis verbunden ist,
entweder als Teil einer Reaktion auf das Domänenereignis oder als
Möglichkeit, Informationen über das Domänenereignis in das System zu
übertragen.**

**Ein [Domain Event](#domain-event) ist ein vollwertiger Teil des
Domänenmodells, eine Darstellung von etwas, das in der Domäne passiert
ist.  Ignoriere irrelevante Domänenaktivitäten, während du die
Ereignisse explizit festlegst, die Domänen-Experten überwachen oder
bei denen sie benachrichtigt werden möchten oder die mit
Zustandsänderungen in den anderen Modellobjekten verbunden sind, .**

In einem verteilten System kann der Zustand einer [Entity](#entity)
aus den [Domain Events](#domain-event) abgeleitet werden, die einem
bestimmten Knoten derzeit bekannt sind, was ein kohärentes Modell
ermöglicht, wenn keine vollständigen Informationen über das System als
Ganzes vorliegen.

[Doman Events](#domain-event) sind normalerweise unveränderlich, da
sie eine Aufzeichnung von etwas in der Vergangenheit sind.  Zusätzlich
zu einer Beschreibung des Ereignisses enthält ein Domänenereignis
typischerweise einen Zeitstempel für den Zeitpunkt des Auftretens des
Ereignisses und die Identität der an dem Ereignis beteiligten
[Entities](#entity).  Außerdem hat ein Domänenereignis oft einen
separaten Zeitstempel, der angibt, wann das Ereignis in das System
eingegeben wurde und die Identität der Person, die es eingegeben hat.
Wenn das nützlich ist, kann eine Identität für das Domänenereignis auf
Basis einiger dieser Eigenschaften definiert werden.  Wenn dann also
beispielsweise zwei Instanzen desselben [Domain Events](#domain-event)
an einem Knoten ankommen, können sie als das gleich Ereigniss erkannt
werden.

*[Domain Event](#domain-event) ist ein neuer Begriff, der nach dem
blauen Buch aus dem Jahre 2004 entstanden ist.*

## Services {#service}

*Dt.: Dienste*

Manchmal ist es einfach kein Ding.

Einige Konzepte aus der Domäne können nicht geeignet als Objekte
modelliert werden. Die Zwang, dass die erforderliche
Domänenfunktionalität in die Verantwortung einer [Entity](#entity)
oder eines [Value Objects](#value-object) fällt, verzerrt entweder die
Definition eines modellbasierten Objekts oder fügt bedeutungslose
künstliche Objekte hinzu.

Daher:

**Wenn ein wichtiger Prozess oder eine signifikante Transformation in
der Domäne nicht in der natürlichen Verantwortung einer
[Entity](#entity) oder eines [Value Objects](#value-object) liegt,
füge dem Modell eine Operation als eigenständige Schnittstelle hinzu,
die als [Service](#service) deklariert ist.  Definiere einen
Servicevertrag, eine Reihe von [Assertions](#assertion) über
Interaktionen mit dem [Service](#service).  Geben Sie diese
[Assertions](#assertion) in der [Ubiquituous
Language](#ubiquituous-language) eines bestimmten [Bounded
Context](#bounded-context) an.  Gib dem [Service](#service) einen
Namen, der auch Teil der [Ubiquituous Language](#ubiquituous-language)
wird.**

## Modules {#module}

*Dt.: Module, auch bekannt als Packages*

Jeder verwendet [Modules](#module), aber nur wenige behandeln sie als
vollwertigen Teil des Modells.  Code wird in alle möglichen Kategorien
unterteilt, von Aspekten der technischen Architektur bis hin zu den
Aufgaben der Entwickler. Selbst Entwickler, die viel refactorn,
begnügen sich oft mit den Modulen, die frühzeitig im Projekt
konzipiert wurden.

Erklärungen von Kopplung und Kohäsion lassen diese Begriffe
tendenziell wie technische Metriken wirken, die mechanisch anhand der
Verteilungen von Assoziationen und Interaktionen beurteilt werden.
Dabei geht es nicht nur um die Aufteilung von Code in Module, sondern
auch um Konzepte.  Es gibt eine Grenze, an wie viele Dinge eine Person
auf einmal denken kann (daher niedrige Kopplung).  Inkohärente
Fragmente von Ideen sind so schwer zu verstehen wie eine
undifferenzierte Ideensuppe (daher hohe Kohäsion).

Daher:

**Wähle Module, die die Geschichte des Systems erzählen und einen
zusammenhängenden Satz von Konzepten enthalten.  Gib den Modulen
Namen, die Teil der [Ubiquituous Language](#ubiquituous-language)
werden.  Module sind Teil des Modells und ihre Namen sollten den
Einblick in die Domäne widerspiegeln.**

**Dies führt oft zu einer geringen Kopplung zwischen den Modulen,
außer wenn man nicht nach Wegen sucht, um das Modell zu ändern und so
die Konzepte zu entwirren, oder nach einem übergreifendem Konzept, das
die Grundlage für ein Modul sein kann, das die Elemente sinnvoll
zusammenbringen würde.  Suchen Sie eine niedrige Kopplung im Sinne von
Konzepten, die unabhängig voneinander verstanden und begründet werden
können.  Verfeinern Sie das Modell, bis es nach
High-Level-Domänenkonzepten partitioniert ist und auch der Code
entsprechend entkoppelt ist.**

## Aggregates {#aggregate}

Es ist schwierig, die Konsistenz von Änderungen an Objekten in einem
Modell mit komplexen Assoziationen zu gewährleisten.  Objekte sollen
ihren eigenen internen konsistenten Zustand beibehalten, können aber
bei Änderungen an anderen Objekten, die konzeptionell Bestandteile
dieser Objekte sind, übergangen werden. Vorsichtige
Datenbank-Sperrschemata führen dazu, dass sich mehrere Benutzer
sinnlos gegenseitig stören, und können ein System unbrauchbar machen.
Ähnliche Probleme entstehen bei der Verteilung von Objekten auf
mehrere Server, oder beim Entwurf asynchroner Transaktionen.

Deshalb:

**Gruppiere die [Entities](#entity) und [Value Objects)(#value-object)
zu [Aggregates](#aggregate) und definiere Grenzen um diese herum.
Wähle eine [Entity](#entity) als Wurzel jedes Aggregats und erlaube
externen Objekten, nur Referenzen auf die Wurzel zu halten. Referenzen
auf interne Elemente werden nur für die Verwendung innerhalb einer
einzigen Operation ausgegeben.  Definiere Eigenschaften und
Invarianten für das Aggregat als Ganzes und übertrage die
Verantwortung für die Durchsetzung auf die Wurzel. oder einen bestimmten
Mechanismus im Framework.**

Verwende die gleichen Aggregate-Grenzen für die Steuerung von
Transaktionen und Verteilung-

Wende innerhalb der Grenze eines [Aggregates](#aggregate) die
Konsistenzregeln synchron an. Über Grenzen hinweg können Updates
asynchron behandelt werden.

Halte das gesamte Aggregat auf einem Server.  Erlaube die Verteilung
verschiedener Aggregate auf die Knoten.

Wenn diese Designentscheidungen nicht gut von den Grenzen der
[Aggregates](#aggregate) geleitet werden, überdenke das Modell.
Deutet das Szenario in der Domäne auf eine wichtige neue Erkenntnis
hin?  Solche Änderungen verbessern oft die Aussagekraft und
Flexibilität des Modells sowie die Lösung der Transaktions- und
Verteilungsfragen.

## Repositories {#repository}

*Dt.: Repsitory*

*Zugriff auf Aggregate durch Anfragen, die in der [Ubiquituous
Language](#ubiquituous-language) ausgedrückt sind.*

Die Verbreitung von übergreifenden Assoziationen, die nur dazu dienen,
Dinge zu finden, bringen das Modell durcheinandner.  In ausgereiften
Modellen drücken Abfragen oft Domänenkonzepte aus.  Dennoch können
Abfragen zu Problemen führen.

Die schiere technische Komplexität bei der Anwendung der meisten
Datenbankzugriffsinfrastrukturen beeinträchtigt schnell den Client-Code,
was Entwickler dazu bringt, die Domänenebene zu reduzieren, was das
Modell irrelevant macht.

Ein Query-Framework kann den größten Teil dieser technischen
Komplexität kapseln, so dass Entwickler genau die Daten, die sie
benötigen, automatisiert oder deklarativ aus der Datenbank beziehen
können, aber das löst nur einen Teil des Problems.

Uneingeschränkte Abfragen können bestimmte Felder aus Objekten
auslesen, die Einkapselung durchbrechen oder bestimmte Objekte aus dem
Inneren eines [Aggregats](#aggregate) instanziieren, die
Aggregatwurzel umgehen und es diesen Objekten unmöglich machen, die
Regeln des Domänenmodells durchzusetzen. Die Domänenlogik verlagert
sich in Abfragen und Code der Anwendungsschicht, und die
[Entities](#entity) und [Value Objects](#value-object) werden zu
reinen Datencontainern.

Daher:

**Erstelle für jeden Aggregattyp, der global zugegriffen werden muss ,
einen Dienst, der die Illusion einer Sammlung aller Objekte des
Wurzeltyps dieses Aggregats vermitteln kann.  Setze den Zugriff über
eine bekannte globale Schnittstelle um.  Stelle Methoden zum
Hinzufügen und Entfernen von Objekten bereit, die das tatsächliche
Einfügen oder Entfernen von Daten im den Datenspeicher kapseln.  Biete
Methoden zur Auswahl von Objekten nach Kriterien an, die für
Domänen-Experten von Bedeutung sind.  Liefere vollständig
instanziierte Objekte oder Sammlungen von Objekten zurück, deren
Attributwerte den Kriterien entsprechen, wodurch die eigentliche
Speicher- und Abfragetechnologie gekapselt wird, oder gibt Proxies
zurück, die die Illusion von vollständig instanziierten Aggregaten
vermitteln, aber die Daten lazy nachladen.  Stelle
[Repositories}(#repository) nur für die Wurzeln der Aggregates bereit,
die tatsächlich direkten Zugriff benötigen.  Halte die Anwendungslogik
auf das Modell fokussier tund delegiere die gesamte Speicherung der
Objekte und den Zugriff auf die Objekte zu den
[Repositories](#repository).**

## Factories {#factory}

*Dt.: Fabriken*

Wenn die Erstellung eines gesamten, intern konsistenten
[Aggregates](#aggregate) oder eines großen [Value
Objects](#value-object) kompliziert wird oder zu viel von der internen
Struktur enthüllt, bieten [Factories](#factory) eine Kapselung.

Das Erzeugen eines Objekts kann ein wichtiger Vorgang an sich sein,
aber komplexe Operationen zumm Zusammenbauen eines Objekts passen
nicht in die Verantwortung der erstellten Objekte.  Die Kombination
dieser Verantwortlichkeiten kann zu schwer verständlichen Designs
führen.  Indem man den Client dazu bringt, das Objekt direkt zu
erzeugen, durchbricht man die Einkapselung des erzeugten Objekts oder
[Aggregates](#aggregate) und koppelt den Client zu stark  mit der
Implementierung des erstellten Objekts.

Daher:

**Verlagere die Verantwortung für das Erstellen von Instanzen
komplexer Objekte und [Aggregates](#aggregate) auf ein separates
Objekt, das selbst keine Verantwortung im Domänenmodell hat, aber
dennoch Teil des Domänendesigns ist.  Stelle eine Schnittstelle zur
Verfügung, die alle komplexen Erzeugungsmöglichkeiten kapselt und die
es nicht erfordert, dass der Client Referenzen auf die konkreten
Klassen der zu instanziierenden Objekte hat.  Erstelle ein ganzes
[Aggregat](#aggregate) als ein Stück und erzwinge seine Invarianten.
Erstelle ein komplexes [Value Object](#value-object) am Stück,
eventuell nach der Zusammenbauen der Elemente mit einem Builder.**
