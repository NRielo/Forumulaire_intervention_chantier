# 📤 Configuration Upload Automatique Google Drive

## 🎯 Objectif

Faire en sorte que chaque PDF généré soit **automatiquement uploadé** dans votre dossier Google Drive :
```
https://drive.google.com/drive/folders/1to1C4MLfBvp_W5u7sKo7HEqky5o2lUFK
```

## ⚙️ Configuration Google Cloud (15 minutes)

### Étape 1 : Créer un projet Google Cloud

1. Allez sur https://console.cloud.google.com
2. Cliquez sur le menu déroulant en haut "Sélectionner un projet"
3. Cliquez sur **"Nouveau projet"**
4. **Nom du projet** : `Formulaire REX ielo`
5. Cliquez sur **"Créer"**
6. Attendez quelques secondes que le projet soit créé
7. **Sélectionnez ce projet** dans le menu déroulant

### Étape 2 : Activer l'API Google Drive

1. Dans le menu de gauche (☰), allez sur **"APIs et services"** → **"Bibliothèque"**
2. Dans la barre de recherche, tapez : `Google Drive API`
3. Cliquez sur **"Google Drive API"**
4. Cliquez sur le bouton **"Activer"**
5. Attendez quelques secondes

### Étape 3 : Configurer l'écran de consentement OAuth

1. Dans le menu de gauche, allez sur **"Écran de consentement OAuth"**
2. Sélectionnez le type d'utilisateur :
   - **Interne** : Si vous avez Google Workspace (recommandé)
   - **Externe** : Si vous avez un compte Gmail standard
3. Cliquez sur **"Créer"**

**Remplissez les informations :**

- **Nom de l'application** : `Formulaire REX Chantiers ielo`
- **E-mail d'assistance utilisateur** : votre email
- **Logo** : (optionnel)
- **Domaine de l'application** : `nrielo.github.io`
- **E-mail du développeur** : votre email

4. Cliquez sur **"Enregistrer et continuer"**

**Champs d'application (Scopes) :**
5. Cliquez sur **"Ajouter ou supprimer des champs d'application"**
6. Recherchez : `drive.file`
7. Cochez : **`https://www.googleapis.com/auth/drive.file`**
   - Description : "Afficher et gérer les fichiers Google Drive créés avec cette application"
8. Cliquez sur **"Mettre à jour"**
9. Cliquez sur **"Enregistrer et continuer"**

**Utilisateurs de test (si "Externe") :**
10. Cliquez sur **"Ajouter des utilisateurs"**
11. Ajoutez les emails des personnes autorisées (vous et votre équipe)
12. Cliquez sur **"Enregistrer et continuer"**

13. Cliquez sur **"Retour au tableau de bord"**

### Étape 4 : Créer des identifiants OAuth 2.0

1. Dans le menu de gauche, allez sur **"Identifiants"**
2. Cliquez sur **"+ Créer des identifiants"** en haut
3. Sélectionnez **"ID client OAuth"**

**Configurez l'ID client :**

4. **Type d'application** : `Application Web`
5. **Nom** : `Formulaire REX Web Client`

**Origines JavaScript autorisées :**
6. Cliquez sur **"+ Ajouter un URI"**
7. Ajoutez : `https://nrielo.github.io`

**URI de redirection autorisés :**
8. Cliquez sur **"+ Ajouter un URI"**
9. Ajoutez : `https://nrielo.github.io/Formulaire_intervention_chantier`

10. Cliquez sur **"Créer"**

### Étape 5 : Récupérer vos identifiants

Une fenêtre s'ouvre avec vos identifiants :

**CLIENT ID** (ressemble à) :
```
123456789012-abcdefghijklmnopqrstuvwxyz123456.apps.googleusercontent.com
```

**CLIENT SECRET** : (pas nécessaire pour notre cas)

⚠️ **COPIEZ le Client ID, vous en aurez besoin !**

### Étape 6 : Créer une clé API (optionnel mais recommandé)

1. Toujours dans **"Identifiants"**
2. Cliquez sur **"+ Créer des identifiants"**
3. Sélectionnez **"Clé API"**
4. Une clé est générée (ressemble à) : `AIzaSyABC123def456GHI789jkl`
5. **Copiez cette clé**
6. Cliquez sur **"Restreindre la clé"**

