# 🚀 DEPLOY EN 5 MINUTOS (sin tecnicismos)

## LO QUE NECESITAS
- Una cuenta **GitHub** (gratis) 
- Una cuenta **Vercel** (gratis)
- Los 5 archivos de la carpeta `hc-app`

---

## PASO 1: Crear repositorio en GitHub

1. Ve a **github.com**
2. Haz login o crea cuenta (es gratis)
3. Arriba a la derecha: **+** → **New repository**
4. Nombre: `historia-clinica-consultorio`
5. Marca "Add a README file"
6. Click **Create repository**

---

## PASO 2: Subir los archivos

1. Entra al repositorio que acabas de crear
2. Click en botón **Add file** (arriba a la derecha)
3. Click en **Upload files**
4. Arrastra estos 5 archivos:
   - `package.json`
   - `vite.config.js`
   - `index.html`
   - `src/App.jsx`
   - `src/main.jsx`
5. Click **Commit changes**

---

## PASO 3: Deploy en Vercel

1. Ve a **vercel.com**
2. Click **Sign Up** → **Continue with GitHub**
3. Autoriza Vercel
4. Click **New Project** (o Dashboard → Add New → Project)
5. Busca tu repositorio `historia-clinica-consultorio`
6. Click **Import**
7. **Deploy!**

**Listo.** En 1-2 minutos te da un link como:
```
https://historia-clinica-consultorio.vercel.app
```

---

## PASO 4: iPad Setup

Tu cliente (médico) hace esto **UNA SOLA VEZ**:

1. Abre Safari en el iPad
2. Va a: `https://historia-clinica-consultorio.vercel.app`
3. Toca **Compartir** (ícono cuadrado con flecha)
4. Toca **Agregar a pantalla de inicio**
5. Le da un nombre (ej: "Historia Clínica")
6. Toca **Añadir**

✅ **Ahora tiene un ícono en el home del iPad que funciona como app nativa**

---

## ✅ YA ESTÁ

El médico toca el ícono → abre la app → llena historias → se guardan automáticamente en el iPad.

Sin internet → funciona igual.
Sin Claude → funciona igual.
Sin descargar nada → funciona igual.

---

## 📱 Cómo funciona

- **Los datos viven en el iPad** — no se pierden
- **Botones grandes** — fácil para tocar
- **12 secciones** completas según Norma 2023
- **Preguntas condicionales** — campos que aparecen/desaparecen según respuestas
- **Dashboard** — ve todos los pacientes de un vistazo
- **Vista detalle** — consulta cualquier historia guardada

---

## ❓ Si algo no funciona

**Error al subir archivos a GitHub:**
- Descarga la carpeta `src` como una subcarpeta (no disuelvas los archivos)

**Vercel dice "Build error":**
- Verifica que todos los archivos estén (especialmente `package.json`)
- Limpia cache (Ctrl+Shift+Del) e intenta de nuevo

**iPad no abre la app:**
- Verifica la URL es correcta
- Prueba en Safari (no en Chrome)
- Prueba en incógnito

---

## 💡 PRO TIP

Comparte la URL con tu cliente:
```
Abre en Safari → https://historia-clinica-consultorio.vercel.app
Luego: Compartir → Agregar a pantalla de inicio
```

**Eso es todo.** No necesita hacer nada más.

---

**Fecha de creación:** 2026
**Versión:** 1.0
