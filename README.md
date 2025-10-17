# Test-technique-Product-Owner
## 1. Spécifications Fonctionnelles Détaillées
   
### 1.1. Gestion des Projets
#### a. Entrées

##### 1. Champs à saisir :

Nom du projet 

Description du projet 

Chef de projet 

Date de début et date de fin (obligatoires, la fin ≥ début)

Budget estimé (coût et temps)

Liste des phases du projet :

Nom de la phase

Description

Ordre d’exécution

Tâches associées 

#### b. Actions possibles

Créer un nouveau projet

Modifier ou supprimer un projet existant

Ajouter , modifier , supprimer une phase

Attribuer un chef de projet

Définir ou ajuster le budget

Consulter la liste des projets

Exporter le projet (PDF, Excel..)

#### c. Résultats attendus

Lors de la création → le projet est ajouté dans la base avec un identifiant unique.

Lors de la modification → le projet est mis à jour et un journal des modifications est enregistré.

Lors de la suppression → le projet est supprimé après confirmation.

Les budgets et phases sont visibles dans la fiche du projet.

Le chef de projet reçoit une notification à sa nomination.

#### d. Règles métier et contraintes

La date de fin ne peut être antérieure à la date de début.

Le budget total des tâches ne doit pas dépasser le budget global du projet.

Chaque projet doit avoir un seul chef de projet.

Un projet ne peut pas dépasser un budget global prédéfini.
→ Si ce seuil est atteint, une alerte est envoyée au chef de projet.

#### e. Fonctionnalités non fonctionnelles

Performance : chargement de la liste des projets.

Sécurité : seuls les chefs de projet ou administrateurs peuvent créer ou supprimer un projet.

Compatibilité : module accessible sur navigateurs récents (Chrome, Edge..).

Disponibilité : 99,9 % d’uptime.

### 1.2. Planification des Tâches
#### a. Entrées

Nom de la tâche 

Description 

Phase associée (obligatoire)

Assignation des utilisateurs (1 à plusieurs)

Budget de la tâche (temps et coût)

Dates de début et de fin

Dépendances (autres tâches)

Commentaires et fichiers attachés

#### b. Actions possibles

Créer / modifier / supprimer une tâche

Attribuer ou retirer un utilisateur

Ajouter une dépendance entre tâches

Ajouter un commentaire ou un fichier

Mettre à jour l’état d’avancement

Modifier les dates selon contraintes

#### c. Résultats attendus

Création : tâche enregistrée et visible dans la phase.

Assignation : notifications envoyées aux utilisateurs concernés.

Ajout de dépendance : le système empêche le démarrage d’une tâche dépendante tant que la tâche précédente n’est pas terminée.

Ajout de commentaire ou fichier : visible immédiatement dans l’interface.

#### d. Règles métier et contraintes

Un utilisateur ne peut pas être affecté à plus de 3 tâches actives sur un même projet.

Les dépendances doivent être respectées : une tâche ne peut commencer qu’après la fin de la tâche dont elle dépend.

Les fichiers joints doivent être de type autorisé (PDF, DOCX..≤ 10 Mo).

Les dates doivent être cohérentes (début ≤ fin).

Le budget d’une tâche ne doit pas faire dépasser le budget global du projet.

#### e. Fonctionnalités non fonctionnelles

Performance : création de tâche rapidement.

Sécurité : contrôle d’accès par rôle (seuls les chefs peuvent créer des dépendances).

Compatibilité : responsive sur tablette et PC.

Sauvegarde automatique en cas de perte de connexion.

### 1.3. Suivi des Performances
##### a. Entrées

Données calculées automatiquement :

Pourcentage d’avancement (nombre de tâches terminées / total)

Dépenses réelles vs budget

Retards sur les délais

##### b. Actions possibles

Consulter le tableau de bord d’un projet

Filtrer par phase, membre ou statut

Exporter le rapport de performance

Configurer des alertes (budget, délai)

##### c. Résultats attendus

Affichage du tableau de bord avec :

% d’achèvement du projet

Budget consommé vs estimé

Tâches en retard

En cas de dépassement du budget ou du délai, une notification est envoyée au chef de projet.

##### d. Règles métier et contraintes

Le calcul du taux d’avancement se base sur les tâches terminées.

Aucune tâche ne peut être considérée comme “terminée” sans validation du chef de projet.

Les notifications doivent être envoyées instantanément en cas de dépassement.

##### e. Fonctionnalités non fonctionnelles

Performance : affichage du tableau de bord ≤ 3 s.

Sécurité : seules les personnes autorisées peuvent consulter les coûts.

Compatibilité : accessible depuis mobile.

Fiabilité : mise à jour des KPIs en temps réel.

### 1.4. Règles Métier Globales
##### a. Règles

Un utilisateur ne peut pas être affecté à plus de 3 tâches actives sur le même projet.

Un projet ne peut pas dépasser un budget global prédéfini.

Si le seuil de budget ou de temps est atteint, alerte automatique au chef de projet.

Les dépendances entre tâches doivent être respectées.

Les dates doivent être logiquement cohérentes.

##### b. Contraintes

Aucune modification budgétaire n’est permise si le projet dépasse le seuil global.

L’assignation d’un 4ᵉ tâche à un utilisateur déclenche une erreur bloquante.

Cohérence des dates et budgets

## 2. Test Manuel - Scénarios de Test et Détection de Bugs
### 1. Scénarios de Test

