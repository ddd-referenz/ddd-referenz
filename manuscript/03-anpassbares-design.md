# III Flexibles Design

Ein Projekt, welches im Laufe der Entwicklung Fahrt aufnehmen kann - anstatt durch sein eigenes Erbe belastet zu werden - erfordert ein Design, mit dem man gerne arbeitet und das zum Wandel einlädt. Ein flexibles Design.

Flexibles Design ist eine Ergänzung zur tiefgehenden Modellierung.

Entwickler spielen hierbei zwei Rollen, von denen jede durch das Design bedient werden muss. Die gleiche Person könnte durchaus beide Rollen spielen - sogar innerhalb von Minuten hin und her wechseln - aber die Beziehung zum Code ist dennoch unterschiedlich. Eine Rolle ist der Entwickler eines Clients, der die Domänenobjekte in den Anwendungscode oder einen anderen Domänenschichtcode einbindet und dabei die Möglichkeiten des Designs nutzt. Ein flexibles Design offenbart ein tiefes Grundmodell, das sein Potenzial deutlich macht. Die Client-Entwicklerin kann flexibel einen minimalen Satz lose gekoppelter Konzepte verwenden, um eine Reihe von Szenarien in der Domäne auszudrücken. Designelemente passen auf natürliche Weise zusammen, mit einem Ergebnis, das vorhersehbar, klar charakterisiert und robust ist.

Ebenso wichtig ist, dass das Design dem Entwickler dienen muss, der daran arbeitet, es zu ändern. Um offen für Veränderungen zu sein, muss ein Design leicht verständlich sein und das gleiche zugrunde liegende Modell offenbaren, auf das der Client-Entwickler zurückgreift. Es muss den Konturen eines tiefen Modells der Domäne folgen, so dass die meisten Änderungen das Design an flexiblen Punkten biegen. Die Auswirkungen des Codes müssen transparent sein, so dass die Folgen einer Änderung leicht zu antizipieren sind.

- Verhalten sichtbar machen
- Reduktion der Änderungskosten
- Erstellung von Software, mit der Entwickler*innen gerne arbeiten

## Intention-Revealing Interfaces {#intention-revealing-interfaces}

*Dt.: Ausdrucksstarke-Interfaces*

Wenn ein Entwickler die Implementierung einer Komponente in Betracht ziehen muss, um sie zu nutzen, geht der Wert der Kapselung verloren. Wenn jemand anderes als der ursprüngliche Entwickler den Zweck eines Objekts oder einer Operation aufgrund seiner Implementierung ableiten muss, kann dieser neue Entwickler einen Zweck ableiten, den die Operation oder Klasse nur durch Zufall erfüllt. Wenn das nicht die Absicht war, kann der Code im Moment funktionieren, aber die konzeptionelle Grundlage des Designs wird beschädigt worden sein, und die beiden Entwickler werden mit Widersprüchen arbeiten.

Daher:

**Benennen Sie Klassen und Operationen, um ihre Wirkung und ihren Zweck zu beschreiben, ohne Bezugnahme auf die Mittel, mit denen sie tun, was sie versprechen. Dies befreit den Client-Entwickler von der Notwendigkeit, die Einbauten zu verstehen. Diese Namen sollten der Ubiquitous Language entsprechen, damit die Teammitglieder schnell ihre Bedeutung ableiten können. Schreiben Sie einen Test für ein Verhalten, bevor Sie es erstellen, um Ihr Denken in den Client-Entwicklermodus zu zwingen.**

## Side-Effect-Free Functions {#side-effect-free-functions}

*Dt.: Seiteneffektfreie Funktionen*

Interaktionen mehrerer Regeln oder Zusammensetzungen von Berechnungen werden extrem schwer vorherzusagen sein. Der Entickler, der eine Operation aufruft, muss ihre Durchführung und die Durchführung aller seiner Delegationen verstehen, um das Ergebnis zu antizipieren. Der Nutzen jeder Abstraktion von Interfaces ist begrenzt, wenn die Entwickler gezwungen sind, den Schleier zu durchbrechen. Ohne sicher vorhersehbare Abstraktionen müssen die Entwickler die kombinatorische Auflösung begrenzen und den Reichtum an Verhalten, der sich aufbauen lässt, mit einer niedrigen Grenze begrenzen.

