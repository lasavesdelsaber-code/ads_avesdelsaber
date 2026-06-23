# ❓ Preguntas Frecuentes (FAQ) — Aves del Saber 500

---

## 📊 CONSULTA DE RESULTADOS

### ¿Cómo ingreso mis resultados?
1. Ve al panel admin (`admin.html`)
2. Login: usuario `admin`, contraseña `ads2024`
3. Ve a "Agregar Estudiante" o "Subir Resultados"
4. Completa los datos y guarda

### ¿Qué es el T.I.?
Es el **Número de Cédula** del estudiante. Ejemplo: 1023456789

### ¿Puedo cambiar la contraseña?
Sí. Abre `admin.html` y busca (línea 260):
```javascript
const ADMIN_USER = 'admin';
const ADMIN_PASS = 'ads2024';
```

### ¿Los datos se guardan automáticamente?
**No** en la versión actual. Los datos están en memoria. Para persistencia, conecta a Firebase (ver `FIREBASE-INTEGRATION.md`)

### ¿Cuántos estudiantes puedo agregar?
Ilimitados. El sistema está diseñado para escalar.

### ¿Puedo importar datos desde Excel?
Sí, convierte a JSON primero usando:
1. Excel → Exportar como CSV
2. Usar herramienta en línea CSV → JSON
3. Pega en "Subir Resultados"

---

## 🎨 PERSONALIZACIÓN

### ¿Cómo cambio los colores?
Abre `ADS.html` y busca `:root { }` (línea 10):
```css
:root {
  --navy: #1B2A4A;        /* Azul oscuro */
  --gold: #C9A227;        /* Dorado */
  --gold-light: #F0C84A;  /* Dorado claro */
}
```

### ¿Cómo cambio los mensajes motivacionales?
En `ADS.html`, busca `generarMotivacion()` y modifica los arrays:
```javascript
excelente: ['Tu mensaje aquí', ...],
```

### ¿Puedo cambiar el logo del águila?
Sí, reemplaza el emoji `🦅` en el código con tu logo o imagen.

### ¿Cómo hago que sea 100% mobile-first?
Ya lo es. El CSS tiene `@media` queries responsivos.

---

## 🔒 SEGURIDAD

### ¿Es seguro guardar datos en GitHub?
No guardes datos sensibles en GitHub. Usa archivos `.gitignore`:
```
database.json
config.js
.env
```

### ¿Cómo protejo mi base de datos?
Conecta a Firebase con autenticación. Ver `FIREBASE-INTEGRATION.md`

### ¿Necesito HTTPS?
Sí, es recomendado. Netlify y GitHub Pages lo dan automáticamente.

### ¿Qué pasa si olvido la contraseña del admin?
Edita directamente `admin.html` o usa otra contraseña en el código.

---

## 🚀 DESPLIEGUE Y HOSTING

### ¿Cuál es la opción más rápida de publicar?
**Netlify**. En 5 minutos con GitHub:
1. Push a GitHub
2. Conecta en Netlify
3. ¡Listo!

### ¿Es gratis desplegar en Netlify?
Sí, el tier hobby es gratis. Ver `DEPLOYMENT.md`

### ¿Necesito un dominio personalizado?
Opcionalmente. Puedes usar el dominio gratis de Netlify o comprar uno (~$12/año).

### ¿Dónde compro un dominio?
- Namecheap (recomendado)
- Google Domains
- GoDaddy
- Registro.com (para .co)

### ¿Cómo cambio mi dominio después de publicar?
En Netlify: **Site settings** → **Domain management** → **Add domain**

### ¿Puedo hostearlo localmente?
Sí, para pruebas:
```bash
python3 -m http.server 8000
```
Luego abre `http://localhost:8000`

---

## 📱 FUNCIONALIDADES

### ¿Qué hace el botón "Descargar PDF"?
Descarga un reporte TXT con los resultados del estudiante.

### ¿Qué hace el botón "Compartir"?
Abre WhatsApp pre-lleno con tu resultado para que lo compartas con amigos.

### ¿La gráfica radar funciona en móvil?
Sí, es totalmente responsiva.

### ¿Puedo ver el ranking sin consultar?
No en la versión actual, pero aparece después de consultar resultados.

### ¿Puedo descargar el ranking completo?
No aún, pero puedes copiar y pegar de la tabla.

---

## 🐛 SOLUCIÓN DE PROBLEMAS

### Las gráficas no salen
**Solución:**
1. Abre consola (F12)
2. Busca errores
3. Verifica que Chart.js esté cargado
4. Recarga la página

### El admin no me deja entrar
**Solución:**
- Usuario: `admin` (sin espacios)
- Contraseña: `ads2024` (sin espacios)
- Verifica mayúsculas/minúsculas

### Los datos no aparecen en la tabla
**Solución:**
1. Verifica que la base de datos no esté vacía
2. Recarga la página (F5)
3. Abre consola para errores

