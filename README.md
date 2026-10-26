# Suivi Horaire

**En ligne : https://tiliochr.github.io/suivi-horaire/**

Petit calculateur d'heures pour un contrat de **35 h/semaine**, avec heures de nuit et repos compensateur.

## Lancer

En ligne, ouvrez le lien ci-dessus. En local, double-cliquez sur **`index.html`** : l'application s'ouvre dans votre navigateur, sans installation ni connexion.

Pour la sauvegarde dans un fichier (bouton **Sauvegarder**), utilisez **Chrome ou Edge**. Les autres navigateurs continuent de fonctionner, mais la sauvegarde sera téléchargée au lieu d'écraser un fichier existant.

## Ce qui est calculé

| Règle | Valeur par défaut |
|---|---|
| Seuil hebdomadaire | 35 h (semaine du lundi au dimanche) |
| Heures supplémentaires | au-delà du seuil |
| Majoration heures supp. | × 1,25, converties en **repos** |
| Majoration nuit | 00h00 → 06h00, × 1,25 |
| Ordre de calcul | nuit d'abord, puis HS sur le total majoré |

**Exemple** : 30 h de jour + 10 h de nuit dans la semaine  
→ 30 + (10 × 1,25) = 42,50 h  
→ 42,50 − 35 = 7,50 h supp.  
→ 7,50 × 1,25 = **9,375 h de repos acquis**

**Pause** : elle est retirée en priorité des heures de jour. Les heures de nuit restent entières.  
Exemple : 08h00 → 01h00 avec 1 h de pause = 16 h travaillées, dont **1 h de nuit**.

## Saisie au quart d'heure

Les horaires et les pauses sont arrondis au quart d'heure (00, 15, 30, 45). Une valeur saisie à 08h07 devient 08h00 ; une pause de 50 min devient 45 min. Les heures de repos se saisissent aussi par quart d'heure (0,25 h = 15 min).

## Horaires habituels et couleurs

Vos horaires habituels sont :

- **lundi, mardi, jeudi, vendredi** : 09h–12h puis 13h–18h ;
- **mercredi** : 14h–18h ;
- samedi et dimanche : pas d'horaire habituel.

Une **journée complète** correspondant à ces horaires est affichée en **vert**. Une journée incomplète (par exemple 09h–12h seulement) ou décalée est affichée en **orangé**, ou en **violet** si des heures de repos sont prises le même jour.

Un **fil** relie, sur le bord gauche, la ligne de la journée à la ligne de repos du même jour.

Deux façons de saisir une journée habituelle complète sont reconnues :

- une seule ligne 09h00–18h00 avec 60 min de pause ;
- ou deux lignes : 09h00–12h00 et 13h00–18h00, sans pause.

Une nouvelle journée est préremplie avec l'horaire habituel du jour choisi. Si vous changez la date d'une journée habituelle complète, les horaires s'adaptent automatiquement (par exemple un vendredi 09h–18h déplacé au mercredi devient 14h–18h).

Si vous prenez du repos le même jour qu'une journée incomplète, les heures de repos sont rappelées sur la ligne de la journée (par exemple « + 5,00 h repos » en dessous des heures travaillées). Le lien entre l'absence et le repos est ainsi visible immédiatement.

## Sauvegarder — où sont mes données ?

Vos heures sont enregistrées **automatiquement dans votre navigateur** (stockage local). C'est ce qui permet de retrouver vos semaines en rouvrant la page.

Le bouton **Sauvegarder** crée en plus un fichier de secours `sauvegarde-heures.json` :

1. au premier clic, choisissez l'emplacement (par exemple le dossier `calculateur-heures`, à côté de `index.html`) ;
2. les clics suivants **écrasent ce même fichier**, sans redemander l'emplacement.

Ce fichier JSON peut être partagé ou réimporté avec le bouton **Importer** (flèche en haut) ou depuis les réglages. Un point orange sur « Sauvegarder » signale des modifications pas encore écrites dans le fichier.

Le détail (nom du fichier, dernière sauvegarde) est visible dans **Réglages → Où sont mes données ?**.

> Si le navigateur ne permet pas d'écrire directement (Safari, Firefox), le fichier est téléchargé dans le dossier Téléchargements ; le navigateur peut alors créer des doublons au lieu d'écraser.

## Utilisation

1. **Journées** : « Ajouter une journée », puis le jour, les heures de début/fin, la pause en minutes et un libellé.
   - Une fin avant le début signifie que la vacation passe minuit.
   - Vert = journée habituelle complète, orangé = journée incomplète ou décalée, violet = journée incomplète avec repos le même jour.
2. **Repos pris** : saisissez les heures de repos posées ; elles sont déduites du solde et rappelées sur la ligne de la journée concernée.
3. **Semaine** : flèches ‹ › pour changer de semaine, « Aujourd'hui » pour revenir.
4. **Réglages** (roue dentée) : seuil, coefficients, plage de nuit, ordre de calcul, règles détaillées, sauvegarde et export CSV.

Le détail du calcul est affiché sous les compteurs : base majorée, heures supp., repos acquis.

**Imprimer** : produit une feuille de semaine compacte (une page), sans les boutons.

## Limites

- Dimanches et jours fériés : le contrat prévoit un paiement (taux normal, sauf 1er janv., 1er mai et 25 déc. à +100 %). Ces majorations financières ne sont pas intégrées au calcul de repos.
- Trajets : un trajet pro entre deux lieux compte comme temps de travail ; le trajet domicile → lieu inhabituel au-delà de 3 h A/R ouvre droit à un repos (max. 8 h/jour). Ces règles sont rappelées dans l'app mais doivent être saisies comme des journées si besoin.
- Calcul indicatif : vérifiez toujours avec votre bulletin de paie ou votre employeur.
