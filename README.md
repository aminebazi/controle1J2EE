# 📦 Mini service de gestion de campagnes de dons

Projet de contrôle de l'UE "Architecture JEE" – 4e année IIR  
🧑‍🏫 Pr. AHAIDOUS Khadija  
📅 Date : 18/04/2025

## ⚙️ Environnement
- **Java 17+**
- **Spring Boot**
- **Spring Data JPA**
- **Base H2 en mémoire**
- **IDE** : IntelliJ IDEA
- **Outils bonus** : Swagger pour la documentation de l'API

---

## ✅ Ce qui a été réalisé

### 🧩 Modélisation (JPA Entities)
- **Campagne** : `id`, `nom`, `objectifMontant`, `dateDebut`, `dateFin`
- **Don** : `id`, `campagne (ManyToOne)`, `nomDonateur`, `montant`, `date`

### 🗂️ Répertoires (Repositories)
- `CampagneRepository` (hérite de `JpaRepository`)
- `DonRepository` (hérite de `JpaRepository`)

### 🔄 DTOs
- `DonDTO` : `id`, `nomCampagne`, `nomDonateur`, `montant`, `date`

### 📊 Projection
- `CampagneRésumé` : Interface avec getters pour `id`, `nom`, `objectifMontant`

### 🛠️ Services
- `ServiceCampagne` :
  - Méthode pour récupérer les campagnes actives (en fonction des dates)
- `ServiceDon` :
  - Méthode pour enregistrer un don
  - Méthode pour transformer une entité `Don` en `DonDTO`

### 🌐 API REST
- **GET** `/api/campagnes/actives`  
  ↳ Retourne la liste des campagnes actives (projection `CampagneRésumé`)
- **POST** `/api/campagnes/{id}/dons`  
  ↳ Permet d’enregistrer un don à une campagne existante (reçoit un `DonDTO`)

### ✔️ Validation et Gestion des erreurs
- Utilisation de `@Valid` :
  - `montant > 0`
  - `nomDonateur` non vide
- Gestion des erreurs centralisée avec `@ControllerAdvice`

### 🧪 Tests
- ✅ Test unitaire de `ServiceCampagne`
- ✅ Test d’intégration de l’API (contrôleur de dons)




## 🚀 Lancement rapide

```bash
# Cloner le projet
git clone https://github.com/ton-compte/mini-don-service.git
cd mini-don-service

# Lancer l'application (avec Maven Wrapper)
./mvnw spring-boot:run
