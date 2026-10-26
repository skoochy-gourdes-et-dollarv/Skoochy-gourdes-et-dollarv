# Skoochy Finance — backend starter

## Sa ki ladan l
- Login administratè sou sèvè a, pa gen modpas admin nan HTML.
- Pri plan chak mwa/ane nan SQLite, vizib pou tout navigatè ki itilize menm sèvè a.
- Demann abònman ak referans tranzaksyon yo anrejistre nan baz done.
- Administratè ka gade demann yo via API epi make yo `approved`, `rejected`, oswa `pending_review`.
- Cookie sesyon `httpOnly`, `sameSite=strict`, limit tantativ login, Helmet, validasyon antre.

## Sa li PA fè
- Li pa verifye MonCash, NatCash, oswa USDT otomatikman.
- Estati `approved` se yon aksyon administratif, pa prèv otomatik ke founisè peman an konfime lajan.
- Pa gen sistèm kont kliyan/modpas kliyan ladan l ankò; fòm sit la voye yon demann sèlman.
- Sa se yon starter pou tès. Fè yon revizyon sekirite, backup baz done, HTTPS, siveyans ak règleman konfidansyalite anvan lansman piblik.

## Kijan pou lanse lokalman
1. Enstale Node.js 20 oswa pi nouvo.
2. Nan katab pwojè a:
   ```bash
   npm install
   ```
3. Kopi `.env.example` kòm `.env`.
4. Chanje `ADMIN_EMAIL`, `ADMIN_PASSWORD` ak `SESSION_SECRET` pou valè inik. Modpas la dwe gen omwen 12 karaktè; sekrè sesyon an omwen 32 karaktè.
5. Lanse:
   ```bash
   npm start
   ```
6. Louvri `http://localhost:3000`.
7. Ale nan “Enskripsyon ak abònman”, konekte kòm administratè, antre pri chak mwa ak chak ane, epi peze “Sove pri abònman yo”.

Pou pwodiksyon, mete `NODE_ENV=production`, sèvi sit la sèlman sou HTTPS, mete sekrè yo nan anviwònman hosting lan (pa nan Git), epi verifye konfigirasyon proxy/cookie selon hosting lan.

## API pou administratè
- `POST /api/admin/login` — `{ "email": "...", "password": "..." }`
- `POST /api/admin/logout`
- `GET /api/plans`
- `PUT /api/admin/prices` — `{ "monthly": 5, "annual": 50 }`
- `GET /api/admin/membership-requests`
- `PATCH /api/admin/membership-requests/:id` — `{ "status": "approved" }`

## API demann abònman
`POST /api/membership-requests`:
```json
{
  "name": "Non kliyan an",
  "email": "kliyan@example.com",
  "method": "MonCash",
  "ref": "REF-TRANZAKSYON",
  "plan": "monthly"
}
```
API a pa sere okenn modpas kliyan. Pa mande kliyan voye enfòmasyon sekrè oswa fraz rekiperasyon wallet.


## Monetizasyon ak Skoochy Finance

- **Abònman:** administratè a ka fikse pri chak mwa/ane; demann yo rete tann verifikasyon manyèl.
- **Mezi tan:** sistèm nan konte tan paj la vizib, voye segonn an ti pakè bay sèvè a, epi bay estatistik 30 dènye jou yo nan panèl administratè a.
- **Piblisite:** poko aktive. Apre sit la fin pibliye, mete yon rezo piblisite ki aksepte sit la (pa egzanp AdSense si sit la ak kont lan kalifye), ajoute etikèt piblisite epi respekte règleman sou vi prive ak bon jan trafik.
- **Limit:** tan itilizasyon pa pwodui revni otomatikman. Pa itilize klik fo, refresh otomatik oswa trafik achte pou fè piblisite parèt plis. Tan an se estimasyon, pa yon kontè egzak.
- **Konfidansyalite:** ID o aza pou sesyon an konsève sèlman nan sessionStorage; bazdone a anrejistre ID pseudonim, non paj la, kantite segonn ak dat la, san non/imèl/IP nan tab analiz la. Mete yon avi vi prive anvan lansman.
