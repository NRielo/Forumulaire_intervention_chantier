# Guide de Test - Formulaire REX Chantiers ielo

## 🧪 Comment tester l'outil

### Option 1 : Test rapide en local (votre situation actuelle)
1. Ouvrez le fichier `formulaire_rex_chantiers.html` directement dans votre navigateur
2. **Fonctionnalités disponibles :**
   - ✅ Saisie de tous les champs
   - ✅ Recherche d'adresse avec autocomplétion
   - ✅ Import de photos (sur mobile : capture directe)
   - ✅ Calculs automatiques
   - ✅ Export JSON
   - ❌ Géolocalisation GPS (nécessite HTTPS)
   - ❌ Caméra web (nécessite HTTPS)

### Option 2 : Test avec serveur local (recommandé pour tester toutes les fonctionnalités)

#### Méthode A : Python (le plus simple)
```bash
# Dans le dossier contenant le fichier HTML
python -m http.server 8000
# Puis ouvrez : http://localhost:8000/formulaire_rex_chantiers.html
```

#### Méthode B : Node.js
```bash
# Installer http-server (une seule fois)
npm install -g http-server

# Lancer le serveur
http-server -p 8000
# Puis ouvrez : http://localhost:8000/formulaire_rex_chantiers.html
```

#### Méthode C : PHP
```bash
php -S localhost:8000
# Puis ouvrez : http://localhost:8000/formulaire_rex_chantiers.html
```

### Option 3 : Test en ligne (pour tester avec HTTPS)
1. Créez un compte gratuit sur l'un de ces services :
   - **GitHub Pages** (gratuit, facile)
   - **Netlify** (gratuit, drag & drop)
   - **Vercel** (gratuit)

2. Uploadez le fichier HTML
3. Vous obtiendrez une URL HTTPS
4. Toutes les fonctionnalités seront disponibles (géolocalisation, caméra)

### Option 4 : Test sur mobile/tablette
1. **Depuis votre ordinateur :**
   - Lancez un serveur local (option 2)
   - Trouvez votre adresse IP locale : `ipconfig` (Windows) ou `ifconfig` (Mac/Linux)
   - Sur votre mobile, ouvrez : `http://[VOTRE_IP]:8000/formulaire_rex_chantiers.html`
   
2. **Transfert direct :**
   - Envoyez le fichier HTML par email
   - Ouvrez-le depuis votre mobile
   - (Note : géolocalisation/caméra ne fonctionneront pas sans serveur)

## 📋 Checklist de test

### Tests de base
- [ ] Remplir tous les champs du formulaire
- [ ] Vérifier les calculs automatiques (volume, masse volumique)
- [ ] Tester la recherche d'adresse
- [ ] Importer plusieurs photos
- [ ] Exporter en JSON
- [ ] Réinitialiser le formulaire

### Tests des photos
- [ ] Importer 1 photo
- [ ] Importer plusieurs photos en même temps
- [ ] Supprimer une photo
- [ ] Vérifier l'affichage en grille
- [ ] Sur mobile : tester la capture directe via "Importer"

### Tests de géolocalisation (nécessite serveur local ou HTTPS)
- [ ] Rechercher une adresse manuellement
- [ ] Sélectionner dans les suggestions
- [ ] Vérifier l'affichage de la carte
- [ ] Cliquer sur le bouton géolocalisation
- [ ] Vérifier les coordonnées GPS affichées

### Tests sur différents appareils
- [ ] Desktop (Chrome)
- [ ] Desktop (Firefox)
- [ ] Desktop (Safari)
- [ ] Mobile Android (Chrome)
- [ ] Mobile iOS (Safari)
- [ ] Tablette

### Tests de sécurité
- [ ] Tester avec un fichier image > 10 MB (doit être refusé)
- [ ] Tester avec un fichier non-image (doit être refusé)
- [ ] Tester les permissions (accepter/refuser)
- [ ] Vérifier que les données restent locales

## 🐛 Problèmes courants et solutions

### "Géolocalisation refusée"
**Cause :** Fichier ouvert en mode local (file://)
**Solution :** Utilisez un serveur local ou HTTPS

### "Caméra non disponible"
**Cause :** Contexte non sécurisé
**Solution :** Utilisez "Importer une photo" (sur mobile, ouvre l'appareil photo)

### Les calculs ne se font pas automatiquement
**Vérification :** Tapez des valeurs numériques valides dans les champs
**Solution :** Vérifiez la console du navigateur (F12)

### Les photos ne s'affichent pas
**Cause possible :** Fichier trop volumineux
**Solution :** Compressez vos images ou limitez à 10 MB

### La recherche d'adresse ne fonctionne pas
**Cause possible :** Pas de connexion Internet
**Solution :** L'API Nominatim nécessite Internet

## 💾 Données de test suggérées

### Exemple de chantier
```
Date: 2025-01-15
Lieu: 12 Rue de la Construction, 75001 Paris
Météo: Ensoleillé, 15°C
Entreprise: EcoBat SARL
Quantité de paille: 2.5 tonnes
Surfaces: 120 m²

Caisson de test:
- Longueur: 2.5 m
- Largeur: 1.2 m
- Hauteur: 3.0 m
- Volume calculé: 9 m³
- Poids nécessaire: 1035 kg

Masse insufflée: 1050 kg
Masse volumique calculée: 116.67 kg/m³
```

## 📊 Résultats attendus

### Calculs automatiques
- Volume = L × l × h
- Poids nécessaire = Volume × 115
- Masse volumique = Masse insufflée / Volume

### Export JSON
Le fichier JSON doit contenir :
- Tous les champs du formulaire
- Les photos (en base64)
- Les coordonnées GPS (si disponibles)
- Les métadonnées (date d'export, version)

## 🚀 Prochaines étapes

Après les tests, si tout fonctionne :
1. Déployer sur un serveur HTTPS pour production
2. Former les utilisateurs terrain
3. Mettre en place un système de backup des exports
4. Envisager l'intégration Google Drive (voir proposition séparée)
