# Grundlegendes zu Azure-Features und -Tools für Governance und Compliance

## Lernziele
Nach Abschluss dieses Moduls können Sie folgende Aufgaben durchführen:

- Beschreiben des Zwecks von Microsoft Purview
- Beschreiben des Zwecks von Azure Policy
- Beschreiben des Zwecks von Ressourcensperren
- Beschreiben des Zwecks des Service Trust Portal

## Microsoft Purview

Microsoft Purview handelt es sich um eine Familie von Datengovernance-, Risiko- und Compliancelösungen, mit denen Sie einen zentralen, einheitlichen Überblick über Ihre Daten erhalten können. Microsoft Purview bietet Erkenntnisse über Ihre lokalen Daten, Multi-Cloud- und Software-as-a-Service-Daten.

Mit Microsoft Purview können Sie ihre Datenlandschaft dank folgender Funktionen auf dem neuesten Stand halten:

- Automatisierte Datenermittlung
- Klassifizierung vertraulicher Daten
- Vollständige Datenherkunft

Durch die Verwaltung und Überwachung Ihrer Daten kann Microsoft Purview Ihre Organisation wie folgt unterstützen:

- Schützen von vertraulichen Daten in Clouds, Apps und auf Geräten
- Identifizieren von Datenrisiken und Verwalten gesetzlicher - Complianceanforderungen
- Erste Schritte mit der Einhaltung gesetzlicher Bestimmungen

### Einheitliche Datengovernance
Microsoft Purview bietet robuste, einheitliche Lösungen für Datengovernance, mit der Sie Ihre lokalen, Multi-Cloud- und SaaS-Daten (Software-as-a-Service) verwalten können. Mit den robusten Datengovernancefunktionen von Microsoft Purview können Sie Ihre in Azure-, SQL- und Hive-Datenbanken gespeicherten Daten lokal und sogar in anderen Clouds wie Amazon S3 verwalten.

Die einheitliche Datengovernance von Microsoft Purview ermöglicht Ihrer Organisation Folgendes:

- Erstellen einer aktuellen Übersicht Ihres gesamten Datenbestands, einschließlich Datenklassifizierung und End-to-End-Herkunft
- Ermitteln, wo vertrauliche Daten in Ihrem Datenbestand gespeichert sind
- Erstellen einer sicheren Umgebung für Datenconsumer, um wertvolle Daten zu finden
- Generieren von Erkenntnissen darüber, wie Ihre Daten gespeichert und verwendet werden
- Sicheres Verwalten des Zugriffs auf die Daten in Ihrem Datenbestand im benötigten Umfang


## Azure Policy

Wie stellen Sie sicher, dass Ihre Ressourcen konform bleiben? Wie können Sie benachrichtigt werden, wenn sich die Konfiguration einer Ressource geändert hat?

Azure Policy ist ein Dienst in Azure, der es Ihnen ermöglicht, Richtlinien zu erstellen, zuzuweisen und zu verwalten, die Ihre Ressourcen steuern oder überwachen. Mit diesen Richtlinien werden unterschiedliche Regeln für Ressourcenkonfigurationen erzwungen, damit diese Konfigurationen stets mit Ihren Unternehmensstandards konform bleiben.

Mit Azure Policy können Sie sowohl einzelne Richtlinien als auch Gruppen verwandter Richtlinien definieren, die als Initiativen bezeichnet werden.

Azure Policy enthält integrierte Richtlinien- und Initiativendefinitionen für Speicher, Netzwerk, Compute, Security Center und Überwachung.

### Azure Policy-Initiativen

Eine Azure Policy-Initiative ist eine Möglichkeit, verwandte Richtlinien zu gruppieren. Eine Initiativendefinition enthält alle Richtliniendefinitionen, um Ihren Konformitätsstatus zur Erreichung eines größeren Ziels besser nachverfolgen können.

Im Rahmen einer Initiative sind die folgenden Richtliniendefinitionen enthalten:

- Überwachung von unverschlüsselten SQL-Datenbanken in Security Center: Diese Richtlinie dient zum Überwachen von unverschlüsselten SQL-Datenbanken und -Servern.
- Überwachung von Betriebssystem-Sicherheitsrisiken in Security Center: Diese Richtlinie überwacht Server, welche die konfigurierte Sicherheitsrisikobaseline des Betriebssystems nicht erfüllen.
- Überwachung des fehlenden Endpoint Protection-Schutzes in Security Center: Diese Richtlinie überwacht Server, auf denen kein Endpoint Protection-Agent installiert ist.

### Ressourcensperren

- Eine Ressourcensperre verhindert, dass Ressourcen versehentlich gelöscht oder geändert werden.

- Ressourcensperren können auf einzelne Ressourcen, Ressourcengruppen oder sogar ein gesamtes Abonnement angewendet werden

#### Typen

1. Löschen: Können nicht gelöscht werden, aber geändert werden
2. ReadOnly: Nur lesen

#### Sperre aufheben

Um eine gesperrte Ressource zu ändern, müssen Sie zunächst die Sperre entfernen. Nachdem Sie die Sperre entfernt haben, können Sie jede beliebige Aktion anwenden, die Sie ausführen dürfen. Ressourcensperren gelten unabhängig von RBAC-Berechtigungen. Selbst wenn Sie Besitzer der Ressource sind, müssen Sie die Sperre aufheben, ehe Sie die blockierte Aktivität tatsächlich durchführen können.

## Service Trust Portal

Über Microsoft Service Trust Portal erhalten Sie Zugriff auf eine Vielfalt an Inhalten, Tools und weiteren Ressourcen zu den Themen Sicherheit, Datenschutz und Compliance bei Microsoft.

Siehe https://servicetrust.microsoft.com/