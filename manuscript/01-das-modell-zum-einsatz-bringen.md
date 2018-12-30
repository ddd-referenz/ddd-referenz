# I. Das Modell zum Einsatz bringen

Domain-driven Design ist ein Ansatz für die Entwicklung komplexer
Software, bei dem wir:

1. Uns auf die [Core Domain](#core-domain) konzentrieren.

2. [Modelle](#model) in einer kreativen Zusammenarbeit von
   Domänen-Praktikern und Software-Praktikern erkunden.

3. Eine [Ubiquitous Language](#ubiquitous-language) in einem
   expliziten [Bounded Context](#bounded-context) sprechen.

Diese Zusammenfassung von DDD in drei Punkten stützt sich auf die 
Definition der Begriffe ab, die in dieser Broschüre definiert sind.

Viele Projekte betreiben Modellierung, ohne am Ende einen echten Nutzen
zu erzielen. Die Muster von DDD stellen erfolgreiche Praktiken aus
Projekten dar, bei denen die Modellierung drastische Vorteile gebracht
hat. Zusammen angewendet stellen sie einen ganz anderen Ansatz für
die Modellierung und Softwareentwicklung vor, der von kleinen Details 
bis hin zur übergreifenden Vision reicht. Strenge Konventionen für die 
Modellierung müssen gegen das freie Erforschen von
Modellen zusammen mit nicht-technischen Personen abgewogen werden.
Taktik und Strategie müssen kombiniert werden, um erfolgreich zu sein 
und DDD befasst sich sowohl mit taktischem als auch mit strategischem
Design.

## Bounded Context {#bounded-context}

*dt.: Begrenzter Kontext*

*Bei jedem großen Projekt sind mehrere Modelle im Spiel.* Sie
entstehen aus vielen Gründen. Zwei Subsysteme bedienen in der Regel
sehr unterschiedliche Benutzergruppen mit unterschiedlichen Aufgaben,
wobei unterschiedliche Modelle sinnvoll sein können. Selbständig
arbeitende Teams können das gleiche Problem durch mangelnde
Kommunikation auf unterschiedliche Weise lösen. Auch können die
benutzten Werkzeuge unterschiedlich sein, so dass Programmcode nicht 
gemeinsam genutzt werden kann.

Mehrere Modelle sind unvermeidlich, aber wenn Code, der auf
verschiedenen Modellen basiert, kombiniert wird, wird Software
fehlerhaft, unzuverlässig und schweirig verständlich. Die Kommunikation
zwischen den Teammitgliedern wird konfus. Oft ist unklar, in
welchem Zusammenhang ein Modell nicht angewendet werden soll.

Ausdrücke aus dem Modell haben, wie jede andere Formulierung auch,
nur im [Kontext](#context) eine Bedeutung.

Daher:

**Definiere explizit den Kontext, in dem ein Modell Anwendung findet.
Lege explizit die Grenzen bezüglich Teamorganisation, Verwendung 
innerhalb bestimmter Teile der Anwendung und
physischen Umsetzungen wie Codebasen und Datenbankschemata fest. Wende
[Continuous Integration](#continuous-integration) an, um
Modellkonzepte und -begriffe innerhalb dieser Grenzen strikt konsistent 
zu halten, lass dich aber nicht von
Problemen außerhalb ablenken oder verwirren. Standardisiere
einen einzigen Entwicklungsprozess innerhalb des Kontextes, der
anderswo nicht verwendet werden muss.**

## Ubiquitous Language {#ubiquitous-language}

*dt.: allgegenwärtige Sprache*

Zuerst schreibst du einen Satz,  
Und dann hackst du ihn klein;  
Dann mische die Stücke und ordne sie so an  
wie sie zufällig gefallen sind:  
Die Reihenfolge der Ausdrücke macht  
überhaupt keinen Unterschied.  

--- Lewis Carroll, "Poeta Fit, Non Nascitur"

Um ein Design zu schaffen, das flexibel und reich an Wissen ist,
bedarf es einer vielseitigen, gemeinsam im Team genutzten Sprache und
lebhaftem Experimentieren mit der Sprache, wie es in
Softwareprojekten selten vorkommt.

Innerhalb eines einzigen [Bounded Context](#bounded-context) kann die
Sprache so
zerbrochen sein, dass sie die Bemühungen um eine anspruchsvolle
Modellierung untergräbt.  Wenn das Modell nur dazu dient,
UML-Diagramme für die Techniker im Team zu erstellen, dann trägt es
nicht zur kreativen Zusammenarbeit, dem Kern von DDD, bei.

Domänenexperten verwenden ihren Fachjargon, während die Techniker im
Team ihre eigene Sprache haben, um die Domäne beim Design
zu diskutieren. Die Terminologie in den täglichen Diskussionen ist von
der im Code verwendeten Terminologie abgetrennt (letztendlich dem
wichtigsten
Produkt eines Softwareprojekts). Und selbst die gleiche
Person verwendet unterschiedliche Sprachen in Wort und Schrift, so
dass die prägnantesten Ausdrücke der Domäne oft in einer flüchtigen
Form entstehen, die nie im Code oder gar schriftlich erfasst wird.

Die Übersetzung stört die Kommunikation und macht das Erarbeiten des
Wissens blutleer.

Doch keiner dieser Dialekte kann eine gemeinsame Sprache werden, weil
keiner alle Bedürfnisse erfüllt.

Domänenexperten sollten gegen Begriffe oder Strukturen protestieren,
die ungeschickt oder unzureichend sind, um das Domänenverständnis zu
vermitteln; Entwickler sollten auf Mehrdeutigkeit oder Inkonsistenz
achten, die das Design stören.

Spielt mit dem Modell, während ihr über das System sprecht. Beschreibt
Szenarien *laut* mit Hilfe der Elemente und Interaktionen aus dem Modell
und kombiniert dabei Konzepte so, wie es das Modell erlaubt. Findet
einfachere Wege, um zu sagen, was ihr sagen wollt, und übertragt diese
neuen Ideen dann wieder zurück in die Diagramme und den Code.

Mit einer [Ubiquitous Language](#ubiquitous-language) ist das Modell
nicht nur ein
Design-Artefakt. Es wird zu einem integralen Bestandteil von allem,
was die Entwickler und Fachexperten gemeinsam tun.

Daher:

**Verwende das Modell als Rückgrat einer Sprache. Verpflichte das Team
dazu,
diese Sprache unermüdlich in der gesamten Kommunikation innerhalb des
Teams und im Code anzuwenden. Verwende in einem [Bounded
Context](#bounded-context) die
gleiche Sprache in Diagrammen, beim Schreiben und insbesondere beim
Sprechen.**

**Berücksichtige, dass eine Änderung der Sprache eine Änderung des
Modells
ist.**

**Löse Schwierigkeiten, indem du mit alternativen Ausdrücken
experimentierst, die alternative Modelle widerspiegeln. Dann
überarbeite den Code und benenne Klassen, Methoden und Module um, so
dass sie
dem neuen Modell entsprechen. Löse Verwirrung über Begriffe in einem
Gespräch auf, und zwar in der Art und Weise, wie wir uns über die
Bedeutung gewöhnlicher Wörter einigen.**

## Continuous Integration {#continuous-integration}

*Sobald ein Bounded Context definiert ist, müssen wir ihn intakt
 halten.*

Wenn mehrere Personen am gleichen [Bounded Context](#bounded-context)
arbeiten, besteht
eine starke Tendenz dazu, dass das Modell fragmentiert wird. Je
größer das
Team, desto größer das Problem, aber schon drei oder vier Personen
können auf ernsthafte Probleme stoßen. Doch die Zerlegung des Systems
in immer kleinere [Bounded Contexts](#bounded-context) führt
letztendlich dazu, das sie
kein ausreichendes Maß an Integration und Kohärenz mehr haben.

Daher:

**Etabliere einen Prozess, bei dem alle Code- und alle andere
  Implementierungsartefakte regelmäßig zusammengeführt werden, und nutze
  automatisierte Tests, um Fragmentierungen schnell zu finden. Wende 
  ständig die [Ubiquitous Language](#ubiquitous-language) an, um
  eine gemeinsame Sicht auf das Modell auszuarbeiten, während sich die
  Konzepte in den Köpfen der verschiedenen beteiligten Personen 
  weiterentwickeln.**

## Model-Driven Design {#model-driven-design}

*dt.: modellgetriebener Entwurf*

*Die enge Verknüpfung des Codes mit einem zugrunde liegenden Modell
gibt dem Code einen Sinn und macht das Modell relevant.*

Wenn das Design oder zumindest ein zentraler Teil davon nicht auf das
Domänenmodell abgebildet werden kann, hat dieses Modell nur einen
geringen
Wert, und die Korrektheit der Software ist fraglich. Gleichzeitig
sind komplexe Abbildungen zwischen Modellen und den Funktionen
des Designs schwer verständlich und in der Praxis nicht
warten, wenn sich das Design ändert. Eine tödliche Kluft
öffnet sich zwischen Analyse und Design, so dass die in den beiden
Aktivitäten gewonnenen Erkenntnisse nicht in die jeweils andere
einfließen.

Leite aus dem Modell die beim Design verwendete Terminologie und die
grundlegende Zuordnung von Verantwortlichkeiten ab. Der Code wird zu
einem Ausdruck des Modells, so dass eine Änderung des Codes eine
Änderung des Modells sein kann. Seine Wirkung muss sich entsprechend
auf den Rest der Projektarbeit auswirken.

Um die Implementierung eng an ein Modell zu binden, sind in der
Regel Softwareentwicklungswerkzeuge und -sprachen erforderlich, die
ein solches Modellierungsparadigma unterstützen, wie beispielsweise die
objekt-orientierte Programmierung.

Daher:

**Entwerfe einen Teil des Softwaresystems so, dass es das
Domänenmodell möglichst genau widerspiegelt, so dass die
Umsetzung offensichtlich ist. Betrachte das Modell immer wieder und
modifiziere es, um es natürlicher in Software zu implementieren, während
wenn du versuchst, einen besseren Einblick in die Domäne zu bekommen.
Erhebe den Anspruch, ein einziges Modell zu finden, das beiden Zwecken
gerecht wird und
zudem eine flüssige [Ubiquitous Language](#ubiquitous-language)
unterstützt.**

## Hands-on Modelers {#hands-on-modelers}

*dt.: Praktizierende Modellierer*

Wenn sich die Personen, die den Code schreiben, nicht für das Modell
verantwortlich fühlen oder nicht verstehen, wie das Modell einer
Anwendung funktionieren soll, dann hat das Modell nichts mit der
Software zu tun.  Wenn Entwickler nicht erkennen, dass Code-Änderungen
das Modell verändern, dann wird ihr Refactoring das Modell eher
schwächen als stärken. Wenn ein Modellierer vom
Implementierungsprozess getrennt ist, gewinnt er oder sie nie ein
Gefühl für
die Restriktionen bei der Implementierung oder verliert sie schnell.
So geht die grundlegende Bedingung des [Model-driven
Designs](#model-driven-design), dass
das Modell eine effektive Implementierung unterstützt und wichtige
Erkenntnisse über die Domain abstrahiert, nahezu verloren und die daraus
resultierenden Modelle werden unpraktisch sein. Schließlich werden die
Kenntnisse und Fähigkeiten erfahrener Designer nicht auf andere
Entwickler übertragen, wenn die Arbeitsteilung die Art der
Zusammenarbeit verhindert, die die Feinheiten der Programmierung eines
modellgetriebenen Designs vermittelt.

Daher:

**Jede technische Person, die am Modell mitwirkt, muss einige Zeit
damit verbringen, am Code zu arbeiten, unabhängig davon, welche
Rolle sie im Projekt vor allem spielt.  Jeder, der für das Ändern von
Codes verantwortlich ist, muss lernen, ein Modell durch den Code
auszudrücken.  Jeder Entwickler muss auf irgendeiner Ebene an der
Diskussion über das Modell beteiligt sein und Kontakt zu
Domänenexperten haben.  Diejenigen, die auf andere Weisen zum Projekt
beitragen, müssen diejenigen, die am Code arbeiten, bewusst in einen
dynamischen Austausch von Ideen zum Modell durch die [Ubiquitous
Language](#ubiquitous-language) einbeziehen.**

## Refactoring Towards Deeper Insight {#refactoring-towards-deeper-insight}

*dt.: Refactoring zum tieferen Verständnis*

Die Verwendung eines bewährten Satzes von Grundbausteinen zusammen mit
einer konsistenten Sprache bringt ein wenig Vernunft in die
Entwicklungsarbeit.  Aber es bleibt eine Herausforderung, tatsächlich
ein prägnantes Modell zu finden, das die subtilen Belange der
Fachexperten aufgreift und ein praktisches Design vorantreiben kann.
Ein Modell, das das Künstliche abstreift und das Wesentliche erfasst,
ist ein tiefgreifendes Modell.  Dadurch sollte die Software 
den Denkweise der Domänenexperten besser entsprechen und besser auf die
Bedürfnisse des Benutzers eingehen.

Traditionell wird Refactoring als Code-Transformation aus technischen
Gründen beschrieben.  Refactoring kann aber auch durch einen
Einblick in die Domäne und eine entsprechende Verfeinerung des Modells
oder dessen Ausdruck im Code motiviert werden.

Anspruchsvolle Domänenmodelle erweisen sich selten als nützlich, außer
wenn sie durch einen iterativen Prozess mit Refactoring entwickelt
werden, einschließlich der engen Einbindung der Domänenexperten mit
Entwicklern, die daran interessiert sind, etwas über die Domäne zu
erfahren.
