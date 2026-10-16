# AutoFolderIcon pour macOS

AutoFolderIcon pose toute seule une icône sur vos dossiers : le dossier système, teinté, avec un symbole ou un emoji
qui dit ce qu'il contient. Un dossier nommé « Factures » devient vert avec un symbole de reçu ; « Voyages », bleu avec un
avion. L'app reconnaît le nom par mot-clé, synonyme, faute de frappe ou sens proche, et vit dans la barre des menus.
Tout reste sur le Mac : aucun compte, aucune télémétrie.

Ce dépôt ne contient que les versions à installer. Le code source n'est pas public.

## Ce qu'il faut

- un Mac à puce Apple (M1 ou plus récent) ;
- macOS 14 ou plus ;
- facultatif : l'Accès complet au disque, pour styler aussi Bureau, Documents et Téléchargements.

Aucun compte GitHub, aucun outil à installer, aucun mot de passe administrateur.

## Installer

Dans Terminal (Cmd + Espace, « Terminal »), une seule commande, qui installe aussi les mises à jour :

```
curl -fsSL https://raw.githubusercontent.com/LucasHRCHatReply/autofoldericon-releases/main/installer.sh | zsh
```

Le script télécharge la dernière version, vérifie l'empreinte SHA-256 du zip, l'identifiant de l'app et sa signature
(équipe Apple `JT9FY7PP7K`, `codesign --verify --deep --strict`), copie `AutoFolderIcon.app` dans `~/Applications`, puis
ouvre l'app. Il garde les règles et les réglages.

## Avertissement : app non validée par Apple

AutoFolderIcon est signée mais pas « notarisée » : cela demande un compte développeur payant. macOS la juge donc non
vérifiée au premier lancement. Le script retire pour cela le blocage du premier lancement (l'attribut de quarantaine posé
par le téléchargement), seulement sur `AutoFolderIcon.app`. À ne lancer que si vous faites confiance à l'auteur ; le
script se lit en entier : [installer.sh](installer.sh). Le contrôle d'équipe et d'empreinte protège contre un zip altéré
en route, pas contre quelqu'un qui détiendrait aussi ce dépôt.

## Mettre à jour

Dans l'app : Réglages › Mises à jour. AutoFolderIcon interroge l'API publique des versions de ce dépôt au démarrage, au
plus une fois par jour (la case se coupe ; « Vérifier maintenant » le fait à la demande), propose la nouvelle version,
contrôle l'équipe, la signature et le numéro, remplace l'app et la relance ; si cela échoue, l'ancienne version revient.
Ou relancer la commande ci-dessus. Journal : `~/Library/Logs/AutoFolderIcon-mise-a-jour.log`.

## Désinstaller

Télécharger le zip de la dernière version dans les [Releases](../../releases/latest), le décompresser, puis lancer
`./uninstall.sh` dans le dossier `AutoFolderIcon-X.Y.Z` : l'app est supprimée, les icônes déjà posées restent, et le
script demande avant d'effacer les règles.
