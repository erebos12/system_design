#  Microsoft Azure-Grundlagen: Beschreiben der Azure-Verwaltung und -Governance 

## Lernziele
Nach Abschluss dieses Moduls können Sie folgende Aufgaben durchführen:

- Beschreiben von Faktoren, die sich auf die Kosten in Azure auswirken können
- Vergleichen von Preis- und Gesamtkostenrechner
- Beschreiben Sie das Microsoft Cost Management Tool
- Beschreiben des Zwecks von Tags

## Wieviel kostet MS Azure ?

### TCO Calculator

- Workload von Services, Storage, Datenbases & Networking  
    - mit TCO Calculator, welcher Kostenerspanisse im Vergleich zur On-Prem Lösung bietet
    - Der Total Cost of Ownership (TCO) Calculator von Microsoft Azure ist ein Online-Tool, das Unternehmen dabei unterstützt, die Gesamtkosten ihrer aktuellen On-Premises-Infrastruktur mit den potenziellen Kosten einer Migration zu Azure zu vergleichen. Ziel ist es, die finanziellen Vorteile und Einsparungen einer Cloud-Migration transparent darzustellen.

### Pricing Calculator

- Kosten basierend auf Auswahl von Subscription, Services, Resources & Third-Party-Splutions 

### Azure Advisor

- Monitoring von aktuellen Kosten in Azure

### Kostenverwaltung mit Cost Management-Tool

Cost Management bietet die Möglichkeit, die Kosten für Azure-Ressourcen schnell zu überprüfen, Warnungen basierend auf Ressourcenausgaben zu erstellen und Budgets zu erstellen, mit denen Sie die Verwaltung von Ressourcen automatisieren können.

Die Kostenanalyse selbst ist nur eine Funktion von Cost Management, die eine schnelle visuelle Darstellung Ihrer Azure-Kosten bietet. Mithilfe der Kostenanalyse können Sie die Gesamtkosten schnell auf verschiedene Arten anzeigen, z. B. nach Abrechnungszeitraum, Region, Ressource usw.

## Beschreiben des Zwecks von Tags

Tags stellen zusätzliche Informationen oder Metadaten zu Ihren Ressourcen bereit. Diese Metadaten eignen sich für:

- Ressourcenverwaltung: Mithilfe von Tags können Sie Ressourcen, die mit bestimmten Workloads, Umgebungen, Geschäftsbereichen und Besitzern verknüpft sind, ermitteln und Aktionen für diese ausführen.

- Kostenverwaltung- und optimierung: Mit Tags können Sie Ressourcen gruppieren, sodass Sie über Kosten berichten, interne Kostenstellen zuweisen, Budgets nachverfolgen und geschätzte Kosten prognostizieren können.

- Vorgangsverwaltung: Mit Tags können Sie Ressourcen entsprechend der Wichtigkeit ihrer Verfügbarkeit für Ihr Unternehmen gruppieren. Diese Gruppierung unterstützt Sie beim Formulieren von Vereinbarungen zum Servicelevel (SLAs). Eine SLA ist eine Betriebszeit- oder Leistungsgarantie zwischen Ihnen und Ihren Benutzern.

- Sicherheit: Mithilfe von Tags können Sie Daten nach ihrer Sicherheitsstufe klassifizieren, z. B. als öffentlich oder vertraulich.

- Governance und Einhaltung gesetzlicher Bestimmungen: Mithilfe von Tags können Sie Ressourcen identifizieren, die den Anforderungen an Governance oder Einhaltung gesetzlicher Vorschriften entsprechen, z. B. ISO 27001. Tags können auch Teil Ihrer Standarddurchsetzungsmaßnahmen sein. Beispielsweise kann es erforderlich sein, dass alle Ressourcen mit einem Besitzer- oder Abteilungsnamen gekennzeichnet werden.

- Optimierung und Automatisierung von Workloads: Mit Tags können Sie alle Ressourcen visualisieren, die Teil komplexer Bereitstellungen sind. Beispielsweise können Sie eine Ressource mit der zugehörigen Workload oder dem Anwendungsnamen markieren und Software wie Azure DevOps zum Ausführen automatisierter Tasks für diese Ressourcen verwenden.

### Wie verwalte ich Ressourcentags?

Sie können Ressourcentags mit Windows PowerShell, der Azure-Befehlszeilenschnittstelle, Azure Resource Manager-Vorlagen, der REST-API oder über das Azure-Portal hinzufügen, ändern oder löschen.

Sie können Azure Policy verwenden, um Taggingregeln und -konventionen zu erzwingen.
