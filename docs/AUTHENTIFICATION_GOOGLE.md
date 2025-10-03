# 🔐 Authentification Google OAuth - Guide complet

## 🎯 Objectif

Restreindre l'accès au formulaire aux seuls utilisateurs autorisés avec un compte Google (@ielo.fr).

## ⚙️ Configuration Google Cloud (15 minutes)

### Étape 1 : Créer un projet Google Cloud

1. Allez sur https://console.cloud.google.com
2. Cliquez sur "Sélectionner un projet" → "Nouveau projet"
3. Nom du projet : `Formulaire REX ielo`
4. Cliquez sur "Créer"

### Étape 2 : Activer l'API Google Sign-In

1. Dans le menu, allez sur "APIs & Services" → "Library"
2. Recherchez "Google+ API" ou "Google Identity"
3. Cliquez sur "Enable"

### Étape 3 : Configurer l'écran de consentement OAuth

1. Menu → "APIs & Services" → "OAuth consent screen"
2. Type : **Internal** (si vous avez Google Workspace)
   - Ou **External** (si compte Google standard)
3. Remplissez :
   - **App name** : Formulaire REX Chantiers ielo
   - **User support email** : votre email
   - **Developer contact** : votre email
4. Cliquez "Save and Continue"
5. Scopes : Laissez par défaut
6. Cliquez "Save and Continue"

### Étape 4 : Créer des identifiants OAuth 2.0

1. Menu → "APIs & Services" → "Credentials"
2. Cliquez "Create Credentials" → "OAuth client ID"
3. Type d'application : **Application Web**
4. Nom : `Formulaire REX Web`
5. **Origines JavaScript autorisées** :
   ```
   https://nrielo.github.io
   ```
6. **URI de redirection autorisés** :
   ```
   https://nrielo.github.io/Formulaire_intervention_chantier/
   ```
7. Cliquez "Create"

### Étape 5 : Récupérer l'ID client

Vous obtiendrez un **Client ID** qui ressemble à :
```
123456789-abcdefghijklmnop.apps.googleusercontent.com
```

⚠️ **Copiez-le, vous en aurez besoin !**

## 💻 Code à ajouter au formulaire

### 1. Ajouter le script Google dans le `<head>`

```html
<script src="https://accounts.google.com/gsi/client" async defer></script>
```

### 2. Remplacer la section d'authentification

Remplacez tout le code entre `<div id="loginScreen">` et `</div>` par :

```html
<div id="loginScreen">
    <div class="login-box">
        <div class="login-logo">🌾</div>
        <h1 class="login-title">REX Chantier ielo</h1>
        <p class="login-subtitle">Connexion avec Google</p>
        
        <div id="g_id_onload"
             data-client_id="VOTRE_CLIENT_ID.apps.googleusercontent.com"
             data-callback="handleCredentialResponse"
             data-auto_prompt="false">
        </div>
        
        <div class="g_id_signin"
             data-type="standard"
             data-size="large"
             data-theme="outline"
             data-text="sign_in_with"
             data-shape="rectangular"
             data-logo_alignment="left">
        </div>
        
        <div id="loginError" class="login-error"></div>
        
        <div class="login-info">
            🔒 Accès réservé aux collaborateurs ielo<br>
            Connectez-vous avec votre compte Google @ielo.fr
        </div>
    </div>
</div>
```

### 3. Remplacer le JavaScript d'authentification