Daher:

**Platzieren Sie so viel von der Logik des Programms wie möglich in Funktionen, Operationen, die Ergebnisse ohne beobachtbare Nebenwirkungen liefern. Trennen Sie Befehle (Methoden, die zu Änderungen des beobachtbaren Zustands führen) strikt in sehr einfache Operationen, die keine Domäneninformationen zurückgeben. Beherrschen Sie Seiteneffekte indem komplexe Logik in Value-Objects verschoben wird, wenn sich ein der Fachlichkeit entsprechendes Konzept präsentiert.

Alle Operationen eines Value-Objects sollten seiteneffektfreie Funktionen sein.**

## Assertions {#assertions}

*Dt.: Versicherungen / Validierungen*

Wenn die Nebenwirkungen von Operationen nur implizit durch ihre Umsetzung definiert werden, werden Designs mit viel Delegation zu einem Gewirr aus Ursache und Wirkung. Der einzige Weg, ein Programm zu verstehen, besteht darin, die Ausführung durch verzweigte Pfade zu verfolgen. Der Wert der Kapselung geht verloren. Die Notwendigkeit, die konkrete Ausführung zu verfolgen, besiegt die Abstraktion.

Daher:

**Geben Sie die Folgezustände der Operationen und die Invarianten der Klassen und Aggregate an. Wenn Assertions nicht direkt in Ihrer Programmiersprache kodiert werden können, schreiben Sie automatisierte Komponententests für sie. Schreiben Sie sie in Dokumentationen oder Diagramme, wie es zum Stil des Entwicklungsprozesses eines Projekts passt.**

Suchen Sie nach Modellen mit kohärenten Konzepten, die einen Entwickler dazu bringen, die beabsichtigten Assertions abzuleiten, die Lernkurve zu beschleunigen und das Risiko von widersprüchlichem Code zu reduzieren.

Assertions definieren Service Contrsacts und Entitätsmodifikatoren. 

Assertions definieren Invarianten auf Aggregates.

## Standalone Classes {#standalone-classses}

*Dt.: Eigenständige Klassen*

Selbst innerhalb eines Moduls nimmt die Schwierigkeit der Interpretation eines Designs mit zunehmenden Abhängigkeiten stark zu. Dies erhöht die geistige Überlastung und begrenzt die Komplexität des Designs, mit der ein Entwickler umgehen kann. Implizite Konzepte tragen zu dieser Belastung noch mehr bei als explizite Referenzen.

**Eine niedrige Kopplung ist für den Entwurf von Objekten von grundlegender Bedeutung. Wenn Sie könnten, sollten Sie ohne Kompromisse den ganzen Weg gehen. Eliminieren Sie alle anderen Konzepte aus dem Bild. Dann ist eine Klasse völlig in sich geschlossen und kann allein studiert und verstanden werden. Jede dieser in sich geschlossenen Klassen erleichtert das Verständnis eines Moduls erheblich.**

## Closure of Operations {#closure-of-operations}

*Dt.: Geschlossene Funktionen*

Die meisten interessanten Objekte tun am Ende Dinge, die nicht nur von primitiven Datentypen charakterisiert werden können.

Daher:

**Wenn es passt, definieren Sie eine Funktion, deren Rückgabetyp derselbe ist wie der Typ ihrer Argumente. Wenn der Implementierer einen Zustand hat, der bei der Berechnung verwendet wird, dann ist der Implementierer praktisch ein Argument der Funktion, so dass das/die Argument(e) und der Rückgabewert vom gleichen Typ wie der Implementierer sein sollten. Eine solche Funktion wird unter der Menge der Instanzen dieses Typs geschlossen. Eine geschlossene Funktion bietet eine High-Level-Schnittstelle, ohne Abhängigkeit auf andere Konzepte.**

