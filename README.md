# 📊 Pricing Intelligence — Micro-SaaS pour solopreneurs

> **Augmentez vos prix sans perdre un client.**
> Le premier outil de pricing pensé pour les indépendants français — là où ProfitWell
> et Price Intelligently ne s'adressent qu'aux équipes, Pricing Intelligence donne au
> solopreneur un chiffre clair, trois scénarios et le bon message pour les annoncer.

**Abonnement : 15 à 30 €/mois** (sans engagement, résiliable à tout moment).

---

## 🚀 Aperçu du produit

| Problème | Solution |
|---|---|
| L'inflation rogne la marge des indépendants chaque année | Un diagnostic pricing chiffré en 5 minutes |
| Les outils existants visent les équipes et les gros volumes | Un outil conçu pour le portefeuille d'un solo (5 à 50 clients) |
| Les solopreneurs ne savent pas comment annoncer une hausse | Messages d'annonce générés selon le scénario choisi |
| Une hausse mal gérée fait fuir les clients | Méthode complète : segmentation, objections, suivi du churn |

---

## 📁 Structure du projet

```
pricing-intelligence/
├── index.html            # Page 3D immersive (Three.js) : hero, 3 offres, formulaire EmailJS
├── calculateur.html      # Diagnostic pricing interactif (JS pur, sans dépendance)
├── chatbot.js            # Widget chatbot (FAQ + capture de leads via EmailJS)
├── chatbot-config.js     # Configuration du chatbot (FAQ Pricing Intelligence)
├── templates/
│   ├── email-annonce-hausse.md        # Email d'annonce de hausse (3 tons + checklist)
│   ├── email-reponse-objection-prix.md # Réponses aux objections de prix (5 objections)
│   ├── argumentaire-valeur.md          # Construire et justifier votre valeur
│   ├── segmentation-clients.md         # Segments A/B/C + séquençage de la hausse
│   └── suivi-churn.md                  # Suivi 90 jours après la hausse + reconquête
└── README.md
```

---

## 🧮 Comment fonctionne le calculateur (`calculateur.html`)

Questionnaire en 4 étapes, 100 % dans le navigateur, aucun serveur :

1. **Vos coûts** — coûts fixes + variables mensuels, marge cible
2. **Votre activité** — heures facturées / mois, nombre de clients
3. **Vos clients** — taux de churn mensuel, tarif actuel moyen (facultatif)
4. **Votre valeur** — valeur perçue, positionnement souhaité

### Le moteur de calcul (déterministe, documenté)

```
coût de revient horaire   = (fixes + variables) ÷ heures facturées
prix horaire break-even   = coût de revient ÷ (1 − marge cible)
prix horaire recommandé   = break-even × multiplicateur valeur × ajustement positionnement
prix par client           = prix horaire recommandé × heures par client
```

| Paramètre | Valeurs |
|---|---|
| Multiplicateur valeur perçue | faible ×1,10 · moyenne ×1,30 · forte ×1,55 · très forte ×1,85 |
| Ajustement positionnement | standard ×0,95 · expert ×1,05 · premium ×1,15 |
| Scénario prudent | prix recommandé × 0,90 |
| Scénario équilibré | prix recommandé × 1,00 |
| Scénario agressif | prix recommandé × 1,18 |
| Pertes clients estimées | clients × min(churn, hausse × 0,25) — élasticité modérée |

**Recommandation automatique :** churn > 7 % → prudent · valeur très forte + positionnement
expert/premium + churn ≤ 4 % → agressif · sinon → équilibré.

**Sorties :** 3 scénarios chiffrés (prix client, prix horaire, % de hausse, clients perdus
estimés, CA projeté, gain mensuel) + message d'annonce de hausse généré selon le scénario,
avec boutons copier / télécharger.

---

## 📧 Formulaire de contact (EmailJS — réel)

Les deux formulaires (demande d'abonnement sur `index.html` et capture de leads du
chatbot) envoient des emails réels via EmailJS :

| Paramètre | Valeur |
|---|---|
| Service ID | `service_cy1ytdb` |
| Template ID | `template_xpo58cv` |
| Clé publique | `8Pui4ZEqxW2jRVF7h` |
| Payload | `{ site, name, email, question }` |

Le champ `site` vaut `Pricing Intelligence` ; `question` contient l'offre choisie ou la
question posée au chatbot. Les leads sont aussi sauvegardés en local (`localStorage`).

---

## 🎨 Design

- Fond sombre haut de gamme **#070b14**, dégradés cyan → violet (`#5eead4 → #38bdf8 → #818cf8`)
- `index.html` : scène WebGL Three.js (1 800 particules, icosaèdres wireframe, anneau
  orbital), parallaxe souris (couches `data-depth`), scroll en profondeur, carte inclinable 3D
- `calculateur.html` : fond particules canvas 2D léger (rapide sur mobile)
- Glassmorphism, boutons glow, typographie claire — tout en français, orthographe soignée

> ⚠️ **Piège CDN Three.js :** le build global `three@0.152.2` est utilisé (les versions
> récentes sont module-only et cassent les scripts classiques).

---

## 🛠️ Tester en local

```bash
cd ~/Documents/livrables/pricing-intelligence
python3 -m http.server 8000
# puis ouvrir http://localhost:8000/index.html
```

Aucune compilation, aucune dépendance à installer : les pages fonctionnent telles quelles.

---

## 🧭 Feuille de route produit

- [x] Page 3D immersive + 3 offres (15 / 25 / 30 €)
- [x] Calculateur de diagnostic gratuit et illimité
- [x] Messages d'annonce générés par scénario
- [x] 5 templates opérationnels (annonce, objections, valeur, segmentation, churn)
- [x] Chatbot FAQ + capture de leads
- [ ] Paiement en ligne (Stripe) pour automatiser l'abonnement
- [ ] Espace membre : historique des diagnostics
- [ ] Module « audit mensuel » pour le Pack Pro (30 €)
- [ ] Version anglaise pour le marché international

---

## ⚖️ Positionnement

**Pour qui :** les solopreneurs français (freelances, artisans, coachs, consultants)
qui facturent entre 300 et 5 000 €/mois et n'ont jamais osé toucher à leurs prix.

**Contre qui :** ProfitWell, Price Intelligently, Paddle — des outils d'équipe, trop
lourds et trop chers pour un portefeuille de 5 à 50 clients.

**Pitch :** « En 5 minutes, sachez combien vous devriez facturer — et annoncez-le à vos
clients sans les perdre. »
