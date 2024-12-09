# Azure virtual networking

Azure virtual networks provide the following key networking capabilities:

- Isolation and segmentation
- Internet communications
- Communicate between Azure resources
- Communicate with on-premises resources
- Route network traffic
- Filter network traffic
- Connect virtual networks

## Communicate between Azure resources

- Virtual networks can connect not only VMs but other Azure resources, such as the App Service Environment for Power Apps, Azure Kubernetes Service, and Azure virtual machine scale sets.
- Service endpoints can connect to other Azure resource types, such as Azure SQL databases and storage accounts. This approach enables you to link multiple Azure resources to virtual networks to improve security and provide optimal routing between resources.

## Azure VNet mit Subnet konfigurieren

### 1. Basis Informationen festlegen

- Name: Gib deinem VNet einen eindeutigen Namen, z. B. MyVNet.
- Region: Wähle die Region aus, in der das VNet erstellt werden soll (z. B. West Europe).
- Abonnement: Wähle das passende Azure-Abonnement.
- Ressourcengruppe: Lege eine neue Ressourcengruppe an oder wähle eine vorhandene aus.
### 2. Adressraum festlegen
Unter IP-Adressraum kannst du den Adressbereich des VNets angeben, z. B. 10.0.0.0/16.

-> /16 = 32-16=16, also 2^16=65.536 verfügbare IP-Adressen (2 sind aber vorreserviert)

Dieser Adressraum wird später in Subnetze unterteilt.
### 3. Subnetze definieren
Erstes Subnet hinzufügen:

Unter Subnetze füge ein Subnetz hinzu, z. B.:
- Frontend-Subnet: 10.0.1.0/24

Du kannst weitere Subnetze hinzufügen, z. B.:
- Backend-Subnet: 10.0.2.0/24

## Azure VPN & VPN Gateway

- A virtual private network (VPN) uses an encrypted tunnel within another network
- VPNs are typically deployed to connect two or more trusted private networks to one another over an untrusted network (typically the public internet)
- You can deploy only one VPN gateway in each virtual network
- When setting up a VPN gateway, you must specify the type of VPN - either policy-based or route-based

### Policy-based VPN gateways
Policy-based VPN gateways specify statically the IP address of packets that should be encrypted through each tunnel. This type of device evaluates every data packet against those sets of IP addresses to choose the tunnel where that packet is going to be sent through.

### Route-based gateways
In Route-based gateways, IPSec tunnels are modeled as a network interface or virtual tunnel interface. IP routing (either static routes or dynamic routing protocols) decides which one of these tunnel interfaces to use when sending each packet. Route-based VPNs are the preferred connection method for on-premises devices. They're more resilient to topology changes such as the creation of new subnets.


Use a route-based VPN gateway if you need any of the following types of connectivity:

- Connections between virtual networks
- Point-to-site connections
- Multisite connections
- Coexistence with an Azure ExpressRoute gateway

## Azure ExpressRoute

Azure ExpressRoute lets you extend your on-premises networks into the Microsoft cloud over a private connection, with the help of a connectivity provider. This connection is called an ExpressRoute Circuit. With ExpressRoute, you can establish connections to Microsoft cloud services, such as Microsoft Azure and Microsoft 365. This feature allows you to connect offices, datacenters, or other facilities to the Microsoft cloud. Each location would have its own ExpressRoute circuit.

## Azure DNS

- Azure DNS can manage DNS records for your Azure services and provide DNS for your external resources as well