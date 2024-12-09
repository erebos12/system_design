
----------

### 1. **TOCTOU-Schwachstellen (Time-of-Check to Time-of-Use)**

-   **Was ist das?** Ein Angreifer manipuliert Ressourcen (z. B. Dateien) zwischen einer Überprüfung (`Check`) und ihrer Nutzung (`Use`), um unerwartete Änderungen zu bewirken.
-   **Beispiel:**
    
    ```java
    File tempFile = new File("/tmp/tempfile.txt");
    if (!tempFile.exists()) { // Time-of-Check
        tempFile.createNewFile(); // Time-of-Use
    }
    
    ```
    
    Während des Zeitfensters könnte ein Angreifer einen symbolischen Link erstellen, der auf eine andere Datei zeigt.
-   **Abhilfe:**
    -   Atomare Dateioperationen verwenden, z. B. `Files.createTempFile()`.
    -   Zugriff auf Ressourcen strikt beschränken.

----------

### 2. **SQL-Injection**

-   **Was ist das?** Unsichere Benutzereingaben werden direkt in SQL-Statements eingefügt, wodurch ein Angreifer das Verhalten der Datenbank manipulieren kann.
-   **Abhilfe:** Prepared Statements oder ORMs verwenden.

----------

### 3. **Cross-Site Scripting (XSS)**

-   **Was ist das?** Ein Angreifer führt schädliches JavaScript im Kontext eines anderen Benutzers aus.
-   **Abhilfe:** Eingaben und Ausgaben validieren/escapen.

----------

### 4. **Buffer Overflow**

-   **Was ist das?** Ein Angreifer überschreibt Speicherbereiche, um Code auszuführen oder Daten zu manipulieren.
-   **Abhilfe:** Längen von Eingaben überprüfen.

----------

### 5. **Unzureichende Input-Validierung**

-   **Was ist das?** Eingaben werden nicht auf unerwartete oder schädliche Werte geprüft.
-   **Abhilfe:** Whitelisting und Validierung verwenden.

----------

### 6. **Cross-Site Request Forgery (CSRF)**

-   **Was ist das?** Ein Angreifer täuscht einem Benutzer vor, eine Aktion unbewusst auszuführen.
-   **Abhilfe:** CSRF-Tokens verwenden.

----------

### 7. **Hardcoded Credentials**

-   **Was ist das?** Passwörter oder API-Schlüssel werden im Quellcode gespeichert.
-   **Abhilfe:** Secrets in sicheren Mechanismen wie Vaults speichern.

----------

### 8. **Directory Traversal**

-   **Was ist das?** Ein Angreifer greift durch manipulierte Pfade auf unautorisierte Dateien zu.
-   **Abhilfe:** Eingaben normalisieren und validieren.

----------

### 9. **Unverschlüsselte Kommunikation**

-   **Was ist das?** Daten werden ohne TLS/HTTPS übertragen und können abgefangen werden.
-   **Abhilfe:** Verschlüsselung verwenden.

----------

### 10. **Insecure Deserialization**

-   **Was ist das?** Ein Angreifer manipuliert serialisierte Daten, um schädlichen Code auszuführen.
-   **Abhilfe:** Deserialisierung auf sichere Datenformate beschränken.

----------

### 11. **Unzureichende Logging und Monitoring**

-   **Was ist das?** Angriffe bleiben unbemerkt, weil keine ausreichenden Logs existieren.
-   **Abhilfe:** Sicherheitsrelevante Ereignisse protokollieren und überwachen.

----------

### 12. **Sensitive Data Exposure**

-   **Was ist das?** Sensible Informationen werden im Klartext gespeichert oder übertragen.
-   **Abhilfe:** Hashing und Verschlüsselung verwenden.

----------

### 13. **Race Conditions**

-   **Was ist das?** Mehrere Threads oder Prozesse greifen gleichzeitig auf dieselbe Ressource zu, was zu unvorhergesehenen Zuständen führt.
-   **Abhilfe:** Zugriffssynchronisation und atomare Operationen verwenden.

----------

### 14. **Unsicherer Umgang mit Ressourcen**

