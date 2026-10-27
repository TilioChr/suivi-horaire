# Suivi Horaire

**En ligne : https://tiliochr.github.io/suivi-horaire/**

Petit calculateur d'heures pour un contrat de **35 h/semaine**, avec heures de nuit et repos compensateur.

## Lancer

En ligne, ouvrez le lien ci-dessus. En local, double-cliquez sur **`index.html`** : l'application s'ouvre dans votre navigateur, sans installation. Le mode local fonctionne hors ligne ; la synchronisation du compte cloud nécessite Internet.

L'export d'une sauvegarde fonctionne dans tous les navigateurs récents (Chrome, Edge, Safari, Firefox).

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

## Sur mobile

Chaque journée s'affiche sous forme de carte compacte : touchez la carte pour ouvrir la saisie, puis son en-tête pour la replier. Le numéro de semaine se valide avec le bouton ✓ ou la touche **Entrée**. Les réglages gardent leurs boutons d'action visibles en bas de l'écran.

## Horaires habituels et couleurs

Les horaires habituels se règlent dans **Réglages → Horaires habituels**. Pour chaque jour, cochez le matin et/ou l'après-midi, puis indiquez les heures. Les modifications s'appliquent immédiatement à toutes les semaines. Par défaut :

- **lundi, mardi, jeudi, vendredi** : 09h–12h puis 13h–18h ;
- **mercredi** : 14h–18h ;
- samedi et dimanche : pas d'horaire habituel.

Une **journée complète** correspondant à ces horaires est affichée en **vert**. Une journée incomplète (par exemple 09h–12h seulement) ou décalée est affichée en **orangé**, ou en **violet** si des heures de repos sont prises le même jour.

**Repos trop long** : si le repos pris un jour dépasse la durée habituelle de ce jour, la journée, le repos et le fil de liaison passent en **rouge**. Exemple : avec un mercredi habituel de 14h–18h (4 h), 4 h 30 de repos ce jour-là déclenchent le rouge.

Un **fil** relie, sur le bord gauche, la ligne de la journée à la ligne de repos du même jour. Les fils sont espacés et s'éclaircissent progressivement pour distinguer les journées.

Deux façons de saisir une journée habituelle complète sont reconnues :

- une seule ligne couvrant les deux périodes, avec une pause égale au temps non travaillé (par exemple 09h00–18h00 avec 60 min de pause) ;
- ou deux lignes séparées (par exemple 09h00–12h00 et 13h00–18h00), sans pause.

Une nouvelle journée est préremplie avec l'horaire habituel du jour choisi. Si vous changez la date d'une journée habituelle complète, les horaires s'adaptent automatiquement (par exemple un vendredi 09h–18h déplacé au mercredi devient 14h–18h).

Si vous prenez du repos le même jour qu'une journée incomplète, les heures de repos sont rappelées sur la ligne de la journée (par exemple « + 5,00 h repos » en dessous des heures travaillées). Le lien entre l'absence et le repos est ainsi visible immédiatement.

## Sauvegarde — où sont mes données ?

Vos heures sont enregistrées **automatiquement dans votre navigateur** (stockage local). C'est ce qui permet de retrouver vos semaines en rouvrant la page.

Avec un **compte cloud** (bouton **Compte**), une copie est aussi synchronisée dans votre projet Supabase : vous retrouvez vos données sur n'importe quel appareil en vous connectant. Le mode local reste disponible si vous n'êtes pas connecté.

Le bouton **Sauvegarde** (en haut) propose :

- **Exporter la sauvegarde (JSON)** : télécharge `suivi-horaire-AAAA-MM-JJ.json`, contenant les réglages, les journées et les repos. C'est le fichier à conserver pour restaurer vos données.
- **Exporter le tableau (CSV)** : télécharge un tableur lisible par Excel, LibreOffice ou Numbers.
- **Importer une sauvegarde…** : remplace les données de l'appareil par un fichier JSON exporté précédemment.

L'export est un simple téléchargement : il fonctionne sans autorisation particulière et ne modifie jamais les données existantes. La date du dernier export apparaît en bas du menu **Sauvegarde**.

## Compte cloud (synchronisation)

Le bouton **Compte** (icône personne, en haut) permet de créer un compte avec **email + mot de passe**. L'email sert d'identifiant et reçoit le lien de confirmation et de réinitialisation du mot de passe. Supabase gère l'authentification : votre mot de passe est haché, jamais stocké par l'application.

