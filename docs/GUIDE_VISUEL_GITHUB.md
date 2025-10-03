# 📸 Guide Visuel - Création du Projet GitHub

## 🎯 Objectif
Mettre en ligne votre formulaire sur GitHub en 10 minutes chrono !

---

## 📥 ÉTAPE 1 : Télécharger les fichiers (1 minute)

### Fichiers à télécharger

Vous avez maintenant **un ZIP prêt à l'emploi** qui contient tout :

📦 **`Formulaire_intervention_chantier.zip`**

Ce ZIP contient :
```
Formulaire_intervention_chantier/
├── index.html                    ← Formulaire mobile (principal)
├── formulaire_complet.html       ← Version complète
├── README.md                     ← Description du projet
├── CHANGELOG.md                  ← Historique des versions
├── CONTRIBUTING.md               ← Guide de contribution
├── LICENSE                       ← Licence
├── .gitignore                    ← Fichiers à ignorer
├── _config.yml                   ← Config GitHub Pages
└── docs/
    ├── QUICKSTART.md
    ├── DEPLOIEMENT_GITHUB.md
    ├── GUIDE_TEST.md
    ├── GOOGLE_DRIVE_INTEGRATION.md
    └── AMELIORATIONS_PROPOSEES.md
```

✅ **Téléchargez et décompressez le ZIP sur votre ordinateur**

---

## 🌐 ÉTAPE 2 : Créer le dépôt GitHub (3 minutes)

### 2.1 - Se connecter à GitHub

1. Allez sur https://github.com
2. Connectez-vous avec votre compte **NRielo**

### 2.2 - Créer un nouveau dépôt

**Action :** Cliquez sur le bouton **"+"** en haut à droite de l'écran

```
[Votre avatar] [+] ↓
```

Puis sélectionnez **"New repository"**

### 2.3 - Configurer le dépôt

Remplissez le formulaire comme suit :

#### Repository name *
```
Formulaire_intervention_chantier
```

#### Description (optionnel)
```
Formulaire à destination des accompagnateurs et des formateurs ielo lors d'interventions sur chantier d'isolation en paille hachée
```

#### Visibilité
- ☑️ **Public** (RECOMMANDÉ - gratuit pour GitHub Pages)
- ☐ Private

#### Initialize this repository with:
- ☑️ **Add a README file** (cochez)
- ☐ Add .gitignore (ne cochez pas, on a déjà le nôtre)
- ☐ Choose a license (ne cochez pas, on a déjà le nôtre)

#### Bouton final
Cliquez sur **"Create repository"** (bouton vert)

🎉 **Votre dépôt est créé !**

---

## 📤 ÉTAPE 3 : Uploader les fichiers (2 minutes)

### 3.1 - Accéder à l'upload

Sur la page de votre nouveau dépôt, vous verrez :

```
NRielo / Formulaire_intervention_chantier
```

Cliquez sur **"uploading an existing file"** dans le message de bienvenue

OU

Cliquez sur **"Add file"** → **"Upload files"**

### 3.2 - Déposer les fichiers

**IMPORTANT :** Uploadez le **CONTENU** du dossier, pas le dossier lui-même !

1. Ouvrez le dossier décompressé `github-project/`
2. **Sélectionnez TOUS les fichiers et dossiers à l'intérieur** :
   - index.html
   - formulaire_complet.html
   - README.md
   - CHANGELOG.md
   - CONTRIBUTING.md
   - LICENSE
   - .gitignore
   - _config.yml
   - docs/ (dossier complet)

3. **Glissez-déposez** tout sur la zone GitHub :
   ```
   ┌─────────────────────────────────────┐
   │  Drag files here to add them to    │
   │  your repository                    │
   │                                     │
   │  or choose your files              │
   └─────────────────────────────────────┘
   ```

4. Attendez que tous les fichiers soient uploadés (barre de progression)

