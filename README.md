# 🎓 Projet Étudiants — Version 2 (Branche `version-2`)

Enrichissement complet du projet Spring Boot avec : BDD Cucumber, page web statique,
Docker Hub, Kubernetes K3S, architecture en couches, CRUD complet, gestion d'erreurs,
Swagger OpenAPI, cache Redis et Jira Scrum.

---

## 📁 Structure du projet

```
projet-etudiants/
├── api-spring-boot/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/example/etudiants/
│   │   │   │   ├── controller/       ← EtudiantController, DepartementController
│   │   │   │   ├── service/          ← EtudiantService, DepartementService
│   │   │   │   ├── repository/       ← EtudiantRepository, DepartementRepository
│   │   │   │   ├── entity/           ← Etudiant (+ age()), Departement
│   │   │   │   ├── dto/              ← EtudiantDTO, DepartementDTO
│   │   │   │   ├── mapper/           ← EtudiantMapper, DepartementMapper
│   │   │   │   └── config/           ← AppConfig, GlobalExceptionHandler, ...
│   │   │   └── resources/
│   │   │       └── static/index.html ← Interface web (Q4)
│   │   └── test/
│   │       ├── java/.../bdd/         ← CucumberRunner, EtudiantSteps (Q3)
│   │       └── resources/features/   ← etudiant.feature (Q3)
│   ├── Dockerfile
│   └── pom.xml
├── k8s/
│   ├── etudiant-deployment.yaml      ← API + Service K8s (Q6)
│   └── postgres-deployment.yaml      ← PostgreSQL + Redis K8s (Q6)
├── docker-compose.yml                ← PostgreSQL + Redis + API
└── README.md
```

---

## 🚀 Lancer avec Docker Compose

```bash
# Branche version-2
git checkout -b version-2

# Démarrer PostgreSQL + Redis + API
docker compose up --build

# API disponible sur :
http://localhost:8080/api/etudiants

# Interface web :
http://localhost:8080/index.html

# Swagger UI :
http://localhost:8080/swagger-ui.html
```

---

## 🧪 Lancer les tests BDD Cucumber (Q3)

```bash
cd api-spring-boot
mvn test
```

---

## 🐳 Publier sur Docker Hub (Q5)

```bash
cd api-spring-boot
docker build -t <votre-username>/etudiant-service:1.0 .
docker login
docker push <votre-username>/etudiant-service:1.0
```

---

## ☸️ Déployer sur K3S (Q6)

```bash
# Sur la VM avec K3S installé
kubectl apply -f k8s/postgres-deployment.yaml
kubectl apply -f k8s/etudiant-deployment.yaml

# Vérifier
kubectl get pods
kubectl get services

# Accès via port-forward
kubectl port-forward service/etudiant-service 8080:8080

# Ou via NodePort
http://<IP-VM>:30080/api/etudiants
```

---

## 📡 Endpoints API

### Étudiants
| Méthode | URL | Description |
|---|---|---|
| GET | `/api/etudiants` | Liste tous les étudiants |
| GET | `/api/etudiants?annee=2020` | Filtre par année d'inscription |
| GET | `/api/etudiants/{id}` | Récupère un étudiant |
| POST | `/api/etudiants` | Crée un étudiant (201) |
| PUT | `/api/etudiants/{id}` | Met à jour un étudiant |
| DELETE | `/api/etudiants/{id}` | Supprime un étudiant (204) |

### Départements
| Méthode | URL | Description |
|---|---|---|
| GET | `/api/departements` | Liste tous les départements |
| GET | `/api/departements/{id}` | Récupère un département |
| POST | `/api/departements` | Crée un département (201) |
| PUT | `/api/departements/{id}` | Met à jour un département |
| DELETE | `/api/departements/{id}` | Supprime un département (204) |

---

## 📋 Jira Scrum — Structure

```
Epic : Gestion des Étudiants
├── Sprint 1 — API REST de base (Partie 1)
│   ├── US-01 : Lister les étudiants (GET /api/etudiants)
│   ├── US-02 : Dockeriser l'application
│   └── US-03 : Application mobile Flutter
└── Sprint 2 — Enrichissement (Partie 2)
    ├── US-04 : Méthode age() + tests BDD Cucumber
    ├── US-05 : Interface web statique (index.html)
    ├── US-06 : Docker Hub + publication image
    ├── US-07 : Déploiement Kubernetes K3S
    ├── US-08 : Entité Département + relation ManyToOne
    ├── US-09 : Architecture en couches (DTO, Mapper, Service)
    ├── US-10 : CRUD complet Etudiant + Département
    ├── US-11 : Gestion des erreurs HTTP (@RestControllerAdvice)
    ├── US-12 : Documentation Swagger / OpenAPI
    └── US-13 : Cache Redis (@Cacheable, @CacheEvict)
```

### Exemple de commits liés à Jira :
```bash
git commit -m "PROJ-04 : ajout méthode age() et tests BDD Cucumber"
git commit -m "PROJ-08 : ajout entité Département avec relation ManyToOne"
git commit -m "PROJ-13 : intégration cache Redis avec @Cacheable"
```

---

## 🛠️ Technologies

| Composant | Technologie |
|---|---|
| API REST | Spring Boot 3.2, Java 21 |
| ORM | Spring Data JPA / Hibernate |
| Cache | Redis 7 + Spring Cache |
| Base de données | PostgreSQL 16 |
| Tests BDD | Cucumber 7 + JUnit 5 |
| Documentation | Swagger UI / SpringDoc OpenAPI 2 |
| Containerisation | Docker, Docker Compose |
| Orchestration | Kubernetes / K3S |
| Application mobile | Flutter 3 |

---

## 👨‍🏫 Formateur : Wahid Hamdi
