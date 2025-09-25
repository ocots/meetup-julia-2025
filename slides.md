---
marp: true
theme: default
paginate: true
size: 16:9
math: mathjax
header: "<div class='qr-code'></div>"
style: |
    @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&display=swap');
    @import url('https://cdn.jsdelivr.net/npm/hack-font@3.3.0/build/web/hack.css');
    
    :root {
        --font-family: 'Roboto', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
        --code-font: 'Hack', 'Fira Code', 'Consolas', monospace;
        --base-font-size: 24px;
        --heading-scale: 1.25;
    }
    
    @page {
        size: 1210px 681px;
        margin: 0;
    }
    
    /* Styles de base */
    section {
        font-family: var(--font-family);
        font-size: var(--base-font-size);
        line-height: 1.5;
        padding: 1.25em 2.5em;
        background-color: white;
        color: #222;
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        min-height: 100%;
        letter-spacing: 0.01em;
    }
    
    /* Affichage du QR code avec une div personnalisée */
    .qr-code {
        position: fixed;
        top: 10px;
        right: 10px;
        width: 100px;
        height: 100px;
        background-image: url('figs/ct-qr-code.svg');
        background-size: contain;
        background-repeat: no-repeat;
        z-index: 1000;
    }

    /* Titres */
    h1 { font-size: calc(var(--base-font-size) * 2.2); margin: 0 0 0.8em 0; }
    h2 { font-size: calc(var(--base-font-size) * 1.8); margin: 0.8em 0 0.6em 0; }
    h3 { font-size: calc(var(--base-font-size) * 1.4); margin: 0.6em 0 0.4em 0; }
    p, li { margin: 0.5em 0; }
    
    /* Styles pour le code */
    code {
        font-family: var(--code-font);
        font-size: 0.85em;
        background: #f5f5f5;
        padding: 0.1em 0.3em;
        border-radius: 3px;
    }
    
    pre {
        font-family: var(--code-font);
        font-size: 0.8em;
        line-height: 1.4;
        background: #f8f8f8;
        border: 1px solid #e1e4e8;
        border-radius: 6px;
        padding: 1em;
        overflow: auto;
        margin: 0.8em 0;
    }
    
    /* Colonnes */
    .custom-columns {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
        gap: 1.5em;
        width: 100%;
        margin: 1em 0;
    }
    
    .column {
        min-width: 0;
        display: flex;
        flex-direction: column;
    }
    
    /* Images */
    .centered-image {
        display: block;
        max-width: 100%;
        height: auto;
        margin: 1em auto;
        border-radius: 4px;
    }
    
    /* Première page */
    section.title {
        justify-content: center;
        text-align: center;
        padding-top: 15%;
    }
    
    section.title h1 {
        font-size: calc(var(--base-font-size) * 2.5);
        margin-bottom: 0.5em;
    }
    
    /* Liste à puces */
    ul, ol {
        margin: 0.5em 0;
        padding-left: 1.5em;
    }
    
    li {
        margin: 0.3em 0;
        padding-left: 0.3em;
    }
    
    /* Liens */
    a {
        color: #0366d6;
        text-decoration: none;
    }
    
    a:hover {
        text-decoration: underline;
    }
    
    /* Citations */
    blockquote {
        border-left: 4px solid #dfe2e5;
        color: #6a737d;
        padding: 0 1em;
        margin: 1em 0;
        font-style: italic;
    }
    
    /* Tableaux */
    table {
        border-collapse: collapse;
        width: 100%;
        margin: 1em 0;
        font-size: 0.9em;
    }
    
    th, td {
        border: 1px solid #dfe2e5;
        padding: 0.5em 1em;
        text-align: left;
    }
    
    th {
        background-color: #f6f8fa;
        font-weight: 600;
    }
    
    /* Légendes */
    .caption {
        font-size: 0.8em;
        color: #6a737d;
        text-align: center;
        margin-top: -0.5em;
        margin-bottom: 1em;
    }
    .custom-columns {
        display: grid;
        grid-template-columns: 1fr 2fr;
        gap: 20px;
        width: 100%;
    }
    .custom-columns .column {
        min-width: 0; /* Pour éviter les problèmes de débordement */
    }
    
    .custom-columns.community {
        display: grid;
        grid-template-columns: 1.5fr 1fr;
        gap: 20px;
        width: 100%;
    }
    
    /* Style pour centrer les images */
    /* Style pour les images centrées avec conteneur */
    div > .centered-image {
        display: block;
        margin: 0 auto 15px auto;  /* 15px de marge en bas */
        max-width: 100%;
        height: auto;
    }
    
    /* Style spécifique pour la première page de titre */
    section.title {
        justify-content: center;
        text-align: center;
    }
    
    /* Style pour le contenu de la première page */
    section.title {
        justify-content: flex-start;
        padding-top: 12%; /* Ajustez cette valeur pour déplacer tout le bloc vers le bas */
    }
    
    section.title > h1 {
        margin: 0 0 1em 0;
        padding: 0;
        text-align: center;
    }
    
    /* Positionnement des titres et contenu */
    section > * {
        flex: 0 0 auto;
        width: 100%;
    }
    
    section > h1 {
        margin: 0.2em 0 0.5em 0;
    }
    
    section > h2 {
        margin: 0.2em 0 0.5em 0;
        flex: 0 0 auto;
        font-size: 1.5em;
        border-bottom: 2px solid #4d64ae;
        padding-bottom: 0.2em;
    }
    
    /* La pagination est gérée par Marp */

    section > h3 {
        margin: 0.2em 0 0.5em 0;
        flex: 0 0 auto;
        font-size: 1.2em;
        color: #399746;
    }
    
    /* Contenu principal - enlève le flex: 1 qui causait le centrage vertical */
    section > *:not(h1):not(h2):not(h3) {
        margin-top: 0.5em;
    }
    .columns {
        display: flex;
        width: 100%;
        gap: 1.5rem;
        align-items: flex-start;
    }
    .column {
        padding: 0;
        min-width: 0; /* Pour éviter les problèmes de débordement */
    }
    /* Colonne par défaut (50/50) */
    .column:not([style*="flex:"]) {
        flex: 1 1 0;
    }
    /* Colonnes avec largeur personnalisée */
    .column[style*="flex:"] {
        flex: 0 0 auto;
    }
    h1 { color: #4d64ae; }      /* bleu */
    h2 { color: #ca3c32; }      /* rouge */
    h3 { color: #399746; }      /* vert */
    p, li { color: #1a1a1a; }   /* texte noir/gris foncé */
    code { background-color: #F4F4F4; padding: 2px 4px; border-radius: 4px; }
    img[alt~="center"] { display: block; margin: 0 auto; }
    .caption { text-align: center; font-style: italic; font-size: 0.8em; }
---
<!-- _class: title -->

# L’écosystème Julia *control-toolbox* pour le contrôle optimal

*Olivier Cots – CNRS, Toulouse INP, IRIT*

*Jean-Baptiste Caillau • Joseph Gergaud • Pierre Martinon • Sophia Sed*

Institute for Celestial Mechanics and Computation of Ephemerides, 25 septembre 2025

---

## Contexte

Le projet **control-toolbox** rassemble plusieurs packages Julia pour modéliser et résoudre des problèmes de contrôle optimal.  

- Package central : **OptimalControl.jl**  
- Architecture modulaire et performante  
- Calcul **CPU et GPU**  
- Connexion fluide entre :  
  - formulation mathématique,  
  - simulation,  
  - optimisation avancée

---

## 1. Introduction

- **Contrôle optimal** = trajectoire optimale d’un système dynamique contrôlé sous contraintes  
- Domaine : math appliquées, optimisation, simulation numérique  
- Applications : robotique, aéronautique, finance, énergie  

<div>
<img src="figs/spatial.png" class="centered-image" alt="" width="540px">
<p class="caption">Transfert Terre–Lune – Mission Apollo XI</p>
</div>

---

## 2. Pourquoi Julia ?

Julia est un langage de haut niveau, rapide et dynamique, idéal pour le calcul scientifique et le contrôle optimal.

- **Performances** : compilation JIT et fonctions stables en type → code machine optimisé  
- **Syntaxe expressive** : proche des notations mathématiques, support Unicode  

<div class="custom-columns">
<div class="column">

```julia
julia> f(x₁, x₂) = x₁^2 + 3x₂^2

julia> ∇f(x₁, x₂) = [
  2x₁, 
  6x₂
]

julia> ∇f(1.0, 2.0)
2-element Vector{Float64}:
  2.0
 12.0
```

</div>
<div class="column ecosystem">

### 🌐 Écosystème riche et spécialisé

<style>
.column h3:first-child {
    margin-top: -0.5em;
}
.column.ecosystem {
    margin-left: 1.5em;
}
</style>

- **AD & EDO** : ForwardDiff.jl, Zygote.jl, DifferentialEquations.jl  
- **Optimisation** : JuMP.jl, JuliaSmoothOptimizers, MadNLP.jl, ExaModels.jl, ADNLPModels.jl  
- **GPU** : CUDA.jl, KernelAbstractions.jl, CUDSS.jl  
- **DSL** : MLStyle.jl, Moshi.jl pour le pattern matching

**Avantages clés** : modélisation intuitive, parallélisme SIMD/GPU, extensibilité, différentiation automatique...

</div>
</div>

---

## 3. Panorama de *control-toolbox*

### Packages principaux

- **OptimalControl.jl** : DSL pour modéliser et résoudre des OCPs (directes/indirectes, CPU/GPU)  
- **OptimalControlProblems.jl** : bibliothèque de problèmes de référence, prête pour benchmarking et comparaisons  

<div class="columns">
<div class="column">

### Briques internes clés et architecture

- **CTBase.jl** : exceptions, fonctions utilitaires
- **CTModels.jl** : types des modèles, solutions, setters, getters et visualisation  
- **CTDirect.jl** : discrétisation et résolution  
- **CTFlows.jl** : systèmes hamiltoniens et flots
- **CTParser.jl** : définition abstraite et parser

</div>

<style>
.column .diagramme {
    margin-top: -1.5em;
}
</style>
<div class="column">
<img src="figs/diagramme.png" class="centered-image diagramme" alt="Architecture modulaire et cohérente" width="450px">
<p class="caption">💡 Architecture modulaire</p>
</div>
</div>

---

## 4. Exemple minimaliste : double intégrateur

**Problème** : Trouver le contrôle optimal pour amener un système de la position $(-1, 0)$ à $(0, 0)$ en minimisant l'énergie du contrôle.

<div class="columns">
<div class="column">

**Formulation mathématique**

$$
\begin{aligned}
\min_{x(\cdot),\, u(\cdot)} \quad & \frac{1}{2} \int_0^1 u^2(t)\,\mathrm{d}t \\[1em]
\text{s.c. :} \quad &
\dot{x}(t) = \begin{bmatrix} x_2(t) \\ u(t) \end{bmatrix}, \\[1em]
& x(0) = \begin{bmatrix} -1 \\ 0 \end{bmatrix}, \quad
x(1) = \begin{bmatrix} 0 \\ 0 \end{bmatrix}.
\end{aligned}
$$

</div>
<div class="column">

**Avec OptimalControl.jl**

```julia
using OptimalControl

ocp = @def begin
    t ∈ [0, 1], time
    x ∈ R², state
    u ∈ R, control

    x(0) == [-1, 0]
    x(1) == [0, 0]

    ẋ(t) == [x₂(t), u(t)]

    0.5∫(u(t)^2) → min
end
```

</div>
</div>

---

### Résolution et visualisation

<div class="columns">
<div class="column">

**Résolution**

```julia
using NLPModelsIpopt
sol = solve(ocp)
```

![w:520px](figs/solve.png)

</div>

<div class="column">

**Visualisation**

```julia
using Plots
plot(sol)
```

![w:550px](figs/plot.png)

</div>
</div>

---

<br>
<br>
<br>
<br>

### Architecture SIMD

[Discrétisation du problème de contrôle optimal](https://control-toolbox.org/OptimalControlProblems.jl/stable/problems-introduction.html)

<br>
<br>

### Autre exemple

[Minimum time orbit transfer](https://control-toolbox.org/Kepler.jl/stable/#orbit)

---

## 5. Architecture logicielle et bonnes pratiques

<br>

### 🏗️ Séparation des responsabilités

- **Modèles** : définition, manipulation et visualisation  
- **Algorithmes** : méthodes de transcription, intégrateurs  
- **Interfaces** : DSL proche des mathématiques  

### ⚡ Performance

- **Différentiation automatique** et compilation Julia  
- **Structure creuse** des problèmes discrétisés  
- Support natif **CPU et GPU** pour le calcul haute performance  

---

### 🔄 Qualité logicielle

- **Intégration continue** : tests, couverture, documentation  
- **Tests unitaires** : modèles, solveurs, API  
- **Benchmarks** : suivi des performances  
- **Détection d'incompatibilités** avec les dépendances  

<div class="columns">
<div class="column">

**Actions CI/CD**

<img src="figs/actions.png" alt="Actions CI/CD" style="max-width: 100%;"/>

</div>
<div class="column">

**Détection d'incompatibilités**

<img src="figs/breakages.png" alt="Détection d'incompatibilités" style="max-width: 100%;"/>

</div>
</div>

<p class="caption">💡 Automatisation et surveillance de la qualité</p>

---

### 📖 Ouverture et communauté

- Documentation complète sur [control-toolbox.org](https://control-toolbox.org) : Manuels pour [OptimalControl.jl](https://control-toolbox.org/OptimalControl.jl/stable), [Tutoriels](https://control-toolbox.org/Tutorials.jl/stable) avancés, Catalogue de [problèmes modélisés](https://control-toolbox.org/OptimalControlProblems.jl/previews/PR139).

- Applications phares de la communauté ([template](https://github.com/control-toolbox/CTAppTemplate.jl)) :
  - [PWL models of gene regulatory networks](https://agustinyabo.github.io/PWLdynamics.jl/stable) (+ [Binder](https://mybinder.org/v2/gh/agustinyabo/PWLdynamics.jl/main))
  - [Loss control regions in optimal control problems](https://control-toolbox.org/LossControl.jl/stable)
  - [Optimal control in Medical Resonance Imaging](https://control-toolbox.org/MedicalResonanceImaging.jl/stable)
  - [Minimum time orbit transfer](https://control-toolbox.org/Kepler.jl/stable)

<div class="custom-columns community">
<div class="column">

**Reproductibilité**

<img src="figs/reproduce_.png" alt="Reproductibilité" style="max-width: 100%;"/>

</div>
<div class="column">

**Communauté active**

- Issues et discussions GitHub
- Contributions bienvenues
- Environnements reproductibles

</div>
</div>

---

## Conclusion & Perspectives

### Principaux atouts

- **Unifié** : Approche unifiée pour les méthodes directes et indirectes  
- **Modulaire** : Architecture flexible et extensible  
- **Performant** : Exploitation des capacités de Julia  
- **Communautaire** : Documentation complète et écosystème en croissance  

### Prochaines étapes

- Extension de l'écosystème : Méthodes indirectes, Méthodes homotopiques  
- Renforcement de la communauté : applications, tutoriels, algorithmes...

---

### Ressources

- 📚 Documentation : [control-toolbox.org](https://control-toolbox.org)  
- 💻 Code source : [github.com/control-toolbox](https://github.com/control-toolbox)  
- 📧 Contact : Olivier Cots, [olivier.cots@irit.fr](mailto:olivier.cots@irit.fr)

<div>
  <img src="figs/control-toolbox.png" alt="Control Toolbox" class="presentation-logo"/>
</div>

<style>
.presentation-logo {
    max-width: 85%;
    height: auto;
    margin: 10px auto;
    display: block;
}
</style>
 
