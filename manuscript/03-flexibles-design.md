# III. Flexibles Design

Ein Projekt, welches im Laufe der Entwicklung Fahrt aufnehmen kann - anstatt durch sein eigenes Erbe belastet zu werden - erfordert ein Design, mit dem man gerne arbeitet und das zum Wandel einlädt. Ein flexibles Design.

Flexibles Design ist die Ergänzung zur tiefgehenden Modellierung.

Entwickler spielen zwei Rollen, von denen jede durch das Design unterstützt werden muss. Die gleiche Person könnte durchaus beide Rollen spielen - sogar innerhalb von Minuten hin und her wechseln - aber die Beziehung zum Code ist dennoch unterschiedlich. Eine Rolle ist der Entwickler eines Clients, der die Domänenobjekte in den Anwendungscode oder einen anderen Domänenschichtcode einbindet und dabei die Möglichkeiten des Designs nutzt. Ein flexibles Design offenbart ein tiefes zugrunde liegendes Modell, das sein Potenzial deutlich macht. Die Client-Entwicklerin kann flexibel einen minimalen Satz lose gekoppelter Konzepte verwenden, um eine Reihe von Szenarien in der Domäne auszudrücken. Elemente des Designs passen auf natürliche Weise zusammen, mit einem Ergebnis, das vorhersehbar, klar charakterisiert und robust ist.

Ebenso wichtig ist, dass das Design dem Entwickler, der daran arbeitet, dienen muss, es zu ändern. Um offen für Veränderungen zu sein, muss ein Design leicht verständlich sein und das gleiche zugrunde liegende Modell offenbaren, auf das der Client-Entwickler zurückgreift. Es muss den Konturen eines tiefen Modells der Domäne folgen, so dass die meisten Änderungen das Design an flexiblen Punkten biegen. Die Auswirkungen des Codes müssen transparent sein, so dass die Folgen einer Änderung leicht voraussehbar sind.

- Verhalten sichtbar machen
- Reduktion der Änderungskosten
- Erstellung von Software, mit der Entwickler*innen gerne arbeiten

## Intention-Revealing Interfaces {#intention-revealing-interfaces}

*dt.: Ausdrucksstarke Schnittstellen*

Wenn ein Entwickler die Implementierung einer Komponente berücksichten muss, um sie zu nutzen, geht der Wert der Kapselung verloren. Wenn jemand anderes als der ursprüngliche Entwickler den Zweck eines Objekts oder einer Operation aufgrund seiner Implementierung ableiten muss, kann dieser neue Entwickler einen Zweck ableiten, den die Operation oder Klasse nur durch Zufall erfüllt. Wenn das nicht die Absicht war, kann der Code im Moment funktionieren, aber die konzeptionelle Grundlage des Designs wird beschädigt sein, und die beiden Entwickler werden gegeneinander arbeiten.

Daher:

**Benenne Klassen und Operationen, um ihre Wirkung und ihren Zweck zu beschreiben, ohne die Mittel zu nennen, mit denen sie das tun, was sie versprechen. Dies befreit den Client-Entwickler von der Notwendigkeit, das Innenleben zu verstehen. Diese Namen sollten der Ubiquitous Language entsprechen, damit Teammitglieder schnell ihre Bedeutung ableiten können. Schreibe einen Test für ein Verhalten, bevor Du es implementierst, um Dein Denken in den Client-Entwicklermodus zu zwingen.**

## Side-Effect-Free Functions {#side-effect-free-functions}

*dt.: Seiteneffektfreie Funktionen*

Interaktionen mehrerer Regeln oder Kompositionen von Berechnungen werden extrem schwer vorherzusagen. Der Entwickler, der eine Operation aufruft, muss ihre Implementierung und die Implementierung aller Delegationen verstehen, um das Ergebnis voraussehen zu können. Der Nutzen jeder Abstraktion von Schnittstellen ist begrenzt, wenn Entwickler gezwungen sind, diesen Schleier zu lüften. Ohne sicher vorhersehbare Abstraktionen müssen Entwickler die kombinatorische Vielfalt begrenzt halten, was eine obere Grenzen für die Menge an Verhalten darstellt, die umgesetzt werden kann.

Daher:

**Platziere so viel von der Programmlogik wie möglich in Funktionen, also Operationen, die Ergebnisse ohne beobachtbare Nebenwirkungen liefern. Separiere Kommandos (Methoden, die zu Änderungen des beobachtbaren Zustands führen) strikt in sehr einfache Operationen, die keine Domäneninformationen zurückgeben. Kontrolliere Seiteneffekte zusätzlich, indem komplexe Logik in Value Objects verschoben wird, wenn sich in der Fachlichkeit ein entsprechendes Konzept zeigt.

Alle Operationen eines Value Objects sollten seiteneffektfreie Funktionen sein.**

## Assertions {#assertions}

*dt.: Zusicherungen*

Wenn die Nebenwirkungen von Operationen nur implizit durch ihre Umsetzung definiert sind, werden Entwürfe mit viel Delegation zu einem Gewirr aus Ursache und Wirkung. Der einzige Weg, ein Programm zu verstehen, besteht darin, die Ausführung durch verzweigte Pfade hindurch nachzuverfolgen. Der Wert der Kapselung geht verloren. Die Notwendigkeit, die konkrete Ausführung nachverfolgen zu müssen, zerstört die Abstraktion.