```javascript
// ============================================
// AUTHENTIFICATION GOOGLE
// ============================================

// Liste des emails autorisés (optionnel)
const AUTHORIZED_EMAILS = [
    'user1@ielo.fr',
    'user2@ielo.fr',
    'admin@ielo.fr'
    // Ajoutez les emails autorisés ici
];

// Ou autorisez tous les emails d'un domaine
const AUTHORIZED_DOMAIN = '@ielo.fr';

function handleCredentialResponse(response) {
    // Décoder le JWT token
    const responsePayload = parseJwt(response.credential);
    
    const email = responsePayload.email;
    const name = responsePayload.name;
    const picture = responsePayload.picture;
    
    console.log('Utilisateur connecté:', name, email);
    
    // Vérifier si l'email est autorisé
    const isAuthorized = checkAuthorization(email);
    
    if (isAuthorized) {
        // Authentification réussie
        document.getElementById('loginScreen').classList.add('hidden');
        document.getElementById('mainContent').classList.add('visible');
        
        // Sauvegarder les infos utilisateur
        sessionStorage.setItem('authenticated', 'true');
        sessionStorage.setItem('userEmail', email);
        sessionStorage.setItem('userName', name);
        sessionStorage.setItem('userPicture', picture);
        
        // Afficher un message de bienvenue
        showToast(`👋 Bienvenue ${name} !`);
        
        // Initialiser le formulaire
        updateProgress();
        document.getElementById('date').valueAsDate = new Date();
        
        // Logger la connexion (optionnel)
        logAccess(name, email);
    } else {
        // Email non autorisé
        const error = document.getElementById('loginError');
        error.textContent = `❌ Accès refusé. L'email ${email} n'est pas autorisé.`;
        error.classList.add('show');
    }
}

function checkAuthorization(email) {
    // Méthode 1 : Vérifier si l'email est dans la liste
    if (AUTHORIZED_EMAILS.length > 0) {
        return AUTHORIZED_EMAILS.includes(email);
    }
    
    // Méthode 2 : Vérifier le domaine
    if (AUTHORIZED_DOMAIN) {
        return email.endsWith(AUTHORIZED_DOMAIN);
    }
    
    // Par défaut : refuser
    return false;
}

function parseJwt(token) {
    const base64Url = token.split('.')[1];
    const base64 = base64Url.replace(/-/g, '+').replace(/_/g, '/');
    const jsonPayload = decodeURIComponent(atob(base64).split('').map(function(c) {
        return '%' + ('00' + c.charCodeAt(0).toString(16)).slice(-2);
    }).join(''));
    return JSON.parse(jsonPayload);
}

function logAccess(name, email) {
    // Vous pouvez logger les accès dans un service externe
    // Par exemple : Google Analytics, un webhook, etc.
    console.log(`[${new Date().toISOString()}] Accès de ${name} (${email})`);
    
    // Exemple d'envoi vers un webhook (optionnel)
    /*
    fetch('https://votre-webhook.com/log', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
            timestamp: new Date().toISOString(),
            user: name,
            email: email,
            action: 'login'
        })
    });
    */
}

// Vérifier si déjà authentifié
window.addEventListener('DOMContentLoaded', () => {
    if (sessionStorage.getItem('authenticated') === 'true') {
        document.getElementById('loginScreen').classList.add('hidden');
        document.getElementById('mainContent').classList.add('visible');
        updateProgress();
        document.getElementById('date').valueAsDate = new Date();
        
        const userName = sessionStorage.getItem('userName');
        if (userName) {
            showToast(`👋 Bon retour ${userName} !`);
        }
    }
});

// Bouton de déconnexion (optionnel)
function logout() {
    sessionStorage.clear();
    location.reload();
}
```

### 4. Ajouter un bouton de déconnexion (optionnel)

Dans le header du formulaire, ajoutez :

```html
<div class="header">
    <h1>🌾 REX Chantier</h1>
    <div class="header-subtitle">
        Retour d'expérience - ielo
        <button onclick="logout()" style="float: right; background: rgba(255,255,255,0.2); border: none; color: white; padding: 5px 10px; border-radius: 5px; cursor: pointer;">
            🚪 Déconnexion
        </button>
    </div>
    <div class="progress-bar">
        <div class="progress-fill" id="progressFill"></div>
    </div>
</div>
```

## 🎨 Personnalisation du bouton Google

Vous pouvez personnaliser l'apparence du bouton en modifiant les attributs `data-*` :

```html
<div class="g_id_signin"
     data-type="standard"          <!-- standard, icon -->
     data-size="large"              <!-- large, medium, small -->
     data-theme="outline"           <!-- outline, filled_blue, filled_black -->
     data-text="sign_in_with"       <!-- signin_with, signup_with, continue_with, signin -->
     data-shape="rectangular"       <!-- rectangular, pill, circle, square -->
     data-logo_alignment="left">    <!-- left, center -->
</div>
```