**Restrictions :**
7. **Nom de la clé** : `Formulaire REX API Key`
8. **Restrictions pour l'application** :
   - Sélectionnez "Références HTTP (sites web)"
   - Ajoutez : `https://nrielo.github.io/Formulaire_intervention_chantier/*`
9. **Restrictions relatives aux API** :
   - Sélectionnez "Restreindre la clé"
   - Cochez : `Google Drive API`
10. Cliquez sur **"Enregistrer"**

---

## 💻 Configurer le formulaire

### Étape 7 : Modifier le fichier index.html

1. Allez sur votre dépôt GitHub
2. Cliquez sur `index.html`
3. Cliquez sur ✏️ **"Edit this file"**

**Trouvez ces lignes (vers la ligne 850) :**

```javascript
const CLIENT_ID = 'VOTRE_CLIENT_ID.apps.googleusercontent.com';
const API_KEY = 'VOTRE_API_KEY';
```

**Remplacez par vos vraies valeurs :**

```javascript
const CLIENT_ID = '123456789012-abcdefghijklmnopqrstuvwxyz123456.apps.googleusercontent.com';
const API_KEY = 'AIzaSyABC123def456GHI789jkl';
```

⚠️ **Utilisez VOS vraies valeurs récupérées à l'étape 5 et 6 !**

### Étape 8 : Commit et déployer

1. Scrollez en bas
2. **Message de commit** : `Config: Add Google Drive credentials`
3. Cliquez sur **"Commit changes"**
4. Attendez 2-3 minutes que GitHub Pages redéploie

---

## 🧪 Tester l'upload automatique

### Test complet

1. Allez sur votre formulaire : `https://nrielo.github.io/Formulaire_intervention_chantier/`
2. Connectez-vous avec le mot de passe
3. **Important** : Cliquez d'abord sur **"🔗 Connecter Drive"**
4. Une popup Google s'ouvre :
   - Sélectionnez votre compte Google
   - Autorisez l'accès (cochez les permissions)
   - Cliquez sur "Autoriser"
5. Vous voyez : **"✅ Connecté à Google Drive !"**

6. Remplissez le formulaire normalement
7. Ajoutez des photos
8. Cliquez sur **"📄 Générer PDF & Upload Drive"**

**Résultat attendu :**
- ✅ PDF généré et téléchargé sur votre ordinateur
- ✅ Message : "🎉 PDF uploadé sur Google Drive !"
- ✅ Popup : "PDF uploadé avec succès ! Voulez-vous l'ouvrir dans Drive ?"
- ✅ Le PDF apparaît dans votre dossier Drive : https://drive.google.com/drive/folders/1to1C4MLfBvp_W5u7sKo7HEqky5o2lUFK

---

## 📋 Vérification dans Google Drive

1. Allez sur votre dossier Drive : https://drive.google.com/drive/folders/1to1C4MLfBvp_W5u7sKo7HEqky5o2lUFK
2. Vous devriez voir un nouveau fichier PDF :
   - Nom : `REX_2025-01-03_1234567890.pdf`
   - Type : PDF
   - Avec toutes les photos incluses
3. Ouvrez-le pour vérifier le contenu

---

## 🎨 Format du PDF généré

Le PDF contient :

**Page 1 - Informations du chantier :**
- En-tête ielo avec logo 🌾
- Date et lieu
- Coordonnées GPS
- Entreprise et météo
- Quantités (paille, surfaces)
- Caisson de test :
  - Dimensions et volume
  - Masse volumique avec **code couleur** (vert/rouge)
- Observations

**Pages suivantes - Photos :**
- 3 photos par page
- Numérotation (Photo 1/5, etc.)
- Haute qualité

**Footer toutes pages :**
- Numéro de page
- Date et heure de génération

---

## 🔒 Permissions et sécurité

### Qui peut uploader ?

Seules les personnes qui :
1. Ont le mot de passe du formulaire
2. Se connectent avec leur compte Google autorisé
3. Autorisent l'accès à leur Drive

### Les fichiers sont créés par qui ?

Les PDF sont créés **au nom de l'utilisateur connecté** (pas au nom d'un compte de service).

### Comment partager le dossier ?

1. Ouvrez le dossier Drive
2. Clic droit → "Partager"
3. Ajoutez les emails de votre équipe
4. Permissions recommandées :
   - **Éditeur** : Peut ajouter/modifier/supprimer
   - **Lecteur** : Peut seulement voir

