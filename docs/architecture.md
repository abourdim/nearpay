# Architecture technique NearPay

## Vue d'ensemble

```
┌─────────────────────────────────────────────────────────┐
│                    Client (téléphone)                   │
│                                                         │
│  NFC tap / QR scan / SMS link                          │
└──────────────────┬──────────────────────────────────────┘
                   │ HTTPS
                   ▼
┌─────────────────────────────────────────────────────────┐
│              API NearPay (REST + WebSocket)             │
│                                                         │
│  GET  /table/:id      → note ouverte                   │
│  POST /table/:id/pay  → initier paiement               │
│  POST /table/:id/call → appeler serveur                │
│  POST /table/:id/order → nouvelle commande             │
└──────────────────┬──────────────────────────────────────┘
                   │
        ┌──────────┼──────────────┐
        ▼          ▼              ▼
┌──────────┐ ┌──────────┐ ┌──────────────┐
│   POS    │ │ Paiement │ │ Notifications│
│ Lightspd │ │  Stripe  │ │  FCM / APNs  │
│  Zelty   │ │  Adyen   │ │  WebSocket   │
│  Cashpad │ │  SumUp   │ └──────────────┘
└──────────┘ └──────────┘
```

## Flux paiement complet

```
1. Client s'assoit → serveur scanne badge → note créée dans POS

2. Commandes ajoutées au fil du repas → note mise à jour

3. Client tap téléphone sur badge
   → NFC lit URL (ex: nearpay.io/t/TABLE-12-TOKEN)
   → navigateur ouvre la page
   → API retourne le détail de la note

4. Client choisit son moyen de paiement
   → Stripe Payment Intent créé côté serveur
   → confirmation Apple Pay / Google Pay

5. Paiement validé
   → webhook Stripe → API → POS clôture la note
   → notification serveur : table libérée
```

## Technologies recommandées

### Backend
- **Runtime** : Node.js 20+ ou Python 3.11+
- **Framework** : Express / FastAPI
- **BDD** : PostgreSQL (transactions ACID)
- **Cache** : Redis (sessions, soldes wallet)
- **Temps réel** : Socket.io / Server-Sent Events

### Frontend
- **Approche** : Progressive Web App (PWA)
- **Framework** : Next.js ou Vanilla JS
- **Paiement UI** : Stripe Elements

### Infrastructure
- **Hébergement** : Vercel / Railway / Scaleway
- **CDN** : Cloudflare
- **Monitoring** : Sentry + Datadog
- **CI/CD** : GitHub Actions

## Sécurité

- Tokens de table à usage unique (UUID v4, TTL 24h)
- HTTPS obligatoire
- Signature webhook Stripe
- Rate limiting sur l'API
- Certification PCI DSS (via Stripe)
- Aucune donnée de carte stockée côté NearPay

## Intégrations POS

| POS | Méthode | Status |
|-----|---------|--------|
| Lightspeed | REST API v3 | ✅ Disponible |
| Zelty | API partenaire | ✅ Disponible |
| Cashpad | Webhook | 🔄 En cours |
| L'Addition | API | 🔄 En cours |
| Revo | SDK | 📋 Planifié |

## Types de badges

| Type | Puce | Mémoire | Usage |
|------|------|---------|-------|
| Sticker table | NTAG213 | 144 bytes | URL simple |
| Carte table | NTAG215 | 504 bytes | URL + data |
| Bracelet | NTAG216 | 888 bytes | Wallet complet |
| Clé hôtel | MIFARE Classic | 1KB | PMS intégration |
