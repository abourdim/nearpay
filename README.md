# NearPay — Le paiement à portée de main

> Solution de paiement NFC sans friction pour restaurants, bars, hôtels et événements.

---

## 🚀 Démarrage rapide

```bash
# Cloner le projet
git clone https://github.com/votre-org/nearpay.git
cd nearpay

# Ouvrir directement (aucune dépendance requise)
open index.html
# ou
python3 -m http.server 3000
# puis naviguer sur http://localhost:3000
```

---

## 📁 Structure du projet

```
nearpay/
├── index.html          # Page principale (HTML + CSS + JS intégrés)
├── README.md           # Ce fichier
├── .gitignore          # Fichiers ignorés par Git
├── assets/             # Images, icônes, logos (à venir)
│   └── .gitkeep
├── i18n/               # Traductions (architecture prête)
│   └── fr.json         # Français (actif)
└── docs/
    └── architecture.md # Documentation technique
```

---

## 🎯 Fonctionnalités de la page

| Fonctionnalité | Description |
|---|---|
| **Bismillah** | بِسْمِ اللَّهِ الرَّحْمَنِ الرَّحِيمِ centré en haut |
| **Mode switcher** | Professionnel / Client — contenu adaptatif |
| **Demo NFC hero** | Badge cliquable avec animation receipt |
| **3 modes d'interaction** | Téléphone→Badge / Badge→Serveur / QR-SMS |
| **9 idées géniales** | Cartes expandables avec notes techniques |
| **Démo interactive** | Simulation paiement pas à pas + confetti |
| **Stats** | Visible en mode Professionnel uniquement |
| **Témoignages** | Adaptés selon le mode actif |
| **CTA** | Texte dynamique selon le mode |
| **4 boutons** | ❓ Aide / 💬 FAQ / 📚 Wiki / ⚙️ Paramètres |
| **i18n ready** | Architecture prête pour EN, ES, AR |
| **Scroll animations** | Intersection Observer, CSS uniquement |

---

## 👥 Audiences

La page s'adapte automatiquement à 2 modes :

- **👔 Professionnel** — restaurateurs, gérants, investisseurs  
  Focus : ROI, rotation des tables, chiffre d'affaires, statistiques
  
- **👤 Client** — utilisateurs finaux  
  Focus : simplicité, rapidité, expérience, plaisir

---

## 💡 9 Idées géniales présentées

1. 🍽️ **Badge à table** — remplacement de l'attente de l'addition
2. ➗ **Partage automatique** — split bill sans calcul
3. 🔄 **Commander sans serveur** — reorder depuis le téléphone
4. 🛎️ **Appeler le serveur** — notification silencieuse
5. ⭐ **Badge VIP** — profil client personnalisé
6. 💳 **Wallet rechargeable** — porte-monnaie multi-services
7. 🎪 **Bracelet événement** — festival, mariage, corporate
8. 🏨 **Clé d'hôtel = paiement** — folio de chambre unifié
9. 🏖️ **Beach club / Rooftop** — commande géolocalisée

---

## 🔧 Architecture technique (pour les ingénieurs)

```
Badge NFC (NTAG213)
    │ URL encodée
    ▼
Téléphone client (NFC/QR)
    │ HTTP GET
    ▼
API NearPay
    │ tableId → noteId
    ▼
POS (Lightspeed / Zelty / Cashpad)
    │ note ouverte
    ▼
Paiement (Stripe Terminal / SumUp / Adyen)
    │ webhook
    ▼
Clôture automatique de la note
```

**Stack suggérée :**
- Frontend : Vanilla JS (0 dépendance) ou Next.js
- Backend : Node.js / FastAPI
- Paiement : Stripe Terminal
- Base de données : PostgreSQL
- Temps réel : WebSocket / Server-Sent Events
- Notifications : FCM (Android) / APNs (iOS)

---

## 🌍 Internationalisation (i18n)

La page est en **français par défaut**. L'architecture est prête pour :
- 🇬🇧 English
- 🇪🇸 Español  
- 🇸🇦 عربي

Les chaînes de caractères sont centralisées dans `/i18n/fr.json`.

---

## 📱 Compatibilité

| Appareil | NFC | QR Code |
|---|---|---|
| iPhone 7+ (iOS 13+) | ✅ | ✅ |
| Android 2015+ | ✅ | ✅ |
| Anciens appareils | ❌ | ✅ |

---

## 🎨 Design system

| Variable | Valeur | Usage |
|---|---|---|
| `--bg` | `#07070F` | Fond principal |
| `--gold` | `#C9A84C` | Couleur primaire |
| `--gold-light` | `#E8D5A3` | Or clair |
| `--text-muted` | `#8A8070` | Texte secondaire |

**Typographie :**
- Amiri (Google Fonts) — Bismillah arabe
- Cormorant Garamond — Titres, logo
- DM Sans — Corps de texte

---

## 📄 Licence

© 2025 NearPay — Tous droits réservés.

---

*v1.0.0 — Construit avec ❤️ et بِسْمِ اللَّهِ*
