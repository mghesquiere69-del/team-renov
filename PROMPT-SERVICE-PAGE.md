# Prompt réutilisable – Réécriture complète d'une page de service Team Renov

> **Mode d'emploi** : Copier ce prompt. Remplacer `[NOM_DU_SERVICE]` + `[FICHIER]` par le service ciblé. Joindre le fichier `.astro` actuel en contexte pour que l'IA connaisse la structure de départ.

---

## Le prompt

Tu cumules 3 expertises pour cette tâche :
1. **Copywriter conversion** — tu appliques les frameworks PAS (Problem → Agitate → Solution) et AIDA (Attention → Intérêt → Désir → Action) à chaque section.
2. **Spécialiste SEO on-page** — tu structures le contenu pour ranker sur les requêtes locales BTP/rénovation.
3. **Développeur front-end Astro/Tailwind** — tu produis du code propre, responsive, accessible.

Ta mission : réécrire intégralement la page de service `[NOM_DU_SERVICE]` (fichier `[FICHIER]`) du site **Team Renov** pour la transformer d'une page squelettique en une page de vente complète, crédible et optimisée.

---

### 1. CONTEXTE ENTREPRISE

| Info | Détail |
|---|---|
| **Entreprise** | Team Renov — artisans rénovation tous corps de métier |
| **Services** | Placo, peinture, électricité, plomberie, carrelage, maçonnerie, menuiserie, enduit, projets clé en main |
| **Zone** | Île-de-France (Paris et petite/grande couronne) |
| **Cible principale** | Propriétaires particuliers qui rénovent leur logement |
| **Cible secondaire** | Investisseurs locatifs, petits pros (cabinets, commerces) |
| **Différenciateurs** | Un seul interlocuteur pour tous les corps de métier · Assurance décennale · Devis gratuit sous 48h · Suivi photo quotidien du chantier · Certification RGE |
| **Ton éditorial** | Direct, concret, rassurant. Vouvoiement. Pas de superlatifs creux. Phrases courtes. On parle comme un artisan qui maîtrise son sujet, pas comme une agence marketing. |
| **Objectif conversion** | Formulaire de contact (devis gratuit) ou appel au 06 21 53 04 53 |

---

### 2. STACK TECHNIQUE & COMPOSANTS

**Framework** : Astro 6 + Tailwind CSS 4 (v4 — `@import "tailwindcss"`, thème via `@theme {}`)

**Composants disponibles** (ne PAS en créer de nouveaux) :

```
ServicePageLayout — Layout parent. Fournit automatiquement :
  ├── Hero (breadcrumb + icône + titre h1)
  ├── HighlightsStrip (4 badges sous le hero)
  ├── <slot /> ← C'EST ICI QUE TU ÉCRIS
  ├── Section "Services associés" (liens vers pages sœurs)
  └── CTA footer (devis + téléphone)

Section — Wrapper de section
  Props : title (string), subtitle? (string), bg ("white"|"light"|"primary"), id? (string)
  Génère : <section> avec <h2> centré + <slot>
```

**NE PAS recréer** ce que le layout fournit déjà. Ton code commence APRÈS `>` de `<ServicePageLayout>` et finit AVANT `</ServicePageLayout>`.

**Classes utilitaires du projet** :
- Boutons : `btn-primary`, `btn-secondary`
- Cards : `card` (bg-white, rounded-xl, shadow, hover effect, p-6)
- Texte : `text-gray-medium`, `text-gray-dark`, `text-primary`, `text-accent`
- Fonds : `bg-gray-light`

**Images** : dossier `/images/services/`. Si une image n'existe pas encore :
```html
<div class="bg-gray-200 rounded-2xl aspect-[4/3] flex items-center justify-center text-gray-400 text-sm italic">
  [Description PRÉCISE de la photo à prendre : angle, sujet, ambiance]
</div>
```

**Animations** : attribut `data-animate` sur le conteneur principal de chaque section (un seul par section, pas imbriqué).

---

### 3. ARCHITECTURE DE LA PAGE — 7 SECTIONS OBLIGATOIRES

Chaque section utilise le composant `<Section>`. Alterner strictement `bg` : white → light → white → light → white → light → white.

---

#### SECTION 1 — « L'accroche » (bg="white")
**Objectif** : accrocher le visiteur en 5 secondes. Framework PAS.

| Élément | Détail |
|---|---|
| **Layout** | Grid 2 colonnes (`lg:grid-cols-2`). Texte à gauche, visuel à droite. |
| **Paragraphe 1** | Commencer par une QUESTION ou SITUATION concrète du client. Ex: "Vos murs sont fissurés et votre installation date de 30 ans ?" |
| **Paragraphe 2** | Agiter le problème : conséquences si on ne fait rien (sécurité, valeur du bien, confort…) |
| **Paragraphe 3** | Introduire Team Renov comme la solution. Mentionner l'expertise et la zone d'intervention. |
| **Mini-liste** | 3 points clés avec icônes check SVG (avantages concrets, pas de banalités) |
| **Visuel** | Image réelle OU slider avant/après OU placeholder détaillé |
| **Volume** | Minimum 180 mots de texte |

