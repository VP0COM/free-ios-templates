# Datentabelle mit Pagination React: Fertiger Code & Beispiele 2026

*So baust du eine React-Datentabelle mit sauberer Seitennavigation, stabilen Keys und einer Struktur, die später auch mit einer API funktioniert.*

Von Lawrence Arya, Gründer von VP0\
Veröffentlicht am 28. September 2026

Eine Datentabelle mit Pagination in React braucht im Kern nur drei Dinge: den aktuellen Seitenindex, die gewünschte Seitengröße und eine berechnete Teilmenge deiner Daten. Für lokale Daten kannst du das vollständig mit `useState`, `slice()` und `map()` lösen. Sobald deine Tabelle viele Datensätze aus einer API lädt, wechselst du besser zu serverseitiger Pagination, damit nicht erst alle Zeilen im Browser landen müssen. React selbst gibt dir die Bausteine für State und Listen-Rendering, während TanStack Table sinnvoll wird, wenn Sortierung, Filter, Spaltenzustand oder serverseitige Pagination dazukommen.

## Wie baut man eine Datentabelle mit Pagination in React?

Für eine einfache React-Tabelle brauchst du keine zusätzliche Tabellenbibliothek. Halte `currentPage` im State, berechne Start und Ende der sichtbaren Zeilen und rendere nur diesen Ausschnitt.

React empfiehlt für Listen stabile `key`-Werte aus deinen Daten, typischerweise eine Datenbank-ID. Das ist bei Tabellen besonders wichtig, weil Zeilen beim Blättern, Filtern oder Sortieren ihre Position ändern können.

Ein vollständiges Minimalbeispiel sieht so aus:

```jsx
import { useState } from "react";

const users = [
  { id: 1, name: "Anna", email: "anna@example.com", role: "Admin" },
  { id: 2, name: "Ben", email: "ben@example.com", role: "Editor" },
  { id: 3, name: "Clara", email: "clara@example.com", role: "User" },
  { id: 4, name: "David", email: "david@example.com", role: "User" },
  { id: 5, name: "Eva", email: "eva@example.com", role: "Editor" },
  { id: 6, name: "Farid", email: "farid@example.com", role: "User" },
  { id: 7, name: "Greta", email: "greta@example.com", role: "Admin" },
  { id: 8, name: "Hannes", email: "hannes@example.com", role: "User" },
  { id: 9, name: "Ida", email: "ida@example.com", role: "Editor" },
  { id: 10, name: "Jonas", email: "jonas@example.com", role: "User" }
];

export default function UserTable() {
  const [currentPage, setCurrentPage] = useState(1);
  const rowsPerPage = 4;

  const totalPages = Math.ceil(users.length / rowsPerPage);
  const startIndex = (currentPage - 1) * rowsPerPage;
  const visibleUsers = users.slice(
    startIndex,
    startIndex + rowsPerPage
  );

  return (
    <div>
      <table>
        <thead>
          <tr>
            <th>Name</th>
            <th>E-Mail</th>
            <th>Rolle</th>
          </tr>
        </thead>

        <tbody>
          {visibleUsers.map((user) => (
            <tr key={user.id}>
              <td>{user.name}</td>
              <td>{user.email}</td>
              <td>{user.role}</td>
            </tr>
          ))}
        </tbody>
      </table>

      <div>
        <button
          onClick={() => setCurrentPage((page) => page - 1)}
          disabled={currentPage === 1}
        >
          Zurück
        </button>

        <span>
          Seite {currentPage} von {totalPages}
        </span>

        <button
          onClick={() => setCurrentPage((page) => page + 1)}
          disabled={currentPage === totalPages}
        >
          Weiter
        </button>
      </div>
    </div>
  );
}
```

`slice(start, end)` erstellt eine flache Kopie des gewünschten Array-Bereichs und verändert das ursprüngliche Array nicht. Genau deshalb passt die Methode gut für einfache clientseitige Pagination.

## Wie funktioniert die Pagination-Logik genau?

Die Pagination ist nur Indexrechnung. Bei Seite 1 und vier Zeilen pro Seite startest du bei Index 0, bei Seite 2 bei Index 4, bei Seite 3 bei Index 8.

Die Formel lautet:

```js
const startIndex = (currentPage - 1) * rowsPerPage;
const endIndex = startIndex + rowsPerPage;
const visibleRows = rows.slice(startIndex, endIndex);
```