Daher:

**Gib die Nachbedingungen von Operationen und die Invarianten von Klassen und Aggregaten an. Wenn Zusicherungen nicht direkt in Deiner Programmiersprache kodiert werden können, schreibe automatisierte Unit Tests für sie. Schreibe sie in Dokumentationen oder in Diagramme, falls dies zum Stil des Entwicklungsprozesses des Projekts passt.**

Suche nach Modellen mit kohärenten Konzepten, die einen Entwickler unterstützen, die beabsichtigten Zusicherungen zu erkennen, dadurch die Lernkurve zu beschleunigen und das Risiko von widersprüchlichem Code zu reduzieren.

Zusicherungen definieren Schnittstellenverträge und Modifikatoren von Entitäten. 

Zusicherungen definieren Invarianten auf Aggregaten.

## Standalone Classes {#standalone-classses}

*dt.: Eigenständige Klassen*

Selbst innerhalb eines Moduls nimmt die Schwierigkeit der Interpretation eines Entwurfs mit zunehmenden Abhängigkeiten stark zu. Dies führt zu geistiger Überlastung und begrenzt die Komplexität des Entwurfs, mit der ein Entwickler umgehen kann. Implizite Konzepte tragen zu dieser Belastung noch mehr bei als explizite Referenzen.

**Eine geringe Kopplung ist für den Entwurf von Objekten von grundlegender Bedeutung. Wenn Du kannst, gehe den ganzen Weg: eliminiere alle anderen Konzepte aus dem Bild. Dann ist eine Klasse völlig in sich geschlossen und kann allein studiert und verstanden werden. Jede dieser in sich geschlossenen Klassen erleichtert das Verständnis eines Moduls erheblich.**

## Closure of Operations {#closure-of-operations}

*dt.: Geschlossene Funktionen*

Die meisten interessanten Objekte tun am Ende Dinge, die nicht nur von primitiven Datentypen charakterisiert werden können.

Daher:

**Wenn es passt, definiere eine Funktion, deren Rückgabetyp derselbe ist wie der Typ ihres/ihrer Argumente(s). Wenn der Implementierer einen Zustand hat, der bei der Berechnung verwendet wird, dann ist der Implementierer faktisch ein Argument der Funktion, so dass das/die Argument(e) und der Rückgabewert vom gleichen Typ wie der Implementierer sein sollten. Eine solche Funktion ist unter der Menge der Instanzen dieses Typs geschlossen. Eine geschlossene Funktion bietet eine höherwertige Schnittstelle, ohne Abhängigkeit auf andere Konzepte.**

Dieses Muster wird meistens auf die Operationen eines Value Objects angewendet. Da der Lebenszyklus einer Entität eine Bedeutung in der Domäne hat, kann man nicht einfach ein neue Entität erzeugen, um eine Anfrage zu beantworten. Es gibt Vorgänge, die unter einem Entitätstyp abgeschlossen sind. Du kannst ein Mitarbeiterobjekt nach seinem Vorgesetzten fragen und ein anderes Mitarbeiterobjekt zurückerhalten. Aber im Allgemeinen sind Entitäten keine Konzepte, die häufig das Ergebnis einer Berechnung sind. In den meisten Fällen ist dies also eine Eigenschaft, die in Value Objects zu suchen ist.

Manchmal erreicht man dieses Muster nur halb: das Argument passt zum Implementierer, aber der Rückgabetyp ist unterschiedlich, oder der Rückgabetyp passt zum Empfänger, aber das Argument ist unterschiedlich. Diese Funktionen sind nicht geschlossen, aber sie bieten einen Teil des Vorteils der Geschlossenheit, indem sie einfacher verständlich sind.

## Declarative Design {#declarative-design}

*Dt.: Deklaratives Design*

Es kann keine wirklichen Garantien in prozeduraler Software geben. Um nur eine Möglichkeit zu nennen, Assertions zu umgehen, könnte Code zusätzliche Seiteneffekte haben, die nicht ausdrücklich ausgeschlossen wurden. Egal wie modellgetrieben unser Design ist, wir schreiben immer noch Prozeduren, um die Wirkung der konzeptionellen Interaktionen zu erzeugen. Und wir verbringen einen Großteil unserer Zeit damit, Boilerplate Code zu schreiben, der keine wirkliche Bedeutung oder Verhalten hat. Intention-revaling Interfaces und die anderen Patterns in diesem Kapitel helfen, aber sie können konventionellen objektorientierten Programmen niemals formale Strenge verleihen.

Dies sind einige der Motivationen für Declarative Design. Dieser Begriff bedeutet verschiedenen Menschen unterschiedliche Dinge, aber normalerweise zeigt er einen Weg an, ein Programm oder einen Teil eines Programms als eine Art ausführbare Spezifikation zu schreiben. Eine sehr genaue Beschreibung der Eigenschaften steuert die Software tatsächlich. In seinen verschiedenen Herangehensweisen könnte dies durch Reflection oder zur Kompilierzeit durch Codegenerierung (automatische Erzeugung von konventionellem Code auf der Grundlage der Deklaration) geschehen. Dieser Ansatz ermöglicht es einem anderen Entwickler, die Deklaration zum Nennwert zu nehmen. Es ist eine absolute Garantie.

