# Intégration Google Drive - Formulaire REX Chantiers

## 🎯 Objectif
Permettre aux utilisateurs d'enregistrer automatiquement leurs rapports et photos dans Google Drive après authentification.

## ✅ Ce qui est possible

### Option 1 : Upload direct avec Google Drive API (RECOMMANDÉ)
**Avantages :**
- Upload automatique des rapports JSON
- Upload automatique des photos
- Organisation en dossiers par date/chantier
- Synchronisation avec le compte Google de l'utilisateur
- Fonctionne sur tous les appareils

**Limitations :**
- Nécessite une configuration Google Cloud Platform
- Nécessite un serveur backend (Node.js, Python, PHP...)
- Coût : Gratuit jusqu'à 1TB de stockage par utilisateur

### Option 2 : Google Drive Picker (SIMPLE)
**Avantages :**
- Plus simple à implémenter
- Pas besoin de backend complet
- L'utilisateur choisit où sauvegarder

**Limitations :**
- L'utilisateur doit choisir le dossier à chaque fois
- Moins automatisé

### Option 3 : Export + Import manuel
**Avantages :**
- Aucune configuration nécessaire
- Fonctionne immédiatement
- Total contrôle utilisateur

**Limitations :**
- L'utilisateur doit uploader manuellement dans Drive

## 🚀 Solution recommandée pour votre cas

### Configuration hybride : Local + Drive optionnel

#### Étape 1 : Configuration Google Cloud Platform

1. **Créer un projet Google Cloud**
   - Aller sur https://console.cloud.google.com
   - Créer un nouveau projet "ielo-rex-chantiers"
   
2. **Activer l'API Google Drive**
   - Dans le projet, activer "Google Drive API"
   - Activer "Google Picker API"

3. **Créer des identifiants OAuth 2.0**
   - Créer un ID client OAuth 2.0
   - Type : Application Web
   - Origines JavaScript autorisées : Votre domaine HTTPS
   - URI de redirection : Votre domaine + /callback

4. **Obtenir la clé API et l'ID client**
   - Vous recevrez un `CLIENT_ID` et une `API_KEY`

#### Étape 2 : Code d'intégration simplifié

Voici le code à ajouter au formulaire :

```html
<!-- Ajouter dans le <head> -->
<script src="https://apis.google.com/js/api.js"></script>
<script src="https://accounts.google.com/gsi/client"></script>

<script>
// Configuration
const CLIENT_ID = 'VOTRE_CLIENT_ID.apps.googleusercontent.com';
const API_KEY = 'VOTRE_API_KEY';
const SCOPES = 'https://www.googleapis.com/auth/drive.file';

let tokenClient;
let accessToken = null;
let gapiInited = false;
let gisInited = false;

// Initialisation GAPI
function gapiLoaded() {
    gapi.load('client:picker', initializeGapiClient);
}

async function initializeGapiClient() {
    await gapi.client.init({
        apiKey: API_KEY,
        discoveryDocs: ['https://www.googleapis.com/discovery/v1/apis/drive/v3/rest'],
    });
    gapiInited = true;
}

// Initialisation Google Identity Services
function gisLoaded() {
    tokenClient = google.accounts.oauth2.initTokenClient({
        client_id: CLIENT_ID,
        scope: SCOPES,
        callback: '', // sera défini plus tard
    });
    gisInited = true;
}

// Connexion à Google Drive
function connectToGoogleDrive() {
    tokenClient.callback = async (response) => {
        if (response.error !== undefined) {
            throw (response);
        }
        accessToken = response.access_token;
        showToast('✅ Connecté à Google Drive');
    };

    if (accessToken === null) {
        tokenClient.requestAccessToken({prompt: 'consent'});
    } else {
        tokenClient.requestAccessToken({prompt: ''});
    }
}

// Upload vers Google Drive
async function uploadToGoogleDrive(fileName, content, mimeType) {
    const metadata = {
        'name': fileName,
        'mimeType': mimeType
    };

    const form = new FormData();
    form.append('metadata', new Blob([JSON.stringify(metadata)], {type: 'application/json'}));
    form.append('file', new Blob([content], {type: mimeType}));

    const response = await fetch('https://www.googleapis.com/upload/drive/v3/files?uploadType=multipart', {
        method: 'POST',
        headers: new Headers({'Authorization': 'Bearer ' + accessToken}),
        body: form
    });

    return await response.json();
}

// Sauvegarder dans Drive
async function saveToGoogleDrive() {
    if (!accessToken) {
        showToast('⚠️ Veuillez vous connecter à Google Drive');
        connectToGoogleDrive();
        return;
    }

    // Préparer les données
    const formData = new FormData(document.getElementById('rexForm'));
    const data = {};
    
    for (let [key, value] of formData.entries()) {
        data[key] = value;
    }
    
    data.photos = photos;
    data.geolocation = locationData;
    data.timestamp = new Date().toISOString();
    
    const json = JSON.stringify(data, null, 2);
    const fileName = `rex_${data.date || 'chantier'}_${Date.now()}.json`;

    try {
        // Upload du fichier JSON
        await uploadToGoogleDrive(fileName, json, 'application/json');
        
        // Upload des photos si présentes
        for (let i = 0; i < photos.length; i++) {
            const photoBlob = await fetch(photos[i]).then(r => r.blob());
            const photoName = `photo_${i+1}_${Date.now()}.jpg`;
            await uploadToGoogleDrive(photoName, photoBlob, 'image/jpeg');
        }
        
        showToast('✅ Données sauvegardées dans Google Drive !');
    } catch (error) {
        console.error('Erreur upload:', error);
        showToast('⚠️ Erreur lors de la sauvegarde');
    }
}
</script>
```

