# 🚀 Despliegue en Render - Backend + Frontend

## 📋 Resumen

Este proyecto se desplegará completamente en **Render**:
- **Backend:** Express.js (Node.js)
- **Frontend:** React + Vite (Static Site)
- **Base de Datos:** FreeSQLDatabase (MySQL)

---

## 🔧 Paso 1: Preparar el Repositorio

### 1.1 Inicializar Git (YA HECHO)
```bash
git init
git remote add origin https://github.com/EGMdev-profesional/SistemaDeVerificacionv13.git
```

### 1.2 Agregar Archivos
```bash
git add .
git commit -m "Initial commit - Sistema de Asistencia QR"
git branch -M main
git push -u origin main
```

---

## 🗄️ Paso 2: Configurar Base de Datos en FreeSQLDatabase

### 2.1 Acceder a FreeSQLDatabase
1. Abre: https://www.freesqldatabase.com/account/
2. Inicia sesión

### 2.2 Importar database.sql
1. Abre **phpMyAdmin**
2. Selecciona tu base de datos
3. Ve a **Import**
4. Sube: `database.sql`
5. Haz clic en **Go**

### 2.3 Guardar Credenciales
```
Host: sql5.freesqldatabase.com
Usuario: sql5810068
Contraseña: [Tu contraseña]
Base de datos: sql5810068
Puerto: 3306
```

---

## 🎯 Paso 3: Desplegar en Render

### 3.1 Crear Servicio Backend

**Opción A: Usando render.yaml (RECOMENDADO)**
1. Abre: https://render.com
2. Haz clic en **"New +"** → **"Web Service"**
3. Conecta tu repositorio de GitHub
4. Render detectará automáticamente `render.yaml`
5. Haz clic en **"Create Web Service"**

**Opción B: Configuración Manual**
1. Abre: https://render.com
2. Haz clic en **"New +"** → **"Web Service"**
3. Conecta tu repositorio
4. Configura:
   - **Name:** `asistencia-qr-backend`
   - **Root Directory:** `backend`
   - **Build Command:** `npm install`
   - **Start Command:** `npm start`
   - **Instance Type:** Free

### 3.2 Agregar Variables de Entorno (Backend)

En el panel de Render, ve a **Environment** y agrega:

```
NODE_ENV=production
PORT=3000
DB_HOST=sql5.freesqldatabase.com
DB_USER=sql5810068
DB_PASSWORD=tu_contraseña_aqui
DB_NAME=sql5810068
DB_PORT=3306
JWT_SECRET=tu_clave_secreta_super_segura_cambiala_en_produccion_2024
HORA_ENTRADA=08:00:00
HORA_SALIDA=13:00:00
```

### 3.3 Obtener URL del Backend
Una vez desplegado, Render te dará una URL como:
```
https://asistencia-qr-backend.onrender.com
```
**Guarda esta URL** ⬅️

---

## 🎨 Paso 4: Desplegar Frontend en Render

### 4.1 Crear Servicio Frontend

1. Abre: https://render.com
2. Haz clic en **"New +"** → **"Static Site"**
3. Conecta tu repositorio
4. Configura:
   - **Name:** `asistencia-qr-frontend`
   - **Root Directory:** `frontend`
   - **Build Command:** `npm install && npm run build`
   - **Publish Directory:** `dist`

### 4.2 Agregar Variables de Entorno (Frontend)

En el panel de Render, ve a **Environment** y agrega:

```
VITE_API_URL=https://asistencia-qr-backend.onrender.com
```

### 4.3 Obtener URL del Frontend
Una vez desplegado, Render te dará una URL como:
```
https://asistencia-qr-frontend.onrender.com
```

---

## ✅ Verificar que Funciona

### 1. Backend Activo
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

### 2. Login Admin
```bash
curl -X POST https://asistencia-qr-backend.onrender.com/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"usuario":"admin","password":"admin123"}'
```

### 3. Acceder al Frontend
Abre en tu navegador:
```
https://asistencia-qr-frontend.onrender.com
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

## 📝 Actualizar Código

Para actualizar el código en producción:

```bash
# Hacer cambios locales
git add .
git commit -m "Descripción del cambio"
git push origin main

# Render se redeploy automáticamente
```

---

## 🆘 Troubleshooting

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

### Backend no responde
- Espera 30 segundos (Render inicia lento)
- Verifica el estado en el panel de Render

### Frontend no carga
- Verifica que `VITE_API_URL` sea correcta en Render
- Verifica que el backend esté activo

---

## 📊 Checklist Final

- [ ] database.sql importado en FreeSQLDatabase
- [ ] Código pusheado a GitHub
- [ ] Backend desplegado en Render
- [ ] Variables de entorno configuradas en Render (Backend)
- [ ] Frontend desplegado en Render
- [ ] Variables de entorno configuradas en Render (Frontend)
- [ ] Login admin funciona
- [ ] Login practicante funciona
- [ ] Escaneo QR funciona

---

¡Tu aplicación está en producción! 🎉

