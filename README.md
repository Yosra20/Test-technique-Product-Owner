# Test-technique-Product-Owner
## 1. Spécifications Fonctionnelles Détaillées
   
### 1.1. Gestion des Projets
#### a. Entrées

##### 1. Champs à saisir :

- Nom du projet 

- Description du projet 

- Chef de projet 

- Date de début et date de fin (obligatoires, la fin ≥ début)

- Budget estimé (coût et temps)

##### 2. Liste des phases du projet :

- Nom de la phase

- Description de la phase

- Ordre d’exécution

- Tâches associées 

#### b. Actions possibles

- Créer un nouveau projet

- Modifier ou supprimer un projet existant

- Ajouter , modifier , supprimer une phase

- Attribuer un chef de projet

- Définir ou ajuster le budget

- Consulter la liste des projets

- Exporter le projet (PDF, Excel..)

#### c. Résultats attendus

- Lors de la création → le projet est ajouté dans la base avec un identifiant unique.

- Lors de la modification → le projet est mis à jour et un journal des modifications est enregistré.

- Lors de la suppression → le projet est supprimé après confirmation.

- Les budgets et phases sont visibles dans la fiche du projet.

- Le chef de projet reçoit une notification à sa nomination.

#### d. Règles métier et contraintes

- La date de fin ne peut être antérieure à la date de début.

- Le budget total des tâches ne doit pas dépasser le budget global du projet.

- Chaque projet doit avoir un seul chef de projet.

- Un projet ne peut pas dépasser un budget global prédéfini.
→ Si ce seuil est atteint, une alerte est envoyée au chef de projet.

#### e. Fonctionnalités non fonctionnelles

- Performance : chargement de la liste des projets.

- Sécurité : seuls les chefs de projet ou administrateurs peuvent créer ou supprimer un projet.

- Compatibilité : module accessible sur navigateurs récents (Chrome, Edge..).

- Disponibilité : 99,9 % d’uptime.

### 1.2. Planification des Tâches
#### a. Entrées

- Nom de la tâche 

- Description de la tâche

- Phase associée (obligatoire)

- Assignation des utilisateurs (1 à plusieurs)

- Budget de la tâche (temps et coût)

- Dates de début et de fin

- Dépendances (autres tâches)

- Commentaires et fichiers attachés

#### b. Actions possibles

- Créer / modifier / supprimer une tâche

- Attribuer ou retirer un utilisateur

- Ajouter une dépendance entre tâches

- Ajouter un commentaire ou un fichier

- Mettre à jour l’état d’avancement

- Modifier les dates selon contraintes

#### c. Résultats attendus

- Création : tâche enregistrée et visible dans la phase.

- Assignation : notifications envoyées aux utilisateurs concernés.

- Ajout de dépendance : le système empêche le démarrage d’une tâche dépendante tant que la tâche précédente n’est pas terminée.

- Ajout de commentaire ou fichier : visible immédiatement dans l’interface.

#### d. Règles métier et contraintes

- Un utilisateur ne peut pas être affecté à plus de 3 tâches actives sur un même projet.

- Les dépendances doivent être respectées : une tâche ne peut commencer qu’après la fin de la tâche dont elle dépend.

- Les fichiers joints doivent être de type autorisé (PDF, DOCX..≤ 10 Mo).

- Les dates doivent être cohérentes (début ≤ fin).

- Le budget d’une tâche ne doit pas faire dépasser le budget global du projet.

#### e. Fonctionnalités non fonctionnelles

- Performance : création de tâche rapidement.

- Sécurité : contrôle d’accès par rôle (seuls les chefs peuvent créer des dépendances).

- Compatibilité : responsive sur tablette et PC.

- Sauvegarde automatique en cas de perte de connexion.

### 1.3. Suivi des Performances
##### a. Entrées

- Données calculées automatiquement :

- Pourcentage d’avancement (nombre de tâches terminées / total)

- Dépenses réelles vs budget

- Retards sur les délais

##### b. Actions possibles

- Consulter le tableau de bord d’un projet

- Filtrer par phase, membre ou statut

- Exporter le rapport de performance

- Configurer des alertes (budget, délai)

