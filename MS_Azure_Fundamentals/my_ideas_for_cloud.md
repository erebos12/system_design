# Cloud-Strategie für MS Azure


## Cloud Act und Microsoft

siehe https://news.microsoft.com/de-de/im-daten-dschungel-wie-microsoft-mit-dem-cloud-act-umgeht/?utm_source=chatgpt.com

##  Pricing
- Allgeminer Vergleich CapEx und OpEx mit On-Prem vs. Cloud-Lösung
    - Vergleich der Kosten eigenes Rechenzentrum und Cloud
    - Immer dran denken: "Du must mindestens so gut (sicher) sein wie Microsoft!", wenn du alles selbst betreibst
- TCO Claculator
    - Vergleich mit On-Prem Kosten
- Pricing Calculator
    - Kosten-Kalkulator allgemein
- Cost Management-Tool
    - laufende Kosten überwachen

##  Monitoring / Management von Cloud-Resourcen
- Azure Resource Manager (ARM)
    - Infrastructure-as-Code in Azure
- Resourcegroups & Tags
    - Strukturierung von Cloud-Resourcen
- Azure Arc (Unified Management System)
    - Cloud Management und Überwachung von Nicht-Cloud und Cloud-Resourcen
    - Aktuell können mit Azure Arc folgende außerhalb von Azure gehostete Ressourcentypen verwaltet werden:
        - Server
        - Kubernetes-Cluster
        - Azure-Datendienste
        - SQL Server
        - VMs (Vorschau)
- Microsoft Purview 
    - Daten-Compliance Management
    - Risiko und Compliance sowie einheitliche Datengovernance
- Azure-Policy
    - Regeln/Richtlinien für Ressourcenkonfigurationen erzwingen, damit diese Konfigurationen stets mit Ihren Unternehmensstandards konform bleiben
    - Azure Policy-Initiative ist eine Möglichkeit, verwandte Richtlinien zu gruppieren
- Ressourcensperren
    - Eine Ressourcensperre verhindert, dass Ressourcen versehentlich gelöscht oder geändert werden
- Service Trust Portal (nur Website)
    - Siehe https://servicetrust.microsoft.com/ 
- Azure Advisor
    - Analyse von Azure-Ressourcen und Empfehlungen 
    - Cloudoptimierung
    - Hilft sie dabei zu unterstützen, die Zuverlässigkeit, Sicherheit und Leistung zu verbessern sowie erstklassige Betriebsprozesse zu erzielen und Kosten zu reduzieren.
- Azure Monitor
    - Azure Monitor ist eine Plattform für das Sammeln von Daten zu Ihren Ressourcen, die Analyse dieser Daten, die Visualisierung der Informationen und sogar die Reaktion auf die Ergebnisse


## Clouddiensttypen (SaaS, PaaS, IaaS, On-prem)

![alt text](image.png)

##  Running Applications in Azure

Möglich über:

- Azure VMs
- Azure Container
- Azure Kubernetes Service (AKS) 
- Azure App Services
    - autom. Deployment von Binaries/Apps
    - bietet Bereitstellung der Laufzeitumgebung, Starten der Anwendung und Skalierung und Verwaltung

## Azure Networking
- Azure VNet
- Azure VPN & VPN Gateway
- Azure ExpressRoute
- Azure DNS

## Azure Storage Services

- you name it...

## Azure Identity, access and security

### Microsoft Entra ID

