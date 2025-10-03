# Guide de contribution

Merci de votre intérêt pour contribuer au Formulaire d'Intervention Chantier ielo ! 🌾

## 🐛 Signaler un bug

Si vous trouvez un bug :

1. Vérifiez qu'il n'a pas déjà été signalé dans les [Issues](https://github.com/NRielo/Formulaire_intervention_chantier/issues)
2. Créez une nouvelle Issue avec le tag `bug`
3. Incluez :
   - Description claire du problème
   - Étapes pour reproduire
   - Comportement attendu vs comportement observé
   - Navigateur et appareil utilisés
   - Captures d'écran si possible

**Template de bug :**
```markdown
**Description du bug**
[Description claire et concise]

**Reproduire le bug**
1. Allez sur '...'
2. Cliquez sur '...'
3. Observez l'erreur

**Comportement attendu**
[Ce qui devrait se passer]

**Environnement**
- Navigateur : [ex: Chrome 120]
- Appareil : [ex: iPhone 12, Android Galaxy S21, Windows PC]
- URL : [ex: https://nrielo.github.io/...]

**Captures d'écran**
[Si applicable]
```

## 💡 Proposer une amélioration

Pour proposer une nouvelle fonctionnalité :

1. Créez une Issue avec le tag `enhancement`
2. Décrivez clairement :
   - Le problème que ça résout
   - La solution proposée
   - Les alternatives considérées
   - L'impact sur les utilisateurs existants

## 🔧 Contribuer au code

### Prérequis

- Connaissances en HTML5, CSS3, JavaScript
- Git installé sur votre machine
- Un éditeur de code (VS Code recommandé)

### Processus

1. **Fork** le dépôt
2. **Clone** votre fork :
   ```bash
   git clone https://github.com/VOTRE_USERNAME/Formulaire_intervention_chantier.git
   cd Formulaire_intervention_chantier
   ```

3. **Créez une branche** pour votre fonctionnalité :
   ```bash
   git checkout -b feature/ma-nouvelle-fonctionnalite
   ```

4. **Développez** votre fonctionnalité :
   - Testez localement avec un serveur (ex: `python -m http.server 8000`)
   - Vérifiez sur mobile et desktop
   - Testez sur différents navigateurs

5. **Committez** vos changements :
   ```bash
   git add .
   git commit -m "feat: ajout de ma nouvelle fonctionnalité"
   ```

6. **Poussez** vers votre fork :
   ```bash
   git push origin feature/ma-nouvelle-fonctionnalite
   ```

7. **Créez une Pull Request** sur le dépôt principal

### Convention de commits

Utilisez le format suivant :

- `feat:` Nouvelle fonctionnalité
- `fix:` Correction de bug
- `docs:` Documentation seulement
- `style:` Changements de formatage
- `refactor:` Refactoring du code
- `test:` Ajout de tests
- `chore:` Maintenance

**Exemples :**
```
feat: ajout export PDF
fix: correction calcul masse volumique
docs: mise à jour README
style: amélioration responsive mobile
```

## 📝 Améliorer la documentation

La documentation est tout aussi importante que le code !

- Corrigez les fautes d'orthographe
- Clarifiez les instructions
- Ajoutez des exemples
- Traduisez en d'autres langues

## 🧪 Tests

Avant de soumettre une Pull Request :

- [ ] Testez sur Chrome, Firefox, Safari
- [ ] Testez sur mobile (iOS et Android)
- [ ] Testez toutes les fonctionnalités :
  - [ ] Formulaire de base
  - [ ] Géolocalisation
  - [ ] Photos
  - [ ] Dictée vocale
  - [ ] Calculs automatiques
  - [ ] Export JSON
- [ ] Vérifiez qu'il n'y a pas d'erreurs dans la console
- [ ] Vérifiez la compatibilité mobile

## ✅ Checklist Pull Request

Avant de soumettre, assurez-vous que :

- [ ] Le code suit les conventions du projet
- [ ] La documentation est à jour
- [ ] Les tests passent
- [ ] Le CHANGELOG est mis à jour
- [ ] Pas de conflits avec la branche main
- [ ] La Pull Request a une description claire

## 🎨 Style de code

### HTML
- Indentation : 4 espaces
- Noms de classes en kebab-case
- Attributs dans l'ordre : id, class, autres

### CSS
- Indentation : 4 espaces
- Ordre des propriétés : positionnement, box model, typographie, visuel
- Mobile-first (media queries après le code de base)

### JavaScript
- Indentation : 4 espaces
- camelCase pour les variables et fonctions
- PascalCase pour les classes
- Commentaires clairs pour la logique complexe

## 📞 Questions ?

Si vous avez des questions, n'hésitez pas à :
- Ouvrir une Issue avec le tag `question`
- Contacter l'équipe ielo

## 🙏 Merci !

Chaque contribution, petite ou grande, est appréciée. Merci de nous aider à améliorer cet outil ! 🌾