## 🔒 Sécurité avancée

### Restriction par domaine email

Pour autoriser uniquement les emails @ielo.fr :

```javascript
const AUTHORIZED_DOMAIN = '@ielo.fr';

function checkAuthorization(email) {
    return email.endsWith(AUTHORIZED_DOMAIN);
}
```

### Liste blanche d'emails

Pour autoriser uniquement certains emails :

```javascript
const AUTHORIZED_EMAILS = [
    'john.doe@ielo.fr',
    'jane.smith@ielo.fr',
    'admin@ielo.fr'
];

function checkAuthorization(email) {
    return AUTHORIZED_EMAILS.includes(email);
}
```

### Combinaison des deux

```javascript
function checkAuthorization(email) {
    // Vérifier d'abord la liste blanche
    if (AUTHORIZED_EMAILS.includes(email)) return true;
    
    // Sinon vérifier le domaine
    if (email.endsWith(AUTHORIZED_DOMAIN)) return true;
    
    return false;
}
```

## 📊 Logs d'accès

### Option 1 : Console du navigateur (simple)

Déjà implémenté dans le code ci-dessus.

### Option 2 : Google Analytics (recommandé)

```javascript
function logAccess(name, email) {
    gtag('event', 'login', {
        'event_category': 'authentication',
        'event_label': email,
        'value': 1
    });
}
```

### Option 3 : Webhook externe

```javascript
function logAccess(name, email) {
    fetch('https://hooks.zapier.com/hooks/catch/XXXXX/YYYYY/', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
            timestamp: new Date().toISOString(),
            user: name,
            email: email,
            action: 'formulaire_access'
        })
    });
}
```

### Option 4 : Google Sheets (via Apps Script)

Créez un Google Apps Script qui reçoit les logs et les écrit dans un Sheet.

## 🧪 Tester l'authentification

### En local (ne fonctionnera pas)

L'authentification Google nécessite HTTPS et un domaine autorisé.

### Sur GitHub Pages (fonctionne)

1. Déployez sur GitHub Pages
2. Ajoutez l'URL dans Google Cloud Console
3. Testez avec votre compte Google

### Test de la liste blanche

1. Connectez-vous avec un email autorisé → ✅ Accès
2. Connectez-vous avec un email non autorisé → ❌ Refus

## 💡 Avantages de Google OAuth

| Avantage | Description |
|----------|-------------|
| 🔐 Sécurisé | Pas de mot de passe à gérer |
| 👤 Identification | Vous savez qui accède au formulaire |
| 📊 Traçabilité | Logs automatiques des accès |
| 🚀 Simple | Connexion en 1 clic |
| 🔄 SSO | Si vous utilisez Google Workspace |
| ⚡ Rapide | Pas besoin de créer de compte |

## ⚠️ Limitations

- Nécessite une connexion Internet
- Nécessite un compte Google
- Configuration initiale plus complexe
- Dépendance à Google

## 🆚 Comparaison des méthodes

| Critère | Mot de passe simple | Google OAuth |
|---------|---------------------|--------------|
| Sécurité | ⭐⭐ | ⭐⭐⭐⭐⭐ |
| Simplicité | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |
| Traçabilité | ❌ | ✅ |
| Coût | Gratuit | Gratuit |
| Configuration | 2 min | 15 min |
| Maintenance | Faible | Aucune |

## 🎯 Recommandation

**Pour démarrer rapidement :** Utilisez le mot de passe simple (déjà fait)

**Pour la production :** Implémentez Google OAuth selon ce guide

**Idéal :** Commencez avec mot de passe, puis migrez vers OAuth quand vous êtes prêt

## 📞 Besoin d'aide ?

Si vous voulez implémenter Google OAuth, je peux :
1. Créer le code complet
2. Vous guider dans la configuration Google Cloud
3. Tester avec vous

Voulez-vous que je crée une version complète avec Google OAuth ?
