# Installer la borne Cervantes

Ce guide s'adresse à la personne qui installe la borne sur place. Aucune connaissance technique n'est
nécessaire : on colle une ligne, on répond à trois questions, on attend, on redémarre.

## Ce qu'il faut avant de commencer

- **Le PC de la borne** : Windows 10 ou 11, carte graphique NVIDIA RTX (RTX 5080 pour l'exposition),
  au moins 32 Go de mémoire et 150 Go libres sur le disque C.
- **Internet** pendant l'installation : environ 60 Go à télécharger, compter 1 à 2 heures.
- **Le mot de passe d'installation**, donné par Clément Chériot.
- **L'écran tactile** branché et tourné en portrait, **la caméra** branchée en USB.
- **Le pilote de la carte NVIDIA** à jour : [nvidia.com/drivers](https://www.nvidia.com/drivers), choisir
  « Game Ready » ou « Studio », installer, redémarrer.

Deux réglages restent à faire à la main, une fois :

1. **Écran en portrait** : clic droit sur le bureau > Paramètres d'affichage > Orientation de l'affichage
   > Portrait.
2. **Rallumage automatique** : si le lieu coupe le courant la nuit, régler le BIOS du PC pour qu'il se
   rallume seul au retour du courant (option « Restore on AC Power Loss » ou « AC Recovery » sur
   « Power On »). Sans ce réglage, la borne reste éteinte le matin.

## Installer

1. Faire un **clic droit sur le bouton Démarrer** de Windows, puis choisir **Terminal (administrateur)**
   (ou **Windows PowerShell (administrateur)**). Accepter la question de Windows.
2. **Copier la ligne ci-dessous, la coller** dans la fenêtre (clic droit colle), appuyer sur **Entrée** :

   ```
   irm https://github.com/ccheriot/cervantes-installation/releases/latest/download/installer.ps1 | iex
   ```

3. **Répondre aux questions** :
   - *Que sera cet ordinateur ?* : **1** pour une borne complète (le cas habituel : calcul et écran sur le
     même PC). Voir plus bas pour plusieurs écrans.
   - *Mot de passe d'installation* : celui donné par Clément (rien ne s'affiche pendant la frappe, c'est
     normal).
   - *Ouverture de session automatique* : répondre **O**, puis le nom du compte Windows (Entrée pour le
     compte actuel) et son mot de passe (vide s'il n'y en a pas). C'est ce qui permet à la borne de
     redémarrer seule.
4. **Attendre.** Les modèles d'intelligence artificielle se téléchargent (le plus long). La fenêtre peut
   rester longtemps sur la même ligne : ne pas la fermer.
5. À la fin, la fenêtre affiche **INSTALLATION TERMINÉE**. Répondre **O** pour redémarrer.

Après le redémarrage, Windows ouvre la session tout seul, le décor de Cervantes apparaît en plein écran
avec le message « La borne se prépare » pendant quelques minutes, puis « Touchez l'écran pour commencer ».

## Vérifier que tout fonctionne

Sur le PC de la borne, ouvrir Chrome (touches **Alt + Tab** pour sortir de l'écran de la borne) à l'adresse :

```
http://127.0.0.1:8010/diagnostic
```

La page doit dire **Tout est prêt**, en vert. Chaque ligne explique ce qui ne va pas sinon, par exemple
« Caméra non détectée (vérifier le câble USB) ». Faire ensuite un portrait d'essai sur l'écran tactile.

Depuis un autre ordinateur du même réseau, la page est à `http://<nom du PC de la borne>:8010/diagnostic`.

## Plusieurs écrans pour un seul PC de calcul

1. Sur le PC qui a la carte graphique, installer en choisissant **2** (serveur seulement). À la fin,
   la fenêtre affiche **le nom de ce PC** : le noter.
2. Sur chaque PC d'écran, installer en choisissant **3** (un écran seulement), et donner ce nom quand
   l'installeur demande l'adresse du serveur. Il vérifie que le serveur répond.

Le serveur sert un visiteur à la fois ; les autres écrans affichent l'attente pendant ce temps.

## Au quotidien

Tout se trouve dans le dossier **C:\Borne** :

| Pour | Double-cliquer sur |
|---|---|
| Arrêter la borne (maintenance) | `ARRETER_BORNE.bat` ; redémarrer le PC la relance |
| Mettre à jour vers la dernière version | `METTRE_A_JOUR.bat` (Internet et mot de passe d'installation) |
| Changer l'adresse du serveur d'un écran | `CHANGER_SERVEUR.bat` |
| Essayer sans caméra (une vidéo remplace la caméra) | `ESSAI_CAMERA.bat`, à chaque double-clic : vidéo duo, vidéo solo, caméra réelle. **Revenir à la caméra réelle avant l'ouverture au public.** |

Pour quitter l'écran de la borne au clavier : **Alt + F4**, puis `ARRETER_BORNE.bat` (sinon elle revient
d'elle-même au bout de 10 secondes).

La borne se surveille seule : si une partie s'arrête ou se fige, elle est relancée automatiquement, et le
PC redémarre en dernier recours. Les photos des visiteurs sont effacées de la borne en moins de
30 minutes.

## En cas de problème

1. Ouvrir la page de diagnostic (voir plus haut) et faire une capture d'écran.
2. Envoyer cette capture et le contenu du dossier **C:\Borne\_logs** à Clément Chériot.
3. Redémarrer le PC résout la plupart des blocages.
