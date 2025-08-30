# ERP Électricité - Système de Gestion d'Entreprise

## 📋 Description

**ERP Électricité** est un système de gestion d'entreprise (Enterprise Resource Planning) spécialement conçu pour les entreprises du secteur électrique. Cette application web développée avec Spring Boot permet de gérer efficacement les clients, les projets, les matériaux et les chantiers d'une entreprise d'électricité.

## 🏗️ Architecture du Projet

Le projet suit l'architecture MVC (Model-View-Controller) de Spring Boot avec une structure organisée en couches :

```
src/main/java/com/monsociete/erp/
├── ErpApplication.java              # Classe principale Spring Boot
├── model/                           # Entités JPA
│   ├── Client.java                 # Entité Client
│   ├── Material.java               # Entité Matériel
│   └── Project.java                # Entité Projet/Chantier
├── repository/                      # Couche d'accès aux données
│   ├── ClientRepository.java       # Repository pour les clients
│   ├── MaterialRepository.java     # Repository pour les matériaux
│   └── ProjectRepository.java      # Repository pour les projets
├── service/                         # Couche métier
│   ├── ClientService.java          # Service de gestion des clients
│   ├── MaterialService.java        # Service de gestion des matériaux
│   └── ProjectService.java         # Service de gestion des projets
└── web/                            # Contrôleurs web
    ├── ClientController.java       # Contrôleur pour les clients
    ├── MaterialController.java     # Contrôleur pour les matériaux
    └── ProjectController.java      # Contrôleur pour les projets
```

## 🚀 Fonctionnalités

### ✅ Fonctionnalités Implémentées
- **Gestion des Clients** : Création, consultation, modification et suppression des clients
- **Gestion des Projets** : CRUD complet pour les projets/chantiers électriques
- **Gestion des Matériaux** : Suivi des stocks et gestion des matériaux
- **Recherche Avancée** : Recherche de projets par différents critères
- **Projets en Retard** : Identification automatique des projets en retard
- **Interface Web** : Interface utilisateur moderne avec Bootstrap 5
- **Base de Données** : Persistance des données avec H2 (base de données en mémoire)
- **Console H2** : Accès direct à la base de données pour le développement

### 🔄 Fonctionnalités à Développer
- **Planification** : Calendrier des interventions et planification des chantiers
- **Facturation** : Génération de devis et factures
- **Reporting** : Tableaux de bord et rapports d'activité
- **Gestion des Employés** : Affectation du personnel aux chantiers
- **Suivi des Coûts** : Analyse de la rentabilité des projets

## 🛠️ Technologies Utilisées

- **Java 17** : Langage de programmation principal
- **Spring Boot 3.1.0** : Framework de développement
- **Spring Data JPA** : Persistance des données avec requêtes JPQL
- **Spring Web MVC** : Architecture web
- **Thymeleaf** : Moteur de template pour les vues
- **H2 Database** : Base de données en mémoire pour le développement
- **Bootstrap 5** : Framework CSS pour l'interface utilisateur
- **Maven** : Gestionnaire de dépendances et build

## 🚀 Installation et Démarrage

### Prérequis
- Java 17 ou version supérieure
- Maven 3.6+ 
- Un IDE Java (IntelliJ IDEA, Eclipse, VS Code)

### Étapes d'installation

1. **Cloner le projet**
```bash
git clone [URL_DU_REPOSITORY]
cd erp-electricite-starter
```

2. **Installer les dépendances**
```bash
mvn clean install
```

3. **Démarrer l'application**
```bash
mvn spring-boot:run
```

4. **Accéder à l'application**
- Application web : http://localhost:8080
- Console H2 : http://localhost:8080/h2-console
  - URL JDBC : `jdbc:h2:mem:testdb`
  - Nom d'utilisateur : `sa`
  - Mot de passe : (laisser vide)

## 📊 Modèle de Données

### Entité Client
- **id** : Identifiant unique
- **nom** : Nom du client
- **prenom** : Prénom du client
- **email** : Adresse email
- **telephone** : Numéro de téléphone
- **adresse** : Adresse complète

### Entité Project (Projet/Chantier)
- **id** : Identifiant unique
- **reference** : Référence unique du projet
- **description** : Description du projet
- **adresseChantier** : Adresse du chantier
- **dateDebut** : Date de début prévue
- **dateFinPrevue** : Date de fin prévue
- **statut** : Statut du projet (En cours, Terminé, En attente)
- **client** : Relation vers le client propriétaire

### Entité Material (Matériel)
- **id** : Identifiant unique
- **nom** : Nom du matériel
- **description** : Description détaillée
- **quantiteStock** : Quantité en stock
- **prixUnitaire** : Prix unitaire
- **categorie** : Catégorie du matériel

## 🔍 Requêtes JPQL Spécialisées

Le projet utilise des requêtes JPQL personnalisées pour des fonctionnalités avancées :

### Recherche de Projets en Retard
```java
@Query("SELECT p FROM Project p WHERE p.dateFinPrevue < :dateActuelle AND p.statut <> 'Terminé'")
List<Project> findProjectsEnRetard(@Param("dateActuelle") LocalDate dateActuelle);
```

### Recherche de Projets se Terminant Prochainement
```java
@Query("SELECT p FROM Project p WHERE p.dateFinPrevue BETWEEN :dateDebut AND :dateFin AND p.statut <> 'Terminé'")
List<Project> findProjectsSeTerminantDans(@Param("dateDebut") LocalDate dateDebut, @Param("dateFin") LocalDate dateFin);
```

### Recherche par Description (Insensible à la Casse)
```java
@Query("SELECT p FROM Project p WHERE LOWER(p.description) LIKE LOWER(CONCAT('%', :description, '%'))")
List<Project> findByDescriptionContainingIgnoreCase(@Param("description") String description);
```

## 🐛 Corrections Récentes

### Correction JPQL - Août 2025
**Problème** : Erreur `BadJpqlGrammarException` due à l'utilisation incorrecte de l'opérateur `!=` dans les requêtes JPQL.

**Solution** : Remplacement de `!=` par `<>` qui est la syntaxe correcte en JPQL pour l'opérateur "différent de".

**Fichiers modifiés** :
- `ProjectRepository.java` : Correction des requêtes `findProjectsEnRetard` et `findProjectsSeTerminantDans`

## 📝 Structure des URLs

- `/` : Page d'accueil
- `/clients` : Liste des clients
- `/clients/nouveau` : Formulaire de création de client
- `/clients/{id}` : Détails d'un client
- `/projets` : Liste des projets
- `/projets/nouveau` : Formulaire de création de projet
- `/projets/{id}` : Détails d'un projet
- `/materiaux` : Liste des matériaux

## 🧪 Tests

Pour exécuter les tests :
```bash
mvn test
```

## 📚 Documentation API

La documentation détaillée des endpoints REST sera disponible avec l'intégration de Swagger/OpenAPI dans une future version.

## 🤝 Contribution

1. Fork le projet
2. Créer une branche pour votre fonctionnalité (`git checkout -b feature/AmazingFeature`)
3. Commit vos changements (`git commit -m 'Add some AmazingFeature'`)
4. Push vers la branche (`git push origin feature/AmazingFeature`)
5. Ouvrir une Pull Request

## 📄 Licence

Ce projet est sous licence MIT. Voir le fichier `LICENSE` pour plus de détails.

## 📞 Support

Pour toute question ou problème :
- Créer une issue sur le repository GitHub
- Contacter l'équipe de développement

---
**Version** : 1.0.0  
**Dernière mise à jour** : Août 2025
