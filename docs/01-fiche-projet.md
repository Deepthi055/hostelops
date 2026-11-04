# Fiche projet : test et validation de HostelOps

## 1. Présentation
| Élément | Contenu |
|---|---|
| Système testé | HostelOps, application web de gestion des réclamations d'un foyer d'étudiants |
| Dépôt d'origine | https://github.com/Deepthi055/hostelops |
| Dépôt de test (fork) | https://github.com/ghada12-ygb/hostelops |
| Équipe | Ghada Yaakoubi, [binôme éventuel] |
| Encadrant | [nom] |
| Période | 10 semaines |

## 2. Technologies du système testé
- Backend : Node.js, Express, Sequelize, SQLite, JWT, bcryptjs, Multer
- Frontend : React 18, React Router, Axios, Context API
- Déploiement : Docker, Docker Compose, Nginx

## 3. Utilisateurs et rôles
| Rôle HostelOps | Équivalent RéclaGest |
|---|---|
| Étudiant | Client |
| Administrateur | Administrateur |
| (aucun agent observé) [À VÉRIFIER] | Agent |

## 4. Fonctions observées
Connexion, tableau de bord avec compteurs (total, en attente, en cours, résolues), dépôt d'une réclamation, recherche par description ou catégorie, filtre par statut, tri, liste des réclamations de l'utilisateur.

## 5. Fonctions critiques
1. Authentification (JWT)
2. Dépôt d'une réclamation et validation des champs
3. Changement de statut par l'administrateur
4. Isolation des données : un étudiant ne voit que ses réclamations
5. Persistance en base SQLite

## 6. Écarts avec le référentiel du sujet (à confirmer par exploration)
| Règle du sujet | Constat sur HostelOps | Statut |
|---|---|---|
| Statuts NOUVELLE, EN_COURS, RESOLUE, CLOTUREE | Pending, In Progress, Resolved (3 statuts) | À vérifier |
| Titre obligatoire de 5 à 100 caractères | Pas de champ titre visible | À vérifier |
| Description de 10 à 1 000 caractères | Limites inconnues | À tester |
| Rôle agent | Non observé | À vérifier |
| Réclamation clôturée non modifiable | Pas de statut clôturé | À adapter |

Adaptation retenue : la règle « clôturée non modifiable » sera appliquée au statut **Resolved**, sauf si l'exploration montre un autre comportement.

## 7. Distinctions de vocabulaire
- **Erreur** : faute humaine du développeur.
- **Défaut** : trace de cette erreur dans le code.
- **Défaillance** : comportement incorrect observé à l'exécution.
- **Vérification** : le produit respecte-t-il sa spécification ?
- **Validation** : le produit répond-il au besoin de l'utilisateur ?

## 8. Objectif
Évaluer la qualité de HostelOps, détecter les anomalies et décider de sa livraison (validation, validation conditionnelle ou refus).
