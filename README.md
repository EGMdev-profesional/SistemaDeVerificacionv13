# 🏛️ Sistema de Asistencia QR - Municipalidad de Piura

Sistema de registro de asistencia mediante códigos QR para practicantes de la Municipalidad de Piura.

## 📋 Características

- ✅ Autenticación con JWT
- ✅ Generación y escaneo de códigos QR
- ✅ Registro de asistencias (entrada/salida)
- ✅ Detección de tardanzas
- ✅ Generación de reportes
- ✅ Panel de administración
- ✅ Gestión de practicantes

---

## 🏗️ Arquitectura

```
Frontend (React + Vite)
    ↓
Render (Static Site)
    ↓
Backend (Express.js)
    ↓
Render (Web Service)
    ↓
Base de Datos (MySQL)
    ↓
FreeSQLDatabase
```

---

## 🚀 Despliegue Rápido

### Opción 1: Desplegar TODO en Render (RECOMENDADO)

1. **Importar Base de Datos**
   ```bash
   # Abre: https://www.freesqldatabase.com/account/
   # phpMyAdmin → Import → database.sql
   ```

2. **Desplegar en Render**
   ```bash
   # Abre: https://render.com
   # Conecta tu repositorio de GitHub
   # Render detectará render.yaml automáticamente
   ```

3. **Configurar Variables de Entorno**
   - Backend: DB_HOST, DB_USER, DB_PASSWORD, JWT_SECRET, etc.
   - Frontend: VITE_API_URL

Ver detalles en: **RENDER_DEPLOYMENT.md**

---

## 📁 Estructura del Proyecto

```
├── backend/
│   ├── config/
│   │   └── database.js
│   ├── controllers/
│   ├── middleware/
│   ├── routes/
│   ├── package.json
│   ├── server.js
│   └── .env.production
│
├── frontend/
│   ├── src/
│   ├── public/
│   ├── package.json
│   ├── vite.config.js
│   └── .env.production
│
├── database.sql
├── render.yaml
└── RENDER_DEPLOYMENT.md
```

---

## 🔐 Credenciales por Defecto

### Administrador
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

## 🛠️ Desarrollo Local

### Backend
```bash
cd backend
npm install
npm run dev
```

### Frontend
```bash
cd frontend
npm install
npm run dev
```

---

## 📦 Dependencias

### Backend
- Express.js
- MySQL2
- bcrypt
- jsonwebtoken
- cors
- dotenv
- multer
- express-validator

### Frontend
- React
- Vite
- React Router
- Axios
- qrcode.react
- html5-qrcode
- Tailwind CSS
- Lucide React

---

## 🗄️ Base de Datos

### Tablas
- `administradores` - Usuarios administradores
- `practicantes` - Practicantes del programa
- `asistencias` - Registros de asistencia

### Vistas
- `vista_asistencias` - Asistencias con información del practicante
- `vista_estadisticas_practicantes` - Estadísticas por practicante

---

## 📝 Variables de Entorno

### Backend (.env)
```
PORT=3000
NODE_ENV=development
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=
DB_NAME=asistencia_qr
DB_PORT=3306
JWT_SECRET=tu_clave_secreta
HORA_ENTRADA=08:00:00
HORA_SALIDA=13:00:00
```

### Frontend (.env)
```
VITE_API_URL=http://localhost:3000
```

---

## 🔗 API Endpoints

### Autenticación
- `POST /api/auth/login` - Login
- `POST /api/auth/logout` - Logout

### Administración
- `GET /api/admin/dashboard` - Dashboard
- `GET /api/admin/practicantes` - Listar practicantes
- `POST /api/admin/practicantes` - Crear practicante

### Practicantes
- `GET /api/practicantes/:id` - Obtener practicante
- `PUT /api/practicantes/:id` - Actualizar practicante

### Asistencias
- `POST /api/asistencias/registrar` - Registrar asistencia
- `GET /api/asistencias/:practicante_id` - Obtener asistencias

### Reportes
- `GET /api/reportes/diario` - Reporte diario
- `GET /api/reportes/mensual` - Reporte mensual

---

## 🧪 Testing

```bash
# Backend
cd backend
npm test

# Frontend
cd frontend
npm test
```

---

## 🐛 Troubleshooting

Ver: **RENDER_DEPLOYMENT.md** - Sección Troubleshooting

---

## 📞 Soporte

Para más información, consulta:
- **RENDER_DEPLOYMENT.md** - Guía de despliegue en Render
- **QUICK_START.md** - Instrucciones rápidas
- **DEPLOYMENT_GUIDE.md** - Guía completa

---

## 📄 Licencia

MIT

---

## 👨‍💻 Autor

ElixirStudio

---

**Última actualización:** Noviembre 2025

