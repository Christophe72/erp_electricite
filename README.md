# ERP Électricité - Système de Gestion d'Entreprise

## 📋 Description

**ERP Électricité** est un système de gestion d'entreprise (Enterprise Resource Planning) spécialement conçu pour les entreprises du secteur électrique. Cette application web développée avec Spring Boot permet de gérer efficacement les clients, les projets, les matériaux et les chantiers d'une entreprise d'électricité.

## 🏗️ Architecture du Projet

Le projet suit l'architecture MVC (Model-View-Controller) de Spring Boot avec une structure organisée en couches :

```
src/main/java/com/monsociete/erp/
├── ErpApplication.java          # Classe principale Spring Boot
├── model/                       # Entités JPA
│   ├── Client.java             # Entité Client
│   ├── Material.java           # Entité Matériel
│   └── Project.java            # Entité Projet
├── repository/                  # Couche d'accès aux données
│   └── ClientRepository.java   # Repository pour les clients
├── service/                     # Couche métier
│   └── ClientService.java      # Service de gestion des clients
└── web/                        # Contrôleurs web
    └── ClientController.java   # Contrôleur pour les clients
```

## 🚀 Fonctionnalités

### ✅ Fonctionnalités Implémentées
- **Gestion des Clients** : Création, consultation, modification et suppression des clients
- **Interface Web** : Interface utilisateur moderne avec Bootstrap 5
- **Base de Données** : Persistance des données avec H2 (base de données en mémoire)
- **Console H2** : Accès direct à la base de données pour le développement

### 🔄 Fonctionnalités à Développer
- **Gestion des Projets** : CRUD complet pour les projets/chantiers
- **Gestion des Matériaux** : Suivi des stocks et des approvisionnements
- **Planification** : Calendrier des interventions et planification des chantiers
- **Facturation** : Génération de devis et factures
- **Reporting** : Tableaux de bord et rapports d'activité

## 🛠️ Technologies Utilisées

- **Java 17** : Langage de programmation principal
- **Spring Boot 3.1.0** : Framework de développement
- **Spring Data JPA** : Persistance des données
- **Spring Web MVC** : Architecture web
- **Thymeleaf** : Moteur de template pour les vues
- **H2 Database** : Base de données en mémoire pour le développement
- **Bootstrap 5** : Framework CSS pour l'interface utilisateur
- **Maven** : Gestionnaire de dépendances et build

## 📦 Prérequis

- **Java Development Kit (JDK) 17** ou supérieur
- **Apache Maven 3.6+** pour la gestion des dépendances
- **IDE recommandé** : IntelliJ IDEA, Eclipse ou VS Code avec extensions Java

## 🚀 Installation et Démarrage

### 1. Cloner le Projet
```bash
git clone [URL_DU_REPOSITORY]
cd erp-electricite-starter
```

### 2. Installer les Dépendances
```bash
mvn clean install
```

### 3. Lancer l'Application
```bash
mvn spring-boot:run
```

### 4. Accéder à l'Application
- **Interface Web** : http://localhost:8080
- **Console H2** : http://localhost:8080/h2-console
  - URL JDBC : `jdbc:h2:mem:erpdb`
  - Utilisateur : `sa`
  - Mot de passe : (laisser vide)

## 🗃️ Modèle de Données

### Client
Représente les clients de l'entreprise d'électricité.
```java
- id : Long (Clé primaire)
- nom : String (Nom du client)
- adresse : String (Adresse complète)
- email : String (Email de contact)
- telephone : String (Numéro de téléphone)
```

### Material (À développer)
Représente les matériaux et équipements électriques.
```java
- id : Long (Clé primaire)
- reference : String (Référence du matériel)
- nom : String (Nom du matériel)
- description : String (Description détaillée)
- quantiteStock : int (Quantité en stock)
- prixUnitaire : double (Prix unitaire)
```

### Project (À développer)
Représente les projets/chantiers électriques.
```java
- id : Long (Clé primaire)
- reference : String (Référence du projet)
- description : String (Description du projet)
- adresseChantier : String (Adresse du chantier)
- dateDebut : LocalDate (Date de début)
- dateFinPrevue : LocalDate (Date de fin prévue)
- statut : String (Statut du projet)
- client : Client (Client associé)
```

## 🌐 API et Endpoints

### Gestion des Clients
- `GET /clients` : Liste tous les clients
- `GET /clients/nouveau` : Formulaire de création d'un nouveau client
- `POST /clients/save` : Sauvegarde d'un client
- `GET /clients/delete/{id}` : Suppression d'un client

### Page d'Accueil
- `GET /` : Page d'accueil de l'application

## 🔧 Configuration

### Base de Données
La configuration de la base de données H2 se trouve dans `application.properties` :
```properties
spring.datasource.url=jdbc:h2:mem:erpdb;DB_CLOSE_DELAY=-1;MODE=PostgreSQL
spring.datasource.username=sa
spring.datasource.password=
spring.jpa.hibernate.ddl-auto=update
spring.h2.console.enabled=true
```

### Serveur Web
- **Port** : 8080 (configurable dans `application.properties`)
- **Cache Thymeleaf** : Désactivé pour le développement

## 🧪 Tests

Pour exécuter les tests unitaires :
```bash
mvn test
```

## 📈 Développement Futur

### Priorités de Développement
1. **Finaliser les entités** Material et Project avec leurs getters/setters
2. **Créer les repositories** pour Material et Project
3. **Développer les services** pour la logique métier
4. **Implémenter les contrôleurs** pour les nouvelles entités
5. **Créer les vues Thymeleaf** pour les interfaces utilisateur
6. **Ajouter la validation** des données avec Bean Validation
7. **Implémenter la sécurité** avec Spring Security
8. **Migrer vers une base de données** de production (PostgreSQL/MySQL)

### Améliorations Techniques
- Ajout de tests d'intégration
- Documentation de l'API avec Swagger/OpenAPI
- Logging avec Logback
- Profils de configuration (dev, test, prod)
- Containerisation avec Docker

## 👥 Contribution

1. Fork le projet
2. Créer une branche pour votre fonctionnalité (`git checkout -b feature/nouvelle-fonctionnalite`)
3. Committer vos changements (`git commit -am 'Ajout de la nouvelle fonctionnalité'`)
4. Pousser vers la branche (`git push origin feature/nouvelle-fonctionnalite`)
5. Créer une Pull Request

## 📝 Licence

Ce projet est développé dans un cadre éducatif pour l'apprentissage de Spring Boot.

## 📞 Support

Pour toute question ou problème, veuillez créer une issue sur le repository du projet.

---

**Projet développé avec ❤️ pour l'apprentissage de Spring Boot et la gestion d'entreprises d'électricité**