Viele deklarative Ansätze können korrumpiert werden, wenn die Entwickler sie absichtlich oder unabsichtlich umgehen. Dies ist wahrscheinlich, wenn das System schwer zu bedienen oder zu restriktiv ist. Jeder muss die Regeln des Rahmens befolgen, um die Vorteile eines deklarativen Programms zu nutzen.

### Ein deklarativer Design-Stil

Sobald Ihr Entwurf über intention-revealing Interfaces, side-effect-free Functions und Assertions verfügt, begeben Sie sich in deklaratives Gebiet. Viele der Vorteile des Declarative Designs werden erzielt, sobald Sie kombinierbare Elemente haben, die ihre Bedeutung kommunizieren, und die charakteristische oder offensichtliche Effekte oder gar keine beobachtbaren Effekte haben.

Ein flexibles Design kann es dem Kundencode ermöglichen, einen deklarativen Designstil zu verwenden. Zur Veranschaulichung werden im nächsten Abschnitt einige der Muster in diesem Kapitel zusammengefasst, um die Spezifikation flexibler und deklarativer zu gestalten.

## Arbeiten auf Basis etablierter Formalismen

Ein enges konzeptionelles Framework von Grund auf zu schaffen, ist etwas, was man nicht jeden Tag tun kann. Manchmal entdeckt und verfeinert man eines davon im Laufe des Lebens eines Projekts. Aber Ihr könnt oft konzeptionelle Systeme verwenden und anpassen, die in Eurer oder anderen fachlichen Domänen seit langem etabliert sind. Einige von denen wurden eventuell sogar über Jahrhunderte hinweg verfeinert und destilliert. Viele Geschäftsanwendungen betreffen z.B. das Rechnungswesen. Das Rechnungswesen definiert ein gut entwickeltes Set von Einheiten und Regeln, die eine einfache Anpassung an ein tiefgehendes Modell und ein flexibles Design ermöglichen.

Es gibt viele solcher formalisierten konzeptionellen Rahmen, aber mein persönlicher Favorit ist die Mathematik. Es ist überraschend, wie nützlich es sein kann, eine gewisse Wendung in der Grundrechenart herauszuziehen. Viele Domänen beinhalten Mathematik irgendwo. Such danach, Grab es aus. Spezialisierte Mathematik ist sauber, kombinierbar mit klaren Regeln, und die Menschen finden sie leicht zu verstehen.

Ein praktisches Beispiel, "Shares Math", wurde in Kapitel 8 des Buches, Domain-Driven Design, diskutiert.

## Conceptual Contours

*Dt.: Konzeptionelle Konturen*

Manchmal favorisieren Leute einen feingranularen Schnitt der Funktionalität, um eine flexible Kombination zu ermöglichen. Manchmal favorisieren sie einen eher grobgranularen Schnitt, um die Komplexität zu kapseln. Manchmal streben sie nach einer konsistenten Granularität, wodurch alle Klassen und Operationen in ähnlicher Größenordnung durchgeführt werden. Das sind übertriebene Vereinfachungen, die als allgemeine Regeln nicht gut funktionieren. Aber sie sind durch grundlegende Probleme motiviert.

Wenn Elemente eines Modells oder Designs in ein monolithisches Konstrukt eingebettet sind, wird deren Funktionalität dupliziert. Die externe Schnittstelle sagt nicht alles, was einem Kunden wichtig sein könnte. Ihre Bedeutung ist schwer zu verstehen, da verschiedene Konzepte miteinander vermischt werden.

Umgekehrt kann die Zerlegung von Klassen und Methoden den Client sinnlos verkomplizieren, indem sie Clients dazu zwingt, zu verstehen, wie kleine Teile zusammenpassen. Schlimmer noch, ein Konzept kann völlig verloren gehen. Die Hälfte eines Uranatoms ist nicht Uran. Und natürlich zählt nicht nur die Korngröße, sondern auch die Art und Weise, wie das Korn läuft.

Daher:

**Zerlege die Designelemente (Funktionen, Interfaces, Klassen und Aggregates) in zusammenhängende Einheiten, wobei Du Deine Intuition der wichtigen Teilbereiche in der Domäne berücksichtigst. Beobachte die Achsen von Veränderung und Stabilität durch sukzessives Refactoring und suche nach den zugrunde liegenden konzeptionellen Konturen, die diese Schermuster erklären. Richte das Modell auf die konsistenten Aspekte der Domäne aus, die es überhaupt zu einem lebensfähigen Wissensgebiet machen.**

Ein flexibles Design, das auf einem tiefgehenden Modell basiert, ergibt eine einfache Reihe von Schnittstellen, die sich logisch kombinieren, um sinnvolle Aussagen in der Ubiquitous Language zu treffen, ohne die Ablenkung und den Wartungsaufwand irrelevanter Optionen.
