# 🚀 Guía de Despliegue — Aves del Saber 500

> Cómo publicar tu sitio en internet para que sea accesible a estudiantes.

---

## Opción 1: Netlify (Recomendado - Más Fácil)

### Paso 1: Preparar archivos
```
aves-del-saber/
├── index.html (renombra ADS.html a index.html)
├── admin.html
├── README.md
└── database-example.json
```

### Paso 2: Crear cuenta en Netlify
1. Ve a https://netlify.com
2. Haz clic en "Sign up"
3. Conecta tu cuenta de GitHub (o crea una)

### Paso 3: Subir proyecto
1. Haz clic en "New site from Git"
2. Conecta tu repositorio GitHub
3. Configura:
   - **Base directory**: (dejar vacío)
   - **Build command**: (dejar vacío)
   - **Publish directory**: (dejar vacío)
4. Haz clic en "Deploy"

**Resultado**: Tu sitio estará en `tu-nombre.netlify.app` en 5 minutos

### Ventajas
✅ HTTPS automático
✅ CDN global
✅ Gratis (tier hobby)
✅ Actualizaciones automáticas desde GitHub

---

## Opción 2: GitHub Pages (Gratis)

### Paso 1: Crear repositorio
1. Ve a https://github.com
2. Haz clic en "New repository"
3. Nombra: `aves-del-saber`
4. Marca "Public"

### Paso 2: Subir archivos
```bash
git clone https://github.com/TU_USUARIO/aves-del-saber.git
cd aves-del-saber
# Copia tus archivos aquí
git add .
git commit -m "Inicial commit"
git push origin main
```

### Paso 3: Habilitar Pages
1. Ve a **Settings** → **Pages**
2. En **Source**, selecciona **main**
3. Haz clic en **Save**

**Resultado**: Tu sitio estará en `tu-usuario.github.io/aves-del-saber`

### Ventajas
✅ Gratis (GitHub es gratis)
✅ Versionado con Git
✅ HTTPS automático
✅ Fácil de actualizar

---

## Opción 3: Vercel (Para desarrolladores)

### Paso 1: Conectar GitHub
1. Ve a https://vercel.com
2. Haz clic en "Sign up"
3. Conecta tu cuenta de GitHub

### Paso 2: Importar proyecto
1. Haz clic en "New Project"
2. Selecciona tu repositorio
3. Haz clic en "Import"

**Resultado**: Deployment automático en `aves-del-saber.vercel.app`

---

## Opción 4: Servidor Propio (Avanzado)

### Requisitos
- Hosting con PHP/Node.js
- Acceso SSH
- FTP o control panel

### Pasos
1. Comprime tus archivos: `aves-del-saber.zip`
2. Sube por FTP a la carpeta `public_html`
3. Descomprime en el servidor
4. Accede a `https://tu-dominio.com`

### Proveedores Recomendados
- **Hostinger** - Desde $2.99/mes
- **SiteGround** - Desde $2.99/mes
- **Bluehost** - Desde $2.95/mes

---

## Opción 5: Servidor Local (Pruebas)

### Windows
```bash
# Instalar Python
python -m http.server 8000

# Abrir navegador
http://localhost:8000
```

### Mac/Linux
```bash
python3 -m http.server 8000
```

---

## Configuración de Dominio Personalizado

### Cambiar dominio en Netlify
1. Ve a **Site settings** → **Domain management**
2. Haz clic en "Add domain"
3. Ingresa tu dominio (ej: `avesdelsaber.com`)
4. Sigue instrucciones para registrar el dominio

### Registradores de Dominio
- **Namecheap** - Dominios baratos y confiables
- **Google Domains** - Integración Google
- **GoDaddy** - Popular, mucha variedad
- **Registro.com** - Especializado en Colombia

**Costo**: ~$12/año (puede variar)

---

## Estructura Recomendada para Producción

```
aves-del-saber/
├── index.html                    # Página principal (ADS.html)
├── admin.html                    # Panel administrador
├── assets/
│   ├── css/
│   │   └── styles.css           # Estilos separados (opcional)
│   ├── js/
│   │   ├── main.js              # JavaScript principal
│   │   └── admin.js             # JS del admin
│   └── images/
│       ├── logo.png
│       └── favicon.ico
├── docs/
│   ├── README.md
│   ├── QUICK-START.md
│   └── FIREBASE-INTEGRATION.md
├── data/
│   └── database-example.json
├── .gitignore
├── package.json (si usas Node.js)
└── netlify.toml (configuración Netlify)
```

