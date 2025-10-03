# Changelog

Toutes les modifications notables de ce projet seront documentées dans ce fichier.

Le format est basé sur [Keep a Changelog](https://keepachangelog.com/fr/1.0.0/),
et ce projet adhère au [Versioning Sémantique](https://semver.org/lang/fr/).

## [1.0.0] - 2025-01-03

### Ajouté
- 🎯 Formulaire mobile-first responsive
- 📍 Géolocalisation GPS automatique
- 🗺️ Recherche d'adresse avec autocomplétion (API Nominatim)
- 📸 Prise de photos avec capture directe sur mobile
- 🎤 **Dictée vocale pour les observations** (Web Speech API)
- 🧮 Calculs automatiques :
  - Volume du caisson
  - Poids de paille nécessaire
  - **Masse volumique avec code couleur** (vert ≥ 105 kg/m³, rouge < 105 kg/m³)
- 💾 Export JSON structuré avec géolocalisation
- 📤 Partage natif mobile
- 📊 Barre de progression du formulaire
- 🔄 Sections collapsibles pour navigation simplifiée
- 🔒 Gestion des permissions (géolocalisation, caméra, microphone)
- 🌐 Carte interactive (Leaflet.js + OpenStreetMap)
- ✅ Validation de formulaire en temps réel
- 📱 Toast notifications pour feedback utilisateur
- 🎨 Design moderne avec palette ielo

### Sécurité
- Validation des fichiers images (type et taille max 10 MB)
- Sanitisation des entrées utilisateur
- Validation des coordonnées GPS
- Toutes les données restent locales (pas de serveur externe)
- HTTPS requis pour fonctionnalités sensibles (géoloc, caméra)

### Documentation
- Guide de test complet
- Guide de déploiement GitHub
- Documentation Google Drive
- Roadmap des améliorations futures
- README professionnel avec badges

## [Unreleased]

### Prévu pour v1.1.0
- Export PDF professionnel
- Sauvegarde automatique locale
- Templates prédéfinis
- Mode hors ligne complet (Service Worker)

### Prévu pour v1.2.0
- Intégration Google Drive automatique
- Signature digitale
- Historique des chantiers
- Import de fichiers JSON existants

### Prévu pour v2.0.0
- Dashboard analytics
- Mode multi-utilisateurs
- Comparaison automatique avec chantiers précédents
- Alertes intelligentes
- Application mobile native (PWA)

---

**Légende :**
- `Ajouté` : Nouvelles fonctionnalités
- `Modifié` : Changements de fonctionnalités existantes
- `Déprécié` : Fonctionnalités bientôt supprimées
- `Supprimé` : Fonctionnalités supprimées
- `Corrigé` : Corrections de bugs
- `Sécurité` : Corrections de vulnérabilités