---

## ⚠️ Résolution de problèmes

### "Erreur : redirect_uri_mismatch"

**Cause :** L'URI de redirection ne correspond pas

**Solution :**
1. Retournez dans Google Cloud Console
2. Identifiants → Cliquez sur votre Client ID OAuth
3. Vérifiez que les URI autorisés incluent EXACTEMENT :
   - Origine : `https://nrielo.github.io`
   - Redirection : `https://nrielo.github.io/Formulaire_intervention_chantier`
4. Pas de "/" à la fin !

### "Erreur : access_denied"

**Cause :** L'utilisateur n'est pas dans la liste des testeurs (si app "Externe")

**Solution :**
1. Google Cloud Console → Écran de consentement OAuth
2. Ajoutez l'email dans "Utilisateurs de test"
3. Ou passez l'app en "Publié" (production)

### "Le PDF se télécharge mais pas d'upload Drive"

**Causes possibles :**
1. Pas connecté à Drive → Cliquez sur "🔗 Connecter Drive"
2. Token expiré → Reconnectez-vous
3. CLIENT_ID incorrect → Vérifiez dans le code

### "Popup bloquée"

**Solution :**
- Autorisez les popups pour nrielo.github.io dans votre navigateur

### "Erreur 403 : Insufficient Permission"

**Cause :** Les scopes OAuth ne sont pas corrects

**Solution :**
1. Vérifiez que le scope inclut : `https://www.googleapis.com/auth/drive.file`
2. Déconnectez-vous et reconnectez-vous pour forcer le nouveau consentement

---

## 🚀 Utilisation en production

### Workflow recommandé

**Premier utilisateur du jour :**
1. Ouvre le formulaire
2. Se connecte (mot de passe)
3. Clique sur "🔗 Connecter Drive"
4. Autorise l'accès Google
5. Remplit le formulaire
6. Génère le PDF → Upload automatique

**Utilisateurs suivants (même session) :**
1. Ouvrent le formulaire
2. Se connectent (mot de passe)
3. Remplissent le formulaire
4. Génèrent le PDF → Upload automatique ✅
   (Pas besoin de reconnecter Drive si même navigateur/session)

### Expiration de la session

La connexion Google Drive expire :
- À la fermeture du navigateur
- Après 1 heure d'inactivité
- En navigation privée : immédiatement

**Solution :** Cliquez à nouveau sur "🔗 Connecter Drive"

---

## 💡 Améliorations futures

### Option 1 : Upload sans demander

Connecter automatiquement à Drive au chargement du formulaire :

```javascript
window.addEventListener('DOMContentLoaded', () => {
    // Connexion auto
    authenticateGoogleDrive();
});
```

### Option 2 : Compte de service

Pour un upload centralisé (tous les PDF sous le même compte) :
- Créer un compte de service
- Partager le dossier Drive avec ce compte
- Plus complexe mais plus professionnel

### Option 3 : Notification email

Envoyer un email à l'équipe à chaque nouveau PDF uploadé :
- Via Google Apps Script
- Ou webhook Zapier/Make

---

## ✅ Checklist de configuration

- [ ] Projet Google Cloud créé
- [ ] API Google Drive activée
- [ ] Écran de consentement OAuth configuré
- [ ] ID client OAuth créé
- [ ] Origines JavaScript ajoutées
- [ ] URI de redirection ajoutés
- [ ] Clé API créée (optionnel)
- [ ] CLIENT_ID copié et collé dans index.html
- [ ] API_KEY copiée et collée dans index.html (optionnel)
- [ ] Fichier commité sur GitHub
- [ ] Attendu 2-3 minutes de redéploiement
- [ ] Testé la connexion Drive
- [ ] Testé la génération de PDF
- [ ] Testé l'upload Drive
- [ ] Vérifié le PDF dans le dossier Drive

---

## 📞 Support

Si vous rencontrez des problèmes :
1. Vérifiez la console du navigateur (F12) pour les erreurs
2. Vérifiez que les identifiants sont corrects
3. Vérifiez les permissions du dossier Drive
4. Reconnectez-vous à Google Drive

---

**Temps total de configuration : 15 minutes**
**Résultat : Upload automatique de PDF avec photos vers Drive !** 🎉