Für 53 Datensätze mit zehn Zeilen pro Seite ergibt `Math.ceil(53 / 10)` insgesamt sechs Seiten. Auf der letzten Seite bleiben drei Datensätze übrig.

`currentPage` ist die aktuell sichtbare Seite, zum Beispiel `2`.

`rowsPerPage` legt die Anzahl der Zeilen pro Seite fest, zum Beispiel `10`.

`startIndex` ist der erste Array-Index der aktuellen Seite, zum Beispiel `10`.

`endIndex` ist das exklusive Ende für `slice()`, zum Beispiel `20`.

`totalPages` ist die Anzahl aller Seiten und wird zum Beispiel mit `Math.ceil(rows.length / 10)` berechnet.

Ein häufiger Fehler ist, den sichtbaren Ausschnitt als eigenen State zu speichern. Das brauchst du meist nicht. Der Ausschnitt lässt sich aus `rows`, `currentPage` und `rowsPerPage` berechnen. So vermeidest du einen zweiten State, der mit den eigentlichen Daten auseinanderlaufen kann.

Wenn die Berechnung wirklich teuer wird, kann `useMemo` sinnvoll sein. React beschreibt `useMemo` aber ausdrücklich als Performance-Optimierung, nicht als Voraussetzung für korrekten Code. Für ein kleines Array ist direkte Berechnung normalerweise klarer.

## Wie fügt man Seitenzahlen statt nur Zurück und Weiter hinzu?

Seitenzahlen sind hilfreich, wenn Nutzer direkt zu einer bestimmten Stelle springen sollen. Für wenige Seiten kannst du einfach ein Array mit allen Seiten erzeugen und Buttons daraus rendern.

```jsx
const pageNumbers = Array.from(
  { length: totalPages },
  (_, index) => index + 1
);

return (
  <nav aria-label="Tabellennavigation">
    <button
      onClick={() => setCurrentPage((page) => Math.max(page - 1, 1))}
      disabled={currentPage === 1}
    >
      Zurück
    </button>

    {pageNumbers.map((page) => (
      <button
        key={page}
        onClick={() => setCurrentPage(page)}
        aria-current={currentPage === page ? "page" : undefined}
      >
        {page}
      </button>
    ))}

    <button
      onClick={() =>
        setCurrentPage((page) => Math.min(page + 1, totalPages))
      }
      disabled={currentPage === totalPages}
    >
      Weiter
    </button>
  </nav>
);
```

Bei 200 Seiten solltest du nicht 200 Buttons rendern. Zeige dann ein kleines Fenster rund um die aktuelle Seite, zum Beispiel `1 2 3 ... 18 19 20 ... 200`, oder kombiniere Zurück und Weiter mit einer direkten Seiteneingabe.

Achte auch auf den Zustand nach Filteränderungen. Wenn ein Filter 20 Seiten auf nur noch zwei reduziert, während `currentPage` noch 12 ist, würdest du sonst eine leere Seite sehen. Setze bei relevanten Filteränderungen die Seite auf 1 zurück oder begrenze sie auf die neue maximale Seitenzahl.

## Wann reicht clientseitige Pagination und wann braucht man den Server?

Clientseitige Pagination passt, wenn der Browser den kompletten Datensatz ohnehin sinnvoll laden kann. Serverseitige Pagination passt, wenn Datenmenge, Transfergröße, Abfragekosten oder Datenschutz dagegen sprechen, alle Zeilen zuerst zum Client zu schicken.

TanStack Table beschreibt genau diese Trennung und unterstützt sowohl clientseitige als auch manuelle serverseitige Pagination. Die Dokumentation weist außerdem darauf hin, dass die sinnvolle Grenze nicht allein von der Zeilenzahl abhängt, sondern auch von Spaltenzahl, Datengröße, Browser-Speicher und der Kostenstruktur der Serverabfrage.

Bei 50 lokalen Datensätzen passt clientseitige Pagination, weil sie simpel ist und keinen zusätzlichen API-Roundtrip benötigt.

Bei 2.000 kleinen Datensätzen kann clientseitige Pagination je nach Spalten und Browser ebenfalls noch problemlos funktionieren.

Bei 100.000 Datensätzen aus einer Datenbank ist serverseitige Pagination sinnvoll, damit nicht alles gleichzeitig übertragen wird.

Wenn die Suche über den gesamten Datenbestand laufen soll, sollte sie serverseitig erfolgen, damit alle Datensätze berücksichtigt werden.

Wenn die Daten bereits komplett im Browser vorhanden sind, bringt eine zusätzliche API-Abfrage für jede Seite oft wenig.

