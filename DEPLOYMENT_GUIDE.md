# 🚀 Guía de Despliegue - Sistema de Asistencia QR

## Arquitectura del Despliegue

```
┌─────────────────────────────────────────────────────────────┐
│                    VERCEL (Frontend)                        │
│              React + Vite (SPA - Static)                    │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│                    RENDER (Backend)                         │
│              Express.js (Node.js Server)                    │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│            FreeSQLDatabase (MySQL Database)                 │
│              phpMyAdmin - sql5.freesqldatabase.com           │
└─────────────────────────────────────────────────────────────┘
```

---

## 📋 Paso 1: Configurar Base de Datos en FreeSQLDatabase

### 1.1 Acceder a FreeSQLDatabase
- Ir a: https://www.freesqldatabase.com/account/
- Iniciar sesión con tu cuenta

### 1.2 Importar el SQL
1. Abre **phpMyAdmin** desde tu cuenta
2. Selecciona tu base de datos `sql5810068`
3. Ve a la pestaña **"Import"**
4. Sube el archivo `database.sql` (ya está actualizado con:
   - ✅ Tablas completas
   - ✅ Campos adicionales de horario y periodo (migration 001)
   - ✅ Contraseñas hasheadas correctamente con bcrypt
   - ✅ Datos de ejemplo listos para usar

### 1.3 Credenciales de Acceso
Guarda estos datos (los verás en tu panel de FreeSQLDatabase):
```
Host: sql5.freesqldatabase.com
Usuario: sql5810068
Contraseña: [Tu contraseña]
Base de datos: sql5810068
Puerto: 3306
```

---

## 🔐 Credenciales de la Aplicación

### Administrador
- **Usuario:** `admin`
- **Contraseña:** `admin123`

### Practicantes (3 ejemplos)
- **Usuario:** `PRACT-001`, `PRACT-002`, `PRACT-003`
- **Contraseña:** `123456` (para todos)

---

## 📦 Paso 2: Desplegar Backend en Render

### 2.1 Preparar el Backend
1. Asegúrate de tener el backend en una carpeta separada
2. Verifica que `backend/package.json` tenga:
   ```json
   "scripts": {
     "start": "node server.js",
     "dev": "nodemon server.js"
   }
   ```

### 2.2 Crear Repositorio en GitHub
```bash
# En la carpeta del proyecto
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/TU_USUARIO/tu-repo.git
git push -u origin main
```

### 2.3 Desplegar en Render
1. Ir a https://render.com
2. Crear cuenta (con GitHub)
3. Hacer clic en **"New +"** → **"Web Service"**
4. Conectar tu repositorio de GitHub
5. Configurar:
   - **Name:** `asistencia-qr-backend`
   - **Root Directory:** `backend`
   - **Build Command:** `npm install`
   - **Start Command:** `npm start`
   - **Instance Type:** Free (o Starter si necesitas más recursos)

### 2.4 Agregar Variables de Entorno en Render
En el panel de Render, ve a **Environment** y agrega:

```
PORT=3000
NODE_ENV=production

DB_HOST=sql5.freesqldatabase.com
DB_USER=sql5810068
DB_PASSWORD=tu_contraseña_aqui
DB_NAME=sql5810068
DB_PORT=3306

JWT_SECRET=tu_clave_secreta_super_segura_cambiala_en_produccion_2024

HORA_ENTRADA=08:00:00
HORA_SALIDA=13:00:00
```

**⚠️ IMPORTANTE:** Reemplaza `tu_contraseña_aqui` con tu contraseña real de FreeSQLDatabase

### 2.5 Obtener URL del Backend
Una vez desplegado, Render te dará una URL como:
```
https://asistencia-qr-backend.onrender.com
```
**Guarda esta URL** para el frontend.

---

## 🎨 Paso 3: Desplegar Frontend en Vercel

### 3.1 Configurar Variables de Entorno
En `frontend/.env`:
```
VITE_API_URL=https://asistencia-qr-backend.onrender.com
```

### 3.2 Desplegar en Vercel
1. Ir a https://vercel.com
2. Crear cuenta (con GitHub)
3. Hacer clic en **"New Project"**
4. Seleccionar tu repositorio
5. Configurar:
   - **Framework Preset:** Vite
   - **Root Directory:** `frontend`
   - **Build Command:** `npm run build`
   - **Output Directory:** `dist`

### 3.3 Agregar Variables de Entorno en Vercel
En el panel de Vercel, ve a **Settings** → **Environment Variables**:
```
VITE_API_URL=https://asistencia-qr-backend.onrender.com
```

### 3.4 Obtener URL del Frontend
Vercel te dará una URL como:
```
https://tu-proyecto.vercel.app
```

---

## 🔗 Actualizar CORS en Backend

Si necesitas permitir tu dominio de Vercel, actualiza `backend/server.js`:

```javascript
app.use(cors({
  origin: [
    'https://tu-proyecto.vercel.app',
    'http://localhost:3000', // para desarrollo local
    'http://localhost:5173'  // para Vite local
  ],
  credentials: true
}));
```

---

## ✅ Checklist de Despliegue

- [ ] Base de datos importada en FreeSQLDatabase
- [ ] Credenciales de BD guardadas
- [ ] Backend desplegado en Render
- [ ] Variables de entorno configuradas en Render
- [ ] URL del backend obtenida
- [ ] Frontend desplegado en Vercel
- [ ] Variables de entorno configuradas en Vercel
- [ ] CORS actualizado si es necesario
- [ ] Pruebas de login realizadas
- [ ] Pruebas de escaneo QR realizadas

---

## 🧪 Pruebas Iniciales

### Test 1: Verificar Backend
```bash
curl https://asistencia-qr-backend.onrender.com
```
Deberías ver:
```json
{
  "message": "API Sistema de Asistencia QR - Municipalidad de Piura",
  "version": "1.0.0",
  "endpoints": {...}
}
```

### Test 2: Login Admin
```bash
curl -X POST https://asistencia-qr-backend.onrender.com/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"usuario":"admin","password":"admin123"}'
```

### Test 3: Acceder al Frontend
Abre tu navegador en:
```
https://tu-proyecto.vercel.app
```

---

## 🐛 Troubleshooting

### Error: "Cannot connect to database"
- Verifica que las credenciales en Render sean correctas
- Asegúrate de que FreeSQLDatabase esté activo
- Comprueba que el host sea `sql5.freesqldatabase.com`

### Error: "CORS error"
- Actualiza la URL de origen en `backend/server.js`
- Redeploy el backend en Render

### Error: "Invalid token"
- Verifica que `JWT_SECRET` sea el mismo en Render
- Limpia cookies del navegador

---

## 📝 Notas Importantes

1. **Contraseñas hasheadas:** Todas las contraseñas en la BD están hasheadas con bcrypt
2. **Datos de ejemplo:** Hay 3 practicantes y 1 admin listos para usar
3. **Horarios:** Configurables en variables de entorno
4. **Uploads:** Los archivos subidos se guardan en la carpeta `uploads/` del backend

---

## 🔄 Actualizar Código

Para actualizar el código en producción:

```bash
# Hacer cambios locales
git add .
git commit -m "Descripción del cambio"
git push origin main

# Render se redeploy automáticamente
# Vercel se redeploy automáticamente
```

---

¡Tu aplicación está lista para producción! 🎉

