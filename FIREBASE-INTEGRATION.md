# 🔥 Integración con Firebase — Aves del Saber 500

> Este archivo te guía para conectar tu sistema a Firebase Firestore en lugar de usar datos en memoria.

---

## 📋 Requisitos

1. Cuenta de Google
2. Proyecto en Firebase Console
3. Básicos de JavaScript

---

## Paso 1: Crear Proyecto en Firebase

1. Ve a [Firebase Console](https://console.firebase.google.com/)
2. Haz clic en "Crear proyecto"
3. Nombra tu proyecto: `aves-del-saber`
4. Selecciona región (Colombia)
5. Finaliza la creación

---

## Paso 2: Obtener Credenciales

1. En Firebase Console, ve a **Configuración del Proyecto** (⚙️)
2. Ve a la pestaña **Tu apps**
3. Haz clic en **Web** (`</>`)
4. Sigue los pasos y copia tu configuración:

```javascript
const firebaseConfig = {
  apiKey: "TU_API_KEY",
  authDomain: "tu-proyecto.firebaseapp.com",
  projectId: "tu-proyecto-123",
  storageBucket: "tu-proyecto.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
};
```

---

## Paso 3: Actualizar ADS.html

### Agregar script de Firebase (antes de `</head>`):

```html
<!-- Firebase -->
<script src="https://www.gstatic.com/firebasejs/10.7.0/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.7.0/firebase-firestore.js"></script>
```

### Agregar inicialización (después de `<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>`):

```javascript
// FIREBASE CONFIG
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.0/firebase-app.js";
import { getFirestore, collection, query, where, getDocs, orderBy } from "https://www.gstatic.com/firebasejs/10.7.0/firebase-firestore.js";

const firebaseConfig = {
  apiKey: "TU_API_KEY",
  authDomain: "tu-proyecto.firebaseapp.com",
  projectId: "tu-proyecto-123",
  storageBucket: "tu-proyecto.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
};

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);
```

---

## Paso 4: Reemplazar Función `consultarEstudiante()`

### Versión Original (en memoria):
```javascript
function consultarEstudiante() {
  const ti = document.getElementById('tiInput').value.trim();
  const estudiante = estudiantesDB.find(e => e.ti === ti);
  if (!estudiante) alert('No encontrado');
  mostrarResultados(estudiante);
}
```

### Versión Firebase:
```javascript
async function consultarEstudiante() {
  const ti = document.getElementById('tiInput').value.trim();
  
  if (!ti) {
    alert('Por favor ingresa tu número de T.I.');
    return;
  }
  
  try {
    const q = query(
      collection(db, 'estudiantes'),
      where('ti', '==', ti)
    );
    
    const querySnapshot = await getDocs(q);
    
    if (querySnapshot.empty) {
      alert('No se encontraron resultados para el T.I.: ' + ti);
      return;
    }
    
    const estudiante = querySnapshot.docs[0].data();
    mostrarResultados(estudiante);
  } catch (error) {
    console.error('Error:', error);
    alert('Error al consultar los resultados');
  }
}
```

---

## Paso 5: Reemplazar Función `obtenerRanking()`

### Versión Firebase:
```javascript
async function obtenerRanking() {
  try {
    const q = query(
      collection(db, 'estudiantes'),
      orderBy('total', 'desc')
    );
    
    const querySnapshot = await getDocs(q);
    
    return querySnapshot.docs.map((doc, idx) => ({
      ...doc.data(),
      id: doc.id,
      posicion: idx + 1
    }));
  } catch (error) {
    console.error('Error:', error);
    return [];
  }
}
```

---

## Paso 6: Crear Colección en Firestore

En Firebase Console:

1. Ve a **Firestore Database**
2. Haz clic en **Crear base de datos**
3. Modo: **Comenzar en modo de prueba** (luego cambiar reglas)
4. Región: Tu continente más cercano
5. Haz clic en **Crear colección** llamada `estudiantes`
6. Agrega documentos con esta estructura:

```
Documento ID: 1023456789
{
  "ti": "1023456789",
  "nombre": "Juan Pérez",
  "matematicas": 85,
  "lectura": 78,
  "sociales": 90,
  "ciencias": 80,
  "ingles": 88,
  "total": 421
}
```

---

## Paso 7: Actualizar admin.html

### Agregar Firebase al panel admin:

Reemplaza la sección de `// DATOS`:

```javascript
// FIREBASE
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.0/firebase-app.js";
import { 
  getFirestore, 
  collection, 
  addDoc, 
  updateDoc, 
  deleteDoc, 
  getDocs,
  doc,
  query,
  where,
  orderBy 
} from "https://www.gstatic.com/firebasejs/10.7.0/firebase-firestore.js";

const firebaseConfig = {
  apiKey: "TU_API_KEY",
  authDomain: "tu-proyecto.firebaseapp.com",
  projectId: "tu-proyecto-123",
  storageBucket: "tu-proyecto.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
};

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);
```

### Reemplazar `agregarEstudiante()`:

```javascript
async function agregarEstudiante() {
  const nombre = document.getElementById('addNombre').value.trim();
  const ti = document.getElementById('addTI').value.trim();
  const math = parseInt(document.getElementById('addMath').value) || 0;
  const reading = parseInt(document.getElementById('addReading').value) || 0;
  const social = parseInt(document.getElementById('addSocial').value) || 0;
  const science = parseInt(document.getElementById('addScience').value) || 0;
  const english = parseInt(document.getElementById('addEnglish').value) || 0;
  
  if (!nombre || !ti) {
    mostrarAlerta('addAlert', 'error', 'Complete todos los campos');
    return;
  }
  
  try {
    const total = math + reading + social + science + english;
    
    await addDoc(collection(db, 'estudiantes'), {
      ti,
      nombre,
      matematicas: math,
      lectura: reading,
      sociales: social,
      ciencias: science,
      ingles: english,
      total: total
    });
    
    mostrarAlerta('addAlert', 'success', 'Estudiante agregado correctamente');
    limpiarFormulario();
    await cargarDashboard();
    await llenarTablaEstudiantes();
  } catch (error) {
    mostrarAlerta('addAlert', 'error', 'Error: ' + error.message);
  }
}
```

---

## Paso 8: Configurar Reglas de Seguridad

En Firebase Console → **Firestore → Reglas**:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Públicamente legible para estudiantes
    match /estudiantes/{document=**} {
      allow read;
    }
    
    // Solo admin puede escribir
    match /estudiantes/{document=**} {
      allow write: if request.auth.uid != null;
    }
  }
}
```

---

## Paso 9: Agregar Autenticación (Opcional)

Para mayor seguridad en el admin, agregar Firebase Auth:

```javascript
import { getAuth, signInWithEmailAndPassword, signOut } from "https://www.gstatic.com/firebasejs/10.7.0/firebase-auth.js";

