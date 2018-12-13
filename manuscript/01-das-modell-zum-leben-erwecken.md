# Das Modell zum Einsatz bringen

Domain-driven Design ist ein Ansatz für die Entwicklung komplexer
Software, bei dem wir:

1. Uns auf die die *Core Domain* konzentrieren.

2. *Models* in einer kreativen Zusammenarbeit von Domain-Praktikern
und Software-Praktikern erkunden.

3. Eine *Ubiquituous Language* in einem *Bounded Context* sprechen.

Diese Drei-Punkte-Zusammenfassung von DDD hängt von der Definition der
Begriffe ab, die in dieser Broschüre definiert sind.

Viele Projekte arbeiten an Modellen, ohne am Ende einen echten Nutzen
zu erzielen.  Die DDD-Patterns stellen erfolgreiche Praktiken aus
Projekten dar, bei denen die Modellierung erhebliche Vorteile gebracht
hat.  Zusammen entwerfen sie einen ganz anderen Ansatz für die
Modellierung und Softwareentwicklung, der von feinen Details bis hin
zu Visionen für höhere Ebenen reicht. Strenge
Modellierungskonventionen müssen gegen die freie Erforschung von
Modellen zusammen mit nicht-technischen Personen abgewogen werden.
Taktik und Strategie müssen kombiniert werden, um erfolgreich zu sein.
DDD befasst sich sowohl mit taktischem als auch mit strategischem
Design.

## Bounded Context

*dt.: Begrenzter Kontext*

*Bei jedem großen Projekt sind mehrere Modelle im Spiel.* Sie
entstehen aus vielen Gründen.  Zwei Subsysteme bedienen in der Regel
sehr unterschiedliche Benutzergruppen mit unterschiedlichen Aufgaben,
wobei unterschiedliche *Models* sinnvoll sein können.  Selbständig
arbeitende Teams können das gleiche Problem durch mangelnde
Kommunikation auf unterschiedliche Weise lösen.  Der Werkzeugsatz
kann auch unterschiedlich sein, so dass Programmcode nicht gemeinsam
genutzt werden kann.

Mehrere *Models* sind unvermeidlich, aber wenn Code, der auf
verschiedenen Modellen basiert, kombiniert wird, wird Software
fehlerhaft, unzuverlässig und schwer verständlich.  Die Kommunikation
zwischen den Teammitgliedern wird verwirrend.  Oft ist unklar, in
welchem Zusammenhang ein Modell nicht angewendet werden soll.

Ausdrücke aus dem *Model* haben, wie jede andere Formulierung auch,
nur im *Context* eine Bedeutung.

Daher:

**Definiere explizit den Kontext, in dem ein Modell angewendet wird.
Legen Sie explizit Grenzen in Bezug auf die Teamorganisation, die
Verwendung innerhalb bestimmter Teile der Anwendung und
Implementierungen wie Codebasen und Datenbankschemata fest.  Wende
Continuous Integration an, um Modellkonzepte und Begriffe innerhalb
dieser Grenzen strickt konsistent zu halten, lass dich aber nicht von
Problemen außerhalb ablenken oder verwirren.  Standardisiere
einen einzigen Entwicklungsprozess innerhalb des Kontextes, der nicht
anderswo verwendet werden muss.**

## Ubiquituos Language 

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

Innerhalb eines einzigen *Bounded Context* kann die Sprache so
zerbrochen sein , dass sie die Bemühungen um eine anspruchsvolle
Modellierung untergräbt.  Wenn das Modell nur dazu dient,
UML-Diagramme für die Techniker im Team zu erstellen, dann trägt es
nicht zur kreativen Zusammenarbeit im Kern von DDD bei.

Domain-Experten verwenden ihren Fachjargon, während die Techniker im
Team ihre eigene Sprache haben, um die Domäne für das Design
zu diskutieren. Die Terminologie der täglichen Diskussionen ist von
der im Code eingebauten Terminologie (letztendlich das wichtigste
Produkt eines Softwareprojekts) abgetrennt.  Und selbst die gleiche
Person verwendet unterschiedliche Sprachen in Wort und Schrift, so
dass die prägnantesten Ausdrücke der Domäne oft in einer flüchtigen
Form entstehen, die nie im Code oder gar in der Schrift erfasst wird.

