# Paramètres multijoueur

## **1. Général**

??? setting "Afficher les options avancées"

```
Si cette option est activée, tous les paramètres multijoueur seront affichés.

Si cette option est désactivée, seuls les paramètres multijoueur de base seront affichés.
```

??? setting "Activer la protection contre le clonage des configurations"

```
Si cette option est activée, la configuration de votre véhicule ne pourra pas être enregistrée par les autres joueurs.

Si cette option est désactivée, les autres joueurs pourront enregistrer la configuration de votre véhicule.
```

??? setting "Désactiver la mise en pause causée par les instabilités"

```
Si cette option est activée, les instabilités physiques ne mettront pas le jeu en pause.

Si cette option est désactivée, les instabilités physiques mettront le jeu en pause.

!!! note ""

    Il est recommandé de laisser cette option désactivée, car des instabilités répétées peuvent provoquer un crash du jeu.
```

??? setting "Utiliser les véhicules simplifiés lorsqu’ils sont disponibles"

```
Si cette option est activée, le jeu remplacera les véhicules des autres joueurs par leur version simplifiée (provenant du trafic IA) lorsqu’elle est disponible.

Si cette option est désactivée, le jeu utilisera les modèles de véhicules prévus.
```

??? setting "Nouveau menu de chat"

```
Si cette option est activée, le chat en jeu sera affiché dans une fenêtre [IMGUI](https://github.com/ocornut/imgui), qui peut notamment être déplacée en dehors du jeu vers un autre écran.

Si cette option est désactivée, le chat en jeu sera affiché dans l’application d’interface utilisateur.

!!! note ""

    Déplacer les fenêtres IMGUI en dehors de la fenêtre principale du jeu peut entraîner des problèmes de performances et peut également perturber certains logiciels d’enregistrement d’écran, qui pourraient enregistrer la fenêtre du chat à la place de la fenêtre principale du jeu.
```

??? setting "Activer le lissage de la position des véhicules"

```
Si cette option est activée, BeamMP utilisera un algorithme pour lisser les mises à jour de position des véhicules à intervalles réguliers. Cela peut être bénéfique lorsque les joueurs ont un ping élevé ou lorsqu’une connexion subit un taux important de perte de paquets.

Si cette option est désactivée, BeamMP mettra à jour la position des véhicules dès que les informations seront reçues.
```

??? setting "Ignorer les avertissements de sécurité des mods"

```
Si cette option est activée, l’avertissement de sécurité des mods ne sera pas affiché lorsque vous essayez de vous connecter à un serveur utilisant des mods.

Si cette option est désactivée, l’avertissement de sécurité des mods sera affiché à chaque connexion à un serveur utilisant des mods.
```

??? setting "Activer la mise en file d’attente des mises à jour/modifications des véhicules des joueurs"

```
Si cette option est activée, l’apparition et les modifications des véhicules des autres joueurs seront placées dans une file d’attente. Consultez la section `2. File d’événements` pour plus d’informations.

Si cette option est désactivée, l’apparition et les modifications des véhicules des autres joueurs seront chargées immédiatement par le jeu.
```

??? setting "Activer la synchronisation automatique des pièces"

```
Si cette option est activée, les pièces de votre véhicule seront automatiquement synchronisées avec les autres joueurs après quelques secondes.

Si cette option est désactivée, vous devrez cliquer sur le bouton de synchronisation des pièces dans le sélecteur de pièces afin de transmettre les modifications aux autres joueurs.
```

??? setting "Désactiver le changement vers les véhicules des autres joueurs"

```
Si cette option est activée, le changement de véhicule avec la touche Tab ignorera les véhicules des autres joueurs.

Si cette option est désactivée, le changement de véhicule avec la touche Tab parcourra tous les véhicules présents.
```

??? setting "Faire disparaître les véhicules lorsqu’ils se rapprochent"

```
Si cette option est activée, les autres véhicules deviendront progressivement transparents lorsqu’ils se rapprocheront.

Si cette option est désactivée, les autres véhicules resteront entièrement visibles quelle que soit la distance.

!!! note ""

    Cette option affecte uniquement le maillage 3D visible du véhicule, et non sa physique (nœuds, poutres et maillage). Pour désactiver également la physique, vous devez activer `Physique de collision simplifiée` dans les paramètres de gameplay.
```

??? setting "Afficher les identifiants des joueurs"