Dieses Muster wird am häufigsten auf die Operationen eines Value-Objects angewendet. Da der Lebenszyklus einer Entity eine Bedeutung in der Domäne hat, kann man nicht einfach ein neue erzeugen, um eine Frage zu beantworten. Es gibt Vorgänge, die unter einem Entitätstyp abgeschlossen sind. Sie können ein Mitarbeiterobjekt nach seinem Vorgesetzten fragen und einen anderen Mitarbeiter zurückholen. Aber im Allgemeinen sind Entities nicht die Art von Konzepten, die wahrscheinlich das Ergebnis einer Berechnung sind. Dies ist also in den meisten Fällen eine Gelegenheit, nach Value Objects Ausschau zu halten.

Manchmal kommt man auf halbem Weg zu diesem Muster. Das Argument passt zum Implementierer, aber der Rückgabetyp ist unterschiedlich, oder der Rückgabetyp passt zum Empfänger und das Argument ist unterschiedlich. Diese Funktionen sind nicht geschlossen, aber sie bieten einen Teil des Vorteils der Schließung, indem sie den Geist befreien.

## Declarative Design {#declarative-design}

*Dt.: Deklaratives Design*

Es kann keine wirklichen Garantien in prozeduraler Software geben. Um nur eine Möglichkeit zu nennen, Assertions zu umgehen, könnte Code zusätzliche Seiteneffekte haben, die nicht ausdrücklich ausgeschlossen wurden. Egal wie modellgetrieben unser Design ist, wir schreiben immer noch Prozeduren, um die Wirkung der konzeptionellen Interaktionen zu erzeugen. Und wir verbringen einen Großteil unserer Zeit damit, Boilerplate Code zu schreiben, der keine wirkliche Bedeutung oder Verhalten hat. Intention-revaling Interfaces und die anderen Patterns in diesem Kapitel helfen, aber sie können konventionellen objektorientierten Programmen niemals formale Strenge verleihen.

Dies sind einige der Motivationen für Declarative Design. Dieser Begriff bedeutet verschiedenen Menschen unterschiedliche Dinge, aber normalerweise zeigt er einen Weg an, ein Programm oder einen Teil eines Programms als eine Art ausführbare Spezifikation zu schreiben. Eine sehr genaue Beschreibung der Eigenschaften steuert die Software tatsächlich. In seinen verschiedenen Herangehensweisen könnte dies durch Reflection oder zur Kompilierzeit durch Codegenerierung (automatische Erzeugung von konventionellem Code auf der Grundlage der Deklaration) geschehen. Dieser Ansatz ermöglicht es einem anderen Entwickler, die Deklaration zum Nennwert zu nehmen. Es ist eine absolute Garantie.

Viele deklarative Ansätze können korrumpiert werden, wenn die Entwickler sie absichtlich oder unabsichtlich umgehen. Dies ist wahrscheinlich, wenn das System schwer zu bedienen oder zu restriktiv ist. Jeder muss die Regeln des Rahmens befolgen, um die Vorteile eines deklarativen Programms zu nutzen.

### Ein deklarativer Design-Stil

Sobald Ihr Entwurf über intention-revealing Interfaces, side-effect-free Functions und Assertions verfügt, begeben Sie sich in deklaratives Gebiet. Viele der Vorteile des Declarative Designs werden erzielt, sobald Sie kombinierbare Elemente haben, die ihre Bedeutung kommunizieren, und die charakteristische oder offensichtliche Effekte oder gar keine beobachtbaren Effekte haben.

Ein flexibles Design kann es dem Kundencode ermöglichen, einen deklarativen Designstil zu verwenden. Zur Veranschaulichung werden im nächsten Abschnitt einige der Muster in diesem Kapitel zusammengefasst, um die Spezifikation flexibler und deklarativer zu gestalten.