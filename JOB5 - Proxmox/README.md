# Installer Proxmox VE 8.1

    Brancher la Clé USB sur votre serveur
    Démarrer la machine en prenant soin de « Booter » sur la Clé USB
        Voir la documentation du Bios de votre Carte mère
![alt text](images/proxmox_installer.webp) 
Sélectionner « Install Proxmox VE (Graphical) ».
Cliquer sur « I agree » (si vous acceptez les conditions d’utilisation).
Sélectionner le disque sur lequel sera installé Proxmox VE.
Cliquer sur « Options » pour configurer le partitionnement.
– Sélectionner le « Filesystem » par défaut « ext4 » (ou un autre si besoin).
– Définir une taille maximale « maxroot » pour le volume logique qui contiendra le système (Ex : 20 GB). Si aucune valeur n’est définie pour « maxroot », 1/4 du disque sera utilisé (ne pas définir cette valeur entraînerait un gaspillage plus ou moins important selon la taille des disques).
– Cliquer sur « Next ».
Pour plus d’informations, consulter : Options de configuration avancées sur le site officiel.
Sélectionner la langue et les autres options de region.
Cliquer sur « Next ».
Renseigner un mot de passe pour l’utilisateur root et l’adresse e-mail de réception pour les alertes.
Cliquer sur « Next ».
Sélectionner l’interface réseau.
Renseigner le nom de machine et la configuration réseau.
Cliquer sur « Next ».
Vérifier le résumé et cliquer sur « Install ».
Une fois l’installation terminée, le terminal s’affiche.

L’interface de Proxmox VE est accessible depuis un navigateur web.
Il faudra utiliser l’adresse présente sur la page de démarrage.
https://AdresseIPProxmoxVe:8006
Ce message risque de s’afficher car le certificat n’est pas valide.
Cela n’empêche pas le fonctionnement de Proxmox VE.
Le message peut être ignoré si vous accédez à Proxmox VE depuis un réseau fiable.

# Présentation de l’interface

L’interface est découpée en 5 régions :

    L’entête qui indique la version de PVE mais surtout comporte des boutons pour créer des VMS et des containers dans le cluster. C’est également ici que se trouve les configurations et actions liées à l’interface web.
    Liste hiérarchique des ressources administrables.
    Éléments (administrables ou non) spécifiques à la ressource sélectionnée à gauche (2).
    Informations et actions disponibles pour l’élément sélectionné à gauche (3).
    Affichage des tâches en arrière plan et des logs du cluster.

Pour aller plus loin : Proxmox VE – Graphical User Interface

# Désactiver le message « No valid subscription » dans Proxmox VE

Si vous n’avez pas de licence valide, le message suivant s’affichera à chaque connexion.
Cette fenêtre est générée par le fichier JavaScript localisé dans /usr/share/javascript/proxmox-widget-toolkit/proxmoxlib.js.

Elle n’empêche en rien le bon fonctionnement de Proxmox VE mais si vous souhaitez la désactiver, il faudra neutraliser son affichage dans le code.
Dans notre contexte, il faut agir au niveau des lignes 543 et 544.