---

#### SECTION 2 — « Ce qu'on fait » — Prestations (bg="light")
**Objectif** : montrer la diversité des compétences.

| Élément | Détail |
|---|---|
| **Layout** | Grid 6 cards (`sm:grid-cols-2 lg:grid-cols-3`) |
| **Chaque card** | Icône SVG (Heroicons, `w-6 h-6`, dans un conteneur `w-10 h-10 bg-accent/10 text-accent rounded-lg`) + titre `<h3>` + description |
| **Description** | 2-3 phrases. Phrase 1 = ce qu'on fait. Phrase 2 = le bénéfice pour le client. Être SPÉCIFIQUE au métier. |
| **Subtitle de section** | Une phrase qui contextualise (ex: "Du diagnostic à la finition, on gère l'intégralité de votre chantier [service].") |

---

#### SECTION 3 — « Vos projets, nos solutions » — Cas d'usage (bg="white")
**Objectif** : le visiteur se reconnaît dans un scénario concret → "c'est exactement mon cas".

| Élément | Détail |
|---|---|
| **Layout** | Grid 2 colonnes (`md:grid-cols-2`), 4 items |
| **Chaque item** | Icône check dans un cercle + titre bold + paragraphe 2-3 phrases |
| **Ton** | Raconter une mini-histoire client. Ex: "Votre locataire est parti et l'appartement a besoin d'un coup de neuf avant remise en location ? Nous intervenons en 2 semaines pour…" |
| **Variété** | Couvrir : résidentiel, investissement locatif, après-sinistre, professionnel |

---

#### SECTION 4 — « Comment ça se passe » — Méthode (bg="light")
**Objectif** : rassurer sur le processus. Éliminer l'incertitude.

| Élément | Détail |
|---|---|
| **Layout** | Grid 4 colonnes (`sm:grid-cols-2 md:grid-cols-4`) |
| **Chaque étape** | Numéro (01-04) dans un badge `w-12 h-12 bg-accent text-white rounded-xl` + titre + 2 phrases |
| **Étapes** | SPÉCIFIQUES au service. Pas "Écoute → Devis → Travaux → Livraison" générique. Décrire ce qui se passe concrètement pour CE service. |
| **Subtitle** | Ex: "De la prise de contact à la réception, voici les étapes de votre chantier." |

---

#### SECTION 5 — « Pourquoi Team Renov » — Confiance (bg="white")
**Objectif** : lever les dernières objections. Preuve > promesse.

