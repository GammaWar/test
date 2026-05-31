# 📢 Server Communication (Technische Spezifikation)

Diese Datei beschreibt die Implementierung der Kommunikation zwischen Client und Server für systemweite Ankündigungen.

---

## 📡 1. API & Kommunikation (`serverAnnouncementApi.js`)

Die Interaktion erfolgt über den `LiveGameService` via WebSockets.

### **A. Funktionen**
*   **`respondToServerAnnouncement(payload)`**: Sendet eine Antwort auf eine vom Server initiierte Ankündigung. Dies wird verwendet, um Bestätigungen oder Reaktionen auf globale Ereignisse zu übermitteln.

---

## ⚙️ 2. Workflow

1.  **Trigger:** Der Server sendet ein Event (z. B. eine globale Nachricht oder ein wichtiges Spielereignis).
2.  **Reaktion:** Der Client empfängt das Event und nutzt `respondToServerAnnouncement`, um den Status der Interaktion an den Server zurückzumelden.


## 🛠️ 3. Bauauftrags-Management (Build Order Thread)

Die Verwaltung von Bauaufträgen erfolgt über einen dedizierten Backend-Thread zur Sicherstellung der Prozessstabilität.

### **A. Stabilität & Fehlerbehebung**
*   **Automatischer Neustart:** Um das Hängenbleiben des Systems zu verhindern, wird der Build-Order-Thread automatisch neu gestartet, falls er für 20 Sekunden keine Aktivität zeigt.
*   **Race Condition Schutz:** Es wurde eine Logik implementiert, die verhindert, dass mehrere Instanzen desselben Threads gleichzeitig gestartet werden (Vermeidung von Duplikaten bei mehrfachen Anfragen).

### **B. Performance-Hinweis**
Die Erstellung neuer Bauaufträge kann unter hoher Last eine gewisse Latenz aufweisen; dies ist ein bekannter Punkt für zukünftige Optimierungen.
