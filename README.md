# 🦅 Aves del Saber 500 — Sistema de Resultados

## 📋 Descripción

Sistema completo de consulta de resultados y ranking para ICFES Saber 11. Incluye:

- ✅ Consulta de resultados por T.I.
- ✅ Gráficas radar interactivas
- ✅ Ranking y tabla de posiciones
- ✅ Panel administrador
- ✅ Descarga de reportes PDF
- ✅ Compartir resultados por WhatsApp

---

## 🚀 Características

### Para Estudiantes

1. **Consultar Resultados**
   - Busca por número de T.I.
   - Ve tu puntaje global y por materia
   - Visualiza tu posición en el ranking
   - Recibe mensajes motivacionales personalizados

2. **Detalles de Desempeño**
   - Puntaje por cada una de las 5 áreas ICFES
   - Barras de progreso con colores según desempeño
   - Etiquetas: Excelente, Muy Bien, Bien, Debe mejorar

3. **Gráfica Radar**
   - Comparación visual de tus 5 áreas
   - Escala de 0-100 en cada materia
   - Hover interactivo con detalles

4. **Ranking Global**
   - Top 5 estudiantes con medallas
   - Tabla completa de posiciones
   - Scroll en dispositivos móviles

5. **Descargas y Compartir**
   - Descargar reporte completo como TXT
   - Compartir resultado por WhatsApp

### Para Administradores

1. **Dashboard**
   - Estadísticas: Total de estudiantes, promedio, máximo puntaje
   - Top 5 ranking

2. **Gestión de Estudiantes**
   - Agregar nuevo estudiante
   - Editar datos existentes
   - Eliminar estudiante

3. **Carga de Resultados**
   - Importar múltiples estudiantes en JSON
   - Actualizar puntajes en lote

---

## 📁 Archivos

```
aves-del-saber/
├── ADS.html                    # Página principal con nueva sección
├── admin.html                  # Panel administrador
├── README.md                   # Este archivo
└── database-example.json       # Ejemplo de formato de datos
```

---

## 🔐 Acceso al Panel Administrador

**URL**: `admin.html`

**Credenciales de Demo**:
- Usuario: `admin`
- Contraseña: `ads2024`

> ⚠️ Cambia estas credenciales en el código para producción

---

## 💾 Base de Datos

Los datos se almacenan en la variable `estudiantesDB` en JavaScript. Para producción, conectar a Firebase o backend.

### Estructura de un Estudiante

```json
{
  "ti": "1023456789",
  "nombre": "Juan Pérez",
  "matematicas": 85,
  "lectura": 78,
  "sociales": 90,
  "ciencias": 80,
  "ingles": 88
}
```

### Importar Datos en Lote

En el panel admin, tab "Subir Resultados", pega un JSON como este:

```json
[
  {
    "ti": "1023456789",
    "nombre": "Juan Pérez",
    "matematicas": 85,
    "lectura": 78,
    "sociales": 90,
    "ciencias": 80,
    "ingles": 88
  },
  {
    "ti": "1087654321",
    "nombre": "María López",
    "matematicas": 82,
    "lectura": 85,
    "sociales": 88,
    "ciencias": 87,
    "ingles": 81
  }
]
```

---

## 🎨 Personalización

### Colores de Materias

- **Matemáticas**: `#3B82F6` (Azul)
- **Lectura Crítica**: `#8B5CF6` (Púrpura)
- **Sociales**: `#EC4899` (Rosa)
- **Ciencias Naturales**: `#10B981` (Verde)
- **Inglés**: `#F59E0B` (Naranja)

### Estados

- **Excelente** (≥400 pts): 🟢 Verde
- **Bueno** (350-399 pts): 🟡 Amarillo
- **Debe mejorar** (<350 pts): 🔴 Rojo

---

## 🔄 Flujo de Uso

### Estudiante

1. Ve a la sección "Consultar Resultados"
2. Ingresa tu número de T.I.
3. Presiona "Consultar"
4. Ver resultados, gráfica y ranking
5. Opcionalmente: Descargar PDF o Compartir

### Administrador

1. Entra a `admin.html`
2. Login con credenciales
3. Dashboard: Ver estadísticas
4. Agregar estudiante: Completa formulario
5. Editar: Busca por T.I., modifica datos
6. Subir resultados: Pega JSON de múltiples estudiantes
7. Ver listado completo de estudiantes

---

## 🚨 Funciones JavaScript Principales

```javascript
// Consultar estudiante por T.I.
consultarEstudiante()

// Mostrar resultados con gráfica
mostrarResultados(estudiante)

// Crear gráfica radar
crearGrafica(estudiante)

// Obtener ranking ordenado
obtenerRanking()

// Generar mensaje motivacional
generarMotivacion(total)

// Descargar PDF
downloadPDF()

// Compartir por WhatsApp
shareResult()

// Panel admin: Agregar estudiante
agregarEstudiante()

// Panel admin: Guardar cambios
guardarCambios()

// Panel admin: Importar JSON
subirJSON()
```

---

## 📱 Responsivo

Totalmente optimizado para:
- ✅ Desktop (1920px+)
- ✅ Tablet (768px+)
- ✅ Móvil (320px+)

---

## 🔗 Integraciones

### Chart.js
Para gráficas radar. CDN incluido:
```html
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
```

### Font Awesome
Iconos. CDN incluido:
```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
```

### Google Fonts
Tipografías (Bebas Neue, Nunito). CDN incluido.

---

## 🔒 Seguridad (Producción)

Para usar en producción:

1. **Cambiar credenciales del admin**:
   - Editar `ADMIN_USER` y `ADMIN_PASS` en `admin.html`
   - O mejor: Usar autenticación con backend/Firebase

2. **Conectar a base de datos real**:
   - Firebase Firestore
   - Base de datos relacional (MySQL, PostgreSQL)
   - Backend propio (Node.js, Python, etc.)

3. **HTTPS**: Siempre usar conexiones seguras

4. **Validar datos**: En servidor (nunca confiar solo en frontend)

5. **Hash de contraseñas**: No guardar en texto plano

---

## 🐛 Troubleshooting

### Las gráficas no aparecen
- Verificar que Chart.js esté cargado
- Abrir consola (F12) y buscar errores

### No se guardan cambios en el admin
- Los datos están solo en memoria
- Conectar a base de datos para persistencia

### El ranking no se ordena bien
- Verificar que todos los puntajes sean números
- Revisar que la función `calcularTotal()` funcione

---

## 📞 Contacto y Soporte

- **WhatsApp**: +57 321 879 0121
- **Instagram**: @preicfes_avesdelsaber
- **Email**: Contacto disponible en redes sociales

---

## 📄 Licencia

Desarrollado para Aves del Saber 500 🦅

---

## 📝 Notas de Desarrollo

- Estudiantes de demo incluidos en la base de datos
- Sistema listo para expandir con más funcionalidades
- Código comentado y modular
- Fácil de personalizar colores y mensajes

¡Vuela alto con ADS! 🦅✨
