# 🌀 Janus Conversationnel — IA Bimétrique

Un site web conversationnel unique qui transforme vos questions en un voyage intellectuel à travers 4 étapes : réponse standard, encodage scientifique, transposition Janus et surprise poétique.

## 📖 Table des matières

- [Le but du site web](#le-but-du-site-web)
- [Comment obtenir l'API Mistral Free Tiers gratuitement](#comment-obtenir-lapi-mistral-free-tiers-gratuitement)
- [Comment marche le site](#comment-marche-le-site)
- [Comment changer les prompts dans le code source](#comment-changer-les-prompts-dans-le-code-source)
- [Idées pour modifier les prompts afin d'être beaucoup plus scientifique](#idées-pour-modifier-les-prompts-afin-dêtre-beaucoup-plus-scientifique)

---

## 🎯 Le but du site web

Ce projet a pour objectif de créer une expérience conversationnelle innovante qui combine :

1. **Pédagogie** : Une réponse simple et accessible à toute question
2. **Créativité scientifique** : Un encodage de la réponse sous forme de pseudo-formule scientifique élégante
3. **Théorie Janus** : Une transposition dans le formalisme bimétrique du physicien Jean-Pierre Petit
4. **Poésie cosmique** : Une sortie artistique et surréaliste inspirée des équations

Le site explore la dualité entre rigueur scientifique et expression poétique, en s'appuyant sur la théorie Janus qui postule l'existence de deux secteurs couplés de l'univers (masses positives et négatives).

---

## 🔑 Comment obtenir l'API Mistral Free Tiers gratuitement

Mistral AI offre un **tier gratuit** généreux pour tester leurs modèles. Voici comment procéder :

### Étape 1 : Créer un compte Mistral AI

1. Rendez-vous sur **[La Plateforme Mistral AI](https://console.mistral.ai/)**
2. Cliquez sur **"Sign Up"** ou **"Get Started"**
3. Inscrivez-vous avec votre email ou via GitHub/Google

### Étape 2 : Accéder à votre clé API

1. Une fois connecté, allez dans **"API Keys"** dans le menu latéral
2. Cliquez sur **"Create new key"**
3. Donnez un nom à votre clé (ex: `janus-project`)
4. **Copiez immédiatement** la clé générée (elle ne sera affichée qu'une seule fois !)

### Étape 3 : Comprendre le Free Tier

Le plan gratuit inclut :
- **Limites mensuelles** : Un certain nombre de tokens gratuits par mois
- **Modèles disponibles** : Accès aux modèles comme `mistral-small`, `mistral-medium`, et parfois `mistral-large`
- **Pas de carte bancaire requise** pour commencer

> ⚠️ **Important** : Le modèle utilisé dans ce projet est `mistral-large-2512`. Vérifiez qu'il est inclus dans le free tier. Sinon, modifiez la constante `MODEL` dans le code pour utiliser `mistral-small` ou `mistral-medium`.

### Étape 4 : Configurer la clé dans le projet

Dans le fichier `index.html`, ligne 238, remplacez :

```javascript
const API_KEY = " mettre ici clee api mistral ";
```

Par votre clé réelle :

```javascript
const API_KEY = "votre_clé_api_mistral_ici";
```

---

## ⚙️ Comment marche le site

### Architecture générale

Le site est une **Single Page Application (SPA)** contenue dans un seul fichier HTML. Il utilise :
- **HTML/CSS** pour l'interface utilisateur
- **JavaScript vanilla** pour la logique
- **L'API Mistral** pour générer les réponses

### Le Pipeline en 4 étapes

```
❓ Question → 📚 Standard → 🔬 Formule → 🌀 Janus
```

#### Étape 1 : ❓ Question
L'utilisateur saisit une question dans le champ de texte (ex: *"Pourquoi le ciel est bleu ?"*)

#### Étape 2 : 📚 Réponse Standard
- **Prompt** : `buildStandardPrompt()`
- **Objectif** : Générer une réponse concise, pédagogique et accessible
- **Style** : Langage simple, imagé, niveau collégien

#### Étape 3 : 🔬 Encodage Scientifique
- **Prompt** : `buildFormulaPrompt()`
- **Objectif** : Transformer la réponse en pseudo-formule mathématique
- **Format** : Symboles définis, opérateurs simples (+, −, ∂, ∫, ⊕)

#### Étape 4 : 🌀 Transposition Janus
- **Prompt** : `buildJanusPrompt()`
- **Objectif** : Appliquer le formalisme bimétrique de Jean-Pierre Petit
- **Sortie** : Deux parties
  - `[POETIC]` : Texte poétique et surréaliste
  - `[VULGARIZED]` : Explication simple en langage humain

### Gestion de la conversation

Le site maintient un **historique de conversation** (`conversationHistory`) limité aux 6 derniers échanges pour donner du contexte aux réponses suivantes.

---

## ✏️ Comment changer les prompts dans le code source

Les prompts sont définis dans trois fonctions JavaScript à partir de la **ligne 347** du fichier `index.html`.

### 1. Modifier le prompt Standard (ligne 347-356)

```javascript
function buildStandardPrompt(question) {
  return `Tu es un assistant pédagogique bienveillant. 
Règles :
- Réponds à la question de façon concise (max 3 phrases)
- Utilise un langage simple, imagé, accessible à un collégien
- Évite le jargon technique ou explique-le immédiatement
- Sois chaleureux et engageant

Question : "${question}"`;
}
```

**Pour modifier** : Changez les règles, le ton, ou la longueur maximale.

### 2. Modifier le prompt Formule (ligne 358-370)

```javascript
function buildFormulaPrompt(question, standardAnswer) {
  return `Tu es un "encodeur scientifique créatif". 
Ta mission : transformer la réponse suivante en une pseudo-formule scientifique élégante mais compréhensible.

Règles :
- Crée 3-5 symboles avec définitions ultra-courtes (ex: L^μ = vecteur amour)
- Utilise des opérateurs simples (+, −, ∂, ∫, ⊕)
- Garde un lien logique avec la réponse originale
- Format : bloc de code avec commentaires courts

Réponse à encoder : "${standardAnswer}"
Question d'origine : "${question}"`;
}
```

**Pour modifier** : Ajoutez des contraintes sur les symboles, changez les opérateurs autorisés, etc.

### 3. Modifier le prompt Janus (ligne 372-407)

```javascript
function buildJanusPrompt(question, standardAnswer, formula) {
  return `Tu es l'IA Janus, basée sur la théorie bimétrique de Jean-Pierre Petit.
...
[CONTENU COMPLET DU PROMPT]
...
⚠️ IMPORTANT : Termine toujours par la section [VULGARIZED]. Ne mets pas de formules dans cette partie.`;
}
```

**Pour modifier** : 
- Ajoutez/supprimez des éléments du contexte Janus
- Changez le format de sortie `[POETIC]` / `[VULGARIZED]`
- Ajustez le ton (plus mystérieux, plus technique, etc.)

### 💡 Conseil de modification

Après chaque modification :
1. **Sauvegardez** le fichier `index.html`
2. **Rafraîchissez** la page dans votre navigateur
3. **Testez** avec une nouvelle question pour voir l'impact

---

## 🧪 Idées pour modifier les prompts afin d'être beaucoup plus scientifique

Voici des suggestions concrètes pour renforcer la dimension scientifique des prompts :

### 1. Pour le prompt Standard

**Ajouter des références scientifiques :**
```javascript
- Cite une loi physique, un principe ou un théorème pertinent si applicable
- Mentionne les unités de mesure appropriées (mètres, secondes, joules, etc.)
- Utilise la méthode scientifique : observation → hypothèse → conclusion
```

**Exemple de modification :**
```javascript
function buildStandardPrompt(question) {
  return `Tu es un assistant scientifique pédagogique. 
Règles :
- Réponds avec rigueur tout en restant accessible (niveau lycée scientifique)
- Structure ta réponse : Phénomène observé → Explication physique → Conclusion
- Cite les lois/principes pertinents (Newton, Maxwell, thermodynamique, etc.)
- Inclus les ordres de grandeur quand c'est pertinent
- Utilise le vocabulaire scientifique correct mais définis les termes techniques

Question : "${question}"`;
}
```

### 2. Pour le prompt Formule

**Rendre les formules plus authentiques :**
```javascript
- Utilise la notation tensorielle (indices grecs : μ, ν, α, β)
- Intègre des équations différentielles partielles
- Ajoute des constantes fondamentales (c, ℏ, G, k_B, ε₀)
- Utilise des opérateurs avancés (∇, Δ, □, ⊗, ∧)
- Inclure des transformations (Fourier, Laplace, Lorentz)
```

**Exemple de modification :**
```javascript
function buildFormulaPrompt(question, standardAnswer) {
  return `Tu es un physicien théorique spécialisé en formalisme mathématique.
Ta mission : encoder la réponse en équations physiques crédibles.

Règles avancées :
- Utilise la notation d'Einstein (somme sur indices répétés)
- Intègre au moins une équation différentielle ou intégrale
- Définis un lagrangien ℒ ou un hamiltonien ℋ si pertinent
- Utilise des tenseurs (g_μν, T^μν, F^μν)
- Inclure des constantes : c (vitesse lumière), ℏ (Planck), G (gravitation)
- Notation bra-ket ⟨ψ|φ⟩ pour les états quantiques si applicable

Format attendu :
```math
ℒ = ... 
∂_μ T^μν = 0
⟨out|S|in⟩ = ...
```

Réponse à encoder : "${standardAnswer}"
Question : "${question}"`;
}
```

### 3. Pour le prompt Janus

**Approfondir le formalisme bimétrique :**
```javascript
- Détailler les métriques g^(+) et g^(-) avec leurs signatures
- Expliciter le couplage via les termes sources croisés
- Utiliser la relativité générale (tenseur d'Einstein G_μν)
- Introduire des concepts de matière exotique (énergie négative)
- Parler des géodésiques et de leur divergence entre secteurs
- Mentionner les implications cosmologiques (expansion, trous noirs)
```

**Exemple de modification :**
```javascript
function buildJanusPrompt(question, standardAnswer, formula) {
  return `Tu es une IA spécialisée en cosmologie bimétrique Janus.

📋 FORMALISME JANUS AVANCÉ :

Équations de champ couplées :
  G^(+)_{μν} + Λg^(+)_{μν} = 8πG (T^(+)_{μν} + φ T^(-)_{μν})
  G^(-)_{μν} + Λg^(-)_{μν} = -8πG (T^(-)_{μν} + φ T^(+)_{μν})

où :
  • g^(±)_{μν} : métriques des secteurs (+) et (-)
  • T^(±)_{μν} : tenseurs énergie-impulsion
  • φ : facteur de couplage inter-sectoriel
  • Signature : (−,+,+,+) pour les deux métriques

Concepts clés :
  • Masse négative ⇒ répulsion gravitationnelle
  • Géodésiques divergentes entre secteurs
  • Conservation : ∇^(+)μ T^(+)μν = −∇^(-)μ T^(-)μν
  • Effets de lentille gravitationnelle inversée
  • Solutions de type "trou noir Janus"

🔁 PROTOCOLE DE TRANSPOSITION :

1. Décomposer chaque entité X → X^(+) ⊗ X^(-)
2. Appliquer le couplage non-linéaire avec inversion de signe
3. Résoudre symboliquement les équations de géodésiques
4. Interpréter physiquement dans les deux secteurs
5. Projeter sur des observables macroscopiques

📤 FORMAT DE SORTIE OBLIGATOIRE :

[POETIC]
→ Narrative cosmique en 8-12 phrases
→ Intégrer les équations comme métaphores opérationnelles
→ Ton : contemplation scientifique sublimée
→ Références implicites à la dualité, symétrie, brisure

[VULGARIZED]
→ Traduction conceptuelle en 3-4 phrases
→ Commencer par : "Physiquement, cela suggère que..."
→ Relier à des phénomènes observables ou testables

📥 DONNÉES :
Question : "${question}"
Réponse standard : "${standardAnswer}"
Formule encodée : 
${formula}

⚠️ CONTRAINTES :
- Aucune équation dans [VULGARIZED]
- Cohérence mathématique dans les métaphores
- Respecter la signature des métriques`;
}
```

### 4. Idées supplémentaires

#### Ajouter un mode "Expert"
Créer une variable `SCIENTIFIC_MODE = true` qui active des prompts encore plus techniques avec :
- Notation de Penrose (diagrammes)
- Groupes de Lie et algèbres
- Théorie des cordes/M-théorie
- Mécanique quantique relativiste

#### Intégrer des références bibliographiques
Demander à l'IA de citer :
- Les articles de Jean-Pierre Petit sur Janus
- Les travaux sur la matière noire/énergie sombre
- La littérature sur les métriques multiples

#### Ajouter des visualisations
Proposer des représentations graphiques :
- Diagrammes d'espace-temps
- Cônes de lumière dans les deux secteurs
- Potentiels effectifs

---

## 🚀 Démarrage rapide

1. **Obtenez votre clé API Mistral** (voir section ci-dessus)
2. **Ouvrez `index.html`** dans un éditeur de texte
3. **Collez votre clé** ligne 238
4. **Ouvrez `index.html`** dans votre navigateur
5. **Posez une question** et observez la magie !

---

## 📚 Ressources

- [Théorie Janus — Jean-Pierre Petit](https://fr.wikipedia.org/wiki/Jean-Pierre_Petit)
- [Mistral AI Platform](https://console.mistral.ai/)
- [Documentation API Mistral](https://docs.mistral.ai/)

---

## ⚠️ Avertissements

- **Sécurité** : Ne commitez jamais votre clé API sur un dépôt public
- **Usage local** : Ce projet est conçu pour un usage personnel en local
- **Coûts** : Surveillez votre consommation de tokens même en free tier

---

Développé avec 🌀 pour explorer les frontières entre science et poésie.