### 3.3 - Committer les fichiers

En bas de la page :

#### Commit message
```
Initial commit - Formulaire REX mobile v1.0
```

#### Extended description (optionnel)
```
- Formulaire mobile-first responsive
- Géolocalisation GPS
- Prise de photos
- Dictée vocale
- Calculs automatiques avec code couleur
- Export JSON
```

#### Bouton
Cliquez sur **"Commit changes"** (bouton vert)

⏳ **Attendez quelques secondes...**

✅ **Vos fichiers sont uploadés !**

---

## 🚀 ÉTAPE 4 : Activer GitHub Pages (2 minutes)

### 4.1 - Accéder aux paramètres

Sur votre dépôt, cliquez sur **"Settings"** (⚙️ icône en haut)

```
< > Code    Issues    Pull requests    Settings ⚙️
```

### 4.2 - Ouvrir la section Pages

Dans le menu de gauche, faites défiler et cliquez sur **"Pages"**

```
General
Access
Branches
> Pages     ← Cliquez ici
Environments
```

### 4.3 - Configurer la source

Dans la section **"Build and deployment"** :

#### Source
Sélectionnez : **Deploy from a branch**

#### Branch
- **Branch:** `main` (ou `master` selon votre cas)
- **Folder:** `/ (root)`

```
Branch: [main ▼]  Folder: [/ (root) ▼]  [Save]
```

Cliquez sur **"Save"**

### 4.4 - Attendre le déploiement

GitHub va construire votre site. Cela prend **1-3 minutes**.

Un message apparaîtra en haut de la page :
```
⏳ Your site is being deployed
```

**Rafraîchissez la page** après 2 minutes (F5)

Vous verrez alors :
```
✅ Your site is live at https://nrielo.github.io/Formulaire_intervention_chantier/
```

🎊 **FÉLICITATIONS ! Votre formulaire est en ligne !**

---

## ✅ ÉTAPE 5 : Tester (2 minutes)

### 5.1 - Cliquer sur l'URL

Cliquez sur le lien :
```
https://nrielo.github.io/Formulaire_intervention_chantier/
```

### 5.2 - Tester sur ordinateur

Vérifiez :
- ✅ Le formulaire s'affiche
- ✅ Vous pouvez remplir les champs
- ✅ La recherche d'adresse fonctionne
- ✅ Les calculs se font automatiquement
- ✅ Le code couleur s'affiche (masse volumique)

### 5.3 - Tester sur mobile

