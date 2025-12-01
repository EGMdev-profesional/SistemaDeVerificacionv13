# ⚡ Quick Start - Despliegue Render + Vercel + FreeSQLDatabase

## 🎯 Resumen Rápido

Tu proyecto está **100% listo** para desplegar. Solo necesitas:

1. **Base de datos:** Importar `database.sql` en FreeSQLDatabase
2. **Backend:** Desplegar en Render
3. **Frontend:** Desplegar en Vercel

---

## 📋 Paso 1: Base de Datos (5 minutos)

```
1. Abre: https://www.freesqldatabase.com/account/
2. Haz clic en "phpMyAdmin"
3. Selecciona tu base de datos
4. Ve a "Import"
5. Sube el archivo: database.sql
6. Haz clic en "Go"
7. ✅ Listo
```

**Credenciales guardadas:**
- Host: `sql5.freesqldatabase.com`
- Usuario: `sql5810068`
- Base de datos: `sql5810068`

---

## 🚀 Paso 2: Backend en Render (10 minutos)

### 2.1 Crear Repositorio GitHub
```bash
cd tu-proyecto
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/TU_USUARIO/tu-repo.git
git push -u origin main
```

### 2.2 Desplegar en Render
1. Abre: https://render.com
2. Haz clic en "New Web Service"
3. Conecta tu repositorio
4. Configura:
   - **Name:** `asistencia-qr-backend`
   - **Root Directory:** `backend`
   - **Build Command:** `npm install`
   - **Start Command:** `npm start`

### 2.3 Agregar Variables de Entorno
En Render → Environment, agrega:
```
DB_HOST=sql5.freesqldatabase.com
DB_USER=sql5810068
DB_PASSWORD=TU_CONTRASEÑA_AQUI
DB_NAME=sql5810068
DB_PORT=3306
JWT_SECRET=tu_clave_secreta_super_segura_2024
NODE_ENV=production
PORT=3000
HORA_ENTRADA=08:00:00
HORA_SALIDA=13:00:00
```

### 2.4 Obtener URL
Cuando termine el deploy, Render te dará:
```
https://asistencia-qr-backend.onrender.com
```
**Guarda esta URL** ⬅️

---

## 🎨 Paso 3: Frontend en Vercel (10 minutos)

### 3.1 Actualizar .env
En `frontend/.env`:
```
VITE_API_URL=https://asistencia-qr-backend.onrender.com
```

### 3.2 Desplegar en Vercel
1. Abre: https://vercel.com
2. Haz clic en "New Project"
3. Selecciona tu repositorio
4. Configura:
   - **Framework:** Vite
   - **Root Directory:** `frontend`

### 3.3 Agregar Variables de Entorno
En Vercel → Settings → Environment Variables:
```
VITE_API_URL=https://asistencia-qr-backend.onrender.com
```

### 3.4 Obtener URL
Vercel te dará:
```
https://tu-proyecto.vercel.app
```

---

## 🔐 Credenciales de Acceso

### Admin
```
Usuario: admin
Contraseña: admin123
```

### Practicantes
```
Usuarios: PRACT-001, PRACT-002, PRACT-003
Contraseña: 123456
```

---

## ✅ Verificar que Funciona

```bash
# 1. Backend activo
curl https://asistencia-qr-backend.onrender.com

# 2. Login admin
curl -X POST https://asistencia-qr-backend.onrender.com/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"usuario":"admin","password":"admin123"}'

# 3. Abrir en navegador
https://tu-proyecto.vercel.app
```

---

## 📁 Archivos Importantes

- **database.sql** ← Importar en FreeSQLDatabase
- **DEPLOYMENT_GUIDE.md** ← Guía completa
- **backend/.env.production** ← Variables para Render
- **frontend/.env.production** ← Variables para Vercel

---

## 🆘 Si Algo Falla

### Error: "Cannot connect to database"
- Verifica credenciales en Render
- Verifica que FreeSQLDatabase esté activo

### Error: "CORS error"
- Actualiza `backend/server.js` con tu URL de Vercel
- Redeploy en Render

### Error: "Invalid token"
- Limpia cookies del navegador
- Verifica que JWT_SECRET sea igual en Render

---

## 📊 Checklist Final

- [ ] database.sql importado en FreeSQLDatabase
- [ ] Backend desplegado en Render
- [ ] Variables de entorno en Render configuradas
- [ ] Frontend desplegado en Vercel
- [ ] Variables de entorno en Vercel configuradas
- [ ] Login admin funciona
- [ ] Login practicante funciona
- [ ] Escaneo QR funciona

---

¡Listo! Tu app está en producción 🎉

