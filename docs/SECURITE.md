# 🔐 Guide de Sécurité - Options d'authentification

## 🎯 Résumé des options

Vous avez **3 options** pour sécuriser l'accès au formulaire :

### ✅ OPTION 1 : Mot de passe simple (IMPLÉMENTÉE)

**État :** ✅ Déjà dans le fichier index.html

**Fonctionnement :**
- Un mot de passe unique partagé
- Saisi à la première connexion
- Session maintenue jusqu'à fermeture du navigateur

**Mot de passe par défaut :** `ielo2025`

⚠️ **IMPORTANT : Changez ce mot de passe avant de déployer !**

**Comment changer le mot de passe :**

1. Ouvrez `index.html`
2. Trouvez la ligne :
   ```javascript
   const CORRECT_PASSWORD = "ielo2025";
   ```
3. Remplacez par votre mot de passe :
   ```javascript
   const CORRECT_PASSWORD = "VotreMotDePasseSecurise2025!";
   ```
4. Sauvegardez

**Avantages :**
- ✅ Simple et rapide
- ✅ Fonctionne immédiatement
- ✅ Aucune configuration externe
- ✅ Gratuit

**Inconvénients :**
- ⚠️ Mot de passe partagé entre tous
- ⚠️ Pas de traçabilité individuelle
- ⚠️ Visible dans le code source

**Sécurité : ⭐⭐ / ⭐⭐⭐⭐⭐**

---

### ⭐ OPTION 2 : Google OAuth (RECOMMANDÉE)

**État :** 📖 Guide complet fourni

**Fonctionnement :**
- Connexion avec compte Google
- Peut restreindre à @ielo.fr
- Peut autoriser uniquement certains emails
- Logs automatiques

**Configuration requise :**
- Compte Google Cloud (gratuit)
- 15 minutes de configuration
- Suivre le guide `docs/AUTHENTIFICATION_GOOGLE.md`

**Avantages :**
- ✅ Très sécurisé
- ✅ Traçabilité complète (qui, quand)
- ✅ Pas de mot de passe à gérer
- ✅ Single Sign-On si Google Workspace
- ✅ Révocation d'accès facile

**Inconvénients :**
- ⚠️ Configuration initiale plus complexe
- ⚠️ Nécessite compte Google pour chaque utilisateur
- ⚠️ Dépendance à Google

**Sécurité : ⭐⭐⭐⭐⭐ / ⭐⭐⭐⭐⭐**

---

### 🔒 OPTION 3 : Dépôt GitHub privé

**État :** 📖 Instructions ci-dessous

**Fonctionnement :**
- Le dépôt GitHub devient privé
- Seuls les membres autorisés peuvent voir le code
- GitHub Pages nécessite GitHub Pro

**Configuration requise :**
- GitHub Pro (4$/mois)
- Ou GitHub Team (44$/mois pour une organisation)

**Avantages :**
- ✅ Code source non visible publiquement
- ✅ Gestion des accès via GitHub
- ✅ Logs d'accès GitHub

**Inconvénients :**
- ⚠️ Payant
- ⚠️ Chaque utilisateur doit avoir un compte GitHub
- ⚠️ Configuration des permissions complexe

**Sécurité : ⭐⭐⭐⭐ / ⭐⭐⭐⭐⭐**

---

## 🎯 Quelle option choisir ?

### Pour démarrer MAINTENANT (5 minutes)
➜ **Option 1 : Mot de passe simple**
- Changez le mot de passe dans le code
- Déployez
- Partagez le mot de passe par canal sécurisé (SMS, email chiffré)

### Pour la PRODUCTION (2 semaines)
➜ **Option 2 : Google OAuth**
- Configuration Google Cloud
- Liste des emails autorisés
- Logs d'accès
- Maximum de sécurité

### Si BUDGET disponible
➜ **Option 3 : GitHub privé + OAuth**
- Combinez dépôt privé et Google OAuth
- Sécurité maximale absolue

---

## 🔧 Implémenter chaque option

### OPTION 1 : Mot de passe simple (FAIT ✅)