```
Si cette option est activée, la liste des joueurs en jeu comportera une ligne supplémentaire affichant l’identifiant de chaque joueur. Cette option est utile pour le développement ou la modération.

Si cette option est désactivée, la liste des joueurs affichera uniquement le nom et le ping de chaque joueur.
```

??? setting "Autoriser l’actualisation de la liste des serveurs en jeu"

```
Si cette option est activée, la liste des serveurs sera actualisée régulièrement pendant que vous jouez. Cela peut provoquer des ralentissements ponctuels.

Si cette option est désactivée, la liste des serveurs ne sera actualisée que lorsque vous ouvrirez le menu principal.
```

## **2. File d’événements**

??? setting "Mettre en évidence les joueurs en attente"

```
Si cette option est activée, les joueurs ayant un événement en attente seront mis en évidence dans la liste des joueurs en jeu.

Si cette option est désactivée, les joueurs ne seront pas mis en évidence individuellement.
```

??? setting "Appliquer les modifications des véhicules avec"

```
Si l’option `Bouton gauche de la souris` est sélectionnée, cliquer avec le bouton gauche de la souris sur le nom d’un joueur dans la liste des joueurs chargera les événements en attente. Un clic avec le bouton droit permettra de suivre ce joueur en mode spectateur.

Si l’option `Bouton droit de la souris` est sélectionnée, cliquer avec le bouton droit de la souris sur le nom d’un joueur dans la liste des joueurs chargera les événements en attente. Un clic avec le bouton gauche permettra de suivre ce joueur en mode spectateur.
```

??? setting "Appliquer automatiquement les modifications des véhicules en attente"

```
Si cette option est activée, les événements en attente seront automatiquement chargés lorsque votre véhicule sera resté sous le seuil de vitesse pendant la durée définie par le délai d’attente.

Si cette option est désactivée, les événements en attente devront être chargés manuellement en cliquant sur le bouton `Événements` en haut de l’écran ou sur le nom d’un joueur dans la liste des joueurs.
```

??? setting "Seuil de vitesse d’application de la file d’événements"

```
Ce paramètre définit le seuil de vitesse à partir duquel les événements en attente peuvent être automatiquement chargés. Votre véhicule doit rester en dessous de cette vitesse pendant plus longtemps que la durée définie par `Délai d’application de la file` afin de charger les événements en attente.
```

??? setting "Délai d’application de la file"

```
Ce paramètre définit le délai avant le chargement automatique des événements en attente. Votre véhicule doit rester en dessous du `Seuil de vitesse d’application de la file` pendant cette durée afin de charger les événements en attente.
```

??? setting "Ignorer la file en mode spectateur"

```
Si cette option est activée, un événement sera chargé immédiatement lorsque vous êtes en train de suivre un autre joueur en mode spectateur.

Si cette option est désactivée, l’événement sera placé dans la file d’attente comme lorsque vous contrôlez votre propre véhicule.
```

??? setting "Ne pas mettre en file d’attente les monocycles (bonshommes de neige/Beamlings)"

```
Si cette option est activée, les événements concernant un bonhomme de neige ou un Beamling seront chargés immédiatement.

Si cette option est désactivée, les bonshommes de neige et les Beamlings seront mis en file d’attente comme les autres véhicules.
```

## **3. Définir le monocycle par défaut**

??? setting "Configuration du monocycle par défaut"

```
Ce paramètre définit la variante de monocycle qui sera chargée par défaut. Vous pouvez choisir parmi les configurations prédéfinies ou utiliser vos propres configurations si vous en avez enregistrées.
```

??? setting "Enregistrer automatiquement le dernier monocycle utilisé"

```
Si cette option est activée, votre dernier monocycle utilisé sera automatiquement enregistré et rechargé lorsque vous en ferez apparaître un nouveau.

Si cette option est désactivée, la configuration de monocycle par défaut sera utilisée à chaque apparition.
```

## **4. Boules**

??? setting "Activer les boules pour les véhicules non apparus"

```
Si cette option est activée, vous verrez une boule au lieu d’un véhicule qui n’a pas encore été chargé.

Si cette option est désactivée, le véhicule non chargé sera invisible.
```

??? setting "Modifier les couleurs"