Une possibilité serait de remplacer la ligne 543 :
if (res === null || res === undefined || !res || res
par
if (true) { orig_cmd(); } else if (res

Ce qui donnerait en lignes de commandes :
Default
Modification du fichier proxmoxlib.js
```bash
sed -Ezi.bak "s/if \(res === null \|\| res === undefined \|\| \!res \|\| res/if (true) { orig_cmd(); } else if (res/gi" /usr/share/javascript/proxmox-widget-toolkit/proxmoxlib.js
```
Redémarrage du service de l'interface web
```bash
systemctl restart pveproxy.service
```

Le message d’avertissement ne s’affichera plus lors des prochaines connexions à Proxmox VE. Une déconnexion puis reconnexion seront peut-être nécessaires ainsi qu’un rafraîchissement du cache du navigateur (généralement Ctrl + F5)

Remarque : Il est possible que le message s’affiche de nouveau après une mise à jour de Proxmox VE. Il faudra donc ré-exécuter la commande.

# Dépôt Proxmox VE No-Subscription

Par défaut, PVE est installé avec le dépôt « Enterprise » activé.
Si vous ne possédez pas de licence valide, PVE affichera un message d’avertissement dans le menu « Repositories » et la mise à jour dans le menu « Updates » ne fonctionneront pas.
## Désactiver le dépôt Enterprise
## Ajouter dépôt No-Subscription

# Créer une machine virtuelle dans Proxmox VE
## Upload d’un ISO

La machine virtuelle aura besoin d’un ISO pour installer son système d’exploitation.
Cliquer sur le stockage nommé « local ».
Cliquer sur « ISO Images » puis « Upload ».
Cliquer sur « Select File » puis sélectionner un fichier ISO sur la machine local.
Cliquer sur « Upload » afin d’uploader l’ISO sur le serveur PVE.
Les messages « finished file import successfully » et « TASK OK » indiquent que l’upload s’est déroulé sans problème.
## Création de la VM
Faire un « clic droit » sur l’hôte de virtualisation sur lequel sera créé la VM.
Cliquer sur « Create VM ».
Ou cliquer directement sur « Create VM » tout en haut de l’interface.

Configurations générales de la VM :
Node : Sélectionner l’hôte de virtualisation du cluster qui hébergera la VM.
VM ID : Identifiant de la VM (Laisser le choix par défaut).
Name : Nom de la VM.

Système d’exploitation de la VM :
1- Sélectionner l’ISO qui servira à installer l’OS.
2- Sélectionner le type d’OS.
3- Sélectionner la version de l’OS.

Hardware de la VM :
Configuration hardware et BIOS de la VM.

Stockage de la VM :
1- Sélectionner l’emplacement où sera stocké le disque virtuel.
2- Définir une taille pour le disque virtuel.

Processeurs la VM :
1- Définir le nombre de sockets CPUs (il est préférable de laisser à 1 et de jouer plutôt sur les cœurs).
2- Nombre de cœurs par processeurs.

RAM de la VM :
1- Définir quantité de RAM.

Configurations réseaux de la VM :
Configurations réseaux (laisser par défaut si aucun besoin spécifique).

Résumé de la configuration de la VM :
Cliquer sur « Finish » si la configuration est correcte.
## Démarrage de la VM
Faire un clic droit sur la VM puis cliquer sur « Console ».
Ou, cliquer directement sur « Console » en haut à droite.
Cliquer sur « Start Now » pour démarrer la VM.
Le programme d’installation de Debian devrait s’afficher.
Pour la suite de l’installation de Debian, se rendre sur Installer Debian 11.

Démarrer automatiquement la VM :
Cocher la case « Start at boot » si il faut que la VM soit démarrée automatiquement au lancement de Proxmox VE.

Pour aller plus loin : QEMU/KVM Virtual Machines

# Créer un cluster Proxmox VE

Installer un nouvel hôte de virtualisation en revenant au début du tutoriel puis revenir à cette étape.
## Création du cluster
Sur l’un des hôtes de virtualisation :
– Cliquer sur « Datacenter » dans la partie de gauche.
– Sélectionner « Cluster » dans la partie du milieu.
– Cliquer sur « Create Cluster ».
– Renseigner le nom du cluster dans « Cluster Name ».
– Sélectionner l’interface réseau qui sera utilisée pour les échanges avec le cluster (Il est recommandé d’utiliser une interface dédiée pour cet usage).
– Cliquer sur « Create ».
Cliquer sur « Join Information » pour obtenir la chaine qui permettra d’ajouter une nouvelle machine au cluster.
## Ajouter un hôte de virtualisation au cluster
Sur un autre hôte de virtualisation :
– Sélectionner « Datacenter ».
– Sélectionner « Cluster ».
– Cliquer sur « Join Cluster ».
– Coller dans le champ « information », la chaine copiée précédemment.
– Renseigner le mot de passe root dans « Password ».
– Sélectionner une interface réseau pour la communication avec le cluster (Il est recommandé d’utiliser une interface dédiée pour cet usage).
– Cliquer sur « Join ‘NomDuCluster' ».

Remarque : Un rechargement de la page peut être nécessaire.
Après rechargement de la page :
La machine a été ajoutée au cluster.
Le panneau de gauche affiche maintenant le nom du cluster.
Les 2 hôtes de virtualisation sont maintenant visibles et administrables depuis l’interface web.