-   **Was ist das?** Ressourcen wie Dateien oder Verbindungen werden nicht korrekt geschlossen.
-   **Abhilfe:** `try-with-resources` in Java verwenden.

----------

### 15. **Nicht verwendete Sicherheitsmechanismen**

-   **Was ist das?** Sicherheitsfeatures wie Content Security Policies oder Secure Cookies werden nicht genutzt.
-   **Abhilfe:** Plattform-Sicherheitsmechanismen aktivieren.

----------
Natürlich! Hier sind **weitere Schwachstellen** über die bisherigen 15 hinaus. Diese decken verschiedene Sicherheitsbereiche ab und sind wichtig für sicheres Programmieren:

---

### 16. **Privilege Escalation**
- **Was ist das?** Ein Angreifer erhöht unberechtigt seine Berechtigungen in einem System.
- **Beispiel:** Ein Angreifer nutzt Schwachstellen in unsicheren APIs, um Admin-Zugriff zu erlangen.
- **Abhilfe:** Least-Privilege-Prinzip (Minimalrechte) und rollenbasierte Zugriffssteuerung (RBAC) implementieren.

---

### 17. **Session Hijacking**
- **Was ist das?** Ein Angreifer stiehlt oder manipuliert eine gültige Benutzersitzung (z. B. durch gestohlene Cookies).
- **Abhilfe:** 
  - Sitzungscookies mit `Secure` und `HttpOnly` markieren.
  - Session-IDs regelmäßig rotieren.

---

### 18. **Unzureichende Passwortsicherheit**
- **Was ist das?** Schwache oder unsichere Passwörter werden verwendet.
- **Abhilfe:** 
  - Passwort-Hashes mit `bcrypt` oder `Argon2` speichern.
  - Passwort-Richtlinien und Zwei-Faktor-Authentifizierung (2FA) durchsetzen.

---

### 19. **Clickjacking**
- **Was ist das?** Ein Angreifer überlagert eine legitime Benutzeroberfläche mit einer unsichtbaren Schicht, um Klicks zu manipulieren.
- **Abhilfe:** 
  - HTTP-Header `X-Frame-Options: DENY` verwenden.
  - Content Security Policies (CSP) implementieren.

---

### 20. **Unsicherer Umgang mit Dateien**
- **Was ist das?** Dateien werden unkontrolliert hochgeladen oder verarbeitet.
- **Abhilfe:**
  - Dateien vor dem Hochladen validieren (Dateitypen und Größe).
  - Hochgeladene Dateien niemals direkt ausführen oder speichern, sondern in sicheren Ordnern.

---

### 21. **Cryptographic Failures (unsichere Verschlüsselung)**
- **Was ist das?** Falsche oder veraltete Verschlüsselungsalgorithmen werden verwendet.
- **Beispiel:** Nutzung von MD5 oder SHA-1.
- **Abhilfe:** 
  - Nur starke Algorithmen wie AES-256 oder SHA-256 verwenden.
  - Zertifikate regelmäßig aktualisieren.

---

### 22. **Unkontrollierte Weiterleitungen (Open Redirects)**
- **Was ist das?** Ein Angreifer manipuliert Weiterleitungen, um Benutzer auf schädliche Seiten zu lenken.
- **Abhilfe:**
  - Ziel-URLs immer validieren und auf bekannte Domains beschränken.

---

### 23. **Unsicherer Umgang mit Third-Party Libraries**
- **Was ist das?** Verwundbare Abhängigkeiten oder unsichere Third-Party-Bibliotheken werden verwendet.
- **Abhilfe:** 
  - Sicherheitsüberprüfungen von Abhängigkeiten (z. B. `OWASP Dependency Check`).
  - Veraltete Bibliotheken regelmäßig aktualisieren.

---

### 24. **Zugriff auf Debugging- oder Entwicklungsfunktionen**
- **Was ist das?** Debugging-Endpoints oder Test-Accounts sind in der Produktion verfügbar.
- **Abhilfe:** 
  - Debugging-Funktionen in Produktionsumgebungen deaktivieren.
  - Test-Daten und Accounts entfernen.

---

