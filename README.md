# 🌾 Formulaire d'Intervention Chantier - ielo

[![License](https://img.shields.io/badge/license-Proprietary-blue.svg)](LICENSE)
[![GitHub Pages](https://img.shields.io/badge/demo-live-green.svg)](https://nrielo.github.io/Formulaire_intervention_chantier/)
[![Mobile](https://img.shields.io/badge/platform-mobile%20%7C%20tablet%20%7C%20desktop-lightgrey.svg)](https://nrielo.github.io/Formulaire_intervention_chantier/)

Formulaire de retour d'expérience (REX) à destination des accompagnateurs et des formateurs ielo lors d'interventions sur chantier d'isolation en paille hachée.

## 🚀 Accès direct

**[📱 Ouvrir le formulaire](https://nrielo.github.io/Formulaire_intervention_chantier/)**

### QR Code pour accès mobile

[Insérer QR Code ici]

Scannez ce code pour accéder instantanément au formulaire depuis votre smartphone !

## ✨ Fonctionnalités

### 📋 Formulaire intelligent
- ✅ Formulaire adaptatif mobile-first
- ✅ Sections collapsibles pour navigation simplifiée
- ✅ Barre de progression en temps réel
- ✅ Validation automatique des champs
- ✅ Sauvegarde locale automatique (évite la perte de données)

### 📸 Gestion des photos
- ✅ Capture directe depuis l'appareil photo
- ✅ Import de photos existantes
- ✅ Prévisualisation immédiate
- ✅ Compression automatique
- ✅ Limite de sécurité (10 MB par photo)

### 📍 Géolocalisation
- ✅ Localisation GPS automatique
- ✅ Recherche d'adresse avec autocomplétion
- ✅ Carte interactive (OpenStreetMap)
- ✅ Coordonnées GPS précises
- ✅ Reverse geocoding (coordonnées → adresse)

### 🎤 Dictée vocale
- ✅ Transcription automatique dans les observations
- ✅ Support multilingue (français prioritaire)
- ✅ Feedback visuel en temps réel
- ✅ Compatible Chrome et Safari

### 🧮 Calculs automatiques
- ✅ Volume du caisson (L × l × h)
- ✅ Poids de paille nécessaire (115 kg/m³)
- ✅ **Masse volumique avec code couleur** :
  - 🟢 **Vert** : ≥ 105 kg/m³ (conforme)
  - 🔴 **Rouge** : < 105 kg/m³ (non conforme)

### 💾 Export et partage
- ✅ Export JSON structuré
- ✅ Partage natif mobile (vers Drive, email, etc.)
- ✅ Données sauvegardées avec géolocalisation
- ✅ Horodatage automatique

## 📱 Compatibilité

| Fonctionnalité | Mobile | Tablette | Desktop |
|----------------|--------|----------|---------|
| Formulaire | ✅ | ✅ | ✅ |
| Photos (import) | ✅ | ✅ | ✅ |
| Photos (capture) | ✅ | ✅ | ✅* |
| Géolocalisation GPS | ✅ | ✅ | ✅* |
| Recherche adresse | ✅ | ✅ | ✅ |
| Dictée vocale | ✅ | ✅ | ✅ |
| Export JSON | ✅ | ✅ | ✅ |
| Partage natif | ✅ | ✅ | ❌ |

*Nécessite HTTPS (activé sur GitHub Pages)

### Navigateurs supportés
- ✅ Chrome/Edge 90+
- ✅ Safari 14+
- ✅ Firefox 88+
- ✅ Samsung Internet 14+

## 🎯 Utilisation

### 1. Ouvrir le formulaire
Trois options :
- Scannez le QR Code
- Accédez à l'URL directement
- Ajoutez aux favoris de votre navigateur

### 2. Remplir les informations
- Les champs obligatoires sont marqués d'un astérisque (*)
- La barre de progression indique votre avancement
- Les sections sont collapsibles pour faciliter la navigation

### 3. Ajouter des photos
- Touchez la zone photo pour :
  - Prendre une photo directement
  - Importer depuis la galerie

### 4. Utiliser la géolocalisation
- Touchez le bouton 📍 pour localisation automatique
- Ou tapez l'adresse manuellement avec autocomplétion

### 5. Dicter les observations
- Touchez le bouton 🎤 dans la zone observations
- Parlez clairement
- Le texte apparaît automatiquement

### 6. Vérifier les calculs
- Entrez les dimensions du caisson
- La masse volumique s'affiche automatiquement
- Code couleur : vert = conforme, rouge = non conforme

### 7. Enregistrer
- Touchez "💾 Enregistrer" pour export JSON
- Ou "📤 Partager" pour partage direct

## 🛠️ Technologies

- **HTML5** : Structure sémantique
- **CSS3** : Design responsive et moderne
- **JavaScript (Vanilla)** : Logique métier
- **Leaflet.js** : Cartes interactives
- **OpenStreetMap** : Données cartographiques
- **Nominatim API** : Géocodage
- **Web Speech API** : Reconnaissance vocale

## 📂 Structure du projet

```
Formulaire_intervention_chantier/
├── index.html                          # Formulaire mobile (principal)
├── formulaire_complet.html             # Version complète avec toutes sections
├── README.md                           # Ce fichier
└── docs/
    ├── GUIDE_TEST.md                   # Guide de test complet
    ├── DEPLOIEMENT_GITHUB.md           # Guide de déploiement
    ├── GOOGLE_DRIVE_INTEGRATION.md     # Intégration Google Drive
    └── AMELIORATIONS_PROPOSEES.md      # Roadmap et améliorations
```

## 📖 Documentation

- **[Guide de test](docs/GUIDE_TEST.md)** : Comment tester le formulaire
- **[Déploiement GitHub](docs/DEPLOIEMENT_GITHUB.md)** : Mise en ligne étape par étape
- **[Intégration Google Drive](docs/GOOGLE_DRIVE_INTEGRATION.md)** : Upload automatique
- **[Améliorations](docs/AMELIORATIONS_PROPOSEES.md)** : Roadmap et suggestions

## 🚀 Installation locale

Pour tester en local avec toutes les fonctionnalités :

### Option 1 : Python
```bash
python -m http.server 8000
# Ouvrir : http://localhost:8000
```

### Option 2 : Node.js
```bash
npx http-server -p 8000
# Ouvrir : http://localhost:8000
```

### Option 3 : PHP
```bash
php -S localhost:8000
# Ouvrir : http://localhost:8000
```

## 🔒 Sécurité et confidentialité

### Données utilisateur
- ✅ Toutes les données restent sur l'appareil de l'utilisateur
- ✅ Aucune donnée n'est envoyée à des serveurs externes
- ✅ Les photos sont encodées en base64 localement
- ✅ Export JSON sous contrôle total de l'utilisateur

### Permissions
- 📍 **Géolocalisation** : Utilisée uniquement pour le champ "Lieu"
- 📷 **Caméra** : Utilisée uniquement pour la prise de photos
- 🎤 **Microphone** : Utilisé uniquement pour la dictée vocale

### APIs externes
- **Nominatim (OpenStreetMap)** : Géocodage et recherche d'adresse
  - Aucune donnée personnelle envoyée
  - Requêtes anonymes
  - Conforme RGPD

## 🤝 Contribution

### Signaler un bug
Ouvrez une [Issue](https://github.com/NRielo/Formulaire_intervention_chantier/issues) avec :
- Description du problème
- Étapes pour reproduire
- Navigateur et appareil utilisés
- Captures d'écran si possible

### Proposer une amélioration
Ouvrez une [Issue](https://github.com/NRielo/Formulaire_intervention_chantier/issues) avec le tag `enhancement`

## 📊 Roadmap

### ✅ Phase 1 (Actuel)
- [x] Formulaire mobile responsive
- [x] Géolocalisation
- [x] Prise de photos
- [x] Dictée vocale
- [x] Calculs automatiques avec code couleur
- [x] Export JSON

### 🔄 Phase 2 (En cours)
- [ ] Export PDF professionnel
- [ ] Sauvegarde automatique locale
- [ ] Templates prédéfinis
- [ ] Mode hors ligne complet

### 📅 Phase 3 (Prévu)
- [ ] Intégration Google Drive
- [ ] Signature digitale
- [ ] Historique des chantiers
- [ ] Dashboard analytics

### 🔮 Phase 4 (Futur)
- [ ] Mode multi-utilisateurs
- [ ] Comparaison automatique avec chantiers précédents
- [ ] Alertes intelligentes
- [ ] Application mobile native

## 📞 Support

Pour toute question ou assistance :
- 📧 Email : [contact@ielo.fr](mailto:contact@ielo.fr)
- 🐛 Issues : [GitHub Issues](https://github.com/NRielo/Formulaire_intervention_chantier/issues)
- 📚 Documentation : [Dossier docs/](docs/)

## 📄 Licence

© 2025 ielo - Tous droits réservés

Ce formulaire est propriété de ielo. Utilisation autorisée uniquement pour les activités officielles de ielo.

## 🙏 Remerciements

- **OpenStreetMap** pour les données cartographiques
- **Nominatim** pour le géocodage
- **Leaflet** pour l'affichage des cartes
- Tous les utilisateurs terrain pour leurs retours

---

**Version** : 1.0.0  
**Dernière mise à jour** : Janvier 2025  
**Mainteneur** : NRielo

⭐ N'oubliez pas de mettre une étoile si ce projet vous est utile !
