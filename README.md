# Historia Clínica Digital - Deployment en Vercel

## ⚡ Setup Rápido (5 minutos)

### Paso 1: Descarga la carpeta `/hc-app`
Descarga todos estos archivos en una carpeta llamada `hc-app`:
- `package.json`
- `vite.config.js`
- `index.html`
- `src/App.jsx`
- `src/main.jsx`

### Paso 2: Crea cuenta Vercel (gratis)
1. Ve a **vercel.com**
2. Haz click en "Sign Up"
3. Elige "Continue with GitHub" (o Google/GitLab)
4. Autoriza Vercel

### Paso 3: Deploy automático
Hay 2 opciones:

#### Opción A: Usando GitHub (la más fácil)
1. Ve a **github.com** y crea una cuenta (si no tienes)
2. Crea un nuevo repositorio llamado `historia-clinica`
3. Sube los archivos de `hc-app` al repositorio
4. Vuelve a **vercel.com** → "New Project"
5. Selecciona tu repositorio `historia-clinica`
6. Haz click en "Deploy"
7. ¡Listo! Vercel te da un URL en 1 minuto

#### Opción B: Sin GitHub (drag & drop)
1. Descarga/instala **Node.js** (nodejs.org)
2. Abre terminal en la carpeta `hc-app`
3. Corre:
   ```bash
   npm install
   npm run build
   ```
4. Ve a **vercel.com** → "Upload"
5. Sube la carpeta `dist` que se creó
6. ¡Listo!

---

## 📱 Cómo usa tu cliente en iPad

1. Abre Safari
2. Entra a la URL que te da Vercel (ej: `historia-clinica-nombre.vercel.app`)
3. Toca **Compartir** → **Agregar a pantalla de inicio**
4. Aparece como app nativa en el home del iPad
5. Los datos se guardan automáticamente en el iPad

---

## 📊 Datos & Almacenamiento

- **Dónde se guardan:** En el iPad (localStorage)
- **¿Necesita internet?** No después de la primera carga
- **¿Se pierden los datos?** No, están en el iPad
- **¿Acceso desde múltiples dispositivos?** Si necesitas esto, dime y agrego base de datos

---

## 🔧 Si necesitas cambios

Edita `src/App.jsx`:
- **Cambiar colores:** Busca `const TEAL = "#0D5C63"` arriba del archivo
- **Cambiar preguntas:** Busca la sección que quieres editar (S1, S2, etc.)
- **Agregar campos:** Copia el patrón de Input / Textarea / ToggleGroup

Después de cambios:
```bash
npm run build
```

---

## 📞 Soporte

Si necesitas:
- Cambiar la especialidad (agregar campos médicos específicos)
- Exportar datos a Excel/PDF
- Sincronizar con tu sistema médico existente
- Cambios en el diseño

Dime y lo hago en 10 minutos.

---

**URL de tu app:** `https://historia-clinica-[nombre].vercel.app`

Comparte este link con tu cliente — funciona en cualquier navegador, en cualquier dispositivo.