Bei einer sehr langen Liste ohne klassische Seiten kann Virtualisierung sinnvoll sein, damit nur die sichtbaren Zeilen gerendert werden.

Die State of JavaScript 2025 Erhebung zeigt React weiterhin als sehr verbreitetes Frontend-Framework. In der Bibliotheksauswertung gaben 83,6 % der befragten Nutzer an, React verwendet zu haben. Das ist kein Argument für eine bestimmte Tabellenlösung, erklärt aber, warum es für React so viele ausgereifte Table- und Data-Grid-Optionen gibt.

Der Web Almanac 2025 analysierte 16,2 Millionen Websites und berichtet, dass 98,1 % der untersuchten Seiten mindestens eine JavaScript-Datei anfordern. Für Datentabellen ist die praktische Lehre nicht, JavaScript zu vermeiden, sondern unnötige Datenübertragung und unnötige Rendering-Arbeit klein zu halten.

## Wie baut man serverseitige Pagination mit React und einer API?

Bei serverseitiger Pagination sendest du mindestens Seitenindex und Seitengröße an deine API. Die Antwort sollte die Zeilen der aktuellen Seite und die Gesamtzahl der Datensätze liefern.

Eine mögliche API-Antwort:

```json
{
  "items": [
    { "id": 41, "name": "Anna" },
    { "id": 42, "name": "Ben" }
  ],
  "total": 248
}
```

Die React-Komponente kann so aussehen:

```jsx
import { useEffect, useState } from "react";

export default function ServerTable() {
  const [page, setPage] = useState(1);
  const [pageSize] = useState(10);
  const [rows, setRows] = useState([]);
  const [total, setTotal] = useState(0);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState("");

  useEffect(() => {
    const controller = new AbortController();

    async function loadRows() {
      setLoading(true);
      setError("");

      try {
        const response = await fetch(
          `/api/users?page=${page}&limit=${pageSize}`,
          { signal: controller.signal }
        );

        if (!response.ok) {
          throw new Error("Daten konnten nicht geladen werden");
        }

        const data = await response.json();
        setRows(data.items);
        setTotal(data.total);
      } catch (err) {
        if (err.name !== "AbortError") {
          setError(err.message);
        }
      } finally {
        if (!controller.signal.aborted) {
          setLoading(false);
        }
      }
    }

    loadRows();

    return () => controller.abort();
  }, [page, pageSize]);

  const totalPages = Math.ceil(total / pageSize);

  return (
    <div>
      {error && <p role="alert">{error}</p>}

      {loading ? (
        <p>Lädt...</p>
      ) : (
        <table>
          <tbody>
            {rows.map((row) => (
              <tr key={row.id}>
                <td>{row.name}</td>
              </tr>
            ))}
          </tbody>
        </table>
      )}

      <button
        onClick={() => setPage((value) => value - 1)}
        disabled={page === 1 || loading}
      >
        Zurück
      </button>

      <span>
        Seite {page} von {totalPages}
      </span>

      <button
        onClick={() => setPage((value) => value + 1)}
        disabled={page === totalPages || loading}
      >
        Weiter
      </button>
    </div>
  );
}
```

In einer echten Anwendung solltest du außerdem Fehlerzustand, leere Ergebnisse und eine Strategie für schnelle Seitenwechsel berücksichtigen. Der `AbortController` im Beispiel verhindert, dass eine ältere Anfrage nach einem schnellen Seitenwechsel noch ungewollt das aktuelle Ergebnis überschreibt.

Wichtig ist auch die Reihenfolge mit Sortierung und Filtern. Bei serverseitiger Pagination gehören globale Suche, Sortierung und Filter normalerweise in dieselbe Serverabfrage. Sonst filterst du nur die zehn gerade geladenen Zeilen und vermittelst dem Nutzer ein falsches Ergebnis.

## Wann lohnt sich TanStack Table für Pagination?

TanStack Table lohnt sich, sobald Pagination nicht mehr die einzige Tabellenfunktion ist. Wenn du zusätzlich Sortierung, Filter, Spaltenzustand, Zeilenauswahl oder kontrollierten Tabellen-State brauchst, vermeidest du damit viel selbst geschriebene Zustandslogik.

Das Paket `@tanstack/react-table` ist headless. Es liefert Tabellenlogik, aber kein festes visuelles Markup. Dadurch kannst du das HTML und Styling selbst bestimmen.

Installation:

```bash
npm install @tanstack/react-table
```