Une fois connecté :

- les modifications sont synchronisées automatiquement (point vert sur le bouton Compte) ;
- sur un autre appareil, connectez-vous avec le même compte pour retrouver la sauvegarde ;
- si l'appareil et le compte contiennent chacun des données, une fenêtre demande laquelle conserver — **aucune fusion automatique** ;
- si deux appareils modifient la sauvegarde, une fenêtre de conflit permet de choisir la version à garder — **aucun écrasement silencieux** ;
- hors ligne, les modifications restent locales et sont synchronisées au retour du réseau.

Le bouton **Sauvegarde** reste utile pour un fichier de secours hors ligne. **Se déconnecter et effacer cet appareil** retire les données locales sans supprimer la sauvegarde du compte.

Les données sont stockées dans votre projet Supabase, accessibles uniquement par votre compte grâce aux règles **RLS**. La clé publique présente dans le code ne permet pas de lire les données d'un autre compte ; la clé `service_role` n'est jamais dans l'application. Comme pour tout service en ligne, l'hébergeur peut techniquement accéder aux données stockées : elles sont protégées en transit et par les règles d'accès, mais pas chiffrées de bout en bout.

> L'offre gratuite Supabase peut mettre le projet en pause après une longue inactivité ; les données restent.

## Utilisation

1. **Journées** : « Ajouter une journée », puis le jour, les heures de début/fin, la pause en minutes et un libellé.
   - La date est préremplie avec la prochaine journée de la semaine : après lundi et mardi, l'ajout propose le mercredi. Si la semaine est complète, la semaine suivante s'ouvre.
   - Une fin avant le début signifie que la vacation passe minuit.
   - Vert = journée habituelle complète, orangé = journée incomplète ou décalée, violet = journée incomplète avec repos le même jour, rouge = repos supérieur à la durée habituelle du jour.
2. **Repos pris** : saisissez les heures de repos posées ; elles sont déduites du solde et rappelées sur la ligne de la journée concernée.
3. **Période** : choisissez **Semaine**, **Mois** ou **Année** en haut à droite. Les flèches ‹ › font défiler la période et « Aujourd'hui » revient à la période en cours.
   - En vue semaine, le numéro est modifiable : saisissez-le et appuyez sur **Entrée**. Une semaine inexistante pour l'année est refusée et la semaine affichée reste inchangée.
4. **Réglages** (roue dentée) : calcul, horaires habituels et règles détaillées.
5. **Sauvegarde** (en haut) : exporter le JSON ou le CSV, ou importer une sauvegarde.
6. **Compte** (icône personne) : connexion, création de compte, synchronisation cloud, déconnexion.

En vue semaine, le détail du calcul est affiché sous les compteurs : base majorée, heures supp., repos acquis.

**Imprimer** : imprime la vue affichée (semaine, mois ou année), sans les boutons.

## Vues mois et année

- **Mois** : un calendrier affiche les heures travaillées de chaque jour, avec les mêmes couleurs que la vue semaine (dont le rouge si le repos dépasse la durée habituelle du jour). Un clic sur un jour ouvre sa semaine.
- **Année** : un tableau récapitule les 12 mois (travaillé, nuit, heures supp., repos acquis, repos pris, solde) et un total annuel. Un clic sur un mois l'ouvre.

Les heures supplémentaires et le repos acquis restent calculés **semaine par semaine**, comme dans le contrat. Ils sont rattachés au **lundi** de la semaine : le total d'un mois peut donc inclure quelques jours du mois voisin lorsqu'une semaine est à cheval. Les heures travaillées, la nuit et le repos pris sont, eux, comptés à leur date.

## Limites

- Dimanches et jours fériés : le contrat prévoit un paiement (taux normal, sauf 1er janv., 1er mai et 25 déc. à +100 %). Ces majorations financières ne sont pas intégrées au calcul de repos.
- Trajets : un trajet pro entre deux lieux compte comme temps de travail ; le trajet domicile → lieu inhabituel au-delà de 3 h A/R ouvre droit à un repos (max. 8 h/jour). Ces règles sont rappelées dans l'app mais doivent être saisies comme des journées si besoin.
- Calcul indicatif : vérifiez toujours avec votre bulletin de paie ou votre employeur.