**Option A : Depuis votre téléphone**
1. Ouvrez le navigateur
2. Tapez l'URL : `nrielo.github.io/Formulaire_intervention_chantier`
3. Testez :
   - 📍 Géolocalisation (autorisez l'accès)
   - 📸 Ajout de photos
   - 🎤 Dictée vocale (autorisez le micro)

**Option B : Avec un QR Code**
1. Allez sur https://www.qr-code-generator.com/
2. Collez votre URL
3. Téléchargez le QR Code
4. Scannez avec votre téléphone

---

## 🎨 BONUS : Personnaliser (optionnel)

### Changer la description du dépôt

1. Sur la page principale du dépôt
2. Cliquez sur ⚙️ à droite de "About"
3. Modifiez la description
4. Ajoutez l'URL du site dans "Website"
5. Ajoutez des topics : `formulaire`, `paille`, `construction`, `rex`
6. Cliquez **"Save changes"**

### Ajouter un logo

1. Créez ou trouvez un logo ielo (format PNG, 200x200px recommandé)
2. Uploadez-le dans le dépôt : `logo.png`
3. Éditez le `_config.yml` :
   ```yaml
   logo: logo.png
   ```

---

## 📱 ÉTAPE 6 : Partager avec l'équipe

### Message type à envoyer

```
🌾 Nouveau Formulaire REX Chantiers en ligne !

📱 Accès direct : https://nrielo.github.io/Formulaire_intervention_chantier/

Nouvelles fonctionnalités :
✅ Géolocalisation automatique
✅ Prise de photos sur chantier
✅ Dictée vocale pour observations
✅ Code couleur masse volumique (vert/rouge)
✅ Export JSON

📲 Ajoutez l'URL à vos favoris pour accès rapide !

🔗 QR Code : [insérer image]
```

### Créer une affiche

Créez une affiche A4 avec :
- Logo ielo
- Titre "Formulaire REX Chantiers"
- QR Code (grand format)
- URL écrite en dessous
- "Scannez pour accéder"

Imprimez et affichez :
- Dans les bureaux
- Sur les camions
- Sur les chantiers

---

## 🔄 Mettre à jour le formulaire

### Méthode simple (via web)

1. Allez sur votre dépôt GitHub
2. Cliquez sur le fichier à modifier (ex: `index.html`)
3. Cliquez sur ✏️ **Edit this file**
4. Faites vos modifications
5. Scrollez en bas
6. Message de commit : décrivez ce que vous avez changé
7. Cliquez **"Commit changes"**
8. Attendez 2 minutes → Site mis à jour automatiquement !

---

## 🆘 Problèmes fréquents

### ❌ "Page 404 Not Found"

**Cause :** GitHub Pages n'est pas encore déployé ou mal configuré

**Solutions :**
1. Attendez 2-5 minutes supplémentaires
2. Vérifiez Settings → Pages → Source = `main` branch, `/ (root)`
3. Vérifiez que le fichier s'appelle bien `index.html`
4. Videz le cache (Ctrl + Shift + R)

### ❌ "Le formulaire ne s'affiche pas correctement"

**Solutions :**
1. Vérifiez que vous avez uploadé `index.html` à la racine
2. Ouvrez la console (F12) pour voir les erreurs
3. Testez sur un autre navigateur

### ❌ "La géolocalisation ne fonctionne pas"

**Cause :** Normal si vous testez en `http://` local

**Solution :** Fonctionne automatiquement sur GitHub Pages (HTTPS ✅)

### ❌ "La dictée vocale ne marche pas"

**Solutions :**
1. Autorisez le micro dans les paramètres du navigateur
2. Utilisez Chrome ou Safari (Firefox pas supporté)
3. Vérifiez le HTTPS (icône cadenas dans l'URL)

---

## 🎯 Checklist finale

Avant de partager avec l'équipe :

- [ ] Le dépôt GitHub est créé
- [ ] Tous les fichiers sont uploadés
- [ ] GitHub Pages est activé
- [ ] L'URL fonctionne : `https://nrielo.github.io/Formulaire_intervention_chantier/`
- [ ] Le formulaire s'affiche correctement
- [ ] La géolocalisation fonctionne (sur HTTPS)
- [ ] Les photos peuvent être ajoutées
- [ ] La dictée vocale fonctionne
- [ ] Les calculs se font automatiquement
- [ ] Le code couleur s'affiche (masse volumique)
- [ ] L'export JSON fonctionne
- [ ] Testé sur mobile
- [ ] Testé sur tablette
- [ ] Testé sur différents navigateurs
- [ ] QR Code créé
- [ ] Équipe informée

---

## 🎊 Félicitations !

Votre formulaire est maintenant :
- ✅ En ligne avec URL HTTPS
- ✅ Accessible 24/7
- ✅ Avec toutes les fonctionnalités activées
- ✅ Versionné et sauvegardé
- ✅ Facilement modifiable
- ✅ Gratuit à 100%

**URL à partager :** `https://nrielo.github.io/Formulaire_intervention_chantier/`

---

## 📞 Besoin d'aide ?

Si vous rencontrez un problème :
1. Consultez la section "Problèmes fréquents" ci-dessus
2. Ouvrez une Issue sur GitHub
3. Contactez le support technique ielo

**Bonne utilisation ! 🌾**