Für clientseitige Pagination brauchst du in TanStack Table das Pagination Row Model:

```jsx
import {
  getCoreRowModel,
  getPaginationRowModel,
  useReactTable
} from "@tanstack/react-table";

const table = useReactTable({
  data,
  columns,
  getCoreRowModel: getCoreRowModel(),
  getPaginationRowModel: getPaginationRowModel(),
  initialState: {
    pagination: {
      pageIndex: 0,
      pageSize: 10
    }
  }
});
```

Für serverseitige Pagination setzt du `manualPagination: true` und gibst `rowCount` oder `pageCount` mit. TanStack Table geht dann davon aus, dass die Daten, die du an die Tabelle übergibst, bereits serverseitig paginiert wurden.

```jsx
const table = useReactTable({
  data: query.data?.items ?? [],
  columns,
  getCoreRowModel: getCoreRowModel(),
  manualPagination: true,
  rowCount: query.data?.total ?? 0,
  state: {
    pagination
  },
  onPaginationChange: setPagination
});
```

Für eine Tabelle mit drei Spalten und 40 lokalen Zeilen würde ich trotzdem bei einfachem React bleiben. Eine Tabellenbibliothek lohnt sich, wenn sie echte Komplexität entfernt, nicht nur weil sie verfügbar ist.

## Welche Fehler machen React-Paginationen am häufigsten?

Die meisten Fehler entstehen nicht beim `slice()`, sondern beim Zusammenspiel von Pagination, Filtern, Sortierung und asynchronen Daten.

Prüfe vor allem diese Punkte:

1. **Instabile Keys:** Nutze eine echte ID statt des Array-Index. React braucht stabile Keys, um Zeilen korrekt wiederzuerkennen.
2. **Seite wird nach Filteränderung nicht zurückgesetzt:** Wenn weniger Seiten übrig bleiben, kann die aktuelle Seite leer werden.
3. **Nur die aktuelle Seite wird gefiltert:** Bei serverseitiger Pagination müssen Filter und Suche serverseitig über den gesamten Datenbestand laufen.
4. **Gesamtzahl fehlt:** Ohne `total`, `rowCount` oder `pageCount` weiß die Oberfläche nicht zuverlässig, wann die letzte Seite erreicht ist.
5. **Doppelte Requests:** Schnelle Seitenwechsel können ältere Antworten später eintreffen lassen. Brich veraltete Requests ab oder nutze eine Datenbibliothek, die Request-Zustände verwaltet.
6. **Blindes Memoisieren:** `useMemo` ist sinnvoll für messbar teure Berechnungen, nicht als Standardhülle um jede Zeile. React beschreibt Memoisierung als Optimierung.
7. **Keine Zustände für Laden, Fehler und keine Daten:** Eine produktive Tabelle braucht mehr als nur den Erfolgsfall.

Ein gutes Debugging-Muster ist, die drei Werte `page`, `pageSize` und `total` sichtbar zu loggen. Wenn diese stimmen, liegen leere Seiten fast immer in der Berechnung, Filterlogik oder API-Antwort.

## Wie gestaltet man die Pagination so, dass sie auf Mobilgeräten funktioniert?

Auf kleinen Bildschirmen sollte die Seitennavigation einfacher werden, nicht dichter. Zwei große Buttons für Zurück und Weiter plus eine kompakte Seitenanzeige sind oft brauchbarer als zehn kleine Seitennummern.

Für ein Webprojekt kannst du die Navigation unter die Tabelle setzen und breite Tabellen horizontal scrollbar machen. Für eine echte iOS-App solltest du dagegen prüfen, ob eine klassische Tabelle überhaupt das passende Muster ist. In mobilen Interfaces sind Listen, Karten und Drill-down-Navigation oft leichter zu bedienen als eine breite Desktop-Tabelle.

Wenn du dieselbe Datenidee in einer iOS-App mit Expo React Native umsetzt, kann VP0 als kostenloser Design-Startpunkt helfen. Die Explore-Seite ist auf Englisch. Du wählst dort einen passenden iOS-Screen oder Flow und gibst den Design-Link an einen KI-Builder weiter. VP0 liefert dabei die UI-Quelle, nicht deine Pagination-, API- oder Datenbanklogik.

VP0 Explore

Gerade bei mobilen Admin- oder Dashboard-Screens würde ich zuerst klären, welche Informationen auf einer Zeile wirklich nötig sind. Vier gut priorisierte Felder sind oft besser als eine Desktop-Tabelle mit zwölf Spalten, die auf dem iPhone nur noch horizontal geschoben wird.

