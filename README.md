# fraud-dashboards-data

Data layer para los dashboards de **Fraud & Risk Prevention** — Payclip.

## Estructura
fraud-dashboards-data/
├── mbr/
│   └── data.js       ← MBR Dashboard (generado automáticamente)
└── .github/
└── workflows/
└── update-data.yml  ← GitHub Action que sincroniza desde Databricks

## ¿Cómo funciona?

1. Un notebook en Databricks genera `data.js` con métricas agregadas de fraude
2. El archivo se guarda en un Unity Catalog Volume en Databricks
3. Este GitHub Action lo descarga 3 veces al día (8am, 11am, 2pm CST) y hace push al repo
4. El canvas HTML en Glean consume el archivo via jsDelivr CDN al abrirse

## URLs

| Recurso | URL |
|---|---|
| data.js (raw) | `https://raw.githubusercontent.com/jobPayclip/fraud-dashboards-data/main/mbr/data.js` |
| data.js (CDN) | `https://cdn.jsdelivr.net/gh/jobPayclip/fraud-dashboards-data@main/mbr/data.js` |
| Purgar caché CDN | `https://purge.jsdelivr.net/gh/jobPayclip/fraud-dashboards-data@main/mbr/data.js` |

## Notas

- El archivo `.js` contiene únicamente métricas agregadas — sin datos personales ni información sensible
- El repo es público porque el canvas en Glean necesita hacer `fetch()` desde el browser
- El acceso al canvas requiere autenticación con cuenta Payclip en Glean
- Para ejecutar el Action manualmente: **Actions → Update data.js from Databricks → Run workflow**