Die Übersetzung stört die Kommunikation und macht das Erarbeiten des
Wissens anämisch.

Doch keiner dieser Dialekte kann eine gemeinsame Sprache sein, weil
keiner alle Bedürfnisse erfüllt.

Domänenexperten sollten gegen Begriffe oder Strukturen Einspruch erheben,
die ungeschickt oder unzureichend sind, um das Domänenverständnis zu
vermitteln; Entwickler sollten auf Mehrdeutigkeit oder Inkonsistenz
achten, die das Design stören.

Spiel mit dem Modell, während du über das System sprichst. Beschreibe
Szenarien laut mit Hilfe der Elemente und Interaktionen des Modells
und kombiniere dabei Konzepte so, wie es das *Model* erlaubt. Finde
einfachere Wege, um zu sagen, was du sagen willst, und übertrage diese
neuen Ideen dann zurück in die Diagramme und den Code.

Mit einer *Ubiquituous Language* ist das *Model* nicht nur ein
Design-Artefakt. Es wird zu einem integralen Bestandteil von allem,
was die Entwickler und Fachexperten gemeinsam tun.

Daher:

**Verwende das Modell als Rückgrat einer Sprache. Verpflichte das Team,
diese Sprache unermüdlich in der gesamten Kommunikation innerhalb des
Teams und im Code anzuwenden. Verwende in einem *Bounded Context* die
gleiche Sprache in Diagrammen, beim Schreiben und insbesondere beim
Sprechen.

Erkenne, dass eine Änderung der Sprache eine Änderung des *Models*
ist.

Löse Schwierigkeiten, indem du mit alternativen Ausdrücken
experimentierst, die alternative *Models* widerspiegeln. Dann
überarbeite den Code und benenne Klassen, Methoden und Module um, um
dem neuen *Model* zu entsprechen.  Löse Verwirrung über Begriffe im
Gespräch auf, und zwar in der Art und Weise, wie wir uns über die
Bedeutung gewöhnlicher Wörter einigen.**

## Continuous Integration

*Sobald ein Bounded Context definiert ist, müssen wir ihn intakt
 halten.*

Wenn mehrere Personen am gleichen *Bounded Context* arbeiten, besteht
eine starke Tendenz zur Fragmentierung des *Models*.  Je größer das
Team, desto größer das Problem, aber schon drei oder vier Personen
können auf ernsthafte Probleme stoßen. Doch die Zerlegung des Systems
in immer kleinere *Bounded Contexts* führt letztendlich dazu, das sie
kein ausreichendes Maß an Integration und Kohärenz mehr haben.

Daher:

**Etabliere einen Prozesses, bei dem alle Code- und alle andere
  Implementierungsartefakte häufig zusammengefügt werden. Nutze
  automatisierte Tests, um Fragmentierung schnell zu finden.  Nutze
  unermüdlich die Ubiquituous Language, um eine gemeinsame Sicht auf
  das Modell zu entwickeln, während sich die Konzepte in den Köpfen
  der verschiedenen beteiligten Personen entwickeln.*

## Model-driven Design

*dt.: modellgetriebenes Design*

*Die enge Verknüpfung des Codes mit einem zugrunde liegenden Modell
gibt dem Code Bedeutung und macht das Modell relevant.*

Wenn das Design oder zumindest ein zentraler Teil davon nicht auf das
Domänenmodell abgebildet werden kann, ist dieses Modell von geringem
Wert, und die Korrektheit der Software ist zweifelhaft.  Gleichzeitig
sind komplexe Zusammenhänge zwischen den Modellen und den Funktionen
des Designs schwer verständlich und in der Praxis nicht
aufrechtzuerhalten, da sich das Design ändert.  Eine tödliche Kluft
öffnet sich zwischen Analyse und Design, so dass die in den beiden
Aktivitäten gewonnenen Erkenntnisse nicht in die jeweils andere
einfließen.

Leite aus dem Modell die beim Design verwendete Terminologie und die
grundlegende Zuordnung von Verantwortlichkeiten ab.  Der Code wird zu
einem Ausdruck des Modells, so dass eine Änderung des Codes eine
Änderung des Modells sein kann.  Seine Wirkung muss sich entsprechend
auf den Rest der Projektarbeit auswirken.