---

## Configuración de netlify.toml

Crea un archivo `netlify.toml` en la raíz:

```toml
[build]
  command = "echo 'Sitio estático'"
  publish = "."

[[redirects]]
  from = "/*"
  to = "index.html"
  status = 200

[[headers]]
  for = "/*"
  [headers.values]
    X-Frame-Options = "SAMEORIGIN"
    X-Content-Type-Options = "nosniff"
```

---

## Variables de Entorno (Firebase)

### En Netlify
1. Ve a **Site settings** → **Build & deploy** → **Environment**
2. Agrega variables:
   - `FIREBASE_API_KEY`
   - `FIREBASE_AUTH_DOMAIN`
   - `FIREBASE_PROJECT_ID`

### En el código
```javascript
const firebaseConfig = {
  apiKey: process.env.FIREBASE_API_KEY,
  authDomain: process.env.FIREBASE_AUTH_DOMAIN,
  projectId: process.env.FIREBASE_PROJECT_ID,
  // ...
};
```

---

## Optimización antes de publicar

### 1. Minificar CSS y JavaScript
```bash
npm install -g terser
terser script.js -c -m -o script.min.js
```

### 2. Optimizar imágenes
- Usar TinyPNG o ImageOptim
- Máximo 100KB por imagen

### 3. Verificar performance
- Google PageSpeed Insights
- GTmetrix
- WebPageTest

### 4. SEO básico
```html
<meta name="description" content="Preparación ICFES con Aves del Saber 500">
<meta name="keywords" content="ICFES, Simulacro, Educación">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

---

## HTTPS y Seguridad

✅ **Netlify**: HTTPS automático
✅ **GitHub Pages**: HTTPS automático
✅ **Vercel**: HTTPS automático
✅ **Hosting propio**: Usar Let's Encrypt (gratis)

---

## Monitoreo después de publicar

### Google Analytics
```html
<!-- Agregar antes de </head> -->
<script async src="https://www.googletagmanager.com/gtag/js?id=GA_ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'GA_ID');
</script>
```

### Errores con Sentry
```html
<script src="https://cdn.ravenjs.com/3.26.4/raven.min.js"></script>
<script>
  Raven.config('https://YOUR_KEY@sentry.io/YOUR_PROJECT').install();
</script>
```

---

## Backup y Control de Versiones

### GitHub
```bash
git status
git add .
git commit -m "Descripción de cambios"
git push origin main
```

### Automatizar backups
- Usar GitHub Gists para datos
- Exportar JSON regularmente
- Mantener versiones locales

---

## Presupuesto Mensual

| Servicio | Costo | Notas |
|----------|-------|-------|
| Dominio | ~$1/mes | De registrador |
| Hosting (Netlify) | GRATIS | Recomendado |
| Hosting (SiteGround) | ~$3/mes | Con email |
| Firebase | $0-50 | Según uso |
| **Total** | **~$4/mes** | Muy accesible |

---

## Checklist de Publicación

- [ ] Cambiar contraseña admin
- [ ] Probar todas las funciones
- [ ] Conectar a Firebase (opcional)
- [ ] Configurar dominio
- [ ] Habilitar HTTPS
- [ ] Agregar Analytics
- [ ] Hacer backup
- [ ] Informar a estudiantes

---

## Pasos Rápidos (3 minutos)

### Opción Más Fácil: Netlify
1. Conecta GitHub (crea repo primero)
2. Selecciona el repositorio en Netlify
3. ¡Listo! Tu sitio está en vivo

### Con dominio personalizado
1. Registra dominio en Namecheap
2. En Netlify, agrega el dominio
3. Sigue instrucciones de DNS
4. Espera 5-30 minutos

---

## Soporte y Ayuda

- **Netlify Docs**: https://docs.netlify.com
- **GitHub Pages**: https://pages.github.com
- **Vercel Docs**: https://vercel.com/docs
- **ADS WhatsApp**: +57 321 879 0121

---

## Siguientes Pasos después de Publicar

1. ✅ Monitorear con Analytics
2. ✅ Recopilar feedback de estudiantes
3. ✅ Agregar más funcionalidades
4. ✅ Conectar a Firebase para persistencia
5. ✅ Escalar a certificados descargables
6. ✅ Integrar pagos (para premium)

**¡Tu plataforma ADS está lista para conquistar! 🦅✨**