```
??? setting "Visible"

    Si cette option est activée, une boule sera affiché avec la couleur définie ci-dessous.

    Si cette option est désactivée, aucune boule ne sera affiché pour la fonction concernée.

??? setting "Valeurs RGB HEX"

    Véhicule en attente : couleur utilisée par la boule lorsqu’un véhicule est en attente d’apparition. Valeur par défaut : #FF6400

    Véhicule illégal : couleur utilisée par la boule lorsqu’un véhicule est considéré comme illégal, par exemple lorsqu’il provient d’un mod ajouté manuellement. Valeur par défaut : #000000

    Véhicule supprimé : couleur utilisée par la boule lorsqu’un véhicule a été supprimé par l’utilisateur. Valeur par défaut : #333333
```

## **5. Étiquettes de nom**

??? setting "Masquer les étiquettes des joueurs"

```
Si cette option est activée, les étiquettes de nom des joueurs ne seront pas affichées.

Si cette option est désactivée, les étiquettes de nom des joueurs seront affichées en fonction de la position relative de leur véhicule.
```

??? setting "Afficher la distance avec les autres joueurs"

```
Si cette option est activée, la distance jusqu’au véhicule concerné sera affichée au début de l’étiquette de nom.

Si cette option est désactivée, aucune distance supplémentaire ne sera affichée.
```

??? setting "Faire apparaître/disparaître progressivement les étiquettes"

```
Si cette option est activée, les étiquettes de nom apparaîtront ou disparaîtront progressivement en fonction de la `Distance de fondu` et de `Inverser la direction du fondu des étiquettes`.

Si cette option est désactivée, les étiquettes seront affichées avec une opacité standard quelle que soit la distance avec le véhicule concerné.
```

??? setting "Distance de fondu / Inverser la direction du fondu des étiquettes"

```
!!! setting "Fondu sortant"

    Les étiquettes deviennent de moins en moins visibles à mesure que le joueur s’éloigne.

    `Distance de fondu` définit la distance à laquelle une étiquette sera affichée avec son opacité minimale.

!!! setting "Fondu entrant"

    Les étiquettes deviennent de plus en plus visibles à mesure que le joueur s’éloigne.

    `Distance de fondu` définit la distance à laquelle une étiquette sera affichée avec son opacité maximale.
```

??? setting "Ne pas masquer complètement les étiquettes"

```
Si cette option est activée, une étiquette ne pourra pas devenir complètement invisible. Elle conservera une opacité minimale quelle que soit la distance.

Si cette option est désactivée, les étiquettes pourront devenir complètement invisibles.
```

??? setting "Raccourcir les étiquettes et les rôles"

```
Si cette option est activée, les noms et les rôles seront tronqués selon la limite définie par `Limite de longueur des étiquettes`.

Si cette option est désactivée, les noms et les rôles seront affichés dans leur intégralité.
```

??? setting "Afficher le nom des spectateurs sous les étiquettes des véhicules"

```
Si cette option est activée, le nom d’un spectateur sera affiché sous l’étiquette du joueur.

Si cette option est désactivée, aucun nom de spectateur ne sera ajouté aux étiquettes.
```

??? setting "Utiliser la même couleur pour les étiquettes des spectateurs"

```
Si cette option est activée, le nom d’un spectateur sera toujours affiché sur un fond gris.

Si cette option est désactivée, le nom du spectateur sera affiché sur un fond coloré correspondant à son rôle.
```

## **6. Autres**

??? setting "Afficher l’activité réseau dans la console"

```
Si cette option est activée, l’activité réseau de BeamMP sera affichée dans la console.

Si cette option est désactivée, aucune activité réseau supplémentaire ne sera affichée dans la console.

!!! danger ""

    Soyez prudent avec cette option, car toutes les informations affichées dans la console sont également enregistrées dans les fichiers journaux.

    Ces fichiers peuvent atteindre plusieurs centaines de Mo en quelques minutes lorsque cette option est activée.
```

??? setting "Port du lanceur"

```
Ce paramètre définit le port utilisé pour communiquer avec le lanceur.

Il ne doit être modifié que si le port par défaut 4444 ne peut pas être utilisé.

N’oubliez pas de modifier également le port du côté du lanceur en modifiant `launcher.cfg`.

!!! tip ""

    Le port spécifié correspond uniquement au premier des deux ports utilisés. Le second port correspond directement au port suivant, soit `port + 1`.

    Le premier port transporte les paquets réseau principaux et le second les paquets réseau du jeu. Les deux utilisent le protocole TCP.
```
