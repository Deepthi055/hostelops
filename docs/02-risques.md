# Analyse des risques et périmètre de test

Score = Probabilité (1 à 3) × Impact (1 à 3). Seuils : 7 à 9 critique, 4 à 6 important, 1 à 3 faible.

## 1. Cartographie des risques
| ID | Risque | Module | P | I | Score | Test prévu |
|---|---|---|---|---|---|---|
| R1 | Un étudiant accède aux réclamations d'un autre | Droits / API | 3 | 3 | 9 | API, E2E |
| R2 | Un étudiant effectue une action réservée à l'admin (changer un statut) | Droits / API | 3 | 3 | 9 | API |
| R3 | Transition de statut incohérente (ex. Resolved vers Pending) | Suivi | 3 | 3 | 9 | Unitaire, état |
| R4 | Authentification faible (mot de passe en clair, jeton JWT non vérifié ou sans expiration) | Authentification | 2 | 3 | 6 | API, sécurité |
| R5 | Validation des champs absente ou incorrecte (vide, trop court, trop long) | Réclamations | 3 | 2 | 6 | Partitions, valeurs limites |
| R6 | Réclamation résolue encore modifiable | Réclamations | 2 | 3 | 6 | Unitaire, API |
| R7 | Données perdues ou incohérentes en base | Persistance | 2 | 3 | 6 | Intégration |
| R8 | Téléversement de fichier dangereux ou trop volumineux (Multer) | Réclamations | 2 | 3 | 6 | API, sécurité |
| R9 | Mauvais codes HTTP ou messages d'erreur trop détaillés | API REST | 2 | 2 | 4 | Postman |
| R10 | Recherche, filtre ou tri erronés | Recherche | 2 | 2 | 4 | E2E, API |
| R11 | Compteurs du tableau de bord faux | Suivi | 2 | 2 | 4 | E2E, intégration |
| R12 | Lenteur sous charge | Global | 2 | 2 | 4 | k6 |
| R13 | Inscription avec email déjà utilisé ou rôle choisi librement (élévation de privilèges) | Utilisateurs | 2 | 3 | 6 | API |

Les risques de score 9 (R1, R2, R3) sont testés en priorité, à plusieurs niveaux.

## 2. Périmètre
**Inclus :** authentification, gestion des réclamations, statuts, droits par rôle, recherche et filtres, API REST, persistance SQLite, un parcours d'interface, un test de performance.

**Exclus (avec justification) :**
- Compatibilité multi-navigateurs complète : un seul navigateur, par manque de temps.
- Audit de sécurité approfondi : seulement des contrôles élémentaires.
- Tests sur le déploiement Docker et Nginx : environnement local uniquement.
- Notifications ou emails : non prévus par le sujet.

## 3. Hypothèses
- Le référentiel de test est celui du sujet, adapté aux statuts et rôles réels de HostelOps.
- Les différences sont listées dans `01-fiche-projet.md`, section 6.
- Les tests s'exécutent sur une base SQLite de test, jamais sur des données réelles.
