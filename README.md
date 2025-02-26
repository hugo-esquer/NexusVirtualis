# Job 1
## Différence entre hyperviseurs de type 1 et type 2
Un hyperviseur est un logiciel qui permet de créer et gérer des machines virtuelles (VM). Il existe deux types d’hyperviseurs :  
Hyperviseur de type 1 ("bare-metal") : Il s’exécute directement sur le matériel physique, sans système d’exploitation sous-jacent. Il gère directement les ressources matérielles et les VM.  
Exemples : VMware ESXi, Microsoft Hyper-V (mode serveur), KVM, Xen.  
Hyperviseur de type 2 ("hosted") : Il s’exécute au-dessus d’un système d’exploitation hôte (Windows, Linux, macOS) et utilise ce dernier pour gérer l’accès aux ressources matérielles.  
Exemples : VMware Workstation, VirtualBox, Microsoft Hyper-V (mode client).  
## Avantages et inconvénients des hyperviseurs de type 1
### Avantages
- Performance optimisée : Accès direct au matériel, sans intermédiaire.
- Sécurité renforcée : Moins de surface d’attaque qu’un OS complet.
- Fiabilité et stabilité : Conçu pour l’exécution en continu de VM.
- Meilleure gestion des ressources : Supporte des fonctionnalités avancées (haute disponibilité, migration à chaud, snapshots, etc.).
### Inconvénients
- Complexité de gestion : Nécessite des compétences en virtualisation et en administration système.
- Coût potentiel élevé : Certaines solutions comme VMware ESXi avec fonctionnalités avancées sont coûteuses.
- Compatibilité matérielle : Certains hyperviseurs (ex. ESXi) nécessitent un matériel certifié.
### Cas d'utilisation typiques
 - Datacenters et cloud computing : AWS, Azure, Google Cloud utilisent des hyperviseurs de type 1 pour offrir des infrastructures virtuelles.
 - Serveurs virtualisés en entreprise : Consolidation des services sur un nombre réduit de serveurs physiques (ex. Active Directory, bases de données, applications métiers).
 - Environnements critiques : Solutions nécessitant haute disponibilité et continuité de service (ex. banques, santé, industrie).
 - Tests et développement : Bien que les hyperviseurs de type 2 soient souvent utilisés pour les tests, les grandes entreprises préfèrent les hyperviseurs de type 1 pour simuler des environnements de production.
# Job 2
## ESXI 8
Pour télécharger  l’image d’ESXI, vous aurez besoin d’un compte VMWarte Customer Connect. Une fois le compte créer vous pourrez naviguer dans la section vSphère et sélectionner l’ISO VMware vSphère Hypervisor (ESXI ISO) image à la version 8.0.3 P04.

## Hyper_V
L’image iso d’hyper v est directement disponible sur me site de microsoft.com

## Proxmox VE
L’image de Proxmox est disponible a cette adresse https://www.proxmox.com/en/downloads/proxmox-virtual-environment/iso

## XCP-ng
Vous pouvez télécharger la dernière version de XCP-ng 8.3 ici https://mirrors.xcp-ng.org/isos/8.3/xcp-ng-8.3.0.iso?https=1.