Um die Implementierung sklavisch an ein Modell zu binden, sind in der
Regel Softwareentwicklungswerkzeuge und -sprachen erforderlich, die
ein Modellierungsparadigma unterstützen, wie beispielsweise die
objektorientierte Programmierung.

Daher:

**Entwerfe einen Teil des Softwaresystems so, dass er das
Domänenmodell im wahrsten Sinne des Wortes widerspiegelt, so dass die
Zuordnung offensichtlich ist.  Greife das Modell wieder auf und
modifiziere es, um es natürlicher in Software zu implementieren, auch
wenn du versuchst, einen tieferen Einblick in die Domäne zu bekommen.
Verlange ein einziges Modell, das beiden Zwecken gerecht wird und
zudem eine flüssige _Ubiquituous Language_ unterstützt.**

## Hands-on Modelers

*dt.: Praktizierende Modellierer*

Wenn sich die Personen, die den Code schreiben, nicht für das Modell
verantwortlich fühlen oder nicht verstehen, wie das Modell für eine
Anwendung funktionieren soll, dann hat das Modell nichts mit der
Software zu tun.  Wenn Entwickler nicht erkennen, dass Code-Änderungen
das Modell verändern, dann wird ihr Refactoring das Modell eher
schwächen als stärken. Wenn ein Modellierer vom
Implementierungsprozess getrennt ist, gewinnt er nie ein Gefühl für
die Restriktionen bei der Implementierung oder verliert sie schnell.
So geht die grundlegende Bedingung des modellgetriebenen Designs, dass
das Modell eine effektive Implementierung unterstützt und wichtige
Erkenntnisse über die Domain abstrahiert, fast verloren und die daraus
resultierenden Modelle werden unpraktisch sein. Schließlich werden die
Kenntnisse und Fähigkeiten erfahrener Designer nicht auf andere
Entwickler übertragen, wenn die Arbeitsteilung die Art der
Zusammenarbeit verhindert, die die Feinheiten der Programmierung eines
modellgetriebenen Designs vermittelt.

Daher:

**Jede technische Person, die am Modell mitwirkt, muss einige Zeit
damit verbringen, am Code zu arbeiten, unabhängig davon, welche
Hauptrolle sie im Projekt spielt.  Jeder, der für die Änderung des
Codes verantwortlich ist, muss lernen, ein Modell durch den Code
auszudrücken.  Jeder Entwickler muss auf irgendeiner Ebene an der
Diskussion über das Modell beteiligt sein und Kontakt zu
Domain-Experten haben.  Diejenigen, die auf unterschiedliche Weise
beitragen, müssen diejenigen, die am Code arbeiten, bewusst in einen
dynamischen Austausch von Ideen zum Modell durch die _Ubiquituous
Language_ einbeziehen. **

## Refactoring Towards Deeper Insight {#refactoring-towards-deeper-insight}

*dt.: Refactoring zum tieferen Verständnis*

Die Verwendung eines bewährten Satzes von Grundbausteinen zusammen mit
einer konsistenten Sprache bringt ein wenig Vernunft in die
Entwicklungsarbeit.  Aber es bleibt eine Herausforderung, tatsächlich
ein prägnantes Modell zu finden, das die subtilen Belange der
Fachexperten aufgreift und ein praktisches Design vorantreiben kann.
Ein Modell, das das Künstliche abstreift und das Wesentliche erfasst,
ist ein tiefgreifendes Modell.  Dadurch sollte die Software besser auf
die Denkweise der Domain-Experten abgestimmt sein und besser auf die
Bedürfnisse des Benutzers eingehen.

Traditionell wird Refactoring als Code-Transformation mit technischen
Motivationen beschrieben.  Refactoring kann aber auch durch einen
Einblick in die Domäne und eine entsprechende Verfeinerung des Modells
oder dessen Ausdruck im Code motiviert werden.

Anspruchsvolle Domänenmodelle erweisen sich selten als nützlich, außer
wenn sie durch einen iterativen Prozess des Refactoring entwickelt
werden, einschließlich der engen Einbindung der Domänenexperten mit
Entwicklern, die daran interessiert sind, etwas über die Domäne zu
erfahren.