### 25. **Eingebetteter Schadcode (Malware in Software)**
- **Was ist das?** Schadcode wird in einer Anwendung versteckt und kann unerwartet ausgeführt werden.
- **Abhilfe:** 
  - Code Reviews und statische Analyse-Tools verwenden.
  - Nur vertrauenswürdige Quellen für Abhängigkeiten nutzen.

---

### 26. **Broken Access Control**
- **Was ist das?** Benutzer greifen unberechtigt auf Ressourcen zu, weil die Zugriffssteuerung fehlerhaft ist.
- **Abhilfe:** 
  - Zugriffskontrollen zentral implementieren.
  - Autorisierungsprüfungen für jede sensible Aktion durchführen.

---

### 27. **Missing Security Headers**
- **Was ist das?** Wichtige HTTP-Sicherheitsheader fehlen, z. B. `Content-Security-Policy` oder `Strict-Transport-Security`.
- **Abhilfe:** Sicherheitsheader wie HSTS, CSP, und X-Frame-Options konsequent nutzen.

---

### 28. **Unsichere Standardkonfigurationen**
- **Was ist das?** Anwendungen oder Frameworks werden mit unsicheren Standardeinstellungen ausgeliefert.
- **Abhilfe:** 
  - Sicherheitsbest Practices anwenden (z. B. deaktivierte Ports, strikte Firewall-Regeln).
  - Konfiguration regelmäßig überprüfen.

---

### 29. **Log Injection**
- **Was ist das?** Ein Angreifer manipuliert Logs, um falsche Informationen einzuschleusen oder Angriffe zu verschleiern.
- **Beispiel:** Ein Angreifer fügt Log-Einträge wie `"\n[ERROR] Access Denied"` hinzu.
- **Abhilfe:** Log-Eingaben escapen und strukturierte Logs verwenden.

---

### 30. **Unsichere Verwendung von Umgebungsvariablen**
- **Was ist das?** Sensible Informationen wie API-Schlüssel werden ungeschützt in Umgebungsvariablen gespeichert.
- **Abhilfe:** Geheimnisse in sicheren Speichern (z. B. Vault) verwalten und Umgebungsvariablen minimieren.

---

### 31. **Eingabemanipulation über Header**
- **Was ist das?** Ein Angreifer manipuliert HTTP-Header, um z. B. unerlaubten Zugriff zu erhalten.
- **Abhilfe:** 
  - Eingaben in HTTP-Headern (z. B. `User-Agent`, `Referer`) validieren.
  - Keine sensiblen Entscheidungen basierend auf Header-Daten treffen.

---

### 32. **Insufficient Transport Layer Security**
- **Was ist das?** Unsichere Protokolle wie HTTP oder veraltete TLS-Versionen werden verwendet.
- **Abhilfe:** 
  - Nur TLS 1.2 oder höher erlauben.
  - Zertifikate regelmäßig erneuern.

---

### 33. **Unsichere API-Implementationen**
- **Was ist das?** APIs haben schwache Authentifizierung oder zu breite Berechtigungen.
- **Abhilfe:** 
  - API-Schlüssel verwenden und Zugriff granular steuern.
  - OAuth2/OpenID für Authentifizierung einsetzen.

---

### 34. **Integer Overflow/Underflow**
- **Was ist das?** Zahlenoperationen führen zu unerwarteten Ergebnissen, z. B. durch Überlauf.
- **Abhilfe:** Wertebereiche für numerische Eingaben prüfen.

---

### 35. **Resource Exhaustion (Denial of Service)**
- **Was ist das?** Ein Angreifer erschöpft Ressourcen wie Speicher, CPU oder Netzwerkbandbreite.
- **Abhilfe:** 
  - Ratenbegrenzung (Rate Limiting) und Zeitlimits für Anfragen implementieren.
  - Ressourcenverbrauch überwachen.

---

### 36. **Server-Side Request Forgery (SSRF)**
- **Was ist das?** Ein Angreifer missbraucht den Server, um Anfragen an andere Dienste auszuführen.
- **Abhilfe:** 
  - Zugriffsfilter implementieren.
  - Anfragen auf erlaubte Domains beschränken.

---