#### Étape 3 : Modifications du formulaire

Ajouter un bouton de connexion Google Drive :

```html
<!-- Dans la barre du bas -->
<div class="bottom-bar">
    <div class="btn-group">
        <button type="button" class="btn btn-primary" onclick="saveForm()">
            💾 Enregistrer local
        </button>
        <button type="button" class="btn btn-primary" onclick="saveToGoogleDrive()">
            ☁️ Drive
        </button>
        <button type="button" class="btn btn-outline" onclick="shareForm()">
            📤 Partager
        </button>
    </div>
</div>

<!-- Ajouter un indicateur de statut Google Drive -->
<div class="drive-status" id="driveStatus">
    <button onclick="connectToGoogleDrive()" class="btn-outline">
        🔗 Connecter Google Drive
    </button>
</div>
```

## 📱 Solution alternative SANS serveur (pour commencer)

Si vous ne voulez pas configurer Google Cloud immédiatement :

### 1. Export local + Upload manuel
L'utilisateur :
1. Remplit le formulaire
2. Clique sur "Enregistrer"
3. Le fichier JSON est téléchargé
4. L'utilisateur ouvre Google Drive sur son téléphone
5. Upload manuel du fichier

### 2. Partage natif (Mobile)
Utiliser l'API Web Share pour partager directement vers Drive :

```javascript
async function shareToGoogleDrive() {
    const data = prepareFormData();
    const blob = new Blob([JSON.stringify(data, null, 2)], {type: 'application/json'});
    const file = new File([blob], `rex_${Date.now()}.json`, {type: 'application/json'});

    if (navigator.canShare && navigator.canShare({files: [file]})) {
        try {
            await navigator.share({
                files: [file],
                title: 'REX Chantier',
                text: 'Rapport de chantier'
            });
        } catch (error) {
            console.log('Partage annulé');
        }
    }
}
```

L'utilisateur peut alors choisir Google Drive dans la liste de partage !

## 🎯 Recommandation finale

**Pour démarrer rapidement (MAINTENANT) :**
1. Utilisez la version mobile simplifiée
2. Export JSON local
3. Partage natif vers Drive sur mobile

**Pour la version finale (PLUS TARD) :**
1. Configurez Google Cloud Platform
2. Ajoutez l'authentification OAuth
3. Upload automatique vers un dossier Drive structuré

## 💰 Coûts

- **Google Drive API** : Gratuit (15 GB par compte Google)
- **Quota API** : 1 milliard de requêtes/jour (gratuit)
- **Hébergement** : 
  - GitHub Pages : Gratuit
  - Netlify : Gratuit
  - Firebase Hosting : Gratuit pour usage modéré

## 🔒 Sécurité

Avec OAuth 2.0 :
- L'utilisateur contrôle l'accès
- Le formulaire n'a accès qu'aux fichiers qu'il crée
- Révocation possible à tout moment
- Aucun stockage de mot de passe

## 📞 Besoin d'aide ?

Si vous voulez implémenter l'intégration Google Drive complète, je peux :
1. Vous guider pas à pas dans la configuration Google Cloud
2. Créer le code d'authentification complet
3. Vous montrer comment structurer les dossiers Drive automatiquement

Voulez-vous que je crée une version avec intégration Google Drive complète ?
