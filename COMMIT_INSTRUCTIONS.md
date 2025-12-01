# 📤 Instrucciones para Commit y Push a GitHub

## ✅ Paso 1: Verificar Estado

```bash
git status
```

Deberías ver archivos sin seguimiento (Untracked files).

---

## ✅ Paso 2: Agregar Todos los Archivos

```bash
git add .
```

---

## ✅ Paso 3: Hacer Commit

```bash
git commit -m "Initial commit - Sistema de Asistencia QR con configuración para Render"
```

---

## ✅ Paso 4: Cambiar Rama a Main

```bash
git branch -M main
```

---

## ✅ Paso 5: Hacer Push a GitHub

```bash
git push -u origin main
```

Si pide credenciales:
- **Usuario:** Tu usuario de GitHub
- **Contraseña:** Tu token de acceso personal (o contraseña)

---

## ✅ Paso 6: Verificar en GitHub

1. Abre: https://github.com/EGMdev-profesional/SistemaDeVerificacionv13
2. Verifica que todos los archivos estén ahí
3. Verifica que `render.yaml` esté en la raíz

---

## 🚀 Paso 7: Desplegar en Render

### 7.1 Crear Servicio Backend

1. Abre: https://render.com
2. Haz clic en **"New +"** → **"Web Service"**
3. Conecta tu repositorio de GitHub
4. Configura:
   - **Name:** `asistencia-qr-backend`
   - **Root Directory:** `backend`
   - **Build Command:** `npm install`
   - **Start Command:** `npm start`
5. Haz clic en **"Create Web Service"**

### 7.2 Agregar Variables de Entorno (Backend)

En el panel de Render, ve a **Environment** y agrega:

```
NODE_ENV=production
PORT=3000
DB_HOST=sql5.freesqldatabase.com
DB_USER=sql5810068
DB_PASSWORD=tu_contraseña_aqui
DB_NAME=sql5810068
DB_PORT=3306
JWT_SECRET=tu_clave_secreta_super_segura_2024
HORA_ENTRADA=08:00:00
HORA_SALIDA=13:00:00
```

### 7.3 Obtener URL del Backend

Una vez desplegado:
```
https://asistencia-qr-backend.onrender.com
```

---

### 7.4 Crear Servicio Frontend

1. Abre: https://render.com
2. Haz clic en **"New +"** → **"Static Site"**
3. Conecta tu repositorio
4. Configura:
   - **Name:** `asistencia-qr-frontend`
   - **Root Directory:** `frontend`
   - **Build Command:** `npm install && npm run build`
   - **Publish Directory:** `dist`
5. Haz clic en **"Create Static Site"**

### 7.5 Agregar Variables de Entorno (Frontend)

En el panel de Render, ve a **Environment** y agrega:

```
VITE_API_URL=https://asistencia-qr-backend.onrender.com
```

### 7.6 Obtener URL del Frontend

Una vez desplegado:
```
https://asistencia-qr-frontend.onrender.com
```

---

## 🧪 Paso 8: Verificar que Funciona

### 8.1 Backend
```bash
curl https://asistencia-qr-backend.onrender.com
```

### 8.2 Frontend
Abre en navegador:
```
https://asistencia-qr-frontend.onrender.com
```

### 8.3 Login
- Usuario: `admin`
- Contraseña: `admin123`

---

## 📋 Checklist Final

- [ ] `git add .`
- [ ] `git commit -m "..."`
- [ ] `git branch -M main`
- [ ] `git push -u origin main`
- [ ] Verificar en GitHub
- [ ] Backend desplegado en Render
- [ ] Variables de entorno configuradas (Backend)
- [ ] Frontend desplegado en Render
- [ ] Variables de entorno configuradas (Frontend)
- [ ] Backend responde
- [ ] Frontend carga
- [ ] Login funciona

---

## 🆘 Si Algo Falla

### Error: "Permission denied (publickey)"
Necesitas configurar SSH en GitHub:
1. Genera clave SSH: `ssh-keygen -t ed25519 -C "tu@email.com"`
2. Agrega la clave pública a GitHub
3. Intenta de nuevo

### Error: "fatal: 'origin' does not appear to be a git repository"
Ya está configurado. Intenta:
```bash
git push -u origin main
```

### Error: "Everything up-to-date"
Ya está todo pusheado. Verifica en GitHub.

---

## 📝 Comandos Rápidos

```bash
# Ver estado
git status

# Ver commits
git log --oneline

# Ver remote
git remote -v

# Cambiar rama
git checkout -b nueva-rama

# Mergear rama
git merge nombre-rama

# Ver diferencias
git diff
```

---

¡Listo! Tu código está en GitHub y desplegado en Render 🎉