const auth = getAuth(app);

async function loginFirebase(email, password) {
  try {
    await signInWithEmailAndPassword(auth, email, password);
    document.getElementById('loginView').style.display = 'none';
    document.getElementById('adminView').style.display = 'block';
  } catch (error) {
    alert('Error: ' + error.message);
  }
}
```

---

## Referencia Rápida de Funciones Firestore

```javascript
// LEER
const q = query(collection(db, 'estudiantes'), where('ti', '==', '123'));
const docs = await getDocs(q);

// CREAR
await addDoc(collection(db, 'estudiantes'), { nombre: 'Juan', ti: '123' });

// ACTUALIZAR
await updateDoc(doc(db, 'estudiantes', 'docId'), { nombre: 'Juan' });

// ELIMINAR
await deleteDoc(doc(db, 'estudiantes', 'docId'));

// ORDENAR
const q = query(collection(db, 'estudiantes'), orderBy('total', 'desc'));
```

---

## Ventajas de Firebase

✅ Base de datos en la nube
✅ Sin servidor que mantener
✅ Escalable automáticamente
✅ Seguridad incorporada
✅ Analytics gratis
✅ Backups automáticos

---

## Próximos Pasos

1. ✅ Conectar ADS.html a Firebase
2. ✅ Conectar admin.html a Firebase
3. ✅ Configurar autenticación
4. ✅ Agregar más funcionalidades (reportes, gráficas)
5. ✅ Publicar en un servidor

---

## Troubleshooting

### Error: "módulos de importación no definidos"
→ Usar módulos ES6 o cargar Firebase desde CDN en línea

### Error: "Permiso denegado en lectura"
→ Revisar reglas de seguridad en Firebase Console

### Los datos no se sincronizan
→ Verificar conexión internet y verificar que Firestore esté habilitado

### Performance lento
→ Agregar índices en Firestore para consultas frecuentes

---

## Contacto y Soporte

¿Necesitas ayuda con la integración?

- **Firebase Docs**: https://firebase.google.com/docs
- **Community**: Stack Overflow tag `firebase`
- **ADS WhatsApp**: +57 321 879 0121

**¡Vuela alto con ADS!** 🦅✨