**Étape 1 : Changer le mot de passe**

Éditez `index.html`, ligne ~270 :

```javascript
const CORRECT_PASSWORD = "VotreNouveauMotDePasse2025!";
```

**Étape 2 : Déployer**

Suivez le guide de déploiement normal.

**Étape 3 : Partager le mot de passe**

⚠️ **Ne l'envoyez JAMAIS par email non chiffré !**

Utilisez :
- Signal / WhatsApp
- Appel téléphonique
- Rencontre en personne
- Gestionnaire de mots de passe partagé (1Password, LastPass)

**Sécurité améliorée : Utiliser un hash**

Au lieu d'un mot de passe en clair, utilisez un hash SHA-256 :

1. Allez sur https://emn178.github.io/online-tools/sha256.html
2. Entrez votre mot de passe : `MonSuperMotDePasse2025!`
3. Copiez le hash : `e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855`
4. Dans le code :

```javascript
const CORRECT_PASSWORD_HASH = "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855";

function checkPassword() {
    const input = document.getElementById('passwordInput');
    const password = input.value;
    
    // Hasher le mot de passe saisi
    const hashedInput = sha256(password);
    
    if (hashedInput === CORRECT_PASSWORD_HASH) {
        // Authentification réussie
        ...
    }
}

// Fonction SHA-256 (ajouter cette bibliothèque)
async function sha256(message) {
    const msgBuffer = new TextEncoder().encode(message);
    const hashBuffer = await crypto.subtle.digest('SHA-256', msgBuffer);
    const hashArray = Array.from(new Uint8Array(hashBuffer));
    return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}
```

---

### OPTION 2 : Google OAuth

**Guide complet disponible :** `docs/AUTHENTIFICATION_GOOGLE.md`

**Résumé rapide :**

1. Créer projet Google Cloud
2. Activer Google Sign-In
3. Obtenir Client ID
4. Remplacer le code d'authentification
5. Configurer emails autorisés

**Temps : 15 minutes**

---

### OPTION 3 : Dépôt privé

**Étape 1 : Passer le dépôt en privé**

1. Allez sur votre dépôt GitHub
2. Settings → General
3. Scrollez en bas : "Danger Zone"
4. "Change repository visibility"
5. Sélectionnez "Private"
6. Confirmez

**Étape 2 : Activer GitHub Pages (nécessite Pro)**

1. Souscrivez à GitHub Pro : https://github.com/pricing
2. Settings → Pages
3. Activez Pages comme d'habitude

**Étape 3 : Gérer les accès**

1. Settings → Collaborators
2. Ajoutez les personnes autorisées
3. Choisissez leur niveau d'accès :
   - **Read** : Voir seulement
   - **Write** : Modifier
   - **Admin** : Tout gérer

---

## 🎨 Combinaisons possibles

### Combo 1 : Mot de passe + IP whitelisting

Restreindre l'accès à certaines IP (bureau ielo, VPN) :

```javascript
const AUTHORIZED_IPS = ['1.2.3.4', '5.6.7.8'];

async function checkIP() {
    const response = await fetch('https://api.ipify.org?format=json');
    const data = await response.json();
    return AUTHORIZED_IPS.includes(data.ip);
}
```

### Combo 2 : Google OAuth + Dépôt privé

Maximum de sécurité :
- Code source non visible (dépôt privé)
- Authentification forte (Google)
- Traçabilité complète (logs)

### Combo 3 : Mot de passe + Expiration

Le mot de passe expire après X jours :

```javascript
const PASSWORD_EXPIRY = 30; // jours
const PASSWORD_CREATION_DATE = '2025-01-03';

function isPasswordExpired() {
    const creationDate = new Date(PASSWORD_CREATION_DATE);
    const now = new Date();
    const daysDiff = (now - creationDate) / (1000 * 60 * 60 * 24);
    return daysDiff > PASSWORD_EXPIRY;
}
```

---

## 📊 Tableau comparatif détaillé

