# Azure Resource Manager und Azure ARM-Vorlagen

Mit Azure Resource Manager können Sie folgende Aktionen ausführen:

- Verwalten Ihrer Infrastruktur über deklarative Vorlagen (anstelle von Skripts) Eine Resource Manager-Vorlage ist eine JSON-Datei, mit der definiert wird, was Sie in Azure bereitstellen möchten.
- Bereitstellen, Verwalten und Überwachen aller Ressourcen für Ihre Lösung als Gruppe, anstatt diese Ressourcen einzeln zu behandeln
- Sie können Ihre Lösung während des Entwicklungszyklus erneut bereitstellen und sicher sein, dass Ihre Ressourcen in einem konsistenten Zustand bereitgestellt werden.
- Sie können die Abhängigkeiten zwischen Ressourcen definieren, damit diese in der richtigen Reihenfolge bereitgestellt werden.
- Wenden Sie die Zugriffssteuerung auf alle Dienste an, da RBAC nativ in die Verwaltungsplattform integriert ist.
- Anwenden von Tags auf Ressourcen, um alle Ressourcen in Ihrem Abonnement logisch zu organisieren
- Sie können genauere Informationen zur Abrechnung Ihrer Organisation erhalten, indem Sie die Kosten für eine Gruppe von Ressourcen anzeigen, die über dasselbe Tag verfügen.



### **Ähnlichkeiten zu Terraform**
1. **Deklarative Konfiguration:** Beide Tools verwenden deklarative Vorlagen, um Ressourcen zu definieren und bereitzustellen.
   - ARM: JSON-Vorlagen
   - Terraform: HCL (HashiCorp Configuration Language)
2. **Infrastrukturautomatisierung:** Beide ermöglichen die automatisierte Bereitstellung, Verwaltung und Aktualisierung von Cloud-Ressourcen.
3. **Versionskontrolle:** Konfigurationsdateien können in Versionskontrollsystemen wie Git verwaltet werden.
4. **Planung und Vorschau:** Beide bieten Funktionen, um die Änderungen vor der Bereitstellung zu überprüfen (Terraform: `terraform plan`, ARM: Bereitstellungsvorschau).
5. **Multi-Cloud-Strategie:** Beide Tools können Cloud-Ressourcen verwalten, aber Terraform ist hier flexibler.

### **Unterschiede**

| Merkmal                | **Azure Resource Manager (ARM)**                              | **Terraform**                                               |
|------------------------|--------------------------------------------------------------|-------------------------------------------------------------|
| **Zweck**              | Speziell für Azure entwickelt                                | Plattformunabhängig, unterstützt mehrere Cloud-Anbieter     |
| **Sprache**            | JSON                                                         | HCL (einfacher und lesbarer als JSON)                      |
| **Multi-Cloud-Support**| Nur für Azure                                                | Unterstützt Azure, AWS, GCP und viele andere Anbieter      |
| **State Management**   | Kein separates Zustandsmanagement                            | Verwendet eine **state file**, um den aktuellen Stand zu verfolgen |
| **Flexibilität**       | Stärker auf Azure-Dienste spezialisiert                      | Flexible, anbieterübergreifende Infrastrukturverwaltung     |
| **Community-Support**  | Fokus auf Azure-Ökosystem                                    | Große Community, zahlreiche Module und Plugins             |
| **Tool-Integration**   | In Azure integriert, z. B. Azure-Portal und CLI              | Eigenständig, aber in andere Tools integrierbar            |

### **Zusammenfassung**
- **Azure Resource Manager** eignet sich hervorragend, wenn Sie ausschließlich in Azure arbeiten und die volle Integration mit dem Azure-Ökosystem wünschen.
- **Terraform** ist die bessere Wahl, wenn Sie eine Multi-Cloud-Strategie verfolgen oder eine einfachere und flexiblere Sprache bevorzugen. 

Falls Sie ausschließlich in Azure arbeiten, können ARM-Vorlagen einfacher zu nutzen sein. Wenn Sie jedoch eine größere Plattformunabhängigkeit oder erweiterte Möglichkeiten möchten, ist Terraform die universellere Lösung.