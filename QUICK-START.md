# 🚀 Guía Rápida — Aves del Saber 500

## Paso 1: Abrir la página principal

Abre `ADS.html` en tu navegador. Verás la nueva sección **"CONSULTA TUS RESULTADOS"** antes de Simulacros.

---

## Paso 2: Consultar resultados (Estudiante)

1. Dirígete a la sección "Consultar Resultados"
2. Ingresa un número de T.I. (ejemplo: `1023456789`)
3. Presiona el botón "Consultar"
4. Verás:
   - Tu nombre y puntaje global
   - Desempeño por cada materia
   - Gráfica radar
   - Tu posición en el ranking
   - Mensaje motivacional

### T.I. de Prueba

```
1023456789 → Juan Pérez (420 pts - #1)
1087654321 → María López (413 pts - #2)
1098765432 → Carlos Ruiz (408 pts - #3)
```

---

## Paso 3: Acceder al Panel Admin

1. Abre `admin.html`
2. Login:
   - **Usuario**: `admin`
   - **Contraseña**: `ads2024`

---

## Paso 4: Gestionar Estudiantes (Admin)

### Dashboard
- Ve estadísticas y top 5 automáticamente

### Agregar Estudiante
1. Ve a "Agregar Estudiante"
2. Completa:
   - Nombre
   - T.I.
   - Puntajes (0-100) en cada materia
3. Presiona "Guardar Estudiante"

### Editar Estudiante
1. Ve a "Editar Estudiante"
2. Ingresa el T.I.
3. Modifica los campos
4. Presiona "Guardar Cambios"

### Eliminar Estudiante
1. En "Editar Estudiante", busca por T.I.
2. Presiona "Eliminar Estudiante"
3. Confirma

### Importar en Lote (JSON)
1. Ve a "Subir Resultados"
2. Pega tu JSON (ver `database-example.json`)
3. Presiona "Subir Datos"

---

## 📊 Ejemplo de Consulta

### Entrada
```
T.I.: 1023456789
```

### Salida
```
Nombre: Juan Pérez
Puntaje Global: 420
Posición: #1
Percentil: 98%

Matemáticas: 85/100 ██████████
Lectura: 78/100 ████████░
Sociales: 90/100 ██████████
Ciencias: 80/100 █████████░
Inglés: 88/100 ██████████

[Gráfica Radar interactiva]
[Top 5 Ranking con medallas]
```

---

## 🎯 Funcionalidades Clave

### Para Estudiantes ✅
- ✅ Buscar por T.I.
- ✅ Ver puntaje global
- ✅ Ver desempeño por materia
- ✅ Ver gráfica comparativa
- ✅ Ver ranking
- ✅ Descargar reporte PDF
- ✅ Compartir por WhatsApp

### Para Administradores ✅
- ✅ Login seguro
- ✅ Ver dashboard con estadísticas
- ✅ Agregar estudiante
- ✅ Editar datos
- ✅ Eliminar estudiante
- ✅ Importar datos en JSON
- ✅ Ver lista completa

---

## 🎨 Colores y Estados

### Estados del Desempeño
```
🟢 Excelente     (≥ 400 puntos)
🟡 Bueno         (350-399 puntos)
🔴 Debe mejorar  (< 350 puntos)
```

### Colores por Materia
```
Matemáticas      🔵 Azul
Lectura Crítica  🟣 Púrpura
Sociales         🌸 Rosa
Ciencias         🟢 Verde
Inglés           🟠 Naranja
```

---

## 🔧 Personalización Rápida

### Cambiar Credenciales Admin
Abre `admin.html` y busca (línea ~260):
```javascript
const ADMIN_USER = 'admin';
const ADMIN_PASS = 'ads2024';
```

Cambia a tus valores.

### Cambiar Mensajes de Motivación
Abre `ADS.html` y busca la función `generarMotivacion()` (línea ~1450).

Modifica los array:
```javascript
excelente: ['Tu mensaje aquí', ...],
bueno: ['Tu mensaje aquí', ...],
mejorar: ['Tu mensaje aquí', ...]
```

---

## 📱 Compatibilidad

✅ Desktop (1920px)
✅ Tablet (768px)
✅ Móvil (320px)

Totalmente responsivo en todos los dispositivos.

---

## ⚡ Tips Prácticos

1. **Probar rápido**: Usa los T.I. de ejemplo
2. **Admin**: Cambia contraseña antes de producción
3. **Backup**: Exporta datos en JSON regularmente
4. **Móvil**: El diseño se adapta automáticamente
5. **WhatsApp**: Los estudiantes pueden compartir directamente

---

## 🐛 Problemas Comunes

### "No se encuentra el resultado"
→ Verifica que el T.I. esté correcto (sin espacios)

### "Las gráficas no salen"
→ Abre consola (F12) y busca errores de Chart.js

### "La contraseña no funciona"
→ Verifica que sea `admin` / `ads2024` (en la demo)

### "Los cambios no se guardan"
→ Los datos están en memoria. Conectar a base de datos para persistencia.

---

## 📞 Soporte

¿Preguntas? Contacta:
- **WhatsApp**: +57 321 879 0121
- **Instagram**: @preicfes_avesdelsaber

---

## ¿Qué Sigue?

- [ ] Conectar a Firebase para persistencia
- [ ] Agregar exportación a Excel
- [ ] Notificaciones por email
- [ ] Análisis de tendencias
- [ ] Certificados descargables

**¡Vuela alto con ADS!** 🦅✨