| Critère | Mot de passe | Google OAuth | GitHub Privé | Combo |
|---------|--------------|--------------|--------------|-------|
| Sécurité | ⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| Simplicité | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ |
| Coût | Gratuit | Gratuit | 4$/mois | 4$/mois |
| Temps config | 2 min | 15 min | 5 min | 20 min |
| Traçabilité | ❌ | ✅✅✅ | ✅ | ✅✅✅ |
| Maintenance | Faible | Aucune | Faible | Faible |
| Scalabilité | ⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ |

---

## 🛡️ Bonnes pratiques de sécurité

### Pour TOUS les modes

1. **HTTPS obligatoire** ✅ (GitHub Pages = HTTPS automatique)
2. **Pas de données sensibles dans le code** ✅
3. **Validation côté client ET serveur** (si backend)
4. **Chiffrement des exports** (optionnel)
5. **Logs d'accès** (recommandé)

### Spécifique mot de passe

1. ⚠️ Mot de passe fort (12+ caractères, majuscules, chiffres, symboles)
2. ⚠️ Changement régulier (tous les 3-6 mois)
3. ⚠️ Partage sécurisé (jamais par email)
4. ⚠️ Utiliser un hash (SHA-256)
5. ⚠️ Limiter les tentatives (anti-bruteforce)

### Spécifique Google OAuth

1. ✅ Restreindre aux emails @ielo.fr
2. ✅ Logger tous les accès
3. ✅ Révocation rapide si problème
4. ✅ Vérifier régulièrement les logs

---

## 🚨 Que faire en cas de problème

### Le mot de passe a fuité

1. **Immédiatement** : Changer le mot de passe dans le code
2. **Committer** et pousser sur GitHub
3. **Attendre 2 minutes** (redéploiement auto)
4. **Informer** tous les utilisateurs du nouveau mot de passe

### Un utilisateur OAuth n'est plus autorisé

1. Retirer son email de la liste `AUTHORIZED_EMAILS`
2. Committer et pousser
3. Attendre le redéploiement
4. Sa session actuelle expire à la fermeture du navigateur

### Accès suspects détectés

1. Vérifier les logs (console, Analytics)
2. Changer immédiatement les identifiants
3. Enquêter sur la source
4. Renforcer la sécurité

---

## ✅ Checklist de sécurité

Avant de déployer en production :

- [ ] J'ai changé le mot de passe par défaut
- [ ] Le mot de passe est fort (12+ caractères)
- [ ] J'ai décidé quelle option utiliser long terme
- [ ] J'ai documenté qui a accès
- [ ] J'ai un plan pour partager les identifiants
- [ ] J'ai un plan pour changer le mot de passe
- [ ] J'ai testé l'authentification
- [ ] Les utilisateurs savent comment se connecter
- [ ] J'ai un plan B si problème d'accès

---

## 🎓 Pour aller plus loin

### Amélioration future : Backend sécurisé

Pour une sécurité maximale, créez un backend qui :
- Gère l'authentification
- Stocke les données dans une base sécurisée
- Fournit une API REST
- Logs centralisés

**Technologies possibles :**
- Firebase (Google)
- Supabase (PostgreSQL)
- AWS Amplify
- Custom Node.js + Express

### Audit de sécurité

Pour une application critique :
- Faire un audit de sécurité professionnel
- Tests de pénétration
- Vérification RGPD
- Conformité ISO 27001

---

## 📞 Aide et support

**Vous voulez :**
- ✅ Garder le mot de passe simple → C'est fait !
- ✅ Implémenter Google OAuth → Suivez `AUTHENTIFICATION_GOOGLE.md`
- ✅ Combiner plusieurs méthodes → Je peux vous aider
- ✅ Autre solution sur mesure → Contactez-moi

**Recommandation personnelle :**

**Phase 1 (maintenant)** : Mot de passe simple
**Phase 2 (dans 1 mois)** : Google OAuth
**Phase 3 (dans 3 mois)** : Backend + API si besoin

---

**Mot de passe actuel : `ielo2025`**
**⚠️ CHANGEZ-LE AVANT DE DÉPLOYER !**