##### A. Gestion des projets — Scénarios de test
Scénario A1 — Création projet (Nominal)

Ouvrir écran Nouveau projet.

Saisir : titre, dates valides, budget coût, budget temps, sélectionner chef de projet.

Cliquer Créer.
Résultat attendu : projet créé, page détail projet ouverte, message succès, projet visible liste projets, entrée d’audit enregistrée.
Validation : vérifier DB (enregistrement), UI (affichage), logs.

Scénario A2 — Création avec dates invalides

Saisir date fin antérieure à date début.

Cliquer Créer.
Résultat attendu : message d’erreur côté client + serveur, projet non créé.
Validation : message d’erreur clair ; pas d’entrée en DB.

Scénario A3 — Modifier budget projet

Modifier budget estimé pour le porter sous le seuil.

Sauvegarder.
Résultat attendu : changement accepté, historique enregistré, notification au chef si config.
Validation : audit, affichage nouveau montant.

Zones de risque (Gestion projets)

Validation dates/budgets côté client et serveur.

Concurrence (deux utilisateurs modifient budget en même temps) → vérifier mécanisme de locking/versioning.

Erreurs d’export (formats).

##### B. Planification des tâches — Scénarios de test
Scénario B1 — Créer tâche et assigner 1 utilisateur

Créer tâche dans phase X, assigner utilisateur U, définir dates valides, estimations.

Sauvegarder.
Résultat attendu : tâche créée, notification à U, visible dans phase et Gantt.
Validation : email/in-app notification reçue, DB contient la tâche.

Scénario B2 — Affectation >3 tâches (contrainte)

Avoir un utilisateur U déjà assigné à 3 tâches actives du projet.

Tenter d’assigner une 4e tâche à U.
Résultat attendu : blocage avec message expliquant la règle R1 ; option override réservée aux admins.
Validation : UI blocking, pas d’assignation en DB, journal d’erreur.

Scénario B3 — Dépendances et replanification automatique

Créer Tâche A (fin prévue 10/10), Tâche B dépendant de A (start on finish of A).

Modifier date fin de A à 15/10.
Résultat attendu : date début proposée pour B recalculée à ≥ 15/10 ; notification de conflit.
Validation : vérification propagation, logs de recalcul.

Scénario B4 — Upload fichier et commentaire

Ajouter fichier valide et un commentaire.
Résultat attendu : fichier stocké, accessible, commentaire visible horodaté.
Validation : test téléchargement, test preview, vérifier métadonnées.

Zones de risque (Planification)

Calcul et propagation des dépendances (cycles, propagation incorrecte)

Contrôle de la contrainte d’affectation (synchronisation entre front/back)

Uploads (corruption, échec, vulnérabilités)

Race conditions lors de modifications simultanées

##### C. Suivi des performances & Notifications — Scénarios de test
Scénario C1 — Dashboard KPI exactitude

Créer projet avec 4 tâches (2 terminées, coûts et temps connus).

Vérifier que le % d’avancement et dépenses affichées concordent avec calcul choisi.
Résultat attendu : KPIs mathématiquement corrects selon formule (déclarer formule testée).
Validation : calcul manuel vs UI ; vérifier DB pour valeurs réelles.

Scénario C2 — Notification dépassement budget tâche

Enregistrer coût réel d’une tâche supérieurs à estimation.
Résultat attendu : notification immédiate au chef de projet.
Validation : réception email/in-app, logs d’envoi, contenu du message conforme.

Scénario C3 — Alerte projet seuil global

Simuler accumulation de coûts au seuil configuré (ex. 90%).
Résultat attendu : alerte au chef de projet, option d’arrêt d’approbation si config.
Validation : audit, UI d’alerte, lien vers rapport.

### 2. Détection des Bugs 
#### a. Zones de risque potentielles

Validation des formulaires (dates, budget, affectations)

Calcul des dépendances entre tâches

Calcul des budgets et pourcentages d’avancement

Gestion des notifications (risque de doublons ou absence d’alerte)

Upload des fichiers (formats, taille)

#### b. Méthodes pour repérer les bugs

Tests fonctionnels manuels pour valider toutes les interactions utilisateur.

Tests de performance pour mesurer les temps de réponse (ex. chargement du dashboard).

Tests de sécurité pour vérifier les droits d’accès et la validation des fichiers.

Tests d’intégration entre modules (projet ↔ tâches ↔ notifications).

#### c. Critères de validation

Les résultats affichés correspondent aux résultats attendus.

Aucun plantage ni erreur inattendue.

Le budget et les délais sont correctement calculés.

Les contraintes (3 tâches max, dépendances) sont respectées.

Les alertes et notifications fonctionnent dans les délais.

### 3. Validation des Spécifications

#### a. Méthode de vérification

Comparer chaque résultat obtenu aux spécifications fonctionnelles rédigées.

Vérifier la conformité des règles métier (limites, alertes, calculs).

Contrôler la cohérence des champs saisis et des messages d’erreur.

#### b. Outils / méthodologies

Outil de gestion de tests : Jira (Xray) ou TestRail.

Suivi des bugs via Trello / Azure DevOps.

Analyse des logs d’erreurs et journaux d’audit.

Tests de performance via JMeter.

#### c. Validation performance & seuils

Exécuter un test de charge sur 1000 tâches → le tableau de bord doit rester fluide.

Simuler un dépassement de budget → vérifier que l’alerte est bien déclenchée.

Vérifier que les temps de traitement et de notification respectent les seuils définis.