##### c. Résultats attendus

- Affichage du tableau de bord avec :

1- % d’achèvement du projet

2- Budget consommé vs estimé

3- Tâches en retard

En cas de dépassement du budget ou du délai, une notification est envoyée au chef de projet.

##### d. Règles métier et contraintes

- Le calcul du taux d’avancement se base sur les tâches terminées.

- Aucune tâche ne peut être considérée comme “terminée” sans validation du chef de projet.

- Les notifications doivent être envoyées instantanément en cas de dépassement.

##### e. Fonctionnalités non fonctionnelles

- Performance : affichage du tableau de bord ≤ 3 s.

- Sécurité : seules les personnes autorisées peuvent consulter les coûts.

- Compatibilité : accessible depuis mobile.

- Fiabilité : mise à jour des KPIs en temps réel.

### 1.4. Règles Métier Globales
##### a. Règles

- Un utilisateur ne peut pas être affecté à plus de 3 tâches actives sur le même projet.

- Un projet ne peut pas dépasser un budget global prédéfini.

- Si le seuil de budget ou de temps est atteint, alerte automatique au chef de projet.

- Les dépendances entre tâches doivent être respectées.

- Les dates doivent être logiquement cohérentes.

##### b. Contraintes

- Aucune modification budgétaire n’est permise si le projet dépasse le seuil global.

- L’assignation d’une 4ème tâche à un utilisateur déclenche une erreur bloquante.

- Cohérence des dates et budgets

## 2. Test Manuel - Scénarios de Test et Détection de Bugs
### 1. Gestion des Projets
#### Scénario GP1 – Création d’un projet valide

Objectif : Vérifier qu’un projet peut être créé avec des données complètes et valides.

Étapes :

- Accéder au module “Gestion des Projets”.

- Cliquer sur le bouton “Créer un projet”.

- Saisir un nom de projet valide, des dates de début et de fin cohérentes, un budget, et sélectionner un chef de projet.

- Cliquer sur “Créer”.

Résultat attendu :
Le projet est créé avec succès et apparaît dans la liste des projets existants.

Validation :
Vérifier que le projet figure bien dans la liste, avec toutes les informations correctement affichées.

#### Scénario GP2 – Création d’un projet avec budget manquant

Objectif : Tester la validation des champs obligatoires lors de la création d’un projet.

Étapes :

- Ouvrir la page “Créer un projet”.

- Renseigner tous les champs sauf le budget.

- Cliquer sur “Créer”.

Résultat attendu :
Message d’erreur “Budget requis” affiché, le projet n’est pas créé.

Validation :
Vérifier que le message d’erreur s’affiche et qu’aucun projet vide n’est ajouté à la liste.

#### Scénario GP3 – Dépassement du budget global

Objectif : Vérifier que le système bloque la création d’un projet dont le budget dépasse le seuil autorisé.

Étapes :

- Créer un projet avec un budget supérieur à la limite autorisée.

- Cliquer sur “Créer”.

Résultat attendu :
Message d’erreur “Budget dépasse le seuil autorisé” et alerte envoyée au chef de projet.

Validation :
Vérifier que le projet n’est pas créé et que le message d’erreur est cohérent.

### 2. Planification des Tâches
#### Scénario PT1 – Création d’une tâche valide

Objectif : Vérifier la création d’une tâche avec des données correctes.

Étapes :

- Aller dans un projet actif.

- Cliquer sur “Ajouter une tâche”.

- Saisir un nom de tâche, des dates cohérentes, et assigner un utilisateur.

- Enregistrer la tâche.

Résultat attendu :
Tâche créée avec succès et notification envoyée à l’utilisateur assigné.

Validation :
Vérifier que la tâche apparaît dans la liste et que la notification a bien été reçue.

#### Scénario PT2 – Dépendance non respectée

Objectif : Tester la gestion des dépendances entre tâches.

Étapes :

- Créer deux tâches A et B, où B dépend de A.

- Tenter de démarrer la tâche B avant la fin de A.

Résultat attendu :
Blocage de la tâche et message “Dépendance non respectée”.

Validation :
Vérifier que la tâche B reste bloquée jusqu’à la complétion de la tâche A.

