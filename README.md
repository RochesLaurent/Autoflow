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
```
Autoflow
├─ backend
│  ├─ .editorconfig
│  ├─ .env
│  ├─ .env.dev
│  ├─ bin
│  │  └─ console
│  ├─ composer.json
│  ├─ composer.lock
│  ├─ config
│  │  ├─ bundles.php
│  │  ├─ packages
│  │  │  ├─ cache.yaml
│  │  │  ├─ framework.yaml
│  │  │  └─ routing.yaml
│  │  ├─ preload.php
│  │  ├─ routes
│  │  │  └─ framework.yaml
│  │  ├─ routes.yaml
│  │  └─ services.yaml
│  ├─ Dockerfile.dev
│  ├─ public
│  │  └─ index.php
│  ├─ src
│  │  ├─ Controller
│  │  └─ Kernel.php
│  ├─ symfony.lock
│  ├─ var
│  │  └─ cache
│  │     └─ dev
│  │        ├─ App_KernelDevDebugContainer.php
│  │        ├─ App_KernelDevDebugContainer.php.lock
│  │        ├─ App_KernelDevDebugContainer.php.meta
│  │        ├─ App_KernelDevDebugContainer.php.meta.json
│  │        ├─ App_KernelDevDebugContainer.preload.php
│  │        ├─ App_KernelDevDebugContainer.xml
│  │        ├─ App_KernelDevDebugContainer.xml.meta
│  │        ├─ App_KernelDevDebugContainer.xml.meta.json
│  │        ├─ App_KernelDevDebugContainerCompiler.log
│  │        ├─ App_KernelDevDebugContainerDeprecations.log
│  │        ├─ ContainerZYAsdwH
│  │        │  ├─ App_KernelDevDebugContainer.php
│  │        │  ├─ getArgumentResolver_BackedEnumResolverService.php
│  │        │  ├─ getArgumentResolver_DatetimeService.php
│  │        │  ├─ getArgumentResolver_DefaultService.php
│  │        │  ├─ getArgumentResolver_QueryParameterValueResolverService.php
│  │        │  ├─ getArgumentResolver_RequestAttributeService.php
│  │        │  ├─ getArgumentResolver_RequestPayloadService.php
│  │        │  ├─ getArgumentResolver_RequestService.php
│  │        │  ├─ getArgumentResolver_ServiceService.php
│  │        │  ├─ getArgumentResolver_SessionService.php
│  │        │  ├─ getArgumentResolver_VariadicService.php
│  │        │  ├─ getCacheWarmerService.php
│  │        │  ├─ getCache_AppClearerService.php
│  │        │  ├─ getCache_AppService.php
│  │        │  ├─ getCache_App_TaggableService.php
│  │        │  ├─ getCache_GlobalClearerService.php
│  │        │  ├─ getCache_SystemClearerService.php
│  │        │  ├─ getCache_SystemService.php
│  │        │  ├─ getConfigBuilder_WarmerService.php
│  │        │  ├─ getConsole_CommandLoaderService.php
│  │        │  ├─ getConsole_Command_AboutService.php
│  │        │  ├─ getConsole_Command_AssetsInstallService.php
│  │        │  ├─ getConsole_Command_CacheClearService.php
│  │        │  ├─ getConsole_Command_CachePoolClearService.php
│  │        │  ├─ getConsole_Command_CachePoolDeleteService.php
│  │        │  ├─ getConsole_Command_CachePoolInvalidateTagsService.php
│  │        │  ├─ getConsole_Command_CachePoolListService.php
│  │        │  ├─ getConsole_Command_CachePoolPruneService.php
│  │        │  ├─ getConsole_Command_CacheWarmupService.php
│  │        │  ├─ getConsole_Command_ConfigDebugService.php
│  │        │  ├─ getConsole_Command_ConfigDumpReferenceService.php
│  │        │  ├─ getConsole_Command_ContainerDebugService.php
│  │        │  ├─ getConsole_Command_ContainerLintService.php
│  │        │  ├─ getConsole_Command_DebugAutowiringService.php
│  │        │  ├─ getConsole_Command_DotenvDebugService.php
│  │        │  ├─ getConsole_Command_ErrorDumperService.php
│  │        │  ├─ getConsole_Command_EventDispatcherDebugService.php
│  │        │  ├─ getConsole_Command_RouterDebugService.php
│  │        │  ├─ getConsole_Command_RouterMatchService.php
│  │        │  ├─ getConsole_Command_SecretsDecryptToLocalService.php
│  │        │  ├─ getConsole_Command_SecretsEncryptFromLocalService.php
│  │        │  ├─ getConsole_Command_SecretsGenerateKeyService.php
│  │        │  ├─ getConsole_Command_SecretsListService.php
│  │        │  ├─ getConsole_Command_SecretsRemoveService.php
│  │        │  ├─ getConsole_Command_SecretsRevealService.php
│  │        │  ├─ getConsole_Command_SecretsSetService.php
│  │        │  ├─ getConsole_Command_YamlLintService.php
│  │        │  ├─ getConsole_ErrorListenerService.php
│  │        │  ├─ getContainer_EnvVarProcessorService.php
│  │        │  ├─ getContainer_EnvVarProcessorsLocatorService.php
│  │        │  ├─ getContainer_GetRoutingConditionServiceService.php
│  │        │  ├─ getDebug_ErrorHandlerConfiguratorService.php
│  │        │  ├─ getErrorControllerService.php
│  │        │  ├─ getErrorHandler_ErrorRenderer_HtmlService.php
│  │        │  ├─ getLoaderInterfaceService.php
│  │        │  ├─ getRedirectControllerService.php
│  │        │  ├─ getRouter_CacheWarmerService.php
│  │        │  ├─ getRouting_LoaderService.php
│  │        │  ├─ getSecrets_EnvVarLoaderService.php
│  │        │  ├─ getSecrets_VaultService.php
│  │        │  ├─ getServicesResetterService.php
│  │        │  ├─ getSession_FactoryService.php
│  │        │  ├─ getTemplateControllerService.php
│  │        │  ├─ get_Console_Command_About_LazyService.php
│  │        │  ├─ get_Console_Command_AssetsInstall_LazyService.php
│  │        │  ├─ get_Console_Command_CacheClear_LazyService.php
│  │        │  ├─ get_Console_Command_CachePoolClear_LazyService.php
│  │        │  ├─ get_Console_Command_CachePoolDelete_LazyService.php
│  │        │  ├─ get_Console_Command_CachePoolInvalidateTags_LazyService.php
│  │        │  ├─ get_Console_Command_CachePoolList_LazyService.php
│  │        │  ├─ get_Console_Command_CachePoolPrune_LazyService.php
│  │        │  ├─ get_Console_Command_CacheWarmup_LazyService.php
│  │        │  ├─ get_Console_Command_ConfigDebug_LazyService.php
│  │        │  ├─ get_Console_Command_ConfigDumpReference_LazyService.php
│  │        │  ├─ get_Console_Command_ContainerDebug_LazyService.php
│  │        │  ├─ get_Console_Command_ContainerLint_LazyService.php
│  │        │  ├─ get_Console_Command_DebugAutowiring_LazyService.php
│  │        │  ├─ get_Console_Command_DotenvDebug_LazyService.php
│  │        │  ├─ get_Console_Command_ErrorDumper_LazyService.php
│  │        │  ├─ get_Console_Command_EventDispatcherDebug_LazyService.php
│  │        │  ├─ get_Console_Command_RouterDebug_LazyService.php
│  │        │  ├─ get_Console_Command_RouterMatch_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsDecryptToLocal_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsEncryptFromLocal_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsGenerateKey_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsList_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsRemove_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsReveal_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsSet_LazyService.php
│  │        │  ├─ get_Console_Command_YamlLint_LazyService.php
│  │        │  ├─ get_ServiceLocator_ZHyJIs5Service.php
│  │        │  ├─ get_ServiceLocator_ZHyJIs5_KernelloadRoutesService.php
│  │        │  ├─ get_ServiceLocator_ZHyJIs5_KernelregisterContainerConfigurationService.php
│  │        │  ├─ removed-ids.php
│  │        │  └─ RequestPayloadValueResolverGhost01ca9cc.php
│  │        ├─ Symfony
│  │        │  └─ Config
│  │        │     ├─ Framework
│  │        │     │  ├─ AnnotationsConfig.php
│  │        │     │  ├─ AssetMapper
│  │        │     │  │  └─ PrecompressConfig.php
│  │        │     │  ├─ AssetMapperConfig.php
│  │        │     │  ├─ Assets
│  │        │     │  │  └─ PackageConfig.php
│  │        │     │  ├─ AssetsConfig.php
│  │        │     │  ├─ Cache
│  │        │     │  │  └─ PoolConfig.php
│  │        │     │  ├─ CacheConfig.php
│  │        │     │  ├─ CsrfProtectionConfig.php
│  │        │     │  ├─ EsiConfig.php
│  │        │     │  ├─ ExceptionConfig.php
│  │        │     │  ├─ Form
│  │        │     │  │  └─ CsrfProtectionConfig.php
│  │        │     │  ├─ FormConfig.php
│  │        │     │  ├─ FragmentsConfig.php
│  │        │     │  ├─ HtmlSanitizer
│  │        │     │  │  └─ SanitizerConfig.php
│  │        │     │  ├─ HtmlSanitizerConfig.php
│  │        │     │  ├─ HttpCacheConfig.php
│  │        │     │  ├─ HttpClient
│  │        │     │  │  ├─ DefaultOptions
│  │        │     │  │  │  ├─ PeerFingerprintConfig.php
│  │        │     │  │  │  ├─ RetryFailed
│  │        │     │  │  │  │  └─ HttpCodeConfig.php
│  │        │     │  │  │  └─ RetryFailedConfig.php
│  │        │     │  │  ├─ DefaultOptionsConfig.php
│  │        │     │  │  ├─ ScopedClientConfig
│  │        │     │  │  │  ├─ PeerFingerprintConfig.php
│  │        │     │  │  │  ├─ RetryFailed
│  │        │     │  │  │  │  └─ HttpCodeConfig.php
│  │        │     │  │  │  └─ RetryFailedConfig.php
│  │        │     │  │  └─ ScopedClientConfig.php
│  │        │     │  ├─ HttpClientConfig.php
│  │        │     │  ├─ JsonStreamerConfig.php
│  │        │     │  ├─ LockConfig.php
│  │        │     │  ├─ Mailer
│  │        │     │  │  ├─ DkimSignerConfig.php
│  │        │     │  │  ├─ EnvelopeConfig.php
│  │        │     │  │  ├─ HeaderConfig.php
│  │        │     │  │  ├─ SmimeEncrypterConfig.php
│  │        │     │  │  └─ SmimeSignerConfig.php
│  │        │     │  ├─ MailerConfig.php
│  │        │     │  ├─ Messenger
│  │        │     │  │  ├─ BusConfig
│  │        │     │  │  │  ├─ DefaultMiddlewareConfig.php
│  │        │     │  │  │  └─ MiddlewareConfig.php
│  │        │     │  │  ├─ BusConfig.php
│  │        │     │  │  ├─ RoutingConfig.php
│  │        │     │  │  ├─ Serializer
│  │        │     │  │  │  └─ SymfonySerializerConfig.php
│  │        │     │  │  ├─ SerializerConfig.php
│  │        │     │  │  ├─ TransportConfig
│  │        │     │  │  │  └─ RetryStrategyConfig.php
│  │        │     │  │  └─ TransportConfig.php
│  │        │     │  ├─ MessengerConfig.php
│  │        │     │  ├─ Notifier
│  │        │     │  │  └─ AdminRecipientConfig.php
│  │        │     │  ├─ NotifierConfig.php
│  │        │     │  ├─ PhpErrorsConfig.php
│  │        │     │  ├─ ProfilerConfig.php
│  │        │     │  ├─ PropertyAccessConfig.php
│  │        │     │  ├─ PropertyInfoConfig.php
│  │        │     │  ├─ RateLimiter
│  │        │     │  │  ├─ LimiterConfig
│  │        │     │  │  │  └─ RateConfig.php
│  │        │     │  │  └─ LimiterConfig.php
│  │        │     │  ├─ RateLimiterConfig.php
│  │        │     │  ├─ RemoteeventConfig.php
│  │        │     │  ├─ RequestConfig.php
│  │        │     │  ├─ RouterConfig.php
│  │        │     │  ├─ SchedulerConfig.php
│  │        │     │  ├─ SecretsConfig.php
│  │        │     │  ├─ SemaphoreConfig.php
│  │        │     │  ├─ Serializer
│  │        │     │  │  ├─ MappingConfig.php
│  │        │     │  │  └─ NamedSerializerConfig.php
│  │        │     │  ├─ SerializerConfig.php
│  │        │     │  ├─ SessionConfig.php
│  │        │     │  ├─ SsiConfig.php
│  │        │     │  ├─ Translator
│  │        │     │  │  ├─ GlobalConfig.php
│  │        │     │  │  ├─ ProviderConfig.php
│  │        │     │  │  └─ PseudoLocalizationConfig.php
│  │        │     │  ├─ TranslatorConfig.php
│  │        │     │  ├─ TypeInfoConfig.php
│  │        │     │  ├─ UidConfig.php
│  │        │     │  ├─ Validation
│  │        │     │  │  ├─ AutoMappingConfig.php
│  │        │     │  │  ├─ MappingConfig.php
│  │        │     │  │  └─ NotCompromisedPasswordConfig.php
│  │        │     │  ├─ ValidationConfig.php
│  │        │     │  ├─ Webhook
│  │        │     │  │  └─ RoutingConfig.php
│  │        │     │  ├─ WebhookConfig.php
│  │        │     │  ├─ WebLinkConfig.php
│  │        │     │  ├─ Workflows
│  │        │     │  │  ├─ WorkflowsConfig
│  │        │     │  │  │  ├─ AuditTrailConfig.php
│  │        │     │  │  │  ├─ MarkingStoreConfig.php
│  │        │     │  │  │  ├─ PlaceConfig.php
│  │        │     │  │  │  └─ TransitionConfig.php
│  │        │     │  │  └─ WorkflowsConfig.php
│  │        │     │  └─ WorkflowsConfig.php
│  │        │     └─ FrameworkConfig.php
│  │        ├─ url_generating_routes.php
│  │        ├─ url_generating_routes.php.meta
│  │        ├─ url_generating_routes.php.meta.json
│  │        ├─ url_matching_routes.php
│  │        ├─ url_matching_routes.php.meta
│  │        └─ url_matching_routes.php.meta.json
│  └─ vendor
│     ├─ autoload.php
│     ├─ autoload_runtime.php
│     ├─ bin
│     │  ├─ patch-type-declarations
│     │  ├─ patch-type-declarations.bat
│     │  ├─ var-dump-server
│     │  ├─ var-dump-server.bat
│     │  ├─ yaml-lint
│     │  └─ yaml-lint.bat
│     ├─ composer
│     │  ├─ autoload_classmap.php
│     │  ├─ autoload_files.php
│     │  ├─ autoload_namespaces.php
│     │  ├─ autoload_psr4.php
│     │  ├─ autoload_real.php
│     │  ├─ autoload_static.php
│     │  ├─ ClassLoader.php
│     │  ├─ installed.json
│     │  ├─ installed.php
│     │  ├─ InstalledVersions.php
│     │  ├─ LICENSE
│     │  └─ platform_check.php
│     ├─ psr
│     │  ├─ cache
│     │  │  ├─ CHANGELOG.md
│     │  │  ├─ composer.json
│     │  │  ├─ LICENSE.txt
│     │  │  ├─ README.md
│     │  │  └─ src
│     │  │     ├─ CacheException.php
│     │  │     ├─ CacheItemInterface.php
│     │  │     ├─ CacheItemPoolInterface.php
│     │  │     └─ InvalidArgumentException.php
│     │  ├─ container
│     │  │  ├─ composer.json
│     │  │  ├─ LICENSE
│     │  │  ├─ README.md
│     │  │  └─ src
│     │  │     ├─ ContainerExceptionInterface.php
│     │  │     ├─ ContainerInterface.php
│     │  │     └─ NotFoundExceptionInterface.php
│     │  ├─ event-dispatcher
│     │  │  ├─ .editorconfig
│     │  │  ├─ composer.json
│     │  │  ├─ LICENSE
│     │  │  ├─ README.md
│     │  │  └─ src
│     │  │     ├─ EventDispatcherInterface.php
│     │  │     ├─ ListenerProviderInterface.php
│     │  │     └─ StoppableEventInterface.php
│     │  └─ log
│     │     ├─ composer.json
│     │     ├─ LICENSE
│     │     ├─ README.md
│     │     └─ src
│     │        ├─ AbstractLogger.php
│     │        ├─ InvalidArgumentException.php
│     │        ├─ LoggerAwareInterface.php
│     │        ├─ LoggerAwareTrait.php
│     │        ├─ LoggerInterface.php
│     │        ├─ LoggerTrait.php
│     │        ├─ LogLevel.php
│     │        └─ NullLogger.php
│     └─ symfony
│        ├─ cache
│        │  ├─ Adapter
│        │  │  ├─ AbstractAdapter.php
│        │  │  ├─ AbstractTagAwareAdapter.php
│        │  │  ├─ AdapterInterface.php
│        │  │  ├─ ApcuAdapter.php
│        │  │  ├─ ArrayAdapter.php
│        │  │  ├─ ChainAdapter.php
│        │  │  ├─ CouchbaseBucketAdapter.php
│        │  │  ├─ CouchbaseCollectionAdapter.php
│        │  │  ├─ DoctrineDbalAdapter.php
│        │  │  ├─ FilesystemAdapter.php
│        │  │  ├─ FilesystemTagAwareAdapter.php
│        │  │  ├─ MemcachedAdapter.php
│        │  │  ├─ NullAdapter.php
│        │  │  ├─ ParameterNormalizer.php
│        │  │  ├─ PdoAdapter.php
│        │  │  ├─ PhpArrayAdapter.php
│        │  │  ├─ PhpFilesAdapter.php
│        │  │  ├─ ProxyAdapter.php
│        │  │  ├─ Psr16Adapter.php
│        │  │  ├─ RedisAdapter.php
│        │  │  ├─ RedisTagAwareAdapter.php
│        │  │  ├─ TagAwareAdapter.php
│        │  │  ├─ TagAwareAdapterInterface.php
│        │  │  ├─ TraceableAdapter.php
│        │  │  └─ TraceableTagAwareAdapter.php
│        │  ├─ CacheItem.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ DataCollector
│        │  │  └─ CacheDataCollector.php
│        │  ├─ DependencyInjection
│        │  │  ├─ CacheCollectorPass.php
│        │  │  ├─ CachePoolClearerPass.php
│        │  │  ├─ CachePoolPass.php
│        │  │  └─ CachePoolPrunerPass.php
│        │  ├─ Exception
│        │  │  ├─ BadMethodCallException.php
│        │  │  ├─ CacheException.php
│        │  │  ├─ InvalidArgumentException.php
│        │  │  └─ LogicException.php
│        │  ├─ LICENSE
│        │  ├─ LockRegistry.php
│        │  ├─ Marshaller
│        │  │  ├─ DefaultMarshaller.php
│        │  │  ├─ DeflateMarshaller.php
│        │  │  ├─ MarshallerInterface.php
│        │  │  ├─ SodiumMarshaller.php
│        │  │  └─ TagAwareMarshaller.php
│        │  ├─ Messenger
│        │  │  ├─ EarlyExpirationDispatcher.php
│        │  │  ├─ EarlyExpirationHandler.php
│        │  │  └─ EarlyExpirationMessage.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ PruneableInterface.php
│        │  ├─ Psr16Cache.php
│        │  ├─ README.md
│        │  ├─ ResettableInterface.php
│        │  ├─ Tests
│        │  │  ├─ Adapter
│        │  │  │  ├─ AbstractRedisAdapterTestCase.php
│        │  │  │  ├─ AdapterTestCase.php
│        │  │  │  ├─ ApcuAdapterTest.php
│        │  │  │  ├─ ArrayAdapterTest.php
│        │  │  │  ├─ ChainAdapterTest.php
│        │  │  │  ├─ CouchbaseBucketAdapterTest.php
│        │  │  │  ├─ CouchbaseCollectionAdapterTest.php
│        │  │  │  ├─ DoctrineDbalAdapterTest.php
│        │  │  │  ├─ FilesystemAdapterTest.php
│        │  │  │  ├─ FilesystemTagAwareAdapterTest.php
│        │  │  │  ├─ MaxIdLengthAdapterTest.php
│        │  │  │  ├─ MemcachedAdapterTest.php
│        │  │  │  ├─ NamespacedProxyAdapterTest.php
│        │  │  │  ├─ NullAdapterTest.php
│        │  │  │  ├─ PdoAdapterTest.php
│        │  │  │  ├─ PhpArrayAdapterTest.php
│        │  │  │  ├─ PhpArrayAdapterWithFallbackTest.php
│        │  │  │  ├─ PhpFilesAdapterAppendOnlyTest.php
│        │  │  │  ├─ PhpFilesAdapterTest.php
│        │  │  │  ├─ PredisAdapterSentinelTest.php
│        │  │  │  ├─ PredisAdapterTest.php
│        │  │  │  ├─ PredisClusterAdapterTest.php
│        │  │  │  ├─ PredisRedisClusterAdapterTest.php
│        │  │  │  ├─ PredisRedisReplicationAdapterTest.php
│        │  │  │  ├─ PredisReplicationAdapterTest.php
│        │  │  │  ├─ PredisTagAwareAdapterTest.php
│        │  │  │  ├─ PredisTagAwareClusterAdapterTest.php
│        │  │  │  ├─ ProxyAdapterAndRedisAdapterTest.php
│        │  │  │  ├─ ProxyAdapterTest.php
│        │  │  │  ├─ Psr16AdapterTest.php
│        │  │  │  ├─ RedisAdapterSentinelTest.php
│        │  │  │  ├─ RedisAdapterTest.php
│        │  │  │  ├─ RedisArrayAdapterTest.php
│        │  │  │  ├─ RedisClusterAdapterTest.php
│        │  │  │  ├─ RedisTagAwareAdapterTest.php
│        │  │  │  ├─ RedisTagAwareArrayAdapterTest.php
│        │  │  │  ├─ RedisTagAwareClusterAdapterTest.php
│        │  │  │  ├─ RedisTagAwareRelayClusterAdapterTest.php
│        │  │  │  ├─ RelayAdapterSentinelTest.php
│        │  │  │  ├─ RelayAdapterTest.php
│        │  │  │  ├─ RelayClusterAdapterTest.php
│        │  │  │  ├─ TagAwareAdapterTest.php
│        │  │  │  ├─ TagAwareAndProxyAdapterIntegrationTest.php
│        │  │  │  ├─ TagAwareTestTrait.php
│        │  │  │  ├─ TraceableAdapterTest.php
│        │  │  │  └─ TraceableTagAwareAdapterTest.php
│        │  │  ├─ CacheItemTest.php
│        │  │  ├─ DataCollector
│        │  │  │  └─ CacheDataCollectorTest.php
│        │  │  ├─ DependencyInjection
│        │  │  │  ├─ CacheCollectorPassTest.php
│        │  │  │  ├─ CachePoolClearerPassTest.php
│        │  │  │  ├─ CachePoolPassTest.php
│        │  │  │  └─ CachePoolPrunerPassTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ ExternalAdapter.php
│        │  │  │  ├─ PrunableAdapter.php
│        │  │  │  ├─ StringableTag.php
│        │  │  │  └─ TestEnum.php
│        │  │  ├─ LockRegistryTest.php
│        │  │  ├─ Marshaller
│        │  │  │  ├─ DefaultMarshallerTest.php
│        │  │  │  ├─ DeflateMarshallerTest.php
│        │  │  │  └─ SodiumMarshallerTest.php
│        │  │  ├─ Messenger
│        │  │  │  ├─ EarlyExpirationDispatcherTest.php
│        │  │  │  ├─ EarlyExpirationHandlerTest.php
│        │  │  │  └─ EarlyExpirationMessageTest.php
│        │  │  ├─ Psr16CacheProxyTest.php
│        │  │  ├─ Psr16CacheTest.php
│        │  │  ├─ Psr16CacheWithExternalAdapter.php
│        │  │  └─ Traits
│        │  │     ├─ RedisProxiesTest.php
│        │  │     └─ RedisTraitTest.php
│        │  └─ Traits
│        │     ├─ AbstractAdapterTrait.php
│        │     ├─ ContractsTrait.php
│        │     ├─ FilesystemCommonTrait.php
│        │     ├─ FilesystemTrait.php
│        │     ├─ ProxyTrait.php
│        │     ├─ Redis5Proxy.php
│        │     ├─ Redis6Proxy.php
│        │     ├─ Redis6ProxyTrait.php
│        │     ├─ RedisCluster5Proxy.php
│        │     ├─ RedisCluster6Proxy.php
│        │     ├─ RedisCluster6ProxyTrait.php
│        │     ├─ RedisClusterNodeProxy.php
│        │     ├─ RedisClusterProxy.php
│        │     ├─ RedisProxy.php
│        │     ├─ RedisProxyTrait.php
│        │     ├─ RedisTrait.php
│        │     ├─ Relay
│        │     │  ├─ CopyTrait.php
│        │     │  ├─ GeosearchTrait.php
│        │     │  ├─ GetrangeTrait.php
│        │     │  ├─ HsetTrait.php
│        │     │  ├─ MoveTrait.php
│        │     │  ├─ NullableReturnTrait.php
│        │     │  └─ PfcountTrait.php
│        │     ├─ RelayClusterProxy.php
│        │     ├─ RelayProxy.php
│        │     ├─ RelayProxyTrait.php
│        │     └─ ValueWrapper.php
│        ├─ cache-contracts
│        │  ├─ CacheInterface.php
│        │  ├─ CacheTrait.php
│        │  ├─ CallbackInterface.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ ItemInterface.php
│        │  ├─ LICENSE
│        │  ├─ NamespacedPoolInterface.php
│        │  ├─ README.md
│        │  └─ TagAwareCacheInterface.php
│        ├─ config
│        │  ├─ Builder
│        │  │  ├─ ClassBuilder.php
│        │  │  ├─ ConfigBuilderGenerator.php
│        │  │  ├─ ConfigBuilderGeneratorInterface.php
│        │  │  ├─ ConfigBuilderInterface.php
│        │  │  ├─ Method.php
│        │  │  └─ Property.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ ConfigCache.php
│        │  ├─ ConfigCacheFactory.php
│        │  ├─ ConfigCacheFactoryInterface.php
│        │  ├─ ConfigCacheInterface.php
│        │  ├─ Definition
│        │  │  ├─ ArrayNode.php
│        │  │  ├─ BaseNode.php
│        │  │  ├─ BooleanNode.php
│        │  │  ├─ Builder
│        │  │  │  ├─ ArrayNodeDefinition.php
│        │  │  │  ├─ BooleanNodeDefinition.php
│        │  │  │  ├─ BuilderAwareInterface.php
│        │  │  │  ├─ EnumNodeDefinition.php
│        │  │  │  ├─ ExprBuilder.php
│        │  │  │  ├─ FloatNodeDefinition.php
│        │  │  │  ├─ IntegerNodeDefinition.php
│        │  │  │  ├─ MergeBuilder.php
│        │  │  │  ├─ NodeBuilder.php
│        │  │  │  ├─ NodeDefinition.php
│        │  │  │  ├─ NodeParentInterface.php
│        │  │  │  ├─ NormalizationBuilder.php
│        │  │  │  ├─ NumericNodeDefinition.php
│        │  │  │  ├─ ParentNodeDefinitionInterface.php
│        │  │  │  ├─ ScalarNodeDefinition.php
│        │  │  │  ├─ StringNodeDefinition.php
│        │  │  │  ├─ TreeBuilder.php
│        │  │  │  ├─ ValidationBuilder.php
│        │  │  │  └─ VariableNodeDefinition.php
│        │  │  ├─ ConfigurableInterface.php
│        │  │  ├─ Configuration.php
│        │  │  ├─ ConfigurationInterface.php
│        │  │  ├─ Configurator
│        │  │  │  └─ DefinitionConfigurator.php
│        │  │  ├─ Dumper
│        │  │  │  ├─ XmlReferenceDumper.php
│        │  │  │  └─ YamlReferenceDumper.php
│        │  │  ├─ EnumNode.php
│        │  │  ├─ Exception
│        │  │  │  ├─ DuplicateKeyException.php
│        │  │  │  ├─ Exception.php
│        │  │  │  ├─ ForbiddenOverwriteException.php
│        │  │  │  ├─ InvalidConfigurationException.php
│        │  │  │  ├─ InvalidDefinitionException.php
│        │  │  │  ├─ InvalidTypeException.php
│        │  │  │  └─ UnsetKeyException.php
│        │  │  ├─ FloatNode.php
│        │  │  ├─ IntegerNode.php
│        │  │  ├─ Loader
│        │  │  │  └─ DefinitionFileLoader.php
│        │  │  ├─ NodeInterface.php
│        │  │  ├─ NumericNode.php
│        │  │  ├─ Processor.php
│        │  │  ├─ PrototypedArrayNode.php
│        │  │  ├─ PrototypeNodeInterface.php
│        │  │  ├─ ScalarNode.php
│        │  │  ├─ StringNode.php
│        │  │  └─ VariableNode.php
│        │  ├─ Exception
│        │  │  ├─ FileLoaderImportCircularReferenceException.php
│        │  │  ├─ FileLocatorFileNotFoundException.php
│        │  │  ├─ LoaderLoadException.php
│        │  │  └─ LogicException.php
│        │  ├─ FileLocator.php
│        │  ├─ FileLocatorInterface.php
│        │  ├─ LICENSE
│        │  ├─ Loader
│        │  │  ├─ DelegatingLoader.php
│        │  │  ├─ DirectoryAwareLoaderInterface.php
│        │  │  ├─ FileLoader.php
│        │  │  ├─ GlobFileLoader.php
│        │  │  ├─ Loader.php
│        │  │  ├─ LoaderInterface.php
│        │  │  ├─ LoaderResolver.php
│        │  │  ├─ LoaderResolverInterface.php
│        │  │  └─ ParamConfigurator.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Resource
│        │  │  ├─ ClassExistenceResource.php
│        │  │  ├─ ComposerResource.php
│        │  │  ├─ DirectoryResource.php
│        │  │  ├─ FileExistenceResource.php
│        │  │  ├─ FileResource.php
│        │  │  ├─ GlobResource.php
│        │  │  ├─ ReflectionClassResource.php
│        │  │  ├─ ResourceInterface.php
│        │  │  ├─ SelfCheckingResourceChecker.php
│        │  │  ├─ SelfCheckingResourceInterface.php
│        │  │  └─ SkippingResourceChecker.php
│        │  ├─ ResourceCheckerConfigCache.php
│        │  ├─ ResourceCheckerConfigCacheFactory.php
│        │  ├─ ResourceCheckerInterface.php
│        │  ├─ Tests
│        │  │  ├─ Builder
│        │  │  │  ├─ Fixtures
│        │  │  │  │  ├─ AddToList
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        ├─ AddToList
│        │  │  │  │  │        │  ├─ Messenger
│        │  │  │  │  │        │  │  ├─ ReceivingConfig.php
│        │  │  │  │  │        │  │  └─ RoutingConfig.php
│        │  │  │  │  │        │  ├─ MessengerConfig.php
│        │  │  │  │  │        │  ├─ Translator
│        │  │  │  │  │        │  │  ├─ Books
│        │  │  │  │  │        │  │  │  └─ PageConfig.php
│        │  │  │  │  │        │  │  └─ BooksConfig.php
│        │  │  │  │  │        │  └─ TranslatorConfig.php
│        │  │  │  │  │        └─ AddToListConfig.php
│        │  │  │  │  ├─ AddToList.config.php
│        │  │  │  │  ├─ AddToList.output.php
│        │  │  │  │  ├─ AddToList.php
│        │  │  │  │  ├─ ArrayExtraKeys
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        ├─ ArrayExtraKeys
│        │  │  │  │  │        │  ├─ BarConfig.php
│        │  │  │  │  │        │  ├─ BazConfig.php
│        │  │  │  │  │        │  └─ FooConfig.php
│        │  │  │  │  │        └─ ArrayExtraKeysConfig.php
│        │  │  │  │  ├─ ArrayExtraKeys.config.php
│        │  │  │  │  ├─ ArrayExtraKeys.output.php
│        │  │  │  │  ├─ ArrayExtraKeys.php
│        │  │  │  │  ├─ NodeInitialValues
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        ├─ NodeInitialValues
│        │  │  │  │  │        │  ├─ Messenger
│        │  │  │  │  │        │  │  └─ TransportsConfig.php
│        │  │  │  │  │        │  ├─ MessengerConfig.php
│        │  │  │  │  │        │  └─ SomeCleverNameConfig.php
│        │  │  │  │  │        └─ NodeInitialValuesConfig.php
│        │  │  │  │  ├─ NodeInitialValues.config.php
│        │  │  │  │  ├─ NodeInitialValues.output.php
│        │  │  │  │  ├─ NodeInitialValues.php
│        │  │  │  │  ├─ Placeholders
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        └─ PlaceholdersConfig.php
│        │  │  │  │  ├─ Placeholders.config.php
│        │  │  │  │  ├─ Placeholders.output.php
│        │  │  │  │  ├─ Placeholders.php
│        │  │  │  │  ├─ PrimitiveTypes
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        └─ PrimitiveTypesConfig.php
│        │  │  │  │  ├─ PrimitiveTypes.config.php
│        │  │  │  │  ├─ PrimitiveTypes.output.php
│        │  │  │  │  ├─ PrimitiveTypes.php
│        │  │  │  │  ├─ ScalarNormalizedTypes
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        ├─ ScalarNormalizedTypes
│        │  │  │  │  │        │  ├─ KeyedListObjectConfig.php
│        │  │  │  │  │        │  ├─ ListObjectConfig.php
│        │  │  │  │  │        │  ├─ Nested
│        │  │  │  │  │        │  │  ├─ NestedListObjectConfig.php
│        │  │  │  │  │        │  │  └─ NestedObjectConfig.php
│        │  │  │  │  │        │  ├─ NestedConfig.php
│        │  │  │  │  │        │  └─ ObjectConfig.php
│        │  │  │  │  │        └─ ScalarNormalizedTypesConfig.php
│        │  │  │  │  ├─ ScalarNormalizedTypes.config.php
│        │  │  │  │  ├─ ScalarNormalizedTypes.output.php
│        │  │  │  │  ├─ ScalarNormalizedTypes.php
│        │  │  │  │  ├─ VariableType
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        └─ VariableTypeConfig.php
│        │  │  │  │  ├─ VariableType.config.php
│        │  │  │  │  ├─ VariableType.output.php
│        │  │  │  │  └─ VariableType.php
│        │  │  │  └─ GeneratedConfigTest.php
│        │  │  ├─ ConfigCacheFactoryTest.php
│        │  │  ├─ ConfigCacheTest.php
│        │  │  ├─ Definition
│        │  │  │  ├─ ArrayNodeTest.php
│        │  │  │  ├─ BaseNodeTest.php
│        │  │  │  ├─ BooleanNodeTest.php
│        │  │  │  ├─ Builder
│        │  │  │  │  ├─ ArrayNodeDefinitionTest.php
│        │  │  │  │  ├─ BooleanNodeDefinitionTest.php
│        │  │  │  │  ├─ EnumNodeDefinitionTest.php
│        │  │  │  │  ├─ ExprBuilderTest.php
│        │  │  │  │  ├─ NodeBuilderTest.php
│        │  │  │  │  ├─ NodeDefinitionTest.php
│        │  │  │  │  ├─ NumericNodeDefinitionTest.php
│        │  │  │  │  └─ TreeBuilderTest.php
│        │  │  │  ├─ Dumper
│        │  │  │  │  ├─ XmlReferenceDumperTest.php
│        │  │  │  │  └─ YamlReferenceDumperTest.php
│        │  │  │  ├─ EnumNodeTest.php
│        │  │  │  ├─ FinalizationTest.php
│        │  │  │  ├─ FloatNodeTest.php
│        │  │  │  ├─ IntegerNodeTest.php
│        │  │  │  ├─ Loader
│        │  │  │  │  └─ DefinitionFileLoaderTest.php
│        │  │  │  ├─ MergeTest.php
│        │  │  │  ├─ NormalizationTest.php
│        │  │  │  ├─ PrototypedArrayNodeTest.php
│        │  │  │  ├─ ScalarNodeTest.php
│        │  │  │  └─ StringNodeTest.php
│        │  │  ├─ Exception
│        │  │  │  └─ LoaderLoadExceptionTest.php
│        │  │  ├─ FileLocatorTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ Again
│        │  │  │  │  └─ foo.xml
│        │  │  │  ├─ BadFileName.php
│        │  │  │  ├─ BadParent.php
│        │  │  │  ├─ BarNode.php
│        │  │  │  ├─ Builder
│        │  │  │  │  ├─ BarNodeDefinition.php
│        │  │  │  │  ├─ NodeBuilder.php
│        │  │  │  │  └─ VariableNodeDefinition.php
│        │  │  │  ├─ Configuration
│        │  │  │  │  ├─ CustomNode.php
│        │  │  │  │  ├─ CustomNodeDefinition.php
│        │  │  │  │  └─ ExampleConfiguration.php
│        │  │  │  ├─ Exclude
│        │  │  │  │  ├─ AnExcludedFile.txt
│        │  │  │  │  └─ ExcludeToo
│        │  │  │  │     └─ AnotheExcludedFile.txt
│        │  │  │  ├─ ExcludeTrailingSlash
│        │  │  │  │  ├─ bar.txt
│        │  │  │  │  ├─ exclude
│        │  │  │  │  │  └─ baz.txt
│        │  │  │  │  └─ foo.txt
│        │  │  │  ├─ foo.xml
│        │  │  │  ├─ Include
│        │  │  │  │  ├─ ExcludeFile.txt
│        │  │  │  │  ├─ IncludeAnotherFile.txt
│        │  │  │  │  └─ IncludeFile.txt
│        │  │  │  ├─ IntegerBackedTestEnum.php
│        │  │  │  ├─ Loader
│        │  │  │  │  └─ node_simple.php
│        │  │  │  ├─ ParseError.php
│        │  │  │  ├─ Resource
│        │  │  │  │  ├─ .hiddenFile
│        │  │  │  │  └─ ConditionalClass.php
│        │  │  │  ├─ some.phar
│        │  │  │  ├─ StringBackedTestEnum.php
│        │  │  │  ├─ StringBackedTestEnum2.php
│        │  │  │  ├─ TestEnum.php
│        │  │  │  ├─ TestEnum2.php
│        │  │  │  └─ Util
│        │  │  │     ├─ document_type.xml
│        │  │  │     ├─ invalid.xml
│        │  │  │     ├─ invalid_schema.xml
│        │  │  │     ├─ not_readable.xml
│        │  │  │     ├─ schema.xsd
│        │  │  │     └─ valid.xml
│        │  │  ├─ Loader
│        │  │  │  ├─ DelegatingLoaderTest.php
│        │  │  │  ├─ FileLoaderTest.php
│        │  │  │  ├─ LoaderResolverTest.php
│        │  │  │  └─ LoaderTest.php
│        │  │  ├─ Resource
│        │  │  │  ├─ ClassExistenceResourceTest.php
│        │  │  │  ├─ ComposerResourceTest.php
│        │  │  │  ├─ DirectoryResourceTest.php
│        │  │  │  ├─ FileExistenceResourceTest.php
│        │  │  │  ├─ FileResourceTest.php
│        │  │  │  ├─ GlobResourceTest.php
│        │  │  │  ├─ ReflectionClassResourceTest.php
│        │  │  │  └─ ResourceStub.php
│        │  │  ├─ ResourceCheckerConfigCacheTest.php
│        │  │  └─ Util
│        │  │     └─ XmlUtilsTest.php
│        │  └─ Util
│        │     ├─ Exception
│        │     │  ├─ InvalidXmlException.php
│        │     │  └─ XmlParsingException.php
│        │     └─ XmlUtils.php
│        ├─ console
│        │  ├─ Application.php
│        │  ├─ Attribute
│        │  │  ├─ Argument.php
│        │  │  ├─ AsCommand.php
│        │  │  └─ Option.php
│        │  ├─ CHANGELOG.md
│        │  ├─ CI
│        │  │  └─ GithubActionReporter.php
│        │  ├─ Color.php
│        │  ├─ Command
│        │  │  ├─ Command.php
│        │  │  ├─ CompleteCommand.php
│        │  │  ├─ DumpCompletionCommand.php
│        │  │  ├─ HelpCommand.php
│        │  │  ├─ InvokableCommand.php
│        │  │  ├─ LazyCommand.php
│        │  │  ├─ ListCommand.php
│        │  │  ├─ LockableTrait.php
│        │  │  ├─ SignalableCommandInterface.php
│        │  │  └─ TraceableCommand.php
│        │  ├─ CommandLoader
│        │  │  ├─ CommandLoaderInterface.php
│        │  │  ├─ ContainerCommandLoader.php
│        │  │  └─ FactoryCommandLoader.php
│        │  ├─ Completion
│        │  │  ├─ CompletionInput.php
│        │  │  ├─ CompletionSuggestions.php
│        │  │  ├─ Output
│        │  │  │  ├─ BashCompletionOutput.php
│        │  │  │  ├─ CompletionOutputInterface.php
│        │  │  │  ├─ FishCompletionOutput.php
│        │  │  │  └─ ZshCompletionOutput.php
│        │  │  └─ Suggestion.php
│        │  ├─ composer.json
│        │  ├─ ConsoleEvents.php
│        │  ├─ Cursor.php
│        │  ├─ DataCollector
│        │  │  └─ CommandDataCollector.php
│        │  ├─ Debug
│        │  │  └─ CliRequest.php
│        │  ├─ DependencyInjection
│        │  │  └─ AddConsoleCommandPass.php
│        │  ├─ Descriptor
│        │  │  ├─ ApplicationDescription.php
│        │  │  ├─ Descriptor.php
│        │  │  ├─ DescriptorInterface.php
│        │  │  ├─ JsonDescriptor.php
│        │  │  ├─ MarkdownDescriptor.php
│        │  │  ├─ ReStructuredTextDescriptor.php
│        │  │  ├─ TextDescriptor.php
│        │  │  └─ XmlDescriptor.php
│        │  ├─ Event
│        │  │  ├─ ConsoleAlarmEvent.php
│        │  │  ├─ ConsoleCommandEvent.php
│        │  │  ├─ ConsoleErrorEvent.php
│        │  │  ├─ ConsoleEvent.php
│        │  │  ├─ ConsoleSignalEvent.php
│        │  │  └─ ConsoleTerminateEvent.php
│        │  ├─ EventListener
│        │  │  └─ ErrorListener.php
│        │  ├─ Exception
│        │  │  ├─ CommandNotFoundException.php
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ InvalidArgumentException.php
│        │  │  ├─ InvalidOptionException.php
│        │  │  ├─ LogicException.php
│        │  │  ├─ MissingInputException.php
│        │  │  ├─ NamespaceNotFoundException.php
│        │  │  ├─ RunCommandFailedException.php
│        │  │  └─ RuntimeException.php
│        │  ├─ Formatter
│        │  │  ├─ NullOutputFormatter.php
│        │  │  ├─ NullOutputFormatterStyle.php
│        │  │  ├─ OutputFormatter.php
│        │  │  ├─ OutputFormatterInterface.php
│        │  │  ├─ OutputFormatterStyle.php
│        │  │  ├─ OutputFormatterStyleInterface.php
│        │  │  ├─ OutputFormatterStyleStack.php
│        │  │  └─ WrappableOutputFormatterInterface.php
│        │  ├─ Helper
│        │  │  ├─ DebugFormatterHelper.php
│        │  │  ├─ DescriptorHelper.php
│        │  │  ├─ Dumper.php
│        │  │  ├─ FormatterHelper.php
│        │  │  ├─ Helper.php
│        │  │  ├─ HelperInterface.php
│        │  │  ├─ HelperSet.php
│        │  │  ├─ InputAwareHelper.php
│        │  │  ├─ OutputWrapper.php
│        │  │  ├─ ProcessHelper.php
│        │  │  ├─ ProgressBar.php
│        │  │  ├─ ProgressIndicator.php
│        │  │  ├─ QuestionHelper.php
│        │  │  ├─ SymfonyQuestionHelper.php
│        │  │  ├─ Table.php
│        │  │  ├─ TableCell.php
│        │  │  ├─ TableCellStyle.php
│        │  │  ├─ TableRows.php
│        │  │  ├─ TableSeparator.php
│        │  │  ├─ TableStyle.php
│        │  │  ├─ TreeHelper.php
│        │  │  ├─ TreeNode.php
│        │  │  └─ TreeStyle.php
│        │  ├─ Input
│        │  │  ├─ ArgvInput.php
│        │  │  ├─ ArrayInput.php
│        │  │  ├─ Input.php
│        │  │  ├─ InputArgument.php
│        │  │  ├─ InputAwareInterface.php
│        │  │  ├─ InputDefinition.php
│        │  │  ├─ InputInterface.php
│        │  │  ├─ InputOption.php
│        │  │  ├─ StreamableInputInterface.php
│        │  │  └─ StringInput.php
│        │  ├─ LICENSE
│        │  ├─ Logger
│        │  │  └─ ConsoleLogger.php
│        │  ├─ Messenger
│        │  │  ├─ RunCommandContext.php
│        │  │  ├─ RunCommandMessage.php
│        │  │  └─ RunCommandMessageHandler.php
│        │  ├─ Output
│        │  │  ├─ AnsiColorMode.php
│        │  │  ├─ BufferedOutput.php
│        │  │  ├─ ConsoleOutput.php
│        │  │  ├─ ConsoleOutputInterface.php
│        │  │  ├─ ConsoleSectionOutput.php
│        │  │  ├─ NullOutput.php
│        │  │  ├─ Output.php
│        │  │  ├─ OutputInterface.php
│        │  │  ├─ StreamOutput.php
│        │  │  └─ TrimmedBufferOutput.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ Question
│        │  │  ├─ ChoiceQuestion.php
│        │  │  ├─ ConfirmationQuestion.php
│        │  │  └─ Question.php
│        │  ├─ README.md
│        │  ├─ Resources
│        │  │  ├─ bin
│        │  │  │  └─ hiddeninput.exe
│        │  │  ├─ completion.bash
│        │  │  ├─ completion.fish
│        │  │  └─ completion.zsh
│        │  ├─ SignalRegistry
│        │  │  ├─ SignalMap.php
│        │  │  └─ SignalRegistry.php
│        │  ├─ SingleCommandApplication.php
│        │  ├─ Style
│        │  │  ├─ OutputStyle.php
│        │  │  ├─ StyleInterface.php
│        │  │  └─ SymfonyStyle.php
│        │  ├─ Terminal.php
│        │  ├─ Tester
│        │  │  ├─ ApplicationTester.php
│        │  │  ├─ CommandCompletionTester.php
│        │  │  ├─ CommandTester.php
│        │  │  ├─ Constraint
│        │  │  │  └─ CommandIsSuccessful.php
│        │  │  └─ TesterTrait.php
│        │  └─ Tests
│        │     ├─ ApplicationTest.php
│        │     ├─ CI
│        │     │  └─ GithubActionReporterTest.php
│        │     ├─ ColorTest.php
│        │     ├─ Command
│        │     │  ├─ CommandTest.php
│        │     │  ├─ CompleteCommandTest.php
│        │     │  ├─ DumpCompletionCommandTest.php
│        │     │  ├─ HelpCommandTest.php
│        │     │  ├─ InvokableCommandTest.php
│        │     │  ├─ ListCommandTest.php
│        │     │  ├─ LockableTraitTest.php
│        │     │  └─ SingleCommandApplicationTest.php
│        │     ├─ CommandLoader
│        │     │  ├─ ContainerCommandLoaderTest.php
│        │     │  └─ FactoryCommandLoaderTest.php
│        │     ├─ Completion
│        │     │  ├─ CompletionInputTest.php
│        │     │  └─ Output
│        │     │     ├─ BashCompletionOutputTest.php
│        │     │     ├─ CompletionOutputTestCase.php
│        │     │     ├─ FishCompletionOutputTest.php
│        │     │     └─ ZshCompletionOutputTest.php
│        │     ├─ ConsoleEventsTest.php
│        │     ├─ CursorTest.php
│        │     ├─ DependencyInjection
│        │     │  └─ AddConsoleCommandPassTest.php
│        │     ├─ Descriptor
│        │     │  ├─ AbstractDescriptorTestCase.php
│        │     │  ├─ ApplicationDescriptionTest.php
│        │     │  ├─ JsonDescriptorTest.php
│        │     │  ├─ MarkdownDescriptorTest.php
│        │     │  ├─ ObjectsProvider.php
│        │     │  ├─ ReStructuredTextDescriptorTest.php
│        │     │  ├─ TextDescriptorTest.php
│        │     │  └─ XmlDescriptorTest.php
│        │     ├─ EventListener
│        │     │  └─ ErrorListenerTest.php
│        │     ├─ Fixtures
│        │     │  ├─ application.dont_run_alternative_namespace_name.txt
│        │     │  ├─ application_1.json
│        │     │  ├─ application_1.md
│        │     │  ├─ application_1.rst
│        │     │  ├─ application_1.txt
│        │     │  ├─ application_1.xml
│        │     │  ├─ application_2.json
│        │     │  ├─ application_2.md
│        │     │  ├─ application_2.rst
│        │     │  ├─ application_2.txt
│        │     │  ├─ application_2.xml
│        │     │  ├─ application_filtered_namespace.txt
│        │     │  ├─ application_gethelp.txt
│        │     │  ├─ application_mbstring.md
│        │     │  ├─ application_mbstring.rst
│        │     │  ├─ application_mbstring.txt
│        │     │  ├─ application_renderexception1.txt
│        │     │  ├─ application_renderexception2.txt
│        │     │  ├─ application_renderexception3.txt
│        │     │  ├─ application_renderexception3decorated.txt
│        │     │  ├─ application_renderexception4.txt
│        │     │  ├─ application_renderexception_doublewidth1.txt
│        │     │  ├─ application_renderexception_doublewidth1decorated.txt
│        │     │  ├─ application_renderexception_doublewidth2.txt
│        │     │  ├─ application_renderexception_escapeslines.txt
│        │     │  ├─ application_renderexception_linebreaks.txt
│        │     │  ├─ application_rendersynopsis_escapesline.txt
│        │     │  ├─ application_run1.txt
│        │     │  ├─ application_run2.txt
│        │     │  ├─ application_run3.txt
│        │     │  ├─ application_run4.txt
│        │     │  ├─ application_run5.txt
│        │     │  ├─ application_signalable.php
│        │     │  ├─ BarBucCommand.php
│        │     │  ├─ BarHiddenCommand.php
│        │     │  ├─ command_1.json
│        │     │  ├─ command_1.md
│        │     │  ├─ command_1.rst
│        │     │  ├─ command_1.txt
│        │     │  ├─ command_1.xml
│        │     │  ├─ command_2.json
│        │     │  ├─ command_2.md
│        │     │  ├─ command_2.rst
│        │     │  ├─ command_2.txt
│        │     │  ├─ command_2.xml
│        │     │  ├─ command_mbstring.md
│        │     │  ├─ command_mbstring.rst
│        │     │  ├─ command_mbstring.txt
│        │     │  ├─ DescriptorApplication1.php
│        │     │  ├─ DescriptorApplication2.php
│        │     │  ├─ DescriptorApplicationMbString.php
│        │     │  ├─ DescriptorCommand1.php
│        │     │  ├─ DescriptorCommand2.php
│        │     │  ├─ DescriptorCommand3.php
│        │     │  ├─ DescriptorCommand4.php
│        │     │  ├─ DescriptorCommandMbString.php
│        │     │  ├─ DummyOutput.php
│        │     │  ├─ Foo1Command.php
│        │     │  ├─ Foo2Command.php
│        │     │  ├─ Foo3Command.php
│        │     │  ├─ Foo4Command.php
│        │     │  ├─ Foo5Command.php
│        │     │  ├─ Foo6Command.php
│        │     │  ├─ FoobarCommand.php
│        │     │  ├─ FooCommand.php
│        │     │  ├─ FooHiddenCommand.php
│        │     │  ├─ FooLock2Command.php
│        │     │  ├─ FooLock3Command.php
│        │     │  ├─ FooLock4InvokableCommand.php
│        │     │  ├─ FooLockCommand.php
│        │     │  ├─ FooOptCommand.php
│        │     │  ├─ FooSameCaseLowercaseCommand.php
│        │     │  ├─ FooSameCaseUppercaseCommand.php
│        │     │  ├─ FooSubnamespaced1Command.php
│        │     │  ├─ FooSubnamespaced2Command.php
│        │     │  ├─ FooWithoutAliasCommand.php
│        │     │  ├─ input_argument_1.json
│        │     │  ├─ input_argument_1.md
│        │     │  ├─ input_argument_1.rst
│        │     │  ├─ input_argument_1.txt
│        │     │  ├─ input_argument_1.xml
│        │     │  ├─ input_argument_2.json
│        │     │  ├─ input_argument_2.md
│        │     │  ├─ input_argument_2.rst
│        │     │  ├─ input_argument_2.txt
│        │     │  ├─ input_argument_2.xml
│        │     │  ├─ input_argument_3.json
│        │     │  ├─ input_argument_3.md
│        │     │  ├─ input_argument_3.rst
│        │     │  ├─ input_argument_3.txt
│        │     │  ├─ input_argument_3.xml
│        │     │  ├─ input_argument_4.json
│        │     │  ├─ input_argument_4.md
│        │     │  ├─ input_argument_4.rst
│        │     │  ├─ input_argument_4.txt
│        │     │  ├─ input_argument_4.xml
│        │     │  ├─ input_argument_with_default_inf_value.json
│        │     │  ├─ input_argument_with_default_inf_value.md
│        │     │  ├─ input_argument_with_default_inf_value.rst
│        │     │  ├─ input_argument_with_default_inf_value.txt
│        │     │  ├─ input_argument_with_default_inf_value.xml
│        │     │  ├─ input_argument_with_style.json
│        │     │  ├─ input_argument_with_style.md
│        │     │  ├─ input_argument_with_style.rst
│        │     │  ├─ input_argument_with_style.txt
│        │     │  ├─ input_argument_with_style.xml
│        │     │  ├─ input_definition_1.json
│        │     │  ├─ input_definition_1.md
│        │     │  ├─ input_definition_1.rst
│        │     │  ├─ input_definition_1.txt
│        │     │  ├─ input_definition_1.xml
│        │     │  ├─ input_definition_2.json
│        │     │  ├─ input_definition_2.md
│        │     │  ├─ input_definition_2.rst
│        │     │  ├─ input_definition_2.txt
│        │     │  ├─ input_definition_2.xml
│        │     │  ├─ input_definition_3.json
│        │     │  ├─ input_definition_3.md
│        │     │  ├─ input_definition_3.rst
│        │     │  ├─ input_definition_3.txt
│        │     │  ├─ input_definition_3.xml
│        │     │  ├─ input_definition_4.json
│        │     │  ├─ input_definition_4.md
│        │     │  ├─ input_definition_4.rst
│        │     │  ├─ input_definition_4.txt
│        │     │  ├─ input_definition_4.xml
│        │     │  ├─ input_option_1.json
│        │     │  ├─ input_option_1.md
│        │     │  ├─ input_option_1.rst
│        │     │  ├─ input_option_1.txt
│        │     │  ├─ input_option_1.xml
│        │     │  ├─ input_option_2.json
│        │     │  ├─ input_option_2.md
│        │     │  ├─ input_option_2.rst
│        │     │  ├─ input_option_2.txt
│        │     │  ├─ input_option_2.xml
│        │     │  ├─ input_option_3.json
│        │     │  ├─ input_option_3.md
│        │     │  ├─ input_option_3.rst
│        │     │  ├─ input_option_3.txt
│        │     │  ├─ input_option_3.xml
│        │     │  ├─ input_option_4.json
│        │     │  ├─ input_option_4.md
│        │     │  ├─ input_option_4.rst
│        │     │  ├─ input_option_4.txt
│        │     │  ├─ input_option_4.xml
│        │     │  ├─ input_option_5.json
│        │     │  ├─ input_option_5.md
│        │     │  ├─ input_option_5.rst
│        │     │  ├─ input_option_5.txt
│        │     │  ├─ input_option_5.xml
│        │     │  ├─ input_option_6.json
│        │     │  ├─ input_option_6.md
│        │     │  ├─ input_option_6.rst
│        │     │  ├─ input_option_6.txt
│        │     │  ├─ input_option_6.xml
│        │     │  ├─ input_option_with_default_inf_value.json
│        │     │  ├─ input_option_with_default_inf_value.md
│        │     │  ├─ input_option_with_default_inf_value.rst
│        │     │  ├─ input_option_with_default_inf_value.txt
│        │     │  ├─ input_option_with_default_inf_value.xml
│        │     │  ├─ input_option_with_style.json
│        │     │  ├─ input_option_with_style.md
│        │     │  ├─ input_option_with_style.rst
│        │     │  ├─ input_option_with_style.txt
│        │     │  ├─ input_option_with_style.xml
│        │     │  ├─ input_option_with_style_array.json
│        │     │  ├─ input_option_with_style_array.md
│        │     │  ├─ input_option_with_style_array.rst
│        │     │  ├─ input_option_with_style_array.txt
│        │     │  ├─ input_option_with_style_array.xml
│        │     │  ├─ MockableAppliationWithTerminalWidth.php
│        │     │  ├─ stream_output_file.txt
│        │     │  ├─ Style
│        │     │  │  └─ SymfonyStyle
│        │     │  │     ├─ command
│        │     │  │     │  ├─ command_0.php
│        │     │  │     │  ├─ command_1.php
│        │     │  │     │  ├─ command_10.php
│        │     │  │     │  ├─ command_11.php
│        │     │  │     │  ├─ command_12.php
│        │     │  │     │  ├─ command_13.php
│        │     │  │     │  ├─ command_14.php
│        │     │  │     │  ├─ command_15.php
│        │     │  │     │  ├─ command_16.php
│        │     │  │     │  ├─ command_17.php
│        │     │  │     │  ├─ command_18.php
│        │     │  │     │  ├─ command_19.php
│        │     │  │     │  ├─ command_2.php
│        │     │  │     │  ├─ command_20.php
│        │     │  │     │  ├─ command_21.php
│        │     │  │     │  ├─ command_22.php
│        │     │  │     │  ├─ command_23.php
│        │     │  │     │  ├─ command_3.php
│        │     │  │     │  ├─ command_4.php
│        │     │  │     │  ├─ command_4_with_iterators.php
│        │     │  │     │  ├─ command_5.php
│        │     │  │     │  ├─ command_6.php
│        │     │  │     │  ├─ command_7.php
│        │     │  │     │  ├─ command_8.php
│        │     │  │     │  ├─ command_9.php
│        │     │  │     │  └─ interactive_command_1.php
│        │     │  │     ├─ output
│        │     │  │     │  ├─ interactive_output_1.txt
│        │     │  │     │  ├─ output_0.txt
│        │     │  │     │  ├─ output_1.txt
│        │     │  │     │  ├─ output_10.txt
│        │     │  │     │  ├─ output_11.txt
│        │     │  │     │  ├─ output_12.txt
│        │     │  │     │  ├─ output_13.txt
│        │     │  │     │  ├─ output_14.txt
│        │     │  │     │  ├─ output_15.txt
│        │     │  │     │  ├─ output_16.txt
│        │     │  │     │  ├─ output_17.txt
│        │     │  │     │  ├─ output_18.txt
│        │     │  │     │  ├─ output_19.txt
│        │     │  │     │  ├─ output_2.txt
│        │     │  │     │  ├─ output_20.txt
│        │     │  │     │  ├─ output_21.txt
│        │     │  │     │  ├─ output_22.txt
│        │     │  │     │  ├─ output_23.txt
│        │     │  │     │  ├─ output_3.txt
│        │     │  │     │  ├─ output_4.txt
│        │     │  │     │  ├─ output_4_with_iterators.txt
│        │     │  │     │  ├─ output_5.txt
│        │     │  │     │  ├─ output_6.txt
│        │     │  │     │  ├─ output_7.txt
│        │     │  │     │  ├─ output_8.txt
│        │     │  │     │  └─ output_9.txt
│        │     │  │     └─ progress
│        │     │  │        ├─ command_progress_iterate.php
│        │     │  │        ├─ output_progress_iterate_no_shade.txt
│        │     │  │        └─ output_progress_iterate_shade.txt
│        │     │  ├─ TestAmbiguousCommandRegistering.php
│        │     │  ├─ TestAmbiguousCommandRegistering2.php
│        │     │  └─ TestCommand.php
│        │     ├─ Formatter
│        │     │  ├─ NullOutputFormatterStyleTest.php
│        │     │  ├─ NullOutputFormatterTest.php
│        │     │  ├─ OutputFormatterStyleStackTest.php
│        │     │  ├─ OutputFormatterStyleTest.php
│        │     │  └─ OutputFormatterTest.php
│        │     ├─ Helper
│        │     │  ├─ AbstractQuestionHelperTestCase.php
│        │     │  ├─ DescriptorHelperTest.php
│        │     │  ├─ DumperNativeFallbackTest.php
│        │     │  ├─ DumperTest.php
│        │     │  ├─ FormatterHelperTest.php
│        │     │  ├─ HelperSetTest.php
│        │     │  ├─ HelperTest.php
│        │     │  ├─ OutputWrapperTest.php
│        │     │  ├─ ProcessHelperTest.php
│        │     │  ├─ ProgressBarTest.php
│        │     │  ├─ ProgressIndicatorTest.php
│        │     │  ├─ QuestionHelperTest.php
│        │     │  ├─ SymfonyQuestionHelperTest.php
│        │     │  ├─ TableCellStyleTest.php
│        │     │  ├─ TableStyleTest.php
│        │     │  ├─ TableTest.php
│        │     │  ├─ TreeHelperTest.php
│        │     │  ├─ TreeNodeTest.php
│        │     │  └─ TreeStyleTest.php
│        │     ├─ Input
│        │     │  ├─ ArgvInputTest.php
│        │     │  ├─ ArrayInputTest.php
│        │     │  ├─ InputArgumentTest.php
│        │     │  ├─ InputDefinitionTest.php
│        │     │  ├─ InputOptionTest.php
│        │     │  ├─ InputTest.php
│        │     │  └─ StringInputTest.php
│        │     ├─ Logger
│        │     │  └─ ConsoleLoggerTest.php
│        │     ├─ Messenger
│        │     │  └─ RunCommandMessageHandlerTest.php
│        │     ├─ Output
│        │     │  ├─ AnsiColorModeTest.php
│        │     │  ├─ ConsoleOutputTest.php
│        │     │  ├─ ConsoleSectionOutputTest.php
│        │     │  ├─ NullOutputTest.php
│        │     │  ├─ OutputTest.php
│        │     │  └─ StreamOutputTest.php
│        │     ├─ phpt
│        │     │  ├─ alarm
│        │     │  │  └─ command_exit.phpt
│        │     │  ├─ signal
│        │     │  │  └─ command_exit.phpt
│        │     │  ├─ single_application
│        │     │  │  ├─ arg.phpt
│        │     │  │  ├─ default.phpt
│        │     │  │  ├─ help_name.phpt
│        │     │  │  ├─ version_default_name.phpt
│        │     │  │  └─ version_name.phpt
│        │     │  └─ uses_stdin_as_interactive_input.phpt
│        │     ├─ Question
│        │     │  ├─ ChoiceQuestionTest.php
│        │     │  ├─ ConfirmationQuestionTest.php
│        │     │  └─ QuestionTest.php
│        │     ├─ SignalRegistry
│        │     │  ├─ SignalMapTest.php
│        │     │  └─ SignalRegistryTest.php
│        │     ├─ Style
│        │     │  └─ SymfonyStyleTest.php
│        │     ├─ TerminalTest.php
│        │     └─ Tester
│        │        ├─ ApplicationTesterTest.php
│        │        ├─ CommandTesterTest.php
│        │        └─ Constraint
│        │           └─ CommandIsSuccessfulTest.php
│        ├─ dependency-injection
│        │  ├─ Alias.php
│        │  ├─ Argument
│        │  │  ├─ AbstractArgument.php
│        │  │  ├─ ArgumentInterface.php
│        │  │  ├─ BoundArgument.php
│        │  │  ├─ IteratorArgument.php
│        │  │  ├─ LazyClosure.php
│        │  │  ├─ RewindableGenerator.php
│        │  │  ├─ ServiceClosureArgument.php
│        │  │  ├─ ServiceLocator.php
│        │  │  ├─ ServiceLocatorArgument.php
│        │  │  └─ TaggedIteratorArgument.php
│        │  ├─ Attribute
│        │  │  ├─ AsAlias.php
│        │  │  ├─ AsDecorator.php
│        │  │  ├─ AsTaggedItem.php
│        │  │  ├─ Autoconfigure.php
│        │  │  ├─ AutoconfigureTag.php
│        │  │  ├─ Autowire.php
│        │  │  ├─ AutowireCallable.php
│        │  │  ├─ AutowireDecorated.php
│        │  │  ├─ AutowireInline.php
│        │  │  ├─ AutowireIterator.php
│        │  │  ├─ AutowireLocator.php
│        │  │  ├─ AutowireMethodOf.php
│        │  │  ├─ AutowireServiceClosure.php
│        │  │  ├─ Exclude.php
│        │  │  ├─ Lazy.php
│        │  │  ├─ TaggedIterator.php
│        │  │  ├─ TaggedLocator.php
│        │  │  ├─ Target.php
│        │  │  ├─ When.php
│        │  │  └─ WhenNot.php
│        │  ├─ CHANGELOG.md
│        │  ├─ ChildDefinition.php
│        │  ├─ Compiler
│        │  │  ├─ AbstractRecursivePass.php
│        │  │  ├─ AliasDeprecatedPublicServicesPass.php
│        │  │  ├─ AnalyzeServiceReferencesPass.php
│        │  │  ├─ AttributeAutoconfigurationPass.php
│        │  │  ├─ AutoAliasServicePass.php
│        │  │  ├─ AutowireAsDecoratorPass.php
│        │  │  ├─ AutowirePass.php
│        │  │  ├─ AutowireRequiredMethodsPass.php
│        │  │  ├─ AutowireRequiredPropertiesPass.php
│        │  │  ├─ CheckAliasValidityPass.php
│        │  │  ├─ CheckArgumentsValidityPass.php
│        │  │  ├─ CheckCircularReferencesPass.php
│        │  │  ├─ CheckDefinitionValidityPass.php
│        │  │  ├─ CheckExceptionOnInvalidReferenceBehaviorPass.php
│        │  │  ├─ CheckReferenceValidityPass.php
│        │  │  ├─ CheckTypeDeclarationsPass.php
│        │  │  ├─ Compiler.php
│        │  │  ├─ CompilerPassInterface.php
│        │  │  ├─ DecoratorServicePass.php
│        │  │  ├─ DefinitionErrorExceptionPass.php
│        │  │  ├─ ExtensionCompilerPass.php
│        │  │  ├─ InlineServiceDefinitionsPass.php
│        │  │  ├─ MergeExtensionConfigurationPass.php
│        │  │  ├─ PassConfig.php
│        │  │  ├─ PriorityTaggedServiceTrait.php
│        │  │  ├─ RegisterAutoconfigureAttributesPass.php
│        │  │  ├─ RegisterEnvVarProcessorsPass.php
│        │  │  ├─ RegisterReverseContainerPass.php
│        │  │  ├─ RegisterServiceSubscribersPass.php
│        │  │  ├─ RemoveAbstractDefinitionsPass.php
│        │  │  ├─ RemoveBuildParametersPass.php
│        │  │  ├─ RemovePrivateAliasesPass.php
│        │  │  ├─ RemoveUnusedDefinitionsPass.php
│        │  │  ├─ ReplaceAliasByActualDefinitionPass.php
│        │  │  ├─ ResolveAutowireInlineAttributesPass.php
│        │  │  ├─ ResolveBindingsPass.php
│        │  │  ├─ ResolveChildDefinitionsPass.php
│        │  │  ├─ ResolveClassPass.php
│        │  │  ├─ ResolveDecoratorStackPass.php
│        │  │  ├─ ResolveEnvPlaceholdersPass.php
│        │  │  ├─ ResolveFactoryClassPass.php
│        │  │  ├─ ResolveHotPathPass.php
│        │  │  ├─ ResolveInstanceofConditionalsPass.php
│        │  │  ├─ ResolveInvalidReferencesPass.php
│        │  │  ├─ ResolveNamedArgumentsPass.php
│        │  │  ├─ ResolveNoPreloadPass.php
│        │  │  ├─ ResolveParameterPlaceHoldersPass.php
│        │  │  ├─ ResolveReferencesToAliasesPass.php
│        │  │  ├─ ResolveServiceSubscribersPass.php
│        │  │  ├─ ResolveTaggedIteratorArgumentPass.php
│        │  │  ├─ ServiceLocatorTagPass.php
│        │  │  ├─ ServiceReferenceGraph.php
│        │  │  ├─ ServiceReferenceGraphEdge.php
│        │  │  ├─ ServiceReferenceGraphNode.php
│        │  │  └─ ValidateEnvPlaceholdersPass.php
│        │  ├─ composer.json
│        │  ├─ Config
│        │  │  ├─ ContainerParametersResource.php
│        │  │  └─ ContainerParametersResourceChecker.php
│        │  ├─ Container.php
│        │  ├─ ContainerBuilder.php
│        │  ├─ ContainerInterface.php
│        │  ├─ Definition.php
│        │  ├─ Dumper
│        │  │  ├─ Dumper.php
│        │  │  ├─ DumperInterface.php
│        │  │  ├─ GraphvizDumper.php
│        │  │  ├─ PhpDumper.php
│        │  │  ├─ Preloader.php
│        │  │  ├─ XmlDumper.php
│        │  │  └─ YamlDumper.php
│        │  ├─ EnvVarLoaderInterface.php
│        │  ├─ EnvVarProcessor.php
│        │  ├─ EnvVarProcessorInterface.php
│        │  ├─ Exception
│        │  │  ├─ AutoconfigureFailedException.php
│        │  │  ├─ AutowiringFailedException.php
│        │  │  ├─ BadMethodCallException.php
│        │  │  ├─ EmptyParameterValueException.php
│        │  │  ├─ EnvNotFoundException.php
│        │  │  ├─ EnvParameterException.php
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ InvalidArgumentException.php
│        │  │  ├─ InvalidParameterTypeException.php
│        │  │  ├─ LogicException.php
│        │  │  ├─ OutOfBoundsException.php
│        │  │  ├─ ParameterCircularReferenceException.php
│        │  │  ├─ ParameterNotFoundException.php
│        │  │  ├─ RuntimeException.php
│        │  │  ├─ ServiceCircularReferenceException.php
│        │  │  └─ ServiceNotFoundException.php
│        │  ├─ ExpressionLanguage.php
│        │  ├─ ExpressionLanguageProvider.php
│        │  ├─ Extension
│        │  │  ├─ AbstractExtension.php
│        │  │  ├─ ConfigurableExtensionInterface.php
│        │  │  ├─ ConfigurationExtensionInterface.php
│        │  │  ├─ Extension.php
│        │  │  ├─ ExtensionInterface.php
│        │  │  ├─ ExtensionTrait.php
│        │  │  └─ PrependExtensionInterface.php
│        │  ├─ LazyProxy
│        │  │  ├─ Instantiator
│        │  │  │  ├─ InstantiatorInterface.php
│        │  │  │  ├─ LazyServiceInstantiator.php
│        │  │  │  └─ RealServiceInstantiator.php
│        │  │  └─ PhpDumper
│        │  │     ├─ DumperInterface.php
│        │  │     ├─ LazyServiceDumper.php
│        │  │     └─ NullDumper.php
│        │  ├─ LICENSE
│        │  ├─ Loader
│        │  │  ├─ ClosureLoader.php
│        │  │  ├─ Configurator
│        │  │  │  ├─ AbstractConfigurator.php
│        │  │  │  ├─ AbstractServiceConfigurator.php
│        │  │  │  ├─ AliasConfigurator.php
│        │  │  │  ├─ ClosureReferenceConfigurator.php
│        │  │  │  ├─ ContainerConfigurator.php
│        │  │  │  ├─ DefaultsConfigurator.php
│        │  │  │  ├─ EnvConfigurator.php
│        │  │  │  ├─ FromCallableConfigurator.php
│        │  │  │  ├─ InlineServiceConfigurator.php
│        │  │  │  ├─ InstanceofConfigurator.php
│        │  │  │  ├─ ParametersConfigurator.php
│        │  │  │  ├─ PrototypeConfigurator.php
│        │  │  │  ├─ ReferenceConfigurator.php
│        │  │  │  ├─ ServiceConfigurator.php
│        │  │  │  ├─ ServicesConfigurator.php
│        │  │  │  └─ Traits
│        │  │  │     ├─ AbstractTrait.php
│        │  │  │     ├─ ArgumentTrait.php
│        │  │  │     ├─ AutoconfigureTrait.php
│        │  │  │     ├─ AutowireTrait.php
│        │  │  │     ├─ BindTrait.php
│        │  │  │     ├─ CallTrait.php
│        │  │  │     ├─ ClassTrait.php
│        │  │  │     ├─ ConfiguratorTrait.php
│        │  │  │     ├─ ConstructorTrait.php
│        │  │  │     ├─ DecorateTrait.php
│        │  │  │     ├─ DeprecateTrait.php
│        │  │  │     ├─ FactoryTrait.php
│        │  │  │     ├─ FileTrait.php
│        │  │  │     ├─ FromCallableTrait.php
│        │  │  │     ├─ LazyTrait.php
│        │  │  │     ├─ ParentTrait.php
│        │  │  │     ├─ PropertyTrait.php
│        │  │  │     ├─ PublicTrait.php
│        │  │  │     ├─ ShareTrait.php
│        │  │  │     ├─ SyntheticTrait.php
│        │  │  │     └─ TagTrait.php
│        │  │  ├─ DirectoryLoader.php
│        │  │  ├─ FileLoader.php
│        │  │  ├─ GlobFileLoader.php
│        │  │  ├─ IniFileLoader.php
│        │  │  ├─ PhpFileLoader.php
│        │  │  ├─ schema
│        │  │  │  └─ dic
│        │  │  │     └─ services
│        │  │  │        └─ services-1.0.xsd
│        │  │  ├─ UndefinedExtensionHandler.php
│        │  │  ├─ XmlFileLoader.php
│        │  │  └─ YamlFileLoader.php
│        │  ├─ Parameter.php
│        │  ├─ ParameterBag
│        │  │  ├─ ContainerBag.php
│        │  │  ├─ ContainerBagInterface.php
│        │  │  ├─ EnvPlaceholderParameterBag.php
│        │  │  ├─ FrozenParameterBag.php
│        │  │  ├─ ParameterBag.php
│        │  │  └─ ParameterBagInterface.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Reference.php
│        │  ├─ ReverseContainer.php
│        │  ├─ ServiceLocator.php
│        │  ├─ StaticEnvVarLoader.php
│        │  ├─ TaggedContainerInterface.php
│        │  ├─ Tests
│        │  │  ├─ AliasTest.php
│        │  │  ├─ Argument
│        │  │  │  ├─ AbstractArgumentTest.php
│        │  │  │  ├─ LazyClosureTest.php
│        │  │  │  ├─ RewindableGeneratorTest.php
│        │  │  │  └─ TaggedIteratorArgumentTest.php
│        │  │  ├─ Attribute
│        │  │  │  ├─ AutowireCallableTest.php
│        │  │  │  ├─ AutowireInlineTest.php
│        │  │  │  ├─ AutowireLocatorTest.php
│        │  │  │  ├─ AutowireMethodOfTest.php
│        │  │  │  └─ AutowireTest.php
│        │  │  ├─ ChildDefinitionTest.php
│        │  │  ├─ Compiler
│        │  │  │  ├─ AbstractRecursivePassTest.php
│        │  │  │  ├─ AliasDeprecatedPublicServicesPassTest.php
│        │  │  │  ├─ AnalyzeServiceReferencesPassTest.php
│        │  │  │  ├─ AttributeAutoconfigurationPassTest.php
│        │  │  │  ├─ AutoAliasServicePassTest.php
│        │  │  │  ├─ AutowirePassTest.php
│        │  │  │  ├─ AutowireRequiredMethodsPassTest.php
│        │  │  │  ├─ AutowireRequiredPropertiesPassTest.php
│        │  │  │  ├─ CheckAliasValidityPassTest.php
│        │  │  │  ├─ CheckArgumentsValidityPassTest.php
│        │  │  │  ├─ CheckCircularReferencesPassTest.php
│        │  │  │  ├─ CheckDefinitionValidityPassTest.php
│        │  │  │  ├─ CheckExceptionOnInvalidReferenceBehaviorPassTest.php
│        │  │  │  ├─ CheckReferenceValidityPassTest.php
│        │  │  │  ├─ CheckTypeDeclarationsPassTest.php
│        │  │  │  ├─ CustomExpressionLanguageFunctionTest.php
│        │  │  │  ├─ DecoratorServicePassTest.php
│        │  │  │  ├─ DefinitionErrorExceptionPassTest.php
│        │  │  │  ├─ ExtensionCompilerPassTest.php
│        │  │  │  ├─ InlineServiceDefinitionsPassTest.php
│        │  │  │  ├─ IntegrationTest.php
│        │  │  │  ├─ MergeExtensionConfigurationPassTest.php
│        │  │  │  ├─ OptionalServiceClass.php
│        │  │  │  ├─ PassConfigTest.php
│        │  │  │  ├─ PriorityTaggedServiceTraitTest.php
│        │  │  │  ├─ RegisterAutoconfigureAttributesPassTest.php
│        │  │  │  ├─ RegisterEnvVarProcessorsPassTest.php
│        │  │  │  ├─ RegisterReverseContainerPassTest.php
│        │  │  │  ├─ RegisterServiceSubscribersPassTest.php
│        │  │  │  ├─ RemoveBuildParametersPassTest.php
│        │  │  │  ├─ RemoveUnusedDefinitionsPassTest.php
│        │  │  │  ├─ ReplaceAliasByActualDefinitionPassTest.php
│        │  │  │  ├─ ResolveAutowireInlineAttributesPassTest.php
│        │  │  │  ├─ ResolveBindingsPassTest.php
│        │  │  │  ├─ ResolveChildDefinitionsPassTest.php
│        │  │  │  ├─ ResolveClassPassTest.php
│        │  │  │  ├─ ResolveFactoryClassPassTest.php
│        │  │  │  ├─ ResolveHotPathPassTest.php
│        │  │  │  ├─ ResolveInstanceofConditionalsPassTest.php
│        │  │  │  ├─ ResolveInvalidReferencesPassTest.php
│        │  │  │  ├─ ResolveNamedArgumentsPassTest.php
│        │  │  │  ├─ ResolveNoPreloadPassTest.php
│        │  │  │  ├─ ResolveParameterPlaceHoldersPassTest.php
│        │  │  │  ├─ ResolveReferencesToAliasesPassTest.php
│        │  │  │  ├─ ResolveTaggedIteratorArgumentPassTest.php
│        │  │  │  ├─ ServiceLocatorTagPassTest.php
│        │  │  │  └─ ValidateEnvPlaceholdersPassTest.php
│        │  │  ├─ Config
│        │  │  │  ├─ ContainerParametersResourceCheckerTest.php
│        │  │  │  └─ ContainerParametersResourceTest.php
│        │  │  ├─ ContainerBuilderTest.php
│        │  │  ├─ ContainerTest.php
│        │  │  ├─ CrossCheckTest.php
│        │  │  ├─ DefinitionTest.php
│        │  │  ├─ Dumper
│        │  │  │  ├─ GraphvizDumperTest.php
│        │  │  │  ├─ PhpDumperTest.php
│        │  │  │  ├─ PreloaderTest.php
│        │  │  │  ├─ XmlDumperTest.php
│        │  │  │  └─ YamlDumperTest.php
│        │  │  ├─ EnvVarProcessorTest.php
│        │  │  ├─ Exception
│        │  │  │  ├─ AutowiringFailedExceptionTest.php
│        │  │  │  └─ InvalidParameterTypeExceptionTest.php
│        │  │  ├─ Extension
│        │  │  │  ├─ AbstractExtensionTest.php
│        │  │  │  └─ ExtensionTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ AcmeConfig
│        │  │  │  │  └─ NestedConfig.php
│        │  │  │  ├─ AcmeConfig.php
│        │  │  │  ├─ array.json
│        │  │  │  ├─ Attribute
│        │  │  │  │  ├─ CustomAnyAttribute.php
│        │  │  │  │  ├─ CustomAutoconfiguration.php
│        │  │  │  │  ├─ CustomChildAttribute.php
│        │  │  │  │  ├─ CustomMethodAttribute.php
│        │  │  │  │  ├─ CustomParameterAttribute.php
│        │  │  │  │  └─ CustomPropertyAttribute.php
│        │  │  │  ├─ AutoconfigureAttributed.php
│        │  │  │  ├─ AutoconfiguredInterface.php
│        │  │  │  ├─ AutoconfiguredInterface2.php
│        │  │  │  ├─ AutoconfiguredService1.php
│        │  │  │  ├─ AutoconfiguredService2.php
│        │  │  │  ├─ AutoconfigureRepeated.php
│        │  │  │  ├─ AutoconfigureRepeatedBindings.php
│        │  │  │  ├─ AutoconfigureRepeatedCalls.php
│        │  │  │  ├─ AutoconfigureRepeatedOverwrite.php
│        │  │  │  ├─ AutoconfigureRepeatedProperties.php
│        │  │  │  ├─ AutoconfigureRepeatedTag.php
│        │  │  │  ├─ AutowireLocatorConsumer.php
│        │  │  │  ├─ Bar.php
│        │  │  │  ├─ BarFactory.php
│        │  │  │  ├─ BarInterface.php
│        │  │  │  ├─ BarTagClass.php
│        │  │  │  ├─ CaseSensitiveClass.php
│        │  │  │  ├─ CheckAliasValidityPass
│        │  │  │  │  ├─ FooImplementing.php
│        │  │  │  │  ├─ FooInterface.php
│        │  │  │  │  └─ FooNotImplementing.php
│        │  │  │  ├─ CheckTypeDeclarationsPass
│        │  │  │  │  ├─ Bar.php
│        │  │  │  │  ├─ BarErroredDependency.php
│        │  │  │  │  ├─ BarMethodCall.php
│        │  │  │  │  ├─ BarOptionalArgument.php
│        │  │  │  │  ├─ BarOptionalArgumentNotNull.php
│        │  │  │  │  ├─ Deprecated.php
│        │  │  │  │  ├─ Foo.php
│        │  │  │  │  ├─ FooObject.php
│        │  │  │  │  ├─ IntersectionConstructor.php
│        │  │  │  │  ├─ UnionConstructor.php
│        │  │  │  │  ├─ UnionConstructorPHP82.php
│        │  │  │  │  ├─ Waldo.php
│        │  │  │  │  ├─ WaldoFoo.php
│        │  │  │  │  ├─ WaldoInterface.php
│        │  │  │  │  └─ Wobble.php
│        │  │  │  ├─ config
│        │  │  │  │  ├─ anonymous.expected.yml
│        │  │  │  │  ├─ anonymous.php
│        │  │  │  │  ├─ basic.expected.yml
│        │  │  │  │  ├─ basic.php
│        │  │  │  │  ├─ child.expected.yml
│        │  │  │  │  ├─ child.php
│        │  │  │  │  ├─ closure.expected.yml
│        │  │  │  │  ├─ closure.php
│        │  │  │  │  ├─ config_builder.expected.yml
│        │  │  │  │  ├─ config_builder.php
│        │  │  │  │  ├─ config_builder_env_configurator.php
│        │  │  │  │  ├─ defaults.expected.yml
│        │  │  │  │  ├─ defaults.php
│        │  │  │  │  ├─ definition
│        │  │  │  │  │  ├─ foo.php
│        │  │  │  │  │  └─ multiple
│        │  │  │  │  │     ├─ bar.php
│        │  │  │  │  │     └─ baz.php
│        │  │  │  │  ├─ env_configurator.php
│        │  │  │  │  ├─ env_param.expected.yml
│        │  │  │  │  ├─ env_param.php
│        │  │  │  │  ├─ expression_factory.expected.yml
│        │  │  │  │  ├─ expression_factory.php
│        │  │  │  │  ├─ factory_short_notation.php
│        │  │  │  │  ├─ from_callable.expected.yml
│        │  │  │  │  ├─ from_callable.php
│        │  │  │  │  ├─ inline_binding.expected.yml
│        │  │  │  │  ├─ inline_binding.php
│        │  │  │  │  ├─ inline_static_constructor.expected.yml
│        │  │  │  │  ├─ inline_static_constructor.php
│        │  │  │  │  ├─ instanceof.expected.yml
│        │  │  │  │  ├─ instanceof.php
│        │  │  │  │  ├─ instanceof_static_constructor.expected.yml
│        │  │  │  │  ├─ instanceof_static_constructor.php
│        │  │  │  │  ├─ lazy_fqcn.expected.yml
│        │  │  │  │  ├─ lazy_fqcn.php
│        │  │  │  │  ├─ nested_bundle_config.php
│        │  │  │  │  ├─ nested_config_builder.php
│        │  │  │  │  ├─ not_when_env.php
│        │  │  │  │  ├─ object.expected.yml
│        │  │  │  │  ├─ object.php
│        │  │  │  │  ├─ packages
│        │  │  │  │  │  ├─ ping.yaml
│        │  │  │  │  │  ├─ third_a.yaml
│        │  │  │  │  │  ├─ third_b.yaml
│        │  │  │  │  │  └─ third_c.yaml
│        │  │  │  │  ├─ php7.expected.yml
│        │  │  │  │  ├─ php7.php
│        │  │  │  │  ├─ prototype.expected.yml
│        │  │  │  │  ├─ prototype.php
│        │  │  │  │  ├─ prototype_array.expected.yml
│        │  │  │  │  ├─ prototype_array.php
│        │  │  │  │  ├─ remove.expected.yml
│        │  │  │  │  ├─ remove.php
│        │  │  │  │  ├─ services.php
│        │  │  │  │  ├─ services9.php
│        │  │  │  │  ├─ services_autoconfigure_with_parent.php
│        │  │  │  │  ├─ services_closure_argument.php
│        │  │  │  │  ├─ services_with_enumeration.php
│        │  │  │  │  ├─ services_with_service_locator_argument.php
│        │  │  │  │  ├─ stack.php
│        │  │  │  │  ├─ static_constructor.expected.yml
│        │  │  │  │  ├─ static_constructor.php
│        │  │  │  │  ├─ when_env.php
│        │  │  │  │  └─ when_not_when_env.php
│        │  │  │  ├─ ConstructNotExists.php
│        │  │  │  ├─ Container
│        │  │  │  │  ├─ ConstructorWithMandatoryArgumentsContainer.php
│        │  │  │  │  ├─ ConstructorWithOptionalArgumentsContainer.php
│        │  │  │  │  ├─ ConstructorWithoutArgumentsContainer.php
│        │  │  │  │  └─ NoConstructorContainer.php
│        │  │  │  ├─ containers
│        │  │  │  │  ├─ container10.php
│        │  │  │  │  ├─ container11.php
│        │  │  │  │  ├─ container12.php
│        │  │  │  │  ├─ container13.php
│        │  │  │  │  ├─ container14.php
│        │  │  │  │  ├─ container15.php
│        │  │  │  │  ├─ container16.php
│        │  │  │  │  ├─ container17.php
│        │  │  │  │  ├─ container19.php
│        │  │  │  │  ├─ container21.php
│        │  │  │  │  ├─ container24.php
│        │  │  │  │  ├─ container33.php
│        │  │  │  │  ├─ container34.php
│        │  │  │  │  ├─ container8.php
│        │  │  │  │  ├─ container9.php
│        │  │  │  │  ├─ container_abstract.php
│        │  │  │  │  ├─ container_almost_circular.php
│        │  │  │  │  ├─ container_deprecated_parameters.php
│        │  │  │  │  ├─ container_env_in_id.php
│        │  │  │  │  ├─ container_inline_requires.php
│        │  │  │  │  ├─ container_nonempty_parameters.php
│        │  │  │  │  ├─ container_non_scalar_tags.php
│        │  │  │  │  ├─ container_service_locator_argument.php
│        │  │  │  │  ├─ container_uninitialized_ref.php
│        │  │  │  │  └─ CustomContainer.php
│        │  │  │  ├─ CustomDefinition.php
│        │  │  │  ├─ DependencyContainer.php
│        │  │  │  ├─ DependencyContainerInterface.php
│        │  │  │  ├─ DeprecatedClass.php
│        │  │  │  ├─ directory
│        │  │  │  │  ├─ import
│        │  │  │  │  │  └─ import.yml
│        │  │  │  │  ├─ recurse
│        │  │  │  │  │  ├─ simple.ini
│        │  │  │  │  │  └─ simple.yml
│        │  │  │  │  └─ simple.php
│        │  │  │  ├─ Extension
│        │  │  │  │  ├─ InvalidConfig
│        │  │  │  │  │  ├─ Configuration.php
│        │  │  │  │  │  └─ InvalidConfigExtension.php
│        │  │  │  │  ├─ SemiValidConfig
│        │  │  │  │  │  ├─ Configuration.php
│        │  │  │  │  │  └─ SemiValidConfigExtension.php
│        │  │  │  │  └─ ValidConfig
│        │  │  │  │     ├─ Configuration.php
│        │  │  │  │     └─ ValidConfigExtension.php
│        │  │  │  ├─ FactoryDummy.php
│        │  │  │  ├─ FactoryDummyWithoutReturnTypes.php
│        │  │  │  ├─ FooBarTaggedClass.php
│        │  │  │  ├─ FooBarTaggedForDefaultPriorityClass.php
│        │  │  │  ├─ FooClassWithDefaultArrayAttribute.php
│        │  │  │  ├─ FooClassWithDefaultEnumAttribute.php
│        │  │  │  ├─ FooClassWithDefaultObjectAttribute.php
│        │  │  │  ├─ FooClassWithEnumAttribute.php
│        │  │  │  ├─ FooForCircularWithAddCalls.php
│        │  │  │  ├─ FooTagClass.php
│        │  │  │  ├─ FooTaggedForInvalidDefaultMethodClass.php
│        │  │  │  ├─ FooUnitEnum.php
│        │  │  │  ├─ FooWithAbstractArgument.php
│        │  │  │  ├─ graphviz
│        │  │  │  │  ├─ services1.dot
│        │  │  │  │  ├─ services10-1.dot
│        │  │  │  │  ├─ services10.dot
│        │  │  │  │  ├─ services13.dot
│        │  │  │  │  ├─ services14.dot
│        │  │  │  │  ├─ services17.dot
│        │  │  │  │  ├─ services18.dot
│        │  │  │  │  ├─ services9.dot
│        │  │  │  │  └─ services_inline.dot
│        │  │  │  ├─ includes
│        │  │  │  │  ├─ AcmeExtension.php
│        │  │  │  │  ├─ autowiring_classes.php
│        │  │  │  │  ├─ autowiring_classes_80.php
│        │  │  │  │  ├─ classes.php
│        │  │  │  │  ├─ compositetype_classes.php
│        │  │  │  │  ├─ createphar.php
│        │  │  │  │  ├─ foo.php
│        │  │  │  │  ├─ FooVariadic.php
│        │  │  │  │  ├─ foo_lazy.php
│        │  │  │  │  ├─ HotPath
│        │  │  │  │  │  ├─ C1.php
│        │  │  │  │  │  ├─ C2.php
│        │  │  │  │  │  ├─ C3.php
│        │  │  │  │  │  ├─ I1.php
│        │  │  │  │  │  ├─ P1.php
│        │  │  │  │  │  └─ T1.php
│        │  │  │  │  ├─ intersectiontype_classes.php
│        │  │  │  │  ├─ MultipleArgumentsOptionalScalarNotReallyOptional.php
│        │  │  │  │  ├─ ProjectExtension.php
│        │  │  │  │  ├─ ProjectWithXsdExtension.php
│        │  │  │  │  ├─ ProjectWithXsdExtensionInPhar.phar
│        │  │  │  │  ├─ schema
│        │  │  │  │  │  └─ project-1.0.xsd
│        │  │  │  │  └─ uniontype_classes.php
│        │  │  │  ├─ ini
│        │  │  │  │  ├─ almostvalid.ini
│        │  │  │  │  ├─ ini_with_wrong_ext.xml
│        │  │  │  │  ├─ nonvalid.ini
│        │  │  │  │  ├─ parameters.ini
│        │  │  │  │  ├─ parameters1.ini
│        │  │  │  │  ├─ parameters2.ini
│        │  │  │  │  ├─ types.ini
│        │  │  │  │  └─ when-env.ini
│        │  │  │  ├─ IntBackedEnum.php
│        │  │  │  ├─ IntTagClass.php
│        │  │  │  ├─ LazyAutoconfigured.php
│        │  │  │  ├─ LazyLoaded.php
│        │  │  │  ├─ MultipleAutoconfigureAttributed.php
│        │  │  │  ├─ NamedArgumentsDummy.php
│        │  │  │  ├─ NamedArgumentsVariadicsDummy.php
│        │  │  │  ├─ NamedEnumArgumentDummy.php
│        │  │  │  ├─ NamedIterableArgumentDummy.php
│        │  │  │  ├─ NewInInitializer.php
│        │  │  │  ├─ OptionalParameter.php
│        │  │  │  ├─ ParentNotExists.php
│        │  │  │  ├─ php
│        │  │  │  │  ├─ autowire_closure.php
│        │  │  │  │  ├─ callable_adapter_consumer.php
│        │  │  │  │  ├─ closure.php
│        │  │  │  │  ├─ closure_proxy.php
│        │  │  │  │  ├─ custom_container_class_constructor_without_arguments.php
│        │  │  │  │  ├─ custom_container_class_without_constructor.php
│        │  │  │  │  ├─ custom_container_class_with_mandatory_constructor_arguments.php
│        │  │  │  │  ├─ custom_container_class_with_optional_constructor_arguments.php
│        │  │  │  │  ├─ inline_adapter_consumer.php
│        │  │  │  │  ├─ lazy_autowire_attribute.php
│        │  │  │  │  ├─ lazy_autowire_attribute_with_intersection.php
│        │  │  │  │  ├─ lazy_closure.php
│        │  │  │  │  ├─ legacy_lazy_autowire_attribute.php
│        │  │  │  │  ├─ legacy_lazy_autowire_attribute_with_intersection.php
│        │  │  │  │  ├─ legacy_services9_lazy_inlined_factories.txt
│        │  │  │  │  ├─ legacy_services_dedup_lazy.php
│        │  │  │  │  ├─ legacy_services_non_shared_lazy.php
│        │  │  │  │  ├─ legacy_services_non_shared_lazy_as_files.txt
│        │  │  │  │  ├─ legacy_services_non_shared_lazy_ghost.php
│        │  │  │  │  ├─ legacy_services_non_shared_lazy_public.php
│        │  │  │  │  ├─ legacy_services_wither_lazy.php
│        │  │  │  │  ├─ legacy_services_wither_lazy_non_shared.php
│        │  │  │  │  ├─ php_with_wrong_ext.yml
│        │  │  │  │  ├─ return_foo_string.php
│        │  │  │  │  ├─ services1-1.php
│        │  │  │  │  ├─ services1.php
│        │  │  │  │  ├─ services10.php
│        │  │  │  │  ├─ services10_as_files.txt
│        │  │  │  │  ├─ services12.php
│        │  │  │  │  ├─ services13.php
│        │  │  │  │  ├─ services19.php
│        │  │  │  │  ├─ services24.php
│        │  │  │  │  ├─ services26.php
│        │  │  │  │  ├─ services33.php
│        │  │  │  │  ├─ services8.php
│        │  │  │  │  ├─ services9_as_files.txt
│        │  │  │  │  ├─ services9_compiled.php
│        │  │  │  │  ├─ services9_inlined_factories.txt
│        │  │  │  │  ├─ services9_inlined_factories_with_tagged_iterrator.txt
│        │  │  │  │  ├─ services9_lazy_inlined_factories.txt
│        │  │  │  │  ├─ services_adawson.php
│        │  │  │  │  ├─ services_almost_circular_private.php
│        │  │  │  │  ├─ services_almost_circular_public.php
│        │  │  │  │  ├─ services_array_params.php
│        │  │  │  │  ├─ services_base64_env.php
│        │  │  │  │  ├─ services_closure_argument_compiled.php
│        │  │  │  │  ├─ services_csv_env.php
│        │  │  │  │  ├─ services_current_factory_inlining.php
│        │  │  │  │  ├─ services_dedup_lazy.php
│        │  │  │  │  ├─ services_deep_graph.php
│        │  │  │  │  ├─ services_default_env.php
│        │  │  │  │  ├─ services_deprecated_parameters.php
│        │  │  │  │  ├─ services_deprecated_parameters_as_files.txt
│        │  │  │  │  ├─ services_env_in_id.php
│        │  │  │  │  ├─ services_errored_definition.php
│        │  │  │  │  ├─ services_inline_requires.php
│        │  │  │  │  ├─ services_inline_self_ref.php
│        │  │  │  │  ├─ services_json_env.php
│        │  │  │  │  ├─ services_locator.php
│        │  │  │  │  ├─ services_new_in_initializer.php
│        │  │  │  │  ├─ services_nonempty_parameters.php
│        │  │  │  │  ├─ services_nonempty_parameters_as_files.txt
│        │  │  │  │  ├─ services_non_shared_duplicates.php
│        │  │  │  │  ├─ services_non_shared_lazy.php
│        │  │  │  │  ├─ services_non_shared_lazy_as_files.txt
│        │  │  │  │  ├─ services_non_shared_lazy_ghost.php
│        │  │  │  │  ├─ services_non_shared_lazy_public.php
│        │  │  │  │  ├─ services_private_frozen.php
│        │  │  │  │  ├─ services_private_in_expression.php
│        │  │  │  │  ├─ services_query_string_env.php
│        │  │  │  │  ├─ services_rot13_env.php
│        │  │  │  │  ├─ services_service_locator_argument.php
│        │  │  │  │  ├─ services_subscriber.php
│        │  │  │  │  ├─ services_tsantos.php
│        │  │  │  │  ├─ services_uninitialized_ref.php
│        │  │  │  │  ├─ services_unsupported_characters.php
│        │  │  │  │  ├─ services_url_env.php
│        │  │  │  │  ├─ services_wither.php
│        │  │  │  │  ├─ services_wither_annotation.php
│        │  │  │  │  ├─ services_wither_lazy.php
│        │  │  │  │  ├─ services_wither_lazy_non_shared.php
│        │  │  │  │  ├─ services_wither_staticreturntype.php
│        │  │  │  │  ├─ simple.php
│        │  │  │  │  └─ static_constructor.php
│        │  │  │  ├─ Preload
│        │  │  │  │  ├─ A.php
│        │  │  │  │  ├─ B.php
│        │  │  │  │  ├─ C.php
│        │  │  │  │  ├─ D.php
│        │  │  │  │  ├─ Dummy.php
│        │  │  │  │  ├─ DummyWithInterface.php
│        │  │  │  │  ├─ E.php
│        │  │  │  │  ├─ F.php
│        │  │  │  │  ├─ G.php
│        │  │  │  │  ├─ IntersectionDummy.php
│        │  │  │  │  └─ UnionDummy.php
│        │  │  │  ├─ Prototype
│        │  │  │  │  ├─ BadAttributes
│        │  │  │  │  │  └─ WhenNotWhenFoo.php
│        │  │  │  │  ├─ BadClasses
│        │  │  │  │  │  └─ MissingParent.php
│        │  │  │  │  ├─ Foo.php
│        │  │  │  │  ├─ FooInterface.php
│        │  │  │  │  ├─ NotFoo.php
│        │  │  │  │  ├─ OtherDir
│        │  │  │  │  │  ├─ AnotherSub
│        │  │  │  │  │  │  └─ DeeperBaz.php
│        │  │  │  │  │  ├─ Baz.php
│        │  │  │  │  │  ├─ Component1
│        │  │  │  │  │  │  ├─ Dir1
│        │  │  │  │  │  │  │  └─ Service1.php
│        │  │  │  │  │  │  └─ Dir2
│        │  │  │  │  │  │     └─ Service2.php
│        │  │  │  │  │  └─ Component2
│        │  │  │  │  │     ├─ Dir1
│        │  │  │  │  │     │  └─ Service4.php
│        │  │  │  │  │     └─ Dir2
│        │  │  │  │  │        └─ Service5.php
│        │  │  │  │  ├─ SinglyImplementedInterface
│        │  │  │  │  │  ├─ Adapter
│        │  │  │  │  │  │  └─ Adapter.php
│        │  │  │  │  │  ├─ AnotherAdapter
│        │  │  │  │  │  │  └─ Adapter.php
│        │  │  │  │  │  └─ Port
│        │  │  │  │  │     └─ PortInterface.php
│        │  │  │  │  ├─ StaticConstructor
│        │  │  │  │  │  ├─ PrototypeStaticConstructor.php
│        │  │  │  │  │  ├─ PrototypeStaticConstructorAsArgument.php
│        │  │  │  │  │  └─ PrototypeStaticConstructorInterface.php
│        │  │  │  │  └─ Sub
│        │  │  │  │     ├─ Bar.php
│        │  │  │  │     └─ BarInterface.php
│        │  │  │  ├─ PrototypeAsAlias
│        │  │  │  │  ├─ AliasBarInterface.php
│        │  │  │  │  ├─ AliasFooInterface.php
│        │  │  │  │  ├─ WithAsAlias.php
│        │  │  │  │  ├─ WithAsAliasBothEnv.php
│        │  │  │  │  ├─ WithAsAliasDevEnv.php
│        │  │  │  │  ├─ WithAsAliasDuplicate.php
│        │  │  │  │  ├─ WithAsAliasIdMultipleInterface.php
│        │  │  │  │  ├─ WithAsAliasInterface.php
│        │  │  │  │  ├─ WithAsAliasMultiple.php
│        │  │  │  │  ├─ WithAsAliasMultipleInterface.php
│        │  │  │  │  └─ WithAsAliasProdEnv.php
│        │  │  │  ├─ ReadOnlyClass.php
│        │  │  │  ├─ RemoteCaller.php
│        │  │  │  ├─ RemoteCallerHttp.php
│        │  │  │  ├─ RemoteCallerSocket.php
│        │  │  │  ├─ ScalarFactory.php
│        │  │  │  ├─ SimilarArgumentsDummy.php
│        │  │  │  ├─ StaticConstructorAutoconfigure.php
│        │  │  │  ├─ StaticMethodTag.php
│        │  │  │  ├─ StdClassDecorator.php
│        │  │  │  ├─ StringBackedEnum.php
│        │  │  │  ├─ StubbedTranslator.php
│        │  │  │  ├─ TaggedConsumerWithExclude.php
│        │  │  │  ├─ TaggedIteratorConsumer.php
│        │  │  │  ├─ TaggedIteratorConsumerWithDefaultIndexMethod.php
│        │  │  │  ├─ TaggedIteratorConsumerWithDefaultIndexMethodAndWithDefaultPriorityMethod.php
│        │  │  │  ├─ TaggedIteratorConsumerWithDefaultPriorityMethod.php
│        │  │  │  ├─ TaggedLocatorConsumer.php
│        │  │  │  ├─ TaggedLocatorConsumerConsumer.php
│        │  │  │  ├─ TaggedLocatorConsumerFactory.php
│        │  │  │  ├─ TaggedLocatorConsumerWithDefaultIndexMethod.php
│        │  │  │  ├─ TaggedLocatorConsumerWithDefaultIndexMethodAndWithDefaultPriorityMethod.php
│        │  │  │  ├─ TaggedLocatorConsumerWithDefaultPriorityMethod.php
│        │  │  │  ├─ TaggedLocatorConsumerWithoutIndex.php
│        │  │  │  ├─ TaggedLocatorConsumerWithServiceSubscriber.php
│        │  │  │  ├─ TaggedService1.php
│        │  │  │  ├─ TaggedService2.php
│        │  │  │  ├─ TaggedService3.php
│        │  │  │  ├─ TaggedService3Configurator.php
│        │  │  │  ├─ TaggedService4.php
│        │  │  │  ├─ TaggedService5.php
│        │  │  │  ├─ TestDefinition1.php
│        │  │  │  ├─ TestDefinition2.php
│        │  │  │  ├─ TestDefinition3.php
│        │  │  │  ├─ TestServiceMethodsSubscriberTrait.php
│        │  │  │  ├─ TestServiceSubscriber.php
│        │  │  │  ├─ TestServiceSubscriberChild.php
│        │  │  │  ├─ TestServiceSubscriberIntersection.php
│        │  │  │  ├─ TestServiceSubscriberIntersectionWithTrait.php
│        │  │  │  ├─ TestServiceSubscriberParent.php
│        │  │  │  ├─ TestServiceSubscriberUnion.php
│        │  │  │  ├─ TestServiceSubscriberUnionWithTrait.php
│        │  │  │  ├─ Utils
│        │  │  │  │  └─ NotAService.php
│        │  │  │  ├─ WitherStaticReturnType.php
│        │  │  │  ├─ WithTarget.php
│        │  │  │  ├─ WithTargetAnonymous.php
│        │  │  │  ├─ xml
│        │  │  │  │  ├─ bindings_and_inner_collections.xml
│        │  │  │  │  ├─ class_from_id.xml
│        │  │  │  │  ├─ closure.xml
│        │  │  │  │  ├─ defaults_bindings.xml
│        │  │  │  │  ├─ defaults_bindings2.xml
│        │  │  │  │  ├─ deprecated_alias_definitions.xml
│        │  │  │  │  ├─ extension1
│        │  │  │  │  │  └─ services.xml
│        │  │  │  │  ├─ extension2
│        │  │  │  │  │  └─ services.xml
│        │  │  │  │  ├─ extensions
│        │  │  │  │  │  ├─ services1.xml
│        │  │  │  │  │  ├─ services2.xml
│        │  │  │  │  │  ├─ services3.xml
│        │  │  │  │  │  ├─ services4.xml
│        │  │  │  │  │  ├─ services5.xml
│        │  │  │  │  │  ├─ services6.xml
│        │  │  │  │  │  └─ services7.xml
│        │  │  │  │  ├─ from_callable.xml
│        │  │  │  │  ├─ invalid_alias_definition.xml
│        │  │  │  │  ├─ key_type_argument.xml
│        │  │  │  │  ├─ key_type_incorrect_bin.xml
│        │  │  │  │  ├─ key_type_property.xml
│        │  │  │  │  ├─ key_type_wrong_constant.xml
│        │  │  │  │  ├─ namespaces.xml
│        │  │  │  │  ├─ nested_service_without_id.xml
│        │  │  │  │  ├─ nonvalid.xml
│        │  │  │  │  ├─ not_singly_implemented_interface_in_multiple_resources.xml
│        │  │  │  │  ├─ not_singly_implemented_interface_in_multiple_resources_with_previously_registered_alias.xml
│        │  │  │  │  ├─ not_singly_implemented_interface_in_multiple_resources_with_previously_registered_alias2.xml
│        │  │  │  │  ├─ returns_clone.xml
│        │  │  │  │  ├─ services1.xml
│        │  │  │  │  ├─ services10.xml
│        │  │  │  │  ├─ services13.xml
│        │  │  │  │  ├─ services14.xml
│        │  │  │  │  ├─ services2.xml
│        │  │  │  │  ├─ services21.xml
│        │  │  │  │  ├─ services23.xml
│        │  │  │  │  ├─ services24.xml
│        │  │  │  │  ├─ services28.xml
│        │  │  │  │  ├─ services29.xml
│        │  │  │  │  ├─ services3.xml
│        │  │  │  │  ├─ services30.xml
│        │  │  │  │  ├─ services4.xml
│        │  │  │  │  ├─ services4_bad_import.xml
│        │  │  │  │  ├─ services4_bad_import_file_not_found.xml
│        │  │  │  │  ├─ services4_bad_import_nonvalid.xml
│        │  │  │  │  ├─ services4_bad_import_with_errors.xml
│        │  │  │  │  ├─ services5.xml
│        │  │  │  │  ├─ services6.xml
│        │  │  │  │  ├─ services7.xml
│        │  │  │  │  ├─ services8.xml
│        │  │  │  │  ├─ services9.xml
│        │  │  │  │  ├─ services_abstract.xml
│        │  │  │  │  ├─ services_autoconfigure.xml
│        │  │  │  │  ├─ services_autoconfigure_with_parent.xml
│        │  │  │  │  ├─ services_bindings.xml
│        │  │  │  │  ├─ services_case.xml
│        │  │  │  │  ├─ services_defaults_with_parent.xml
│        │  │  │  │  ├─ services_deprecated.xml
│        │  │  │  │  ├─ services_dump_load.xml
│        │  │  │  │  ├─ services_inline_not_candidate.xml
│        │  │  │  │  ├─ services_instanceof.xml
│        │  │  │  │  ├─ services_instanceof_with_parent.xml
│        │  │  │  │  ├─ services_lazy_fqcn.xml
│        │  │  │  │  ├─ services_named_args.xml
│        │  │  │  │  ├─ services_prototype.xml
│        │  │  │  │  ├─ services_prototype_array.xml
│        │  │  │  │  ├─ services_prototype_array_with_empty_node.xml
│        │  │  │  │  ├─ services_prototype_array_with_space_node.xml
│        │  │  │  │  ├─ services_prototype_constructor.xml
│        │  │  │  │  ├─ services_tsantos.xml
│        │  │  │  │  ├─ services_without_id.xml
│        │  │  │  │  ├─ services_with_abstract_argument.xml
│        │  │  │  │  ├─ services_with_array_tags.xml
│        │  │  │  │  ├─ services_with_default_array.xml
│        │  │  │  │  ├─ services_with_default_enumeration.xml
│        │  │  │  │  ├─ services_with_default_object.xml
│        │  │  │  │  ├─ services_with_deprecated_tagged.xml
│        │  │  │  │  ├─ services_with_enumeration.xml
│        │  │  │  │  ├─ services_with_invalid_enumeration.xml
│        │  │  │  │  ├─ services_with_service_closure.xml
│        │  │  │  │  ├─ services_with_service_locator_argument.xml
│        │  │  │  │  ├─ services_with_tagged_arguments.xml
│        │  │  │  │  ├─ service_with_abstract_argument.xml
│        │  │  │  │  ├─ singly_implemented_interface_in_multiple_resources.xml
│        │  │  │  │  ├─ stack.xml
│        │  │  │  │  ├─ static_constructor.xml
│        │  │  │  │  ├─ static_constructor_and_factory.xml
│        │  │  │  │  ├─ tag_without_name.xml
│        │  │  │  │  ├─ tag_with_empty_name.xml
│        │  │  │  │  ├─ tag_with_name_attribute.xml
│        │  │  │  │  ├─ when-env-services.xml
│        │  │  │  │  ├─ when-env.xml
│        │  │  │  │  ├─ withdoctype.xml
│        │  │  │  │  ├─ with_key_outside_collection.xml
│        │  │  │  │  └─ xml_with_wrong_ext.php
│        │  │  │  └─ yaml
│        │  │  │     ├─ alt_call.yaml
│        │  │  │     ├─ anonymous_services.yml
│        │  │  │     ├─ anonymous_services_alias.yml
│        │  │  │     ├─ anonymous_services_in_instanceof.yml
│        │  │  │     ├─ anonymous_services_in_parameters.yml
│        │  │  │     ├─ badtag1.yml
│        │  │  │     ├─ badtag2.yml
│        │  │  │     ├─ bad_alias.yml
│        │  │  │     ├─ bad_calls.yml
│        │  │  │     ├─ bad_decorates.yml
│        │  │  │     ├─ bad_decoration_on_invalid_null.yml
│        │  │  │     ├─ bad_empty_defaults.yml
│        │  │  │     ├─ bad_empty_instanceof.yml
│        │  │  │     ├─ bad_factory_syntax.yml
│        │  │  │     ├─ bad_format.yml
│        │  │  │     ├─ bad_import.yml
│        │  │  │     ├─ bad_imports.yml
│        │  │  │     ├─ bad_keyword.yml
│        │  │  │     ├─ bad_parameters.yml
│        │  │  │     ├─ bad_parent.yml
│        │  │  │     ├─ bad_service.yml
│        │  │  │     ├─ bad_services.yml
│        │  │  │     ├─ bar
│        │  │  │     │  └─ services.yml
│        │  │  │     ├─ class_from_id.yml
│        │  │  │     ├─ closure.yml
│        │  │  │     ├─ constructor_with_factory.yml
│        │  │  │     ├─ defaults_bindings.yml
│        │  │  │     ├─ defaults_bindings2.yml
│        │  │  │     ├─ deprecated_alias_definitions.yml
│        │  │  │     ├─ deprecated_alias_definitions_without_package_and_version.yml
│        │  │  │     ├─ deprecated_definition_without_message.yml
│        │  │  │     ├─ foo
│        │  │  │     │  └─ services.yml
│        │  │  │     ├─ from_callable.yml
│        │  │  │     ├─ integration
│        │  │  │     │  ├─ autoconfigure_child_not_applied
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  ├─ main.yml
│        │  │  │     │  │  └─ _child.yml
│        │  │  │     │  ├─ autoconfigure_parent_child
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  ├─ main.yml
│        │  │  │     │  │  └─ _child.yml
│        │  │  │     │  ├─ autoconfigure_parent_child_tags
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  ├─ main.yml
│        │  │  │     │  │  └─ _child.yml
│        │  │  │     │  ├─ child_parent
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  └─ main.yml
│        │  │  │     │  ├─ defaults_child_tags
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  └─ main.yml
│        │  │  │     │  ├─ defaults_instanceof_importance
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  └─ main.yml
│        │  │  │     │  ├─ defaults_parent_child
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  ├─ main.yml
│        │  │  │     │  │  └─ _child.yml
│        │  │  │     │  ├─ instanceof_and_calls
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  └─ main.yml
│        │  │  │     │  └─ instanceof_parent_child
│        │  │  │     │     ├─ expected.yml
│        │  │  │     │     ├─ main.yml
│        │  │  │     │     └─ _child.yml
│        │  │  │     ├─ nonvalid1.yml
│        │  │  │     ├─ nonvalid2.yml
│        │  │  │     ├─ not_singly_implemented_interface_in_multiple_resources.yml
│        │  │  │     ├─ not_singly_implemented_interface_in_multiple_resources_with_previously_registered_alias.yml
│        │  │  │     ├─ not_singly_implemented_interface_in_multiple_resources_with_previously_registered_alias2.yml
│        │  │  │     ├─ null_config.yml
│        │  │  │     ├─ returns_clone.yaml
│        │  │  │     ├─ services1.yml
│        │  │  │     ├─ services10.yml
│        │  │  │     ├─ services11.yml
│        │  │  │     ├─ services13.yml
│        │  │  │     ├─ services14.yml
│        │  │  │     ├─ services2.yml
│        │  │  │     ├─ services21.yml
│        │  │  │     ├─ services23.yml
│        │  │  │     ├─ services24.yml
│        │  │  │     ├─ services26.yml
│        │  │  │     ├─ services28.yml
│        │  │  │     ├─ services29.yml
│        │  │  │     ├─ services3.yml
│        │  │  │     ├─ services30.yml
│        │  │  │     ├─ services31_invalid_tags.yml
│        │  │  │     ├─ services34.yml
│        │  │  │     ├─ services4.yml
│        │  │  │     ├─ services4_bad_import.yml
│        │  │  │     ├─ services4_bad_import_file_not_found.yml
│        │  │  │     ├─ services4_bad_import_nonvalid.yml
│        │  │  │     ├─ services4_bad_import_with_errors.yml
│        │  │  │     ├─ services6.yml
│        │  │  │     ├─ services7.yml
│        │  │  │     ├─ services8.yml
│        │  │  │     ├─ services9.yml
│        │  │  │     ├─ services_adawson.yml
│        │  │  │     ├─ services_autoconfigure.yml
│        │  │  │     ├─ services_autoconfigure_with_parent.yml
│        │  │  │     ├─ services_bindings.yml
│        │  │  │     ├─ services_case.yml
│        │  │  │     ├─ services_configurator_short_syntax.yml
│        │  │  │     ├─ services_deep_graph.yml
│        │  │  │     ├─ services_defaults_with_parent.yml
│        │  │  │     ├─ services_dump_load.yml
│        │  │  │     ├─ services_inline.yml
│        │  │  │     ├─ services_instanceof.yml
│        │  │  │     ├─ services_instanceof_with_parent.yml
│        │  │  │     ├─ services_lazy_fqcn.yml
│        │  │  │     ├─ services_named_args.yml
│        │  │  │     ├─ services_not_existing.yml
│        │  │  │     ├─ services_prototype.yml
│        │  │  │     ├─ services_prototype_namespace.yml
│        │  │  │     ├─ services_prototype_namespace_without_resource.yml
│        │  │  │     ├─ services_prototype_with_empty_node.yml
│        │  │  │     ├─ services_prototype_with_null_node.yml
│        │  │  │     ├─ services_short_syntax.yml
│        │  │  │     ├─ services_underscore.yml
│        │  │  │     ├─ services_with_abstract_argument.yml
│        │  │  │     ├─ services_with_array_tags.yml
│        │  │  │     ├─ services_with_default_array.yml
│        │  │  │     ├─ services_with_default_enumeration.yml
│        │  │  │     ├─ services_with_default_object.yml
│        │  │  │     ├─ services_with_enumeration.yml
│        │  │  │     ├─ services_with_enumeration_enum_tag.yml
│        │  │  │     ├─ services_with_invalid_enumeration.yml
│        │  │  │     ├─ services_with_service_closure.yml
│        │  │  │     ├─ services_with_service_locator_argument.yml
│        │  │  │     ├─ services_with_short_service_closure.yml
│        │  │  │     ├─ services_with_tagged_argument.yml
│        │  │  │     ├─ service_instanceof_factory.yml
│        │  │  │     ├─ singly_implemented_interface_in_multiple_resources.yml
│        │  │  │     ├─ stack.yaml
│        │  │  │     ├─ static_constructor.yml
│        │  │  │     ├─ tagged_deprecated.yml
│        │  │  │     ├─ tagged_iterator_optional.yml
│        │  │  │     ├─ tag_array_arguments.yml
│        │  │  │     ├─ tag_name_empty_string.yml
│        │  │  │     ├─ tag_name_no_string.yml
│        │  │  │     ├─ tag_name_only.yml
│        │  │  │     ├─ when-env.yaml
│        │  │  │     └─ yaml_with_wrong_ext.ini
│        │  │  ├─ LazyProxy
│        │  │  │  ├─ Instantiator
│        │  │  │  │  └─ RealServiceInstantiatorTest.php
│        │  │  │  └─ PhpDumper
│        │  │  │     ├─ LazyServiceDumperTest.php
│        │  │  │     └─ NullDumperTest.php
│        │  │  ├─ Loader
│        │  │  │  ├─ ClosureLoaderTest.php
│        │  │  │  ├─ Configurator
│        │  │  │  │  └─ EnvConfiguratorTest.php
│        │  │  │  ├─ DirectoryLoaderTest.php
│        │  │  │  ├─ FileLoaderTest.php
│        │  │  │  ├─ GlobFileLoaderTest.php
│        │  │  │  ├─ IniFileLoaderTest.php
│        │  │  │  ├─ LoaderResolverTest.php
│        │  │  │  ├─ PhpFileLoaderTest.php
│        │  │  │  ├─ XmlFileLoaderTest.php
│        │  │  │  └─ YamlFileLoaderTest.php
│        │  │  ├─ ParameterBag
│        │  │  │  ├─ ContainerBagTest.php
│        │  │  │  ├─ EnvPlaceholderParameterBagTest.php
│        │  │  │  ├─ FrozenParameterBagTest.php
│        │  │  │  └─ ParameterBagTest.php
│        │  │  ├─ ParameterTest.php
│        │  │  ├─ ReferenceTest.php
│        │  │  ├─ ServiceLocatorTest.php
│        │  │  └─ StaticEnvVarLoaderTest.php
│        │  ├─ TypedReference.php
│        │  └─ Variable.php
│        ├─ deprecation-contracts
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ function.php
│        │  ├─ LICENSE
│        │  └─ README.md
│        ├─ dotenv
│        │  ├─ CHANGELOG.md
│        │  ├─ Command
│        │  │  ├─ DebugCommand.php
│        │  │  └─ DotenvDumpCommand.php
│        │  ├─ composer.json
│        │  ├─ Dotenv.php
│        │  ├─ Exception
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ FormatException.php
│        │  │  ├─ FormatExceptionContext.php
│        │  │  └─ PathException.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  └─ Tests
│        │     ├─ Command
│        │     │  ├─ DebugCommandTest.php
│        │     │  ├─ DotenvDumpCommandTest.php
│        │     │  └─ Fixtures
│        │     │     ├─ Scenario1
│        │     │     │  ├─ .env
│        │     │     │  ├─ .env.local
│        │     │     │  ├─ .env.prod.local
│        │     │     │  └─ .env.test
│        │     │     ├─ Scenario2
│        │     │     │  ├─ .env.dist
│        │     │     │  ├─ .env.local.php
│        │     │     │  └─ .env.prod
│        │     │     └─ Scenario3
│        │     │        ├─ .env
│        │     │        └─ .env.dist
│        │     ├─ DotenvTest.php
│        │     └─ fixtures
│        │        └─ file_with_bom
│        ├─ error-handler
│        │  ├─ BufferingLogger.php
│        │  ├─ CHANGELOG.md
│        │  ├─ Command
│        │  │  └─ ErrorDumpCommand.php
│        │  ├─ composer.json
│        │  ├─ Debug.php
│        │  ├─ DebugClassLoader.php
│        │  ├─ Error
│        │  │  ├─ ClassNotFoundError.php
│        │  │  ├─ FatalError.php
│        │  │  ├─ OutOfMemoryError.php
│        │  │  ├─ UndefinedFunctionError.php
│        │  │  └─ UndefinedMethodError.php
│        │  ├─ ErrorEnhancer
│        │  │  ├─ ClassNotFoundErrorEnhancer.php
│        │  │  ├─ ErrorEnhancerInterface.php
│        │  │  ├─ UndefinedFunctionErrorEnhancer.php
│        │  │  └─ UndefinedMethodErrorEnhancer.php
│        │  ├─ ErrorHandler.php
│        │  ├─ ErrorRenderer
│        │  │  ├─ CliErrorRenderer.php
│        │  │  ├─ ErrorRendererInterface.php
│        │  │  ├─ FileLinkFormatter.php
│        │  │  ├─ HtmlErrorRenderer.php
│        │  │  └─ SerializerErrorRenderer.php
│        │  ├─ Exception
│        │  │  ├─ FlattenException.php
│        │  │  └─ SilencedErrorContext.php
│        │  ├─ Internal
│        │  │  └─ TentativeTypes.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Resources
│        │  │  ├─ assets
│        │  │  │  ├─ css
│        │  │  │  │  ├─ error.css
│        │  │  │  │  ├─ exception.css
│        │  │  │  │  └─ exception_full.css
│        │  │  │  ├─ images
│        │  │  │  │  ├─ chevron-right.svg
│        │  │  │  │  ├─ favicon.png.base64
│        │  │  │  │  ├─ icon-book.svg
│        │  │  │  │  ├─ icon-copy.svg
│        │  │  │  │  ├─ icon-minus-square-o.svg
│        │  │  │  │  ├─ icon-minus-square.svg
│        │  │  │  │  ├─ icon-plus-square-o.svg
│        │  │  │  │  ├─ icon-plus-square.svg
│        │  │  │  │  ├─ icon-support.svg
│        │  │  │  │  ├─ symfony-ghost.svg.php
│        │  │  │  │  └─ symfony-logo.svg
│        │  │  │  └─ js
│        │  │  │     └─ exception.js
│        │  │  ├─ bin
│        │  │  │  ├─ extract-tentative-return-types.php
│        │  │  │  └─ patch-type-declarations
│        │  │  └─ views
│        │  │     ├─ error.html.php
│        │  │     ├─ exception.html.php
│        │  │     ├─ exception_full.html.php
│        │  │     ├─ logs.html.php
│        │  │     ├─ trace.html.php
│        │  │     ├─ traces.html.php
│        │  │     └─ traces_text.html.php
│        │  ├─ Tests
│        │  │  ├─ Command
│        │  │  │  └─ ErrorDumpCommandTest.php
│        │  │  ├─ DebugClassLoaderTest.php
│        │  │  ├─ ErrorEnhancer
│        │  │  │  ├─ ClassNotFoundErrorEnhancerTest.php
│        │  │  │  ├─ UndefinedFunctionErrorEnhancerTest.php
│        │  │  │  └─ UndefinedMethodErrorEnhancerTest.php
│        │  │  ├─ ErrorHandlerTest.php
│        │  │  ├─ ErrorRenderer
│        │  │  │  ├─ FileLinkFormatterTest.php
│        │  │  │  ├─ HtmlErrorRendererTest.php
│        │  │  │  └─ SerializerErrorRendererTest.php
│        │  │  ├─ Exception
│        │  │  │  └─ FlattenExceptionTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ AnnotatedClass.php
│        │  │  │  ├─ casemismatch.php
│        │  │  │  ├─ ClassAlias.php
│        │  │  │  ├─ ClassWithAnnotatedParameters.php
│        │  │  │  ├─ DefinitionInEvaluatedCode.php
│        │  │  │  ├─ DeprecatedClass.php
│        │  │  │  ├─ DeprecatedInterface.php
│        │  │  │  ├─ ErrorHandlerThatUsesThePreviousOne.php
│        │  │  │  ├─ ExtendedFinalMethod.php
│        │  │  │  ├─ FinalClasses.php
│        │  │  │  ├─ FinalConstant
│        │  │  │  │  ├─ FinalConstants.php
│        │  │  │  │  ├─ FinalConstants2.php
│        │  │  │  │  ├─ FinalConstantsInterface.php
│        │  │  │  │  ├─ FinalConstantsInterface2.php
│        │  │  │  │  ├─ OverrideFinalConstant.php
│        │  │  │  │  └─ OverrideFinalConstant81.php
│        │  │  │  ├─ FinalMethod.php
│        │  │  │  ├─ FinalMethod2Trait.php
│        │  │  │  ├─ FinalProperty
│        │  │  │  │  ├─ FinalProperty.php
│        │  │  │  │  ├─ OutsideFinalProperty.php
│        │  │  │  │  └─ OverrideFinalPropertySameNamespace.php
│        │  │  │  ├─ InterfaceWithAnnotatedParameters.php
│        │  │  │  ├─ InternalClass.php
│        │  │  │  ├─ InternalInterface.php
│        │  │  │  ├─ InternalTrait.php
│        │  │  │  ├─ InternalTrait2.php
│        │  │  │  ├─ LoggerThatSetAnErrorHandler.php
│        │  │  │  ├─ NonDeprecatedInterface.php
│        │  │  │  ├─ notPsr0Bis.php
│        │  │  │  ├─ OutsideInterface.php
│        │  │  │  ├─ OverrideFinalProperty.php
│        │  │  │  ├─ OverrideOutsideFinalProperty.php
│        │  │  │  ├─ PEARClass.php
│        │  │  │  ├─ pixel.png
│        │  │  │  ├─ psr4
│        │  │  │  │  └─ Psr4CaseMismatch.php
│        │  │  │  ├─ reallyNotPsr0.php
│        │  │  │  ├─ ReturnType.php
│        │  │  │  ├─ ReturnTypeGrandParent.php
│        │  │  │  ├─ ReturnTypeInterface.php
│        │  │  │  ├─ ReturnTypeParent.php
│        │  │  │  ├─ ReturnTypeParentInterface.php
│        │  │  │  ├─ ReturnTypeParentPhp83.php
│        │  │  │  ├─ ReturnTypePhp83.php
│        │  │  │  ├─ StringErrorCodeException.php
│        │  │  │  ├─ SubClassWithAnnotatedParameters.php
│        │  │  │  ├─ Throwing.php
│        │  │  │  ├─ TraitWithAnnotatedParameters.php
│        │  │  │  ├─ TraitWithInternalMethod.php
│        │  │  │  ├─ VirtualClass.php
│        │  │  │  ├─ VirtualClassMagicCall.php
│        │  │  │  ├─ VirtualInterface.php
│        │  │  │  ├─ VirtualSubInterface.php
│        │  │  │  └─ VirtualTrait.php
│        │  │  ├─ Fixtures2
│        │  │  │  └─ RequiredTwice.php
│        │  │  ├─ HeaderMock.php
│        │  │  └─ phpt
│        │  │     ├─ debug_class_loader.phpt
│        │  │     ├─ decorate_exception_handler.phpt
│        │  │     ├─ exception_rethrown.phpt
│        │  │     └─ fatal_with_nested_handlers.phpt
│        │  └─ ThrowableUtils.php
│        ├─ event-dispatcher
│        │  ├─ Attribute
│        │  │  └─ AsEventListener.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ Debug
│        │  │  ├─ TraceableEventDispatcher.php
│        │  │  └─ WrappedListener.php
│        │  ├─ DependencyInjection
│        │  │  ├─ AddEventAliasesPass.php
│        │  │  └─ RegisterListenersPass.php
│        │  ├─ EventDispatcher.php
│        │  ├─ EventDispatcherInterface.php
│        │  ├─ EventSubscriberInterface.php
│        │  ├─ GenericEvent.php
│        │  ├─ ImmutableEventDispatcher.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  └─ Tests
│        │     ├─ ChildEventDispatcherTest.php
│        │     ├─ Debug
│        │     │  ├─ TraceableEventDispatcherTest.php
│        │     │  └─ WrappedListenerTest.php
│        │     ├─ DependencyInjection
│        │     │  └─ RegisterListenersPassTest.php
│        │     ├─ EventDispatcherTest.php
│        │     ├─ Fixtures
│        │     │  ├─ CustomEvent.php
│        │     │  ├─ TaggedInvokableListener.php
│        │     │  └─ TaggedMultiListener.php
│        │     ├─ GenericEventTest.php
│        │     └─ ImmutableEventDispatcherTest.php
│        ├─ event-dispatcher-contracts
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ Event.php
│        │  ├─ EventDispatcherInterface.php
│        │  ├─ LICENSE
│        │  └─ README.md
│        ├─ filesystem
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ Exception
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ FileNotFoundException.php
│        │  │  ├─ InvalidArgumentException.php
│        │  │  ├─ IOException.php
│        │  │  ├─ IOExceptionInterface.php
│        │  │  └─ RuntimeException.php
│        │  ├─ Filesystem.php
│        │  ├─ LICENSE
│        │  ├─ Path.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  └─ Tests
│        │     ├─ ExceptionTest.php
│        │     ├─ FilesystemTest.php
│        │     ├─ FilesystemTestCase.php
│        │     ├─ Fixtures
│        │     │  ├─ MockStream
│        │     │  │  └─ MockStream.php
│        │     │  └─ web
│        │     │     ├─ index.php
│        │     │     └─ logo_symfony_header.png
│        │     └─ PathTest.php
│        ├─ finder
│        │  ├─ CHANGELOG.md
│        │  ├─ Comparator
│        │  │  ├─ Comparator.php
│        │  │  ├─ DateComparator.php
│        │  │  └─ NumberComparator.php
│        │  ├─ composer.json
│        │  ├─ Exception
│        │  │  ├─ AccessDeniedException.php
│        │  │  └─ DirectoryNotFoundException.php
│        │  ├─ Finder.php
│        │  ├─ Gitignore.php
│        │  ├─ Glob.php
│        │  ├─ Iterator
│        │  │  ├─ CustomFilterIterator.php
│        │  │  ├─ DateRangeFilterIterator.php
│        │  │  ├─ DepthRangeFilterIterator.php
│        │  │  ├─ ExcludeDirectoryFilterIterator.php
│        │  │  ├─ FilecontentFilterIterator.php
│        │  │  ├─ FilenameFilterIterator.php
│        │  │  ├─ FileTypeFilterIterator.php
│        │  │  ├─ LazyIterator.php
│        │  │  ├─ MultiplePcreFilterIterator.php
│        │  │  ├─ PathFilterIterator.php
│        │  │  ├─ RecursiveDirectoryIterator.php
│        │  │  ├─ SizeRangeFilterIterator.php
│        │  │  ├─ SortableIterator.php
│        │  │  └─ VcsIgnoredFilterIterator.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ SplFileInfo.php
│        │  └─ Tests
│        │     ├─ Comparator
│        │     │  ├─ ComparatorTest.php
│        │     │  ├─ DateComparatorTest.php
│        │     │  └─ NumberComparatorTest.php
│        │     ├─ FinderOpenBasedirTest.php
│        │     ├─ FinderTest.php
│        │     ├─ Fixtures
│        │     │  ├─ .dot
│        │     │  │  ├─ a
│        │     │  │  └─ b
│        │     │  │     ├─ c.neon
│        │     │  │     └─ d.neon
│        │     │  ├─ A
│        │     │  │  ├─ a.dat
│        │     │  │  └─ B
│        │     │  │     ├─ ab.dat
│        │     │  │     └─ C
│        │     │  │        └─ abc.dat
│        │     │  ├─ copy
│        │     │  │  └─ A
│        │     │  │     ├─ a.dat.copy
│        │     │  │     └─ B
│        │     │  │        ├─ ab.dat.copy
│        │     │  │        └─ C
│        │     │  │           └─ abc.dat.copy
│        │     │  ├─ dolor.txt
│        │     │  ├─ gitignore
│        │     │  │  ├─ git_root
│        │     │  │  │  └─ search_root
│        │     │  │  │     ├─ b.txt
│        │     │  │  │     └─ dir
│        │     │  │  │        └─ a.txt
│        │     │  │  └─ search_root
│        │     │  │     ├─ a.txt
│        │     │  │     ├─ b.txt
│        │     │  │     ├─ c.txt
│        │     │  │     └─ dir
│        │     │  │        ├─ a.txt
│        │     │  │        ├─ b.txt
│        │     │  │        └─ c.txt
│        │     │  ├─ ipsum.txt
│        │     │  ├─ lorem.txt
│        │     │  ├─ one
│        │     │  │  ├─ .dot
│        │     │  │  ├─ a
│        │     │  │  └─ b
│        │     │  │     ├─ c.neon
│        │     │  │     └─ d.neon
│        │     │  ├─ r+e.gex[c]a(r)s
│        │     │  │  └─ dir
│        │     │  │     └─ bar.dat
│        │     │  └─ with space
│        │     │     └─ foo.txt
│        │     ├─ GitignoreTest.php
│        │     ├─ GlobTest.php
│        │     └─ Iterator
│        │        ├─ CustomFilterIteratorTest.php
│        │        ├─ DateRangeFilterIteratorTest.php
│        │        ├─ DepthRangeFilterIteratorTest.php
│        │        ├─ ExcludeDirectoryFilterIteratorTest.php
│        │        ├─ FilecontentFilterIteratorTest.php
│        │        ├─ FilenameFilterIteratorTest.php
│        │        ├─ FileTypeFilterIteratorTest.php
│        │        ├─ InnerNameIterator.php
│        │        ├─ Iterator.php
│        │        ├─ IteratorTestCase.php
│        │        ├─ LazyIteratorTest.php
│        │        ├─ MockFileListIterator.php
│        │        ├─ MockSplFileInfo.php
│        │        ├─ MultiplePcreFilterIteratorTest.php
│        │        ├─ PathFilterIteratorTest.php
│        │        ├─ RealIteratorTestCase.php
│        │        ├─ RecursiveDirectoryIteratorTest.php
│        │        ├─ SizeRangeFilterIteratorTest.php
│        │        ├─ SortableIteratorTest.php
│        │        ├─ VcsIgnoredFilterIteratorTest.php
│        │        └─ VfsIteratorTestTrait.php
│        ├─ flex
│        │  ├─ .php-cs-fixer.dist.php
│        │  ├─ composer.json
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ src
│        │  │  ├─ Command
│        │  │  │  ├─ DumpEnvCommand.php
│        │  │  │  ├─ InstallRecipesCommand.php
│        │  │  │  ├─ RecipesCommand.php
│        │  │  │  └─ UpdateRecipesCommand.php
│        │  │  ├─ Configurator
│        │  │  │  ├─ AbstractConfigurator.php
│        │  │  │  ├─ AddLinesConfigurator.php
│        │  │  │  ├─ BundlesConfigurator.php
│        │  │  │  ├─ ComposerCommandsConfigurator.php
│        │  │  │  ├─ ComposerScriptsConfigurator.php
│        │  │  │  ├─ ContainerConfigurator.php
│        │  │  │  ├─ CopyFromPackageConfigurator.php
│        │  │  │  ├─ CopyFromRecipeConfigurator.php
│        │  │  │  ├─ DockerComposeConfigurator.php
│        │  │  │  ├─ DockerfileConfigurator.php
│        │  │  │  ├─ DotenvConfigurator.php
│        │  │  │  ├─ EnvConfigurator.php
│        │  │  │  ├─ GitignoreConfigurator.php
│        │  │  │  └─ MakefileConfigurator.php
│        │  │  ├─ Configurator.php
│        │  │  ├─ Downloader.php
│        │  │  ├─ Event
│        │  │  │  └─ UpdateEvent.php
│        │  │  ├─ Flex.php
│        │  │  ├─ GithubApi.php
│        │  │  ├─ InformationOperation.php
│        │  │  ├─ Lock.php
│        │  │  ├─ Options.php
│        │  │  ├─ PackageFilter.php
│        │  │  ├─ PackageJsonSynchronizer.php
│        │  │  ├─ PackageResolver.php
│        │  │  ├─ Path.php
│        │  │  ├─ Recipe.php
│        │  │  ├─ Response.php
│        │  │  ├─ ScriptExecutor.php
│        │  │  ├─ SymfonyBundle.php
│        │  │  ├─ SymfonyPackInstaller.php
│        │  │  ├─ Unpack
│        │  │  │  ├─ Operation.php
│        │  │  │  └─ Result.php
│        │  │  ├─ Unpacker.php
│        │  │  └─ Update
│        │  │     ├─ DiffHelper.php
│        │  │     ├─ RecipePatch.php
│        │  │     ├─ RecipePatcher.php
│        │  │     └─ RecipeUpdate.php
│        │  └─ tests
│        │     ├─ bootstrap.php
│        │     ├─ Command
│        │     │  ├─ DumpEnvCommandTest.php
│        │     │  ├─ InstallRecipesCommandTest.php
│        │     │  └─ UpdateRecipesCommandTest.php
│        │     ├─ Configurator
│        │     │  ├─ AddLinesConfiguratorTest.php
│        │     │  ├─ BundlesConfiguratorTest.php
│        │     │  ├─ ComposerCommandConfiguratorTest.php
│        │     │  ├─ ComposerScriptsConfiguratorTest.php
│        │     │  ├─ ContainerConfiguratorTest.php
│        │     │  ├─ CopyDirectoryFromPackageConfiguratorTest.php
│        │     │  ├─ CopyFromPackageConfiguratorTest.php
│        │     │  ├─ CopyFromRecipeConfiguratorTest.php
│        │     │  ├─ DockerComposeConfiguratorTest.php
│        │     │  ├─ DockerfileConfiguratorTest.php
│        │     │  ├─ DotenvConfiguratorTest.php
│        │     │  ├─ EnvConfiguratorTest.php
│        │     │  ├─ GitignoreConfiguratorTest.php
│        │     │  └─ MakefileConfiguratorTest.php
│        │     ├─ Fixtures
│        │     │  ├─ packageJson
│        │     │  │  ├─ assets
│        │     │  │  │  └─ controllers.json
│        │     │  │  ├─ elevated_dependencies_package.json
│        │     │  │  ├─ package.json
│        │     │  │  ├─ stricter_constraints_package.json
│        │     │  │  └─ vendor
│        │     │  │     └─ symfony
│        │     │  │        ├─ existing-package
│        │     │  │        │  └─ Resources
│        │     │  │        │     └─ assets
│        │     │  │        │        └─ package.json
│        │     │  │        ├─ importmap-invalid-constraint-package
│        │     │  │        │  └─ assets
│        │     │  │        │     └─ package.json
│        │     │  │        ├─ new-package
│        │     │  │        │  └─ assets
│        │     │  │        │     └─ package.json
│        │     │  │        └─ package-no-file-package
│        │     │  │           └─ assets
│        │     │  │              └─ package.json
│        │     │  ├─ phpunit.xml.dist
│        │     │  ├─ update_recipes
│        │     │  │  ├─ composer.json
│        │     │  │  ├─ console
│        │     │  │  └─ symfony.lock
│        │     │  └─ vendor
│        │     │     ├─ composer
│        │     │     │  └─ ca-bundle
│        │     │     │     └─ src
│        │     │     │        └─ CaBundle.php
│        │     │     ├─ doctrine
│        │     │     │  └─ doctrine-cache-bundle
│        │     │     │     └─ DoctrineCacheBundle.php
│        │     │     ├─ dunglas
│        │     │     │  └─ sylius-acme-plugin
│        │     │     │     └─ src
│        │     │     │        └─ DunglasSyliusAcmePlugin.php
│        │     │     ├─ easycorp
│        │     │     │  ├─ easy-deploy-bundle
│        │     │     │  │  └─ src
│        │     │     │  │     └─ EasyDeployBundle.php
│        │     │     │  └─ easy-security-bundle
│        │     │     │     └─ EasySecurityBundle.php
│        │     │     ├─ eightpoints
│        │     │     │  └─ guzzle-bundle
│        │     │     │     └─ EightPoints
│        │     │     │        └─ Bundle
│        │     │     │           └─ GuzzleBundle
│        │     │     │              └─ GuzzleBundle.php
│        │     │     ├─ sylius
│        │     │     │  └─ shop-api-plugin
│        │     │     │     └─ src
│        │     │     │        └─ ShopApiPlugin.php
│        │     │     ├─ symfony
│        │     │     │  ├─ debug-bundle
│        │     │     │  │  └─ DebugBundle.php
│        │     │     │  ├─ dummy
│        │     │     │  │  ├─ FirstDummyBundle
│        │     │     │  │  │  └─ FirstDummyBundle.php
│        │     │     │  │  └─ SecondDummyBundle
│        │     │     │  │     └─ SecondDummyBundle.php
│        │     │     │  └─ nouse-bundle
│        │     │     │     └─ NouseBundle.php
│        │     │     ├─ symfony-cmf
│        │     │     │  └─ routing-bundle
│        │     │     │     └─ CmfRoutingBundle.php
│        │     │     └─ web-token
│        │     │        └─ jwt-bundle
│        │     │           └─ JoseFrameworkBundle.php
│        │     ├─ FlexTest.php
│        │     ├─ OptionsTest.php
│        │     ├─ PackageFilterTest.php
│        │     ├─ PackageJsonSynchronizerTest.php
│        │     ├─ PackageResolverTest.php
│        │     ├─ PathTest.php
│        │     ├─ ScriptExecutorTest.php
│        │     ├─ SymfonyBundleTest.php
│        │     ├─ UnpackerTest.php
│        │     └─ Update
│        │        ├─ DiffHelperTest.php
│        │        ├─ RecipePatcherTest.php
│        │        ├─ RecipePatchTest.php
│        │        └─ RecipeUpdateTest.php
│        ├─ framework-bundle
│        │  ├─ CacheWarmer
│        │  │  ├─ AbstractPhpFileCacheWarmer.php
│        │  │  ├─ CachePoolClearerCacheWarmer.php
│        │  │  ├─ ConfigBuilderCacheWarmer.php
│        │  │  ├─ RouterCacheWarmer.php
│        │  │  ├─ SerializerCacheWarmer.php
│        │  │  ├─ TranslationsCacheWarmer.php
│        │  │  └─ ValidatorCacheWarmer.php
│        │  ├─ CHANGELOG.md
│        │  ├─ Command
│        │  │  ├─ AboutCommand.php
│        │  │  ├─ AbstractConfigCommand.php
│        │  │  ├─ AssetsInstallCommand.php
│        │  │  ├─ BuildDebugContainerTrait.php
│        │  │  ├─ CacheClearCommand.php
│        │  │  ├─ CachePoolClearCommand.php
│        │  │  ├─ CachePoolDeleteCommand.php
│        │  │  ├─ CachePoolInvalidateTagsCommand.php
│        │  │  ├─ CachePoolListCommand.php
│        │  │  ├─ CachePoolPruneCommand.php
│        │  │  ├─ CacheWarmupCommand.php
│        │  │  ├─ ConfigDebugCommand.php
│        │  │  ├─ ConfigDumpReferenceCommand.php
│        │  │  ├─ ContainerDebugCommand.php
│        │  │  ├─ ContainerLintCommand.php
│        │  │  ├─ DebugAutowiringCommand.php
│        │  │  ├─ EventDispatcherDebugCommand.php
│        │  │  ├─ RouterDebugCommand.php
│        │  │  ├─ RouterMatchCommand.php
│        │  │  ├─ SecretsDecryptToLocalCommand.php
│        │  │  ├─ SecretsEncryptFromLocalCommand.php
│        │  │  ├─ SecretsGenerateKeysCommand.php
│        │  │  ├─ SecretsListCommand.php
│        │  │  ├─ SecretsRemoveCommand.php
│        │  │  ├─ SecretsRevealCommand.php
│        │  │  ├─ SecretsSetCommand.php
│        │  │  ├─ TranslationDebugCommand.php
│        │  │  ├─ TranslationExtractCommand.php
│        │  │  ├─ TranslationUpdateCommand.php
│        │  │  ├─ WorkflowDumpCommand.php
│        │  │  ├─ XliffLintCommand.php
│        │  │  └─ YamlLintCommand.php
│        │  ├─ composer.json
│        │  ├─ Console
│        │  │  ├─ Application.php
│        │  │  ├─ Descriptor
│        │  │  │  ├─ Descriptor.php
│        │  │  │  ├─ JsonDescriptor.php
│        │  │  │  ├─ MarkdownDescriptor.php
│        │  │  │  ├─ TextDescriptor.php
│        │  │  │  └─ XmlDescriptor.php
│        │  │  └─ Helper
│        │  │     └─ DescriptorHelper.php
│        │  ├─ Controller
│        │  │  ├─ AbstractController.php
│        │  │  ├─ ControllerResolver.php
│        │  │  ├─ RedirectController.php
│        │  │  └─ TemplateController.php
│        │  ├─ DataCollector
│        │  │  ├─ AbstractDataCollector.php
│        │  │  ├─ RouterDataCollector.php
│        │  │  └─ TemplateAwareDataCollectorInterface.php
│        │  ├─ DependencyInjection
│        │  │  ├─ Compiler
│        │  │  │  ├─ AddDebugLogProcessorPass.php
│        │  │  │  ├─ AssetsContextPass.php
│        │  │  │  ├─ ContainerBuilderDebugDumpPass.php
│        │  │  │  ├─ ErrorLoggerCompilerPass.php
│        │  │  │  ├─ ProfilerPass.php
│        │  │  │  ├─ RemoveUnusedSessionMarshallingHandlerPass.php
│        │  │  │  ├─ TestServiceContainerRealRefPass.php
│        │  │  │  ├─ TestServiceContainerWeakRefPass.php
│        │  │  │  ├─ TranslationLintCommandPass.php
│        │  │  │  ├─ TranslationUpdateCommandPass.php
│        │  │  │  └─ UnusedTagsPass.php
│        │  │  ├─ Configuration.php
│        │  │  ├─ FrameworkExtension.php
│        │  │  └─ VirtualRequestStackPass.php
│        │  ├─ EventListener
│        │  │  ├─ ConsoleProfilerListener.php
│        │  │  └─ SuggestMissingPackageSubscriber.php
│        │  ├─ FrameworkBundle.php
│        │  ├─ HttpCache
│        │  │  └─ HttpCache.php
│        │  ├─ Kernel
│        │  │  └─ MicroKernelTrait.php
│        │  ├─ KernelBrowser.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Resources
│        │  │  ├─ bin
│        │  │  │  └─ check-unused-known-tags.php
│        │  │  └─ config
│        │  │     ├─ assets.php
│        │  │     ├─ asset_mapper.php
│        │  │     ├─ cache.php
│        │  │     ├─ cache_debug.php
│        │  │     ├─ collectors.php
│        │  │     ├─ console.php
│        │  │     ├─ debug.php
│        │  │     ├─ debug_prod.php
│        │  │     ├─ error_renderer.php
│        │  │     ├─ esi.php
│        │  │     ├─ form.php
│        │  │     ├─ form_csrf.php
│        │  │     ├─ form_debug.php
│        │  │     ├─ fragment_listener.php
│        │  │     ├─ fragment_renderer.php
│        │  │     ├─ html_sanitizer.php
│        │  │     ├─ http_client.php
│        │  │     ├─ http_client_debug.php
│        │  │     ├─ identity_translator.php
│        │  │     ├─ json_streamer.php
│        │  │     ├─ lock.php
│        │  │     ├─ mailer.php
│        │  │     ├─ mailer_debug.php
│        │  │     ├─ mailer_transports.php
│        │  │     ├─ mailer_webhook.php
│        │  │     ├─ messenger.php
│        │  │     ├─ messenger_debug.php
│        │  │     ├─ mime_type.php
│        │  │     ├─ notifier.php
│        │  │     ├─ notifier_debug.php
│        │  │     ├─ notifier_transports.php
│        │  │     ├─ notifier_webhook.php
│        │  │     ├─ object_mapper.php
│        │  │     ├─ process.php
│        │  │     ├─ profiling.php
│        │  │     ├─ property_access.php
│        │  │     ├─ property_info.php
│        │  │     ├─ rate_limiter.php
│        │  │     ├─ remote_event.php
│        │  │     ├─ request.php
│        │  │     ├─ routing
│        │  │     │  ├─ errors.php
│        │  │     │  ├─ errors.xml
│        │  │     │  ├─ webhook.php
│        │  │     │  └─ webhook.xml
│        │  │     ├─ routing.php
│        │  │     ├─ scheduler.php
│        │  │     ├─ schema
│        │  │     │  └─ symfony-1.0.xsd
│        │  │     ├─ secrets.php
│        │  │     ├─ security_csrf.php
│        │  │     ├─ semaphore.php
│        │  │     ├─ serializer.php
│        │  │     ├─ serializer_debug.php
│        │  │     ├─ services.php
│        │  │     ├─ session.php
│        │  │     ├─ ssi.php
│        │  │     ├─ test.php
│        │  │     ├─ translation.php
│        │  │     ├─ translation_debug.php
│        │  │     ├─ translation_providers.php
│        │  │     ├─ type_info.php
│        │  │     ├─ uid.php
│        │  │     ├─ validator.php
│        │  │     ├─ validator_debug.php
│        │  │     ├─ web.php
│        │  │     ├─ webhook.php
│        │  │     ├─ web_link.php
│        │  │     ├─ workflow.php
│        │  │     └─ workflow_debug.php
│        │  ├─ Routing
│        │  │  ├─ Attribute
│        │  │  │  └─ AsRoutingConditionService.php
│        │  │  ├─ AttributeRouteControllerLoader.php
│        │  │  ├─ DelegatingLoader.php
│        │  │  ├─ RedirectableCompiledUrlMatcher.php
│        │  │  ├─ RouteLoaderInterface.php
│        │  │  └─ Router.php
│        │  ├─ Secrets
│        │  │  ├─ AbstractVault.php
│        │  │  ├─ DotenvVault.php
│        │  │  └─ SodiumVault.php
│        │  ├─ Test
│        │  │  ├─ BrowserKitAssertionsTrait.php
│        │  │  ├─ DomCrawlerAssertionsTrait.php
│        │  │  ├─ HttpClientAssertionsTrait.php
│        │  │  ├─ KernelTestCase.php
│        │  │  ├─ MailerAssertionsTrait.php
│        │  │  ├─ NotificationAssertionsTrait.php
│        │  │  ├─ TestBrowserToken.php
│        │  │  ├─ TestContainer.php
│        │  │  ├─ WebTestAssertionsTrait.php
│        │  │  └─ WebTestCase.php
│        │  ├─ Tests
│        │  │  ├─ CacheWarmer
│        │  │  │  ├─ ConfigBuilderCacheWarmerTest.php
│        │  │  │  ├─ RouterCacheWarmerTest.php
│        │  │  │  ├─ SerializerCacheWarmerTest.php
│        │  │  │  └─ ValidatorCacheWarmerTest.php
│        │  │  ├─ Command
│        │  │  │  ├─ AboutCommand
│        │  │  │  │  ├─ AboutCommandTest.php
│        │  │  │  │  └─ Fixture
│        │  │  │  │     └─ TestAppKernel.php
│        │  │  │  ├─ CacheClearCommand
│        │  │  │  │  ├─ CacheClearCommandTest.php
│        │  │  │  │  └─ Fixture
│        │  │  │  │     ├─ config.yml
│        │  │  │  │     └─ TestAppKernel.php
│        │  │  │  ├─ CachePoolClearCommandTest.php
│        │  │  │  ├─ CachePoolDeleteCommandTest.php
│        │  │  │  ├─ CachePoolInvalidateTagsCommandTest.php
│        │  │  │  ├─ CachePruneCommandTest.php
│        │  │  │  ├─ EventDispatcherDebugCommandTest.php
│        │  │  │  ├─ RouterMatchCommandTest.php
│        │  │  │  ├─ SecretsListCommandTest.php
│        │  │  │  ├─ SecretsRemoveCommandTest.php
│        │  │  │  ├─ SecretsRevealCommandTest.php
│        │  │  │  ├─ SecretsSetCommandTest.php
│        │  │  │  ├─ TranslationDebugCommandTest.php
│        │  │  │  ├─ TranslationExtractCommandCompletionTest.php
│        │  │  │  ├─ TranslationExtractCommandTest.php
│        │  │  │  ├─ WorkflowDumpCommandTest.php
│        │  │  │  ├─ XliffLintCommandTest.php
│        │  │  │  └─ YamlLintCommandTest.php
│        │  │  ├─ Console
│        │  │  │  ├─ ApplicationTest.php
│        │  │  │  └─ Descriptor
│        │  │  │     ├─ AbstractDescriptorTestCase.php
│        │  │  │     ├─ JsonDescriptorTest.php
│        │  │  │     ├─ MarkdownDescriptorTest.php
│        │  │  │     ├─ ObjectsProvider.php
│        │  │  │     ├─ TextDescriptorTest.php
│        │  │  │     └─ XmlDescriptorTest.php
│        │  │  ├─ Controller
│        │  │  │  ├─ AbstractControllerTest.php
│        │  │  │  ├─ ControllerResolverTest.php
│        │  │  │  ├─ RedirectControllerTest.php
│        │  │  │  ├─ TemplateControllerTest.php
│        │  │  │  └─ TestAbstractController.php
│        │  │  ├─ DataCollector
│        │  │  │  └─ RouterDataCollectorTest.php
│        │  │  ├─ DependencyInjection
│        │  │  │  ├─ Compiler
│        │  │  │  │  ├─ ProfilerPassTest.php
│        │  │  │  │  ├─ TestServiceContainerRefPassesTest.php
│        │  │  │  │  ├─ UnusedTagsPassTest.php
│        │  │  │  │  └─ UnusedTagsPassUtils.php
│        │  │  │  ├─ config
│        │  │  │  │  ├─ serializer
│        │  │  │  │  │  └─ foo.yml
│        │  │  │  │  └─ validator
│        │  │  │  │     └─ foo.xml
│        │  │  │  ├─ ConfigurationTest.php
│        │  │  │  ├─ Fixtures
│        │  │  │  │  ├─ CustomPathBundle
│        │  │  │  │  │  ├─ Resources
│        │  │  │  │  │  │  └─ config
│        │  │  │  │  │  │     ├─ validation.xml
│        │  │  │  │  │  │     └─ validation.yml
│        │  │  │  │  │  └─ src
│        │  │  │  │  │     └─ CustomPathBundle.php
│        │  │  │  │  ├─ php
│        │  │  │  │  │  ├─ assets.php
│        │  │  │  │  │  ├─ assets_disabled.php
│        │  │  │  │  │  ├─ assets_version_strategy_as_service.php
│        │  │  │  │  │  ├─ asset_mapper_without_assets.php
│        │  │  │  │  │  ├─ cache.php
│        │  │  │  │  │  ├─ cache_app_redis_tag_aware.php
│        │  │  │  │  │  ├─ cache_app_redis_tag_aware_pool.php
│        │  │  │  │  │  ├─ csrf.php
│        │  │  │  │  │  ├─ csrf_needs_session.php
│        │  │  │  │  │  ├─ default_config.php
│        │  │  │  │  │  ├─ esi_and_ssi_without_fragments.php
│        │  │  │  │  │  ├─ esi_disabled.php
│        │  │  │  │  │  ├─ exceptions.php
│        │  │  │  │  │  ├─ form_csrf_disabled.php
│        │  │  │  │  │  ├─ form_csrf_field_attr.php
│        │  │  │  │  │  ├─ form_default_csrf.php
│        │  │  │  │  │  ├─ form_no_csrf.php
│        │  │  │  │  │  ├─ fragments_and_hinclude.php
│        │  │  │  │  │  ├─ full.php
│        │  │  │  │  │  ├─ html_sanitizer.php
│        │  │  │  │  │  ├─ html_sanitizer_default_allowed_link_and_media_hosts.php
│        │  │  │  │  │  ├─ html_sanitizer_default_config.php
│        │  │  │  │  │  ├─ http_client_default_options.php
│        │  │  │  │  │  ├─ http_client_full_default_options.php
│        │  │  │  │  │  ├─ http_client_mock_response_factory.php
│        │  │  │  │  │  ├─ http_client_override_default_options.php
│        │  │  │  │  │  ├─ http_client_rate_limiter.php
│        │  │  │  │  │  ├─ http_client_retry.php
│        │  │  │  │  │  ├─ http_client_scoped_without_query_option.php
│        │  │  │  │  │  ├─ http_client_xml_key.php
│        │  │  │  │  │  ├─ json_streamer.php
│        │  │  │  │  │  ├─ lock.php
│        │  │  │  │  │  ├─ lock_named.php
│        │  │  │  │  │  ├─ lock_service.php
│        │  │  │  │  │  ├─ mailer.php
│        │  │  │  │  │  ├─ mailer_with_disabled_message_bus.php
│        │  │  │  │  │  ├─ mailer_with_dsn.php
│        │  │  │  │  │  ├─ mailer_with_specific_message_bus.php
│        │  │  │  │  │  ├─ mailer_with_transports.php
│        │  │  │  │  │  ├─ messenger.php
│        │  │  │  │  │  ├─ messenger_disabled.php
│        │  │  │  │  │  ├─ messenger_middleware_factory_erroneous_format.php
│        │  │  │  │  │  ├─ messenger_multiple_buses_without_deduplicate_middleware.php
│        │  │  │  │  │  ├─ messenger_multiple_buses_with_deduplicate_middleware.php
│        │  │  │  │  │  ├─ messenger_multiple_failure_transports.php
│        │  │  │  │  │  ├─ messenger_multiple_failure_transports_global.php
│        │  │  │  │  │  ├─ messenger_routing.php
│        │  │  │  │  │  ├─ messenger_routing_invalid_transport.php
│        │  │  │  │  │  ├─ messenger_routing_invalid_wildcard.php
│        │  │  │  │  │  ├─ messenger_routing_single.php
│        │  │  │  │  │  ├─ messenger_transport.php
│        │  │  │  │  │  ├─ messenger_transports.php
│        │  │  │  │  │  ├─ notifier.php
│        │  │  │  │  │  ├─ notifier_without_mailer.php
│        │  │  │  │  │  ├─ notifier_without_messenger.php
│        │  │  │  │  │  ├─ notifier_without_transports.php
│        │  │  │  │  │  ├─ notifier_with_disabled_message_bus.php
│        │  │  │  │  │  ├─ notifier_with_specific_message_bus.php
│        │  │  │  │  │  ├─ php_errors_disabled.php
│        │  │  │  │  │  ├─ php_errors_enabled.php
│        │  │  │  │  │  ├─ php_errors_log_level.php
│        │  │  │  │  │  ├─ php_errors_log_levels.php
│        │  │  │  │  │  ├─ profiler.php
│        │  │  │  │  │  ├─ property_accessor.php
│        │  │  │  │  │  ├─ property_info.php
│        │  │  │  │  │  ├─ property_info_with_constructor_extractor.php
│        │  │  │  │  │  ├─ request.php
│        │  │  │  │  │  ├─ semaphore.php
│        │  │  │  │  │  ├─ semaphore_named.php
│        │  │  │  │  │  ├─ semaphore_service.php
│        │  │  │  │  │  ├─ serializer_disabled.php
│        │  │  │  │  │  ├─ serializer_enabled.php
│        │  │  │  │  │  ├─ serializer_mapping.php
│        │  │  │  │  │  ├─ serializer_mapping_without_annotations.php
│        │  │  │  │  │  ├─ serializer_without_translator.php
│        │  │  │  │  │  ├─ session.php
│        │  │  │  │  │  ├─ session_cookie_secure_auto.php
│        │  │  │  │  │  ├─ ssi_disabled.php
│        │  │  │  │  │  ├─ translator_cache_dir_disabled.php
│        │  │  │  │  │  ├─ translator_fallbacks.php
│        │  │  │  │  │  ├─ translator_globals.php
│        │  │  │  │  │  ├─ translator_without_globals.php
│        │  │  │  │  │  ├─ trusted_proxies_private_ranges.php
│        │  │  │  │  │  ├─ type_info.php
│        │  │  │  │  │  ├─ validation_attributes.php
│        │  │  │  │  │  ├─ validation_auto_mapping.php
│        │  │  │  │  │  ├─ validation_email_validation_mode.php
│        │  │  │  │  │  ├─ validation_mapping.php
│        │  │  │  │  │  ├─ validation_multiple_static_methods.php
│        │  │  │  │  │  ├─ validation_no_static_method.php
│        │  │  │  │  │  ├─ validation_translation_domain.php
│        │  │  │  │  │  ├─ webhook.php
│        │  │  │  │  │  ├─ webhook_without_serializer.php
│        │  │  │  │  │  ├─ web_link.php
│        │  │  │  │  │  ├─ workflows.php
│        │  │  │  │  │  ├─ workflows_enabled.php
│        │  │  │  │  │  ├─ workflows_explicitly_enabled.php
│        │  │  │  │  │  ├─ workflows_explicitly_enabled_named_workflows.php
│        │  │  │  │  │  ├─ workflow_not_valid.php
│        │  │  │  │  │  ├─ workflow_without_support_and_support_strategy.php
│        │  │  │  │  │  ├─ workflow_with_guard_expression.php
│        │  │  │  │  │  ├─ workflow_with_multiple_transitions_with_same_name.php
│        │  │  │  │  │  ├─ workflow_with_no_events_to_dispatch.php
│        │  │  │  │  │  ├─ workflow_with_specified_events_to_dispatch.php
│        │  │  │  │  │  └─ workflow_with_support_and_support_strategy.php
│        │  │  │  │  ├─ TestBundle
│        │  │  │  │  │  ├─ Resources
│        │  │  │  │  │  │  └─ config
│        │  │  │  │  │  │     ├─ serialization.xml
│        │  │  │  │  │  │     ├─ serialization.yml
│        │  │  │  │  │  │     ├─ serializer_mapping
│        │  │  │  │  │  │     │  ├─ files
│        │  │  │  │  │  │     │  │  ├─ foo.xml
│        │  │  │  │  │  │     │  │  └─ foo.yml
│        │  │  │  │  │  │     │  ├─ serialization.yaml
│        │  │  │  │  │  │     │  └─ serialization.yml
│        │  │  │  │  │  │     ├─ validation.xml
│        │  │  │  │  │  │     ├─ validation.yml
│        │  │  │  │  │  │     └─ validation_mapping
│        │  │  │  │  │  │        ├─ files
│        │  │  │  │  │  │        │  ├─ foo.xml
│        │  │  │  │  │  │        │  └─ foo.yml
│        │  │  │  │  │  │        ├─ validation.yaml
│        │  │  │  │  │  │        └─ validation.yml
│        │  │  │  │  │  └─ TestBundle.php
│        │  │  │  │  ├─ translations
│        │  │  │  │  │  ├─ domain.with.dots.en.yml
│        │  │  │  │  │  └─ test_paths.en.yml
│        │  │  │  │  ├─ Workflow
│        │  │  │  │  │  └─ Validator
│        │  │  │  │  │     └─ DefinitionValidator.php
│        │  │  │  │  ├─ xml
│        │  │  │  │  │  ├─ assets.xml
│        │  │  │  │  │  ├─ assets_disabled.xml
│        │  │  │  │  │  ├─ assets_version_strategy_as_service.xml
│        │  │  │  │  │  ├─ asset_mapper.xml
│        │  │  │  │  │  ├─ asset_mapper_without_assets.xml
│        │  │  │  │  │  ├─ cache.xml
│        │  │  │  │  │  ├─ cache_app_redis_tag_aware.xml
│        │  │  │  │  │  ├─ cache_app_redis_tag_aware_pool.xml
│        │  │  │  │  │  ├─ csrf.xml
│        │  │  │  │  │  ├─ csrf_disabled.xml
│        │  │  │  │  │  ├─ csrf_needs_session.xml
│        │  │  │  │  │  ├─ default_config.xml
│        │  │  │  │  │  ├─ esi_and_ssi_without_fragments.xml
│        │  │  │  │  │  ├─ esi_disabled.xml
│        │  │  │  │  │  ├─ exceptions.xml
│        │  │  │  │  │  ├─ form_csrf_disabled.xml
│        │  │  │  │  │  ├─ form_csrf_field_attr.xml
│        │  │  │  │  │  ├─ form_default_csrf.xml
│        │  │  │  │  │  ├─ form_no_csrf.xml
│        │  │  │  │  │  ├─ fragments_and_hinclude.xml
│        │  │  │  │  │  ├─ full.xml
│        │  │  │  │  │  ├─ html_sanitizer.xml
│        │  │  │  │  │  ├─ html_sanitizer_default_allowed_link_and_media_hosts.xml
│        │  │  │  │  │  ├─ html_sanitizer_default_config.xml
│        │  │  │  │  │  ├─ http_client_default_options.xml
│        │  │  │  │  │  ├─ http_client_full_default_options.xml
│        │  │  │  │  │  ├─ http_client_mock_response_factory.xml
│        │  │  │  │  │  ├─ http_client_override_default_options.xml
│        │  │  │  │  │  ├─ http_client_rate_limiter.xml
│        │  │  │  │  │  ├─ http_client_retry.xml
│        │  │  │  │  │  ├─ http_client_scoped_without_query_option.xml
│        │  │  │  │  │  ├─ http_client_xml_key.xml
│        │  │  │  │  │  ├─ json_streamer.xml
│        │  │  │  │  │  ├─ lock.xml
│        │  │  │  │  │  ├─ lock_named.xml
│        │  │  │  │  │  ├─ lock_service.xml
│        │  │  │  │  │  ├─ mailer_with_disabled_message_bus.xml
│        │  │  │  │  │  ├─ mailer_with_dsn.xml
│        │  │  │  │  │  ├─ mailer_with_specific_message_bus.xml
│        │  │  │  │  │  ├─ mailer_with_transports.xml
│        │  │  │  │  │  ├─ messenger.xml
│        │  │  │  │  │  ├─ messenger_disabled.xml
│        │  │  │  │  │  ├─ messenger_multiple_buses_without_deduplicate_middleware.xml
│        │  │  │  │  │  ├─ messenger_multiple_buses_with_deduplicate_middleware.xml
│        │  │  │  │  │  ├─ messenger_multiple_failure_transports.xml
│        │  │  │  │  │  ├─ messenger_multiple_failure_transports_global.xml
│        │  │  │  │  │  ├─ messenger_routing.xml
│        │  │  │  │  │  ├─ messenger_routing_invalid_transport.xml
│        │  │  │  │  │  ├─ messenger_routing_invalid_wildcard.xml
│        │  │  │  │  │  ├─ messenger_routing_single.xml
│        │  │  │  │  │  ├─ messenger_schedule.xml
│        │  │  │  │  │  ├─ messenger_transport.xml
│        │  │  │  │  │  ├─ messenger_transports.xml
│        │  │  │  │  │  ├─ notifier.xml
│        │  │  │  │  │  ├─ notifier_without_mailer.xml
│        │  │  │  │  │  ├─ notifier_without_messenger.xml
│        │  │  │  │  │  ├─ notifier_without_transports.xml
│        │  │  │  │  │  ├─ notifier_with_disabled_message_bus.xml
│        │  │  │  │  │  ├─ notifier_with_specific_message_bus.xml
│        │  │  │  │  │  ├─ php_errors_disabled.xml
│        │  │  │  │  │  ├─ php_errors_enabled.xml
│        │  │  │  │  │  ├─ php_errors_log_level.xml
│        │  │  │  │  │  ├─ php_errors_log_levels.xml
│        │  │  │  │  │  ├─ profiler.xml
│        │  │  │  │  │  ├─ property_accessor.xml
│        │  │  │  │  │  ├─ property_info.xml
│        │  │  │  │  │  ├─ property_info_with_constructor_extractor.xml
│        │  │  │  │  │  ├─ rate_limiter.xml
│        │  │  │  │  │  ├─ request.xml
│        │  │  │  │  │  ├─ semaphore.xml
│        │  │  │  │  │  ├─ semaphore_named.xml
│        │  │  │  │  │  ├─ semaphore_service.xml
│        │  │  │  │  │  ├─ serializer_disabled.xml
│        │  │  │  │  │  ├─ serializer_enabled.xml
│        │  │  │  │  │  ├─ serializer_mapping.xml
│        │  │  │  │  │  ├─ serializer_mapping_without_annotations.xml
│        │  │  │  │  │  ├─ serializer_without_translator.xml
│        │  │  │  │  │  ├─ session.xml
│        │  │  │  │  │  ├─ session_cookie_secure_auto.xml
│        │  │  │  │  │  ├─ ssi_disabled.xml
│        │  │  │  │  │  ├─ translator_cache_dir_disabled.xml
│        │  │  │  │  │  ├─ translator_fallbacks.xml
│        │  │  │  │  │  ├─ translator_globals.xml
│        │  │  │  │  │  ├─ translator_without_globals.xml
│        │  │  │  │  │  ├─ trusted_proxies_private_ranges.xml
│        │  │  │  │  │  ├─ type_info.xml
│        │  │  │  │  │  ├─ validation_attributes.xml
│        │  │  │  │  │  ├─ validation_auto_mapping.xml
│        │  │  │  │  │  ├─ validation_email_validation_mode.xml
│        │  │  │  │  │  ├─ validation_mapping.xml
│        │  │  │  │  │  ├─ validation_multiple_static_methods.xml
│        │  │  │  │  │  ├─ validation_no_static_method.xml
│        │  │  │  │  │  ├─ validation_translation_domain.xml
│        │  │  │  │  │  ├─ webhook.xml
│        │  │  │  │  │  ├─ webhook_without_serializer.xml
│        │  │  │  │  │  ├─ web_link.xml
│        │  │  │  │  │  ├─ workflows.xml
│        │  │  │  │  │  ├─ workflows_enabled.xml
│        │  │  │  │  │  ├─ workflows_explicitly_enabled.xml
│        │  │  │  │  │  ├─ workflows_explicitly_enabled_named_workflows.xml
│        │  │  │  │  │  ├─ workflow_not_valid.xml
│        │  │  │  │  │  ├─ workflow_without_support_and_support_strategy.xml
│        │  │  │  │  │  ├─ workflow_with_guard_expression.xml
│        │  │  │  │  │  ├─ workflow_with_multiple_transitions_with_same_name.xml
│        │  │  │  │  │  ├─ workflow_with_no_events_to_dispatch.xml
│        │  │  │  │  │  ├─ workflow_with_specified_events_to_dispatch.xml
│        │  │  │  │  │  └─ workflow_with_support_and_support_strategy.xml
│        │  │  │  │  └─ yml
│        │  │  │  │     ├─ assets.yml
│        │  │  │  │     ├─ assets_disabled.yml
│        │  │  │  │     ├─ assets_version_strategy_as_service.yml
│        │  │  │  │     ├─ asset_mapper_without_assets.yml
│        │  │  │  │     ├─ cache.yml
│        │  │  │  │     ├─ cache_app_redis_tag_aware.yml
│        │  │  │  │     ├─ cache_app_redis_tag_aware_pool.yml
│        │  │  │  │     ├─ csrf.yml
│        │  │  │  │     ├─ csrf_needs_session.yml
│        │  │  │  │     ├─ default_config.yml
│        │  │  │  │     ├─ esi_and_ssi_without_fragments.yml
│        │  │  │  │     ├─ esi_disabled.yml
│        │  │  │  │     ├─ exceptions.yml
│        │  │  │  │     ├─ form_csrf_disabled.yml
│        │  │  │  │     ├─ form_csrf_field_attr.yml
│        │  │  │  │     ├─ form_default_csrf.yml
│        │  │  │  │     ├─ form_no_csrf.yml
│        │  │  │  │     ├─ fragments_and_hinclude.yml
│        │  │  │  │     ├─ full.yml
│        │  │  │  │     ├─ html_sanitizer.yml
│        │  │  │  │     ├─ html_sanitizer_default_allowed_link_and_media_hosts.yml
│        │  │  │  │     ├─ html_sanitizer_default_config.yml
│        │  │  │  │     ├─ http_client_default_options.yml
│        │  │  │  │     ├─ http_client_full_default_options.yml
│        │  │  │  │     ├─ http_client_mock_response_factory.yml
│        │  │  │  │     ├─ http_client_override_default_options.yml
│        │  │  │  │     ├─ http_client_rate_limiter.yml
│        │  │  │  │     ├─ http_client_retry.yml
│        │  │  │  │     ├─ http_client_scoped_without_query_option.yml
│        │  │  │  │     ├─ http_client_xml_key.yml
│        │  │  │  │     ├─ json_streamer.yml
│        │  │  │  │     ├─ lock.yml
│        │  │  │  │     ├─ lock_named.yml
│        │  │  │  │     ├─ lock_service.yml
│        │  │  │  │     ├─ mailer_with_disabled_message_bus.yml
│        │  │  │  │     ├─ mailer_with_dsn.yml
│        │  │  │  │     ├─ mailer_with_specific_message_bus.yml
│        │  │  │  │     ├─ mailer_with_transports.yml
│        │  │  │  │     ├─ messenger.yml
│        │  │  │  │     ├─ messenger_disabled.yml
│        │  │  │  │     ├─ messenger_middleware_factory_erroneous_format.yml
│        │  │  │  │     ├─ messenger_multiple_buses_without_deduplicate_middleware.yml
│        │  │  │  │     ├─ messenger_multiple_buses_with_deduplicate_middleware.yml
│        │  │  │  │     ├─ messenger_multiple_failure_transports.yml
│        │  │  │  │     ├─ messenger_multiple_failure_transports_global.yml
│        │  │  │  │     ├─ messenger_routing.yml
│        │  │  │  │     ├─ messenger_routing_invalid_transport.yml
│        │  │  │  │     ├─ messenger_routing_invalid_wildcard.yml
│        │  │  │  │     ├─ messenger_routing_single.yml
│        │  │  │  │     ├─ messenger_schedule.yml
│        │  │  │  │     ├─ messenger_transport.yml
│        │  │  │  │     ├─ messenger_transports.yml
│        │  │  │  │     ├─ messenger_with_disabled_reset_on_message.yml
│        │  │  │  │     ├─ messenger_with_explict_reset_on_message_legacy.yml
│        │  │  │  │     ├─ notifier.yml
│        │  │  │  │     ├─ notifier_without_mailer.yml
│        │  │  │  │     ├─ notifier_without_messenger.yml
│        │  │  │  │     ├─ notifier_without_transports.yml
│        │  │  │  │     ├─ notifier_with_disabled_message_bus.yml
│        │  │  │  │     ├─ notifier_with_specific_message_bus.yml
│        │  │  │  │     ├─ php_errors_disabled.yml
│        │  │  │  │     ├─ php_errors_enabled.yml
│        │  │  │  │     ├─ php_errors_log_level.yml
│        │  │  │  │     ├─ php_errors_log_levels.yml
│        │  │  │  │     ├─ profiler.yml
│        │  │  │  │     ├─ property_accessor.yml
│        │  │  │  │     ├─ property_info.yml
│        │  │  │  │     ├─ property_info_with_constructor_extractor.yml
│        │  │  │  │     ├─ request.yml
│        │  │  │  │     ├─ semaphore.yml
│        │  │  │  │     ├─ semaphore_named.yml
│        │  │  │  │     ├─ semaphore_service.yml
│        │  │  │  │     ├─ serializer_disabled.yml
│        │  │  │  │     ├─ serializer_enabled.yml
│        │  │  │  │     ├─ serializer_mapping.yml
│        │  │  │  │     ├─ serializer_mapping_without_annotations.yml
│        │  │  │  │     ├─ serializer_without_translator.yml
│        │  │  │  │     ├─ session.yml
│        │  │  │  │     ├─ session_cookie_secure_auto.yml
│        │  │  │  │     ├─ ssi_disabled.yml
│        │  │  │  │     ├─ translator_cache_dir_disabled.yml
│        │  │  │  │     ├─ translator_fallbacks.yml
│        │  │  │  │     ├─ translator_globals.yml
│        │  │  │  │     ├─ translator_without_globals.yml
│        │  │  │  │     ├─ trusted_proxies_private_ranges.yml
│        │  │  │  │     ├─ type_info.yml
│        │  │  │  │     ├─ validation_attributes.yml
│        │  │  │  │     ├─ validation_auto_mapping.yml
│        │  │  │  │     ├─ validation_email_validation_mode.yml
│        │  │  │  │     ├─ validation_mapping.yml
│        │  │  │  │     ├─ validation_multiple_static_methods.yml
│        │  │  │  │     ├─ validation_no_static_method.yml
│        │  │  │  │     ├─ validation_translation_domain.yml
│        │  │  │  │     ├─ webhook.yml
│        │  │  │  │     ├─ webhook_without_serializer.yml
│        │  │  │  │     ├─ web_link.yml
│        │  │  │  │     ├─ workflows.yml
│        │  │  │  │     ├─ workflows_enabled.yml
│        │  │  │  │     ├─ workflows_explicitly_enabled.yml
│        │  │  │  │     ├─ workflows_explicitly_enabled_named_workflows.yml
│        │  │  │  │     ├─ workflow_not_valid.yml
│        │  │  │  │     ├─ workflow_without_support_and_support_strategy.yml
│        │  │  │  │     ├─ workflow_with_guard_expression.yml
│        │  │  │  │     ├─ workflow_with_multiple_transitions_with_same_name.yml
│        │  │  │  │     ├─ workflow_with_no_events_to_dispatch.yml
│        │  │  │  │     ├─ workflow_with_specified_events_to_dispatch.yml
│        │  │  │  │     └─ workflow_with_support_and_support_strategy.yml
│        │  │  │  ├─ FrameworkExtensionTestCase.php
│        │  │  │  ├─ PhpFrameworkExtensionTest.php
│        │  │  │  ├─ translations
│        │  │  │  │  ├─ security.en.yaml
│        │  │  │  │  └─ test_default.en.xlf
│        │  │  │  ├─ XmlFrameworkExtensionTest.php
│        │  │  │  └─ YamlFrameworkExtensionTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ BackslashClass.php
│        │  │  │  ├─ ClassAliasExampleClass.php
│        │  │  │  ├─ ClassAliasTargetClass.php
│        │  │  │  ├─ ContainerExcluded.php
│        │  │  │  ├─ DeclaredClass.php
│        │  │  │  ├─ DeprecatedClass.php
│        │  │  │  ├─ Descriptor
│        │  │  │  │  ├─ alias_1.json
│        │  │  │  │  ├─ alias_1.md
│        │  │  │  │  ├─ alias_1.txt
│        │  │  │  │  ├─ alias_1.xml
│        │  │  │  │  ├─ alias_2.json
│        │  │  │  │  ├─ alias_2.md
│        │  │  │  │  ├─ alias_2.txt
│        │  │  │  │  ├─ alias_2.xml
│        │  │  │  │  ├─ alias_with_definition_1.json
│        │  │  │  │  ├─ alias_with_definition_1.md
│        │  │  │  │  ├─ alias_with_definition_1.txt
│        │  │  │  │  ├─ alias_with_definition_1.xml
│        │  │  │  │  ├─ alias_with_definition_2.json
│        │  │  │  │  ├─ alias_with_definition_2.md
│        │  │  │  │  ├─ alias_with_definition_2.txt
│        │  │  │  │  ├─ alias_with_definition_2.xml
│        │  │  │  │  ├─ array_parameter.json
│        │  │  │  │  ├─ array_parameter.md
│        │  │  │  │  ├─ array_parameter.txt
│        │  │  │  │  ├─ array_parameter.xml
│        │  │  │  │  ├─ builder_1_arguments.json
│        │  │  │  │  ├─ builder_1_arguments.md
│        │  │  │  │  ├─ builder_1_arguments.txt
│        │  │  │  │  ├─ builder_1_arguments.xml
│        │  │  │  │  ├─ builder_1_public.json
│        │  │  │  │  ├─ builder_1_public.md
│        │  │  │  │  ├─ builder_1_public.txt
│        │  │  │  │  ├─ builder_1_public.xml
│        │  │  │  │  ├─ builder_1_services.json
│        │  │  │  │  ├─ builder_1_services.md
│        │  │  │  │  ├─ builder_1_services.txt
│        │  │  │  │  ├─ builder_1_services.xml
│        │  │  │  │  ├─ builder_1_tag1.json
│        │  │  │  │  ├─ builder_1_tag1.md
│        │  │  │  │  ├─ builder_1_tag1.txt
│        │  │  │  │  ├─ builder_1_tag1.xml
│        │  │  │  │  ├─ builder_1_tags.json
│        │  │  │  │  ├─ builder_1_tags.md
│        │  │  │  │  ├─ builder_1_tags.txt
│        │  │  │  │  ├─ builder_1_tags.xml
│        │  │  │  │  ├─ builder_priority_tag.json
│        │  │  │  │  ├─ builder_priority_tag.md
│        │  │  │  │  ├─ builder_priority_tag.txt
│        │  │  │  │  ├─ builder_priority_tag.xml
│        │  │  │  │  ├─ cache
│        │  │  │  │  │  ├─ KernelContainerWithDeprecations.log
│        │  │  │  │  │  └─ KernelContainerWithoutDeprecations.log
│        │  │  │  │  ├─ callable_1.json
│        │  │  │  │  ├─ callable_1.md
│        │  │  │  │  ├─ callable_1.txt
│        │  │  │  │  ├─ callable_1.xml
│        │  │  │  │  ├─ callable_2.json
│        │  │  │  │  ├─ callable_2.md
│        │  │  │  │  ├─ callable_2.txt
│        │  │  │  │  ├─ callable_2.xml
│        │  │  │  │  ├─ callable_3.json
│        │  │  │  │  ├─ callable_3.md
│        │  │  │  │  ├─ callable_3.txt
│        │  │  │  │  ├─ callable_3.xml
│        │  │  │  │  ├─ callable_4.json
│        │  │  │  │  ├─ callable_4.md
│        │  │  │  │  ├─ callable_4.txt
│        │  │  │  │  ├─ callable_4.xml
│        │  │  │  │  ├─ callable_5.json
│        │  │  │  │  ├─ callable_5.md
│        │  │  │  │  ├─ callable_5.txt
│        │  │  │  │  ├─ callable_5.xml
│        │  │  │  │  ├─ callable_6.json
│        │  │  │  │  ├─ callable_6.md
│        │  │  │  │  ├─ callable_6.txt
│        │  │  │  │  ├─ callable_6.xml
│        │  │  │  │  ├─ callable_7.json
│        │  │  │  │  ├─ callable_7.md
│        │  │  │  │  ├─ callable_7.txt
│        │  │  │  │  ├─ callable_7.xml
│        │  │  │  │  ├─ callable_from_callable.json
│        │  │  │  │  ├─ callable_from_callable.md
│        │  │  │  │  ├─ callable_from_callable.txt
│        │  │  │  │  ├─ callable_from_callable.xml
│        │  │  │  │  ├─ definition_1.json
│        │  │  │  │  ├─ definition_1.md
│        │  │  │  │  ├─ definition_1.txt
│        │  │  │  │  ├─ definition_1.xml
│        │  │  │  │  ├─ definition_2.json
│        │  │  │  │  ├─ definition_2.md
│        │  │  │  │  ├─ definition_2.txt
│        │  │  │  │  ├─ definition_2.xml
│        │  │  │  │  ├─ definition_3.json
│        │  │  │  │  ├─ definition_3.md
│        │  │  │  │  ├─ definition_3.txt
│        │  │  │  │  ├─ definition_3.xml
│        │  │  │  │  ├─ definition_arguments_1.json
│        │  │  │  │  ├─ definition_arguments_1.md
│        │  │  │  │  ├─ definition_arguments_1.txt
│        │  │  │  │  ├─ definition_arguments_1.xml
│        │  │  │  │  ├─ definition_arguments_2.json
│        │  │  │  │  ├─ definition_arguments_2.md
│        │  │  │  │  ├─ definition_arguments_2.txt
│        │  │  │  │  ├─ definition_arguments_2.xml
│        │  │  │  │  ├─ definition_arguments_3.json
│        │  │  │  │  ├─ definition_arguments_3.md
│        │  │  │  │  ├─ definition_arguments_3.txt
│        │  │  │  │  ├─ definition_arguments_3.xml
│        │  │  │  │  ├─ definition_arguments_without_class.json
│        │  │  │  │  ├─ definition_arguments_without_class.md
│        │  │  │  │  ├─ definition_arguments_without_class.txt
│        │  │  │  │  ├─ definition_arguments_without_class.xml
│        │  │  │  │  ├─ definition_arguments_with_enum.json
│        │  │  │  │  ├─ definition_arguments_with_enum.md
│        │  │  │  │  ├─ definition_arguments_with_enum.txt
│        │  │  │  │  ├─ definition_arguments_with_enum.xml
│        │  │  │  │  ├─ definition_without_class.json
│        │  │  │  │  ├─ definition_without_class.md
│        │  │  │  │  ├─ definition_without_class.txt
│        │  │  │  │  ├─ definition_without_class.xml
│        │  │  │  │  ├─ deprecated_parameter.json
│        │  │  │  │  ├─ deprecated_parameter.md
│        │  │  │  │  ├─ deprecated_parameter.txt
│        │  │  │  │  ├─ deprecated_parameter.xml
│        │  │  │  │  ├─ deprecated_parameters.json
│        │  │  │  │  ├─ deprecated_parameters.md
│        │  │  │  │  ├─ deprecated_parameters.txt
│        │  │  │  │  ├─ deprecated_parameters.xml
│        │  │  │  │  ├─ deprecations.json
│        │  │  │  │  ├─ deprecations.md
│        │  │  │  │  ├─ deprecations.txt
│        │  │  │  │  ├─ deprecations.xml
│        │  │  │  │  ├─ deprecations_empty.json
│        │  │  │  │  ├─ deprecations_empty.md
│        │  │  │  │  ├─ deprecations_empty.txt
│        │  │  │  │  ├─ deprecations_empty.xml
│        │  │  │  │  ├─ event_dispatcher_1_event1.json
│        │  │  │  │  ├─ event_dispatcher_1_event1.md
│        │  │  │  │  ├─ event_dispatcher_1_event1.txt
│        │  │  │  │  ├─ event_dispatcher_1_event1.xml
│        │  │  │  │  ├─ event_dispatcher_1_events.json
│        │  │  │  │  ├─ event_dispatcher_1_events.md
│        │  │  │  │  ├─ event_dispatcher_1_events.txt
│        │  │  │  │  ├─ event_dispatcher_1_events.xml
│        │  │  │  │  ├─ existing_class_def_1.json
│        │  │  │  │  ├─ existing_class_def_1.md
│        │  │  │  │  ├─ existing_class_def_1.txt
│        │  │  │  │  ├─ existing_class_def_1.xml
│        │  │  │  │  ├─ existing_class_def_2.json
│        │  │  │  │  ├─ existing_class_def_2.md
│        │  │  │  │  ├─ existing_class_def_2.txt
│        │  │  │  │  ├─ existing_class_def_2.xml
│        │  │  │  │  ├─ parameter.json
│        │  │  │  │  ├─ parameter.md
│        │  │  │  │  ├─ parameter.txt
│        │  │  │  │  ├─ parameter.xml
│        │  │  │  │  ├─ parameters_1.json
│        │  │  │  │  ├─ parameters_1.md
│        │  │  │  │  ├─ parameters_1.txt
│        │  │  │  │  ├─ parameters_1.xml
│        │  │  │  │  ├─ parameters_enums.json
│        │  │  │  │  ├─ parameters_enums.md
│        │  │  │  │  ├─ parameters_enums.txt
│        │  │  │  │  ├─ parameters_enums.xml
│        │  │  │  │  ├─ route_1.json
│        │  │  │  │  ├─ route_1.md
│        │  │  │  │  ├─ route_1.txt
│        │  │  │  │  ├─ route_1.xml
│        │  │  │  │  ├─ route_1_link.txt
│        │  │  │  │  ├─ route_2.json
│        │  │  │  │  ├─ route_2.md
│        │  │  │  │  ├─ route_2.txt
│        │  │  │  │  ├─ route_2.xml
│        │  │  │  │  ├─ route_2_link.txt
│        │  │  │  │  ├─ route_collection_1.json
│        │  │  │  │  ├─ route_collection_1.md
│        │  │  │  │  ├─ route_collection_1.txt
│        │  │  │  │  ├─ route_collection_1.xml
│        │  │  │  │  ├─ route_collection_2.json
│        │  │  │  │  ├─ route_collection_2.md
│        │  │  │  │  ├─ route_collection_2.txt
│        │  │  │  │  ├─ route_collection_2.xml
│        │  │  │  │  ├─ route_collection_3.json
│        │  │  │  │  ├─ route_collection_3.md
│        │  │  │  │  ├─ route_collection_3.txt
│        │  │  │  │  └─ route_collection_3.xml
│        │  │  │  ├─ FooUnitEnum.php
│        │  │  │  ├─ Messenger
│        │  │  │  │  ├─ BarMessage.php
│        │  │  │  │  ├─ DummyMessage.php
│        │  │  │  │  ├─ DummyMessageInterface.php
│        │  │  │  │  ├─ DummySchedule.php
│        │  │  │  │  ├─ DummyTask.php
│        │  │  │  │  ├─ DummyTaskWithCustomReceiver.php
│        │  │  │  │  ├─ FooMessage.php
│        │  │  │  │  └─ SecondMessage.php
│        │  │  │  ├─ ObjectMapper
│        │  │  │  │  ├─ ObjectMapped.php
│        │  │  │  │  ├─ ObjectToBeMapped.php
│        │  │  │  │  └─ TransformCallable.php
│        │  │  │  ├─ Resources
│        │  │  │  │  ├─ BaseBundle
│        │  │  │  │  │  └─ views
│        │  │  │  │  │     ├─ base.format.engine
│        │  │  │  │  │     └─ controller
│        │  │  │  │  │        └─ custom.format.engine
│        │  │  │  │  ├─ translations
│        │  │  │  │  │  ├─ domain.with.dots.en.yml
│        │  │  │  │  │  └─ messages.fr.yml
│        │  │  │  │  ├─ translations2
│        │  │  │  │  │  └─ ccc.fr.yml
│        │  │  │  │  └─ views
│        │  │  │  │     ├─ resource.format.engine
│        │  │  │  │     ├─ this.is.a.template.format.engine
│        │  │  │  │     └─ translation.html.php
│        │  │  │  ├─ Serialization
│        │  │  │  │  ├─ Author.php
│        │  │  │  │  ├─ Person.php
│        │  │  │  │  └─ Resources
│        │  │  │  │     ├─ author.yml
│        │  │  │  │     ├─ does_not_exist.yaml
│        │  │  │  │     └─ person.xml
│        │  │  │  ├─ Serializer
│        │  │  │  │  ├─ CircularReferenceHandler.php
│        │  │  │  │  └─ MaxDepthHandler.php
│        │  │  │  ├─ Suit.php
│        │  │  │  ├─ TemplatePathsCache
│        │  │  │  │  ├─ templates-empty.php
│        │  │  │  │  └─ templates.php
│        │  │  │  ├─ templates.php
│        │  │  │  ├─ TranslatableBackedEnum.php
│        │  │  │  ├─ Validation
│        │  │  │  │  ├─ Article.php
│        │  │  │  │  ├─ Author.php
│        │  │  │  │  ├─ Category.php
│        │  │  │  │  ├─ Person.php
│        │  │  │  │  ├─ Resources
│        │  │  │  │  │  ├─ author.yml
│        │  │  │  │  │  ├─ categories.yml
│        │  │  │  │  │  ├─ does_not_exist.yaml
│        │  │  │  │  │  └─ person.xml
│        │  │  │  │  └─ SubCategory.php
│        │  │  │  └─ WarmedClass.php
│        │  │  ├─ Functional
│        │  │  │  ├─ AbstractAttributeRoutingTestCase.php
│        │  │  │  ├─ AbstractWebTestCase.php
│        │  │  │  ├─ AnnotatedControllerTest.php
│        │  │  │  ├─ ApiAttributesTest.php
│        │  │  │  ├─ app
│        │  │  │  │  ├─ AnnotatedController
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ ApiAttributesTest
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ AppKernel.php
│        │  │  │  │  ├─ AutowiringTypes
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ BundlePaths
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ CacheAttributeListener
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ CachePoolClear
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ CachePools
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ default.yml
│        │  │  │  │  │  ├─ redis_config.yml
│        │  │  │  │  │  └─ redis_custom_config.yml
│        │  │  │  │  ├─ config
│        │  │  │  │  │  ├─ default.yml
│        │  │  │  │  │  └─ framework.yml
│        │  │  │  │  ├─ ConfigDump
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ ContainerDebug
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ ContainerDump
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ ControllerServiceResolution
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ Fragment
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ routing.yml
│        │  │  │  │  │  └─ services.yml
│        │  │  │  │  ├─ HttpClient
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ routing.yml
│        │  │  │  │  │  └─ services.yml
│        │  │  │  │  ├─ JsonStreamer
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ Dto
│        │  │  │  │  │  │  └─ Dummy.php
│        │  │  │  │  │  ├─ RangeToStringValueTransformer.php
│        │  │  │  │  │  └─ StringToRangeValueTransformer.php
│        │  │  │  │  ├─ Mailer
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ routing.yml
│        │  │  │  │  │  └─ services.yml
│        │  │  │  │  ├─ Notifier
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ routing.yml
│        │  │  │  │  │  └─ services.yml
│        │  │  │  │  ├─ ObjectMapper
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ Profiler
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ ProfilerCollectParameter
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ Psr4Routing
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ RouterDebug
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ RoutingConditionService
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ routing.yml
│        │  │  │  │  │  ├─ services_auto_configured.yml
│        │  │  │  │  │  └─ services_manually_configured.yml
│        │  │  │  │  ├─ Scheduler
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ Security
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ Serializer
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ default_context.yaml
│        │  │  │  │  ├─ Session
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ Slugger
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ services.yml
│        │  │  │  │  ├─ templates
│        │  │  │  │  │  └─ fragment.html.twig
│        │  │  │  │  ├─ TestServiceContainer
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ services.yml
│        │  │  │  │  │  └─ test_disabled.yml
│        │  │  │  │  ├─ TransDebug
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ services.yml
│        │  │  │  │  ├─ TypeInfo
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ Dummy.php
│        │  │  │  │  └─ Uid
│        │  │  │  │     ├─ bundles.php
│        │  │  │  │     ├─ config_disabled.yml
│        │  │  │  │     ├─ config_enabled.yml
│        │  │  │  │     └─ routing.yml
│        │  │  │  ├─ AutowiringTypesTest.php
│        │  │  │  ├─ Bundle
│        │  │  │  │  ├─ DefaultConfigTestBundle
│        │  │  │  │  │  ├─ DefaultConfigTestBundle.php
│        │  │  │  │  │  └─ DependencyInjection
│        │  │  │  │  │     ├─ Configuration.php
│        │  │  │  │  │     └─ DefaultConfigTestExtension.php
│        │  │  │  │  ├─ ExtensionWithoutConfigTestBundle
│        │  │  │  │  │  ├─ DependencyInjection
│        │  │  │  │  │  │  └─ ExtensionWithoutConfigTestExtension.php
│        │  │  │  │  │  └─ ExtensionWithoutConfigTestBundle.php
│        │  │  │  │  ├─ LegacyBundle
│        │  │  │  │  │  ├─ Entity
│        │  │  │  │  │  │  └─ LegacyPerson.php
│        │  │  │  │  │  ├─ LegacyBundle.php
│        │  │  │  │  │  └─ Resources
│        │  │  │  │  │     ├─ config
│        │  │  │  │  │     │  ├─ serialization.yaml
│        │  │  │  │  │     │  └─ validation.yaml
│        │  │  │  │  │     ├─ public
│        │  │  │  │  │     │  └─ legacy.css
│        │  │  │  │  │     ├─ translations
│        │  │  │  │  │     │  └─ legacy.en.yaml
│        │  │  │  │  │     └─ views
│        │  │  │  │  │        └─ index.html.twig
│        │  │  │  │  ├─ ModernBundle
│        │  │  │  │  │  ├─ config
│        │  │  │  │  │  │  ├─ serialization.yaml
│        │  │  │  │  │  │  └─ validation.yaml
│        │  │  │  │  │  ├─ public
│        │  │  │  │  │  │  └─ modern.css
│        │  │  │  │  │  ├─ src
│        │  │  │  │  │  │  ├─ Entity
│        │  │  │  │  │  │  │  └─ ModernPerson.php
│        │  │  │  │  │  │  └─ ModernBundle.php
│        │  │  │  │  │  ├─ templates
│        │  │  │  │  │  │  └─ index.html.twig
│        │  │  │  │  │  └─ translations
│        │  │  │  │  │     └─ modern.en.yaml
│        │  │  │  │  ├─ RoutingConditionServiceBundle
│        │  │  │  │  │  ├─ Controller
│        │  │  │  │  │  │  └─ DefaultController.php
│        │  │  │  │  │  ├─ RoutingConditionServiceBundle.php
│        │  │  │  │  │  └─ Service
│        │  │  │  │  │     ├─ AutoConfiguredNonAliasedService.php
│        │  │  │  │  │     ├─ AutoConfiguredService.php
│        │  │  │  │  │     ├─ FooOriginalService.php
│        │  │  │  │  │     ├─ FooReplacementService.php
│        │  │  │  │  │     └─ ManuallyTaggedService.php
│        │  │  │  │  └─ TestBundle
│        │  │  │  │     ├─ AutowiringTypes
│        │  │  │  │     │  └─ AutowiredServices.php
│        │  │  │  │     ├─ Controller
│        │  │  │  │     │  ├─ AnnotatedController.php
│        │  │  │  │     │  ├─ EmailController.php
│        │  │  │  │     │  ├─ FragmentController.php
│        │  │  │  │     │  ├─ HttpClientController.php
│        │  │  │  │     │  ├─ NotificationController.php
│        │  │  │  │     │  ├─ ProfilerController.php
│        │  │  │  │     │  ├─ SecurityController.php
│        │  │  │  │     │  ├─ SessionController.php
│        │  │  │  │     │  ├─ SubRequestController.php
│        │  │  │  │     │  ├─ SubRequestServiceResolutionController.php
│        │  │  │  │     │  ├─ TransController.php
│        │  │  │  │     │  └─ UidController.php
│        │  │  │  │     ├─ DependencyInjection
│        │  │  │  │     │  ├─ Config
│        │  │  │  │     │  │  └─ CustomConfig.php
│        │  │  │  │     │  ├─ Configuration.php
│        │  │  │  │     │  └─ TestExtension.php
│        │  │  │  │     ├─ Resources
│        │  │  │  │     │  └─ config
│        │  │  │  │     │     └─ routing.yml
│        │  │  │  │     ├─ Slugger
│        │  │  │  │     │  └─ SlugConstructArgService.php
│        │  │  │  │     ├─ TestBundle.php
│        │  │  │  │     ├─ Tests
│        │  │  │  │     │  └─ MockClientCallback.php
│        │  │  │  │     ├─ TestServiceContainer
│        │  │  │  │     │  ├─ NonPublicService.php
│        │  │  │  │     │  ├─ PrivateService.php
│        │  │  │  │     │  ├─ PublicService.php
│        │  │  │  │     │  ├─ ResettableService.php
│        │  │  │  │     │  └─ UnusedPrivateService.php
│        │  │  │  │     └─ TransDebug
│        │  │  │  │        ├─ TransConstructArgService.php
│        │  │  │  │        ├─ TransMethodCallsService.php
│        │  │  │  │        ├─ TransPropertyService.php
│        │  │  │  │        └─ TransSubscriberService.php
│        │  │  │  ├─ BundlePathsTest.php
│        │  │  │  ├─ CacheAttributeListenerTest.php
│        │  │  │  ├─ CachePoolClearCommandTest.php
│        │  │  │  ├─ CachePoolListCommandTest.php
│        │  │  │  ├─ CachePoolsTest.php
│        │  │  │  ├─ ConfigDebugCommandTest.php
│        │  │  │  ├─ ConfigDumpReferenceCommandTest.php
│        │  │  │  ├─ ContainerDebugCommandTest.php
│        │  │  │  ├─ ContainerDumpTest.php
│        │  │  │  ├─ DebugAutowiringCommandTest.php
│        │  │  │  ├─ Extension
│        │  │  │  │  └─ TestDumpExtension.php
│        │  │  │  ├─ Fixtures
│        │  │  │  │  └─ describe_env_vars.txt
│        │  │  │  ├─ FragmentTest.php
│        │  │  │  ├─ HttpClientTest.php
│        │  │  │  ├─ JsonStreamerTest.php
│        │  │  │  ├─ MailerTest.php
│        │  │  │  ├─ NotificationTest.php
│        │  │  │  ├─ ObjectMapperTest.php
│        │  │  │  ├─ ProfilerTest.php
│        │  │  │  ├─ PropertyInfoTest.php
│        │  │  │  ├─ Psr4RoutingTest.php
│        │  │  │  ├─ RouterDebugCommandTest.php
│        │  │  │  ├─ RoutingConditionServiceTest.php
│        │  │  │  ├─ SchedulerTest.php
│        │  │  │  ├─ SecurityTest.php
│        │  │  │  ├─ SerializerTest.php
│        │  │  │  ├─ SessionTest.php
│        │  │  │  ├─ SluggerLocaleAwareTest.php
│        │  │  │  ├─ SubRequestsTest.php
│        │  │  │  ├─ TestServiceContainerTest.php
│        │  │  │  ├─ TranslationDebugCommandTest.php
│        │  │  │  ├─ TypeInfoTest.php
│        │  │  │  └─ UidTest.php
│        │  │  ├─ Kernel
│        │  │  │  ├─ ConcreteMicroKernel.php
│        │  │  │  ├─ default
│        │  │  │  │  ├─ config
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ routes.yaml
│        │  │  │  │  │  └─ services.yaml
│        │  │  │  │  └─ src
│        │  │  │  │     └─ DefaultKernel.php
│        │  │  │  ├─ flex-style
│        │  │  │  │  ├─ config
│        │  │  │  │  │  └─ bundles.php
│        │  │  │  │  └─ src
│        │  │  │  │     └─ FlexStyleMicroKernel.php
│        │  │  │  ├─ KernelCommand.php
│        │  │  │  ├─ MicroKernelTraitTest.php
│        │  │  │  └─ SimpleKernel.php
│        │  │  ├─ KernelBrowserTest.php
│        │  │  ├─ Routing
│        │  │  │  ├─ DelegatingLoaderTest.php
│        │  │  │  ├─ Fixtures
│        │  │  │  │  └─ with_condition.yaml
│        │  │  │  ├─ RedirectableCompiledUrlMatcherTest.php
│        │  │  │  └─ RouterTest.php
│        │  │  ├─ Secrets
│        │  │  │  ├─ DotenvVaultTest.php
│        │  │  │  └─ SodiumVaultTest.php
│        │  │  ├─ Test
│        │  │  │  ├─ TestBrowserTokenTest.php
│        │  │  │  └─ WebTestCaseTest.php
│        │  │  ├─ TestCase.php
│        │  │  └─ Translation
│        │  │     └─ TranslatorTest.php
│        │  └─ Translation
│        │     └─ Translator.php
│        ├─ http-foundation
│        │  ├─ AcceptHeader.php
│        │  ├─ AcceptHeaderItem.php
│        │  ├─ BinaryFileResponse.php
│        │  ├─ ChainRequestMatcher.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ Cookie.php
│        │  ├─ EventStreamResponse.php
│        │  ├─ Exception
│        │  │  ├─ BadRequestException.php
│        │  │  ├─ ConflictingHeadersException.php
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ ExpiredSignedUriException.php
│        │  │  ├─ JsonException.php
│        │  │  ├─ LogicException.php
│        │  │  ├─ RequestExceptionInterface.php
│        │  │  ├─ SessionNotFoundException.php
│        │  │  ├─ SignedUriException.php
│        │  │  ├─ SuspiciousOperationException.php
│        │  │  ├─ UnexpectedValueException.php
│        │  │  ├─ UnsignedUriException.php
│        │  │  └─ UnverifiedSignedUriException.php
│        │  ├─ File
│        │  │  ├─ Exception
│        │  │  │  ├─ AccessDeniedException.php
│        │  │  │  ├─ CannotWriteFileException.php
│        │  │  │  ├─ ExtensionFileException.php
│        │  │  │  ├─ FileException.php
│        │  │  │  ├─ FileNotFoundException.php
│        │  │  │  ├─ FormSizeFileException.php
│        │  │  │  ├─ IniSizeFileException.php
│        │  │  │  ├─ NoFileException.php
│        │  │  │  ├─ NoTmpDirFileException.php
│        │  │  │  ├─ PartialFileException.php
│        │  │  │  ├─ UnexpectedTypeException.php
│        │  │  │  └─ UploadException.php
│        │  │  ├─ File.php
│        │  │  ├─ Stream.php
│        │  │  └─ UploadedFile.php
│        │  ├─ FileBag.php
│        │  ├─ HeaderBag.php
│        │  ├─ HeaderUtils.php
│        │  ├─ InputBag.php
│        │  ├─ IpUtils.php
│        │  ├─ JsonResponse.php
│        │  ├─ LICENSE
│        │  ├─ ParameterBag.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ RateLimiter
│        │  │  ├─ AbstractRequestRateLimiter.php
│        │  │  ├─ PeekableRequestRateLimiterInterface.php
│        │  │  └─ RequestRateLimiterInterface.php
│        │  ├─ README.md
│        │  ├─ RedirectResponse.php
│        │  ├─ Request.php
│        │  ├─ RequestMatcher
│        │  │  ├─ AttributesRequestMatcher.php
│        │  │  ├─ ExpressionRequestMatcher.php
│        │  │  ├─ HeaderRequestMatcher.php
│        │  │  ├─ HostRequestMatcher.php
│        │  │  ├─ IpsRequestMatcher.php
│        │  │  ├─ IsJsonRequestMatcher.php
│        │  │  ├─ MethodRequestMatcher.php
│        │  │  ├─ PathRequestMatcher.php
│        │  │  ├─ PortRequestMatcher.php
│        │  │  ├─ QueryParameterRequestMatcher.php
│        │  │  └─ SchemeRequestMatcher.php
│        │  ├─ RequestMatcherInterface.php
│        │  ├─ RequestStack.php
│        │  ├─ Response.php
│        │  ├─ ResponseHeaderBag.php
│        │  ├─ ServerBag.php
│        │  ├─ ServerEvent.php
│        │  ├─ Session
│        │  │  ├─ Attribute
│        │  │  │  ├─ AttributeBag.php
│        │  │  │  └─ AttributeBagInterface.php
│        │  │  ├─ Flash
│        │  │  │  ├─ AutoExpireFlashBag.php
│        │  │  │  ├─ FlashBag.php
│        │  │  │  └─ FlashBagInterface.php
│        │  │  ├─ FlashBagAwareSessionInterface.php
│        │  │  ├─ Session.php
│        │  │  ├─ SessionBagInterface.php
│        │  │  ├─ SessionBagProxy.php
│        │  │  ├─ SessionFactory.php
│        │  │  ├─ SessionFactoryInterface.php
│        │  │  ├─ SessionInterface.php
│        │  │  ├─ SessionUtils.php
│        │  │  └─ Storage
│        │  │     ├─ Handler
│        │  │     │  ├─ AbstractSessionHandler.php
│        │  │     │  ├─ IdentityMarshaller.php
│        │  │     │  ├─ MarshallingSessionHandler.php
│        │  │     │  ├─ MemcachedSessionHandler.php
│        │  │     │  ├─ MigratingSessionHandler.php
│        │  │     │  ├─ MongoDbSessionHandler.php
│        │  │     │  ├─ NativeFileSessionHandler.php
│        │  │     │  ├─ NullSessionHandler.php
│        │  │     │  ├─ PdoSessionHandler.php
│        │  │     │  ├─ RedisSessionHandler.php
│        │  │     │  ├─ SessionHandlerFactory.php
│        │  │     │  └─ StrictSessionHandler.php
│        │  │     ├─ MetadataBag.php
│        │  │     ├─ MockArraySessionStorage.php
│        │  │     ├─ MockFileSessionStorage.php
│        │  │     ├─ MockFileSessionStorageFactory.php
│        │  │     ├─ NativeSessionStorage.php
│        │  │     ├─ NativeSessionStorageFactory.php
│        │  │     ├─ PhpBridgeSessionStorage.php
│        │  │     ├─ PhpBridgeSessionStorageFactory.php
│        │  │     ├─ Proxy
│        │  │     │  ├─ AbstractProxy.php
│        │  │     │  └─ SessionHandlerProxy.php
│        │  │     ├─ SessionStorageFactoryInterface.php
│        │  │     └─ SessionStorageInterface.php
│        │  ├─ StreamedJsonResponse.php
│        │  ├─ StreamedResponse.php
│        │  ├─ Test
│        │  │  └─ Constraint
│        │  │     ├─ RequestAttributeValueSame.php
│        │  │     ├─ ResponseCookieValueSame.php
│        │  │     ├─ ResponseFormatSame.php
│        │  │     ├─ ResponseHasCookie.php
│        │  │     ├─ ResponseHasHeader.php
│        │  │     ├─ ResponseHeaderLocationSame.php
│        │  │     ├─ ResponseHeaderSame.php
│        │  │     ├─ ResponseIsRedirected.php
│        │  │     ├─ ResponseIsSuccessful.php
│        │  │     ├─ ResponseIsUnprocessable.php
│        │  │     └─ ResponseStatusCodeSame.php
│        │  ├─ Tests
│        │  │  ├─ AcceptHeaderItemTest.php
│        │  │  ├─ AcceptHeaderTest.php
│        │  │  ├─ BinaryFileResponseTest.php
│        │  │  ├─ CookieTest.php
│        │  │  ├─ EventStreamResponseTest.php
│        │  │  ├─ File
│        │  │  │  ├─ FakeFile.php
│        │  │  │  ├─ FileTest.php
│        │  │  │  ├─ Fixtures
│        │  │  │  │  ├─ -test
│        │  │  │  │  ├─ .unknownextension
│        │  │  │  │  ├─ case-sensitive-mime-type.xlsm
│        │  │  │  │  ├─ directory
│        │  │  │  │  │  └─ .empty
│        │  │  │  │  ├─ other-file.example
│        │  │  │  │  ├─ test
│        │  │  │  │  ├─ test.gif
│        │  │  │  │  └─ webkitdirectory
│        │  │  │  │     ├─ nested
│        │  │  │  │     │  └─ test.txt
│        │  │  │  │     └─ test.txt
│        │  │  │  └─ UploadedFileTest.php
│        │  │  ├─ FileBagTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ FooEnum.php
│        │  │  │  ├─ response-functional
│        │  │  │  │  ├─ common.inc
│        │  │  │  │  ├─ cookie_raw_urlencode.expected
│        │  │  │  │  ├─ cookie_raw_urlencode.php
│        │  │  │  │  ├─ cookie_samesite_lax.expected
│        │  │  │  │  ├─ cookie_samesite_lax.php
│        │  │  │  │  ├─ cookie_samesite_strict.expected
│        │  │  │  │  ├─ cookie_samesite_strict.php
│        │  │  │  │  ├─ cookie_urlencode.expected
│        │  │  │  │  ├─ cookie_urlencode.php
│        │  │  │  │  ├─ deleted_cookie.expected
│        │  │  │  │  ├─ deleted_cookie.php
│        │  │  │  │  ├─ early_hints.php
│        │  │  │  │  ├─ invalid_cookie_name.expected
│        │  │  │  │  └─ invalid_cookie_name.php
│        │  │  │  └─ xml
│        │  │  │     └─ http-status-codes.xml
│        │  │  ├─ HeaderBagTest.php
│        │  │  ├─ HeaderUtilsTest.php
│        │  │  ├─ InputBagTest.php
│        │  │  ├─ IpUtilsTest.php
│        │  │  ├─ JsonResponseTest.php
│        │  │  ├─ ParameterBagTest.php
│        │  │  ├─ RateLimiter
│        │  │  │  ├─ AbstractRequestRateLimiterTest.php
│        │  │  │  └─ MockAbstractRequestRateLimiter.php
│        │  │  ├─ RedirectResponseTest.php
│        │  │  ├─ RequestMatcher
│        │  │  │  ├─ AttributesRequestMatcherTest.php
│        │  │  │  ├─ ExpressionRequestMatcherTest.php
│        │  │  │  ├─ HeaderRequestMatcherTest.php
│        │  │  │  ├─ HostRequestMatcherTest.php
│        │  │  │  ├─ IpsRequestMatcherTest.php
│        │  │  │  ├─ IsJsonRequestMatcherTest.php
│        │  │  │  ├─ MethodRequestMatcherTest.php
│        │  │  │  ├─ PathRequestMatcherTest.php
│        │  │  │  ├─ PortRequestMatcherTest.php
│        │  │  │  ├─ QueryParameterRequestMatcherTest.php
│        │  │  │  └─ SchemeRequestMatcherTest.php
│        │  │  ├─ RequestStackTest.php
│        │  │  ├─ RequestTest.php
│        │  │  ├─ ResponseFunctionalTest.php
│        │  │  ├─ ResponseHeaderBagTest.php
│        │  │  ├─ ResponseTest.php
│        │  │  ├─ ResponseTestCase.php
│        │  │  ├─ schema
│        │  │  │  ├─ http-status-codes.rng
│        │  │  │  └─ iana-registry.rng
│        │  │  ├─ ServerBagTest.php
│        │  │  ├─ Session
│        │  │  │  ├─ Attribute
│        │  │  │  │  └─ AttributeBagTest.php
│        │  │  │  ├─ Flash
│        │  │  │  │  ├─ AutoExpireFlashBagTest.php
│        │  │  │  │  └─ FlashBagTest.php
│        │  │  │  ├─ SessionTest.php
│        │  │  │  └─ Storage
│        │  │  │     ├─ Handler
│        │  │  │     │  ├─ AbstractRedisSessionHandlerTestCase.php
│        │  │  │     │  ├─ AbstractSessionHandlerTest.php
│        │  │  │     │  ├─ Fixtures
│        │  │  │     │  │  ├─ common.inc
│        │  │  │     │  │  ├─ empty_destroys.expected
│        │  │  │     │  │  ├─ empty_destroys.php
│        │  │  │     │  │  ├─ invalid_regenerate.expected
│        │  │  │     │  │  ├─ invalid_regenerate.php
│        │  │  │     │  │  ├─ read_only.expected
│        │  │  │     │  │  ├─ read_only.php
│        │  │  │     │  │  ├─ regenerate.expected
│        │  │  │     │  │  ├─ regenerate.php
│        │  │  │     │  │  ├─ storage.expected
│        │  │  │     │  │  ├─ storage.php
│        │  │  │     │  │  ├─ with_cookie.expected
│        │  │  │     │  │  ├─ with_cookie.php
│        │  │  │     │  │  ├─ with_cookie_and_session.expected
│        │  │  │     │  │  ├─ with_cookie_and_session.php
│        │  │  │     │  │  ├─ with_samesite.expected
│        │  │  │     │  │  ├─ with_samesite.php
│        │  │  │     │  │  ├─ with_samesite_and_migration.expected
│        │  │  │     │  │  └─ with_samesite_and_migration.php
│        │  │  │     │  ├─ IdentityMarshallerTest.php
│        │  │  │     │  ├─ MarshallingSessionHandlerTest.php
│        │  │  │     │  ├─ MemcachedSessionHandlerTest.php
│        │  │  │     │  ├─ MigratingSessionHandlerTest.php
│        │  │  │     │  ├─ MongoDbSessionHandlerTest.php
│        │  │  │     │  ├─ NativeFileSessionHandlerTest.php
│        │  │  │     │  ├─ NullSessionHandlerTest.php
│        │  │  │     │  ├─ PdoSessionHandlerTest.php
│        │  │  │     │  ├─ PredisClusterSessionHandlerTest.php
│        │  │  │     │  ├─ PredisSessionHandlerTest.php
│        │  │  │     │  ├─ RedisArraySessionHandlerTest.php
│        │  │  │     │  ├─ RedisClusterSessionHandlerTest.php
│        │  │  │     │  ├─ RedisSessionHandlerTest.php
│        │  │  │     │  ├─ RelaySessionHandlerTest.php
│        │  │  │     │  ├─ SessionHandlerFactoryTest.php
│        │  │  │     │  ├─ StrictSessionHandlerTest.php
│        │  │  │     │  └─ stubs
│        │  │  │     │     └─ mongodb.php
│        │  │  │     ├─ MetadataBagTest.php
│        │  │  │     ├─ MockArraySessionStorageTest.php
│        │  │  │     ├─ MockFileSessionStorageTest.php
│        │  │  │     ├─ NativeSessionStorageTest.php
│        │  │  │     ├─ PhpBridgeSessionStorageTest.php
│        │  │  │     └─ Proxy
│        │  │  │        ├─ AbstractProxyTest.php
│        │  │  │        └─ SessionHandlerProxyTest.php
│        │  │  ├─ StreamedJsonResponseTest.php
│        │  │  ├─ StreamedResponseTest.php
│        │  │  ├─ Test
│        │  │  │  └─ Constraint
│        │  │  │     ├─ RequestAttributeValueSameTest.php
│        │  │  │     ├─ ResponseCookieValueSameTest.php
│        │  │  │     ├─ ResponseFormatSameTest.php
│        │  │  │     ├─ ResponseHasCookieTest.php
│        │  │  │     ├─ ResponseHasHeaderTest.php
│        │  │  │     ├─ ResponseHeaderLocationSameTest.php
│        │  │  │     ├─ ResponseHeaderSameTest.php
│        │  │  │     ├─ ResponseIsRedirectedTest.php
│        │  │  │     ├─ ResponseIsSuccessfulTest.php
│        │  │  │     ├─ ResponseIsUnprocessableTest.php
│        │  │  │     └─ ResponseStatusCodeSameTest.php
│        │  │  ├─ UriSignerTest.php
│        │  │  └─ UrlHelperTest.php
│        │  ├─ UriSigner.php
│        │  └─ UrlHelper.php
│        ├─ http-kernel
│        │  ├─ Attribute
│        │  │  ├─ AsController.php
│        │  │  ├─ AsTargetedValueResolver.php
│        │  │  ├─ Cache.php
│        │  │  ├─ MapDateTime.php
│        │  │  ├─ MapQueryParameter.php
│        │  │  ├─ MapQueryString.php
│        │  │  ├─ MapRequestPayload.php
│        │  │  ├─ MapUploadedFile.php
│        │  │  ├─ ValueResolver.php
│        │  │  ├─ WithHttpStatus.php
│        │  │  └─ WithLogLevel.php
│        │  ├─ Bundle
│        │  │  ├─ AbstractBundle.php
│        │  │  ├─ Bundle.php
│        │  │  ├─ BundleExtension.php
│        │  │  └─ BundleInterface.php
│        │  ├─ CacheClearer
│        │  │  ├─ CacheClearerInterface.php
│        │  │  ├─ ChainCacheClearer.php
│        │  │  └─ Psr6CacheClearer.php
│        │  ├─ CacheWarmer
│        │  │  ├─ CacheWarmer.php
│        │  │  ├─ CacheWarmerAggregate.php
│        │  │  ├─ CacheWarmerInterface.php
│        │  │  └─ WarmableInterface.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ Config
│        │  │  └─ FileLocator.php
│        │  ├─ Controller
│        │  │  ├─ ArgumentResolver
│        │  │  │  ├─ BackedEnumValueResolver.php
│        │  │  │  ├─ DateTimeValueResolver.php
│        │  │  │  ├─ DefaultValueResolver.php
│        │  │  │  ├─ NotTaggedControllerValueResolver.php
│        │  │  │  ├─ QueryParameterValueResolver.php
│        │  │  │  ├─ RequestAttributeValueResolver.php
│        │  │  │  ├─ RequestPayloadValueResolver.php
│        │  │  │  ├─ RequestValueResolver.php
│        │  │  │  ├─ ServiceValueResolver.php
│        │  │  │  ├─ SessionValueResolver.php
│        │  │  │  ├─ TraceableValueResolver.php
│        │  │  │  ├─ UidValueResolver.php
│        │  │  │  └─ VariadicValueResolver.php
│        │  │  ├─ ArgumentResolver.php
│        │  │  ├─ ArgumentResolverInterface.php
│        │  │  ├─ ContainerControllerResolver.php
│        │  │  ├─ ControllerReference.php
│        │  │  ├─ ControllerResolver.php
│        │  │  ├─ ControllerResolverInterface.php
│        │  │  ├─ ErrorController.php
│        │  │  ├─ TraceableArgumentResolver.php
│        │  │  ├─ TraceableControllerResolver.php
│        │  │  └─ ValueResolverInterface.php
│        │  ├─ ControllerMetadata
│        │  │  ├─ ArgumentMetadata.php
│        │  │  ├─ ArgumentMetadataFactory.php
│        │  │  └─ ArgumentMetadataFactoryInterface.php
│        │  ├─ DataCollector
│        │  │  ├─ AjaxDataCollector.php
│        │  │  ├─ ConfigDataCollector.php
│        │  │  ├─ DataCollector.php
│        │  │  ├─ DataCollectorInterface.php
│        │  │  ├─ DumpDataCollector.php
│        │  │  ├─ EventDataCollector.php
│        │  │  ├─ ExceptionDataCollector.php
│        │  │  ├─ LateDataCollectorInterface.php
│        │  │  ├─ LoggerDataCollector.php
│        │  │  ├─ MemoryDataCollector.php
│        │  │  ├─ RequestDataCollector.php
│        │  │  ├─ RouterDataCollector.php
│        │  │  └─ TimeDataCollector.php
│        │  ├─ Debug
│        │  │  ├─ ErrorHandlerConfigurator.php
│        │  │  ├─ TraceableEventDispatcher.php
│        │  │  └─ VirtualRequestStack.php
│        │  ├─ DependencyInjection
│        │  │  ├─ AddAnnotatedClassesToCachePass.php
│        │  │  ├─ ConfigurableExtension.php
│        │  │  ├─ ControllerArgumentValueResolverPass.php
│        │  │  ├─ Extension.php
│        │  │  ├─ FragmentRendererPass.php
│        │  │  ├─ LazyLoadingFragmentHandler.php
│        │  │  ├─ LoggerPass.php
│        │  │  ├─ MergeExtensionConfigurationPass.php
│        │  │  ├─ RegisterControllerArgumentLocatorsPass.php
│        │  │  ├─ RegisterLocaleAwareServicesPass.php
│        │  │  ├─ RemoveEmptyControllerArgumentLocatorsPass.php
│        │  │  ├─ ResettableServicePass.php
│        │  │  ├─ ServicesResetter.php
│        │  │  └─ ServicesResetterInterface.php
│        │  ├─ Event
│        │  │  ├─ ControllerArgumentsEvent.php
│        │  │  ├─ ControllerEvent.php
│        │  │  ├─ ExceptionEvent.php
│        │  │  ├─ FinishRequestEvent.php
│        │  │  ├─ KernelEvent.php
│        │  │  ├─ RequestEvent.php
│        │  │  ├─ ResponseEvent.php
│        │  │  ├─ TerminateEvent.php
│        │  │  └─ ViewEvent.php
│        │  ├─ EventListener
│        │  │  ├─ AbstractSessionListener.php
│        │  │  ├─ AddRequestFormatsListener.php
│        │  │  ├─ CacheAttributeListener.php
│        │  │  ├─ DebugHandlersListener.php
│        │  │  ├─ DisallowRobotsIndexingListener.php
│        │  │  ├─ DumpListener.php
│        │  │  ├─ ErrorListener.php
│        │  │  ├─ FragmentListener.php
│        │  │  ├─ LocaleAwareListener.php
│        │  │  ├─ LocaleListener.php
│        │  │  ├─ ProfilerListener.php
│        │  │  ├─ ResponseListener.php
│        │  │  ├─ RouterListener.php
│        │  │  ├─ SessionListener.php
│        │  │  ├─ SurrogateListener.php
│        │  │  └─ ValidateRequestListener.php
│        │  ├─ Exception
│        │  │  ├─ AccessDeniedHttpException.php
│        │  │  ├─ BadRequestHttpException.php
│        │  │  ├─ ConflictHttpException.php
│        │  │  ├─ ControllerDoesNotReturnResponseException.php
│        │  │  ├─ GoneHttpException.php
│        │  │  ├─ HttpException.php
│        │  │  ├─ HttpExceptionInterface.php
│        │  │  ├─ InvalidMetadataException.php
│        │  │  ├─ LengthRequiredHttpException.php
│        │  │  ├─ LockedHttpException.php
│        │  │  ├─ MethodNotAllowedHttpException.php
│        │  │  ├─ NearMissValueResolverException.php
│        │  │  ├─ NotAcceptableHttpException.php
│        │  │  ├─ NotFoundHttpException.php
│        │  │  ├─ PreconditionFailedHttpException.php
│        │  │  ├─ PreconditionRequiredHttpException.php
│        │  │  ├─ ResolverNotFoundException.php
│        │  │  ├─ ServiceUnavailableHttpException.php
│        │  │  ├─ TooManyRequestsHttpException.php
│        │  │  ├─ UnauthorizedHttpException.php
│        │  │  ├─ UnexpectedSessionUsageException.php
│        │  │  ├─ UnprocessableEntityHttpException.php
│        │  │  └─ UnsupportedMediaTypeHttpException.php
│        │  ├─ Fragment
│        │  │  ├─ AbstractSurrogateFragmentRenderer.php
│        │  │  ├─ EsiFragmentRenderer.php
│        │  │  ├─ FragmentHandler.php
│        │  │  ├─ FragmentRendererInterface.php
│        │  │  ├─ FragmentUriGenerator.php
│        │  │  ├─ FragmentUriGeneratorInterface.php
│        │  │  ├─ HIncludeFragmentRenderer.php
│        │  │  ├─ InlineFragmentRenderer.php
│        │  │  ├─ RoutableFragmentRenderer.php
│        │  │  └─ SsiFragmentRenderer.php
│        │  ├─ HttpCache
│        │  │  ├─ AbstractSurrogate.php
│        │  │  ├─ Esi.php
│        │  │  ├─ HttpCache.php
│        │  │  ├─ ResponseCacheStrategy.php
│        │  │  ├─ ResponseCacheStrategyInterface.php
│        │  │  ├─ Ssi.php
│        │  │  ├─ Store.php
│        │  │  ├─ StoreInterface.php
│        │  │  ├─ SubRequestHandler.php
│        │  │  └─ SurrogateInterface.php
│        │  ├─ HttpClientKernel.php
│        │  ├─ HttpKernel.php
│        │  ├─ HttpKernelBrowser.php
│        │  ├─ HttpKernelInterface.php
│        │  ├─ Kernel.php
│        │  ├─ KernelEvents.php
│        │  ├─ KernelInterface.php
│        │  ├─ LICENSE
│        │  ├─ Log
│        │  │  ├─ DebugLoggerConfigurator.php
│        │  │  ├─ DebugLoggerInterface.php
│        │  │  └─ Logger.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ Profiler
│        │  │  ├─ FileProfilerStorage.php
│        │  │  ├─ Profile.php
│        │  │  ├─ Profiler.php
│        │  │  ├─ ProfilerStateChecker.php
│        │  │  └─ ProfilerStorageInterface.php
│        │  ├─ README.md
│        │  ├─ RebootableInterface.php
│        │  ├─ Resources
│        │  │  └─ welcome.html.php
│        │  ├─ TerminableInterface.php
│        │  └─ Tests
│        │     ├─ Attribute
│        │     │  └─ WithLogLevelTest.php
│        │     ├─ Bundle
│        │     │  └─ BundleTest.php
│        │     ├─ CacheClearer
│        │     │  ├─ ChainCacheClearerTest.php
│        │     │  └─ Psr6CacheClearerTest.php
│        │     ├─ CacheWarmer
│        │     │  ├─ CacheWarmerAggregateTest.php
│        │     │  └─ CacheWarmerTest.php
│        │     ├─ Config
│        │     │  └─ FileLocatorTest.php
│        │     ├─ Controller
│        │     │  ├─ ArgumentResolver
│        │     │  │  ├─ BackedEnumValueResolverTest.php
│        │     │  │  ├─ DateTimeValueResolverTest.php
│        │     │  │  ├─ NotTaggedControllerValueResolverTest.php
│        │     │  │  ├─ QueryParameterValueResolverTest.php
│        │     │  │  ├─ RequestPayloadValueResolverTest.php
│        │     │  │  ├─ RequestValueResolverTest.php
│        │     │  │  ├─ ServiceValueResolverTest.php
│        │     │  │  ├─ TraceableValueResolverTest.php
│        │     │  │  ├─ UidValueResolverTest.php
│        │     │  │  └─ UploadedFileValueResolverTest.php
│        │     │  ├─ ArgumentResolverTest.php
│        │     │  ├─ ContainerControllerResolverTest.php
│        │     │  ├─ ControllerResolverTest.php
│        │     │  ├─ ErrorControllerTest.php
│        │     │  ├─ TraceableArgumentResolverTest.php
│        │     │  └─ TraceableControllerResolverTest.php
│        │     ├─ ControllerMetadata
│        │     │  ├─ ArgumentMetadataFactoryTest.php
│        │     │  └─ ArgumentMetadataTest.php
│        │     ├─ DataCollector
│        │     │  ├─ Compiler.log
│        │     │  ├─ ConfigDataCollectorTest.php
│        │     │  ├─ DataCollectorTest.php
│        │     │  ├─ DumpDataCollectorTest.php
│        │     │  ├─ ExceptionDataCollectorTest.php
│        │     │  ├─ LoggerDataCollectorTest.php
│        │     │  ├─ MemoryDataCollectorTest.php
│        │     │  ├─ RequestDataCollectorTest.php
│        │     │  ├─ RouterDataCollectorTest.php
│        │     │  └─ TimeDataCollectorTest.php
│        │     ├─ Debug
│        │     │  ├─ ErrorHandlerConfiguratorTest.php
│        │     │  └─ TraceableEventDispatcherTest.php
│        │     ├─ DependencyInjection
│        │     │  ├─ AddAnnotatedClassesToCachePassTest.php
│        │     │  ├─ ControllerArgumentValueResolverPassTest.php
│        │     │  ├─ FragmentRendererPassTest.php
│        │     │  ├─ LazyLoadingFragmentHandlerTest.php
│        │     │  ├─ LoggerPassTest.php
│        │     │  ├─ MergeExtensionConfigurationPassTest.php
│        │     │  ├─ RegisterControllerArgumentLocatorsPassTest.php
│        │     │  ├─ RegisterLocaleAwareServicesPassTest.php
│        │     │  ├─ RemoveEmptyControllerArgumentLocatorsPassTest.php
│        │     │  ├─ ResettableServicePassTest.php
│        │     │  └─ ServicesResetterTest.php
│        │     ├─ Event
│        │     │  ├─ ControllerArgumentsEventTest.php
│        │     │  ├─ ControllerEventTest.php
│        │     │  └─ ExceptionEventTest.php
│        │     ├─ EventListener
│        │     │  ├─ AddRequestFormatsListenerTest.php
│        │     │  ├─ CacheAttributeListenerTest.php
│        │     │  ├─ DebugHandlersListenerTest.php
│        │     │  ├─ DisallowRobotsIndexingListenerTest.php
│        │     │  ├─ DumpListenerTest.php
│        │     │  ├─ ErrorListenerTest.php
│        │     │  ├─ FragmentListenerTest.php
│        │     │  ├─ LocaleAwareListenerTest.php
│        │     │  ├─ LocaleListenerTest.php
│        │     │  ├─ ProfilerListenerTest.php
│        │     │  ├─ ResponseListenerTest.php
│        │     │  ├─ RouterListenerTest.php
│        │     │  ├─ SessionListenerTest.php
│        │     │  ├─ SurrogateListenerTest.php
│        │     │  └─ ValidateRequestListenerTest.php
│        │     ├─ Exception
│        │     │  ├─ AccessDeniedHttpExceptionTest.php
│        │     │  ├─ BadRequestHttpExceptionTest.php
│        │     │  ├─ ConflictHttpExceptionTest.php
│        │     │  ├─ GoneHttpExceptionTest.php
│        │     │  ├─ HttpExceptionTest.php
│        │     │  ├─ LengthRequiredHttpExceptionTest.php
│        │     │  ├─ LockedHttpExceptionTest.php
│        │     │  ├─ MethodNotAllowedHttpExceptionTest.php
│        │     │  ├─ NotAcceptableHttpExceptionTest.php
│        │     │  ├─ NotFoundHttpExceptionTest.php
│        │     │  ├─ PreconditionFailedHttpExceptionTest.php
│        │     │  ├─ PreconditionRequiredHttpExceptionTest.php
│        │     │  ├─ ServiceUnavailableHttpExceptionTest.php
│        │     │  ├─ TooManyRequestsHttpExceptionTest.php
│        │     │  ├─ UnauthorizedHttpExceptionTest.php
│        │     │  ├─ UnprocessableEntityHttpExceptionTest.php
│        │     │  └─ UnsupportedMediaTypeHttpExceptionTest.php
│        │     ├─ Fixtures
│        │     │  ├─ AcmeFooBundle
│        │     │  │  ├─ AcmeFooBundle.php
│        │     │  │  └─ Resources
│        │     │  │     └─ config
│        │     │  │        ├─ definition.php
│        │     │  │        └─ services.php
│        │     │  ├─ Attribute
│        │     │  │  ├─ Bar.php
│        │     │  │  ├─ Baz.php
│        │     │  │  └─ Foo.php
│        │     │  ├─ Bundle1Bundle
│        │     │  │  ├─ foo.txt
│        │     │  │  └─ Resources
│        │     │  ├─ ClearableService.php
│        │     │  ├─ Controller
│        │     │  │  ├─ ArgumentResolver
│        │     │  │  │  └─ UploadedFile
│        │     │  │  │     ├─ file-big.txt
│        │     │  │  │     └─ file-small.txt
│        │     │  │  ├─ AttributeController.php
│        │     │  │  ├─ BasicTypesController.php
│        │     │  │  ├─ CacheAttributeController.php
│        │     │  │  ├─ ExtendingRequest.php
│        │     │  │  ├─ ExtendingSession.php
│        │     │  │  ├─ NullableController.php
│        │     │  │  └─ VariadicController.php
│        │     │  ├─ DataCollector
│        │     │  │  ├─ CloneVarDataCollector.php
│        │     │  │  └─ DummyController.php
│        │     │  ├─ ExtensionNotValidBundle
│        │     │  │  ├─ DependencyInjection
│        │     │  │  │  └─ ExtensionNotValidExtension.php
│        │     │  │  └─ ExtensionNotValidBundle.php
│        │     │  ├─ ExtensionPresentBundle
│        │     │  │  ├─ DependencyInjection
│        │     │  │  │  └─ ExtensionPresentExtension.php
│        │     │  │  └─ ExtensionPresentBundle.php
│        │     │  ├─ IntEnum.php
│        │     │  ├─ KernelWithoutBundles.php
│        │     │  ├─ LazyResettableService.php
│        │     │  ├─ MockableUploadFileWithClientSize.php
│        │     │  ├─ MultiResettableService.php
│        │     │  ├─ ResettableService.php
│        │     │  ├─ Suit.php
│        │     │  ├─ TestClient.php
│        │     │  ├─ UsePropertyInDestruct.php
│        │     │  └─ WithPublicObjectProperty.php
│        │     ├─ Fragment
│        │     │  ├─ EsiFragmentRendererTest.php
│        │     │  ├─ FragmentHandlerTest.php
│        │     │  ├─ HIncludeFragmentRendererTest.php
│        │     │  ├─ InlineFragmentRendererTest.php
│        │     │  ├─ RoutableFragmentRendererTest.php
│        │     │  └─ SsiFragmentRendererTest.php
│        │     ├─ HttpCache
│        │     │  ├─ EsiTest.php
│        │     │  ├─ HttpCacheTest.php
│        │     │  ├─ HttpCacheTestCase.php
│        │     │  ├─ ResponseCacheStrategyTest.php
│        │     │  ├─ SsiTest.php
│        │     │  ├─ StoreTest.php
│        │     │  ├─ SubRequestHandlerTest.php
│        │     │  ├─ TestHttpKernel.php
│        │     │  └─ TestMultipleHttpKernel.php
│        │     ├─ HttpClientKernelTest.php
│        │     ├─ HttpKernelBrowserTest.php
│        │     ├─ HttpKernelTest.php
│        │     ├─ KernelTest.php
│        │     ├─ Log
│        │     │  └─ LoggerTest.php
│        │     ├─ Logger.php
│        │     ├─ Profiler
│        │     │  ├─ FileProfilerStorageTest.php
│        │     │  └─ ProfilerTest.php
│        │     └─ TestHttpKernel.php
│        ├─ polyfill-intl-grapheme
│        │  ├─ bootstrap.php
│        │  ├─ bootstrap80.php
│        │  ├─ composer.json
│        │  ├─ Grapheme.php
│        │  ├─ LICENSE
│        │  └─ README.md
│        ├─ polyfill-intl-normalizer
│        │  ├─ bootstrap.php
│        │  ├─ bootstrap80.php
│        │  ├─ composer.json
│        │  ├─ LICENSE
│        │  ├─ Normalizer.php
│        │  ├─ README.md
│        │  └─ Resources
│        │     ├─ stubs
│        │     │  └─ Normalizer.php
│        │     └─ unidata
│        │        ├─ canonicalComposition.php
│        │        ├─ canonicalDecomposition.php
│        │        ├─ combiningClass.php
│        │        └─ compatibilityDecomposition.php
│        ├─ polyfill-mbstring
│        │  ├─ bootstrap.php
│        │  ├─ bootstrap80.php
│        │  ├─ composer.json
│        │  ├─ LICENSE
│        │  ├─ Mbstring.php
│        │  ├─ README.md
│        │  └─ Resources
│        │     └─ unidata
│        │        ├─ caseFolding.php
│        │        ├─ lowerCase.php
│        │        ├─ titleCaseRegexp.php
│        │        └─ upperCase.php
│        ├─ polyfill-php83
│        │  ├─ bootstrap.php
│        │  ├─ bootstrap81.php
│        │  ├─ composer.json
│        │  ├─ LICENSE
│        │  ├─ Php83.php
│        │  ├─ README.md
│        │  └─ Resources
│        │     └─ stubs
│        │        ├─ DateError.php
│        │        ├─ DateException.php
│        │        ├─ DateInvalidOperationException.php
│        │        ├─ DateInvalidTimeZoneException.php
│        │        ├─ DateMalformedIntervalStringException.php
│        │        ├─ DateMalformedPeriodStringException.php
│        │        ├─ DateMalformedStringException.php
│        │        ├─ DateObjectError.php
│        │        ├─ DateRangeError.php
│        │        ├─ Override.php
│        │        └─ SQLite3Exception.php
│        ├─ routing
│        │  ├─ Alias.php
│        │  ├─ Annotation
│        │  │  └─ Route.php
│        │  ├─ Attribute
│        │  │  ├─ DeprecatedAlias.php
│        │  │  └─ Route.php
│        │  ├─ CHANGELOG.md
│        │  ├─ CompiledRoute.php
│        │  ├─ composer.json
│        │  ├─ DependencyInjection
│        │  │  ├─ AddExpressionLanguageProvidersPass.php
│        │  │  └─ RoutingResolverPass.php
│        │  ├─ Exception
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ InvalidArgumentException.php
│        │  │  ├─ InvalidParameterException.php
│        │  │  ├─ LogicException.php
│        │  │  ├─ MethodNotAllowedException.php
│        │  │  ├─ MissingMandatoryParametersException.php
│        │  │  ├─ NoConfigurationException.php
│        │  │  ├─ ResourceNotFoundException.php
│        │  │  ├─ RouteCircularReferenceException.php
│        │  │  ├─ RouteNotFoundException.php
│        │  │  └─ RuntimeException.php
│        │  ├─ Generator
│        │  │  ├─ CompiledUrlGenerator.php
│        │  │  ├─ ConfigurableRequirementsInterface.php
│        │  │  ├─ Dumper
│        │  │  │  ├─ CompiledUrlGeneratorDumper.php
│        │  │  │  ├─ GeneratorDumper.php
│        │  │  │  └─ GeneratorDumperInterface.php
│        │  │  ├─ UrlGenerator.php
│        │  │  └─ UrlGeneratorInterface.php
│        │  ├─ LICENSE
│        │  ├─ Loader
│        │  │  ├─ AttributeClassLoader.php
│        │  │  ├─ AttributeDirectoryLoader.php
│        │  │  ├─ AttributeFileLoader.php
│        │  │  ├─ ClosureLoader.php
│        │  │  ├─ Configurator
│        │  │  │  ├─ AliasConfigurator.php
│        │  │  │  ├─ CollectionConfigurator.php
│        │  │  │  ├─ ImportConfigurator.php
│        │  │  │  ├─ RouteConfigurator.php
│        │  │  │  ├─ RoutingConfigurator.php
│        │  │  │  └─ Traits
│        │  │  │     ├─ AddTrait.php
│        │  │  │     ├─ HostTrait.php
│        │  │  │     ├─ LocalizedRouteTrait.php
│        │  │  │     ├─ PrefixTrait.php
│        │  │  │     └─ RouteTrait.php
│        │  │  ├─ ContainerLoader.php
│        │  │  ├─ DirectoryLoader.php
│        │  │  ├─ GlobFileLoader.php
│        │  │  ├─ ObjectLoader.php
│        │  │  ├─ PhpFileLoader.php
│        │  │  ├─ Psr4DirectoryLoader.php
│        │  │  ├─ schema
│        │  │  │  └─ routing
│        │  │  │     └─ routing-1.0.xsd
│        │  │  ├─ XmlFileLoader.php
│        │  │  └─ YamlFileLoader.php
│        │  ├─ Matcher
│        │  │  ├─ CompiledUrlMatcher.php
│        │  │  ├─ Dumper
│        │  │  │  ├─ CompiledUrlMatcherDumper.php
│        │  │  │  ├─ CompiledUrlMatcherTrait.php
│        │  │  │  ├─ MatcherDumper.php
│        │  │  │  ├─ MatcherDumperInterface.php
│        │  │  │  └─ StaticPrefixCollection.php
│        │  │  ├─ ExpressionLanguageProvider.php
│        │  │  ├─ RedirectableUrlMatcher.php
│        │  │  ├─ RedirectableUrlMatcherInterface.php
│        │  │  ├─ RequestMatcherInterface.php
│        │  │  ├─ TraceableUrlMatcher.php
│        │  │  ├─ UrlMatcher.php
│        │  │  └─ UrlMatcherInterface.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ RequestContext.php
│        │  ├─ RequestContextAwareInterface.php
│        │  ├─ Requirement
│        │  │  ├─ EnumRequirement.php
│        │  │  └─ Requirement.php
│        │  ├─ Route.php
│        │  ├─ RouteCollection.php
│        │  ├─ RouteCompiler.php
│        │  ├─ RouteCompilerInterface.php
│        │  ├─ Router.php
│        │  ├─ RouterInterface.php
│        │  └─ Tests
│        │     ├─ Attribute
│        │     │  └─ RouteTest.php
│        │     ├─ CompiledRouteTest.php
│        │     ├─ DependencyInjection
│        │     │  ├─ AddExpressionLanguageProvidersPassTest.php
│        │     │  └─ RoutingResolverPassTest.php
│        │     ├─ Fixtures
│        │     │  ├─ alias
│        │     │  │  ├─ alias.php
│        │     │  │  ├─ alias.xml
│        │     │  │  ├─ alias.yaml
│        │     │  │  ├─ expected.php
│        │     │  │  ├─ invalid-alias.yaml
│        │     │  │  ├─ invalid-deprecated-no-package.xml
│        │     │  │  ├─ invalid-deprecated-no-package.yaml
│        │     │  │  ├─ invalid-deprecated-no-version.xml
│        │     │  │  ├─ invalid-deprecated-no-version.yaml
│        │     │  │  └─ override.yaml
│        │     │  ├─ annotated.php
│        │     │  ├─ AttributedClasses
│        │     │  │  ├─ AbstractClass.php
│        │     │  │  ├─ BarClass.php
│        │     │  │  ├─ BazClass.php
│        │     │  │  ├─ EncodingClass.php
│        │     │  │  ├─ FooClass.php
│        │     │  │  └─ FooTrait.php
│        │     │  ├─ AttributeFixtures
│        │     │  │  ├─ AbstractClassController.php
│        │     │  │  ├─ ActionPathController.php
│        │     │  │  ├─ AliasClassController.php
│        │     │  │  ├─ AliasInvokableController.php
│        │     │  │  ├─ AliasRouteController.php
│        │     │  │  ├─ BazClass.php
│        │     │  │  ├─ DefaultValueController.php
│        │     │  │  ├─ DeprecatedAliasCustomMessageRouteController.php
│        │     │  │  ├─ DeprecatedAliasRouteController.php
│        │     │  │  ├─ EncodingClass.php
│        │     │  │  ├─ ExplicitLocalizedActionPathController.php
│        │     │  │  ├─ ExtendedRoute.php
│        │     │  │  ├─ ExtendedRouteOnClassController.php
│        │     │  │  ├─ ExtendedRouteOnMethodController.php
│        │     │  │  ├─ FooController.php
│        │     │  │  ├─ GlobalDefaultsClass.php
│        │     │  │  ├─ InvokableController.php
│        │     │  │  ├─ InvokableFQCNAliasConflictController.php
│        │     │  │  ├─ InvokableLocalizedController.php
│        │     │  │  ├─ InvokableMethodController.php
│        │     │  │  ├─ LocalizedActionPathController.php
│        │     │  │  ├─ LocalizedMethodActionControllers.php
│        │     │  │  ├─ LocalizedPrefixLocalizedActionController.php
│        │     │  │  ├─ LocalizedPrefixMissingLocaleActionController.php
│        │     │  │  ├─ LocalizedPrefixMissingRouteLocaleActionController.php
│        │     │  │  ├─ LocalizedPrefixWithRouteWithoutLocale.php
│        │     │  │  ├─ MethodActionControllers.php
│        │     │  │  ├─ MethodsAndSchemes.php
│        │     │  │  ├─ MissingRouteNameController.php
│        │     │  │  ├─ MultipleDeprecatedAliasRouteController.php
│        │     │  │  ├─ NothingButNameController.php
│        │     │  │  ├─ PrefixedActionLocalizedRouteController.php
│        │     │  │  ├─ PrefixedActionPathController.php
│        │     │  │  ├─ RequirementsWithoutPlaceholderNameController.php
│        │     │  │  ├─ RouteWithEnv.php
│        │     │  │  ├─ RouteWithPrefixController.php
│        │     │  │  ├─ RouteWithPriorityController.php
│        │     │  │  └─ Utf8ActionControllers.php
│        │     │  ├─ Attributes
│        │     │  │  └─ FooAttributes.php
│        │     │  ├─ AttributesFixtures
│        │     │  │  ├─ AttributesClassParamAfterCommaController.php
│        │     │  │  ├─ AttributesClassParamAfterParenthesisController.php
│        │     │  │  ├─ AttributesClassParamInlineAfterCommaController.php
│        │     │  │  ├─ AttributesClassParamInlineAfterParenthesisController.php
│        │     │  │  ├─ AttributesClassParamInlineQuotedAfterCommaController.php
│        │     │  │  ├─ AttributesClassParamInlineQuotedAfterParenthesisController.php
│        │     │  │  ├─ AttributesClassParamQuotedAfterCommaController.php
│        │     │  │  └─ AttributesClassParamQuotedAfterParenthesisController.php
│        │     │  ├─ bad_format.yml
│        │     │  ├─ bar.xml
│        │     │  ├─ class-attributes.php
│        │     │  ├─ class-attributes.xml
│        │     │  ├─ class-attributes.yaml
│        │     │  ├─ collection-defaults.php
│        │     │  ├─ controller
│        │     │  │  ├─ empty_wildcard
│        │     │  │  ├─ import_controller.xml
│        │     │  │  ├─ import_controller.yml
│        │     │  │  ├─ import_override_defaults.xml
│        │     │  │  ├─ import_override_defaults.yml
│        │     │  │  ├─ import__controller.xml
│        │     │  │  ├─ import__controller.yml
│        │     │  │  ├─ override_defaults.xml
│        │     │  │  ├─ override_defaults.yml
│        │     │  │  ├─ routing.xml
│        │     │  │  └─ routing.yml
│        │     │  ├─ CustomCompiledRoute.php
│        │     │  ├─ CustomRouteCompiler.php
│        │     │  ├─ CustomXmlFileLoader.php
│        │     │  ├─ defaults.php
│        │     │  ├─ defaults.xml
│        │     │  ├─ defaults.yml
│        │     │  ├─ directory
│        │     │  │  ├─ recurse
│        │     │  │  │  ├─ routes1.yml
│        │     │  │  │  └─ routes2.yml
│        │     │  │  └─ routes3.yml
│        │     │  ├─ directory_import
│        │     │  │  └─ import.yml
│        │     │  ├─ dumper
│        │     │  │  ├─ compiled_url_matcher0.php
│        │     │  │  ├─ compiled_url_matcher1.php
│        │     │  │  ├─ compiled_url_matcher10.php
│        │     │  │  ├─ compiled_url_matcher11.php
│        │     │  │  ├─ compiled_url_matcher12.php
│        │     │  │  ├─ compiled_url_matcher13.php
│        │     │  │  ├─ compiled_url_matcher14.php
│        │     │  │  ├─ compiled_url_matcher2.php
│        │     │  │  ├─ compiled_url_matcher3.php
│        │     │  │  ├─ compiled_url_matcher4.php
│        │     │  │  ├─ compiled_url_matcher5.php
│        │     │  │  ├─ compiled_url_matcher6.php
│        │     │  │  ├─ compiled_url_matcher7.php
│        │     │  │  ├─ compiled_url_matcher8.php
│        │     │  │  └─ compiled_url_matcher9.php
│        │     │  ├─ empty.yml
│        │     │  ├─ Enum
│        │     │  │  ├─ TestIntBackedEnum.php
│        │     │  │  ├─ TestStringBackedEnum.php
│        │     │  │  ├─ TestStringBackedEnum2.php
│        │     │  │  └─ TestUnitEnum.php
│        │     │  ├─ file_resource.yml
│        │     │  ├─ foo.xml
│        │     │  ├─ foo1.xml
│        │     │  ├─ glob
│        │     │  │  ├─ bar.xml
│        │     │  │  ├─ bar.yml
│        │     │  │  ├─ baz.xml
│        │     │  │  ├─ baz.yml
│        │     │  │  ├─ import_multiple.xml
│        │     │  │  ├─ import_multiple.yml
│        │     │  │  ├─ import_single.xml
│        │     │  │  ├─ import_single.yml
│        │     │  │  ├─ php_dsl.php
│        │     │  │  ├─ php_dsl_bar.php
│        │     │  │  └─ php_dsl_baz.php
│        │     │  ├─ imported-with-defaults.php
│        │     │  ├─ imported-with-defaults.xml
│        │     │  ├─ imported-with-defaults.yml
│        │     │  ├─ importer-with-defaults.php
│        │     │  ├─ importer-with-defaults.xml
│        │     │  ├─ importer-with-defaults.yml
│        │     │  ├─ import_with_name_prefix
│        │     │  │  ├─ routing.xml
│        │     │  │  └─ routing.yml
│        │     │  ├─ import_with_no_trailing_slash
│        │     │  │  ├─ routing.xml
│        │     │  │  └─ routing.yml
│        │     │  ├─ incomplete.yml
│        │     │  ├─ list_defaults.xml
│        │     │  ├─ list_in_list_defaults.xml
│        │     │  ├─ list_in_map_defaults.xml
│        │     │  ├─ list_null_values.xml
│        │     │  ├─ locale_and_host
│        │     │  │  ├─ import-with-host-expected-collection.php
│        │     │  │  ├─ import-with-locale-and-host-expected-collection.php
│        │     │  │  ├─ import-with-single-host-expected-collection.php
│        │     │  │  ├─ import-without-host-expected-collection.php
│        │     │  │  ├─ imported.php
│        │     │  │  ├─ imported.xml
│        │     │  │  ├─ imported.yml
│        │     │  │  ├─ importer-with-host.php
│        │     │  │  ├─ importer-with-host.xml
│        │     │  │  ├─ importer-with-host.yml
│        │     │  │  ├─ importer-with-locale-and-host.php
│        │     │  │  ├─ importer-with-locale-and-host.xml
│        │     │  │  ├─ importer-with-locale-and-host.yml
│        │     │  │  ├─ importer-with-single-host.php
│        │     │  │  ├─ importer-with-single-host.xml
│        │     │  │  ├─ importer-with-single-host.yml
│        │     │  │  ├─ importer-without-host.php
│        │     │  │  ├─ importer-without-host.xml
│        │     │  │  ├─ importer-without-host.yml
│        │     │  │  ├─ priorized-host.yml
│        │     │  │  ├─ route-with-hosts-expected-collection.php
│        │     │  │  ├─ route-with-hosts.php
│        │     │  │  ├─ route-with-hosts.xml
│        │     │  │  └─ route-with-hosts.yml
│        │     │  ├─ localized
│        │     │  │  ├─ imported-with-locale-but-not-localized.xml
│        │     │  │  ├─ imported-with-locale-but-not-localized.yml
│        │     │  │  ├─ imported-with-locale.xml
│        │     │  │  ├─ imported-with-locale.yml
│        │     │  │  ├─ imported-with-utf8.php
│        │     │  │  ├─ imported-with-utf8.xml
│        │     │  │  ├─ imported-with-utf8.yml
│        │     │  │  ├─ importer-with-controller-default.yml
│        │     │  │  ├─ importer-with-locale-imports-non-localized-route.xml
│        │     │  │  ├─ importer-with-locale-imports-non-localized-route.yml
│        │     │  │  ├─ importer-with-locale.xml
│        │     │  │  ├─ importer-with-locale.yml
│        │     │  │  ├─ importer-with-utf8.php
│        │     │  │  ├─ importer-with-utf8.xml
│        │     │  │  ├─ importer-with-utf8.yml
│        │     │  │  ├─ importing-localized-route.yml
│        │     │  │  ├─ localized-prefix.yml
│        │     │  │  ├─ localized-route.yml
│        │     │  │  ├─ missing-locale-in-importer.yml
│        │     │  │  ├─ not-localized.yml
│        │     │  │  ├─ officially_formatted_locales.yml
│        │     │  │  ├─ route-without-path-or-locales.yml
│        │     │  │  ├─ utf8.php
│        │     │  │  ├─ utf8.xml
│        │     │  │  └─ utf8.yml
│        │     │  ├─ localized.xml
│        │     │  ├─ map_defaults.xml
│        │     │  ├─ map_in_list_defaults.xml
│        │     │  ├─ map_in_map_defaults.xml
│        │     │  ├─ map_null_values.xml
│        │     │  ├─ missing_id.xml
│        │     │  ├─ missing_path.xml
│        │     │  ├─ namespaceprefix.xml
│        │     │  ├─ nonesense_resource_plus_path.yml
│        │     │  ├─ nonesense_type_without_resource.yml
│        │     │  ├─ nonvalid-deprecated-route.xml
│        │     │  ├─ nonvalid.xml
│        │     │  ├─ nonvalid.yml
│        │     │  ├─ nonvalid2.yml
│        │     │  ├─ nonvalidkeys.yml
│        │     │  ├─ nonvalidnode.xml
│        │     │  ├─ nonvalidroute.xml
│        │     │  ├─ null_values.xml
│        │     │  ├─ OtherAnnotatedClasses
│        │     │  │  ├─ NoStartTagClass.php
│        │     │  │  └─ VariadicClass.php
│        │     │  ├─ php_dsl.php
│        │     │  ├─ php_dsl_i18n.php
│        │     │  ├─ php_dsl_sub.php
│        │     │  ├─ php_dsl_sub_i18n.php
│        │     │  ├─ php_dsl_sub_root.php
│        │     │  ├─ php_object_dsl.php
│        │     │  ├─ psr4-attributes.php
│        │     │  ├─ psr4-attributes.xml
│        │     │  ├─ psr4-attributes.yaml
│        │     │  ├─ psr4-controllers-redirection
│        │     │  │  ├─ psr4-attributes.php
│        │     │  │  ├─ psr4-attributes.xml
│        │     │  │  └─ psr4-attributes.yaml
│        │     │  ├─ psr4-controllers-redirection.php
│        │     │  ├─ psr4-controllers-redirection.xml
│        │     │  ├─ psr4-controllers-redirection.yaml
│        │     │  ├─ Psr4Controllers
│        │     │  │  ├─ MyController.php
│        │     │  │  ├─ MyUnannotatedController.php
│        │     │  │  └─ SubNamespace
│        │     │  │     ├─ EvenDeeperNamespace
│        │     │  │     │  └─ MyOtherController.php
│        │     │  │     ├─ IrrelevantClass.php
│        │     │  │     ├─ IrrelevantEnum.php
│        │     │  │     ├─ IrrelevantInterface.php
│        │     │  │     ├─ MyAbstractController.php
│        │     │  │     ├─ MyChildController.php
│        │     │  │     ├─ MyControllerWithATrait.php
│        │     │  │     └─ SomeSharedImplementation.php
│        │     │  ├─ RedirectableUrlMatcher.php
│        │     │  ├─ requirements_without_placeholder_name.yml
│        │     │  ├─ scalar_defaults.xml
│        │     │  ├─ special_route_name.yml
│        │     │  ├─ TraceableAttributeClassLoader.php
│        │     │  ├─ validpattern.php
│        │     │  ├─ validpattern.xml
│        │     │  ├─ validpattern.yml
│        │     │  ├─ validresource.php
│        │     │  ├─ validresource.xml
│        │     │  ├─ validresource.yml
│        │     │  ├─ when-env.xml
│        │     │  ├─ when-env.yml
│        │     │  ├─ withdoctype.xml
│        │     │  └─ with_define_path_variable.php
│        │     ├─ Generator
│        │     │  ├─ Dumper
│        │     │  │  └─ CompiledUrlGeneratorDumperTest.php
│        │     │  └─ UrlGeneratorTest.php
│        │     ├─ Loader
│        │     │  ├─ AttributeClassLoaderTest.php
│        │     │  ├─ AttributeDirectoryLoaderTest.php
│        │     │  ├─ AttributeFileLoaderTest.php
│        │     │  ├─ ClosureLoaderTest.php
│        │     │  ├─ ContainerLoaderTest.php
│        │     │  ├─ DirectoryLoaderTest.php
│        │     │  ├─ FileLocatorStub.php
│        │     │  ├─ GlobFileLoaderTest.php
│        │     │  ├─ ObjectLoaderTest.php
│        │     │  ├─ PhpFileLoaderTest.php
│        │     │  ├─ Psr4DirectoryLoaderTest.php
│        │     │  ├─ XmlFileLoaderTest.php
│        │     │  └─ YamlFileLoaderTest.php
│        │     ├─ Matcher
│        │     │  ├─ CompiledRedirectableUrlMatcherTest.php
│        │     │  ├─ CompiledUrlMatcherTest.php
│        │     │  ├─ Dumper
│        │     │  │  ├─ CompiledUrlMatcherDumperTest.php
│        │     │  │  └─ StaticPrefixCollectionTest.php
│        │     │  ├─ ExpressionLanguageProviderTest.php
│        │     │  ├─ RedirectableUrlMatcherTest.php
│        │     │  ├─ TraceableUrlMatcherTest.php
│        │     │  └─ UrlMatcherTest.php
│        │     ├─ RequestContextTest.php
│        │     ├─ Requirement
│        │     │  ├─ EnumRequirementTest.php
│        │     │  └─ RequirementTest.php
│        │     ├─ RouteCollectionTest.php
│        │     ├─ RouteCompilerTest.php
│        │     ├─ RouterTest.php
│        │     └─ RouteTest.php
│        ├─ runtime
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ GenericRuntime.php
│        │  ├─ Internal
│        │  │  ├─ autoload_runtime.template
│        │  │  ├─ BasicErrorHandler.php
│        │  │  ├─ ComposerPlugin.php
│        │  │  ├─ Console
│        │  │  │  ├─ ApplicationRuntime.php
│        │  │  │  ├─ Command
│        │  │  │  │  └─ CommandRuntime.php
│        │  │  │  ├─ Input
│        │  │  │  │  └─ InputInterfaceRuntime.php
│        │  │  │  └─ Output
│        │  │  │     └─ OutputInterfaceRuntime.php
│        │  │  ├─ HttpFoundation
│        │  │  │  ├─ RequestRuntime.php
│        │  │  │  └─ ResponseRuntime.php
│        │  │  ├─ HttpKernel
│        │  │  │  └─ HttpKernelInterfaceRuntime.php
│        │  │  ├─ MissingDotenv.php
│        │  │  └─ SymfonyErrorHandler.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Resolver
│        │  │  ├─ ClosureResolver.php
│        │  │  └─ DebugClosureResolver.php
│        │  ├─ ResolverInterface.php
│        │  ├─ Runner
│        │  │  ├─ ClosureRunner.php
│        │  │  └─ Symfony
│        │  │     ├─ ConsoleApplicationRunner.php
│        │  │     ├─ HttpKernelRunner.php
│        │  │     └─ ResponseRunner.php
│        │  ├─ RunnerInterface.php
│        │  ├─ RuntimeInterface.php
│        │  ├─ SymfonyRuntime.php
│        │  └─ Tests
│        │     └─ phpt
│        │        ├─ .env
│        │        ├─ .env.extra
│        │        ├─ application.php
│        │        ├─ application.phpt
│        │        ├─ autoload.php
│        │        ├─ command.php
│        │        ├─ command.phpt
│        │        ├─ command2.php
│        │        ├─ command2.phpt
│        │        ├─ command_list.php
│        │        ├─ command_list.phpt
│        │        ├─ dotenv_extra_load.php
│        │        ├─ dotenv_extra_load.phpt
│        │        ├─ dotenv_extra_overload.php
│        │        ├─ dotenv_extra_overload.phpt
│        │        ├─ dotenv_overload.php
│        │        ├─ dotenv_overload.phpt
│        │        ├─ dotenv_overload_command_debug_exists_0_to_1.php
│        │        ├─ dotenv_overload_command_debug_exists_0_to_1.phpt
│        │        ├─ dotenv_overload_command_debug_exists_1_to_0.php
│        │        ├─ dotenv_overload_command_debug_exists_1_to_0.phpt
│        │        ├─ dotenv_overload_command_env_conflict.php
│        │        ├─ dotenv_overload_command_env_conflict.phpt
│        │        ├─ dotenv_overload_command_env_exists.php
│        │        ├─ dotenv_overload_command_env_exists.phpt
│        │        ├─ dotenv_overload_command_no_debug.php
│        │        ├─ dotenv_overload_command_no_debug.phpt
│        │        ├─ generic-request.php
│        │        ├─ generic-request.phpt
│        │        ├─ hello.php
│        │        ├─ hello.phpt
│        │        ├─ kernel-loop.php
│        │        ├─ kernel-loop.phpt
│        │        ├─ kernel.php
│        │        ├─ kernel.phpt
│        │        ├─ kernel_register_argc_argv.phpt
│        │        ├─ request.php
│        │        ├─ request.phpt
│        │        ├─ runtime-options.php
│        │        └─ runtime-options.phpt
│        ├─ service-contracts
│        │  ├─ Attribute
│        │  │  ├─ Required.php
│        │  │  └─ SubscribedService.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ LICENSE
│        │  ├─ README.md
│        │  ├─ ResetInterface.php
│        │  ├─ ServiceCollectionInterface.php
│        │  ├─ ServiceLocatorTrait.php
│        │  ├─ ServiceMethodsSubscriberTrait.php
│        │  ├─ ServiceProviderInterface.php
│        │  ├─ ServiceSubscriberInterface.php
│        │  ├─ ServiceSubscriberTrait.php
│        │  └─ Test
│        │     ├─ ServiceLocatorTest.php
│        │     └─ ServiceLocatorTestCase.php
│        ├─ string
│        │  ├─ AbstractString.php
│        │  ├─ AbstractUnicodeString.php
│        │  ├─ ByteString.php
│        │  ├─ CHANGELOG.md
│        │  ├─ CodePointString.php
│        │  ├─ composer.json
│        │  ├─ Exception
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ InvalidArgumentException.php
│        │  │  └─ RuntimeException.php
│        │  ├─ Inflector
│        │  │  ├─ EnglishInflector.php
│        │  │  ├─ FrenchInflector.php
│        │  │  ├─ InflectorInterface.php
│        │  │  └─ SpanishInflector.php
│        │  ├─ LazyString.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Resources
│        │  │  ├─ bin
│        │  │  │  └─ update-data.php
│        │  │  ├─ data
│        │  │  │  ├─ wcswidth_table_wide.php
│        │  │  │  └─ wcswidth_table_zero.php
│        │  │  ├─ functions.php
│        │  │  └─ WcswidthDataGenerator.php
│        │  ├─ Slugger
│        │  │  ├─ AsciiSlugger.php
│        │  │  └─ SluggerInterface.php
│        │  ├─ Tests
│        │  │  ├─ AbstractAsciiTestCase.php
│        │  │  ├─ AbstractUnicodeTestCase.php
│        │  │  ├─ ByteStringTest.php
│        │  │  ├─ CodePointStringTest.php
│        │  │  ├─ FunctionsTest.php
│        │  │  ├─ Inflector
│        │  │  │  ├─ EnglishInflectorTest.php
│        │  │  │  ├─ FrenchInflectorTest.php
│        │  │  │  └─ SpanishInflectorTest.php
│        │  │  ├─ LazyStringTest.php
│        │  │  ├─ Slugger
│        │  │  │  └─ AsciiSluggerTest.php
│        │  │  ├─ SluggerTest.php
│        │  │  └─ UnicodeStringTest.php
│        │  ├─ TruncateMode.php
│        │  └─ UnicodeString.php
│        ├─ var-dumper
│        │  ├─ Caster
│        │  │  ├─ AddressInfoCaster.php
│        │  │  ├─ AmqpCaster.php
│        │  │  ├─ ArgsStub.php
│        │  │  ├─ Caster.php
│        │  │  ├─ ClassStub.php
│        │  │  ├─ ConstStub.php
│        │  │  ├─ CurlCaster.php
│        │  │  ├─ CutArrayStub.php
│        │  │  ├─ CutStub.php
│        │  │  ├─ DateCaster.php
│        │  │  ├─ DoctrineCaster.php
│        │  │  ├─ DOMCaster.php
│        │  │  ├─ DsCaster.php
│        │  │  ├─ DsPairStub.php
│        │  │  ├─ EnumStub.php
│        │  │  ├─ ExceptionCaster.php
│        │  │  ├─ FFICaster.php
│        │  │  ├─ FiberCaster.php
│        │  │  ├─ FrameStub.php
│        │  │  ├─ GdCaster.php
│        │  │  ├─ GmpCaster.php
│        │  │  ├─ ImagineCaster.php
│        │  │  ├─ ImgStub.php
│        │  │  ├─ IntlCaster.php
│        │  │  ├─ LinkStub.php
│        │  │  ├─ MemcachedCaster.php
│        │  │  ├─ MysqliCaster.php
│        │  │  ├─ OpenSSLCaster.php
│        │  │  ├─ PdoCaster.php
│        │  │  ├─ PgSqlCaster.php
│        │  │  ├─ ProxyManagerCaster.php
│        │  │  ├─ RdKafkaCaster.php
│        │  │  ├─ RedisCaster.php
│        │  │  ├─ ReflectionCaster.php
│        │  │  ├─ ResourceCaster.php
│        │  │  ├─ ScalarStub.php
│        │  │  ├─ SocketCaster.php
│        │  │  ├─ SplCaster.php
│        │  │  ├─ SqliteCaster.php
│        │  │  ├─ StubCaster.php
│        │  │  ├─ SymfonyCaster.php
│        │  │  ├─ TraceStub.php
│        │  │  ├─ UninitializedStub.php
│        │  │  ├─ UuidCaster.php
│        │  │  ├─ VirtualStub.php
│        │  │  ├─ XmlReaderCaster.php
│        │  │  └─ XmlResourceCaster.php
│        │  ├─ CHANGELOG.md
│        │  ├─ Cloner
│        │  │  ├─ AbstractCloner.php
│        │  │  ├─ ClonerInterface.php
│        │  │  ├─ Cursor.php
│        │  │  ├─ Data.php
│        │  │  ├─ DumperInterface.php
│        │  │  ├─ Internal
│        │  │  │  └─ NoDefault.php
│        │  │  ├─ Stub.php
│        │  │  └─ VarCloner.php
│        │  ├─ Command
│        │  │  ├─ Descriptor
│        │  │  │  ├─ CliDescriptor.php
│        │  │  │  ├─ DumpDescriptorInterface.php
│        │  │  │  └─ HtmlDescriptor.php
│        │  │  └─ ServerDumpCommand.php
│        │  ├─ composer.json
│        │  ├─ Dumper
│        │  │  ├─ AbstractDumper.php
│        │  │  ├─ CliDumper.php
│        │  │  ├─ ContextProvider
│        │  │  │  ├─ CliContextProvider.php
│        │  │  │  ├─ ContextProviderInterface.php
│        │  │  │  ├─ RequestContextProvider.php
│        │  │  │  └─ SourceContextProvider.php
│        │  │  ├─ ContextualizedDumper.php
│        │  │  ├─ DataDumperInterface.php
│        │  │  ├─ HtmlDumper.php
│        │  │  └─ ServerDumper.php
│        │  ├─ Exception
│        │  │  └─ ThrowingCasterException.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Resources
│        │  │  ├─ bin
│        │  │  │  └─ var-dump-server
│        │  │  ├─ css
│        │  │  │  └─ htmlDescriptor.css
│        │  │  ├─ functions
│        │  │  │  └─ dump.php
│        │  │  └─ js
│        │  │     └─ htmlDescriptor.js
│        │  ├─ Server
│        │  │  ├─ Connection.php
│        │  │  └─ DumpServer.php
│        │  ├─ Test
│        │  │  └─ VarDumperTestTrait.php
│        │  ├─ Tests
│        │  │  ├─ Caster
│        │  │  │  ├─ AddressInfoCasterTest.php
│        │  │  │  ├─ CasterTest.php
│        │  │  │  ├─ CurlCasterTest.php
│        │  │  │  ├─ DateCasterTest.php
│        │  │  │  ├─ DoctrineCasterTest.php
│        │  │  │  ├─ DOMCasterTest.php
│        │  │  │  ├─ ExceptionCasterTest.php
│        │  │  │  ├─ FFICasterTest.php
│        │  │  │  ├─ FiberCasterTest.php
│        │  │  │  ├─ GmpCasterTest.php
│        │  │  │  ├─ IntlCasterTest.php
│        │  │  │  ├─ MemcachedCasterTest.php
│        │  │  │  ├─ MysqliCasterTest.php
│        │  │  │  ├─ OpenSSLCasterTest.php
│        │  │  │  ├─ PdoCasterTest.php
│        │  │  │  ├─ RdKafkaCasterTest.php
│        │  │  │  ├─ RedisCasterTest.php
│        │  │  │  ├─ ReflectionCasterTest.php
│        │  │  │  ├─ ResourceCasterTest.php
│        │  │  │  ├─ SocketCasterTest.php
│        │  │  │  ├─ SplCasterTest.php
│        │  │  │  ├─ SqliteCasterTest.php
│        │  │  │  ├─ StubCasterTest.php
│        │  │  │  ├─ SymfonyCasterTest.php
│        │  │  │  └─ XmlReaderCasterTest.php
│        │  │  ├─ Cloner
│        │  │  │  ├─ DataTest.php
│        │  │  │  ├─ StubTest.php
│        │  │  │  └─ VarClonerTest.php
│        │  │  ├─ Command
│        │  │  │  ├─ Descriptor
│        │  │  │  │  ├─ CliDescriptorTest.php
│        │  │  │  │  └─ HtmlDescriptorTest.php
│        │  │  │  └─ ServerDumpCommandTest.php
│        │  │  ├─ Dumper
│        │  │  │  ├─ CliDumperTest.php
│        │  │  │  ├─ ContextProvider
│        │  │  │  │  └─ RequestContextProviderTest.php
│        │  │  │  ├─ ContextualizedDumperTest.php
│        │  │  │  ├─ functions
│        │  │  │  │  ├─ dd_with_multiple_args.phpt
│        │  │  │  │  ├─ dd_with_named_args.phpt
│        │  │  │  │  ├─ dd_with_null.phpt
│        │  │  │  │  ├─ dd_with_single_arg.phpt
│        │  │  │  │  ├─ dump_data_collector_with_spl_array.phpt
│        │  │  │  │  ├─ dump_without_args.phpt
│        │  │  │  │  ├─ dump_with_multiple_args.phpt
│        │  │  │  │  ├─ dump_with_named_args.phpt
│        │  │  │  │  ├─ dump_with_null.phpt
│        │  │  │  │  └─ dump_with_single_arg.phpt
│        │  │  │  ├─ FunctionsTest.php
│        │  │  │  ├─ HtmlDumperTest.php
│        │  │  │  └─ ServerDumperTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ BackedEnumFixture.php
│        │  │  │  ├─ DateTimeChild.php
│        │  │  │  ├─ dumb-var.php
│        │  │  │  ├─ dump_server.php
│        │  │  │  ├─ ExtendsReflectionTypeFixture.php
│        │  │  │  ├─ FooInterface.php
│        │  │  │  ├─ GeneratorDemo.php
│        │  │  │  ├─ LotsOfAttributes.php
│        │  │  │  ├─ MyAttribute.php
│        │  │  │  ├─ NotLoadableClass.php
│        │  │  │  ├─ Php74.php
│        │  │  │  ├─ Php81Enums.php
│        │  │  │  ├─ Php82NullStandaloneReturnType.php
│        │  │  │  ├─ ReflectionIntersectionTypeFixture.php
│        │  │  │  ├─ ReflectionNamedTypeFixture.php
│        │  │  │  ├─ ReflectionUnionTypeFixture.php
│        │  │  │  ├─ ReflectionUnionTypeWithIntersectionFixture.php
│        │  │  │  ├─ Twig.php
│        │  │  │  ├─ UnitEnumFixture.php
│        │  │  │  ├─ VirtualProperty.php
│        │  │  │  └─ xml_reader.xml
│        │  │  ├─ Server
│        │  │  │  └─ ConnectionTest.php
│        │  │  └─ Test
│        │  │     └─ VarDumperTestTraitTest.php
│        │  └─ VarDumper.php
│        ├─ var-exporter
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ Exception
│        │  │  ├─ ClassNotFoundException.php
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ LogicException.php
│        │  │  └─ NotInstantiableTypeException.php
│        │  ├─ Hydrator.php
│        │  ├─ Instantiator.php
│        │  ├─ Internal
│        │  │  ├─ Exporter.php
│        │  │  ├─ Hydrator.php
│        │  │  ├─ LazyDecoratorTrait.php
│        │  │  ├─ LazyObjectRegistry.php
│        │  │  ├─ LazyObjectState.php
│        │  │  ├─ LazyObjectTrait.php
│        │  │  ├─ Reference.php
│        │  │  ├─ Registry.php
│        │  │  └─ Values.php
│        │  ├─ LazyGhostTrait.php
│        │  ├─ LazyObjectInterface.php
│        │  ├─ LazyProxyTrait.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ ProxyHelper.php
│        │  ├─ README.md
│        │  ├─ Tests
│        │  │  ├─ Fixtures
│        │  │  │  ├─ abstract-parent.php
│        │  │  │  ├─ array-iterator.php
│        │  │  │  ├─ array-object-custom.php
│        │  │  │  ├─ array-object.php
│        │  │  │  ├─ backed-property.php
│        │  │  │  ├─ BackedProperty.php
│        │  │  │  ├─ bool.php
│        │  │  │  ├─ clone.php
│        │  │  │  ├─ datetime.php
│        │  │  │  ├─ error.php
│        │  │  │  ├─ external-references.php
│        │  │  │  ├─ final-array-iterator.php
│        │  │  │  ├─ final-error.php
│        │  │  │  ├─ final-stdclass.php
│        │  │  │  ├─ foo-serializable.php
│        │  │  │  ├─ FooReadonly.php
│        │  │  │  ├─ FooSerializable.php
│        │  │  │  ├─ FooUnitEnum.php
│        │  │  │  ├─ hard-references-recursive.php
│        │  │  │  ├─ hard-references.php
│        │  │  │  ├─ incomplete-class.php
│        │  │  │  ├─ LazyGhost
│        │  │  │  │  ├─ ChildMagicClass.php
│        │  │  │  │  ├─ ChildStdClass.php
│        │  │  │  │  ├─ ChildTestClass.php
│        │  │  │  │  ├─ ClassWithUninitializedObjectProperty.php
│        │  │  │  │  ├─ LazyClass.php
│        │  │  │  │  ├─ MagicClass.php
│        │  │  │  │  ├─ NoMagicClass.php
│        │  │  │  │  ├─ ReadOnlyClass.php
│        │  │  │  │  ├─ RegularClass.php
│        │  │  │  │  └─ TestClass.php
│        │  │  │  ├─ LazyProxy
│        │  │  │  │  ├─ AbstractHooked.php
│        │  │  │  │  ├─ AsymmetricVisibility.php
│        │  │  │  │  ├─ ConcreteReadOnlyClass.php
│        │  │  │  │  ├─ FinalPublicClass.php
│        │  │  │  │  ├─ Hooked.php
│        │  │  │  │  ├─ HookedInterface.php
│        │  │  │  │  ├─ HookedWithDefaultValue.php
│        │  │  │  │  ├─ Php82NullStandaloneReturnType.php
│        │  │  │  │  ├─ ReadOnlyClass.php
│        │  │  │  │  ├─ StringMagicGetClass.php
│        │  │  │  │  ├─ TestClass.php
│        │  │  │  │  ├─ TestOverwritePropClass.php
│        │  │  │  │  ├─ TestUnserializeClass.php
│        │  │  │  │  └─ TestWakeupClass.php
│        │  │  │  ├─ lf-ending-string.php
│        │  │  │  ├─ multiline-string.php
│        │  │  │  ├─ MySerializable.php
│        │  │  │  ├─ partially-indexed-array.php
│        │  │  │  ├─ php74-serializable.php
│        │  │  │  ├─ private-constructor.php
│        │  │  │  ├─ private.php
│        │  │  │  ├─ readonly.php
│        │  │  │  ├─ serializable.php
│        │  │  │  ├─ simple-array.php
│        │  │  │  ├─ SimpleObject.php
│        │  │  │  ├─ spl-object-storage.php
│        │  │  │  ├─ unit-enum.php
│        │  │  │  ├─ var-on-sleep.php
│        │  │  │  ├─ wakeup-refl.php
│        │  │  │  ├─ wakeup.php
│        │  │  │  ├─ __serialize-but-no-__unserialize.php
│        │  │  │  └─ __unserialize-but-no-__serialize.php
│        │  │  ├─ InstantiatorTest.php
│        │  │  ├─ LazyProxyTraitTest.php
│        │  │  ├─ LegacyLazyGhostTraitTest.php
│        │  │  ├─ LegacyLazyProxyTraitTest.php
│        │  │  ├─ LegacyProxyHelperTest.php
│        │  │  ├─ ProxyHelperTest.php
│        │  │  └─ VarExporterTest.php
│        │  └─ VarExporter.php
│        └─ yaml
│           ├─ CHANGELOG.md
│           ├─ Command
│           │  └─ LintCommand.php
│           ├─ composer.json
│           ├─ Dumper.php
│           ├─ Escaper.php
│           ├─ Exception
│           │  ├─ DumpException.php
│           │  ├─ ExceptionInterface.php
│           │  ├─ ParseException.php
│           │  └─ RuntimeException.php
│           ├─ Inline.php
│           ├─ LICENSE
│           ├─ Parser.php
│           ├─ phpunit.xml.dist
│           ├─ README.md
│           ├─ Resources
│           │  └─ bin
│           │     └─ yaml-lint
│           ├─ Tag
│           │  └─ TaggedValue.php
│           ├─ Tests
│           │  ├─ Command
│           │  │  └─ LintCommandTest.php
│           │  ├─ DumperTest.php
│           │  ├─ Fixtures
│           │  │  ├─ arrow.gif
│           │  │  ├─ booleanMappingKeys.yml
│           │  │  ├─ embededPhp.yml
│           │  │  ├─ escapedCharacters.yml
│           │  │  ├─ FooBackedEnum.php
│           │  │  ├─ FooUnitEnum.php
│           │  │  ├─ index.yml
│           │  │  ├─ nonStringKeys.yml
│           │  │  ├─ not_readable.yml
│           │  │  ├─ nullMappingKey.yml
│           │  │  ├─ numericMappingKeys.yml
│           │  │  ├─ sfComments.yml
│           │  │  ├─ sfCompact.yml
│           │  │  ├─ sfMergeKey.yml
│           │  │  ├─ sfObjects.yml
│           │  │  ├─ sfQuotes.yml
│           │  │  ├─ sfTests.yml
│           │  │  ├─ unindentedCollections.yml
│           │  │  ├─ YtsAnchorAlias.yml
│           │  │  ├─ YtsBasicTests.yml
│           │  │  ├─ YtsBlockMapping.yml
│           │  │  ├─ YtsDocumentSeparator.yml
│           │  │  ├─ YtsErrorTests.yml
│           │  │  ├─ YtsFlowCollections.yml
│           │  │  ├─ YtsFoldedScalars.yml
│           │  │  ├─ YtsNullsAndEmpties.yml
│           │  │  ├─ YtsSpecificationExamples.yml
│           │  │  └─ YtsTypeTransfers.yml
│           │  ├─ InlineTest.php
│           │  ├─ ParseExceptionTest.php
│           │  ├─ ParserTest.php
│           │  └─ YamlTest.php
│           ├─ Unescaper.php
│           └─ Yaml.php
├─ docker-compose.dev.yml
├─ docs
├─ frontend
│  ├─ .editorconfig
│  ├─ .prettierrc.json
│  ├─ Dockerfile.dev
│  ├─ env.d.ts
│  ├─ eslint.config.ts
│  ├─ index.html
│  ├─ package-lock.json
│  ├─ package.json
│  ├─ playwright.config.ts
│  ├─ public
│  │  └─ favicon.ico
│  ├─ README.md
│  ├─ src
│  │  ├─ App.vue
│  │  ├─ assets
│  │  │  ├─ base.css
│  │  │  ├─ logo.svg
│  │  │  └─ main.css
│  │  ├─ components
│  │  │  ├─ HelloWorld.vue
│  │  │  ├─ icons
│  │  │  │  ├─ IconCommunity.vue
│  │  │  │  ├─ IconDocumentation.vue
│  │  │  │  ├─ IconEcosystem.vue
│  │  │  │  ├─ IconSupport.vue
│  │  │  │  └─ IconTooling.vue
│  │  │  ├─ TheWelcome.vue
│  │  │  ├─ WelcomeItem.vue
│  │  │  └─ __tests__
│  │  │     └─ HelloWorld.spec.ts
│  │  ├─ main.ts
│  │  ├─ router
│  │  │  └─ index.ts
│  │  ├─ stores
│  │  │  └─ counter.ts
│  │  └─ views
│  │     ├─ AboutView.vue
│  │     └─ HomeView.vue
│  ├─ tests
│  │  ├─ auth
│  │  │  └─ user.json
│  │  ├─ e2e
│  │  │  ├─ auth.spec.ts
│  │  │  ├─ clients.spec.ts
│  │  │  ├─ dashboard.spec.ts
│  │  │  ├─ invoicing.spec.ts
│  │  │  ├─ subscriptions.spec.ts
│  │  │  ├─ tsconfig.json
│  │  │  ├─ urssaf.spec.ts
│  │  │  └─ vue.spec.ts
│  │  ├─ fixtures
│  │  │  └─ test-data.json
│  │  └─ utils
│  │     └─ helpers.ts
│  ├─ tsconfig.app.json
│  ├─ tsconfig.json
│  ├─ tsconfig.node.json
│  ├─ tsconfig.vitest.json
│  ├─ vite.config.ts
│  └─ vitest.config.ts
├─ infrastructure
├─ LICENSE
└─ README.md

```
```
Autoflow
├─ backend
│  ├─ .editorconfig
│  ├─ .env
│  ├─ .env.dev
│  ├─ bin
│  │  └─ console
│  ├─ composer.json
│  ├─ composer.lock
│  ├─ config
│  │  ├─ bundles.php
│  │  ├─ packages
│  │  │  ├─ cache.yaml
│  │  │  ├─ framework.yaml
│  │  │  └─ routing.yaml
│  │  ├─ preload.php
│  │  ├─ routes
│  │  │  └─ framework.yaml
│  │  ├─ routes.yaml
│  │  └─ services.yaml
│  ├─ Dockerfile.dev
│  ├─ public
│  │  └─ index.php
│  ├─ src
│  │  ├─ Controller
│  │  └─ Kernel.php
│  ├─ symfony.lock
│  ├─ var
│  │  └─ cache
│  │     └─ dev
│  │        ├─ App_KernelDevDebugContainer.php
│  │        ├─ App_KernelDevDebugContainer.php.lock
│  │        ├─ App_KernelDevDebugContainer.php.meta
│  │        ├─ App_KernelDevDebugContainer.php.meta.json
│  │        ├─ App_KernelDevDebugContainer.preload.php
│  │        ├─ App_KernelDevDebugContainer.xml
│  │        ├─ App_KernelDevDebugContainer.xml.meta
│  │        ├─ App_KernelDevDebugContainer.xml.meta.json
│  │        ├─ App_KernelDevDebugContainerCompiler.log
│  │        ├─ App_KernelDevDebugContainerDeprecations.log
│  │        ├─ ContainerZYAsdwH
│  │        │  ├─ App_KernelDevDebugContainer.php
│  │        │  ├─ getArgumentResolver_BackedEnumResolverService.php
│  │        │  ├─ getArgumentResolver_DatetimeService.php
│  │        │  ├─ getArgumentResolver_DefaultService.php
│  │        │  ├─ getArgumentResolver_QueryParameterValueResolverService.php
│  │        │  ├─ getArgumentResolver_RequestAttributeService.php
│  │        │  ├─ getArgumentResolver_RequestPayloadService.php
│  │        │  ├─ getArgumentResolver_RequestService.php
│  │        │  ├─ getArgumentResolver_ServiceService.php
│  │        │  ├─ getArgumentResolver_SessionService.php
│  │        │  ├─ getArgumentResolver_VariadicService.php
│  │        │  ├─ getCacheWarmerService.php
│  │        │  ├─ getCache_AppClearerService.php
│  │        │  ├─ getCache_AppService.php
│  │        │  ├─ getCache_App_TaggableService.php
│  │        │  ├─ getCache_GlobalClearerService.php
│  │        │  ├─ getCache_SystemClearerService.php
│  │        │  ├─ getCache_SystemService.php
│  │        │  ├─ getConfigBuilder_WarmerService.php
│  │        │  ├─ getConsole_CommandLoaderService.php
│  │        │  ├─ getConsole_Command_AboutService.php
│  │        │  ├─ getConsole_Command_AssetsInstallService.php
│  │        │  ├─ getConsole_Command_CacheClearService.php
│  │        │  ├─ getConsole_Command_CachePoolClearService.php
│  │        │  ├─ getConsole_Command_CachePoolDeleteService.php
│  │        │  ├─ getConsole_Command_CachePoolInvalidateTagsService.php
│  │        │  ├─ getConsole_Command_CachePoolListService.php
│  │        │  ├─ getConsole_Command_CachePoolPruneService.php
│  │        │  ├─ getConsole_Command_CacheWarmupService.php
│  │        │  ├─ getConsole_Command_ConfigDebugService.php
│  │        │  ├─ getConsole_Command_ConfigDumpReferenceService.php
│  │        │  ├─ getConsole_Command_ContainerDebugService.php
│  │        │  ├─ getConsole_Command_ContainerLintService.php
│  │        │  ├─ getConsole_Command_DebugAutowiringService.php
│  │        │  ├─ getConsole_Command_DotenvDebugService.php
│  │        │  ├─ getConsole_Command_ErrorDumperService.php
│  │        │  ├─ getConsole_Command_EventDispatcherDebugService.php
│  │        │  ├─ getConsole_Command_RouterDebugService.php
│  │        │  ├─ getConsole_Command_RouterMatchService.php
│  │        │  ├─ getConsole_Command_SecretsDecryptToLocalService.php
│  │        │  ├─ getConsole_Command_SecretsEncryptFromLocalService.php
│  │        │  ├─ getConsole_Command_SecretsGenerateKeyService.php
│  │        │  ├─ getConsole_Command_SecretsListService.php
│  │        │  ├─ getConsole_Command_SecretsRemoveService.php
│  │        │  ├─ getConsole_Command_SecretsRevealService.php
│  │        │  ├─ getConsole_Command_SecretsSetService.php
│  │        │  ├─ getConsole_Command_YamlLintService.php
│  │        │  ├─ getConsole_ErrorListenerService.php
│  │        │  ├─ getContainer_EnvVarProcessorService.php
│  │        │  ├─ getContainer_EnvVarProcessorsLocatorService.php
│  │        │  ├─ getContainer_GetRoutingConditionServiceService.php
│  │        │  ├─ getDebug_ErrorHandlerConfiguratorService.php
│  │        │  ├─ getErrorControllerService.php
│  │        │  ├─ getErrorHandler_ErrorRenderer_HtmlService.php
│  │        │  ├─ getLoaderInterfaceService.php
│  │        │  ├─ getRedirectControllerService.php
│  │        │  ├─ getRouter_CacheWarmerService.php
│  │        │  ├─ getRouting_LoaderService.php
│  │        │  ├─ getSecrets_EnvVarLoaderService.php
│  │        │  ├─ getSecrets_VaultService.php
│  │        │  ├─ getServicesResetterService.php
│  │        │  ├─ getSession_FactoryService.php
│  │        │  ├─ getTemplateControllerService.php
│  │        │  ├─ get_Console_Command_About_LazyService.php
│  │        │  ├─ get_Console_Command_AssetsInstall_LazyService.php
│  │        │  ├─ get_Console_Command_CacheClear_LazyService.php
│  │        │  ├─ get_Console_Command_CachePoolClear_LazyService.php
│  │        │  ├─ get_Console_Command_CachePoolDelete_LazyService.php
│  │        │  ├─ get_Console_Command_CachePoolInvalidateTags_LazyService.php
│  │        │  ├─ get_Console_Command_CachePoolList_LazyService.php
│  │        │  ├─ get_Console_Command_CachePoolPrune_LazyService.php
│  │        │  ├─ get_Console_Command_CacheWarmup_LazyService.php
│  │        │  ├─ get_Console_Command_ConfigDebug_LazyService.php
│  │        │  ├─ get_Console_Command_ConfigDumpReference_LazyService.php
│  │        │  ├─ get_Console_Command_ContainerDebug_LazyService.php
│  │        │  ├─ get_Console_Command_ContainerLint_LazyService.php
│  │        │  ├─ get_Console_Command_DebugAutowiring_LazyService.php
│  │        │  ├─ get_Console_Command_DotenvDebug_LazyService.php
│  │        │  ├─ get_Console_Command_ErrorDumper_LazyService.php
│  │        │  ├─ get_Console_Command_EventDispatcherDebug_LazyService.php
│  │        │  ├─ get_Console_Command_RouterDebug_LazyService.php
│  │        │  ├─ get_Console_Command_RouterMatch_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsDecryptToLocal_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsEncryptFromLocal_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsGenerateKey_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsList_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsRemove_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsReveal_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsSet_LazyService.php
│  │        │  ├─ get_Console_Command_YamlLint_LazyService.php
│  │        │  ├─ get_ServiceLocator_ZHyJIs5Service.php
│  │        │  ├─ get_ServiceLocator_ZHyJIs5_KernelloadRoutesService.php
│  │        │  ├─ get_ServiceLocator_ZHyJIs5_KernelregisterContainerConfigurationService.php
│  │        │  ├─ removed-ids.php
│  │        │  └─ RequestPayloadValueResolverGhost01ca9cc.php
│  │        ├─ Symfony
│  │        │  └─ Config
│  │        │     ├─ Framework
│  │        │     │  ├─ AnnotationsConfig.php
│  │        │     │  ├─ AssetMapper
│  │        │     │  │  └─ PrecompressConfig.php
│  │        │     │  ├─ AssetMapperConfig.php
│  │        │     │  ├─ Assets
│  │        │     │  │  └─ PackageConfig.php
│  │        │     │  ├─ AssetsConfig.php
│  │        │     │  ├─ Cache
│  │        │     │  │  └─ PoolConfig.php
│  │        │     │  ├─ CacheConfig.php
│  │        │     │  ├─ CsrfProtectionConfig.php
│  │        │     │  ├─ EsiConfig.php
│  │        │     │  ├─ ExceptionConfig.php
│  │        │     │  ├─ Form
│  │        │     │  │  └─ CsrfProtectionConfig.php
│  │        │     │  ├─ FormConfig.php
│  │        │     │  ├─ FragmentsConfig.php
│  │        │     │  ├─ HtmlSanitizer
│  │        │     │  │  └─ SanitizerConfig.php
│  │        │     │  ├─ HtmlSanitizerConfig.php
│  │        │     │  ├─ HttpCacheConfig.php
│  │        │     │  ├─ HttpClient
│  │        │     │  │  ├─ DefaultOptions
│  │        │     │  │  │  ├─ PeerFingerprintConfig.php
│  │        │     │  │  │  ├─ RetryFailed
│  │        │     │  │  │  │  └─ HttpCodeConfig.php
│  │        │     │  │  │  └─ RetryFailedConfig.php
│  │        │     │  │  ├─ DefaultOptionsConfig.php
│  │        │     │  │  ├─ ScopedClientConfig
│  │        │     │  │  │  ├─ PeerFingerprintConfig.php
│  │        │     │  │  │  ├─ RetryFailed
│  │        │     │  │  │  │  └─ HttpCodeConfig.php
│  │        │     │  │  │  └─ RetryFailedConfig.php
│  │        │     │  │  └─ ScopedClientConfig.php
│  │        │     │  ├─ HttpClientConfig.php
│  │        │     │  ├─ JsonStreamerConfig.php
│  │        │     │  ├─ LockConfig.php
│  │        │     │  ├─ Mailer
│  │        │     │  │  ├─ DkimSignerConfig.php
│  │        │     │  │  ├─ EnvelopeConfig.php
│  │        │     │  │  ├─ HeaderConfig.php
│  │        │     │  │  ├─ SmimeEncrypterConfig.php
│  │        │     │  │  └─ SmimeSignerConfig.php
│  │        │     │  ├─ MailerConfig.php
│  │        │     │  ├─ Messenger
│  │        │     │  │  ├─ BusConfig
│  │        │     │  │  │  ├─ DefaultMiddlewareConfig.php
│  │        │     │  │  │  └─ MiddlewareConfig.php
│  │        │     │  │  ├─ BusConfig.php
│  │        │     │  │  ├─ RoutingConfig.php
│  │        │     │  │  ├─ Serializer
│  │        │     │  │  │  └─ SymfonySerializerConfig.php
│  │        │     │  │  ├─ SerializerConfig.php
│  │        │     │  │  ├─ TransportConfig
│  │        │     │  │  │  └─ RetryStrategyConfig.php
│  │        │     │  │  └─ TransportConfig.php
│  │        │     │  ├─ MessengerConfig.php
│  │        │     │  ├─ Notifier
│  │        │     │  │  └─ AdminRecipientConfig.php
│  │        │     │  ├─ NotifierConfig.php
│  │        │     │  ├─ PhpErrorsConfig.php
│  │        │     │  ├─ ProfilerConfig.php
│  │        │     │  ├─ PropertyAccessConfig.php
│  │        │     │  ├─ PropertyInfoConfig.php
│  │        │     │  ├─ RateLimiter
│  │        │     │  │  ├─ LimiterConfig
│  │        │     │  │  │  └─ RateConfig.php
│  │        │     │  │  └─ LimiterConfig.php
│  │        │     │  ├─ RateLimiterConfig.php
│  │        │     │  ├─ RemoteeventConfig.php
│  │        │     │  ├─ RequestConfig.php
│  │        │     │  ├─ RouterConfig.php
│  │        │     │  ├─ SchedulerConfig.php
│  │        │     │  ├─ SecretsConfig.php
│  │        │     │  ├─ SemaphoreConfig.php
│  │        │     │  ├─ Serializer
│  │        │     │  │  ├─ MappingConfig.php
│  │        │     │  │  └─ NamedSerializerConfig.php
│  │        │     │  ├─ SerializerConfig.php
│  │        │     │  ├─ SessionConfig.php
│  │        │     │  ├─ SsiConfig.php
│  │        │     │  ├─ Translator
│  │        │     │  │  ├─ GlobalConfig.php
│  │        │     │  │  ├─ ProviderConfig.php
│  │        │     │  │  └─ PseudoLocalizationConfig.php
│  │        │     │  ├─ TranslatorConfig.php
│  │        │     │  ├─ TypeInfoConfig.php
│  │        │     │  ├─ UidConfig.php
│  │        │     │  ├─ Validation
│  │        │     │  │  ├─ AutoMappingConfig.php
│  │        │     │  │  ├─ MappingConfig.php
│  │        │     │  │  └─ NotCompromisedPasswordConfig.php
│  │        │     │  ├─ ValidationConfig.php
│  │        │     │  ├─ Webhook
│  │        │     │  │  └─ RoutingConfig.php
│  │        │     │  ├─ WebhookConfig.php
│  │        │     │  ├─ WebLinkConfig.php
│  │        │     │  ├─ Workflows
│  │        │     │  │  ├─ WorkflowsConfig
│  │        │     │  │  │  ├─ AuditTrailConfig.php
│  │        │     │  │  │  ├─ MarkingStoreConfig.php
│  │        │     │  │  │  ├─ PlaceConfig.php
│  │        │     │  │  │  └─ TransitionConfig.php
│  │        │     │  │  └─ WorkflowsConfig.php
│  │        │     │  └─ WorkflowsConfig.php
│  │        │     └─ FrameworkConfig.php
│  │        ├─ url_generating_routes.php
│  │        ├─ url_generating_routes.php.meta
│  │        ├─ url_generating_routes.php.meta.json
│  │        ├─ url_matching_routes.php
│  │        ├─ url_matching_routes.php.meta
│  │        └─ url_matching_routes.php.meta.json
│  └─ vendor
│     ├─ autoload.php
│     ├─ autoload_runtime.php
│     ├─ bin
│     │  ├─ patch-type-declarations
│     │  ├─ patch-type-declarations.bat
│     │  ├─ var-dump-server
│     │  ├─ var-dump-server.bat
│     │  ├─ yaml-lint
│     │  └─ yaml-lint.bat
│     ├─ composer
│     │  ├─ autoload_classmap.php
│     │  ├─ autoload_files.php
│     │  ├─ autoload_namespaces.php
│     │  ├─ autoload_psr4.php
│     │  ├─ autoload_real.php
│     │  ├─ autoload_static.php
│     │  ├─ ClassLoader.php
│     │  ├─ installed.json
│     │  ├─ installed.php
│     │  ├─ InstalledVersions.php
│     │  ├─ LICENSE
│     │  └─ platform_check.php
│     ├─ psr
│     │  ├─ cache
│     │  │  ├─ CHANGELOG.md
│     │  │  ├─ composer.json
│     │  │  ├─ LICENSE.txt
│     │  │  ├─ README.md
│     │  │  └─ src
│     │  │     ├─ CacheException.php
│     │  │     ├─ CacheItemInterface.php
│     │  │     ├─ CacheItemPoolInterface.php
│     │  │     └─ InvalidArgumentException.php
│     │  ├─ container
│     │  │  ├─ composer.json
│     │  │  ├─ LICENSE
│     │  │  ├─ README.md
│     │  │  └─ src
│     │  │     ├─ ContainerExceptionInterface.php
│     │  │     ├─ ContainerInterface.php
│     │  │     └─ NotFoundExceptionInterface.php
│     │  ├─ event-dispatcher
│     │  │  ├─ .editorconfig
│     │  │  ├─ composer.json
│     │  │  ├─ LICENSE
│     │  │  ├─ README.md
│     │  │  └─ src
│     │  │     ├─ EventDispatcherInterface.php
│     │  │     ├─ ListenerProviderInterface.php
│     │  │     └─ StoppableEventInterface.php
│     │  └─ log
│     │     ├─ composer.json
│     │     ├─ LICENSE
│     │     ├─ README.md
│     │     └─ src
│     │        ├─ AbstractLogger.php
│     │        ├─ InvalidArgumentException.php
│     │        ├─ LoggerAwareInterface.php
│     │        ├─ LoggerAwareTrait.php
│     │        ├─ LoggerInterface.php
│     │        ├─ LoggerTrait.php
│     │        ├─ LogLevel.php
│     │        └─ NullLogger.php
│     └─ symfony
│        ├─ cache
│        │  ├─ Adapter
│        │  │  ├─ AbstractAdapter.php
│        │  │  ├─ AbstractTagAwareAdapter.php
│        │  │  ├─ AdapterInterface.php
│        │  │  ├─ ApcuAdapter.php
│        │  │  ├─ ArrayAdapter.php
│        │  │  ├─ ChainAdapter.php
│        │  │  ├─ CouchbaseBucketAdapter.php
│        │  │  ├─ CouchbaseCollectionAdapter.php
│        │  │  ├─ DoctrineDbalAdapter.php
│        │  │  ├─ FilesystemAdapter.php
│        │  │  ├─ FilesystemTagAwareAdapter.php
│        │  │  ├─ MemcachedAdapter.php
│        │  │  ├─ NullAdapter.php
│        │  │  ├─ ParameterNormalizer.php
│        │  │  ├─ PdoAdapter.php
│        │  │  ├─ PhpArrayAdapter.php
│        │  │  ├─ PhpFilesAdapter.php
│        │  │  ├─ ProxyAdapter.php
│        │  │  ├─ Psr16Adapter.php
│        │  │  ├─ RedisAdapter.php
│        │  │  ├─ RedisTagAwareAdapter.php
│        │  │  ├─ TagAwareAdapter.php
│        │  │  ├─ TagAwareAdapterInterface.php
│        │  │  ├─ TraceableAdapter.php
│        │  │  └─ TraceableTagAwareAdapter.php
│        │  ├─ CacheItem.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ DataCollector
│        │  │  └─ CacheDataCollector.php
│        │  ├─ DependencyInjection
│        │  │  ├─ CacheCollectorPass.php
│        │  │  ├─ CachePoolClearerPass.php
│        │  │  ├─ CachePoolPass.php
│        │  │  └─ CachePoolPrunerPass.php
│        │  ├─ Exception
│        │  │  ├─ BadMethodCallException.php
│        │  │  ├─ CacheException.php
│        │  │  ├─ InvalidArgumentException.php
│        │  │  └─ LogicException.php
│        │  ├─ LICENSE
│        │  ├─ LockRegistry.php
│        │  ├─ Marshaller
│        │  │  ├─ DefaultMarshaller.php
│        │  │  ├─ DeflateMarshaller.php
│        │  │  ├─ MarshallerInterface.php
│        │  │  ├─ SodiumMarshaller.php
│        │  │  └─ TagAwareMarshaller.php
│        │  ├─ Messenger
│        │  │  ├─ EarlyExpirationDispatcher.php
│        │  │  ├─ EarlyExpirationHandler.php
│        │  │  └─ EarlyExpirationMessage.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ PruneableInterface.php
│        │  ├─ Psr16Cache.php
│        │  ├─ README.md
│        │  ├─ ResettableInterface.php
│        │  ├─ Tests
│        │  │  ├─ Adapter
│        │  │  │  ├─ AbstractRedisAdapterTestCase.php
│        │  │  │  ├─ AdapterTestCase.php
│        │  │  │  ├─ ApcuAdapterTest.php
│        │  │  │  ├─ ArrayAdapterTest.php
│        │  │  │  ├─ ChainAdapterTest.php
│        │  │  │  ├─ CouchbaseBucketAdapterTest.php
│        │  │  │  ├─ CouchbaseCollectionAdapterTest.php
│        │  │  │  ├─ DoctrineDbalAdapterTest.php
│        │  │  │  ├─ FilesystemAdapterTest.php
│        │  │  │  ├─ FilesystemTagAwareAdapterTest.php
│        │  │  │  ├─ MaxIdLengthAdapterTest.php
│        │  │  │  ├─ MemcachedAdapterTest.php
│        │  │  │  ├─ NamespacedProxyAdapterTest.php
│        │  │  │  ├─ NullAdapterTest.php
│        │  │  │  ├─ PdoAdapterTest.php
│        │  │  │  ├─ PhpArrayAdapterTest.php
│        │  │  │  ├─ PhpArrayAdapterWithFallbackTest.php
│        │  │  │  ├─ PhpFilesAdapterAppendOnlyTest.php
│        │  │  │  ├─ PhpFilesAdapterTest.php
│        │  │  │  ├─ PredisAdapterSentinelTest.php
│        │  │  │  ├─ PredisAdapterTest.php
│        │  │  │  ├─ PredisClusterAdapterTest.php
│        │  │  │  ├─ PredisRedisClusterAdapterTest.php
│        │  │  │  ├─ PredisRedisReplicationAdapterTest.php
│        │  │  │  ├─ PredisReplicationAdapterTest.php
│        │  │  │  ├─ PredisTagAwareAdapterTest.php
│        │  │  │  ├─ PredisTagAwareClusterAdapterTest.php
│        │  │  │  ├─ ProxyAdapterAndRedisAdapterTest.php
│        │  │  │  ├─ ProxyAdapterTest.php
│        │  │  │  ├─ Psr16AdapterTest.php
│        │  │  │  ├─ RedisAdapterSentinelTest.php
│        │  │  │  ├─ RedisAdapterTest.php
│        │  │  │  ├─ RedisArrayAdapterTest.php
│        │  │  │  ├─ RedisClusterAdapterTest.php
│        │  │  │  ├─ RedisTagAwareAdapterTest.php
│        │  │  │  ├─ RedisTagAwareArrayAdapterTest.php
│        │  │  │  ├─ RedisTagAwareClusterAdapterTest.php
│        │  │  │  ├─ RedisTagAwareRelayClusterAdapterTest.php
│        │  │  │  ├─ RelayAdapterSentinelTest.php
│        │  │  │  ├─ RelayAdapterTest.php
│        │  │  │  ├─ RelayClusterAdapterTest.php
│        │  │  │  ├─ TagAwareAdapterTest.php
│        │  │  │  ├─ TagAwareAndProxyAdapterIntegrationTest.php
│        │  │  │  ├─ TagAwareTestTrait.php
│        │  │  │  ├─ TraceableAdapterTest.php
│        │  │  │  └─ TraceableTagAwareAdapterTest.php
│        │  │  ├─ CacheItemTest.php
│        │  │  ├─ DataCollector
│        │  │  │  └─ CacheDataCollectorTest.php
│        │  │  ├─ DependencyInjection
│        │  │  │  ├─ CacheCollectorPassTest.php
│        │  │  │  ├─ CachePoolClearerPassTest.php
│        │  │  │  ├─ CachePoolPassTest.php
│        │  │  │  └─ CachePoolPrunerPassTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ ExternalAdapter.php
│        │  │  │  ├─ PrunableAdapter.php
│        │  │  │  ├─ StringableTag.php
│        │  │  │  └─ TestEnum.php
│        │  │  ├─ LockRegistryTest.php
│        │  │  ├─ Marshaller
│        │  │  │  ├─ DefaultMarshallerTest.php
│        │  │  │  ├─ DeflateMarshallerTest.php
│        │  │  │  └─ SodiumMarshallerTest.php
│        │  │  ├─ Messenger
│        │  │  │  ├─ EarlyExpirationDispatcherTest.php
│        │  │  │  ├─ EarlyExpirationHandlerTest.php
│        │  │  │  └─ EarlyExpirationMessageTest.php
│        │  │  ├─ Psr16CacheProxyTest.php
│        │  │  ├─ Psr16CacheTest.php
│        │  │  ├─ Psr16CacheWithExternalAdapter.php
│        │  │  └─ Traits
│        │  │     ├─ RedisProxiesTest.php
│        │  │     └─ RedisTraitTest.php
│        │  └─ Traits
│        │     ├─ AbstractAdapterTrait.php
│        │     ├─ ContractsTrait.php
│        │     ├─ FilesystemCommonTrait.php
│        │     ├─ FilesystemTrait.php
│        │     ├─ ProxyTrait.php
│        │     ├─ Redis5Proxy.php
│        │     ├─ Redis6Proxy.php
│        │     ├─ Redis6ProxyTrait.php
│        │     ├─ RedisCluster5Proxy.php
│        │     ├─ RedisCluster6Proxy.php
│        │     ├─ RedisCluster6ProxyTrait.php
│        │     ├─ RedisClusterNodeProxy.php
│        │     ├─ RedisClusterProxy.php
│        │     ├─ RedisProxy.php
│        │     ├─ RedisProxyTrait.php
│        │     ├─ RedisTrait.php
│        │     ├─ Relay
│        │     │  ├─ CopyTrait.php
│        │     │  ├─ GeosearchTrait.php
│        │     │  ├─ GetrangeTrait.php
│        │     │  ├─ HsetTrait.php
│        │     │  ├─ MoveTrait.php
│        │     │  ├─ NullableReturnTrait.php
│        │     │  └─ PfcountTrait.php
│        │     ├─ RelayClusterProxy.php
│        │     ├─ RelayProxy.php
│        │     ├─ RelayProxyTrait.php
│        │     └─ ValueWrapper.php
│        ├─ cache-contracts
│        │  ├─ CacheInterface.php
│        │  ├─ CacheTrait.php
│        │  ├─ CallbackInterface.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ ItemInterface.php
│        │  ├─ LICENSE
│        │  ├─ NamespacedPoolInterface.php
│        │  ├─ README.md
│        │  └─ TagAwareCacheInterface.php
│        ├─ config
│        │  ├─ Builder
│        │  │  ├─ ClassBuilder.php
│        │  │  ├─ ConfigBuilderGenerator.php
│        │  │  ├─ ConfigBuilderGeneratorInterface.php
│        │  │  ├─ ConfigBuilderInterface.php
│        │  │  ├─ Method.php
│        │  │  └─ Property.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ ConfigCache.php
│        │  ├─ ConfigCacheFactory.php
│        │  ├─ ConfigCacheFactoryInterface.php
│        │  ├─ ConfigCacheInterface.php
│        │  ├─ Definition
│        │  │  ├─ ArrayNode.php
│        │  │  ├─ BaseNode.php
│        │  │  ├─ BooleanNode.php
│        │  │  ├─ Builder
│        │  │  │  ├─ ArrayNodeDefinition.php
│        │  │  │  ├─ BooleanNodeDefinition.php
│        │  │  │  ├─ BuilderAwareInterface.php
│        │  │  │  ├─ EnumNodeDefinition.php
│        │  │  │  ├─ ExprBuilder.php
│        │  │  │  ├─ FloatNodeDefinition.php
│        │  │  │  ├─ IntegerNodeDefinition.php
│        │  │  │  ├─ MergeBuilder.php
│        │  │  │  ├─ NodeBuilder.php
│        │  │  │  ├─ NodeDefinition.php
│        │  │  │  ├─ NodeParentInterface.php
│        │  │  │  ├─ NormalizationBuilder.php
│        │  │  │  ├─ NumericNodeDefinition.php
│        │  │  │  ├─ ParentNodeDefinitionInterface.php
│        │  │  │  ├─ ScalarNodeDefinition.php
│        │  │  │  ├─ StringNodeDefinition.php
│        │  │  │  ├─ TreeBuilder.php
│        │  │  │  ├─ ValidationBuilder.php
│        │  │  │  └─ VariableNodeDefinition.php
│        │  │  ├─ ConfigurableInterface.php
│        │  │  ├─ Configuration.php
│        │  │  ├─ ConfigurationInterface.php
│        │  │  ├─ Configurator
│        │  │  │  └─ DefinitionConfigurator.php
│        │  │  ├─ Dumper
│        │  │  │  ├─ XmlReferenceDumper.php
│        │  │  │  └─ YamlReferenceDumper.php
│        │  │  ├─ EnumNode.php
│        │  │  ├─ Exception
│        │  │  │  ├─ DuplicateKeyException.php
│        │  │  │  ├─ Exception.php
│        │  │  │  ├─ ForbiddenOverwriteException.php
│        │  │  │  ├─ InvalidConfigurationException.php
│        │  │  │  ├─ InvalidDefinitionException.php
│        │  │  │  ├─ InvalidTypeException.php
│        │  │  │  └─ UnsetKeyException.php
│        │  │  ├─ FloatNode.php
│        │  │  ├─ IntegerNode.php
│        │  │  ├─ Loader
│        │  │  │  └─ DefinitionFileLoader.php
│        │  │  ├─ NodeInterface.php
│        │  │  ├─ NumericNode.php
│        │  │  ├─ Processor.php
│        │  │  ├─ PrototypedArrayNode.php
│        │  │  ├─ PrototypeNodeInterface.php
│        │  │  ├─ ScalarNode.php
│        │  │  ├─ StringNode.php
│        │  │  └─ VariableNode.php
│        │  ├─ Exception
│        │  │  ├─ FileLoaderImportCircularReferenceException.php
│        │  │  ├─ FileLocatorFileNotFoundException.php
│        │  │  ├─ LoaderLoadException.php
│        │  │  └─ LogicException.php
│        │  ├─ FileLocator.php
│        │  ├─ FileLocatorInterface.php
│        │  ├─ LICENSE
│        │  ├─ Loader
│        │  │  ├─ DelegatingLoader.php
│        │  │  ├─ DirectoryAwareLoaderInterface.php
│        │  │  ├─ FileLoader.php
│        │  │  ├─ GlobFileLoader.php
│        │  │  ├─ Loader.php
│        │  │  ├─ LoaderInterface.php
│        │  │  ├─ LoaderResolver.php
│        │  │  ├─ LoaderResolverInterface.php
│        │  │  └─ ParamConfigurator.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Resource
│        │  │  ├─ ClassExistenceResource.php
│        │  │  ├─ ComposerResource.php
│        │  │  ├─ DirectoryResource.php
│        │  │  ├─ FileExistenceResource.php
│        │  │  ├─ FileResource.php
│        │  │  ├─ GlobResource.php
│        │  │  ├─ ReflectionClassResource.php
│        │  │  ├─ ResourceInterface.php
│        │  │  ├─ SelfCheckingResourceChecker.php
│        │  │  ├─ SelfCheckingResourceInterface.php
│        │  │  └─ SkippingResourceChecker.php
│        │  ├─ ResourceCheckerConfigCache.php
│        │  ├─ ResourceCheckerConfigCacheFactory.php
│        │  ├─ ResourceCheckerInterface.php
│        │  ├─ Tests
│        │  │  ├─ Builder
│        │  │  │  ├─ Fixtures
│        │  │  │  │  ├─ AddToList
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        ├─ AddToList
│        │  │  │  │  │        │  ├─ Messenger
│        │  │  │  │  │        │  │  ├─ ReceivingConfig.php
│        │  │  │  │  │        │  │  └─ RoutingConfig.php
│        │  │  │  │  │        │  ├─ MessengerConfig.php
│        │  │  │  │  │        │  ├─ Translator
│        │  │  │  │  │        │  │  ├─ Books
│        │  │  │  │  │        │  │  │  └─ PageConfig.php
│        │  │  │  │  │        │  │  └─ BooksConfig.php
│        │  │  │  │  │        │  └─ TranslatorConfig.php
│        │  │  │  │  │        └─ AddToListConfig.php
│        │  │  │  │  ├─ AddToList.config.php
│        │  │  │  │  ├─ AddToList.output.php
│        │  │  │  │  ├─ AddToList.php
│        │  │  │  │  ├─ ArrayExtraKeys
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        ├─ ArrayExtraKeys
│        │  │  │  │  │        │  ├─ BarConfig.php
│        │  │  │  │  │        │  ├─ BazConfig.php
│        │  │  │  │  │        │  └─ FooConfig.php
│        │  │  │  │  │        └─ ArrayExtraKeysConfig.php
│        │  │  │  │  ├─ ArrayExtraKeys.config.php
│        │  │  │  │  ├─ ArrayExtraKeys.output.php
│        │  │  │  │  ├─ ArrayExtraKeys.php
│        │  │  │  │  ├─ NodeInitialValues
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        ├─ NodeInitialValues
│        │  │  │  │  │        │  ├─ Messenger
│        │  │  │  │  │        │  │  └─ TransportsConfig.php
│        │  │  │  │  │        │  ├─ MessengerConfig.php
│        │  │  │  │  │        │  └─ SomeCleverNameConfig.php
│        │  │  │  │  │        └─ NodeInitialValuesConfig.php
│        │  │  │  │  ├─ NodeInitialValues.config.php
│        │  │  │  │  ├─ NodeInitialValues.output.php
│        │  │  │  │  ├─ NodeInitialValues.php
│        │  │  │  │  ├─ Placeholders
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        └─ PlaceholdersConfig.php
│        │  │  │  │  ├─ Placeholders.config.php
│        │  │  │  │  ├─ Placeholders.output.php
│        │  │  │  │  ├─ Placeholders.php
│        │  │  │  │  ├─ PrimitiveTypes
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        └─ PrimitiveTypesConfig.php
│        │  │  │  │  ├─ PrimitiveTypes.config.php
│        │  │  │  │  ├─ PrimitiveTypes.output.php
│        │  │  │  │  ├─ PrimitiveTypes.php
│        │  │  │  │  ├─ ScalarNormalizedTypes
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        ├─ ScalarNormalizedTypes
│        │  │  │  │  │        │  ├─ KeyedListObjectConfig.php
│        │  │  │  │  │        │  ├─ ListObjectConfig.php
│        │  │  │  │  │        │  ├─ Nested
│        │  │  │  │  │        │  │  ├─ NestedListObjectConfig.php
│        │  │  │  │  │        │  │  └─ NestedObjectConfig.php
│        │  │  │  │  │        │  ├─ NestedConfig.php
│        │  │  │  │  │        │  └─ ObjectConfig.php
│        │  │  │  │  │        └─ ScalarNormalizedTypesConfig.php
│        │  │  │  │  ├─ ScalarNormalizedTypes.config.php
│        │  │  │  │  ├─ ScalarNormalizedTypes.output.php
│        │  │  │  │  ├─ ScalarNormalizedTypes.php
│        │  │  │  │  ├─ VariableType
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        └─ VariableTypeConfig.php
│        │  │  │  │  ├─ VariableType.config.php
│        │  │  │  │  ├─ VariableType.output.php
│        │  │  │  │  └─ VariableType.php
│        │  │  │  └─ GeneratedConfigTest.php
│        │  │  ├─ ConfigCacheFactoryTest.php
│        │  │  ├─ ConfigCacheTest.php
│        │  │  ├─ Definition
│        │  │  │  ├─ ArrayNodeTest.php
│        │  │  │  ├─ BaseNodeTest.php
│        │  │  │  ├─ BooleanNodeTest.php
│        │  │  │  ├─ Builder
│        │  │  │  │  ├─ ArrayNodeDefinitionTest.php
│        │  │  │  │  ├─ BooleanNodeDefinitionTest.php
│        │  │  │  │  ├─ EnumNodeDefinitionTest.php
│        │  │  │  │  ├─ ExprBuilderTest.php
│        │  │  │  │  ├─ NodeBuilderTest.php
│        │  │  │  │  ├─ NodeDefinitionTest.php
│        │  │  │  │  ├─ NumericNodeDefinitionTest.php
│        │  │  │  │  └─ TreeBuilderTest.php
│        │  │  │  ├─ Dumper
│        │  │  │  │  ├─ XmlReferenceDumperTest.php
│        │  │  │  │  └─ YamlReferenceDumperTest.php
│        │  │  │  ├─ EnumNodeTest.php
│        │  │  │  ├─ FinalizationTest.php
│        │  │  │  ├─ FloatNodeTest.php
│        │  │  │  ├─ IntegerNodeTest.php
│        │  │  │  ├─ Loader
│        │  │  │  │  └─ DefinitionFileLoaderTest.php
│        │  │  │  ├─ MergeTest.php
│        │  │  │  ├─ NormalizationTest.php
│        │  │  │  ├─ PrototypedArrayNodeTest.php
│        │  │  │  ├─ ScalarNodeTest.php
│        │  │  │  └─ StringNodeTest.php
│        │  │  ├─ Exception
│        │  │  │  └─ LoaderLoadExceptionTest.php
│        │  │  ├─ FileLocatorTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ Again
│        │  │  │  │  └─ foo.xml
│        │  │  │  ├─ BadFileName.php
│        │  │  │  ├─ BadParent.php
│        │  │  │  ├─ BarNode.php
│        │  │  │  ├─ Builder
│        │  │  │  │  ├─ BarNodeDefinition.php
│        │  │  │  │  ├─ NodeBuilder.php
│        │  │  │  │  └─ VariableNodeDefinition.php
│        │  │  │  ├─ Configuration
│        │  │  │  │  ├─ CustomNode.php
│        │  │  │  │  ├─ CustomNodeDefinition.php
│        │  │  │  │  └─ ExampleConfiguration.php
│        │  │  │  ├─ Exclude
│        │  │  │  │  ├─ AnExcludedFile.txt
│        │  │  │  │  └─ ExcludeToo
│        │  │  │  │     └─ AnotheExcludedFile.txt
│        │  │  │  ├─ ExcludeTrailingSlash
│        │  │  │  │  ├─ bar.txt
│        │  │  │  │  ├─ exclude
│        │  │  │  │  │  └─ baz.txt
│        │  │  │  │  └─ foo.txt
│        │  │  │  ├─ foo.xml
│        │  │  │  ├─ Include
│        │  │  │  │  ├─ ExcludeFile.txt
│        │  │  │  │  ├─ IncludeAnotherFile.txt
│        │  │  │  │  └─ IncludeFile.txt
│        │  │  │  ├─ IntegerBackedTestEnum.php
│        │  │  │  ├─ Loader
│        │  │  │  │  └─ node_simple.php
│        │  │  │  ├─ ParseError.php
│        │  │  │  ├─ Resource
│        │  │  │  │  ├─ .hiddenFile
│        │  │  │  │  └─ ConditionalClass.php
│        │  │  │  ├─ some.phar
│        │  │  │  ├─ StringBackedTestEnum.php
│        │  │  │  ├─ StringBackedTestEnum2.php
│        │  │  │  ├─ TestEnum.php
│        │  │  │  ├─ TestEnum2.php
│        │  │  │  └─ Util
│        │  │  │     ├─ document_type.xml
│        │  │  │     ├─ invalid.xml
│        │  │  │     ├─ invalid_schema.xml
│        │  │  │     ├─ not_readable.xml
│        │  │  │     ├─ schema.xsd
│        │  │  │     └─ valid.xml
│        │  │  ├─ Loader
│        │  │  │  ├─ DelegatingLoaderTest.php
│        │  │  │  ├─ FileLoaderTest.php
│        │  │  │  ├─ LoaderResolverTest.php
│        │  │  │  └─ LoaderTest.php
│        │  │  ├─ Resource
│        │  │  │  ├─ ClassExistenceResourceTest.php
│        │  │  │  ├─ ComposerResourceTest.php
│        │  │  │  ├─ DirectoryResourceTest.php
│        │  │  │  ├─ FileExistenceResourceTest.php
│        │  │  │  ├─ FileResourceTest.php
│        │  │  │  ├─ GlobResourceTest.php
│        │  │  │  ├─ ReflectionClassResourceTest.php
│        │  │  │  └─ ResourceStub.php
│        │  │  ├─ ResourceCheckerConfigCacheTest.php
│        │  │  └─ Util
│        │  │     └─ XmlUtilsTest.php
│        │  └─ Util
│        │     ├─ Exception
│        │     │  ├─ InvalidXmlException.php
│        │     │  └─ XmlParsingException.php
│        │     └─ XmlUtils.php
│        ├─ console
│        │  ├─ Application.php
│        │  ├─ Attribute
│        │  │  ├─ Argument.php
│        │  │  ├─ AsCommand.php
│        │  │  └─ Option.php
│        │  ├─ CHANGELOG.md
│        │  ├─ CI
│        │  │  └─ GithubActionReporter.php
│        │  ├─ Color.php
│        │  ├─ Command
│        │  │  ├─ Command.php
│        │  │  ├─ CompleteCommand.php
│        │  │  ├─ DumpCompletionCommand.php
│        │  │  ├─ HelpCommand.php
│        │  │  ├─ InvokableCommand.php
│        │  │  ├─ LazyCommand.php
│        │  │  ├─ ListCommand.php
│        │  │  ├─ LockableTrait.php
│        │  │  ├─ SignalableCommandInterface.php
│        │  │  └─ TraceableCommand.php
│        │  ├─ CommandLoader
│        │  │  ├─ CommandLoaderInterface.php
│        │  │  ├─ ContainerCommandLoader.php
│        │  │  └─ FactoryCommandLoader.php
│        │  ├─ Completion
│        │  │  ├─ CompletionInput.php
│        │  │  ├─ CompletionSuggestions.php
│        │  │  ├─ Output
│        │  │  │  ├─ BashCompletionOutput.php
│        │  │  │  ├─ CompletionOutputInterface.php
│        │  │  │  ├─ FishCompletionOutput.php
│        │  │  │  └─ ZshCompletionOutput.php
│        │  │  └─ Suggestion.php
│        │  ├─ composer.json
│        │  ├─ ConsoleEvents.php
│        │  ├─ Cursor.php
│        │  ├─ DataCollector
│        │  │  └─ CommandDataCollector.php
│        │  ├─ Debug
│        │  │  └─ CliRequest.php
│        │  ├─ DependencyInjection
│        │  │  └─ AddConsoleCommandPass.php
│        │  ├─ Descriptor
│        │  │  ├─ ApplicationDescription.php
│        │  │  ├─ Descriptor.php
│        │  │  ├─ DescriptorInterface.php
│        │  │  ├─ JsonDescriptor.php
│        │  │  ├─ MarkdownDescriptor.php
│        │  │  ├─ ReStructuredTextDescriptor.php
│        │  │  ├─ TextDescriptor.php
│        │  │  └─ XmlDescriptor.php
│        │  ├─ Event
│        │  │  ├─ ConsoleAlarmEvent.php
│        │  │  ├─ ConsoleCommandEvent.php
│        │  │  ├─ ConsoleErrorEvent.php
│        │  │  ├─ ConsoleEvent.php
│        │  │  ├─ ConsoleSignalEvent.php
│        │  │  └─ ConsoleTerminateEvent.php
│        │  ├─ EventListener
│        │  │  └─ ErrorListener.php
│        │  ├─ Exception
│        │  │  ├─ CommandNotFoundException.php
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ InvalidArgumentException.php
│        │  │  ├─ InvalidOptionException.php
│        │  │  ├─ LogicException.php
│        │  │  ├─ MissingInputException.php
│        │  │  ├─ NamespaceNotFoundException.php
│        │  │  ├─ RunCommandFailedException.php
│        │  │  └─ RuntimeException.php
│        │  ├─ Formatter
│        │  │  ├─ NullOutputFormatter.php
│        │  │  ├─ NullOutputFormatterStyle.php
│        │  │  ├─ OutputFormatter.php
│        │  │  ├─ OutputFormatterInterface.php
│        │  │  ├─ OutputFormatterStyle.php
│        │  │  ├─ OutputFormatterStyleInterface.php
│        │  │  ├─ OutputFormatterStyleStack.php
│        │  │  └─ WrappableOutputFormatterInterface.php
│        │  ├─ Helper
│        │  │  ├─ DebugFormatterHelper.php
│        │  │  ├─ DescriptorHelper.php
│        │  │  ├─ Dumper.php
│        │  │  ├─ FormatterHelper.php
│        │  │  ├─ Helper.php
│        │  │  ├─ HelperInterface.php
│        │  │  ├─ HelperSet.php
│        │  │  ├─ InputAwareHelper.php
│        │  │  ├─ OutputWrapper.php
│        │  │  ├─ ProcessHelper.php
│        │  │  ├─ ProgressBar.php
│        │  │  ├─ ProgressIndicator.php
│        │  │  ├─ QuestionHelper.php
│        │  │  ├─ SymfonyQuestionHelper.php
│        │  │  ├─ Table.php
│        │  │  ├─ TableCell.php
│        │  │  ├─ TableCellStyle.php
│        │  │  ├─ TableRows.php
│        │  │  ├─ TableSeparator.php
│        │  │  ├─ TableStyle.php
│        │  │  ├─ TreeHelper.php
│        │  │  ├─ TreeNode.php
│        │  │  └─ TreeStyle.php
│        │  ├─ Input
│        │  │  ├─ ArgvInput.php
│        │  │  ├─ ArrayInput.php
│        │  │  ├─ Input.php
│        │  │  ├─ InputArgument.php
│        │  │  ├─ InputAwareInterface.php
│        │  │  ├─ InputDefinition.php
│        │  │  ├─ InputInterface.php
│        │  │  ├─ InputOption.php
│        │  │  ├─ StreamableInputInterface.php
│        │  │  └─ StringInput.php
│        │  ├─ LICENSE
│        │  ├─ Logger
│        │  │  └─ ConsoleLogger.php
│        │  ├─ Messenger
│        │  │  ├─ RunCommandContext.php
│        │  │  ├─ RunCommandMessage.php
│        │  │  └─ RunCommandMessageHandler.php
│        │  ├─ Output
│        │  │  ├─ AnsiColorMode.php
│        │  │  ├─ BufferedOutput.php
│        │  │  ├─ ConsoleOutput.php
│        │  │  ├─ ConsoleOutputInterface.php
│        │  │  ├─ ConsoleSectionOutput.php
│        │  │  ├─ NullOutput.php
│        │  │  ├─ Output.php
│        │  │  ├─ OutputInterface.php
│        │  │  ├─ StreamOutput.php
│        │  │  └─ TrimmedBufferOutput.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ Question
│        │  │  ├─ ChoiceQuestion.php
│        │  │  ├─ ConfirmationQuestion.php
│        │  │  └─ Question.php
│        │  ├─ README.md
│        │  ├─ Resources
│        │  │  ├─ bin
│        │  │  │  └─ hiddeninput.exe
│        │  │  ├─ completion.bash
│        │  │  ├─ completion.fish
│        │  │  └─ completion.zsh
│        │  ├─ SignalRegistry
│        │  │  ├─ SignalMap.php
│        │  │  └─ SignalRegistry.php
│        │  ├─ SingleCommandApplication.php
│        │  ├─ Style
│        │  │  ├─ OutputStyle.php
│        │  │  ├─ StyleInterface.php
│        │  │  └─ SymfonyStyle.php
│        │  ├─ Terminal.php
│        │  ├─ Tester
│        │  │  ├─ ApplicationTester.php
│        │  │  ├─ CommandCompletionTester.php
│        │  │  ├─ CommandTester.php
│        │  │  ├─ Constraint
│        │  │  │  └─ CommandIsSuccessful.php
│        │  │  └─ TesterTrait.php
│        │  └─ Tests
│        │     ├─ ApplicationTest.php
│        │     ├─ CI
│        │     │  └─ GithubActionReporterTest.php
│        │     ├─ ColorTest.php
│        │     ├─ Command
│        │     │  ├─ CommandTest.php
│        │     │  ├─ CompleteCommandTest.php
│        │     │  ├─ DumpCompletionCommandTest.php
│        │     │  ├─ HelpCommandTest.php
│        │     │  ├─ InvokableCommandTest.php
│        │     │  ├─ ListCommandTest.php
│        │     │  ├─ LockableTraitTest.php
│        │     │  └─ SingleCommandApplicationTest.php
│        │     ├─ CommandLoader
│        │     │  ├─ ContainerCommandLoaderTest.php
│        │     │  └─ FactoryCommandLoaderTest.php
│        │     ├─ Completion
│        │     │  ├─ CompletionInputTest.php
│        │     │  └─ Output
│        │     │     ├─ BashCompletionOutputTest.php
│        │     │     ├─ CompletionOutputTestCase.php
│        │     │     ├─ FishCompletionOutputTest.php
│        │     │     └─ ZshCompletionOutputTest.php
│        │     ├─ ConsoleEventsTest.php
│        │     ├─ CursorTest.php
│        │     ├─ DependencyInjection
│        │     │  └─ AddConsoleCommandPassTest.php
│        │     ├─ Descriptor
│        │     │  ├─ AbstractDescriptorTestCase.php
│        │     │  ├─ ApplicationDescriptionTest.php
│        │     │  ├─ JsonDescriptorTest.php
│        │     │  ├─ MarkdownDescriptorTest.php
│        │     │  ├─ ObjectsProvider.php
│        │     │  ├─ ReStructuredTextDescriptorTest.php
│        │     │  ├─ TextDescriptorTest.php
│        │     │  └─ XmlDescriptorTest.php
│        │     ├─ EventListener
│        │     │  └─ ErrorListenerTest.php
│        │     ├─ Fixtures
│        │     │  ├─ application.dont_run_alternative_namespace_name.txt
│        │     │  ├─ application_1.json
│        │     │  ├─ application_1.md
│        │     │  ├─ application_1.rst
│        │     │  ├─ application_1.txt
│        │     │  ├─ application_1.xml
│        │     │  ├─ application_2.json
│        │     │  ├─ application_2.md
│        │     │  ├─ application_2.rst
│        │     │  ├─ application_2.txt
│        │     │  ├─ application_2.xml
│        │     │  ├─ application_filtered_namespace.txt
│        │     │  ├─ application_gethelp.txt
│        │     │  ├─ application_mbstring.md
│        │     │  ├─ application_mbstring.rst
│        │     │  ├─ application_mbstring.txt
│        │     │  ├─ application_renderexception1.txt
│        │     │  ├─ application_renderexception2.txt
│        │     │  ├─ application_renderexception3.txt
│        │     │  ├─ application_renderexception3decorated.txt
│        │     │  ├─ application_renderexception4.txt
│        │     │  ├─ application_renderexception_doublewidth1.txt
│        │     │  ├─ application_renderexception_doublewidth1decorated.txt
│        │     │  ├─ application_renderexception_doublewidth2.txt
│        │     │  ├─ application_renderexception_escapeslines.txt
│        │     │  ├─ application_renderexception_linebreaks.txt
│        │     │  ├─ application_rendersynopsis_escapesline.txt
│        │     │  ├─ application_run1.txt
│        │     │  ├─ application_run2.txt
│        │     │  ├─ application_run3.txt
│        │     │  ├─ application_run4.txt
│        │     │  ├─ application_run5.txt
│        │     │  ├─ application_signalable.php
│        │     │  ├─ BarBucCommand.php
│        │     │  ├─ BarHiddenCommand.php
│        │     │  ├─ command_1.json
│        │     │  ├─ command_1.md
│        │     │  ├─ command_1.rst
│        │     │  ├─ command_1.txt
│        │     │  ├─ command_1.xml
│        │     │  ├─ command_2.json
│        │     │  ├─ command_2.md
│        │     │  ├─ command_2.rst
│        │     │  ├─ command_2.txt
│        │     │  ├─ command_2.xml
│        │     │  ├─ command_mbstring.md
│        │     │  ├─ command_mbstring.rst
│        │     │  ├─ command_mbstring.txt
│        │     │  ├─ DescriptorApplication1.php
│        │     │  ├─ DescriptorApplication2.php
│        │     │  ├─ DescriptorApplicationMbString.php
│        │     │  ├─ DescriptorCommand1.php
│        │     │  ├─ DescriptorCommand2.php
│        │     │  ├─ DescriptorCommand3.php
│        │     │  ├─ DescriptorCommand4.php
│        │     │  ├─ DescriptorCommandMbString.php
│        │     │  ├─ DummyOutput.php
│        │     │  ├─ Foo1Command.php
│        │     │  ├─ Foo2Command.php
│        │     │  ├─ Foo3Command.php
│        │     │  ├─ Foo4Command.php
│        │     │  ├─ Foo5Command.php
│        │     │  ├─ Foo6Command.php
│        │     │  ├─ FoobarCommand.php
│        │     │  ├─ FooCommand.php
│        │     │  ├─ FooHiddenCommand.php
│        │     │  ├─ FooLock2Command.php
│        │     │  ├─ FooLock3Command.php
│        │     │  ├─ FooLock4InvokableCommand.php
│        │     │  ├─ FooLockCommand.php
│        │     │  ├─ FooOptCommand.php
│        │     │  ├─ FooSameCaseLowercaseCommand.php
│        │     │  ├─ FooSameCaseUppercaseCommand.php
│        │     │  ├─ FooSubnamespaced1Command.php
│        │     │  ├─ FooSubnamespaced2Command.php
│        │     │  ├─ FooWithoutAliasCommand.php
│        │     │  ├─ input_argument_1.json
│        │     │  ├─ input_argument_1.md
│        │     │  ├─ input_argument_1.rst
│        │     │  ├─ input_argument_1.txt
│        │     │  ├─ input_argument_1.xml
│        │     │  ├─ input_argument_2.json
│        │     │  ├─ input_argument_2.md
│        │     │  ├─ input_argument_2.rst
│        │     │  ├─ input_argument_2.txt
│        │     │  ├─ input_argument_2.xml
│        │     │  ├─ input_argument_3.json
│        │     │  ├─ input_argument_3.md
│        │     │  ├─ input_argument_3.rst
│        │     │  ├─ input_argument_3.txt
│        │     │  ├─ input_argument_3.xml
│        │     │  ├─ input_argument_4.json
│        │     │  ├─ input_argument_4.md
│        │     │  ├─ input_argument_4.rst
│        │     │  ├─ input_argument_4.txt
│        │     │  ├─ input_argument_4.xml
│        │     │  ├─ input_argument_with_default_inf_value.json
│        │     │  ├─ input_argument_with_default_inf_value.md
│        │     │  ├─ input_argument_with_default_inf_value.rst
│        │     │  ├─ input_argument_with_default_inf_value.txt
│        │     │  ├─ input_argument_with_default_inf_value.xml
│        │     │  ├─ input_argument_with_style.json
│        │     │  ├─ input_argument_with_style.md
│        │     │  ├─ input_argument_with_style.rst
│        │     │  ├─ input_argument_with_style.txt
│        │     │  ├─ input_argument_with_style.xml
│        │     │  ├─ input_definition_1.json
│        │     │  ├─ input_definition_1.md
│        │     │  ├─ input_definition_1.rst
│        │     │  ├─ input_definition_1.txt
│        │     │  ├─ input_definition_1.xml
│        │     │  ├─ input_definition_2.json
│        │     │  ├─ input_definition_2.md
│        │     │  ├─ input_definition_2.rst
│        │     │  ├─ input_definition_2.txt
│        │     │  ├─ input_definition_2.xml
│        │     │  ├─ input_definition_3.json
│        │     │  ├─ input_definition_3.md
│        │     │  ├─ input_definition_3.rst
│        │     │  ├─ input_definition_3.txt
│        │     │  ├─ input_definition_3.xml
│        │     │  ├─ input_definition_4.json
│        │     │  ├─ input_definition_4.md
│        │     │  ├─ input_definition_4.rst
│        │     │  ├─ input_definition_4.txt
│        │     │  ├─ input_definition_4.xml
│        │     │  ├─ input_option_1.json
│        │     │  ├─ input_option_1.md
│        │     │  ├─ input_option_1.rst
│        │     │  ├─ input_option_1.txt
│        │     │  ├─ input_option_1.xml
│        │     │  ├─ input_option_2.json
│        │     │  ├─ input_option_2.md
│        │     │  ├─ input_option_2.rst
│        │     │  ├─ input_option_2.txt
│        │     │  ├─ input_option_2.xml
│        │     │  ├─ input_option_3.json
│        │     │  ├─ input_option_3.md
│        │     │  ├─ input_option_3.rst
│        │     │  ├─ input_option_3.txt
│        │     │  ├─ input_option_3.xml
│        │     │  ├─ input_option_4.json
│        │     │  ├─ input_option_4.md
│        │     │  ├─ input_option_4.rst
│        │     │  ├─ input_option_4.txt
│        │     │  ├─ input_option_4.xml
│        │     │  ├─ input_option_5.json
│        │     │  ├─ input_option_5.md
│        │     │  ├─ input_option_5.rst
│        │     │  ├─ input_option_5.txt
│        │     │  ├─ input_option_5.xml
│        │     │  ├─ input_option_6.json
│        │     │  ├─ input_option_6.md
│        │     │  ├─ input_option_6.rst
│        │     │  ├─ input_option_6.txt
│        │     │  ├─ input_option_6.xml
│        │     │  ├─ input_option_with_default_inf_value.json
│        │     │  ├─ input_option_with_default_inf_value.md
│        │     │  ├─ input_option_with_default_inf_value.rst
│        │     │  ├─ input_option_with_default_inf_value.txt
│        │     │  ├─ input_option_with_default_inf_value.xml
│        │     │  ├─ input_option_with_style.json
│        │     │  ├─ input_option_with_style.md
│        │     │  ├─ input_option_with_style.rst
│        │     │  ├─ input_option_with_style.txt
│        │     │  ├─ input_option_with_style.xml
│        │     │  ├─ input_option_with_style_array.json
│        │     │  ├─ input_option_with_style_array.md
│        │     │  ├─ input_option_with_style_array.rst
│        │     │  ├─ input_option_with_style_array.txt
│        │     │  ├─ input_option_with_style_array.xml
│        │     │  ├─ MockableAppliationWithTerminalWidth.php
│        │     │  ├─ stream_output_file.txt
│        │     │  ├─ Style
│        │     │  │  └─ SymfonyStyle
│        │     │  │     ├─ command
│        │     │  │     │  ├─ command_0.php
│        │     │  │     │  ├─ command_1.php
│        │     │  │     │  ├─ command_10.php
│        │     │  │     │  ├─ command_11.php
│        │     │  │     │  ├─ command_12.php
│        │     │  │     │  ├─ command_13.php
│        │     │  │     │  ├─ command_14.php
│        │     │  │     │  ├─ command_15.php
│        │     │  │     │  ├─ command_16.php
│        │     │  │     │  ├─ command_17.php
│        │     │  │     │  ├─ command_18.php
│        │     │  │     │  ├─ command_19.php
│        │     │  │     │  ├─ command_2.php
│        │     │  │     │  ├─ command_20.php
│        │     │  │     │  ├─ command_21.php
│        │     │  │     │  ├─ command_22.php
│        │     │  │     │  ├─ command_23.php
│        │     │  │     │  ├─ command_3.php
│        │     │  │     │  ├─ command_4.php
│        │     │  │     │  ├─ command_4_with_iterators.php
│        │     │  │     │  ├─ command_5.php
│        │     │  │     │  ├─ command_6.php
│        │     │  │     │  ├─ command_7.php
│        │     │  │     │  ├─ command_8.php
│        │     │  │     │  ├─ command_9.php
│        │     │  │     │  └─ interactive_command_1.php
│        │     │  │     ├─ output
│        │     │  │     │  ├─ interactive_output_1.txt
│        │     │  │     │  ├─ output_0.txt
│        │     │  │     │  ├─ output_1.txt
│        │     │  │     │  ├─ output_10.txt
│        │     │  │     │  ├─ output_11.txt
│        │     │  │     │  ├─ output_12.txt
│        │     │  │     │  ├─ output_13.txt
│        │     │  │     │  ├─ output_14.txt
│        │     │  │     │  ├─ output_15.txt
│        │     │  │     │  ├─ output_16.txt
│        │     │  │     │  ├─ output_17.txt
│        │     │  │     │  ├─ output_18.txt
│        │     │  │     │  ├─ output_19.txt
│        │     │  │     │  ├─ output_2.txt
│        │     │  │     │  ├─ output_20.txt
│        │     │  │     │  ├─ output_21.txt
│        │     │  │     │  ├─ output_22.txt
│        │     │  │     │  ├─ output_23.txt
│        │     │  │     │  ├─ output_3.txt
│        │     │  │     │  ├─ output_4.txt
│        │     │  │     │  ├─ output_4_with_iterators.txt
│        │     │  │     │  ├─ output_5.txt
│        │     │  │     │  ├─ output_6.txt
│        │     │  │     │  ├─ output_7.txt
│        │     │  │     │  ├─ output_8.txt
│        │     │  │     │  └─ output_9.txt
│        │     │  │     └─ progress
│        │     │  │        ├─ command_progress_iterate.php
│        │     │  │        ├─ output_progress_iterate_no_shade.txt
│        │     │  │        └─ output_progress_iterate_shade.txt
│        │     │  ├─ TestAmbiguousCommandRegistering.php
│        │     │  ├─ TestAmbiguousCommandRegistering2.php
│        │     │  └─ TestCommand.php
│        │     ├─ Formatter
│        │     │  ├─ NullOutputFormatterStyleTest.php
│        │     │  ├─ NullOutputFormatterTest.php
│        │     │  ├─ OutputFormatterStyleStackTest.php
│        │     │  ├─ OutputFormatterStyleTest.php
│        │     │  └─ OutputFormatterTest.php
│        │     ├─ Helper
│        │     │  ├─ AbstractQuestionHelperTestCase.php
│        │     │  ├─ DescriptorHelperTest.php
│        │     │  ├─ DumperNativeFallbackTest.php
│        │     │  ├─ DumperTest.php
│        │     │  ├─ FormatterHelperTest.php
│        │     │  ├─ HelperSetTest.php
│        │     │  ├─ HelperTest.php
│        │     │  ├─ OutputWrapperTest.php
│        │     │  ├─ ProcessHelperTest.php
│        │     │  ├─ ProgressBarTest.php
│        │     │  ├─ ProgressIndicatorTest.php
│        │     │  ├─ QuestionHelperTest.php
│        │     │  ├─ SymfonyQuestionHelperTest.php
│        │     │  ├─ TableCellStyleTest.php
│        │     │  ├─ TableStyleTest.php
│        │     │  ├─ TableTest.php
│        │     │  ├─ TreeHelperTest.php
│        │     │  ├─ TreeNodeTest.php
│        │     │  └─ TreeStyleTest.php
│        │     ├─ Input
│        │     │  ├─ ArgvInputTest.php
│        │     │  ├─ ArrayInputTest.php
│        │     │  ├─ InputArgumentTest.php
│        │     │  ├─ InputDefinitionTest.php
│        │     │  ├─ InputOptionTest.php
│        │     │  ├─ InputTest.php
│        │     │  └─ StringInputTest.php
│        │     ├─ Logger
│        │     │  └─ ConsoleLoggerTest.php
│        │     ├─ Messenger
│        │     │  └─ RunCommandMessageHandlerTest.php
│        │     ├─ Output
│        │     │  ├─ AnsiColorModeTest.php
│        │     │  ├─ ConsoleOutputTest.php
│        │     │  ├─ ConsoleSectionOutputTest.php
│        │     │  ├─ NullOutputTest.php
│        │     │  ├─ OutputTest.php
│        │     │  └─ StreamOutputTest.php
│        │     ├─ phpt
│        │     │  ├─ alarm
│        │     │  │  └─ command_exit.phpt
│        │     │  ├─ signal
│        │     │  │  └─ command_exit.phpt
│        │     │  ├─ single_application
│        │     │  │  ├─ arg.phpt
│        │     │  │  ├─ default.phpt
│        │     │  │  ├─ help_name.phpt
│        │     │  │  ├─ version_default_name.phpt
│        │     │  │  └─ version_name.phpt
│        │     │  └─ uses_stdin_as_interactive_input.phpt
│        │     ├─ Question
│        │     │  ├─ ChoiceQuestionTest.php
│        │     │  ├─ ConfirmationQuestionTest.php
│        │     │  └─ QuestionTest.php
│        │     ├─ SignalRegistry
│        │     │  ├─ SignalMapTest.php
│        │     │  └─ SignalRegistryTest.php
│        │     ├─ Style
│        │     │  └─ SymfonyStyleTest.php
│        │     ├─ TerminalTest.php
│        │     └─ Tester
│        │        ├─ ApplicationTesterTest.php
│        │        ├─ CommandTesterTest.php
│        │        └─ Constraint
│        │           └─ CommandIsSuccessfulTest.php
│        ├─ dependency-injection
│        │  ├─ Alias.php
│        │  ├─ Argument
│        │  │  ├─ AbstractArgument.php
│        │  │  ├─ ArgumentInterface.php
│        │  │  ├─ BoundArgument.php
│        │  │  ├─ IteratorArgument.php
│        │  │  ├─ LazyClosure.php
│        │  │  ├─ RewindableGenerator.php
│        │  │  ├─ ServiceClosureArgument.php
│        │  │  ├─ ServiceLocator.php
│        │  │  ├─ ServiceLocatorArgument.php
│        │  │  └─ TaggedIteratorArgument.php
│        │  ├─ Attribute
│        │  │  ├─ AsAlias.php
│        │  │  ├─ AsDecorator.php
│        │  │  ├─ AsTaggedItem.php
│        │  │  ├─ Autoconfigure.php
│        │  │  ├─ AutoconfigureTag.php
│        │  │  ├─ Autowire.php
│        │  │  ├─ AutowireCallable.php
│        │  │  ├─ AutowireDecorated.php
│        │  │  ├─ AutowireInline.php
│        │  │  ├─ AutowireIterator.php
│        │  │  ├─ AutowireLocator.php
│        │  │  ├─ AutowireMethodOf.php
│        │  │  ├─ AutowireServiceClosure.php
│        │  │  ├─ Exclude.php
│        │  │  ├─ Lazy.php
│        │  │  ├─ TaggedIterator.php
│        │  │  ├─ TaggedLocator.php
│        │  │  ├─ Target.php
│        │  │  ├─ When.php
│        │  │  └─ WhenNot.php
│        │  ├─ CHANGELOG.md
│        │  ├─ ChildDefinition.php
│        │  ├─ Compiler
│        │  │  ├─ AbstractRecursivePass.php
│        │  │  ├─ AliasDeprecatedPublicServicesPass.php
│        │  │  ├─ AnalyzeServiceReferencesPass.php
│        │  │  ├─ AttributeAutoconfigurationPass.php
│        │  │  ├─ AutoAliasServicePass.php
│        │  │  ├─ AutowireAsDecoratorPass.php
│        │  │  ├─ AutowirePass.php
│        │  │  ├─ AutowireRequiredMethodsPass.php
│        │  │  ├─ AutowireRequiredPropertiesPass.php
│        │  │  ├─ CheckAliasValidityPass.php
│        │  │  ├─ CheckArgumentsValidityPass.php
│        │  │  ├─ CheckCircularReferencesPass.php
│        │  │  ├─ CheckDefinitionValidityPass.php
│        │  │  ├─ CheckExceptionOnInvalidReferenceBehaviorPass.php
│        │  │  ├─ CheckReferenceValidityPass.php
│        │  │  ├─ CheckTypeDeclarationsPass.php
│        │  │  ├─ Compiler.php
│        │  │  ├─ CompilerPassInterface.php
│        │  │  ├─ DecoratorServicePass.php
│        │  │  ├─ DefinitionErrorExceptionPass.php
│        │  │  ├─ ExtensionCompilerPass.php
│        │  │  ├─ InlineServiceDefinitionsPass.php
│        │  │  ├─ MergeExtensionConfigurationPass.php
│        │  │  ├─ PassConfig.php
│        │  │  ├─ PriorityTaggedServiceTrait.php
│        │  │  ├─ RegisterAutoconfigureAttributesPass.php
│        │  │  ├─ RegisterEnvVarProcessorsPass.php
│        │  │  ├─ RegisterReverseContainerPass.php
│        │  │  ├─ RegisterServiceSubscribersPass.php
│        │  │  ├─ RemoveAbstractDefinitionsPass.php
│        │  │  ├─ RemoveBuildParametersPass.php
│        │  │  ├─ RemovePrivateAliasesPass.php
│        │  │  ├─ RemoveUnusedDefinitionsPass.php
│        │  │  ├─ ReplaceAliasByActualDefinitionPass.php
│        │  │  ├─ ResolveAutowireInlineAttributesPass.php
│        │  │  ├─ ResolveBindingsPass.php
│        │  │  ├─ ResolveChildDefinitionsPass.php
│        │  │  ├─ ResolveClassPass.php
│        │  │  ├─ ResolveDecoratorStackPass.php
│        │  │  ├─ ResolveEnvPlaceholdersPass.php
│        │  │  ├─ ResolveFactoryClassPass.php
│        │  │  ├─ ResolveHotPathPass.php
│        │  │  ├─ ResolveInstanceofConditionalsPass.php
│        │  │  ├─ ResolveInvalidReferencesPass.php
│        │  │  ├─ ResolveNamedArgumentsPass.php
│        │  │  ├─ ResolveNoPreloadPass.php
│        │  │  ├─ ResolveParameterPlaceHoldersPass.php
│        │  │  ├─ ResolveReferencesToAliasesPass.php
│        │  │  ├─ ResolveServiceSubscribersPass.php
│        │  │  ├─ ResolveTaggedIteratorArgumentPass.php
│        │  │  ├─ ServiceLocatorTagPass.php
│        │  │  ├─ ServiceReferenceGraph.php
│        │  │  ├─ ServiceReferenceGraphEdge.php
│        │  │  ├─ ServiceReferenceGraphNode.php
│        │  │  └─ ValidateEnvPlaceholdersPass.php
│        │  ├─ composer.json
│        │  ├─ Config
│        │  │  ├─ ContainerParametersResource.php
│        │  │  └─ ContainerParametersResourceChecker.php
│        │  ├─ Container.php
│        │  ├─ ContainerBuilder.php
│        │  ├─ ContainerInterface.php
│        │  ├─ Definition.php
│        │  ├─ Dumper
│        │  │  ├─ Dumper.php
│        │  │  ├─ DumperInterface.php
│        │  │  ├─ GraphvizDumper.php
│        │  │  ├─ PhpDumper.php
│        │  │  ├─ Preloader.php
│        │  │  ├─ XmlDumper.php
│        │  │  └─ YamlDumper.php
│        │  ├─ EnvVarLoaderInterface.php
│        │  ├─ EnvVarProcessor.php
│        │  ├─ EnvVarProcessorInterface.php
│        │  ├─ Exception
│        │  │  ├─ AutoconfigureFailedException.php
│        │  │  ├─ AutowiringFailedException.php
│        │  │  ├─ BadMethodCallException.php
│        │  │  ├─ EmptyParameterValueException.php
│        │  │  ├─ EnvNotFoundException.php
│        │  │  ├─ EnvParameterException.php
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ InvalidArgumentException.php
│        │  │  ├─ InvalidParameterTypeException.php
│        │  │  ├─ LogicException.php
│        │  │  ├─ OutOfBoundsException.php
│        │  │  ├─ ParameterCircularReferenceException.php
│        │  │  ├─ ParameterNotFoundException.php
│        │  │  ├─ RuntimeException.php
│        │  │  ├─ ServiceCircularReferenceException.php
│        │  │  └─ ServiceNotFoundException.php
│        │  ├─ ExpressionLanguage.php
│        │  ├─ ExpressionLanguageProvider.php
│        │  ├─ Extension
│        │  │  ├─ AbstractExtension.php
│        │  │  ├─ ConfigurableExtensionInterface.php
│        │  │  ├─ ConfigurationExtensionInterface.php
│        │  │  ├─ Extension.php
│        │  │  ├─ ExtensionInterface.php
│        │  │  ├─ ExtensionTrait.php
│        │  │  └─ PrependExtensionInterface.php
│        │  ├─ LazyProxy
│        │  │  ├─ Instantiator
│        │  │  │  ├─ InstantiatorInterface.php
│        │  │  │  ├─ LazyServiceInstantiator.php
│        │  │  │  └─ RealServiceInstantiator.php
│        │  │  └─ PhpDumper
│        │  │     ├─ DumperInterface.php
│        │  │     ├─ LazyServiceDumper.php
│        │  │     └─ NullDumper.php
│        │  ├─ LICENSE
│        │  ├─ Loader
│        │  │  ├─ ClosureLoader.php
│        │  │  ├─ Configurator
│        │  │  │  ├─ AbstractConfigurator.php
│        │  │  │  ├─ AbstractServiceConfigurator.php
│        │  │  │  ├─ AliasConfigurator.php
│        │  │  │  ├─ ClosureReferenceConfigurator.php
│        │  │  │  ├─ ContainerConfigurator.php
│        │  │  │  ├─ DefaultsConfigurator.php
│        │  │  │  ├─ EnvConfigurator.php
│        │  │  │  ├─ FromCallableConfigurator.php
│        │  │  │  ├─ InlineServiceConfigurator.php
│        │  │  │  ├─ InstanceofConfigurator.php
│        │  │  │  ├─ ParametersConfigurator.php
│        │  │  │  ├─ PrototypeConfigurator.php
│        │  │  │  ├─ ReferenceConfigurator.php
│        │  │  │  ├─ ServiceConfigurator.php
│        │  │  │  ├─ ServicesConfigurator.php
│        │  │  │  └─ Traits
│        │  │  │     ├─ AbstractTrait.php
│        │  │  │     ├─ ArgumentTrait.php
│        │  │  │     ├─ AutoconfigureTrait.php
│        │  │  │     ├─ AutowireTrait.php
│        │  │  │     ├─ BindTrait.php
│        │  │  │     ├─ CallTrait.php
│        │  │  │     ├─ ClassTrait.php
│        │  │  │     ├─ ConfiguratorTrait.php
│        │  │  │     ├─ ConstructorTrait.php
│        │  │  │     ├─ DecorateTrait.php
│        │  │  │     ├─ DeprecateTrait.php
│        │  │  │     ├─ FactoryTrait.php
│        │  │  │     ├─ FileTrait.php
│        │  │  │     ├─ FromCallableTrait.php
│        │  │  │     ├─ LazyTrait.php
│        │  │  │     ├─ ParentTrait.php
│        │  │  │     ├─ PropertyTrait.php
│        │  │  │     ├─ PublicTrait.php
│        │  │  │     ├─ ShareTrait.php
│        │  │  │     ├─ SyntheticTrait.php
│        │  │  │     └─ TagTrait.php
│        │  │  ├─ DirectoryLoader.php
│        │  │  ├─ FileLoader.php
│        │  │  ├─ GlobFileLoader.php
│        │  │  ├─ IniFileLoader.php
│        │  │  ├─ PhpFileLoader.php
│        │  │  ├─ schema
│        │  │  │  └─ dic
│        │  │  │     └─ services
│        │  │  │        └─ services-1.0.xsd
│        │  │  ├─ UndefinedExtensionHandler.php
│        │  │  ├─ XmlFileLoader.php
│        │  │  └─ YamlFileLoader.php
│        │  ├─ Parameter.php
│        │  ├─ ParameterBag
│        │  │  ├─ ContainerBag.php
│        │  │  ├─ ContainerBagInterface.php
│        │  │  ├─ EnvPlaceholderParameterBag.php
│        │  │  ├─ FrozenParameterBag.php
│        │  │  ├─ ParameterBag.php
│        │  │  └─ ParameterBagInterface.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Reference.php
│        │  ├─ ReverseContainer.php
│        │  ├─ ServiceLocator.php
│        │  ├─ StaticEnvVarLoader.php
│        │  ├─ TaggedContainerInterface.php
│        │  ├─ Tests
│        │  │  ├─ AliasTest.php
│        │  │  ├─ Argument
│        │  │  │  ├─ AbstractArgumentTest.php
│        │  │  │  ├─ LazyClosureTest.php
│        │  │  │  ├─ RewindableGeneratorTest.php
│        │  │  │  └─ TaggedIteratorArgumentTest.php
│        │  │  ├─ Attribute
│        │  │  │  ├─ AutowireCallableTest.php
│        │  │  │  ├─ AutowireInlineTest.php
│        │  │  │  ├─ AutowireLocatorTest.php
│        │  │  │  ├─ AutowireMethodOfTest.php
│        │  │  │  └─ AutowireTest.php
│        │  │  ├─ ChildDefinitionTest.php
│        │  │  ├─ Compiler
│        │  │  │  ├─ AbstractRecursivePassTest.php
│        │  │  │  ├─ AliasDeprecatedPublicServicesPassTest.php
│        │  │  │  ├─ AnalyzeServiceReferencesPassTest.php
│        │  │  │  ├─ AttributeAutoconfigurationPassTest.php
│        │  │  │  ├─ AutoAliasServicePassTest.php
│        │  │  │  ├─ AutowirePassTest.php
│        │  │  │  ├─ AutowireRequiredMethodsPassTest.php
│        │  │  │  ├─ AutowireRequiredPropertiesPassTest.php
│        │  │  │  ├─ CheckAliasValidityPassTest.php
│        │  │  │  ├─ CheckArgumentsValidityPassTest.php
│        │  │  │  ├─ CheckCircularReferencesPassTest.php
│        │  │  │  ├─ CheckDefinitionValidityPassTest.php
│        │  │  │  ├─ CheckExceptionOnInvalidReferenceBehaviorPassTest.php
│        │  │  │  ├─ CheckReferenceValidityPassTest.php
│        │  │  │  ├─ CheckTypeDeclarationsPassTest.php
│        │  │  │  ├─ CustomExpressionLanguageFunctionTest.php
│        │  │  │  ├─ DecoratorServicePassTest.php
│        │  │  │  ├─ DefinitionErrorExceptionPassTest.php
│        │  │  │  ├─ ExtensionCompilerPassTest.php
│        │  │  │  ├─ InlineServiceDefinitionsPassTest.php
│        │  │  │  ├─ IntegrationTest.php
│        │  │  │  ├─ MergeExtensionConfigurationPassTest.php
│        │  │  │  ├─ OptionalServiceClass.php
│        │  │  │  ├─ PassConfigTest.php
│        │  │  │  ├─ PriorityTaggedServiceTraitTest.php
│        │  │  │  ├─ RegisterAutoconfigureAttributesPassTest.php
│        │  │  │  ├─ RegisterEnvVarProcessorsPassTest.php
│        │  │  │  ├─ RegisterReverseContainerPassTest.php
│        │  │  │  ├─ RegisterServiceSubscribersPassTest.php
│        │  │  │  ├─ RemoveBuildParametersPassTest.php
│        │  │  │  ├─ RemoveUnusedDefinitionsPassTest.php
│        │  │  │  ├─ ReplaceAliasByActualDefinitionPassTest.php
│        │  │  │  ├─ ResolveAutowireInlineAttributesPassTest.php
│        │  │  │  ├─ ResolveBindingsPassTest.php
│        │  │  │  ├─ ResolveChildDefinitionsPassTest.php
│        │  │  │  ├─ ResolveClassPassTest.php
│        │  │  │  ├─ ResolveFactoryClassPassTest.php
│        │  │  │  ├─ ResolveHotPathPassTest.php
│        │  │  │  ├─ ResolveInstanceofConditionalsPassTest.php
│        │  │  │  ├─ ResolveInvalidReferencesPassTest.php
│        │  │  │  ├─ ResolveNamedArgumentsPassTest.php
│        │  │  │  ├─ ResolveNoPreloadPassTest.php
│        │  │  │  ├─ ResolveParameterPlaceHoldersPassTest.php
│        │  │  │  ├─ ResolveReferencesToAliasesPassTest.php
│        │  │  │  ├─ ResolveTaggedIteratorArgumentPassTest.php
│        │  │  │  ├─ ServiceLocatorTagPassTest.php
│        │  │  │  └─ ValidateEnvPlaceholdersPassTest.php
│        │  │  ├─ Config
│        │  │  │  ├─ ContainerParametersResourceCheckerTest.php
│        │  │  │  └─ ContainerParametersResourceTest.php
│        │  │  ├─ ContainerBuilderTest.php
│        │  │  ├─ ContainerTest.php
│        │  │  ├─ CrossCheckTest.php
│        │  │  ├─ DefinitionTest.php
│        │  │  ├─ Dumper
│        │  │  │  ├─ GraphvizDumperTest.php
│        │  │  │  ├─ PhpDumperTest.php
│        │  │  │  ├─ PreloaderTest.php
│        │  │  │  ├─ XmlDumperTest.php
│        │  │  │  └─ YamlDumperTest.php
│        │  │  ├─ EnvVarProcessorTest.php
│        │  │  ├─ Exception
│        │  │  │  ├─ AutowiringFailedExceptionTest.php
│        │  │  │  └─ InvalidParameterTypeExceptionTest.php
│        │  │  ├─ Extension
│        │  │  │  ├─ AbstractExtensionTest.php
│        │  │  │  └─ ExtensionTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ AcmeConfig
│        │  │  │  │  └─ NestedConfig.php
│        │  │  │  ├─ AcmeConfig.php
│        │  │  │  ├─ array.json
│        │  │  │  ├─ Attribute
│        │  │  │  │  ├─ CustomAnyAttribute.php
│        │  │  │  │  ├─ CustomAutoconfiguration.php
│        │  │  │  │  ├─ CustomChildAttribute.php
│        │  │  │  │  ├─ CustomMethodAttribute.php
│        │  │  │  │  ├─ CustomParameterAttribute.php
│        │  │  │  │  └─ CustomPropertyAttribute.php
│        │  │  │  ├─ AutoconfigureAttributed.php
│        │  │  │  ├─ AutoconfiguredInterface.php
│        │  │  │  ├─ AutoconfiguredInterface2.php
│        │  │  │  ├─ AutoconfiguredService1.php
│        │  │  │  ├─ AutoconfiguredService2.php
│        │  │  │  ├─ AutoconfigureRepeated.php
│        │  │  │  ├─ AutoconfigureRepeatedBindings.php
│        │  │  │  ├─ AutoconfigureRepeatedCalls.php
│        │  │  │  ├─ AutoconfigureRepeatedOverwrite.php
│        │  │  │  ├─ AutoconfigureRepeatedProperties.php
│        │  │  │  ├─ AutoconfigureRepeatedTag.php
│        │  │  │  ├─ AutowireLocatorConsumer.php
│        │  │  │  ├─ Bar.php
│        │  │  │  ├─ BarFactory.php
│        │  │  │  ├─ BarInterface.php
│        │  │  │  ├─ BarTagClass.php
│        │  │  │  ├─ CaseSensitiveClass.php
│        │  │  │  ├─ CheckAliasValidityPass
│        │  │  │  │  ├─ FooImplementing.php
│        │  │  │  │  ├─ FooInterface.php
│        │  │  │  │  └─ FooNotImplementing.php
│        │  │  │  ├─ CheckTypeDeclarationsPass
│        │  │  │  │  ├─ Bar.php
│        │  │  │  │  ├─ BarErroredDependency.php
│        │  │  │  │  ├─ BarMethodCall.php
│        │  │  │  │  ├─ BarOptionalArgument.php
│        │  │  │  │  ├─ BarOptionalArgumentNotNull.php
│        │  │  │  │  ├─ Deprecated.php
│        │  │  │  │  ├─ Foo.php
│        │  │  │  │  ├─ FooObject.php
│        │  │  │  │  ├─ IntersectionConstructor.php
│        │  │  │  │  ├─ UnionConstructor.php
│        │  │  │  │  ├─ UnionConstructorPHP82.php
│        │  │  │  │  ├─ Waldo.php
│        │  │  │  │  ├─ WaldoFoo.php
│        │  │  │  │  ├─ WaldoInterface.php
│        │  │  │  │  └─ Wobble.php
│        │  │  │  ├─ config
│        │  │  │  │  ├─ anonymous.expected.yml
│        │  │  │  │  ├─ anonymous.php
│        │  │  │  │  ├─ basic.expected.yml
│        │  │  │  │  ├─ basic.php
│        │  │  │  │  ├─ child.expected.yml
│        │  │  │  │  ├─ child.php
│        │  │  │  │  ├─ closure.expected.yml
│        │  │  │  │  ├─ closure.php
│        │  │  │  │  ├─ config_builder.expected.yml
│        │  │  │  │  ├─ config_builder.php
│        │  │  │  │  ├─ config_builder_env_configurator.php
│        │  │  │  │  ├─ defaults.expected.yml
│        │  │  │  │  ├─ defaults.php
│        │  │  │  │  ├─ definition
│        │  │  │  │  │  ├─ foo.php
│        │  │  │  │  │  └─ multiple
│        │  │  │  │  │     ├─ bar.php
│        │  │  │  │  │     └─ baz.php
│        │  │  │  │  ├─ env_configurator.php
│        │  │  │  │  ├─ env_param.expected.yml
│        │  │  │  │  ├─ env_param.php
│        │  │  │  │  ├─ expression_factory.expected.yml
│        │  │  │  │  ├─ expression_factory.php
│        │  │  │  │  ├─ factory_short_notation.php
│        │  │  │  │  ├─ from_callable.expected.yml
│        │  │  │  │  ├─ from_callable.php
│        │  │  │  │  ├─ inline_binding.expected.yml
│        │  │  │  │  ├─ inline_binding.php
│        │  │  │  │  ├─ inline_static_constructor.expected.yml
│        │  │  │  │  ├─ inline_static_constructor.php
│        │  │  │  │  ├─ instanceof.expected.yml
│        │  │  │  │  ├─ instanceof.php
│        │  │  │  │  ├─ instanceof_static_constructor.expected.yml
│        │  │  │  │  ├─ instanceof_static_constructor.php
│        │  │  │  │  ├─ lazy_fqcn.expected.yml
│        │  │  │  │  ├─ lazy_fqcn.php
│        │  │  │  │  ├─ nested_bundle_config.php
│        │  │  │  │  ├─ nested_config_builder.php
│        │  │  │  │  ├─ not_when_env.php
│        │  │  │  │  ├─ object.expected.yml
│        │  │  │  │  ├─ object.php
│        │  │  │  │  ├─ packages
│        │  │  │  │  │  ├─ ping.yaml
│        │  │  │  │  │  ├─ third_a.yaml
│        │  │  │  │  │  ├─ third_b.yaml
│        │  │  │  │  │  └─ third_c.yaml
│        │  │  │  │  ├─ php7.expected.yml
│        │  │  │  │  ├─ php7.php
│        │  │  │  │  ├─ prototype.expected.yml
│        │  │  │  │  ├─ prototype.php
│        │  │  │  │  ├─ prototype_array.expected.yml
│        │  │  │  │  ├─ prototype_array.php
│        │  │  │  │  ├─ remove.expected.yml
│        │  │  │  │  ├─ remove.php
│        │  │  │  │  ├─ services.php
│        │  │  │  │  ├─ services9.php
│        │  │  │  │  ├─ services_autoconfigure_with_parent.php
│        │  │  │  │  ├─ services_closure_argument.php
│        │  │  │  │  ├─ services_with_enumeration.php
│        │  │  │  │  ├─ services_with_service_locator_argument.php
│        │  │  │  │  ├─ stack.php
│        │  │  │  │  ├─ static_constructor.expected.yml
│        │  │  │  │  ├─ static_constructor.php
│        │  │  │  │  ├─ when_env.php
│        │  │  │  │  └─ when_not_when_env.php
│        │  │  │  ├─ ConstructNotExists.php
│        │  │  │  ├─ Container
│        │  │  │  │  ├─ ConstructorWithMandatoryArgumentsContainer.php
│        │  │  │  │  ├─ ConstructorWithOptionalArgumentsContainer.php
│        │  │  │  │  ├─ ConstructorWithoutArgumentsContainer.php
│        │  │  │  │  └─ NoConstructorContainer.php
│        │  │  │  ├─ containers
│        │  │  │  │  ├─ container10.php
│        │  │  │  │  ├─ container11.php
│        │  │  │  │  ├─ container12.php
│        │  │  │  │  ├─ container13.php
│        │  │  │  │  ├─ container14.php
│        │  │  │  │  ├─ container15.php
│        │  │  │  │  ├─ container16.php
│        │  │  │  │  ├─ container17.php
│        │  │  │  │  ├─ container19.php
│        │  │  │  │  ├─ container21.php
│        │  │  │  │  ├─ container24.php
│        │  │  │  │  ├─ container33.php
│        │  │  │  │  ├─ container34.php
│        │  │  │  │  ├─ container8.php
│        │  │  │  │  ├─ container9.php
│        │  │  │  │  ├─ container_abstract.php
│        │  │  │  │  ├─ container_almost_circular.php
│        │  │  │  │  ├─ container_deprecated_parameters.php
│        │  │  │  │  ├─ container_env_in_id.php
│        │  │  │  │  ├─ container_inline_requires.php
│        │  │  │  │  ├─ container_nonempty_parameters.php
│        │  │  │  │  ├─ container_non_scalar_tags.php
│        │  │  │  │  ├─ container_service_locator_argument.php
│        │  │  │  │  ├─ container_uninitialized_ref.php
│        │  │  │  │  └─ CustomContainer.php
│        │  │  │  ├─ CustomDefinition.php
│        │  │  │  ├─ DependencyContainer.php
│        │  │  │  ├─ DependencyContainerInterface.php
│        │  │  │  ├─ DeprecatedClass.php
│        │  │  │  ├─ directory
│        │  │  │  │  ├─ import
│        │  │  │  │  │  └─ import.yml
│        │  │  │  │  ├─ recurse
│        │  │  │  │  │  ├─ simple.ini
│        │  │  │  │  │  └─ simple.yml
│        │  │  │  │  └─ simple.php
│        │  │  │  ├─ Extension
│        │  │  │  │  ├─ InvalidConfig
│        │  │  │  │  │  ├─ Configuration.php
│        │  │  │  │  │  └─ InvalidConfigExtension.php
│        │  │  │  │  ├─ SemiValidConfig
│        │  │  │  │  │  ├─ Configuration.php
│        │  │  │  │  │  └─ SemiValidConfigExtension.php
│        │  │  │  │  └─ ValidConfig
│        │  │  │  │     ├─ Configuration.php
│        │  │  │  │     └─ ValidConfigExtension.php
│        │  │  │  ├─ FactoryDummy.php
│        │  │  │  ├─ FactoryDummyWithoutReturnTypes.php
│        │  │  │  ├─ FooBarTaggedClass.php
│        │  │  │  ├─ FooBarTaggedForDefaultPriorityClass.php
│        │  │  │  ├─ FooClassWithDefaultArrayAttribute.php
│        │  │  │  ├─ FooClassWithDefaultEnumAttribute.php
│        │  │  │  ├─ FooClassWithDefaultObjectAttribute.php
│        │  │  │  ├─ FooClassWithEnumAttribute.php
│        │  │  │  ├─ FooForCircularWithAddCalls.php
│        │  │  │  ├─ FooTagClass.php
│        │  │  │  ├─ FooTaggedForInvalidDefaultMethodClass.php
│        │  │  │  ├─ FooUnitEnum.php
│        │  │  │  ├─ FooWithAbstractArgument.php
│        │  │  │  ├─ graphviz
│        │  │  │  │  ├─ services1.dot
│        │  │  │  │  ├─ services10-1.dot
│        │  │  │  │  ├─ services10.dot
│        │  │  │  │  ├─ services13.dot
│        │  │  │  │  ├─ services14.dot
│        │  │  │  │  ├─ services17.dot
│        │  │  │  │  ├─ services18.dot
│        │  │  │  │  ├─ services9.dot
│        │  │  │  │  └─ services_inline.dot
│        │  │  │  ├─ includes
│        │  │  │  │  ├─ AcmeExtension.php
│        │  │  │  │  ├─ autowiring_classes.php
│        │  │  │  │  ├─ autowiring_classes_80.php
│        │  │  │  │  ├─ classes.php
│        │  │  │  │  ├─ compositetype_classes.php
│        │  │  │  │  ├─ createphar.php
│        │  │  │  │  ├─ foo.php
│        │  │  │  │  ├─ FooVariadic.php
│        │  │  │  │  ├─ foo_lazy.php
│        │  │  │  │  ├─ HotPath
│        │  │  │  │  │  ├─ C1.php
│        │  │  │  │  │  ├─ C2.php
│        │  │  │  │  │  ├─ C3.php
│        │  │  │  │  │  ├─ I1.php
│        │  │  │  │  │  ├─ P1.php
│        │  │  │  │  │  └─ T1.php
│        │  │  │  │  ├─ intersectiontype_classes.php
│        │  │  │  │  ├─ MultipleArgumentsOptionalScalarNotReallyOptional.php
│        │  │  │  │  ├─ ProjectExtension.php
│        │  │  │  │  ├─ ProjectWithXsdExtension.php
│        │  │  │  │  ├─ ProjectWithXsdExtensionInPhar.phar
│        │  │  │  │  ├─ schema
│        │  │  │  │  │  └─ project-1.0.xsd
│        │  │  │  │  └─ uniontype_classes.php
│        │  │  │  ├─ ini
│        │  │  │  │  ├─ almostvalid.ini
│        │  │  │  │  ├─ ini_with_wrong_ext.xml
│        │  │  │  │  ├─ nonvalid.ini
│        │  │  │  │  ├─ parameters.ini
│        │  │  │  │  ├─ parameters1.ini
│        │  │  │  │  ├─ parameters2.ini
│        │  │  │  │  ├─ types.ini
│        │  │  │  │  └─ when-env.ini
│        │  │  │  ├─ IntBackedEnum.php
│        │  │  │  ├─ IntTagClass.php
│        │  │  │  ├─ LazyAutoconfigured.php
│        │  │  │  ├─ LazyLoaded.php
│        │  │  │  ├─ MultipleAutoconfigureAttributed.php
│        │  │  │  ├─ NamedArgumentsDummy.php
│        │  │  │  ├─ NamedArgumentsVariadicsDummy.php
│        │  │  │  ├─ NamedEnumArgumentDummy.php
│        │  │  │  ├─ NamedIterableArgumentDummy.php
│        │  │  │  ├─ NewInInitializer.php
│        │  │  │  ├─ OptionalParameter.php
│        │  │  │  ├─ ParentNotExists.php
│        │  │  │  ├─ php
│        │  │  │  │  ├─ autowire_closure.php
│        │  │  │  │  ├─ callable_adapter_consumer.php
│        │  │  │  │  ├─ closure.php
│        │  │  │  │  ├─ closure_proxy.php
│        │  │  │  │  ├─ custom_container_class_constructor_without_arguments.php
│        │  │  │  │  ├─ custom_container_class_without_constructor.php
│        │  │  │  │  ├─ custom_container_class_with_mandatory_constructor_arguments.php
│        │  │  │  │  ├─ custom_container_class_with_optional_constructor_arguments.php
│        │  │  │  │  ├─ inline_adapter_consumer.php
│        │  │  │  │  ├─ lazy_autowire_attribute.php
│        │  │  │  │  ├─ lazy_autowire_attribute_with_intersection.php
│        │  │  │  │  ├─ lazy_closure.php
│        │  │  │  │  ├─ legacy_lazy_autowire_attribute.php
│        │  │  │  │  ├─ legacy_lazy_autowire_attribute_with_intersection.php
│        │  │  │  │  ├─ legacy_services9_lazy_inlined_factories.txt
│        │  │  │  │  ├─ legacy_services_dedup_lazy.php
│        │  │  │  │  ├─ legacy_services_non_shared_lazy.php
│        │  │  │  │  ├─ legacy_services_non_shared_lazy_as_files.txt
│        │  │  │  │  ├─ legacy_services_non_shared_lazy_ghost.php
│        │  │  │  │  ├─ legacy_services_non_shared_lazy_public.php
│        │  │  │  │  ├─ legacy_services_wither_lazy.php
│        │  │  │  │  ├─ legacy_services_wither_lazy_non_shared.php
│        │  │  │  │  ├─ php_with_wrong_ext.yml
│        │  │  │  │  ├─ return_foo_string.php
│        │  │  │  │  ├─ services1-1.php
│        │  │  │  │  ├─ services1.php
│        │  │  │  │  ├─ services10.php
│        │  │  │  │  ├─ services10_as_files.txt
│        │  │  │  │  ├─ services12.php
│        │  │  │  │  ├─ services13.php
│        │  │  │  │  ├─ services19.php
│        │  │  │  │  ├─ services24.php
│        │  │  │  │  ├─ services26.php
│        │  │  │  │  ├─ services33.php
│        │  │  │  │  ├─ services8.php
│        │  │  │  │  ├─ services9_as_files.txt
│        │  │  │  │  ├─ services9_compiled.php
│        │  │  │  │  ├─ services9_inlined_factories.txt
│        │  │  │  │  ├─ services9_inlined_factories_with_tagged_iterrator.txt
│        │  │  │  │  ├─ services9_lazy_inlined_factories.txt
│        │  │  │  │  ├─ services_adawson.php
│        │  │  │  │  ├─ services_almost_circular_private.php
│        │  │  │  │  ├─ services_almost_circular_public.php
│        │  │  │  │  ├─ services_array_params.php
│        │  │  │  │  ├─ services_base64_env.php
│        │  │  │  │  ├─ services_closure_argument_compiled.php
│        │  │  │  │  ├─ services_csv_env.php
│        │  │  │  │  ├─ services_current_factory_inlining.php
│        │  │  │  │  ├─ services_dedup_lazy.php
│        │  │  │  │  ├─ services_deep_graph.php
│        │  │  │  │  ├─ services_default_env.php
│        │  │  │  │  ├─ services_deprecated_parameters.php
│        │  │  │  │  ├─ services_deprecated_parameters_as_files.txt
│        │  │  │  │  ├─ services_env_in_id.php
│        │  │  │  │  ├─ services_errored_definition.php
│        │  │  │  │  ├─ services_inline_requires.php
│        │  │  │  │  ├─ services_inline_self_ref.php
│        │  │  │  │  ├─ services_json_env.php
│        │  │  │  │  ├─ services_locator.php
│        │  │  │  │  ├─ services_new_in_initializer.php
│        │  │  │  │  ├─ services_nonempty_parameters.php
│        │  │  │  │  ├─ services_nonempty_parameters_as_files.txt
│        │  │  │  │  ├─ services_non_shared_duplicates.php
│        │  │  │  │  ├─ services_non_shared_lazy.php
│        │  │  │  │  ├─ services_non_shared_lazy_as_files.txt
│        │  │  │  │  ├─ services_non_shared_lazy_ghost.php
│        │  │  │  │  ├─ services_non_shared_lazy_public.php
│        │  │  │  │  ├─ services_private_frozen.php
│        │  │  │  │  ├─ services_private_in_expression.php
│        │  │  │  │  ├─ services_query_string_env.php
│        │  │  │  │  ├─ services_rot13_env.php
│        │  │  │  │  ├─ services_service_locator_argument.php
│        │  │  │  │  ├─ services_subscriber.php
│        │  │  │  │  ├─ services_tsantos.php
│        │  │  │  │  ├─ services_uninitialized_ref.php
│        │  │  │  │  ├─ services_unsupported_characters.php
│        │  │  │  │  ├─ services_url_env.php
│        │  │  │  │  ├─ services_wither.php
│        │  │  │  │  ├─ services_wither_annotation.php
│        │  │  │  │  ├─ services_wither_lazy.php
│        │  │  │  │  ├─ services_wither_lazy_non_shared.php
│        │  │  │  │  ├─ services_wither_staticreturntype.php
│        │  │  │  │  ├─ simple.php
│        │  │  │  │  └─ static_constructor.php
│        │  │  │  ├─ Preload
│        │  │  │  │  ├─ A.php
│        │  │  │  │  ├─ B.php
│        │  │  │  │  ├─ C.php
│        │  │  │  │  ├─ D.php
│        │  │  │  │  ├─ Dummy.php
│        │  │  │  │  ├─ DummyWithInterface.php
│        │  │  │  │  ├─ E.php
│        │  │  │  │  ├─ F.php
│        │  │  │  │  ├─ G.php
│        │  │  │  │  ├─ IntersectionDummy.php
│        │  │  │  │  └─ UnionDummy.php
│        │  │  │  ├─ Prototype
│        │  │  │  │  ├─ BadAttributes
│        │  │  │  │  │  └─ WhenNotWhenFoo.php
│        │  │  │  │  ├─ BadClasses
│        │  │  │  │  │  └─ MissingParent.php
│        │  │  │  │  ├─ Foo.php
│        │  │  │  │  ├─ FooInterface.php
│        │  │  │  │  ├─ NotFoo.php
│        │  │  │  │  ├─ OtherDir
│        │  │  │  │  │  ├─ AnotherSub
│        │  │  │  │  │  │  └─ DeeperBaz.php
│        │  │  │  │  │  ├─ Baz.php
│        │  │  │  │  │  ├─ Component1
│        │  │  │  │  │  │  ├─ Dir1
│        │  │  │  │  │  │  │  └─ Service1.php
│        │  │  │  │  │  │  └─ Dir2
│        │  │  │  │  │  │     └─ Service2.php
│        │  │  │  │  │  └─ Component2
│        │  │  │  │  │     ├─ Dir1
│        │  │  │  │  │     │  └─ Service4.php
│        │  │  │  │  │     └─ Dir2
│        │  │  │  │  │        └─ Service5.php
│        │  │  │  │  ├─ SinglyImplementedInterface
│        │  │  │  │  │  ├─ Adapter
│        │  │  │  │  │  │  └─ Adapter.php
│        │  │  │  │  │  ├─ AnotherAdapter
│        │  │  │  │  │  │  └─ Adapter.php
│        │  │  │  │  │  └─ Port
│        │  │  │  │  │     └─ PortInterface.php
│        │  │  │  │  ├─ StaticConstructor
│        │  │  │  │  │  ├─ PrototypeStaticConstructor.php
│        │  │  │  │  │  ├─ PrototypeStaticConstructorAsArgument.php
│        │  │  │  │  │  └─ PrototypeStaticConstructorInterface.php
│        │  │  │  │  └─ Sub
│        │  │  │  │     ├─ Bar.php
│        │  │  │  │     └─ BarInterface.php
│        │  │  │  ├─ PrototypeAsAlias
│        │  │  │  │  ├─ AliasBarInterface.php
│        │  │  │  │  ├─ AliasFooInterface.php
│        │  │  │  │  ├─ WithAsAlias.php
│        │  │  │  │  ├─ WithAsAliasBothEnv.php
│        │  │  │  │  ├─ WithAsAliasDevEnv.php
│        │  │  │  │  ├─ WithAsAliasDuplicate.php
│        │  │  │  │  ├─ WithAsAliasIdMultipleInterface.php
│        │  │  │  │  ├─ WithAsAliasInterface.php
│        │  │  │  │  ├─ WithAsAliasMultiple.php
│        │  │  │  │  ├─ WithAsAliasMultipleInterface.php
│        │  │  │  │  └─ WithAsAliasProdEnv.php
│        │  │  │  ├─ ReadOnlyClass.php
│        │  │  │  ├─ RemoteCaller.php
│        │  │  │  ├─ RemoteCallerHttp.php
│        │  │  │  ├─ RemoteCallerSocket.php
│        │  │  │  ├─ ScalarFactory.php
│        │  │  │  ├─ SimilarArgumentsDummy.php
│        │  │  │  ├─ StaticConstructorAutoconfigure.php
│        │  │  │  ├─ StaticMethodTag.php
│        │  │  │  ├─ StdClassDecorator.php
│        │  │  │  ├─ StringBackedEnum.php
│        │  │  │  ├─ StubbedTranslator.php
│        │  │  │  ├─ TaggedConsumerWithExclude.php
│        │  │  │  ├─ TaggedIteratorConsumer.php
│        │  │  │  ├─ TaggedIteratorConsumerWithDefaultIndexMethod.php
│        │  │  │  ├─ TaggedIteratorConsumerWithDefaultIndexMethodAndWithDefaultPriorityMethod.php
│        │  │  │  ├─ TaggedIteratorConsumerWithDefaultPriorityMethod.php
│        │  │  │  ├─ TaggedLocatorConsumer.php
│        │  │  │  ├─ TaggedLocatorConsumerConsumer.php
│        │  │  │  ├─ TaggedLocatorConsumerFactory.php
│        │  │  │  ├─ TaggedLocatorConsumerWithDefaultIndexMethod.php
│        │  │  │  ├─ TaggedLocatorConsumerWithDefaultIndexMethodAndWithDefaultPriorityMethod.php
│        │  │  │  ├─ TaggedLocatorConsumerWithDefaultPriorityMethod.php
│        │  │  │  ├─ TaggedLocatorConsumerWithoutIndex.php
│        │  │  │  ├─ TaggedLocatorConsumerWithServiceSubscriber.php
│        │  │  │  ├─ TaggedService1.php
│        │  │  │  ├─ TaggedService2.php
│        │  │  │  ├─ TaggedService3.php
│        │  │  │  ├─ TaggedService3Configurator.php
│        │  │  │  ├─ TaggedService4.php
│        │  │  │  ├─ TaggedService5.php
│        │  │  │  ├─ TestDefinition1.php
│        │  │  │  ├─ TestDefinition2.php
│        │  │  │  ├─ TestDefinition3.php
│        │  │  │  ├─ TestServiceMethodsSubscriberTrait.php
│        │  │  │  ├─ TestServiceSubscriber.php
│        │  │  │  ├─ TestServiceSubscriberChild.php
│        │  │  │  ├─ TestServiceSubscriberIntersection.php
│        │  │  │  ├─ TestServiceSubscriberIntersectionWithTrait.php
│        │  │  │  ├─ TestServiceSubscriberParent.php
│        │  │  │  ├─ TestServiceSubscriberUnion.php
│        │  │  │  ├─ TestServiceSubscriberUnionWithTrait.php
│        │  │  │  ├─ Utils
│        │  │  │  │  └─ NotAService.php
│        │  │  │  ├─ WitherStaticReturnType.php
│        │  │  │  ├─ WithTarget.php
│        │  │  │  ├─ WithTargetAnonymous.php
│        │  │  │  ├─ xml
│        │  │  │  │  ├─ bindings_and_inner_collections.xml
│        │  │  │  │  ├─ class_from_id.xml
│        │  │  │  │  ├─ closure.xml
│        │  │  │  │  ├─ defaults_bindings.xml
│        │  │  │  │  ├─ defaults_bindings2.xml
│        │  │  │  │  ├─ deprecated_alias_definitions.xml
│        │  │  │  │  ├─ extension1
│        │  │  │  │  │  └─ services.xml
│        │  │  │  │  ├─ extension2
│        │  │  │  │  │  └─ services.xml
│        │  │  │  │  ├─ extensions
│        │  │  │  │  │  ├─ services1.xml
│        │  │  │  │  │  ├─ services2.xml
│        │  │  │  │  │  ├─ services3.xml
│        │  │  │  │  │  ├─ services4.xml
│        │  │  │  │  │  ├─ services5.xml
│        │  │  │  │  │  ├─ services6.xml
│        │  │  │  │  │  └─ services7.xml
│        │  │  │  │  ├─ from_callable.xml
│        │  │  │  │  ├─ invalid_alias_definition.xml
│        │  │  │  │  ├─ key_type_argument.xml
│        │  │  │  │  ├─ key_type_incorrect_bin.xml
│        │  │  │  │  ├─ key_type_property.xml
│        │  │  │  │  ├─ key_type_wrong_constant.xml
│        │  │  │  │  ├─ namespaces.xml
│        │  │  │  │  ├─ nested_service_without_id.xml
│        │  │  │  │  ├─ nonvalid.xml
│        │  │  │  │  ├─ not_singly_implemented_interface_in_multiple_resources.xml
│        │  │  │  │  ├─ not_singly_implemented_interface_in_multiple_resources_with_previously_registered_alias.xml
│        │  │  │  │  ├─ not_singly_implemented_interface_in_multiple_resources_with_previously_registered_alias2.xml
│        │  │  │  │  ├─ returns_clone.xml
│        │  │  │  │  ├─ services1.xml
│        │  │  │  │  ├─ services10.xml
│        │  │  │  │  ├─ services13.xml
│        │  │  │  │  ├─ services14.xml
│        │  │  │  │  ├─ services2.xml
│        │  │  │  │  ├─ services21.xml
│        │  │  │  │  ├─ services23.xml
│        │  │  │  │  ├─ services24.xml
│        │  │  │  │  ├─ services28.xml
│        │  │  │  │  ├─ services29.xml
│        │  │  │  │  ├─ services3.xml
│        │  │  │  │  ├─ services30.xml
│        │  │  │  │  ├─ services4.xml
│        │  │  │  │  ├─ services4_bad_import.xml
│        │  │  │  │  ├─ services4_bad_import_file_not_found.xml
│        │  │  │  │  ├─ services4_bad_import_nonvalid.xml
│        │  │  │  │  ├─ services4_bad_import_with_errors.xml
│        │  │  │  │  ├─ services5.xml
│        │  │  │  │  ├─ services6.xml
│        │  │  │  │  ├─ services7.xml
│        │  │  │  │  ├─ services8.xml
│        │  │  │  │  ├─ services9.xml
│        │  │  │  │  ├─ services_abstract.xml
│        │  │  │  │  ├─ services_autoconfigure.xml
│        │  │  │  │  ├─ services_autoconfigure_with_parent.xml
│        │  │  │  │  ├─ services_bindings.xml
│        │  │  │  │  ├─ services_case.xml
│        │  │  │  │  ├─ services_defaults_with_parent.xml
│        │  │  │  │  ├─ services_deprecated.xml
│        │  │  │  │  ├─ services_dump_load.xml
│        │  │  │  │  ├─ services_inline_not_candidate.xml
│        │  │  │  │  ├─ services_instanceof.xml
│        │  │  │  │  ├─ services_instanceof_with_parent.xml
│        │  │  │  │  ├─ services_lazy_fqcn.xml
│        │  │  │  │  ├─ services_named_args.xml
│        │  │  │  │  ├─ services_prototype.xml
│        │  │  │  │  ├─ services_prototype_array.xml
│        │  │  │  │  ├─ services_prototype_array_with_empty_node.xml
│        │  │  │  │  ├─ services_prototype_array_with_space_node.xml
│        │  │  │  │  ├─ services_prototype_constructor.xml
│        │  │  │  │  ├─ services_tsantos.xml
│        │  │  │  │  ├─ services_without_id.xml
│        │  │  │  │  ├─ services_with_abstract_argument.xml
│        │  │  │  │  ├─ services_with_array_tags.xml
│        │  │  │  │  ├─ services_with_default_array.xml
│        │  │  │  │  ├─ services_with_default_enumeration.xml
│        │  │  │  │  ├─ services_with_default_object.xml
│        │  │  │  │  ├─ services_with_deprecated_tagged.xml
│        │  │  │  │  ├─ services_with_enumeration.xml
│        │  │  │  │  ├─ services_with_invalid_enumeration.xml
│        │  │  │  │  ├─ services_with_service_closure.xml
│        │  │  │  │  ├─ services_with_service_locator_argument.xml
│        │  │  │  │  ├─ services_with_tagged_arguments.xml
│        │  │  │  │  ├─ service_with_abstract_argument.xml
│        │  │  │  │  ├─ singly_implemented_interface_in_multiple_resources.xml
│        │  │  │  │  ├─ stack.xml
│        │  │  │  │  ├─ static_constructor.xml
│        │  │  │  │  ├─ static_constructor_and_factory.xml
│        │  │  │  │  ├─ tag_without_name.xml
│        │  │  │  │  ├─ tag_with_empty_name.xml
│        │  │  │  │  ├─ tag_with_name_attribute.xml
│        │  │  │  │  ├─ when-env-services.xml
│        │  │  │  │  ├─ when-env.xml
│        │  │  │  │  ├─ withdoctype.xml
│        │  │  │  │  ├─ with_key_outside_collection.xml
│        │  │  │  │  └─ xml_with_wrong_ext.php
│        │  │  │  └─ yaml
│        │  │  │     ├─ alt_call.yaml
│        │  │  │     ├─ anonymous_services.yml
│        │  │  │     ├─ anonymous_services_alias.yml
│        │  │  │     ├─ anonymous_services_in_instanceof.yml
│        │  │  │     ├─ anonymous_services_in_parameters.yml
│        │  │  │     ├─ badtag1.yml
│        │  │  │     ├─ badtag2.yml
│        │  │  │     ├─ bad_alias.yml
│        │  │  │     ├─ bad_calls.yml
│        │  │  │     ├─ bad_decorates.yml
│        │  │  │     ├─ bad_decoration_on_invalid_null.yml
│        │  │  │     ├─ bad_empty_defaults.yml
│        │  │  │     ├─ bad_empty_instanceof.yml
│        │  │  │     ├─ bad_factory_syntax.yml
│        │  │  │     ├─ bad_format.yml
│        │  │  │     ├─ bad_import.yml
│        │  │  │     ├─ bad_imports.yml
│        │  │  │     ├─ bad_keyword.yml
│        │  │  │     ├─ bad_parameters.yml
│        │  │  │     ├─ bad_parent.yml
│        │  │  │     ├─ bad_service.yml
│        │  │  │     ├─ bad_services.yml
│        │  │  │     ├─ bar
│        │  │  │     │  └─ services.yml
│        │  │  │     ├─ class_from_id.yml
│        │  │  │     ├─ closure.yml
│        │  │  │     ├─ constructor_with_factory.yml
│        │  │  │     ├─ defaults_bindings.yml
│        │  │  │     ├─ defaults_bindings2.yml
│        │  │  │     ├─ deprecated_alias_definitions.yml
│        │  │  │     ├─ deprecated_alias_definitions_without_package_and_version.yml
│        │  │  │     ├─ deprecated_definition_without_message.yml
│        │  │  │     ├─ foo
│        │  │  │     │  └─ services.yml
│        │  │  │     ├─ from_callable.yml
│        │  │  │     ├─ integration
│        │  │  │     │  ├─ autoconfigure_child_not_applied
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  ├─ main.yml
│        │  │  │     │  │  └─ _child.yml
│        │  │  │     │  ├─ autoconfigure_parent_child
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  ├─ main.yml
│        │  │  │     │  │  └─ _child.yml
│        │  │  │     │  ├─ autoconfigure_parent_child_tags
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  ├─ main.yml
│        │  │  │     │  │  └─ _child.yml
│        │  │  │     │  ├─ child_parent
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  └─ main.yml
│        │  │  │     │  ├─ defaults_child_tags
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  └─ main.yml
│        │  │  │     │  ├─ defaults_instanceof_importance
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  └─ main.yml
│        │  │  │     │  ├─ defaults_parent_child
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  ├─ main.yml
│        │  │  │     │  │  └─ _child.yml
│        │  │  │     │  ├─ instanceof_and_calls
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  └─ main.yml
│        │  │  │     │  └─ instanceof_parent_child
│        │  │  │     │     ├─ expected.yml
│        │  │  │     │     ├─ main.yml
│        │  │  │     │     └─ _child.yml
│        │  │  │     ├─ nonvalid1.yml
│        │  │  │     ├─ nonvalid2.yml
│        │  │  │     ├─ not_singly_implemented_interface_in_multiple_resources.yml
│        │  │  │     ├─ not_singly_implemented_interface_in_multiple_resources_with_previously_registered_alias.yml
│        │  │  │     ├─ not_singly_implemented_interface_in_multiple_resources_with_previously_registered_alias2.yml
│        │  │  │     ├─ null_config.yml
│        │  │  │     ├─ returns_clone.yaml
│        │  │  │     ├─ services1.yml
│        │  │  │     ├─ services10.yml
│        │  │  │     ├─ services11.yml
│        │  │  │     ├─ services13.yml
│        │  │  │     ├─ services14.yml
│        │  │  │     ├─ services2.yml
│        │  │  │     ├─ services21.yml
│        │  │  │     ├─ services23.yml
│        │  │  │     ├─ services24.yml
│        │  │  │     ├─ services26.yml
│        │  │  │     ├─ services28.yml
│        │  │  │     ├─ services29.yml
│        │  │  │     ├─ services3.yml
│        │  │  │     ├─ services30.yml
│        │  │  │     ├─ services31_invalid_tags.yml
│        │  │  │     ├─ services34.yml
│        │  │  │     ├─ services4.yml
│        │  │  │     ├─ services4_bad_import.yml
│        │  │  │     ├─ services4_bad_import_file_not_found.yml
│        │  │  │     ├─ services4_bad_import_nonvalid.yml
│        │  │  │     ├─ services4_bad_import_with_errors.yml
│        │  │  │     ├─ services6.yml
│        │  │  │     ├─ services7.yml
│        │  │  │     ├─ services8.yml
│        │  │  │     ├─ services9.yml
│        │  │  │     ├─ services_adawson.yml
│        │  │  │     ├─ services_autoconfigure.yml
│        │  │  │     ├─ services_autoconfigure_with_parent.yml
│        │  │  │     ├─ services_bindings.yml
│        │  │  │     ├─ services_case.yml
│        │  │  │     ├─ services_configurator_short_syntax.yml
│        │  │  │     ├─ services_deep_graph.yml
│        │  │  │     ├─ services_defaults_with_parent.yml
│        │  │  │     ├─ services_dump_load.yml
│        │  │  │     ├─ services_inline.yml
│        │  │  │     ├─ services_instanceof.yml
│        │  │  │     ├─ services_instanceof_with_parent.yml
│        │  │  │     ├─ services_lazy_fqcn.yml
│        │  │  │     ├─ services_named_args.yml
│        │  │  │     ├─ services_not_existing.yml
│        │  │  │     ├─ services_prototype.yml
│        │  │  │     ├─ services_prototype_namespace.yml
│        │  │  │     ├─ services_prototype_namespace_without_resource.yml
│        │  │  │     ├─ services_prototype_with_empty_node.yml
│        │  │  │     ├─ services_prototype_with_null_node.yml
│        │  │  │     ├─ services_short_syntax.yml
│        │  │  │     ├─ services_underscore.yml
│        │  │  │     ├─ services_with_abstract_argument.yml
│        │  │  │     ├─ services_with_array_tags.yml
│        │  │  │     ├─ services_with_default_array.yml
│        │  │  │     ├─ services_with_default_enumeration.yml
│        │  │  │     ├─ services_with_default_object.yml
│        │  │  │     ├─ services_with_enumeration.yml
│        │  │  │     ├─ services_with_enumeration_enum_tag.yml
│        │  │  │     ├─ services_with_invalid_enumeration.yml
│        │  │  │     ├─ services_with_service_closure.yml
│        │  │  │     ├─ services_with_service_locator_argument.yml
│        │  │  │     ├─ services_with_short_service_closure.yml
│        │  │  │     ├─ services_with_tagged_argument.yml
│        │  │  │     ├─ service_instanceof_factory.yml
│        │  │  │     ├─ singly_implemented_interface_in_multiple_resources.yml
│        │  │  │     ├─ stack.yaml
│        │  │  │     ├─ static_constructor.yml
│        │  │  │     ├─ tagged_deprecated.yml
│        │  │  │     ├─ tagged_iterator_optional.yml
│        │  │  │     ├─ tag_array_arguments.yml
│        │  │  │     ├─ tag_name_empty_string.yml
│        │  │  │     ├─ tag_name_no_string.yml
│        │  │  │     ├─ tag_name_only.yml
│        │  │  │     ├─ when-env.yaml
│        │  │  │     └─ yaml_with_wrong_ext.ini
│        │  │  ├─ LazyProxy
│        │  │  │  ├─ Instantiator
│        │  │  │  │  └─ RealServiceInstantiatorTest.php
│        │  │  │  └─ PhpDumper
│        │  │  │     ├─ LazyServiceDumperTest.php
│        │  │  │     └─ NullDumperTest.php
│        │  │  ├─ Loader
│        │  │  │  ├─ ClosureLoaderTest.php
│        │  │  │  ├─ Configurator
│        │  │  │  │  └─ EnvConfiguratorTest.php
│        │  │  │  ├─ DirectoryLoaderTest.php
│        │  │  │  ├─ FileLoaderTest.php
│        │  │  │  ├─ GlobFileLoaderTest.php
│        │  │  │  ├─ IniFileLoaderTest.php
│        │  │  │  ├─ LoaderResolverTest.php
│        │  │  │  ├─ PhpFileLoaderTest.php
│        │  │  │  ├─ XmlFileLoaderTest.php
│        │  │  │  └─ YamlFileLoaderTest.php
│        │  │  ├─ ParameterBag
│        │  │  │  ├─ ContainerBagTest.php
│        │  │  │  ├─ EnvPlaceholderParameterBagTest.php
│        │  │  │  ├─ FrozenParameterBagTest.php
│        │  │  │  └─ ParameterBagTest.php
│        │  │  ├─ ParameterTest.php
│        │  │  ├─ ReferenceTest.php
│        │  │  ├─ ServiceLocatorTest.php
│        │  │  └─ StaticEnvVarLoaderTest.php
│        │  ├─ TypedReference.php
│        │  └─ Variable.php
│        ├─ deprecation-contracts
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ function.php
│        │  ├─ LICENSE
│        │  └─ README.md
│        ├─ dotenv
│        │  ├─ CHANGELOG.md
│        │  ├─ Command
│        │  │  ├─ DebugCommand.php
│        │  │  └─ DotenvDumpCommand.php
│        │  ├─ composer.json
│        │  ├─ Dotenv.php
│        │  ├─ Exception
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ FormatException.php
│        │  │  ├─ FormatExceptionContext.php
│        │  │  └─ PathException.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  └─ Tests
│        │     ├─ Command
│        │     │  ├─ DebugCommandTest.php
│        │     │  ├─ DotenvDumpCommandTest.php
│        │     │  └─ Fixtures
│        │     │     ├─ Scenario1
│        │     │     │  ├─ .env
│        │     │     │  ├─ .env.local
│        │     │     │  ├─ .env.prod.local
│        │     │     │  └─ .env.test
│        │     │     ├─ Scenario2
│        │     │     │  ├─ .env.dist
│        │     │     │  ├─ .env.local.php
│        │     │     │  └─ .env.prod
│        │     │     └─ Scenario3
│        │     │        ├─ .env
│        │     │        └─ .env.dist
│        │     ├─ DotenvTest.php
│        │     └─ fixtures
│        │        └─ file_with_bom
│        ├─ error-handler
│        │  ├─ BufferingLogger.php
│        │  ├─ CHANGELOG.md
│        │  ├─ Command
│        │  │  └─ ErrorDumpCommand.php
│        │  ├─ composer.json
│        │  ├─ Debug.php
│        │  ├─ DebugClassLoader.php
│        │  ├─ Error
│        │  │  ├─ ClassNotFoundError.php
│        │  │  ├─ FatalError.php
│        │  │  ├─ OutOfMemoryError.php
│        │  │  ├─ UndefinedFunctionError.php
│        │  │  └─ UndefinedMethodError.php
│        │  ├─ ErrorEnhancer
│        │  │  ├─ ClassNotFoundErrorEnhancer.php
│        │  │  ├─ ErrorEnhancerInterface.php
│        │  │  ├─ UndefinedFunctionErrorEnhancer.php
│        │  │  └─ UndefinedMethodErrorEnhancer.php
│        │  ├─ ErrorHandler.php
│        │  ├─ ErrorRenderer
│        │  │  ├─ CliErrorRenderer.php
│        │  │  ├─ ErrorRendererInterface.php
│        │  │  ├─ FileLinkFormatter.php
│        │  │  ├─ HtmlErrorRenderer.php
│        │  │  └─ SerializerErrorRenderer.php
│        │  ├─ Exception
│        │  │  ├─ FlattenException.php
│        │  │  └─ SilencedErrorContext.php
│        │  ├─ Internal
│        │  │  └─ TentativeTypes.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Resources
│        │  │  ├─ assets
│        │  │  │  ├─ css
│        │  │  │  │  ├─ error.css
│        │  │  │  │  ├─ exception.css
│        │  │  │  │  └─ exception_full.css
│        │  │  │  ├─ images
│        │  │  │  │  ├─ chevron-right.svg
│        │  │  │  │  ├─ favicon.png.base64
│        │  │  │  │  ├─ icon-book.svg
│        │  │  │  │  ├─ icon-copy.svg
│        │  │  │  │  ├─ icon-minus-square-o.svg
│        │  │  │  │  ├─ icon-minus-square.svg
│        │  │  │  │  ├─ icon-plus-square-o.svg
│        │  │  │  │  ├─ icon-plus-square.svg
│        │  │  │  │  ├─ icon-support.svg
│        │  │  │  │  ├─ symfony-ghost.svg.php
│        │  │  │  │  └─ symfony-logo.svg
│        │  │  │  └─ js
│        │  │  │     └─ exception.js
│        │  │  ├─ bin
│        │  │  │  ├─ extract-tentative-return-types.php
│        │  │  │  └─ patch-type-declarations
│        │  │  └─ views
│        │  │     ├─ error.html.php
│        │  │     ├─ exception.html.php
│        │  │     ├─ exception_full.html.php
│        │  │     ├─ logs.html.php
│        │  │     ├─ trace.html.php
│        │  │     ├─ traces.html.php
│        │  │     └─ traces_text.html.php
│        │  ├─ Tests
│        │  │  ├─ Command
│        │  │  │  └─ ErrorDumpCommandTest.php
│        │  │  ├─ DebugClassLoaderTest.php
│        │  │  ├─ ErrorEnhancer
│        │  │  │  ├─ ClassNotFoundErrorEnhancerTest.php
│        │  │  │  ├─ UndefinedFunctionErrorEnhancerTest.php
│        │  │  │  └─ UndefinedMethodErrorEnhancerTest.php
│        │  │  ├─ ErrorHandlerTest.php
│        │  │  ├─ ErrorRenderer
│        │  │  │  ├─ FileLinkFormatterTest.php
│        │  │  │  ├─ HtmlErrorRendererTest.php
│        │  │  │  └─ SerializerErrorRendererTest.php
│        │  │  ├─ Exception
│        │  │  │  └─ FlattenExceptionTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ AnnotatedClass.php
│        │  │  │  ├─ casemismatch.php
│        │  │  │  ├─ ClassAlias.php
│        │  │  │  ├─ ClassWithAnnotatedParameters.php
│        │  │  │  ├─ DefinitionInEvaluatedCode.php
│        │  │  │  ├─ DeprecatedClass.php
│        │  │  │  ├─ DeprecatedInterface.php
│        │  │  │  ├─ ErrorHandlerThatUsesThePreviousOne.php
│        │  │  │  ├─ ExtendedFinalMethod.php
│        │  │  │  ├─ FinalClasses.php
│        │  │  │  ├─ FinalConstant
│        │  │  │  │  ├─ FinalConstants.php
│        │  │  │  │  ├─ FinalConstants2.php
│        │  │  │  │  ├─ FinalConstantsInterface.php
│        │  │  │  │  ├─ FinalConstantsInterface2.php
│        │  │  │  │  ├─ OverrideFinalConstant.php
│        │  │  │  │  └─ OverrideFinalConstant81.php
│        │  │  │  ├─ FinalMethod.php
│        │  │  │  ├─ FinalMethod2Trait.php
│        │  │  │  ├─ FinalProperty
│        │  │  │  │  ├─ FinalProperty.php
│        │  │  │  │  ├─ OutsideFinalProperty.php
│        │  │  │  │  └─ OverrideFinalPropertySameNamespace.php
│        │  │  │  ├─ InterfaceWithAnnotatedParameters.php
│        │  │  │  ├─ InternalClass.php
│        │  │  │  ├─ InternalInterface.php
│        │  │  │  ├─ InternalTrait.php
│        │  │  │  ├─ InternalTrait2.php
│        │  │  │  ├─ LoggerThatSetAnErrorHandler.php
│        │  │  │  ├─ NonDeprecatedInterface.php
│        │  │  │  ├─ notPsr0Bis.php
│        │  │  │  ├─ OutsideInterface.php
│        │  │  │  ├─ OverrideFinalProperty.php
│        │  │  │  ├─ OverrideOutsideFinalProperty.php
│        │  │  │  ├─ PEARClass.php
│        │  │  │  ├─ pixel.png
│        │  │  │  ├─ psr4
│        │  │  │  │  └─ Psr4CaseMismatch.php
│        │  │  │  ├─ reallyNotPsr0.php
│        │  │  │  ├─ ReturnType.php
│        │  │  │  ├─ ReturnTypeGrandParent.php
│        │  │  │  ├─ ReturnTypeInterface.php
│        │  │  │  ├─ ReturnTypeParent.php
│        │  │  │  ├─ ReturnTypeParentInterface.php
│        │  │  │  ├─ ReturnTypeParentPhp83.php
│        │  │  │  ├─ ReturnTypePhp83.php
│        │  │  │  ├─ StringErrorCodeException.php
│        │  │  │  ├─ SubClassWithAnnotatedParameters.php
│        │  │  │  ├─ Throwing.php
│        │  │  │  ├─ TraitWithAnnotatedParameters.php
│        │  │  │  ├─ TraitWithInternalMethod.php
│        │  │  │  ├─ VirtualClass.php
│        │  │  │  ├─ VirtualClassMagicCall.php
│        │  │  │  ├─ VirtualInterface.php
│        │  │  │  ├─ VirtualSubInterface.php
│        │  │  │  └─ VirtualTrait.php
│        │  │  ├─ Fixtures2
│        │  │  │  └─ RequiredTwice.php
│        │  │  ├─ HeaderMock.php
│        │  │  └─ phpt
│        │  │     ├─ debug_class_loader.phpt
│        │  │     ├─ decorate_exception_handler.phpt
│        │  │     ├─ exception_rethrown.phpt
│        │  │     └─ fatal_with_nested_handlers.phpt
│        │  └─ ThrowableUtils.php
│        ├─ event-dispatcher
│        │  ├─ Attribute
│        │  │  └─ AsEventListener.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ Debug
│        │  │  ├─ TraceableEventDispatcher.php
│        │  │  └─ WrappedListener.php
│        │  ├─ DependencyInjection
│        │  │  ├─ AddEventAliasesPass.php
│        │  │  └─ RegisterListenersPass.php
│        │  ├─ EventDispatcher.php
│        │  ├─ EventDispatcherInterface.php
│        │  ├─ EventSubscriberInterface.php
│        │  ├─ GenericEvent.php
│        │  ├─ ImmutableEventDispatcher.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  └─ Tests
│        │     ├─ ChildEventDispatcherTest.php
│        │     ├─ Debug
│        │     │  ├─ TraceableEventDispatcherTest.php
│        │     │  └─ WrappedListenerTest.php
│        │     ├─ DependencyInjection
│        │     │  └─ RegisterListenersPassTest.php
│        │     ├─ EventDispatcherTest.php
│        │     ├─ Fixtures
│        │     │  ├─ CustomEvent.php
│        │     │  ├─ TaggedInvokableListener.php
│        │     │  └─ TaggedMultiListener.php
│        │     ├─ GenericEventTest.php
│        │     └─ ImmutableEventDispatcherTest.php
│        ├─ event-dispatcher-contracts
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ Event.php
│        │  ├─ EventDispatcherInterface.php
│        │  ├─ LICENSE
│        │  └─ README.md
│        ├─ filesystem
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ Exception
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ FileNotFoundException.php
│        │  │  ├─ InvalidArgumentException.php
│        │  │  ├─ IOException.php
│        │  │  ├─ IOExceptionInterface.php
│        │  │  └─ RuntimeException.php
│        │  ├─ Filesystem.php
│        │  ├─ LICENSE
│        │  ├─ Path.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  └─ Tests
│        │     ├─ ExceptionTest.php
│        │     ├─ FilesystemTest.php
│        │     ├─ FilesystemTestCase.php
│        │     ├─ Fixtures
│        │     │  ├─ MockStream
│        │     │  │  └─ MockStream.php
│        │     │  └─ web
│        │     │     ├─ index.php
│        │     │     └─ logo_symfony_header.png
│        │     └─ PathTest.php
│        ├─ finder
│        │  ├─ CHANGELOG.md
│        │  ├─ Comparator
│        │  │  ├─ Comparator.php
│        │  │  ├─ DateComparator.php
│        │  │  └─ NumberComparator.php
│        │  ├─ composer.json
│        │  ├─ Exception
│        │  │  ├─ AccessDeniedException.php
│        │  │  └─ DirectoryNotFoundException.php
│        │  ├─ Finder.php
│        │  ├─ Gitignore.php
│        │  ├─ Glob.php
│        │  ├─ Iterator
│        │  │  ├─ CustomFilterIterator.php
│        │  │  ├─ DateRangeFilterIterator.php
│        │  │  ├─ DepthRangeFilterIterator.php
│        │  │  ├─ ExcludeDirectoryFilterIterator.php
│        │  │  ├─ FilecontentFilterIterator.php
│        │  │  ├─ FilenameFilterIterator.php
│        │  │  ├─ FileTypeFilterIterator.php
│        │  │  ├─ LazyIterator.php
│        │  │  ├─ MultiplePcreFilterIterator.php
│        │  │  ├─ PathFilterIterator.php
│        │  │  ├─ RecursiveDirectoryIterator.php
│        │  │  ├─ SizeRangeFilterIterator.php
│        │  │  ├─ SortableIterator.php
│        │  │  └─ VcsIgnoredFilterIterator.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ SplFileInfo.php
│        │  └─ Tests
│        │     ├─ Comparator
│        │     │  ├─ ComparatorTest.php
│        │     │  ├─ DateComparatorTest.php
│        │     │  └─ NumberComparatorTest.php
│        │     ├─ FinderOpenBasedirTest.php
│        │     ├─ FinderTest.php
│        │     ├─ Fixtures
│        │     │  ├─ .dot
│        │     │  │  ├─ a
│        │     │  │  └─ b
│        │     │  │     ├─ c.neon
│        │     │  │     └─ d.neon
│        │     │  ├─ A
│        │     │  │  ├─ a.dat
│        │     │  │  └─ B
│        │     │  │     ├─ ab.dat
│        │     │  │     └─ C
│        │     │  │        └─ abc.dat
│        │     │  ├─ copy
│        │     │  │  └─ A
│        │     │  │     ├─ a.dat.copy
│        │     │  │     └─ B
│        │     │  │        ├─ ab.dat.copy
│        │     │  │        └─ C
│        │     │  │           └─ abc.dat.copy
│        │     │  ├─ dolor.txt
│        │     │  ├─ gitignore
│        │     │  │  ├─ git_root
│        │     │  │  │  └─ search_root
│        │     │  │  │     ├─ b.txt
│        │     │  │  │     └─ dir
│        │     │  │  │        └─ a.txt
│        │     │  │  └─ search_root
│        │     │  │     ├─ a.txt
│        │     │  │     ├─ b.txt
│        │     │  │     ├─ c.txt
│        │     │  │     └─ dir
│        │     │  │        ├─ a.txt
│        │     │  │        ├─ b.txt
│        │     │  │        └─ c.txt
│        │     │  ├─ ipsum.txt
│        │     │  ├─ lorem.txt
│        │     │  ├─ one
│        │     │  │  ├─ .dot
│        │     │  │  ├─ a
│        │     │  │  └─ b
│        │     │  │     ├─ c.neon
│        │     │  │     └─ d.neon
│        │     │  ├─ r+e.gex[c]a(r)s
│        │     │  │  └─ dir
│        │     │  │     └─ bar.dat
│        │     │  └─ with space
│        │     │     └─ foo.txt
│        │     ├─ GitignoreTest.php
│        │     ├─ GlobTest.php
│        │     └─ Iterator
│        │        ├─ CustomFilterIteratorTest.php
│        │        ├─ DateRangeFilterIteratorTest.php
│        │        ├─ DepthRangeFilterIteratorTest.php
│        │        ├─ ExcludeDirectoryFilterIteratorTest.php
│        │        ├─ FilecontentFilterIteratorTest.php
│        │        ├─ FilenameFilterIteratorTest.php
│        │        ├─ FileTypeFilterIteratorTest.php
│        │        ├─ InnerNameIterator.php
│        │        ├─ Iterator.php
│        │        ├─ IteratorTestCase.php
│        │        ├─ LazyIteratorTest.php
│        │        ├─ MockFileListIterator.php
│        │        ├─ MockSplFileInfo.php
│        │        ├─ MultiplePcreFilterIteratorTest.php
│        │        ├─ PathFilterIteratorTest.php
│        │        ├─ RealIteratorTestCase.php
│        │        ├─ RecursiveDirectoryIteratorTest.php
│        │        ├─ SizeRangeFilterIteratorTest.php
│        │        ├─ SortableIteratorTest.php
│        │        ├─ VcsIgnoredFilterIteratorTest.php
│        │        └─ VfsIteratorTestTrait.php
│        ├─ flex
│        │  ├─ .php-cs-fixer.dist.php
│        │  ├─ composer.json
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ src
│        │  │  ├─ Command
│        │  │  │  ├─ DumpEnvCommand.php
│        │  │  │  ├─ InstallRecipesCommand.php
│        │  │  │  ├─ RecipesCommand.php
│        │  │  │  └─ UpdateRecipesCommand.php
│        │  │  ├─ Configurator
│        │  │  │  ├─ AbstractConfigurator.php
│        │  │  │  ├─ AddLinesConfigurator.php
│        │  │  │  ├─ BundlesConfigurator.php
│        │  │  │  ├─ ComposerCommandsConfigurator.php
│        │  │  │  ├─ ComposerScriptsConfigurator.php
│        │  │  │  ├─ ContainerConfigurator.php
│        │  │  │  ├─ CopyFromPackageConfigurator.php
│        │  │  │  ├─ CopyFromRecipeConfigurator.php
│        │  │  │  ├─ DockerComposeConfigurator.php
│        │  │  │  ├─ DockerfileConfigurator.php
│        │  │  │  ├─ DotenvConfigurator.php
│        │  │  │  ├─ EnvConfigurator.php
│        │  │  │  ├─ GitignoreConfigurator.php
│        │  │  │  └─ MakefileConfigurator.php
│        │  │  ├─ Configurator.php
│        │  │  ├─ Downloader.php
│        │  │  ├─ Event
│        │  │  │  └─ UpdateEvent.php
│        │  │  ├─ Flex.php
│        │  │  ├─ GithubApi.php
│        │  │  ├─ InformationOperation.php
│        │  │  ├─ Lock.php
│        │  │  ├─ Options.php
│        │  │  ├─ PackageFilter.php
│        │  │  ├─ PackageJsonSynchronizer.php
│        │  │  ├─ PackageResolver.php
│        │  │  ├─ Path.php
│        │  │  ├─ Recipe.php
│        │  │  ├─ Response.php
│        │  │  ├─ ScriptExecutor.php
│        │  │  ├─ SymfonyBundle.php
│        │  │  ├─ SymfonyPackInstaller.php
│        │  │  ├─ Unpack
│        │  │  │  ├─ Operation.php
│        │  │  │  └─ Result.php
│        │  │  ├─ Unpacker.php
│        │  │  └─ Update
│        │  │     ├─ DiffHelper.php
│        │  │     ├─ RecipePatch.php
│        │  │     ├─ RecipePatcher.php
│        │  │     └─ RecipeUpdate.php
│        │  └─ tests
│        │     ├─ bootstrap.php
│        │     ├─ Command
│        │     │  ├─ DumpEnvCommandTest.php
│        │     │  ├─ InstallRecipesCommandTest.php
│        │     │  └─ UpdateRecipesCommandTest.php
│        │     ├─ Configurator
│        │     │  ├─ AddLinesConfiguratorTest.php
│        │     │  ├─ BundlesConfiguratorTest.php
│        │     │  ├─ ComposerCommandConfiguratorTest.php
│        │     │  ├─ ComposerScriptsConfiguratorTest.php
│        │     │  ├─ ContainerConfiguratorTest.php
│        │     │  ├─ CopyDirectoryFromPackageConfiguratorTest.php
│        │     │  ├─ CopyFromPackageConfiguratorTest.php
│        │     │  ├─ CopyFromRecipeConfiguratorTest.php
│        │     │  ├─ DockerComposeConfiguratorTest.php
│        │     │  ├─ DockerfileConfiguratorTest.php
│        │     │  ├─ DotenvConfiguratorTest.php
│        │     │  ├─ EnvConfiguratorTest.php
│        │     │  ├─ GitignoreConfiguratorTest.php
│        │     │  └─ MakefileConfiguratorTest.php
│        │     ├─ Fixtures
│        │     │  ├─ packageJson
│        │     │  │  ├─ assets
│        │     │  │  │  └─ controllers.json
│        │     │  │  ├─ elevated_dependencies_package.json
│        │     │  │  ├─ package.json
│        │     │  │  ├─ stricter_constraints_package.json
│        │     │  │  └─ vendor
│        │     │  │     └─ symfony
│        │     │  │        ├─ existing-package
│        │     │  │        │  └─ Resources
│        │     │  │        │     └─ assets
│        │     │  │        │        └─ package.json
│        │     │  │        ├─ importmap-invalid-constraint-package
│        │     │  │        │  └─ assets
│        │     │  │        │     └─ package.json
│        │     │  │        ├─ new-package
│        │     │  │        │  └─ assets
│        │     │  │        │     └─ package.json
│        │     │  │        └─ package-no-file-package
│        │     │  │           └─ assets
│        │     │  │              └─ package.json
│        │     │  ├─ phpunit.xml.dist
│        │     │  ├─ update_recipes
│        │     │  │  ├─ composer.json
│        │     │  │  ├─ console
│        │     │  │  └─ symfony.lock
│        │     │  └─ vendor
│        │     │     ├─ composer
│        │     │     │  └─ ca-bundle
│        │     │     │     └─ src
│        │     │     │        └─ CaBundle.php
│        │     │     ├─ doctrine
│        │     │     │  └─ doctrine-cache-bundle
│        │     │     │     └─ DoctrineCacheBundle.php
│        │     │     ├─ dunglas
│        │     │     │  └─ sylius-acme-plugin
│        │     │     │     └─ src
│        │     │     │        └─ DunglasSyliusAcmePlugin.php
│        │     │     ├─ easycorp
│        │     │     │  ├─ easy-deploy-bundle
│        │     │     │  │  └─ src
│        │     │     │  │     └─ EasyDeployBundle.php
│        │     │     │  └─ easy-security-bundle
│        │     │     │     └─ EasySecurityBundle.php
│        │     │     ├─ eightpoints
│        │     │     │  └─ guzzle-bundle
│        │     │     │     └─ EightPoints
│        │     │     │        └─ Bundle
│        │     │     │           └─ GuzzleBundle
│        │     │     │              └─ GuzzleBundle.php
│        │     │     ├─ sylius
│        │     │     │  └─ shop-api-plugin
│        │     │     │     └─ src
│        │     │     │        └─ ShopApiPlugin.php
│        │     │     ├─ symfony
│        │     │     │  ├─ debug-bundle
│        │     │     │  │  └─ DebugBundle.php
│        │     │     │  ├─ dummy
│        │     │     │  │  ├─ FirstDummyBundle
│        │     │     │  │  │  └─ FirstDummyBundle.php
│        │     │     │  │  └─ SecondDummyBundle
│        │     │     │  │     └─ SecondDummyBundle.php
│        │     │     │  └─ nouse-bundle
│        │     │     │     └─ NouseBundle.php
│        │     │     ├─ symfony-cmf
│        │     │     │  └─ routing-bundle
│        │     │     │     └─ CmfRoutingBundle.php
│        │     │     └─ web-token
│        │     │        └─ jwt-bundle
│        │     │           └─ JoseFrameworkBundle.php
│        │     ├─ FlexTest.php
│        │     ├─ OptionsTest.php
│        │     ├─ PackageFilterTest.php
│        │     ├─ PackageJsonSynchronizerTest.php
│        │     ├─ PackageResolverTest.php
│        │     ├─ PathTest.php
│        │     ├─ ScriptExecutorTest.php
│        │     ├─ SymfonyBundleTest.php
│        │     ├─ UnpackerTest.php
│        │     └─ Update
│        │        ├─ DiffHelperTest.php
│        │        ├─ RecipePatcherTest.php
│        │        ├─ RecipePatchTest.php
│        │        └─ RecipeUpdateTest.php
│        ├─ framework-bundle
│        │  ├─ CacheWarmer
│        │  │  ├─ AbstractPhpFileCacheWarmer.php
│        │  │  ├─ CachePoolClearerCacheWarmer.php
│        │  │  ├─ ConfigBuilderCacheWarmer.php
│        │  │  ├─ RouterCacheWarmer.php
│        │  │  ├─ SerializerCacheWarmer.php
│        │  │  ├─ TranslationsCacheWarmer.php
│        │  │  └─ ValidatorCacheWarmer.php
│        │  ├─ CHANGELOG.md
│        │  ├─ Command
│        │  │  ├─ AboutCommand.php
│        │  │  ├─ AbstractConfigCommand.php
│        │  │  ├─ AssetsInstallCommand.php
│        │  │  ├─ BuildDebugContainerTrait.php
│        │  │  ├─ CacheClearCommand.php
│        │  │  ├─ CachePoolClearCommand.php
│        │  │  ├─ CachePoolDeleteCommand.php
│        │  │  ├─ CachePoolInvalidateTagsCommand.php
│        │  │  ├─ CachePoolListCommand.php
│        │  │  ├─ CachePoolPruneCommand.php
│        │  │  ├─ CacheWarmupCommand.php
│        │  │  ├─ ConfigDebugCommand.php
│        │  │  ├─ ConfigDumpReferenceCommand.php
│        │  │  ├─ ContainerDebugCommand.php
│        │  │  ├─ ContainerLintCommand.php
│        │  │  ├─ DebugAutowiringCommand.php
│        │  │  ├─ EventDispatcherDebugCommand.php
│        │  │  ├─ RouterDebugCommand.php
│        │  │  ├─ RouterMatchCommand.php
│        │  │  ├─ SecretsDecryptToLocalCommand.php
│        │  │  ├─ SecretsEncryptFromLocalCommand.php
│        │  │  ├─ SecretsGenerateKeysCommand.php
│        │  │  ├─ SecretsListCommand.php
│        │  │  ├─ SecretsRemoveCommand.php
│        │  │  ├─ SecretsRevealCommand.php
│        │  │  ├─ SecretsSetCommand.php
│        │  │  ├─ TranslationDebugCommand.php
│        │  │  ├─ TranslationExtractCommand.php
│        │  │  ├─ TranslationUpdateCommand.php
│        │  │  ├─ WorkflowDumpCommand.php
│        │  │  ├─ XliffLintCommand.php
│        │  │  └─ YamlLintCommand.php
│        │  ├─ composer.json
│        │  ├─ Console
│        │  │  ├─ Application.php
│        │  │  ├─ Descriptor
│        │  │  │  ├─ Descriptor.php
│        │  │  │  ├─ JsonDescriptor.php
│        │  │  │  ├─ MarkdownDescriptor.php
│        │  │  │  ├─ TextDescriptor.php
│        │  │  │  └─ XmlDescriptor.php
│        │  │  └─ Helper
│        │  │     └─ DescriptorHelper.php
│        │  ├─ Controller
│        │  │  ├─ AbstractController.php
│        │  │  ├─ ControllerResolver.php
│        │  │  ├─ RedirectController.php
│        │  │  └─ TemplateController.php
│        │  ├─ DataCollector
│        │  │  ├─ AbstractDataCollector.php
│        │  │  ├─ RouterDataCollector.php
│        │  │  └─ TemplateAwareDataCollectorInterface.php
│        │  ├─ DependencyInjection
│        │  │  ├─ Compiler
│        │  │  │  ├─ AddDebugLogProcessorPass.php
│        │  │  │  ├─ AssetsContextPass.php
│        │  │  │  ├─ ContainerBuilderDebugDumpPass.php
│        │  │  │  ├─ ErrorLoggerCompilerPass.php
│        │  │  │  ├─ ProfilerPass.php
│        │  │  │  ├─ RemoveUnusedSessionMarshallingHandlerPass.php
│        │  │  │  ├─ TestServiceContainerRealRefPass.php
│        │  │  │  ├─ TestServiceContainerWeakRefPass.php
│        │  │  │  ├─ TranslationLintCommandPass.php
│        │  │  │  ├─ TranslationUpdateCommandPass.php
│        │  │  │  └─ UnusedTagsPass.php
│        │  │  ├─ Configuration.php
│        │  │  ├─ FrameworkExtension.php
│        │  │  └─ VirtualRequestStackPass.php
│        │  ├─ EventListener
│        │  │  ├─ ConsoleProfilerListener.php
│        │  │  └─ SuggestMissingPackageSubscriber.php
│        │  ├─ FrameworkBundle.php
│        │  ├─ HttpCache
│        │  │  └─ HttpCache.php
│        │  ├─ Kernel
│        │  │  └─ MicroKernelTrait.php
│        │  ├─ KernelBrowser.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Resources
│        │  │  ├─ bin
│        │  │  │  └─ check-unused-known-tags.php
│        │  │  └─ config
│        │  │     ├─ assets.php
│        │  │     ├─ asset_mapper.php
│        │  │     ├─ cache.php
│        │  │     ├─ cache_debug.php
│        │  │     ├─ collectors.php
│        │  │     ├─ console.php
│        │  │     ├─ debug.php
│        │  │     ├─ debug_prod.php
│        │  │     ├─ error_renderer.php
│        │  │     ├─ esi.php
│        │  │     ├─ form.php
│        │  │     ├─ form_csrf.php
│        │  │     ├─ form_debug.php
│        │  │     ├─ fragment_listener.php
│        │  │     ├─ fragment_renderer.php
│        │  │     ├─ html_sanitizer.php
│        │  │     ├─ http_client.php
│        │  │     ├─ http_client_debug.php
│        │  │     ├─ identity_translator.php
│        │  │     ├─ json_streamer.php
│        │  │     ├─ lock.php
│        │  │     ├─ mailer.php
│        │  │     ├─ mailer_debug.php
│        │  │     ├─ mailer_transports.php
│        │  │     ├─ mailer_webhook.php
│        │  │     ├─ messenger.php
│        │  │     ├─ messenger_debug.php
│        │  │     ├─ mime_type.php
│        │  │     ├─ notifier.php
│        │  │     ├─ notifier_debug.php
│        │  │     ├─ notifier_transports.php
│        │  │     ├─ notifier_webhook.php
│        │  │     ├─ object_mapper.php
│        │  │     ├─ process.php
│        │  │     ├─ profiling.php
│        │  │     ├─ property_access.php
│        │  │     ├─ property_info.php
│        │  │     ├─ rate_limiter.php
│        │  │     ├─ remote_event.php
│        │  │     ├─ request.php
│        │  │     ├─ routing
│        │  │     │  ├─ errors.php
│        │  │     │  ├─ errors.xml
│        │  │     │  ├─ webhook.php
│        │  │     │  └─ webhook.xml
│        │  │     ├─ routing.php
│        │  │     ├─ scheduler.php
│        │  │     ├─ schema
│        │  │     │  └─ symfony-1.0.xsd
│        │  │     ├─ secrets.php
│        │  │     ├─ security_csrf.php
│        │  │     ├─ semaphore.php
│        │  │     ├─ serializer.php
│        │  │     ├─ serializer_debug.php
│        │  │     ├─ services.php
│        │  │     ├─ session.php
│        │  │     ├─ ssi.php
│        │  │     ├─ test.php
│        │  │     ├─ translation.php
│        │  │     ├─ translation_debug.php
│        │  │     ├─ translation_providers.php
│        │  │     ├─ type_info.php
│        │  │     ├─ uid.php
│        │  │     ├─ validator.php
│        │  │     ├─ validator_debug.php
│        │  │     ├─ web.php
│        │  │     ├─ webhook.php
│        │  │     ├─ web_link.php
│        │  │     ├─ workflow.php
│        │  │     └─ workflow_debug.php
│        │  ├─ Routing
│        │  │  ├─ Attribute
│        │  │  │  └─ AsRoutingConditionService.php
│        │  │  ├─ AttributeRouteControllerLoader.php
│        │  │  ├─ DelegatingLoader.php
│        │  │  ├─ RedirectableCompiledUrlMatcher.php
│        │  │  ├─ RouteLoaderInterface.php
│        │  │  └─ Router.php
│        │  ├─ Secrets
│        │  │  ├─ AbstractVault.php
│        │  │  ├─ DotenvVault.php
│        │  │  └─ SodiumVault.php
│        │  ├─ Test
│        │  │  ├─ BrowserKitAssertionsTrait.php
│        │  │  ├─ DomCrawlerAssertionsTrait.php
│        │  │  ├─ HttpClientAssertionsTrait.php
│        │  │  ├─ KernelTestCase.php
│        │  │  ├─ MailerAssertionsTrait.php
│        │  │  ├─ NotificationAssertionsTrait.php
│        │  │  ├─ TestBrowserToken.php
│        │  │  ├─ TestContainer.php
│        │  │  ├─ WebTestAssertionsTrait.php
│        │  │  └─ WebTestCase.php
│        │  ├─ Tests
│        │  │  ├─ CacheWarmer
│        │  │  │  ├─ ConfigBuilderCacheWarmerTest.php
│        │  │  │  ├─ RouterCacheWarmerTest.php
│        │  │  │  ├─ SerializerCacheWarmerTest.php
│        │  │  │  └─ ValidatorCacheWarmerTest.php
│        │  │  ├─ Command
│        │  │  │  ├─ AboutCommand
│        │  │  │  │  ├─ AboutCommandTest.php
│        │  │  │  │  └─ Fixture
│        │  │  │  │     └─ TestAppKernel.php
│        │  │  │  ├─ CacheClearCommand
│        │  │  │  │  ├─ CacheClearCommandTest.php
│        │  │  │  │  └─ Fixture
│        │  │  │  │     ├─ config.yml
│        │  │  │  │     └─ TestAppKernel.php
│        │  │  │  ├─ CachePoolClearCommandTest.php
│        │  │  │  ├─ CachePoolDeleteCommandTest.php
│        │  │  │  ├─ CachePoolInvalidateTagsCommandTest.php
│        │  │  │  ├─ CachePruneCommandTest.php
│        │  │  │  ├─ EventDispatcherDebugCommandTest.php
│        │  │  │  ├─ RouterMatchCommandTest.php
│        │  │  │  ├─ SecretsListCommandTest.php
│        │  │  │  ├─ SecretsRemoveCommandTest.php
│        │  │  │  ├─ SecretsRevealCommandTest.php
│        │  │  │  ├─ SecretsSetCommandTest.php
│        │  │  │  ├─ TranslationDebugCommandTest.php
│        │  │  │  ├─ TranslationExtractCommandCompletionTest.php
│        │  │  │  ├─ TranslationExtractCommandTest.php
│        │  │  │  ├─ WorkflowDumpCommandTest.php
│        │  │  │  ├─ XliffLintCommandTest.php
│        │  │  │  └─ YamlLintCommandTest.php
│        │  │  ├─ Console
│        │  │  │  ├─ ApplicationTest.php
│        │  │  │  └─ Descriptor
│        │  │  │     ├─ AbstractDescriptorTestCase.php
│        │  │  │     ├─ JsonDescriptorTest.php
│        │  │  │     ├─ MarkdownDescriptorTest.php
│        │  │  │     ├─ ObjectsProvider.php
│        │  │  │     ├─ TextDescriptorTest.php
│        │  │  │     └─ XmlDescriptorTest.php
│        │  │  ├─ Controller
│        │  │  │  ├─ AbstractControllerTest.php
│        │  │  │  ├─ ControllerResolverTest.php
│        │  │  │  ├─ RedirectControllerTest.php
│        │  │  │  ├─ TemplateControllerTest.php
│        │  │  │  └─ TestAbstractController.php
│        │  │  ├─ DataCollector
│        │  │  │  └─ RouterDataCollectorTest.php
│        │  │  ├─ DependencyInjection
│        │  │  │  ├─ Compiler
│        │  │  │  │  ├─ ProfilerPassTest.php
│        │  │  │  │  ├─ TestServiceContainerRefPassesTest.php
│        │  │  │  │  ├─ UnusedTagsPassTest.php
│        │  │  │  │  └─ UnusedTagsPassUtils.php
│        │  │  │  ├─ config
│        │  │  │  │  ├─ serializer
│        │  │  │  │  │  └─ foo.yml
│        │  │  │  │  └─ validator
│        │  │  │  │     └─ foo.xml
│        │  │  │  ├─ ConfigurationTest.php
│        │  │  │  ├─ Fixtures
│        │  │  │  │  ├─ CustomPathBundle
│        │  │  │  │  │  ├─ Resources
│        │  │  │  │  │  │  └─ config
│        │  │  │  │  │  │     ├─ validation.xml
│        │  │  │  │  │  │     └─ validation.yml
│        │  │  │  │  │  └─ src
│        │  │  │  │  │     └─ CustomPathBundle.php
│        │  │  │  │  ├─ php
│        │  │  │  │  │  ├─ assets.php
│        │  │  │  │  │  ├─ assets_disabled.php
│        │  │  │  │  │  ├─ assets_version_strategy_as_service.php
│        │  │  │  │  │  ├─ asset_mapper_without_assets.php
│        │  │  │  │  │  ├─ cache.php
│        │  │  │  │  │  ├─ cache_app_redis_tag_aware.php
│        │  │  │  │  │  ├─ cache_app_redis_tag_aware_pool.php
│        │  │  │  │  │  ├─ csrf.php
│        │  │  │  │  │  ├─ csrf_needs_session.php
│        │  │  │  │  │  ├─ default_config.php
│        │  │  │  │  │  ├─ esi_and_ssi_without_fragments.php
│        │  │  │  │  │  ├─ esi_disabled.php
│        │  │  │  │  │  ├─ exceptions.php
│        │  │  │  │  │  ├─ form_csrf_disabled.php
│        │  │  │  │  │  ├─ form_csrf_field_attr.php
│        │  │  │  │  │  ├─ form_default_csrf.php
│        │  │  │  │  │  ├─ form_no_csrf.php
│        │  │  │  │  │  ├─ fragments_and_hinclude.php
│        │  │  │  │  │  ├─ full.php
│        │  │  │  │  │  ├─ html_sanitizer.php
│        │  │  │  │  │  ├─ html_sanitizer_default_allowed_link_and_media_hosts.php
│        │  │  │  │  │  ├─ html_sanitizer_default_config.php
│        │  │  │  │  │  ├─ http_client_default_options.php
│        │  │  │  │  │  ├─ http_client_full_default_options.php
│        │  │  │  │  │  ├─ http_client_mock_response_factory.php
│        │  │  │  │  │  ├─ http_client_override_default_options.php
│        │  │  │  │  │  ├─ http_client_rate_limiter.php
│        │  │  │  │  │  ├─ http_client_retry.php
│        │  │  │  │  │  ├─ http_client_scoped_without_query_option.php
│        │  │  │  │  │  ├─ http_client_xml_key.php
│        │  │  │  │  │  ├─ json_streamer.php
│        │  │  │  │  │  ├─ lock.php
│        │  │  │  │  │  ├─ lock_named.php
│        │  │  │  │  │  ├─ lock_service.php
│        │  │  │  │  │  ├─ mailer.php
│        │  │  │  │  │  ├─ mailer_with_disabled_message_bus.php
│        │  │  │  │  │  ├─ mailer_with_dsn.php
│        │  │  │  │  │  ├─ mailer_with_specific_message_bus.php
│        │  │  │  │  │  ├─ mailer_with_transports.php
│        │  │  │  │  │  ├─ messenger.php
│        │  │  │  │  │  ├─ messenger_disabled.php
│        │  │  │  │  │  ├─ messenger_middleware_factory_erroneous_format.php
│        │  │  │  │  │  ├─ messenger_multiple_buses_without_deduplicate_middleware.php
│        │  │  │  │  │  ├─ messenger_multiple_buses_with_deduplicate_middleware.php
│        │  │  │  │  │  ├─ messenger_multiple_failure_transports.php
│        │  │  │  │  │  ├─ messenger_multiple_failure_transports_global.php
│        │  │  │  │  │  ├─ messenger_routing.php
│        │  │  │  │  │  ├─ messenger_routing_invalid_transport.php
│        │  │  │  │  │  ├─ messenger_routing_invalid_wildcard.php
│        │  │  │  │  │  ├─ messenger_routing_single.php
│        │  │  │  │  │  ├─ messenger_transport.php
│        │  │  │  │  │  ├─ messenger_transports.php
│        │  │  │  │  │  ├─ notifier.php
│        │  │  │  │  │  ├─ notifier_without_mailer.php
│        │  │  │  │  │  ├─ notifier_without_messenger.php
│        │  │  │  │  │  ├─ notifier_without_transports.php
│        │  │  │  │  │  ├─ notifier_with_disabled_message_bus.php
│        │  │  │  │  │  ├─ notifier_with_specific_message_bus.php
│        │  │  │  │  │  ├─ php_errors_disabled.php
│        │  │  │  │  │  ├─ php_errors_enabled.php
│        │  │  │  │  │  ├─ php_errors_log_level.php
│        │  │  │  │  │  ├─ php_errors_log_levels.php
│        │  │  │  │  │  ├─ profiler.php
│        │  │  │  │  │  ├─ property_accessor.php
│        │  │  │  │  │  ├─ property_info.php
│        │  │  │  │  │  ├─ property_info_with_constructor_extractor.php
│        │  │  │  │  │  ├─ request.php
│        │  │  │  │  │  ├─ semaphore.php
│        │  │  │  │  │  ├─ semaphore_named.php
│        │  │  │  │  │  ├─ semaphore_service.php
│        │  │  │  │  │  ├─ serializer_disabled.php
│        │  │  │  │  │  ├─ serializer_enabled.php
│        │  │  │  │  │  ├─ serializer_mapping.php
│        │  │  │  │  │  ├─ serializer_mapping_without_annotations.php
│        │  │  │  │  │  ├─ serializer_without_translator.php
│        │  │  │  │  │  ├─ session.php
│        │  │  │  │  │  ├─ session_cookie_secure_auto.php
│        │  │  │  │  │  ├─ ssi_disabled.php
│        │  │  │  │  │  ├─ translator_cache_dir_disabled.php
│        │  │  │  │  │  ├─ translator_fallbacks.php
│        │  │  │  │  │  ├─ translator_globals.php
│        │  │  │  │  │  ├─ translator_without_globals.php
│        │  │  │  │  │  ├─ trusted_proxies_private_ranges.php
│        │  │  │  │  │  ├─ type_info.php
│        │  │  │  │  │  ├─ validation_attributes.php
│        │  │  │  │  │  ├─ validation_auto_mapping.php
│        │  │  │  │  │  ├─ validation_email_validation_mode.php
│        │  │  │  │  │  ├─ validation_mapping.php
│        │  │  │  │  │  ├─ validation_multiple_static_methods.php
│        │  │  │  │  │  ├─ validation_no_static_method.php
│        │  │  │  │  │  ├─ validation_translation_domain.php
│        │  │  │  │  │  ├─ webhook.php
│        │  │  │  │  │  ├─ webhook_without_serializer.php
│        │  │  │  │  │  ├─ web_link.php
│        │  │  │  │  │  ├─ workflows.php
│        │  │  │  │  │  ├─ workflows_enabled.php
│        │  │  │  │  │  ├─ workflows_explicitly_enabled.php
│        │  │  │  │  │  ├─ workflows_explicitly_enabled_named_workflows.php
│        │  │  │  │  │  ├─ workflow_not_valid.php
│        │  │  │  │  │  ├─ workflow_without_support_and_support_strategy.php
│        │  │  │  │  │  ├─ workflow_with_guard_expression.php
│        │  │  │  │  │  ├─ workflow_with_multiple_transitions_with_same_name.php
│        │  │  │  │  │  ├─ workflow_with_no_events_to_dispatch.php
│        │  │  │  │  │  ├─ workflow_with_specified_events_to_dispatch.php
│        │  │  │  │  │  └─ workflow_with_support_and_support_strategy.php
│        │  │  │  │  ├─ TestBundle
│        │  │  │  │  │  ├─ Resources
│        │  │  │  │  │  │  └─ config
│        │  │  │  │  │  │     ├─ serialization.xml
│        │  │  │  │  │  │     ├─ serialization.yml
│        │  │  │  │  │  │     ├─ serializer_mapping
│        │  │  │  │  │  │     │  ├─ files
│        │  │  │  │  │  │     │  │  ├─ foo.xml
│        │  │  │  │  │  │     │  │  └─ foo.yml
│        │  │  │  │  │  │     │  ├─ serialization.yaml
│        │  │  │  │  │  │     │  └─ serialization.yml
│        │  │  │  │  │  │     ├─ validation.xml
│        │  │  │  │  │  │     ├─ validation.yml
│        │  │  │  │  │  │     └─ validation_mapping
│        │  │  │  │  │  │        ├─ files
│        │  │  │  │  │  │        │  ├─ foo.xml
│        │  │  │  │  │  │        │  └─ foo.yml
│        │  │  │  │  │  │        ├─ validation.yaml
│        │  │  │  │  │  │        └─ validation.yml
│        │  │  │  │  │  └─ TestBundle.php
│        │  │  │  │  ├─ translations
│        │  │  │  │  │  ├─ domain.with.dots.en.yml
│        │  │  │  │  │  └─ test_paths.en.yml
│        │  │  │  │  ├─ Workflow
│        │  │  │  │  │  └─ Validator
│        │  │  │  │  │     └─ DefinitionValidator.php
│        │  │  │  │  ├─ xml
│        │  │  │  │  │  ├─ assets.xml
│        │  │  │  │  │  ├─ assets_disabled.xml
│        │  │  │  │  │  ├─ assets_version_strategy_as_service.xml
│        │  │  │  │  │  ├─ asset_mapper.xml
│        │  │  │  │  │  ├─ asset_mapper_without_assets.xml
│        │  │  │  │  │  ├─ cache.xml
│        │  │  │  │  │  ├─ cache_app_redis_tag_aware.xml
│        │  │  │  │  │  ├─ cache_app_redis_tag_aware_pool.xml
│        │  │  │  │  │  ├─ csrf.xml
│        │  │  │  │  │  ├─ csrf_disabled.xml
│        │  │  │  │  │  ├─ csrf_needs_session.xml
│        │  │  │  │  │  ├─ default_config.xml
│        │  │  │  │  │  ├─ esi_and_ssi_without_fragments.xml
│        │  │  │  │  │  ├─ esi_disabled.xml
│        │  │  │  │  │  ├─ exceptions.xml
│        │  │  │  │  │  ├─ form_csrf_disabled.xml
│        │  │  │  │  │  ├─ form_csrf_field_attr.xml
│        │  │  │  │  │  ├─ form_default_csrf.xml
│        │  │  │  │  │  ├─ form_no_csrf.xml
│        │  │  │  │  │  ├─ fragments_and_hinclude.xml
│        │  │  │  │  │  ├─ full.xml
│        │  │  │  │  │  ├─ html_sanitizer.xml
│        │  │  │  │  │  ├─ html_sanitizer_default_allowed_link_and_media_hosts.xml
│        │  │  │  │  │  ├─ html_sanitizer_default_config.xml
│        │  │  │  │  │  ├─ http_client_default_options.xml
│        │  │  │  │  │  ├─ http_client_full_default_options.xml
│        │  │  │  │  │  ├─ http_client_mock_response_factory.xml
│        │  │  │  │  │  ├─ http_client_override_default_options.xml
│        │  │  │  │  │  ├─ http_client_rate_limiter.xml
│        │  │  │  │  │  ├─ http_client_retry.xml
│        │  │  │  │  │  ├─ http_client_scoped_without_query_option.xml
│        │  │  │  │  │  ├─ http_client_xml_key.xml
│        │  │  │  │  │  ├─ json_streamer.xml
│        │  │  │  │  │  ├─ lock.xml
│        │  │  │  │  │  ├─ lock_named.xml
│        │  │  │  │  │  ├─ lock_service.xml
│        │  │  │  │  │  ├─ mailer_with_disabled_message_bus.xml
│        │  │  │  │  │  ├─ mailer_with_dsn.xml
│        │  │  │  │  │  ├─ mailer_with_specific_message_bus.xml
│        │  │  │  │  │  ├─ mailer_with_transports.xml
│        │  │  │  │  │  ├─ messenger.xml
│        │  │  │  │  │  ├─ messenger_disabled.xml
│        │  │  │  │  │  ├─ messenger_multiple_buses_without_deduplicate_middleware.xml
│        │  │  │  │  │  ├─ messenger_multiple_buses_with_deduplicate_middleware.xml
│        │  │  │  │  │  ├─ messenger_multiple_failure_transports.xml
│        │  │  │  │  │  ├─ messenger_multiple_failure_transports_global.xml
│        │  │  │  │  │  ├─ messenger_routing.xml
│        │  │  │  │  │  ├─ messenger_routing_invalid_transport.xml
│        │  │  │  │  │  ├─ messenger_routing_invalid_wildcard.xml
│        │  │  │  │  │  ├─ messenger_routing_single.xml
│        │  │  │  │  │  ├─ messenger_schedule.xml
│        │  │  │  │  │  ├─ messenger_transport.xml
│        │  │  │  │  │  ├─ messenger_transports.xml
│        │  │  │  │  │  ├─ notifier.xml
│        │  │  │  │  │  ├─ notifier_without_mailer.xml
│        │  │  │  │  │  ├─ notifier_without_messenger.xml
│        │  │  │  │  │  ├─ notifier_without_transports.xml
│        │  │  │  │  │  ├─ notifier_with_disabled_message_bus.xml
│        │  │  │  │  │  ├─ notifier_with_specific_message_bus.xml
│        │  │  │  │  │  ├─ php_errors_disabled.xml
│        │  │  │  │  │  ├─ php_errors_enabled.xml
│        │  │  │  │  │  ├─ php_errors_log_level.xml
│        │  │  │  │  │  ├─ php_errors_log_levels.xml
│        │  │  │  │  │  ├─ profiler.xml
│        │  │  │  │  │  ├─ property_accessor.xml
│        │  │  │  │  │  ├─ property_info.xml
│        │  │  │  │  │  ├─ property_info_with_constructor_extractor.xml
│        │  │  │  │  │  ├─ rate_limiter.xml
│        │  │  │  │  │  ├─ request.xml
│        │  │  │  │  │  ├─ semaphore.xml
│        │  │  │  │  │  ├─ semaphore_named.xml
│        │  │  │  │  │  ├─ semaphore_service.xml
│        │  │  │  │  │  ├─ serializer_disabled.xml
│        │  │  │  │  │  ├─ serializer_enabled.xml
│        │  │  │  │  │  ├─ serializer_mapping.xml
│        │  │  │  │  │  ├─ serializer_mapping_without_annotations.xml
│        │  │  │  │  │  ├─ serializer_without_translator.xml
│        │  │  │  │  │  ├─ session.xml
│        │  │  │  │  │  ├─ session_cookie_secure_auto.xml
│        │  │  │  │  │  ├─ ssi_disabled.xml
│        │  │  │  │  │  ├─ translator_cache_dir_disabled.xml
│        │  │  │  │  │  ├─ translator_fallbacks.xml
│        │  │  │  │  │  ├─ translator_globals.xml
│        │  │  │  │  │  ├─ translator_without_globals.xml
│        │  │  │  │  │  ├─ trusted_proxies_private_ranges.xml
│        │  │  │  │  │  ├─ type_info.xml
│        │  │  │  │  │  ├─ validation_attributes.xml
│        │  │  │  │  │  ├─ validation_auto_mapping.xml
│        │  │  │  │  │  ├─ validation_email_validation_mode.xml
│        │  │  │  │  │  ├─ validation_mapping.xml
│        │  │  │  │  │  ├─ validation_multiple_static_methods.xml
│        │  │  │  │  │  ├─ validation_no_static_method.xml
│        │  │  │  │  │  ├─ validation_translation_domain.xml
│        │  │  │  │  │  ├─ webhook.xml
│        │  │  │  │  │  ├─ webhook_without_serializer.xml
│        │  │  │  │  │  ├─ web_link.xml
│        │  │  │  │  │  ├─ workflows.xml
│        │  │  │  │  │  ├─ workflows_enabled.xml
│        │  │  │  │  │  ├─ workflows_explicitly_enabled.xml
│        │  │  │  │  │  ├─ workflows_explicitly_enabled_named_workflows.xml
│        │  │  │  │  │  ├─ workflow_not_valid.xml
│        │  │  │  │  │  ├─ workflow_without_support_and_support_strategy.xml
│        │  │  │  │  │  ├─ workflow_with_guard_expression.xml
│        │  │  │  │  │  ├─ workflow_with_multiple_transitions_with_same_name.xml
│        │  │  │  │  │  ├─ workflow_with_no_events_to_dispatch.xml
│        │  │  │  │  │  ├─ workflow_with_specified_events_to_dispatch.xml
│        │  │  │  │  │  └─ workflow_with_support_and_support_strategy.xml
│        │  │  │  │  └─ yml
│        │  │  │  │     ├─ assets.yml
│        │  │  │  │     ├─ assets_disabled.yml
│        │  │  │  │     ├─ assets_version_strategy_as_service.yml
│        │  │  │  │     ├─ asset_mapper_without_assets.yml
│        │  │  │  │     ├─ cache.yml
│        │  │  │  │     ├─ cache_app_redis_tag_aware.yml
│        │  │  │  │     ├─ cache_app_redis_tag_aware_pool.yml
│        │  │  │  │     ├─ csrf.yml
│        │  │  │  │     ├─ csrf_needs_session.yml
│        │  │  │  │     ├─ default_config.yml
│        │  │  │  │     ├─ esi_and_ssi_without_fragments.yml
│        │  │  │  │     ├─ esi_disabled.yml
│        │  │  │  │     ├─ exceptions.yml
│        │  │  │  │     ├─ form_csrf_disabled.yml
│        │  │  │  │     ├─ form_csrf_field_attr.yml
│        │  │  │  │     ├─ form_default_csrf.yml
│        │  │  │  │     ├─ form_no_csrf.yml
│        │  │  │  │     ├─ fragments_and_hinclude.yml
│        │  │  │  │     ├─ full.yml
│        │  │  │  │     ├─ html_sanitizer.yml
│        │  │  │  │     ├─ html_sanitizer_default_allowed_link_and_media_hosts.yml
│        │  │  │  │     ├─ html_sanitizer_default_config.yml
│        │  │  │  │     ├─ http_client_default_options.yml
│        │  │  │  │     ├─ http_client_full_default_options.yml
│        │  │  │  │     ├─ http_client_mock_response_factory.yml
│        │  │  │  │     ├─ http_client_override_default_options.yml
│        │  │  │  │     ├─ http_client_rate_limiter.yml
│        │  │  │  │     ├─ http_client_retry.yml
│        │  │  │  │     ├─ http_client_scoped_without_query_option.yml
│        │  │  │  │     ├─ http_client_xml_key.yml
│        │  │  │  │     ├─ json_streamer.yml
│        │  │  │  │     ├─ lock.yml
│        │  │  │  │     ├─ lock_named.yml
│        │  │  │  │     ├─ lock_service.yml
│        │  │  │  │     ├─ mailer_with_disabled_message_bus.yml
│        │  │  │  │     ├─ mailer_with_dsn.yml
│        │  │  │  │     ├─ mailer_with_specific_message_bus.yml
│        │  │  │  │     ├─ mailer_with_transports.yml
│        │  │  │  │     ├─ messenger.yml
│        │  │  │  │     ├─ messenger_disabled.yml
│        │  │  │  │     ├─ messenger_middleware_factory_erroneous_format.yml
│        │  │  │  │     ├─ messenger_multiple_buses_without_deduplicate_middleware.yml
│        │  │  │  │     ├─ messenger_multiple_buses_with_deduplicate_middleware.yml
│        │  │  │  │     ├─ messenger_multiple_failure_transports.yml
│        │  │  │  │     ├─ messenger_multiple_failure_transports_global.yml
│        │  │  │  │     ├─ messenger_routing.yml
│        │  │  │  │     ├─ messenger_routing_invalid_transport.yml
│        │  │  │  │     ├─ messenger_routing_invalid_wildcard.yml
│        │  │  │  │     ├─ messenger_routing_single.yml
│        │  │  │  │     ├─ messenger_schedule.yml
│        │  │  │  │     ├─ messenger_transport.yml
│        │  │  │  │     ├─ messenger_transports.yml
│        │  │  │  │     ├─ messenger_with_disabled_reset_on_message.yml
│        │  │  │  │     ├─ messenger_with_explict_reset_on_message_legacy.yml
│        │  │  │  │     ├─ notifier.yml
│        │  │  │  │     ├─ notifier_without_mailer.yml
│        │  │  │  │     ├─ notifier_without_messenger.yml
│        │  │  │  │     ├─ notifier_without_transports.yml
│        │  │  │  │     ├─ notifier_with_disabled_message_bus.yml
│        │  │  │  │     ├─ notifier_with_specific_message_bus.yml
│        │  │  │  │     ├─ php_errors_disabled.yml
│        │  │  │  │     ├─ php_errors_enabled.yml
│        │  │  │  │     ├─ php_errors_log_level.yml
│        │  │  │  │     ├─ php_errors_log_levels.yml
│        │  │  │  │     ├─ profiler.yml
│        │  │  │  │     ├─ property_accessor.yml
│        │  │  │  │     ├─ property_info.yml
│        │  │  │  │     ├─ property_info_with_constructor_extractor.yml
│        │  │  │  │     ├─ request.yml
│        │  │  │  │     ├─ semaphore.yml
│        │  │  │  │     ├─ semaphore_named.yml
│        │  │  │  │     ├─ semaphore_service.yml
│        │  │  │  │     ├─ serializer_disabled.yml
│        │  │  │  │     ├─ serializer_enabled.yml
│        │  │  │  │     ├─ serializer_mapping.yml
│        │  │  │  │     ├─ serializer_mapping_without_annotations.yml
│        │  │  │  │     ├─ serializer_without_translator.yml
│        │  │  │  │     ├─ session.yml
│        │  │  │  │     ├─ session_cookie_secure_auto.yml
│        │  │  │  │     ├─ ssi_disabled.yml
│        │  │  │  │     ├─ translator_cache_dir_disabled.yml
│        │  │  │  │     ├─ translator_fallbacks.yml
│        │  │  │  │     ├─ translator_globals.yml
│        │  │  │  │     ├─ translator_without_globals.yml
│        │  │  │  │     ├─ trusted_proxies_private_ranges.yml
│        │  │  │  │     ├─ type_info.yml
│        │  │  │  │     ├─ validation_attributes.yml
│        │  │  │  │     ├─ validation_auto_mapping.yml
│        │  │  │  │     ├─ validation_email_validation_mode.yml
│        │  │  │  │     ├─ validation_mapping.yml
│        │  │  │  │     ├─ validation_multiple_static_methods.yml
│        │  │  │  │     ├─ validation_no_static_method.yml
│        │  │  │  │     ├─ validation_translation_domain.yml
│        │  │  │  │     ├─ webhook.yml
│        │  │  │  │     ├─ webhook_without_serializer.yml
│        │  │  │  │     ├─ web_link.yml
│        │  │  │  │     ├─ workflows.yml
│        │  │  │  │     ├─ workflows_enabled.yml
│        │  │  │  │     ├─ workflows_explicitly_enabled.yml
│        │  │  │  │     ├─ workflows_explicitly_enabled_named_workflows.yml
│        │  │  │  │     ├─ workflow_not_valid.yml
│        │  │  │  │     ├─ workflow_without_support_and_support_strategy.yml
│        │  │  │  │     ├─ workflow_with_guard_expression.yml
│        │  │  │  │     ├─ workflow_with_multiple_transitions_with_same_name.yml
│        │  │  │  │     ├─ workflow_with_no_events_to_dispatch.yml
│        │  │  │  │     ├─ workflow_with_specified_events_to_dispatch.yml
│        │  │  │  │     └─ workflow_with_support_and_support_strategy.yml
│        │  │  │  ├─ FrameworkExtensionTestCase.php
│        │  │  │  ├─ PhpFrameworkExtensionTest.php
│        │  │  │  ├─ translations
│        │  │  │  │  ├─ security.en.yaml
│        │  │  │  │  └─ test_default.en.xlf
│        │  │  │  ├─ XmlFrameworkExtensionTest.php
│        │  │  │  └─ YamlFrameworkExtensionTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ BackslashClass.php
│        │  │  │  ├─ ClassAliasExampleClass.php
│        │  │  │  ├─ ClassAliasTargetClass.php
│        │  │  │  ├─ ContainerExcluded.php
│        │  │  │  ├─ DeclaredClass.php
│        │  │  │  ├─ DeprecatedClass.php
│        │  │  │  ├─ Descriptor
│        │  │  │  │  ├─ alias_1.json
│        │  │  │  │  ├─ alias_1.md
│        │  │  │  │  ├─ alias_1.txt
│        │  │  │  │  ├─ alias_1.xml
│        │  │  │  │  ├─ alias_2.json
│        │  │  │  │  ├─ alias_2.md
│        │  │  │  │  ├─ alias_2.txt
│        │  │  │  │  ├─ alias_2.xml
│        │  │  │  │  ├─ alias_with_definition_1.json
│        │  │  │  │  ├─ alias_with_definition_1.md
│        │  │  │  │  ├─ alias_with_definition_1.txt
│        │  │  │  │  ├─ alias_with_definition_1.xml
│        │  │  │  │  ├─ alias_with_definition_2.json
│        │  │  │  │  ├─ alias_with_definition_2.md
│        │  │  │  │  ├─ alias_with_definition_2.txt
│        │  │  │  │  ├─ alias_with_definition_2.xml
│        │  │  │  │  ├─ array_parameter.json
│        │  │  │  │  ├─ array_parameter.md
│        │  │  │  │  ├─ array_parameter.txt
│        │  │  │  │  ├─ array_parameter.xml
│        │  │  │  │  ├─ builder_1_arguments.json
│        │  │  │  │  ├─ builder_1_arguments.md
│        │  │  │  │  ├─ builder_1_arguments.txt
│        │  │  │  │  ├─ builder_1_arguments.xml
│        │  │  │  │  ├─ builder_1_public.json
│        │  │  │  │  ├─ builder_1_public.md
│        │  │  │  │  ├─ builder_1_public.txt
│        │  │  │  │  ├─ builder_1_public.xml
│        │  │  │  │  ├─ builder_1_services.json
│        │  │  │  │  ├─ builder_1_services.md
│        │  │  │  │  ├─ builder_1_services.txt
│        │  │  │  │  ├─ builder_1_services.xml
│        │  │  │  │  ├─ builder_1_tag1.json
│        │  │  │  │  ├─ builder_1_tag1.md
│        │  │  │  │  ├─ builder_1_tag1.txt
│        │  │  │  │  ├─ builder_1_tag1.xml
│        │  │  │  │  ├─ builder_1_tags.json
│        │  │  │  │  ├─ builder_1_tags.md
│        │  │  │  │  ├─ builder_1_tags.txt
│        │  │  │  │  ├─ builder_1_tags.xml
│        │  │  │  │  ├─ builder_priority_tag.json
│        │  │  │  │  ├─ builder_priority_tag.md
│        │  │  │  │  ├─ builder_priority_tag.txt
│        │  │  │  │  ├─ builder_priority_tag.xml
│        │  │  │  │  ├─ cache
│        │  │  │  │  │  ├─ KernelContainerWithDeprecations.log
│        │  │  │  │  │  └─ KernelContainerWithoutDeprecations.log
│        │  │  │  │  ├─ callable_1.json
│        │  │  │  │  ├─ callable_1.md
│        │  │  │  │  ├─ callable_1.txt
│        │  │  │  │  ├─ callable_1.xml
│        │  │  │  │  ├─ callable_2.json
│        │  │  │  │  ├─ callable_2.md
│        │  │  │  │  ├─ callable_2.txt
│        │  │  │  │  ├─ callable_2.xml
│        │  │  │  │  ├─ callable_3.json
│        │  │  │  │  ├─ callable_3.md
│        │  │  │  │  ├─ callable_3.txt
│        │  │  │  │  ├─ callable_3.xml
│        │  │  │  │  ├─ callable_4.json
│        │  │  │  │  ├─ callable_4.md
│        │  │  │  │  ├─ callable_4.txt
│        │  │  │  │  ├─ callable_4.xml
│        │  │  │  │  ├─ callable_5.json
│        │  │  │  │  ├─ callable_5.md
│        │  │  │  │  ├─ callable_5.txt
│        │  │  │  │  ├─ callable_5.xml
│        │  │  │  │  ├─ callable_6.json
│        │  │  │  │  ├─ callable_6.md
│        │  │  │  │  ├─ callable_6.txt
│        │  │  │  │  ├─ callable_6.xml
│        │  │  │  │  ├─ callable_7.json
│        │  │  │  │  ├─ callable_7.md
│        │  │  │  │  ├─ callable_7.txt
│        │  │  │  │  ├─ callable_7.xml
│        │  │  │  │  ├─ callable_from_callable.json
│        │  │  │  │  ├─ callable_from_callable.md
│        │  │  │  │  ├─ callable_from_callable.txt
│        │  │  │  │  ├─ callable_from_callable.xml
│        │  │  │  │  ├─ definition_1.json
│        │  │  │  │  ├─ definition_1.md
│        │  │  │  │  ├─ definition_1.txt
│        │  │  │  │  ├─ definition_1.xml
│        │  │  │  │  ├─ definition_2.json
│        │  │  │  │  ├─ definition_2.md
│        │  │  │  │  ├─ definition_2.txt
│        │  │  │  │  ├─ definition_2.xml
│        │  │  │  │  ├─ definition_3.json
│        │  │  │  │  ├─ definition_3.md
│        │  │  │  │  ├─ definition_3.txt
│        │  │  │  │  ├─ definition_3.xml
│        │  │  │  │  ├─ definition_arguments_1.json
│        │  │  │  │  ├─ definition_arguments_1.md
│        │  │  │  │  ├─ definition_arguments_1.txt
│        │  │  │  │  ├─ definition_arguments_1.xml
│        │  │  │  │  ├─ definition_arguments_2.json
│        │  │  │  │  ├─ definition_arguments_2.md
│        │  │  │  │  ├─ definition_arguments_2.txt
│        │  │  │  │  ├─ definition_arguments_2.xml
│        │  │  │  │  ├─ definition_arguments_3.json
│        │  │  │  │  ├─ definition_arguments_3.md
│        │  │  │  │  ├─ definition_arguments_3.txt
│        │  │  │  │  ├─ definition_arguments_3.xml
│        │  │  │  │  ├─ definition_arguments_without_class.json
│        │  │  │  │  ├─ definition_arguments_without_class.md
│        │  │  │  │  ├─ definition_arguments_without_class.txt
│        │  │  │  │  ├─ definition_arguments_without_class.xml
│        │  │  │  │  ├─ definition_arguments_with_enum.json
│        │  │  │  │  ├─ definition_arguments_with_enum.md
│        │  │  │  │  ├─ definition_arguments_with_enum.txt
│        │  │  │  │  ├─ definition_arguments_with_enum.xml
│        │  │  │  │  ├─ definition_without_class.json
│        │  │  │  │  ├─ definition_without_class.md
│        │  │  │  │  ├─ definition_without_class.txt
│        │  │  │  │  ├─ definition_without_class.xml
│        │  │  │  │  ├─ deprecated_parameter.json
│        │  │  │  │  ├─ deprecated_parameter.md
│        │  │  │  │  ├─ deprecated_parameter.txt
│        │  │  │  │  ├─ deprecated_parameter.xml
│        │  │  │  │  ├─ deprecated_parameters.json
│        │  │  │  │  ├─ deprecated_parameters.md
│        │  │  │  │  ├─ deprecated_parameters.txt
│        │  │  │  │  ├─ deprecated_parameters.xml
│        │  │  │  │  ├─ deprecations.json
│        │  │  │  │  ├─ deprecations.md
│        │  │  │  │  ├─ deprecations.txt
│        │  │  │  │  ├─ deprecations.xml
│        │  │  │  │  ├─ deprecations_empty.json
│        │  │  │  │  ├─ deprecations_empty.md
│        │  │  │  │  ├─ deprecations_empty.txt
│        │  │  │  │  ├─ deprecations_empty.xml
│        │  │  │  │  ├─ event_dispatcher_1_event1.json
│        │  │  │  │  ├─ event_dispatcher_1_event1.md
│        │  │  │  │  ├─ event_dispatcher_1_event1.txt
│        │  │  │  │  ├─ event_dispatcher_1_event1.xml
│        │  │  │  │  ├─ event_dispatcher_1_events.json
│        │  │  │  │  ├─ event_dispatcher_1_events.md
│        │  │  │  │  ├─ event_dispatcher_1_events.txt
│        │  │  │  │  ├─ event_dispatcher_1_events.xml
│        │  │  │  │  ├─ existing_class_def_1.json
│        │  │  │  │  ├─ existing_class_def_1.md
│        │  │  │  │  ├─ existing_class_def_1.txt
│        │  │  │  │  ├─ existing_class_def_1.xml
│        │  │  │  │  ├─ existing_class_def_2.json
│        │  │  │  │  ├─ existing_class_def_2.md
│        │  │  │  │  ├─ existing_class_def_2.txt
│        │  │  │  │  ├─ existing_class_def_2.xml
│        │  │  │  │  ├─ parameter.json
│        │  │  │  │  ├─ parameter.md
│        │  │  │  │  ├─ parameter.txt
│        │  │  │  │  ├─ parameter.xml
│        │  │  │  │  ├─ parameters_1.json
│        │  │  │  │  ├─ parameters_1.md
│        │  │  │  │  ├─ parameters_1.txt
│        │  │  │  │  ├─ parameters_1.xml
│        │  │  │  │  ├─ parameters_enums.json
│        │  │  │  │  ├─ parameters_enums.md
│        │  │  │  │  ├─ parameters_enums.txt
│        │  │  │  │  ├─ parameters_enums.xml
│        │  │  │  │  ├─ route_1.json
│        │  │  │  │  ├─ route_1.md
│        │  │  │  │  ├─ route_1.txt
│        │  │  │  │  ├─ route_1.xml
│        │  │  │  │  ├─ route_1_link.txt
│        │  │  │  │  ├─ route_2.json
│        │  │  │  │  ├─ route_2.md
│        │  │  │  │  ├─ route_2.txt
│        │  │  │  │  ├─ route_2.xml
│        │  │  │  │  ├─ route_2_link.txt
│        │  │  │  │  ├─ route_collection_1.json
│        │  │  │  │  ├─ route_collection_1.md
│        │  │  │  │  ├─ route_collection_1.txt
│        │  │  │  │  ├─ route_collection_1.xml
│        │  │  │  │  ├─ route_collection_2.json
│        │  │  │  │  ├─ route_collection_2.md
│        │  │  │  │  ├─ route_collection_2.txt
│        │  │  │  │  ├─ route_collection_2.xml
│        │  │  │  │  ├─ route_collection_3.json
│        │  │  │  │  ├─ route_collection_3.md
│        │  │  │  │  ├─ route_collection_3.txt
│        │  │  │  │  └─ route_collection_3.xml
│        │  │  │  ├─ FooUnitEnum.php
│        │  │  │  ├─ Messenger
│        │  │  │  │  ├─ BarMessage.php
│        │  │  │  │  ├─ DummyMessage.php
│        │  │  │  │  ├─ DummyMessageInterface.php
│        │  │  │  │  ├─ DummySchedule.php
│        │  │  │  │  ├─ DummyTask.php
│        │  │  │  │  ├─ DummyTaskWithCustomReceiver.php
│        │  │  │  │  ├─ FooMessage.php
│        │  │  │  │  └─ SecondMessage.php
│        │  │  │  ├─ ObjectMapper
│        │  │  │  │  ├─ ObjectMapped.php
│        │  │  │  │  ├─ ObjectToBeMapped.php
│        │  │  │  │  └─ TransformCallable.php
│        │  │  │  ├─ Resources
│        │  │  │  │  ├─ BaseBundle
│        │  │  │  │  │  └─ views
│        │  │  │  │  │     ├─ base.format.engine
│        │  │  │  │  │     └─ controller
│        │  │  │  │  │        └─ custom.format.engine
│        │  │  │  │  ├─ translations
│        │  │  │  │  │  ├─ domain.with.dots.en.yml
│        │  │  │  │  │  └─ messages.fr.yml
│        │  │  │  │  ├─ translations2
│        │  │  │  │  │  └─ ccc.fr.yml
│        │  │  │  │  └─ views
│        │  │  │  │     ├─ resource.format.engine
│        │  │  │  │     ├─ this.is.a.template.format.engine
│        │  │  │  │     └─ translation.html.php
│        │  │  │  ├─ Serialization
│        │  │  │  │  ├─ Author.php
│        │  │  │  │  ├─ Person.php
│        │  │  │  │  └─ Resources
│        │  │  │  │     ├─ author.yml
│        │  │  │  │     ├─ does_not_exist.yaml
│        │  │  │  │     └─ person.xml
│        │  │  │  ├─ Serializer
│        │  │  │  │  ├─ CircularReferenceHandler.php
│        │  │  │  │  └─ MaxDepthHandler.php
│        │  │  │  ├─ Suit.php
│        │  │  │  ├─ TemplatePathsCache
│        │  │  │  │  ├─ templates-empty.php
│        │  │  │  │  └─ templates.php
│        │  │  │  ├─ templates.php
│        │  │  │  ├─ TranslatableBackedEnum.php
│        │  │  │  ├─ Validation
│        │  │  │  │  ├─ Article.php
│        │  │  │  │  ├─ Author.php
│        │  │  │  │  ├─ Category.php
│        │  │  │  │  ├─ Person.php
│        │  │  │  │  ├─ Resources
│        │  │  │  │  │  ├─ author.yml
│        │  │  │  │  │  ├─ categories.yml
│        │  │  │  │  │  ├─ does_not_exist.yaml
│        │  │  │  │  │  └─ person.xml
│        │  │  │  │  └─ SubCategory.php
│        │  │  │  └─ WarmedClass.php
│        │  │  ├─ Functional
│        │  │  │  ├─ AbstractAttributeRoutingTestCase.php
│        │  │  │  ├─ AbstractWebTestCase.php
│        │  │  │  ├─ AnnotatedControllerTest.php
│        │  │  │  ├─ ApiAttributesTest.php
│        │  │  │  ├─ app
│        │  │  │  │  ├─ AnnotatedController
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ ApiAttributesTest
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ AppKernel.php
│        │  │  │  │  ├─ AutowiringTypes
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ BundlePaths
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ CacheAttributeListener
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ CachePoolClear
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ CachePools
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ default.yml
│        │  │  │  │  │  ├─ redis_config.yml
│        │  │  │  │  │  └─ redis_custom_config.yml
│        │  │  │  │  ├─ config
│        │  │  │  │  │  ├─ default.yml
│        │  │  │  │  │  └─ framework.yml
│        │  │  │  │  ├─ ConfigDump
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ ContainerDebug
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ ContainerDump
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ ControllerServiceResolution
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ Fragment
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ routing.yml
│        │  │  │  │  │  └─ services.yml
│        │  │  │  │  ├─ HttpClient
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ routing.yml
│        │  │  │  │  │  └─ services.yml
│        │  │  │  │  ├─ JsonStreamer
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ Dto
│        │  │  │  │  │  │  └─ Dummy.php
│        │  │  │  │  │  ├─ RangeToStringValueTransformer.php
│        │  │  │  │  │  └─ StringToRangeValueTransformer.php
│        │  │  │  │  ├─ Mailer
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ routing.yml
│        │  │  │  │  │  └─ services.yml
│        │  │  │  │  ├─ Notifier
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ routing.yml
│        │  │  │  │  │  └─ services.yml
│        │  │  │  │  ├─ ObjectMapper
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ Profiler
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ ProfilerCollectParameter
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ Psr4Routing
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ RouterDebug
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ RoutingConditionService
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ routing.yml
│        │  │  │  │  │  ├─ services_auto_configured.yml
│        │  │  │  │  │  └─ services_manually_configured.yml
│        │  │  │  │  ├─ Scheduler
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ Security
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ Serializer
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ default_context.yaml
│        │  │  │  │  ├─ Session
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ Slugger
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ services.yml
│        │  │  │  │  ├─ templates
│        │  │  │  │  │  └─ fragment.html.twig
│        │  │  │  │  ├─ TestServiceContainer
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ services.yml
│        │  │  │  │  │  └─ test_disabled.yml
│        │  │  │  │  ├─ TransDebug
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ services.yml
│        │  │  │  │  ├─ TypeInfo
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ Dummy.php
│        │  │  │  │  └─ Uid
│        │  │  │  │     ├─ bundles.php
│        │  │  │  │     ├─ config_disabled.yml
│        │  │  │  │     ├─ config_enabled.yml
│        │  │  │  │     └─ routing.yml
│        │  │  │  ├─ AutowiringTypesTest.php
│        │  │  │  ├─ Bundle
│        │  │  │  │  ├─ DefaultConfigTestBundle
│        │  │  │  │  │  ├─ DefaultConfigTestBundle.php
│        │  │  │  │  │  └─ DependencyInjection
│        │  │  │  │  │     ├─ Configuration.php
│        │  │  │  │  │     └─ DefaultConfigTestExtension.php
│        │  │  │  │  ├─ ExtensionWithoutConfigTestBundle
│        │  │  │  │  │  ├─ DependencyInjection
│        │  │  │  │  │  │  └─ ExtensionWithoutConfigTestExtension.php
│        │  │  │  │  │  └─ ExtensionWithoutConfigTestBundle.php
│        │  │  │  │  ├─ LegacyBundle
│        │  │  │  │  │  ├─ Entity
│        │  │  │  │  │  │  └─ LegacyPerson.php
│        │  │  │  │  │  ├─ LegacyBundle.php
│        │  │  │  │  │  └─ Resources
│        │  │  │  │  │     ├─ config
│        │  │  │  │  │     │  ├─ serialization.yaml
│        │  │  │  │  │     │  └─ validation.yaml
│        │  │  │  │  │     ├─ public
│        │  │  │  │  │     │  └─ legacy.css
│        │  │  │  │  │     ├─ translations
│        │  │  │  │  │     │  └─ legacy.en.yaml
│        │  │  │  │  │     └─ views
│        │  │  │  │  │        └─ index.html.twig
│        │  │  │  │  ├─ ModernBundle
│        │  │  │  │  │  ├─ config
│        │  │  │  │  │  │  ├─ serialization.yaml
│        │  │  │  │  │  │  └─ validation.yaml
│        │  │  │  │  │  ├─ public
│        │  │  │  │  │  │  └─ modern.css
│        │  │  │  │  │  ├─ src
│        │  │  │  │  │  │  ├─ Entity
│        │  │  │  │  │  │  │  └─ ModernPerson.php
│        │  │  │  │  │  │  └─ ModernBundle.php
│        │  │  │  │  │  ├─ templates
│        │  │  │  │  │  │  └─ index.html.twig
│        │  │  │  │  │  └─ translations
│        │  │  │  │  │     └─ modern.en.yaml
│        │  │  │  │  ├─ RoutingConditionServiceBundle
│        │  │  │  │  │  ├─ Controller
│        │  │  │  │  │  │  └─ DefaultController.php
│        │  │  │  │  │  ├─ RoutingConditionServiceBundle.php
│        │  │  │  │  │  └─ Service
│        │  │  │  │  │     ├─ AutoConfiguredNonAliasedService.php
│        │  │  │  │  │     ├─ AutoConfiguredService.php
│        │  │  │  │  │     ├─ FooOriginalService.php
│        │  │  │  │  │     ├─ FooReplacementService.php
│        │  │  │  │  │     └─ ManuallyTaggedService.php
│        │  │  │  │  └─ TestBundle
│        │  │  │  │     ├─ AutowiringTypes
│        │  │  │  │     │  └─ AutowiredServices.php
│        │  │  │  │     ├─ Controller
│        │  │  │  │     │  ├─ AnnotatedController.php
│        │  │  │  │     │  ├─ EmailController.php
│        │  │  │  │     │  ├─ FragmentController.php
│        │  │  │  │     │  ├─ HttpClientController.php
│        │  │  │  │     │  ├─ NotificationController.php
│        │  │  │  │     │  ├─ ProfilerController.php
│        │  │  │  │     │  ├─ SecurityController.php
│        │  │  │  │     │  ├─ SessionController.php
│        │  │  │  │     │  ├─ SubRequestController.php
│        │  │  │  │     │  ├─ SubRequestServiceResolutionController.php
│        │  │  │  │     │  ├─ TransController.php
│        │  │  │  │     │  └─ UidController.php
│        │  │  │  │     ├─ DependencyInjection
│        │  │  │  │     │  ├─ Config
│        │  │  │  │     │  │  └─ CustomConfig.php
│        │  │  │  │     │  ├─ Configuration.php
│        │  │  │  │     │  └─ TestExtension.php
│        │  │  │  │     ├─ Resources
│        │  │  │  │     │  └─ config
│        │  │  │  │     │     └─ routing.yml
│        │  │  │  │     ├─ Slugger
│        │  │  │  │     │  └─ SlugConstructArgService.php
│        │  │  │  │     ├─ TestBundle.php
│        │  │  │  │     ├─ Tests
│        │  │  │  │     │  └─ MockClientCallback.php
│        │  │  │  │     ├─ TestServiceContainer
│        │  │  │  │     │  ├─ NonPublicService.php
│        │  │  │  │     │  ├─ PrivateService.php
│        │  │  │  │     │  ├─ PublicService.php
│        │  │  │  │     │  ├─ ResettableService.php
│        │  │  │  │     │  └─ UnusedPrivateService.php
│        │  │  │  │     └─ TransDebug
│        │  │  │  │        ├─ TransConstructArgService.php
│        │  │  │  │        ├─ TransMethodCallsService.php
│        │  │  │  │        ├─ TransPropertyService.php
│        │  │  │  │        └─ TransSubscriberService.php
│        │  │  │  ├─ BundlePathsTest.php
│        │  │  │  ├─ CacheAttributeListenerTest.php
│        │  │  │  ├─ CachePoolClearCommandTest.php
│        │  │  │  ├─ CachePoolListCommandTest.php
│        │  │  │  ├─ CachePoolsTest.php
│        │  │  │  ├─ ConfigDebugCommandTest.php
│        │  │  │  ├─ ConfigDumpReferenceCommandTest.php
│        │  │  │  ├─ ContainerDebugCommandTest.php
│        │  │  │  ├─ ContainerDumpTest.php
│        │  │  │  ├─ DebugAutowiringCommandTest.php
│        │  │  │  ├─ Extension
│        │  │  │  │  └─ TestDumpExtension.php
│        │  │  │  ├─ Fixtures
│        │  │  │  │  └─ describe_env_vars.txt
│        │  │  │  ├─ FragmentTest.php
│        │  │  │  ├─ HttpClientTest.php
│        │  │  │  ├─ JsonStreamerTest.php
│        │  │  │  ├─ MailerTest.php
│        │  │  │  ├─ NotificationTest.php
│        │  │  │  ├─ ObjectMapperTest.php
│        │  │  │  ├─ ProfilerTest.php
│        │  │  │  ├─ PropertyInfoTest.php
│        │  │  │  ├─ Psr4RoutingTest.php
│        │  │  │  ├─ RouterDebugCommandTest.php
│        │  │  │  ├─ RoutingConditionServiceTest.php
│        │  │  │  ├─ SchedulerTest.php
│        │  │  │  ├─ SecurityTest.php
│        │  │  │  ├─ SerializerTest.php
│        │  │  │  ├─ SessionTest.php
│        │  │  │  ├─ SluggerLocaleAwareTest.php
│        │  │  │  ├─ SubRequestsTest.php
│        │  │  │  ├─ TestServiceContainerTest.php
│        │  │  │  ├─ TranslationDebugCommandTest.php
│        │  │  │  ├─ TypeInfoTest.php
│        │  │  │  └─ UidTest.php
│        │  │  ├─ Kernel
│        │  │  │  ├─ ConcreteMicroKernel.php
│        │  │  │  ├─ default
│        │  │  │  │  ├─ config
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ routes.yaml
│        │  │  │  │  │  └─ services.yaml
│        │  │  │  │  └─ src
│        │  │  │  │     └─ DefaultKernel.php
│        │  │  │  ├─ flex-style
│        │  │  │  │  ├─ config
│        │  │  │  │  │  └─ bundles.php
│        │  │  │  │  └─ src
│        │  │  │  │     └─ FlexStyleMicroKernel.php
│        │  │  │  ├─ KernelCommand.php
│        │  │  │  ├─ MicroKernelTraitTest.php
│        │  │  │  └─ SimpleKernel.php
│        │  │  ├─ KernelBrowserTest.php
│        │  │  ├─ Routing
│        │  │  │  ├─ DelegatingLoaderTest.php
│        │  │  │  ├─ Fixtures
│        │  │  │  │  └─ with_condition.yaml
│        │  │  │  ├─ RedirectableCompiledUrlMatcherTest.php
│        │  │  │  └─ RouterTest.php
│        │  │  ├─ Secrets
│        │  │  │  ├─ DotenvVaultTest.php
│        │  │  │  └─ SodiumVaultTest.php
│        │  │  ├─ Test
│        │  │  │  ├─ TestBrowserTokenTest.php
│        │  │  │  └─ WebTestCaseTest.php
│        │  │  ├─ TestCase.php
│        │  │  └─ Translation
│        │  │     └─ TranslatorTest.php
│        │  └─ Translation
│        │     └─ Translator.php
│        ├─ http-foundation
│        │  ├─ AcceptHeader.php
│        │  ├─ AcceptHeaderItem.php
│        │  ├─ BinaryFileResponse.php
│        │  ├─ ChainRequestMatcher.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ Cookie.php
│        │  ├─ EventStreamResponse.php
│        │  ├─ Exception
│        │  │  ├─ BadRequestException.php
│        │  │  ├─ ConflictingHeadersException.php
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ ExpiredSignedUriException.php
│        │  │  ├─ JsonException.php
│        │  │  ├─ LogicException.php
│        │  │  ├─ RequestExceptionInterface.php
│        │  │  ├─ SessionNotFoundException.php
│        │  │  ├─ SignedUriException.php
│        │  │  ├─ SuspiciousOperationException.php
│        │  │  ├─ UnexpectedValueException.php
│        │  │  ├─ UnsignedUriException.php
│        │  │  └─ UnverifiedSignedUriException.php
│        │  ├─ File
│        │  │  ├─ Exception
│        │  │  │  ├─ AccessDeniedException.php
│        │  │  │  ├─ CannotWriteFileException.php
│        │  │  │  ├─ ExtensionFileException.php
│        │  │  │  ├─ FileException.php
│        │  │  │  ├─ FileNotFoundException.php
│        │  │  │  ├─ FormSizeFileException.php
│        │  │  │  ├─ IniSizeFileException.php
│        │  │  │  ├─ NoFileException.php
│        │  │  │  ├─ NoTmpDirFileException.php
│        │  │  │  ├─ PartialFileException.php
│        │  │  │  ├─ UnexpectedTypeException.php
│        │  │  │  └─ UploadException.php
│        │  │  ├─ File.php
│        │  │  ├─ Stream.php
│        │  │  └─ UploadedFile.php
│        │  ├─ FileBag.php
│        │  ├─ HeaderBag.php
│        │  ├─ HeaderUtils.php
│        │  ├─ InputBag.php
│        │  ├─ IpUtils.php
│        │  ├─ JsonResponse.php
│        │  ├─ LICENSE
│        │  ├─ ParameterBag.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ RateLimiter
│        │  │  ├─ AbstractRequestRateLimiter.php
│        │  │  ├─ PeekableRequestRateLimiterInterface.php
│        │  │  └─ RequestRateLimiterInterface.php
│        │  ├─ README.md
│        │  ├─ RedirectResponse.php
│        │  ├─ Request.php
│        │  ├─ RequestMatcher
│        │  │  ├─ AttributesRequestMatcher.php
│        │  │  ├─ ExpressionRequestMatcher.php
│        │  │  ├─ HeaderRequestMatcher.php
│        │  │  ├─ HostRequestMatcher.php
│        │  │  ├─ IpsRequestMatcher.php
│        │  │  ├─ IsJsonRequestMatcher.php
│        │  │  ├─ MethodRequestMatcher.php
│        │  │  ├─ PathRequestMatcher.php
│        │  │  ├─ PortRequestMatcher.php
│        │  │  ├─ QueryParameterRequestMatcher.php
│        │  │  └─ SchemeRequestMatcher.php
│        │  ├─ RequestMatcherInterface.php
│        │  ├─ RequestStack.php
│        │  ├─ Response.php
│        │  ├─ ResponseHeaderBag.php
│        │  ├─ ServerBag.php
│        │  ├─ ServerEvent.php
│        │  ├─ Session
│        │  │  ├─ Attribute
│        │  │  │  ├─ AttributeBag.php
│        │  │  │  └─ AttributeBagInterface.php
│        │  │  ├─ Flash
│        │  │  │  ├─ AutoExpireFlashBag.php
│        │  │  │  ├─ FlashBag.php
│        │  │  │  └─ FlashBagInterface.php
│        │  │  ├─ FlashBagAwareSessionInterface.php
│        │  │  ├─ Session.php
│        │  │  ├─ SessionBagInterface.php
│        │  │  ├─ SessionBagProxy.php
│        │  │  ├─ SessionFactory.php
│        │  │  ├─ SessionFactoryInterface.php
│        │  │  ├─ SessionInterface.php
│        │  │  ├─ SessionUtils.php
│        │  │  └─ Storage
│        │  │     ├─ Handler
│        │  │     │  ├─ AbstractSessionHandler.php
│        │  │     │  ├─ IdentityMarshaller.php
│        │  │     │  ├─ MarshallingSessionHandler.php
│        │  │     │  ├─ MemcachedSessionHandler.php
│        │  │     │  ├─ MigratingSessionHandler.php
│        │  │     │  ├─ MongoDbSessionHandler.php
│        │  │     │  ├─ NativeFileSessionHandler.php
│        │  │     │  ├─ NullSessionHandler.php
│        │  │     │  ├─ PdoSessionHandler.php
│        │  │     │  ├─ RedisSessionHandler.php
│        │  │     │  ├─ SessionHandlerFactory.php
│        │  │     │  └─ StrictSessionHandler.php
│        │  │     ├─ MetadataBag.php
│        │  │     ├─ MockArraySessionStorage.php
│        │  │     ├─ MockFileSessionStorage.php
│        │  │     ├─ MockFileSessionStorageFactory.php
│        │  │     ├─ NativeSessionStorage.php
│        │  │     ├─ NativeSessionStorageFactory.php
│        │  │     ├─ PhpBridgeSessionStorage.php
│        │  │     ├─ PhpBridgeSessionStorageFactory.php
│        │  │     ├─ Proxy
│        │  │     │  ├─ AbstractProxy.php
│        │  │     │  └─ SessionHandlerProxy.php
│        │  │     ├─ SessionStorageFactoryInterface.php
│        │  │     └─ SessionStorageInterface.php
│        │  ├─ StreamedJsonResponse.php
│        │  ├─ StreamedResponse.php
│        │  ├─ Test
│        │  │  └─ Constraint
│        │  │     ├─ RequestAttributeValueSame.php
│        │  │     ├─ ResponseCookieValueSame.php
│        │  │     ├─ ResponseFormatSame.php
│        │  │     ├─ ResponseHasCookie.php
│        │  │     ├─ ResponseHasHeader.php
│        │  │     ├─ ResponseHeaderLocationSame.php
│        │  │     ├─ ResponseHeaderSame.php
│        │  │     ├─ ResponseIsRedirected.php
│        │  │     ├─ ResponseIsSuccessful.php
│        │  │     ├─ ResponseIsUnprocessable.php
│        │  │     └─ ResponseStatusCodeSame.php
│        │  ├─ Tests
│        │  │  ├─ AcceptHeaderItemTest.php
│        │  │  ├─ AcceptHeaderTest.php
│        │  │  ├─ BinaryFileResponseTest.php
│        │  │  ├─ CookieTest.php
│        │  │  ├─ EventStreamResponseTest.php
│        │  │  ├─ File
│        │  │  │  ├─ FakeFile.php
│        │  │  │  ├─ FileTest.php
│        │  │  │  ├─ Fixtures
│        │  │  │  │  ├─ -test
│        │  │  │  │  ├─ .unknownextension
│        │  │  │  │  ├─ case-sensitive-mime-type.xlsm
│        │  │  │  │  ├─ directory
│        │  │  │  │  │  └─ .empty
│        │  │  │  │  ├─ other-file.example
│        │  │  │  │  ├─ test
│        │  │  │  │  ├─ test.gif
│        │  │  │  │  └─ webkitdirectory
│        │  │  │  │     ├─ nested
│        │  │  │  │     │  └─ test.txt
│        │  │  │  │     └─ test.txt
│        │  │  │  └─ UploadedFileTest.php
│        │  │  ├─ FileBagTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ FooEnum.php
│        │  │  │  ├─ response-functional
│        │  │  │  │  ├─ common.inc
│        │  │  │  │  ├─ cookie_raw_urlencode.expected
│        │  │  │  │  ├─ cookie_raw_urlencode.php
│        │  │  │  │  ├─ cookie_samesite_lax.expected
│        │  │  │  │  ├─ cookie_samesite_lax.php
│        │  │  │  │  ├─ cookie_samesite_strict.expected
│        │  │  │  │  ├─ cookie_samesite_strict.php
│        │  │  │  │  ├─ cookie_urlencode.expected
│        │  │  │  │  ├─ cookie_urlencode.php
│        │  │  │  │  ├─ deleted_cookie.expected
│        │  │  │  │  ├─ deleted_cookie.php
│        │  │  │  │  ├─ early_hints.php
│        │  │  │  │  ├─ invalid_cookie_name.expected
│        │  │  │  │  └─ invalid_cookie_name.php
│        │  │  │  └─ xml
│        │  │  │     └─ http-status-codes.xml
│        │  │  ├─ HeaderBagTest.php
│        │  │  ├─ HeaderUtilsTest.php
│        │  │  ├─ InputBagTest.php
│        │  │  ├─ IpUtilsTest.php
│        │  │  ├─ JsonResponseTest.php
│        │  │  ├─ ParameterBagTest.php
│        │  │  ├─ RateLimiter
│        │  │  │  ├─ AbstractRequestRateLimiterTest.php
│        │  │  │  └─ MockAbstractRequestRateLimiter.php
│        │  │  ├─ RedirectResponseTest.php
│        │  │  ├─ RequestMatcher
│        │  │  │  ├─ AttributesRequestMatcherTest.php
│        │  │  │  ├─ ExpressionRequestMatcherTest.php
│        │  │  │  ├─ HeaderRequestMatcherTest.php
│        │  │  │  ├─ HostRequestMatcherTest.php
│        │  │  │  ├─ IpsRequestMatcherTest.php
│        │  │  │  ├─ IsJsonRequestMatcherTest.php
│        │  │  │  ├─ MethodRequestMatcherTest.php
│        │  │  │  ├─ PathRequestMatcherTest.php
│        │  │  │  ├─ PortRequestMatcherTest.php
│        │  │  │  ├─ QueryParameterRequestMatcherTest.php
│        │  │  │  └─ SchemeRequestMatcherTest.php
│        │  │  ├─ RequestStackTest.php
│        │  │  ├─ RequestTest.php
│        │  │  ├─ ResponseFunctionalTest.php
│        │  │  ├─ ResponseHeaderBagTest.php
│        │  │  ├─ ResponseTest.php
│        │  │  ├─ ResponseTestCase.php
│        │  │  ├─ schema
│        │  │  │  ├─ http-status-codes.rng
│        │  │  │  └─ iana-registry.rng
│        │  │  ├─ ServerBagTest.php
│        │  │  ├─ Session
│        │  │  │  ├─ Attribute
│        │  │  │  │  └─ AttributeBagTest.php
│        │  │  │  ├─ Flash
│        │  │  │  │  ├─ AutoExpireFlashBagTest.php
│        │  │  │  │  └─ FlashBagTest.php
│        │  │  │  ├─ SessionTest.php
│        │  │  │  └─ Storage
│        │  │  │     ├─ Handler
│        │  │  │     │  ├─ AbstractRedisSessionHandlerTestCase.php
│        │  │  │     │  ├─ AbstractSessionHandlerTest.php
│        │  │  │     │  ├─ Fixtures
│        │  │  │     │  │  ├─ common.inc
│        │  │  │     │  │  ├─ empty_destroys.expected
│        │  │  │     │  │  ├─ empty_destroys.php
│        │  │  │     │  │  ├─ invalid_regenerate.expected
│        │  │  │     │  │  ├─ invalid_regenerate.php
│        │  │  │     │  │  ├─ read_only.expected
│        │  │  │     │  │  ├─ read_only.php
│        │  │  │     │  │  ├─ regenerate.expected
│        │  │  │     │  │  ├─ regenerate.php
│        │  │  │     │  │  ├─ storage.expected
│        │  │  │     │  │  ├─ storage.php
│        │  │  │     │  │  ├─ with_cookie.expected
│        │  │  │     │  │  ├─ with_cookie.php
│        │  │  │     │  │  ├─ with_cookie_and_session.expected
│        │  │  │     │  │  ├─ with_cookie_and_session.php
│        │  │  │     │  │  ├─ with_samesite.expected
│        │  │  │     │  │  ├─ with_samesite.php
│        │  │  │     │  │  ├─ with_samesite_and_migration.expected
│        │  │  │     │  │  └─ with_samesite_and_migration.php
│        │  │  │     │  ├─ IdentityMarshallerTest.php
│        │  │  │     │  ├─ MarshallingSessionHandlerTest.php
│        │  │  │     │  ├─ MemcachedSessionHandlerTest.php
│        │  │  │     │  ├─ MigratingSessionHandlerTest.php
│        │  │  │     │  ├─ MongoDbSessionHandlerTest.php
│        │  │  │     │  ├─ NativeFileSessionHandlerTest.php
│        │  │  │     │  ├─ NullSessionHandlerTest.php
│        │  │  │     │  ├─ PdoSessionHandlerTest.php
│        │  │  │     │  ├─ PredisClusterSessionHandlerTest.php
│        │  │  │     │  ├─ PredisSessionHandlerTest.php
│        │  │  │     │  ├─ RedisArraySessionHandlerTest.php
│        │  │  │     │  ├─ RedisClusterSessionHandlerTest.php
│        │  │  │     │  ├─ RedisSessionHandlerTest.php
│        │  │  │     │  ├─ RelaySessionHandlerTest.php
│        │  │  │     │  ├─ SessionHandlerFactoryTest.php
│        │  │  │     │  ├─ StrictSessionHandlerTest.php
│        │  │  │     │  └─ stubs
│        │  │  │     │     └─ mongodb.php
│        │  │  │     ├─ MetadataBagTest.php
│        │  │  │     ├─ MockArraySessionStorageTest.php
│        │  │  │     ├─ MockFileSessionStorageTest.php
│        │  │  │     ├─ NativeSessionStorageTest.php
│        │  │  │     ├─ PhpBridgeSessionStorageTest.php
│        │  │  │     └─ Proxy
│        │  │  │        ├─ AbstractProxyTest.php
│        │  │  │        └─ SessionHandlerProxyTest.php
│        │  │  ├─ StreamedJsonResponseTest.php
│        │  │  ├─ StreamedResponseTest.php
│        │  │  ├─ Test
│        │  │  │  └─ Constraint
│        │  │  │     ├─ RequestAttributeValueSameTest.php
│        │  │  │     ├─ ResponseCookieValueSameTest.php
│        │  │  │     ├─ ResponseFormatSameTest.php
│        │  │  │     ├─ ResponseHasCookieTest.php
│        │  │  │     ├─ ResponseHasHeaderTest.php
│        │  │  │     ├─ ResponseHeaderLocationSameTest.php
│        │  │  │     ├─ ResponseHeaderSameTest.php
│        │  │  │     ├─ ResponseIsRedirectedTest.php
│        │  │  │     ├─ ResponseIsSuccessfulTest.php
│        │  │  │     ├─ ResponseIsUnprocessableTest.php
│        │  │  │     └─ ResponseStatusCodeSameTest.php
│        │  │  ├─ UriSignerTest.php
│        │  │  └─ UrlHelperTest.php
│        │  ├─ UriSigner.php
│        │  └─ UrlHelper.php
│        ├─ http-kernel
│        │  ├─ Attribute
│        │  │  ├─ AsController.php
│        │  │  ├─ AsTargetedValueResolver.php
│        │  │  ├─ Cache.php
│        │  │  ├─ MapDateTime.php
│        │  │  ├─ MapQueryParameter.php
│        │  │  ├─ MapQueryString.php
│        │  │  ├─ MapRequestPayload.php
│        │  │  ├─ MapUploadedFile.php
│        │  │  ├─ ValueResolver.php
│        │  │  ├─ WithHttpStatus.php
│        │  │  └─ WithLogLevel.php
│        │  ├─ Bundle
│        │  │  ├─ AbstractBundle.php
│        │  │  ├─ Bundle.php
│        │  │  ├─ BundleExtension.php
│        │  │  └─ BundleInterface.php
│        │  ├─ CacheClearer
│        │  │  ├─ CacheClearerInterface.php
│        │  │  ├─ ChainCacheClearer.php
│        │  │  └─ Psr6CacheClearer.php
│        │  ├─ CacheWarmer
│        │  │  ├─ CacheWarmer.php
│        │  │  ├─ CacheWarmerAggregate.php
│        │  │  ├─ CacheWarmerInterface.php
│        │  │  └─ WarmableInterface.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ Config
│        │  │  └─ FileLocator.php
│        │  ├─ Controller
│        │  │  ├─ ArgumentResolver
│        │  │  │  ├─ BackedEnumValueResolver.php
│        │  │  │  ├─ DateTimeValueResolver.php
│        │  │  │  ├─ DefaultValueResolver.php
│        │  │  │  ├─ NotTaggedControllerValueResolver.php
│        │  │  │  ├─ QueryParameterValueResolver.php
│        │  │  │  ├─ RequestAttributeValueResolver.php
│        │  │  │  ├─ RequestPayloadValueResolver.php
│        │  │  │  ├─ RequestValueResolver.php
│        │  │  │  ├─ ServiceValueResolver.php
│        │  │  │  ├─ SessionValueResolver.php
│        │  │  │  ├─ TraceableValueResolver.php
│        │  │  │  ├─ UidValueResolver.php
│        │  │  │  └─ VariadicValueResolver.php
│        │  │  ├─ ArgumentResolver.php
│        │  │  ├─ ArgumentResolverInterface.php
│        │  │  ├─ ContainerControllerResolver.php
│        │  │  ├─ ControllerReference.php
│        │  │  ├─ ControllerResolver.php
│        │  │  ├─ ControllerResolverInterface.php
│        │  │  ├─ ErrorController.php
│        │  │  ├─ TraceableArgumentResolver.php
│        │  │  ├─ TraceableControllerResolver.php
│        │  │  └─ ValueResolverInterface.php
│        │  ├─ ControllerMetadata
│        │  │  ├─ ArgumentMetadata.php
│        │  │  ├─ ArgumentMetadataFactory.php
│        │  │  └─ ArgumentMetadataFactoryInterface.php
│        │  ├─ DataCollector
│        │  │  ├─ AjaxDataCollector.php
│        │  │  ├─ ConfigDataCollector.php
│        │  │  ├─ DataCollector.php
│        │  │  ├─ DataCollectorInterface.php
│        │  │  ├─ DumpDataCollector.php
│        │  │  ├─ EventDataCollector.php
│        │  │  ├─ ExceptionDataCollector.php
│        │  │  ├─ LateDataCollectorInterface.php
│        │  │  ├─ LoggerDataCollector.php
│        │  │  ├─ MemoryDataCollector.php
│        │  │  ├─ RequestDataCollector.php
│        │  │  ├─ RouterDataCollector.php
│        │  │  └─ TimeDataCollector.php
│        │  ├─ Debug
│        │  │  ├─ ErrorHandlerConfigurator.php
│        │  │  ├─ TraceableEventDispatcher.php
│        │  │  └─ VirtualRequestStack.php
│        │  ├─ DependencyInjection
│        │  │  ├─ AddAnnotatedClassesToCachePass.php
│        │  │  ├─ ConfigurableExtension.php
│        │  │  ├─ ControllerArgumentValueResolverPass.php
│        │  │  ├─ Extension.php
│        │  │  ├─ FragmentRendererPass.php
│        │  │  ├─ LazyLoadingFragmentHandler.php
│        │  │  ├─ LoggerPass.php
│        │  │  ├─ MergeExtensionConfigurationPass.php
│        │  │  ├─ RegisterControllerArgumentLocatorsPass.php
│        │  │  ├─ RegisterLocaleAwareServicesPass.php
│        │  │  ├─ RemoveEmptyControllerArgumentLocatorsPass.php
│        │  │  ├─ ResettableServicePass.php
│        │  │  ├─ ServicesResetter.php
│        │  │  └─ ServicesResetterInterface.php
│        │  ├─ Event
│        │  │  ├─ ControllerArgumentsEvent.php
│        │  │  ├─ ControllerEvent.php
│        │  │  ├─ ExceptionEvent.php
│        │  │  ├─ FinishRequestEvent.php
│        │  │  ├─ KernelEvent.php
│        │  │  ├─ RequestEvent.php
│        │  │  ├─ ResponseEvent.php
│        │  │  ├─ TerminateEvent.php
│        │  │  └─ ViewEvent.php
│        │  ├─ EventListener
│        │  │  ├─ AbstractSessionListener.php
│        │  │  ├─ AddRequestFormatsListener.php
│        │  │  ├─ CacheAttributeListener.php
│        │  │  ├─ DebugHandlersListener.php
│        │  │  ├─ DisallowRobotsIndexingListener.php
│        │  │  ├─ DumpListener.php
│        │  │  ├─ ErrorListener.php
│        │  │  ├─ FragmentListener.php
│        │  │  ├─ LocaleAwareListener.php
│        │  │  ├─ LocaleListener.php
│        │  │  ├─ ProfilerListener.php
│        │  │  ├─ ResponseListener.php
│        │  │  ├─ RouterListener.php
│        │  │  ├─ SessionListener.php
│        │  │  ├─ SurrogateListener.php
│        │  │  └─ ValidateRequestListener.php
│        │  ├─ Exception
│        │  │  ├─ AccessDeniedHttpException.php
│        │  │  ├─ BadRequestHttpException.php
│        │  │  ├─ ConflictHttpException.php
│        │  │  ├─ ControllerDoesNotReturnResponseException.php
│        │  │  ├─ GoneHttpException.php
│        │  │  ├─ HttpException.php
│        │  │  ├─ HttpExceptionInterface.php
│        │  │  ├─ InvalidMetadataException.php
│        │  │  ├─ LengthRequiredHttpException.php
│        │  │  ├─ LockedHttpException.php
│        │  │  ├─ MethodNotAllowedHttpException.php
│        │  │  ├─ NearMissValueResolverException.php
│        │  │  ├─ NotAcceptableHttpException.php
│        │  │  ├─ NotFoundHttpException.php
│        │  │  ├─ PreconditionFailedHttpException.php
│        │  │  ├─ PreconditionRequiredHttpException.php
│        │  │  ├─ ResolverNotFoundException.php
│        │  │  ├─ ServiceUnavailableHttpException.php
│        │  │  ├─ TooManyRequestsHttpException.php
│        │  │  ├─ UnauthorizedHttpException.php
│        │  │  ├─ UnexpectedSessionUsageException.php
│        │  │  ├─ UnprocessableEntityHttpException.php
│        │  │  └─ UnsupportedMediaTypeHttpException.php
│        │  ├─ Fragment
│        │  │  ├─ AbstractSurrogateFragmentRenderer.php
│        │  │  ├─ EsiFragmentRenderer.php
│        │  │  ├─ FragmentHandler.php
│        │  │  ├─ FragmentRendererInterface.php
│        │  │  ├─ FragmentUriGenerator.php
│        │  │  ├─ FragmentUriGeneratorInterface.php
│        │  │  ├─ HIncludeFragmentRenderer.php
│        │  │  ├─ InlineFragmentRenderer.php
│        │  │  ├─ RoutableFragmentRenderer.php
│        │  │  └─ SsiFragmentRenderer.php
│        │  ├─ HttpCache
│        │  │  ├─ AbstractSurrogate.php
│        │  │  ├─ Esi.php
│        │  │  ├─ HttpCache.php
│        │  │  ├─ ResponseCacheStrategy.php
│        │  │  ├─ ResponseCacheStrategyInterface.php
│        │  │  ├─ Ssi.php
│        │  │  ├─ Store.php
│        │  │  ├─ StoreInterface.php
│        │  │  ├─ SubRequestHandler.php
│        │  │  └─ SurrogateInterface.php
│        │  ├─ HttpClientKernel.php
│        │  ├─ HttpKernel.php
│        │  ├─ HttpKernelBrowser.php
│        │  ├─ HttpKernelInterface.php
│        │  ├─ Kernel.php
│        │  ├─ KernelEvents.php
│        │  ├─ KernelInterface.php
│        │  ├─ LICENSE
│        │  ├─ Log
│        │  │  ├─ DebugLoggerConfigurator.php
│        │  │  ├─ DebugLoggerInterface.php
│        │  │  └─ Logger.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ Profiler
│        │  │  ├─ FileProfilerStorage.php
│        │  │  ├─ Profile.php
│        │  │  ├─ Profiler.php
│        │  │  ├─ ProfilerStateChecker.php
│        │  │  └─ ProfilerStorageInterface.php
│        │  ├─ README.md
│        │  ├─ RebootableInterface.php
│        │  ├─ Resources
│        │  │  └─ welcome.html.php
│        │  ├─ TerminableInterface.php
│        │  └─ Tests
│        │     ├─ Attribute
│        │     │  └─ WithLogLevelTest.php
│        │     ├─ Bundle
│        │     │  └─ BundleTest.php
│        │     ├─ CacheClearer
│        │     │  ├─ ChainCacheClearerTest.php
│        │     │  └─ Psr6CacheClearerTest.php
│        │     ├─ CacheWarmer
│        │     │  ├─ CacheWarmerAggregateTest.php
│        │     │  └─ CacheWarmerTest.php
│        │     ├─ Config
│        │     │  └─ FileLocatorTest.php
│        │     ├─ Controller
│        │     │  ├─ ArgumentResolver
│        │     │  │  ├─ BackedEnumValueResolverTest.php
│        │     │  │  ├─ DateTimeValueResolverTest.php
│        │     │  │  ├─ NotTaggedControllerValueResolverTest.php
│        │     │  │  ├─ QueryParameterValueResolverTest.php
│        │     │  │  ├─ RequestPayloadValueResolverTest.php
│        │     │  │  ├─ RequestValueResolverTest.php
│        │     │  │  ├─ ServiceValueResolverTest.php
│        │     │  │  ├─ TraceableValueResolverTest.php
│        │     │  │  ├─ UidValueResolverTest.php
│        │     │  │  └─ UploadedFileValueResolverTest.php
│        │     │  ├─ ArgumentResolverTest.php
│        │     │  ├─ ContainerControllerResolverTest.php
│        │     │  ├─ ControllerResolverTest.php
│        │     │  ├─ ErrorControllerTest.php
│        │     │  ├─ TraceableArgumentResolverTest.php
│        │     │  └─ TraceableControllerResolverTest.php
│        │     ├─ ControllerMetadata
│        │     │  ├─ ArgumentMetadataFactoryTest.php
│        │     │  └─ ArgumentMetadataTest.php
│        │     ├─ DataCollector
│        │     │  ├─ Compiler.log
│        │     │  ├─ ConfigDataCollectorTest.php
│        │     │  ├─ DataCollectorTest.php
│        │     │  ├─ DumpDataCollectorTest.php
│        │     │  ├─ ExceptionDataCollectorTest.php
│        │     │  ├─ LoggerDataCollectorTest.php
│        │     │  ├─ MemoryDataCollectorTest.php
│        │     │  ├─ RequestDataCollectorTest.php
│        │     │  ├─ RouterDataCollectorTest.php
│        │     │  └─ TimeDataCollectorTest.php
│        │     ├─ Debug
│        │     │  ├─ ErrorHandlerConfiguratorTest.php
│        │     │  └─ TraceableEventDispatcherTest.php
│        │     ├─ DependencyInjection
│        │     │  ├─ AddAnnotatedClassesToCachePassTest.php
│        │     │  ├─ ControllerArgumentValueResolverPassTest.php
│        │     │  ├─ FragmentRendererPassTest.php
│        │     │  ├─ LazyLoadingFragmentHandlerTest.php
│        │     │  ├─ LoggerPassTest.php
│        │     │  ├─ MergeExtensionConfigurationPassTest.php
│        │     │  ├─ RegisterControllerArgumentLocatorsPassTest.php
│        │     │  ├─ RegisterLocaleAwareServicesPassTest.php
│        │     │  ├─ RemoveEmptyControllerArgumentLocatorsPassTest.php
│        │     │  ├─ ResettableServicePassTest.php
│        │     │  └─ ServicesResetterTest.php
│        │     ├─ Event
│        │     │  ├─ ControllerArgumentsEventTest.php
│        │     │  ├─ ControllerEventTest.php
│        │     │  └─ ExceptionEventTest.php
│        │     ├─ EventListener
│        │     │  ├─ AddRequestFormatsListenerTest.php
│        │     │  ├─ CacheAttributeListenerTest.php
│        │     │  ├─ DebugHandlersListenerTest.php
│        │     │  ├─ DisallowRobotsIndexingListenerTest.php
│        │     │  ├─ DumpListenerTest.php
│        │     │  ├─ ErrorListenerTest.php
│        │     │  ├─ FragmentListenerTest.php
│        │     │  ├─ LocaleAwareListenerTest.php
│        │     │  ├─ LocaleListenerTest.php
│        │     │  ├─ ProfilerListenerTest.php
│        │     │  ├─ ResponseListenerTest.php
│        │     │  ├─ RouterListenerTest.php
│        │     │  ├─ SessionListenerTest.php
│        │     │  ├─ SurrogateListenerTest.php
│        │     │  └─ ValidateRequestListenerTest.php
│        │     ├─ Exception
│        │     │  ├─ AccessDeniedHttpExceptionTest.php
│        │     │  ├─ BadRequestHttpExceptionTest.php
│        │     │  ├─ ConflictHttpExceptionTest.php
│        │     │  ├─ GoneHttpExceptionTest.php
│        │     │  ├─ HttpExceptionTest.php
│        │     │  ├─ LengthRequiredHttpExceptionTest.php
│        │     │  ├─ LockedHttpExceptionTest.php
│        │     │  ├─ MethodNotAllowedHttpExceptionTest.php
│        │     │  ├─ NotAcceptableHttpExceptionTest.php
│        │     │  ├─ NotFoundHttpExceptionTest.php
│        │     │  ├─ PreconditionFailedHttpExceptionTest.php
│        │     │  ├─ PreconditionRequiredHttpExceptionTest.php
│        │     │  ├─ ServiceUnavailableHttpExceptionTest.php
│        │     │  ├─ TooManyRequestsHttpExceptionTest.php
│        │     │  ├─ UnauthorizedHttpExceptionTest.php
│        │     │  ├─ UnprocessableEntityHttpExceptionTest.php
│        │     │  └─ UnsupportedMediaTypeHttpExceptionTest.php
│        │     ├─ Fixtures
│        │     │  ├─ AcmeFooBundle
│        │     │  │  ├─ AcmeFooBundle.php
│        │     │  │  └─ Resources
│        │     │  │     └─ config
│        │     │  │        ├─ definition.php
│        │     │  │        └─ services.php
│        │     │  ├─ Attribute
│        │     │  │  ├─ Bar.php
│        │     │  │  ├─ Baz.php
│        │     │  │  └─ Foo.php
│        │     │  ├─ Bundle1Bundle
│        │     │  │  ├─ foo.txt
│        │     │  │  └─ Resources
│        │     │  ├─ ClearableService.php
│        │     │  ├─ Controller
│        │     │  │  ├─ ArgumentResolver
│        │     │  │  │  └─ UploadedFile
│        │     │  │  │     ├─ file-big.txt
│        │     │  │  │     └─ file-small.txt
│        │     │  │  ├─ AttributeController.php
│        │     │  │  ├─ BasicTypesController.php
│        │     │  │  ├─ CacheAttributeController.php
│        │     │  │  ├─ ExtendingRequest.php
│        │     │  │  ├─ ExtendingSession.php
│        │     │  │  ├─ NullableController.php
│        │     │  │  └─ VariadicController.php
│        │     │  ├─ DataCollector
│        │     │  │  ├─ CloneVarDataCollector.php
│        │     │  │  └─ DummyController.php
│        │     │  ├─ ExtensionNotValidBundle
│        │     │  │  ├─ DependencyInjection
│        │     │  │  │  └─ ExtensionNotValidExtension.php
│        │     │  │  └─ ExtensionNotValidBundle.php
│        │     │  ├─ ExtensionPresentBundle
│        │     │  │  ├─ DependencyInjection
│        │     │  │  │  └─ ExtensionPresentExtension.php
│        │     │  │  └─ ExtensionPresentBundle.php
│        │     │  ├─ IntEnum.php
│        │     │  ├─ KernelWithoutBundles.php
│        │     │  ├─ LazyResettableService.php
│        │     │  ├─ MockableUploadFileWithClientSize.php
│        │     │  ├─ MultiResettableService.php
│        │     │  ├─ ResettableService.php
│        │     │  ├─ Suit.php
│        │     │  ├─ TestClient.php
│        │     │  ├─ UsePropertyInDestruct.php
│        │     │  └─ WithPublicObjectProperty.php
│        │     ├─ Fragment
│        │     │  ├─ EsiFragmentRendererTest.php
│        │     │  ├─ FragmentHandlerTest.php
│        │     │  ├─ HIncludeFragmentRendererTest.php
│        │     │  ├─ InlineFragmentRendererTest.php
│        │     │  ├─ RoutableFragmentRendererTest.php
│        │     │  └─ SsiFragmentRendererTest.php
│        │     ├─ HttpCache
│        │     │  ├─ EsiTest.php
│        │     │  ├─ HttpCacheTest.php
│        │     │  ├─ HttpCacheTestCase.php
│        │     │  ├─ ResponseCacheStrategyTest.php
│        │     │  ├─ SsiTest.php
│        │     │  ├─ StoreTest.php
│        │     │  ├─ SubRequestHandlerTest.php
│        │     │  ├─ TestHttpKernel.php
│        │     │  └─ TestMultipleHttpKernel.php
│        │     ├─ HttpClientKernelTest.php
│        │     ├─ HttpKernelBrowserTest.php
│        │     ├─ HttpKernelTest.php
│        │     ├─ KernelTest.php
│        │     ├─ Log
│        │     │  └─ LoggerTest.php
│        │     ├─ Logger.php
│        │     ├─ Profiler
│        │     │  ├─ FileProfilerStorageTest.php
│        │     │  └─ ProfilerTest.php
│        │     └─ TestHttpKernel.php
│        ├─ polyfill-intl-grapheme
│        │  ├─ bootstrap.php
│        │  ├─ bootstrap80.php
│        │  ├─ composer.json
│        │  ├─ Grapheme.php
│        │  ├─ LICENSE
│        │  └─ README.md
│        ├─ polyfill-intl-normalizer
│        │  ├─ bootstrap.php
│        │  ├─ bootstrap80.php
│        │  ├─ composer.json
│        │  ├─ LICENSE
│        │  ├─ Normalizer.php
│        │  ├─ README.md
│        │  └─ Resources
│        │     ├─ stubs
│        │     │  └─ Normalizer.php
│        │     └─ unidata
│        │        ├─ canonicalComposition.php
│        │        ├─ canonicalDecomposition.php
│        │        ├─ combiningClass.php
│        │        └─ compatibilityDecomposition.php
│        ├─ polyfill-mbstring
│        │  ├─ bootstrap.php
│        │  ├─ bootstrap80.php
│        │  ├─ composer.json
│        │  ├─ LICENSE
│        │  ├─ Mbstring.php
│        │  ├─ README.md
│        │  └─ Resources
│        │     └─ unidata
│        │        ├─ caseFolding.php
│        │        ├─ lowerCase.php
│        │        ├─ titleCaseRegexp.php
│        │        └─ upperCase.php
│        ├─ polyfill-php83
│        │  ├─ bootstrap.php
│        │  ├─ bootstrap81.php
│        │  ├─ composer.json
│        │  ├─ LICENSE
│        │  ├─ Php83.php
│        │  ├─ README.md
│        │  └─ Resources
│        │     └─ stubs
│        │        ├─ DateError.php
│        │        ├─ DateException.php
│        │        ├─ DateInvalidOperationException.php
│        │        ├─ DateInvalidTimeZoneException.php
│        │        ├─ DateMalformedIntervalStringException.php
│        │        ├─ DateMalformedPeriodStringException.php
│        │        ├─ DateMalformedStringException.php
│        │        ├─ DateObjectError.php
│        │        ├─ DateRangeError.php
│        │        ├─ Override.php
│        │        └─ SQLite3Exception.php
│        ├─ routing
│        │  ├─ Alias.php
│        │  ├─ Annotation
│        │  │  └─ Route.php
│        │  ├─ Attribute
│        │  │  ├─ DeprecatedAlias.php
│        │  │  └─ Route.php
│        │  ├─ CHANGELOG.md
│        │  ├─ CompiledRoute.php
│        │  ├─ composer.json
│        │  ├─ DependencyInjection
│        │  │  ├─ AddExpressionLanguageProvidersPass.php
│        │  │  └─ RoutingResolverPass.php
│        │  ├─ Exception
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ InvalidArgumentException.php
│        │  │  ├─ InvalidParameterException.php
│        │  │  ├─ LogicException.php
│        │  │  ├─ MethodNotAllowedException.php
│        │  │  ├─ MissingMandatoryParametersException.php
│        │  │  ├─ NoConfigurationException.php
│        │  │  ├─ ResourceNotFoundException.php
│        │  │  ├─ RouteCircularReferenceException.php
│        │  │  ├─ RouteNotFoundException.php
│        │  │  └─ RuntimeException.php
│        │  ├─ Generator
│        │  │  ├─ CompiledUrlGenerator.php
│        │  │  ├─ ConfigurableRequirementsInterface.php
│        │  │  ├─ Dumper
│        │  │  │  ├─ CompiledUrlGeneratorDumper.php
│        │  │  │  ├─ GeneratorDumper.php
│        │  │  │  └─ GeneratorDumperInterface.php
│        │  │  ├─ UrlGenerator.php
│        │  │  └─ UrlGeneratorInterface.php
│        │  ├─ LICENSE
│        │  ├─ Loader
│        │  │  ├─ AttributeClassLoader.php
│        │  │  ├─ AttributeDirectoryLoader.php
│        │  │  ├─ AttributeFileLoader.php
│        │  │  ├─ ClosureLoader.php
│        │  │  ├─ Configurator
│        │  │  │  ├─ AliasConfigurator.php
│        │  │  │  ├─ CollectionConfigurator.php
│        │  │  │  ├─ ImportConfigurator.php
│        │  │  │  ├─ RouteConfigurator.php
│        │  │  │  ├─ RoutingConfigurator.php
│        │  │  │  └─ Traits
│        │  │  │     ├─ AddTrait.php
│        │  │  │     ├─ HostTrait.php
│        │  │  │     ├─ LocalizedRouteTrait.php
│        │  │  │     ├─ PrefixTrait.php
│        │  │  │     └─ RouteTrait.php
│        │  │  ├─ ContainerLoader.php
│        │  │  ├─ DirectoryLoader.php
│        │  │  ├─ GlobFileLoader.php
│        │  │  ├─ ObjectLoader.php
│        │  │  ├─ PhpFileLoader.php
│        │  │  ├─ Psr4DirectoryLoader.php
│        │  │  ├─ schema
│        │  │  │  └─ routing
│        │  │  │     └─ routing-1.0.xsd
│        │  │  ├─ XmlFileLoader.php
│        │  │  └─ YamlFileLoader.php
│        │  ├─ Matcher
│        │  │  ├─ CompiledUrlMatcher.php
│        │  │  ├─ Dumper
│        │  │  │  ├─ CompiledUrlMatcherDumper.php
│        │  │  │  ├─ CompiledUrlMatcherTrait.php
│        │  │  │  ├─ MatcherDumper.php
│        │  │  │  ├─ MatcherDumperInterface.php
│        │  │  │  └─ StaticPrefixCollection.php
│        │  │  ├─ ExpressionLanguageProvider.php
│        │  │  ├─ RedirectableUrlMatcher.php
│        │  │  ├─ RedirectableUrlMatcherInterface.php
│        │  │  ├─ RequestMatcherInterface.php
│        │  │  ├─ TraceableUrlMatcher.php
│        │  │  ├─ UrlMatcher.php
│        │  │  └─ UrlMatcherInterface.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ RequestContext.php
│        │  ├─ RequestContextAwareInterface.php
│        │  ├─ Requirement
│        │  │  ├─ EnumRequirement.php
│        │  │  └─ Requirement.php
│        │  ├─ Route.php
│        │  ├─ RouteCollection.php
│        │  ├─ RouteCompiler.php
│        │  ├─ RouteCompilerInterface.php
│        │  ├─ Router.php
│        │  ├─ RouterInterface.php
│        │  └─ Tests
│        │     ├─ Attribute
│        │     │  └─ RouteTest.php
│        │     ├─ CompiledRouteTest.php
│        │     ├─ DependencyInjection
│        │     │  ├─ AddExpressionLanguageProvidersPassTest.php
│        │     │  └─ RoutingResolverPassTest.php
│        │     ├─ Fixtures
│        │     │  ├─ alias
│        │     │  │  ├─ alias.php
│        │     │  │  ├─ alias.xml
│        │     │  │  ├─ alias.yaml
│        │     │  │  ├─ expected.php
│        │     │  │  ├─ invalid-alias.yaml
│        │     │  │  ├─ invalid-deprecated-no-package.xml
│        │     │  │  ├─ invalid-deprecated-no-package.yaml
│        │     │  │  ├─ invalid-deprecated-no-version.xml
│        │     │  │  ├─ invalid-deprecated-no-version.yaml
│        │     │  │  └─ override.yaml
│        │     │  ├─ annotated.php
│        │     │  ├─ AttributedClasses
│        │     │  │  ├─ AbstractClass.php
│        │     │  │  ├─ BarClass.php
│        │     │  │  ├─ BazClass.php
│        │     │  │  ├─ EncodingClass.php
│        │     │  │  ├─ FooClass.php
│        │     │  │  └─ FooTrait.php
│        │     │  ├─ AttributeFixtures
│        │     │  │  ├─ AbstractClassController.php
│        │     │  │  ├─ ActionPathController.php
│        │     │  │  ├─ AliasClassController.php
│        │     │  │  ├─ AliasInvokableController.php
│        │     │  │  ├─ AliasRouteController.php
│        │     │  │  ├─ BazClass.php
│        │     │  │  ├─ DefaultValueController.php
│        │     │  │  ├─ DeprecatedAliasCustomMessageRouteController.php
│        │     │  │  ├─ DeprecatedAliasRouteController.php
│        │     │  │  ├─ EncodingClass.php
│        │     │  │  ├─ ExplicitLocalizedActionPathController.php
│        │     │  │  ├─ ExtendedRoute.php
│        │     │  │  ├─ ExtendedRouteOnClassController.php
│        │     │  │  ├─ ExtendedRouteOnMethodController.php
│        │     │  │  ├─ FooController.php
│        │     │  │  ├─ GlobalDefaultsClass.php
│        │     │  │  ├─ InvokableController.php
│        │     │  │  ├─ InvokableFQCNAliasConflictController.php
│        │     │  │  ├─ InvokableLocalizedController.php
│        │     │  │  ├─ InvokableMethodController.php
│        │     │  │  ├─ LocalizedActionPathController.php
│        │     │  │  ├─ LocalizedMethodActionControllers.php
│        │     │  │  ├─ LocalizedPrefixLocalizedActionController.php
│        │     │  │  ├─ LocalizedPrefixMissingLocaleActionController.php
│        │     │  │  ├─ LocalizedPrefixMissingRouteLocaleActionController.php
│        │     │  │  ├─ LocalizedPrefixWithRouteWithoutLocale.php
│        │     │  │  ├─ MethodActionControllers.php
│        │     │  │  ├─ MethodsAndSchemes.php
│        │     │  │  ├─ MissingRouteNameController.php
│        │     │  │  ├─ MultipleDeprecatedAliasRouteController.php
│        │     │  │  ├─ NothingButNameController.php
│        │     │  │  ├─ PrefixedActionLocalizedRouteController.php
│        │     │  │  ├─ PrefixedActionPathController.php
│        │     │  │  ├─ RequirementsWithoutPlaceholderNameController.php
│        │     │  │  ├─ RouteWithEnv.php
│        │     │  │  ├─ RouteWithPrefixController.php
│        │     │  │  ├─ RouteWithPriorityController.php
│        │     │  │  └─ Utf8ActionControllers.php
│        │     │  ├─ Attributes
│        │     │  │  └─ FooAttributes.php
│        │     │  ├─ AttributesFixtures
│        │     │  │  ├─ AttributesClassParamAfterCommaController.php
│        │     │  │  ├─ AttributesClassParamAfterParenthesisController.php
│        │     │  │  ├─ AttributesClassParamInlineAfterCommaController.php
│        │     │  │  ├─ AttributesClassParamInlineAfterParenthesisController.php
│        │     │  │  ├─ AttributesClassParamInlineQuotedAfterCommaController.php
│        │     │  │  ├─ AttributesClassParamInlineQuotedAfterParenthesisController.php
│        │     │  │  ├─ AttributesClassParamQuotedAfterCommaController.php
│        │     │  │  └─ AttributesClassParamQuotedAfterParenthesisController.php
│        │     │  ├─ bad_format.yml
│        │     │  ├─ bar.xml
│        │     │  ├─ class-attributes.php
│        │     │  ├─ class-attributes.xml
│        │     │  ├─ class-attributes.yaml
│        │     │  ├─ collection-defaults.php
│        │     │  ├─ controller
│        │     │  │  ├─ empty_wildcard
│        │     │  │  ├─ import_controller.xml
│        │     │  │  ├─ import_controller.yml
│        │     │  │  ├─ import_override_defaults.xml
│        │     │  │  ├─ import_override_defaults.yml
│        │     │  │  ├─ import__controller.xml
│        │     │  │  ├─ import__controller.yml
│        │     │  │  ├─ override_defaults.xml
│        │     │  │  ├─ override_defaults.yml
│        │     │  │  ├─ routing.xml
│        │     │  │  └─ routing.yml
│        │     │  ├─ CustomCompiledRoute.php
│        │     │  ├─ CustomRouteCompiler.php
│        │     │  ├─ CustomXmlFileLoader.php
│        │     │  ├─ defaults.php
│        │     │  ├─ defaults.xml
│        │     │  ├─ defaults.yml
│        │     │  ├─ directory
│        │     │  │  ├─ recurse
│        │     │  │  │  ├─ routes1.yml
│        │     │  │  │  └─ routes2.yml
│        │     │  │  └─ routes3.yml
│        │     │  ├─ directory_import
│        │     │  │  └─ import.yml
│        │     │  ├─ dumper
│        │     │  │  ├─ compiled_url_matcher0.php
│        │     │  │  ├─ compiled_url_matcher1.php
│        │     │  │  ├─ compiled_url_matcher10.php
│        │     │  │  ├─ compiled_url_matcher11.php
│        │     │  │  ├─ compiled_url_matcher12.php
│        │     │  │  ├─ compiled_url_matcher13.php
│        │     │  │  ├─ compiled_url_matcher14.php
│        │     │  │  ├─ compiled_url_matcher2.php
│        │     │  │  ├─ compiled_url_matcher3.php
│        │     │  │  ├─ compiled_url_matcher4.php
│        │     │  │  ├─ compiled_url_matcher5.php
│        │     │  │  ├─ compiled_url_matcher6.php
│        │     │  │  ├─ compiled_url_matcher7.php
│        │     │  │  ├─ compiled_url_matcher8.php
│        │     │  │  └─ compiled_url_matcher9.php
│        │     │  ├─ empty.yml
│        │     │  ├─ Enum
│        │     │  │  ├─ TestIntBackedEnum.php
│        │     │  │  ├─ TestStringBackedEnum.php
│        │     │  │  ├─ TestStringBackedEnum2.php
│        │     │  │  └─ TestUnitEnum.php
│        │     │  ├─ file_resource.yml
│        │     │  ├─ foo.xml
│        │     │  ├─ foo1.xml
│        │     │  ├─ glob
│        │     │  │  ├─ bar.xml
│        │     │  │  ├─ bar.yml
│        │     │  │  ├─ baz.xml
│        │     │  │  ├─ baz.yml
│        │     │  │  ├─ import_multiple.xml
│        │     │  │  ├─ import_multiple.yml
│        │     │  │  ├─ import_single.xml
│        │     │  │  ├─ import_single.yml
│        │     │  │  ├─ php_dsl.php
│        │     │  │  ├─ php_dsl_bar.php
│        │     │  │  └─ php_dsl_baz.php
│        │     │  ├─ imported-with-defaults.php
│        │     │  ├─ imported-with-defaults.xml
│        │     │  ├─ imported-with-defaults.yml
│        │     │  ├─ importer-with-defaults.php
│        │     │  ├─ importer-with-defaults.xml
│        │     │  ├─ importer-with-defaults.yml
│        │     │  ├─ import_with_name_prefix
│        │     │  │  ├─ routing.xml
│        │     │  │  └─ routing.yml
│        │     │  ├─ import_with_no_trailing_slash
│        │     │  │  ├─ routing.xml
│        │     │  │  └─ routing.yml
│        │     │  ├─ incomplete.yml
│        │     │  ├─ list_defaults.xml
│        │     │  ├─ list_in_list_defaults.xml
│        │     │  ├─ list_in_map_defaults.xml
│        │     │  ├─ list_null_values.xml
│        │     │  ├─ locale_and_host
│        │     │  │  ├─ import-with-host-expected-collection.php
│        │     │  │  ├─ import-with-locale-and-host-expected-collection.php
│        │     │  │  ├─ import-with-single-host-expected-collection.php
│        │     │  │  ├─ import-without-host-expected-collection.php
│        │     │  │  ├─ imported.php
│        │     │  │  ├─ imported.xml
│        │     │  │  ├─ imported.yml
│        │     │  │  ├─ importer-with-host.php
│        │     │  │  ├─ importer-with-host.xml
│        │     │  │  ├─ importer-with-host.yml
│        │     │  │  ├─ importer-with-locale-and-host.php
│        │     │  │  ├─ importer-with-locale-and-host.xml
│        │     │  │  ├─ importer-with-locale-and-host.yml
│        │     │  │  ├─ importer-with-single-host.php
│        │     │  │  ├─ importer-with-single-host.xml
│        │     │  │  ├─ importer-with-single-host.yml
│        │     │  │  ├─ importer-without-host.php
│        │     │  │  ├─ importer-without-host.xml
│        │     │  │  ├─ importer-without-host.yml
│        │     │  │  ├─ priorized-host.yml
│        │     │  │  ├─ route-with-hosts-expected-collection.php
│        │     │  │  ├─ route-with-hosts.php
│        │     │  │  ├─ route-with-hosts.xml
│        │     │  │  └─ route-with-hosts.yml
│        │     │  ├─ localized
│        │     │  │  ├─ imported-with-locale-but-not-localized.xml
│        │     │  │  ├─ imported-with-locale-but-not-localized.yml
│        │     │  │  ├─ imported-with-locale.xml
│        │     │  │  ├─ imported-with-locale.yml
│        │     │  │  ├─ imported-with-utf8.php
│        │     │  │  ├─ imported-with-utf8.xml
│        │     │  │  ├─ imported-with-utf8.yml
│        │     │  │  ├─ importer-with-controller-default.yml
│        │     │  │  ├─ importer-with-locale-imports-non-localized-route.xml
│        │     │  │  ├─ importer-with-locale-imports-non-localized-route.yml
│        │     │  │  ├─ importer-with-locale.xml
│        │     │  │  ├─ importer-with-locale.yml
│        │     │  │  ├─ importer-with-utf8.php
│        │     │  │  ├─ importer-with-utf8.xml
│        │     │  │  ├─ importer-with-utf8.yml
│        │     │  │  ├─ importing-localized-route.yml
│        │     │  │  ├─ localized-prefix.yml
│        │     │  │  ├─ localized-route.yml
│        │     │  │  ├─ missing-locale-in-importer.yml
│        │     │  │  ├─ not-localized.yml
│        │     │  │  ├─ officially_formatted_locales.yml
│        │     │  │  ├─ route-without-path-or-locales.yml
│        │     │  │  ├─ utf8.php
│        │     │  │  ├─ utf8.xml
│        │     │  │  └─ utf8.yml
│        │     │  ├─ localized.xml
│        │     │  ├─ map_defaults.xml
│        │     │  ├─ map_in_list_defaults.xml
│        │     │  ├─ map_in_map_defaults.xml
│        │     │  ├─ map_null_values.xml
│        │     │  ├─ missing_id.xml
│        │     │  ├─ missing_path.xml
│        │     │  ├─ namespaceprefix.xml
│        │     │  ├─ nonesense_resource_plus_path.yml
│        │     │  ├─ nonesense_type_without_resource.yml
│        │     │  ├─ nonvalid-deprecated-route.xml
│        │     │  ├─ nonvalid.xml
│        │     │  ├─ nonvalid.yml
│        │     │  ├─ nonvalid2.yml
│        │     │  ├─ nonvalidkeys.yml
│        │     │  ├─ nonvalidnode.xml
│        │     │  ├─ nonvalidroute.xml
│        │     │  ├─ null_values.xml
│        │     │  ├─ OtherAnnotatedClasses
│        │     │  │  ├─ NoStartTagClass.php
│        │     │  │  └─ VariadicClass.php
│        │     │  ├─ php_dsl.php
│        │     │  ├─ php_dsl_i18n.php
│        │     │  ├─ php_dsl_sub.php
│        │     │  ├─ php_dsl_sub_i18n.php
│        │     │  ├─ php_dsl_sub_root.php
│        │     │  ├─ php_object_dsl.php
│        │     │  ├─ psr4-attributes.php
│        │     │  ├─ psr4-attributes.xml
│        │     │  ├─ psr4-attributes.yaml
│        │     │  ├─ psr4-controllers-redirection
│        │     │  │  ├─ psr4-attributes.php
│        │     │  │  ├─ psr4-attributes.xml
│        │     │  │  └─ psr4-attributes.yaml
│        │     │  ├─ psr4-controllers-redirection.php
│        │     │  ├─ psr4-controllers-redirection.xml
│        │     │  ├─ psr4-controllers-redirection.yaml
│        │     │  ├─ Psr4Controllers
│        │     │  │  ├─ MyController.php
│        │     │  │  ├─ MyUnannotatedController.php
│        │     │  │  └─ SubNamespace
│        │     │  │     ├─ EvenDeeperNamespace
│        │     │  │     │  └─ MyOtherController.php
│        │     │  │     ├─ IrrelevantClass.php
│        │     │  │     ├─ IrrelevantEnum.php
│        │     │  │     ├─ IrrelevantInterface.php
│        │     │  │     ├─ MyAbstractController.php
│        │     │  │     ├─ MyChildController.php
│        │     │  │     ├─ MyControllerWithATrait.php
│        │     │  │     └─ SomeSharedImplementation.php
│        │     │  ├─ RedirectableUrlMatcher.php
│        │     │  ├─ requirements_without_placeholder_name.yml
│        │     │  ├─ scalar_defaults.xml
│        │     │  ├─ special_route_name.yml
│        │     │  ├─ TraceableAttributeClassLoader.php
│        │     │  ├─ validpattern.php
│        │     │  ├─ validpattern.xml
│        │     │  ├─ validpattern.yml
│        │     │  ├─ validresource.php
│        │     │  ├─ validresource.xml
│        │     │  ├─ validresource.yml
│        │     │  ├─ when-env.xml
│        │     │  ├─ when-env.yml
│        │     │  ├─ withdoctype.xml
│        │     │  └─ with_define_path_variable.php
│        │     ├─ Generator
│        │     │  ├─ Dumper
│        │     │  │  └─ CompiledUrlGeneratorDumperTest.php
│        │     │  └─ UrlGeneratorTest.php
│        │     ├─ Loader
│        │     │  ├─ AttributeClassLoaderTest.php
│        │     │  ├─ AttributeDirectoryLoaderTest.php
│        │     │  ├─ AttributeFileLoaderTest.php
│        │     │  ├─ ClosureLoaderTest.php
│        │     │  ├─ ContainerLoaderTest.php
│        │     │  ├─ DirectoryLoaderTest.php
│        │     │  ├─ FileLocatorStub.php
│        │     │  ├─ GlobFileLoaderTest.php
│        │     │  ├─ ObjectLoaderTest.php
│        │     │  ├─ PhpFileLoaderTest.php
│        │     │  ├─ Psr4DirectoryLoaderTest.php
│        │     │  ├─ XmlFileLoaderTest.php
│        │     │  └─ YamlFileLoaderTest.php
│        │     ├─ Matcher
│        │     │  ├─ CompiledRedirectableUrlMatcherTest.php
│        │     │  ├─ CompiledUrlMatcherTest.php
│        │     │  ├─ Dumper
│        │     │  │  ├─ CompiledUrlMatcherDumperTest.php
│        │     │  │  └─ StaticPrefixCollectionTest.php
│        │     │  ├─ ExpressionLanguageProviderTest.php
│        │     │  ├─ RedirectableUrlMatcherTest.php
│        │     │  ├─ TraceableUrlMatcherTest.php
│        │     │  └─ UrlMatcherTest.php
│        │     ├─ RequestContextTest.php
│        │     ├─ Requirement
│        │     │  ├─ EnumRequirementTest.php
│        │     │  └─ RequirementTest.php
│        │     ├─ RouteCollectionTest.php
│        │     ├─ RouteCompilerTest.php
│        │     ├─ RouterTest.php
│        │     └─ RouteTest.php
│        ├─ runtime
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ GenericRuntime.php
│        │  ├─ Internal
│        │  │  ├─ autoload_runtime.template
│        │  │  ├─ BasicErrorHandler.php
│        │  │  ├─ ComposerPlugin.php
│        │  │  ├─ Console
│        │  │  │  ├─ ApplicationRuntime.php
│        │  │  │  ├─ Command
│        │  │  │  │  └─ CommandRuntime.php
│        │  │  │  ├─ Input
│        │  │  │  │  └─ InputInterfaceRuntime.php
│        │  │  │  └─ Output
│        │  │  │     └─ OutputInterfaceRuntime.php
│        │  │  ├─ HttpFoundation
│        │  │  │  ├─ RequestRuntime.php
│        │  │  │  └─ ResponseRuntime.php
│        │  │  ├─ HttpKernel
│        │  │  │  └─ HttpKernelInterfaceRuntime.php
│        │  │  ├─ MissingDotenv.php
│        │  │  └─ SymfonyErrorHandler.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Resolver
│        │  │  ├─ ClosureResolver.php
│        │  │  └─ DebugClosureResolver.php
│        │  ├─ ResolverInterface.php
│        │  ├─ Runner
│        │  │  ├─ ClosureRunner.php
│        │  │  └─ Symfony
│        │  │     ├─ ConsoleApplicationRunner.php
│        │  │     ├─ HttpKernelRunner.php
│        │  │     └─ ResponseRunner.php
│        │  ├─ RunnerInterface.php
│        │  ├─ RuntimeInterface.php
│        │  ├─ SymfonyRuntime.php
│        │  └─ Tests
│        │     └─ phpt
│        │        ├─ .env
│        │        ├─ .env.extra
│        │        ├─ application.php
│        │        ├─ application.phpt
│        │        ├─ autoload.php
│        │        ├─ command.php
│        │        ├─ command.phpt
│        │        ├─ command2.php
│        │        ├─ command2.phpt
│        │        ├─ command_list.php
│        │        ├─ command_list.phpt
│        │        ├─ dotenv_extra_load.php
│        │        ├─ dotenv_extra_load.phpt
│        │        ├─ dotenv_extra_overload.php
│        │        ├─ dotenv_extra_overload.phpt
│        │        ├─ dotenv_overload.php
│        │        ├─ dotenv_overload.phpt
│        │        ├─ dotenv_overload_command_debug_exists_0_to_1.php
│        │        ├─ dotenv_overload_command_debug_exists_0_to_1.phpt
│        │        ├─ dotenv_overload_command_debug_exists_1_to_0.php
│        │        ├─ dotenv_overload_command_debug_exists_1_to_0.phpt
│        │        ├─ dotenv_overload_command_env_conflict.php
│        │        ├─ dotenv_overload_command_env_conflict.phpt
│        │        ├─ dotenv_overload_command_env_exists.php
│        │        ├─ dotenv_overload_command_env_exists.phpt
│        │        ├─ dotenv_overload_command_no_debug.php
│        │        ├─ dotenv_overload_command_no_debug.phpt
│        │        ├─ generic-request.php
│        │        ├─ generic-request.phpt
│        │        ├─ hello.php
│        │        ├─ hello.phpt
│        │        ├─ kernel-loop.php
│        │        ├─ kernel-loop.phpt
│        │        ├─ kernel.php
│        │        ├─ kernel.phpt
│        │        ├─ kernel_register_argc_argv.phpt
│        │        ├─ request.php
│        │        ├─ request.phpt
│        │        ├─ runtime-options.php
│        │        └─ runtime-options.phpt
│        ├─ service-contracts
│        │  ├─ Attribute
│        │  │  ├─ Required.php
│        │  │  └─ SubscribedService.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ LICENSE
│        │  ├─ README.md
│        │  ├─ ResetInterface.php
│        │  ├─ ServiceCollectionInterface.php
│        │  ├─ ServiceLocatorTrait.php
│        │  ├─ ServiceMethodsSubscriberTrait.php
│        │  ├─ ServiceProviderInterface.php
│        │  ├─ ServiceSubscriberInterface.php
│        │  ├─ ServiceSubscriberTrait.php
│        │  └─ Test
│        │     ├─ ServiceLocatorTest.php
│        │     └─ ServiceLocatorTestCase.php
│        ├─ string
│        │  ├─ AbstractString.php
│        │  ├─ AbstractUnicodeString.php
│        │  ├─ ByteString.php
│        │  ├─ CHANGELOG.md
│        │  ├─ CodePointString.php
│        │  ├─ composer.json
│        │  ├─ Exception
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ InvalidArgumentException.php
│        │  │  └─ RuntimeException.php
│        │  ├─ Inflector
│        │  │  ├─ EnglishInflector.php
│        │  │  ├─ FrenchInflector.php
│        │  │  ├─ InflectorInterface.php
│        │  │  └─ SpanishInflector.php
│        │  ├─ LazyString.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Resources
│        │  │  ├─ bin
│        │  │  │  └─ update-data.php
│        │  │  ├─ data
│        │  │  │  ├─ wcswidth_table_wide.php
│        │  │  │  └─ wcswidth_table_zero.php
│        │  │  ├─ functions.php
│        │  │  └─ WcswidthDataGenerator.php
│        │  ├─ Slugger
│        │  │  ├─ AsciiSlugger.php
│        │  │  └─ SluggerInterface.php
│        │  ├─ Tests
│        │  │  ├─ AbstractAsciiTestCase.php
│        │  │  ├─ AbstractUnicodeTestCase.php
│        │  │  ├─ ByteStringTest.php
│        │  │  ├─ CodePointStringTest.php
│        │  │  ├─ FunctionsTest.php
│        │  │  ├─ Inflector
│        │  │  │  ├─ EnglishInflectorTest.php
│        │  │  │  ├─ FrenchInflectorTest.php
│        │  │  │  └─ SpanishInflectorTest.php
│        │  │  ├─ LazyStringTest.php
│        │  │  ├─ Slugger
│        │  │  │  └─ AsciiSluggerTest.php
│        │  │  ├─ SluggerTest.php
│        │  │  └─ UnicodeStringTest.php
│        │  ├─ TruncateMode.php
│        │  └─ UnicodeString.php
│        ├─ var-dumper
│        │  ├─ Caster
│        │  │  ├─ AddressInfoCaster.php
│        │  │  ├─ AmqpCaster.php
│        │  │  ├─ ArgsStub.php
│        │  │  ├─ Caster.php
│        │  │  ├─ ClassStub.php
│        │  │  ├─ ConstStub.php
│        │  │  ├─ CurlCaster.php
│        │  │  ├─ CutArrayStub.php
│        │  │  ├─ CutStub.php
│        │  │  ├─ DateCaster.php
│        │  │  ├─ DoctrineCaster.php
│        │  │  ├─ DOMCaster.php
│        │  │  ├─ DsCaster.php
│        │  │  ├─ DsPairStub.php
│        │  │  ├─ EnumStub.php
│        │  │  ├─ ExceptionCaster.php
│        │  │  ├─ FFICaster.php
│        │  │  ├─ FiberCaster.php
│        │  │  ├─ FrameStub.php
│        │  │  ├─ GdCaster.php
│        │  │  ├─ GmpCaster.php
│        │  │  ├─ ImagineCaster.php
│        │  │  ├─ ImgStub.php
│        │  │  ├─ IntlCaster.php
│        │  │  ├─ LinkStub.php
│        │  │  ├─ MemcachedCaster.php
│        │  │  ├─ MysqliCaster.php
│        │  │  ├─ OpenSSLCaster.php
│        │  │  ├─ PdoCaster.php
│        │  │  ├─ PgSqlCaster.php
│        │  │  ├─ ProxyManagerCaster.php
│        │  │  ├─ RdKafkaCaster.php
│        │  │  ├─ RedisCaster.php
│        │  │  ├─ ReflectionCaster.php
│        │  │  ├─ ResourceCaster.php
│        │  │  ├─ ScalarStub.php
│        │  │  ├─ SocketCaster.php
│        │  │  ├─ SplCaster.php
│        │  │  ├─ SqliteCaster.php
│        │  │  ├─ StubCaster.php
│        │  │  ├─ SymfonyCaster.php
│        │  │  ├─ TraceStub.php
│        │  │  ├─ UninitializedStub.php
│        │  │  ├─ UuidCaster.php
│        │  │  ├─ VirtualStub.php
│        │  │  ├─ XmlReaderCaster.php
│        │  │  └─ XmlResourceCaster.php
│        │  ├─ CHANGELOG.md
│        │  ├─ Cloner
│        │  │  ├─ AbstractCloner.php
│        │  │  ├─ ClonerInterface.php
│        │  │  ├─ Cursor.php
│        │  │  ├─ Data.php
│        │  │  ├─ DumperInterface.php
│        │  │  ├─ Internal
│        │  │  │  └─ NoDefault.php
│        │  │  ├─ Stub.php
│        │  │  └─ VarCloner.php
│        │  ├─ Command
│        │  │  ├─ Descriptor
│        │  │  │  ├─ CliDescriptor.php
│        │  │  │  ├─ DumpDescriptorInterface.php
│        │  │  │  └─ HtmlDescriptor.php
│        │  │  └─ ServerDumpCommand.php
│        │  ├─ composer.json
│        │  ├─ Dumper
│        │  │  ├─ AbstractDumper.php
│        │  │  ├─ CliDumper.php
│        │  │  ├─ ContextProvider
│        │  │  │  ├─ CliContextProvider.php
│        │  │  │  ├─ ContextProviderInterface.php
│        │  │  │  ├─ RequestContextProvider.php
│        │  │  │  └─ SourceContextProvider.php
│        │  │  ├─ ContextualizedDumper.php
│        │  │  ├─ DataDumperInterface.php
│        │  │  ├─ HtmlDumper.php
│        │  │  └─ ServerDumper.php
│        │  ├─ Exception
│        │  │  └─ ThrowingCasterException.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Resources
│        │  │  ├─ bin
│        │  │  │  └─ var-dump-server
│        │  │  ├─ css
│        │  │  │  └─ htmlDescriptor.css
│        │  │  ├─ functions
│        │  │  │  └─ dump.php
│        │  │  └─ js
│        │  │     └─ htmlDescriptor.js
│        │  ├─ Server
│        │  │  ├─ Connection.php
│        │  │  └─ DumpServer.php
│        │  ├─ Test
│        │  │  └─ VarDumperTestTrait.php
│        │  ├─ Tests
│        │  │  ├─ Caster
│        │  │  │  ├─ AddressInfoCasterTest.php
│        │  │  │  ├─ CasterTest.php
│        │  │  │  ├─ CurlCasterTest.php
│        │  │  │  ├─ DateCasterTest.php
│        │  │  │  ├─ DoctrineCasterTest.php
│        │  │  │  ├─ DOMCasterTest.php
│        │  │  │  ├─ ExceptionCasterTest.php
│        │  │  │  ├─ FFICasterTest.php
│        │  │  │  ├─ FiberCasterTest.php
│        │  │  │  ├─ GmpCasterTest.php
│        │  │  │  ├─ IntlCasterTest.php
│        │  │  │  ├─ MemcachedCasterTest.php
│        │  │  │  ├─ MysqliCasterTest.php
│        │  │  │  ├─ OpenSSLCasterTest.php
│        │  │  │  ├─ PdoCasterTest.php
│        │  │  │  ├─ RdKafkaCasterTest.php
│        │  │  │  ├─ RedisCasterTest.php
│        │  │  │  ├─ ReflectionCasterTest.php
│        │  │  │  ├─ ResourceCasterTest.php
│        │  │  │  ├─ SocketCasterTest.php
│        │  │  │  ├─ SplCasterTest.php
│        │  │  │  ├─ SqliteCasterTest.php
│        │  │  │  ├─ StubCasterTest.php
│        │  │  │  ├─ SymfonyCasterTest.php
│        │  │  │  └─ XmlReaderCasterTest.php
│        │  │  ├─ Cloner
│        │  │  │  ├─ DataTest.php
│        │  │  │  ├─ StubTest.php
│        │  │  │  └─ VarClonerTest.php
│        │  │  ├─ Command
│        │  │  │  ├─ Descriptor
│        │  │  │  │  ├─ CliDescriptorTest.php
│        │  │  │  │  └─ HtmlDescriptorTest.php
│        │  │  │  └─ ServerDumpCommandTest.php
│        │  │  ├─ Dumper
│        │  │  │  ├─ CliDumperTest.php
│        │  │  │  ├─ ContextProvider
│        │  │  │  │  └─ RequestContextProviderTest.php
│        │  │  │  ├─ ContextualizedDumperTest.php
│        │  │  │  ├─ functions
│        │  │  │  │  ├─ dd_with_multiple_args.phpt
│        │  │  │  │  ├─ dd_with_named_args.phpt
│        │  │  │  │  ├─ dd_with_null.phpt
│        │  │  │  │  ├─ dd_with_single_arg.phpt
│        │  │  │  │  ├─ dump_data_collector_with_spl_array.phpt
│        │  │  │  │  ├─ dump_without_args.phpt
│        │  │  │  │  ├─ dump_with_multiple_args.phpt
│        │  │  │  │  ├─ dump_with_named_args.phpt
│        │  │  │  │  ├─ dump_with_null.phpt
│        │  │  │  │  └─ dump_with_single_arg.phpt
│        │  │  │  ├─ FunctionsTest.php
│        │  │  │  ├─ HtmlDumperTest.php
│        │  │  │  └─ ServerDumperTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ BackedEnumFixture.php
│        │  │  │  ├─ DateTimeChild.php
│        │  │  │  ├─ dumb-var.php
│        │  │  │  ├─ dump_server.php
│        │  │  │  ├─ ExtendsReflectionTypeFixture.php
│        │  │  │  ├─ FooInterface.php
│        │  │  │  ├─ GeneratorDemo.php
│        │  │  │  ├─ LotsOfAttributes.php
│        │  │  │  ├─ MyAttribute.php
│        │  │  │  ├─ NotLoadableClass.php
│        │  │  │  ├─ Php74.php
│        │  │  │  ├─ Php81Enums.php
│        │  │  │  ├─ Php82NullStandaloneReturnType.php
│        │  │  │  ├─ ReflectionIntersectionTypeFixture.php
│        │  │  │  ├─ ReflectionNamedTypeFixture.php
│        │  │  │  ├─ ReflectionUnionTypeFixture.php
│        │  │  │  ├─ ReflectionUnionTypeWithIntersectionFixture.php
│        │  │  │  ├─ Twig.php
│        │  │  │  ├─ UnitEnumFixture.php
│        │  │  │  ├─ VirtualProperty.php
│        │  │  │  └─ xml_reader.xml
│        │  │  ├─ Server
│        │  │  │  └─ ConnectionTest.php
│        │  │  └─ Test
│        │  │     └─ VarDumperTestTraitTest.php
│        │  └─ VarDumper.php
│        ├─ var-exporter
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ Exception
│        │  │  ├─ ClassNotFoundException.php
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ LogicException.php
│        │  │  └─ NotInstantiableTypeException.php
│        │  ├─ Hydrator.php
│        │  ├─ Instantiator.php
│        │  ├─ Internal
│        │  │  ├─ Exporter.php
│        │  │  ├─ Hydrator.php
│        │  │  ├─ LazyDecoratorTrait.php
│        │  │  ├─ LazyObjectRegistry.php
│        │  │  ├─ LazyObjectState.php
│        │  │  ├─ LazyObjectTrait.php
│        │  │  ├─ Reference.php
│        │  │  ├─ Registry.php
│        │  │  └─ Values.php
│        │  ├─ LazyGhostTrait.php
│        │  ├─ LazyObjectInterface.php
│        │  ├─ LazyProxyTrait.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ ProxyHelper.php
│        │  ├─ README.md
│        │  ├─ Tests
│        │  │  ├─ Fixtures
│        │  │  │  ├─ abstract-parent.php
│        │  │  │  ├─ array-iterator.php
│        │  │  │  ├─ array-object-custom.php
│        │  │  │  ├─ array-object.php
│        │  │  │  ├─ backed-property.php
│        │  │  │  ├─ BackedProperty.php
│        │  │  │  ├─ bool.php
│        │  │  │  ├─ clone.php
│        │  │  │  ├─ datetime.php
│        │  │  │  ├─ error.php
│        │  │  │  ├─ external-references.php
│        │  │  │  ├─ final-array-iterator.php
│        │  │  │  ├─ final-error.php
│        │  │  │  ├─ final-stdclass.php
│        │  │  │  ├─ foo-serializable.php
│        │  │  │  ├─ FooReadonly.php
│        │  │  │  ├─ FooSerializable.php
│        │  │  │  ├─ FooUnitEnum.php
│        │  │  │  ├─ hard-references-recursive.php
│        │  │  │  ├─ hard-references.php
│        │  │  │  ├─ incomplete-class.php
│        │  │  │  ├─ LazyGhost
│        │  │  │  │  ├─ ChildMagicClass.php
│        │  │  │  │  ├─ ChildStdClass.php
│        │  │  │  │  ├─ ChildTestClass.php
│        │  │  │  │  ├─ ClassWithUninitializedObjectProperty.php
│        │  │  │  │  ├─ LazyClass.php
│        │  │  │  │  ├─ MagicClass.php
│        │  │  │  │  ├─ NoMagicClass.php
│        │  │  │  │  ├─ ReadOnlyClass.php
│        │  │  │  │  ├─ RegularClass.php
│        │  │  │  │  └─ TestClass.php
│        │  │  │  ├─ LazyProxy
│        │  │  │  │  ├─ AbstractHooked.php
│        │  │  │  │  ├─ AsymmetricVisibility.php
│        │  │  │  │  ├─ ConcreteReadOnlyClass.php
│        │  │  │  │  ├─ FinalPublicClass.php
│        │  │  │  │  ├─ Hooked.php
│        │  │  │  │  ├─ HookedInterface.php
│        │  │  │  │  ├─ HookedWithDefaultValue.php
│        │  │  │  │  ├─ Php82NullStandaloneReturnType.php
│        │  │  │  │  ├─ ReadOnlyClass.php
│        │  │  │  │  ├─ StringMagicGetClass.php
│        │  │  │  │  ├─ TestClass.php
│        │  │  │  │  ├─ TestOverwritePropClass.php
│        │  │  │  │  ├─ TestUnserializeClass.php
│        │  │  │  │  └─ TestWakeupClass.php
│        │  │  │  ├─ lf-ending-string.php
│        │  │  │  ├─ multiline-string.php
│        │  │  │  ├─ MySerializable.php
│        │  │  │  ├─ partially-indexed-array.php
│        │  │  │  ├─ php74-serializable.php
│        │  │  │  ├─ private-constructor.php
│        │  │  │  ├─ private.php
│        │  │  │  ├─ readonly.php
│        │  │  │  ├─ serializable.php
│        │  │  │  ├─ simple-array.php
│        │  │  │  ├─ SimpleObject.php
│        │  │  │  ├─ spl-object-storage.php
│        │  │  │  ├─ unit-enum.php
│        │  │  │  ├─ var-on-sleep.php
│        │  │  │  ├─ wakeup-refl.php
│        │  │  │  ├─ wakeup.php
│        │  │  │  ├─ __serialize-but-no-__unserialize.php
│        │  │  │  └─ __unserialize-but-no-__serialize.php
│        │  │  ├─ InstantiatorTest.php
│        │  │  ├─ LazyProxyTraitTest.php
│        │  │  ├─ LegacyLazyGhostTraitTest.php
│        │  │  ├─ LegacyLazyProxyTraitTest.php
│        │  │  ├─ LegacyProxyHelperTest.php
│        │  │  ├─ ProxyHelperTest.php
│        │  │  └─ VarExporterTest.php
│        │  └─ VarExporter.php
│        └─ yaml
│           ├─ CHANGELOG.md
│           ├─ Command
│           │  └─ LintCommand.php
│           ├─ composer.json
│           ├─ Dumper.php
│           ├─ Escaper.php
│           ├─ Exception
│           │  ├─ DumpException.php
│           │  ├─ ExceptionInterface.php
│           │  ├─ ParseException.php
│           │  └─ RuntimeException.php
│           ├─ Inline.php
│           ├─ LICENSE
│           ├─ Parser.php
│           ├─ phpunit.xml.dist
│           ├─ README.md
│           ├─ Resources
│           │  └─ bin
│           │     └─ yaml-lint
│           ├─ Tag
│           │  └─ TaggedValue.php
│           ├─ Tests
│           │  ├─ Command
│           │  │  └─ LintCommandTest.php
│           │  ├─ DumperTest.php
│           │  ├─ Fixtures
│           │  │  ├─ arrow.gif
│           │  │  ├─ booleanMappingKeys.yml
│           │  │  ├─ embededPhp.yml
│           │  │  ├─ escapedCharacters.yml
│           │  │  ├─ FooBackedEnum.php
│           │  │  ├─ FooUnitEnum.php
│           │  │  ├─ index.yml
│           │  │  ├─ nonStringKeys.yml
│           │  │  ├─ not_readable.yml
│           │  │  ├─ nullMappingKey.yml
│           │  │  ├─ numericMappingKeys.yml
│           │  │  ├─ sfComments.yml
│           │  │  ├─ sfCompact.yml
│           │  │  ├─ sfMergeKey.yml
│           │  │  ├─ sfObjects.yml
│           │  │  ├─ sfQuotes.yml
│           │  │  ├─ sfTests.yml
│           │  │  ├─ unindentedCollections.yml
│           │  │  ├─ YtsAnchorAlias.yml
│           │  │  ├─ YtsBasicTests.yml
│           │  │  ├─ YtsBlockMapping.yml
│           │  │  ├─ YtsDocumentSeparator.yml
│           │  │  ├─ YtsErrorTests.yml
│           │  │  ├─ YtsFlowCollections.yml
│           │  │  ├─ YtsFoldedScalars.yml
│           │  │  ├─ YtsNullsAndEmpties.yml
│           │  │  ├─ YtsSpecificationExamples.yml
│           │  │  └─ YtsTypeTransfers.yml
│           │  ├─ InlineTest.php
│           │  ├─ ParseExceptionTest.php
│           │  ├─ ParserTest.php
│           │  └─ YamlTest.php
│           ├─ Unescaper.php
│           └─ Yaml.php
├─ docker-compose.dev.yml
├─ docs
├─ frontend
│  ├─ .editorconfig
│  ├─ .prettierrc.json
│  ├─ Dockerfile.dev
│  ├─ env.d.ts
│  ├─ eslint.config.ts
│  ├─ index.html
│  ├─ package-lock.json
│  ├─ package.json
│  ├─ playwright.config.ts
│  ├─ public
│  │  └─ favicon.ico
│  ├─ README.md
│  ├─ src
│  │  ├─ App.vue
│  │  ├─ assets
│  │  │  ├─ base.css
│  │  │  ├─ logo.svg
│  │  │  └─ main.css
│  │  ├─ components
│  │  │  ├─ HelloWorld.vue
│  │  │  ├─ icons
│  │  │  │  ├─ IconCommunity.vue
│  │  │  │  ├─ IconDocumentation.vue
│  │  │  │  ├─ IconEcosystem.vue
│  │  │  │  ├─ IconSupport.vue
│  │  │  │  └─ IconTooling.vue
│  │  │  ├─ TheWelcome.vue
│  │  │  ├─ WelcomeItem.vue
│  │  │  └─ __tests__
│  │  │     └─ HelloWorld.spec.ts
│  │  ├─ main.ts
│  │  ├─ router
│  │  │  └─ index.ts
│  │  ├─ stores
│  │  │  └─ counter.ts
│  │  └─ views
│  │     ├─ AboutView.vue
│  │     └─ HomeView.vue
│  ├─ tests
│  │  ├─ auth
│  │  │  └─ user.json
│  │  ├─ e2e
│  │  │  ├─ auth.spec.ts
│  │  │  ├─ clients.spec.ts
│  │  │  ├─ dashboard.spec.ts
│  │  │  ├─ invoicing.spec.ts
│  │  │  ├─ subscriptions.spec.ts
│  │  │  ├─ tsconfig.json
│  │  │  ├─ urssaf.spec.ts
│  │  │  └─ vue.spec.ts
│  │  ├─ fixtures
│  │  │  └─ test-data.json
│  │  └─ utils
│  │     └─ helpers.ts
│  ├─ tsconfig.app.json
│  ├─ tsconfig.json
│  ├─ tsconfig.node.json
│  ├─ tsconfig.vitest.json
│  ├─ vite.config.ts
│  └─ vitest.config.ts
├─ infrastructure
├─ LICENSE
└─ README.md

```
```
Autoflow
├─ backend
│  ├─ .editorconfig
│  ├─ .env
│  ├─ .env.dev
│  ├─ bin
│  │  └─ console
│  ├─ composer.json
│  ├─ composer.lock
│  ├─ config
│  │  ├─ bundles.php
│  │  ├─ packages
│  │  │  ├─ cache.yaml
│  │  │  ├─ framework.yaml
│  │  │  └─ routing.yaml
│  │  ├─ preload.php
│  │  ├─ routes
│  │  │  └─ framework.yaml
│  │  ├─ routes.yaml
│  │  └─ services.yaml
│  ├─ Dockerfile.dev
│  ├─ public
│  │  └─ index.php
│  ├─ src
│  │  ├─ Controller
│  │  └─ Kernel.php
│  ├─ symfony.lock
│  ├─ var
│  │  └─ cache
│  │     └─ dev
│  │        ├─ App_KernelDevDebugContainer.php
│  │        ├─ App_KernelDevDebugContainer.php.lock
│  │        ├─ App_KernelDevDebugContainer.php.meta
│  │        ├─ App_KernelDevDebugContainer.php.meta.json
│  │        ├─ App_KernelDevDebugContainer.preload.php
│  │        ├─ App_KernelDevDebugContainer.xml
│  │        ├─ App_KernelDevDebugContainer.xml.meta
│  │        ├─ App_KernelDevDebugContainer.xml.meta.json
│  │        ├─ App_KernelDevDebugContainerCompiler.log
│  │        ├─ App_KernelDevDebugContainerDeprecations.log
│  │        ├─ ContainerZYAsdwH
│  │        │  ├─ App_KernelDevDebugContainer.php
│  │        │  ├─ getArgumentResolver_BackedEnumResolverService.php
│  │        │  ├─ getArgumentResolver_DatetimeService.php
│  │        │  ├─ getArgumentResolver_DefaultService.php
│  │        │  ├─ getArgumentResolver_QueryParameterValueResolverService.php
│  │        │  ├─ getArgumentResolver_RequestAttributeService.php
│  │        │  ├─ getArgumentResolver_RequestPayloadService.php
│  │        │  ├─ getArgumentResolver_RequestService.php
│  │        │  ├─ getArgumentResolver_ServiceService.php
│  │        │  ├─ getArgumentResolver_SessionService.php
│  │        │  ├─ getArgumentResolver_VariadicService.php
│  │        │  ├─ getCacheWarmerService.php
│  │        │  ├─ getCache_AppClearerService.php
│  │        │  ├─ getCache_AppService.php
│  │        │  ├─ getCache_App_TaggableService.php
│  │        │  ├─ getCache_GlobalClearerService.php
│  │        │  ├─ getCache_SystemClearerService.php
│  │        │  ├─ getCache_SystemService.php
│  │        │  ├─ getConfigBuilder_WarmerService.php
│  │        │  ├─ getConsole_CommandLoaderService.php
│  │        │  ├─ getConsole_Command_AboutService.php
│  │        │  ├─ getConsole_Command_AssetsInstallService.php
│  │        │  ├─ getConsole_Command_CacheClearService.php
│  │        │  ├─ getConsole_Command_CachePoolClearService.php
│  │        │  ├─ getConsole_Command_CachePoolDeleteService.php
│  │        │  ├─ getConsole_Command_CachePoolInvalidateTagsService.php
│  │        │  ├─ getConsole_Command_CachePoolListService.php
│  │        │  ├─ getConsole_Command_CachePoolPruneService.php
│  │        │  ├─ getConsole_Command_CacheWarmupService.php
│  │        │  ├─ getConsole_Command_ConfigDebugService.php
│  │        │  ├─ getConsole_Command_ConfigDumpReferenceService.php
│  │        │  ├─ getConsole_Command_ContainerDebugService.php
│  │        │  ├─ getConsole_Command_ContainerLintService.php
│  │        │  ├─ getConsole_Command_DebugAutowiringService.php
│  │        │  ├─ getConsole_Command_DotenvDebugService.php
│  │        │  ├─ getConsole_Command_ErrorDumperService.php
│  │        │  ├─ getConsole_Command_EventDispatcherDebugService.php
│  │        │  ├─ getConsole_Command_RouterDebugService.php
│  │        │  ├─ getConsole_Command_RouterMatchService.php
│  │        │  ├─ getConsole_Command_SecretsDecryptToLocalService.php
│  │        │  ├─ getConsole_Command_SecretsEncryptFromLocalService.php
│  │        │  ├─ getConsole_Command_SecretsGenerateKeyService.php
│  │        │  ├─ getConsole_Command_SecretsListService.php
│  │        │  ├─ getConsole_Command_SecretsRemoveService.php
│  │        │  ├─ getConsole_Command_SecretsRevealService.php
│  │        │  ├─ getConsole_Command_SecretsSetService.php
│  │        │  ├─ getConsole_Command_YamlLintService.php
│  │        │  ├─ getConsole_ErrorListenerService.php
│  │        │  ├─ getContainer_EnvVarProcessorService.php
│  │        │  ├─ getContainer_EnvVarProcessorsLocatorService.php
│  │        │  ├─ getContainer_GetRoutingConditionServiceService.php
│  │        │  ├─ getDebug_ErrorHandlerConfiguratorService.php
│  │        │  ├─ getErrorControllerService.php
│  │        │  ├─ getErrorHandler_ErrorRenderer_HtmlService.php
│  │        │  ├─ getLoaderInterfaceService.php
│  │        │  ├─ getRedirectControllerService.php
│  │        │  ├─ getRouter_CacheWarmerService.php
│  │        │  ├─ getRouting_LoaderService.php
│  │        │  ├─ getSecrets_EnvVarLoaderService.php
│  │        │  ├─ getSecrets_VaultService.php
│  │        │  ├─ getServicesResetterService.php
│  │        │  ├─ getSession_FactoryService.php
│  │        │  ├─ getTemplateControllerService.php
│  │        │  ├─ get_Console_Command_About_LazyService.php
│  │        │  ├─ get_Console_Command_AssetsInstall_LazyService.php
│  │        │  ├─ get_Console_Command_CacheClear_LazyService.php
│  │        │  ├─ get_Console_Command_CachePoolClear_LazyService.php
│  │        │  ├─ get_Console_Command_CachePoolDelete_LazyService.php
│  │        │  ├─ get_Console_Command_CachePoolInvalidateTags_LazyService.php
│  │        │  ├─ get_Console_Command_CachePoolList_LazyService.php
│  │        │  ├─ get_Console_Command_CachePoolPrune_LazyService.php
│  │        │  ├─ get_Console_Command_CacheWarmup_LazyService.php
│  │        │  ├─ get_Console_Command_ConfigDebug_LazyService.php
│  │        │  ├─ get_Console_Command_ConfigDumpReference_LazyService.php
│  │        │  ├─ get_Console_Command_ContainerDebug_LazyService.php
│  │        │  ├─ get_Console_Command_ContainerLint_LazyService.php
│  │        │  ├─ get_Console_Command_DebugAutowiring_LazyService.php
│  │        │  ├─ get_Console_Command_DotenvDebug_LazyService.php
│  │        │  ├─ get_Console_Command_ErrorDumper_LazyService.php
│  │        │  ├─ get_Console_Command_EventDispatcherDebug_LazyService.php
│  │        │  ├─ get_Console_Command_RouterDebug_LazyService.php
│  │        │  ├─ get_Console_Command_RouterMatch_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsDecryptToLocal_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsEncryptFromLocal_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsGenerateKey_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsList_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsRemove_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsReveal_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsSet_LazyService.php
│  │        │  ├─ get_Console_Command_YamlLint_LazyService.php
│  │        │  ├─ get_ServiceLocator_ZHyJIs5Service.php
│  │        │  ├─ get_ServiceLocator_ZHyJIs5_KernelloadRoutesService.php
│  │        │  ├─ get_ServiceLocator_ZHyJIs5_KernelregisterContainerConfigurationService.php
│  │        │  ├─ removed-ids.php
│  │        │  └─ RequestPayloadValueResolverGhost01ca9cc.php
│  │        ├─ Symfony
│  │        │  └─ Config
│  │        │     ├─ Framework
│  │        │     │  ├─ AnnotationsConfig.php
│  │        │     │  ├─ AssetMapper
│  │        │     │  │  └─ PrecompressConfig.php
│  │        │     │  ├─ AssetMapperConfig.php
│  │        │     │  ├─ Assets
│  │        │     │  │  └─ PackageConfig.php
│  │        │     │  ├─ AssetsConfig.php
│  │        │     │  ├─ Cache
│  │        │     │  │  └─ PoolConfig.php
│  │        │     │  ├─ CacheConfig.php
│  │        │     │  ├─ CsrfProtectionConfig.php
│  │        │     │  ├─ EsiConfig.php
│  │        │     │  ├─ ExceptionConfig.php
│  │        │     │  ├─ Form
│  │        │     │  │  └─ CsrfProtectionConfig.php
│  │        │     │  ├─ FormConfig.php
│  │        │     │  ├─ FragmentsConfig.php
│  │        │     │  ├─ HtmlSanitizer
│  │        │     │  │  └─ SanitizerConfig.php
│  │        │     │  ├─ HtmlSanitizerConfig.php
│  │        │     │  ├─ HttpCacheConfig.php
│  │        │     │  ├─ HttpClient
│  │        │     │  │  ├─ DefaultOptions
│  │        │     │  │  │  ├─ PeerFingerprintConfig.php
│  │        │     │  │  │  ├─ RetryFailed
│  │        │     │  │  │  │  └─ HttpCodeConfig.php
│  │        │     │  │  │  └─ RetryFailedConfig.php
│  │        │     │  │  ├─ DefaultOptionsConfig.php
│  │        │     │  │  ├─ ScopedClientConfig
│  │        │     │  │  │  ├─ PeerFingerprintConfig.php
│  │        │     │  │  │  ├─ RetryFailed
│  │        │     │  │  │  │  └─ HttpCodeConfig.php
│  │        │     │  │  │  └─ RetryFailedConfig.php
│  │        │     │  │  └─ ScopedClientConfig.php
│  │        │     │  ├─ HttpClientConfig.php
│  │        │     │  ├─ JsonStreamerConfig.php
│  │        │     │  ├─ LockConfig.php
│  │        │     │  ├─ Mailer
│  │        │     │  │  ├─ DkimSignerConfig.php
│  │        │     │  │  ├─ EnvelopeConfig.php
│  │        │     │  │  ├─ HeaderConfig.php
│  │        │     │  │  ├─ SmimeEncrypterConfig.php
│  │        │     │  │  └─ SmimeSignerConfig.php
│  │        │     │  ├─ MailerConfig.php
│  │        │     │  ├─ Messenger
│  │        │     │  │  ├─ BusConfig
│  │        │     │  │  │  ├─ DefaultMiddlewareConfig.php
│  │        │     │  │  │  └─ MiddlewareConfig.php
│  │        │     │  │  ├─ BusConfig.php
│  │        │     │  │  ├─ RoutingConfig.php
│  │        │     │  │  ├─ Serializer
│  │        │     │  │  │  └─ SymfonySerializerConfig.php
│  │        │     │  │  ├─ SerializerConfig.php
│  │        │     │  │  ├─ TransportConfig
│  │        │     │  │  │  └─ RetryStrategyConfig.php
│  │        │     │  │  └─ TransportConfig.php
│  │        │     │  ├─ MessengerConfig.php
│  │        │     │  ├─ Notifier
│  │        │     │  │  └─ AdminRecipientConfig.php
│  │        │     │  ├─ NotifierConfig.php
│  │        │     │  ├─ PhpErrorsConfig.php
│  │        │     │  ├─ ProfilerConfig.php
│  │        │     │  ├─ PropertyAccessConfig.php
│  │        │     │  ├─ PropertyInfoConfig.php
│  │        │     │  ├─ RateLimiter
│  │        │     │  │  ├─ LimiterConfig
│  │        │     │  │  │  └─ RateConfig.php
│  │        │     │  │  └─ LimiterConfig.php
│  │        │     │  ├─ RateLimiterConfig.php
│  │        │     │  ├─ RemoteeventConfig.php
│  │        │     │  ├─ RequestConfig.php
│  │        │     │  ├─ RouterConfig.php
│  │        │     │  ├─ SchedulerConfig.php
│  │        │     │  ├─ SecretsConfig.php
│  │        │     │  ├─ SemaphoreConfig.php
│  │        │     │  ├─ Serializer
│  │        │     │  │  ├─ MappingConfig.php
│  │        │     │  │  └─ NamedSerializerConfig.php
│  │        │     │  ├─ SerializerConfig.php
│  │        │     │  ├─ SessionConfig.php
│  │        │     │  ├─ SsiConfig.php
│  │        │     │  ├─ Translator
│  │        │     │  │  ├─ GlobalConfig.php
│  │        │     │  │  ├─ ProviderConfig.php
│  │        │     │  │  └─ PseudoLocalizationConfig.php
│  │        │     │  ├─ TranslatorConfig.php
│  │        │     │  ├─ TypeInfoConfig.php
│  │        │     │  ├─ UidConfig.php
│  │        │     │  ├─ Validation
│  │        │     │  │  ├─ AutoMappingConfig.php
│  │        │     │  │  ├─ MappingConfig.php
│  │        │     │  │  └─ NotCompromisedPasswordConfig.php
│  │        │     │  ├─ ValidationConfig.php
│  │        │     │  ├─ Webhook
│  │        │     │  │  └─ RoutingConfig.php
│  │        │     │  ├─ WebhookConfig.php
│  │        │     │  ├─ WebLinkConfig.php
│  │        │     │  ├─ Workflows
│  │        │     │  │  ├─ WorkflowsConfig
│  │        │     │  │  │  ├─ AuditTrailConfig.php
│  │        │     │  │  │  ├─ MarkingStoreConfig.php
│  │        │     │  │  │  ├─ PlaceConfig.php
│  │        │     │  │  │  └─ TransitionConfig.php
│  │        │     │  │  └─ WorkflowsConfig.php
│  │        │     │  └─ WorkflowsConfig.php
│  │        │     └─ FrameworkConfig.php
│  │        ├─ url_generating_routes.php
│  │        ├─ url_generating_routes.php.meta
│  │        ├─ url_generating_routes.php.meta.json
│  │        ├─ url_matching_routes.php
│  │        ├─ url_matching_routes.php.meta
│  │        └─ url_matching_routes.php.meta.json
│  └─ vendor
│     ├─ autoload.php
│     ├─ autoload_runtime.php
│     ├─ bin
│     │  ├─ patch-type-declarations
│     │  ├─ patch-type-declarations.bat
│     │  ├─ var-dump-server
│     │  ├─ var-dump-server.bat
│     │  ├─ yaml-lint
│     │  └─ yaml-lint.bat
│     ├─ composer
│     │  ├─ autoload_classmap.php
│     │  ├─ autoload_files.php
│     │  ├─ autoload_namespaces.php
│     │  ├─ autoload_psr4.php
│     │  ├─ autoload_real.php
│     │  ├─ autoload_static.php
│     │  ├─ ClassLoader.php
│     │  ├─ installed.json
│     │  ├─ installed.php
│     │  ├─ InstalledVersions.php
│     │  ├─ LICENSE
│     │  └─ platform_check.php
│     ├─ psr
│     │  ├─ cache
│     │  │  ├─ CHANGELOG.md
│     │  │  ├─ composer.json
│     │  │  ├─ LICENSE.txt
│     │  │  ├─ README.md
│     │  │  └─ src
│     │  │     ├─ CacheException.php
│     │  │     ├─ CacheItemInterface.php
│     │  │     ├─ CacheItemPoolInterface.php
│     │  │     └─ InvalidArgumentException.php
│     │  ├─ container
│     │  │  ├─ composer.json
│     │  │  ├─ LICENSE
│     │  │  ├─ README.md
│     │  │  └─ src
│     │  │     ├─ ContainerExceptionInterface.php
│     │  │     ├─ ContainerInterface.php
│     │  │     └─ NotFoundExceptionInterface.php
│     │  ├─ event-dispatcher
│     │  │  ├─ .editorconfig
│     │  │  ├─ composer.json
│     │  │  ├─ LICENSE
│     │  │  ├─ README.md
│     │  │  └─ src
│     │  │     ├─ EventDispatcherInterface.php
│     │  │     ├─ ListenerProviderInterface.php
│     │  │     └─ StoppableEventInterface.php
│     │  └─ log
│     │     ├─ composer.json
│     │     ├─ LICENSE
│     │     ├─ README.md
│     │     └─ src
│     │        ├─ AbstractLogger.php
│     │        ├─ InvalidArgumentException.php
│     │        ├─ LoggerAwareInterface.php
│     │        ├─ LoggerAwareTrait.php
│     │        ├─ LoggerInterface.php
│     │        ├─ LoggerTrait.php
│     │        ├─ LogLevel.php
│     │        └─ NullLogger.php
│     └─ symfony
│        ├─ cache
│        │  ├─ Adapter
│        │  │  ├─ AbstractAdapter.php
│        │  │  ├─ AbstractTagAwareAdapter.php
│        │  │  ├─ AdapterInterface.php
│        │  │  ├─ ApcuAdapter.php
│        │  │  ├─ ArrayAdapter.php
│        │  │  ├─ ChainAdapter.php
│        │  │  ├─ CouchbaseBucketAdapter.php
│        │  │  ├─ CouchbaseCollectionAdapter.php
│        │  │  ├─ DoctrineDbalAdapter.php
│        │  │  ├─ FilesystemAdapter.php
│        │  │  ├─ FilesystemTagAwareAdapter.php
│        │  │  ├─ MemcachedAdapter.php
│        │  │  ├─ NullAdapter.php
│        │  │  ├─ ParameterNormalizer.php
│        │  │  ├─ PdoAdapter.php
│        │  │  ├─ PhpArrayAdapter.php
│        │  │  ├─ PhpFilesAdapter.php
│        │  │  ├─ ProxyAdapter.php
│        │  │  ├─ Psr16Adapter.php
│        │  │  ├─ RedisAdapter.php
│        │  │  ├─ RedisTagAwareAdapter.php
│        │  │  ├─ TagAwareAdapter.php
│        │  │  ├─ TagAwareAdapterInterface.php
│        │  │  ├─ TraceableAdapter.php
│        │  │  └─ TraceableTagAwareAdapter.php
│        │  ├─ CacheItem.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ DataCollector
│        │  │  └─ CacheDataCollector.php
│        │  ├─ DependencyInjection
│        │  │  ├─ CacheCollectorPass.php
│        │  │  ├─ CachePoolClearerPass.php
│        │  │  ├─ CachePoolPass.php
│        │  │  └─ CachePoolPrunerPass.php
│        │  ├─ Exception
│        │  │  ├─ BadMethodCallException.php
│        │  │  ├─ CacheException.php
│        │  │  ├─ InvalidArgumentException.php
│        │  │  └─ LogicException.php
│        │  ├─ LICENSE
│        │  ├─ LockRegistry.php
│        │  ├─ Marshaller
│        │  │  ├─ DefaultMarshaller.php
│        │  │  ├─ DeflateMarshaller.php
│        │  │  ├─ MarshallerInterface.php
│        │  │  ├─ SodiumMarshaller.php
│        │  │  └─ TagAwareMarshaller.php
│        │  ├─ Messenger
│        │  │  ├─ EarlyExpirationDispatcher.php
│        │  │  ├─ EarlyExpirationHandler.php
│        │  │  └─ EarlyExpirationMessage.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ PruneableInterface.php
│        │  ├─ Psr16Cache.php
│        │  ├─ README.md
│        │  ├─ ResettableInterface.php
│        │  ├─ Tests
│        │  │  ├─ Adapter
│        │  │  │  ├─ AbstractRedisAdapterTestCase.php
│        │  │  │  ├─ AdapterTestCase.php
│        │  │  │  ├─ ApcuAdapterTest.php
│        │  │  │  ├─ ArrayAdapterTest.php
│        │  │  │  ├─ ChainAdapterTest.php
│        │  │  │  ├─ CouchbaseBucketAdapterTest.php
│        │  │  │  ├─ CouchbaseCollectionAdapterTest.php
│        │  │  │  ├─ DoctrineDbalAdapterTest.php
│        │  │  │  ├─ FilesystemAdapterTest.php
│        │  │  │  ├─ FilesystemTagAwareAdapterTest.php
│        │  │  │  ├─ MaxIdLengthAdapterTest.php
│        │  │  │  ├─ MemcachedAdapterTest.php
│        │  │  │  ├─ NamespacedProxyAdapterTest.php
│        │  │  │  ├─ NullAdapterTest.php
│        │  │  │  ├─ PdoAdapterTest.php
│        │  │  │  ├─ PhpArrayAdapterTest.php
│        │  │  │  ├─ PhpArrayAdapterWithFallbackTest.php
│        │  │  │  ├─ PhpFilesAdapterAppendOnlyTest.php
│        │  │  │  ├─ PhpFilesAdapterTest.php
│        │  │  │  ├─ PredisAdapterSentinelTest.php
│        │  │  │  ├─ PredisAdapterTest.php
│        │  │  │  ├─ PredisClusterAdapterTest.php
│        │  │  │  ├─ PredisRedisClusterAdapterTest.php
│        │  │  │  ├─ PredisRedisReplicationAdapterTest.php
│        │  │  │  ├─ PredisReplicationAdapterTest.php
│        │  │  │  ├─ PredisTagAwareAdapterTest.php
│        │  │  │  ├─ PredisTagAwareClusterAdapterTest.php
│        │  │  │  ├─ ProxyAdapterAndRedisAdapterTest.php
│        │  │  │  ├─ ProxyAdapterTest.php
│        │  │  │  ├─ Psr16AdapterTest.php
│        │  │  │  ├─ RedisAdapterSentinelTest.php
│        │  │  │  ├─ RedisAdapterTest.php
│        │  │  │  ├─ RedisArrayAdapterTest.php
│        │  │  │  ├─ RedisClusterAdapterTest.php
│        │  │  │  ├─ RedisTagAwareAdapterTest.php
│        │  │  │  ├─ RedisTagAwareArrayAdapterTest.php
│        │  │  │  ├─ RedisTagAwareClusterAdapterTest.php
│        │  │  │  ├─ RedisTagAwareRelayClusterAdapterTest.php
│        │  │  │  ├─ RelayAdapterSentinelTest.php
│        │  │  │  ├─ RelayAdapterTest.php
│        │  │  │  ├─ RelayClusterAdapterTest.php
│        │  │  │  ├─ TagAwareAdapterTest.php
│        │  │  │  ├─ TagAwareAndProxyAdapterIntegrationTest.php
│        │  │  │  ├─ TagAwareTestTrait.php
│        │  │  │  ├─ TraceableAdapterTest.php
│        │  │  │  └─ TraceableTagAwareAdapterTest.php
│        │  │  ├─ CacheItemTest.php
│        │  │  ├─ DataCollector
│        │  │  │  └─ CacheDataCollectorTest.php
│        │  │  ├─ DependencyInjection
│        │  │  │  ├─ CacheCollectorPassTest.php
│        │  │  │  ├─ CachePoolClearerPassTest.php
│        │  │  │  ├─ CachePoolPassTest.php
│        │  │  │  └─ CachePoolPrunerPassTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ ExternalAdapter.php
│        │  │  │  ├─ PrunableAdapter.php
│        │  │  │  ├─ StringableTag.php
│        │  │  │  └─ TestEnum.php
│        │  │  ├─ LockRegistryTest.php
│        │  │  ├─ Marshaller
│        │  │  │  ├─ DefaultMarshallerTest.php
│        │  │  │  ├─ DeflateMarshallerTest.php
│        │  │  │  └─ SodiumMarshallerTest.php
│        │  │  ├─ Messenger
│        │  │  │  ├─ EarlyExpirationDispatcherTest.php
│        │  │  │  ├─ EarlyExpirationHandlerTest.php
│        │  │  │  └─ EarlyExpirationMessageTest.php
│        │  │  ├─ Psr16CacheProxyTest.php
│        │  │  ├─ Psr16CacheTest.php
│        │  │  ├─ Psr16CacheWithExternalAdapter.php
│        │  │  └─ Traits
│        │  │     ├─ RedisProxiesTest.php
│        │  │     └─ RedisTraitTest.php
│        │  └─ Traits
│        │     ├─ AbstractAdapterTrait.php
│        │     ├─ ContractsTrait.php
│        │     ├─ FilesystemCommonTrait.php
│        │     ├─ FilesystemTrait.php
│        │     ├─ ProxyTrait.php
│        │     ├─ Redis5Proxy.php
│        │     ├─ Redis6Proxy.php
│        │     ├─ Redis6ProxyTrait.php
│        │     ├─ RedisCluster5Proxy.php
│        │     ├─ RedisCluster6Proxy.php
│        │     ├─ RedisCluster6ProxyTrait.php
│        │     ├─ RedisClusterNodeProxy.php
│        │     ├─ RedisClusterProxy.php
│        │     ├─ RedisProxy.php
│        │     ├─ RedisProxyTrait.php
│        │     ├─ RedisTrait.php
│        │     ├─ Relay
│        │     │  ├─ CopyTrait.php
│        │     │  ├─ GeosearchTrait.php
│        │     │  ├─ GetrangeTrait.php
│        │     │  ├─ HsetTrait.php
│        │     │  ├─ MoveTrait.php
│        │     │  ├─ NullableReturnTrait.php
│        │     │  └─ PfcountTrait.php
│        │     ├─ RelayClusterProxy.php
│        │     ├─ RelayProxy.php
│        │     ├─ RelayProxyTrait.php
│        │     └─ ValueWrapper.php
│        ├─ cache-contracts
│        │  ├─ CacheInterface.php
│        │  ├─ CacheTrait.php
│        │  ├─ CallbackInterface.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ ItemInterface.php
│        │  ├─ LICENSE
│        │  ├─ NamespacedPoolInterface.php
│        │  ├─ README.md
│        │  └─ TagAwareCacheInterface.php
│        ├─ config
│        │  ├─ Builder
│        │  │  ├─ ClassBuilder.php
│        │  │  ├─ ConfigBuilderGenerator.php
│        │  │  ├─ ConfigBuilderGeneratorInterface.php
│        │  │  ├─ ConfigBuilderInterface.php
│        │  │  ├─ Method.php
│        │  │  └─ Property.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ ConfigCache.php
│        │  ├─ ConfigCacheFactory.php
│        │  ├─ ConfigCacheFactoryInterface.php
│        │  ├─ ConfigCacheInterface.php
│        │  ├─ Definition
│        │  │  ├─ ArrayNode.php
│        │  │  ├─ BaseNode.php
│        │  │  ├─ BooleanNode.php
│        │  │  ├─ Builder
│        │  │  │  ├─ ArrayNodeDefinition.php
│        │  │  │  ├─ BooleanNodeDefinition.php
│        │  │  │  ├─ BuilderAwareInterface.php
│        │  │  │  ├─ EnumNodeDefinition.php
│        │  │  │  ├─ ExprBuilder.php
│        │  │  │  ├─ FloatNodeDefinition.php
│        │  │  │  ├─ IntegerNodeDefinition.php
│        │  │  │  ├─ MergeBuilder.php
│        │  │  │  ├─ NodeBuilder.php
│        │  │  │  ├─ NodeDefinition.php
│        │  │  │  ├─ NodeParentInterface.php
│        │  │  │  ├─ NormalizationBuilder.php
│        │  │  │  ├─ NumericNodeDefinition.php
│        │  │  │  ├─ ParentNodeDefinitionInterface.php
│        │  │  │  ├─ ScalarNodeDefinition.php
│        │  │  │  ├─ StringNodeDefinition.php
│        │  │  │  ├─ TreeBuilder.php
│        │  │  │  ├─ ValidationBuilder.php
│        │  │  │  └─ VariableNodeDefinition.php
│        │  │  ├─ ConfigurableInterface.php
│        │  │  ├─ Configuration.php
│        │  │  ├─ ConfigurationInterface.php
│        │  │  ├─ Configurator
│        │  │  │  └─ DefinitionConfigurator.php
│        │  │  ├─ Dumper
│        │  │  │  ├─ XmlReferenceDumper.php
│        │  │  │  └─ YamlReferenceDumper.php
│        │  │  ├─ EnumNode.php
│        │  │  ├─ Exception
│        │  │  │  ├─ DuplicateKeyException.php
│        │  │  │  ├─ Exception.php
│        │  │  │  ├─ ForbiddenOverwriteException.php
│        │  │  │  ├─ InvalidConfigurationException.php
│        │  │  │  ├─ InvalidDefinitionException.php
│        │  │  │  ├─ InvalidTypeException.php
│        │  │  │  └─ UnsetKeyException.php
│        │  │  ├─ FloatNode.php
│        │  │  ├─ IntegerNode.php
│        │  │  ├─ Loader
│        │  │  │  └─ DefinitionFileLoader.php
│        │  │  ├─ NodeInterface.php
│        │  │  ├─ NumericNode.php
│        │  │  ├─ Processor.php
│        │  │  ├─ PrototypedArrayNode.php
│        │  │  ├─ PrototypeNodeInterface.php
│        │  │  ├─ ScalarNode.php
│        │  │  ├─ StringNode.php
│        │  │  └─ VariableNode.php
│        │  ├─ Exception
│        │  │  ├─ FileLoaderImportCircularReferenceException.php
│        │  │  ├─ FileLocatorFileNotFoundException.php
│        │  │  ├─ LoaderLoadException.php
│        │  │  └─ LogicException.php
│        │  ├─ FileLocator.php
│        │  ├─ FileLocatorInterface.php
│        │  ├─ LICENSE
│        │  ├─ Loader
│        │  │  ├─ DelegatingLoader.php
│        │  │  ├─ DirectoryAwareLoaderInterface.php
│        │  │  ├─ FileLoader.php
│        │  │  ├─ GlobFileLoader.php
│        │  │  ├─ Loader.php
│        │  │  ├─ LoaderInterface.php
│        │  │  ├─ LoaderResolver.php
│        │  │  ├─ LoaderResolverInterface.php
│        │  │  └─ ParamConfigurator.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Resource
│        │  │  ├─ ClassExistenceResource.php
│        │  │  ├─ ComposerResource.php
│        │  │  ├─ DirectoryResource.php
│        │  │  ├─ FileExistenceResource.php
│        │  │  ├─ FileResource.php
│        │  │  ├─ GlobResource.php
│        │  │  ├─ ReflectionClassResource.php
│        │  │  ├─ ResourceInterface.php
│        │  │  ├─ SelfCheckingResourceChecker.php
│        │  │  ├─ SelfCheckingResourceInterface.php
│        │  │  └─ SkippingResourceChecker.php
│        │  ├─ ResourceCheckerConfigCache.php
│        │  ├─ ResourceCheckerConfigCacheFactory.php
│        │  ├─ ResourceCheckerInterface.php
│        │  ├─ Tests
│        │  │  ├─ Builder
│        │  │  │  ├─ Fixtures
│        │  │  │  │  ├─ AddToList
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        ├─ AddToList
│        │  │  │  │  │        │  ├─ Messenger
│        │  │  │  │  │        │  │  ├─ ReceivingConfig.php
│        │  │  │  │  │        │  │  └─ RoutingConfig.php
│        │  │  │  │  │        │  ├─ MessengerConfig.php
│        │  │  │  │  │        │  ├─ Translator
│        │  │  │  │  │        │  │  ├─ Books
│        │  │  │  │  │        │  │  │  └─ PageConfig.php
│        │  │  │  │  │        │  │  └─ BooksConfig.php
│        │  │  │  │  │        │  └─ TranslatorConfig.php
│        │  │  │  │  │        └─ AddToListConfig.php
│        │  │  │  │  ├─ AddToList.config.php
│        │  │  │  │  ├─ AddToList.output.php
│        │  │  │  │  ├─ AddToList.php
│        │  │  │  │  ├─ ArrayExtraKeys
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        ├─ ArrayExtraKeys
│        │  │  │  │  │        │  ├─ BarConfig.php
│        │  │  │  │  │        │  ├─ BazConfig.php
│        │  │  │  │  │        │  └─ FooConfig.php
│        │  │  │  │  │        └─ ArrayExtraKeysConfig.php
│        │  │  │  │  ├─ ArrayExtraKeys.config.php
│        │  │  │  │  ├─ ArrayExtraKeys.output.php
│        │  │  │  │  ├─ ArrayExtraKeys.php
│        │  │  │  │  ├─ NodeInitialValues
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        ├─ NodeInitialValues
│        │  │  │  │  │        │  ├─ Messenger
│        │  │  │  │  │        │  │  └─ TransportsConfig.php
│        │  │  │  │  │        │  ├─ MessengerConfig.php
│        │  │  │  │  │        │  └─ SomeCleverNameConfig.php
│        │  │  │  │  │        └─ NodeInitialValuesConfig.php
│        │  │  │  │  ├─ NodeInitialValues.config.php
│        │  │  │  │  ├─ NodeInitialValues.output.php
│        │  │  │  │  ├─ NodeInitialValues.php
│        │  │  │  │  ├─ Placeholders
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        └─ PlaceholdersConfig.php
│        │  │  │  │  ├─ Placeholders.config.php
│        │  │  │  │  ├─ Placeholders.output.php
│        │  │  │  │  ├─ Placeholders.php
│        │  │  │  │  ├─ PrimitiveTypes
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        └─ PrimitiveTypesConfig.php
│        │  │  │  │  ├─ PrimitiveTypes.config.php
│        │  │  │  │  ├─ PrimitiveTypes.output.php
│        │  │  │  │  ├─ PrimitiveTypes.php
│        │  │  │  │  ├─ ScalarNormalizedTypes
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        ├─ ScalarNormalizedTypes
│        │  │  │  │  │        │  ├─ KeyedListObjectConfig.php
│        │  │  │  │  │        │  ├─ ListObjectConfig.php
│        │  │  │  │  │        │  ├─ Nested
│        │  │  │  │  │        │  │  ├─ NestedListObjectConfig.php
│        │  │  │  │  │        │  │  └─ NestedObjectConfig.php
│        │  │  │  │  │        │  ├─ NestedConfig.php
│        │  │  │  │  │        │  └─ ObjectConfig.php
│        │  │  │  │  │        └─ ScalarNormalizedTypesConfig.php
│        │  │  │  │  ├─ ScalarNormalizedTypes.config.php
│        │  │  │  │  ├─ ScalarNormalizedTypes.output.php
│        │  │  │  │  ├─ ScalarNormalizedTypes.php
│        │  │  │  │  ├─ VariableType
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        └─ VariableTypeConfig.php
│        │  │  │  │  ├─ VariableType.config.php
│        │  │  │  │  ├─ VariableType.output.php
│        │  │  │  │  └─ VariableType.php
│        │  │  │  └─ GeneratedConfigTest.php
│        │  │  ├─ ConfigCacheFactoryTest.php
│        │  │  ├─ ConfigCacheTest.php
│        │  │  ├─ Definition
│        │  │  │  ├─ ArrayNodeTest.php
│        │  │  │  ├─ BaseNodeTest.php
│        │  │  │  ├─ BooleanNodeTest.php
│        │  │  │  ├─ Builder
│        │  │  │  │  ├─ ArrayNodeDefinitionTest.php
│        │  │  │  │  ├─ BooleanNodeDefinitionTest.php
│        │  │  │  │  ├─ EnumNodeDefinitionTest.php
│        │  │  │  │  ├─ ExprBuilderTest.php
│        │  │  │  │  ├─ NodeBuilderTest.php
│        │  │  │  │  ├─ NodeDefinitionTest.php
│        │  │  │  │  ├─ NumericNodeDefinitionTest.php
│        │  │  │  │  └─ TreeBuilderTest.php
│        │  │  │  ├─ Dumper
│        │  │  │  │  ├─ XmlReferenceDumperTest.php
│        │  │  │  │  └─ YamlReferenceDumperTest.php
│        │  │  │  ├─ EnumNodeTest.php
│        │  │  │  ├─ FinalizationTest.php
│        │  │  │  ├─ FloatNodeTest.php
│        │  │  │  ├─ IntegerNodeTest.php
│        │  │  │  ├─ Loader
│        │  │  │  │  └─ DefinitionFileLoaderTest.php
│        │  │  │  ├─ MergeTest.php
│        │  │  │  ├─ NormalizationTest.php
│        │  │  │  ├─ PrototypedArrayNodeTest.php
│        │  │  │  ├─ ScalarNodeTest.php
│        │  │  │  └─ StringNodeTest.php
│        │  │  ├─ Exception
│        │  │  │  └─ LoaderLoadExceptionTest.php
│        │  │  ├─ FileLocatorTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ Again
│        │  │  │  │  └─ foo.xml
│        │  │  │  ├─ BadFileName.php
│        │  │  │  ├─ BadParent.php
│        │  │  │  ├─ BarNode.php
│        │  │  │  ├─ Builder
│        │  │  │  │  ├─ BarNodeDefinition.php
│        │  │  │  │  ├─ NodeBuilder.php
│        │  │  │  │  └─ VariableNodeDefinition.php
│        │  │  │  ├─ Configuration
│        │  │  │  │  ├─ CustomNode.php
│        │  │  │  │  ├─ CustomNodeDefinition.php
│        │  │  │  │  └─ ExampleConfiguration.php
│        │  │  │  ├─ Exclude
│        │  │  │  │  ├─ AnExcludedFile.txt
│        │  │  │  │  └─ ExcludeToo
│        │  │  │  │     └─ AnotheExcludedFile.txt
│        │  │  │  ├─ ExcludeTrailingSlash
│        │  │  │  │  ├─ bar.txt
│        │  │  │  │  ├─ exclude
│        │  │  │  │  │  └─ baz.txt
│        │  │  │  │  └─ foo.txt
│        │  │  │  ├─ foo.xml
│        │  │  │  ├─ Include
│        │  │  │  │  ├─ ExcludeFile.txt
│        │  │  │  │  ├─ IncludeAnotherFile.txt
│        │  │  │  │  └─ IncludeFile.txt
│        │  │  │  ├─ IntegerBackedTestEnum.php
│        │  │  │  ├─ Loader
│        │  │  │  │  └─ node_simple.php
│        │  │  │  ├─ ParseError.php
│        │  │  │  ├─ Resource
│        │  │  │  │  ├─ .hiddenFile
│        │  │  │  │  └─ ConditionalClass.php
│        │  │  │  ├─ some.phar
│        │  │  │  ├─ StringBackedTestEnum.php
│        │  │  │  ├─ StringBackedTestEnum2.php
│        │  │  │  ├─ TestEnum.php
│        │  │  │  ├─ TestEnum2.php
│        │  │  │  └─ Util
│        │  │  │     ├─ document_type.xml
│        │  │  │     ├─ invalid.xml
│        │  │  │     ├─ invalid_schema.xml
│        │  │  │     ├─ not_readable.xml
│        │  │  │     ├─ schema.xsd
│        │  │  │     └─ valid.xml
│        │  │  ├─ Loader
│        │  │  │  ├─ DelegatingLoaderTest.php
│        │  │  │  ├─ FileLoaderTest.php
│        │  │  │  ├─ LoaderResolverTest.php
│        │  │  │  └─ LoaderTest.php
│        │  │  ├─ Resource
│        │  │  │  ├─ ClassExistenceResourceTest.php
│        │  │  │  ├─ ComposerResourceTest.php
│        │  │  │  ├─ DirectoryResourceTest.php
│        │  │  │  ├─ FileExistenceResourceTest.php
│        │  │  │  ├─ FileResourceTest.php
│        │  │  │  ├─ GlobResourceTest.php
│        │  │  │  ├─ ReflectionClassResourceTest.php
│        │  │  │  └─ ResourceStub.php
│        │  │  ├─ ResourceCheckerConfigCacheTest.php
│        │  │  └─ Util
│        │  │     └─ XmlUtilsTest.php
│        │  └─ Util
│        │     ├─ Exception
│        │     │  ├─ InvalidXmlException.php
│        │     │  └─ XmlParsingException.php
│        │     └─ XmlUtils.php
│        ├─ console
│        │  ├─ Application.php
│        │  ├─ Attribute
│        │  │  ├─ Argument.php
│        │  │  ├─ AsCommand.php
│        │  │  └─ Option.php
│        │  ├─ CHANGELOG.md
│        │  ├─ CI
│        │  │  └─ GithubActionReporter.php
│        │  ├─ Color.php
│        │  ├─ Command
│        │  │  ├─ Command.php
│        │  │  ├─ CompleteCommand.php
│        │  │  ├─ DumpCompletionCommand.php
│        │  │  ├─ HelpCommand.php
│        │  │  ├─ InvokableCommand.php
│        │  │  ├─ LazyCommand.php
│        │  │  ├─ ListCommand.php
│        │  │  ├─ LockableTrait.php
│        │  │  ├─ SignalableCommandInterface.php
│        │  │  └─ TraceableCommand.php
│        │  ├─ CommandLoader
│        │  │  ├─ CommandLoaderInterface.php
│        │  │  ├─ ContainerCommandLoader.php
│        │  │  └─ FactoryCommandLoader.php
│        │  ├─ Completion
│        │  │  ├─ CompletionInput.php
│        │  │  ├─ CompletionSuggestions.php
│        │  │  ├─ Output
│        │  │  │  ├─ BashCompletionOutput.php
│        │  │  │  ├─ CompletionOutputInterface.php
│        │  │  │  ├─ FishCompletionOutput.php
│        │  │  │  └─ ZshCompletionOutput.php
│        │  │  └─ Suggestion.php
│        │  ├─ composer.json
│        │  ├─ ConsoleEvents.php
│        │  ├─ Cursor.php
│        │  ├─ DataCollector
│        │  │  └─ CommandDataCollector.php
│        │  ├─ Debug
│        │  │  └─ CliRequest.php
│        │  ├─ DependencyInjection
│        │  │  └─ AddConsoleCommandPass.php
│        │  ├─ Descriptor
│        │  │  ├─ ApplicationDescription.php
│        │  │  ├─ Descriptor.php
│        │  │  ├─ DescriptorInterface.php
│        │  │  ├─ JsonDescriptor.php
│        │  │  ├─ MarkdownDescriptor.php
│        │  │  ├─ ReStructuredTextDescriptor.php
│        │  │  ├─ TextDescriptor.php
│        │  │  └─ XmlDescriptor.php
│        │  ├─ Event
│        │  │  ├─ ConsoleAlarmEvent.php
│        │  │  ├─ ConsoleCommandEvent.php
│        │  │  ├─ ConsoleErrorEvent.php
│        │  │  ├─ ConsoleEvent.php
│        │  │  ├─ ConsoleSignalEvent.php
│        │  │  └─ ConsoleTerminateEvent.php
│        │  ├─ EventListener
│        │  │  └─ ErrorListener.php
│        │  ├─ Exception
│        │  │  ├─ CommandNotFoundException.php
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ InvalidArgumentException.php
│        │  │  ├─ InvalidOptionException.php
│        │  │  ├─ LogicException.php
│        │  │  ├─ MissingInputException.php
│        │  │  ├─ NamespaceNotFoundException.php
│        │  │  ├─ RunCommandFailedException.php
│        │  │  └─ RuntimeException.php
│        │  ├─ Formatter
│        │  │  ├─ NullOutputFormatter.php
│        │  │  ├─ NullOutputFormatterStyle.php
│        │  │  ├─ OutputFormatter.php
│        │  │  ├─ OutputFormatterInterface.php
│        │  │  ├─ OutputFormatterStyle.php
│        │  │  ├─ OutputFormatterStyleInterface.php
│        │  │  ├─ OutputFormatterStyleStack.php
│        │  │  └─ WrappableOutputFormatterInterface.php
│        │  ├─ Helper
│        │  │  ├─ DebugFormatterHelper.php
│        │  │  ├─ DescriptorHelper.php
│        │  │  ├─ Dumper.php
│        │  │  ├─ FormatterHelper.php
│        │  │  ├─ Helper.php
│        │  │  ├─ HelperInterface.php
│        │  │  ├─ HelperSet.php
│        │  │  ├─ InputAwareHelper.php
│        │  │  ├─ OutputWrapper.php
│        │  │  ├─ ProcessHelper.php
│        │  │  ├─ ProgressBar.php
│        │  │  ├─ ProgressIndicator.php
│        │  │  ├─ QuestionHelper.php
│        │  │  ├─ SymfonyQuestionHelper.php
│        │  │  ├─ Table.php
│        │  │  ├─ TableCell.php
│        │  │  ├─ TableCellStyle.php
│        │  │  ├─ TableRows.php
│        │  │  ├─ TableSeparator.php
│        │  │  ├─ TableStyle.php
│        │  │  ├─ TreeHelper.php
│        │  │  ├─ TreeNode.php
│        │  │  └─ TreeStyle.php
│        │  ├─ Input
│        │  │  ├─ ArgvInput.php
│        │  │  ├─ ArrayInput.php
│        │  │  ├─ Input.php
│        │  │  ├─ InputArgument.php
│        │  │  ├─ InputAwareInterface.php
│        │  │  ├─ InputDefinition.php
│        │  │  ├─ InputInterface.php
│        │  │  ├─ InputOption.php
│        │  │  ├─ StreamableInputInterface.php
│        │  │  └─ StringInput.php
│        │  ├─ LICENSE
│        │  ├─ Logger
│        │  │  └─ ConsoleLogger.php
│        │  ├─ Messenger
│        │  │  ├─ RunCommandContext.php
│        │  │  ├─ RunCommandMessage.php
│        │  │  └─ RunCommandMessageHandler.php
│        │  ├─ Output
│        │  │  ├─ AnsiColorMode.php
│        │  │  ├─ BufferedOutput.php
│        │  │  ├─ ConsoleOutput.php
│        │  │  ├─ ConsoleOutputInterface.php
│        │  │  ├─ ConsoleSectionOutput.php
│        │  │  ├─ NullOutput.php
│        │  │  ├─ Output.php
│        │  │  ├─ OutputInterface.php
│        │  │  ├─ StreamOutput.php
│        │  │  └─ TrimmedBufferOutput.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ Question
│        │  │  ├─ ChoiceQuestion.php
│        │  │  ├─ ConfirmationQuestion.php
│        │  │  └─ Question.php
│        │  ├─ README.md
│        │  ├─ Resources
│        │  │  ├─ bin
│        │  │  │  └─ hiddeninput.exe
│        │  │  ├─ completion.bash
│        │  │  ├─ completion.fish
│        │  │  └─ completion.zsh
│        │  ├─ SignalRegistry
│        │  │  ├─ SignalMap.php
│        │  │  └─ SignalRegistry.php
│        │  ├─ SingleCommandApplication.php
│        │  ├─ Style
│        │  │  ├─ OutputStyle.php
│        │  │  ├─ StyleInterface.php
│        │  │  └─ SymfonyStyle.php
│        │  ├─ Terminal.php
│        │  ├─ Tester
│        │  │  ├─ ApplicationTester.php
│        │  │  ├─ CommandCompletionTester.php
│        │  │  ├─ CommandTester.php
│        │  │  ├─ Constraint
│        │  │  │  └─ CommandIsSuccessful.php
│        │  │  └─ TesterTrait.php
│        │  └─ Tests
│        │     ├─ ApplicationTest.php
│        │     ├─ CI
│        │     │  └─ GithubActionReporterTest.php
│        │     ├─ ColorTest.php
│        │     ├─ Command
│        │     │  ├─ CommandTest.php
│        │     │  ├─ CompleteCommandTest.php
│        │     │  ├─ DumpCompletionCommandTest.php
│        │     │  ├─ HelpCommandTest.php
│        │     │  ├─ InvokableCommandTest.php
│        │     │  ├─ ListCommandTest.php
│        │     │  ├─ LockableTraitTest.php
│        │     │  └─ SingleCommandApplicationTest.php
│        │     ├─ CommandLoader
│        │     │  ├─ ContainerCommandLoaderTest.php
│        │     │  └─ FactoryCommandLoaderTest.php
│        │     ├─ Completion
│        │     │  ├─ CompletionInputTest.php
│        │     │  └─ Output
│        │     │     ├─ BashCompletionOutputTest.php
│        │     │     ├─ CompletionOutputTestCase.php
│        │     │     ├─ FishCompletionOutputTest.php
│        │     │     └─ ZshCompletionOutputTest.php
│        │     ├─ ConsoleEventsTest.php
│        │     ├─ CursorTest.php
│        │     ├─ DependencyInjection
│        │     │  └─ AddConsoleCommandPassTest.php
│        │     ├─ Descriptor
│        │     │  ├─ AbstractDescriptorTestCase.php
│        │     │  ├─ ApplicationDescriptionTest.php
│        │     │  ├─ JsonDescriptorTest.php
│        │     │  ├─ MarkdownDescriptorTest.php
│        │     │  ├─ ObjectsProvider.php
│        │     │  ├─ ReStructuredTextDescriptorTest.php
│        │     │  ├─ TextDescriptorTest.php
│        │     │  └─ XmlDescriptorTest.php
│        │     ├─ EventListener
│        │     │  └─ ErrorListenerTest.php
│        │     ├─ Fixtures
│        │     │  ├─ application.dont_run_alternative_namespace_name.txt
│        │     │  ├─ application_1.json
│        │     │  ├─ application_1.md
│        │     │  ├─ application_1.rst
│        │     │  ├─ application_1.txt
│        │     │  ├─ application_1.xml
│        │     │  ├─ application_2.json
│        │     │  ├─ application_2.md
│        │     │  ├─ application_2.rst
│        │     │  ├─ application_2.txt
│        │     │  ├─ application_2.xml
│        │     │  ├─ application_filtered_namespace.txt
│        │     │  ├─ application_gethelp.txt
│        │     │  ├─ application_mbstring.md
│        │     │  ├─ application_mbstring.rst
│        │     │  ├─ application_mbstring.txt
│        │     │  ├─ application_renderexception1.txt
│        │     │  ├─ application_renderexception2.txt
│        │     │  ├─ application_renderexception3.txt
│        │     │  ├─ application_renderexception3decorated.txt
│        │     │  ├─ application_renderexception4.txt
│        │     │  ├─ application_renderexception_doublewidth1.txt
│        │     │  ├─ application_renderexception_doublewidth1decorated.txt
│        │     │  ├─ application_renderexception_doublewidth2.txt
│        │     │  ├─ application_renderexception_escapeslines.txt
│        │     │  ├─ application_renderexception_linebreaks.txt
│        │     │  ├─ application_rendersynopsis_escapesline.txt
│        │     │  ├─ application_run1.txt
│        │     │  ├─ application_run2.txt
│        │     │  ├─ application_run3.txt
│        │     │  ├─ application_run4.txt
│        │     │  ├─ application_run5.txt
│        │     │  ├─ application_signalable.php
│        │     │  ├─ BarBucCommand.php
│        │     │  ├─ BarHiddenCommand.php
│        │     │  ├─ command_1.json
│        │     │  ├─ command_1.md
│        │     │  ├─ command_1.rst
│        │     │  ├─ command_1.txt
│        │     │  ├─ command_1.xml
│        │     │  ├─ command_2.json
│        │     │  ├─ command_2.md
│        │     │  ├─ command_2.rst
│        │     │  ├─ command_2.txt
│        │     │  ├─ command_2.xml
│        │     │  ├─ command_mbstring.md
│        │     │  ├─ command_mbstring.rst
│        │     │  ├─ command_mbstring.txt
│        │     │  ├─ DescriptorApplication1.php
│        │     │  ├─ DescriptorApplication2.php
│        │     │  ├─ DescriptorApplicationMbString.php
│        │     │  ├─ DescriptorCommand1.php
│        │     │  ├─ DescriptorCommand2.php
│        │     │  ├─ DescriptorCommand3.php
│        │     │  ├─ DescriptorCommand4.php
│        │     │  ├─ DescriptorCommandMbString.php
│        │     │  ├─ DummyOutput.php
│        │     │  ├─ Foo1Command.php
│        │     │  ├─ Foo2Command.php
│        │     │  ├─ Foo3Command.php
│        │     │  ├─ Foo4Command.php
│        │     │  ├─ Foo5Command.php
│        │     │  ├─ Foo6Command.php
│        │     │  ├─ FoobarCommand.php
│        │     │  ├─ FooCommand.php
│        │     │  ├─ FooHiddenCommand.php
│        │     │  ├─ FooLock2Command.php
│        │     │  ├─ FooLock3Command.php
│        │     │  ├─ FooLock4InvokableCommand.php
│        │     │  ├─ FooLockCommand.php
│        │     │  ├─ FooOptCommand.php
│        │     │  ├─ FooSameCaseLowercaseCommand.php
│        │     │  ├─ FooSameCaseUppercaseCommand.php
│        │     │  ├─ FooSubnamespaced1Command.php
│        │     │  ├─ FooSubnamespaced2Command.php
│        │     │  ├─ FooWithoutAliasCommand.php
│        │     │  ├─ input_argument_1.json
│        │     │  ├─ input_argument_1.md
│        │     │  ├─ input_argument_1.rst
│        │     │  ├─ input_argument_1.txt
│        │     │  ├─ input_argument_1.xml
│        │     │  ├─ input_argument_2.json
│        │     │  ├─ input_argument_2.md
│        │     │  ├─ input_argument_2.rst
│        │     │  ├─ input_argument_2.txt
│        │     │  ├─ input_argument_2.xml
│        │     │  ├─ input_argument_3.json
│        │     │  ├─ input_argument_3.md
│        │     │  ├─ input_argument_3.rst
│        │     │  ├─ input_argument_3.txt
│        │     │  ├─ input_argument_3.xml
│        │     │  ├─ input_argument_4.json
│        │     │  ├─ input_argument_4.md
│        │     │  ├─ input_argument_4.rst
│        │     │  ├─ input_argument_4.txt
│        │     │  ├─ input_argument_4.xml
│        │     │  ├─ input_argument_with_default_inf_value.json
│        │     │  ├─ input_argument_with_default_inf_value.md
│        │     │  ├─ input_argument_with_default_inf_value.rst
│        │     │  ├─ input_argument_with_default_inf_value.txt
│        │     │  ├─ input_argument_with_default_inf_value.xml
│        │     │  ├─ input_argument_with_style.json
│        │     │  ├─ input_argument_with_style.md
│        │     │  ├─ input_argument_with_style.rst
│        │     │  ├─ input_argument_with_style.txt
│        │     │  ├─ input_argument_with_style.xml
│        │     │  ├─ input_definition_1.json
│        │     │  ├─ input_definition_1.md
│        │     │  ├─ input_definition_1.rst
│        │     │  ├─ input_definition_1.txt
│        │     │  ├─ input_definition_1.xml
│        │     │  ├─ input_definition_2.json
│        │     │  ├─ input_definition_2.md
│        │     │  ├─ input_definition_2.rst
│        │     │  ├─ input_definition_2.txt
│        │     │  ├─ input_definition_2.xml
│        │     │  ├─ input_definition_3.json
│        │     │  ├─ input_definition_3.md
│        │     │  ├─ input_definition_3.rst
│        │     │  ├─ input_definition_3.txt
│        │     │  ├─ input_definition_3.xml
│        │     │  ├─ input_definition_4.json
│        │     │  ├─ input_definition_4.md
│        │     │  ├─ input_definition_4.rst
│        │     │  ├─ input_definition_4.txt
│        │     │  ├─ input_definition_4.xml
│        │     │  ├─ input_option_1.json
│        │     │  ├─ input_option_1.md
│        │     │  ├─ input_option_1.rst
│        │     │  ├─ input_option_1.txt
│        │     │  ├─ input_option_1.xml
│        │     │  ├─ input_option_2.json
│        │     │  ├─ input_option_2.md
│        │     │  ├─ input_option_2.rst
│        │     │  ├─ input_option_2.txt
│        │     │  ├─ input_option_2.xml
│        │     │  ├─ input_option_3.json
│        │     │  ├─ input_option_3.md
│        │     │  ├─ input_option_3.rst
│        │     │  ├─ input_option_3.txt
│        │     │  ├─ input_option_3.xml
│        │     │  ├─ input_option_4.json
│        │     │  ├─ input_option_4.md
│        │     │  ├─ input_option_4.rst
│        │     │  ├─ input_option_4.txt
│        │     │  ├─ input_option_4.xml
│        │     │  ├─ input_option_5.json
│        │     │  ├─ input_option_5.md
│        │     │  ├─ input_option_5.rst
│        │     │  ├─ input_option_5.txt
│        │     │  ├─ input_option_5.xml
│        │     │  ├─ input_option_6.json
│        │     │  ├─ input_option_6.md
│        │     │  ├─ input_option_6.rst
│        │     │  ├─ input_option_6.txt
│        │     │  ├─ input_option_6.xml
│        │     │  ├─ input_option_with_default_inf_value.json
│        │     │  ├─ input_option_with_default_inf_value.md
│        │     │  ├─ input_option_with_default_inf_value.rst
│        │     │  ├─ input_option_with_default_inf_value.txt
│        │     │  ├─ input_option_with_default_inf_value.xml
│        │     │  ├─ input_option_with_style.json
│        │     │  ├─ input_option_with_style.md
│        │     │  ├─ input_option_with_style.rst
│        │     │  ├─ input_option_with_style.txt
│        │     │  ├─ input_option_with_style.xml
│        │     │  ├─ input_option_with_style_array.json
│        │     │  ├─ input_option_with_style_array.md
│        │     │  ├─ input_option_with_style_array.rst
│        │     │  ├─ input_option_with_style_array.txt
│        │     │  ├─ input_option_with_style_array.xml
│        │     │  ├─ MockableAppliationWithTerminalWidth.php
│        │     │  ├─ stream_output_file.txt
│        │     │  ├─ Style
│        │     │  │  └─ SymfonyStyle
│        │     │  │     ├─ command
│        │     │  │     │  ├─ command_0.php
│        │     │  │     │  ├─ command_1.php
│        │     │  │     │  ├─ command_10.php
│        │     │  │     │  ├─ command_11.php
│        │     │  │     │  ├─ command_12.php
│        │     │  │     │  ├─ command_13.php
│        │     │  │     │  ├─ command_14.php
│        │     │  │     │  ├─ command_15.php
│        │     │  │     │  ├─ command_16.php
│        │     │  │     │  ├─ command_17.php
│        │     │  │     │  ├─ command_18.php
│        │     │  │     │  ├─ command_19.php
│        │     │  │     │  ├─ command_2.php
│        │     │  │     │  ├─ command_20.php
│        │     │  │     │  ├─ command_21.php
│        │     │  │     │  ├─ command_22.php
│        │     │  │     │  ├─ command_23.php
│        │     │  │     │  ├─ command_3.php
│        │     │  │     │  ├─ command_4.php
│        │     │  │     │  ├─ command_4_with_iterators.php
│        │     │  │     │  ├─ command_5.php
│        │     │  │     │  ├─ command_6.php
│        │     │  │     │  ├─ command_7.php
│        │     │  │     │  ├─ command_8.php
│        │     │  │     │  ├─ command_9.php
│        │     │  │     │  └─ interactive_command_1.php
│        │     │  │     ├─ output
│        │     │  │     │  ├─ interactive_output_1.txt
│        │     │  │     │  ├─ output_0.txt
│        │     │  │     │  ├─ output_1.txt
│        │     │  │     │  ├─ output_10.txt
│        │     │  │     │  ├─ output_11.txt
│        │     │  │     │  ├─ output_12.txt
│        │     │  │     │  ├─ output_13.txt
│        │     │  │     │  ├─ output_14.txt
│        │     │  │     │  ├─ output_15.txt
│        │     │  │     │  ├─ output_16.txt
│        │     │  │     │  ├─ output_17.txt
│        │     │  │     │  ├─ output_18.txt
│        │     │  │     │  ├─ output_19.txt
│        │     │  │     │  ├─ output_2.txt
│        │     │  │     │  ├─ output_20.txt
│        │     │  │     │  ├─ output_21.txt
│        │     │  │     │  ├─ output_22.txt
│        │     │  │     │  ├─ output_23.txt
│        │     │  │     │  ├─ output_3.txt
│        │     │  │     │  ├─ output_4.txt
│        │     │  │     │  ├─ output_4_with_iterators.txt
│        │     │  │     │  ├─ output_5.txt
│        │     │  │     │  ├─ output_6.txt
│        │     │  │     │  ├─ output_7.txt
│        │     │  │     │  ├─ output_8.txt
│        │     │  │     │  └─ output_9.txt
│        │     │  │     └─ progress
│        │     │  │        ├─ command_progress_iterate.php
│        │     │  │        ├─ output_progress_iterate_no_shade.txt
│        │     │  │        └─ output_progress_iterate_shade.txt
│        │     │  ├─ TestAmbiguousCommandRegistering.php
│        │     │  ├─ TestAmbiguousCommandRegistering2.php
│        │     │  └─ TestCommand.php
│        │     ├─ Formatter
│        │     │  ├─ NullOutputFormatterStyleTest.php
│        │     │  ├─ NullOutputFormatterTest.php
│        │     │  ├─ OutputFormatterStyleStackTest.php
│        │     │  ├─ OutputFormatterStyleTest.php
│        │     │  └─ OutputFormatterTest.php
│        │     ├─ Helper
│        │     │  ├─ AbstractQuestionHelperTestCase.php
│        │     │  ├─ DescriptorHelperTest.php
│        │     │  ├─ DumperNativeFallbackTest.php
│        │     │  ├─ DumperTest.php
│        │     │  ├─ FormatterHelperTest.php
│        │     │  ├─ HelperSetTest.php
│        │     │  ├─ HelperTest.php
│        │     │  ├─ OutputWrapperTest.php
│        │     │  ├─ ProcessHelperTest.php
│        │     │  ├─ ProgressBarTest.php
│        │     │  ├─ ProgressIndicatorTest.php
│        │     │  ├─ QuestionHelperTest.php
│        │     │  ├─ SymfonyQuestionHelperTest.php
│        │     │  ├─ TableCellStyleTest.php
│        │     │  ├─ TableStyleTest.php
│        │     │  ├─ TableTest.php
│        │     │  ├─ TreeHelperTest.php
│        │     │  ├─ TreeNodeTest.php
│        │     │  └─ TreeStyleTest.php
│        │     ├─ Input
│        │     │  ├─ ArgvInputTest.php
│        │     │  ├─ ArrayInputTest.php
│        │     │  ├─ InputArgumentTest.php
│        │     │  ├─ InputDefinitionTest.php
│        │     │  ├─ InputOptionTest.php
│        │     │  ├─ InputTest.php
│        │     │  └─ StringInputTest.php
│        │     ├─ Logger
│        │     │  └─ ConsoleLoggerTest.php
│        │     ├─ Messenger
│        │     │  └─ RunCommandMessageHandlerTest.php
│        │     ├─ Output
│        │     │  ├─ AnsiColorModeTest.php
│        │     │  ├─ ConsoleOutputTest.php
│        │     │  ├─ ConsoleSectionOutputTest.php
│        │     │  ├─ NullOutputTest.php
│        │     │  ├─ OutputTest.php
│        │     │  └─ StreamOutputTest.php
│        │     ├─ phpt
│        │     │  ├─ alarm
│        │     │  │  └─ command_exit.phpt
│        │     │  ├─ signal
│        │     │  │  └─ command_exit.phpt
│        │     │  ├─ single_application
│        │     │  │  ├─ arg.phpt
│        │     │  │  ├─ default.phpt
│        │     │  │  ├─ help_name.phpt
│        │     │  │  ├─ version_default_name.phpt
│        │     │  │  └─ version_name.phpt
│        │     │  └─ uses_stdin_as_interactive_input.phpt
│        │     ├─ Question
│        │     │  ├─ ChoiceQuestionTest.php
│        │     │  ├─ ConfirmationQuestionTest.php
│        │     │  └─ QuestionTest.php
│        │     ├─ SignalRegistry
│        │     │  ├─ SignalMapTest.php
│        │     │  └─ SignalRegistryTest.php
│        │     ├─ Style
│        │     │  └─ SymfonyStyleTest.php
│        │     ├─ TerminalTest.php
│        │     └─ Tester
│        │        ├─ ApplicationTesterTest.php
│        │        ├─ CommandTesterTest.php
│        │        └─ Constraint
│        │           └─ CommandIsSuccessfulTest.php
│        ├─ dependency-injection
│        │  ├─ Alias.php
│        │  ├─ Argument
│        │  │  ├─ AbstractArgument.php
│        │  │  ├─ ArgumentInterface.php
│        │  │  ├─ BoundArgument.php
│        │  │  ├─ IteratorArgument.php
│        │  │  ├─ LazyClosure.php
│        │  │  ├─ RewindableGenerator.php
│        │  │  ├─ ServiceClosureArgument.php
│        │  │  ├─ ServiceLocator.php
│        │  │  ├─ ServiceLocatorArgument.php
│        │  │  └─ TaggedIteratorArgument.php
│        │  ├─ Attribute
│        │  │  ├─ AsAlias.php
│        │  │  ├─ AsDecorator.php
│        │  │  ├─ AsTaggedItem.php
│        │  │  ├─ Autoconfigure.php
│        │  │  ├─ AutoconfigureTag.php
│        │  │  ├─ Autowire.php
│        │  │  ├─ AutowireCallable.php
│        │  │  ├─ AutowireDecorated.php
│        │  │  ├─ AutowireInline.php
│        │  │  ├─ AutowireIterator.php
│        │  │  ├─ AutowireLocator.php
│        │  │  ├─ AutowireMethodOf.php
│        │  │  ├─ AutowireServiceClosure.php
│        │  │  ├─ Exclude.php
│        │  │  ├─ Lazy.php
│        │  │  ├─ TaggedIterator.php
│        │  │  ├─ TaggedLocator.php
│        │  │  ├─ Target.php
│        │  │  ├─ When.php
│        │  │  └─ WhenNot.php
│        │  ├─ CHANGELOG.md
│        │  ├─ ChildDefinition.php
│        │  ├─ Compiler
│        │  │  ├─ AbstractRecursivePass.php
│        │  │  ├─ AliasDeprecatedPublicServicesPass.php
│        │  │  ├─ AnalyzeServiceReferencesPass.php
│        │  │  ├─ AttributeAutoconfigurationPass.php
│        │  │  ├─ AutoAliasServicePass.php
│        │  │  ├─ AutowireAsDecoratorPass.php
│        │  │  ├─ AutowirePass.php
│        │  │  ├─ AutowireRequiredMethodsPass.php
│        │  │  ├─ AutowireRequiredPropertiesPass.php
│        │  │  ├─ CheckAliasValidityPass.php
│        │  │  ├─ CheckArgumentsValidityPass.php
│        │  │  ├─ CheckCircularReferencesPass.php
│        │  │  ├─ CheckDefinitionValidityPass.php
│        │  │  ├─ CheckExceptionOnInvalidReferenceBehaviorPass.php
│        │  │  ├─ CheckReferenceValidityPass.php
│        │  │  ├─ CheckTypeDeclarationsPass.php
│        │  │  ├─ Compiler.php
│        │  │  ├─ CompilerPassInterface.php
│        │  │  ├─ DecoratorServicePass.php
│        │  │  ├─ DefinitionErrorExceptionPass.php
│        │  │  ├─ ExtensionCompilerPass.php
│        │  │  ├─ InlineServiceDefinitionsPass.php
│        │  │  ├─ MergeExtensionConfigurationPass.php
│        │  │  ├─ PassConfig.php
│        │  │  ├─ PriorityTaggedServiceTrait.php
│        │  │  ├─ RegisterAutoconfigureAttributesPass.php
│        │  │  ├─ RegisterEnvVarProcessorsPass.php
│        │  │  ├─ RegisterReverseContainerPass.php
│        │  │  ├─ RegisterServiceSubscribersPass.php
│        │  │  ├─ RemoveAbstractDefinitionsPass.php
│        │  │  ├─ RemoveBuildParametersPass.php
│        │  │  ├─ RemovePrivateAliasesPass.php
│        │  │  ├─ RemoveUnusedDefinitionsPass.php
│        │  │  ├─ ReplaceAliasByActualDefinitionPass.php
│        │  │  ├─ ResolveAutowireInlineAttributesPass.php
│        │  │  ├─ ResolveBindingsPass.php
│        │  │  ├─ ResolveChildDefinitionsPass.php
│        │  │  ├─ ResolveClassPass.php
│        │  │  ├─ ResolveDecoratorStackPass.php
│        │  │  ├─ ResolveEnvPlaceholdersPass.php
│        │  │  ├─ ResolveFactoryClassPass.php
│        │  │  ├─ ResolveHotPathPass.php
│        │  │  ├─ ResolveInstanceofConditionalsPass.php
│        │  │  ├─ ResolveInvalidReferencesPass.php
│        │  │  ├─ ResolveNamedArgumentsPass.php
│        │  │  ├─ ResolveNoPreloadPass.php
│        │  │  ├─ ResolveParameterPlaceHoldersPass.php
│        │  │  ├─ ResolveReferencesToAliasesPass.php
│        │  │  ├─ ResolveServiceSubscribersPass.php
│        │  │  ├─ ResolveTaggedIteratorArgumentPass.php
│        │  │  ├─ ServiceLocatorTagPass.php
│        │  │  ├─ ServiceReferenceGraph.php
│        │  │  ├─ ServiceReferenceGraphEdge.php
│        │  │  ├─ ServiceReferenceGraphNode.php
│        │  │  └─ ValidateEnvPlaceholdersPass.php
│        │  ├─ composer.json
│        │  ├─ Config
│        │  │  ├─ ContainerParametersResource.php
│        │  │  └─ ContainerParametersResourceChecker.php
│        │  ├─ Container.php
│        │  ├─ ContainerBuilder.php
│        │  ├─ ContainerInterface.php
│        │  ├─ Definition.php
│        │  ├─ Dumper
│        │  │  ├─ Dumper.php
│        │  │  ├─ DumperInterface.php
│        │  │  ├─ GraphvizDumper.php
│        │  │  ├─ PhpDumper.php
│        │  │  ├─ Preloader.php
│        │  │  ├─ XmlDumper.php
│        │  │  └─ YamlDumper.php
│        │  ├─ EnvVarLoaderInterface.php
│        │  ├─ EnvVarProcessor.php
│        │  ├─ EnvVarProcessorInterface.php
│        │  ├─ Exception
│        │  │  ├─ AutoconfigureFailedException.php
│        │  │  ├─ AutowiringFailedException.php
│        │  │  ├─ BadMethodCallException.php
│        │  │  ├─ EmptyParameterValueException.php
│        │  │  ├─ EnvNotFoundException.php
│        │  │  ├─ EnvParameterException.php
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ InvalidArgumentException.php
│        │  │  ├─ InvalidParameterTypeException.php
│        │  │  ├─ LogicException.php
│        │  │  ├─ OutOfBoundsException.php
│        │  │  ├─ ParameterCircularReferenceException.php
│        │  │  ├─ ParameterNotFoundException.php
│        │  │  ├─ RuntimeException.php
│        │  │  ├─ ServiceCircularReferenceException.php
│        │  │  └─ ServiceNotFoundException.php
│        │  ├─ ExpressionLanguage.php
│        │  ├─ ExpressionLanguageProvider.php
│        │  ├─ Extension
│        │  │  ├─ AbstractExtension.php
│        │  │  ├─ ConfigurableExtensionInterface.php
│        │  │  ├─ ConfigurationExtensionInterface.php
│        │  │  ├─ Extension.php
│        │  │  ├─ ExtensionInterface.php
│        │  │  ├─ ExtensionTrait.php
│        │  │  └─ PrependExtensionInterface.php
│        │  ├─ LazyProxy
│        │  │  ├─ Instantiator
│        │  │  │  ├─ InstantiatorInterface.php
│        │  │  │  ├─ LazyServiceInstantiator.php
│        │  │  │  └─ RealServiceInstantiator.php
│        │  │  └─ PhpDumper
│        │  │     ├─ DumperInterface.php
│        │  │     ├─ LazyServiceDumper.php
│        │  │     └─ NullDumper.php
│        │  ├─ LICENSE
│        │  ├─ Loader
│        │  │  ├─ ClosureLoader.php
│        │  │  ├─ Configurator
│        │  │  │  ├─ AbstractConfigurator.php
│        │  │  │  ├─ AbstractServiceConfigurator.php
│        │  │  │  ├─ AliasConfigurator.php
│        │  │  │  ├─ ClosureReferenceConfigurator.php
│        │  │  │  ├─ ContainerConfigurator.php
│        │  │  │  ├─ DefaultsConfigurator.php
│        │  │  │  ├─ EnvConfigurator.php
│        │  │  │  ├─ FromCallableConfigurator.php
│        │  │  │  ├─ InlineServiceConfigurator.php
│        │  │  │  ├─ InstanceofConfigurator.php
│        │  │  │  ├─ ParametersConfigurator.php
│        │  │  │  ├─ PrototypeConfigurator.php
│        │  │  │  ├─ ReferenceConfigurator.php
│        │  │  │  ├─ ServiceConfigurator.php
│        │  │  │  ├─ ServicesConfigurator.php
│        │  │  │  └─ Traits
│        │  │  │     ├─ AbstractTrait.php
│        │  │  │     ├─ ArgumentTrait.php
│        │  │  │     ├─ AutoconfigureTrait.php
│        │  │  │     ├─ AutowireTrait.php
│        │  │  │     ├─ BindTrait.php
│        │  │  │     ├─ CallTrait.php
│        │  │  │     ├─ ClassTrait.php
│        │  │  │     ├─ ConfiguratorTrait.php
│        │  │  │     ├─ ConstructorTrait.php
│        │  │  │     ├─ DecorateTrait.php
│        │  │  │     ├─ DeprecateTrait.php
│        │  │  │     ├─ FactoryTrait.php
│        │  │  │     ├─ FileTrait.php
│        │  │  │     ├─ FromCallableTrait.php
│        │  │  │     ├─ LazyTrait.php
│        │  │  │     ├─ ParentTrait.php
│        │  │  │     ├─ PropertyTrait.php
│        │  │  │     ├─ PublicTrait.php
│        │  │  │     ├─ ShareTrait.php
│        │  │  │     ├─ SyntheticTrait.php
│        │  │  │     └─ TagTrait.php
│        │  │  ├─ DirectoryLoader.php
│        │  │  ├─ FileLoader.php
│        │  │  ├─ GlobFileLoader.php
│        │  │  ├─ IniFileLoader.php
│        │  │  ├─ PhpFileLoader.php
│        │  │  ├─ schema
│        │  │  │  └─ dic
│        │  │  │     └─ services
│        │  │  │        └─ services-1.0.xsd
│        │  │  ├─ UndefinedExtensionHandler.php
│        │  │  ├─ XmlFileLoader.php
│        │  │  └─ YamlFileLoader.php
│        │  ├─ Parameter.php
│        │  ├─ ParameterBag
│        │  │  ├─ ContainerBag.php
│        │  │  ├─ ContainerBagInterface.php
│        │  │  ├─ EnvPlaceholderParameterBag.php
│        │  │  ├─ FrozenParameterBag.php
│        │  │  ├─ ParameterBag.php
│        │  │  └─ ParameterBagInterface.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Reference.php
│        │  ├─ ReverseContainer.php
│        │  ├─ ServiceLocator.php
│        │  ├─ StaticEnvVarLoader.php
│        │  ├─ TaggedContainerInterface.php
│        │  ├─ Tests
│        │  │  ├─ AliasTest.php
│        │  │  ├─ Argument
│        │  │  │  ├─ AbstractArgumentTest.php
│        │  │  │  ├─ LazyClosureTest.php
│        │  │  │  ├─ RewindableGeneratorTest.php
│        │  │  │  └─ TaggedIteratorArgumentTest.php
│        │  │  ├─ Attribute
│        │  │  │  ├─ AutowireCallableTest.php
│        │  │  │  ├─ AutowireInlineTest.php
│        │  │  │  ├─ AutowireLocatorTest.php
│        │  │  │  ├─ AutowireMethodOfTest.php
│        │  │  │  └─ AutowireTest.php
│        │  │  ├─ ChildDefinitionTest.php
│        │  │  ├─ Compiler
│        │  │  │  ├─ AbstractRecursivePassTest.php
│        │  │  │  ├─ AliasDeprecatedPublicServicesPassTest.php
│        │  │  │  ├─ AnalyzeServiceReferencesPassTest.php
│        │  │  │  ├─ AttributeAutoconfigurationPassTest.php
│        │  │  │  ├─ AutoAliasServicePassTest.php
│        │  │  │  ├─ AutowirePassTest.php
│        │  │  │  ├─ AutowireRequiredMethodsPassTest.php
│        │  │  │  ├─ AutowireRequiredPropertiesPassTest.php
│        │  │  │  ├─ CheckAliasValidityPassTest.php
│        │  │  │  ├─ CheckArgumentsValidityPassTest.php
│        │  │  │  ├─ CheckCircularReferencesPassTest.php
│        │  │  │  ├─ CheckDefinitionValidityPassTest.php
│        │  │  │  ├─ CheckExceptionOnInvalidReferenceBehaviorPassTest.php
│        │  │  │  ├─ CheckReferenceValidityPassTest.php
│        │  │  │  ├─ CheckTypeDeclarationsPassTest.php
│        │  │  │  ├─ CustomExpressionLanguageFunctionTest.php
│        │  │  │  ├─ DecoratorServicePassTest.php
│        │  │  │  ├─ DefinitionErrorExceptionPassTest.php
│        │  │  │  ├─ ExtensionCompilerPassTest.php
│        │  │  │  ├─ InlineServiceDefinitionsPassTest.php
│        │  │  │  ├─ IntegrationTest.php
│        │  │  │  ├─ MergeExtensionConfigurationPassTest.php
│        │  │  │  ├─ OptionalServiceClass.php
│        │  │  │  ├─ PassConfigTest.php
│        │  │  │  ├─ PriorityTaggedServiceTraitTest.php
│        │  │  │  ├─ RegisterAutoconfigureAttributesPassTest.php
│        │  │  │  ├─ RegisterEnvVarProcessorsPassTest.php
│        │  │  │  ├─ RegisterReverseContainerPassTest.php
│        │  │  │  ├─ RegisterServiceSubscribersPassTest.php
│        │  │  │  ├─ RemoveBuildParametersPassTest.php
│        │  │  │  ├─ RemoveUnusedDefinitionsPassTest.php
│        │  │  │  ├─ ReplaceAliasByActualDefinitionPassTest.php
│        │  │  │  ├─ ResolveAutowireInlineAttributesPassTest.php
│        │  │  │  ├─ ResolveBindingsPassTest.php
│        │  │  │  ├─ ResolveChildDefinitionsPassTest.php
│        │  │  │  ├─ ResolveClassPassTest.php
│        │  │  │  ├─ ResolveFactoryClassPassTest.php
│        │  │  │  ├─ ResolveHotPathPassTest.php
│        │  │  │  ├─ ResolveInstanceofConditionalsPassTest.php
│        │  │  │  ├─ ResolveInvalidReferencesPassTest.php
│        │  │  │  ├─ ResolveNamedArgumentsPassTest.php
│        │  │  │  ├─ ResolveNoPreloadPassTest.php
│        │  │  │  ├─ ResolveParameterPlaceHoldersPassTest.php
│        │  │  │  ├─ ResolveReferencesToAliasesPassTest.php
│        │  │  │  ├─ ResolveTaggedIteratorArgumentPassTest.php
│        │  │  │  ├─ ServiceLocatorTagPassTest.php
│        │  │  │  └─ ValidateEnvPlaceholdersPassTest.php
│        │  │  ├─ Config
│        │  │  │  ├─ ContainerParametersResourceCheckerTest.php
│        │  │  │  └─ ContainerParametersResourceTest.php
│        │  │  ├─ ContainerBuilderTest.php
│        │  │  ├─ ContainerTest.php
│        │  │  ├─ CrossCheckTest.php
│        │  │  ├─ DefinitionTest.php
│        │  │  ├─ Dumper
│        │  │  │  ├─ GraphvizDumperTest.php
│        │  │  │  ├─ PhpDumperTest.php
│        │  │  │  ├─ PreloaderTest.php
│        │  │  │  ├─ XmlDumperTest.php
│        │  │  │  └─ YamlDumperTest.php
│        │  │  ├─ EnvVarProcessorTest.php
│        │  │  ├─ Exception
│        │  │  │  ├─ AutowiringFailedExceptionTest.php
│        │  │  │  └─ InvalidParameterTypeExceptionTest.php
│        │  │  ├─ Extension
│        │  │  │  ├─ AbstractExtensionTest.php
│        │  │  │  └─ ExtensionTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ AcmeConfig
│        │  │  │  │  └─ NestedConfig.php
│        │  │  │  ├─ AcmeConfig.php
│        │  │  │  ├─ array.json
│        │  │  │  ├─ Attribute
│        │  │  │  │  ├─ CustomAnyAttribute.php
│        │  │  │  │  ├─ CustomAutoconfiguration.php
│        │  │  │  │  ├─ CustomChildAttribute.php
│        │  │  │  │  ├─ CustomMethodAttribute.php
│        │  │  │  │  ├─ CustomParameterAttribute.php
│        │  │  │  │  └─ CustomPropertyAttribute.php
│        │  │  │  ├─ AutoconfigureAttributed.php
│        │  │  │  ├─ AutoconfiguredInterface.php
│        │  │  │  ├─ AutoconfiguredInterface2.php
│        │  │  │  ├─ AutoconfiguredService1.php
│        │  │  │  ├─ AutoconfiguredService2.php
│        │  │  │  ├─ AutoconfigureRepeated.php
│        │  │  │  ├─ AutoconfigureRepeatedBindings.php
│        │  │  │  ├─ AutoconfigureRepeatedCalls.php
│        │  │  │  ├─ AutoconfigureRepeatedOverwrite.php
│        │  │  │  ├─ AutoconfigureRepeatedProperties.php
│        │  │  │  ├─ AutoconfigureRepeatedTag.php
│        │  │  │  ├─ AutowireLocatorConsumer.php
│        │  │  │  ├─ Bar.php
│        │  │  │  ├─ BarFactory.php
│        │  │  │  ├─ BarInterface.php
│        │  │  │  ├─ BarTagClass.php
│        │  │  │  ├─ CaseSensitiveClass.php
│        │  │  │  ├─ CheckAliasValidityPass
│        │  │  │  │  ├─ FooImplementing.php
│        │  │  │  │  ├─ FooInterface.php
│        │  │  │  │  └─ FooNotImplementing.php
│        │  │  │  ├─ CheckTypeDeclarationsPass
│        │  │  │  │  ├─ Bar.php
│        │  │  │  │  ├─ BarErroredDependency.php
│        │  │  │  │  ├─ BarMethodCall.php
│        │  │  │  │  ├─ BarOptionalArgument.php
│        │  │  │  │  ├─ BarOptionalArgumentNotNull.php
│        │  │  │  │  ├─ Deprecated.php
│        │  │  │  │  ├─ Foo.php
│        │  │  │  │  ├─ FooObject.php
│        │  │  │  │  ├─ IntersectionConstructor.php
│        │  │  │  │  ├─ UnionConstructor.php
│        │  │  │  │  ├─ UnionConstructorPHP82.php
│        │  │  │  │  ├─ Waldo.php
│        │  │  │  │  ├─ WaldoFoo.php
│        │  │  │  │  ├─ WaldoInterface.php
│        │  │  │  │  └─ Wobble.php
│        │  │  │  ├─ config
│        │  │  │  │  ├─ anonymous.expected.yml
│        │  │  │  │  ├─ anonymous.php
│        │  │  │  │  ├─ basic.expected.yml
│        │  │  │  │  ├─ basic.php
│        │  │  │  │  ├─ child.expected.yml
│        │  │  │  │  ├─ child.php
│        │  │  │  │  ├─ closure.expected.yml
│        │  │  │  │  ├─ closure.php
│        │  │  │  │  ├─ config_builder.expected.yml
│        │  │  │  │  ├─ config_builder.php
│        │  │  │  │  ├─ config_builder_env_configurator.php
│        │  │  │  │  ├─ defaults.expected.yml
│        │  │  │  │  ├─ defaults.php
│        │  │  │  │  ├─ definition
│        │  │  │  │  │  ├─ foo.php
│        │  │  │  │  │  └─ multiple
│        │  │  │  │  │     ├─ bar.php
│        │  │  │  │  │     └─ baz.php
│        │  │  │  │  ├─ env_configurator.php
│        │  │  │  │  ├─ env_param.expected.yml
│        │  │  │  │  ├─ env_param.php
│        │  │  │  │  ├─ expression_factory.expected.yml
│        │  │  │  │  ├─ expression_factory.php
│        │  │  │  │  ├─ factory_short_notation.php
│        │  │  │  │  ├─ from_callable.expected.yml
│        │  │  │  │  ├─ from_callable.php
│        │  │  │  │  ├─ inline_binding.expected.yml
│        │  │  │  │  ├─ inline_binding.php
│        │  │  │  │  ├─ inline_static_constructor.expected.yml
│        │  │  │  │  ├─ inline_static_constructor.php
│        │  │  │  │  ├─ instanceof.expected.yml
│        │  │  │  │  ├─ instanceof.php
│        │  │  │  │  ├─ instanceof_static_constructor.expected.yml
│        │  │  │  │  ├─ instanceof_static_constructor.php
│        │  │  │  │  ├─ lazy_fqcn.expected.yml
│        │  │  │  │  ├─ lazy_fqcn.php
│        │  │  │  │  ├─ nested_bundle_config.php
│        │  │  │  │  ├─ nested_config_builder.php
│        │  │  │  │  ├─ not_when_env.php
│        │  │  │  │  ├─ object.expected.yml
│        │  │  │  │  ├─ object.php
│        │  │  │  │  ├─ packages
│        │  │  │  │  │  ├─ ping.yaml
│        │  │  │  │  │  ├─ third_a.yaml
│        │  │  │  │  │  ├─ third_b.yaml
│        │  │  │  │  │  └─ third_c.yaml
│        │  │  │  │  ├─ php7.expected.yml
│        │  │  │  │  ├─ php7.php
│        │  │  │  │  ├─ prototype.expected.yml
│        │  │  │  │  ├─ prototype.php
│        │  │  │  │  ├─ prototype_array.expected.yml
│        │  │  │  │  ├─ prototype_array.php
│        │  │  │  │  ├─ remove.expected.yml
│        │  │  │  │  ├─ remove.php
│        │  │  │  │  ├─ services.php
│        │  │  │  │  ├─ services9.php
│        │  │  │  │  ├─ services_autoconfigure_with_parent.php
│        │  │  │  │  ├─ services_closure_argument.php
│        │  │  │  │  ├─ services_with_enumeration.php
│        │  │  │  │  ├─ services_with_service_locator_argument.php
│        │  │  │  │  ├─ stack.php
│        │  │  │  │  ├─ static_constructor.expected.yml
│        │  │  │  │  ├─ static_constructor.php
│        │  │  │  │  ├─ when_env.php
│        │  │  │  │  └─ when_not_when_env.php
│        │  │  │  ├─ ConstructNotExists.php
│        │  │  │  ├─ Container
│        │  │  │  │  ├─ ConstructorWithMandatoryArgumentsContainer.php
│        │  │  │  │  ├─ ConstructorWithOptionalArgumentsContainer.php
│        │  │  │  │  ├─ ConstructorWithoutArgumentsContainer.php
│        │  │  │  │  └─ NoConstructorContainer.php
│        │  │  │  ├─ containers
│        │  │  │  │  ├─ container10.php
│        │  │  │  │  ├─ container11.php
│        │  │  │  │  ├─ container12.php
│        │  │  │  │  ├─ container13.php
│        │  │  │  │  ├─ container14.php
│        │  │  │  │  ├─ container15.php
│        │  │  │  │  ├─ container16.php
│        │  │  │  │  ├─ container17.php
│        │  │  │  │  ├─ container19.php
│        │  │  │  │  ├─ container21.php
│        │  │  │  │  ├─ container24.php
│        │  │  │  │  ├─ container33.php
│        │  │  │  │  ├─ container34.php
│        │  │  │  │  ├─ container8.php
│        │  │  │  │  ├─ container9.php
│        │  │  │  │  ├─ container_abstract.php
│        │  │  │  │  ├─ container_almost_circular.php
│        │  │  │  │  ├─ container_deprecated_parameters.php
│        │  │  │  │  ├─ container_env_in_id.php
│        │  │  │  │  ├─ container_inline_requires.php
│        │  │  │  │  ├─ container_nonempty_parameters.php
│        │  │  │  │  ├─ container_non_scalar_tags.php
│        │  │  │  │  ├─ container_service_locator_argument.php
│        │  │  │  │  ├─ container_uninitialized_ref.php
│        │  │  │  │  └─ CustomContainer.php
│        │  │  │  ├─ CustomDefinition.php
│        │  │  │  ├─ DependencyContainer.php
│        │  │  │  ├─ DependencyContainerInterface.php
│        │  │  │  ├─ DeprecatedClass.php
│        │  │  │  ├─ directory
│        │  │  │  │  ├─ import
│        │  │  │  │  │  └─ import.yml
│        │  │  │  │  ├─ recurse
│        │  │  │  │  │  ├─ simple.ini
│        │  │  │  │  │  └─ simple.yml
│        │  │  │  │  └─ simple.php
│        │  │  │  ├─ Extension
│        │  │  │  │  ├─ InvalidConfig
│        │  │  │  │  │  ├─ Configuration.php
│        │  │  │  │  │  └─ InvalidConfigExtension.php
│        │  │  │  │  ├─ SemiValidConfig
│        │  │  │  │  │  ├─ Configuration.php
│        │  │  │  │  │  └─ SemiValidConfigExtension.php
│        │  │  │  │  └─ ValidConfig
│        │  │  │  │     ├─ Configuration.php
│        │  │  │  │     └─ ValidConfigExtension.php
│        │  │  │  ├─ FactoryDummy.php
│        │  │  │  ├─ FactoryDummyWithoutReturnTypes.php
│        │  │  │  ├─ FooBarTaggedClass.php
│        │  │  │  ├─ FooBarTaggedForDefaultPriorityClass.php
│        │  │  │  ├─ FooClassWithDefaultArrayAttribute.php
│        │  │  │  ├─ FooClassWithDefaultEnumAttribute.php
│        │  │  │  ├─ FooClassWithDefaultObjectAttribute.php
│        │  │  │  ├─ FooClassWithEnumAttribute.php
│        │  │  │  ├─ FooForCircularWithAddCalls.php
│        │  │  │  ├─ FooTagClass.php
│        │  │  │  ├─ FooTaggedForInvalidDefaultMethodClass.php
│        │  │  │  ├─ FooUnitEnum.php
│        │  │  │  ├─ FooWithAbstractArgument.php
│        │  │  │  ├─ graphviz
│        │  │  │  │  ├─ services1.dot
│        │  │  │  │  ├─ services10-1.dot
│        │  │  │  │  ├─ services10.dot
│        │  │  │  │  ├─ services13.dot
│        │  │  │  │  ├─ services14.dot
│        │  │  │  │  ├─ services17.dot
│        │  │  │  │  ├─ services18.dot
│        │  │  │  │  ├─ services9.dot
│        │  │  │  │  └─ services_inline.dot
│        │  │  │  ├─ includes
│        │  │  │  │  ├─ AcmeExtension.php
│        │  │  │  │  ├─ autowiring_classes.php
│        │  │  │  │  ├─ autowiring_classes_80.php
│        │  │  │  │  ├─ classes.php
│        │  │  │  │  ├─ compositetype_classes.php
│        │  │  │  │  ├─ createphar.php
│        │  │  │  │  ├─ foo.php
│        │  │  │  │  ├─ FooVariadic.php
│        │  │  │  │  ├─ foo_lazy.php
│        │  │  │  │  ├─ HotPath
│        │  │  │  │  │  ├─ C1.php
│        │  │  │  │  │  ├─ C2.php
│        │  │  │  │  │  ├─ C3.php
│        │  │  │  │  │  ├─ I1.php
│        │  │  │  │  │  ├─ P1.php
│        │  │  │  │  │  └─ T1.php
│        │  │  │  │  ├─ intersectiontype_classes.php
│        │  │  │  │  ├─ MultipleArgumentsOptionalScalarNotReallyOptional.php
│        │  │  │  │  ├─ ProjectExtension.php
│        │  │  │  │  ├─ ProjectWithXsdExtension.php
│        │  │  │  │  ├─ ProjectWithXsdExtensionInPhar.phar
│        │  │  │  │  ├─ schema
│        │  │  │  │  │  └─ project-1.0.xsd
│        │  │  │  │  └─ uniontype_classes.php
│        │  │  │  ├─ ini
│        │  │  │  │  ├─ almostvalid.ini
│        │  │  │  │  ├─ ini_with_wrong_ext.xml
│        │  │  │  │  ├─ nonvalid.ini
│        │  │  │  │  ├─ parameters.ini
│        │  │  │  │  ├─ parameters1.ini
│        │  │  │  │  ├─ parameters2.ini
│        │  │  │  │  ├─ types.ini
│        │  │  │  │  └─ when-env.ini
│        │  │  │  ├─ IntBackedEnum.php
│        │  │  │  ├─ IntTagClass.php
│        │  │  │  ├─ LazyAutoconfigured.php
│        │  │  │  ├─ LazyLoaded.php
│        │  │  │  ├─ MultipleAutoconfigureAttributed.php
│        │  │  │  ├─ NamedArgumentsDummy.php
│        │  │  │  ├─ NamedArgumentsVariadicsDummy.php
│        │  │  │  ├─ NamedEnumArgumentDummy.php
│        │  │  │  ├─ NamedIterableArgumentDummy.php
│        │  │  │  ├─ NewInInitializer.php
│        │  │  │  ├─ OptionalParameter.php
│        │  │  │  ├─ ParentNotExists.php
│        │  │  │  ├─ php
│        │  │  │  │  ├─ autowire_closure.php
│        │  │  │  │  ├─ callable_adapter_consumer.php
│        │  │  │  │  ├─ closure.php
│        │  │  │  │  ├─ closure_proxy.php
│        │  │  │  │  ├─ custom_container_class_constructor_without_arguments.php
│        │  │  │  │  ├─ custom_container_class_without_constructor.php
│        │  │  │  │  ├─ custom_container_class_with_mandatory_constructor_arguments.php
│        │  │  │  │  ├─ custom_container_class_with_optional_constructor_arguments.php
│        │  │  │  │  ├─ inline_adapter_consumer.php
│        │  │  │  │  ├─ lazy_autowire_attribute.php
│        │  │  │  │  ├─ lazy_autowire_attribute_with_intersection.php
│        │  │  │  │  ├─ lazy_closure.php
│        │  │  │  │  ├─ legacy_lazy_autowire_attribute.php
│        │  │  │  │  ├─ legacy_lazy_autowire_attribute_with_intersection.php
│        │  │  │  │  ├─ legacy_services9_lazy_inlined_factories.txt
│        │  │  │  │  ├─ legacy_services_dedup_lazy.php
│        │  │  │  │  ├─ legacy_services_non_shared_lazy.php
│        │  │  │  │  ├─ legacy_services_non_shared_lazy_as_files.txt
│        │  │  │  │  ├─ legacy_services_non_shared_lazy_ghost.php
│        │  │  │  │  ├─ legacy_services_non_shared_lazy_public.php
│        │  │  │  │  ├─ legacy_services_wither_lazy.php
│        │  │  │  │  ├─ legacy_services_wither_lazy_non_shared.php
│        │  │  │  │  ├─ php_with_wrong_ext.yml
│        │  │  │  │  ├─ return_foo_string.php
│        │  │  │  │  ├─ services1-1.php
│        │  │  │  │  ├─ services1.php
│        │  │  │  │  ├─ services10.php
│        │  │  │  │  ├─ services10_as_files.txt
│        │  │  │  │  ├─ services12.php
│        │  │  │  │  ├─ services13.php
│        │  │  │  │  ├─ services19.php
│        │  │  │  │  ├─ services24.php
│        │  │  │  │  ├─ services26.php
│        │  │  │  │  ├─ services33.php
│        │  │  │  │  ├─ services8.php
│        │  │  │  │  ├─ services9_as_files.txt
│        │  │  │  │  ├─ services9_compiled.php
│        │  │  │  │  ├─ services9_inlined_factories.txt
│        │  │  │  │  ├─ services9_inlined_factories_with_tagged_iterrator.txt
│        │  │  │  │  ├─ services9_lazy_inlined_factories.txt
│        │  │  │  │  ├─ services_adawson.php
│        │  │  │  │  ├─ services_almost_circular_private.php
│        │  │  │  │  ├─ services_almost_circular_public.php
│        │  │  │  │  ├─ services_array_params.php
│        │  │  │  │  ├─ services_base64_env.php
│        │  │  │  │  ├─ services_closure_argument_compiled.php
│        │  │  │  │  ├─ services_csv_env.php
│        │  │  │  │  ├─ services_current_factory_inlining.php
│        │  │  │  │  ├─ services_dedup_lazy.php
│        │  │  │  │  ├─ services_deep_graph.php
│        │  │  │  │  ├─ services_default_env.php
│        │  │  │  │  ├─ services_deprecated_parameters.php
│        │  │  │  │  ├─ services_deprecated_parameters_as_files.txt
│        │  │  │  │  ├─ services_env_in_id.php
│        │  │  │  │  ├─ services_errored_definition.php
│        │  │  │  │  ├─ services_inline_requires.php
│        │  │  │  │  ├─ services_inline_self_ref.php
│        │  │  │  │  ├─ services_json_env.php
│        │  │  │  │  ├─ services_locator.php
│        │  │  │  │  ├─ services_new_in_initializer.php
│        │  │  │  │  ├─ services_nonempty_parameters.php
│        │  │  │  │  ├─ services_nonempty_parameters_as_files.txt
│        │  │  │  │  ├─ services_non_shared_duplicates.php
│        │  │  │  │  ├─ services_non_shared_lazy.php
│        │  │  │  │  ├─ services_non_shared_lazy_as_files.txt
│        │  │  │  │  ├─ services_non_shared_lazy_ghost.php
│        │  │  │  │  ├─ services_non_shared_lazy_public.php
│        │  │  │  │  ├─ services_private_frozen.php
│        │  │  │  │  ├─ services_private_in_expression.php
│        │  │  │  │  ├─ services_query_string_env.php
│        │  │  │  │  ├─ services_rot13_env.php
│        │  │  │  │  ├─ services_service_locator_argument.php
│        │  │  │  │  ├─ services_subscriber.php
│        │  │  │  │  ├─ services_tsantos.php
│        │  │  │  │  ├─ services_uninitialized_ref.php
│        │  │  │  │  ├─ services_unsupported_characters.php
│        │  │  │  │  ├─ services_url_env.php
│        │  │  │  │  ├─ services_wither.php
│        │  │  │  │  ├─ services_wither_annotation.php
│        │  │  │  │  ├─ services_wither_lazy.php
│        │  │  │  │  ├─ services_wither_lazy_non_shared.php
│        │  │  │  │  ├─ services_wither_staticreturntype.php
│        │  │  │  │  ├─ simple.php
│        │  │  │  │  └─ static_constructor.php
│        │  │  │  ├─ Preload
│        │  │  │  │  ├─ A.php
│        │  │  │  │  ├─ B.php
│        │  │  │  │  ├─ C.php
│        │  │  │  │  ├─ D.php
│        │  │  │  │  ├─ Dummy.php
│        │  │  │  │  ├─ DummyWithInterface.php
│        │  │  │  │  ├─ E.php
│        │  │  │  │  ├─ F.php
│        │  │  │  │  ├─ G.php
│        │  │  │  │  ├─ IntersectionDummy.php
│        │  │  │  │  └─ UnionDummy.php
│        │  │  │  ├─ Prototype
│        │  │  │  │  ├─ BadAttributes
│        │  │  │  │  │  └─ WhenNotWhenFoo.php
│        │  │  │  │  ├─ BadClasses
│        │  │  │  │  │  └─ MissingParent.php
│        │  │  │  │  ├─ Foo.php
│        │  │  │  │  ├─ FooInterface.php
│        │  │  │  │  ├─ NotFoo.php
│        │  │  │  │  ├─ OtherDir
│        │  │  │  │  │  ├─ AnotherSub
│        │  │  │  │  │  │  └─ DeeperBaz.php
│        │  │  │  │  │  ├─ Baz.php
│        │  │  │  │  │  ├─ Component1
│        │  │  │  │  │  │  ├─ Dir1
│        │  │  │  │  │  │  │  └─ Service1.php
│        │  │  │  │  │  │  └─ Dir2
│        │  │  │  │  │  │     └─ Service2.php
│        │  │  │  │  │  └─ Component2
│        │  │  │  │  │     ├─ Dir1
│        │  │  │  │  │     │  └─ Service4.php
│        │  │  │  │  │     └─ Dir2
│        │  │  │  │  │        └─ Service5.php
│        │  │  │  │  ├─ SinglyImplementedInterface
│        │  │  │  │  │  ├─ Adapter
│        │  │  │  │  │  │  └─ Adapter.php
│        │  │  │  │  │  ├─ AnotherAdapter
│        │  │  │  │  │  │  └─ Adapter.php
│        │  │  │  │  │  └─ Port
│        │  │  │  │  │     └─ PortInterface.php
│        │  │  │  │  ├─ StaticConstructor
│        │  │  │  │  │  ├─ PrototypeStaticConstructor.php
│        │  │  │  │  │  ├─ PrototypeStaticConstructorAsArgument.php
│        │  │  │  │  │  └─ PrototypeStaticConstructorInterface.php
│        │  │  │  │  └─ Sub
│        │  │  │  │     ├─ Bar.php
│        │  │  │  │     └─ BarInterface.php
│        │  │  │  ├─ PrototypeAsAlias
│        │  │  │  │  ├─ AliasBarInterface.php
│        │  │  │  │  ├─ AliasFooInterface.php
│        │  │  │  │  ├─ WithAsAlias.php
│        │  │  │  │  ├─ WithAsAliasBothEnv.php
│        │  │  │  │  ├─ WithAsAliasDevEnv.php
│        │  │  │  │  ├─ WithAsAliasDuplicate.php
│        │  │  │  │  ├─ WithAsAliasIdMultipleInterface.php
│        │  │  │  │  ├─ WithAsAliasInterface.php
│        │  │  │  │  ├─ WithAsAliasMultiple.php
│        │  │  │  │  ├─ WithAsAliasMultipleInterface.php
│        │  │  │  │  └─ WithAsAliasProdEnv.php
│        │  │  │  ├─ ReadOnlyClass.php
│        │  │  │  ├─ RemoteCaller.php
│        │  │  │  ├─ RemoteCallerHttp.php
│        │  │  │  ├─ RemoteCallerSocket.php
│        │  │  │  ├─ ScalarFactory.php
│        │  │  │  ├─ SimilarArgumentsDummy.php
│        │  │  │  ├─ StaticConstructorAutoconfigure.php
│        │  │  │  ├─ StaticMethodTag.php
│        │  │  │  ├─ StdClassDecorator.php
│        │  │  │  ├─ StringBackedEnum.php
│        │  │  │  ├─ StubbedTranslator.php
│        │  │  │  ├─ TaggedConsumerWithExclude.php
│        │  │  │  ├─ TaggedIteratorConsumer.php
│        │  │  │  ├─ TaggedIteratorConsumerWithDefaultIndexMethod.php
│        │  │  │  ├─ TaggedIteratorConsumerWithDefaultIndexMethodAndWithDefaultPriorityMethod.php
│        │  │  │  ├─ TaggedIteratorConsumerWithDefaultPriorityMethod.php
│        │  │  │  ├─ TaggedLocatorConsumer.php
│        │  │  │  ├─ TaggedLocatorConsumerConsumer.php
│        │  │  │  ├─ TaggedLocatorConsumerFactory.php
│        │  │  │  ├─ TaggedLocatorConsumerWithDefaultIndexMethod.php
│        │  │  │  ├─ TaggedLocatorConsumerWithDefaultIndexMethodAndWithDefaultPriorityMethod.php
│        │  │  │  ├─ TaggedLocatorConsumerWithDefaultPriorityMethod.php
│        │  │  │  ├─ TaggedLocatorConsumerWithoutIndex.php
│        │  │  │  ├─ TaggedLocatorConsumerWithServiceSubscriber.php
│        │  │  │  ├─ TaggedService1.php
│        │  │  │  ├─ TaggedService2.php
│        │  │  │  ├─ TaggedService3.php
│        │  │  │  ├─ TaggedService3Configurator.php
│        │  │  │  ├─ TaggedService4.php
│        │  │  │  ├─ TaggedService5.php
│        │  │  │  ├─ TestDefinition1.php
│        │  │  │  ├─ TestDefinition2.php
│        │  │  │  ├─ TestDefinition3.php
│        │  │  │  ├─ TestServiceMethodsSubscriberTrait.php
│        │  │  │  ├─ TestServiceSubscriber.php
│        │  │  │  ├─ TestServiceSubscriberChild.php
│        │  │  │  ├─ TestServiceSubscriberIntersection.php
│        │  │  │  ├─ TestServiceSubscriberIntersectionWithTrait.php
│        │  │  │  ├─ TestServiceSubscriberParent.php
│        │  │  │  ├─ TestServiceSubscriberUnion.php
│        │  │  │  ├─ TestServiceSubscriberUnionWithTrait.php
│        │  │  │  ├─ Utils
│        │  │  │  │  └─ NotAService.php
│        │  │  │  ├─ WitherStaticReturnType.php
│        │  │  │  ├─ WithTarget.php
│        │  │  │  ├─ WithTargetAnonymous.php
│        │  │  │  ├─ xml
│        │  │  │  │  ├─ bindings_and_inner_collections.xml
│        │  │  │  │  ├─ class_from_id.xml
│        │  │  │  │  ├─ closure.xml
│        │  │  │  │  ├─ defaults_bindings.xml
│        │  │  │  │  ├─ defaults_bindings2.xml
│        │  │  │  │  ├─ deprecated_alias_definitions.xml
│        │  │  │  │  ├─ extension1
│        │  │  │  │  │  └─ services.xml
│        │  │  │  │  ├─ extension2
│        │  │  │  │  │  └─ services.xml
│        │  │  │  │  ├─ extensions
│        │  │  │  │  │  ├─ services1.xml
│        │  │  │  │  │  ├─ services2.xml
│        │  │  │  │  │  ├─ services3.xml
│        │  │  │  │  │  ├─ services4.xml
│        │  │  │  │  │  ├─ services5.xml
│        │  │  │  │  │  ├─ services6.xml
│        │  │  │  │  │  └─ services7.xml
│        │  │  │  │  ├─ from_callable.xml
│        │  │  │  │  ├─ invalid_alias_definition.xml
│        │  │  │  │  ├─ key_type_argument.xml
│        │  │  │  │  ├─ key_type_incorrect_bin.xml
│        │  │  │  │  ├─ key_type_property.xml
│        │  │  │  │  ├─ key_type_wrong_constant.xml
│        │  │  │  │  ├─ namespaces.xml
│        │  │  │  │  ├─ nested_service_without_id.xml
│        │  │  │  │  ├─ nonvalid.xml
│        │  │  │  │  ├─ not_singly_implemented_interface_in_multiple_resources.xml
│        │  │  │  │  ├─ not_singly_implemented_interface_in_multiple_resources_with_previously_registered_alias.xml
│        │  │  │  │  ├─ not_singly_implemented_interface_in_multiple_resources_with_previously_registered_alias2.xml
│        │  │  │  │  ├─ returns_clone.xml
│        │  │  │  │  ├─ services1.xml
│        │  │  │  │  ├─ services10.xml
│        │  │  │  │  ├─ services13.xml
│        │  │  │  │  ├─ services14.xml
│        │  │  │  │  ├─ services2.xml
│        │  │  │  │  ├─ services21.xml
│        │  │  │  │  ├─ services23.xml
│        │  │  │  │  ├─ services24.xml
│        │  │  │  │  ├─ services28.xml
│        │  │  │  │  ├─ services29.xml
│        │  │  │  │  ├─ services3.xml
│        │  │  │  │  ├─ services30.xml
│        │  │  │  │  ├─ services4.xml
│        │  │  │  │  ├─ services4_bad_import.xml
│        │  │  │  │  ├─ services4_bad_import_file_not_found.xml
│        │  │  │  │  ├─ services4_bad_import_nonvalid.xml
│        │  │  │  │  ├─ services4_bad_import_with_errors.xml
│        │  │  │  │  ├─ services5.xml
│        │  │  │  │  ├─ services6.xml
│        │  │  │  │  ├─ services7.xml
│        │  │  │  │  ├─ services8.xml
│        │  │  │  │  ├─ services9.xml
│        │  │  │  │  ├─ services_abstract.xml
│        │  │  │  │  ├─ services_autoconfigure.xml
│        │  │  │  │  ├─ services_autoconfigure_with_parent.xml
│        │  │  │  │  ├─ services_bindings.xml
│        │  │  │  │  ├─ services_case.xml
│        │  │  │  │  ├─ services_defaults_with_parent.xml
│        │  │  │  │  ├─ services_deprecated.xml
│        │  │  │  │  ├─ services_dump_load.xml
│        │  │  │  │  ├─ services_inline_not_candidate.xml
│        │  │  │  │  ├─ services_instanceof.xml
│        │  │  │  │  ├─ services_instanceof_with_parent.xml
│        │  │  │  │  ├─ services_lazy_fqcn.xml
│        │  │  │  │  ├─ services_named_args.xml
│        │  │  │  │  ├─ services_prototype.xml
│        │  │  │  │  ├─ services_prototype_array.xml
│        │  │  │  │  ├─ services_prototype_array_with_empty_node.xml
│        │  │  │  │  ├─ services_prototype_array_with_space_node.xml
│        │  │  │  │  ├─ services_prototype_constructor.xml
│        │  │  │  │  ├─ services_tsantos.xml
│        │  │  │  │  ├─ services_without_id.xml
│        │  │  │  │  ├─ services_with_abstract_argument.xml
│        │  │  │  │  ├─ services_with_array_tags.xml
│        │  │  │  │  ├─ services_with_default_array.xml
│        │  │  │  │  ├─ services_with_default_enumeration.xml
│        │  │  │  │  ├─ services_with_default_object.xml
│        │  │  │  │  ├─ services_with_deprecated_tagged.xml
│        │  │  │  │  ├─ services_with_enumeration.xml
│        │  │  │  │  ├─ services_with_invalid_enumeration.xml
│        │  │  │  │  ├─ services_with_service_closure.xml
│        │  │  │  │  ├─ services_with_service_locator_argument.xml
│        │  │  │  │  ├─ services_with_tagged_arguments.xml
│        │  │  │  │  ├─ service_with_abstract_argument.xml
│        │  │  │  │  ├─ singly_implemented_interface_in_multiple_resources.xml
│        │  │  │  │  ├─ stack.xml
│        │  │  │  │  ├─ static_constructor.xml
│        │  │  │  │  ├─ static_constructor_and_factory.xml
│        │  │  │  │  ├─ tag_without_name.xml
│        │  │  │  │  ├─ tag_with_empty_name.xml
│        │  │  │  │  ├─ tag_with_name_attribute.xml
│        │  │  │  │  ├─ when-env-services.xml
│        │  │  │  │  ├─ when-env.xml
│        │  │  │  │  ├─ withdoctype.xml
│        │  │  │  │  ├─ with_key_outside_collection.xml
│        │  │  │  │  └─ xml_with_wrong_ext.php
│        │  │  │  └─ yaml
│        │  │  │     ├─ alt_call.yaml
│        │  │  │     ├─ anonymous_services.yml
│        │  │  │     ├─ anonymous_services_alias.yml
│        │  │  │     ├─ anonymous_services_in_instanceof.yml
│        │  │  │     ├─ anonymous_services_in_parameters.yml
│        │  │  │     ├─ badtag1.yml
│        │  │  │     ├─ badtag2.yml
│        │  │  │     ├─ bad_alias.yml
│        │  │  │     ├─ bad_calls.yml
│        │  │  │     ├─ bad_decorates.yml
│        │  │  │     ├─ bad_decoration_on_invalid_null.yml
│        │  │  │     ├─ bad_empty_defaults.yml
│        │  │  │     ├─ bad_empty_instanceof.yml
│        │  │  │     ├─ bad_factory_syntax.yml
│        │  │  │     ├─ bad_format.yml
│        │  │  │     ├─ bad_import.yml
│        │  │  │     ├─ bad_imports.yml
│        │  │  │     ├─ bad_keyword.yml
│        │  │  │     ├─ bad_parameters.yml
│        │  │  │     ├─ bad_parent.yml
│        │  │  │     ├─ bad_service.yml
│        │  │  │     ├─ bad_services.yml
│        │  │  │     ├─ bar
│        │  │  │     │  └─ services.yml
│        │  │  │     ├─ class_from_id.yml
│        │  │  │     ├─ closure.yml
│        │  │  │     ├─ constructor_with_factory.yml
│        │  │  │     ├─ defaults_bindings.yml
│        │  │  │     ├─ defaults_bindings2.yml
│        │  │  │     ├─ deprecated_alias_definitions.yml
│        │  │  │     ├─ deprecated_alias_definitions_without_package_and_version.yml
│        │  │  │     ├─ deprecated_definition_without_message.yml
│        │  │  │     ├─ foo
│        │  │  │     │  └─ services.yml
│        │  │  │     ├─ from_callable.yml
│        │  │  │     ├─ integration
│        │  │  │     │  ├─ autoconfigure_child_not_applied
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  ├─ main.yml
│        │  │  │     │  │  └─ _child.yml
│        │  │  │     │  ├─ autoconfigure_parent_child
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  ├─ main.yml
│        │  │  │     │  │  └─ _child.yml
│        │  │  │     │  ├─ autoconfigure_parent_child_tags
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  ├─ main.yml
│        │  │  │     │  │  └─ _child.yml
│        │  │  │     │  ├─ child_parent
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  └─ main.yml
│        │  │  │     │  ├─ defaults_child_tags
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  └─ main.yml
│        │  │  │     │  ├─ defaults_instanceof_importance
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  └─ main.yml
│        │  │  │     │  ├─ defaults_parent_child
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  ├─ main.yml
│        │  │  │     │  │  └─ _child.yml
│        │  │  │     │  ├─ instanceof_and_calls
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  └─ main.yml
│        │  │  │     │  └─ instanceof_parent_child
│        │  │  │     │     ├─ expected.yml
│        │  │  │     │     ├─ main.yml
│        │  │  │     │     └─ _child.yml
│        │  │  │     ├─ nonvalid1.yml
│        │  │  │     ├─ nonvalid2.yml
│        │  │  │     ├─ not_singly_implemented_interface_in_multiple_resources.yml
│        │  │  │     ├─ not_singly_implemented_interface_in_multiple_resources_with_previously_registered_alias.yml
│        │  │  │     ├─ not_singly_implemented_interface_in_multiple_resources_with_previously_registered_alias2.yml
│        │  │  │     ├─ null_config.yml
│        │  │  │     ├─ returns_clone.yaml
│        │  │  │     ├─ services1.yml
│        │  │  │     ├─ services10.yml
│        │  │  │     ├─ services11.yml
│        │  │  │     ├─ services13.yml
│        │  │  │     ├─ services14.yml
│        │  │  │     ├─ services2.yml
│        │  │  │     ├─ services21.yml
│        │  │  │     ├─ services23.yml
│        │  │  │     ├─ services24.yml
│        │  │  │     ├─ services26.yml
│        │  │  │     ├─ services28.yml
│        │  │  │     ├─ services29.yml
│        │  │  │     ├─ services3.yml
│        │  │  │     ├─ services30.yml
│        │  │  │     ├─ services31_invalid_tags.yml
│        │  │  │     ├─ services34.yml
│        │  │  │     ├─ services4.yml
│        │  │  │     ├─ services4_bad_import.yml
│        │  │  │     ├─ services4_bad_import_file_not_found.yml
│        │  │  │     ├─ services4_bad_import_nonvalid.yml
│        │  │  │     ├─ services4_bad_import_with_errors.yml
│        │  │  │     ├─ services6.yml
│        │  │  │     ├─ services7.yml
│        │  │  │     ├─ services8.yml
│        │  │  │     ├─ services9.yml
│        │  │  │     ├─ services_adawson.yml
│        │  │  │     ├─ services_autoconfigure.yml
│        │  │  │     ├─ services_autoconfigure_with_parent.yml
│        │  │  │     ├─ services_bindings.yml
│        │  │  │     ├─ services_case.yml
│        │  │  │     ├─ services_configurator_short_syntax.yml
│        │  │  │     ├─ services_deep_graph.yml
│        │  │  │     ├─ services_defaults_with_parent.yml
│        │  │  │     ├─ services_dump_load.yml
│        │  │  │     ├─ services_inline.yml
│        │  │  │     ├─ services_instanceof.yml
│        │  │  │     ├─ services_instanceof_with_parent.yml
│        │  │  │     ├─ services_lazy_fqcn.yml
│        │  │  │     ├─ services_named_args.yml
│        │  │  │     ├─ services_not_existing.yml
│        │  │  │     ├─ services_prototype.yml
│        │  │  │     ├─ services_prototype_namespace.yml
│        │  │  │     ├─ services_prototype_namespace_without_resource.yml
│        │  │  │     ├─ services_prototype_with_empty_node.yml
│        │  │  │     ├─ services_prototype_with_null_node.yml
│        │  │  │     ├─ services_short_syntax.yml
│        │  │  │     ├─ services_underscore.yml
│        │  │  │     ├─ services_with_abstract_argument.yml
│        │  │  │     ├─ services_with_array_tags.yml
│        │  │  │     ├─ services_with_default_array.yml
│        │  │  │     ├─ services_with_default_enumeration.yml
│        │  │  │     ├─ services_with_default_object.yml
│        │  │  │     ├─ services_with_enumeration.yml
│        │  │  │     ├─ services_with_enumeration_enum_tag.yml
│        │  │  │     ├─ services_with_invalid_enumeration.yml
│        │  │  │     ├─ services_with_service_closure.yml
│        │  │  │     ├─ services_with_service_locator_argument.yml
│        │  │  │     ├─ services_with_short_service_closure.yml
│        │  │  │     ├─ services_with_tagged_argument.yml
│        │  │  │     ├─ service_instanceof_factory.yml
│        │  │  │     ├─ singly_implemented_interface_in_multiple_resources.yml
│        │  │  │     ├─ stack.yaml
│        │  │  │     ├─ static_constructor.yml
│        │  │  │     ├─ tagged_deprecated.yml
│        │  │  │     ├─ tagged_iterator_optional.yml
│        │  │  │     ├─ tag_array_arguments.yml
│        │  │  │     ├─ tag_name_empty_string.yml
│        │  │  │     ├─ tag_name_no_string.yml
│        │  │  │     ├─ tag_name_only.yml
│        │  │  │     ├─ when-env.yaml
│        │  │  │     └─ yaml_with_wrong_ext.ini
│        │  │  ├─ LazyProxy
│        │  │  │  ├─ Instantiator
│        │  │  │  │  └─ RealServiceInstantiatorTest.php
│        │  │  │  └─ PhpDumper
│        │  │  │     ├─ LazyServiceDumperTest.php
│        │  │  │     └─ NullDumperTest.php
│        │  │  ├─ Loader
│        │  │  │  ├─ ClosureLoaderTest.php
│        │  │  │  ├─ Configurator
│        │  │  │  │  └─ EnvConfiguratorTest.php
│        │  │  │  ├─ DirectoryLoaderTest.php
│        │  │  │  ├─ FileLoaderTest.php
│        │  │  │  ├─ GlobFileLoaderTest.php
│        │  │  │  ├─ IniFileLoaderTest.php
│        │  │  │  ├─ LoaderResolverTest.php
│        │  │  │  ├─ PhpFileLoaderTest.php
│        │  │  │  ├─ XmlFileLoaderTest.php
│        │  │  │  └─ YamlFileLoaderTest.php
│        │  │  ├─ ParameterBag
│        │  │  │  ├─ ContainerBagTest.php
│        │  │  │  ├─ EnvPlaceholderParameterBagTest.php
│        │  │  │  ├─ FrozenParameterBagTest.php
│        │  │  │  └─ ParameterBagTest.php
│        │  │  ├─ ParameterTest.php
│        │  │  ├─ ReferenceTest.php
│        │  │  ├─ ServiceLocatorTest.php
│        │  │  └─ StaticEnvVarLoaderTest.php
│        │  ├─ TypedReference.php
│        │  └─ Variable.php
│        ├─ deprecation-contracts
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ function.php
│        │  ├─ LICENSE
│        │  └─ README.md
│        ├─ dotenv
│        │  ├─ CHANGELOG.md
│        │  ├─ Command
│        │  │  ├─ DebugCommand.php
│        │  │  └─ DotenvDumpCommand.php
│        │  ├─ composer.json
│        │  ├─ Dotenv.php
│        │  ├─ Exception
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ FormatException.php
│        │  │  ├─ FormatExceptionContext.php
│        │  │  └─ PathException.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  └─ Tests
│        │     ├─ Command
│        │     │  ├─ DebugCommandTest.php
│        │     │  ├─ DotenvDumpCommandTest.php
│        │     │  └─ Fixtures
│        │     │     ├─ Scenario1
│        │     │     │  ├─ .env
│        │     │     │  ├─ .env.local
│        │     │     │  ├─ .env.prod.local
│        │     │     │  └─ .env.test
│        │     │     ├─ Scenario2
│        │     │     │  ├─ .env.dist
│        │     │     │  ├─ .env.local.php
│        │     │     │  └─ .env.prod
│        │     │     └─ Scenario3
│        │     │        ├─ .env
│        │     │        └─ .env.dist
│        │     ├─ DotenvTest.php
│        │     └─ fixtures
│        │        └─ file_with_bom
│        ├─ error-handler
│        │  ├─ BufferingLogger.php
│        │  ├─ CHANGELOG.md
│        │  ├─ Command
│        │  │  └─ ErrorDumpCommand.php
│        │  ├─ composer.json
│        │  ├─ Debug.php
│        │  ├─ DebugClassLoader.php
│        │  ├─ Error
│        │  │  ├─ ClassNotFoundError.php
│        │  │  ├─ FatalError.php
│        │  │  ├─ OutOfMemoryError.php
│        │  │  ├─ UndefinedFunctionError.php
│        │  │  └─ UndefinedMethodError.php
│        │  ├─ ErrorEnhancer
│        │  │  ├─ ClassNotFoundErrorEnhancer.php
│        │  │  ├─ ErrorEnhancerInterface.php
│        │  │  ├─ UndefinedFunctionErrorEnhancer.php
│        │  │  └─ UndefinedMethodErrorEnhancer.php
│        │  ├─ ErrorHandler.php
│        │  ├─ ErrorRenderer
│        │  │  ├─ CliErrorRenderer.php
│        │  │  ├─ ErrorRendererInterface.php
│        │  │  ├─ FileLinkFormatter.php
│        │  │  ├─ HtmlErrorRenderer.php
│        │  │  └─ SerializerErrorRenderer.php
│        │  ├─ Exception
│        │  │  ├─ FlattenException.php
│        │  │  └─ SilencedErrorContext.php
│        │  ├─ Internal
│        │  │  └─ TentativeTypes.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Resources
│        │  │  ├─ assets
│        │  │  │  ├─ css
│        │  │  │  │  ├─ error.css
│        │  │  │  │  ├─ exception.css
│        │  │  │  │  └─ exception_full.css
│        │  │  │  ├─ images
│        │  │  │  │  ├─ chevron-right.svg
│        │  │  │  │  ├─ favicon.png.base64
│        │  │  │  │  ├─ icon-book.svg
│        │  │  │  │  ├─ icon-copy.svg
│        │  │  │  │  ├─ icon-minus-square-o.svg
│        │  │  │  │  ├─ icon-minus-square.svg
│        │  │  │  │  ├─ icon-plus-square-o.svg
│        │  │  │  │  ├─ icon-plus-square.svg
│        │  │  │  │  ├─ icon-support.svg
│        │  │  │  │  ├─ symfony-ghost.svg.php
│        │  │  │  │  └─ symfony-logo.svg
│        │  │  │  └─ js
│        │  │  │     └─ exception.js
│        │  │  ├─ bin
│        │  │  │  ├─ extract-tentative-return-types.php
│        │  │  │  └─ patch-type-declarations
│        │  │  └─ views
│        │  │     ├─ error.html.php
│        │  │     ├─ exception.html.php
│        │  │     ├─ exception_full.html.php
│        │  │     ├─ logs.html.php
│        │  │     ├─ trace.html.php
│        │  │     ├─ traces.html.php
│        │  │     └─ traces_text.html.php
│        │  ├─ Tests
│        │  │  ├─ Command
│        │  │  │  └─ ErrorDumpCommandTest.php
│        │  │  ├─ DebugClassLoaderTest.php
│        │  │  ├─ ErrorEnhancer
│        │  │  │  ├─ ClassNotFoundErrorEnhancerTest.php
│        │  │  │  ├─ UndefinedFunctionErrorEnhancerTest.php
│        │  │  │  └─ UndefinedMethodErrorEnhancerTest.php
│        │  │  ├─ ErrorHandlerTest.php
│        │  │  ├─ ErrorRenderer
│        │  │  │  ├─ FileLinkFormatterTest.php
│        │  │  │  ├─ HtmlErrorRendererTest.php
│        │  │  │  └─ SerializerErrorRendererTest.php
│        │  │  ├─ Exception
│        │  │  │  └─ FlattenExceptionTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ AnnotatedClass.php
│        │  │  │  ├─ casemismatch.php
│        │  │  │  ├─ ClassAlias.php
│        │  │  │  ├─ ClassWithAnnotatedParameters.php
│        │  │  │  ├─ DefinitionInEvaluatedCode.php
│        │  │  │  ├─ DeprecatedClass.php
│        │  │  │  ├─ DeprecatedInterface.php
│        │  │  │  ├─ ErrorHandlerThatUsesThePreviousOne.php
│        │  │  │  ├─ ExtendedFinalMethod.php
│        │  │  │  ├─ FinalClasses.php
│        │  │  │  ├─ FinalConstant
│        │  │  │  │  ├─ FinalConstants.php
│        │  │  │  │  ├─ FinalConstants2.php
│        │  │  │  │  ├─ FinalConstantsInterface.php
│        │  │  │  │  ├─ FinalConstantsInterface2.php
│        │  │  │  │  ├─ OverrideFinalConstant.php
│        │  │  │  │  └─ OverrideFinalConstant81.php
│        │  │  │  ├─ FinalMethod.php
│        │  │  │  ├─ FinalMethod2Trait.php
│        │  │  │  ├─ FinalProperty
│        │  │  │  │  ├─ FinalProperty.php
│        │  │  │  │  ├─ OutsideFinalProperty.php
│        │  │  │  │  └─ OverrideFinalPropertySameNamespace.php
│        │  │  │  ├─ InterfaceWithAnnotatedParameters.php
│        │  │  │  ├─ InternalClass.php
│        │  │  │  ├─ InternalInterface.php
│        │  │  │  ├─ InternalTrait.php
│        │  │  │  ├─ InternalTrait2.php
│        │  │  │  ├─ LoggerThatSetAnErrorHandler.php
│        │  │  │  ├─ NonDeprecatedInterface.php
│        │  │  │  ├─ notPsr0Bis.php
│        │  │  │  ├─ OutsideInterface.php
│        │  │  │  ├─ OverrideFinalProperty.php
│        │  │  │  ├─ OverrideOutsideFinalProperty.php
│        │  │  │  ├─ PEARClass.php
│        │  │  │  ├─ pixel.png
│        │  │  │  ├─ psr4
│        │  │  │  │  └─ Psr4CaseMismatch.php
│        │  │  │  ├─ reallyNotPsr0.php
│        │  │  │  ├─ ReturnType.php
│        │  │  │  ├─ ReturnTypeGrandParent.php
│        │  │  │  ├─ ReturnTypeInterface.php
│        │  │  │  ├─ ReturnTypeParent.php
│        │  │  │  ├─ ReturnTypeParentInterface.php
│        │  │  │  ├─ ReturnTypeParentPhp83.php
│        │  │  │  ├─ ReturnTypePhp83.php
│        │  │  │  ├─ StringErrorCodeException.php
│        │  │  │  ├─ SubClassWithAnnotatedParameters.php
│        │  │  │  ├─ Throwing.php
│        │  │  │  ├─ TraitWithAnnotatedParameters.php
│        │  │  │  ├─ TraitWithInternalMethod.php
│        │  │  │  ├─ VirtualClass.php
│        │  │  │  ├─ VirtualClassMagicCall.php
│        │  │  │  ├─ VirtualInterface.php
│        │  │  │  ├─ VirtualSubInterface.php
│        │  │  │  └─ VirtualTrait.php
│        │  │  ├─ Fixtures2
│        │  │  │  └─ RequiredTwice.php
│        │  │  ├─ HeaderMock.php
│        │  │  └─ phpt
│        │  │     ├─ debug_class_loader.phpt
│        │  │     ├─ decorate_exception_handler.phpt
│        │  │     ├─ exception_rethrown.phpt
│        │  │     └─ fatal_with_nested_handlers.phpt
│        │  └─ ThrowableUtils.php
│        ├─ event-dispatcher
│        │  ├─ Attribute
│        │  │  └─ AsEventListener.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ Debug
│        │  │  ├─ TraceableEventDispatcher.php
│        │  │  └─ WrappedListener.php
│        │  ├─ DependencyInjection
│        │  │  ├─ AddEventAliasesPass.php
│        │  │  └─ RegisterListenersPass.php
│        │  ├─ EventDispatcher.php
│        │  ├─ EventDispatcherInterface.php
│        │  ├─ EventSubscriberInterface.php
│        │  ├─ GenericEvent.php
│        │  ├─ ImmutableEventDispatcher.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  └─ Tests
│        │     ├─ ChildEventDispatcherTest.php
│        │     ├─ Debug
│        │     │  ├─ TraceableEventDispatcherTest.php
│        │     │  └─ WrappedListenerTest.php
│        │     ├─ DependencyInjection
│        │     │  └─ RegisterListenersPassTest.php
│        │     ├─ EventDispatcherTest.php
│        │     ├─ Fixtures
│        │     │  ├─ CustomEvent.php
│        │     │  ├─ TaggedInvokableListener.php
│        │     │  └─ TaggedMultiListener.php
│        │     ├─ GenericEventTest.php
│        │     └─ ImmutableEventDispatcherTest.php
│        ├─ event-dispatcher-contracts
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ Event.php
│        │  ├─ EventDispatcherInterface.php
│        │  ├─ LICENSE
│        │  └─ README.md
│        ├─ filesystem
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ Exception
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ FileNotFoundException.php
│        │  │  ├─ InvalidArgumentException.php
│        │  │  ├─ IOException.php
│        │  │  ├─ IOExceptionInterface.php
│        │  │  └─ RuntimeException.php
│        │  ├─ Filesystem.php
│        │  ├─ LICENSE
│        │  ├─ Path.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  └─ Tests
│        │     ├─ ExceptionTest.php
│        │     ├─ FilesystemTest.php
│        │     ├─ FilesystemTestCase.php
│        │     ├─ Fixtures
│        │     │  ├─ MockStream
│        │     │  │  └─ MockStream.php
│        │     │  └─ web
│        │     │     ├─ index.php
│        │     │     └─ logo_symfony_header.png
│        │     └─ PathTest.php
│        ├─ finder
│        │  ├─ CHANGELOG.md
│        │  ├─ Comparator
│        │  │  ├─ Comparator.php
│        │  │  ├─ DateComparator.php
│        │  │  └─ NumberComparator.php
│        │  ├─ composer.json
│        │  ├─ Exception
│        │  │  ├─ AccessDeniedException.php
│        │  │  └─ DirectoryNotFoundException.php
│        │  ├─ Finder.php
│        │  ├─ Gitignore.php
│        │  ├─ Glob.php
│        │  ├─ Iterator
│        │  │  ├─ CustomFilterIterator.php
│        │  │  ├─ DateRangeFilterIterator.php
│        │  │  ├─ DepthRangeFilterIterator.php
│        │  │  ├─ ExcludeDirectoryFilterIterator.php
│        │  │  ├─ FilecontentFilterIterator.php
│        │  │  ├─ FilenameFilterIterator.php
│        │  │  ├─ FileTypeFilterIterator.php
│        │  │  ├─ LazyIterator.php
│        │  │  ├─ MultiplePcreFilterIterator.php
│        │  │  ├─ PathFilterIterator.php
│        │  │  ├─ RecursiveDirectoryIterator.php
│        │  │  ├─ SizeRangeFilterIterator.php
│        │  │  ├─ SortableIterator.php
│        │  │  └─ VcsIgnoredFilterIterator.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ SplFileInfo.php
│        │  └─ Tests
│        │     ├─ Comparator
│        │     │  ├─ ComparatorTest.php
│        │     │  ├─ DateComparatorTest.php
│        │     │  └─ NumberComparatorTest.php
│        │     ├─ FinderOpenBasedirTest.php
│        │     ├─ FinderTest.php
│        │     ├─ Fixtures
│        │     │  ├─ .dot
│        │     │  │  ├─ a
│        │     │  │  └─ b
│        │     │  │     ├─ c.neon
│        │     │  │     └─ d.neon
│        │     │  ├─ A
│        │     │  │  ├─ a.dat
│        │     │  │  └─ B
│        │     │  │     ├─ ab.dat
│        │     │  │     └─ C
│        │     │  │        └─ abc.dat
│        │     │  ├─ copy
│        │     │  │  └─ A
│        │     │  │     ├─ a.dat.copy
│        │     │  │     └─ B
│        │     │  │        ├─ ab.dat.copy
│        │     │  │        └─ C
│        │     │  │           └─ abc.dat.copy
│        │     │  ├─ dolor.txt
│        │     │  ├─ gitignore
│        │     │  │  ├─ git_root
│        │     │  │  │  └─ search_root
│        │     │  │  │     ├─ b.txt
│        │     │  │  │     └─ dir
│        │     │  │  │        └─ a.txt
│        │     │  │  └─ search_root
│        │     │  │     ├─ a.txt
│        │     │  │     ├─ b.txt
│        │     │  │     ├─ c.txt
│        │     │  │     └─ dir
│        │     │  │        ├─ a.txt
│        │     │  │        ├─ b.txt
│        │     │  │        └─ c.txt
│        │     │  ├─ ipsum.txt
│        │     │  ├─ lorem.txt
│        │     │  ├─ one
│        │     │  │  ├─ .dot
│        │     │  │  ├─ a
│        │     │  │  └─ b
│        │     │  │     ├─ c.neon
│        │     │  │     └─ d.neon
│        │     │  ├─ r+e.gex[c]a(r)s
│        │     │  │  └─ dir
│        │     │  │     └─ bar.dat
│        │     │  └─ with space
│        │     │     └─ foo.txt
│        │     ├─ GitignoreTest.php
│        │     ├─ GlobTest.php
│        │     └─ Iterator
│        │        ├─ CustomFilterIteratorTest.php
│        │        ├─ DateRangeFilterIteratorTest.php
│        │        ├─ DepthRangeFilterIteratorTest.php
│        │        ├─ ExcludeDirectoryFilterIteratorTest.php
│        │        ├─ FilecontentFilterIteratorTest.php
│        │        ├─ FilenameFilterIteratorTest.php
│        │        ├─ FileTypeFilterIteratorTest.php
│        │        ├─ InnerNameIterator.php
│        │        ├─ Iterator.php
│        │        ├─ IteratorTestCase.php
│        │        ├─ LazyIteratorTest.php
│        │        ├─ MockFileListIterator.php
│        │        ├─ MockSplFileInfo.php
│        │        ├─ MultiplePcreFilterIteratorTest.php
│        │        ├─ PathFilterIteratorTest.php
│        │        ├─ RealIteratorTestCase.php
│        │        ├─ RecursiveDirectoryIteratorTest.php
│        │        ├─ SizeRangeFilterIteratorTest.php
│        │        ├─ SortableIteratorTest.php
│        │        ├─ VcsIgnoredFilterIteratorTest.php
│        │        └─ VfsIteratorTestTrait.php
│        ├─ flex
│        │  ├─ .php-cs-fixer.dist.php
│        │  ├─ composer.json
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ src
│        │  │  ├─ Command
│        │  │  │  ├─ DumpEnvCommand.php
│        │  │  │  ├─ InstallRecipesCommand.php
│        │  │  │  ├─ RecipesCommand.php
│        │  │  │  └─ UpdateRecipesCommand.php
│        │  │  ├─ Configurator
│        │  │  │  ├─ AbstractConfigurator.php
│        │  │  │  ├─ AddLinesConfigurator.php
│        │  │  │  ├─ BundlesConfigurator.php
│        │  │  │  ├─ ComposerCommandsConfigurator.php
│        │  │  │  ├─ ComposerScriptsConfigurator.php
│        │  │  │  ├─ ContainerConfigurator.php
│        │  │  │  ├─ CopyFromPackageConfigurator.php
│        │  │  │  ├─ CopyFromRecipeConfigurator.php
│        │  │  │  ├─ DockerComposeConfigurator.php
│        │  │  │  ├─ DockerfileConfigurator.php
│        │  │  │  ├─ DotenvConfigurator.php
│        │  │  │  ├─ EnvConfigurator.php
│        │  │  │  ├─ GitignoreConfigurator.php
│        │  │  │  └─ MakefileConfigurator.php
│        │  │  ├─ Configurator.php
│        │  │  ├─ Downloader.php
│        │  │  ├─ Event
│        │  │  │  └─ UpdateEvent.php
│        │  │  ├─ Flex.php
│        │  │  ├─ GithubApi.php
│        │  │  ├─ InformationOperation.php
│        │  │  ├─ Lock.php
│        │  │  ├─ Options.php
│        │  │  ├─ PackageFilter.php
│        │  │  ├─ PackageJsonSynchronizer.php
│        │  │  ├─ PackageResolver.php
│        │  │  ├─ Path.php
│        │  │  ├─ Recipe.php
│        │  │  ├─ Response.php
│        │  │  ├─ ScriptExecutor.php
│        │  │  ├─ SymfonyBundle.php
│        │  │  ├─ SymfonyPackInstaller.php
│        │  │  ├─ Unpack
│        │  │  │  ├─ Operation.php
│        │  │  │  └─ Result.php
│        │  │  ├─ Unpacker.php
│        │  │  └─ Update
│        │  │     ├─ DiffHelper.php
│        │  │     ├─ RecipePatch.php
│        │  │     ├─ RecipePatcher.php
│        │  │     └─ RecipeUpdate.php
│        │  └─ tests
│        │     ├─ bootstrap.php
│        │     ├─ Command
│        │     │  ├─ DumpEnvCommandTest.php
│        │     │  ├─ InstallRecipesCommandTest.php
│        │     │  └─ UpdateRecipesCommandTest.php
│        │     ├─ Configurator
│        │     │  ├─ AddLinesConfiguratorTest.php
│        │     │  ├─ BundlesConfiguratorTest.php
│        │     │  ├─ ComposerCommandConfiguratorTest.php
│        │     │  ├─ ComposerScriptsConfiguratorTest.php
│        │     │  ├─ ContainerConfiguratorTest.php
│        │     │  ├─ CopyDirectoryFromPackageConfiguratorTest.php
│        │     │  ├─ CopyFromPackageConfiguratorTest.php
│        │     │  ├─ CopyFromRecipeConfiguratorTest.php
│        │     │  ├─ DockerComposeConfiguratorTest.php
│        │     │  ├─ DockerfileConfiguratorTest.php
│        │     │  ├─ DotenvConfiguratorTest.php
│        │     │  ├─ EnvConfiguratorTest.php
│        │     │  ├─ GitignoreConfiguratorTest.php
│        │     │  └─ MakefileConfiguratorTest.php
│        │     ├─ Fixtures
│        │     │  ├─ packageJson
│        │     │  │  ├─ assets
│        │     │  │  │  └─ controllers.json
│        │     │  │  ├─ elevated_dependencies_package.json
│        │     │  │  ├─ package.json
│        │     │  │  ├─ stricter_constraints_package.json
│        │     │  │  └─ vendor
│        │     │  │     └─ symfony
│        │     │  │        ├─ existing-package
│        │     │  │        │  └─ Resources
│        │     │  │        │     └─ assets
│        │     │  │        │        └─ package.json
│        │     │  │        ├─ importmap-invalid-constraint-package
│        │     │  │        │  └─ assets
│        │     │  │        │     └─ package.json
│        │     │  │        ├─ new-package
│        │     │  │        │  └─ assets
│        │     │  │        │     └─ package.json
│        │     │  │        └─ package-no-file-package
│        │     │  │           └─ assets
│        │     │  │              └─ package.json
│        │     │  ├─ phpunit.xml.dist
│        │     │  ├─ update_recipes
│        │     │  │  ├─ composer.json
│        │     │  │  ├─ console
│        │     │  │  └─ symfony.lock
│        │     │  └─ vendor
│        │     │     ├─ composer
│        │     │     │  └─ ca-bundle
│        │     │     │     └─ src
│        │     │     │        └─ CaBundle.php
│        │     │     ├─ doctrine
│        │     │     │  └─ doctrine-cache-bundle
│        │     │     │     └─ DoctrineCacheBundle.php
│        │     │     ├─ dunglas
│        │     │     │  └─ sylius-acme-plugin
│        │     │     │     └─ src
│        │     │     │        └─ DunglasSyliusAcmePlugin.php
│        │     │     ├─ easycorp
│        │     │     │  ├─ easy-deploy-bundle
│        │     │     │  │  └─ src
│        │     │     │  │     └─ EasyDeployBundle.php
│        │     │     │  └─ easy-security-bundle
│        │     │     │     └─ EasySecurityBundle.php
│        │     │     ├─ eightpoints
│        │     │     │  └─ guzzle-bundle
│        │     │     │     └─ EightPoints
│        │     │     │        └─ Bundle
│        │     │     │           └─ GuzzleBundle
│        │     │     │              └─ GuzzleBundle.php
│        │     │     ├─ sylius
│        │     │     │  └─ shop-api-plugin
│        │     │     │     └─ src
│        │     │     │        └─ ShopApiPlugin.php
│        │     │     ├─ symfony
│        │     │     │  ├─ debug-bundle
│        │     │     │  │  └─ DebugBundle.php
│        │     │     │  ├─ dummy
│        │     │     │  │  ├─ FirstDummyBundle
│        │     │     │  │  │  └─ FirstDummyBundle.php
│        │     │     │  │  └─ SecondDummyBundle
│        │     │     │  │     └─ SecondDummyBundle.php
│        │     │     │  └─ nouse-bundle
│        │     │     │     └─ NouseBundle.php
│        │     │     ├─ symfony-cmf
│        │     │     │  └─ routing-bundle
│        │     │     │     └─ CmfRoutingBundle.php
│        │     │     └─ web-token
│        │     │        └─ jwt-bundle
│        │     │           └─ JoseFrameworkBundle.php
│        │     ├─ FlexTest.php
│        │     ├─ OptionsTest.php
│        │     ├─ PackageFilterTest.php
│        │     ├─ PackageJsonSynchronizerTest.php
│        │     ├─ PackageResolverTest.php
│        │     ├─ PathTest.php
│        │     ├─ ScriptExecutorTest.php
│        │     ├─ SymfonyBundleTest.php
│        │     ├─ UnpackerTest.php
│        │     └─ Update
│        │        ├─ DiffHelperTest.php
│        │        ├─ RecipePatcherTest.php
│        │        ├─ RecipePatchTest.php
│        │        └─ RecipeUpdateTest.php
│        ├─ framework-bundle
│        │  ├─ CacheWarmer
│        │  │  ├─ AbstractPhpFileCacheWarmer.php
│        │  │  ├─ CachePoolClearerCacheWarmer.php
│        │  │  ├─ ConfigBuilderCacheWarmer.php
│        │  │  ├─ RouterCacheWarmer.php
│        │  │  ├─ SerializerCacheWarmer.php
│        │  │  ├─ TranslationsCacheWarmer.php
│        │  │  └─ ValidatorCacheWarmer.php
│        │  ├─ CHANGELOG.md
│        │  ├─ Command
│        │  │  ├─ AboutCommand.php
│        │  │  ├─ AbstractConfigCommand.php
│        │  │  ├─ AssetsInstallCommand.php
│        │  │  ├─ BuildDebugContainerTrait.php
│        │  │  ├─ CacheClearCommand.php
│        │  │  ├─ CachePoolClearCommand.php
│        │  │  ├─ CachePoolDeleteCommand.php
│        │  │  ├─ CachePoolInvalidateTagsCommand.php
│        │  │  ├─ CachePoolListCommand.php
│        │  │  ├─ CachePoolPruneCommand.php
│        │  │  ├─ CacheWarmupCommand.php
│        │  │  ├─ ConfigDebugCommand.php
│        │  │  ├─ ConfigDumpReferenceCommand.php
│        │  │  ├─ ContainerDebugCommand.php
│        │  │  ├─ ContainerLintCommand.php
│        │  │  ├─ DebugAutowiringCommand.php
│        │  │  ├─ EventDispatcherDebugCommand.php
│        │  │  ├─ RouterDebugCommand.php
│        │  │  ├─ RouterMatchCommand.php
│        │  │  ├─ SecretsDecryptToLocalCommand.php
│        │  │  ├─ SecretsEncryptFromLocalCommand.php
│        │  │  ├─ SecretsGenerateKeysCommand.php
│        │  │  ├─ SecretsListCommand.php
│        │  │  ├─ SecretsRemoveCommand.php
│        │  │  ├─ SecretsRevealCommand.php
│        │  │  ├─ SecretsSetCommand.php
│        │  │  ├─ TranslationDebugCommand.php
│        │  │  ├─ TranslationExtractCommand.php
│        │  │  ├─ TranslationUpdateCommand.php
│        │  │  ├─ WorkflowDumpCommand.php
│        │  │  ├─ XliffLintCommand.php
│        │  │  └─ YamlLintCommand.php
│        │  ├─ composer.json
│        │  ├─ Console
│        │  │  ├─ Application.php
│        │  │  ├─ Descriptor
│        │  │  │  ├─ Descriptor.php
│        │  │  │  ├─ JsonDescriptor.php
│        │  │  │  ├─ MarkdownDescriptor.php
│        │  │  │  ├─ TextDescriptor.php
│        │  │  │  └─ XmlDescriptor.php
│        │  │  └─ Helper
│        │  │     └─ DescriptorHelper.php
│        │  ├─ Controller
│        │  │  ├─ AbstractController.php
│        │  │  ├─ ControllerResolver.php
│        │  │  ├─ RedirectController.php
│        │  │  └─ TemplateController.php
│        │  ├─ DataCollector
│        │  │  ├─ AbstractDataCollector.php
│        │  │  ├─ RouterDataCollector.php
│        │  │  └─ TemplateAwareDataCollectorInterface.php
│        │  ├─ DependencyInjection
│        │  │  ├─ Compiler
│        │  │  │  ├─ AddDebugLogProcessorPass.php
│        │  │  │  ├─ AssetsContextPass.php
│        │  │  │  ├─ ContainerBuilderDebugDumpPass.php
│        │  │  │  ├─ ErrorLoggerCompilerPass.php
│        │  │  │  ├─ ProfilerPass.php
│        │  │  │  ├─ RemoveUnusedSessionMarshallingHandlerPass.php
│        │  │  │  ├─ TestServiceContainerRealRefPass.php
│        │  │  │  ├─ TestServiceContainerWeakRefPass.php
│        │  │  │  ├─ TranslationLintCommandPass.php
│        │  │  │  ├─ TranslationUpdateCommandPass.php
│        │  │  │  └─ UnusedTagsPass.php
│        │  │  ├─ Configuration.php
│        │  │  ├─ FrameworkExtension.php
│        │  │  └─ VirtualRequestStackPass.php
│        │  ├─ EventListener
│        │  │  ├─ ConsoleProfilerListener.php
│        │  │  └─ SuggestMissingPackageSubscriber.php
│        │  ├─ FrameworkBundle.php
│        │  ├─ HttpCache
│        │  │  └─ HttpCache.php
│        │  ├─ Kernel
│        │  │  └─ MicroKernelTrait.php
│        │  ├─ KernelBrowser.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Resources
│        │  │  ├─ bin
│        │  │  │  └─ check-unused-known-tags.php
│        │  │  └─ config
│        │  │     ├─ assets.php
│        │  │     ├─ asset_mapper.php
│        │  │     ├─ cache.php
│        │  │     ├─ cache_debug.php
│        │  │     ├─ collectors.php
│        │  │     ├─ console.php
│        │  │     ├─ debug.php
│        │  │     ├─ debug_prod.php
│        │  │     ├─ error_renderer.php
│        │  │     ├─ esi.php
│        │  │     ├─ form.php
│        │  │     ├─ form_csrf.php
│        │  │     ├─ form_debug.php
│        │  │     ├─ fragment_listener.php
│        │  │     ├─ fragment_renderer.php
│        │  │     ├─ html_sanitizer.php
│        │  │     ├─ http_client.php
│        │  │     ├─ http_client_debug.php
│        │  │     ├─ identity_translator.php
│        │  │     ├─ json_streamer.php
│        │  │     ├─ lock.php
│        │  │     ├─ mailer.php
│        │  │     ├─ mailer_debug.php
│        │  │     ├─ mailer_transports.php
│        │  │     ├─ mailer_webhook.php
│        │  │     ├─ messenger.php
│        │  │     ├─ messenger_debug.php
│        │  │     ├─ mime_type.php
│        │  │     ├─ notifier.php
│        │  │     ├─ notifier_debug.php
│        │  │     ├─ notifier_transports.php
│        │  │     ├─ notifier_webhook.php
│        │  │     ├─ object_mapper.php
│        │  │     ├─ process.php
│        │  │     ├─ profiling.php
│        │  │     ├─ property_access.php
│        │  │     ├─ property_info.php
│        │  │     ├─ rate_limiter.php
│        │  │     ├─ remote_event.php
│        │  │     ├─ request.php
│        │  │     ├─ routing
│        │  │     │  ├─ errors.php
│        │  │     │  ├─ errors.xml
│        │  │     │  ├─ webhook.php
│        │  │     │  └─ webhook.xml
│        │  │     ├─ routing.php
│        │  │     ├─ scheduler.php
│        │  │     ├─ schema
│        │  │     │  └─ symfony-1.0.xsd
│        │  │     ├─ secrets.php
│        │  │     ├─ security_csrf.php
│        │  │     ├─ semaphore.php
│        │  │     ├─ serializer.php
│        │  │     ├─ serializer_debug.php
│        │  │     ├─ services.php
│        │  │     ├─ session.php
│        │  │     ├─ ssi.php
│        │  │     ├─ test.php
│        │  │     ├─ translation.php
│        │  │     ├─ translation_debug.php
│        │  │     ├─ translation_providers.php
│        │  │     ├─ type_info.php
│        │  │     ├─ uid.php
│        │  │     ├─ validator.php
│        │  │     ├─ validator_debug.php
│        │  │     ├─ web.php
│        │  │     ├─ webhook.php
│        │  │     ├─ web_link.php
│        │  │     ├─ workflow.php
│        │  │     └─ workflow_debug.php
│        │  ├─ Routing
│        │  │  ├─ Attribute
│        │  │  │  └─ AsRoutingConditionService.php
│        │  │  ├─ AttributeRouteControllerLoader.php
│        │  │  ├─ DelegatingLoader.php
│        │  │  ├─ RedirectableCompiledUrlMatcher.php
│        │  │  ├─ RouteLoaderInterface.php
│        │  │  └─ Router.php
│        │  ├─ Secrets
│        │  │  ├─ AbstractVault.php
│        │  │  ├─ DotenvVault.php
│        │  │  └─ SodiumVault.php
│        │  ├─ Test
│        │  │  ├─ BrowserKitAssertionsTrait.php
│        │  │  ├─ DomCrawlerAssertionsTrait.php
│        │  │  ├─ HttpClientAssertionsTrait.php
│        │  │  ├─ KernelTestCase.php
│        │  │  ├─ MailerAssertionsTrait.php
│        │  │  ├─ NotificationAssertionsTrait.php
│        │  │  ├─ TestBrowserToken.php
│        │  │  ├─ TestContainer.php
│        │  │  ├─ WebTestAssertionsTrait.php
│        │  │  └─ WebTestCase.php
│        │  ├─ Tests
│        │  │  ├─ CacheWarmer
│        │  │  │  ├─ ConfigBuilderCacheWarmerTest.php
│        │  │  │  ├─ RouterCacheWarmerTest.php
│        │  │  │  ├─ SerializerCacheWarmerTest.php
│        │  │  │  └─ ValidatorCacheWarmerTest.php
│        │  │  ├─ Command
│        │  │  │  ├─ AboutCommand
│        │  │  │  │  ├─ AboutCommandTest.php
│        │  │  │  │  └─ Fixture
│        │  │  │  │     └─ TestAppKernel.php
│        │  │  │  ├─ CacheClearCommand
│        │  │  │  │  ├─ CacheClearCommandTest.php
│        │  │  │  │  └─ Fixture
│        │  │  │  │     ├─ config.yml
│        │  │  │  │     └─ TestAppKernel.php
│        │  │  │  ├─ CachePoolClearCommandTest.php
│        │  │  │  ├─ CachePoolDeleteCommandTest.php
│        │  │  │  ├─ CachePoolInvalidateTagsCommandTest.php
│        │  │  │  ├─ CachePruneCommandTest.php
│        │  │  │  ├─ EventDispatcherDebugCommandTest.php
│        │  │  │  ├─ RouterMatchCommandTest.php
│        │  │  │  ├─ SecretsListCommandTest.php
│        │  │  │  ├─ SecretsRemoveCommandTest.php
│        │  │  │  ├─ SecretsRevealCommandTest.php
│        │  │  │  ├─ SecretsSetCommandTest.php
│        │  │  │  ├─ TranslationDebugCommandTest.php
│        │  │  │  ├─ TranslationExtractCommandCompletionTest.php
│        │  │  │  ├─ TranslationExtractCommandTest.php
│        │  │  │  ├─ WorkflowDumpCommandTest.php
│        │  │  │  ├─ XliffLintCommandTest.php
│        │  │  │  └─ YamlLintCommandTest.php
│        │  │  ├─ Console
│        │  │  │  ├─ ApplicationTest.php
│        │  │  │  └─ Descriptor
│        │  │  │     ├─ AbstractDescriptorTestCase.php
│        │  │  │     ├─ JsonDescriptorTest.php
│        │  │  │     ├─ MarkdownDescriptorTest.php
│        │  │  │     ├─ ObjectsProvider.php
│        │  │  │     ├─ TextDescriptorTest.php
│        │  │  │     └─ XmlDescriptorTest.php
│        │  │  ├─ Controller
│        │  │  │  ├─ AbstractControllerTest.php
│        │  │  │  ├─ ControllerResolverTest.php
│        │  │  │  ├─ RedirectControllerTest.php
│        │  │  │  ├─ TemplateControllerTest.php
│        │  │  │  └─ TestAbstractController.php
│        │  │  ├─ DataCollector
│        │  │  │  └─ RouterDataCollectorTest.php
│        │  │  ├─ DependencyInjection
│        │  │  │  ├─ Compiler
│        │  │  │  │  ├─ ProfilerPassTest.php
│        │  │  │  │  ├─ TestServiceContainerRefPassesTest.php
│        │  │  │  │  ├─ UnusedTagsPassTest.php
│        │  │  │  │  └─ UnusedTagsPassUtils.php
│        │  │  │  ├─ config
│        │  │  │  │  ├─ serializer
│        │  │  │  │  │  └─ foo.yml
│        │  │  │  │  └─ validator
│        │  │  │  │     └─ foo.xml
│        │  │  │  ├─ ConfigurationTest.php
│        │  │  │  ├─ Fixtures
│        │  │  │  │  ├─ CustomPathBundle
│        │  │  │  │  │  ├─ Resources
│        │  │  │  │  │  │  └─ config
│        │  │  │  │  │  │     ├─ validation.xml
│        │  │  │  │  │  │     └─ validation.yml
│        │  │  │  │  │  └─ src
│        │  │  │  │  │     └─ CustomPathBundle.php
│        │  │  │  │  ├─ php
│        │  │  │  │  │  ├─ assets.php
│        │  │  │  │  │  ├─ assets_disabled.php
│        │  │  │  │  │  ├─ assets_version_strategy_as_service.php
│        │  │  │  │  │  ├─ asset_mapper_without_assets.php
│        │  │  │  │  │  ├─ cache.php
│        │  │  │  │  │  ├─ cache_app_redis_tag_aware.php
│        │  │  │  │  │  ├─ cache_app_redis_tag_aware_pool.php
│        │  │  │  │  │  ├─ csrf.php
│        │  │  │  │  │  ├─ csrf_needs_session.php
│        │  │  │  │  │  ├─ default_config.php
│        │  │  │  │  │  ├─ esi_and_ssi_without_fragments.php
│        │  │  │  │  │  ├─ esi_disabled.php
│        │  │  │  │  │  ├─ exceptions.php
│        │  │  │  │  │  ├─ form_csrf_disabled.php
│        │  │  │  │  │  ├─ form_csrf_field_attr.php
│        │  │  │  │  │  ├─ form_default_csrf.php
│        │  │  │  │  │  ├─ form_no_csrf.php
│        │  │  │  │  │  ├─ fragments_and_hinclude.php
│        │  │  │  │  │  ├─ full.php
│        │  │  │  │  │  ├─ html_sanitizer.php
│        │  │  │  │  │  ├─ html_sanitizer_default_allowed_link_and_media_hosts.php
│        │  │  │  │  │  ├─ html_sanitizer_default_config.php
│        │  │  │  │  │  ├─ http_client_default_options.php
│        │  │  │  │  │  ├─ http_client_full_default_options.php
│        │  │  │  │  │  ├─ http_client_mock_response_factory.php
│        │  │  │  │  │  ├─ http_client_override_default_options.php
│        │  │  │  │  │  ├─ http_client_rate_limiter.php
│        │  │  │  │  │  ├─ http_client_retry.php
│        │  │  │  │  │  ├─ http_client_scoped_without_query_option.php
│        │  │  │  │  │  ├─ http_client_xml_key.php
│        │  │  │  │  │  ├─ json_streamer.php
│        │  │  │  │  │  ├─ lock.php
│        │  │  │  │  │  ├─ lock_named.php
│        │  │  │  │  │  ├─ lock_service.php
│        │  │  │  │  │  ├─ mailer.php
│        │  │  │  │  │  ├─ mailer_with_disabled_message_bus.php
│        │  │  │  │  │  ├─ mailer_with_dsn.php
│        │  │  │  │  │  ├─ mailer_with_specific_message_bus.php
│        │  │  │  │  │  ├─ mailer_with_transports.php
│        │  │  │  │  │  ├─ messenger.php
│        │  │  │  │  │  ├─ messenger_disabled.php
│        │  │  │  │  │  ├─ messenger_middleware_factory_erroneous_format.php
│        │  │  │  │  │  ├─ messenger_multiple_buses_without_deduplicate_middleware.php
│        │  │  │  │  │  ├─ messenger_multiple_buses_with_deduplicate_middleware.php
│        │  │  │  │  │  ├─ messenger_multiple_failure_transports.php
│        │  │  │  │  │  ├─ messenger_multiple_failure_transports_global.php
│        │  │  │  │  │  ├─ messenger_routing.php
│        │  │  │  │  │  ├─ messenger_routing_invalid_transport.php
│        │  │  │  │  │  ├─ messenger_routing_invalid_wildcard.php
│        │  │  │  │  │  ├─ messenger_routing_single.php
│        │  │  │  │  │  ├─ messenger_transport.php
│        │  │  │  │  │  ├─ messenger_transports.php
│        │  │  │  │  │  ├─ notifier.php
│        │  │  │  │  │  ├─ notifier_without_mailer.php
│        │  │  │  │  │  ├─ notifier_without_messenger.php
│        │  │  │  │  │  ├─ notifier_without_transports.php
│        │  │  │  │  │  ├─ notifier_with_disabled_message_bus.php
│        │  │  │  │  │  ├─ notifier_with_specific_message_bus.php
│        │  │  │  │  │  ├─ php_errors_disabled.php
│        │  │  │  │  │  ├─ php_errors_enabled.php
│        │  │  │  │  │  ├─ php_errors_log_level.php
│        │  │  │  │  │  ├─ php_errors_log_levels.php
│        │  │  │  │  │  ├─ profiler.php
│        │  │  │  │  │  ├─ property_accessor.php
│        │  │  │  │  │  ├─ property_info.php
│        │  │  │  │  │  ├─ property_info_with_constructor_extractor.php
│        │  │  │  │  │  ├─ request.php
│        │  │  │  │  │  ├─ semaphore.php
│        │  │  │  │  │  ├─ semaphore_named.php
│        │  │  │  │  │  ├─ semaphore_service.php
│        │  │  │  │  │  ├─ serializer_disabled.php
│        │  │  │  │  │  ├─ serializer_enabled.php
│        │  │  │  │  │  ├─ serializer_mapping.php
│        │  │  │  │  │  ├─ serializer_mapping_without_annotations.php
│        │  │  │  │  │  ├─ serializer_without_translator.php
│        │  │  │  │  │  ├─ session.php
│        │  │  │  │  │  ├─ session_cookie_secure_auto.php
│        │  │  │  │  │  ├─ ssi_disabled.php
│        │  │  │  │  │  ├─ translator_cache_dir_disabled.php
│        │  │  │  │  │  ├─ translator_fallbacks.php
│        │  │  │  │  │  ├─ translator_globals.php
│        │  │  │  │  │  ├─ translator_without_globals.php
│        │  │  │  │  │  ├─ trusted_proxies_private_ranges.php
│        │  │  │  │  │  ├─ type_info.php
│        │  │  │  │  │  ├─ validation_attributes.php
│        │  │  │  │  │  ├─ validation_auto_mapping.php
│        │  │  │  │  │  ├─ validation_email_validation_mode.php
│        │  │  │  │  │  ├─ validation_mapping.php
│        │  │  │  │  │  ├─ validation_multiple_static_methods.php
│        │  │  │  │  │  ├─ validation_no_static_method.php
│        │  │  │  │  │  ├─ validation_translation_domain.php
│        │  │  │  │  │  ├─ webhook.php
│        │  │  │  │  │  ├─ webhook_without_serializer.php
│        │  │  │  │  │  ├─ web_link.php
│        │  │  │  │  │  ├─ workflows.php
│        │  │  │  │  │  ├─ workflows_enabled.php
│        │  │  │  │  │  ├─ workflows_explicitly_enabled.php
│        │  │  │  │  │  ├─ workflows_explicitly_enabled_named_workflows.php
│        │  │  │  │  │  ├─ workflow_not_valid.php
│        │  │  │  │  │  ├─ workflow_without_support_and_support_strategy.php
│        │  │  │  │  │  ├─ workflow_with_guard_expression.php
│        │  │  │  │  │  ├─ workflow_with_multiple_transitions_with_same_name.php
│        │  │  │  │  │  ├─ workflow_with_no_events_to_dispatch.php
│        │  │  │  │  │  ├─ workflow_with_specified_events_to_dispatch.php
│        │  │  │  │  │  └─ workflow_with_support_and_support_strategy.php
│        │  │  │  │  ├─ TestBundle
│        │  │  │  │  │  ├─ Resources
│        │  │  │  │  │  │  └─ config
│        │  │  │  │  │  │     ├─ serialization.xml
│        │  │  │  │  │  │     ├─ serialization.yml
│        │  │  │  │  │  │     ├─ serializer_mapping
│        │  │  │  │  │  │     │  ├─ files
│        │  │  │  │  │  │     │  │  ├─ foo.xml
│        │  │  │  │  │  │     │  │  └─ foo.yml
│        │  │  │  │  │  │     │  ├─ serialization.yaml
│        │  │  │  │  │  │     │  └─ serialization.yml
│        │  │  │  │  │  │     ├─ validation.xml
│        │  │  │  │  │  │     ├─ validation.yml
│        │  │  │  │  │  │     └─ validation_mapping
│        │  │  │  │  │  │        ├─ files
│        │  │  │  │  │  │        │  ├─ foo.xml
│        │  │  │  │  │  │        │  └─ foo.yml
│        │  │  │  │  │  │        ├─ validation.yaml
│        │  │  │  │  │  │        └─ validation.yml
│        │  │  │  │  │  └─ TestBundle.php
│        │  │  │  │  ├─ translations
│        │  │  │  │  │  ├─ domain.with.dots.en.yml
│        │  │  │  │  │  └─ test_paths.en.yml
│        │  │  │  │  ├─ Workflow
│        │  │  │  │  │  └─ Validator
│        │  │  │  │  │     └─ DefinitionValidator.php
│        │  │  │  │  ├─ xml
│        │  │  │  │  │  ├─ assets.xml
│        │  │  │  │  │  ├─ assets_disabled.xml
│        │  │  │  │  │  ├─ assets_version_strategy_as_service.xml
│        │  │  │  │  │  ├─ asset_mapper.xml
│        │  │  │  │  │  ├─ asset_mapper_without_assets.xml
│        │  │  │  │  │  ├─ cache.xml
│        │  │  │  │  │  ├─ cache_app_redis_tag_aware.xml
│        │  │  │  │  │  ├─ cache_app_redis_tag_aware_pool.xml
│        │  │  │  │  │  ├─ csrf.xml
│        │  │  │  │  │  ├─ csrf_disabled.xml
│        │  │  │  │  │  ├─ csrf_needs_session.xml
│        │  │  │  │  │  ├─ default_config.xml
│        │  │  │  │  │  ├─ esi_and_ssi_without_fragments.xml
│        │  │  │  │  │  ├─ esi_disabled.xml
│        │  │  │  │  │  ├─ exceptions.xml
│        │  │  │  │  │  ├─ form_csrf_disabled.xml
│        │  │  │  │  │  ├─ form_csrf_field_attr.xml
│        │  │  │  │  │  ├─ form_default_csrf.xml
│        │  │  │  │  │  ├─ form_no_csrf.xml
│        │  │  │  │  │  ├─ fragments_and_hinclude.xml
│        │  │  │  │  │  ├─ full.xml
│        │  │  │  │  │  ├─ html_sanitizer.xml
│        │  │  │  │  │  ├─ html_sanitizer_default_allowed_link_and_media_hosts.xml
│        │  │  │  │  │  ├─ html_sanitizer_default_config.xml
│        │  │  │  │  │  ├─ http_client_default_options.xml
│        │  │  │  │  │  ├─ http_client_full_default_options.xml
│        │  │  │  │  │  ├─ http_client_mock_response_factory.xml
│        │  │  │  │  │  ├─ http_client_override_default_options.xml
│        │  │  │  │  │  ├─ http_client_rate_limiter.xml
│        │  │  │  │  │  ├─ http_client_retry.xml
│        │  │  │  │  │  ├─ http_client_scoped_without_query_option.xml
│        │  │  │  │  │  ├─ http_client_xml_key.xml
│        │  │  │  │  │  ├─ json_streamer.xml
│        │  │  │  │  │  ├─ lock.xml
│        │  │  │  │  │  ├─ lock_named.xml
│        │  │  │  │  │  ├─ lock_service.xml
│        │  │  │  │  │  ├─ mailer_with_disabled_message_bus.xml
│        │  │  │  │  │  ├─ mailer_with_dsn.xml
│        │  │  │  │  │  ├─ mailer_with_specific_message_bus.xml
│        │  │  │  │  │  ├─ mailer_with_transports.xml
│        │  │  │  │  │  ├─ messenger.xml
│        │  │  │  │  │  ├─ messenger_disabled.xml
│        │  │  │  │  │  ├─ messenger_multiple_buses_without_deduplicate_middleware.xml
│        │  │  │  │  │  ├─ messenger_multiple_buses_with_deduplicate_middleware.xml
│        │  │  │  │  │  ├─ messenger_multiple_failure_transports.xml
│        │  │  │  │  │  ├─ messenger_multiple_failure_transports_global.xml
│        │  │  │  │  │  ├─ messenger_routing.xml
│        │  │  │  │  │  ├─ messenger_routing_invalid_transport.xml
│        │  │  │  │  │  ├─ messenger_routing_invalid_wildcard.xml
│        │  │  │  │  │  ├─ messenger_routing_single.xml
│        │  │  │  │  │  ├─ messenger_schedule.xml
│        │  │  │  │  │  ├─ messenger_transport.xml
│        │  │  │  │  │  ├─ messenger_transports.xml
│        │  │  │  │  │  ├─ notifier.xml
│        │  │  │  │  │  ├─ notifier_without_mailer.xml
│        │  │  │  │  │  ├─ notifier_without_messenger.xml
│        │  │  │  │  │  ├─ notifier_without_transports.xml
│        │  │  │  │  │  ├─ notifier_with_disabled_message_bus.xml
│        │  │  │  │  │  ├─ notifier_with_specific_message_bus.xml
│        │  │  │  │  │  ├─ php_errors_disabled.xml
│        │  │  │  │  │  ├─ php_errors_enabled.xml
│        │  │  │  │  │  ├─ php_errors_log_level.xml
│        │  │  │  │  │  ├─ php_errors_log_levels.xml
│        │  │  │  │  │  ├─ profiler.xml
│        │  │  │  │  │  ├─ property_accessor.xml
│        │  │  │  │  │  ├─ property_info.xml
│        │  │  │  │  │  ├─ property_info_with_constructor_extractor.xml
│        │  │  │  │  │  ├─ rate_limiter.xml
│        │  │  │  │  │  ├─ request.xml
│        │  │  │  │  │  ├─ semaphore.xml
│        │  │  │  │  │  ├─ semaphore_named.xml
│        │  │  │  │  │  ├─ semaphore_service.xml
│        │  │  │  │  │  ├─ serializer_disabled.xml
│        │  │  │  │  │  ├─ serializer_enabled.xml
│        │  │  │  │  │  ├─ serializer_mapping.xml
│        │  │  │  │  │  ├─ serializer_mapping_without_annotations.xml
│        │  │  │  │  │  ├─ serializer_without_translator.xml
│        │  │  │  │  │  ├─ session.xml
│        │  │  │  │  │  ├─ session_cookie_secure_auto.xml
│        │  │  │  │  │  ├─ ssi_disabled.xml
│        │  │  │  │  │  ├─ translator_cache_dir_disabled.xml
│        │  │  │  │  │  ├─ translator_fallbacks.xml
│        │  │  │  │  │  ├─ translator_globals.xml
│        │  │  │  │  │  ├─ translator_without_globals.xml
│        │  │  │  │  │  ├─ trusted_proxies_private_ranges.xml
│        │  │  │  │  │  ├─ type_info.xml
│        │  │  │  │  │  ├─ validation_attributes.xml
│        │  │  │  │  │  ├─ validation_auto_mapping.xml
│        │  │  │  │  │  ├─ validation_email_validation_mode.xml
│        │  │  │  │  │  ├─ validation_mapping.xml
│        │  │  │  │  │  ├─ validation_multiple_static_methods.xml
│        │  │  │  │  │  ├─ validation_no_static_method.xml
│        │  │  │  │  │  ├─ validation_translation_domain.xml
│        │  │  │  │  │  ├─ webhook.xml
│        │  │  │  │  │  ├─ webhook_without_serializer.xml
│        │  │  │  │  │  ├─ web_link.xml
│        │  │  │  │  │  ├─ workflows.xml
│        │  │  │  │  │  ├─ workflows_enabled.xml
│        │  │  │  │  │  ├─ workflows_explicitly_enabled.xml
│        │  │  │  │  │  ├─ workflows_explicitly_enabled_named_workflows.xml
│        │  │  │  │  │  ├─ workflow_not_valid.xml
│        │  │  │  │  │  ├─ workflow_without_support_and_support_strategy.xml
│        │  │  │  │  │  ├─ workflow_with_guard_expression.xml
│        │  │  │  │  │  ├─ workflow_with_multiple_transitions_with_same_name.xml
│        │  │  │  │  │  ├─ workflow_with_no_events_to_dispatch.xml
│        │  │  │  │  │  ├─ workflow_with_specified_events_to_dispatch.xml
│        │  │  │  │  │  └─ workflow_with_support_and_support_strategy.xml
│        │  │  │  │  └─ yml
│        │  │  │  │     ├─ assets.yml
│        │  │  │  │     ├─ assets_disabled.yml
│        │  │  │  │     ├─ assets_version_strategy_as_service.yml
│        │  │  │  │     ├─ asset_mapper_without_assets.yml
│        │  │  │  │     ├─ cache.yml
│        │  │  │  │     ├─ cache_app_redis_tag_aware.yml
│        │  │  │  │     ├─ cache_app_redis_tag_aware_pool.yml
│        │  │  │  │     ├─ csrf.yml
│        │  │  │  │     ├─ csrf_needs_session.yml
│        │  │  │  │     ├─ default_config.yml
│        │  │  │  │     ├─ esi_and_ssi_without_fragments.yml
│        │  │  │  │     ├─ esi_disabled.yml
│        │  │  │  │     ├─ exceptions.yml
│        │  │  │  │     ├─ form_csrf_disabled.yml
│        │  │  │  │     ├─ form_csrf_field_attr.yml
│        │  │  │  │     ├─ form_default_csrf.yml
│        │  │  │  │     ├─ form_no_csrf.yml
│        │  │  │  │     ├─ fragments_and_hinclude.yml
│        │  │  │  │     ├─ full.yml
│        │  │  │  │     ├─ html_sanitizer.yml
│        │  │  │  │     ├─ html_sanitizer_default_allowed_link_and_media_hosts.yml
│        │  │  │  │     ├─ html_sanitizer_default_config.yml
│        │  │  │  │     ├─ http_client_default_options.yml
│        │  │  │  │     ├─ http_client_full_default_options.yml
│        │  │  │  │     ├─ http_client_mock_response_factory.yml
│        │  │  │  │     ├─ http_client_override_default_options.yml
│        │  │  │  │     ├─ http_client_rate_limiter.yml
│        │  │  │  │     ├─ http_client_retry.yml
│        │  │  │  │     ├─ http_client_scoped_without_query_option.yml
│        │  │  │  │     ├─ http_client_xml_key.yml
│        │  │  │  │     ├─ json_streamer.yml
│        │  │  │  │     ├─ lock.yml
│        │  │  │  │     ├─ lock_named.yml
│        │  │  │  │     ├─ lock_service.yml
│        │  │  │  │     ├─ mailer_with_disabled_message_bus.yml
│        │  │  │  │     ├─ mailer_with_dsn.yml
│        │  │  │  │     ├─ mailer_with_specific_message_bus.yml
│        │  │  │  │     ├─ mailer_with_transports.yml
│        │  │  │  │     ├─ messenger.yml
│        │  │  │  │     ├─ messenger_disabled.yml
│        │  │  │  │     ├─ messenger_middleware_factory_erroneous_format.yml
│        │  │  │  │     ├─ messenger_multiple_buses_without_deduplicate_middleware.yml
│        │  │  │  │     ├─ messenger_multiple_buses_with_deduplicate_middleware.yml
│        │  │  │  │     ├─ messenger_multiple_failure_transports.yml
│        │  │  │  │     ├─ messenger_multiple_failure_transports_global.yml
│        │  │  │  │     ├─ messenger_routing.yml
│        │  │  │  │     ├─ messenger_routing_invalid_transport.yml
│        │  │  │  │     ├─ messenger_routing_invalid_wildcard.yml
│        │  │  │  │     ├─ messenger_routing_single.yml
│        │  │  │  │     ├─ messenger_schedule.yml
│        │  │  │  │     ├─ messenger_transport.yml
│        │  │  │  │     ├─ messenger_transports.yml
│        │  │  │  │     ├─ messenger_with_disabled_reset_on_message.yml
│        │  │  │  │     ├─ messenger_with_explict_reset_on_message_legacy.yml
│        │  │  │  │     ├─ notifier.yml
│        │  │  │  │     ├─ notifier_without_mailer.yml
│        │  │  │  │     ├─ notifier_without_messenger.yml
│        │  │  │  │     ├─ notifier_without_transports.yml
│        │  │  │  │     ├─ notifier_with_disabled_message_bus.yml
│        │  │  │  │     ├─ notifier_with_specific_message_bus.yml
│        │  │  │  │     ├─ php_errors_disabled.yml
│        │  │  │  │     ├─ php_errors_enabled.yml
│        │  │  │  │     ├─ php_errors_log_level.yml
│        │  │  │  │     ├─ php_errors_log_levels.yml
│        │  │  │  │     ├─ profiler.yml
│        │  │  │  │     ├─ property_accessor.yml
│        │  │  │  │     ├─ property_info.yml
│        │  │  │  │     ├─ property_info_with_constructor_extractor.yml
│        │  │  │  │     ├─ request.yml
│        │  │  │  │     ├─ semaphore.yml
│        │  │  │  │     ├─ semaphore_named.yml
│        │  │  │  │     ├─ semaphore_service.yml
│        │  │  │  │     ├─ serializer_disabled.yml
│        │  │  │  │     ├─ serializer_enabled.yml
│        │  │  │  │     ├─ serializer_mapping.yml
│        │  │  │  │     ├─ serializer_mapping_without_annotations.yml
│        │  │  │  │     ├─ serializer_without_translator.yml
│        │  │  │  │     ├─ session.yml
│        │  │  │  │     ├─ session_cookie_secure_auto.yml
│        │  │  │  │     ├─ ssi_disabled.yml
│        │  │  │  │     ├─ translator_cache_dir_disabled.yml
│        │  │  │  │     ├─ translator_fallbacks.yml
│        │  │  │  │     ├─ translator_globals.yml
│        │  │  │  │     ├─ translator_without_globals.yml
│        │  │  │  │     ├─ trusted_proxies_private_ranges.yml
│        │  │  │  │     ├─ type_info.yml
│        │  │  │  │     ├─ validation_attributes.yml
│        │  │  │  │     ├─ validation_auto_mapping.yml
│        │  │  │  │     ├─ validation_email_validation_mode.yml
│        │  │  │  │     ├─ validation_mapping.yml
│        │  │  │  │     ├─ validation_multiple_static_methods.yml
│        │  │  │  │     ├─ validation_no_static_method.yml
│        │  │  │  │     ├─ validation_translation_domain.yml
│        │  │  │  │     ├─ webhook.yml
│        │  │  │  │     ├─ webhook_without_serializer.yml
│        │  │  │  │     ├─ web_link.yml
│        │  │  │  │     ├─ workflows.yml
│        │  │  │  │     ├─ workflows_enabled.yml
│        │  │  │  │     ├─ workflows_explicitly_enabled.yml
│        │  │  │  │     ├─ workflows_explicitly_enabled_named_workflows.yml
│        │  │  │  │     ├─ workflow_not_valid.yml
│        │  │  │  │     ├─ workflow_without_support_and_support_strategy.yml
│        │  │  │  │     ├─ workflow_with_guard_expression.yml
│        │  │  │  │     ├─ workflow_with_multiple_transitions_with_same_name.yml
│        │  │  │  │     ├─ workflow_with_no_events_to_dispatch.yml
│        │  │  │  │     ├─ workflow_with_specified_events_to_dispatch.yml
│        │  │  │  │     └─ workflow_with_support_and_support_strategy.yml
│        │  │  │  ├─ FrameworkExtensionTestCase.php
│        │  │  │  ├─ PhpFrameworkExtensionTest.php
│        │  │  │  ├─ translations
│        │  │  │  │  ├─ security.en.yaml
│        │  │  │  │  └─ test_default.en.xlf
│        │  │  │  ├─ XmlFrameworkExtensionTest.php
│        │  │  │  └─ YamlFrameworkExtensionTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ BackslashClass.php
│        │  │  │  ├─ ClassAliasExampleClass.php
│        │  │  │  ├─ ClassAliasTargetClass.php
│        │  │  │  ├─ ContainerExcluded.php
│        │  │  │  ├─ DeclaredClass.php
│        │  │  │  ├─ DeprecatedClass.php
│        │  │  │  ├─ Descriptor
│        │  │  │  │  ├─ alias_1.json
│        │  │  │  │  ├─ alias_1.md
│        │  │  │  │  ├─ alias_1.txt
│        │  │  │  │  ├─ alias_1.xml
│        │  │  │  │  ├─ alias_2.json
│        │  │  │  │  ├─ alias_2.md
│        │  │  │  │  ├─ alias_2.txt
│        │  │  │  │  ├─ alias_2.xml
│        │  │  │  │  ├─ alias_with_definition_1.json
│        │  │  │  │  ├─ alias_with_definition_1.md
│        │  │  │  │  ├─ alias_with_definition_1.txt
│        │  │  │  │  ├─ alias_with_definition_1.xml
│        │  │  │  │  ├─ alias_with_definition_2.json
│        │  │  │  │  ├─ alias_with_definition_2.md
│        │  │  │  │  ├─ alias_with_definition_2.txt
│        │  │  │  │  ├─ alias_with_definition_2.xml
│        │  │  │  │  ├─ array_parameter.json
│        │  │  │  │  ├─ array_parameter.md
│        │  │  │  │  ├─ array_parameter.txt
│        │  │  │  │  ├─ array_parameter.xml
│        │  │  │  │  ├─ builder_1_arguments.json
│        │  │  │  │  ├─ builder_1_arguments.md
│        │  │  │  │  ├─ builder_1_arguments.txt
│        │  │  │  │  ├─ builder_1_arguments.xml
│        │  │  │  │  ├─ builder_1_public.json
│        │  │  │  │  ├─ builder_1_public.md
│        │  │  │  │  ├─ builder_1_public.txt
│        │  │  │  │  ├─ builder_1_public.xml
│        │  │  │  │  ├─ builder_1_services.json
│        │  │  │  │  ├─ builder_1_services.md
│        │  │  │  │  ├─ builder_1_services.txt
│        │  │  │  │  ├─ builder_1_services.xml
│        │  │  │  │  ├─ builder_1_tag1.json
│        │  │  │  │  ├─ builder_1_tag1.md
│        │  │  │  │  ├─ builder_1_tag1.txt
│        │  │  │  │  ├─ builder_1_tag1.xml
│        │  │  │  │  ├─ builder_1_tags.json
│        │  │  │  │  ├─ builder_1_tags.md
│        │  │  │  │  ├─ builder_1_tags.txt
│        │  │  │  │  ├─ builder_1_tags.xml
│        │  │  │  │  ├─ builder_priority_tag.json
│        │  │  │  │  ├─ builder_priority_tag.md
│        │  │  │  │  ├─ builder_priority_tag.txt
│        │  │  │  │  ├─ builder_priority_tag.xml
│        │  │  │  │  ├─ cache
│        │  │  │  │  │  ├─ KernelContainerWithDeprecations.log
│        │  │  │  │  │  └─ KernelContainerWithoutDeprecations.log
│        │  │  │  │  ├─ callable_1.json
│        │  │  │  │  ├─ callable_1.md
│        │  │  │  │  ├─ callable_1.txt
│        │  │  │  │  ├─ callable_1.xml
│        │  │  │  │  ├─ callable_2.json
│        │  │  │  │  ├─ callable_2.md
│        │  │  │  │  ├─ callable_2.txt
│        │  │  │  │  ├─ callable_2.xml
│        │  │  │  │  ├─ callable_3.json
│        │  │  │  │  ├─ callable_3.md
│        │  │  │  │  ├─ callable_3.txt
│        │  │  │  │  ├─ callable_3.xml
│        │  │  │  │  ├─ callable_4.json
│        │  │  │  │  ├─ callable_4.md
│        │  │  │  │  ├─ callable_4.txt
│        │  │  │  │  ├─ callable_4.xml
│        │  │  │  │  ├─ callable_5.json
│        │  │  │  │  ├─ callable_5.md
│        │  │  │  │  ├─ callable_5.txt
│        │  │  │  │  ├─ callable_5.xml
│        │  │  │  │  ├─ callable_6.json
│        │  │  │  │  ├─ callable_6.md
│        │  │  │  │  ├─ callable_6.txt
│        │  │  │  │  ├─ callable_6.xml
│        │  │  │  │  ├─ callable_7.json
│        │  │  │  │  ├─ callable_7.md
│        │  │  │  │  ├─ callable_7.txt
│        │  │  │  │  ├─ callable_7.xml
│        │  │  │  │  ├─ callable_from_callable.json
│        │  │  │  │  ├─ callable_from_callable.md
│        │  │  │  │  ├─ callable_from_callable.txt
│        │  │  │  │  ├─ callable_from_callable.xml
│        │  │  │  │  ├─ definition_1.json
│        │  │  │  │  ├─ definition_1.md
│        │  │  │  │  ├─ definition_1.txt
│        │  │  │  │  ├─ definition_1.xml
│        │  │  │  │  ├─ definition_2.json
│        │  │  │  │  ├─ definition_2.md
│        │  │  │  │  ├─ definition_2.txt
│        │  │  │  │  ├─ definition_2.xml
│        │  │  │  │  ├─ definition_3.json
│        │  │  │  │  ├─ definition_3.md
│        │  │  │  │  ├─ definition_3.txt
│        │  │  │  │  ├─ definition_3.xml
│        │  │  │  │  ├─ definition_arguments_1.json
│        │  │  │  │  ├─ definition_arguments_1.md
│        │  │  │  │  ├─ definition_arguments_1.txt
│        │  │  │  │  ├─ definition_arguments_1.xml
│        │  │  │  │  ├─ definition_arguments_2.json
│        │  │  │  │  ├─ definition_arguments_2.md
│        │  │  │  │  ├─ definition_arguments_2.txt
│        │  │  │  │  ├─ definition_arguments_2.xml
│        │  │  │  │  ├─ definition_arguments_3.json
│        │  │  │  │  ├─ definition_arguments_3.md
│        │  │  │  │  ├─ definition_arguments_3.txt
│        │  │  │  │  ├─ definition_arguments_3.xml
│        │  │  │  │  ├─ definition_arguments_without_class.json
│        │  │  │  │  ├─ definition_arguments_without_class.md
│        │  │  │  │  ├─ definition_arguments_without_class.txt
│        │  │  │  │  ├─ definition_arguments_without_class.xml
│        │  │  │  │  ├─ definition_arguments_with_enum.json
│        │  │  │  │  ├─ definition_arguments_with_enum.md
│        │  │  │  │  ├─ definition_arguments_with_enum.txt
│        │  │  │  │  ├─ definition_arguments_with_enum.xml
│        │  │  │  │  ├─ definition_without_class.json
│        │  │  │  │  ├─ definition_without_class.md
│        │  │  │  │  ├─ definition_without_class.txt
│        │  │  │  │  ├─ definition_without_class.xml
│        │  │  │  │  ├─ deprecated_parameter.json
│        │  │  │  │  ├─ deprecated_parameter.md
│        │  │  │  │  ├─ deprecated_parameter.txt
│        │  │  │  │  ├─ deprecated_parameter.xml
│        │  │  │  │  ├─ deprecated_parameters.json
│        │  │  │  │  ├─ deprecated_parameters.md
│        │  │  │  │  ├─ deprecated_parameters.txt
│        │  │  │  │  ├─ deprecated_parameters.xml
│        │  │  │  │  ├─ deprecations.json
│        │  │  │  │  ├─ deprecations.md
│        │  │  │  │  ├─ deprecations.txt
│        │  │  │  │  ├─ deprecations.xml
│        │  │  │  │  ├─ deprecations_empty.json
│        │  │  │  │  ├─ deprecations_empty.md
│        │  │  │  │  ├─ deprecations_empty.txt
│        │  │  │  │  ├─ deprecations_empty.xml
│        │  │  │  │  ├─ event_dispatcher_1_event1.json
│        │  │  │  │  ├─ event_dispatcher_1_event1.md
│        │  │  │  │  ├─ event_dispatcher_1_event1.txt
│        │  │  │  │  ├─ event_dispatcher_1_event1.xml
│        │  │  │  │  ├─ event_dispatcher_1_events.json
│        │  │  │  │  ├─ event_dispatcher_1_events.md
│        │  │  │  │  ├─ event_dispatcher_1_events.txt
│        │  │  │  │  ├─ event_dispatcher_1_events.xml
│        │  │  │  │  ├─ existing_class_def_1.json
│        │  │  │  │  ├─ existing_class_def_1.md
│        │  │  │  │  ├─ existing_class_def_1.txt
│        │  │  │  │  ├─ existing_class_def_1.xml
│        │  │  │  │  ├─ existing_class_def_2.json
│        │  │  │  │  ├─ existing_class_def_2.md
│        │  │  │  │  ├─ existing_class_def_2.txt
│        │  │  │  │  ├─ existing_class_def_2.xml
│        │  │  │  │  ├─ parameter.json
│        │  │  │  │  ├─ parameter.md
│        │  │  │  │  ├─ parameter.txt
│        │  │  │  │  ├─ parameter.xml
│        │  │  │  │  ├─ parameters_1.json
│        │  │  │  │  ├─ parameters_1.md
│        │  │  │  │  ├─ parameters_1.txt
│        │  │  │  │  ├─ parameters_1.xml
│        │  │  │  │  ├─ parameters_enums.json
│        │  │  │  │  ├─ parameters_enums.md
│        │  │  │  │  ├─ parameters_enums.txt
│        │  │  │  │  ├─ parameters_enums.xml
│        │  │  │  │  ├─ route_1.json
│        │  │  │  │  ├─ route_1.md
│        │  │  │  │  ├─ route_1.txt
│        │  │  │  │  ├─ route_1.xml
│        │  │  │  │  ├─ route_1_link.txt
│        │  │  │  │  ├─ route_2.json
│        │  │  │  │  ├─ route_2.md
│        │  │  │  │  ├─ route_2.txt
│        │  │  │  │  ├─ route_2.xml
│        │  │  │  │  ├─ route_2_link.txt
│        │  │  │  │  ├─ route_collection_1.json
│        │  │  │  │  ├─ route_collection_1.md
│        │  │  │  │  ├─ route_collection_1.txt
│        │  │  │  │  ├─ route_collection_1.xml
│        │  │  │  │  ├─ route_collection_2.json
│        │  │  │  │  ├─ route_collection_2.md
│        │  │  │  │  ├─ route_collection_2.txt
│        │  │  │  │  ├─ route_collection_2.xml
│        │  │  │  │  ├─ route_collection_3.json
│        │  │  │  │  ├─ route_collection_3.md
│        │  │  │  │  ├─ route_collection_3.txt
│        │  │  │  │  └─ route_collection_3.xml
│        │  │  │  ├─ FooUnitEnum.php
│        │  │  │  ├─ Messenger
│        │  │  │  │  ├─ BarMessage.php
│        │  │  │  │  ├─ DummyMessage.php
│        │  │  │  │  ├─ DummyMessageInterface.php
│        │  │  │  │  ├─ DummySchedule.php
│        │  │  │  │  ├─ DummyTask.php
│        │  │  │  │  ├─ DummyTaskWithCustomReceiver.php
│        │  │  │  │  ├─ FooMessage.php
│        │  │  │  │  └─ SecondMessage.php
│        │  │  │  ├─ ObjectMapper
│        │  │  │  │  ├─ ObjectMapped.php
│        │  │  │  │  ├─ ObjectToBeMapped.php
│        │  │  │  │  └─ TransformCallable.php
│        │  │  │  ├─ Resources
│        │  │  │  │  ├─ BaseBundle
│        │  │  │  │  │  └─ views
│        │  │  │  │  │     ├─ base.format.engine
│        │  │  │  │  │     └─ controller
│        │  │  │  │  │        └─ custom.format.engine
│        │  │  │  │  ├─ translations
│        │  │  │  │  │  ├─ domain.with.dots.en.yml
│        │  │  │  │  │  └─ messages.fr.yml
│        │  │  │  │  ├─ translations2
│        │  │  │  │  │  └─ ccc.fr.yml
│        │  │  │  │  └─ views
│        │  │  │  │     ├─ resource.format.engine
│        │  │  │  │     ├─ this.is.a.template.format.engine
│        │  │  │  │     └─ translation.html.php
│        │  │  │  ├─ Serialization
│        │  │  │  │  ├─ Author.php
│        │  │  │  │  ├─ Person.php
│        │  │  │  │  └─ Resources
│        │  │  │  │     ├─ author.yml
│        │  │  │  │     ├─ does_not_exist.yaml
│        │  │  │  │     └─ person.xml
│        │  │  │  ├─ Serializer
│        │  │  │  │  ├─ CircularReferenceHandler.php
│        │  │  │  │  └─ MaxDepthHandler.php
│        │  │  │  ├─ Suit.php
│        │  │  │  ├─ TemplatePathsCache
│        │  │  │  │  ├─ templates-empty.php
│        │  │  │  │  └─ templates.php
│        │  │  │  ├─ templates.php
│        │  │  │  ├─ TranslatableBackedEnum.php
│        │  │  │  ├─ Validation
│        │  │  │  │  ├─ Article.php
│        │  │  │  │  ├─ Author.php
│        │  │  │  │  ├─ Category.php
│        │  │  │  │  ├─ Person.php
│        │  │  │  │  ├─ Resources
│        │  │  │  │  │  ├─ author.yml
│        │  │  │  │  │  ├─ categories.yml
│        │  │  │  │  │  ├─ does_not_exist.yaml
│        │  │  │  │  │  └─ person.xml
│        │  │  │  │  └─ SubCategory.php
│        │  │  │  └─ WarmedClass.php
│        │  │  ├─ Functional
│        │  │  │  ├─ AbstractAttributeRoutingTestCase.php
│        │  │  │  ├─ AbstractWebTestCase.php
│        │  │  │  ├─ AnnotatedControllerTest.php
│        │  │  │  ├─ ApiAttributesTest.php
│        │  │  │  ├─ app
│        │  │  │  │  ├─ AnnotatedController
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ ApiAttributesTest
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ AppKernel.php
│        │  │  │  │  ├─ AutowiringTypes
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ BundlePaths
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ CacheAttributeListener
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ CachePoolClear
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ CachePools
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ default.yml
│        │  │  │  │  │  ├─ redis_config.yml
│        │  │  │  │  │  └─ redis_custom_config.yml
│        │  │  │  │  ├─ config
│        │  │  │  │  │  ├─ default.yml
│        │  │  │  │  │  └─ framework.yml
│        │  │  │  │  ├─ ConfigDump
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ ContainerDebug
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ ContainerDump
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ ControllerServiceResolution
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ Fragment
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ routing.yml
│        │  │  │  │  │  └─ services.yml
│        │  │  │  │  ├─ HttpClient
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ routing.yml
│        │  │  │  │  │  └─ services.yml
│        │  │  │  │  ├─ JsonStreamer
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ Dto
│        │  │  │  │  │  │  └─ Dummy.php
│        │  │  │  │  │  ├─ RangeToStringValueTransformer.php
│        │  │  │  │  │  └─ StringToRangeValueTransformer.php
│        │  │  │  │  ├─ Mailer
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ routing.yml
│        │  │  │  │  │  └─ services.yml
│        │  │  │  │  ├─ Notifier
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ routing.yml
│        │  │  │  │  │  └─ services.yml
│        │  │  │  │  ├─ ObjectMapper
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ Profiler
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ ProfilerCollectParameter
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ Psr4Routing
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ RouterDebug
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ RoutingConditionService
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ routing.yml
│        │  │  │  │  │  ├─ services_auto_configured.yml
│        │  │  │  │  │  └─ services_manually_configured.yml
│        │  │  │  │  ├─ Scheduler
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ Security
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ Serializer
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ default_context.yaml
│        │  │  │  │  ├─ Session
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ Slugger
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ services.yml
│        │  │  │  │  ├─ templates
│        │  │  │  │  │  └─ fragment.html.twig
│        │  │  │  │  ├─ TestServiceContainer
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ services.yml
│        │  │  │  │  │  └─ test_disabled.yml
│        │  │  │  │  ├─ TransDebug
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ services.yml
│        │  │  │  │  ├─ TypeInfo
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ Dummy.php
│        │  │  │  │  └─ Uid
│        │  │  │  │     ├─ bundles.php
│        │  │  │  │     ├─ config_disabled.yml
│        │  │  │  │     ├─ config_enabled.yml
│        │  │  │  │     └─ routing.yml
│        │  │  │  ├─ AutowiringTypesTest.php
│        │  │  │  ├─ Bundle
│        │  │  │  │  ├─ DefaultConfigTestBundle
│        │  │  │  │  │  ├─ DefaultConfigTestBundle.php
│        │  │  │  │  │  └─ DependencyInjection
│        │  │  │  │  │     ├─ Configuration.php
│        │  │  │  │  │     └─ DefaultConfigTestExtension.php
│        │  │  │  │  ├─ ExtensionWithoutConfigTestBundle
│        │  │  │  │  │  ├─ DependencyInjection
│        │  │  │  │  │  │  └─ ExtensionWithoutConfigTestExtension.php
│        │  │  │  │  │  └─ ExtensionWithoutConfigTestBundle.php
│        │  │  │  │  ├─ LegacyBundle
│        │  │  │  │  │  ├─ Entity
│        │  │  │  │  │  │  └─ LegacyPerson.php
│        │  │  │  │  │  ├─ LegacyBundle.php
│        │  │  │  │  │  └─ Resources
│        │  │  │  │  │     ├─ config
│        │  │  │  │  │     │  ├─ serialization.yaml
│        │  │  │  │  │     │  └─ validation.yaml
│        │  │  │  │  │     ├─ public
│        │  │  │  │  │     │  └─ legacy.css
│        │  │  │  │  │     ├─ translations
│        │  │  │  │  │     │  └─ legacy.en.yaml
│        │  │  │  │  │     └─ views
│        │  │  │  │  │        └─ index.html.twig
│        │  │  │  │  ├─ ModernBundle
│        │  │  │  │  │  ├─ config
│        │  │  │  │  │  │  ├─ serialization.yaml
│        │  │  │  │  │  │  └─ validation.yaml
│        │  │  │  │  │  ├─ public
│        │  │  │  │  │  │  └─ modern.css
│        │  │  │  │  │  ├─ src
│        │  │  │  │  │  │  ├─ Entity
│        │  │  │  │  │  │  │  └─ ModernPerson.php
│        │  │  │  │  │  │  └─ ModernBundle.php
│        │  │  │  │  │  ├─ templates
│        │  │  │  │  │  │  └─ index.html.twig
│        │  │  │  │  │  └─ translations
│        │  │  │  │  │     └─ modern.en.yaml
│        │  │  │  │  ├─ RoutingConditionServiceBundle
│        │  │  │  │  │  ├─ Controller
│        │  │  │  │  │  │  └─ DefaultController.php
│        │  │  │  │  │  ├─ RoutingConditionServiceBundle.php
│        │  │  │  │  │  └─ Service
│        │  │  │  │  │     ├─ AutoConfiguredNonAliasedService.php
│        │  │  │  │  │     ├─ AutoConfiguredService.php
│        │  │  │  │  │     ├─ FooOriginalService.php
│        │  │  │  │  │     ├─ FooReplacementService.php
│        │  │  │  │  │     └─ ManuallyTaggedService.php
│        │  │  │  │  └─ TestBundle
│        │  │  │  │     ├─ AutowiringTypes
│        │  │  │  │     │  └─ AutowiredServices.php
│        │  │  │  │     ├─ Controller
│        │  │  │  │     │  ├─ AnnotatedController.php
│        │  │  │  │     │  ├─ EmailController.php
│        │  │  │  │     │  ├─ FragmentController.php
│        │  │  │  │     │  ├─ HttpClientController.php
│        │  │  │  │     │  ├─ NotificationController.php
│        │  │  │  │     │  ├─ ProfilerController.php
│        │  │  │  │     │  ├─ SecurityController.php
│        │  │  │  │     │  ├─ SessionController.php
│        │  │  │  │     │  ├─ SubRequestController.php
│        │  │  │  │     │  ├─ SubRequestServiceResolutionController.php
│        │  │  │  │     │  ├─ TransController.php
│        │  │  │  │     │  └─ UidController.php
│        │  │  │  │     ├─ DependencyInjection
│        │  │  │  │     │  ├─ Config
│        │  │  │  │     │  │  └─ CustomConfig.php
│        │  │  │  │     │  ├─ Configuration.php
│        │  │  │  │     │  └─ TestExtension.php
│        │  │  │  │     ├─ Resources
│        │  │  │  │     │  └─ config
│        │  │  │  │     │     └─ routing.yml
│        │  │  │  │     ├─ Slugger
│        │  │  │  │     │  └─ SlugConstructArgService.php
│        │  │  │  │     ├─ TestBundle.php
│        │  │  │  │     ├─ Tests
│        │  │  │  │     │  └─ MockClientCallback.php
│        │  │  │  │     ├─ TestServiceContainer
│        │  │  │  │     │  ├─ NonPublicService.php
│        │  │  │  │     │  ├─ PrivateService.php
│        │  │  │  │     │  ├─ PublicService.php
│        │  │  │  │     │  ├─ ResettableService.php
│        │  │  │  │     │  └─ UnusedPrivateService.php
│        │  │  │  │     └─ TransDebug
│        │  │  │  │        ├─ TransConstructArgService.php
│        │  │  │  │        ├─ TransMethodCallsService.php
│        │  │  │  │        ├─ TransPropertyService.php
│        │  │  │  │        └─ TransSubscriberService.php
│        │  │  │  ├─ BundlePathsTest.php
│        │  │  │  ├─ CacheAttributeListenerTest.php
│        │  │  │  ├─ CachePoolClearCommandTest.php
│        │  │  │  ├─ CachePoolListCommandTest.php
│        │  │  │  ├─ CachePoolsTest.php
│        │  │  │  ├─ ConfigDebugCommandTest.php
│        │  │  │  ├─ ConfigDumpReferenceCommandTest.php
│        │  │  │  ├─ ContainerDebugCommandTest.php
│        │  │  │  ├─ ContainerDumpTest.php
│        │  │  │  ├─ DebugAutowiringCommandTest.php
│        │  │  │  ├─ Extension
│        │  │  │  │  └─ TestDumpExtension.php
│        │  │  │  ├─ Fixtures
│        │  │  │  │  └─ describe_env_vars.txt
│        │  │  │  ├─ FragmentTest.php
│        │  │  │  ├─ HttpClientTest.php
│        │  │  │  ├─ JsonStreamerTest.php
│        │  │  │  ├─ MailerTest.php
│        │  │  │  ├─ NotificationTest.php
│        │  │  │  ├─ ObjectMapperTest.php
│        │  │  │  ├─ ProfilerTest.php
│        │  │  │  ├─ PropertyInfoTest.php
│        │  │  │  ├─ Psr4RoutingTest.php
│        │  │  │  ├─ RouterDebugCommandTest.php
│        │  │  │  ├─ RoutingConditionServiceTest.php
│        │  │  │  ├─ SchedulerTest.php
│        │  │  │  ├─ SecurityTest.php
│        │  │  │  ├─ SerializerTest.php
│        │  │  │  ├─ SessionTest.php
│        │  │  │  ├─ SluggerLocaleAwareTest.php
│        │  │  │  ├─ SubRequestsTest.php
│        │  │  │  ├─ TestServiceContainerTest.php
│        │  │  │  ├─ TranslationDebugCommandTest.php
│        │  │  │  ├─ TypeInfoTest.php
│        │  │  │  └─ UidTest.php
│        │  │  ├─ Kernel
│        │  │  │  ├─ ConcreteMicroKernel.php
│        │  │  │  ├─ default
│        │  │  │  │  ├─ config
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ routes.yaml
│        │  │  │  │  │  └─ services.yaml
│        │  │  │  │  └─ src
│        │  │  │  │     └─ DefaultKernel.php
│        │  │  │  ├─ flex-style
│        │  │  │  │  ├─ config
│        │  │  │  │  │  └─ bundles.php
│        │  │  │  │  └─ src
│        │  │  │  │     └─ FlexStyleMicroKernel.php
│        │  │  │  ├─ KernelCommand.php
│        │  │  │  ├─ MicroKernelTraitTest.php
│        │  │  │  └─ SimpleKernel.php
│        │  │  ├─ KernelBrowserTest.php
│        │  │  ├─ Routing
│        │  │  │  ├─ DelegatingLoaderTest.php
│        │  │  │  ├─ Fixtures
│        │  │  │  │  └─ with_condition.yaml
│        │  │  │  ├─ RedirectableCompiledUrlMatcherTest.php
│        │  │  │  └─ RouterTest.php
│        │  │  ├─ Secrets
│        │  │  │  ├─ DotenvVaultTest.php
│        │  │  │  └─ SodiumVaultTest.php
│        │  │  ├─ Test
│        │  │  │  ├─ TestBrowserTokenTest.php
│        │  │  │  └─ WebTestCaseTest.php
│        │  │  ├─ TestCase.php
│        │  │  └─ Translation
│        │  │     └─ TranslatorTest.php
│        │  └─ Translation
│        │     └─ Translator.php
│        ├─ http-foundation
│        │  ├─ AcceptHeader.php
│        │  ├─ AcceptHeaderItem.php
│        │  ├─ BinaryFileResponse.php
│        │  ├─ ChainRequestMatcher.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ Cookie.php
│        │  ├─ EventStreamResponse.php
│        │  ├─ Exception
│        │  │  ├─ BadRequestException.php
│        │  │  ├─ ConflictingHeadersException.php
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ ExpiredSignedUriException.php
│        │  │  ├─ JsonException.php
│        │  │  ├─ LogicException.php
│        │  │  ├─ RequestExceptionInterface.php
│        │  │  ├─ SessionNotFoundException.php
│        │  │  ├─ SignedUriException.php
│        │  │  ├─ SuspiciousOperationException.php
│        │  │  ├─ UnexpectedValueException.php
│        │  │  ├─ UnsignedUriException.php
│        │  │  └─ UnverifiedSignedUriException.php
│        │  ├─ File
│        │  │  ├─ Exception
│        │  │  │  ├─ AccessDeniedException.php
│        │  │  │  ├─ CannotWriteFileException.php
│        │  │  │  ├─ ExtensionFileException.php
│        │  │  │  ├─ FileException.php
│        │  │  │  ├─ FileNotFoundException.php
│        │  │  │  ├─ FormSizeFileException.php
│        │  │  │  ├─ IniSizeFileException.php
│        │  │  │  ├─ NoFileException.php
│        │  │  │  ├─ NoTmpDirFileException.php
│        │  │  │  ├─ PartialFileException.php
│        │  │  │  ├─ UnexpectedTypeException.php
│        │  │  │  └─ UploadException.php
│        │  │  ├─ File.php
│        │  │  ├─ Stream.php
│        │  │  └─ UploadedFile.php
│        │  ├─ FileBag.php
│        │  ├─ HeaderBag.php
│        │  ├─ HeaderUtils.php
│        │  ├─ InputBag.php
│        │  ├─ IpUtils.php
│        │  ├─ JsonResponse.php
│        │  ├─ LICENSE
│        │  ├─ ParameterBag.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ RateLimiter
│        │  │  ├─ AbstractRequestRateLimiter.php
│        │  │  ├─ PeekableRequestRateLimiterInterface.php
│        │  │  └─ RequestRateLimiterInterface.php
│        │  ├─ README.md
│        │  ├─ RedirectResponse.php
│        │  ├─ Request.php
│        │  ├─ RequestMatcher
│        │  │  ├─ AttributesRequestMatcher.php
│        │  │  ├─ ExpressionRequestMatcher.php
│        │  │  ├─ HeaderRequestMatcher.php
│        │  │  ├─ HostRequestMatcher.php
│        │  │  ├─ IpsRequestMatcher.php
│        │  │  ├─ IsJsonRequestMatcher.php
│        │  │  ├─ MethodRequestMatcher.php
│        │  │  ├─ PathRequestMatcher.php
│        │  │  ├─ PortRequestMatcher.php
│        │  │  ├─ QueryParameterRequestMatcher.php
│        │  │  └─ SchemeRequestMatcher.php
│        │  ├─ RequestMatcherInterface.php
│        │  ├─ RequestStack.php
│        │  ├─ Response.php
│        │  ├─ ResponseHeaderBag.php
│        │  ├─ ServerBag.php
│        │  ├─ ServerEvent.php
│        │  ├─ Session
│        │  │  ├─ Attribute
│        │  │  │  ├─ AttributeBag.php
│        │  │  │  └─ AttributeBagInterface.php
│        │  │  ├─ Flash
│        │  │  │  ├─ AutoExpireFlashBag.php
│        │  │  │  ├─ FlashBag.php
│        │  │  │  └─ FlashBagInterface.php
│        │  │  ├─ FlashBagAwareSessionInterface.php
│        │  │  ├─ Session.php
│        │  │  ├─ SessionBagInterface.php
│        │  │  ├─ SessionBagProxy.php
│        │  │  ├─ SessionFactory.php
│        │  │  ├─ SessionFactoryInterface.php
│        │  │  ├─ SessionInterface.php
│        │  │  ├─ SessionUtils.php
│        │  │  └─ Storage
│        │  │     ├─ Handler
│        │  │     │  ├─ AbstractSessionHandler.php
│        │  │     │  ├─ IdentityMarshaller.php
│        │  │     │  ├─ MarshallingSessionHandler.php
│        │  │     │  ├─ MemcachedSessionHandler.php
│        │  │     │  ├─ MigratingSessionHandler.php
│        │  │     │  ├─ MongoDbSessionHandler.php
│        │  │     │  ├─ NativeFileSessionHandler.php
│        │  │     │  ├─ NullSessionHandler.php
│        │  │     │  ├─ PdoSessionHandler.php
│        │  │     │  ├─ RedisSessionHandler.php
│        │  │     │  ├─ SessionHandlerFactory.php
│        │  │     │  └─ StrictSessionHandler.php
│        │  │     ├─ MetadataBag.php
│        │  │     ├─ MockArraySessionStorage.php
│        │  │     ├─ MockFileSessionStorage.php
│        │  │     ├─ MockFileSessionStorageFactory.php
│        │  │     ├─ NativeSessionStorage.php
│        │  │     ├─ NativeSessionStorageFactory.php
│        │  │     ├─ PhpBridgeSessionStorage.php
│        │  │     ├─ PhpBridgeSessionStorageFactory.php
│        │  │     ├─ Proxy
│        │  │     │  ├─ AbstractProxy.php
│        │  │     │  └─ SessionHandlerProxy.php
│        │  │     ├─ SessionStorageFactoryInterface.php
│        │  │     └─ SessionStorageInterface.php
│        │  ├─ StreamedJsonResponse.php
│        │  ├─ StreamedResponse.php
│        │  ├─ Test
│        │  │  └─ Constraint
│        │  │     ├─ RequestAttributeValueSame.php
│        │  │     ├─ ResponseCookieValueSame.php
│        │  │     ├─ ResponseFormatSame.php
│        │  │     ├─ ResponseHasCookie.php
│        │  │     ├─ ResponseHasHeader.php
│        │  │     ├─ ResponseHeaderLocationSame.php
│        │  │     ├─ ResponseHeaderSame.php
│        │  │     ├─ ResponseIsRedirected.php
│        │  │     ├─ ResponseIsSuccessful.php
│        │  │     ├─ ResponseIsUnprocessable.php
│        │  │     └─ ResponseStatusCodeSame.php
│        │  ├─ Tests
│        │  │  ├─ AcceptHeaderItemTest.php
│        │  │  ├─ AcceptHeaderTest.php
│        │  │  ├─ BinaryFileResponseTest.php
│        │  │  ├─ CookieTest.php
│        │  │  ├─ EventStreamResponseTest.php
│        │  │  ├─ File
│        │  │  │  ├─ FakeFile.php
│        │  │  │  ├─ FileTest.php
│        │  │  │  ├─ Fixtures
│        │  │  │  │  ├─ -test
│        │  │  │  │  ├─ .unknownextension
│        │  │  │  │  ├─ case-sensitive-mime-type.xlsm
│        │  │  │  │  ├─ directory
│        │  │  │  │  │  └─ .empty
│        │  │  │  │  ├─ other-file.example
│        │  │  │  │  ├─ test
│        │  │  │  │  ├─ test.gif
│        │  │  │  │  └─ webkitdirectory
│        │  │  │  │     ├─ nested
│        │  │  │  │     │  └─ test.txt
│        │  │  │  │     └─ test.txt
│        │  │  │  └─ UploadedFileTest.php
│        │  │  ├─ FileBagTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ FooEnum.php
│        │  │  │  ├─ response-functional
│        │  │  │  │  ├─ common.inc
│        │  │  │  │  ├─ cookie_raw_urlencode.expected
│        │  │  │  │  ├─ cookie_raw_urlencode.php
│        │  │  │  │  ├─ cookie_samesite_lax.expected
│        │  │  │  │  ├─ cookie_samesite_lax.php
│        │  │  │  │  ├─ cookie_samesite_strict.expected
│        │  │  │  │  ├─ cookie_samesite_strict.php
│        │  │  │  │  ├─ cookie_urlencode.expected
│        │  │  │  │  ├─ cookie_urlencode.php
│        │  │  │  │  ├─ deleted_cookie.expected
│        │  │  │  │  ├─ deleted_cookie.php
│        │  │  │  │  ├─ early_hints.php
│        │  │  │  │  ├─ invalid_cookie_name.expected
│        │  │  │  │  └─ invalid_cookie_name.php
│        │  │  │  └─ xml
│        │  │  │     └─ http-status-codes.xml
│        │  │  ├─ HeaderBagTest.php
│        │  │  ├─ HeaderUtilsTest.php
│        │  │  ├─ InputBagTest.php
│        │  │  ├─ IpUtilsTest.php
│        │  │  ├─ JsonResponseTest.php
│        │  │  ├─ ParameterBagTest.php
│        │  │  ├─ RateLimiter
│        │  │  │  ├─ AbstractRequestRateLimiterTest.php
│        │  │  │  └─ MockAbstractRequestRateLimiter.php
│        │  │  ├─ RedirectResponseTest.php
│        │  │  ├─ RequestMatcher
│        │  │  │  ├─ AttributesRequestMatcherTest.php
│        │  │  │  ├─ ExpressionRequestMatcherTest.php
│        │  │  │  ├─ HeaderRequestMatcherTest.php
│        │  │  │  ├─ HostRequestMatcherTest.php
│        │  │  │  ├─ IpsRequestMatcherTest.php
│        │  │  │  ├─ IsJsonRequestMatcherTest.php
│        │  │  │  ├─ MethodRequestMatcherTest.php
│        │  │  │  ├─ PathRequestMatcherTest.php
│        │  │  │  ├─ PortRequestMatcherTest.php
│        │  │  │  ├─ QueryParameterRequestMatcherTest.php
│        │  │  │  └─ SchemeRequestMatcherTest.php
│        │  │  ├─ RequestStackTest.php
│        │  │  ├─ RequestTest.php
│        │  │  ├─ ResponseFunctionalTest.php
│        │  │  ├─ ResponseHeaderBagTest.php
│        │  │  ├─ ResponseTest.php
│        │  │  ├─ ResponseTestCase.php
│        │  │  ├─ schema
│        │  │  │  ├─ http-status-codes.rng
│        │  │  │  └─ iana-registry.rng
│        │  │  ├─ ServerBagTest.php
│        │  │  ├─ Session
│        │  │  │  ├─ Attribute
│        │  │  │  │  └─ AttributeBagTest.php
│        │  │  │  ├─ Flash
│        │  │  │  │  ├─ AutoExpireFlashBagTest.php
│        │  │  │  │  └─ FlashBagTest.php
│        │  │  │  ├─ SessionTest.php
│        │  │  │  └─ Storage
│        │  │  │     ├─ Handler
│        │  │  │     │  ├─ AbstractRedisSessionHandlerTestCase.php
│        │  │  │     │  ├─ AbstractSessionHandlerTest.php
│        │  │  │     │  ├─ Fixtures
│        │  │  │     │  │  ├─ common.inc
│        │  │  │     │  │  ├─ empty_destroys.expected
│        │  │  │     │  │  ├─ empty_destroys.php
│        │  │  │     │  │  ├─ invalid_regenerate.expected
│        │  │  │     │  │  ├─ invalid_regenerate.php
│        │  │  │     │  │  ├─ read_only.expected
│        │  │  │     │  │  ├─ read_only.php
│        │  │  │     │  │  ├─ regenerate.expected
│        │  │  │     │  │  ├─ regenerate.php
│        │  │  │     │  │  ├─ storage.expected
│        │  │  │     │  │  ├─ storage.php
│        │  │  │     │  │  ├─ with_cookie.expected
│        │  │  │     │  │  ├─ with_cookie.php
│        │  │  │     │  │  ├─ with_cookie_and_session.expected
│        │  │  │     │  │  ├─ with_cookie_and_session.php
│        │  │  │     │  │  ├─ with_samesite.expected
│        │  │  │     │  │  ├─ with_samesite.php
│        │  │  │     │  │  ├─ with_samesite_and_migration.expected
│        │  │  │     │  │  └─ with_samesite_and_migration.php
│        │  │  │     │  ├─ IdentityMarshallerTest.php
│        │  │  │     │  ├─ MarshallingSessionHandlerTest.php
│        │  │  │     │  ├─ MemcachedSessionHandlerTest.php
│        │  │  │     │  ├─ MigratingSessionHandlerTest.php
│        │  │  │     │  ├─ MongoDbSessionHandlerTest.php
│        │  │  │     │  ├─ NativeFileSessionHandlerTest.php
│        │  │  │     │  ├─ NullSessionHandlerTest.php
│        │  │  │     │  ├─ PdoSessionHandlerTest.php
│        │  │  │     │  ├─ PredisClusterSessionHandlerTest.php
│        │  │  │     │  ├─ PredisSessionHandlerTest.php
│        │  │  │     │  ├─ RedisArraySessionHandlerTest.php
│        │  │  │     │  ├─ RedisClusterSessionHandlerTest.php
│        │  │  │     │  ├─ RedisSessionHandlerTest.php
│        │  │  │     │  ├─ RelaySessionHandlerTest.php
│        │  │  │     │  ├─ SessionHandlerFactoryTest.php
│        │  │  │     │  ├─ StrictSessionHandlerTest.php
│        │  │  │     │  └─ stubs
│        │  │  │     │     └─ mongodb.php
│        │  │  │     ├─ MetadataBagTest.php
│        │  │  │     ├─ MockArraySessionStorageTest.php
│        │  │  │     ├─ MockFileSessionStorageTest.php
│        │  │  │     ├─ NativeSessionStorageTest.php
│        │  │  │     ├─ PhpBridgeSessionStorageTest.php
│        │  │  │     └─ Proxy
│        │  │  │        ├─ AbstractProxyTest.php
│        │  │  │        └─ SessionHandlerProxyTest.php
│        │  │  ├─ StreamedJsonResponseTest.php
│        │  │  ├─ StreamedResponseTest.php
│        │  │  ├─ Test
│        │  │  │  └─ Constraint
│        │  │  │     ├─ RequestAttributeValueSameTest.php
│        │  │  │     ├─ ResponseCookieValueSameTest.php
│        │  │  │     ├─ ResponseFormatSameTest.php
│        │  │  │     ├─ ResponseHasCookieTest.php
│        │  │  │     ├─ ResponseHasHeaderTest.php
│        │  │  │     ├─ ResponseHeaderLocationSameTest.php
│        │  │  │     ├─ ResponseHeaderSameTest.php
│        │  │  │     ├─ ResponseIsRedirectedTest.php
│        │  │  │     ├─ ResponseIsSuccessfulTest.php
│        │  │  │     ├─ ResponseIsUnprocessableTest.php
│        │  │  │     └─ ResponseStatusCodeSameTest.php
│        │  │  ├─ UriSignerTest.php
│        │  │  └─ UrlHelperTest.php
│        │  ├─ UriSigner.php
│        │  └─ UrlHelper.php
│        ├─ http-kernel
│        │  ├─ Attribute
│        │  │  ├─ AsController.php
│        │  │  ├─ AsTargetedValueResolver.php
│        │  │  ├─ Cache.php
│        │  │  ├─ MapDateTime.php
│        │  │  ├─ MapQueryParameter.php
│        │  │  ├─ MapQueryString.php
│        │  │  ├─ MapRequestPayload.php
│        │  │  ├─ MapUploadedFile.php
│        │  │  ├─ ValueResolver.php
│        │  │  ├─ WithHttpStatus.php
│        │  │  └─ WithLogLevel.php
│        │  ├─ Bundle
│        │  │  ├─ AbstractBundle.php
│        │  │  ├─ Bundle.php
│        │  │  ├─ BundleExtension.php
│        │  │  └─ BundleInterface.php
│        │  ├─ CacheClearer
│        │  │  ├─ CacheClearerInterface.php
│        │  │  ├─ ChainCacheClearer.php
│        │  │  └─ Psr6CacheClearer.php
│        │  ├─ CacheWarmer
│        │  │  ├─ CacheWarmer.php
│        │  │  ├─ CacheWarmerAggregate.php
│        │  │  ├─ CacheWarmerInterface.php
│        │  │  └─ WarmableInterface.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ Config
│        │  │  └─ FileLocator.php
│        │  ├─ Controller
│        │  │  ├─ ArgumentResolver
│        │  │  │  ├─ BackedEnumValueResolver.php
│        │  │  │  ├─ DateTimeValueResolver.php
│        │  │  │  ├─ DefaultValueResolver.php
│        │  │  │  ├─ NotTaggedControllerValueResolver.php
│        │  │  │  ├─ QueryParameterValueResolver.php
│        │  │  │  ├─ RequestAttributeValueResolver.php
│        │  │  │  ├─ RequestPayloadValueResolver.php
│        │  │  │  ├─ RequestValueResolver.php
│        │  │  │  ├─ ServiceValueResolver.php
│        │  │  │  ├─ SessionValueResolver.php
│        │  │  │  ├─ TraceableValueResolver.php
│        │  │  │  ├─ UidValueResolver.php
│        │  │  │  └─ VariadicValueResolver.php
│        │  │  ├─ ArgumentResolver.php
│        │  │  ├─ ArgumentResolverInterface.php
│        │  │  ├─ ContainerControllerResolver.php
│        │  │  ├─ ControllerReference.php
│        │  │  ├─ ControllerResolver.php
│        │  │  ├─ ControllerResolverInterface.php
│        │  │  ├─ ErrorController.php
│        │  │  ├─ TraceableArgumentResolver.php
│        │  │  ├─ TraceableControllerResolver.php
│        │  │  └─ ValueResolverInterface.php
│        │  ├─ ControllerMetadata
│        │  │  ├─ ArgumentMetadata.php
│        │  │  ├─ ArgumentMetadataFactory.php
│        │  │  └─ ArgumentMetadataFactoryInterface.php
│        │  ├─ DataCollector
│        │  │  ├─ AjaxDataCollector.php
│        │  │  ├─ ConfigDataCollector.php
│        │  │  ├─ DataCollector.php
│        │  │  ├─ DataCollectorInterface.php
│        │  │  ├─ DumpDataCollector.php
│        │  │  ├─ EventDataCollector.php
│        │  │  ├─ ExceptionDataCollector.php
│        │  │  ├─ LateDataCollectorInterface.php
│        │  │  ├─ LoggerDataCollector.php
│        │  │  ├─ MemoryDataCollector.php
│        │  │  ├─ RequestDataCollector.php
│        │  │  ├─ RouterDataCollector.php
│        │  │  └─ TimeDataCollector.php
│        │  ├─ Debug
│        │  │  ├─ ErrorHandlerConfigurator.php
│        │  │  ├─ TraceableEventDispatcher.php
│        │  │  └─ VirtualRequestStack.php
│        │  ├─ DependencyInjection
│        │  │  ├─ AddAnnotatedClassesToCachePass.php
│        │  │  ├─ ConfigurableExtension.php
│        │  │  ├─ ControllerArgumentValueResolverPass.php
│        │  │  ├─ Extension.php
│        │  │  ├─ FragmentRendererPass.php
│        │  │  ├─ LazyLoadingFragmentHandler.php
│        │  │  ├─ LoggerPass.php
│        │  │  ├─ MergeExtensionConfigurationPass.php
│        │  │  ├─ RegisterControllerArgumentLocatorsPass.php
│        │  │  ├─ RegisterLocaleAwareServicesPass.php
│        │  │  ├─ RemoveEmptyControllerArgumentLocatorsPass.php
│        │  │  ├─ ResettableServicePass.php
│        │  │  ├─ ServicesResetter.php
│        │  │  └─ ServicesResetterInterface.php
│        │  ├─ Event
│        │  │  ├─ ControllerArgumentsEvent.php
│        │  │  ├─ ControllerEvent.php
│        │  │  ├─ ExceptionEvent.php
│        │  │  ├─ FinishRequestEvent.php
│        │  │  ├─ KernelEvent.php
│        │  │  ├─ RequestEvent.php
│        │  │  ├─ ResponseEvent.php
│        │  │  ├─ TerminateEvent.php
│        │  │  └─ ViewEvent.php
│        │  ├─ EventListener
│        │  │  ├─ AbstractSessionListener.php
│        │  │  ├─ AddRequestFormatsListener.php
│        │  │  ├─ CacheAttributeListener.php
│        │  │  ├─ DebugHandlersListener.php
│        │  │  ├─ DisallowRobotsIndexingListener.php
│        │  │  ├─ DumpListener.php
│        │  │  ├─ ErrorListener.php
│        │  │  ├─ FragmentListener.php
│        │  │  ├─ LocaleAwareListener.php
│        │  │  ├─ LocaleListener.php
│        │  │  ├─ ProfilerListener.php
│        │  │  ├─ ResponseListener.php
│        │  │  ├─ RouterListener.php
│        │  │  ├─ SessionListener.php
│        │  │  ├─ SurrogateListener.php
│        │  │  └─ ValidateRequestListener.php
│        │  ├─ Exception
│        │  │  ├─ AccessDeniedHttpException.php
│        │  │  ├─ BadRequestHttpException.php
│        │  │  ├─ ConflictHttpException.php
│        │  │  ├─ ControllerDoesNotReturnResponseException.php
│        │  │  ├─ GoneHttpException.php
│        │  │  ├─ HttpException.php
│        │  │  ├─ HttpExceptionInterface.php
│        │  │  ├─ InvalidMetadataException.php
│        │  │  ├─ LengthRequiredHttpException.php
│        │  │  ├─ LockedHttpException.php
│        │  │  ├─ MethodNotAllowedHttpException.php
│        │  │  ├─ NearMissValueResolverException.php
│        │  │  ├─ NotAcceptableHttpException.php
│        │  │  ├─ NotFoundHttpException.php
│        │  │  ├─ PreconditionFailedHttpException.php
│        │  │  ├─ PreconditionRequiredHttpException.php
│        │  │  ├─ ResolverNotFoundException.php
│        │  │  ├─ ServiceUnavailableHttpException.php
│        │  │  ├─ TooManyRequestsHttpException.php
│        │  │  ├─ UnauthorizedHttpException.php
│        │  │  ├─ UnexpectedSessionUsageException.php
│        │  │  ├─ UnprocessableEntityHttpException.php
│        │  │  └─ UnsupportedMediaTypeHttpException.php
│        │  ├─ Fragment
│        │  │  ├─ AbstractSurrogateFragmentRenderer.php
│        │  │  ├─ EsiFragmentRenderer.php
│        │  │  ├─ FragmentHandler.php
│        │  │  ├─ FragmentRendererInterface.php
│        │  │  ├─ FragmentUriGenerator.php
│        │  │  ├─ FragmentUriGeneratorInterface.php
│        │  │  ├─ HIncludeFragmentRenderer.php
│        │  │  ├─ InlineFragmentRenderer.php
│        │  │  ├─ RoutableFragmentRenderer.php
│        │  │  └─ SsiFragmentRenderer.php
│        │  ├─ HttpCache
│        │  │  ├─ AbstractSurrogate.php
│        │  │  ├─ Esi.php
│        │  │  ├─ HttpCache.php
│        │  │  ├─ ResponseCacheStrategy.php
│        │  │  ├─ ResponseCacheStrategyInterface.php
│        │  │  ├─ Ssi.php
│        │  │  ├─ Store.php
│        │  │  ├─ StoreInterface.php
│        │  │  ├─ SubRequestHandler.php
│        │  │  └─ SurrogateInterface.php
│        │  ├─ HttpClientKernel.php
│        │  ├─ HttpKernel.php
│        │  ├─ HttpKernelBrowser.php
│        │  ├─ HttpKernelInterface.php
│        │  ├─ Kernel.php
│        │  ├─ KernelEvents.php
│        │  ├─ KernelInterface.php
│        │  ├─ LICENSE
│        │  ├─ Log
│        │  │  ├─ DebugLoggerConfigurator.php
│        │  │  ├─ DebugLoggerInterface.php
│        │  │  └─ Logger.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ Profiler
│        │  │  ├─ FileProfilerStorage.php
│        │  │  ├─ Profile.php
│        │  │  ├─ Profiler.php
│        │  │  ├─ ProfilerStateChecker.php
│        │  │  └─ ProfilerStorageInterface.php
│        │  ├─ README.md
│        │  ├─ RebootableInterface.php
│        │  ├─ Resources
│        │  │  └─ welcome.html.php
│        │  ├─ TerminableInterface.php
│        │  └─ Tests
│        │     ├─ Attribute
│        │     │  └─ WithLogLevelTest.php
│        │     ├─ Bundle
│        │     │  └─ BundleTest.php
│        │     ├─ CacheClearer
│        │     │  ├─ ChainCacheClearerTest.php
│        │     │  └─ Psr6CacheClearerTest.php
│        │     ├─ CacheWarmer
│        │     │  ├─ CacheWarmerAggregateTest.php
│        │     │  └─ CacheWarmerTest.php
│        │     ├─ Config
│        │     │  └─ FileLocatorTest.php
│        │     ├─ Controller
│        │     │  ├─ ArgumentResolver
│        │     │  │  ├─ BackedEnumValueResolverTest.php
│        │     │  │  ├─ DateTimeValueResolverTest.php
│        │     │  │  ├─ NotTaggedControllerValueResolverTest.php
│        │     │  │  ├─ QueryParameterValueResolverTest.php
│        │     │  │  ├─ RequestPayloadValueResolverTest.php
│        │     │  │  ├─ RequestValueResolverTest.php
│        │     │  │  ├─ ServiceValueResolverTest.php
│        │     │  │  ├─ TraceableValueResolverTest.php
│        │     │  │  ├─ UidValueResolverTest.php
│        │     │  │  └─ UploadedFileValueResolverTest.php
│        │     │  ├─ ArgumentResolverTest.php
│        │     │  ├─ ContainerControllerResolverTest.php
│        │     │  ├─ ControllerResolverTest.php
│        │     │  ├─ ErrorControllerTest.php
│        │     │  ├─ TraceableArgumentResolverTest.php
│        │     │  └─ TraceableControllerResolverTest.php
│        │     ├─ ControllerMetadata
│        │     │  ├─ ArgumentMetadataFactoryTest.php
│        │     │  └─ ArgumentMetadataTest.php
│        │     ├─ DataCollector
│        │     │  ├─ Compiler.log
│        │     │  ├─ ConfigDataCollectorTest.php
│        │     │  ├─ DataCollectorTest.php
│        │     │  ├─ DumpDataCollectorTest.php
│        │     │  ├─ ExceptionDataCollectorTest.php
│        │     │  ├─ LoggerDataCollectorTest.php
│        │     │  ├─ MemoryDataCollectorTest.php
│        │     │  ├─ RequestDataCollectorTest.php
│        │     │  ├─ RouterDataCollectorTest.php
│        │     │  └─ TimeDataCollectorTest.php
│        │     ├─ Debug
│        │     │  ├─ ErrorHandlerConfiguratorTest.php
│        │     │  └─ TraceableEventDispatcherTest.php
│        │     ├─ DependencyInjection
│        │     │  ├─ AddAnnotatedClassesToCachePassTest.php
│        │     │  ├─ ControllerArgumentValueResolverPassTest.php
│        │     │  ├─ FragmentRendererPassTest.php
│        │     │  ├─ LazyLoadingFragmentHandlerTest.php
│        │     │  ├─ LoggerPassTest.php
│        │     │  ├─ MergeExtensionConfigurationPassTest.php
│        │     │  ├─ RegisterControllerArgumentLocatorsPassTest.php
│        │     │  ├─ RegisterLocaleAwareServicesPassTest.php
│        │     │  ├─ RemoveEmptyControllerArgumentLocatorsPassTest.php
│        │     │  ├─ ResettableServicePassTest.php
│        │     │  └─ ServicesResetterTest.php
│        │     ├─ Event
│        │     │  ├─ ControllerArgumentsEventTest.php
│        │     │  ├─ ControllerEventTest.php
│        │     │  └─ ExceptionEventTest.php
│        │     ├─ EventListener
│        │     │  ├─ AddRequestFormatsListenerTest.php
│        │     │  ├─ CacheAttributeListenerTest.php
│        │     │  ├─ DebugHandlersListenerTest.php
│        │     │  ├─ DisallowRobotsIndexingListenerTest.php
│        │     │  ├─ DumpListenerTest.php
│        │     │  ├─ ErrorListenerTest.php
│        │     │  ├─ FragmentListenerTest.php
│        │     │  ├─ LocaleAwareListenerTest.php
│        │     │  ├─ LocaleListenerTest.php
│        │     │  ├─ ProfilerListenerTest.php
│        │     │  ├─ ResponseListenerTest.php
│        │     │  ├─ RouterListenerTest.php
│        │     │  ├─ SessionListenerTest.php
│        │     │  ├─ SurrogateListenerTest.php
│        │     │  └─ ValidateRequestListenerTest.php
│        │     ├─ Exception
│        │     │  ├─ AccessDeniedHttpExceptionTest.php
│        │     │  ├─ BadRequestHttpExceptionTest.php
│        │     │  ├─ ConflictHttpExceptionTest.php
│        │     │  ├─ GoneHttpExceptionTest.php
│        │     │  ├─ HttpExceptionTest.php
│        │     │  ├─ LengthRequiredHttpExceptionTest.php
│        │     │  ├─ LockedHttpExceptionTest.php
│        │     │  ├─ MethodNotAllowedHttpExceptionTest.php
│        │     │  ├─ NotAcceptableHttpExceptionTest.php
│        │     │  ├─ NotFoundHttpExceptionTest.php
│        │     │  ├─ PreconditionFailedHttpExceptionTest.php
│        │     │  ├─ PreconditionRequiredHttpExceptionTest.php
│        │     │  ├─ ServiceUnavailableHttpExceptionTest.php
│        │     │  ├─ TooManyRequestsHttpExceptionTest.php
│        │     │  ├─ UnauthorizedHttpExceptionTest.php
│        │     │  ├─ UnprocessableEntityHttpExceptionTest.php
│        │     │  └─ UnsupportedMediaTypeHttpExceptionTest.php
│        │     ├─ Fixtures
│        │     │  ├─ AcmeFooBundle
│        │     │  │  ├─ AcmeFooBundle.php
│        │     │  │  └─ Resources
│        │     │  │     └─ config
│        │     │  │        ├─ definition.php
│        │     │  │        └─ services.php
│        │     │  ├─ Attribute
│        │     │  │  ├─ Bar.php
│        │     │  │  ├─ Baz.php
│        │     │  │  └─ Foo.php
│        │     │  ├─ Bundle1Bundle
│        │     │  │  ├─ foo.txt
│        │     │  │  └─ Resources
│        │     │  ├─ ClearableService.php
│        │     │  ├─ Controller
│        │     │  │  ├─ ArgumentResolver
│        │     │  │  │  └─ UploadedFile
│        │     │  │  │     ├─ file-big.txt
│        │     │  │  │     └─ file-small.txt
│        │     │  │  ├─ AttributeController.php
│        │     │  │  ├─ BasicTypesController.php
│        │     │  │  ├─ CacheAttributeController.php
│        │     │  │  ├─ ExtendingRequest.php
│        │     │  │  ├─ ExtendingSession.php
│        │     │  │  ├─ NullableController.php
│        │     │  │  └─ VariadicController.php
│        │     │  ├─ DataCollector
│        │     │  │  ├─ CloneVarDataCollector.php
│        │     │  │  └─ DummyController.php
│        │     │  ├─ ExtensionNotValidBundle
│        │     │  │  ├─ DependencyInjection
│        │     │  │  │  └─ ExtensionNotValidExtension.php
│        │     │  │  └─ ExtensionNotValidBundle.php
│        │     │  ├─ ExtensionPresentBundle
│        │     │  │  ├─ DependencyInjection
│        │     │  │  │  └─ ExtensionPresentExtension.php
│        │     │  │  └─ ExtensionPresentBundle.php
│        │     │  ├─ IntEnum.php
│        │     │  ├─ KernelWithoutBundles.php
│        │     │  ├─ LazyResettableService.php
│        │     │  ├─ MockableUploadFileWithClientSize.php
│        │     │  ├─ MultiResettableService.php
│        │     │  ├─ ResettableService.php
│        │     │  ├─ Suit.php
│        │     │  ├─ TestClient.php
│        │     │  ├─ UsePropertyInDestruct.php
│        │     │  └─ WithPublicObjectProperty.php
│        │     ├─ Fragment
│        │     │  ├─ EsiFragmentRendererTest.php
│        │     │  ├─ FragmentHandlerTest.php
│        │     │  ├─ HIncludeFragmentRendererTest.php
│        │     │  ├─ InlineFragmentRendererTest.php
│        │     │  ├─ RoutableFragmentRendererTest.php
│        │     │  └─ SsiFragmentRendererTest.php
│        │     ├─ HttpCache
│        │     │  ├─ EsiTest.php
│        │     │  ├─ HttpCacheTest.php
│        │     │  ├─ HttpCacheTestCase.php
│        │     │  ├─ ResponseCacheStrategyTest.php
│        │     │  ├─ SsiTest.php
│        │     │  ├─ StoreTest.php
│        │     │  ├─ SubRequestHandlerTest.php
│        │     │  ├─ TestHttpKernel.php
│        │     │  └─ TestMultipleHttpKernel.php
│        │     ├─ HttpClientKernelTest.php
│        │     ├─ HttpKernelBrowserTest.php
│        │     ├─ HttpKernelTest.php
│        │     ├─ KernelTest.php
│        │     ├─ Log
│        │     │  └─ LoggerTest.php
│        │     ├─ Logger.php
│        │     ├─ Profiler
│        │     │  ├─ FileProfilerStorageTest.php
│        │     │  └─ ProfilerTest.php
│        │     └─ TestHttpKernel.php
│        ├─ polyfill-intl-grapheme
│        │  ├─ bootstrap.php
│        │  ├─ bootstrap80.php
│        │  ├─ composer.json
│        │  ├─ Grapheme.php
│        │  ├─ LICENSE
│        │  └─ README.md
│        ├─ polyfill-intl-normalizer
│        │  ├─ bootstrap.php
│        │  ├─ bootstrap80.php
│        │  ├─ composer.json
│        │  ├─ LICENSE
│        │  ├─ Normalizer.php
│        │  ├─ README.md
│        │  └─ Resources
│        │     ├─ stubs
│        │     │  └─ Normalizer.php
│        │     └─ unidata
│        │        ├─ canonicalComposition.php
│        │        ├─ canonicalDecomposition.php
│        │        ├─ combiningClass.php
│        │        └─ compatibilityDecomposition.php
│        ├─ polyfill-mbstring
│        │  ├─ bootstrap.php
│        │  ├─ bootstrap80.php
│        │  ├─ composer.json
│        │  ├─ LICENSE
│        │  ├─ Mbstring.php
│        │  ├─ README.md
│        │  └─ Resources
│        │     └─ unidata
│        │        ├─ caseFolding.php
│        │        ├─ lowerCase.php
│        │        ├─ titleCaseRegexp.php
│        │        └─ upperCase.php
│        ├─ polyfill-php83
│        │  ├─ bootstrap.php
│        │  ├─ bootstrap81.php
│        │  ├─ composer.json
│        │  ├─ LICENSE
│        │  ├─ Php83.php
│        │  ├─ README.md
│        │  └─ Resources
│        │     └─ stubs
│        │        ├─ DateError.php
│        │        ├─ DateException.php
│        │        ├─ DateInvalidOperationException.php
│        │        ├─ DateInvalidTimeZoneException.php
│        │        ├─ DateMalformedIntervalStringException.php
│        │        ├─ DateMalformedPeriodStringException.php
│        │        ├─ DateMalformedStringException.php
│        │        ├─ DateObjectError.php
│        │        ├─ DateRangeError.php
│        │        ├─ Override.php
│        │        └─ SQLite3Exception.php
│        ├─ routing
│        │  ├─ Alias.php
│        │  ├─ Annotation
│        │  │  └─ Route.php
│        │  ├─ Attribute
│        │  │  ├─ DeprecatedAlias.php
│        │  │  └─ Route.php
│        │  ├─ CHANGELOG.md
│        │  ├─ CompiledRoute.php
│        │  ├─ composer.json
│        │  ├─ DependencyInjection
│        │  │  ├─ AddExpressionLanguageProvidersPass.php
│        │  │  └─ RoutingResolverPass.php
│        │  ├─ Exception
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ InvalidArgumentException.php
│        │  │  ├─ InvalidParameterException.php
│        │  │  ├─ LogicException.php
│        │  │  ├─ MethodNotAllowedException.php
│        │  │  ├─ MissingMandatoryParametersException.php
│        │  │  ├─ NoConfigurationException.php
│        │  │  ├─ ResourceNotFoundException.php
│        │  │  ├─ RouteCircularReferenceException.php
│        │  │  ├─ RouteNotFoundException.php
│        │  │  └─ RuntimeException.php
│        │  ├─ Generator
│        │  │  ├─ CompiledUrlGenerator.php
│        │  │  ├─ ConfigurableRequirementsInterface.php
│        │  │  ├─ Dumper
│        │  │  │  ├─ CompiledUrlGeneratorDumper.php
│        │  │  │  ├─ GeneratorDumper.php
│        │  │  │  └─ GeneratorDumperInterface.php
│        │  │  ├─ UrlGenerator.php
│        │  │  └─ UrlGeneratorInterface.php
│        │  ├─ LICENSE
│        │  ├─ Loader
│        │  │  ├─ AttributeClassLoader.php
│        │  │  ├─ AttributeDirectoryLoader.php
│        │  │  ├─ AttributeFileLoader.php
│        │  │  ├─ ClosureLoader.php
│        │  │  ├─ Configurator
│        │  │  │  ├─ AliasConfigurator.php
│        │  │  │  ├─ CollectionConfigurator.php
│        │  │  │  ├─ ImportConfigurator.php
│        │  │  │  ├─ RouteConfigurator.php
│        │  │  │  ├─ RoutingConfigurator.php
│        │  │  │  └─ Traits
│        │  │  │     ├─ AddTrait.php
│        │  │  │     ├─ HostTrait.php
│        │  │  │     ├─ LocalizedRouteTrait.php
│        │  │  │     ├─ PrefixTrait.php
│        │  │  │     └─ RouteTrait.php
│        │  │  ├─ ContainerLoader.php
│        │  │  ├─ DirectoryLoader.php
│        │  │  ├─ GlobFileLoader.php
│        │  │  ├─ ObjectLoader.php
│        │  │  ├─ PhpFileLoader.php
│        │  │  ├─ Psr4DirectoryLoader.php
│        │  │  ├─ schema
│        │  │  │  └─ routing
│        │  │  │     └─ routing-1.0.xsd
│        │  │  ├─ XmlFileLoader.php
│        │  │  └─ YamlFileLoader.php
│        │  ├─ Matcher
│        │  │  ├─ CompiledUrlMatcher.php
│        │  │  ├─ Dumper
│        │  │  │  ├─ CompiledUrlMatcherDumper.php
│        │  │  │  ├─ CompiledUrlMatcherTrait.php
│        │  │  │  ├─ MatcherDumper.php
│        │  │  │  ├─ MatcherDumperInterface.php
│        │  │  │  └─ StaticPrefixCollection.php
│        │  │  ├─ ExpressionLanguageProvider.php
│        │  │  ├─ RedirectableUrlMatcher.php
│        │  │  ├─ RedirectableUrlMatcherInterface.php
│        │  │  ├─ RequestMatcherInterface.php
│        │  │  ├─ TraceableUrlMatcher.php
│        │  │  ├─ UrlMatcher.php
│        │  │  └─ UrlMatcherInterface.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ RequestContext.php
│        │  ├─ RequestContextAwareInterface.php
│        │  ├─ Requirement
│        │  │  ├─ EnumRequirement.php
│        │  │  └─ Requirement.php
│        │  ├─ Route.php
│        │  ├─ RouteCollection.php
│        │  ├─ RouteCompiler.php
│        │  ├─ RouteCompilerInterface.php
│        │  ├─ Router.php
│        │  ├─ RouterInterface.php
│        │  └─ Tests
│        │     ├─ Attribute
│        │     │  └─ RouteTest.php
│        │     ├─ CompiledRouteTest.php
│        │     ├─ DependencyInjection
│        │     │  ├─ AddExpressionLanguageProvidersPassTest.php
│        │     │  └─ RoutingResolverPassTest.php
│        │     ├─ Fixtures
│        │     │  ├─ alias
│        │     │  │  ├─ alias.php
│        │     │  │  ├─ alias.xml
│        │     │  │  ├─ alias.yaml
│        │     │  │  ├─ expected.php
│        │     │  │  ├─ invalid-alias.yaml
│        │     │  │  ├─ invalid-deprecated-no-package.xml
│        │     │  │  ├─ invalid-deprecated-no-package.yaml
│        │     │  │  ├─ invalid-deprecated-no-version.xml
│        │     │  │  ├─ invalid-deprecated-no-version.yaml
│        │     │  │  └─ override.yaml
│        │     │  ├─ annotated.php
│        │     │  ├─ AttributedClasses
│        │     │  │  ├─ AbstractClass.php
│        │     │  │  ├─ BarClass.php
│        │     │  │  ├─ BazClass.php
│        │     │  │  ├─ EncodingClass.php
│        │     │  │  ├─ FooClass.php
│        │     │  │  └─ FooTrait.php
│        │     │  ├─ AttributeFixtures
│        │     │  │  ├─ AbstractClassController.php
│        │     │  │  ├─ ActionPathController.php
│        │     │  │  ├─ AliasClassController.php
│        │     │  │  ├─ AliasInvokableController.php
│        │     │  │  ├─ AliasRouteController.php
│        │     │  │  ├─ BazClass.php
│        │     │  │  ├─ DefaultValueController.php
│        │     │  │  ├─ DeprecatedAliasCustomMessageRouteController.php
│        │     │  │  ├─ DeprecatedAliasRouteController.php
│        │     │  │  ├─ EncodingClass.php
│        │     │  │  ├─ ExplicitLocalizedActionPathController.php
│        │     │  │  ├─ ExtendedRoute.php
│        │     │  │  ├─ ExtendedRouteOnClassController.php
│        │     │  │  ├─ ExtendedRouteOnMethodController.php
│        │     │  │  ├─ FooController.php
│        │     │  │  ├─ GlobalDefaultsClass.php
│        │     │  │  ├─ InvokableController.php
│        │     │  │  ├─ InvokableFQCNAliasConflictController.php
│        │     │  │  ├─ InvokableLocalizedController.php
│        │     │  │  ├─ InvokableMethodController.php
│        │     │  │  ├─ LocalizedActionPathController.php
│        │     │  │  ├─ LocalizedMethodActionControllers.php
│        │     │  │  ├─ LocalizedPrefixLocalizedActionController.php
│        │     │  │  ├─ LocalizedPrefixMissingLocaleActionController.php
│        │     │  │  ├─ LocalizedPrefixMissingRouteLocaleActionController.php
│        │     │  │  ├─ LocalizedPrefixWithRouteWithoutLocale.php
│        │     │  │  ├─ MethodActionControllers.php
│        │     │  │  ├─ MethodsAndSchemes.php
│        │     │  │  ├─ MissingRouteNameController.php
│        │     │  │  ├─ MultipleDeprecatedAliasRouteController.php
│        │     │  │  ├─ NothingButNameController.php
│        │     │  │  ├─ PrefixedActionLocalizedRouteController.php
│        │     │  │  ├─ PrefixedActionPathController.php
│        │     │  │  ├─ RequirementsWithoutPlaceholderNameController.php
│        │     │  │  ├─ RouteWithEnv.php
│        │     │  │  ├─ RouteWithPrefixController.php
│        │     │  │  ├─ RouteWithPriorityController.php
│        │     │  │  └─ Utf8ActionControllers.php
│        │     │  ├─ Attributes
│        │     │  │  └─ FooAttributes.php
│        │     │  ├─ AttributesFixtures
│        │     │  │  ├─ AttributesClassParamAfterCommaController.php
│        │     │  │  ├─ AttributesClassParamAfterParenthesisController.php
│        │     │  │  ├─ AttributesClassParamInlineAfterCommaController.php
│        │     │  │  ├─ AttributesClassParamInlineAfterParenthesisController.php
│        │     │  │  ├─ AttributesClassParamInlineQuotedAfterCommaController.php
│        │     │  │  ├─ AttributesClassParamInlineQuotedAfterParenthesisController.php
│        │     │  │  ├─ AttributesClassParamQuotedAfterCommaController.php
│        │     │  │  └─ AttributesClassParamQuotedAfterParenthesisController.php
│        │     │  ├─ bad_format.yml
│        │     │  ├─ bar.xml
│        │     │  ├─ class-attributes.php
│        │     │  ├─ class-attributes.xml
│        │     │  ├─ class-attributes.yaml
│        │     │  ├─ collection-defaults.php
│        │     │  ├─ controller
│        │     │  │  ├─ empty_wildcard
│        │     │  │  ├─ import_controller.xml
│        │     │  │  ├─ import_controller.yml
│        │     │  │  ├─ import_override_defaults.xml
│        │     │  │  ├─ import_override_defaults.yml
│        │     │  │  ├─ import__controller.xml
│        │     │  │  ├─ import__controller.yml
│        │     │  │  ├─ override_defaults.xml
│        │     │  │  ├─ override_defaults.yml
│        │     │  │  ├─ routing.xml
│        │     │  │  └─ routing.yml
│        │     │  ├─ CustomCompiledRoute.php
│        │     │  ├─ CustomRouteCompiler.php
│        │     │  ├─ CustomXmlFileLoader.php
│        │     │  ├─ defaults.php
│        │     │  ├─ defaults.xml
│        │     │  ├─ defaults.yml
│        │     │  ├─ directory
│        │     │  │  ├─ recurse
│        │     │  │  │  ├─ routes1.yml
│        │     │  │  │  └─ routes2.yml
│        │     │  │  └─ routes3.yml
│        │     │  ├─ directory_import
│        │     │  │  └─ import.yml
│        │     │  ├─ dumper
│        │     │  │  ├─ compiled_url_matcher0.php
│        │     │  │  ├─ compiled_url_matcher1.php
│        │     │  │  ├─ compiled_url_matcher10.php
│        │     │  │  ├─ compiled_url_matcher11.php
│        │     │  │  ├─ compiled_url_matcher12.php
│        │     │  │  ├─ compiled_url_matcher13.php
│        │     │  │  ├─ compiled_url_matcher14.php
│        │     │  │  ├─ compiled_url_matcher2.php
│        │     │  │  ├─ compiled_url_matcher3.php
│        │     │  │  ├─ compiled_url_matcher4.php
│        │     │  │  ├─ compiled_url_matcher5.php
│        │     │  │  ├─ compiled_url_matcher6.php
│        │     │  │  ├─ compiled_url_matcher7.php
│        │     │  │  ├─ compiled_url_matcher8.php
│        │     │  │  └─ compiled_url_matcher9.php
│        │     │  ├─ empty.yml
│        │     │  ├─ Enum
│        │     │  │  ├─ TestIntBackedEnum.php
│        │     │  │  ├─ TestStringBackedEnum.php
│        │     │  │  ├─ TestStringBackedEnum2.php
│        │     │  │  └─ TestUnitEnum.php
│        │     │  ├─ file_resource.yml
│        │     │  ├─ foo.xml
│        │     │  ├─ foo1.xml
│        │     │  ├─ glob
│        │     │  │  ├─ bar.xml
│        │     │  │  ├─ bar.yml
│        │     │  │  ├─ baz.xml
│        │     │  │  ├─ baz.yml
│        │     │  │  ├─ import_multiple.xml
│        │     │  │  ├─ import_multiple.yml
│        │     │  │  ├─ import_single.xml
│        │     │  │  ├─ import_single.yml
│        │     │  │  ├─ php_dsl.php
│        │     │  │  ├─ php_dsl_bar.php
│        │     │  │  └─ php_dsl_baz.php
│        │     │  ├─ imported-with-defaults.php
│        │     │  ├─ imported-with-defaults.xml
│        │     │  ├─ imported-with-defaults.yml
│        │     │  ├─ importer-with-defaults.php
│        │     │  ├─ importer-with-defaults.xml
│        │     │  ├─ importer-with-defaults.yml
│        │     │  ├─ import_with_name_prefix
│        │     │  │  ├─ routing.xml
│        │     │  │  └─ routing.yml
│        │     │  ├─ import_with_no_trailing_slash
│        │     │  │  ├─ routing.xml
│        │     │  │  └─ routing.yml
│        │     │  ├─ incomplete.yml
│        │     │  ├─ list_defaults.xml
│        │     │  ├─ list_in_list_defaults.xml
│        │     │  ├─ list_in_map_defaults.xml
│        │     │  ├─ list_null_values.xml
│        │     │  ├─ locale_and_host
│        │     │  │  ├─ import-with-host-expected-collection.php
│        │     │  │  ├─ import-with-locale-and-host-expected-collection.php
│        │     │  │  ├─ import-with-single-host-expected-collection.php
│        │     │  │  ├─ import-without-host-expected-collection.php
│        │     │  │  ├─ imported.php
│        │     │  │  ├─ imported.xml
│        │     │  │  ├─ imported.yml
│        │     │  │  ├─ importer-with-host.php
│        │     │  │  ├─ importer-with-host.xml
│        │     │  │  ├─ importer-with-host.yml
│        │     │  │  ├─ importer-with-locale-and-host.php
│        │     │  │  ├─ importer-with-locale-and-host.xml
│        │     │  │  ├─ importer-with-locale-and-host.yml
│        │     │  │  ├─ importer-with-single-host.php
│        │     │  │  ├─ importer-with-single-host.xml
│        │     │  │  ├─ importer-with-single-host.yml
│        │     │  │  ├─ importer-without-host.php
│        │     │  │  ├─ importer-without-host.xml
│        │     │  │  ├─ importer-without-host.yml
│        │     │  │  ├─ priorized-host.yml
│        │     │  │  ├─ route-with-hosts-expected-collection.php
│        │     │  │  ├─ route-with-hosts.php
│        │     │  │  ├─ route-with-hosts.xml
│        │     │  │  └─ route-with-hosts.yml
│        │     │  ├─ localized
│        │     │  │  ├─ imported-with-locale-but-not-localized.xml
│        │     │  │  ├─ imported-with-locale-but-not-localized.yml
│        │     │  │  ├─ imported-with-locale.xml
│        │     │  │  ├─ imported-with-locale.yml
│        │     │  │  ├─ imported-with-utf8.php
│        │     │  │  ├─ imported-with-utf8.xml
│        │     │  │  ├─ imported-with-utf8.yml
│        │     │  │  ├─ importer-with-controller-default.yml
│        │     │  │  ├─ importer-with-locale-imports-non-localized-route.xml
│        │     │  │  ├─ importer-with-locale-imports-non-localized-route.yml
│        │     │  │  ├─ importer-with-locale.xml
│        │     │  │  ├─ importer-with-locale.yml
│        │     │  │  ├─ importer-with-utf8.php
│        │     │  │  ├─ importer-with-utf8.xml
│        │     │  │  ├─ importer-with-utf8.yml
│        │     │  │  ├─ importing-localized-route.yml
│        │     │  │  ├─ localized-prefix.yml
│        │     │  │  ├─ localized-route.yml
│        │     │  │  ├─ missing-locale-in-importer.yml
│        │     │  │  ├─ not-localized.yml
│        │     │  │  ├─ officially_formatted_locales.yml
│        │     │  │  ├─ route-without-path-or-locales.yml
│        │     │  │  ├─ utf8.php
│        │     │  │  ├─ utf8.xml
│        │     │  │  └─ utf8.yml
│        │     │  ├─ localized.xml
│        │     │  ├─ map_defaults.xml
│        │     │  ├─ map_in_list_defaults.xml
│        │     │  ├─ map_in_map_defaults.xml
│        │     │  ├─ map_null_values.xml
│        │     │  ├─ missing_id.xml
│        │     │  ├─ missing_path.xml
│        │     │  ├─ namespaceprefix.xml
│        │     │  ├─ nonesense_resource_plus_path.yml
│        │     │  ├─ nonesense_type_without_resource.yml
│        │     │  ├─ nonvalid-deprecated-route.xml
│        │     │  ├─ nonvalid.xml
│        │     │  ├─ nonvalid.yml
│        │     │  ├─ nonvalid2.yml
│        │     │  ├─ nonvalidkeys.yml
│        │     │  ├─ nonvalidnode.xml
│        │     │  ├─ nonvalidroute.xml
│        │     │  ├─ null_values.xml
│        │     │  ├─ OtherAnnotatedClasses
│        │     │  │  ├─ NoStartTagClass.php
│        │     │  │  └─ VariadicClass.php
│        │     │  ├─ php_dsl.php
│        │     │  ├─ php_dsl_i18n.php
│        │     │  ├─ php_dsl_sub.php
│        │     │  ├─ php_dsl_sub_i18n.php
│        │     │  ├─ php_dsl_sub_root.php
│        │     │  ├─ php_object_dsl.php
│        │     │  ├─ psr4-attributes.php
│        │     │  ├─ psr4-attributes.xml
│        │     │  ├─ psr4-attributes.yaml
│        │     │  ├─ psr4-controllers-redirection
│        │     │  │  ├─ psr4-attributes.php
│        │     │  │  ├─ psr4-attributes.xml
│        │     │  │  └─ psr4-attributes.yaml
│        │     │  ├─ psr4-controllers-redirection.php
│        │     │  ├─ psr4-controllers-redirection.xml
│        │     │  ├─ psr4-controllers-redirection.yaml
│        │     │  ├─ Psr4Controllers
│        │     │  │  ├─ MyController.php
│        │     │  │  ├─ MyUnannotatedController.php
│        │     │  │  └─ SubNamespace
│        │     │  │     ├─ EvenDeeperNamespace
│        │     │  │     │  └─ MyOtherController.php
│        │     │  │     ├─ IrrelevantClass.php
│        │     │  │     ├─ IrrelevantEnum.php
│        │     │  │     ├─ IrrelevantInterface.php
│        │     │  │     ├─ MyAbstractController.php
│        │     │  │     ├─ MyChildController.php
│        │     │  │     ├─ MyControllerWithATrait.php
│        │     │  │     └─ SomeSharedImplementation.php
│        │     │  ├─ RedirectableUrlMatcher.php
│        │     │  ├─ requirements_without_placeholder_name.yml
│        │     │  ├─ scalar_defaults.xml
│        │     │  ├─ special_route_name.yml
│        │     │  ├─ TraceableAttributeClassLoader.php
│        │     │  ├─ validpattern.php
│        │     │  ├─ validpattern.xml
│        │     │  ├─ validpattern.yml
│        │     │  ├─ validresource.php
│        │     │  ├─ validresource.xml
│        │     │  ├─ validresource.yml
│        │     │  ├─ when-env.xml
│        │     │  ├─ when-env.yml
│        │     │  ├─ withdoctype.xml
│        │     │  └─ with_define_path_variable.php
│        │     ├─ Generator
│        │     │  ├─ Dumper
│        │     │  │  └─ CompiledUrlGeneratorDumperTest.php
│        │     │  └─ UrlGeneratorTest.php
│        │     ├─ Loader
│        │     │  ├─ AttributeClassLoaderTest.php
│        │     │  ├─ AttributeDirectoryLoaderTest.php
│        │     │  ├─ AttributeFileLoaderTest.php
│        │     │  ├─ ClosureLoaderTest.php
│        │     │  ├─ ContainerLoaderTest.php
│        │     │  ├─ DirectoryLoaderTest.php
│        │     │  ├─ FileLocatorStub.php
│        │     │  ├─ GlobFileLoaderTest.php
│        │     │  ├─ ObjectLoaderTest.php
│        │     │  ├─ PhpFileLoaderTest.php
│        │     │  ├─ Psr4DirectoryLoaderTest.php
│        │     │  ├─ XmlFileLoaderTest.php
│        │     │  └─ YamlFileLoaderTest.php
│        │     ├─ Matcher
│        │     │  ├─ CompiledRedirectableUrlMatcherTest.php
│        │     │  ├─ CompiledUrlMatcherTest.php
│        │     │  ├─ Dumper
│        │     │  │  ├─ CompiledUrlMatcherDumperTest.php
│        │     │  │  └─ StaticPrefixCollectionTest.php
│        │     │  ├─ ExpressionLanguageProviderTest.php
│        │     │  ├─ RedirectableUrlMatcherTest.php
│        │     │  ├─ TraceableUrlMatcherTest.php
│        │     │  └─ UrlMatcherTest.php
│        │     ├─ RequestContextTest.php
│        │     ├─ Requirement
│        │     │  ├─ EnumRequirementTest.php
│        │     │  └─ RequirementTest.php
│        │     ├─ RouteCollectionTest.php
│        │     ├─ RouteCompilerTest.php
│        │     ├─ RouterTest.php
│        │     └─ RouteTest.php
│        ├─ runtime
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ GenericRuntime.php
│        │  ├─ Internal
│        │  │  ├─ autoload_runtime.template
│        │  │  ├─ BasicErrorHandler.php
│        │  │  ├─ ComposerPlugin.php
│        │  │  ├─ Console
│        │  │  │  ├─ ApplicationRuntime.php
│        │  │  │  ├─ Command
│        │  │  │  │  └─ CommandRuntime.php
│        │  │  │  ├─ Input
│        │  │  │  │  └─ InputInterfaceRuntime.php
│        │  │  │  └─ Output
│        │  │  │     └─ OutputInterfaceRuntime.php
│        │  │  ├─ HttpFoundation
│        │  │  │  ├─ RequestRuntime.php
│        │  │  │  └─ ResponseRuntime.php
│        │  │  ├─ HttpKernel
│        │  │  │  └─ HttpKernelInterfaceRuntime.php
│        │  │  ├─ MissingDotenv.php
│        │  │  └─ SymfonyErrorHandler.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Resolver
│        │  │  ├─ ClosureResolver.php
│        │  │  └─ DebugClosureResolver.php
│        │  ├─ ResolverInterface.php
│        │  ├─ Runner
│        │  │  ├─ ClosureRunner.php
│        │  │  └─ Symfony
│        │  │     ├─ ConsoleApplicationRunner.php
│        │  │     ├─ HttpKernelRunner.php
│        │  │     └─ ResponseRunner.php
│        │  ├─ RunnerInterface.php
│        │  ├─ RuntimeInterface.php
│        │  ├─ SymfonyRuntime.php
│        │  └─ Tests
│        │     └─ phpt
│        │        ├─ .env
│        │        ├─ .env.extra
│        │        ├─ application.php
│        │        ├─ application.phpt
│        │        ├─ autoload.php
│        │        ├─ command.php
│        │        ├─ command.phpt
│        │        ├─ command2.php
│        │        ├─ command2.phpt
│        │        ├─ command_list.php
│        │        ├─ command_list.phpt
│        │        ├─ dotenv_extra_load.php
│        │        ├─ dotenv_extra_load.phpt
│        │        ├─ dotenv_extra_overload.php
│        │        ├─ dotenv_extra_overload.phpt
│        │        ├─ dotenv_overload.php
│        │        ├─ dotenv_overload.phpt
│        │        ├─ dotenv_overload_command_debug_exists_0_to_1.php
│        │        ├─ dotenv_overload_command_debug_exists_0_to_1.phpt
│        │        ├─ dotenv_overload_command_debug_exists_1_to_0.php
│        │        ├─ dotenv_overload_command_debug_exists_1_to_0.phpt
│        │        ├─ dotenv_overload_command_env_conflict.php
│        │        ├─ dotenv_overload_command_env_conflict.phpt
│        │        ├─ dotenv_overload_command_env_exists.php
│        │        ├─ dotenv_overload_command_env_exists.phpt
│        │        ├─ dotenv_overload_command_no_debug.php
│        │        ├─ dotenv_overload_command_no_debug.phpt
│        │        ├─ generic-request.php
│        │        ├─ generic-request.phpt
│        │        ├─ hello.php
│        │        ├─ hello.phpt
│        │        ├─ kernel-loop.php
│        │        ├─ kernel-loop.phpt
│        │        ├─ kernel.php
│        │        ├─ kernel.phpt
│        │        ├─ kernel_register_argc_argv.phpt
│        │        ├─ request.php
│        │        ├─ request.phpt
│        │        ├─ runtime-options.php
│        │        └─ runtime-options.phpt
│        ├─ service-contracts
│        │  ├─ Attribute
│        │  │  ├─ Required.php
│        │  │  └─ SubscribedService.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ LICENSE
│        │  ├─ README.md
│        │  ├─ ResetInterface.php
│        │  ├─ ServiceCollectionInterface.php
│        │  ├─ ServiceLocatorTrait.php
│        │  ├─ ServiceMethodsSubscriberTrait.php
│        │  ├─ ServiceProviderInterface.php
│        │  ├─ ServiceSubscriberInterface.php
│        │  ├─ ServiceSubscriberTrait.php
│        │  └─ Test
│        │     ├─ ServiceLocatorTest.php
│        │     └─ ServiceLocatorTestCase.php
│        ├─ string
│        │  ├─ AbstractString.php
│        │  ├─ AbstractUnicodeString.php
│        │  ├─ ByteString.php
│        │  ├─ CHANGELOG.md
│        │  ├─ CodePointString.php
│        │  ├─ composer.json
│        │  ├─ Exception
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ InvalidArgumentException.php
│        │  │  └─ RuntimeException.php
│        │  ├─ Inflector
│        │  │  ├─ EnglishInflector.php
│        │  │  ├─ FrenchInflector.php
│        │  │  ├─ InflectorInterface.php
│        │  │  └─ SpanishInflector.php
│        │  ├─ LazyString.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Resources
│        │  │  ├─ bin
│        │  │  │  └─ update-data.php
│        │  │  ├─ data
│        │  │  │  ├─ wcswidth_table_wide.php
│        │  │  │  └─ wcswidth_table_zero.php
│        │  │  ├─ functions.php
│        │  │  └─ WcswidthDataGenerator.php
│        │  ├─ Slugger
│        │  │  ├─ AsciiSlugger.php
│        │  │  └─ SluggerInterface.php
│        │  ├─ Tests
│        │  │  ├─ AbstractAsciiTestCase.php
│        │  │  ├─ AbstractUnicodeTestCase.php
│        │  │  ├─ ByteStringTest.php
│        │  │  ├─ CodePointStringTest.php
│        │  │  ├─ FunctionsTest.php
│        │  │  ├─ Inflector
│        │  │  │  ├─ EnglishInflectorTest.php
│        │  │  │  ├─ FrenchInflectorTest.php
│        │  │  │  └─ SpanishInflectorTest.php
│        │  │  ├─ LazyStringTest.php
│        │  │  ├─ Slugger
│        │  │  │  └─ AsciiSluggerTest.php
│        │  │  ├─ SluggerTest.php
│        │  │  └─ UnicodeStringTest.php
│        │  ├─ TruncateMode.php
│        │  └─ UnicodeString.php
│        ├─ var-dumper
│        │  ├─ Caster
│        │  │  ├─ AddressInfoCaster.php
│        │  │  ├─ AmqpCaster.php
│        │  │  ├─ ArgsStub.php
│        │  │  ├─ Caster.php
│        │  │  ├─ ClassStub.php
│        │  │  ├─ ConstStub.php
│        │  │  ├─ CurlCaster.php
│        │  │  ├─ CutArrayStub.php
│        │  │  ├─ CutStub.php
│        │  │  ├─ DateCaster.php
│        │  │  ├─ DoctrineCaster.php
│        │  │  ├─ DOMCaster.php
│        │  │  ├─ DsCaster.php
│        │  │  ├─ DsPairStub.php
│        │  │  ├─ EnumStub.php
│        │  │  ├─ ExceptionCaster.php
│        │  │  ├─ FFICaster.php
│        │  │  ├─ FiberCaster.php
│        │  │  ├─ FrameStub.php
│        │  │  ├─ GdCaster.php
│        │  │  ├─ GmpCaster.php
│        │  │  ├─ ImagineCaster.php
│        │  │  ├─ ImgStub.php
│        │  │  ├─ IntlCaster.php
│        │  │  ├─ LinkStub.php
│        │  │  ├─ MemcachedCaster.php
│        │  │  ├─ MysqliCaster.php
│        │  │  ├─ OpenSSLCaster.php
│        │  │  ├─ PdoCaster.php
│        │  │  ├─ PgSqlCaster.php
│        │  │  ├─ ProxyManagerCaster.php
│        │  │  ├─ RdKafkaCaster.php
│        │  │  ├─ RedisCaster.php
│        │  │  ├─ ReflectionCaster.php
│        │  │  ├─ ResourceCaster.php
│        │  │  ├─ ScalarStub.php
│        │  │  ├─ SocketCaster.php
│        │  │  ├─ SplCaster.php
│        │  │  ├─ SqliteCaster.php
│        │  │  ├─ StubCaster.php
│        │  │  ├─ SymfonyCaster.php
│        │  │  ├─ TraceStub.php
│        │  │  ├─ UninitializedStub.php
│        │  │  ├─ UuidCaster.php
│        │  │  ├─ VirtualStub.php
│        │  │  ├─ XmlReaderCaster.php
│        │  │  └─ XmlResourceCaster.php
│        │  ├─ CHANGELOG.md
│        │  ├─ Cloner
│        │  │  ├─ AbstractCloner.php
│        │  │  ├─ ClonerInterface.php
│        │  │  ├─ Cursor.php
│        │  │  ├─ Data.php
│        │  │  ├─ DumperInterface.php
│        │  │  ├─ Internal
│        │  │  │  └─ NoDefault.php
│        │  │  ├─ Stub.php
│        │  │  └─ VarCloner.php
│        │  ├─ Command
│        │  │  ├─ Descriptor
│        │  │  │  ├─ CliDescriptor.php
│        │  │  │  ├─ DumpDescriptorInterface.php
│        │  │  │  └─ HtmlDescriptor.php
│        │  │  └─ ServerDumpCommand.php
│        │  ├─ composer.json
│        │  ├─ Dumper
│        │  │  ├─ AbstractDumper.php
│        │  │  ├─ CliDumper.php
│        │  │  ├─ ContextProvider
│        │  │  │  ├─ CliContextProvider.php
│        │  │  │  ├─ ContextProviderInterface.php
│        │  │  │  ├─ RequestContextProvider.php
│        │  │  │  └─ SourceContextProvider.php
│        │  │  ├─ ContextualizedDumper.php
│        │  │  ├─ DataDumperInterface.php
│        │  │  ├─ HtmlDumper.php
│        │  │  └─ ServerDumper.php
│        │  ├─ Exception
│        │  │  └─ ThrowingCasterException.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Resources
│        │  │  ├─ bin
│        │  │  │  └─ var-dump-server
│        │  │  ├─ css
│        │  │  │  └─ htmlDescriptor.css
│        │  │  ├─ functions
│        │  │  │  └─ dump.php
│        │  │  └─ js
│        │  │     └─ htmlDescriptor.js
│        │  ├─ Server
│        │  │  ├─ Connection.php
│        │  │  └─ DumpServer.php
│        │  ├─ Test
│        │  │  └─ VarDumperTestTrait.php
│        │  ├─ Tests
│        │  │  ├─ Caster
│        │  │  │  ├─ AddressInfoCasterTest.php
│        │  │  │  ├─ CasterTest.php
│        │  │  │  ├─ CurlCasterTest.php
│        │  │  │  ├─ DateCasterTest.php
│        │  │  │  ├─ DoctrineCasterTest.php
│        │  │  │  ├─ DOMCasterTest.php
│        │  │  │  ├─ ExceptionCasterTest.php
│        │  │  │  ├─ FFICasterTest.php
│        │  │  │  ├─ FiberCasterTest.php
│        │  │  │  ├─ GmpCasterTest.php
│        │  │  │  ├─ IntlCasterTest.php
│        │  │  │  ├─ MemcachedCasterTest.php
│        │  │  │  ├─ MysqliCasterTest.php
│        │  │  │  ├─ OpenSSLCasterTest.php
│        │  │  │  ├─ PdoCasterTest.php
│        │  │  │  ├─ RdKafkaCasterTest.php
│        │  │  │  ├─ RedisCasterTest.php
│        │  │  │  ├─ ReflectionCasterTest.php
│        │  │  │  ├─ ResourceCasterTest.php
│        │  │  │  ├─ SocketCasterTest.php
│        │  │  │  ├─ SplCasterTest.php
│        │  │  │  ├─ SqliteCasterTest.php
│        │  │  │  ├─ StubCasterTest.php
│        │  │  │  ├─ SymfonyCasterTest.php
│        │  │  │  └─ XmlReaderCasterTest.php
│        │  │  ├─ Cloner
│        │  │  │  ├─ DataTest.php
│        │  │  │  ├─ StubTest.php
│        │  │  │  └─ VarClonerTest.php
│        │  │  ├─ Command
│        │  │  │  ├─ Descriptor
│        │  │  │  │  ├─ CliDescriptorTest.php
│        │  │  │  │  └─ HtmlDescriptorTest.php
│        │  │  │  └─ ServerDumpCommandTest.php
│        │  │  ├─ Dumper
│        │  │  │  ├─ CliDumperTest.php
│        │  │  │  ├─ ContextProvider
│        │  │  │  │  └─ RequestContextProviderTest.php
│        │  │  │  ├─ ContextualizedDumperTest.php
│        │  │  │  ├─ functions
│        │  │  │  │  ├─ dd_with_multiple_args.phpt
│        │  │  │  │  ├─ dd_with_named_args.phpt
│        │  │  │  │  ├─ dd_with_null.phpt
│        │  │  │  │  ├─ dd_with_single_arg.phpt
│        │  │  │  │  ├─ dump_data_collector_with_spl_array.phpt
│        │  │  │  │  ├─ dump_without_args.phpt
│        │  │  │  │  ├─ dump_with_multiple_args.phpt
│        │  │  │  │  ├─ dump_with_named_args.phpt
│        │  │  │  │  ├─ dump_with_null.phpt
│        │  │  │  │  └─ dump_with_single_arg.phpt
│        │  │  │  ├─ FunctionsTest.php
│        │  │  │  ├─ HtmlDumperTest.php
│        │  │  │  └─ ServerDumperTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ BackedEnumFixture.php
│        │  │  │  ├─ DateTimeChild.php
│        │  │  │  ├─ dumb-var.php
│        │  │  │  ├─ dump_server.php
│        │  │  │  ├─ ExtendsReflectionTypeFixture.php
│        │  │  │  ├─ FooInterface.php
│        │  │  │  ├─ GeneratorDemo.php
│        │  │  │  ├─ LotsOfAttributes.php
│        │  │  │  ├─ MyAttribute.php
│        │  │  │  ├─ NotLoadableClass.php
│        │  │  │  ├─ Php74.php
│        │  │  │  ├─ Php81Enums.php
│        │  │  │  ├─ Php82NullStandaloneReturnType.php
│        │  │  │  ├─ ReflectionIntersectionTypeFixture.php
│        │  │  │  ├─ ReflectionNamedTypeFixture.php
│        │  │  │  ├─ ReflectionUnionTypeFixture.php
│        │  │  │  ├─ ReflectionUnionTypeWithIntersectionFixture.php
│        │  │  │  ├─ Twig.php
│        │  │  │  ├─ UnitEnumFixture.php
│        │  │  │  ├─ VirtualProperty.php
│        │  │  │  └─ xml_reader.xml
│        │  │  ├─ Server
│        │  │  │  └─ ConnectionTest.php
│        │  │  └─ Test
│        │  │     └─ VarDumperTestTraitTest.php
│        │  └─ VarDumper.php
│        ├─ var-exporter
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ Exception
│        │  │  ├─ ClassNotFoundException.php
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ LogicException.php
│        │  │  └─ NotInstantiableTypeException.php
│        │  ├─ Hydrator.php
│        │  ├─ Instantiator.php
│        │  ├─ Internal
│        │  │  ├─ Exporter.php
│        │  │  ├─ Hydrator.php
│        │  │  ├─ LazyDecoratorTrait.php
│        │  │  ├─ LazyObjectRegistry.php
│        │  │  ├─ LazyObjectState.php
│        │  │  ├─ LazyObjectTrait.php
│        │  │  ├─ Reference.php
│        │  │  ├─ Registry.php
│        │  │  └─ Values.php
│        │  ├─ LazyGhostTrait.php
│        │  ├─ LazyObjectInterface.php
│        │  ├─ LazyProxyTrait.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ ProxyHelper.php
│        │  ├─ README.md
│        │  ├─ Tests
│        │  │  ├─ Fixtures
│        │  │  │  ├─ abstract-parent.php
│        │  │  │  ├─ array-iterator.php
│        │  │  │  ├─ array-object-custom.php
│        │  │  │  ├─ array-object.php
│        │  │  │  ├─ backed-property.php
│        │  │  │  ├─ BackedProperty.php
│        │  │  │  ├─ bool.php
│        │  │  │  ├─ clone.php
│        │  │  │  ├─ datetime.php
│        │  │  │  ├─ error.php
│        │  │  │  ├─ external-references.php
│        │  │  │  ├─ final-array-iterator.php
│        │  │  │  ├─ final-error.php
│        │  │  │  ├─ final-stdclass.php
│        │  │  │  ├─ foo-serializable.php
│        │  │  │  ├─ FooReadonly.php
│        │  │  │  ├─ FooSerializable.php
│        │  │  │  ├─ FooUnitEnum.php
│        │  │  │  ├─ hard-references-recursive.php
│        │  │  │  ├─ hard-references.php
│        │  │  │  ├─ incomplete-class.php
│        │  │  │  ├─ LazyGhost
│        │  │  │  │  ├─ ChildMagicClass.php
│        │  │  │  │  ├─ ChildStdClass.php
│        │  │  │  │  ├─ ChildTestClass.php
│        │  │  │  │  ├─ ClassWithUninitializedObjectProperty.php
│        │  │  │  │  ├─ LazyClass.php
│        │  │  │  │  ├─ MagicClass.php
│        │  │  │  │  ├─ NoMagicClass.php
│        │  │  │  │  ├─ ReadOnlyClass.php
│        │  │  │  │  ├─ RegularClass.php
│        │  │  │  │  └─ TestClass.php
│        │  │  │  ├─ LazyProxy
│        │  │  │  │  ├─ AbstractHooked.php
│        │  │  │  │  ├─ AsymmetricVisibility.php
│        │  │  │  │  ├─ ConcreteReadOnlyClass.php
│        │  │  │  │  ├─ FinalPublicClass.php
│        │  │  │  │  ├─ Hooked.php
│        │  │  │  │  ├─ HookedInterface.php
│        │  │  │  │  ├─ HookedWithDefaultValue.php
│        │  │  │  │  ├─ Php82NullStandaloneReturnType.php
│        │  │  │  │  ├─ ReadOnlyClass.php
│        │  │  │  │  ├─ StringMagicGetClass.php
│        │  │  │  │  ├─ TestClass.php
│        │  │  │  │  ├─ TestOverwritePropClass.php
│        │  │  │  │  ├─ TestUnserializeClass.php
│        │  │  │  │  └─ TestWakeupClass.php
│        │  │  │  ├─ lf-ending-string.php
│        │  │  │  ├─ multiline-string.php
│        │  │  │  ├─ MySerializable.php
│        │  │  │  ├─ partially-indexed-array.php
│        │  │  │  ├─ php74-serializable.php
│        │  │  │  ├─ private-constructor.php
│        │  │  │  ├─ private.php
│        │  │  │  ├─ readonly.php
│        │  │  │  ├─ serializable.php
│        │  │  │  ├─ simple-array.php
│        │  │  │  ├─ SimpleObject.php
│        │  │  │  ├─ spl-object-storage.php
│        │  │  │  ├─ unit-enum.php
│        │  │  │  ├─ var-on-sleep.php
│        │  │  │  ├─ wakeup-refl.php
│        │  │  │  ├─ wakeup.php
│        │  │  │  ├─ __serialize-but-no-__unserialize.php
│        │  │  │  └─ __unserialize-but-no-__serialize.php
│        │  │  ├─ InstantiatorTest.php
│        │  │  ├─ LazyProxyTraitTest.php
│        │  │  ├─ LegacyLazyGhostTraitTest.php
│        │  │  ├─ LegacyLazyProxyTraitTest.php
│        │  │  ├─ LegacyProxyHelperTest.php
│        │  │  ├─ ProxyHelperTest.php
│        │  │  └─ VarExporterTest.php
│        │  └─ VarExporter.php
│        └─ yaml
│           ├─ CHANGELOG.md
│           ├─ Command
│           │  └─ LintCommand.php
│           ├─ composer.json
│           ├─ Dumper.php
│           ├─ Escaper.php
│           ├─ Exception
│           │  ├─ DumpException.php
│           │  ├─ ExceptionInterface.php
│           │  ├─ ParseException.php
│           │  └─ RuntimeException.php
│           ├─ Inline.php
│           ├─ LICENSE
│           ├─ Parser.php
│           ├─ phpunit.xml.dist
│           ├─ README.md
│           ├─ Resources
│           │  └─ bin
│           │     └─ yaml-lint
│           ├─ Tag
│           │  └─ TaggedValue.php
│           ├─ Tests
│           │  ├─ Command
│           │  │  └─ LintCommandTest.php
│           │  ├─ DumperTest.php
│           │  ├─ Fixtures
│           │  │  ├─ arrow.gif
│           │  │  ├─ booleanMappingKeys.yml
│           │  │  ├─ embededPhp.yml
│           │  │  ├─ escapedCharacters.yml
│           │  │  ├─ FooBackedEnum.php
│           │  │  ├─ FooUnitEnum.php
│           │  │  ├─ index.yml
│           │  │  ├─ nonStringKeys.yml
│           │  │  ├─ not_readable.yml
│           │  │  ├─ nullMappingKey.yml
│           │  │  ├─ numericMappingKeys.yml
│           │  │  ├─ sfComments.yml
│           │  │  ├─ sfCompact.yml
│           │  │  ├─ sfMergeKey.yml
│           │  │  ├─ sfObjects.yml
│           │  │  ├─ sfQuotes.yml
│           │  │  ├─ sfTests.yml
│           │  │  ├─ unindentedCollections.yml
│           │  │  ├─ YtsAnchorAlias.yml
│           │  │  ├─ YtsBasicTests.yml
│           │  │  ├─ YtsBlockMapping.yml
│           │  │  ├─ YtsDocumentSeparator.yml
│           │  │  ├─ YtsErrorTests.yml
│           │  │  ├─ YtsFlowCollections.yml
│           │  │  ├─ YtsFoldedScalars.yml
│           │  │  ├─ YtsNullsAndEmpties.yml
│           │  │  ├─ YtsSpecificationExamples.yml
│           │  │  └─ YtsTypeTransfers.yml
│           │  ├─ InlineTest.php
│           │  ├─ ParseExceptionTest.php
│           │  ├─ ParserTest.php
│           │  └─ YamlTest.php
│           ├─ Unescaper.php
│           └─ Yaml.php
├─ docker-compose.dev.yml
├─ docs
├─ frontend
│  ├─ .editorconfig
│  ├─ .prettierrc.json
│  ├─ Dockerfile.dev
│  ├─ env.d.ts
│  ├─ eslint.config.ts
│  ├─ index.html
│  ├─ package-lock.json
│  ├─ package.json
│  ├─ playwright.config.ts
│  ├─ public
│  │  └─ favicon.ico
│  ├─ README.md
│  ├─ src
│  │  ├─ App.vue
│  │  ├─ assets
│  │  │  ├─ base.css
│  │  │  ├─ logo.svg
│  │  │  └─ main.css
│  │  ├─ components
│  │  │  ├─ HelloWorld.vue
│  │  │  ├─ icons
│  │  │  │  ├─ IconCommunity.vue
│  │  │  │  ├─ IconDocumentation.vue
│  │  │  │  ├─ IconEcosystem.vue
│  │  │  │  ├─ IconSupport.vue
│  │  │  │  └─ IconTooling.vue
│  │  │  ├─ TheWelcome.vue
│  │  │  ├─ WelcomeItem.vue
│  │  │  └─ __tests__
│  │  │     └─ HelloWorld.spec.ts
│  │  ├─ main.ts
│  │  ├─ router
│  │  │  └─ index.ts
│  │  ├─ stores
│  │  │  └─ counter.ts
│  │  └─ views
│  │     ├─ AboutView.vue
│  │     └─ HomeView.vue
│  ├─ tests
│  │  ├─ auth
│  │  │  └─ user.json
│  │  ├─ e2e
│  │  │  ├─ auth.spec.ts
│  │  │  ├─ clients.spec.ts
│  │  │  ├─ dashboard.spec.ts
│  │  │  ├─ invoicing.spec.ts
│  │  │  ├─ subscriptions.spec.ts
│  │  │  ├─ tsconfig.json
│  │  │  ├─ urssaf.spec.ts
│  │  │  └─ vue.spec.ts
│  │  ├─ fixtures
│  │  │  └─ test-data.json
│  │  └─ utils
│  │     └─ helpers.ts
│  ├─ tsconfig.app.json
│  ├─ tsconfig.json
│  ├─ tsconfig.node.json
│  ├─ tsconfig.vitest.json
│  ├─ vite.config.ts
│  └─ vitest.config.ts
├─ infrastructure
├─ LICENSE
└─ README.md

```
```
Autoflow
├─ backend
│  ├─ .editorconfig
│  ├─ .env
│  ├─ .env.dev
│  ├─ bin
│  │  └─ console
│  ├─ composer.json
│  ├─ composer.lock
│  ├─ config
│  │  ├─ bundles.php
│  │  ├─ packages
│  │  │  ├─ cache.yaml
│  │  │  ├─ framework.yaml
│  │  │  └─ routing.yaml
│  │  ├─ preload.php
│  │  ├─ routes
│  │  │  └─ framework.yaml
│  │  ├─ routes.yaml
│  │  └─ services.yaml
│  ├─ Dockerfile.dev
│  ├─ public
│  │  └─ index.php
│  ├─ src
│  │  ├─ Controller
│  │  └─ Kernel.php
│  ├─ symfony.lock
│  ├─ var
│  │  └─ cache
│  │     └─ dev
│  │        ├─ App_KernelDevDebugContainer.php
│  │        ├─ App_KernelDevDebugContainer.php.lock
│  │        ├─ App_KernelDevDebugContainer.php.meta
│  │        ├─ App_KernelDevDebugContainer.php.meta.json
│  │        ├─ App_KernelDevDebugContainer.preload.php
│  │        ├─ App_KernelDevDebugContainer.xml
│  │        ├─ App_KernelDevDebugContainer.xml.meta
│  │        ├─ App_KernelDevDebugContainer.xml.meta.json
│  │        ├─ App_KernelDevDebugContainerCompiler.log
│  │        ├─ App_KernelDevDebugContainerDeprecations.log
│  │        ├─ ContainerZYAsdwH
│  │        │  ├─ App_KernelDevDebugContainer.php
│  │        │  ├─ getArgumentResolver_BackedEnumResolverService.php
│  │        │  ├─ getArgumentResolver_DatetimeService.php
│  │        │  ├─ getArgumentResolver_DefaultService.php
│  │        │  ├─ getArgumentResolver_QueryParameterValueResolverService.php
│  │        │  ├─ getArgumentResolver_RequestAttributeService.php
│  │        │  ├─ getArgumentResolver_RequestPayloadService.php
│  │        │  ├─ getArgumentResolver_RequestService.php
│  │        │  ├─ getArgumentResolver_ServiceService.php
│  │        │  ├─ getArgumentResolver_SessionService.php
│  │        │  ├─ getArgumentResolver_VariadicService.php
│  │        │  ├─ getCacheWarmerService.php
│  │        │  ├─ getCache_AppClearerService.php
│  │        │  ├─ getCache_AppService.php
│  │        │  ├─ getCache_App_TaggableService.php
│  │        │  ├─ getCache_GlobalClearerService.php
│  │        │  ├─ getCache_SystemClearerService.php
│  │        │  ├─ getCache_SystemService.php
│  │        │  ├─ getConfigBuilder_WarmerService.php
│  │        │  ├─ getConsole_CommandLoaderService.php
│  │        │  ├─ getConsole_Command_AboutService.php
│  │        │  ├─ getConsole_Command_AssetsInstallService.php
│  │        │  ├─ getConsole_Command_CacheClearService.php
│  │        │  ├─ getConsole_Command_CachePoolClearService.php
│  │        │  ├─ getConsole_Command_CachePoolDeleteService.php
│  │        │  ├─ getConsole_Command_CachePoolInvalidateTagsService.php
│  │        │  ├─ getConsole_Command_CachePoolListService.php
│  │        │  ├─ getConsole_Command_CachePoolPruneService.php
│  │        │  ├─ getConsole_Command_CacheWarmupService.php
│  │        │  ├─ getConsole_Command_ConfigDebugService.php
│  │        │  ├─ getConsole_Command_ConfigDumpReferenceService.php
│  │        │  ├─ getConsole_Command_ContainerDebugService.php
│  │        │  ├─ getConsole_Command_ContainerLintService.php
│  │        │  ├─ getConsole_Command_DebugAutowiringService.php
│  │        │  ├─ getConsole_Command_DotenvDebugService.php
│  │        │  ├─ getConsole_Command_ErrorDumperService.php
│  │        │  ├─ getConsole_Command_EventDispatcherDebugService.php
│  │        │  ├─ getConsole_Command_RouterDebugService.php
│  │        │  ├─ getConsole_Command_RouterMatchService.php
│  │        │  ├─ getConsole_Command_SecretsDecryptToLocalService.php
│  │        │  ├─ getConsole_Command_SecretsEncryptFromLocalService.php
│  │        │  ├─ getConsole_Command_SecretsGenerateKeyService.php
│  │        │  ├─ getConsole_Command_SecretsListService.php
│  │        │  ├─ getConsole_Command_SecretsRemoveService.php
│  │        │  ├─ getConsole_Command_SecretsRevealService.php
│  │        │  ├─ getConsole_Command_SecretsSetService.php
│  │        │  ├─ getConsole_Command_YamlLintService.php
│  │        │  ├─ getConsole_ErrorListenerService.php
│  │        │  ├─ getContainer_EnvVarProcessorService.php
│  │        │  ├─ getContainer_EnvVarProcessorsLocatorService.php
│  │        │  ├─ getContainer_GetRoutingConditionServiceService.php
│  │        │  ├─ getDebug_ErrorHandlerConfiguratorService.php
│  │        │  ├─ getErrorControllerService.php
│  │        │  ├─ getErrorHandler_ErrorRenderer_HtmlService.php
│  │        │  ├─ getLoaderInterfaceService.php
│  │        │  ├─ getRedirectControllerService.php
│  │        │  ├─ getRouter_CacheWarmerService.php
│  │        │  ├─ getRouting_LoaderService.php
│  │        │  ├─ getSecrets_EnvVarLoaderService.php
│  │        │  ├─ getSecrets_VaultService.php
│  │        │  ├─ getServicesResetterService.php
│  │        │  ├─ getSession_FactoryService.php
│  │        │  ├─ getTemplateControllerService.php
│  │        │  ├─ get_Console_Command_About_LazyService.php
│  │        │  ├─ get_Console_Command_AssetsInstall_LazyService.php
│  │        │  ├─ get_Console_Command_CacheClear_LazyService.php
│  │        │  ├─ get_Console_Command_CachePoolClear_LazyService.php
│  │        │  ├─ get_Console_Command_CachePoolDelete_LazyService.php
│  │        │  ├─ get_Console_Command_CachePoolInvalidateTags_LazyService.php
│  │        │  ├─ get_Console_Command_CachePoolList_LazyService.php
│  │        │  ├─ get_Console_Command_CachePoolPrune_LazyService.php
│  │        │  ├─ get_Console_Command_CacheWarmup_LazyService.php
│  │        │  ├─ get_Console_Command_ConfigDebug_LazyService.php
│  │        │  ├─ get_Console_Command_ConfigDumpReference_LazyService.php
│  │        │  ├─ get_Console_Command_ContainerDebug_LazyService.php
│  │        │  ├─ get_Console_Command_ContainerLint_LazyService.php
│  │        │  ├─ get_Console_Command_DebugAutowiring_LazyService.php
│  │        │  ├─ get_Console_Command_DotenvDebug_LazyService.php
│  │        │  ├─ get_Console_Command_ErrorDumper_LazyService.php
│  │        │  ├─ get_Console_Command_EventDispatcherDebug_LazyService.php
│  │        │  ├─ get_Console_Command_RouterDebug_LazyService.php
│  │        │  ├─ get_Console_Command_RouterMatch_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsDecryptToLocal_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsEncryptFromLocal_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsGenerateKey_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsList_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsRemove_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsReveal_LazyService.php
│  │        │  ├─ get_Console_Command_SecretsSet_LazyService.php
│  │        │  ├─ get_Console_Command_YamlLint_LazyService.php
│  │        │  ├─ get_ServiceLocator_ZHyJIs5Service.php
│  │        │  ├─ get_ServiceLocator_ZHyJIs5_KernelloadRoutesService.php
│  │        │  ├─ get_ServiceLocator_ZHyJIs5_KernelregisterContainerConfigurationService.php
│  │        │  ├─ removed-ids.php
│  │        │  └─ RequestPayloadValueResolverGhost01ca9cc.php
│  │        ├─ Symfony
│  │        │  └─ Config
│  │        │     ├─ Framework
│  │        │     │  ├─ AnnotationsConfig.php
│  │        │     │  ├─ AssetMapper
│  │        │     │  │  └─ PrecompressConfig.php
│  │        │     │  ├─ AssetMapperConfig.php
│  │        │     │  ├─ Assets
│  │        │     │  │  └─ PackageConfig.php
│  │        │     │  ├─ AssetsConfig.php
│  │        │     │  ├─ Cache
│  │        │     │  │  └─ PoolConfig.php
│  │        │     │  ├─ CacheConfig.php
│  │        │     │  ├─ CsrfProtectionConfig.php
│  │        │     │  ├─ EsiConfig.php
│  │        │     │  ├─ ExceptionConfig.php
│  │        │     │  ├─ Form
│  │        │     │  │  └─ CsrfProtectionConfig.php
│  │        │     │  ├─ FormConfig.php
│  │        │     │  ├─ FragmentsConfig.php
│  │        │     │  ├─ HtmlSanitizer
│  │        │     │  │  └─ SanitizerConfig.php
│  │        │     │  ├─ HtmlSanitizerConfig.php
│  │        │     │  ├─ HttpCacheConfig.php
│  │        │     │  ├─ HttpClient
│  │        │     │  │  ├─ DefaultOptions
│  │        │     │  │  │  ├─ PeerFingerprintConfig.php
│  │        │     │  │  │  ├─ RetryFailed
│  │        │     │  │  │  │  └─ HttpCodeConfig.php
│  │        │     │  │  │  └─ RetryFailedConfig.php
│  │        │     │  │  ├─ DefaultOptionsConfig.php
│  │        │     │  │  ├─ ScopedClientConfig
│  │        │     │  │  │  ├─ PeerFingerprintConfig.php
│  │        │     │  │  │  ├─ RetryFailed
│  │        │     │  │  │  │  └─ HttpCodeConfig.php
│  │        │     │  │  │  └─ RetryFailedConfig.php
│  │        │     │  │  └─ ScopedClientConfig.php
│  │        │     │  ├─ HttpClientConfig.php
│  │        │     │  ├─ JsonStreamerConfig.php
│  │        │     │  ├─ LockConfig.php
│  │        │     │  ├─ Mailer
│  │        │     │  │  ├─ DkimSignerConfig.php
│  │        │     │  │  ├─ EnvelopeConfig.php
│  │        │     │  │  ├─ HeaderConfig.php
│  │        │     │  │  ├─ SmimeEncrypterConfig.php
│  │        │     │  │  └─ SmimeSignerConfig.php
│  │        │     │  ├─ MailerConfig.php
│  │        │     │  ├─ Messenger
│  │        │     │  │  ├─ BusConfig
│  │        │     │  │  │  ├─ DefaultMiddlewareConfig.php
│  │        │     │  │  │  └─ MiddlewareConfig.php
│  │        │     │  │  ├─ BusConfig.php
│  │        │     │  │  ├─ RoutingConfig.php
│  │        │     │  │  ├─ Serializer
│  │        │     │  │  │  └─ SymfonySerializerConfig.php
│  │        │     │  │  ├─ SerializerConfig.php
│  │        │     │  │  ├─ TransportConfig
│  │        │     │  │  │  └─ RetryStrategyConfig.php
│  │        │     │  │  └─ TransportConfig.php
│  │        │     │  ├─ MessengerConfig.php
│  │        │     │  ├─ Notifier
│  │        │     │  │  └─ AdminRecipientConfig.php
│  │        │     │  ├─ NotifierConfig.php
│  │        │     │  ├─ PhpErrorsConfig.php
│  │        │     │  ├─ ProfilerConfig.php
│  │        │     │  ├─ PropertyAccessConfig.php
│  │        │     │  ├─ PropertyInfoConfig.php
│  │        │     │  ├─ RateLimiter
│  │        │     │  │  ├─ LimiterConfig
│  │        │     │  │  │  └─ RateConfig.php
│  │        │     │  │  └─ LimiterConfig.php
│  │        │     │  ├─ RateLimiterConfig.php
│  │        │     │  ├─ RemoteeventConfig.php
│  │        │     │  ├─ RequestConfig.php
│  │        │     │  ├─ RouterConfig.php
│  │        │     │  ├─ SchedulerConfig.php
│  │        │     │  ├─ SecretsConfig.php
│  │        │     │  ├─ SemaphoreConfig.php
│  │        │     │  ├─ Serializer
│  │        │     │  │  ├─ MappingConfig.php
│  │        │     │  │  └─ NamedSerializerConfig.php
│  │        │     │  ├─ SerializerConfig.php
│  │        │     │  ├─ SessionConfig.php
│  │        │     │  ├─ SsiConfig.php
│  │        │     │  ├─ Translator
│  │        │     │  │  ├─ GlobalConfig.php
│  │        │     │  │  ├─ ProviderConfig.php
│  │        │     │  │  └─ PseudoLocalizationConfig.php
│  │        │     │  ├─ TranslatorConfig.php
│  │        │     │  ├─ TypeInfoConfig.php
│  │        │     │  ├─ UidConfig.php
│  │        │     │  ├─ Validation
│  │        │     │  │  ├─ AutoMappingConfig.php
│  │        │     │  │  ├─ MappingConfig.php
│  │        │     │  │  └─ NotCompromisedPasswordConfig.php
│  │        │     │  ├─ ValidationConfig.php
│  │        │     │  ├─ Webhook
│  │        │     │  │  └─ RoutingConfig.php
│  │        │     │  ├─ WebhookConfig.php
│  │        │     │  ├─ WebLinkConfig.php
│  │        │     │  ├─ Workflows
│  │        │     │  │  ├─ WorkflowsConfig
│  │        │     │  │  │  ├─ AuditTrailConfig.php
│  │        │     │  │  │  ├─ MarkingStoreConfig.php
│  │        │     │  │  │  ├─ PlaceConfig.php
│  │        │     │  │  │  └─ TransitionConfig.php
│  │        │     │  │  └─ WorkflowsConfig.php
│  │        │     │  └─ WorkflowsConfig.php
│  │        │     └─ FrameworkConfig.php
│  │        ├─ url_generating_routes.php
│  │        ├─ url_generating_routes.php.meta
│  │        ├─ url_generating_routes.php.meta.json
│  │        ├─ url_matching_routes.php
│  │        ├─ url_matching_routes.php.meta
│  │        └─ url_matching_routes.php.meta.json
│  └─ vendor
│     ├─ autoload.php
│     ├─ autoload_runtime.php
│     ├─ bin
│     │  ├─ patch-type-declarations
│     │  ├─ patch-type-declarations.bat
│     │  ├─ var-dump-server
│     │  ├─ var-dump-server.bat
│     │  ├─ yaml-lint
│     │  └─ yaml-lint.bat
│     ├─ composer
│     │  ├─ autoload_classmap.php
│     │  ├─ autoload_files.php
│     │  ├─ autoload_namespaces.php
│     │  ├─ autoload_psr4.php
│     │  ├─ autoload_real.php
│     │  ├─ autoload_static.php
│     │  ├─ ClassLoader.php
│     │  ├─ installed.json
│     │  ├─ installed.php
│     │  ├─ InstalledVersions.php
│     │  ├─ LICENSE
│     │  └─ platform_check.php
│     ├─ psr
│     │  ├─ cache
│     │  │  ├─ CHANGELOG.md
│     │  │  ├─ composer.json
│     │  │  ├─ LICENSE.txt
│     │  │  ├─ README.md
│     │  │  └─ src
│     │  │     ├─ CacheException.php
│     │  │     ├─ CacheItemInterface.php
│     │  │     ├─ CacheItemPoolInterface.php
│     │  │     └─ InvalidArgumentException.php
│     │  ├─ container
│     │  │  ├─ composer.json
│     │  │  ├─ LICENSE
│     │  │  ├─ README.md
│     │  │  └─ src
│     │  │     ├─ ContainerExceptionInterface.php
│     │  │     ├─ ContainerInterface.php
│     │  │     └─ NotFoundExceptionInterface.php
│     │  ├─ event-dispatcher
│     │  │  ├─ .editorconfig
│     │  │  ├─ composer.json
│     │  │  ├─ LICENSE
│     │  │  ├─ README.md
│     │  │  └─ src
│     │  │     ├─ EventDispatcherInterface.php
│     │  │     ├─ ListenerProviderInterface.php
│     │  │     └─ StoppableEventInterface.php
│     │  └─ log
│     │     ├─ composer.json
│     │     ├─ LICENSE
│     │     ├─ README.md
│     │     └─ src
│     │        ├─ AbstractLogger.php
│     │        ├─ InvalidArgumentException.php
│     │        ├─ LoggerAwareInterface.php
│     │        ├─ LoggerAwareTrait.php
│     │        ├─ LoggerInterface.php
│     │        ├─ LoggerTrait.php
│     │        ├─ LogLevel.php
│     │        └─ NullLogger.php
│     └─ symfony
│        ├─ cache
│        │  ├─ Adapter
│        │  │  ├─ AbstractAdapter.php
│        │  │  ├─ AbstractTagAwareAdapter.php
│        │  │  ├─ AdapterInterface.php
│        │  │  ├─ ApcuAdapter.php
│        │  │  ├─ ArrayAdapter.php
│        │  │  ├─ ChainAdapter.php
│        │  │  ├─ CouchbaseBucketAdapter.php
│        │  │  ├─ CouchbaseCollectionAdapter.php
│        │  │  ├─ DoctrineDbalAdapter.php
│        │  │  ├─ FilesystemAdapter.php
│        │  │  ├─ FilesystemTagAwareAdapter.php
│        │  │  ├─ MemcachedAdapter.php
│        │  │  ├─ NullAdapter.php
│        │  │  ├─ ParameterNormalizer.php
│        │  │  ├─ PdoAdapter.php
│        │  │  ├─ PhpArrayAdapter.php
│        │  │  ├─ PhpFilesAdapter.php
│        │  │  ├─ ProxyAdapter.php
│        │  │  ├─ Psr16Adapter.php
│        │  │  ├─ RedisAdapter.php
│        │  │  ├─ RedisTagAwareAdapter.php
│        │  │  ├─ TagAwareAdapter.php
│        │  │  ├─ TagAwareAdapterInterface.php
│        │  │  ├─ TraceableAdapter.php
│        │  │  └─ TraceableTagAwareAdapter.php
│        │  ├─ CacheItem.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ DataCollector
│        │  │  └─ CacheDataCollector.php
│        │  ├─ DependencyInjection
│        │  │  ├─ CacheCollectorPass.php
│        │  │  ├─ CachePoolClearerPass.php
│        │  │  ├─ CachePoolPass.php
│        │  │  └─ CachePoolPrunerPass.php
│        │  ├─ Exception
│        │  │  ├─ BadMethodCallException.php
│        │  │  ├─ CacheException.php
│        │  │  ├─ InvalidArgumentException.php
│        │  │  └─ LogicException.php
│        │  ├─ LICENSE
│        │  ├─ LockRegistry.php
│        │  ├─ Marshaller
│        │  │  ├─ DefaultMarshaller.php
│        │  │  ├─ DeflateMarshaller.php
│        │  │  ├─ MarshallerInterface.php
│        │  │  ├─ SodiumMarshaller.php
│        │  │  └─ TagAwareMarshaller.php
│        │  ├─ Messenger
│        │  │  ├─ EarlyExpirationDispatcher.php
│        │  │  ├─ EarlyExpirationHandler.php
│        │  │  └─ EarlyExpirationMessage.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ PruneableInterface.php
│        │  ├─ Psr16Cache.php
│        │  ├─ README.md
│        │  ├─ ResettableInterface.php
│        │  ├─ Tests
│        │  │  ├─ Adapter
│        │  │  │  ├─ AbstractRedisAdapterTestCase.php
│        │  │  │  ├─ AdapterTestCase.php
│        │  │  │  ├─ ApcuAdapterTest.php
│        │  │  │  ├─ ArrayAdapterTest.php
│        │  │  │  ├─ ChainAdapterTest.php
│        │  │  │  ├─ CouchbaseBucketAdapterTest.php
│        │  │  │  ├─ CouchbaseCollectionAdapterTest.php
│        │  │  │  ├─ DoctrineDbalAdapterTest.php
│        │  │  │  ├─ FilesystemAdapterTest.php
│        │  │  │  ├─ FilesystemTagAwareAdapterTest.php
│        │  │  │  ├─ MaxIdLengthAdapterTest.php
│        │  │  │  ├─ MemcachedAdapterTest.php
│        │  │  │  ├─ NamespacedProxyAdapterTest.php
│        │  │  │  ├─ NullAdapterTest.php
│        │  │  │  ├─ PdoAdapterTest.php
│        │  │  │  ├─ PhpArrayAdapterTest.php
│        │  │  │  ├─ PhpArrayAdapterWithFallbackTest.php
│        │  │  │  ├─ PhpFilesAdapterAppendOnlyTest.php
│        │  │  │  ├─ PhpFilesAdapterTest.php
│        │  │  │  ├─ PredisAdapterSentinelTest.php
│        │  │  │  ├─ PredisAdapterTest.php
│        │  │  │  ├─ PredisClusterAdapterTest.php
│        │  │  │  ├─ PredisRedisClusterAdapterTest.php
│        │  │  │  ├─ PredisRedisReplicationAdapterTest.php
│        │  │  │  ├─ PredisReplicationAdapterTest.php
│        │  │  │  ├─ PredisTagAwareAdapterTest.php
│        │  │  │  ├─ PredisTagAwareClusterAdapterTest.php
│        │  │  │  ├─ ProxyAdapterAndRedisAdapterTest.php
│        │  │  │  ├─ ProxyAdapterTest.php
│        │  │  │  ├─ Psr16AdapterTest.php
│        │  │  │  ├─ RedisAdapterSentinelTest.php
│        │  │  │  ├─ RedisAdapterTest.php
│        │  │  │  ├─ RedisArrayAdapterTest.php
│        │  │  │  ├─ RedisClusterAdapterTest.php
│        │  │  │  ├─ RedisTagAwareAdapterTest.php
│        │  │  │  ├─ RedisTagAwareArrayAdapterTest.php
│        │  │  │  ├─ RedisTagAwareClusterAdapterTest.php
│        │  │  │  ├─ RedisTagAwareRelayClusterAdapterTest.php
│        │  │  │  ├─ RelayAdapterSentinelTest.php
│        │  │  │  ├─ RelayAdapterTest.php
│        │  │  │  ├─ RelayClusterAdapterTest.php
│        │  │  │  ├─ TagAwareAdapterTest.php
│        │  │  │  ├─ TagAwareAndProxyAdapterIntegrationTest.php
│        │  │  │  ├─ TagAwareTestTrait.php
│        │  │  │  ├─ TraceableAdapterTest.php
│        │  │  │  └─ TraceableTagAwareAdapterTest.php
│        │  │  ├─ CacheItemTest.php
│        │  │  ├─ DataCollector
│        │  │  │  └─ CacheDataCollectorTest.php
│        │  │  ├─ DependencyInjection
│        │  │  │  ├─ CacheCollectorPassTest.php
│        │  │  │  ├─ CachePoolClearerPassTest.php
│        │  │  │  ├─ CachePoolPassTest.php
│        │  │  │  └─ CachePoolPrunerPassTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ ExternalAdapter.php
│        │  │  │  ├─ PrunableAdapter.php
│        │  │  │  ├─ StringableTag.php
│        │  │  │  └─ TestEnum.php
│        │  │  ├─ LockRegistryTest.php
│        │  │  ├─ Marshaller
│        │  │  │  ├─ DefaultMarshallerTest.php
│        │  │  │  ├─ DeflateMarshallerTest.php
│        │  │  │  └─ SodiumMarshallerTest.php
│        │  │  ├─ Messenger
│        │  │  │  ├─ EarlyExpirationDispatcherTest.php
│        │  │  │  ├─ EarlyExpirationHandlerTest.php
│        │  │  │  └─ EarlyExpirationMessageTest.php
│        │  │  ├─ Psr16CacheProxyTest.php
│        │  │  ├─ Psr16CacheTest.php
│        │  │  ├─ Psr16CacheWithExternalAdapter.php
│        │  │  └─ Traits
│        │  │     ├─ RedisProxiesTest.php
│        │  │     └─ RedisTraitTest.php
│        │  └─ Traits
│        │     ├─ AbstractAdapterTrait.php
│        │     ├─ ContractsTrait.php
│        │     ├─ FilesystemCommonTrait.php
│        │     ├─ FilesystemTrait.php
│        │     ├─ ProxyTrait.php
│        │     ├─ Redis5Proxy.php
│        │     ├─ Redis6Proxy.php
│        │     ├─ Redis6ProxyTrait.php
│        │     ├─ RedisCluster5Proxy.php
│        │     ├─ RedisCluster6Proxy.php
│        │     ├─ RedisCluster6ProxyTrait.php
│        │     ├─ RedisClusterNodeProxy.php
│        │     ├─ RedisClusterProxy.php
│        │     ├─ RedisProxy.php
│        │     ├─ RedisProxyTrait.php
│        │     ├─ RedisTrait.php
│        │     ├─ Relay
│        │     │  ├─ CopyTrait.php
│        │     │  ├─ GeosearchTrait.php
│        │     │  ├─ GetrangeTrait.php
│        │     │  ├─ HsetTrait.php
│        │     │  ├─ MoveTrait.php
│        │     │  ├─ NullableReturnTrait.php
│        │     │  └─ PfcountTrait.php
│        │     ├─ RelayClusterProxy.php
│        │     ├─ RelayProxy.php
│        │     ├─ RelayProxyTrait.php
│        │     └─ ValueWrapper.php
│        ├─ cache-contracts
│        │  ├─ CacheInterface.php
│        │  ├─ CacheTrait.php
│        │  ├─ CallbackInterface.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ ItemInterface.php
│        │  ├─ LICENSE
│        │  ├─ NamespacedPoolInterface.php
│        │  ├─ README.md
│        │  └─ TagAwareCacheInterface.php
│        ├─ config
│        │  ├─ Builder
│        │  │  ├─ ClassBuilder.php
│        │  │  ├─ ConfigBuilderGenerator.php
│        │  │  ├─ ConfigBuilderGeneratorInterface.php
│        │  │  ├─ ConfigBuilderInterface.php
│        │  │  ├─ Method.php
│        │  │  └─ Property.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ ConfigCache.php
│        │  ├─ ConfigCacheFactory.php
│        │  ├─ ConfigCacheFactoryInterface.php
│        │  ├─ ConfigCacheInterface.php
│        │  ├─ Definition
│        │  │  ├─ ArrayNode.php
│        │  │  ├─ BaseNode.php
│        │  │  ├─ BooleanNode.php
│        │  │  ├─ Builder
│        │  │  │  ├─ ArrayNodeDefinition.php
│        │  │  │  ├─ BooleanNodeDefinition.php
│        │  │  │  ├─ BuilderAwareInterface.php
│        │  │  │  ├─ EnumNodeDefinition.php
│        │  │  │  ├─ ExprBuilder.php
│        │  │  │  ├─ FloatNodeDefinition.php
│        │  │  │  ├─ IntegerNodeDefinition.php
│        │  │  │  ├─ MergeBuilder.php
│        │  │  │  ├─ NodeBuilder.php
│        │  │  │  ├─ NodeDefinition.php
│        │  │  │  ├─ NodeParentInterface.php
│        │  │  │  ├─ NormalizationBuilder.php
│        │  │  │  ├─ NumericNodeDefinition.php
│        │  │  │  ├─ ParentNodeDefinitionInterface.php
│        │  │  │  ├─ ScalarNodeDefinition.php
│        │  │  │  ├─ StringNodeDefinition.php
│        │  │  │  ├─ TreeBuilder.php
│        │  │  │  ├─ ValidationBuilder.php
│        │  │  │  └─ VariableNodeDefinition.php
│        │  │  ├─ ConfigurableInterface.php
│        │  │  ├─ Configuration.php
│        │  │  ├─ ConfigurationInterface.php
│        │  │  ├─ Configurator
│        │  │  │  └─ DefinitionConfigurator.php
│        │  │  ├─ Dumper
│        │  │  │  ├─ XmlReferenceDumper.php
│        │  │  │  └─ YamlReferenceDumper.php
│        │  │  ├─ EnumNode.php
│        │  │  ├─ Exception
│        │  │  │  ├─ DuplicateKeyException.php
│        │  │  │  ├─ Exception.php
│        │  │  │  ├─ ForbiddenOverwriteException.php
│        │  │  │  ├─ InvalidConfigurationException.php
│        │  │  │  ├─ InvalidDefinitionException.php
│        │  │  │  ├─ InvalidTypeException.php
│        │  │  │  └─ UnsetKeyException.php
│        │  │  ├─ FloatNode.php
│        │  │  ├─ IntegerNode.php
│        │  │  ├─ Loader
│        │  │  │  └─ DefinitionFileLoader.php
│        │  │  ├─ NodeInterface.php
│        │  │  ├─ NumericNode.php
│        │  │  ├─ Processor.php
│        │  │  ├─ PrototypedArrayNode.php
│        │  │  ├─ PrototypeNodeInterface.php
│        │  │  ├─ ScalarNode.php
│        │  │  ├─ StringNode.php
│        │  │  └─ VariableNode.php
│        │  ├─ Exception
│        │  │  ├─ FileLoaderImportCircularReferenceException.php
│        │  │  ├─ FileLocatorFileNotFoundException.php
│        │  │  ├─ LoaderLoadException.php
│        │  │  └─ LogicException.php
│        │  ├─ FileLocator.php
│        │  ├─ FileLocatorInterface.php
│        │  ├─ LICENSE
│        │  ├─ Loader
│        │  │  ├─ DelegatingLoader.php
│        │  │  ├─ DirectoryAwareLoaderInterface.php
│        │  │  ├─ FileLoader.php
│        │  │  ├─ GlobFileLoader.php
│        │  │  ├─ Loader.php
│        │  │  ├─ LoaderInterface.php
│        │  │  ├─ LoaderResolver.php
│        │  │  ├─ LoaderResolverInterface.php
│        │  │  └─ ParamConfigurator.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Resource
│        │  │  ├─ ClassExistenceResource.php
│        │  │  ├─ ComposerResource.php
│        │  │  ├─ DirectoryResource.php
│        │  │  ├─ FileExistenceResource.php
│        │  │  ├─ FileResource.php
│        │  │  ├─ GlobResource.php
│        │  │  ├─ ReflectionClassResource.php
│        │  │  ├─ ResourceInterface.php
│        │  │  ├─ SelfCheckingResourceChecker.php
│        │  │  ├─ SelfCheckingResourceInterface.php
│        │  │  └─ SkippingResourceChecker.php
│        │  ├─ ResourceCheckerConfigCache.php
│        │  ├─ ResourceCheckerConfigCacheFactory.php
│        │  ├─ ResourceCheckerInterface.php
│        │  ├─ Tests
│        │  │  ├─ Builder
│        │  │  │  ├─ Fixtures
│        │  │  │  │  ├─ AddToList
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        ├─ AddToList
│        │  │  │  │  │        │  ├─ Messenger
│        │  │  │  │  │        │  │  ├─ ReceivingConfig.php
│        │  │  │  │  │        │  │  └─ RoutingConfig.php
│        │  │  │  │  │        │  ├─ MessengerConfig.php
│        │  │  │  │  │        │  ├─ Translator
│        │  │  │  │  │        │  │  ├─ Books
│        │  │  │  │  │        │  │  │  └─ PageConfig.php
│        │  │  │  │  │        │  │  └─ BooksConfig.php
│        │  │  │  │  │        │  └─ TranslatorConfig.php
│        │  │  │  │  │        └─ AddToListConfig.php
│        │  │  │  │  ├─ AddToList.config.php
│        │  │  │  │  ├─ AddToList.output.php
│        │  │  │  │  ├─ AddToList.php
│        │  │  │  │  ├─ ArrayExtraKeys
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        ├─ ArrayExtraKeys
│        │  │  │  │  │        │  ├─ BarConfig.php
│        │  │  │  │  │        │  ├─ BazConfig.php
│        │  │  │  │  │        │  └─ FooConfig.php
│        │  │  │  │  │        └─ ArrayExtraKeysConfig.php
│        │  │  │  │  ├─ ArrayExtraKeys.config.php
│        │  │  │  │  ├─ ArrayExtraKeys.output.php
│        │  │  │  │  ├─ ArrayExtraKeys.php
│        │  │  │  │  ├─ NodeInitialValues
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        ├─ NodeInitialValues
│        │  │  │  │  │        │  ├─ Messenger
│        │  │  │  │  │        │  │  └─ TransportsConfig.php
│        │  │  │  │  │        │  ├─ MessengerConfig.php
│        │  │  │  │  │        │  └─ SomeCleverNameConfig.php
│        │  │  │  │  │        └─ NodeInitialValuesConfig.php
│        │  │  │  │  ├─ NodeInitialValues.config.php
│        │  │  │  │  ├─ NodeInitialValues.output.php
│        │  │  │  │  ├─ NodeInitialValues.php
│        │  │  │  │  ├─ Placeholders
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        └─ PlaceholdersConfig.php
│        │  │  │  │  ├─ Placeholders.config.php
│        │  │  │  │  ├─ Placeholders.output.php
│        │  │  │  │  ├─ Placeholders.php
│        │  │  │  │  ├─ PrimitiveTypes
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        └─ PrimitiveTypesConfig.php
│        │  │  │  │  ├─ PrimitiveTypes.config.php
│        │  │  │  │  ├─ PrimitiveTypes.output.php
│        │  │  │  │  ├─ PrimitiveTypes.php
│        │  │  │  │  ├─ ScalarNormalizedTypes
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        ├─ ScalarNormalizedTypes
│        │  │  │  │  │        │  ├─ KeyedListObjectConfig.php
│        │  │  │  │  │        │  ├─ ListObjectConfig.php
│        │  │  │  │  │        │  ├─ Nested
│        │  │  │  │  │        │  │  ├─ NestedListObjectConfig.php
│        │  │  │  │  │        │  │  └─ NestedObjectConfig.php
│        │  │  │  │  │        │  ├─ NestedConfig.php
│        │  │  │  │  │        │  └─ ObjectConfig.php
│        │  │  │  │  │        └─ ScalarNormalizedTypesConfig.php
│        │  │  │  │  ├─ ScalarNormalizedTypes.config.php
│        │  │  │  │  ├─ ScalarNormalizedTypes.output.php
│        │  │  │  │  ├─ ScalarNormalizedTypes.php
│        │  │  │  │  ├─ VariableType
│        │  │  │  │  │  └─ Symfony
│        │  │  │  │  │     └─ Config
│        │  │  │  │  │        └─ VariableTypeConfig.php
│        │  │  │  │  ├─ VariableType.config.php
│        │  │  │  │  ├─ VariableType.output.php
│        │  │  │  │  └─ VariableType.php
│        │  │  │  └─ GeneratedConfigTest.php
│        │  │  ├─ ConfigCacheFactoryTest.php
│        │  │  ├─ ConfigCacheTest.php
│        │  │  ├─ Definition
│        │  │  │  ├─ ArrayNodeTest.php
│        │  │  │  ├─ BaseNodeTest.php
│        │  │  │  ├─ BooleanNodeTest.php
│        │  │  │  ├─ Builder
│        │  │  │  │  ├─ ArrayNodeDefinitionTest.php
│        │  │  │  │  ├─ BooleanNodeDefinitionTest.php
│        │  │  │  │  ├─ EnumNodeDefinitionTest.php
│        │  │  │  │  ├─ ExprBuilderTest.php
│        │  │  │  │  ├─ NodeBuilderTest.php
│        │  │  │  │  ├─ NodeDefinitionTest.php
│        │  │  │  │  ├─ NumericNodeDefinitionTest.php
│        │  │  │  │  └─ TreeBuilderTest.php
│        │  │  │  ├─ Dumper
│        │  │  │  │  ├─ XmlReferenceDumperTest.php
│        │  │  │  │  └─ YamlReferenceDumperTest.php
│        │  │  │  ├─ EnumNodeTest.php
│        │  │  │  ├─ FinalizationTest.php
│        │  │  │  ├─ FloatNodeTest.php
│        │  │  │  ├─ IntegerNodeTest.php
│        │  │  │  ├─ Loader
│        │  │  │  │  └─ DefinitionFileLoaderTest.php
│        │  │  │  ├─ MergeTest.php
│        │  │  │  ├─ NormalizationTest.php
│        │  │  │  ├─ PrototypedArrayNodeTest.php
│        │  │  │  ├─ ScalarNodeTest.php
│        │  │  │  └─ StringNodeTest.php
│        │  │  ├─ Exception
│        │  │  │  └─ LoaderLoadExceptionTest.php
│        │  │  ├─ FileLocatorTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ Again
│        │  │  │  │  └─ foo.xml
│        │  │  │  ├─ BadFileName.php
│        │  │  │  ├─ BadParent.php
│        │  │  │  ├─ BarNode.php
│        │  │  │  ├─ Builder
│        │  │  │  │  ├─ BarNodeDefinition.php
│        │  │  │  │  ├─ NodeBuilder.php
│        │  │  │  │  └─ VariableNodeDefinition.php
│        │  │  │  ├─ Configuration
│        │  │  │  │  ├─ CustomNode.php
│        │  │  │  │  ├─ CustomNodeDefinition.php
│        │  │  │  │  └─ ExampleConfiguration.php
│        │  │  │  ├─ Exclude
│        │  │  │  │  ├─ AnExcludedFile.txt
│        │  │  │  │  └─ ExcludeToo
│        │  │  │  │     └─ AnotheExcludedFile.txt
│        │  │  │  ├─ ExcludeTrailingSlash
│        │  │  │  │  ├─ bar.txt
│        │  │  │  │  ├─ exclude
│        │  │  │  │  │  └─ baz.txt
│        │  │  │  │  └─ foo.txt
│        │  │  │  ├─ foo.xml
│        │  │  │  ├─ Include
│        │  │  │  │  ├─ ExcludeFile.txt
│        │  │  │  │  ├─ IncludeAnotherFile.txt
│        │  │  │  │  └─ IncludeFile.txt
│        │  │  │  ├─ IntegerBackedTestEnum.php
│        │  │  │  ├─ Loader
│        │  │  │  │  └─ node_simple.php
│        │  │  │  ├─ ParseError.php
│        │  │  │  ├─ Resource
│        │  │  │  │  ├─ .hiddenFile
│        │  │  │  │  └─ ConditionalClass.php
│        │  │  │  ├─ some.phar
│        │  │  │  ├─ StringBackedTestEnum.php
│        │  │  │  ├─ StringBackedTestEnum2.php
│        │  │  │  ├─ TestEnum.php
│        │  │  │  ├─ TestEnum2.php
│        │  │  │  └─ Util
│        │  │  │     ├─ document_type.xml
│        │  │  │     ├─ invalid.xml
│        │  │  │     ├─ invalid_schema.xml
│        │  │  │     ├─ not_readable.xml
│        │  │  │     ├─ schema.xsd
│        │  │  │     └─ valid.xml
│        │  │  ├─ Loader
│        │  │  │  ├─ DelegatingLoaderTest.php
│        │  │  │  ├─ FileLoaderTest.php
│        │  │  │  ├─ LoaderResolverTest.php
│        │  │  │  └─ LoaderTest.php
│        │  │  ├─ Resource
│        │  │  │  ├─ ClassExistenceResourceTest.php
│        │  │  │  ├─ ComposerResourceTest.php
│        │  │  │  ├─ DirectoryResourceTest.php
│        │  │  │  ├─ FileExistenceResourceTest.php
│        │  │  │  ├─ FileResourceTest.php
│        │  │  │  ├─ GlobResourceTest.php
│        │  │  │  ├─ ReflectionClassResourceTest.php
│        │  │  │  └─ ResourceStub.php
│        │  │  ├─ ResourceCheckerConfigCacheTest.php
│        │  │  └─ Util
│        │  │     └─ XmlUtilsTest.php
│        │  └─ Util
│        │     ├─ Exception
│        │     │  ├─ InvalidXmlException.php
│        │     │  └─ XmlParsingException.php
│        │     └─ XmlUtils.php
│        ├─ console
│        │  ├─ Application.php
│        │  ├─ Attribute
│        │  │  ├─ Argument.php
│        │  │  ├─ AsCommand.php
│        │  │  └─ Option.php
│        │  ├─ CHANGELOG.md
│        │  ├─ CI
│        │  │  └─ GithubActionReporter.php
│        │  ├─ Color.php
│        │  ├─ Command
│        │  │  ├─ Command.php
│        │  │  ├─ CompleteCommand.php
│        │  │  ├─ DumpCompletionCommand.php
│        │  │  ├─ HelpCommand.php
│        │  │  ├─ InvokableCommand.php
│        │  │  ├─ LazyCommand.php
│        │  │  ├─ ListCommand.php
│        │  │  ├─ LockableTrait.php
│        │  │  ├─ SignalableCommandInterface.php
│        │  │  └─ TraceableCommand.php
│        │  ├─ CommandLoader
│        │  │  ├─ CommandLoaderInterface.php
│        │  │  ├─ ContainerCommandLoader.php
│        │  │  └─ FactoryCommandLoader.php
│        │  ├─ Completion
│        │  │  ├─ CompletionInput.php
│        │  │  ├─ CompletionSuggestions.php
│        │  │  ├─ Output
│        │  │  │  ├─ BashCompletionOutput.php
│        │  │  │  ├─ CompletionOutputInterface.php
│        │  │  │  ├─ FishCompletionOutput.php
│        │  │  │  └─ ZshCompletionOutput.php
│        │  │  └─ Suggestion.php
│        │  ├─ composer.json
│        │  ├─ ConsoleEvents.php
│        │  ├─ Cursor.php
│        │  ├─ DataCollector
│        │  │  └─ CommandDataCollector.php
│        │  ├─ Debug
│        │  │  └─ CliRequest.php
│        │  ├─ DependencyInjection
│        │  │  └─ AddConsoleCommandPass.php
│        │  ├─ Descriptor
│        │  │  ├─ ApplicationDescription.php
│        │  │  ├─ Descriptor.php
│        │  │  ├─ DescriptorInterface.php
│        │  │  ├─ JsonDescriptor.php
│        │  │  ├─ MarkdownDescriptor.php
│        │  │  ├─ ReStructuredTextDescriptor.php
│        │  │  ├─ TextDescriptor.php
│        │  │  └─ XmlDescriptor.php
│        │  ├─ Event
│        │  │  ├─ ConsoleAlarmEvent.php
│        │  │  ├─ ConsoleCommandEvent.php
│        │  │  ├─ ConsoleErrorEvent.php
│        │  │  ├─ ConsoleEvent.php
│        │  │  ├─ ConsoleSignalEvent.php
│        │  │  └─ ConsoleTerminateEvent.php
│        │  ├─ EventListener
│        │  │  └─ ErrorListener.php
│        │  ├─ Exception
│        │  │  ├─ CommandNotFoundException.php
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ InvalidArgumentException.php
│        │  │  ├─ InvalidOptionException.php
│        │  │  ├─ LogicException.php
│        │  │  ├─ MissingInputException.php
│        │  │  ├─ NamespaceNotFoundException.php
│        │  │  ├─ RunCommandFailedException.php
│        │  │  └─ RuntimeException.php
│        │  ├─ Formatter
│        │  │  ├─ NullOutputFormatter.php
│        │  │  ├─ NullOutputFormatterStyle.php
│        │  │  ├─ OutputFormatter.php
│        │  │  ├─ OutputFormatterInterface.php
│        │  │  ├─ OutputFormatterStyle.php
│        │  │  ├─ OutputFormatterStyleInterface.php
│        │  │  ├─ OutputFormatterStyleStack.php
│        │  │  └─ WrappableOutputFormatterInterface.php
│        │  ├─ Helper
│        │  │  ├─ DebugFormatterHelper.php
│        │  │  ├─ DescriptorHelper.php
│        │  │  ├─ Dumper.php
│        │  │  ├─ FormatterHelper.php
│        │  │  ├─ Helper.php
│        │  │  ├─ HelperInterface.php
│        │  │  ├─ HelperSet.php
│        │  │  ├─ InputAwareHelper.php
│        │  │  ├─ OutputWrapper.php
│        │  │  ├─ ProcessHelper.php
│        │  │  ├─ ProgressBar.php
│        │  │  ├─ ProgressIndicator.php
│        │  │  ├─ QuestionHelper.php
│        │  │  ├─ SymfonyQuestionHelper.php
│        │  │  ├─ Table.php
│        │  │  ├─ TableCell.php
│        │  │  ├─ TableCellStyle.php
│        │  │  ├─ TableRows.php
│        │  │  ├─ TableSeparator.php
│        │  │  ├─ TableStyle.php
│        │  │  ├─ TreeHelper.php
│        │  │  ├─ TreeNode.php
│        │  │  └─ TreeStyle.php
│        │  ├─ Input
│        │  │  ├─ ArgvInput.php
│        │  │  ├─ ArrayInput.php
│        │  │  ├─ Input.php
│        │  │  ├─ InputArgument.php
│        │  │  ├─ InputAwareInterface.php
│        │  │  ├─ InputDefinition.php
│        │  │  ├─ InputInterface.php
│        │  │  ├─ InputOption.php
│        │  │  ├─ StreamableInputInterface.php
│        │  │  └─ StringInput.php
│        │  ├─ LICENSE
│        │  ├─ Logger
│        │  │  └─ ConsoleLogger.php
│        │  ├─ Messenger
│        │  │  ├─ RunCommandContext.php
│        │  │  ├─ RunCommandMessage.php
│        │  │  └─ RunCommandMessageHandler.php
│        │  ├─ Output
│        │  │  ├─ AnsiColorMode.php
│        │  │  ├─ BufferedOutput.php
│        │  │  ├─ ConsoleOutput.php
│        │  │  ├─ ConsoleOutputInterface.php
│        │  │  ├─ ConsoleSectionOutput.php
│        │  │  ├─ NullOutput.php
│        │  │  ├─ Output.php
│        │  │  ├─ OutputInterface.php
│        │  │  ├─ StreamOutput.php
│        │  │  └─ TrimmedBufferOutput.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ Question
│        │  │  ├─ ChoiceQuestion.php
│        │  │  ├─ ConfirmationQuestion.php
│        │  │  └─ Question.php
│        │  ├─ README.md
│        │  ├─ Resources
│        │  │  ├─ bin
│        │  │  │  └─ hiddeninput.exe
│        │  │  ├─ completion.bash
│        │  │  ├─ completion.fish
│        │  │  └─ completion.zsh
│        │  ├─ SignalRegistry
│        │  │  ├─ SignalMap.php
│        │  │  └─ SignalRegistry.php
│        │  ├─ SingleCommandApplication.php
│        │  ├─ Style
│        │  │  ├─ OutputStyle.php
│        │  │  ├─ StyleInterface.php
│        │  │  └─ SymfonyStyle.php
│        │  ├─ Terminal.php
│        │  ├─ Tester
│        │  │  ├─ ApplicationTester.php
│        │  │  ├─ CommandCompletionTester.php
│        │  │  ├─ CommandTester.php
│        │  │  ├─ Constraint
│        │  │  │  └─ CommandIsSuccessful.php
│        │  │  └─ TesterTrait.php
│        │  └─ Tests
│        │     ├─ ApplicationTest.php
│        │     ├─ CI
│        │     │  └─ GithubActionReporterTest.php
│        │     ├─ ColorTest.php
│        │     ├─ Command
│        │     │  ├─ CommandTest.php
│        │     │  ├─ CompleteCommandTest.php
│        │     │  ├─ DumpCompletionCommandTest.php
│        │     │  ├─ HelpCommandTest.php
│        │     │  ├─ InvokableCommandTest.php
│        │     │  ├─ ListCommandTest.php
│        │     │  ├─ LockableTraitTest.php
│        │     │  └─ SingleCommandApplicationTest.php
│        │     ├─ CommandLoader
│        │     │  ├─ ContainerCommandLoaderTest.php
│        │     │  └─ FactoryCommandLoaderTest.php
│        │     ├─ Completion
│        │     │  ├─ CompletionInputTest.php
│        │     │  └─ Output
│        │     │     ├─ BashCompletionOutputTest.php
│        │     │     ├─ CompletionOutputTestCase.php
│        │     │     ├─ FishCompletionOutputTest.php
│        │     │     └─ ZshCompletionOutputTest.php
│        │     ├─ ConsoleEventsTest.php
│        │     ├─ CursorTest.php
│        │     ├─ DependencyInjection
│        │     │  └─ AddConsoleCommandPassTest.php
│        │     ├─ Descriptor
│        │     │  ├─ AbstractDescriptorTestCase.php
│        │     │  ├─ ApplicationDescriptionTest.php
│        │     │  ├─ JsonDescriptorTest.php
│        │     │  ├─ MarkdownDescriptorTest.php
│        │     │  ├─ ObjectsProvider.php
│        │     │  ├─ ReStructuredTextDescriptorTest.php
│        │     │  ├─ TextDescriptorTest.php
│        │     │  └─ XmlDescriptorTest.php
│        │     ├─ EventListener
│        │     │  └─ ErrorListenerTest.php
│        │     ├─ Fixtures
│        │     │  ├─ application.dont_run_alternative_namespace_name.txt
│        │     │  ├─ application_1.json
│        │     │  ├─ application_1.md
│        │     │  ├─ application_1.rst
│        │     │  ├─ application_1.txt
│        │     │  ├─ application_1.xml
│        │     │  ├─ application_2.json
│        │     │  ├─ application_2.md
│        │     │  ├─ application_2.rst
│        │     │  ├─ application_2.txt
│        │     │  ├─ application_2.xml
│        │     │  ├─ application_filtered_namespace.txt
│        │     │  ├─ application_gethelp.txt
│        │     │  ├─ application_mbstring.md
│        │     │  ├─ application_mbstring.rst
│        │     │  ├─ application_mbstring.txt
│        │     │  ├─ application_renderexception1.txt
│        │     │  ├─ application_renderexception2.txt
│        │     │  ├─ application_renderexception3.txt
│        │     │  ├─ application_renderexception3decorated.txt
│        │     │  ├─ application_renderexception4.txt
│        │     │  ├─ application_renderexception_doublewidth1.txt
│        │     │  ├─ application_renderexception_doublewidth1decorated.txt
│        │     │  ├─ application_renderexception_doublewidth2.txt
│        │     │  ├─ application_renderexception_escapeslines.txt
│        │     │  ├─ application_renderexception_linebreaks.txt
│        │     │  ├─ application_rendersynopsis_escapesline.txt
│        │     │  ├─ application_run1.txt
│        │     │  ├─ application_run2.txt
│        │     │  ├─ application_run3.txt
│        │     │  ├─ application_run4.txt
│        │     │  ├─ application_run5.txt
│        │     │  ├─ application_signalable.php
│        │     │  ├─ BarBucCommand.php
│        │     │  ├─ BarHiddenCommand.php
│        │     │  ├─ command_1.json
│        │     │  ├─ command_1.md
│        │     │  ├─ command_1.rst
│        │     │  ├─ command_1.txt
│        │     │  ├─ command_1.xml
│        │     │  ├─ command_2.json
│        │     │  ├─ command_2.md
│        │     │  ├─ command_2.rst
│        │     │  ├─ command_2.txt
│        │     │  ├─ command_2.xml
│        │     │  ├─ command_mbstring.md
│        │     │  ├─ command_mbstring.rst
│        │     │  ├─ command_mbstring.txt
│        │     │  ├─ DescriptorApplication1.php
│        │     │  ├─ DescriptorApplication2.php
│        │     │  ├─ DescriptorApplicationMbString.php
│        │     │  ├─ DescriptorCommand1.php
│        │     │  ├─ DescriptorCommand2.php
│        │     │  ├─ DescriptorCommand3.php
│        │     │  ├─ DescriptorCommand4.php
│        │     │  ├─ DescriptorCommandMbString.php
│        │     │  ├─ DummyOutput.php
│        │     │  ├─ Foo1Command.php
│        │     │  ├─ Foo2Command.php
│        │     │  ├─ Foo3Command.php
│        │     │  ├─ Foo4Command.php
│        │     │  ├─ Foo5Command.php
│        │     │  ├─ Foo6Command.php
│        │     │  ├─ FoobarCommand.php
│        │     │  ├─ FooCommand.php
│        │     │  ├─ FooHiddenCommand.php
│        │     │  ├─ FooLock2Command.php
│        │     │  ├─ FooLock3Command.php
│        │     │  ├─ FooLock4InvokableCommand.php
│        │     │  ├─ FooLockCommand.php
│        │     │  ├─ FooOptCommand.php
│        │     │  ├─ FooSameCaseLowercaseCommand.php
│        │     │  ├─ FooSameCaseUppercaseCommand.php
│        │     │  ├─ FooSubnamespaced1Command.php
│        │     │  ├─ FooSubnamespaced2Command.php
│        │     │  ├─ FooWithoutAliasCommand.php
│        │     │  ├─ input_argument_1.json
│        │     │  ├─ input_argument_1.md
│        │     │  ├─ input_argument_1.rst
│        │     │  ├─ input_argument_1.txt
│        │     │  ├─ input_argument_1.xml
│        │     │  ├─ input_argument_2.json
│        │     │  ├─ input_argument_2.md
│        │     │  ├─ input_argument_2.rst
│        │     │  ├─ input_argument_2.txt
│        │     │  ├─ input_argument_2.xml
│        │     │  ├─ input_argument_3.json
│        │     │  ├─ input_argument_3.md
│        │     │  ├─ input_argument_3.rst
│        │     │  ├─ input_argument_3.txt
│        │     │  ├─ input_argument_3.xml
│        │     │  ├─ input_argument_4.json
│        │     │  ├─ input_argument_4.md
│        │     │  ├─ input_argument_4.rst
│        │     │  ├─ input_argument_4.txt
│        │     │  ├─ input_argument_4.xml
│        │     │  ├─ input_argument_with_default_inf_value.json
│        │     │  ├─ input_argument_with_default_inf_value.md
│        │     │  ├─ input_argument_with_default_inf_value.rst
│        │     │  ├─ input_argument_with_default_inf_value.txt
│        │     │  ├─ input_argument_with_default_inf_value.xml
│        │     │  ├─ input_argument_with_style.json
│        │     │  ├─ input_argument_with_style.md
│        │     │  ├─ input_argument_with_style.rst
│        │     │  ├─ input_argument_with_style.txt
│        │     │  ├─ input_argument_with_style.xml
│        │     │  ├─ input_definition_1.json
│        │     │  ├─ input_definition_1.md
│        │     │  ├─ input_definition_1.rst
│        │     │  ├─ input_definition_1.txt
│        │     │  ├─ input_definition_1.xml
│        │     │  ├─ input_definition_2.json
│        │     │  ├─ input_definition_2.md
│        │     │  ├─ input_definition_2.rst
│        │     │  ├─ input_definition_2.txt
│        │     │  ├─ input_definition_2.xml
│        │     │  ├─ input_definition_3.json
│        │     │  ├─ input_definition_3.md
│        │     │  ├─ input_definition_3.rst
│        │     │  ├─ input_definition_3.txt
│        │     │  ├─ input_definition_3.xml
│        │     │  ├─ input_definition_4.json
│        │     │  ├─ input_definition_4.md
│        │     │  ├─ input_definition_4.rst
│        │     │  ├─ input_definition_4.txt
│        │     │  ├─ input_definition_4.xml
│        │     │  ├─ input_option_1.json
│        │     │  ├─ input_option_1.md
│        │     │  ├─ input_option_1.rst
│        │     │  ├─ input_option_1.txt
│        │     │  ├─ input_option_1.xml
│        │     │  ├─ input_option_2.json
│        │     │  ├─ input_option_2.md
│        │     │  ├─ input_option_2.rst
│        │     │  ├─ input_option_2.txt
│        │     │  ├─ input_option_2.xml
│        │     │  ├─ input_option_3.json
│        │     │  ├─ input_option_3.md
│        │     │  ├─ input_option_3.rst
│        │     │  ├─ input_option_3.txt
│        │     │  ├─ input_option_3.xml
│        │     │  ├─ input_option_4.json
│        │     │  ├─ input_option_4.md
│        │     │  ├─ input_option_4.rst
│        │     │  ├─ input_option_4.txt
│        │     │  ├─ input_option_4.xml
│        │     │  ├─ input_option_5.json
│        │     │  ├─ input_option_5.md
│        │     │  ├─ input_option_5.rst
│        │     │  ├─ input_option_5.txt
│        │     │  ├─ input_option_5.xml
│        │     │  ├─ input_option_6.json
│        │     │  ├─ input_option_6.md
│        │     │  ├─ input_option_6.rst
│        │     │  ├─ input_option_6.txt
│        │     │  ├─ input_option_6.xml
│        │     │  ├─ input_option_with_default_inf_value.json
│        │     │  ├─ input_option_with_default_inf_value.md
│        │     │  ├─ input_option_with_default_inf_value.rst
│        │     │  ├─ input_option_with_default_inf_value.txt
│        │     │  ├─ input_option_with_default_inf_value.xml
│        │     │  ├─ input_option_with_style.json
│        │     │  ├─ input_option_with_style.md
│        │     │  ├─ input_option_with_style.rst
│        │     │  ├─ input_option_with_style.txt
│        │     │  ├─ input_option_with_style.xml
│        │     │  ├─ input_option_with_style_array.json
│        │     │  ├─ input_option_with_style_array.md
│        │     │  ├─ input_option_with_style_array.rst
│        │     │  ├─ input_option_with_style_array.txt
│        │     │  ├─ input_option_with_style_array.xml
│        │     │  ├─ MockableAppliationWithTerminalWidth.php
│        │     │  ├─ stream_output_file.txt
│        │     │  ├─ Style
│        │     │  │  └─ SymfonyStyle
│        │     │  │     ├─ command
│        │     │  │     │  ├─ command_0.php
│        │     │  │     │  ├─ command_1.php
│        │     │  │     │  ├─ command_10.php
│        │     │  │     │  ├─ command_11.php
│        │     │  │     │  ├─ command_12.php
│        │     │  │     │  ├─ command_13.php
│        │     │  │     │  ├─ command_14.php
│        │     │  │     │  ├─ command_15.php
│        │     │  │     │  ├─ command_16.php
│        │     │  │     │  ├─ command_17.php
│        │     │  │     │  ├─ command_18.php
│        │     │  │     │  ├─ command_19.php
│        │     │  │     │  ├─ command_2.php
│        │     │  │     │  ├─ command_20.php
│        │     │  │     │  ├─ command_21.php
│        │     │  │     │  ├─ command_22.php
│        │     │  │     │  ├─ command_23.php
│        │     │  │     │  ├─ command_3.php
│        │     │  │     │  ├─ command_4.php
│        │     │  │     │  ├─ command_4_with_iterators.php
│        │     │  │     │  ├─ command_5.php
│        │     │  │     │  ├─ command_6.php
│        │     │  │     │  ├─ command_7.php
│        │     │  │     │  ├─ command_8.php
│        │     │  │     │  ├─ command_9.php
│        │     │  │     │  └─ interactive_command_1.php
│        │     │  │     ├─ output
│        │     │  │     │  ├─ interactive_output_1.txt
│        │     │  │     │  ├─ output_0.txt
│        │     │  │     │  ├─ output_1.txt
│        │     │  │     │  ├─ output_10.txt
│        │     │  │     │  ├─ output_11.txt
│        │     │  │     │  ├─ output_12.txt
│        │     │  │     │  ├─ output_13.txt
│        │     │  │     │  ├─ output_14.txt
│        │     │  │     │  ├─ output_15.txt
│        │     │  │     │  ├─ output_16.txt
│        │     │  │     │  ├─ output_17.txt
│        │     │  │     │  ├─ output_18.txt
│        │     │  │     │  ├─ output_19.txt
│        │     │  │     │  ├─ output_2.txt
│        │     │  │     │  ├─ output_20.txt
│        │     │  │     │  ├─ output_21.txt
│        │     │  │     │  ├─ output_22.txt
│        │     │  │     │  ├─ output_23.txt
│        │     │  │     │  ├─ output_3.txt
│        │     │  │     │  ├─ output_4.txt
│        │     │  │     │  ├─ output_4_with_iterators.txt
│        │     │  │     │  ├─ output_5.txt
│        │     │  │     │  ├─ output_6.txt
│        │     │  │     │  ├─ output_7.txt
│        │     │  │     │  ├─ output_8.txt
│        │     │  │     │  └─ output_9.txt
│        │     │  │     └─ progress
│        │     │  │        ├─ command_progress_iterate.php
│        │     │  │        ├─ output_progress_iterate_no_shade.txt
│        │     │  │        └─ output_progress_iterate_shade.txt
│        │     │  ├─ TestAmbiguousCommandRegistering.php
│        │     │  ├─ TestAmbiguousCommandRegistering2.php
│        │     │  └─ TestCommand.php
│        │     ├─ Formatter
│        │     │  ├─ NullOutputFormatterStyleTest.php
│        │     │  ├─ NullOutputFormatterTest.php
│        │     │  ├─ OutputFormatterStyleStackTest.php
│        │     │  ├─ OutputFormatterStyleTest.php
│        │     │  └─ OutputFormatterTest.php
│        │     ├─ Helper
│        │     │  ├─ AbstractQuestionHelperTestCase.php
│        │     │  ├─ DescriptorHelperTest.php
│        │     │  ├─ DumperNativeFallbackTest.php
│        │     │  ├─ DumperTest.php
│        │     │  ├─ FormatterHelperTest.php
│        │     │  ├─ HelperSetTest.php
│        │     │  ├─ HelperTest.php
│        │     │  ├─ OutputWrapperTest.php
│        │     │  ├─ ProcessHelperTest.php
│        │     │  ├─ ProgressBarTest.php
│        │     │  ├─ ProgressIndicatorTest.php
│        │     │  ├─ QuestionHelperTest.php
│        │     │  ├─ SymfonyQuestionHelperTest.php
│        │     │  ├─ TableCellStyleTest.php
│        │     │  ├─ TableStyleTest.php
│        │     │  ├─ TableTest.php
│        │     │  ├─ TreeHelperTest.php
│        │     │  ├─ TreeNodeTest.php
│        │     │  └─ TreeStyleTest.php
│        │     ├─ Input
│        │     │  ├─ ArgvInputTest.php
│        │     │  ├─ ArrayInputTest.php
│        │     │  ├─ InputArgumentTest.php
│        │     │  ├─ InputDefinitionTest.php
│        │     │  ├─ InputOptionTest.php
│        │     │  ├─ InputTest.php
│        │     │  └─ StringInputTest.php
│        │     ├─ Logger
│        │     │  └─ ConsoleLoggerTest.php
│        │     ├─ Messenger
│        │     │  └─ RunCommandMessageHandlerTest.php
│        │     ├─ Output
│        │     │  ├─ AnsiColorModeTest.php
│        │     │  ├─ ConsoleOutputTest.php
│        │     │  ├─ ConsoleSectionOutputTest.php
│        │     │  ├─ NullOutputTest.php
│        │     │  ├─ OutputTest.php
│        │     │  └─ StreamOutputTest.php
│        │     ├─ phpt
│        │     │  ├─ alarm
│        │     │  │  └─ command_exit.phpt
│        │     │  ├─ signal
│        │     │  │  └─ command_exit.phpt
│        │     │  ├─ single_application
│        │     │  │  ├─ arg.phpt
│        │     │  │  ├─ default.phpt
│        │     │  │  ├─ help_name.phpt
│        │     │  │  ├─ version_default_name.phpt
│        │     │  │  └─ version_name.phpt
│        │     │  └─ uses_stdin_as_interactive_input.phpt
│        │     ├─ Question
│        │     │  ├─ ChoiceQuestionTest.php
│        │     │  ├─ ConfirmationQuestionTest.php
│        │     │  └─ QuestionTest.php
│        │     ├─ SignalRegistry
│        │     │  ├─ SignalMapTest.php
│        │     │  └─ SignalRegistryTest.php
│        │     ├─ Style
│        │     │  └─ SymfonyStyleTest.php
│        │     ├─ TerminalTest.php
│        │     └─ Tester
│        │        ├─ ApplicationTesterTest.php
│        │        ├─ CommandTesterTest.php
│        │        └─ Constraint
│        │           └─ CommandIsSuccessfulTest.php
│        ├─ dependency-injection
│        │  ├─ Alias.php
│        │  ├─ Argument
│        │  │  ├─ AbstractArgument.php
│        │  │  ├─ ArgumentInterface.php
│        │  │  ├─ BoundArgument.php
│        │  │  ├─ IteratorArgument.php
│        │  │  ├─ LazyClosure.php
│        │  │  ├─ RewindableGenerator.php
│        │  │  ├─ ServiceClosureArgument.php
│        │  │  ├─ ServiceLocator.php
│        │  │  ├─ ServiceLocatorArgument.php
│        │  │  └─ TaggedIteratorArgument.php
│        │  ├─ Attribute
│        │  │  ├─ AsAlias.php
│        │  │  ├─ AsDecorator.php
│        │  │  ├─ AsTaggedItem.php
│        │  │  ├─ Autoconfigure.php
│        │  │  ├─ AutoconfigureTag.php
│        │  │  ├─ Autowire.php
│        │  │  ├─ AutowireCallable.php
│        │  │  ├─ AutowireDecorated.php
│        │  │  ├─ AutowireInline.php
│        │  │  ├─ AutowireIterator.php
│        │  │  ├─ AutowireLocator.php
│        │  │  ├─ AutowireMethodOf.php
│        │  │  ├─ AutowireServiceClosure.php
│        │  │  ├─ Exclude.php
│        │  │  ├─ Lazy.php
│        │  │  ├─ TaggedIterator.php
│        │  │  ├─ TaggedLocator.php
│        │  │  ├─ Target.php
│        │  │  ├─ When.php
│        │  │  └─ WhenNot.php
│        │  ├─ CHANGELOG.md
│        │  ├─ ChildDefinition.php
│        │  ├─ Compiler
│        │  │  ├─ AbstractRecursivePass.php
│        │  │  ├─ AliasDeprecatedPublicServicesPass.php
│        │  │  ├─ AnalyzeServiceReferencesPass.php
│        │  │  ├─ AttributeAutoconfigurationPass.php
│        │  │  ├─ AutoAliasServicePass.php
│        │  │  ├─ AutowireAsDecoratorPass.php
│        │  │  ├─ AutowirePass.php
│        │  │  ├─ AutowireRequiredMethodsPass.php
│        │  │  ├─ AutowireRequiredPropertiesPass.php
│        │  │  ├─ CheckAliasValidityPass.php
│        │  │  ├─ CheckArgumentsValidityPass.php
│        │  │  ├─ CheckCircularReferencesPass.php
│        │  │  ├─ CheckDefinitionValidityPass.php
│        │  │  ├─ CheckExceptionOnInvalidReferenceBehaviorPass.php
│        │  │  ├─ CheckReferenceValidityPass.php
│        │  │  ├─ CheckTypeDeclarationsPass.php
│        │  │  ├─ Compiler.php
│        │  │  ├─ CompilerPassInterface.php
│        │  │  ├─ DecoratorServicePass.php
│        │  │  ├─ DefinitionErrorExceptionPass.php
│        │  │  ├─ ExtensionCompilerPass.php
│        │  │  ├─ InlineServiceDefinitionsPass.php
│        │  │  ├─ MergeExtensionConfigurationPass.php
│        │  │  ├─ PassConfig.php
│        │  │  ├─ PriorityTaggedServiceTrait.php
│        │  │  ├─ RegisterAutoconfigureAttributesPass.php
│        │  │  ├─ RegisterEnvVarProcessorsPass.php
│        │  │  ├─ RegisterReverseContainerPass.php
│        │  │  ├─ RegisterServiceSubscribersPass.php
│        │  │  ├─ RemoveAbstractDefinitionsPass.php
│        │  │  ├─ RemoveBuildParametersPass.php
│        │  │  ├─ RemovePrivateAliasesPass.php
│        │  │  ├─ RemoveUnusedDefinitionsPass.php
│        │  │  ├─ ReplaceAliasByActualDefinitionPass.php
│        │  │  ├─ ResolveAutowireInlineAttributesPass.php
│        │  │  ├─ ResolveBindingsPass.php
│        │  │  ├─ ResolveChildDefinitionsPass.php
│        │  │  ├─ ResolveClassPass.php
│        │  │  ├─ ResolveDecoratorStackPass.php
│        │  │  ├─ ResolveEnvPlaceholdersPass.php
│        │  │  ├─ ResolveFactoryClassPass.php
│        │  │  ├─ ResolveHotPathPass.php
│        │  │  ├─ ResolveInstanceofConditionalsPass.php
│        │  │  ├─ ResolveInvalidReferencesPass.php
│        │  │  ├─ ResolveNamedArgumentsPass.php
│        │  │  ├─ ResolveNoPreloadPass.php
│        │  │  ├─ ResolveParameterPlaceHoldersPass.php
│        │  │  ├─ ResolveReferencesToAliasesPass.php
│        │  │  ├─ ResolveServiceSubscribersPass.php
│        │  │  ├─ ResolveTaggedIteratorArgumentPass.php
│        │  │  ├─ ServiceLocatorTagPass.php
│        │  │  ├─ ServiceReferenceGraph.php
│        │  │  ├─ ServiceReferenceGraphEdge.php
│        │  │  ├─ ServiceReferenceGraphNode.php
│        │  │  └─ ValidateEnvPlaceholdersPass.php
│        │  ├─ composer.json
│        │  ├─ Config
│        │  │  ├─ ContainerParametersResource.php
│        │  │  └─ ContainerParametersResourceChecker.php
│        │  ├─ Container.php
│        │  ├─ ContainerBuilder.php
│        │  ├─ ContainerInterface.php
│        │  ├─ Definition.php
│        │  ├─ Dumper
│        │  │  ├─ Dumper.php
│        │  │  ├─ DumperInterface.php
│        │  │  ├─ GraphvizDumper.php
│        │  │  ├─ PhpDumper.php
│        │  │  ├─ Preloader.php
│        │  │  ├─ XmlDumper.php
│        │  │  └─ YamlDumper.php
│        │  ├─ EnvVarLoaderInterface.php
│        │  ├─ EnvVarProcessor.php
│        │  ├─ EnvVarProcessorInterface.php
│        │  ├─ Exception
│        │  │  ├─ AutoconfigureFailedException.php
│        │  │  ├─ AutowiringFailedException.php
│        │  │  ├─ BadMethodCallException.php
│        │  │  ├─ EmptyParameterValueException.php
│        │  │  ├─ EnvNotFoundException.php
│        │  │  ├─ EnvParameterException.php
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ InvalidArgumentException.php
│        │  │  ├─ InvalidParameterTypeException.php
│        │  │  ├─ LogicException.php
│        │  │  ├─ OutOfBoundsException.php
│        │  │  ├─ ParameterCircularReferenceException.php
│        │  │  ├─ ParameterNotFoundException.php
│        │  │  ├─ RuntimeException.php
│        │  │  ├─ ServiceCircularReferenceException.php
│        │  │  └─ ServiceNotFoundException.php
│        │  ├─ ExpressionLanguage.php
│        │  ├─ ExpressionLanguageProvider.php
│        │  ├─ Extension
│        │  │  ├─ AbstractExtension.php
│        │  │  ├─ ConfigurableExtensionInterface.php
│        │  │  ├─ ConfigurationExtensionInterface.php
│        │  │  ├─ Extension.php
│        │  │  ├─ ExtensionInterface.php
│        │  │  ├─ ExtensionTrait.php
│        │  │  └─ PrependExtensionInterface.php
│        │  ├─ LazyProxy
│        │  │  ├─ Instantiator
│        │  │  │  ├─ InstantiatorInterface.php
│        │  │  │  ├─ LazyServiceInstantiator.php
│        │  │  │  └─ RealServiceInstantiator.php
│        │  │  └─ PhpDumper
│        │  │     ├─ DumperInterface.php
│        │  │     ├─ LazyServiceDumper.php
│        │  │     └─ NullDumper.php
│        │  ├─ LICENSE
│        │  ├─ Loader
│        │  │  ├─ ClosureLoader.php
│        │  │  ├─ Configurator
│        │  │  │  ├─ AbstractConfigurator.php
│        │  │  │  ├─ AbstractServiceConfigurator.php
│        │  │  │  ├─ AliasConfigurator.php
│        │  │  │  ├─ ClosureReferenceConfigurator.php
│        │  │  │  ├─ ContainerConfigurator.php
│        │  │  │  ├─ DefaultsConfigurator.php
│        │  │  │  ├─ EnvConfigurator.php
│        │  │  │  ├─ FromCallableConfigurator.php
│        │  │  │  ├─ InlineServiceConfigurator.php
│        │  │  │  ├─ InstanceofConfigurator.php
│        │  │  │  ├─ ParametersConfigurator.php
│        │  │  │  ├─ PrototypeConfigurator.php
│        │  │  │  ├─ ReferenceConfigurator.php
│        │  │  │  ├─ ServiceConfigurator.php
│        │  │  │  ├─ ServicesConfigurator.php
│        │  │  │  └─ Traits
│        │  │  │     ├─ AbstractTrait.php
│        │  │  │     ├─ ArgumentTrait.php
│        │  │  │     ├─ AutoconfigureTrait.php
│        │  │  │     ├─ AutowireTrait.php
│        │  │  │     ├─ BindTrait.php
│        │  │  │     ├─ CallTrait.php
│        │  │  │     ├─ ClassTrait.php
│        │  │  │     ├─ ConfiguratorTrait.php
│        │  │  │     ├─ ConstructorTrait.php
│        │  │  │     ├─ DecorateTrait.php
│        │  │  │     ├─ DeprecateTrait.php
│        │  │  │     ├─ FactoryTrait.php
│        │  │  │     ├─ FileTrait.php
│        │  │  │     ├─ FromCallableTrait.php
│        │  │  │     ├─ LazyTrait.php
│        │  │  │     ├─ ParentTrait.php
│        │  │  │     ├─ PropertyTrait.php
│        │  │  │     ├─ PublicTrait.php
│        │  │  │     ├─ ShareTrait.php
│        │  │  │     ├─ SyntheticTrait.php
│        │  │  │     └─ TagTrait.php
│        │  │  ├─ DirectoryLoader.php
│        │  │  ├─ FileLoader.php
│        │  │  ├─ GlobFileLoader.php
│        │  │  ├─ IniFileLoader.php
│        │  │  ├─ PhpFileLoader.php
│        │  │  ├─ schema
│        │  │  │  └─ dic
│        │  │  │     └─ services
│        │  │  │        └─ services-1.0.xsd
│        │  │  ├─ UndefinedExtensionHandler.php
│        │  │  ├─ XmlFileLoader.php
│        │  │  └─ YamlFileLoader.php
│        │  ├─ Parameter.php
│        │  ├─ ParameterBag
│        │  │  ├─ ContainerBag.php
│        │  │  ├─ ContainerBagInterface.php
│        │  │  ├─ EnvPlaceholderParameterBag.php
│        │  │  ├─ FrozenParameterBag.php
│        │  │  ├─ ParameterBag.php
│        │  │  └─ ParameterBagInterface.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Reference.php
│        │  ├─ ReverseContainer.php
│        │  ├─ ServiceLocator.php
│        │  ├─ StaticEnvVarLoader.php
│        │  ├─ TaggedContainerInterface.php
│        │  ├─ Tests
│        │  │  ├─ AliasTest.php
│        │  │  ├─ Argument
│        │  │  │  ├─ AbstractArgumentTest.php
│        │  │  │  ├─ LazyClosureTest.php
│        │  │  │  ├─ RewindableGeneratorTest.php
│        │  │  │  └─ TaggedIteratorArgumentTest.php
│        │  │  ├─ Attribute
│        │  │  │  ├─ AutowireCallableTest.php
│        │  │  │  ├─ AutowireInlineTest.php
│        │  │  │  ├─ AutowireLocatorTest.php
│        │  │  │  ├─ AutowireMethodOfTest.php
│        │  │  │  └─ AutowireTest.php
│        │  │  ├─ ChildDefinitionTest.php
│        │  │  ├─ Compiler
│        │  │  │  ├─ AbstractRecursivePassTest.php
│        │  │  │  ├─ AliasDeprecatedPublicServicesPassTest.php
│        │  │  │  ├─ AnalyzeServiceReferencesPassTest.php
│        │  │  │  ├─ AttributeAutoconfigurationPassTest.php
│        │  │  │  ├─ AutoAliasServicePassTest.php
│        │  │  │  ├─ AutowirePassTest.php
│        │  │  │  ├─ AutowireRequiredMethodsPassTest.php
│        │  │  │  ├─ AutowireRequiredPropertiesPassTest.php
│        │  │  │  ├─ CheckAliasValidityPassTest.php
│        │  │  │  ├─ CheckArgumentsValidityPassTest.php
│        │  │  │  ├─ CheckCircularReferencesPassTest.php
│        │  │  │  ├─ CheckDefinitionValidityPassTest.php
│        │  │  │  ├─ CheckExceptionOnInvalidReferenceBehaviorPassTest.php
│        │  │  │  ├─ CheckReferenceValidityPassTest.php
│        │  │  │  ├─ CheckTypeDeclarationsPassTest.php
│        │  │  │  ├─ CustomExpressionLanguageFunctionTest.php
│        │  │  │  ├─ DecoratorServicePassTest.php
│        │  │  │  ├─ DefinitionErrorExceptionPassTest.php
│        │  │  │  ├─ ExtensionCompilerPassTest.php
│        │  │  │  ├─ InlineServiceDefinitionsPassTest.php
│        │  │  │  ├─ IntegrationTest.php
│        │  │  │  ├─ MergeExtensionConfigurationPassTest.php
│        │  │  │  ├─ OptionalServiceClass.php
│        │  │  │  ├─ PassConfigTest.php
│        │  │  │  ├─ PriorityTaggedServiceTraitTest.php
│        │  │  │  ├─ RegisterAutoconfigureAttributesPassTest.php
│        │  │  │  ├─ RegisterEnvVarProcessorsPassTest.php
│        │  │  │  ├─ RegisterReverseContainerPassTest.php
│        │  │  │  ├─ RegisterServiceSubscribersPassTest.php
│        │  │  │  ├─ RemoveBuildParametersPassTest.php
│        │  │  │  ├─ RemoveUnusedDefinitionsPassTest.php
│        │  │  │  ├─ ReplaceAliasByActualDefinitionPassTest.php
│        │  │  │  ├─ ResolveAutowireInlineAttributesPassTest.php
│        │  │  │  ├─ ResolveBindingsPassTest.php
│        │  │  │  ├─ ResolveChildDefinitionsPassTest.php
│        │  │  │  ├─ ResolveClassPassTest.php
│        │  │  │  ├─ ResolveFactoryClassPassTest.php
│        │  │  │  ├─ ResolveHotPathPassTest.php
│        │  │  │  ├─ ResolveInstanceofConditionalsPassTest.php
│        │  │  │  ├─ ResolveInvalidReferencesPassTest.php
│        │  │  │  ├─ ResolveNamedArgumentsPassTest.php
│        │  │  │  ├─ ResolveNoPreloadPassTest.php
│        │  │  │  ├─ ResolveParameterPlaceHoldersPassTest.php
│        │  │  │  ├─ ResolveReferencesToAliasesPassTest.php
│        │  │  │  ├─ ResolveTaggedIteratorArgumentPassTest.php
│        │  │  │  ├─ ServiceLocatorTagPassTest.php
│        │  │  │  └─ ValidateEnvPlaceholdersPassTest.php
│        │  │  ├─ Config
│        │  │  │  ├─ ContainerParametersResourceCheckerTest.php
│        │  │  │  └─ ContainerParametersResourceTest.php
│        │  │  ├─ ContainerBuilderTest.php
│        │  │  ├─ ContainerTest.php
│        │  │  ├─ CrossCheckTest.php
│        │  │  ├─ DefinitionTest.php
│        │  │  ├─ Dumper
│        │  │  │  ├─ GraphvizDumperTest.php
│        │  │  │  ├─ PhpDumperTest.php
│        │  │  │  ├─ PreloaderTest.php
│        │  │  │  ├─ XmlDumperTest.php
│        │  │  │  └─ YamlDumperTest.php
│        │  │  ├─ EnvVarProcessorTest.php
│        │  │  ├─ Exception
│        │  │  │  ├─ AutowiringFailedExceptionTest.php
│        │  │  │  └─ InvalidParameterTypeExceptionTest.php
│        │  │  ├─ Extension
│        │  │  │  ├─ AbstractExtensionTest.php
│        │  │  │  └─ ExtensionTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ AcmeConfig
│        │  │  │  │  └─ NestedConfig.php
│        │  │  │  ├─ AcmeConfig.php
│        │  │  │  ├─ array.json
│        │  │  │  ├─ Attribute
│        │  │  │  │  ├─ CustomAnyAttribute.php
│        │  │  │  │  ├─ CustomAutoconfiguration.php
│        │  │  │  │  ├─ CustomChildAttribute.php
│        │  │  │  │  ├─ CustomMethodAttribute.php
│        │  │  │  │  ├─ CustomParameterAttribute.php
│        │  │  │  │  └─ CustomPropertyAttribute.php
│        │  │  │  ├─ AutoconfigureAttributed.php
│        │  │  │  ├─ AutoconfiguredInterface.php
│        │  │  │  ├─ AutoconfiguredInterface2.php
│        │  │  │  ├─ AutoconfiguredService1.php
│        │  │  │  ├─ AutoconfiguredService2.php
│        │  │  │  ├─ AutoconfigureRepeated.php
│        │  │  │  ├─ AutoconfigureRepeatedBindings.php
│        │  │  │  ├─ AutoconfigureRepeatedCalls.php
│        │  │  │  ├─ AutoconfigureRepeatedOverwrite.php
│        │  │  │  ├─ AutoconfigureRepeatedProperties.php
│        │  │  │  ├─ AutoconfigureRepeatedTag.php
│        │  │  │  ├─ AutowireLocatorConsumer.php
│        │  │  │  ├─ Bar.php
│        │  │  │  ├─ BarFactory.php
│        │  │  │  ├─ BarInterface.php
│        │  │  │  ├─ BarTagClass.php
│        │  │  │  ├─ CaseSensitiveClass.php
│        │  │  │  ├─ CheckAliasValidityPass
│        │  │  │  │  ├─ FooImplementing.php
│        │  │  │  │  ├─ FooInterface.php
│        │  │  │  │  └─ FooNotImplementing.php
│        │  │  │  ├─ CheckTypeDeclarationsPass
│        │  │  │  │  ├─ Bar.php
│        │  │  │  │  ├─ BarErroredDependency.php
│        │  │  │  │  ├─ BarMethodCall.php
│        │  │  │  │  ├─ BarOptionalArgument.php
│        │  │  │  │  ├─ BarOptionalArgumentNotNull.php
│        │  │  │  │  ├─ Deprecated.php
│        │  │  │  │  ├─ Foo.php
│        │  │  │  │  ├─ FooObject.php
│        │  │  │  │  ├─ IntersectionConstructor.php
│        │  │  │  │  ├─ UnionConstructor.php
│        │  │  │  │  ├─ UnionConstructorPHP82.php
│        │  │  │  │  ├─ Waldo.php
│        │  │  │  │  ├─ WaldoFoo.php
│        │  │  │  │  ├─ WaldoInterface.php
│        │  │  │  │  └─ Wobble.php
│        │  │  │  ├─ config
│        │  │  │  │  ├─ anonymous.expected.yml
│        │  │  │  │  ├─ anonymous.php
│        │  │  │  │  ├─ basic.expected.yml
│        │  │  │  │  ├─ basic.php
│        │  │  │  │  ├─ child.expected.yml
│        │  │  │  │  ├─ child.php
│        │  │  │  │  ├─ closure.expected.yml
│        │  │  │  │  ├─ closure.php
│        │  │  │  │  ├─ config_builder.expected.yml
│        │  │  │  │  ├─ config_builder.php
│        │  │  │  │  ├─ config_builder_env_configurator.php
│        │  │  │  │  ├─ defaults.expected.yml
│        │  │  │  │  ├─ defaults.php
│        │  │  │  │  ├─ definition
│        │  │  │  │  │  ├─ foo.php
│        │  │  │  │  │  └─ multiple
│        │  │  │  │  │     ├─ bar.php
│        │  │  │  │  │     └─ baz.php
│        │  │  │  │  ├─ env_configurator.php
│        │  │  │  │  ├─ env_param.expected.yml
│        │  │  │  │  ├─ env_param.php
│        │  │  │  │  ├─ expression_factory.expected.yml
│        │  │  │  │  ├─ expression_factory.php
│        │  │  │  │  ├─ factory_short_notation.php
│        │  │  │  │  ├─ from_callable.expected.yml
│        │  │  │  │  ├─ from_callable.php
│        │  │  │  │  ├─ inline_binding.expected.yml
│        │  │  │  │  ├─ inline_binding.php
│        │  │  │  │  ├─ inline_static_constructor.expected.yml
│        │  │  │  │  ├─ inline_static_constructor.php
│        │  │  │  │  ├─ instanceof.expected.yml
│        │  │  │  │  ├─ instanceof.php
│        │  │  │  │  ├─ instanceof_static_constructor.expected.yml
│        │  │  │  │  ├─ instanceof_static_constructor.php
│        │  │  │  │  ├─ lazy_fqcn.expected.yml
│        │  │  │  │  ├─ lazy_fqcn.php
│        │  │  │  │  ├─ nested_bundle_config.php
│        │  │  │  │  ├─ nested_config_builder.php
│        │  │  │  │  ├─ not_when_env.php
│        │  │  │  │  ├─ object.expected.yml
│        │  │  │  │  ├─ object.php
│        │  │  │  │  ├─ packages
│        │  │  │  │  │  ├─ ping.yaml
│        │  │  │  │  │  ├─ third_a.yaml
│        │  │  │  │  │  ├─ third_b.yaml
│        │  │  │  │  │  └─ third_c.yaml
│        │  │  │  │  ├─ php7.expected.yml
│        │  │  │  │  ├─ php7.php
│        │  │  │  │  ├─ prototype.expected.yml
│        │  │  │  │  ├─ prototype.php
│        │  │  │  │  ├─ prototype_array.expected.yml
│        │  │  │  │  ├─ prototype_array.php
│        │  │  │  │  ├─ remove.expected.yml
│        │  │  │  │  ├─ remove.php
│        │  │  │  │  ├─ services.php
│        │  │  │  │  ├─ services9.php
│        │  │  │  │  ├─ services_autoconfigure_with_parent.php
│        │  │  │  │  ├─ services_closure_argument.php
│        │  │  │  │  ├─ services_with_enumeration.php
│        │  │  │  │  ├─ services_with_service_locator_argument.php
│        │  │  │  │  ├─ stack.php
│        │  │  │  │  ├─ static_constructor.expected.yml
│        │  │  │  │  ├─ static_constructor.php
│        │  │  │  │  ├─ when_env.php
│        │  │  │  │  └─ when_not_when_env.php
│        │  │  │  ├─ ConstructNotExists.php
│        │  │  │  ├─ Container
│        │  │  │  │  ├─ ConstructorWithMandatoryArgumentsContainer.php
│        │  │  │  │  ├─ ConstructorWithOptionalArgumentsContainer.php
│        │  │  │  │  ├─ ConstructorWithoutArgumentsContainer.php
│        │  │  │  │  └─ NoConstructorContainer.php
│        │  │  │  ├─ containers
│        │  │  │  │  ├─ container10.php
│        │  │  │  │  ├─ container11.php
│        │  │  │  │  ├─ container12.php
│        │  │  │  │  ├─ container13.php
│        │  │  │  │  ├─ container14.php
│        │  │  │  │  ├─ container15.php
│        │  │  │  │  ├─ container16.php
│        │  │  │  │  ├─ container17.php
│        │  │  │  │  ├─ container19.php
│        │  │  │  │  ├─ container21.php
│        │  │  │  │  ├─ container24.php
│        │  │  │  │  ├─ container33.php
│        │  │  │  │  ├─ container34.php
│        │  │  │  │  ├─ container8.php
│        │  │  │  │  ├─ container9.php
│        │  │  │  │  ├─ container_abstract.php
│        │  │  │  │  ├─ container_almost_circular.php
│        │  │  │  │  ├─ container_deprecated_parameters.php
│        │  │  │  │  ├─ container_env_in_id.php
│        │  │  │  │  ├─ container_inline_requires.php
│        │  │  │  │  ├─ container_nonempty_parameters.php
│        │  │  │  │  ├─ container_non_scalar_tags.php
│        │  │  │  │  ├─ container_service_locator_argument.php
│        │  │  │  │  ├─ container_uninitialized_ref.php
│        │  │  │  │  └─ CustomContainer.php
│        │  │  │  ├─ CustomDefinition.php
│        │  │  │  ├─ DependencyContainer.php
│        │  │  │  ├─ DependencyContainerInterface.php
│        │  │  │  ├─ DeprecatedClass.php
│        │  │  │  ├─ directory
│        │  │  │  │  ├─ import
│        │  │  │  │  │  └─ import.yml
│        │  │  │  │  ├─ recurse
│        │  │  │  │  │  ├─ simple.ini
│        │  │  │  │  │  └─ simple.yml
│        │  │  │  │  └─ simple.php
│        │  │  │  ├─ Extension
│        │  │  │  │  ├─ InvalidConfig
│        │  │  │  │  │  ├─ Configuration.php
│        │  │  │  │  │  └─ InvalidConfigExtension.php
│        │  │  │  │  ├─ SemiValidConfig
│        │  │  │  │  │  ├─ Configuration.php
│        │  │  │  │  │  └─ SemiValidConfigExtension.php
│        │  │  │  │  └─ ValidConfig
│        │  │  │  │     ├─ Configuration.php
│        │  │  │  │     └─ ValidConfigExtension.php
│        │  │  │  ├─ FactoryDummy.php
│        │  │  │  ├─ FactoryDummyWithoutReturnTypes.php
│        │  │  │  ├─ FooBarTaggedClass.php
│        │  │  │  ├─ FooBarTaggedForDefaultPriorityClass.php
│        │  │  │  ├─ FooClassWithDefaultArrayAttribute.php
│        │  │  │  ├─ FooClassWithDefaultEnumAttribute.php
│        │  │  │  ├─ FooClassWithDefaultObjectAttribute.php
│        │  │  │  ├─ FooClassWithEnumAttribute.php
│        │  │  │  ├─ FooForCircularWithAddCalls.php
│        │  │  │  ├─ FooTagClass.php
│        │  │  │  ├─ FooTaggedForInvalidDefaultMethodClass.php
│        │  │  │  ├─ FooUnitEnum.php
│        │  │  │  ├─ FooWithAbstractArgument.php
│        │  │  │  ├─ graphviz
│        │  │  │  │  ├─ services1.dot
│        │  │  │  │  ├─ services10-1.dot
│        │  │  │  │  ├─ services10.dot
│        │  │  │  │  ├─ services13.dot
│        │  │  │  │  ├─ services14.dot
│        │  │  │  │  ├─ services17.dot
│        │  │  │  │  ├─ services18.dot
│        │  │  │  │  ├─ services9.dot
│        │  │  │  │  └─ services_inline.dot
│        │  │  │  ├─ includes
│        │  │  │  │  ├─ AcmeExtension.php
│        │  │  │  │  ├─ autowiring_classes.php
│        │  │  │  │  ├─ autowiring_classes_80.php
│        │  │  │  │  ├─ classes.php
│        │  │  │  │  ├─ compositetype_classes.php
│        │  │  │  │  ├─ createphar.php
│        │  │  │  │  ├─ foo.php
│        │  │  │  │  ├─ FooVariadic.php
│        │  │  │  │  ├─ foo_lazy.php
│        │  │  │  │  ├─ HotPath
│        │  │  │  │  │  ├─ C1.php
│        │  │  │  │  │  ├─ C2.php
│        │  │  │  │  │  ├─ C3.php
│        │  │  │  │  │  ├─ I1.php
│        │  │  │  │  │  ├─ P1.php
│        │  │  │  │  │  └─ T1.php
│        │  │  │  │  ├─ intersectiontype_classes.php
│        │  │  │  │  ├─ MultipleArgumentsOptionalScalarNotReallyOptional.php
│        │  │  │  │  ├─ ProjectExtension.php
│        │  │  │  │  ├─ ProjectWithXsdExtension.php
│        │  │  │  │  ├─ ProjectWithXsdExtensionInPhar.phar
│        │  │  │  │  ├─ schema
│        │  │  │  │  │  └─ project-1.0.xsd
│        │  │  │  │  └─ uniontype_classes.php
│        │  │  │  ├─ ini
│        │  │  │  │  ├─ almostvalid.ini
│        │  │  │  │  ├─ ini_with_wrong_ext.xml
│        │  │  │  │  ├─ nonvalid.ini
│        │  │  │  │  ├─ parameters.ini
│        │  │  │  │  ├─ parameters1.ini
│        │  │  │  │  ├─ parameters2.ini
│        │  │  │  │  ├─ types.ini
│        │  │  │  │  └─ when-env.ini
│        │  │  │  ├─ IntBackedEnum.php
│        │  │  │  ├─ IntTagClass.php
│        │  │  │  ├─ LazyAutoconfigured.php
│        │  │  │  ├─ LazyLoaded.php
│        │  │  │  ├─ MultipleAutoconfigureAttributed.php
│        │  │  │  ├─ NamedArgumentsDummy.php
│        │  │  │  ├─ NamedArgumentsVariadicsDummy.php
│        │  │  │  ├─ NamedEnumArgumentDummy.php
│        │  │  │  ├─ NamedIterableArgumentDummy.php
│        │  │  │  ├─ NewInInitializer.php
│        │  │  │  ├─ OptionalParameter.php
│        │  │  │  ├─ ParentNotExists.php
│        │  │  │  ├─ php
│        │  │  │  │  ├─ autowire_closure.php
│        │  │  │  │  ├─ callable_adapter_consumer.php
│        │  │  │  │  ├─ closure.php
│        │  │  │  │  ├─ closure_proxy.php
│        │  │  │  │  ├─ custom_container_class_constructor_without_arguments.php
│        │  │  │  │  ├─ custom_container_class_without_constructor.php
│        │  │  │  │  ├─ custom_container_class_with_mandatory_constructor_arguments.php
│        │  │  │  │  ├─ custom_container_class_with_optional_constructor_arguments.php
│        │  │  │  │  ├─ inline_adapter_consumer.php
│        │  │  │  │  ├─ lazy_autowire_attribute.php
│        │  │  │  │  ├─ lazy_autowire_attribute_with_intersection.php
│        │  │  │  │  ├─ lazy_closure.php
│        │  │  │  │  ├─ legacy_lazy_autowire_attribute.php
│        │  │  │  │  ├─ legacy_lazy_autowire_attribute_with_intersection.php
│        │  │  │  │  ├─ legacy_services9_lazy_inlined_factories.txt
│        │  │  │  │  ├─ legacy_services_dedup_lazy.php
│        │  │  │  │  ├─ legacy_services_non_shared_lazy.php
│        │  │  │  │  ├─ legacy_services_non_shared_lazy_as_files.txt
│        │  │  │  │  ├─ legacy_services_non_shared_lazy_ghost.php
│        │  │  │  │  ├─ legacy_services_non_shared_lazy_public.php
│        │  │  │  │  ├─ legacy_services_wither_lazy.php
│        │  │  │  │  ├─ legacy_services_wither_lazy_non_shared.php
│        │  │  │  │  ├─ php_with_wrong_ext.yml
│        │  │  │  │  ├─ return_foo_string.php
│        │  │  │  │  ├─ services1-1.php
│        │  │  │  │  ├─ services1.php
│        │  │  │  │  ├─ services10.php
│        │  │  │  │  ├─ services10_as_files.txt
│        │  │  │  │  ├─ services12.php
│        │  │  │  │  ├─ services13.php
│        │  │  │  │  ├─ services19.php
│        │  │  │  │  ├─ services24.php
│        │  │  │  │  ├─ services26.php
│        │  │  │  │  ├─ services33.php
│        │  │  │  │  ├─ services8.php
│        │  │  │  │  ├─ services9_as_files.txt
│        │  │  │  │  ├─ services9_compiled.php
│        │  │  │  │  ├─ services9_inlined_factories.txt
│        │  │  │  │  ├─ services9_inlined_factories_with_tagged_iterrator.txt
│        │  │  │  │  ├─ services9_lazy_inlined_factories.txt
│        │  │  │  │  ├─ services_adawson.php
│        │  │  │  │  ├─ services_almost_circular_private.php
│        │  │  │  │  ├─ services_almost_circular_public.php
│        │  │  │  │  ├─ services_array_params.php
│        │  │  │  │  ├─ services_base64_env.php
│        │  │  │  │  ├─ services_closure_argument_compiled.php
│        │  │  │  │  ├─ services_csv_env.php
│        │  │  │  │  ├─ services_current_factory_inlining.php
│        │  │  │  │  ├─ services_dedup_lazy.php
│        │  │  │  │  ├─ services_deep_graph.php
│        │  │  │  │  ├─ services_default_env.php
│        │  │  │  │  ├─ services_deprecated_parameters.php
│        │  │  │  │  ├─ services_deprecated_parameters_as_files.txt
│        │  │  │  │  ├─ services_env_in_id.php
│        │  │  │  │  ├─ services_errored_definition.php
│        │  │  │  │  ├─ services_inline_requires.php
│        │  │  │  │  ├─ services_inline_self_ref.php
│        │  │  │  │  ├─ services_json_env.php
│        │  │  │  │  ├─ services_locator.php
│        │  │  │  │  ├─ services_new_in_initializer.php
│        │  │  │  │  ├─ services_nonempty_parameters.php
│        │  │  │  │  ├─ services_nonempty_parameters_as_files.txt
│        │  │  │  │  ├─ services_non_shared_duplicates.php
│        │  │  │  │  ├─ services_non_shared_lazy.php
│        │  │  │  │  ├─ services_non_shared_lazy_as_files.txt
│        │  │  │  │  ├─ services_non_shared_lazy_ghost.php
│        │  │  │  │  ├─ services_non_shared_lazy_public.php
│        │  │  │  │  ├─ services_private_frozen.php
│        │  │  │  │  ├─ services_private_in_expression.php
│        │  │  │  │  ├─ services_query_string_env.php
│        │  │  │  │  ├─ services_rot13_env.php
│        │  │  │  │  ├─ services_service_locator_argument.php
│        │  │  │  │  ├─ services_subscriber.php
│        │  │  │  │  ├─ services_tsantos.php
│        │  │  │  │  ├─ services_uninitialized_ref.php
│        │  │  │  │  ├─ services_unsupported_characters.php
│        │  │  │  │  ├─ services_url_env.php
│        │  │  │  │  ├─ services_wither.php
│        │  │  │  │  ├─ services_wither_annotation.php
│        │  │  │  │  ├─ services_wither_lazy.php
│        │  │  │  │  ├─ services_wither_lazy_non_shared.php
│        │  │  │  │  ├─ services_wither_staticreturntype.php
│        │  │  │  │  ├─ simple.php
│        │  │  │  │  └─ static_constructor.php
│        │  │  │  ├─ Preload
│        │  │  │  │  ├─ A.php
│        │  │  │  │  ├─ B.php
│        │  │  │  │  ├─ C.php
│        │  │  │  │  ├─ D.php
│        │  │  │  │  ├─ Dummy.php
│        │  │  │  │  ├─ DummyWithInterface.php
│        │  │  │  │  ├─ E.php
│        │  │  │  │  ├─ F.php
│        │  │  │  │  ├─ G.php
│        │  │  │  │  ├─ IntersectionDummy.php
│        │  │  │  │  └─ UnionDummy.php
│        │  │  │  ├─ Prototype
│        │  │  │  │  ├─ BadAttributes
│        │  │  │  │  │  └─ WhenNotWhenFoo.php
│        │  │  │  │  ├─ BadClasses
│        │  │  │  │  │  └─ MissingParent.php
│        │  │  │  │  ├─ Foo.php
│        │  │  │  │  ├─ FooInterface.php
│        │  │  │  │  ├─ NotFoo.php
│        │  │  │  │  ├─ OtherDir
│        │  │  │  │  │  ├─ AnotherSub
│        │  │  │  │  │  │  └─ DeeperBaz.php
│        │  │  │  │  │  ├─ Baz.php
│        │  │  │  │  │  ├─ Component1
│        │  │  │  │  │  │  ├─ Dir1
│        │  │  │  │  │  │  │  └─ Service1.php
│        │  │  │  │  │  │  └─ Dir2
│        │  │  │  │  │  │     └─ Service2.php
│        │  │  │  │  │  └─ Component2
│        │  │  │  │  │     ├─ Dir1
│        │  │  │  │  │     │  └─ Service4.php
│        │  │  │  │  │     └─ Dir2
│        │  │  │  │  │        └─ Service5.php
│        │  │  │  │  ├─ SinglyImplementedInterface
│        │  │  │  │  │  ├─ Adapter
│        │  │  │  │  │  │  └─ Adapter.php
│        │  │  │  │  │  ├─ AnotherAdapter
│        │  │  │  │  │  │  └─ Adapter.php
│        │  │  │  │  │  └─ Port
│        │  │  │  │  │     └─ PortInterface.php
│        │  │  │  │  ├─ StaticConstructor
│        │  │  │  │  │  ├─ PrototypeStaticConstructor.php
│        │  │  │  │  │  ├─ PrototypeStaticConstructorAsArgument.php
│        │  │  │  │  │  └─ PrototypeStaticConstructorInterface.php
│        │  │  │  │  └─ Sub
│        │  │  │  │     ├─ Bar.php
│        │  │  │  │     └─ BarInterface.php
│        │  │  │  ├─ PrototypeAsAlias
│        │  │  │  │  ├─ AliasBarInterface.php
│        │  │  │  │  ├─ AliasFooInterface.php
│        │  │  │  │  ├─ WithAsAlias.php
│        │  │  │  │  ├─ WithAsAliasBothEnv.php
│        │  │  │  │  ├─ WithAsAliasDevEnv.php
│        │  │  │  │  ├─ WithAsAliasDuplicate.php
│        │  │  │  │  ├─ WithAsAliasIdMultipleInterface.php
│        │  │  │  │  ├─ WithAsAliasInterface.php
│        │  │  │  │  ├─ WithAsAliasMultiple.php
│        │  │  │  │  ├─ WithAsAliasMultipleInterface.php
│        │  │  │  │  └─ WithAsAliasProdEnv.php
│        │  │  │  ├─ ReadOnlyClass.php
│        │  │  │  ├─ RemoteCaller.php
│        │  │  │  ├─ RemoteCallerHttp.php
│        │  │  │  ├─ RemoteCallerSocket.php
│        │  │  │  ├─ ScalarFactory.php
│        │  │  │  ├─ SimilarArgumentsDummy.php
│        │  │  │  ├─ StaticConstructorAutoconfigure.php
│        │  │  │  ├─ StaticMethodTag.php
│        │  │  │  ├─ StdClassDecorator.php
│        │  │  │  ├─ StringBackedEnum.php
│        │  │  │  ├─ StubbedTranslator.php
│        │  │  │  ├─ TaggedConsumerWithExclude.php
│        │  │  │  ├─ TaggedIteratorConsumer.php
│        │  │  │  ├─ TaggedIteratorConsumerWithDefaultIndexMethod.php
│        │  │  │  ├─ TaggedIteratorConsumerWithDefaultIndexMethodAndWithDefaultPriorityMethod.php
│        │  │  │  ├─ TaggedIteratorConsumerWithDefaultPriorityMethod.php
│        │  │  │  ├─ TaggedLocatorConsumer.php
│        │  │  │  ├─ TaggedLocatorConsumerConsumer.php
│        │  │  │  ├─ TaggedLocatorConsumerFactory.php
│        │  │  │  ├─ TaggedLocatorConsumerWithDefaultIndexMethod.php
│        │  │  │  ├─ TaggedLocatorConsumerWithDefaultIndexMethodAndWithDefaultPriorityMethod.php
│        │  │  │  ├─ TaggedLocatorConsumerWithDefaultPriorityMethod.php
│        │  │  │  ├─ TaggedLocatorConsumerWithoutIndex.php
│        │  │  │  ├─ TaggedLocatorConsumerWithServiceSubscriber.php
│        │  │  │  ├─ TaggedService1.php
│        │  │  │  ├─ TaggedService2.php
│        │  │  │  ├─ TaggedService3.php
│        │  │  │  ├─ TaggedService3Configurator.php
│        │  │  │  ├─ TaggedService4.php
│        │  │  │  ├─ TaggedService5.php
│        │  │  │  ├─ TestDefinition1.php
│        │  │  │  ├─ TestDefinition2.php
│        │  │  │  ├─ TestDefinition3.php
│        │  │  │  ├─ TestServiceMethodsSubscriberTrait.php
│        │  │  │  ├─ TestServiceSubscriber.php
│        │  │  │  ├─ TestServiceSubscriberChild.php
│        │  │  │  ├─ TestServiceSubscriberIntersection.php
│        │  │  │  ├─ TestServiceSubscriberIntersectionWithTrait.php
│        │  │  │  ├─ TestServiceSubscriberParent.php
│        │  │  │  ├─ TestServiceSubscriberUnion.php
│        │  │  │  ├─ TestServiceSubscriberUnionWithTrait.php
│        │  │  │  ├─ Utils
│        │  │  │  │  └─ NotAService.php
│        │  │  │  ├─ WitherStaticReturnType.php
│        │  │  │  ├─ WithTarget.php
│        │  │  │  ├─ WithTargetAnonymous.php
│        │  │  │  ├─ xml
│        │  │  │  │  ├─ bindings_and_inner_collections.xml
│        │  │  │  │  ├─ class_from_id.xml
│        │  │  │  │  ├─ closure.xml
│        │  │  │  │  ├─ defaults_bindings.xml
│        │  │  │  │  ├─ defaults_bindings2.xml
│        │  │  │  │  ├─ deprecated_alias_definitions.xml
│        │  │  │  │  ├─ extension1
│        │  │  │  │  │  └─ services.xml
│        │  │  │  │  ├─ extension2
│        │  │  │  │  │  └─ services.xml
│        │  │  │  │  ├─ extensions
│        │  │  │  │  │  ├─ services1.xml
│        │  │  │  │  │  ├─ services2.xml
│        │  │  │  │  │  ├─ services3.xml
│        │  │  │  │  │  ├─ services4.xml
│        │  │  │  │  │  ├─ services5.xml
│        │  │  │  │  │  ├─ services6.xml
│        │  │  │  │  │  └─ services7.xml
│        │  │  │  │  ├─ from_callable.xml
│        │  │  │  │  ├─ invalid_alias_definition.xml
│        │  │  │  │  ├─ key_type_argument.xml
│        │  │  │  │  ├─ key_type_incorrect_bin.xml
│        │  │  │  │  ├─ key_type_property.xml
│        │  │  │  │  ├─ key_type_wrong_constant.xml
│        │  │  │  │  ├─ namespaces.xml
│        │  │  │  │  ├─ nested_service_without_id.xml
│        │  │  │  │  ├─ nonvalid.xml
│        │  │  │  │  ├─ not_singly_implemented_interface_in_multiple_resources.xml
│        │  │  │  │  ├─ not_singly_implemented_interface_in_multiple_resources_with_previously_registered_alias.xml
│        │  │  │  │  ├─ not_singly_implemented_interface_in_multiple_resources_with_previously_registered_alias2.xml
│        │  │  │  │  ├─ returns_clone.xml
│        │  │  │  │  ├─ services1.xml
│        │  │  │  │  ├─ services10.xml
│        │  │  │  │  ├─ services13.xml
│        │  │  │  │  ├─ services14.xml
│        │  │  │  │  ├─ services2.xml
│        │  │  │  │  ├─ services21.xml
│        │  │  │  │  ├─ services23.xml
│        │  │  │  │  ├─ services24.xml
│        │  │  │  │  ├─ services28.xml
│        │  │  │  │  ├─ services29.xml
│        │  │  │  │  ├─ services3.xml
│        │  │  │  │  ├─ services30.xml
│        │  │  │  │  ├─ services4.xml
│        │  │  │  │  ├─ services4_bad_import.xml
│        │  │  │  │  ├─ services4_bad_import_file_not_found.xml
│        │  │  │  │  ├─ services4_bad_import_nonvalid.xml
│        │  │  │  │  ├─ services4_bad_import_with_errors.xml
│        │  │  │  │  ├─ services5.xml
│        │  │  │  │  ├─ services6.xml
│        │  │  │  │  ├─ services7.xml
│        │  │  │  │  ├─ services8.xml
│        │  │  │  │  ├─ services9.xml
│        │  │  │  │  ├─ services_abstract.xml
│        │  │  │  │  ├─ services_autoconfigure.xml
│        │  │  │  │  ├─ services_autoconfigure_with_parent.xml
│        │  │  │  │  ├─ services_bindings.xml
│        │  │  │  │  ├─ services_case.xml
│        │  │  │  │  ├─ services_defaults_with_parent.xml
│        │  │  │  │  ├─ services_deprecated.xml
│        │  │  │  │  ├─ services_dump_load.xml
│        │  │  │  │  ├─ services_inline_not_candidate.xml
│        │  │  │  │  ├─ services_instanceof.xml
│        │  │  │  │  ├─ services_instanceof_with_parent.xml
│        │  │  │  │  ├─ services_lazy_fqcn.xml
│        │  │  │  │  ├─ services_named_args.xml
│        │  │  │  │  ├─ services_prototype.xml
│        │  │  │  │  ├─ services_prototype_array.xml
│        │  │  │  │  ├─ services_prototype_array_with_empty_node.xml
│        │  │  │  │  ├─ services_prototype_array_with_space_node.xml
│        │  │  │  │  ├─ services_prototype_constructor.xml
│        │  │  │  │  ├─ services_tsantos.xml
│        │  │  │  │  ├─ services_without_id.xml
│        │  │  │  │  ├─ services_with_abstract_argument.xml
│        │  │  │  │  ├─ services_with_array_tags.xml
│        │  │  │  │  ├─ services_with_default_array.xml
│        │  │  │  │  ├─ services_with_default_enumeration.xml
│        │  │  │  │  ├─ services_with_default_object.xml
│        │  │  │  │  ├─ services_with_deprecated_tagged.xml
│        │  │  │  │  ├─ services_with_enumeration.xml
│        │  │  │  │  ├─ services_with_invalid_enumeration.xml
│        │  │  │  │  ├─ services_with_service_closure.xml
│        │  │  │  │  ├─ services_with_service_locator_argument.xml
│        │  │  │  │  ├─ services_with_tagged_arguments.xml
│        │  │  │  │  ├─ service_with_abstract_argument.xml
│        │  │  │  │  ├─ singly_implemented_interface_in_multiple_resources.xml
│        │  │  │  │  ├─ stack.xml
│        │  │  │  │  ├─ static_constructor.xml
│        │  │  │  │  ├─ static_constructor_and_factory.xml
│        │  │  │  │  ├─ tag_without_name.xml
│        │  │  │  │  ├─ tag_with_empty_name.xml
│        │  │  │  │  ├─ tag_with_name_attribute.xml
│        │  │  │  │  ├─ when-env-services.xml
│        │  │  │  │  ├─ when-env.xml
│        │  │  │  │  ├─ withdoctype.xml
│        │  │  │  │  ├─ with_key_outside_collection.xml
│        │  │  │  │  └─ xml_with_wrong_ext.php
│        │  │  │  └─ yaml
│        │  │  │     ├─ alt_call.yaml
│        │  │  │     ├─ anonymous_services.yml
│        │  │  │     ├─ anonymous_services_alias.yml
│        │  │  │     ├─ anonymous_services_in_instanceof.yml
│        │  │  │     ├─ anonymous_services_in_parameters.yml
│        │  │  │     ├─ badtag1.yml
│        │  │  │     ├─ badtag2.yml
│        │  │  │     ├─ bad_alias.yml
│        │  │  │     ├─ bad_calls.yml
│        │  │  │     ├─ bad_decorates.yml
│        │  │  │     ├─ bad_decoration_on_invalid_null.yml
│        │  │  │     ├─ bad_empty_defaults.yml
│        │  │  │     ├─ bad_empty_instanceof.yml
│        │  │  │     ├─ bad_factory_syntax.yml
│        │  │  │     ├─ bad_format.yml
│        │  │  │     ├─ bad_import.yml
│        │  │  │     ├─ bad_imports.yml
│        │  │  │     ├─ bad_keyword.yml
│        │  │  │     ├─ bad_parameters.yml
│        │  │  │     ├─ bad_parent.yml
│        │  │  │     ├─ bad_service.yml
│        │  │  │     ├─ bad_services.yml
│        │  │  │     ├─ bar
│        │  │  │     │  └─ services.yml
│        │  │  │     ├─ class_from_id.yml
│        │  │  │     ├─ closure.yml
│        │  │  │     ├─ constructor_with_factory.yml
│        │  │  │     ├─ defaults_bindings.yml
│        │  │  │     ├─ defaults_bindings2.yml
│        │  │  │     ├─ deprecated_alias_definitions.yml
│        │  │  │     ├─ deprecated_alias_definitions_without_package_and_version.yml
│        │  │  │     ├─ deprecated_definition_without_message.yml
│        │  │  │     ├─ foo
│        │  │  │     │  └─ services.yml
│        │  │  │     ├─ from_callable.yml
│        │  │  │     ├─ integration
│        │  │  │     │  ├─ autoconfigure_child_not_applied
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  ├─ main.yml
│        │  │  │     │  │  └─ _child.yml
│        │  │  │     │  ├─ autoconfigure_parent_child
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  ├─ main.yml
│        │  │  │     │  │  └─ _child.yml
│        │  │  │     │  ├─ autoconfigure_parent_child_tags
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  ├─ main.yml
│        │  │  │     │  │  └─ _child.yml
│        │  │  │     │  ├─ child_parent
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  └─ main.yml
│        │  │  │     │  ├─ defaults_child_tags
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  └─ main.yml
│        │  │  │     │  ├─ defaults_instanceof_importance
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  └─ main.yml
│        │  │  │     │  ├─ defaults_parent_child
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  ├─ main.yml
│        │  │  │     │  │  └─ _child.yml
│        │  │  │     │  ├─ instanceof_and_calls
│        │  │  │     │  │  ├─ expected.yml
│        │  │  │     │  │  └─ main.yml
│        │  │  │     │  └─ instanceof_parent_child
│        │  │  │     │     ├─ expected.yml
│        │  │  │     │     ├─ main.yml
│        │  │  │     │     └─ _child.yml
│        │  │  │     ├─ nonvalid1.yml
│        │  │  │     ├─ nonvalid2.yml
│        │  │  │     ├─ not_singly_implemented_interface_in_multiple_resources.yml
│        │  │  │     ├─ not_singly_implemented_interface_in_multiple_resources_with_previously_registered_alias.yml
│        │  │  │     ├─ not_singly_implemented_interface_in_multiple_resources_with_previously_registered_alias2.yml
│        │  │  │     ├─ null_config.yml
│        │  │  │     ├─ returns_clone.yaml
│        │  │  │     ├─ services1.yml
│        │  │  │     ├─ services10.yml
│        │  │  │     ├─ services11.yml
│        │  │  │     ├─ services13.yml
│        │  │  │     ├─ services14.yml
│        │  │  │     ├─ services2.yml
│        │  │  │     ├─ services21.yml
│        │  │  │     ├─ services23.yml
│        │  │  │     ├─ services24.yml
│        │  │  │     ├─ services26.yml
│        │  │  │     ├─ services28.yml
│        │  │  │     ├─ services29.yml
│        │  │  │     ├─ services3.yml
│        │  │  │     ├─ services30.yml
│        │  │  │     ├─ services31_invalid_tags.yml
│        │  │  │     ├─ services34.yml
│        │  │  │     ├─ services4.yml
│        │  │  │     ├─ services4_bad_import.yml
│        │  │  │     ├─ services4_bad_import_file_not_found.yml
│        │  │  │     ├─ services4_bad_import_nonvalid.yml
│        │  │  │     ├─ services4_bad_import_with_errors.yml
│        │  │  │     ├─ services6.yml
│        │  │  │     ├─ services7.yml
│        │  │  │     ├─ services8.yml
│        │  │  │     ├─ services9.yml
│        │  │  │     ├─ services_adawson.yml
│        │  │  │     ├─ services_autoconfigure.yml
│        │  │  │     ├─ services_autoconfigure_with_parent.yml
│        │  │  │     ├─ services_bindings.yml
│        │  │  │     ├─ services_case.yml
│        │  │  │     ├─ services_configurator_short_syntax.yml
│        │  │  │     ├─ services_deep_graph.yml
│        │  │  │     ├─ services_defaults_with_parent.yml
│        │  │  │     ├─ services_dump_load.yml
│        │  │  │     ├─ services_inline.yml
│        │  │  │     ├─ services_instanceof.yml
│        │  │  │     ├─ services_instanceof_with_parent.yml
│        │  │  │     ├─ services_lazy_fqcn.yml
│        │  │  │     ├─ services_named_args.yml
│        │  │  │     ├─ services_not_existing.yml
│        │  │  │     ├─ services_prototype.yml
│        │  │  │     ├─ services_prototype_namespace.yml
│        │  │  │     ├─ services_prototype_namespace_without_resource.yml
│        │  │  │     ├─ services_prototype_with_empty_node.yml
│        │  │  │     ├─ services_prototype_with_null_node.yml
│        │  │  │     ├─ services_short_syntax.yml
│        │  │  │     ├─ services_underscore.yml
│        │  │  │     ├─ services_with_abstract_argument.yml
│        │  │  │     ├─ services_with_array_tags.yml
│        │  │  │     ├─ services_with_default_array.yml
│        │  │  │     ├─ services_with_default_enumeration.yml
│        │  │  │     ├─ services_with_default_object.yml
│        │  │  │     ├─ services_with_enumeration.yml
│        │  │  │     ├─ services_with_enumeration_enum_tag.yml
│        │  │  │     ├─ services_with_invalid_enumeration.yml
│        │  │  │     ├─ services_with_service_closure.yml
│        │  │  │     ├─ services_with_service_locator_argument.yml
│        │  │  │     ├─ services_with_short_service_closure.yml
│        │  │  │     ├─ services_with_tagged_argument.yml
│        │  │  │     ├─ service_instanceof_factory.yml
│        │  │  │     ├─ singly_implemented_interface_in_multiple_resources.yml
│        │  │  │     ├─ stack.yaml
│        │  │  │     ├─ static_constructor.yml
│        │  │  │     ├─ tagged_deprecated.yml
│        │  │  │     ├─ tagged_iterator_optional.yml
│        │  │  │     ├─ tag_array_arguments.yml
│        │  │  │     ├─ tag_name_empty_string.yml
│        │  │  │     ├─ tag_name_no_string.yml
│        │  │  │     ├─ tag_name_only.yml
│        │  │  │     ├─ when-env.yaml
│        │  │  │     └─ yaml_with_wrong_ext.ini
│        │  │  ├─ LazyProxy
│        │  │  │  ├─ Instantiator
│        │  │  │  │  └─ RealServiceInstantiatorTest.php
│        │  │  │  └─ PhpDumper
│        │  │  │     ├─ LazyServiceDumperTest.php
│        │  │  │     └─ NullDumperTest.php
│        │  │  ├─ Loader
│        │  │  │  ├─ ClosureLoaderTest.php
│        │  │  │  ├─ Configurator
│        │  │  │  │  └─ EnvConfiguratorTest.php
│        │  │  │  ├─ DirectoryLoaderTest.php
│        │  │  │  ├─ FileLoaderTest.php
│        │  │  │  ├─ GlobFileLoaderTest.php
│        │  │  │  ├─ IniFileLoaderTest.php
│        │  │  │  ├─ LoaderResolverTest.php
│        │  │  │  ├─ PhpFileLoaderTest.php
│        │  │  │  ├─ XmlFileLoaderTest.php
│        │  │  │  └─ YamlFileLoaderTest.php
│        │  │  ├─ ParameterBag
│        │  │  │  ├─ ContainerBagTest.php
│        │  │  │  ├─ EnvPlaceholderParameterBagTest.php
│        │  │  │  ├─ FrozenParameterBagTest.php
│        │  │  │  └─ ParameterBagTest.php
│        │  │  ├─ ParameterTest.php
│        │  │  ├─ ReferenceTest.php
│        │  │  ├─ ServiceLocatorTest.php
│        │  │  └─ StaticEnvVarLoaderTest.php
│        │  ├─ TypedReference.php
│        │  └─ Variable.php
│        ├─ deprecation-contracts
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ function.php
│        │  ├─ LICENSE
│        │  └─ README.md
│        ├─ dotenv
│        │  ├─ CHANGELOG.md
│        │  ├─ Command
│        │  │  ├─ DebugCommand.php
│        │  │  └─ DotenvDumpCommand.php
│        │  ├─ composer.json
│        │  ├─ Dotenv.php
│        │  ├─ Exception
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ FormatException.php
│        │  │  ├─ FormatExceptionContext.php
│        │  │  └─ PathException.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  └─ Tests
│        │     ├─ Command
│        │     │  ├─ DebugCommandTest.php
│        │     │  ├─ DotenvDumpCommandTest.php
│        │     │  └─ Fixtures
│        │     │     ├─ Scenario1
│        │     │     │  ├─ .env
│        │     │     │  ├─ .env.local
│        │     │     │  ├─ .env.prod.local
│        │     │     │  └─ .env.test
│        │     │     ├─ Scenario2
│        │     │     │  ├─ .env.dist
│        │     │     │  ├─ .env.local.php
│        │     │     │  └─ .env.prod
│        │     │     └─ Scenario3
│        │     │        ├─ .env
│        │     │        └─ .env.dist
│        │     ├─ DotenvTest.php
│        │     └─ fixtures
│        │        └─ file_with_bom
│        ├─ error-handler
│        │  ├─ BufferingLogger.php
│        │  ├─ CHANGELOG.md
│        │  ├─ Command
│        │  │  └─ ErrorDumpCommand.php
│        │  ├─ composer.json
│        │  ├─ Debug.php
│        │  ├─ DebugClassLoader.php
│        │  ├─ Error
│        │  │  ├─ ClassNotFoundError.php
│        │  │  ├─ FatalError.php
│        │  │  ├─ OutOfMemoryError.php
│        │  │  ├─ UndefinedFunctionError.php
│        │  │  └─ UndefinedMethodError.php
│        │  ├─ ErrorEnhancer
│        │  │  ├─ ClassNotFoundErrorEnhancer.php
│        │  │  ├─ ErrorEnhancerInterface.php
│        │  │  ├─ UndefinedFunctionErrorEnhancer.php
│        │  │  └─ UndefinedMethodErrorEnhancer.php
│        │  ├─ ErrorHandler.php
│        │  ├─ ErrorRenderer
│        │  │  ├─ CliErrorRenderer.php
│        │  │  ├─ ErrorRendererInterface.php
│        │  │  ├─ FileLinkFormatter.php
│        │  │  ├─ HtmlErrorRenderer.php
│        │  │  └─ SerializerErrorRenderer.php
│        │  ├─ Exception
│        │  │  ├─ FlattenException.php
│        │  │  └─ SilencedErrorContext.php
│        │  ├─ Internal
│        │  │  └─ TentativeTypes.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Resources
│        │  │  ├─ assets
│        │  │  │  ├─ css
│        │  │  │  │  ├─ error.css
│        │  │  │  │  ├─ exception.css
│        │  │  │  │  └─ exception_full.css
│        │  │  │  ├─ images
│        │  │  │  │  ├─ chevron-right.svg
│        │  │  │  │  ├─ favicon.png.base64
│        │  │  │  │  ├─ icon-book.svg
│        │  │  │  │  ├─ icon-copy.svg
│        │  │  │  │  ├─ icon-minus-square-o.svg
│        │  │  │  │  ├─ icon-minus-square.svg
│        │  │  │  │  ├─ icon-plus-square-o.svg
│        │  │  │  │  ├─ icon-plus-square.svg
│        │  │  │  │  ├─ icon-support.svg
│        │  │  │  │  ├─ symfony-ghost.svg.php
│        │  │  │  │  └─ symfony-logo.svg
│        │  │  │  └─ js
│        │  │  │     └─ exception.js
│        │  │  ├─ bin
│        │  │  │  ├─ extract-tentative-return-types.php
│        │  │  │  └─ patch-type-declarations
│        │  │  └─ views
│        │  │     ├─ error.html.php
│        │  │     ├─ exception.html.php
│        │  │     ├─ exception_full.html.php
│        │  │     ├─ logs.html.php
│        │  │     ├─ trace.html.php
│        │  │     ├─ traces.html.php
│        │  │     └─ traces_text.html.php
│        │  ├─ Tests
│        │  │  ├─ Command
│        │  │  │  └─ ErrorDumpCommandTest.php
│        │  │  ├─ DebugClassLoaderTest.php
│        │  │  ├─ ErrorEnhancer
│        │  │  │  ├─ ClassNotFoundErrorEnhancerTest.php
│        │  │  │  ├─ UndefinedFunctionErrorEnhancerTest.php
│        │  │  │  └─ UndefinedMethodErrorEnhancerTest.php
│        │  │  ├─ ErrorHandlerTest.php
│        │  │  ├─ ErrorRenderer
│        │  │  │  ├─ FileLinkFormatterTest.php
│        │  │  │  ├─ HtmlErrorRendererTest.php
│        │  │  │  └─ SerializerErrorRendererTest.php
│        │  │  ├─ Exception
│        │  │  │  └─ FlattenExceptionTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ AnnotatedClass.php
│        │  │  │  ├─ casemismatch.php
│        │  │  │  ├─ ClassAlias.php
│        │  │  │  ├─ ClassWithAnnotatedParameters.php
│        │  │  │  ├─ DefinitionInEvaluatedCode.php
│        │  │  │  ├─ DeprecatedClass.php
│        │  │  │  ├─ DeprecatedInterface.php
│        │  │  │  ├─ ErrorHandlerThatUsesThePreviousOne.php
│        │  │  │  ├─ ExtendedFinalMethod.php
│        │  │  │  ├─ FinalClasses.php
│        │  │  │  ├─ FinalConstant
│        │  │  │  │  ├─ FinalConstants.php
│        │  │  │  │  ├─ FinalConstants2.php
│        │  │  │  │  ├─ FinalConstantsInterface.php
│        │  │  │  │  ├─ FinalConstantsInterface2.php
│        │  │  │  │  ├─ OverrideFinalConstant.php
│        │  │  │  │  └─ OverrideFinalConstant81.php
│        │  │  │  ├─ FinalMethod.php
│        │  │  │  ├─ FinalMethod2Trait.php
│        │  │  │  ├─ FinalProperty
│        │  │  │  │  ├─ FinalProperty.php
│        │  │  │  │  ├─ OutsideFinalProperty.php
│        │  │  │  │  └─ OverrideFinalPropertySameNamespace.php
│        │  │  │  ├─ InterfaceWithAnnotatedParameters.php
│        │  │  │  ├─ InternalClass.php
│        │  │  │  ├─ InternalInterface.php
│        │  │  │  ├─ InternalTrait.php
│        │  │  │  ├─ InternalTrait2.php
│        │  │  │  ├─ LoggerThatSetAnErrorHandler.php
│        │  │  │  ├─ NonDeprecatedInterface.php
│        │  │  │  ├─ notPsr0Bis.php
│        │  │  │  ├─ OutsideInterface.php
│        │  │  │  ├─ OverrideFinalProperty.php
│        │  │  │  ├─ OverrideOutsideFinalProperty.php
│        │  │  │  ├─ PEARClass.php
│        │  │  │  ├─ pixel.png
│        │  │  │  ├─ psr4
│        │  │  │  │  └─ Psr4CaseMismatch.php
│        │  │  │  ├─ reallyNotPsr0.php
│        │  │  │  ├─ ReturnType.php
│        │  │  │  ├─ ReturnTypeGrandParent.php
│        │  │  │  ├─ ReturnTypeInterface.php
│        │  │  │  ├─ ReturnTypeParent.php
│        │  │  │  ├─ ReturnTypeParentInterface.php
│        │  │  │  ├─ ReturnTypeParentPhp83.php
│        │  │  │  ├─ ReturnTypePhp83.php
│        │  │  │  ├─ StringErrorCodeException.php
│        │  │  │  ├─ SubClassWithAnnotatedParameters.php
│        │  │  │  ├─ Throwing.php
│        │  │  │  ├─ TraitWithAnnotatedParameters.php
│        │  │  │  ├─ TraitWithInternalMethod.php
│        │  │  │  ├─ VirtualClass.php
│        │  │  │  ├─ VirtualClassMagicCall.php
│        │  │  │  ├─ VirtualInterface.php
│        │  │  │  ├─ VirtualSubInterface.php
│        │  │  │  └─ VirtualTrait.php
│        │  │  ├─ Fixtures2
│        │  │  │  └─ RequiredTwice.php
│        │  │  ├─ HeaderMock.php
│        │  │  └─ phpt
│        │  │     ├─ debug_class_loader.phpt
│        │  │     ├─ decorate_exception_handler.phpt
│        │  │     ├─ exception_rethrown.phpt
│        │  │     └─ fatal_with_nested_handlers.phpt
│        │  └─ ThrowableUtils.php
│        ├─ event-dispatcher
│        │  ├─ Attribute
│        │  │  └─ AsEventListener.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ Debug
│        │  │  ├─ TraceableEventDispatcher.php
│        │  │  └─ WrappedListener.php
│        │  ├─ DependencyInjection
│        │  │  ├─ AddEventAliasesPass.php
│        │  │  └─ RegisterListenersPass.php
│        │  ├─ EventDispatcher.php
│        │  ├─ EventDispatcherInterface.php
│        │  ├─ EventSubscriberInterface.php
│        │  ├─ GenericEvent.php
│        │  ├─ ImmutableEventDispatcher.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  └─ Tests
│        │     ├─ ChildEventDispatcherTest.php
│        │     ├─ Debug
│        │     │  ├─ TraceableEventDispatcherTest.php
│        │     │  └─ WrappedListenerTest.php
│        │     ├─ DependencyInjection
│        │     │  └─ RegisterListenersPassTest.php
│        │     ├─ EventDispatcherTest.php
│        │     ├─ Fixtures
│        │     │  ├─ CustomEvent.php
│        │     │  ├─ TaggedInvokableListener.php
│        │     │  └─ TaggedMultiListener.php
│        │     ├─ GenericEventTest.php
│        │     └─ ImmutableEventDispatcherTest.php
│        ├─ event-dispatcher-contracts
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ Event.php
│        │  ├─ EventDispatcherInterface.php
│        │  ├─ LICENSE
│        │  └─ README.md
│        ├─ filesystem
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ Exception
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ FileNotFoundException.php
│        │  │  ├─ InvalidArgumentException.php
│        │  │  ├─ IOException.php
│        │  │  ├─ IOExceptionInterface.php
│        │  │  └─ RuntimeException.php
│        │  ├─ Filesystem.php
│        │  ├─ LICENSE
│        │  ├─ Path.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  └─ Tests
│        │     ├─ ExceptionTest.php
│        │     ├─ FilesystemTest.php
│        │     ├─ FilesystemTestCase.php
│        │     ├─ Fixtures
│        │     │  ├─ MockStream
│        │     │  │  └─ MockStream.php
│        │     │  └─ web
│        │     │     ├─ index.php
│        │     │     └─ logo_symfony_header.png
│        │     └─ PathTest.php
│        ├─ finder
│        │  ├─ CHANGELOG.md
│        │  ├─ Comparator
│        │  │  ├─ Comparator.php
│        │  │  ├─ DateComparator.php
│        │  │  └─ NumberComparator.php
│        │  ├─ composer.json
│        │  ├─ Exception
│        │  │  ├─ AccessDeniedException.php
│        │  │  └─ DirectoryNotFoundException.php
│        │  ├─ Finder.php
│        │  ├─ Gitignore.php
│        │  ├─ Glob.php
│        │  ├─ Iterator
│        │  │  ├─ CustomFilterIterator.php
│        │  │  ├─ DateRangeFilterIterator.php
│        │  │  ├─ DepthRangeFilterIterator.php
│        │  │  ├─ ExcludeDirectoryFilterIterator.php
│        │  │  ├─ FilecontentFilterIterator.php
│        │  │  ├─ FilenameFilterIterator.php
│        │  │  ├─ FileTypeFilterIterator.php
│        │  │  ├─ LazyIterator.php
│        │  │  ├─ MultiplePcreFilterIterator.php
│        │  │  ├─ PathFilterIterator.php
│        │  │  ├─ RecursiveDirectoryIterator.php
│        │  │  ├─ SizeRangeFilterIterator.php
│        │  │  ├─ SortableIterator.php
│        │  │  └─ VcsIgnoredFilterIterator.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ SplFileInfo.php
│        │  └─ Tests
│        │     ├─ Comparator
│        │     │  ├─ ComparatorTest.php
│        │     │  ├─ DateComparatorTest.php
│        │     │  └─ NumberComparatorTest.php
│        │     ├─ FinderOpenBasedirTest.php
│        │     ├─ FinderTest.php
│        │     ├─ Fixtures
│        │     │  ├─ .dot
│        │     │  │  ├─ a
│        │     │  │  └─ b
│        │     │  │     ├─ c.neon
│        │     │  │     └─ d.neon
│        │     │  ├─ A
│        │     │  │  ├─ a.dat
│        │     │  │  └─ B
│        │     │  │     ├─ ab.dat
│        │     │  │     └─ C
│        │     │  │        └─ abc.dat
│        │     │  ├─ copy
│        │     │  │  └─ A
│        │     │  │     ├─ a.dat.copy
│        │     │  │     └─ B
│        │     │  │        ├─ ab.dat.copy
│        │     │  │        └─ C
│        │     │  │           └─ abc.dat.copy
│        │     │  ├─ dolor.txt
│        │     │  ├─ gitignore
│        │     │  │  ├─ git_root
│        │     │  │  │  └─ search_root
│        │     │  │  │     ├─ b.txt
│        │     │  │  │     └─ dir
│        │     │  │  │        └─ a.txt
│        │     │  │  └─ search_root
│        │     │  │     ├─ a.txt
│        │     │  │     ├─ b.txt
│        │     │  │     ├─ c.txt
│        │     │  │     └─ dir
│        │     │  │        ├─ a.txt
│        │     │  │        ├─ b.txt
│        │     │  │        └─ c.txt
│        │     │  ├─ ipsum.txt
│        │     │  ├─ lorem.txt
│        │     │  ├─ one
│        │     │  │  ├─ .dot
│        │     │  │  ├─ a
│        │     │  │  └─ b
│        │     │  │     ├─ c.neon
│        │     │  │     └─ d.neon
│        │     │  ├─ r+e.gex[c]a(r)s
│        │     │  │  └─ dir
│        │     │  │     └─ bar.dat
│        │     │  └─ with space
│        │     │     └─ foo.txt
│        │     ├─ GitignoreTest.php
│        │     ├─ GlobTest.php
│        │     └─ Iterator
│        │        ├─ CustomFilterIteratorTest.php
│        │        ├─ DateRangeFilterIteratorTest.php
│        │        ├─ DepthRangeFilterIteratorTest.php
│        │        ├─ ExcludeDirectoryFilterIteratorTest.php
│        │        ├─ FilecontentFilterIteratorTest.php
│        │        ├─ FilenameFilterIteratorTest.php
│        │        ├─ FileTypeFilterIteratorTest.php
│        │        ├─ InnerNameIterator.php
│        │        ├─ Iterator.php
│        │        ├─ IteratorTestCase.php
│        │        ├─ LazyIteratorTest.php
│        │        ├─ MockFileListIterator.php
│        │        ├─ MockSplFileInfo.php
│        │        ├─ MultiplePcreFilterIteratorTest.php
│        │        ├─ PathFilterIteratorTest.php
│        │        ├─ RealIteratorTestCase.php
│        │        ├─ RecursiveDirectoryIteratorTest.php
│        │        ├─ SizeRangeFilterIteratorTest.php
│        │        ├─ SortableIteratorTest.php
│        │        ├─ VcsIgnoredFilterIteratorTest.php
│        │        └─ VfsIteratorTestTrait.php
│        ├─ flex
│        │  ├─ .php-cs-fixer.dist.php
│        │  ├─ composer.json
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ src
│        │  │  ├─ Command
│        │  │  │  ├─ DumpEnvCommand.php
│        │  │  │  ├─ InstallRecipesCommand.php
│        │  │  │  ├─ RecipesCommand.php
│        │  │  │  └─ UpdateRecipesCommand.php
│        │  │  ├─ Configurator
│        │  │  │  ├─ AbstractConfigurator.php
│        │  │  │  ├─ AddLinesConfigurator.php
│        │  │  │  ├─ BundlesConfigurator.php
│        │  │  │  ├─ ComposerCommandsConfigurator.php
│        │  │  │  ├─ ComposerScriptsConfigurator.php
│        │  │  │  ├─ ContainerConfigurator.php
│        │  │  │  ├─ CopyFromPackageConfigurator.php
│        │  │  │  ├─ CopyFromRecipeConfigurator.php
│        │  │  │  ├─ DockerComposeConfigurator.php
│        │  │  │  ├─ DockerfileConfigurator.php
│        │  │  │  ├─ DotenvConfigurator.php
│        │  │  │  ├─ EnvConfigurator.php
│        │  │  │  ├─ GitignoreConfigurator.php
│        │  │  │  └─ MakefileConfigurator.php
│        │  │  ├─ Configurator.php
│        │  │  ├─ Downloader.php
│        │  │  ├─ Event
│        │  │  │  └─ UpdateEvent.php
│        │  │  ├─ Flex.php
│        │  │  ├─ GithubApi.php
│        │  │  ├─ InformationOperation.php
│        │  │  ├─ Lock.php
│        │  │  ├─ Options.php
│        │  │  ├─ PackageFilter.php
│        │  │  ├─ PackageJsonSynchronizer.php
│        │  │  ├─ PackageResolver.php
│        │  │  ├─ Path.php
│        │  │  ├─ Recipe.php
│        │  │  ├─ Response.php
│        │  │  ├─ ScriptExecutor.php
│        │  │  ├─ SymfonyBundle.php
│        │  │  ├─ SymfonyPackInstaller.php
│        │  │  ├─ Unpack
│        │  │  │  ├─ Operation.php
│        │  │  │  └─ Result.php
│        │  │  ├─ Unpacker.php
│        │  │  └─ Update
│        │  │     ├─ DiffHelper.php
│        │  │     ├─ RecipePatch.php
│        │  │     ├─ RecipePatcher.php
│        │  │     └─ RecipeUpdate.php
│        │  └─ tests
│        │     ├─ bootstrap.php
│        │     ├─ Command
│        │     │  ├─ DumpEnvCommandTest.php
│        │     │  ├─ InstallRecipesCommandTest.php
│        │     │  └─ UpdateRecipesCommandTest.php
│        │     ├─ Configurator
│        │     │  ├─ AddLinesConfiguratorTest.php
│        │     │  ├─ BundlesConfiguratorTest.php
│        │     │  ├─ ComposerCommandConfiguratorTest.php
│        │     │  ├─ ComposerScriptsConfiguratorTest.php
│        │     │  ├─ ContainerConfiguratorTest.php
│        │     │  ├─ CopyDirectoryFromPackageConfiguratorTest.php
│        │     │  ├─ CopyFromPackageConfiguratorTest.php
│        │     │  ├─ CopyFromRecipeConfiguratorTest.php
│        │     │  ├─ DockerComposeConfiguratorTest.php
│        │     │  ├─ DockerfileConfiguratorTest.php
│        │     │  ├─ DotenvConfiguratorTest.php
│        │     │  ├─ EnvConfiguratorTest.php
│        │     │  ├─ GitignoreConfiguratorTest.php
│        │     │  └─ MakefileConfiguratorTest.php
│        │     ├─ Fixtures
│        │     │  ├─ packageJson
│        │     │  │  ├─ assets
│        │     │  │  │  └─ controllers.json
│        │     │  │  ├─ elevated_dependencies_package.json
│        │     │  │  ├─ package.json
│        │     │  │  ├─ stricter_constraints_package.json
│        │     │  │  └─ vendor
│        │     │  │     └─ symfony
│        │     │  │        ├─ existing-package
│        │     │  │        │  └─ Resources
│        │     │  │        │     └─ assets
│        │     │  │        │        └─ package.json
│        │     │  │        ├─ importmap-invalid-constraint-package
│        │     │  │        │  └─ assets
│        │     │  │        │     └─ package.json
│        │     │  │        ├─ new-package
│        │     │  │        │  └─ assets
│        │     │  │        │     └─ package.json
│        │     │  │        └─ package-no-file-package
│        │     │  │           └─ assets
│        │     │  │              └─ package.json
│        │     │  ├─ phpunit.xml.dist
│        │     │  ├─ update_recipes
│        │     │  │  ├─ composer.json
│        │     │  │  ├─ console
│        │     │  │  └─ symfony.lock
│        │     │  └─ vendor
│        │     │     ├─ composer
│        │     │     │  └─ ca-bundle
│        │     │     │     └─ src
│        │     │     │        └─ CaBundle.php
│        │     │     ├─ doctrine
│        │     │     │  └─ doctrine-cache-bundle
│        │     │     │     └─ DoctrineCacheBundle.php
│        │     │     ├─ dunglas
│        │     │     │  └─ sylius-acme-plugin
│        │     │     │     └─ src
│        │     │     │        └─ DunglasSyliusAcmePlugin.php
│        │     │     ├─ easycorp
│        │     │     │  ├─ easy-deploy-bundle
│        │     │     │  │  └─ src
│        │     │     │  │     └─ EasyDeployBundle.php
│        │     │     │  └─ easy-security-bundle
│        │     │     │     └─ EasySecurityBundle.php
│        │     │     ├─ eightpoints
│        │     │     │  └─ guzzle-bundle
│        │     │     │     └─ EightPoints
│        │     │     │        └─ Bundle
│        │     │     │           └─ GuzzleBundle
│        │     │     │              └─ GuzzleBundle.php
│        │     │     ├─ sylius
│        │     │     │  └─ shop-api-plugin
│        │     │     │     └─ src
│        │     │     │        └─ ShopApiPlugin.php
│        │     │     ├─ symfony
│        │     │     │  ├─ debug-bundle
│        │     │     │  │  └─ DebugBundle.php
│        │     │     │  ├─ dummy
│        │     │     │  │  ├─ FirstDummyBundle
│        │     │     │  │  │  └─ FirstDummyBundle.php
│        │     │     │  │  └─ SecondDummyBundle
│        │     │     │  │     └─ SecondDummyBundle.php
│        │     │     │  └─ nouse-bundle
│        │     │     │     └─ NouseBundle.php
│        │     │     ├─ symfony-cmf
│        │     │     │  └─ routing-bundle
│        │     │     │     └─ CmfRoutingBundle.php
│        │     │     └─ web-token
│        │     │        └─ jwt-bundle
│        │     │           └─ JoseFrameworkBundle.php
│        │     ├─ FlexTest.php
│        │     ├─ OptionsTest.php
│        │     ├─ PackageFilterTest.php
│        │     ├─ PackageJsonSynchronizerTest.php
│        │     ├─ PackageResolverTest.php
│        │     ├─ PathTest.php
│        │     ├─ ScriptExecutorTest.php
│        │     ├─ SymfonyBundleTest.php
│        │     ├─ UnpackerTest.php
│        │     └─ Update
│        │        ├─ DiffHelperTest.php
│        │        ├─ RecipePatcherTest.php
│        │        ├─ RecipePatchTest.php
│        │        └─ RecipeUpdateTest.php
│        ├─ framework-bundle
│        │  ├─ CacheWarmer
│        │  │  ├─ AbstractPhpFileCacheWarmer.php
│        │  │  ├─ CachePoolClearerCacheWarmer.php
│        │  │  ├─ ConfigBuilderCacheWarmer.php
│        │  │  ├─ RouterCacheWarmer.php
│        │  │  ├─ SerializerCacheWarmer.php
│        │  │  ├─ TranslationsCacheWarmer.php
│        │  │  └─ ValidatorCacheWarmer.php
│        │  ├─ CHANGELOG.md
│        │  ├─ Command
│        │  │  ├─ AboutCommand.php
│        │  │  ├─ AbstractConfigCommand.php
│        │  │  ├─ AssetsInstallCommand.php
│        │  │  ├─ BuildDebugContainerTrait.php
│        │  │  ├─ CacheClearCommand.php
│        │  │  ├─ CachePoolClearCommand.php
│        │  │  ├─ CachePoolDeleteCommand.php
│        │  │  ├─ CachePoolInvalidateTagsCommand.php
│        │  │  ├─ CachePoolListCommand.php
│        │  │  ├─ CachePoolPruneCommand.php
│        │  │  ├─ CacheWarmupCommand.php
│        │  │  ├─ ConfigDebugCommand.php
│        │  │  ├─ ConfigDumpReferenceCommand.php
│        │  │  ├─ ContainerDebugCommand.php
│        │  │  ├─ ContainerLintCommand.php
│        │  │  ├─ DebugAutowiringCommand.php
│        │  │  ├─ EventDispatcherDebugCommand.php
│        │  │  ├─ RouterDebugCommand.php
│        │  │  ├─ RouterMatchCommand.php
│        │  │  ├─ SecretsDecryptToLocalCommand.php
│        │  │  ├─ SecretsEncryptFromLocalCommand.php
│        │  │  ├─ SecretsGenerateKeysCommand.php
│        │  │  ├─ SecretsListCommand.php
│        │  │  ├─ SecretsRemoveCommand.php
│        │  │  ├─ SecretsRevealCommand.php
│        │  │  ├─ SecretsSetCommand.php
│        │  │  ├─ TranslationDebugCommand.php
│        │  │  ├─ TranslationExtractCommand.php
│        │  │  ├─ TranslationUpdateCommand.php
│        │  │  ├─ WorkflowDumpCommand.php
│        │  │  ├─ XliffLintCommand.php
│        │  │  └─ YamlLintCommand.php
│        │  ├─ composer.json
│        │  ├─ Console
│        │  │  ├─ Application.php
│        │  │  ├─ Descriptor
│        │  │  │  ├─ Descriptor.php
│        │  │  │  ├─ JsonDescriptor.php
│        │  │  │  ├─ MarkdownDescriptor.php
│        │  │  │  ├─ TextDescriptor.php
│        │  │  │  └─ XmlDescriptor.php
│        │  │  └─ Helper
│        │  │     └─ DescriptorHelper.php
│        │  ├─ Controller
│        │  │  ├─ AbstractController.php
│        │  │  ├─ ControllerResolver.php
│        │  │  ├─ RedirectController.php
│        │  │  └─ TemplateController.php
│        │  ├─ DataCollector
│        │  │  ├─ AbstractDataCollector.php
│        │  │  ├─ RouterDataCollector.php
│        │  │  └─ TemplateAwareDataCollectorInterface.php
│        │  ├─ DependencyInjection
│        │  │  ├─ Compiler
│        │  │  │  ├─ AddDebugLogProcessorPass.php
│        │  │  │  ├─ AssetsContextPass.php
│        │  │  │  ├─ ContainerBuilderDebugDumpPass.php
│        │  │  │  ├─ ErrorLoggerCompilerPass.php
│        │  │  │  ├─ ProfilerPass.php
│        │  │  │  ├─ RemoveUnusedSessionMarshallingHandlerPass.php
│        │  │  │  ├─ TestServiceContainerRealRefPass.php
│        │  │  │  ├─ TestServiceContainerWeakRefPass.php
│        │  │  │  ├─ TranslationLintCommandPass.php
│        │  │  │  ├─ TranslationUpdateCommandPass.php
│        │  │  │  └─ UnusedTagsPass.php
│        │  │  ├─ Configuration.php
│        │  │  ├─ FrameworkExtension.php
│        │  │  └─ VirtualRequestStackPass.php
│        │  ├─ EventListener
│        │  │  ├─ ConsoleProfilerListener.php
│        │  │  └─ SuggestMissingPackageSubscriber.php
│        │  ├─ FrameworkBundle.php
│        │  ├─ HttpCache
│        │  │  └─ HttpCache.php
│        │  ├─ Kernel
│        │  │  └─ MicroKernelTrait.php
│        │  ├─ KernelBrowser.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Resources
│        │  │  ├─ bin
│        │  │  │  └─ check-unused-known-tags.php
│        │  │  └─ config
│        │  │     ├─ assets.php
│        │  │     ├─ asset_mapper.php
│        │  │     ├─ cache.php
│        │  │     ├─ cache_debug.php
│        │  │     ├─ collectors.php
│        │  │     ├─ console.php
│        │  │     ├─ debug.php
│        │  │     ├─ debug_prod.php
│        │  │     ├─ error_renderer.php
│        │  │     ├─ esi.php
│        │  │     ├─ form.php
│        │  │     ├─ form_csrf.php
│        │  │     ├─ form_debug.php
│        │  │     ├─ fragment_listener.php
│        │  │     ├─ fragment_renderer.php
│        │  │     ├─ html_sanitizer.php
│        │  │     ├─ http_client.php
│        │  │     ├─ http_client_debug.php
│        │  │     ├─ identity_translator.php
│        │  │     ├─ json_streamer.php
│        │  │     ├─ lock.php
│        │  │     ├─ mailer.php
│        │  │     ├─ mailer_debug.php
│        │  │     ├─ mailer_transports.php
│        │  │     ├─ mailer_webhook.php
│        │  │     ├─ messenger.php
│        │  │     ├─ messenger_debug.php
│        │  │     ├─ mime_type.php
│        │  │     ├─ notifier.php
│        │  │     ├─ notifier_debug.php
│        │  │     ├─ notifier_transports.php
│        │  │     ├─ notifier_webhook.php
│        │  │     ├─ object_mapper.php
│        │  │     ├─ process.php
│        │  │     ├─ profiling.php
│        │  │     ├─ property_access.php
│        │  │     ├─ property_info.php
│        │  │     ├─ rate_limiter.php
│        │  │     ├─ remote_event.php
│        │  │     ├─ request.php
│        │  │     ├─ routing
│        │  │     │  ├─ errors.php
│        │  │     │  ├─ errors.xml
│        │  │     │  ├─ webhook.php
│        │  │     │  └─ webhook.xml
│        │  │     ├─ routing.php
│        │  │     ├─ scheduler.php
│        │  │     ├─ schema
│        │  │     │  └─ symfony-1.0.xsd
│        │  │     ├─ secrets.php
│        │  │     ├─ security_csrf.php
│        │  │     ├─ semaphore.php
│        │  │     ├─ serializer.php
│        │  │     ├─ serializer_debug.php
│        │  │     ├─ services.php
│        │  │     ├─ session.php
│        │  │     ├─ ssi.php
│        │  │     ├─ test.php
│        │  │     ├─ translation.php
│        │  │     ├─ translation_debug.php
│        │  │     ├─ translation_providers.php
│        │  │     ├─ type_info.php
│        │  │     ├─ uid.php
│        │  │     ├─ validator.php
│        │  │     ├─ validator_debug.php
│        │  │     ├─ web.php
│        │  │     ├─ webhook.php
│        │  │     ├─ web_link.php
│        │  │     ├─ workflow.php
│        │  │     └─ workflow_debug.php
│        │  ├─ Routing
│        │  │  ├─ Attribute
│        │  │  │  └─ AsRoutingConditionService.php
│        │  │  ├─ AttributeRouteControllerLoader.php
│        │  │  ├─ DelegatingLoader.php
│        │  │  ├─ RedirectableCompiledUrlMatcher.php
│        │  │  ├─ RouteLoaderInterface.php
│        │  │  └─ Router.php
│        │  ├─ Secrets
│        │  │  ├─ AbstractVault.php
│        │  │  ├─ DotenvVault.php
│        │  │  └─ SodiumVault.php
│        │  ├─ Test
│        │  │  ├─ BrowserKitAssertionsTrait.php
│        │  │  ├─ DomCrawlerAssertionsTrait.php
│        │  │  ├─ HttpClientAssertionsTrait.php
│        │  │  ├─ KernelTestCase.php
│        │  │  ├─ MailerAssertionsTrait.php
│        │  │  ├─ NotificationAssertionsTrait.php
│        │  │  ├─ TestBrowserToken.php
│        │  │  ├─ TestContainer.php
│        │  │  ├─ WebTestAssertionsTrait.php
│        │  │  └─ WebTestCase.php
│        │  ├─ Tests
│        │  │  ├─ CacheWarmer
│        │  │  │  ├─ ConfigBuilderCacheWarmerTest.php
│        │  │  │  ├─ RouterCacheWarmerTest.php
│        │  │  │  ├─ SerializerCacheWarmerTest.php
│        │  │  │  └─ ValidatorCacheWarmerTest.php
│        │  │  ├─ Command
│        │  │  │  ├─ AboutCommand
│        │  │  │  │  ├─ AboutCommandTest.php
│        │  │  │  │  └─ Fixture
│        │  │  │  │     └─ TestAppKernel.php
│        │  │  │  ├─ CacheClearCommand
│        │  │  │  │  ├─ CacheClearCommandTest.php
│        │  │  │  │  └─ Fixture
│        │  │  │  │     ├─ config.yml
│        │  │  │  │     └─ TestAppKernel.php
│        │  │  │  ├─ CachePoolClearCommandTest.php
│        │  │  │  ├─ CachePoolDeleteCommandTest.php
│        │  │  │  ├─ CachePoolInvalidateTagsCommandTest.php
│        │  │  │  ├─ CachePruneCommandTest.php
│        │  │  │  ├─ EventDispatcherDebugCommandTest.php
│        │  │  │  ├─ RouterMatchCommandTest.php
│        │  │  │  ├─ SecretsListCommandTest.php
│        │  │  │  ├─ SecretsRemoveCommandTest.php
│        │  │  │  ├─ SecretsRevealCommandTest.php
│        │  │  │  ├─ SecretsSetCommandTest.php
│        │  │  │  ├─ TranslationDebugCommandTest.php
│        │  │  │  ├─ TranslationExtractCommandCompletionTest.php
│        │  │  │  ├─ TranslationExtractCommandTest.php
│        │  │  │  ├─ WorkflowDumpCommandTest.php
│        │  │  │  ├─ XliffLintCommandTest.php
│        │  │  │  └─ YamlLintCommandTest.php
│        │  │  ├─ Console
│        │  │  │  ├─ ApplicationTest.php
│        │  │  │  └─ Descriptor
│        │  │  │     ├─ AbstractDescriptorTestCase.php
│        │  │  │     ├─ JsonDescriptorTest.php
│        │  │  │     ├─ MarkdownDescriptorTest.php
│        │  │  │     ├─ ObjectsProvider.php
│        │  │  │     ├─ TextDescriptorTest.php
│        │  │  │     └─ XmlDescriptorTest.php
│        │  │  ├─ Controller
│        │  │  │  ├─ AbstractControllerTest.php
│        │  │  │  ├─ ControllerResolverTest.php
│        │  │  │  ├─ RedirectControllerTest.php
│        │  │  │  ├─ TemplateControllerTest.php
│        │  │  │  └─ TestAbstractController.php
│        │  │  ├─ DataCollector
│        │  │  │  └─ RouterDataCollectorTest.php
│        │  │  ├─ DependencyInjection
│        │  │  │  ├─ Compiler
│        │  │  │  │  ├─ ProfilerPassTest.php
│        │  │  │  │  ├─ TestServiceContainerRefPassesTest.php
│        │  │  │  │  ├─ UnusedTagsPassTest.php
│        │  │  │  │  └─ UnusedTagsPassUtils.php
│        │  │  │  ├─ config
│        │  │  │  │  ├─ serializer
│        │  │  │  │  │  └─ foo.yml
│        │  │  │  │  └─ validator
│        │  │  │  │     └─ foo.xml
│        │  │  │  ├─ ConfigurationTest.php
│        │  │  │  ├─ Fixtures
│        │  │  │  │  ├─ CustomPathBundle
│        │  │  │  │  │  ├─ Resources
│        │  │  │  │  │  │  └─ config
│        │  │  │  │  │  │     ├─ validation.xml
│        │  │  │  │  │  │     └─ validation.yml
│        │  │  │  │  │  └─ src
│        │  │  │  │  │     └─ CustomPathBundle.php
│        │  │  │  │  ├─ php
│        │  │  │  │  │  ├─ assets.php
│        │  │  │  │  │  ├─ assets_disabled.php
│        │  │  │  │  │  ├─ assets_version_strategy_as_service.php
│        │  │  │  │  │  ├─ asset_mapper_without_assets.php
│        │  │  │  │  │  ├─ cache.php
│        │  │  │  │  │  ├─ cache_app_redis_tag_aware.php
│        │  │  │  │  │  ├─ cache_app_redis_tag_aware_pool.php
│        │  │  │  │  │  ├─ csrf.php
│        │  │  │  │  │  ├─ csrf_needs_session.php
│        │  │  │  │  │  ├─ default_config.php
│        │  │  │  │  │  ├─ esi_and_ssi_without_fragments.php
│        │  │  │  │  │  ├─ esi_disabled.php
│        │  │  │  │  │  ├─ exceptions.php
│        │  │  │  │  │  ├─ form_csrf_disabled.php
│        │  │  │  │  │  ├─ form_csrf_field_attr.php
│        │  │  │  │  │  ├─ form_default_csrf.php
│        │  │  │  │  │  ├─ form_no_csrf.php
│        │  │  │  │  │  ├─ fragments_and_hinclude.php
│        │  │  │  │  │  ├─ full.php
│        │  │  │  │  │  ├─ html_sanitizer.php
│        │  │  │  │  │  ├─ html_sanitizer_default_allowed_link_and_media_hosts.php
│        │  │  │  │  │  ├─ html_sanitizer_default_config.php
│        │  │  │  │  │  ├─ http_client_default_options.php
│        │  │  │  │  │  ├─ http_client_full_default_options.php
│        │  │  │  │  │  ├─ http_client_mock_response_factory.php
│        │  │  │  │  │  ├─ http_client_override_default_options.php
│        │  │  │  │  │  ├─ http_client_rate_limiter.php
│        │  │  │  │  │  ├─ http_client_retry.php
│        │  │  │  │  │  ├─ http_client_scoped_without_query_option.php
│        │  │  │  │  │  ├─ http_client_xml_key.php
│        │  │  │  │  │  ├─ json_streamer.php
│        │  │  │  │  │  ├─ lock.php
│        │  │  │  │  │  ├─ lock_named.php
│        │  │  │  │  │  ├─ lock_service.php
│        │  │  │  │  │  ├─ mailer.php
│        │  │  │  │  │  ├─ mailer_with_disabled_message_bus.php
│        │  │  │  │  │  ├─ mailer_with_dsn.php
│        │  │  │  │  │  ├─ mailer_with_specific_message_bus.php
│        │  │  │  │  │  ├─ mailer_with_transports.php
│        │  │  │  │  │  ├─ messenger.php
│        │  │  │  │  │  ├─ messenger_disabled.php
│        │  │  │  │  │  ├─ messenger_middleware_factory_erroneous_format.php
│        │  │  │  │  │  ├─ messenger_multiple_buses_without_deduplicate_middleware.php
│        │  │  │  │  │  ├─ messenger_multiple_buses_with_deduplicate_middleware.php
│        │  │  │  │  │  ├─ messenger_multiple_failure_transports.php
│        │  │  │  │  │  ├─ messenger_multiple_failure_transports_global.php
│        │  │  │  │  │  ├─ messenger_routing.php
│        │  │  │  │  │  ├─ messenger_routing_invalid_transport.php
│        │  │  │  │  │  ├─ messenger_routing_invalid_wildcard.php
│        │  │  │  │  │  ├─ messenger_routing_single.php
│        │  │  │  │  │  ├─ messenger_transport.php
│        │  │  │  │  │  ├─ messenger_transports.php
│        │  │  │  │  │  ├─ notifier.php
│        │  │  │  │  │  ├─ notifier_without_mailer.php
│        │  │  │  │  │  ├─ notifier_without_messenger.php
│        │  │  │  │  │  ├─ notifier_without_transports.php
│        │  │  │  │  │  ├─ notifier_with_disabled_message_bus.php
│        │  │  │  │  │  ├─ notifier_with_specific_message_bus.php
│        │  │  │  │  │  ├─ php_errors_disabled.php
│        │  │  │  │  │  ├─ php_errors_enabled.php
│        │  │  │  │  │  ├─ php_errors_log_level.php
│        │  │  │  │  │  ├─ php_errors_log_levels.php
│        │  │  │  │  │  ├─ profiler.php
│        │  │  │  │  │  ├─ property_accessor.php
│        │  │  │  │  │  ├─ property_info.php
│        │  │  │  │  │  ├─ property_info_with_constructor_extractor.php
│        │  │  │  │  │  ├─ request.php
│        │  │  │  │  │  ├─ semaphore.php
│        │  │  │  │  │  ├─ semaphore_named.php
│        │  │  │  │  │  ├─ semaphore_service.php
│        │  │  │  │  │  ├─ serializer_disabled.php
│        │  │  │  │  │  ├─ serializer_enabled.php
│        │  │  │  │  │  ├─ serializer_mapping.php
│        │  │  │  │  │  ├─ serializer_mapping_without_annotations.php
│        │  │  │  │  │  ├─ serializer_without_translator.php
│        │  │  │  │  │  ├─ session.php
│        │  │  │  │  │  ├─ session_cookie_secure_auto.php
│        │  │  │  │  │  ├─ ssi_disabled.php
│        │  │  │  │  │  ├─ translator_cache_dir_disabled.php
│        │  │  │  │  │  ├─ translator_fallbacks.php
│        │  │  │  │  │  ├─ translator_globals.php
│        │  │  │  │  │  ├─ translator_without_globals.php
│        │  │  │  │  │  ├─ trusted_proxies_private_ranges.php
│        │  │  │  │  │  ├─ type_info.php
│        │  │  │  │  │  ├─ validation_attributes.php
│        │  │  │  │  │  ├─ validation_auto_mapping.php
│        │  │  │  │  │  ├─ validation_email_validation_mode.php
│        │  │  │  │  │  ├─ validation_mapping.php
│        │  │  │  │  │  ├─ validation_multiple_static_methods.php
│        │  │  │  │  │  ├─ validation_no_static_method.php
│        │  │  │  │  │  ├─ validation_translation_domain.php
│        │  │  │  │  │  ├─ webhook.php
│        │  │  │  │  │  ├─ webhook_without_serializer.php
│        │  │  │  │  │  ├─ web_link.php
│        │  │  │  │  │  ├─ workflows.php
│        │  │  │  │  │  ├─ workflows_enabled.php
│        │  │  │  │  │  ├─ workflows_explicitly_enabled.php
│        │  │  │  │  │  ├─ workflows_explicitly_enabled_named_workflows.php
│        │  │  │  │  │  ├─ workflow_not_valid.php
│        │  │  │  │  │  ├─ workflow_without_support_and_support_strategy.php
│        │  │  │  │  │  ├─ workflow_with_guard_expression.php
│        │  │  │  │  │  ├─ workflow_with_multiple_transitions_with_same_name.php
│        │  │  │  │  │  ├─ workflow_with_no_events_to_dispatch.php
│        │  │  │  │  │  ├─ workflow_with_specified_events_to_dispatch.php
│        │  │  │  │  │  └─ workflow_with_support_and_support_strategy.php
│        │  │  │  │  ├─ TestBundle
│        │  │  │  │  │  ├─ Resources
│        │  │  │  │  │  │  └─ config
│        │  │  │  │  │  │     ├─ serialization.xml
│        │  │  │  │  │  │     ├─ serialization.yml
│        │  │  │  │  │  │     ├─ serializer_mapping
│        │  │  │  │  │  │     │  ├─ files
│        │  │  │  │  │  │     │  │  ├─ foo.xml
│        │  │  │  │  │  │     │  │  └─ foo.yml
│        │  │  │  │  │  │     │  ├─ serialization.yaml
│        │  │  │  │  │  │     │  └─ serialization.yml
│        │  │  │  │  │  │     ├─ validation.xml
│        │  │  │  │  │  │     ├─ validation.yml
│        │  │  │  │  │  │     └─ validation_mapping
│        │  │  │  │  │  │        ├─ files
│        │  │  │  │  │  │        │  ├─ foo.xml
│        │  │  │  │  │  │        │  └─ foo.yml
│        │  │  │  │  │  │        ├─ validation.yaml
│        │  │  │  │  │  │        └─ validation.yml
│        │  │  │  │  │  └─ TestBundle.php
│        │  │  │  │  ├─ translations
│        │  │  │  │  │  ├─ domain.with.dots.en.yml
│        │  │  │  │  │  └─ test_paths.en.yml
│        │  │  │  │  ├─ Workflow
│        │  │  │  │  │  └─ Validator
│        │  │  │  │  │     └─ DefinitionValidator.php
│        │  │  │  │  ├─ xml
│        │  │  │  │  │  ├─ assets.xml
│        │  │  │  │  │  ├─ assets_disabled.xml
│        │  │  │  │  │  ├─ assets_version_strategy_as_service.xml
│        │  │  │  │  │  ├─ asset_mapper.xml
│        │  │  │  │  │  ├─ asset_mapper_without_assets.xml
│        │  │  │  │  │  ├─ cache.xml
│        │  │  │  │  │  ├─ cache_app_redis_tag_aware.xml
│        │  │  │  │  │  ├─ cache_app_redis_tag_aware_pool.xml
│        │  │  │  │  │  ├─ csrf.xml
│        │  │  │  │  │  ├─ csrf_disabled.xml
│        │  │  │  │  │  ├─ csrf_needs_session.xml
│        │  │  │  │  │  ├─ default_config.xml
│        │  │  │  │  │  ├─ esi_and_ssi_without_fragments.xml
│        │  │  │  │  │  ├─ esi_disabled.xml
│        │  │  │  │  │  ├─ exceptions.xml
│        │  │  │  │  │  ├─ form_csrf_disabled.xml
│        │  │  │  │  │  ├─ form_csrf_field_attr.xml
│        │  │  │  │  │  ├─ form_default_csrf.xml
│        │  │  │  │  │  ├─ form_no_csrf.xml
│        │  │  │  │  │  ├─ fragments_and_hinclude.xml
│        │  │  │  │  │  ├─ full.xml
│        │  │  │  │  │  ├─ html_sanitizer.xml
│        │  │  │  │  │  ├─ html_sanitizer_default_allowed_link_and_media_hosts.xml
│        │  │  │  │  │  ├─ html_sanitizer_default_config.xml
│        │  │  │  │  │  ├─ http_client_default_options.xml
│        │  │  │  │  │  ├─ http_client_full_default_options.xml
│        │  │  │  │  │  ├─ http_client_mock_response_factory.xml
│        │  │  │  │  │  ├─ http_client_override_default_options.xml
│        │  │  │  │  │  ├─ http_client_rate_limiter.xml
│        │  │  │  │  │  ├─ http_client_retry.xml
│        │  │  │  │  │  ├─ http_client_scoped_without_query_option.xml
│        │  │  │  │  │  ├─ http_client_xml_key.xml
│        │  │  │  │  │  ├─ json_streamer.xml
│        │  │  │  │  │  ├─ lock.xml
│        │  │  │  │  │  ├─ lock_named.xml
│        │  │  │  │  │  ├─ lock_service.xml
│        │  │  │  │  │  ├─ mailer_with_disabled_message_bus.xml
│        │  │  │  │  │  ├─ mailer_with_dsn.xml
│        │  │  │  │  │  ├─ mailer_with_specific_message_bus.xml
│        │  │  │  │  │  ├─ mailer_with_transports.xml
│        │  │  │  │  │  ├─ messenger.xml
│        │  │  │  │  │  ├─ messenger_disabled.xml
│        │  │  │  │  │  ├─ messenger_multiple_buses_without_deduplicate_middleware.xml
│        │  │  │  │  │  ├─ messenger_multiple_buses_with_deduplicate_middleware.xml
│        │  │  │  │  │  ├─ messenger_multiple_failure_transports.xml
│        │  │  │  │  │  ├─ messenger_multiple_failure_transports_global.xml
│        │  │  │  │  │  ├─ messenger_routing.xml
│        │  │  │  │  │  ├─ messenger_routing_invalid_transport.xml
│        │  │  │  │  │  ├─ messenger_routing_invalid_wildcard.xml
│        │  │  │  │  │  ├─ messenger_routing_single.xml
│        │  │  │  │  │  ├─ messenger_schedule.xml
│        │  │  │  │  │  ├─ messenger_transport.xml
│        │  │  │  │  │  ├─ messenger_transports.xml
│        │  │  │  │  │  ├─ notifier.xml
│        │  │  │  │  │  ├─ notifier_without_mailer.xml
│        │  │  │  │  │  ├─ notifier_without_messenger.xml
│        │  │  │  │  │  ├─ notifier_without_transports.xml
│        │  │  │  │  │  ├─ notifier_with_disabled_message_bus.xml
│        │  │  │  │  │  ├─ notifier_with_specific_message_bus.xml
│        │  │  │  │  │  ├─ php_errors_disabled.xml
│        │  │  │  │  │  ├─ php_errors_enabled.xml
│        │  │  │  │  │  ├─ php_errors_log_level.xml
│        │  │  │  │  │  ├─ php_errors_log_levels.xml
│        │  │  │  │  │  ├─ profiler.xml
│        │  │  │  │  │  ├─ property_accessor.xml
│        │  │  │  │  │  ├─ property_info.xml
│        │  │  │  │  │  ├─ property_info_with_constructor_extractor.xml
│        │  │  │  │  │  ├─ rate_limiter.xml
│        │  │  │  │  │  ├─ request.xml
│        │  │  │  │  │  ├─ semaphore.xml
│        │  │  │  │  │  ├─ semaphore_named.xml
│        │  │  │  │  │  ├─ semaphore_service.xml
│        │  │  │  │  │  ├─ serializer_disabled.xml
│        │  │  │  │  │  ├─ serializer_enabled.xml
│        │  │  │  │  │  ├─ serializer_mapping.xml
│        │  │  │  │  │  ├─ serializer_mapping_without_annotations.xml
│        │  │  │  │  │  ├─ serializer_without_translator.xml
│        │  │  │  │  │  ├─ session.xml
│        │  │  │  │  │  ├─ session_cookie_secure_auto.xml
│        │  │  │  │  │  ├─ ssi_disabled.xml
│        │  │  │  │  │  ├─ translator_cache_dir_disabled.xml
│        │  │  │  │  │  ├─ translator_fallbacks.xml
│        │  │  │  │  │  ├─ translator_globals.xml
│        │  │  │  │  │  ├─ translator_without_globals.xml
│        │  │  │  │  │  ├─ trusted_proxies_private_ranges.xml
│        │  │  │  │  │  ├─ type_info.xml
│        │  │  │  │  │  ├─ validation_attributes.xml
│        │  │  │  │  │  ├─ validation_auto_mapping.xml
│        │  │  │  │  │  ├─ validation_email_validation_mode.xml
│        │  │  │  │  │  ├─ validation_mapping.xml
│        │  │  │  │  │  ├─ validation_multiple_static_methods.xml
│        │  │  │  │  │  ├─ validation_no_static_method.xml
│        │  │  │  │  │  ├─ validation_translation_domain.xml
│        │  │  │  │  │  ├─ webhook.xml
│        │  │  │  │  │  ├─ webhook_without_serializer.xml
│        │  │  │  │  │  ├─ web_link.xml
│        │  │  │  │  │  ├─ workflows.xml
│        │  │  │  │  │  ├─ workflows_enabled.xml
│        │  │  │  │  │  ├─ workflows_explicitly_enabled.xml
│        │  │  │  │  │  ├─ workflows_explicitly_enabled_named_workflows.xml
│        │  │  │  │  │  ├─ workflow_not_valid.xml
│        │  │  │  │  │  ├─ workflow_without_support_and_support_strategy.xml
│        │  │  │  │  │  ├─ workflow_with_guard_expression.xml
│        │  │  │  │  │  ├─ workflow_with_multiple_transitions_with_same_name.xml
│        │  │  │  │  │  ├─ workflow_with_no_events_to_dispatch.xml
│        │  │  │  │  │  ├─ workflow_with_specified_events_to_dispatch.xml
│        │  │  │  │  │  └─ workflow_with_support_and_support_strategy.xml
│        │  │  │  │  └─ yml
│        │  │  │  │     ├─ assets.yml
│        │  │  │  │     ├─ assets_disabled.yml
│        │  │  │  │     ├─ assets_version_strategy_as_service.yml
│        │  │  │  │     ├─ asset_mapper_without_assets.yml
│        │  │  │  │     ├─ cache.yml
│        │  │  │  │     ├─ cache_app_redis_tag_aware.yml
│        │  │  │  │     ├─ cache_app_redis_tag_aware_pool.yml
│        │  │  │  │     ├─ csrf.yml
│        │  │  │  │     ├─ csrf_needs_session.yml
│        │  │  │  │     ├─ default_config.yml
│        │  │  │  │     ├─ esi_and_ssi_without_fragments.yml
│        │  │  │  │     ├─ esi_disabled.yml
│        │  │  │  │     ├─ exceptions.yml
│        │  │  │  │     ├─ form_csrf_disabled.yml
│        │  │  │  │     ├─ form_csrf_field_attr.yml
│        │  │  │  │     ├─ form_default_csrf.yml
│        │  │  │  │     ├─ form_no_csrf.yml
│        │  │  │  │     ├─ fragments_and_hinclude.yml
│        │  │  │  │     ├─ full.yml
│        │  │  │  │     ├─ html_sanitizer.yml
│        │  │  │  │     ├─ html_sanitizer_default_allowed_link_and_media_hosts.yml
│        │  │  │  │     ├─ html_sanitizer_default_config.yml
│        │  │  │  │     ├─ http_client_default_options.yml
│        │  │  │  │     ├─ http_client_full_default_options.yml
│        │  │  │  │     ├─ http_client_mock_response_factory.yml
│        │  │  │  │     ├─ http_client_override_default_options.yml
│        │  │  │  │     ├─ http_client_rate_limiter.yml
│        │  │  │  │     ├─ http_client_retry.yml
│        │  │  │  │     ├─ http_client_scoped_without_query_option.yml
│        │  │  │  │     ├─ http_client_xml_key.yml
│        │  │  │  │     ├─ json_streamer.yml
│        │  │  │  │     ├─ lock.yml
│        │  │  │  │     ├─ lock_named.yml
│        │  │  │  │     ├─ lock_service.yml
│        │  │  │  │     ├─ mailer_with_disabled_message_bus.yml
│        │  │  │  │     ├─ mailer_with_dsn.yml
│        │  │  │  │     ├─ mailer_with_specific_message_bus.yml
│        │  │  │  │     ├─ mailer_with_transports.yml
│        │  │  │  │     ├─ messenger.yml
│        │  │  │  │     ├─ messenger_disabled.yml
│        │  │  │  │     ├─ messenger_middleware_factory_erroneous_format.yml
│        │  │  │  │     ├─ messenger_multiple_buses_without_deduplicate_middleware.yml
│        │  │  │  │     ├─ messenger_multiple_buses_with_deduplicate_middleware.yml
│        │  │  │  │     ├─ messenger_multiple_failure_transports.yml
│        │  │  │  │     ├─ messenger_multiple_failure_transports_global.yml
│        │  │  │  │     ├─ messenger_routing.yml
│        │  │  │  │     ├─ messenger_routing_invalid_transport.yml
│        │  │  │  │     ├─ messenger_routing_invalid_wildcard.yml
│        │  │  │  │     ├─ messenger_routing_single.yml
│        │  │  │  │     ├─ messenger_schedule.yml
│        │  │  │  │     ├─ messenger_transport.yml
│        │  │  │  │     ├─ messenger_transports.yml
│        │  │  │  │     ├─ messenger_with_disabled_reset_on_message.yml
│        │  │  │  │     ├─ messenger_with_explict_reset_on_message_legacy.yml
│        │  │  │  │     ├─ notifier.yml
│        │  │  │  │     ├─ notifier_without_mailer.yml
│        │  │  │  │     ├─ notifier_without_messenger.yml
│        │  │  │  │     ├─ notifier_without_transports.yml
│        │  │  │  │     ├─ notifier_with_disabled_message_bus.yml
│        │  │  │  │     ├─ notifier_with_specific_message_bus.yml
│        │  │  │  │     ├─ php_errors_disabled.yml
│        │  │  │  │     ├─ php_errors_enabled.yml
│        │  │  │  │     ├─ php_errors_log_level.yml
│        │  │  │  │     ├─ php_errors_log_levels.yml
│        │  │  │  │     ├─ profiler.yml
│        │  │  │  │     ├─ property_accessor.yml
│        │  │  │  │     ├─ property_info.yml
│        │  │  │  │     ├─ property_info_with_constructor_extractor.yml
│        │  │  │  │     ├─ request.yml
│        │  │  │  │     ├─ semaphore.yml
│        │  │  │  │     ├─ semaphore_named.yml
│        │  │  │  │     ├─ semaphore_service.yml
│        │  │  │  │     ├─ serializer_disabled.yml
│        │  │  │  │     ├─ serializer_enabled.yml
│        │  │  │  │     ├─ serializer_mapping.yml
│        │  │  │  │     ├─ serializer_mapping_without_annotations.yml
│        │  │  │  │     ├─ serializer_without_translator.yml
│        │  │  │  │     ├─ session.yml
│        │  │  │  │     ├─ session_cookie_secure_auto.yml
│        │  │  │  │     ├─ ssi_disabled.yml
│        │  │  │  │     ├─ translator_cache_dir_disabled.yml
│        │  │  │  │     ├─ translator_fallbacks.yml
│        │  │  │  │     ├─ translator_globals.yml
│        │  │  │  │     ├─ translator_without_globals.yml
│        │  │  │  │     ├─ trusted_proxies_private_ranges.yml
│        │  │  │  │     ├─ type_info.yml
│        │  │  │  │     ├─ validation_attributes.yml
│        │  │  │  │     ├─ validation_auto_mapping.yml
│        │  │  │  │     ├─ validation_email_validation_mode.yml
│        │  │  │  │     ├─ validation_mapping.yml
│        │  │  │  │     ├─ validation_multiple_static_methods.yml
│        │  │  │  │     ├─ validation_no_static_method.yml
│        │  │  │  │     ├─ validation_translation_domain.yml
│        │  │  │  │     ├─ webhook.yml
│        │  │  │  │     ├─ webhook_without_serializer.yml
│        │  │  │  │     ├─ web_link.yml
│        │  │  │  │     ├─ workflows.yml
│        │  │  │  │     ├─ workflows_enabled.yml
│        │  │  │  │     ├─ workflows_explicitly_enabled.yml
│        │  │  │  │     ├─ workflows_explicitly_enabled_named_workflows.yml
│        │  │  │  │     ├─ workflow_not_valid.yml
│        │  │  │  │     ├─ workflow_without_support_and_support_strategy.yml
│        │  │  │  │     ├─ workflow_with_guard_expression.yml
│        │  │  │  │     ├─ workflow_with_multiple_transitions_with_same_name.yml
│        │  │  │  │     ├─ workflow_with_no_events_to_dispatch.yml
│        │  │  │  │     ├─ workflow_with_specified_events_to_dispatch.yml
│        │  │  │  │     └─ workflow_with_support_and_support_strategy.yml
│        │  │  │  ├─ FrameworkExtensionTestCase.php
│        │  │  │  ├─ PhpFrameworkExtensionTest.php
│        │  │  │  ├─ translations
│        │  │  │  │  ├─ security.en.yaml
│        │  │  │  │  └─ test_default.en.xlf
│        │  │  │  ├─ XmlFrameworkExtensionTest.php
│        │  │  │  └─ YamlFrameworkExtensionTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ BackslashClass.php
│        │  │  │  ├─ ClassAliasExampleClass.php
│        │  │  │  ├─ ClassAliasTargetClass.php
│        │  │  │  ├─ ContainerExcluded.php
│        │  │  │  ├─ DeclaredClass.php
│        │  │  │  ├─ DeprecatedClass.php
│        │  │  │  ├─ Descriptor
│        │  │  │  │  ├─ alias_1.json
│        │  │  │  │  ├─ alias_1.md
│        │  │  │  │  ├─ alias_1.txt
│        │  │  │  │  ├─ alias_1.xml
│        │  │  │  │  ├─ alias_2.json
│        │  │  │  │  ├─ alias_2.md
│        │  │  │  │  ├─ alias_2.txt
│        │  │  │  │  ├─ alias_2.xml
│        │  │  │  │  ├─ alias_with_definition_1.json
│        │  │  │  │  ├─ alias_with_definition_1.md
│        │  │  │  │  ├─ alias_with_definition_1.txt
│        │  │  │  │  ├─ alias_with_definition_1.xml
│        │  │  │  │  ├─ alias_with_definition_2.json
│        │  │  │  │  ├─ alias_with_definition_2.md
│        │  │  │  │  ├─ alias_with_definition_2.txt
│        │  │  │  │  ├─ alias_with_definition_2.xml
│        │  │  │  │  ├─ array_parameter.json
│        │  │  │  │  ├─ array_parameter.md
│        │  │  │  │  ├─ array_parameter.txt
│        │  │  │  │  ├─ array_parameter.xml
│        │  │  │  │  ├─ builder_1_arguments.json
│        │  │  │  │  ├─ builder_1_arguments.md
│        │  │  │  │  ├─ builder_1_arguments.txt
│        │  │  │  │  ├─ builder_1_arguments.xml
│        │  │  │  │  ├─ builder_1_public.json
│        │  │  │  │  ├─ builder_1_public.md
│        │  │  │  │  ├─ builder_1_public.txt
│        │  │  │  │  ├─ builder_1_public.xml
│        │  │  │  │  ├─ builder_1_services.json
│        │  │  │  │  ├─ builder_1_services.md
│        │  │  │  │  ├─ builder_1_services.txt
│        │  │  │  │  ├─ builder_1_services.xml
│        │  │  │  │  ├─ builder_1_tag1.json
│        │  │  │  │  ├─ builder_1_tag1.md
│        │  │  │  │  ├─ builder_1_tag1.txt
│        │  │  │  │  ├─ builder_1_tag1.xml
│        │  │  │  │  ├─ builder_1_tags.json
│        │  │  │  │  ├─ builder_1_tags.md
│        │  │  │  │  ├─ builder_1_tags.txt
│        │  │  │  │  ├─ builder_1_tags.xml
│        │  │  │  │  ├─ builder_priority_tag.json
│        │  │  │  │  ├─ builder_priority_tag.md
│        │  │  │  │  ├─ builder_priority_tag.txt
│        │  │  │  │  ├─ builder_priority_tag.xml
│        │  │  │  │  ├─ cache
│        │  │  │  │  │  ├─ KernelContainerWithDeprecations.log
│        │  │  │  │  │  └─ KernelContainerWithoutDeprecations.log
│        │  │  │  │  ├─ callable_1.json
│        │  │  │  │  ├─ callable_1.md
│        │  │  │  │  ├─ callable_1.txt
│        │  │  │  │  ├─ callable_1.xml
│        │  │  │  │  ├─ callable_2.json
│        │  │  │  │  ├─ callable_2.md
│        │  │  │  │  ├─ callable_2.txt
│        │  │  │  │  ├─ callable_2.xml
│        │  │  │  │  ├─ callable_3.json
│        │  │  │  │  ├─ callable_3.md
│        │  │  │  │  ├─ callable_3.txt
│        │  │  │  │  ├─ callable_3.xml
│        │  │  │  │  ├─ callable_4.json
│        │  │  │  │  ├─ callable_4.md
│        │  │  │  │  ├─ callable_4.txt
│        │  │  │  │  ├─ callable_4.xml
│        │  │  │  │  ├─ callable_5.json
│        │  │  │  │  ├─ callable_5.md
│        │  │  │  │  ├─ callable_5.txt
│        │  │  │  │  ├─ callable_5.xml
│        │  │  │  │  ├─ callable_6.json
│        │  │  │  │  ├─ callable_6.md
│        │  │  │  │  ├─ callable_6.txt
│        │  │  │  │  ├─ callable_6.xml
│        │  │  │  │  ├─ callable_7.json
│        │  │  │  │  ├─ callable_7.md
│        │  │  │  │  ├─ callable_7.txt
│        │  │  │  │  ├─ callable_7.xml
│        │  │  │  │  ├─ callable_from_callable.json
│        │  │  │  │  ├─ callable_from_callable.md
│        │  │  │  │  ├─ callable_from_callable.txt
│        │  │  │  │  ├─ callable_from_callable.xml
│        │  │  │  │  ├─ definition_1.json
│        │  │  │  │  ├─ definition_1.md
│        │  │  │  │  ├─ definition_1.txt
│        │  │  │  │  ├─ definition_1.xml
│        │  │  │  │  ├─ definition_2.json
│        │  │  │  │  ├─ definition_2.md
│        │  │  │  │  ├─ definition_2.txt
│        │  │  │  │  ├─ definition_2.xml
│        │  │  │  │  ├─ definition_3.json
│        │  │  │  │  ├─ definition_3.md
│        │  │  │  │  ├─ definition_3.txt
│        │  │  │  │  ├─ definition_3.xml
│        │  │  │  │  ├─ definition_arguments_1.json
│        │  │  │  │  ├─ definition_arguments_1.md
│        │  │  │  │  ├─ definition_arguments_1.txt
│        │  │  │  │  ├─ definition_arguments_1.xml
│        │  │  │  │  ├─ definition_arguments_2.json
│        │  │  │  │  ├─ definition_arguments_2.md
│        │  │  │  │  ├─ definition_arguments_2.txt
│        │  │  │  │  ├─ definition_arguments_2.xml
│        │  │  │  │  ├─ definition_arguments_3.json
│        │  │  │  │  ├─ definition_arguments_3.md
│        │  │  │  │  ├─ definition_arguments_3.txt
│        │  │  │  │  ├─ definition_arguments_3.xml
│        │  │  │  │  ├─ definition_arguments_without_class.json
│        │  │  │  │  ├─ definition_arguments_without_class.md
│        │  │  │  │  ├─ definition_arguments_without_class.txt
│        │  │  │  │  ├─ definition_arguments_without_class.xml
│        │  │  │  │  ├─ definition_arguments_with_enum.json
│        │  │  │  │  ├─ definition_arguments_with_enum.md
│        │  │  │  │  ├─ definition_arguments_with_enum.txt
│        │  │  │  │  ├─ definition_arguments_with_enum.xml
│        │  │  │  │  ├─ definition_without_class.json
│        │  │  │  │  ├─ definition_without_class.md
│        │  │  │  │  ├─ definition_without_class.txt
│        │  │  │  │  ├─ definition_without_class.xml
│        │  │  │  │  ├─ deprecated_parameter.json
│        │  │  │  │  ├─ deprecated_parameter.md
│        │  │  │  │  ├─ deprecated_parameter.txt
│        │  │  │  │  ├─ deprecated_parameter.xml
│        │  │  │  │  ├─ deprecated_parameters.json
│        │  │  │  │  ├─ deprecated_parameters.md
│        │  │  │  │  ├─ deprecated_parameters.txt
│        │  │  │  │  ├─ deprecated_parameters.xml
│        │  │  │  │  ├─ deprecations.json
│        │  │  │  │  ├─ deprecations.md
│        │  │  │  │  ├─ deprecations.txt
│        │  │  │  │  ├─ deprecations.xml
│        │  │  │  │  ├─ deprecations_empty.json
│        │  │  │  │  ├─ deprecations_empty.md
│        │  │  │  │  ├─ deprecations_empty.txt
│        │  │  │  │  ├─ deprecations_empty.xml
│        │  │  │  │  ├─ event_dispatcher_1_event1.json
│        │  │  │  │  ├─ event_dispatcher_1_event1.md
│        │  │  │  │  ├─ event_dispatcher_1_event1.txt
│        │  │  │  │  ├─ event_dispatcher_1_event1.xml
│        │  │  │  │  ├─ event_dispatcher_1_events.json
│        │  │  │  │  ├─ event_dispatcher_1_events.md
│        │  │  │  │  ├─ event_dispatcher_1_events.txt
│        │  │  │  │  ├─ event_dispatcher_1_events.xml
│        │  │  │  │  ├─ existing_class_def_1.json
│        │  │  │  │  ├─ existing_class_def_1.md
│        │  │  │  │  ├─ existing_class_def_1.txt
│        │  │  │  │  ├─ existing_class_def_1.xml
│        │  │  │  │  ├─ existing_class_def_2.json
│        │  │  │  │  ├─ existing_class_def_2.md
│        │  │  │  │  ├─ existing_class_def_2.txt
│        │  │  │  │  ├─ existing_class_def_2.xml
│        │  │  │  │  ├─ parameter.json
│        │  │  │  │  ├─ parameter.md
│        │  │  │  │  ├─ parameter.txt
│        │  │  │  │  ├─ parameter.xml
│        │  │  │  │  ├─ parameters_1.json
│        │  │  │  │  ├─ parameters_1.md
│        │  │  │  │  ├─ parameters_1.txt
│        │  │  │  │  ├─ parameters_1.xml
│        │  │  │  │  ├─ parameters_enums.json
│        │  │  │  │  ├─ parameters_enums.md
│        │  │  │  │  ├─ parameters_enums.txt
│        │  │  │  │  ├─ parameters_enums.xml
│        │  │  │  │  ├─ route_1.json
│        │  │  │  │  ├─ route_1.md
│        │  │  │  │  ├─ route_1.txt
│        │  │  │  │  ├─ route_1.xml
│        │  │  │  │  ├─ route_1_link.txt
│        │  │  │  │  ├─ route_2.json
│        │  │  │  │  ├─ route_2.md
│        │  │  │  │  ├─ route_2.txt
│        │  │  │  │  ├─ route_2.xml
│        │  │  │  │  ├─ route_2_link.txt
│        │  │  │  │  ├─ route_collection_1.json
│        │  │  │  │  ├─ route_collection_1.md
│        │  │  │  │  ├─ route_collection_1.txt
│        │  │  │  │  ├─ route_collection_1.xml
│        │  │  │  │  ├─ route_collection_2.json
│        │  │  │  │  ├─ route_collection_2.md
│        │  │  │  │  ├─ route_collection_2.txt
│        │  │  │  │  ├─ route_collection_2.xml
│        │  │  │  │  ├─ route_collection_3.json
│        │  │  │  │  ├─ route_collection_3.md
│        │  │  │  │  ├─ route_collection_3.txt
│        │  │  │  │  └─ route_collection_3.xml
│        │  │  │  ├─ FooUnitEnum.php
│        │  │  │  ├─ Messenger
│        │  │  │  │  ├─ BarMessage.php
│        │  │  │  │  ├─ DummyMessage.php
│        │  │  │  │  ├─ DummyMessageInterface.php
│        │  │  │  │  ├─ DummySchedule.php
│        │  │  │  │  ├─ DummyTask.php
│        │  │  │  │  ├─ DummyTaskWithCustomReceiver.php
│        │  │  │  │  ├─ FooMessage.php
│        │  │  │  │  └─ SecondMessage.php
│        │  │  │  ├─ ObjectMapper
│        │  │  │  │  ├─ ObjectMapped.php
│        │  │  │  │  ├─ ObjectToBeMapped.php
│        │  │  │  │  └─ TransformCallable.php
│        │  │  │  ├─ Resources
│        │  │  │  │  ├─ BaseBundle
│        │  │  │  │  │  └─ views
│        │  │  │  │  │     ├─ base.format.engine
│        │  │  │  │  │     └─ controller
│        │  │  │  │  │        └─ custom.format.engine
│        │  │  │  │  ├─ translations
│        │  │  │  │  │  ├─ domain.with.dots.en.yml
│        │  │  │  │  │  └─ messages.fr.yml
│        │  │  │  │  ├─ translations2
│        │  │  │  │  │  └─ ccc.fr.yml
│        │  │  │  │  └─ views
│        │  │  │  │     ├─ resource.format.engine
│        │  │  │  │     ├─ this.is.a.template.format.engine
│        │  │  │  │     └─ translation.html.php
│        │  │  │  ├─ Serialization
│        │  │  │  │  ├─ Author.php
│        │  │  │  │  ├─ Person.php
│        │  │  │  │  └─ Resources
│        │  │  │  │     ├─ author.yml
│        │  │  │  │     ├─ does_not_exist.yaml
│        │  │  │  │     └─ person.xml
│        │  │  │  ├─ Serializer
│        │  │  │  │  ├─ CircularReferenceHandler.php
│        │  │  │  │  └─ MaxDepthHandler.php
│        │  │  │  ├─ Suit.php
│        │  │  │  ├─ TemplatePathsCache
│        │  │  │  │  ├─ templates-empty.php
│        │  │  │  │  └─ templates.php
│        │  │  │  ├─ templates.php
│        │  │  │  ├─ TranslatableBackedEnum.php
│        │  │  │  ├─ Validation
│        │  │  │  │  ├─ Article.php
│        │  │  │  │  ├─ Author.php
│        │  │  │  │  ├─ Category.php
│        │  │  │  │  ├─ Person.php
│        │  │  │  │  ├─ Resources
│        │  │  │  │  │  ├─ author.yml
│        │  │  │  │  │  ├─ categories.yml
│        │  │  │  │  │  ├─ does_not_exist.yaml
│        │  │  │  │  │  └─ person.xml
│        │  │  │  │  └─ SubCategory.php
│        │  │  │  └─ WarmedClass.php
│        │  │  ├─ Functional
│        │  │  │  ├─ AbstractAttributeRoutingTestCase.php
│        │  │  │  ├─ AbstractWebTestCase.php
│        │  │  │  ├─ AnnotatedControllerTest.php
│        │  │  │  ├─ ApiAttributesTest.php
│        │  │  │  ├─ app
│        │  │  │  │  ├─ AnnotatedController
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ ApiAttributesTest
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ AppKernel.php
│        │  │  │  │  ├─ AutowiringTypes
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ BundlePaths
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ CacheAttributeListener
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ CachePoolClear
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ CachePools
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ default.yml
│        │  │  │  │  │  ├─ redis_config.yml
│        │  │  │  │  │  └─ redis_custom_config.yml
│        │  │  │  │  ├─ config
│        │  │  │  │  │  ├─ default.yml
│        │  │  │  │  │  └─ framework.yml
│        │  │  │  │  ├─ ConfigDump
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ ContainerDebug
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ ContainerDump
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ ControllerServiceResolution
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ Fragment
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ routing.yml
│        │  │  │  │  │  └─ services.yml
│        │  │  │  │  ├─ HttpClient
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ routing.yml
│        │  │  │  │  │  └─ services.yml
│        │  │  │  │  ├─ JsonStreamer
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ Dto
│        │  │  │  │  │  │  └─ Dummy.php
│        │  │  │  │  │  ├─ RangeToStringValueTransformer.php
│        │  │  │  │  │  └─ StringToRangeValueTransformer.php
│        │  │  │  │  ├─ Mailer
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ routing.yml
│        │  │  │  │  │  └─ services.yml
│        │  │  │  │  ├─ Notifier
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ routing.yml
│        │  │  │  │  │  └─ services.yml
│        │  │  │  │  ├─ ObjectMapper
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ Profiler
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ ProfilerCollectParameter
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ Psr4Routing
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ RouterDebug
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ RoutingConditionService
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ routing.yml
│        │  │  │  │  │  ├─ services_auto_configured.yml
│        │  │  │  │  │  └─ services_manually_configured.yml
│        │  │  │  │  ├─ Scheduler
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  └─ config.yml
│        │  │  │  │  ├─ Security
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ Serializer
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ default_context.yaml
│        │  │  │  │  ├─ Session
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ routing.yml
│        │  │  │  │  ├─ Slugger
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ services.yml
│        │  │  │  │  ├─ templates
│        │  │  │  │  │  └─ fragment.html.twig
│        │  │  │  │  ├─ TestServiceContainer
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  ├─ services.yml
│        │  │  │  │  │  └─ test_disabled.yml
│        │  │  │  │  ├─ TransDebug
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ services.yml
│        │  │  │  │  ├─ TypeInfo
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ config.yml
│        │  │  │  │  │  └─ Dummy.php
│        │  │  │  │  └─ Uid
│        │  │  │  │     ├─ bundles.php
│        │  │  │  │     ├─ config_disabled.yml
│        │  │  │  │     ├─ config_enabled.yml
│        │  │  │  │     └─ routing.yml
│        │  │  │  ├─ AutowiringTypesTest.php
│        │  │  │  ├─ Bundle
│        │  │  │  │  ├─ DefaultConfigTestBundle
│        │  │  │  │  │  ├─ DefaultConfigTestBundle.php
│        │  │  │  │  │  └─ DependencyInjection
│        │  │  │  │  │     ├─ Configuration.php
│        │  │  │  │  │     └─ DefaultConfigTestExtension.php
│        │  │  │  │  ├─ ExtensionWithoutConfigTestBundle
│        │  │  │  │  │  ├─ DependencyInjection
│        │  │  │  │  │  │  └─ ExtensionWithoutConfigTestExtension.php
│        │  │  │  │  │  └─ ExtensionWithoutConfigTestBundle.php
│        │  │  │  │  ├─ LegacyBundle
│        │  │  │  │  │  ├─ Entity
│        │  │  │  │  │  │  └─ LegacyPerson.php
│        │  │  │  │  │  ├─ LegacyBundle.php
│        │  │  │  │  │  └─ Resources
│        │  │  │  │  │     ├─ config
│        │  │  │  │  │     │  ├─ serialization.yaml
│        │  │  │  │  │     │  └─ validation.yaml
│        │  │  │  │  │     ├─ public
│        │  │  │  │  │     │  └─ legacy.css
│        │  │  │  │  │     ├─ translations
│        │  │  │  │  │     │  └─ legacy.en.yaml
│        │  │  │  │  │     └─ views
│        │  │  │  │  │        └─ index.html.twig
│        │  │  │  │  ├─ ModernBundle
│        │  │  │  │  │  ├─ config
│        │  │  │  │  │  │  ├─ serialization.yaml
│        │  │  │  │  │  │  └─ validation.yaml
│        │  │  │  │  │  ├─ public
│        │  │  │  │  │  │  └─ modern.css
│        │  │  │  │  │  ├─ src
│        │  │  │  │  │  │  ├─ Entity
│        │  │  │  │  │  │  │  └─ ModernPerson.php
│        │  │  │  │  │  │  └─ ModernBundle.php
│        │  │  │  │  │  ├─ templates
│        │  │  │  │  │  │  └─ index.html.twig
│        │  │  │  │  │  └─ translations
│        │  │  │  │  │     └─ modern.en.yaml
│        │  │  │  │  ├─ RoutingConditionServiceBundle
│        │  │  │  │  │  ├─ Controller
│        │  │  │  │  │  │  └─ DefaultController.php
│        │  │  │  │  │  ├─ RoutingConditionServiceBundle.php
│        │  │  │  │  │  └─ Service
│        │  │  │  │  │     ├─ AutoConfiguredNonAliasedService.php
│        │  │  │  │  │     ├─ AutoConfiguredService.php
│        │  │  │  │  │     ├─ FooOriginalService.php
│        │  │  │  │  │     ├─ FooReplacementService.php
│        │  │  │  │  │     └─ ManuallyTaggedService.php
│        │  │  │  │  └─ TestBundle
│        │  │  │  │     ├─ AutowiringTypes
│        │  │  │  │     │  └─ AutowiredServices.php
│        │  │  │  │     ├─ Controller
│        │  │  │  │     │  ├─ AnnotatedController.php
│        │  │  │  │     │  ├─ EmailController.php
│        │  │  │  │     │  ├─ FragmentController.php
│        │  │  │  │     │  ├─ HttpClientController.php
│        │  │  │  │     │  ├─ NotificationController.php
│        │  │  │  │     │  ├─ ProfilerController.php
│        │  │  │  │     │  ├─ SecurityController.php
│        │  │  │  │     │  ├─ SessionController.php
│        │  │  │  │     │  ├─ SubRequestController.php
│        │  │  │  │     │  ├─ SubRequestServiceResolutionController.php
│        │  │  │  │     │  ├─ TransController.php
│        │  │  │  │     │  └─ UidController.php
│        │  │  │  │     ├─ DependencyInjection
│        │  │  │  │     │  ├─ Config
│        │  │  │  │     │  │  └─ CustomConfig.php
│        │  │  │  │     │  ├─ Configuration.php
│        │  │  │  │     │  └─ TestExtension.php
│        │  │  │  │     ├─ Resources
│        │  │  │  │     │  └─ config
│        │  │  │  │     │     └─ routing.yml
│        │  │  │  │     ├─ Slugger
│        │  │  │  │     │  └─ SlugConstructArgService.php
│        │  │  │  │     ├─ TestBundle.php
│        │  │  │  │     ├─ Tests
│        │  │  │  │     │  └─ MockClientCallback.php
│        │  │  │  │     ├─ TestServiceContainer
│        │  │  │  │     │  ├─ NonPublicService.php
│        │  │  │  │     │  ├─ PrivateService.php
│        │  │  │  │     │  ├─ PublicService.php
│        │  │  │  │     │  ├─ ResettableService.php
│        │  │  │  │     │  └─ UnusedPrivateService.php
│        │  │  │  │     └─ TransDebug
│        │  │  │  │        ├─ TransConstructArgService.php
│        │  │  │  │        ├─ TransMethodCallsService.php
│        │  │  │  │        ├─ TransPropertyService.php
│        │  │  │  │        └─ TransSubscriberService.php
│        │  │  │  ├─ BundlePathsTest.php
│        │  │  │  ├─ CacheAttributeListenerTest.php
│        │  │  │  ├─ CachePoolClearCommandTest.php
│        │  │  │  ├─ CachePoolListCommandTest.php
│        │  │  │  ├─ CachePoolsTest.php
│        │  │  │  ├─ ConfigDebugCommandTest.php
│        │  │  │  ├─ ConfigDumpReferenceCommandTest.php
│        │  │  │  ├─ ContainerDebugCommandTest.php
│        │  │  │  ├─ ContainerDumpTest.php
│        │  │  │  ├─ DebugAutowiringCommandTest.php
│        │  │  │  ├─ Extension
│        │  │  │  │  └─ TestDumpExtension.php
│        │  │  │  ├─ Fixtures
│        │  │  │  │  └─ describe_env_vars.txt
│        │  │  │  ├─ FragmentTest.php
│        │  │  │  ├─ HttpClientTest.php
│        │  │  │  ├─ JsonStreamerTest.php
│        │  │  │  ├─ MailerTest.php
│        │  │  │  ├─ NotificationTest.php
│        │  │  │  ├─ ObjectMapperTest.php
│        │  │  │  ├─ ProfilerTest.php
│        │  │  │  ├─ PropertyInfoTest.php
│        │  │  │  ├─ Psr4RoutingTest.php
│        │  │  │  ├─ RouterDebugCommandTest.php
│        │  │  │  ├─ RoutingConditionServiceTest.php
│        │  │  │  ├─ SchedulerTest.php
│        │  │  │  ├─ SecurityTest.php
│        │  │  │  ├─ SerializerTest.php
│        │  │  │  ├─ SessionTest.php
│        │  │  │  ├─ SluggerLocaleAwareTest.php
│        │  │  │  ├─ SubRequestsTest.php
│        │  │  │  ├─ TestServiceContainerTest.php
│        │  │  │  ├─ TranslationDebugCommandTest.php
│        │  │  │  ├─ TypeInfoTest.php
│        │  │  │  └─ UidTest.php
│        │  │  ├─ Kernel
│        │  │  │  ├─ ConcreteMicroKernel.php
│        │  │  │  ├─ default
│        │  │  │  │  ├─ config
│        │  │  │  │  │  ├─ bundles.php
│        │  │  │  │  │  ├─ routes.yaml
│        │  │  │  │  │  └─ services.yaml
│        │  │  │  │  └─ src
│        │  │  │  │     └─ DefaultKernel.php
│        │  │  │  ├─ flex-style
│        │  │  │  │  ├─ config
│        │  │  │  │  │  └─ bundles.php
│        │  │  │  │  └─ src
│        │  │  │  │     └─ FlexStyleMicroKernel.php
│        │  │  │  ├─ KernelCommand.php
│        │  │  │  ├─ MicroKernelTraitTest.php
│        │  │  │  └─ SimpleKernel.php
│        │  │  ├─ KernelBrowserTest.php
│        │  │  ├─ Routing
│        │  │  │  ├─ DelegatingLoaderTest.php
│        │  │  │  ├─ Fixtures
│        │  │  │  │  └─ with_condition.yaml
│        │  │  │  ├─ RedirectableCompiledUrlMatcherTest.php
│        │  │  │  └─ RouterTest.php
│        │  │  ├─ Secrets
│        │  │  │  ├─ DotenvVaultTest.php
│        │  │  │  └─ SodiumVaultTest.php
│        │  │  ├─ Test
│        │  │  │  ├─ TestBrowserTokenTest.php
│        │  │  │  └─ WebTestCaseTest.php
│        │  │  ├─ TestCase.php
│        │  │  └─ Translation
│        │  │     └─ TranslatorTest.php
│        │  └─ Translation
│        │     └─ Translator.php
│        ├─ http-foundation
│        │  ├─ AcceptHeader.php
│        │  ├─ AcceptHeaderItem.php
│        │  ├─ BinaryFileResponse.php
│        │  ├─ ChainRequestMatcher.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ Cookie.php
│        │  ├─ EventStreamResponse.php
│        │  ├─ Exception
│        │  │  ├─ BadRequestException.php
│        │  │  ├─ ConflictingHeadersException.php
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ ExpiredSignedUriException.php
│        │  │  ├─ JsonException.php
│        │  │  ├─ LogicException.php
│        │  │  ├─ RequestExceptionInterface.php
│        │  │  ├─ SessionNotFoundException.php
│        │  │  ├─ SignedUriException.php
│        │  │  ├─ SuspiciousOperationException.php
│        │  │  ├─ UnexpectedValueException.php
│        │  │  ├─ UnsignedUriException.php
│        │  │  └─ UnverifiedSignedUriException.php
│        │  ├─ File
│        │  │  ├─ Exception
│        │  │  │  ├─ AccessDeniedException.php
│        │  │  │  ├─ CannotWriteFileException.php
│        │  │  │  ├─ ExtensionFileException.php
│        │  │  │  ├─ FileException.php
│        │  │  │  ├─ FileNotFoundException.php
│        │  │  │  ├─ FormSizeFileException.php
│        │  │  │  ├─ IniSizeFileException.php
│        │  │  │  ├─ NoFileException.php
│        │  │  │  ├─ NoTmpDirFileException.php
│        │  │  │  ├─ PartialFileException.php
│        │  │  │  ├─ UnexpectedTypeException.php
│        │  │  │  └─ UploadException.php
│        │  │  ├─ File.php
│        │  │  ├─ Stream.php
│        │  │  └─ UploadedFile.php
│        │  ├─ FileBag.php
│        │  ├─ HeaderBag.php
│        │  ├─ HeaderUtils.php
│        │  ├─ InputBag.php
│        │  ├─ IpUtils.php
│        │  ├─ JsonResponse.php
│        │  ├─ LICENSE
│        │  ├─ ParameterBag.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ RateLimiter
│        │  │  ├─ AbstractRequestRateLimiter.php
│        │  │  ├─ PeekableRequestRateLimiterInterface.php
│        │  │  └─ RequestRateLimiterInterface.php
│        │  ├─ README.md
│        │  ├─ RedirectResponse.php
│        │  ├─ Request.php
│        │  ├─ RequestMatcher
│        │  │  ├─ AttributesRequestMatcher.php
│        │  │  ├─ ExpressionRequestMatcher.php
│        │  │  ├─ HeaderRequestMatcher.php
│        │  │  ├─ HostRequestMatcher.php
│        │  │  ├─ IpsRequestMatcher.php
│        │  │  ├─ IsJsonRequestMatcher.php
│        │  │  ├─ MethodRequestMatcher.php
│        │  │  ├─ PathRequestMatcher.php
│        │  │  ├─ PortRequestMatcher.php
│        │  │  ├─ QueryParameterRequestMatcher.php
│        │  │  └─ SchemeRequestMatcher.php
│        │  ├─ RequestMatcherInterface.php
│        │  ├─ RequestStack.php
│        │  ├─ Response.php
│        │  ├─ ResponseHeaderBag.php
│        │  ├─ ServerBag.php
│        │  ├─ ServerEvent.php
│        │  ├─ Session
│        │  │  ├─ Attribute
│        │  │  │  ├─ AttributeBag.php
│        │  │  │  └─ AttributeBagInterface.php
│        │  │  ├─ Flash
│        │  │  │  ├─ AutoExpireFlashBag.php
│        │  │  │  ├─ FlashBag.php
│        │  │  │  └─ FlashBagInterface.php
│        │  │  ├─ FlashBagAwareSessionInterface.php
│        │  │  ├─ Session.php
│        │  │  ├─ SessionBagInterface.php
│        │  │  ├─ SessionBagProxy.php
│        │  │  ├─ SessionFactory.php
│        │  │  ├─ SessionFactoryInterface.php
│        │  │  ├─ SessionInterface.php
│        │  │  ├─ SessionUtils.php
│        │  │  └─ Storage
│        │  │     ├─ Handler
│        │  │     │  ├─ AbstractSessionHandler.php
│        │  │     │  ├─ IdentityMarshaller.php
│        │  │     │  ├─ MarshallingSessionHandler.php
│        │  │     │  ├─ MemcachedSessionHandler.php
│        │  │     │  ├─ MigratingSessionHandler.php
│        │  │     │  ├─ MongoDbSessionHandler.php
│        │  │     │  ├─ NativeFileSessionHandler.php
│        │  │     │  ├─ NullSessionHandler.php
│        │  │     │  ├─ PdoSessionHandler.php
│        │  │     │  ├─ RedisSessionHandler.php
│        │  │     │  ├─ SessionHandlerFactory.php
│        │  │     │  └─ StrictSessionHandler.php
│        │  │     ├─ MetadataBag.php
│        │  │     ├─ MockArraySessionStorage.php
│        │  │     ├─ MockFileSessionStorage.php
│        │  │     ├─ MockFileSessionStorageFactory.php
│        │  │     ├─ NativeSessionStorage.php
│        │  │     ├─ NativeSessionStorageFactory.php
│        │  │     ├─ PhpBridgeSessionStorage.php
│        │  │     ├─ PhpBridgeSessionStorageFactory.php
│        │  │     ├─ Proxy
│        │  │     │  ├─ AbstractProxy.php
│        │  │     │  └─ SessionHandlerProxy.php
│        │  │     ├─ SessionStorageFactoryInterface.php
│        │  │     └─ SessionStorageInterface.php
│        │  ├─ StreamedJsonResponse.php
│        │  ├─ StreamedResponse.php
│        │  ├─ Test
│        │  │  └─ Constraint
│        │  │     ├─ RequestAttributeValueSame.php
│        │  │     ├─ ResponseCookieValueSame.php
│        │  │     ├─ ResponseFormatSame.php
│        │  │     ├─ ResponseHasCookie.php
│        │  │     ├─ ResponseHasHeader.php
│        │  │     ├─ ResponseHeaderLocationSame.php
│        │  │     ├─ ResponseHeaderSame.php
│        │  │     ├─ ResponseIsRedirected.php
│        │  │     ├─ ResponseIsSuccessful.php
│        │  │     ├─ ResponseIsUnprocessable.php
│        │  │     └─ ResponseStatusCodeSame.php
│        │  ├─ Tests
│        │  │  ├─ AcceptHeaderItemTest.php
│        │  │  ├─ AcceptHeaderTest.php
│        │  │  ├─ BinaryFileResponseTest.php
│        │  │  ├─ CookieTest.php
│        │  │  ├─ EventStreamResponseTest.php
│        │  │  ├─ File
│        │  │  │  ├─ FakeFile.php
│        │  │  │  ├─ FileTest.php
│        │  │  │  ├─ Fixtures
│        │  │  │  │  ├─ -test
│        │  │  │  │  ├─ .unknownextension
│        │  │  │  │  ├─ case-sensitive-mime-type.xlsm
│        │  │  │  │  ├─ directory
│        │  │  │  │  │  └─ .empty
│        │  │  │  │  ├─ other-file.example
│        │  │  │  │  ├─ test
│        │  │  │  │  ├─ test.gif
│        │  │  │  │  └─ webkitdirectory
│        │  │  │  │     ├─ nested
│        │  │  │  │     │  └─ test.txt
│        │  │  │  │     └─ test.txt
│        │  │  │  └─ UploadedFileTest.php
│        │  │  ├─ FileBagTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ FooEnum.php
│        │  │  │  ├─ response-functional
│        │  │  │  │  ├─ common.inc
│        │  │  │  │  ├─ cookie_raw_urlencode.expected
│        │  │  │  │  ├─ cookie_raw_urlencode.php
│        │  │  │  │  ├─ cookie_samesite_lax.expected
│        │  │  │  │  ├─ cookie_samesite_lax.php
│        │  │  │  │  ├─ cookie_samesite_strict.expected
│        │  │  │  │  ├─ cookie_samesite_strict.php
│        │  │  │  │  ├─ cookie_urlencode.expected
│        │  │  │  │  ├─ cookie_urlencode.php
│        │  │  │  │  ├─ deleted_cookie.expected
│        │  │  │  │  ├─ deleted_cookie.php
│        │  │  │  │  ├─ early_hints.php
│        │  │  │  │  ├─ invalid_cookie_name.expected
│        │  │  │  │  └─ invalid_cookie_name.php
│        │  │  │  └─ xml
│        │  │  │     └─ http-status-codes.xml
│        │  │  ├─ HeaderBagTest.php
│        │  │  ├─ HeaderUtilsTest.php
│        │  │  ├─ InputBagTest.php
│        │  │  ├─ IpUtilsTest.php
│        │  │  ├─ JsonResponseTest.php
│        │  │  ├─ ParameterBagTest.php
│        │  │  ├─ RateLimiter
│        │  │  │  ├─ AbstractRequestRateLimiterTest.php
│        │  │  │  └─ MockAbstractRequestRateLimiter.php
│        │  │  ├─ RedirectResponseTest.php
│        │  │  ├─ RequestMatcher
│        │  │  │  ├─ AttributesRequestMatcherTest.php
│        │  │  │  ├─ ExpressionRequestMatcherTest.php
│        │  │  │  ├─ HeaderRequestMatcherTest.php
│        │  │  │  ├─ HostRequestMatcherTest.php
│        │  │  │  ├─ IpsRequestMatcherTest.php
│        │  │  │  ├─ IsJsonRequestMatcherTest.php
│        │  │  │  ├─ MethodRequestMatcherTest.php
│        │  │  │  ├─ PathRequestMatcherTest.php
│        │  │  │  ├─ PortRequestMatcherTest.php
│        │  │  │  ├─ QueryParameterRequestMatcherTest.php
│        │  │  │  └─ SchemeRequestMatcherTest.php
│        │  │  ├─ RequestStackTest.php
│        │  │  ├─ RequestTest.php
│        │  │  ├─ ResponseFunctionalTest.php
│        │  │  ├─ ResponseHeaderBagTest.php
│        │  │  ├─ ResponseTest.php
│        │  │  ├─ ResponseTestCase.php
│        │  │  ├─ schema
│        │  │  │  ├─ http-status-codes.rng
│        │  │  │  └─ iana-registry.rng
│        │  │  ├─ ServerBagTest.php
│        │  │  ├─ Session
│        │  │  │  ├─ Attribute
│        │  │  │  │  └─ AttributeBagTest.php
│        │  │  │  ├─ Flash
│        │  │  │  │  ├─ AutoExpireFlashBagTest.php
│        │  │  │  │  └─ FlashBagTest.php
│        │  │  │  ├─ SessionTest.php
│        │  │  │  └─ Storage
│        │  │  │     ├─ Handler
│        │  │  │     │  ├─ AbstractRedisSessionHandlerTestCase.php
│        │  │  │     │  ├─ AbstractSessionHandlerTest.php
│        │  │  │     │  ├─ Fixtures
│        │  │  │     │  │  ├─ common.inc
│        │  │  │     │  │  ├─ empty_destroys.expected
│        │  │  │     │  │  ├─ empty_destroys.php
│        │  │  │     │  │  ├─ invalid_regenerate.expected
│        │  │  │     │  │  ├─ invalid_regenerate.php
│        │  │  │     │  │  ├─ read_only.expected
│        │  │  │     │  │  ├─ read_only.php
│        │  │  │     │  │  ├─ regenerate.expected
│        │  │  │     │  │  ├─ regenerate.php
│        │  │  │     │  │  ├─ storage.expected
│        │  │  │     │  │  ├─ storage.php
│        │  │  │     │  │  ├─ with_cookie.expected
│        │  │  │     │  │  ├─ with_cookie.php
│        │  │  │     │  │  ├─ with_cookie_and_session.expected
│        │  │  │     │  │  ├─ with_cookie_and_session.php
│        │  │  │     │  │  ├─ with_samesite.expected
│        │  │  │     │  │  ├─ with_samesite.php
│        │  │  │     │  │  ├─ with_samesite_and_migration.expected
│        │  │  │     │  │  └─ with_samesite_and_migration.php
│        │  │  │     │  ├─ IdentityMarshallerTest.php
│        │  │  │     │  ├─ MarshallingSessionHandlerTest.php
│        │  │  │     │  ├─ MemcachedSessionHandlerTest.php
│        │  │  │     │  ├─ MigratingSessionHandlerTest.php
│        │  │  │     │  ├─ MongoDbSessionHandlerTest.php
│        │  │  │     │  ├─ NativeFileSessionHandlerTest.php
│        │  │  │     │  ├─ NullSessionHandlerTest.php
│        │  │  │     │  ├─ PdoSessionHandlerTest.php
│        │  │  │     │  ├─ PredisClusterSessionHandlerTest.php
│        │  │  │     │  ├─ PredisSessionHandlerTest.php
│        │  │  │     │  ├─ RedisArraySessionHandlerTest.php
│        │  │  │     │  ├─ RedisClusterSessionHandlerTest.php
│        │  │  │     │  ├─ RedisSessionHandlerTest.php
│        │  │  │     │  ├─ RelaySessionHandlerTest.php
│        │  │  │     │  ├─ SessionHandlerFactoryTest.php
│        │  │  │     │  ├─ StrictSessionHandlerTest.php
│        │  │  │     │  └─ stubs
│        │  │  │     │     └─ mongodb.php
│        │  │  │     ├─ MetadataBagTest.php
│        │  │  │     ├─ MockArraySessionStorageTest.php
│        │  │  │     ├─ MockFileSessionStorageTest.php
│        │  │  │     ├─ NativeSessionStorageTest.php
│        │  │  │     ├─ PhpBridgeSessionStorageTest.php
│        │  │  │     └─ Proxy
│        │  │  │        ├─ AbstractProxyTest.php
│        │  │  │        └─ SessionHandlerProxyTest.php
│        │  │  ├─ StreamedJsonResponseTest.php
│        │  │  ├─ StreamedResponseTest.php
│        │  │  ├─ Test
│        │  │  │  └─ Constraint
│        │  │  │     ├─ RequestAttributeValueSameTest.php
│        │  │  │     ├─ ResponseCookieValueSameTest.php
│        │  │  │     ├─ ResponseFormatSameTest.php
│        │  │  │     ├─ ResponseHasCookieTest.php
│        │  │  │     ├─ ResponseHasHeaderTest.php
│        │  │  │     ├─ ResponseHeaderLocationSameTest.php
│        │  │  │     ├─ ResponseHeaderSameTest.php
│        │  │  │     ├─ ResponseIsRedirectedTest.php
│        │  │  │     ├─ ResponseIsSuccessfulTest.php
│        │  │  │     ├─ ResponseIsUnprocessableTest.php
│        │  │  │     └─ ResponseStatusCodeSameTest.php
│        │  │  ├─ UriSignerTest.php
│        │  │  └─ UrlHelperTest.php
│        │  ├─ UriSigner.php
│        │  └─ UrlHelper.php
│        ├─ http-kernel
│        │  ├─ Attribute
│        │  │  ├─ AsController.php
│        │  │  ├─ AsTargetedValueResolver.php
│        │  │  ├─ Cache.php
│        │  │  ├─ MapDateTime.php
│        │  │  ├─ MapQueryParameter.php
│        │  │  ├─ MapQueryString.php
│        │  │  ├─ MapRequestPayload.php
│        │  │  ├─ MapUploadedFile.php
│        │  │  ├─ ValueResolver.php
│        │  │  ├─ WithHttpStatus.php
│        │  │  └─ WithLogLevel.php
│        │  ├─ Bundle
│        │  │  ├─ AbstractBundle.php
│        │  │  ├─ Bundle.php
│        │  │  ├─ BundleExtension.php
│        │  │  └─ BundleInterface.php
│        │  ├─ CacheClearer
│        │  │  ├─ CacheClearerInterface.php
│        │  │  ├─ ChainCacheClearer.php
│        │  │  └─ Psr6CacheClearer.php
│        │  ├─ CacheWarmer
│        │  │  ├─ CacheWarmer.php
│        │  │  ├─ CacheWarmerAggregate.php
│        │  │  ├─ CacheWarmerInterface.php
│        │  │  └─ WarmableInterface.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ Config
│        │  │  └─ FileLocator.php
│        │  ├─ Controller
│        │  │  ├─ ArgumentResolver
│        │  │  │  ├─ BackedEnumValueResolver.php
│        │  │  │  ├─ DateTimeValueResolver.php
│        │  │  │  ├─ DefaultValueResolver.php
│        │  │  │  ├─ NotTaggedControllerValueResolver.php
│        │  │  │  ├─ QueryParameterValueResolver.php
│        │  │  │  ├─ RequestAttributeValueResolver.php
│        │  │  │  ├─ RequestPayloadValueResolver.php
│        │  │  │  ├─ RequestValueResolver.php
│        │  │  │  ├─ ServiceValueResolver.php
│        │  │  │  ├─ SessionValueResolver.php
│        │  │  │  ├─ TraceableValueResolver.php
│        │  │  │  ├─ UidValueResolver.php
│        │  │  │  └─ VariadicValueResolver.php
│        │  │  ├─ ArgumentResolver.php
│        │  │  ├─ ArgumentResolverInterface.php
│        │  │  ├─ ContainerControllerResolver.php
│        │  │  ├─ ControllerReference.php
│        │  │  ├─ ControllerResolver.php
│        │  │  ├─ ControllerResolverInterface.php
│        │  │  ├─ ErrorController.php
│        │  │  ├─ TraceableArgumentResolver.php
│        │  │  ├─ TraceableControllerResolver.php
│        │  │  └─ ValueResolverInterface.php
│        │  ├─ ControllerMetadata
│        │  │  ├─ ArgumentMetadata.php
│        │  │  ├─ ArgumentMetadataFactory.php
│        │  │  └─ ArgumentMetadataFactoryInterface.php
│        │  ├─ DataCollector
│        │  │  ├─ AjaxDataCollector.php
│        │  │  ├─ ConfigDataCollector.php
│        │  │  ├─ DataCollector.php
│        │  │  ├─ DataCollectorInterface.php
│        │  │  ├─ DumpDataCollector.php
│        │  │  ├─ EventDataCollector.php
│        │  │  ├─ ExceptionDataCollector.php
│        │  │  ├─ LateDataCollectorInterface.php
│        │  │  ├─ LoggerDataCollector.php
│        │  │  ├─ MemoryDataCollector.php
│        │  │  ├─ RequestDataCollector.php
│        │  │  ├─ RouterDataCollector.php
│        │  │  └─ TimeDataCollector.php
│        │  ├─ Debug
│        │  │  ├─ ErrorHandlerConfigurator.php
│        │  │  ├─ TraceableEventDispatcher.php
│        │  │  └─ VirtualRequestStack.php
│        │  ├─ DependencyInjection
│        │  │  ├─ AddAnnotatedClassesToCachePass.php
│        │  │  ├─ ConfigurableExtension.php
│        │  │  ├─ ControllerArgumentValueResolverPass.php
│        │  │  ├─ Extension.php
│        │  │  ├─ FragmentRendererPass.php
│        │  │  ├─ LazyLoadingFragmentHandler.php
│        │  │  ├─ LoggerPass.php
│        │  │  ├─ MergeExtensionConfigurationPass.php
│        │  │  ├─ RegisterControllerArgumentLocatorsPass.php
│        │  │  ├─ RegisterLocaleAwareServicesPass.php
│        │  │  ├─ RemoveEmptyControllerArgumentLocatorsPass.php
│        │  │  ├─ ResettableServicePass.php
│        │  │  ├─ ServicesResetter.php
│        │  │  └─ ServicesResetterInterface.php
│        │  ├─ Event
│        │  │  ├─ ControllerArgumentsEvent.php
│        │  │  ├─ ControllerEvent.php
│        │  │  ├─ ExceptionEvent.php
│        │  │  ├─ FinishRequestEvent.php
│        │  │  ├─ KernelEvent.php
│        │  │  ├─ RequestEvent.php
│        │  │  ├─ ResponseEvent.php
│        │  │  ├─ TerminateEvent.php
│        │  │  └─ ViewEvent.php
│        │  ├─ EventListener
│        │  │  ├─ AbstractSessionListener.php
│        │  │  ├─ AddRequestFormatsListener.php
│        │  │  ├─ CacheAttributeListener.php
│        │  │  ├─ DebugHandlersListener.php
│        │  │  ├─ DisallowRobotsIndexingListener.php
│        │  │  ├─ DumpListener.php
│        │  │  ├─ ErrorListener.php
│        │  │  ├─ FragmentListener.php
│        │  │  ├─ LocaleAwareListener.php
│        │  │  ├─ LocaleListener.php
│        │  │  ├─ ProfilerListener.php
│        │  │  ├─ ResponseListener.php
│        │  │  ├─ RouterListener.php
│        │  │  ├─ SessionListener.php
│        │  │  ├─ SurrogateListener.php
│        │  │  └─ ValidateRequestListener.php
│        │  ├─ Exception
│        │  │  ├─ AccessDeniedHttpException.php
│        │  │  ├─ BadRequestHttpException.php
│        │  │  ├─ ConflictHttpException.php
│        │  │  ├─ ControllerDoesNotReturnResponseException.php
│        │  │  ├─ GoneHttpException.php
│        │  │  ├─ HttpException.php
│        │  │  ├─ HttpExceptionInterface.php
│        │  │  ├─ InvalidMetadataException.php
│        │  │  ├─ LengthRequiredHttpException.php
│        │  │  ├─ LockedHttpException.php
│        │  │  ├─ MethodNotAllowedHttpException.php
│        │  │  ├─ NearMissValueResolverException.php
│        │  │  ├─ NotAcceptableHttpException.php
│        │  │  ├─ NotFoundHttpException.php
│        │  │  ├─ PreconditionFailedHttpException.php
│        │  │  ├─ PreconditionRequiredHttpException.php
│        │  │  ├─ ResolverNotFoundException.php
│        │  │  ├─ ServiceUnavailableHttpException.php
│        │  │  ├─ TooManyRequestsHttpException.php
│        │  │  ├─ UnauthorizedHttpException.php
│        │  │  ├─ UnexpectedSessionUsageException.php
│        │  │  ├─ UnprocessableEntityHttpException.php
│        │  │  └─ UnsupportedMediaTypeHttpException.php
│        │  ├─ Fragment
│        │  │  ├─ AbstractSurrogateFragmentRenderer.php
│        │  │  ├─ EsiFragmentRenderer.php
│        │  │  ├─ FragmentHandler.php
│        │  │  ├─ FragmentRendererInterface.php
│        │  │  ├─ FragmentUriGenerator.php
│        │  │  ├─ FragmentUriGeneratorInterface.php
│        │  │  ├─ HIncludeFragmentRenderer.php
│        │  │  ├─ InlineFragmentRenderer.php
│        │  │  ├─ RoutableFragmentRenderer.php
│        │  │  └─ SsiFragmentRenderer.php
│        │  ├─ HttpCache
│        │  │  ├─ AbstractSurrogate.php
│        │  │  ├─ Esi.php
│        │  │  ├─ HttpCache.php
│        │  │  ├─ ResponseCacheStrategy.php
│        │  │  ├─ ResponseCacheStrategyInterface.php
│        │  │  ├─ Ssi.php
│        │  │  ├─ Store.php
│        │  │  ├─ StoreInterface.php
│        │  │  ├─ SubRequestHandler.php
│        │  │  └─ SurrogateInterface.php
│        │  ├─ HttpClientKernel.php
│        │  ├─ HttpKernel.php
│        │  ├─ HttpKernelBrowser.php
│        │  ├─ HttpKernelInterface.php
│        │  ├─ Kernel.php
│        │  ├─ KernelEvents.php
│        │  ├─ KernelInterface.php
│        │  ├─ LICENSE
│        │  ├─ Log
│        │  │  ├─ DebugLoggerConfigurator.php
│        │  │  ├─ DebugLoggerInterface.php
│        │  │  └─ Logger.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ Profiler
│        │  │  ├─ FileProfilerStorage.php
│        │  │  ├─ Profile.php
│        │  │  ├─ Profiler.php
│        │  │  ├─ ProfilerStateChecker.php
│        │  │  └─ ProfilerStorageInterface.php
│        │  ├─ README.md
│        │  ├─ RebootableInterface.php
│        │  ├─ Resources
│        │  │  └─ welcome.html.php
│        │  ├─ TerminableInterface.php
│        │  └─ Tests
│        │     ├─ Attribute
│        │     │  └─ WithLogLevelTest.php
│        │     ├─ Bundle
│        │     │  └─ BundleTest.php
│        │     ├─ CacheClearer
│        │     │  ├─ ChainCacheClearerTest.php
│        │     │  └─ Psr6CacheClearerTest.php
│        │     ├─ CacheWarmer
│        │     │  ├─ CacheWarmerAggregateTest.php
│        │     │  └─ CacheWarmerTest.php
│        │     ├─ Config
│        │     │  └─ FileLocatorTest.php
│        │     ├─ Controller
│        │     │  ├─ ArgumentResolver
│        │     │  │  ├─ BackedEnumValueResolverTest.php
│        │     │  │  ├─ DateTimeValueResolverTest.php
│        │     │  │  ├─ NotTaggedControllerValueResolverTest.php
│        │     │  │  ├─ QueryParameterValueResolverTest.php
│        │     │  │  ├─ RequestPayloadValueResolverTest.php
│        │     │  │  ├─ RequestValueResolverTest.php
│        │     │  │  ├─ ServiceValueResolverTest.php
│        │     │  │  ├─ TraceableValueResolverTest.php
│        │     │  │  ├─ UidValueResolverTest.php
│        │     │  │  └─ UploadedFileValueResolverTest.php
│        │     │  ├─ ArgumentResolverTest.php
│        │     │  ├─ ContainerControllerResolverTest.php
│        │     │  ├─ ControllerResolverTest.php
│        │     │  ├─ ErrorControllerTest.php
│        │     │  ├─ TraceableArgumentResolverTest.php
│        │     │  └─ TraceableControllerResolverTest.php
│        │     ├─ ControllerMetadata
│        │     │  ├─ ArgumentMetadataFactoryTest.php
│        │     │  └─ ArgumentMetadataTest.php
│        │     ├─ DataCollector
│        │     │  ├─ Compiler.log
│        │     │  ├─ ConfigDataCollectorTest.php
│        │     │  ├─ DataCollectorTest.php
│        │     │  ├─ DumpDataCollectorTest.php
│        │     │  ├─ ExceptionDataCollectorTest.php
│        │     │  ├─ LoggerDataCollectorTest.php
│        │     │  ├─ MemoryDataCollectorTest.php
│        │     │  ├─ RequestDataCollectorTest.php
│        │     │  ├─ RouterDataCollectorTest.php
│        │     │  └─ TimeDataCollectorTest.php
│        │     ├─ Debug
│        │     │  ├─ ErrorHandlerConfiguratorTest.php
│        │     │  └─ TraceableEventDispatcherTest.php
│        │     ├─ DependencyInjection
│        │     │  ├─ AddAnnotatedClassesToCachePassTest.php
│        │     │  ├─ ControllerArgumentValueResolverPassTest.php
│        │     │  ├─ FragmentRendererPassTest.php
│        │     │  ├─ LazyLoadingFragmentHandlerTest.php
│        │     │  ├─ LoggerPassTest.php
│        │     │  ├─ MergeExtensionConfigurationPassTest.php
│        │     │  ├─ RegisterControllerArgumentLocatorsPassTest.php
│        │     │  ├─ RegisterLocaleAwareServicesPassTest.php
│        │     │  ├─ RemoveEmptyControllerArgumentLocatorsPassTest.php
│        │     │  ├─ ResettableServicePassTest.php
│        │     │  └─ ServicesResetterTest.php
│        │     ├─ Event
│        │     │  ├─ ControllerArgumentsEventTest.php
│        │     │  ├─ ControllerEventTest.php
│        │     │  └─ ExceptionEventTest.php
│        │     ├─ EventListener
│        │     │  ├─ AddRequestFormatsListenerTest.php
│        │     │  ├─ CacheAttributeListenerTest.php
│        │     │  ├─ DebugHandlersListenerTest.php
│        │     │  ├─ DisallowRobotsIndexingListenerTest.php
│        │     │  ├─ DumpListenerTest.php
│        │     │  ├─ ErrorListenerTest.php
│        │     │  ├─ FragmentListenerTest.php
│        │     │  ├─ LocaleAwareListenerTest.php
│        │     │  ├─ LocaleListenerTest.php
│        │     │  ├─ ProfilerListenerTest.php
│        │     │  ├─ ResponseListenerTest.php
│        │     │  ├─ RouterListenerTest.php
│        │     │  ├─ SessionListenerTest.php
│        │     │  ├─ SurrogateListenerTest.php
│        │     │  └─ ValidateRequestListenerTest.php
│        │     ├─ Exception
│        │     │  ├─ AccessDeniedHttpExceptionTest.php
│        │     │  ├─ BadRequestHttpExceptionTest.php
│        │     │  ├─ ConflictHttpExceptionTest.php
│        │     │  ├─ GoneHttpExceptionTest.php
│        │     │  ├─ HttpExceptionTest.php
│        │     │  ├─ LengthRequiredHttpExceptionTest.php
│        │     │  ├─ LockedHttpExceptionTest.php
│        │     │  ├─ MethodNotAllowedHttpExceptionTest.php
│        │     │  ├─ NotAcceptableHttpExceptionTest.php
│        │     │  ├─ NotFoundHttpExceptionTest.php
│        │     │  ├─ PreconditionFailedHttpExceptionTest.php
│        │     │  ├─ PreconditionRequiredHttpExceptionTest.php
│        │     │  ├─ ServiceUnavailableHttpExceptionTest.php
│        │     │  ├─ TooManyRequestsHttpExceptionTest.php
│        │     │  ├─ UnauthorizedHttpExceptionTest.php
│        │     │  ├─ UnprocessableEntityHttpExceptionTest.php
│        │     │  └─ UnsupportedMediaTypeHttpExceptionTest.php
│        │     ├─ Fixtures
│        │     │  ├─ AcmeFooBundle
│        │     │  │  ├─ AcmeFooBundle.php
│        │     │  │  └─ Resources
│        │     │  │     └─ config
│        │     │  │        ├─ definition.php
│        │     │  │        └─ services.php
│        │     │  ├─ Attribute
│        │     │  │  ├─ Bar.php
│        │     │  │  ├─ Baz.php
│        │     │  │  └─ Foo.php
│        │     │  ├─ Bundle1Bundle
│        │     │  │  ├─ foo.txt
│        │     │  │  └─ Resources
│        │     │  ├─ ClearableService.php
│        │     │  ├─ Controller
│        │     │  │  ├─ ArgumentResolver
│        │     │  │  │  └─ UploadedFile
│        │     │  │  │     ├─ file-big.txt
│        │     │  │  │     └─ file-small.txt
│        │     │  │  ├─ AttributeController.php
│        │     │  │  ├─ BasicTypesController.php
│        │     │  │  ├─ CacheAttributeController.php
│        │     │  │  ├─ ExtendingRequest.php
│        │     │  │  ├─ ExtendingSession.php
│        │     │  │  ├─ NullableController.php
│        │     │  │  └─ VariadicController.php
│        │     │  ├─ DataCollector
│        │     │  │  ├─ CloneVarDataCollector.php
│        │     │  │  └─ DummyController.php
│        │     │  ├─ ExtensionNotValidBundle
│        │     │  │  ├─ DependencyInjection
│        │     │  │  │  └─ ExtensionNotValidExtension.php
│        │     │  │  └─ ExtensionNotValidBundle.php
│        │     │  ├─ ExtensionPresentBundle
│        │     │  │  ├─ DependencyInjection
│        │     │  │  │  └─ ExtensionPresentExtension.php
│        │     │  │  └─ ExtensionPresentBundle.php
│        │     │  ├─ IntEnum.php
│        │     │  ├─ KernelWithoutBundles.php
│        │     │  ├─ LazyResettableService.php
│        │     │  ├─ MockableUploadFileWithClientSize.php
│        │     │  ├─ MultiResettableService.php
│        │     │  ├─ ResettableService.php
│        │     │  ├─ Suit.php
│        │     │  ├─ TestClient.php
│        │     │  ├─ UsePropertyInDestruct.php
│        │     │  └─ WithPublicObjectProperty.php
│        │     ├─ Fragment
│        │     │  ├─ EsiFragmentRendererTest.php
│        │     │  ├─ FragmentHandlerTest.php
│        │     │  ├─ HIncludeFragmentRendererTest.php
│        │     │  ├─ InlineFragmentRendererTest.php
│        │     │  ├─ RoutableFragmentRendererTest.php
│        │     │  └─ SsiFragmentRendererTest.php
│        │     ├─ HttpCache
│        │     │  ├─ EsiTest.php
│        │     │  ├─ HttpCacheTest.php
│        │     │  ├─ HttpCacheTestCase.php
│        │     │  ├─ ResponseCacheStrategyTest.php
│        │     │  ├─ SsiTest.php
│        │     │  ├─ StoreTest.php
│        │     │  ├─ SubRequestHandlerTest.php
│        │     │  ├─ TestHttpKernel.php
│        │     │  └─ TestMultipleHttpKernel.php
│        │     ├─ HttpClientKernelTest.php
│        │     ├─ HttpKernelBrowserTest.php
│        │     ├─ HttpKernelTest.php
│        │     ├─ KernelTest.php
│        │     ├─ Log
│        │     │  └─ LoggerTest.php
│        │     ├─ Logger.php
│        │     ├─ Profiler
│        │     │  ├─ FileProfilerStorageTest.php
│        │     │  └─ ProfilerTest.php
│        │     └─ TestHttpKernel.php
│        ├─ polyfill-intl-grapheme
│        │  ├─ bootstrap.php
│        │  ├─ bootstrap80.php
│        │  ├─ composer.json
│        │  ├─ Grapheme.php
│        │  ├─ LICENSE
│        │  └─ README.md
│        ├─ polyfill-intl-normalizer
│        │  ├─ bootstrap.php
│        │  ├─ bootstrap80.php
│        │  ├─ composer.json
│        │  ├─ LICENSE
│        │  ├─ Normalizer.php
│        │  ├─ README.md
│        │  └─ Resources
│        │     ├─ stubs
│        │     │  └─ Normalizer.php
│        │     └─ unidata
│        │        ├─ canonicalComposition.php
│        │        ├─ canonicalDecomposition.php
│        │        ├─ combiningClass.php
│        │        └─ compatibilityDecomposition.php
│        ├─ polyfill-mbstring
│        │  ├─ bootstrap.php
│        │  ├─ bootstrap80.php
│        │  ├─ composer.json
│        │  ├─ LICENSE
│        │  ├─ Mbstring.php
│        │  ├─ README.md
│        │  └─ Resources
│        │     └─ unidata
│        │        ├─ caseFolding.php
│        │        ├─ lowerCase.php
│        │        ├─ titleCaseRegexp.php
│        │        └─ upperCase.php
│        ├─ polyfill-php83
│        │  ├─ bootstrap.php
│        │  ├─ bootstrap81.php
│        │  ├─ composer.json
│        │  ├─ LICENSE
│        │  ├─ Php83.php
│        │  ├─ README.md
│        │  └─ Resources
│        │     └─ stubs
│        │        ├─ DateError.php
│        │        ├─ DateException.php
│        │        ├─ DateInvalidOperationException.php
│        │        ├─ DateInvalidTimeZoneException.php
│        │        ├─ DateMalformedIntervalStringException.php
│        │        ├─ DateMalformedPeriodStringException.php
│        │        ├─ DateMalformedStringException.php
│        │        ├─ DateObjectError.php
│        │        ├─ DateRangeError.php
│        │        ├─ Override.php
│        │        └─ SQLite3Exception.php
│        ├─ routing
│        │  ├─ Alias.php
│        │  ├─ Annotation
│        │  │  └─ Route.php
│        │  ├─ Attribute
│        │  │  ├─ DeprecatedAlias.php
│        │  │  └─ Route.php
│        │  ├─ CHANGELOG.md
│        │  ├─ CompiledRoute.php
│        │  ├─ composer.json
│        │  ├─ DependencyInjection
│        │  │  ├─ AddExpressionLanguageProvidersPass.php
│        │  │  └─ RoutingResolverPass.php
│        │  ├─ Exception
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ InvalidArgumentException.php
│        │  │  ├─ InvalidParameterException.php
│        │  │  ├─ LogicException.php
│        │  │  ├─ MethodNotAllowedException.php
│        │  │  ├─ MissingMandatoryParametersException.php
│        │  │  ├─ NoConfigurationException.php
│        │  │  ├─ ResourceNotFoundException.php
│        │  │  ├─ RouteCircularReferenceException.php
│        │  │  ├─ RouteNotFoundException.php
│        │  │  └─ RuntimeException.php
│        │  ├─ Generator
│        │  │  ├─ CompiledUrlGenerator.php
│        │  │  ├─ ConfigurableRequirementsInterface.php
│        │  │  ├─ Dumper
│        │  │  │  ├─ CompiledUrlGeneratorDumper.php
│        │  │  │  ├─ GeneratorDumper.php
│        │  │  │  └─ GeneratorDumperInterface.php
│        │  │  ├─ UrlGenerator.php
│        │  │  └─ UrlGeneratorInterface.php
│        │  ├─ LICENSE
│        │  ├─ Loader
│        │  │  ├─ AttributeClassLoader.php
│        │  │  ├─ AttributeDirectoryLoader.php
│        │  │  ├─ AttributeFileLoader.php
│        │  │  ├─ ClosureLoader.php
│        │  │  ├─ Configurator
│        │  │  │  ├─ AliasConfigurator.php
│        │  │  │  ├─ CollectionConfigurator.php
│        │  │  │  ├─ ImportConfigurator.php
│        │  │  │  ├─ RouteConfigurator.php
│        │  │  │  ├─ RoutingConfigurator.php
│        │  │  │  └─ Traits
│        │  │  │     ├─ AddTrait.php
│        │  │  │     ├─ HostTrait.php
│        │  │  │     ├─ LocalizedRouteTrait.php
│        │  │  │     ├─ PrefixTrait.php
│        │  │  │     └─ RouteTrait.php
│        │  │  ├─ ContainerLoader.php
│        │  │  ├─ DirectoryLoader.php
│        │  │  ├─ GlobFileLoader.php
│        │  │  ├─ ObjectLoader.php
│        │  │  ├─ PhpFileLoader.php
│        │  │  ├─ Psr4DirectoryLoader.php
│        │  │  ├─ schema
│        │  │  │  └─ routing
│        │  │  │     └─ routing-1.0.xsd
│        │  │  ├─ XmlFileLoader.php
│        │  │  └─ YamlFileLoader.php
│        │  ├─ Matcher
│        │  │  ├─ CompiledUrlMatcher.php
│        │  │  ├─ Dumper
│        │  │  │  ├─ CompiledUrlMatcherDumper.php
│        │  │  │  ├─ CompiledUrlMatcherTrait.php
│        │  │  │  ├─ MatcherDumper.php
│        │  │  │  ├─ MatcherDumperInterface.php
│        │  │  │  └─ StaticPrefixCollection.php
│        │  │  ├─ ExpressionLanguageProvider.php
│        │  │  ├─ RedirectableUrlMatcher.php
│        │  │  ├─ RedirectableUrlMatcherInterface.php
│        │  │  ├─ RequestMatcherInterface.php
│        │  │  ├─ TraceableUrlMatcher.php
│        │  │  ├─ UrlMatcher.php
│        │  │  └─ UrlMatcherInterface.php
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ RequestContext.php
│        │  ├─ RequestContextAwareInterface.php
│        │  ├─ Requirement
│        │  │  ├─ EnumRequirement.php
│        │  │  └─ Requirement.php
│        │  ├─ Route.php
│        │  ├─ RouteCollection.php
│        │  ├─ RouteCompiler.php
│        │  ├─ RouteCompilerInterface.php
│        │  ├─ Router.php
│        │  ├─ RouterInterface.php
│        │  └─ Tests
│        │     ├─ Attribute
│        │     │  └─ RouteTest.php
│        │     ├─ CompiledRouteTest.php
│        │     ├─ DependencyInjection
│        │     │  ├─ AddExpressionLanguageProvidersPassTest.php
│        │     │  └─ RoutingResolverPassTest.php
│        │     ├─ Fixtures
│        │     │  ├─ alias
│        │     │  │  ├─ alias.php
│        │     │  │  ├─ alias.xml
│        │     │  │  ├─ alias.yaml
│        │     │  │  ├─ expected.php
│        │     │  │  ├─ invalid-alias.yaml
│        │     │  │  ├─ invalid-deprecated-no-package.xml
│        │     │  │  ├─ invalid-deprecated-no-package.yaml
│        │     │  │  ├─ invalid-deprecated-no-version.xml
│        │     │  │  ├─ invalid-deprecated-no-version.yaml
│        │     │  │  └─ override.yaml
│        │     │  ├─ annotated.php
│        │     │  ├─ AttributedClasses
│        │     │  │  ├─ AbstractClass.php
│        │     │  │  ├─ BarClass.php
│        │     │  │  ├─ BazClass.php
│        │     │  │  ├─ EncodingClass.php
│        │     │  │  ├─ FooClass.php
│        │     │  │  └─ FooTrait.php
│        │     │  ├─ AttributeFixtures
│        │     │  │  ├─ AbstractClassController.php
│        │     │  │  ├─ ActionPathController.php
│        │     │  │  ├─ AliasClassController.php
│        │     │  │  ├─ AliasInvokableController.php
│        │     │  │  ├─ AliasRouteController.php
│        │     │  │  ├─ BazClass.php
│        │     │  │  ├─ DefaultValueController.php
│        │     │  │  ├─ DeprecatedAliasCustomMessageRouteController.php
│        │     │  │  ├─ DeprecatedAliasRouteController.php
│        │     │  │  ├─ EncodingClass.php
│        │     │  │  ├─ ExplicitLocalizedActionPathController.php
│        │     │  │  ├─ ExtendedRoute.php
│        │     │  │  ├─ ExtendedRouteOnClassController.php
│        │     │  │  ├─ ExtendedRouteOnMethodController.php
│        │     │  │  ├─ FooController.php
│        │     │  │  ├─ GlobalDefaultsClass.php
│        │     │  │  ├─ InvokableController.php
│        │     │  │  ├─ InvokableFQCNAliasConflictController.php
│        │     │  │  ├─ InvokableLocalizedController.php
│        │     │  │  ├─ InvokableMethodController.php
│        │     │  │  ├─ LocalizedActionPathController.php
│        │     │  │  ├─ LocalizedMethodActionControllers.php
│        │     │  │  ├─ LocalizedPrefixLocalizedActionController.php
│        │     │  │  ├─ LocalizedPrefixMissingLocaleActionController.php
│        │     │  │  ├─ LocalizedPrefixMissingRouteLocaleActionController.php
│        │     │  │  ├─ LocalizedPrefixWithRouteWithoutLocale.php
│        │     │  │  ├─ MethodActionControllers.php
│        │     │  │  ├─ MethodsAndSchemes.php
│        │     │  │  ├─ MissingRouteNameController.php
│        │     │  │  ├─ MultipleDeprecatedAliasRouteController.php
│        │     │  │  ├─ NothingButNameController.php
│        │     │  │  ├─ PrefixedActionLocalizedRouteController.php
│        │     │  │  ├─ PrefixedActionPathController.php
│        │     │  │  ├─ RequirementsWithoutPlaceholderNameController.php
│        │     │  │  ├─ RouteWithEnv.php
│        │     │  │  ├─ RouteWithPrefixController.php
│        │     │  │  ├─ RouteWithPriorityController.php
│        │     │  │  └─ Utf8ActionControllers.php
│        │     │  ├─ Attributes
│        │     │  │  └─ FooAttributes.php
│        │     │  ├─ AttributesFixtures
│        │     │  │  ├─ AttributesClassParamAfterCommaController.php
│        │     │  │  ├─ AttributesClassParamAfterParenthesisController.php
│        │     │  │  ├─ AttributesClassParamInlineAfterCommaController.php
│        │     │  │  ├─ AttributesClassParamInlineAfterParenthesisController.php
│        │     │  │  ├─ AttributesClassParamInlineQuotedAfterCommaController.php
│        │     │  │  ├─ AttributesClassParamInlineQuotedAfterParenthesisController.php
│        │     │  │  ├─ AttributesClassParamQuotedAfterCommaController.php
│        │     │  │  └─ AttributesClassParamQuotedAfterParenthesisController.php
│        │     │  ├─ bad_format.yml
│        │     │  ├─ bar.xml
│        │     │  ├─ class-attributes.php
│        │     │  ├─ class-attributes.xml
│        │     │  ├─ class-attributes.yaml
│        │     │  ├─ collection-defaults.php
│        │     │  ├─ controller
│        │     │  │  ├─ empty_wildcard
│        │     │  │  ├─ import_controller.xml
│        │     │  │  ├─ import_controller.yml
│        │     │  │  ├─ import_override_defaults.xml
│        │     │  │  ├─ import_override_defaults.yml
│        │     │  │  ├─ import__controller.xml
│        │     │  │  ├─ import__controller.yml
│        │     │  │  ├─ override_defaults.xml
│        │     │  │  ├─ override_defaults.yml
│        │     │  │  ├─ routing.xml
│        │     │  │  └─ routing.yml
│        │     │  ├─ CustomCompiledRoute.php
│        │     │  ├─ CustomRouteCompiler.php
│        │     │  ├─ CustomXmlFileLoader.php
│        │     │  ├─ defaults.php
│        │     │  ├─ defaults.xml
│        │     │  ├─ defaults.yml
│        │     │  ├─ directory
│        │     │  │  ├─ recurse
│        │     │  │  │  ├─ routes1.yml
│        │     │  │  │  └─ routes2.yml
│        │     │  │  └─ routes3.yml
│        │     │  ├─ directory_import
│        │     │  │  └─ import.yml
│        │     │  ├─ dumper
│        │     │  │  ├─ compiled_url_matcher0.php
│        │     │  │  ├─ compiled_url_matcher1.php
│        │     │  │  ├─ compiled_url_matcher10.php
│        │     │  │  ├─ compiled_url_matcher11.php
│        │     │  │  ├─ compiled_url_matcher12.php
│        │     │  │  ├─ compiled_url_matcher13.php
│        │     │  │  ├─ compiled_url_matcher14.php
│        │     │  │  ├─ compiled_url_matcher2.php
│        │     │  │  ├─ compiled_url_matcher3.php
│        │     │  │  ├─ compiled_url_matcher4.php
│        │     │  │  ├─ compiled_url_matcher5.php
│        │     │  │  ├─ compiled_url_matcher6.php
│        │     │  │  ├─ compiled_url_matcher7.php
│        │     │  │  ├─ compiled_url_matcher8.php
│        │     │  │  └─ compiled_url_matcher9.php
│        │     │  ├─ empty.yml
│        │     │  ├─ Enum
│        │     │  │  ├─ TestIntBackedEnum.php
│        │     │  │  ├─ TestStringBackedEnum.php
│        │     │  │  ├─ TestStringBackedEnum2.php
│        │     │  │  └─ TestUnitEnum.php
│        │     │  ├─ file_resource.yml
│        │     │  ├─ foo.xml
│        │     │  ├─ foo1.xml
│        │     │  ├─ glob
│        │     │  │  ├─ bar.xml
│        │     │  │  ├─ bar.yml
│        │     │  │  ├─ baz.xml
│        │     │  │  ├─ baz.yml
│        │     │  │  ├─ import_multiple.xml
│        │     │  │  ├─ import_multiple.yml
│        │     │  │  ├─ import_single.xml
│        │     │  │  ├─ import_single.yml
│        │     │  │  ├─ php_dsl.php
│        │     │  │  ├─ php_dsl_bar.php
│        │     │  │  └─ php_dsl_baz.php
│        │     │  ├─ imported-with-defaults.php
│        │     │  ├─ imported-with-defaults.xml
│        │     │  ├─ imported-with-defaults.yml
│        │     │  ├─ importer-with-defaults.php
│        │     │  ├─ importer-with-defaults.xml
│        │     │  ├─ importer-with-defaults.yml
│        │     │  ├─ import_with_name_prefix
│        │     │  │  ├─ routing.xml
│        │     │  │  └─ routing.yml
│        │     │  ├─ import_with_no_trailing_slash
│        │     │  │  ├─ routing.xml
│        │     │  │  └─ routing.yml
│        │     │  ├─ incomplete.yml
│        │     │  ├─ list_defaults.xml
│        │     │  ├─ list_in_list_defaults.xml
│        │     │  ├─ list_in_map_defaults.xml
│        │     │  ├─ list_null_values.xml
│        │     │  ├─ locale_and_host
│        │     │  │  ├─ import-with-host-expected-collection.php
│        │     │  │  ├─ import-with-locale-and-host-expected-collection.php
│        │     │  │  ├─ import-with-single-host-expected-collection.php
│        │     │  │  ├─ import-without-host-expected-collection.php
│        │     │  │  ├─ imported.php
│        │     │  │  ├─ imported.xml
│        │     │  │  ├─ imported.yml
│        │     │  │  ├─ importer-with-host.php
│        │     │  │  ├─ importer-with-host.xml
│        │     │  │  ├─ importer-with-host.yml
│        │     │  │  ├─ importer-with-locale-and-host.php
│        │     │  │  ├─ importer-with-locale-and-host.xml
│        │     │  │  ├─ importer-with-locale-and-host.yml
│        │     │  │  ├─ importer-with-single-host.php
│        │     │  │  ├─ importer-with-single-host.xml
│        │     │  │  ├─ importer-with-single-host.yml
│        │     │  │  ├─ importer-without-host.php
│        │     │  │  ├─ importer-without-host.xml
│        │     │  │  ├─ importer-without-host.yml
│        │     │  │  ├─ priorized-host.yml
│        │     │  │  ├─ route-with-hosts-expected-collection.php
│        │     │  │  ├─ route-with-hosts.php
│        │     │  │  ├─ route-with-hosts.xml
│        │     │  │  └─ route-with-hosts.yml
│        │     │  ├─ localized
│        │     │  │  ├─ imported-with-locale-but-not-localized.xml
│        │     │  │  ├─ imported-with-locale-but-not-localized.yml
│        │     │  │  ├─ imported-with-locale.xml
│        │     │  │  ├─ imported-with-locale.yml
│        │     │  │  ├─ imported-with-utf8.php
│        │     │  │  ├─ imported-with-utf8.xml
│        │     │  │  ├─ imported-with-utf8.yml
│        │     │  │  ├─ importer-with-controller-default.yml
│        │     │  │  ├─ importer-with-locale-imports-non-localized-route.xml
│        │     │  │  ├─ importer-with-locale-imports-non-localized-route.yml
│        │     │  │  ├─ importer-with-locale.xml
│        │     │  │  ├─ importer-with-locale.yml
│        │     │  │  ├─ importer-with-utf8.php
│        │     │  │  ├─ importer-with-utf8.xml
│        │     │  │  ├─ importer-with-utf8.yml
│        │     │  │  ├─ importing-localized-route.yml
│        │     │  │  ├─ localized-prefix.yml
│        │     │  │  ├─ localized-route.yml
│        │     │  │  ├─ missing-locale-in-importer.yml
│        │     │  │  ├─ not-localized.yml
│        │     │  │  ├─ officially_formatted_locales.yml
│        │     │  │  ├─ route-without-path-or-locales.yml
│        │     │  │  ├─ utf8.php
│        │     │  │  ├─ utf8.xml
│        │     │  │  └─ utf8.yml
│        │     │  ├─ localized.xml
│        │     │  ├─ map_defaults.xml
│        │     │  ├─ map_in_list_defaults.xml
│        │     │  ├─ map_in_map_defaults.xml
│        │     │  ├─ map_null_values.xml
│        │     │  ├─ missing_id.xml
│        │     │  ├─ missing_path.xml
│        │     │  ├─ namespaceprefix.xml
│        │     │  ├─ nonesense_resource_plus_path.yml
│        │     │  ├─ nonesense_type_without_resource.yml
│        │     │  ├─ nonvalid-deprecated-route.xml
│        │     │  ├─ nonvalid.xml
│        │     │  ├─ nonvalid.yml
│        │     │  ├─ nonvalid2.yml
│        │     │  ├─ nonvalidkeys.yml
│        │     │  ├─ nonvalidnode.xml
│        │     │  ├─ nonvalidroute.xml
│        │     │  ├─ null_values.xml
│        │     │  ├─ OtherAnnotatedClasses
│        │     │  │  ├─ NoStartTagClass.php
│        │     │  │  └─ VariadicClass.php
│        │     │  ├─ php_dsl.php
│        │     │  ├─ php_dsl_i18n.php
│        │     │  ├─ php_dsl_sub.php
│        │     │  ├─ php_dsl_sub_i18n.php
│        │     │  ├─ php_dsl_sub_root.php
│        │     │  ├─ php_object_dsl.php
│        │     │  ├─ psr4-attributes.php
│        │     │  ├─ psr4-attributes.xml
│        │     │  ├─ psr4-attributes.yaml
│        │     │  ├─ psr4-controllers-redirection
│        │     │  │  ├─ psr4-attributes.php
│        │     │  │  ├─ psr4-attributes.xml
│        │     │  │  └─ psr4-attributes.yaml
│        │     │  ├─ psr4-controllers-redirection.php
│        │     │  ├─ psr4-controllers-redirection.xml
│        │     │  ├─ psr4-controllers-redirection.yaml
│        │     │  ├─ Psr4Controllers
│        │     │  │  ├─ MyController.php
│        │     │  │  ├─ MyUnannotatedController.php
│        │     │  │  └─ SubNamespace
│        │     │  │     ├─ EvenDeeperNamespace
│        │     │  │     │  └─ MyOtherController.php
│        │     │  │     ├─ IrrelevantClass.php
│        │     │  │     ├─ IrrelevantEnum.php
│        │     │  │     ├─ IrrelevantInterface.php
│        │     │  │     ├─ MyAbstractController.php
│        │     │  │     ├─ MyChildController.php
│        │     │  │     ├─ MyControllerWithATrait.php
│        │     │  │     └─ SomeSharedImplementation.php
│        │     │  ├─ RedirectableUrlMatcher.php
│        │     │  ├─ requirements_without_placeholder_name.yml
│        │     │  ├─ scalar_defaults.xml
│        │     │  ├─ special_route_name.yml
│        │     │  ├─ TraceableAttributeClassLoader.php
│        │     │  ├─ validpattern.php
│        │     │  ├─ validpattern.xml
│        │     │  ├─ validpattern.yml
│        │     │  ├─ validresource.php
│        │     │  ├─ validresource.xml
│        │     │  ├─ validresource.yml
│        │     │  ├─ when-env.xml
│        │     │  ├─ when-env.yml
│        │     │  ├─ withdoctype.xml
│        │     │  └─ with_define_path_variable.php
│        │     ├─ Generator
│        │     │  ├─ Dumper
│        │     │  │  └─ CompiledUrlGeneratorDumperTest.php
│        │     │  └─ UrlGeneratorTest.php
│        │     ├─ Loader
│        │     │  ├─ AttributeClassLoaderTest.php
│        │     │  ├─ AttributeDirectoryLoaderTest.php
│        │     │  ├─ AttributeFileLoaderTest.php
│        │     │  ├─ ClosureLoaderTest.php
│        │     │  ├─ ContainerLoaderTest.php
│        │     │  ├─ DirectoryLoaderTest.php
│        │     │  ├─ FileLocatorStub.php
│        │     │  ├─ GlobFileLoaderTest.php
│        │     │  ├─ ObjectLoaderTest.php
│        │     │  ├─ PhpFileLoaderTest.php
│        │     │  ├─ Psr4DirectoryLoaderTest.php
│        │     │  ├─ XmlFileLoaderTest.php
│        │     │  └─ YamlFileLoaderTest.php
│        │     ├─ Matcher
│        │     │  ├─ CompiledRedirectableUrlMatcherTest.php
│        │     │  ├─ CompiledUrlMatcherTest.php
│        │     │  ├─ Dumper
│        │     │  │  ├─ CompiledUrlMatcherDumperTest.php
│        │     │  │  └─ StaticPrefixCollectionTest.php
│        │     │  ├─ ExpressionLanguageProviderTest.php
│        │     │  ├─ RedirectableUrlMatcherTest.php
│        │     │  ├─ TraceableUrlMatcherTest.php
│        │     │  └─ UrlMatcherTest.php
│        │     ├─ RequestContextTest.php
│        │     ├─ Requirement
│        │     │  ├─ EnumRequirementTest.php
│        │     │  └─ RequirementTest.php
│        │     ├─ RouteCollectionTest.php
│        │     ├─ RouteCompilerTest.php
│        │     ├─ RouterTest.php
│        │     └─ RouteTest.php
│        ├─ runtime
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ GenericRuntime.php
│        │  ├─ Internal
│        │  │  ├─ autoload_runtime.template
│        │  │  ├─ BasicErrorHandler.php
│        │  │  ├─ ComposerPlugin.php
│        │  │  ├─ Console
│        │  │  │  ├─ ApplicationRuntime.php
│        │  │  │  ├─ Command
│        │  │  │  │  └─ CommandRuntime.php
│        │  │  │  ├─ Input
│        │  │  │  │  └─ InputInterfaceRuntime.php
│        │  │  │  └─ Output
│        │  │  │     └─ OutputInterfaceRuntime.php
│        │  │  ├─ HttpFoundation
│        │  │  │  ├─ RequestRuntime.php
│        │  │  │  └─ ResponseRuntime.php
│        │  │  ├─ HttpKernel
│        │  │  │  └─ HttpKernelInterfaceRuntime.php
│        │  │  ├─ MissingDotenv.php
│        │  │  └─ SymfonyErrorHandler.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Resolver
│        │  │  ├─ ClosureResolver.php
│        │  │  └─ DebugClosureResolver.php
│        │  ├─ ResolverInterface.php
│        │  ├─ Runner
│        │  │  ├─ ClosureRunner.php
│        │  │  └─ Symfony
│        │  │     ├─ ConsoleApplicationRunner.php
│        │  │     ├─ HttpKernelRunner.php
│        │  │     └─ ResponseRunner.php
│        │  ├─ RunnerInterface.php
│        │  ├─ RuntimeInterface.php
│        │  ├─ SymfonyRuntime.php
│        │  └─ Tests
│        │     └─ phpt
│        │        ├─ .env
│        │        ├─ .env.extra
│        │        ├─ application.php
│        │        ├─ application.phpt
│        │        ├─ autoload.php
│        │        ├─ command.php
│        │        ├─ command.phpt
│        │        ├─ command2.php
│        │        ├─ command2.phpt
│        │        ├─ command_list.php
│        │        ├─ command_list.phpt
│        │        ├─ dotenv_extra_load.php
│        │        ├─ dotenv_extra_load.phpt
│        │        ├─ dotenv_extra_overload.php
│        │        ├─ dotenv_extra_overload.phpt
│        │        ├─ dotenv_overload.php
│        │        ├─ dotenv_overload.phpt
│        │        ├─ dotenv_overload_command_debug_exists_0_to_1.php
│        │        ├─ dotenv_overload_command_debug_exists_0_to_1.phpt
│        │        ├─ dotenv_overload_command_debug_exists_1_to_0.php
│        │        ├─ dotenv_overload_command_debug_exists_1_to_0.phpt
│        │        ├─ dotenv_overload_command_env_conflict.php
│        │        ├─ dotenv_overload_command_env_conflict.phpt
│        │        ├─ dotenv_overload_command_env_exists.php
│        │        ├─ dotenv_overload_command_env_exists.phpt
│        │        ├─ dotenv_overload_command_no_debug.php
│        │        ├─ dotenv_overload_command_no_debug.phpt
│        │        ├─ generic-request.php
│        │        ├─ generic-request.phpt
│        │        ├─ hello.php
│        │        ├─ hello.phpt
│        │        ├─ kernel-loop.php
│        │        ├─ kernel-loop.phpt
│        │        ├─ kernel.php
│        │        ├─ kernel.phpt
│        │        ├─ kernel_register_argc_argv.phpt
│        │        ├─ request.php
│        │        ├─ request.phpt
│        │        ├─ runtime-options.php
│        │        └─ runtime-options.phpt
│        ├─ service-contracts
│        │  ├─ Attribute
│        │  │  ├─ Required.php
│        │  │  └─ SubscribedService.php
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ LICENSE
│        │  ├─ README.md
│        │  ├─ ResetInterface.php
│        │  ├─ ServiceCollectionInterface.php
│        │  ├─ ServiceLocatorTrait.php
│        │  ├─ ServiceMethodsSubscriberTrait.php
│        │  ├─ ServiceProviderInterface.php
│        │  ├─ ServiceSubscriberInterface.php
│        │  ├─ ServiceSubscriberTrait.php
│        │  └─ Test
│        │     ├─ ServiceLocatorTest.php
│        │     └─ ServiceLocatorTestCase.php
│        ├─ string
│        │  ├─ AbstractString.php
│        │  ├─ AbstractUnicodeString.php
│        │  ├─ ByteString.php
│        │  ├─ CHANGELOG.md
│        │  ├─ CodePointString.php
│        │  ├─ composer.json
│        │  ├─ Exception
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ InvalidArgumentException.php
│        │  │  └─ RuntimeException.php
│        │  ├─ Inflector
│        │  │  ├─ EnglishInflector.php
│        │  │  ├─ FrenchInflector.php
│        │  │  ├─ InflectorInterface.php
│        │  │  └─ SpanishInflector.php
│        │  ├─ LazyString.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Resources
│        │  │  ├─ bin
│        │  │  │  └─ update-data.php
│        │  │  ├─ data
│        │  │  │  ├─ wcswidth_table_wide.php
│        │  │  │  └─ wcswidth_table_zero.php
│        │  │  ├─ functions.php
│        │  │  └─ WcswidthDataGenerator.php
│        │  ├─ Slugger
│        │  │  ├─ AsciiSlugger.php
│        │  │  └─ SluggerInterface.php
│        │  ├─ Tests
│        │  │  ├─ AbstractAsciiTestCase.php
│        │  │  ├─ AbstractUnicodeTestCase.php
│        │  │  ├─ ByteStringTest.php
│        │  │  ├─ CodePointStringTest.php
│        │  │  ├─ FunctionsTest.php
│        │  │  ├─ Inflector
│        │  │  │  ├─ EnglishInflectorTest.php
│        │  │  │  ├─ FrenchInflectorTest.php
│        │  │  │  └─ SpanishInflectorTest.php
│        │  │  ├─ LazyStringTest.php
│        │  │  ├─ Slugger
│        │  │  │  └─ AsciiSluggerTest.php
│        │  │  ├─ SluggerTest.php
│        │  │  └─ UnicodeStringTest.php
│        │  ├─ TruncateMode.php
│        │  └─ UnicodeString.php
│        ├─ var-dumper
│        │  ├─ Caster
│        │  │  ├─ AddressInfoCaster.php
│        │  │  ├─ AmqpCaster.php
│        │  │  ├─ ArgsStub.php
│        │  │  ├─ Caster.php
│        │  │  ├─ ClassStub.php
│        │  │  ├─ ConstStub.php
│        │  │  ├─ CurlCaster.php
│        │  │  ├─ CutArrayStub.php
│        │  │  ├─ CutStub.php
│        │  │  ├─ DateCaster.php
│        │  │  ├─ DoctrineCaster.php
│        │  │  ├─ DOMCaster.php
│        │  │  ├─ DsCaster.php
│        │  │  ├─ DsPairStub.php
│        │  │  ├─ EnumStub.php
│        │  │  ├─ ExceptionCaster.php
│        │  │  ├─ FFICaster.php
│        │  │  ├─ FiberCaster.php
│        │  │  ├─ FrameStub.php
│        │  │  ├─ GdCaster.php
│        │  │  ├─ GmpCaster.php
│        │  │  ├─ ImagineCaster.php
│        │  │  ├─ ImgStub.php
│        │  │  ├─ IntlCaster.php
│        │  │  ├─ LinkStub.php
│        │  │  ├─ MemcachedCaster.php
│        │  │  ├─ MysqliCaster.php
│        │  │  ├─ OpenSSLCaster.php
│        │  │  ├─ PdoCaster.php
│        │  │  ├─ PgSqlCaster.php
│        │  │  ├─ ProxyManagerCaster.php
│        │  │  ├─ RdKafkaCaster.php
│        │  │  ├─ RedisCaster.php
│        │  │  ├─ ReflectionCaster.php
│        │  │  ├─ ResourceCaster.php
│        │  │  ├─ ScalarStub.php
│        │  │  ├─ SocketCaster.php
│        │  │  ├─ SplCaster.php
│        │  │  ├─ SqliteCaster.php
│        │  │  ├─ StubCaster.php
│        │  │  ├─ SymfonyCaster.php
│        │  │  ├─ TraceStub.php
│        │  │  ├─ UninitializedStub.php
│        │  │  ├─ UuidCaster.php
│        │  │  ├─ VirtualStub.php
│        │  │  ├─ XmlReaderCaster.php
│        │  │  └─ XmlResourceCaster.php
│        │  ├─ CHANGELOG.md
│        │  ├─ Cloner
│        │  │  ├─ AbstractCloner.php
│        │  │  ├─ ClonerInterface.php
│        │  │  ├─ Cursor.php
│        │  │  ├─ Data.php
│        │  │  ├─ DumperInterface.php
│        │  │  ├─ Internal
│        │  │  │  └─ NoDefault.php
│        │  │  ├─ Stub.php
│        │  │  └─ VarCloner.php
│        │  ├─ Command
│        │  │  ├─ Descriptor
│        │  │  │  ├─ CliDescriptor.php
│        │  │  │  ├─ DumpDescriptorInterface.php
│        │  │  │  └─ HtmlDescriptor.php
│        │  │  └─ ServerDumpCommand.php
│        │  ├─ composer.json
│        │  ├─ Dumper
│        │  │  ├─ AbstractDumper.php
│        │  │  ├─ CliDumper.php
│        │  │  ├─ ContextProvider
│        │  │  │  ├─ CliContextProvider.php
│        │  │  │  ├─ ContextProviderInterface.php
│        │  │  │  ├─ RequestContextProvider.php
│        │  │  │  └─ SourceContextProvider.php
│        │  │  ├─ ContextualizedDumper.php
│        │  │  ├─ DataDumperInterface.php
│        │  │  ├─ HtmlDumper.php
│        │  │  └─ ServerDumper.php
│        │  ├─ Exception
│        │  │  └─ ThrowingCasterException.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ README.md
│        │  ├─ Resources
│        │  │  ├─ bin
│        │  │  │  └─ var-dump-server
│        │  │  ├─ css
│        │  │  │  └─ htmlDescriptor.css
│        │  │  ├─ functions
│        │  │  │  └─ dump.php
│        │  │  └─ js
│        │  │     └─ htmlDescriptor.js
│        │  ├─ Server
│        │  │  ├─ Connection.php
│        │  │  └─ DumpServer.php
│        │  ├─ Test
│        │  │  └─ VarDumperTestTrait.php
│        │  ├─ Tests
│        │  │  ├─ Caster
│        │  │  │  ├─ AddressInfoCasterTest.php
│        │  │  │  ├─ CasterTest.php
│        │  │  │  ├─ CurlCasterTest.php
│        │  │  │  ├─ DateCasterTest.php
│        │  │  │  ├─ DoctrineCasterTest.php
│        │  │  │  ├─ DOMCasterTest.php
│        │  │  │  ├─ ExceptionCasterTest.php
│        │  │  │  ├─ FFICasterTest.php
│        │  │  │  ├─ FiberCasterTest.php
│        │  │  │  ├─ GmpCasterTest.php
│        │  │  │  ├─ IntlCasterTest.php
│        │  │  │  ├─ MemcachedCasterTest.php
│        │  │  │  ├─ MysqliCasterTest.php
│        │  │  │  ├─ OpenSSLCasterTest.php
│        │  │  │  ├─ PdoCasterTest.php
│        │  │  │  ├─ RdKafkaCasterTest.php
│        │  │  │  ├─ RedisCasterTest.php
│        │  │  │  ├─ ReflectionCasterTest.php
│        │  │  │  ├─ ResourceCasterTest.php
│        │  │  │  ├─ SocketCasterTest.php
│        │  │  │  ├─ SplCasterTest.php
│        │  │  │  ├─ SqliteCasterTest.php
│        │  │  │  ├─ StubCasterTest.php
│        │  │  │  ├─ SymfonyCasterTest.php
│        │  │  │  └─ XmlReaderCasterTest.php
│        │  │  ├─ Cloner
│        │  │  │  ├─ DataTest.php
│        │  │  │  ├─ StubTest.php
│        │  │  │  └─ VarClonerTest.php
│        │  │  ├─ Command
│        │  │  │  ├─ Descriptor
│        │  │  │  │  ├─ CliDescriptorTest.php
│        │  │  │  │  └─ HtmlDescriptorTest.php
│        │  │  │  └─ ServerDumpCommandTest.php
│        │  │  ├─ Dumper
│        │  │  │  ├─ CliDumperTest.php
│        │  │  │  ├─ ContextProvider
│        │  │  │  │  └─ RequestContextProviderTest.php
│        │  │  │  ├─ ContextualizedDumperTest.php
│        │  │  │  ├─ functions
│        │  │  │  │  ├─ dd_with_multiple_args.phpt
│        │  │  │  │  ├─ dd_with_named_args.phpt
│        │  │  │  │  ├─ dd_with_null.phpt
│        │  │  │  │  ├─ dd_with_single_arg.phpt
│        │  │  │  │  ├─ dump_data_collector_with_spl_array.phpt
│        │  │  │  │  ├─ dump_without_args.phpt
│        │  │  │  │  ├─ dump_with_multiple_args.phpt
│        │  │  │  │  ├─ dump_with_named_args.phpt
│        │  │  │  │  ├─ dump_with_null.phpt
│        │  │  │  │  └─ dump_with_single_arg.phpt
│        │  │  │  ├─ FunctionsTest.php
│        │  │  │  ├─ HtmlDumperTest.php
│        │  │  │  └─ ServerDumperTest.php
│        │  │  ├─ Fixtures
│        │  │  │  ├─ BackedEnumFixture.php
│        │  │  │  ├─ DateTimeChild.php
│        │  │  │  ├─ dumb-var.php
│        │  │  │  ├─ dump_server.php
│        │  │  │  ├─ ExtendsReflectionTypeFixture.php
│        │  │  │  ├─ FooInterface.php
│        │  │  │  ├─ GeneratorDemo.php
│        │  │  │  ├─ LotsOfAttributes.php
│        │  │  │  ├─ MyAttribute.php
│        │  │  │  ├─ NotLoadableClass.php
│        │  │  │  ├─ Php74.php
│        │  │  │  ├─ Php81Enums.php
│        │  │  │  ├─ Php82NullStandaloneReturnType.php
│        │  │  │  ├─ ReflectionIntersectionTypeFixture.php
│        │  │  │  ├─ ReflectionNamedTypeFixture.php
│        │  │  │  ├─ ReflectionUnionTypeFixture.php
│        │  │  │  ├─ ReflectionUnionTypeWithIntersectionFixture.php
│        │  │  │  ├─ Twig.php
│        │  │  │  ├─ UnitEnumFixture.php
│        │  │  │  ├─ VirtualProperty.php
│        │  │  │  └─ xml_reader.xml
│        │  │  ├─ Server
│        │  │  │  └─ ConnectionTest.php
│        │  │  └─ Test
│        │  │     └─ VarDumperTestTraitTest.php
│        │  └─ VarDumper.php
│        ├─ var-exporter
│        │  ├─ CHANGELOG.md
│        │  ├─ composer.json
│        │  ├─ Exception
│        │  │  ├─ ClassNotFoundException.php
│        │  │  ├─ ExceptionInterface.php
│        │  │  ├─ LogicException.php
│        │  │  └─ NotInstantiableTypeException.php
│        │  ├─ Hydrator.php
│        │  ├─ Instantiator.php
│        │  ├─ Internal
│        │  │  ├─ Exporter.php
│        │  │  ├─ Hydrator.php
│        │  │  ├─ LazyDecoratorTrait.php
│        │  │  ├─ LazyObjectRegistry.php
│        │  │  ├─ LazyObjectState.php
│        │  │  ├─ LazyObjectTrait.php
│        │  │  ├─ Reference.php
│        │  │  ├─ Registry.php
│        │  │  └─ Values.php
│        │  ├─ LazyGhostTrait.php
│        │  ├─ LazyObjectInterface.php
│        │  ├─ LazyProxyTrait.php
│        │  ├─ LICENSE
│        │  ├─ phpunit.xml.dist
│        │  ├─ ProxyHelper.php
│        │  ├─ README.md
│        │  ├─ Tests
│        │  │  ├─ Fixtures
│        │  │  │  ├─ abstract-parent.php
│        │  │  │  ├─ array-iterator.php
│        │  │  │  ├─ array-object-custom.php
│        │  │  │  ├─ array-object.php
│        │  │  │  ├─ backed-property.php
│        │  │  │  ├─ BackedProperty.php
│        │  │  │  ├─ bool.php
│        │  │  │  ├─ clone.php
│        │  │  │  ├─ datetime.php
│        │  │  │  ├─ error.php
│        │  │  │  ├─ external-references.php
│        │  │  │  ├─ final-array-iterator.php
│        │  │  │  ├─ final-error.php
│        │  │  │  ├─ final-stdclass.php
│        │  │  │  ├─ foo-serializable.php
│        │  │  │  ├─ FooReadonly.php
│        │  │  │  ├─ FooSerializable.php
│        │  │  │  ├─ FooUnitEnum.php
│        │  │  │  ├─ hard-references-recursive.php
│        │  │  │  ├─ hard-references.php
│        │  │  │  ├─ incomplete-class.php
│        │  │  │  ├─ LazyGhost
│        │  │  │  │  ├─ ChildMagicClass.php
│        │  │  │  │  ├─ ChildStdClass.php
│        │  │  │  │  ├─ ChildTestClass.php
│        │  │  │  │  ├─ ClassWithUninitializedObjectProperty.php
│        │  │  │  │  ├─ LazyClass.php
│        │  │  │  │  ├─ MagicClass.php
│        │  │  │  │  ├─ NoMagicClass.php
│        │  │  │  │  ├─ ReadOnlyClass.php
│        │  │  │  │  ├─ RegularClass.php
│        │  │  │  │  └─ TestClass.php
│        │  │  │  ├─ LazyProxy
│        │  │  │  │  ├─ AbstractHooked.php
│        │  │  │  │  ├─ AsymmetricVisibility.php
│        │  │  │  │  ├─ ConcreteReadOnlyClass.php
│        │  │  │  │  ├─ FinalPublicClass.php
│        │  │  │  │  ├─ Hooked.php
│        │  │  │  │  ├─ HookedInterface.php
│        │  │  │  │  ├─ HookedWithDefaultValue.php
│        │  │  │  │  ├─ Php82NullStandaloneReturnType.php
│        │  │  │  │  ├─ ReadOnlyClass.php
│        │  │  │  │  ├─ StringMagicGetClass.php
│        │  │  │  │  ├─ TestClass.php
│        │  │  │  │  ├─ TestOverwritePropClass.php
│        │  │  │  │  ├─ TestUnserializeClass.php
│        │  │  │  │  └─ TestWakeupClass.php
│        │  │  │  ├─ lf-ending-string.php
│        │  │  │  ├─ multiline-string.php
│        │  │  │  ├─ MySerializable.php
│        │  │  │  ├─ partially-indexed-array.php
│        │  │  │  ├─ php74-serializable.php
│        │  │  │  ├─ private-constructor.php
│        │  │  │  ├─ private.php
│        │  │  │  ├─ readonly.php
│        │  │  │  ├─ serializable.php
│        │  │  │  ├─ simple-array.php
│        │  │  │  ├─ SimpleObject.php
│        │  │  │  ├─ spl-object-storage.php
│        │  │  │  ├─ unit-enum.php
│        │  │  │  ├─ var-on-sleep.php
│        │  │  │  ├─ wakeup-refl.php
│        │  │  │  ├─ wakeup.php
│        │  │  │  ├─ __serialize-but-no-__unserialize.php
│        │  │  │  └─ __unserialize-but-no-__serialize.php
│        │  │  ├─ InstantiatorTest.php
│        │  │  ├─ LazyProxyTraitTest.php
│        │  │  ├─ LegacyLazyGhostTraitTest.php
│        │  │  ├─ LegacyLazyProxyTraitTest.php
│        │  │  ├─ LegacyProxyHelperTest.php
│        │  │  ├─ ProxyHelperTest.php
│        │  │  └─ VarExporterTest.php
│        │  └─ VarExporter.php
│        └─ yaml
│           ├─ CHANGELOG.md
│           ├─ Command
│           │  └─ LintCommand.php
│           ├─ composer.json
│           ├─ Dumper.php
│           ├─ Escaper.php
│           ├─ Exception
│           │  ├─ DumpException.php
│           │  ├─ ExceptionInterface.php
│           │  ├─ ParseException.php
│           │  └─ RuntimeException.php
│           ├─ Inline.php
│           ├─ LICENSE
│           ├─ Parser.php
│           ├─ phpunit.xml.dist
│           ├─ README.md
│           ├─ Resources
│           │  └─ bin
│           │     └─ yaml-lint
│           ├─ Tag
│           │  └─ TaggedValue.php
│           ├─ Tests
│           │  ├─ Command
│           │  │  └─ LintCommandTest.php
│           │  ├─ DumperTest.php
│           │  ├─ Fixtures
│           │  │  ├─ arrow.gif
│           │  │  ├─ booleanMappingKeys.yml
│           │  │  ├─ embededPhp.yml
│           │  │  ├─ escapedCharacters.yml
│           │  │  ├─ FooBackedEnum.php
│           │  │  ├─ FooUnitEnum.php
│           │  │  ├─ index.yml
│           │  │  ├─ nonStringKeys.yml
│           │  │  ├─ not_readable.yml
│           │  │  ├─ nullMappingKey.yml
│           │  │  ├─ numericMappingKeys.yml
│           │  │  ├─ sfComments.yml
│           │  │  ├─ sfCompact.yml
│           │  │  ├─ sfMergeKey.yml
│           │  │  ├─ sfObjects.yml
│           │  │  ├─ sfQuotes.yml
│           │  │  ├─ sfTests.yml
│           │  │  ├─ unindentedCollections.yml
│           │  │  ├─ YtsAnchorAlias.yml
│           │  │  ├─ YtsBasicTests.yml
│           │  │  ├─ YtsBlockMapping.yml
│           │  │  ├─ YtsDocumentSeparator.yml
│           │  │  ├─ YtsErrorTests.yml
│           │  │  ├─ YtsFlowCollections.yml
│           │  │  ├─ YtsFoldedScalars.yml
│           │  │  ├─ YtsNullsAndEmpties.yml
│           │  │  ├─ YtsSpecificationExamples.yml
│           │  │  └─ YtsTypeTransfers.yml
│           │  ├─ InlineTest.php
│           │  ├─ ParseExceptionTest.php
│           │  ├─ ParserTest.php
│           │  └─ YamlTest.php
│           ├─ Unescaper.php
│           └─ Yaml.php
├─ docker-compose.dev.yml
├─ docs
├─ frontend
│  ├─ .editorconfig
│  ├─ .prettierrc.json
│  ├─ Dockerfile.dev
│  ├─ env.d.ts
│  ├─ eslint.config.ts
│  ├─ index.html
│  ├─ package-lock.json
│  ├─ package.json
│  ├─ playwright.config.ts
│  ├─ public
│  │  └─ favicon.ico
│  ├─ README.md
│  ├─ src
│  │  ├─ App.vue
│  │  ├─ assets
│  │  │  ├─ base.css
│  │  │  ├─ logo.svg
│  │  │  └─ main.css
│  │  ├─ components
│  │  │  ├─ HelloWorld.vue
│  │  │  ├─ icons
│  │  │  │  ├─ IconCommunity.vue
│  │  │  │  ├─ IconDocumentation.vue
│  │  │  │  ├─ IconEcosystem.vue
│  │  │  │  ├─ IconSupport.vue
│  │  │  │  └─ IconTooling.vue
│  │  │  ├─ TheWelcome.vue
│  │  │  ├─ WelcomeItem.vue
│  │  │  └─ __tests__
│  │  │     └─ HelloWorld.spec.ts
│  │  ├─ main.ts
│  │  ├─ router
│  │  │  └─ index.ts
│  │  ├─ stores
│  │  │  └─ counter.ts
│  │  └─ views
│  │     ├─ AboutView.vue
│  │     └─ HomeView.vue
│  ├─ tests
│  │  ├─ auth
│  │  │  └─ user.json
│  │  ├─ e2e
│  │  │  ├─ auth.spec.ts
│  │  │  ├─ clients.spec.ts
│  │  │  ├─ dashboard.spec.ts
│  │  │  ├─ invoicing.spec.ts
│  │  │  ├─ subscriptions.spec.ts
│  │  │  ├─ tsconfig.json
│  │  │  ├─ urssaf.spec.ts
│  │  │  └─ vue.spec.ts
│  │  ├─ fixtures
│  │  │  └─ test-data.json
│  │  └─ utils
│  │     └─ helpers.ts
│  ├─ tsconfig.app.json
│  ├─ tsconfig.json
│  ├─ tsconfig.node.json
│  ├─ tsconfig.vitest.json
│  ├─ vite.config.ts
│  └─ vitest.config.ts
├─ infrastructure
├─ LICENSE
└─ README.md

```