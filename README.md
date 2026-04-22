# AmorProof

Aplicación web de la metodología AmorProof basada en los 4 cuadrantes modales de Peirce.

## Archivos

```
amorproof/
├── index.html          ← Home
├── testimonios.html    ← Testimonios
├── prueba.html         ← Flujo completo (4 pantallas)
├── assets/
│   ├── logosinletra.svg  ← Tu logo actual
│   └── tamara.mp4        ← Video testimonio
└── README.md
```

## Cómo publicar en GitHub Pages (paso a paso)

### 1. Crear el repositorio
1. Ve a https://github.com/new
2. Nombre del repositorio: `amorproof`
3. Marca "Public"
4. Clic en "Create repository"

### 2. Subir los archivos
**Opción A — Desde el navegador (más fácil):**
1. En tu repositorio, clic en "uploading an existing file"
2. Arrastra todos los archivos y la carpeta `assets/`
3. Clic en "Commit changes"

**Opción B — Desde la terminal:**
```bash
cd carpeta-amorproof
git init
git add .
git commit -m "primera versión"
git remote add origin https://github.com/TU_USUARIO/amorproof.git
git push -u origin main
```

### 3. Activar GitHub Pages
1. Ve a Settings → Pages (en tu repositorio)
2. En "Source" selecciona "Deploy from a branch"
3. Branch: `main`, carpeta: `/ (root)`
4. Clic en "Save"
5. En ~2 minutos tu app estará en:
   **https://TU_USUARIO.github.io/amorproof**

---

## Agregar tu dominio propio (opcional)
1. En Settings → Pages → Custom domain: escribe `amorproof.com`
2. En tu proveedor de dominio agrega un registro CNAME:
   - Nombre: `www`
   - Valor: `TU_USUARIO.github.io`

---

## Para conectar Supabase (guardar datos de usuarios) — cuando estés lista

### 1. Crear proyecto en Supabase
1. Ve a https://supabase.com y crea una cuenta
2. Nuevo proyecto → anota la URL y la API Key pública

### 2. Crear tabla en Supabase
```sql
create table diagnosticos (
  id uuid default gen_random_uuid() primary key,
  created_at timestamp with time zone default now(),
  desde text,
  hacia text,
  por_donde text,
  resultado text,
  cuadrante text,
  arquetipo_sombra text,
  arquetipo_positivo text,
  antes int,
  ahora int,
  verif_pensamiento text,
  verif_accion text,
  verif_sensacion text
);
```

### 3. Agregar en prueba.html (en la función calcDx, justo después de asignar S.diagQ)
```javascript
// SUPABASE — descomentar cuando esté listo
// const SUPABASE_URL = 'https://TU_PROYECTO.supabase.co';
// const SUPABASE_KEY = 'TU_API_KEY_PUBLICA';
// await fetch(`${SUPABASE_URL}/rest/v1/diagnosticos`, {
//   method: 'POST',
//   headers: {
//     'Content-Type': 'application/json',
//     'apikey': SUPABASE_KEY,
//     'Authorization': `Bearer ${SUPABASE_KEY}`
//   },
//   body: JSON.stringify({
//     desde: S.coords[0],
//     hacia: S.coords[1],
//     por_donde: S.coords[2],
//     resultado: S.coords[3],
//     cuadrante: S.diagQ,
//     arquetipo_sombra: QD[S.diagQ].shadow,
//     arquetipo_positivo: QD[S.diagQ].positive
//   })
// });
```

---

## Notas importantes
- La API key de Claude está siendo manejada por el proxy de Claude.ai en el prototipo.
  Para producción real necesitarás un backend propio que proteja la key.
  La opción más simple: usar Supabase Edge Functions como proxy seguro.
- El video `assets/tamara.mp4` debe estar en la carpeta `assets/` junto a los HTML.
