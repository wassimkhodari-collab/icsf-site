# Résumé session ICSF — à coller en début de nouvelle conversation

## Projet
Site oncologie **ICSF** (Institut de Cancérologie du Sud Francilien)
Repo : `wassimkhodari-collab/icsf-site`
URL prod : `https://www.icsf91.fr`
Branche principale : `main`

## Stack
HTML/CSS/JS statique — 14 pages HTML + sitemap.xml

## Pages
```
index.html, institut.html, equipe.html, expertises.html, parcours.html,
rendez-vous.html, centre-sein.html, traitements.html, irm-linac.html,
reirradiation.html, oncogenetique.html, etablissements.html,
hospitalisation.html, soins-support.html
```

## Travaux réalisés (sessions précédentes)

### Intro / Preloader
- Logique combo sessionStorage + localStorage 30min TTL
- **DERNIÈRE VERSION** : skip intro uniquement si `document.referrer` contient `icsf91.fr`
  → venu de Google = intro joue toujours
  → navigation interne < 30min = skip
- Logo ICSF clicable : efface les deux flags → rejoue l'intro
```javascript
const _isInternal = document.referrer.includes('icsf91.fr');
const _plLsTs = localStorage.getItem('_plTs');
const _skipPl = _isInternal && (
  sessionStorage.getItem('_plDone') ||
  (_plLsTs && (Date.now() - parseInt(_plLsTs, 10)) < 1800000)
);
```

### Navigation / Burger menu
- Hub links dans burger : `institut.html`, `parcours.html`, `expertises.html` en font-weight:600
- "Prendre RDV" pointe partout vers `rendez-vous.html`
- `.nav-overlay` z-index: 500 (corrigé depuis 300 sur anciennes pages)
- Section labels supprimés du burger (n'étaient pas clicables, écrits en double)
- `summary::marker { display: none; }` ajouté sur 10 pages (fix Firefox)

### Firefox mobile
- `min-width: 0` sur `.section-body` (overflow flex fix)
- `-webkit-backdrop-filter` + `@supports not (backdrop-filter)` fallback
- `summary::marker` fix (10 pages)

### Photos
- Dr Mahé : `https://drive.google.com/thumbnail?id=1zYfKrJCpRJt2bJFDLWbZ77GDGGBKO2dz&sz=w400`
  + `style="object-position:top"`

### Contenu
- `expertises.html` : supprimé références centres partenaires et CHU parisiens
- `centre-sein.html` : 3 chirurgiens → "Chirurgie des cancers gynécologiques et du sein"
- `rendez-vous.html` : nouvelle page dédiée RDV (contact rows, badge 48h inline)

### SEO
- `sitemap.xml` : 14 pages
- JSON-LD ItemList sur index.html : position 6 "Prendre RDV" → rendez-vous.html

## Points de vigilance
- Ne jamais push sur une autre branche que `main` sans accord
- Images Google Drive : utiliser format `drive.google.com/thumbnail?id=...&sz=w400`
- Toujours ajouter `summary::marker { display: none; }` sur les pages avec `<details>`
- `.section-body` doit avoir `min-width: 0` pour Firefox