## Wann ist VP0 nicht der richtige Startpunkt?

Für eine klassische React-Web-Datentabelle ist VP0 nicht der richtige Tabellenbaukasten. VP0 ist auf iOS-App-Designs in Expo React Native ausgerichtet, während eine Web-Datentabelle andere Komponenten, Semantik und Interaktionen braucht.

Wenn dein Ziel eine Webanwendung mit komplexen Tabellen ist, passt eine React-Lösung mit eigenem HTML oder eine headless Bibliothek wie TanStack Table besser. Wenn du dagegen eine iOS-App mit KI baust und einen visuellen Startpunkt für Listen, Dashboards oder Detailansichten brauchst, kann VP0 an der Design-Ebene helfen.

Auch dort gilt die Grenze klar: VP0 liefert UI-Startpunkte. Konten, Backend, Datenbank, Pagination und App-Store-Einreichung bleiben Teil deines eigentlichen Projekts.

## Das solltest du wählen

Für eine kleine lokale Datentabelle würde ich mit normalem React anfangen: `useState` für die aktuelle Seite, `slice()` für die sichtbaren Zeilen und stabile IDs als `key`. Das ist leicht zu lesen, leicht zu testen und ohne zusätzliche Abhängigkeit vollständig.

Sobald die Daten aus einer größeren Datenbank kommen, verschiebe Pagination, Suche und Sortierung auf den Server. Liefere der Oberfläche `items` plus `total`, damit sie die Seitenzahl korrekt berechnen kann.

TanStack Table ist der nächste sinnvolle Schritt, wenn deine Tabelle mehrere Zustände gleichzeitig verwaltet, etwa Pagination, Sortierung, Filter und Spaltenauswahl. Für mobile iOS-Oberflächen würde ich das Tabellenmuster dagegen neu denken und eher mit einer guten Listen- oder Dashboard-Struktur starten.

## Häufig gestellte Fragen (FAQ)

### Wie baut man eine Datentabelle mit Pagination in React?

Du speicherst die aktuelle Seite im State, berechnest den Startindex mit `(currentPage - 1) * rowsPerPage` und schneidest die sichtbaren Zeilen mit `slice()` aus deinem Array. Danach renderst du die Zeilen mit `map()` und stabilen IDs als React-Keys.

### Was ist die beste Pagination für eine React-Datentabelle?

Die beste Lösung hängt von der Datenmenge und Datenquelle ab. Für kleine, bereits geladene Arrays ist clientseitige Pagination mit `slice()` am einfachsten. Für große API-Datensätze ist serverseitige Pagination sinnvoller. Wenn zusätzlich Sortierung und Filter dazukommen, ist TanStack Table eine praktische Option.

### Sollte ich Pagination oder Virtualisierung verwenden?

Pagination teilt den Datenbestand in Seiten. Virtualisierung kann dagegen viele vorhandene Zeilen im Browser behalten und nur den sichtbaren Teil rendern. Wenn das Problem vor allem die Anzahl gerenderter DOM-Zeilen ist, kann Virtualisierung helfen. Wenn schon das Laden des gesamten Datensatzes zu teuer ist, brauchst du weiterhin serverseitige Datenabfragen. TanStack Table beschreibt beide Ansätze als unterschiedliche Werkzeuge.

### Wie viele Zeilen sollte eine Seite haben?

Es gibt keine universelle Zahl. Zehn, 20 oder 50 Zeilen sind übliche Produktentscheidungen, aber die richtige Größe hängt von Lesbarkeit, Zeilenhöhe, Arbeitsablauf und Datenmenge ab. Biete bei datenintensiven Anwendungen ruhig eine Auswahl der Seitengröße an und behalte die aktuelle Auswahl im Tabellen-State.

### Brauche ich TanStack Table für React-Pagination?

Nein. Für einfache Pagination reicht React mit `useState`, `slice()` und `map()`. TanStack Table lohnt sich, wenn du mehrere Tabellenfunktionen zuverlässig kombinieren willst oder serverseitige Pagination über einen kontrollierten Tabellen-State abbilden möchtest.

### Kann VP0 die Pagination für meine React-Tabelle bauen?

VP0 liefert Design-Startpunkte für iOS-Apps, nicht die Geschäftslogik einer React-Web-Tabelle. Für eine iOS-App kannst du einen VP0-Screen als visuelle Grundlage verwenden, die Pagination oder API-Logik implementierst du aber im eigentlichen Projekt.