#### Scénario PT3 – Affectation de plus de 3 tâches à un utilisateur

Objectif : Vérifier la limite d’affectation des tâches par utilisateur.

Étapes :

- Identifier un utilisateur déjà assigné à 3 tâches actives.

- Tenter de lui assigner une quatrième tâche.

Résultat attendu :
Message d’erreur “Limite atteinte : 3 tâches actives maximum”.

Validation :
Vérifier que la tâche n’est pas créée et que le message est bien affiché.

#### Scénario PT4 – Ajout de fichier non autorisé

Objectif : Tester la validation des fichiers lors du téléchargement.

Étapes :

- Ouvrir une tâche et cliquer sur “Joindre un fichier”.

- Tenter d’ajouter un fichier de type .exe.

Résultat attendu :
Message d’erreur “Type de fichier non autorisé”.

Validation :
Vérifier qu’aucun fichier non conforme n’est ajouté à la tâche.

### 3. Suivi des Performances
#### Scénario SP1 – Affichage du tableau de bord

Objectif : Vérifier que les indicateurs clés (KPIs) s’affichent correctement.

Étapes :

- Accéder à la section “Tableau de bord” d’un projet actif.

- Observer l’affichage des KPIs (budget, avancement, délais, etc.).

Résultat attendu :
Les KPIs s’affichent correctement et reflètent les données réelles du projet.

Validation :
Comparer les valeurs affichées avec les données sources dans la base de données ou les rapports internes.

#### Scénario SP2 – Dépassement du budget

Objectif : Tester la détection automatique d’un dépassement budgétaire.

Étapes :

- Augmenter les dépenses réelles du projet au-delà du budget défini.

- Observer la réaction du système.

Résultat attendu :
Notification immédiate envoyée au chef de projet.

Validation :
Vérifier la réception de la notification et le bon affichage du dépassement dans le tableau de bord.

#### Scénario SP3 – Retard sur une tâche

Objectif : Vérifier la génération d’alerte en cas de retard de tâche.

Étapes :

- Laisser passer la date de fin d’une tâche sans la marquer comme terminée.

- Observer les alertes générées.

Résultat attendu :
Alerte “Tâche en retard” affichée sur le tableau de bord.

Validation :
Vérifier que l’alerte s’affiche et reste visible jusqu’à la clôture de la tâche.

### 4. Détection des Bugs
Zones de risques potentielles :

- Validation de formulaires (champs obligatoires non renseignés, formats incorrects)

- Calcul du budget et dépassement des seuils

- Gestion des dépendances entre tâches

- Téléversement de fichiers non conformes

- Affichage et mise à jour des indicateurs du tableau de bord

Méthodes utilisées pour repérer les bugs :

- Tests fonctionnels : vérifier chaque scénario prévu dans les spécifications.

- Tests de validation : comparer le résultat attendu et le résultat réel.

- Tests de performance : observer le temps de réponse du tableau de bord.

- Tests de sécurité : s’assurer que les fichiers malveillants (.exe) sont bloqués.

Critères de validation :

- Conformité avec les exigences fonctionnelles.

- Absence d’erreurs visibles (messages incorrects, crashs, données incohérentes).

- Bon affichage des messages d’erreur et alertes.

- Respect des contraintes de budget, dépendances et délais.

### 5. Validation des Spécifications Fonctionnelles
Méthodologie :

- Comparer le résultat attendu de chaque scénario avec le résultat obtenu.

- Documenter les écarts observés et les anomalies détectées.

- Utiliser une grille de tests (Excel ou TestLink) pour suivre le statut (Passé / Échoué).

Outils de test possibles :

- Jira ou TestLink pour la gestion des cas de test.

- Excel / Google Sheets pour le suivi manuel.

- Captures d’écran / rapports PDF pour la traçabilité.

- Logs applicatifs pour identifier les erreurs côté serveur.

Validation de la performance :

- Vérifier que les temps de chargement des pages restent acceptables (< 3s).

- S’assurer que les notifications et alertes sont émises en temps réel.

- Confirmer qu’aucun dépassement de budget ni retard non signalé n’apparaît.
