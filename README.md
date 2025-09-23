# L’écosystème Julia *control-toolbox* pour le contrôle optimal

*[Olivier Cots](https://github.com/ocots) – CNRS, Toulouse INP, IRIT*

En collaboration avec
[Jean-Baptiste Caillau](http://caillau.perso.math.cnrs.fr),
[Joseph Gergaud](https://github.com/joseph-gergaud),
[Pierre Martinon](https://github.com/PierreMartinon),
[Sophia Sed](https://sed-sam-blog.gitlabpages.inria.fr).

### Abstract

Le projet <a href="https://github.com/control-toolbox" style="display:inline-flex; align-items:center;">
  <img src="https://raw.githubusercontent.com/control-toolbox/control-toolbox.github.io/main/assets/img/ct-logo.svg" width="16em" style="margin-right:0.3em; margin-bottom:0.25em;">
  control-toolbox
</a> rassemble plusieurs packages <a href="https://julialang.org" style="display:inline-flex; align-items:center;">
  <img src="https://raw.githubusercontent.com/JuliaLang/julia-logo-graphics/master/images/julia.ico" width="16em" style="margin-right:0.3em; margin-bottom:0.25em;">
  Julia
</a> pour modéliser et résoudre des problèmes de contrôle optimal. Autour du package central **OptimalControl.jl**, il propose une architecture modulaire, performante et adaptée au calcul CPU et GPU, permettant de connecter formulation mathématique, simulation et optimisation avancée.  

## 1. Introduction

Le **contrôle optimal** consiste à déterminer la trajectoire optimale d’un système dynamique sous contraintes, en minimisant ou maximisant un critère donné. Il combine mathématiques appliquées, optimisation et simulation numérique, avec des applications dans la robotique, l’aéronautique, la finance et l’énergie.  

Ici, nous présentons un **écosystème Julia** capable de modéliser, résoudre et partager efficacement des problèmes de contrôle optimal, tirant parti de la vitesse, de la syntaxe expressive et du riche écosystème Julia.  

<figure style="text-align: center;">
  <img 
    src="spatial.png"
    alt="Transfert Terre-Lune Apollo XI"
    width="100%"
    style="margin-top:10px; margin-bottom:10px; max-width:500px"
    />
  <figcaption><em>Figure :</em> Transfert Terre–Lune de la mission <strong>Apollo XI</strong>.</figcaption>
</figure>

## 2. Pourquoi Julia ? 🚀

Julia est un langage de haut niveau, rapide et dynamique, conçu pour le calcul scientifique et les applications numériques, idéal pour le contrôle optimal.

### ⚡ Performances de haut niveau

Grâce à sa compilation Just-In-Time (JIT), Julia combine syntaxe expressive et vitesse exceptionnelle. Cependant, pour que le compilateur puisse générer un code machine optimisé, il est essentiel que les fonctions soient **stables en type**. Cela signifie que le type de sortie d'une fonction doit dépendre uniquement des types de ses entrées, et non de leurs valeurs.

### ✍️ Syntaxe intuitive et expressive

Sa syntaxe claire, proche de Python et des notations mathématiques classiques, facilite la modélisation et la résolution. Julia permet également d’utiliser des **caractères Unicode** pour nommer des variables et fonctions, ce qui rend le code très proche des notations mathématiques :

```julia
f(x₁, x₂) = x₁^2 + 3x₂^2      # fonction quadratique
∇f(x₁, x₂) = [2x₁, 6x₂]       # gradient : ∇f = [∂f/∂x₁, ∂f/∂x₂]
∇f(1.0, 2.0)                  # retourne [2.0, 12.0]
```

### 🌐 Écosystème riche et spécialisé

Julia dispose d’un écosystème complet pour l'optimisation, le calcul scientifique en général, et le contrôle optimal en particulier :

- **🧮 Différentiation automatique et équations différentielles** :  
  - [ForwardDiff.jl](https://juliadiff.org/ForwardDiff.jl/stable) et [Zygote.jl](https://fluxml.ai/Zygote.jl/stable) pour calculer gradients, Jacobiennes et Hessiennes.  
  - [DifferentialEquations.jl](https://docs.sciml.ai/DiffEqDocs/stable) pour résoudre des équations différentielles ordinaires.

- **📊 Optimisation – solveurs et modeleurs** :  
  - [JuMP.jl](https://jump.dev/JuMP.jl/stable) pour formuler des problèmes linéaires, non linéaires, en nombre entiers.  
  - [JuliaSmoothOptimizers](https://jso.dev) pour modéliser, résoudre et analyser des problèmes d’optimisation.  
  - [MadNLP.jl](https://madnlp.github.io/MadNLP.jl/stable), solveur intérieur-point entièrement en Julia, avec support GPU.  
  - [ExaModels.jl](https://exanauts.github.io/ExaModels.jl/stable) compile ces modèles en code SIMD-friendly pour GPU, incluant la différentiation automatique et l’évaluation vectorisée.  
  - [ADNLPModels.jl](https://jso.dev/ADNLPModels.jl/stable) : modélisation rapide de problèmes non linéaires en Julia, avec différentiation automatique et compatibilité [NLPModels.jl](https://jso.dev/NLPModels.jl/stable).  

- **🟩 Calculs sur GPU** : l’ensemble permet d’exploiter le parallélisme SIMD naturel des OCPs, du modèle jusqu’au solveur.  
  - [CUDA.jl](https://cuda.juliagpu.org/stable) pour programmer les GPU NVIDIA à différents niveaux d’abstraction.  
  - [KernelAbstractions.jl](https://juliagpu.github.io/KernelAbstractions.jl/stable) pour écrire des kernels portables multi-backend GPU.  
  - [CUDSS.jl](https://exanauts.github.io/CUDSS.jl/dev) pour résoudre efficacement des systèmes linéaires creux sur GPU.  

- **🖥️ Langage dédié** :  
  - [MLStyle.jl](https://thautwarm.github.io/MLStyle.jl/latest) et [Moshi.jl](https://rogerluo.dev/Moshi.jl) pour le pattern matching et la métaprogrammation, facilitant la construction de DSL personnalisés, pour une écriture des problèmes de contrôle optimal proche des mathématiques.

- **🏆 Avantages clés pour le contrôle optimal** :  
  - Modélisation intuitive avec DSL proches de la notation mathématique.  
  - Accélération GPU et parallélisme SIMD pour résoudre de très grands OCPs.  
  - Extensibilité et portabilité grâce à la métaprogrammation et aux abstractions haut-niveau.  
  - Intégration fluide avec la différentiation automatique et la gestion de la parcimonie.  

## 3. Panorama de *control-toolbox*

L’écosystème *control-toolbox* rassemble plusieurs packages Julia dédiés au contrôle mathématique et à ses applications.

Le package central, [**OptimalControl.jl**](https://github.com/control-toolbox/OptimalControl.jl), fournit un DSL pour modéliser et résoudre des problèmes de contrôle optimal définis par des équations différentielles ordinaires. Il prend en charge les méthodes directes et indirectes, et s’exécute aussi bien sur CPU que sur GPU.  

En complément, [**OptimalControlProblems.jl**](https://github.com/control-toolbox/OptimalControlProblems.jl) propose une collection de problèmes de contrôle optimal de référence, formulés en Julia. Chaque problème est disponible à la fois dans le DSL **OptimalControl** et dans **JuMP**, avec des versions discrétisées prêtes à être résolues avec le solveur de votre choix. Ce package est particulièrement utile pour le benchmarking et la comparaison de différentes stratégies de résolution.  

Les autres briques de l’écosystème sont plus internes, mais assurent une architecture modulaire, flexible et cohérente :  

- **[CTBase.jl](https://github.com/control-toolbox/CTBase.jl)** : regroupe les éléments fondamentaux les plus génériques de l’écosystème : exceptions, concept de description, et fonctions auxiliaires réutilisables.  
- **[CTModels.jl](https://github.com/control-toolbox/CTModels.jl)** : définit les types principaux pour les modèles de contrôle optimal (problèmes, solutions), ainsi que tous les outils pour les construire (`setter`, `builder`), les afficher (`print`, `plot`) et les interroger (`getter`).  
- **[CTDirect.jl](https://github.com/control-toolbox/CTDirect.jl)** : implémente la transcription directe des problèmes de contrôle optimal en problèmes de programmation non linéaire (NLP) et leur résolution.  
- **[CTFlows.jl](https://github.com/control-toolbox/CTFlows.jl)** : propose des intégrateurs pour les systèmes dynamiques, incluant des flots classiques, hamiltoniens, et issus de problèmes de contrôle optimal.  
- **[CTParser.jl](https://github.com/control-toolbox/CTParser.jl)** : fournit un parser pour définir un problème de contrôle optimal via une syntaxe abstraite, facilitant l’interfaçage avec d’autres outils.  

👉 L’ensemble de ces packages est disponible sur le dépôt [*control-toolbox*](https://github.com/orgs/control-toolbox/repositories?type=all). Le package principal est organisé ainsi :

<div align="center">

```mermaid
flowchart TD
B(<a href='https://control-toolbox.org/OptimalControl.jl/stable/dev-ctbase.html'>CTBase</a>)
M(<a href='https://control-toolbox.org/OptimalControl.jl/stable/dev-ctmodels.html'>CTModels</a>)
P(<a href='https://control-toolbox.org/OptimalControl.jl/stable/dev-ctparser.html'>CTParser</a>)
O(<a href='https://control-toolbox.org/OptimalControl.jl/stable/dev-optimalcontrol.html'>OptimalControl</a>)
D(<a href='https://control-toolbox.org/OptimalControl.jl/stable/dev-ctdirect.html'>CTDirect</a>)
F(<a href='https://control-toolbox.org/OptimalControl.jl/stable/dev-ctflows.html'>CTFlows</a>)
O --> D
O --> M
O --> F
O --> P
F --> M
O --> B
F --> B
D --> B
D --> M
P --> M
P --> B
M --> B
```

</div>

## 4. Exemple minimaliste

### Problème : double intégrateur

Considérons un système simple : un **double intégrateur** où l’accélération est contrôlée par une entrée scalaire $u(t)$.  
L’objectif est de **minimiser l’énergie du contrôle** pour amener le système d’une position initiale donnée à une position finale fixée.

<div style="display: flex; gap: 20px;">

<div style="flex: 1;">

**Formulation mathématique**

$$
\begin{aligned}
\min_{x(\cdot),\, u(\cdot)} \quad & \frac{1}{2} \int_0^1 u^2(t)\,\mathrm{d}t \\[1.2em]
\text{s.c. :} \quad &
\dot{x}(t) = \begin{bmatrix} x_2(t) \\ u(t) \end{bmatrix}, \\[1.2em]
& x(0) = \begin{bmatrix} -1 \\ 0 \end{bmatrix}, \quad
x(1) = \begin{bmatrix} 0 \\ 0 \end{bmatrix}.
\end{aligned}
$$

</div>

<div style="flex: 1;">

**Formulation avec OptimalControl.jl**

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

Une fois le problème défini, il peut être **résolu numériquement** et la trajectoire obtenue visualisée en quelques lignes de code :

<div style="display: flex; gap: 20px;">

<div style="flex: 1;">

```julia
using NLPModelsIpopt
sol = solve(ocp)
```

<img src="solve.png" alt="solve" width="100%" style="margin-top:10px; margin-bottom:10px;"/>

</div>

<div style="flex: 1;">

```julia
using Plots
plot(sol)
```

<img src="plot.png" alt="plot" width="100%" style="margin-top:10px; margin-bottom:10px;"/>

</div>
</div>

👉 Une démonstration complète, avec la résolution et les graphiques détaillés, est disponible dans la documentation : [Double intégrateur – résolution et visualisation](https://control-toolbox.org/OptimalControl.jl/stable/example-double-integrator-energy.html).

## 5. Architecture logicielle et bonnes pratiques 🧩

L’écosystème *control-toolbox* repose sur une architecture modulaire, conçue pour assurer **clarté**, **performance** et **pérennité**.

### 🏗️ Séparation des responsabilités

- **Modèles** : définition (types), manipulation (getters, setters) et visualisation (print, plot) des systèmes dynamiques, des problèmes de contrôle optimal et de leurs solutions.  
- **Algorithmes** : méthodes de transcription (directes, indirectes), avec réutilisation des intégrateurs et solveurs existants.  
- **Interfaces** : DSL offrant une formulation proche des mathématiques et permettant des transformations abstraites de problème (par ex. conversion d’un problème à temps final libre en problème à temps final fixe).  

### 🔄 Qualité logicielle

- **Intégration continue (CI)** : vérification automatique des tests, de la couverture et de la documentation.  
- **Tests unitaires** couvrant modèles, solveurs et API.  
- **Benchmarks réguliers** pour suivre l’évolution des performances.  
- **Détection d’incompatibilités** (“breakages”) avec les dépendances en aval.  
- **Centralisation des actions** CI/CD via le dépôt GitHub [CTActions](https://github.com/control-toolbox/CTActions).  

<div style="display: flex; gap: 20px;">
<div style="flex: 1;">
<img src="actions.png" alt="solve" width="100%" style="margin-top:10px; margin-bottom:10px;"/>
</div>
<div style="flex: 1;">
<img src="breakages.png" alt="plot" width="100%" style="margin-top:10px; margin-bottom:10px;"/>
</div>
</div>

### ⚡ Performance

- Utilisation de la **différentiation automatique** et de la compilation Julia pour un code hautement optimisé.  
- Exploitation de la **structure creuse** issue de la discrétisation des problèmes par les méthodes directes.  
- Support natif **CPU et GPU** pour traiter des problèmes de grande dimension et hautement parallélisables.  

### 📖 Ouverture et communauté

- [Documentation](https://control-toolbox.org) en ligne complète et illustrée, incluant :  
  - des [manuels](https://control-toolbox.org/OptimalControl.jl/stable) pour OptimalControl.jl ;  
  - des [tutoriels](https://control-toolbox.org/Tutorials.jl/stable) sur la discrétisation, la complémentarité direct–indirect et l’interface avec divers solveurs NLP ;  
  - des applications développées par la communauté :  
    - [Calculus of Variations](https://control-toolbox.org/CalculusOfVariations.jl/stable),  
    - [PWL models of gene regulatory networks](https://agustinyabo.github.io/PWLdynamics.jl/stable), jouable en ligne via Binder,  
    - [Geometric Preconditioner](https://control-toolbox.org/GeometricPreconditioner.jl/stable),  
    - [Loss control regions in optimal control problems](https://control-toolbox.org/LossControl.jl/stable),  
    - [Optimal control in Medical Resonance Imaging](https://control-toolbox.org/MedicalResonanceImaging.jl/stable),  
    - [Minimum time orbit transfer](https://control-toolbox.org/Kepler.jl/stable),  
    - [SIR model with social distancing](https://anasxbouali.github.io/SIRcontrol.jl/stable).  
  - un catalogue de [problèmes](https://control-toolbox.org/OptimalControlProblems.jl/stable) déjà modélisés sous OptimalControl et JuMP pour le benchmarking.  

- **Exemples reproductibles** : chaque package, tutoriel ou application fournit un `Project.toml`, un `Manifest.toml` et les informations de configuration machine.  
<img src="reproduce.png" alt="reproducibility" width="100%" style="margin-top:10px; margin-bottom:10px; max-width:700px;"/>

- **Contribution ouverte** : issues, pull requests et discussions via GitHub.  

## 7. Conclusion

### Perspectives

- Étendre l’écosystème (méthodes indirectes, méthodes homotopiques).
- Renforcer la communauté autour de *control-toolbox*.
- Vers un framework Julia de référence pour le contrôle optimal.

### Ressources

- GitHub : [https://github.com/control-toolbox](https://github.com/control-toolbox)
- Documentation en ligne : [https://control-toolbox.org](https://control-toolbox.org)
- Contact : Olivier Cots, [olivier.cots@irit.fr](mailto:olivier.cots@irit.fr)

![reproducibility](control-toolbox.png)

<!--
CSS style
-->
<style>
h1 { color: #4d64ae; }      /* bleu */
h2 { color: #ca3c32; }      /* rouge */
h3 { color: #399746; }      /* vert */
p, li { color: #1a1a1a; }   /* texte noir/gris foncé */
code { background-color: #F4F4F4; padding: 2px 4px; border-radius: 4px; }
img[alt="reproducibility"] {
    display: block;
    margin: 20px auto;
    max-width: 100%;
}
</style>