| Élément | Détail |
|---|---|
| **Layout** | Grid 6 cards (`sm:grid-cols-2 lg:grid-cols-3`) + CTA en dessous |
| **Chaque card** | Titre bold + texte 1-2 phrases |
| **Contenu** | Être FACTUEL. Utiliser des chiffres, des noms de marques/certifications, des détails vérifiables. **Zéro phrase creuse.** |
| **Arguments obligatoires** | ① Artisans qualifiés (années d'expérience) ② Matériaux de marque (nommer les marques) ③ Respect des délais ④ Chantier propre ⑤ Coordination multi-corps ⑥ Devis transparent ligne par ligne |
| **CTA final** | Texte accrocheur + `btn-primary` lien vers /contact |

---

#### SECTION 6 — « Questions fréquentes » — FAQ SEO (bg="light")
**Objectif** : ranker sur les requêtes longue traîne + rassurer les hésitants.

| Élément | Détail |
|---|---|
| **Layout** | 5-6 questions en `<details><summary>`, max-w-3xl centré |
| **Style summary** | `cursor-pointer font-semibold text-primary py-4 border-b border-gray-200` |
| **Style contenu** | `text-gray-medium text-sm leading-relaxed pb-4` |
| **Questions obligatoires** | ① Combien ça coûte (fourchette de prix ou "sur devis" + facteurs) ② Combien de temps durent les travaux ③ Faut-il quitter le logement pendant les travaux ④ Quelles garanties ⑤ Question spécifique au métier |
| **Réponses** | Directes, honnêtes, 2-4 phrases. Terminer par "Contactez-nous pour un devis précis adapté à votre projet." |
| **Schema.org** | Commenter `<!-- FAQ schema à ajouter en JSON-LD -->` en haut de la section pour rappel futur |

---

#### SECTION 7 — « Nos chiffres » — Preuve sociale (bg="white")
**Objectif** : ancrage de crédibilité avant le CTA final du layout.

| Élément | Détail |
|---|---|
| **Layout** | Grid 3 ou 4 stats (`sm:grid-cols-2 md:grid-cols-4`), centré |
| **Chaque stat** | Chiffre grand (`text-4xl font-extrabold text-accent`) + label (`text-sm text-gray-medium`) |
| **Stats possibles** | "10+ ans d'expérience", "150+ chantiers réalisés", "48h pour un devis", "100% assuré décennale", "Note 4.8/5" — choisir les plus pertinentes pour ce service |

---

### 4. RÈGLES DE RÉDACTION — NON NÉGOCIABLES

| # | Règle | Mauvais exemple ❌ | Bon exemple ✅ |
|---|---|---|---|
| 1 | **Minimum 1000 mots** de contenu texte visible (hors HTML) | Page de 200 mots avec 2 sections | Page dense avec 7 sections riches |
| 2 | **Chaque phrase apporte un FAIT** | "Nous sommes passionnés par notre métier" | "Nos peintres appliquent systématiquement 2 couches croisées avec un temps de séchage de 6h entre chaque passe" |
| 3 | **Bénéfice client > description technique** | "Nous posons du placo BA13 sur ossature métallique" | "Vous gagnez une pièce supplémentaire en 3 jours, sans toucher aux murs porteurs" |
| 4 | **Interdit** : "passionné", "à votre écoute", "solutions sur mesure", "savoir-faire", "vos envies", "accompagnement personnalisé" | | Remplacer par des preuves concrètes |
| 5 | **SEO naturel** | Bourrage de mots-clés | Nom du service + "Île-de-France" dans le H2 d'une section + variantes longue traîne dans les paragraphes |
| 6 | **CTA intermédiaire** | Un seul CTA en bas de page | Au minimum 2 CTA dans le slot : un après section 1 ou 3, un après section 5 |
| 7 | **Phrases courtes** | Phrases de 40+ mots | Max 25 mots par phrase. Alterner phrases courtes/moyennes. |
| 8 | **Zéro placeholder** | "Lorem ipsum" / "Description à venir" | Contenu final publiable (sauf placeholders d'images avec description précise) |
| 9 | **Vocabulaire concret du bâtiment** | Rester vague et générique | Utiliser les vrais termes du métier : "sous-couche d'accrochage", "mortier-colle C2", "norme NF C 15-100", etc. |
| 10 | **Vouvoiement + ton direct** | "N'hésitez pas à faire appel à nos services" | "Appelez-nous. On se déplace sous 48h pour établir votre devis." |

---

### 5. RÈGLES TECHNIQUES

1. **Composants** : uniquement `Section` et `ServicePageLayout` — pas de nouveau composant
2. **Icônes** : SVG Heroicons inline, `stroke-width="1.5"`, classes `w-6 h-6` (ou `w-5 h-5` pour les checks)
3. **`data-animate`** : un seul par section, sur le conteneur principal, JAMAIS imbriqué dans un autre `data-animate`
4. **Alternance `bg`** : white → light → white → light → white → light → white (strictement)
5. **Tailwind only** : pas de `<style>` sauf cas très spécifique documenté (slider avant/après)
6. **Responsive** : mobile-first. Grilles : `grid-cols-1` → `sm:grid-cols-2` → `lg:grid-cols-3`
7. **Images** : `alt` descriptif SEO, pas de `loading="lazy"` sur le premier visuel visible
8. **Accessibilité** : contraste suffisant, liens descriptifs, `aria-label` sur les éléments interactifs

### 6. FRONTMATTER — CHECK-LIST

```javascript
const highlights = [
  // 4 items COURTS (3-5 mots max) — bénéfice client, pas feature technique
  // ❌ "NF C 15-100" → ✅ "Installation aux normes"
];

const relatedServices = [
  // 4 à 6 liens vers les services complémentaires logiques
  // { title: "Nom visible", href: "/services/slug" }
];
```

| Prop | Contrainte |
|---|---|
| `title` | Le nom du service tel qu'affiché dans le H1. Clair et descriptif. |
| `metaTitle` | Max 60 caractères. Format : "[Service] – Team Renov \| [Bénéfice clé]" |
| `metaDescription` | Max 155 caractères. Inclure : service + zone + CTA implicite ("Devis gratuit") |
| `highlights` | 4 strings courtes. Orientées bénéfice, pas jargon. |
| `relatedServices` | 4-6 objets `{title, href}`. Services logiquement liés. |

---

### 7. FORMAT DE SORTIE

Retourne le fichier `.astro` **complet** prêt à copier-coller, du `---` d'ouverture au dernier `</ServicePageLayout>`. Inclure :
- Le frontmatter avec toutes les variables
- Les imports
- Toutes les 7 sections
- Les `<style>` / `<script>` éventuels (FAQ accordéon, slider)

**Aucune explication autour du code.** Juste le fichier.
