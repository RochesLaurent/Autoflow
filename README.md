# 🚀 Autoflow

**La plateforme SaaS moderne de gestion administrative et fiscale pour micro-entrepreneurs français**

> L'outil de gestion le plus simple et moderne pour micro-entrepreneurs, créé par un développeur pour des entrepreneurs.

[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)](#)
[![License](https://img.shields.io/badge/license-Proprietary-red.svg)](LICENSE)
[![Build Status](https://img.shields.io/badge/build-passing-brightgreen.svg)](#)

---
⚠️ **PROJET PROPRIÉTAIRE** - Ce repository contient du code propriétaire et confidentiel. Accès restreint aux membres autorisés de l'équipe uniquement.

---

## 📋 Table des matières

- [🎯 Vision du projet](#-vision-du-projet)
- [✨ Fonctionnalités principales](#-fonctionnalités-principales)
- [🏗️ Architecture technique](#️-architecture-technique)
- [🚀 Installation et démarrage](#-installation-et-démarrage)
- [💰 Plans tarifaires](#-plans-tarifaires)
- [📊 Base de données](#-base-de-données)
- [🔧 API et intégrations](#-api-et-intégrations)
- [🧪 Tests et qualité](#-tests-et-qualité)
- [📈 Roadmap](#-roadmap)
- [🤝 Contribution](#-contribution)

## 🎯 Vision du projet

Autoflow révolutionne la gestion administrative des micro-entrepreneurs français en proposant une plateforme SaaS moderne, intuitive et conforme aux réglementations URSSAF.

### Public cible
- **Primaire** : Développeurs web freelances, consultants IT
- **Secondaire** : Tous micro-entrepreneurs (artisans, consultants, professions libérales)
- **Tertiaire** : Futurs créateurs d'entreprise

### Proposition de valeur
- ✅ Conformité automatique URSSAF et fiscale
- ✅ Interface moderne et intuitive
- ✅ Gestion multi-régimes (BNC, BIC prestations, BIC ventes)
- ✅ Intégrations bancaires automatiques
- ✅ Analytics avancées et reporting

## ✨ Fonctionnalités principales

### 📊 Dashboard intelligent
- Chiffre d'affaires en temps réel
- Suivi des seuils légaux (TVA, plafonds micro-entreprise)
- Alertes automatiques et notifications
- Métriques personnalisables

### 🧾 Gestion des factures
- Éditeur WYSIWYG avec templates professionnels
- Calculs automatiques HT/TTC selon régime
- Factures récurrentes et devis
- Export PDF et envoi automatique

### 👥 Gestion des clients
- Base clients complète avec historique
- Segmentation par tags
- Import/Export CSV/Excel
- Suivi des délais de paiement

### ⚖️ Conformité URSSAF
- Livre des recettes automatique
- Calculs cotisations sociales en temps réel
- Rappels déclarations URSSAF
- Support multi-régimes avec répartition automatique

### 🏦 Intégrations bancaires
- Open Banking (PSD2) avec principales banques françaises
- Rapprochement automatique factures/paiements
- Notifications de paiement en temps réel

## 🏗️ Architecture technique

### Stack technologique

**Frontend**
```
React 18+ + TypeScript
Vite (Build tool)
Tailwind CSS + HeadlessUI
Zustand (State management)
React Hook Form + Zod
Recharts (Analytics)
```

**Backend**
```
Symfony 6.4 LTS
API Platform (REST/GraphQL)
Doctrine ORM
JWT + Refresh Tokens
MySQL 8.0+
Redis (Cache & Sessions)
```

**Infrastructure**
```
Docker + Docker Compose
GitHub Actions (CI/CD)
AWS S3 (Storage)
Sentry (Monitoring)
```

### Architecture système

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   React SPA     │◄──►│   Symfony API    │◄──►│     MySQL       │
│   (Port 3000)   │    │   (Port 8000)    │    │   (Port 3306)   │
└─────────────────┘    └──────────────────┘    └─────────────────┘
        │                       │                       │
        ▼                       ▼                       │
┌─────────────────┐    ┌─────────────────┐              │
│     Redis       │    │  File Storage   │              │
│   (Port 6379)   │    │    (AWS S3)     │              │
└─────────────────┘    └─────────────────┘              │
        │                       │                       │
        ▼                       ▼                       ▼
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│ Service Workers │    │   Monitoring    │    │    Backup       │
│  (Background)   │    │ (Sentry/Logs)   │    │   (Automated)   │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

## 🚀 Installation et démarrage

### Prérequis
- Node.js 18+
- PHP 8.1+
- MySQL 8.0+
- Redis
- Docker (optionnel)

### Installation avec Docker (recommandé)

```bash
# Cloner le repository (accès autorisé requis)
git clone [REPOSITORY_URL]
cd autoflow

# Démarrer avec Docker
docker-compose up -d

# Installer les dépendances frontend
cd frontend
npm install
npm run dev

# Installer les dépendances backend
cd ../backend
composer install
php bin/console doctrine:migrations:migrate
```

### Installation manuelle

```bash
# Configuration base de données
cp .env.example .env
# Éditer .env avec vos paramètres

# Backend
cd backend
composer install
php bin/console doctrine:database:create
php bin/console doctrine:migrations:migrate
php bin/console doctrine:fixtures:load
symfony server:start

# Frontend
cd ../frontend
npm install
npm run dev
```

### Accès à l'application
- Frontend : http://localhost:3000
- Backend API : http://localhost:8000
- Documentation API : http://localhost:8000/api/docs

## 💰 Plans tarifaires

### 🆓 Essai gratuit
- **14 jours** sans carte bancaire
- Accès à toutes les fonctionnalités Pro

### 💎 Starter - 5,99€/mois
- ✅ 25 factures/mois max
- ✅ 10 clients max
- ✅ Dashboard métriques de base
- ✅ Export PDF factures
- ✅ Support email (48h)
- ✅ 100 MB stockage

### 🚀 Pro - 9,99€/mois
- ✅ Factures illimitées
- ✅ Clients illimités
- ✅ Analytics avancées + métriques personnalisées
- ✅ Export PDF + Excel + API
- ✅ Rappels automatiques clients
- ✅ Intégrations bancaires + comptables
- ✅ Support email (24h) + Chat
- ✅ 1 GB stockage
- ✅ Multi-régimes BIC/BNC/Mixte

## 📊 Base de données

### Modèle de données principal

```sql
-- Utilisateurs et authentification
users (id, email, password_hash, status, trial_ends_at, ...)
subscriptions (id, user_id, plan_type, status, stripe_subscription_id, ...)
company_profiles (id, user_id, company_name, siret, regime_type, ...)

-- Gestion commerciale
clients (id, user_id, company_name, contact_info, payment_terms, ...)
invoices (id, user_id, client_id, status, amounts, due_date, ...)
invoice_items (id, invoice_id, description, quantity, unit_price, ...)
quotes (id, user_id, client_id, status, converted_to_invoice_id, ...)

-- Conformité fiscale
revenue_book (id, user_id, invoice_id, revenue_date, amount, regime_type, ...)
urssaf_declarations (id, user_id, period, revenue_amount, contributions, ...)

-- Intégrations et automatisation
bank_integrations (id, user_id, bank_name, access_tokens, ...)
bank_transactions (id, bank_integration_id, amount, matched_invoice_id, ...)
automatic_reminders (id, user_id, invoice_id, reminder_type, sent_at, ...)
```

### Schéma complet
Le fichier `AutoFlow.sql` contient le schéma complet avec toutes les relations, contraintes et index optimisés.

## 🔧 API et intégrations

### API REST

```bash
# Authentification
POST /api/auth/login
POST /api/auth/refresh
POST /api/auth/logout

# Facturation
GET    /api/invoices
POST   /api/invoices
PUT    /api/invoices/{id}
DELETE /api/invoices/{id}

# Clients
GET    /api/clients
POST   /api/clients
PUT    /api/clients/{id}

# Analytics
GET    /api/dashboard/metrics
GET    /api/dashboard/charts

# URSSAF
GET    /api/urssaf/declarations
POST   /api/urssaf/declarations
```

### Webhooks disponibles
- `invoice.created`
- `invoice.paid`
- `threshold.reached`
- `payment.received`

### Intégrations bancaires
- Crédit Agricole, BNP Paribas, Société Générale
- LCL, CIC, Banque Postale
- Banques en ligne : Boursorama, Hello Bank
- Néobanques : Qonto, Shine, Manager.one

## 🧪 Tests et qualité

### Stratégie de tests

**Frontend (React)**
```bash
# Tests unitaires
npm run test              # Jest + React Testing Library
npm run test:coverage     # Coverage report

# Tests E2E
npm run cypress:open      # Interface Cypress
npm run cypress:run       # Headless

# Tests visuels
npm run chromatic         # Régression visuelle
```

**Backend (Symfony)**
```bash
# Tests unitaires
php bin/phpunit                    # >95% coverage
php bin/phpunit --coverage-html    # Rapport HTML

# Tests fonctionnels
php bin/phpunit tests/Functional   # API tests

# Analyse qualité
vendor/bin/php-cs-fixer fix        # Code style
vendor/bin/phpstan analyse         # Analyse statique
```

### Pipeline CI/CD

```yaml
# .github/workflows/ci.yml
- Code Quality (ESLint, PHP-CS-Fixer, SonarCloud)
- Tests (Jest, PHPUnit, Cypress)
- Security (OWASP ZAP scans)
- Build & Deploy (Docker, Staging, Production)
- Monitoring (Sentry, Performance, Uptime)
```

### Métriques qualité
- ✅ Coverage frontend : >90%
- ✅ Coverage backend : >95%
- ✅ Performance : <2s page load
- ✅ Uptime : >99.9%
- ✅ Security : 0 incidents critiques

## 📈 Roadmap

### 🎯 MVP (Mois 1-3) ✅
- [ ] Architecture & environnements
- [ ] Authentication & user management
- [ ] CRUD factures et clients
- [ ] Dashboard simple
- [ ] Calculs régime BNC
- [ ] Système abonnements Stripe

### 🚀 Version 1.0 (Mois 4-6)
- [ ] Multi-régimes (BIC/BNC/Mixte)
- [ ] Métriques personnalisables
- [ ] Rappels URSSAF automatiques
- [ ] API complète
- [ ] Onboarding optimisé
- [ ] Mobile responsive

### 📱 Version 2.0 (Mois 7-12)
- [ ] Progressive Web App
- [ ] Intégrations bancaires avancées
- [ ] Module CRM
- [ ] Multi-utilisateurs (équipes)
- [ ] Expansion internationale (Belgique/Suisse)

### 🔮 Version 3.0+ (An 2)
- [ ] Intelligence artificielle (prédictions, automatisation)
- [ ] Module comptabilité complète
- [ ] Gestion RH (micro → PME)
- [ ] Marketplace d'intégrations

## 🤝 Développement en équipe

### Accès au repository

Ce projet est **privé et propriétaire**. L'accès est limité aux membres autorisés de l'équipe de développement. Pour obtenir l'accès :

1. Contacter l'administrateur du projet
2. Signer l'accord de confidentialité (NDA)
3. Recevoir les autorisations Git appropriées

### Guidelines de développement

**Confidentialité**
- ❌ Ne jamais partager le code en dehors de l'équipe
- ❌ Ne pas créer de forks publics
- ❌ Ne pas publier de screenshots ou extraits
- ✅ Utiliser uniquement les canaux de communication autorisés

**Workflow de développement**

1. **Créer** une branche feature (`git checkout -b feature/amazing-feature`)
2. **Développer** en suivant les standards de l'équipe
3. **Tester** localement (tests requis)
4. **Commit** avec messages descriptifs
5. **Push** et créer une **Pull Request**
6. **Review** par un membre senior avant merge

### Standards de code

**Frontend**
- ESLint + Prettier configuration
- Tests unitaires requis (coverage >90%)
- Documentation JSDoc pour fonctions publiques

**Backend**
- PSR-12 coding standard
- Tests PHPUnit requis (coverage >95%)
- Documentation Symfony standards

### Architecture des commits
```
feat: add bank integration for Crédit Agricole
fix: resolve invoice PDF generation issue
docs: update API documentation
test: add unit tests for URSSAF calculations
refactor: optimize dashboard performance
```

## 📞 Support et contacts

### Équipe interne
- **Lead Developer** : [email_lead@autoflow.fr]
- **Product Owner** : [email_po@autoflow.fr]
- **DevOps** : [email_devops@autoflow.fr]

### Environnements
- **Production** : [URL_PRODUCTION]
- **Staging** : [URL_STAGING]
- **Documentation interne** : [URL_DOCS_INTERNE]

### Outils équipe
- **Project Management** : [Lien_vers_outil]
- **Chat équipe** : [Slack/Discord_prive]
- **Monitoring** : [URL_monitoring]

## 📄 Licence

Ce projet est sous **licence propriétaire**. Voir le fichier [LICENSE](LICENSE) pour les termes complets.

**⚠️ CONFIDENTIALITÉ :** Ce code est la propriété exclusive de RochesWebStudio et est protégé par le droit d'auteur et les accords de confidentialité.

---

**Autoflow** - La révolution de la gestion micro-entrepreneurs 🚀

*Développé par ROCHES Laurent - Tous droits réservés*