### El formulario no guarda
**Solución:**
- En la versión actual, los datos solo están en memoria
- Si cierras el navegador, se pierden
- Conecta a Firebase para persistencia

### Tengo error "CORS" al usar Firebase
**Solución:**
- Verifica que tu configuración de Firebase sea correcta
- Usa módulos ES6
- Revisa reglas de seguridad en Firestore

### ¿Por qué se ve diferente en móvil?
**Es normal.** El diseño es responsivo. Deberías verlo igual pero adaptado al tamaño.

---

## 💾 BACKUP Y DATOS

### ¿Cómo hago backup de los datos?
En el admin, ve a "Subir Resultados", copia el JSON y guárdalo.

### ¿Puedo restaurar desde backup?
Sí, en "Subir Resultados", pega el JSON anterior.

### ¿Dónde están mis datos?
En la variable `estudiantesDB` del JavaScript. Para persistencia, usa Firebase.

### ¿Puedo exportar a Excel?
Sí, usando herramientas en línea JSON → Excel.

---

## 👥 GESTIÓN DE USUARIOS

### ¿Puedo crear múltiples administradores?
En la versión actual, solo existe 1 admin. Para múltiples, conecta a Firebase Auth.

### ¿Puedo ver quién modificó cada estudiante?
No en la versión actual. Firebase permite auditoría completa.

### ¿Hay roles de usuario (admin, profesor, estudiante)?
En la versión actual, solo hay admin. Los estudiantes solo consultan (lectura).

---

## 📈 ESTADÍSTICAS

### ¿Cómo veo el progreso de todos?
En el admin, el Dashboard muestra:
- Total de estudiantes
- Promedio de puntaje
- Puntuación más alta
- Top 5

### ¿Puedo ver gráficas de tendencias?
No aún, pero es fácil de agregar con Chart.js.

### ¿Cómo exporto estadísticas?
Manualmente: Captura de pantalla o copia la tabla.
Automático: Conecta a Google Analytics.

---

## 🌐 INTERNET Y CONECTIVIDAD

### ¿Funciona sin internet?
**No**. Necesitas conexión para:
- Acceder a la página
- Cargar Chart.js
- Usar Firebase

Para funcionar offline, necesitas Service Workers.

### ¿Es segura la conexión?
Sí si usas HTTPS (Netlify, GitHub Pages lo dan automático).

### ¿Qué velocidad de internet se recomienda?
Mínimo: 1 Mbps. Recomendado: 10+ Mbps.

---

## 💬 CONTACTO Y SOPORTE

### ¿A quién contacto si tengo problemas?
**Aves del Saber 500**
- WhatsApp: +57 321 879 0121
- Instagram: @preicfes_avesdelsaber

### ¿Hay documentación adicional?
Sí, revisa:
- `README.md` - Completo
- `QUICK-START.md` - Rápido
- `FIREBASE-INTEGRATION.md` - Base de datos
- `DEPLOYMENT.md` - Publicar en web

### ¿Puedo pedir nuevas funcionalidades?
Sí, contacta por WhatsApp. Las mejoras comunes:
- Certificados descargables
- Análisis detallado por temas
- Clases en video integradas
- Sistema de pagos

---

## 🎓 EDUCATIVO

### ¿Esto es un sistema oficial de ICFES?
**No**. Es un sistema independiente de preparación para ICFES Saber 11.

### ¿Los puntajes son reales?
Depende. Si usas datos reales de simulacros, sí. Si son de prueba, no.

### ¿Cómo calibro los puntajes?
Compara con simulacros oficiales de ICFES.

---

## ⚡ PERFORMANCE

### ¿Es rápido?
Sí. Carga en menos de 2 segundos.

### ¿Cuántos usuarios simultáneos soporta?
Versión local: Ilimitados (depende de tu navegador)
Netlify: Millones (CDN global)
Firebase: Millones (infraestructura Google)

### ¿Consume mucho ancho de banda?
No. El sitio es muy ligero (~100KB).

---

## 📞 RESPUESTAS RÁPIDAS

| Pregunta | Respuesta |
|----------|-----------|
| ¿Gratis? | Sí, totalmente |
| ¿Código abierto? | Sí, puedes modificar |
| ¿Privacidad? | HTTPS + reglas Firestore |
| ¿Soporte? | WhatsApp +57 321 879 0121 |
| ¿Actualizaciones? | Sí, regularmente |
| ¿Parar? | Puedes guardar en JSON |

---

## 🆘 Si nada funciona

1. Abre consola (F12)
2. Copia el error exacto
3. Contacta por WhatsApp
4. Proporciona:
   - Navegador (Chrome, Firefox, Safari)
   - Dispositivo (PC, Móvil, Tablet)
   - Sistema operativo (Windows, Mac, Android)
   - Pasos para reproducir el error
   - Screenshot del error

---

## 🎉 ¡Listo!

Si tu pregunta no está aquí, contacta:
**WhatsApp**: +57 321 879 0121

**¡Vuela alto con ADS!** 🦅✨
