# ✅ Base de Datos - CORREGIDA

## 🔧 Problema Resuelto

El error que recibiste fue:
```
#1293 - Incorrecta definición de tabla; Solamente debe haber una columna TIMESTAMP 
con CURRENT_TIMESTAMP en DEFAULT o ON UPDATE cláusula
```

**Causa:** FreeSQLDatabase (MySQL antiguo) no permite dos columnas TIMESTAMP con CURRENT_TIMESTAMP.

**Solución:** Cambié las tablas para usar solo UNA columna TIMESTAMP.

---

## ✅ Lo que se Corrigió

### Antes (ERROR):
```sql
fecha_creacion TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
fecha_actualizacion TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
```

### Después (CORRECTO):
```sql
fecha_creacion TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
```

---

## 📥 Cómo Importar Nuevamente

### Opción 1: Usar el archivo corregido (RECOMENDADO)

1. Abre: https://www.freesqldatabase.com/account/
2. phpMyAdmin → Tu base de datos
3. Ve a **"Import"**
4. Sube: `database.sql` (ya está corregido en GitHub)
5. Haz clic en **"Go"**

### Opción 2: Copiar y pegar el SQL directamente

1. Abre: https://www.freesqldatabase.com/account/
2. phpMyAdmin → Tu base de datos
3. Ve a **"SQL"**
4. Copia y pega el SQL de abajo
5. Haz clic en **"Go"**

---

## 📋 SQL Corregido (Copia y Pega)

```sql
-- ============================================================================
-- Base de datos para Sistema de Asistencia por QR
-- Municipalidad de Piura - Practicantes UCV
-- ============================================================================

-- Tabla de Administradores
CREATE TABLE IF NOT EXISTS administradores (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    apellidos VARCHAR(100) NOT NULL,
    usuario VARCHAR(50) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    email VARCHAR(100),
    telefono VARCHAR(20),
    foto VARCHAR(255) DEFAULT 'default-avatar.png',
    activo BOOLEAN DEFAULT TRUE,
    fecha_creacion TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

-- Tabla de Practicantes
CREATE TABLE IF NOT EXISTS practicantes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    apellidos VARCHAR(100) NOT NULL,
    documento VARCHAR(20) UNIQUE NOT NULL,
    telefono VARCHAR(20),
    codigo VARCHAR(50) UNIQUE NOT NULL,
    usuario VARCHAR(50) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    email VARCHAR(100),
    foto VARCHAR(255) DEFAULT 'default-avatar.png',
    horario JSON NULL,
    periodo_inicio DATE NULL,
    periodo_fin DATE NULL,
    activo BOOLEAN DEFAULT TRUE,
    fecha_creacion TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

-- Tabla de Asistencias
CREATE TABLE IF NOT EXISTS asistencias (
    id INT AUTO_INCREMENT PRIMARY KEY,
    practicante_id INT NOT NULL,
    fecha DATE NOT NULL,
    hora TIME NOT NULL,
    tipo ENUM('entrada', 'salida') NOT NULL,
    es_tardanza BOOLEAN DEFAULT FALSE,
    es_salida_temprana BOOLEAN DEFAULT FALSE,
    observaciones TEXT,
    registrado_por INT,
    fecha_registro TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (practicante_id) REFERENCES practicantes(id) ON DELETE CASCADE,
    FOREIGN KEY (registrado_por) REFERENCES administradores(id) ON DELETE SET NULL,
    INDEX idx_practicante_fecha (practicante_id, fecha),
    INDEX idx_fecha (fecha),
    INDEX idx_tipo (tipo)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

-- ============================================================================
-- INSERCIÓN DE DATOS INICIALES
-- ============================================================================

-- Insertar administrador por defecto
INSERT IGNORE INTO administradores (nombre, apellidos, usuario, password, email, telefono) 
VALUES (
    'Administrador', 
    'Sistema', 
    'admin', 
    '$2b$10$EVv/Y.Zr2Q9XOxlxjCuSwOLEgF4EA1i0fl1zh0lhusEtBCdgpvxa2',
    'admin@municipalidad-piura.gob.pe',
    '073-123456'
);

-- Insertar practicantes de ejemplo
INSERT IGNORE INTO practicantes (nombre, apellidos, documento, telefono, codigo, usuario, password, email) 
VALUES 
(
    'Juan Carlos', 
    'Pérez García', 
    '72345678', 
    '987654321', 
    'PRACT-001', 
    'PRACT-001', 
    '$2b$10$92IXUNpkjO0rOQ5byMi.Ye4oKoEa3Ro9llC/.og/at2.uheWG/igi',
    'juan.perez@ucv.edu.pe'
),
(
    'María Elena', 
    'Rodríguez López', 
    '71234567', 
    '987654322', 
    'PRACT-002', 
    'PRACT-002', 
    '$2b$10$92IXUNpkjO0rOQ5byMi.Ye4oKoEa3Ro9llC/.og/at2.uheWG/igi',
    'maria.rodriguez@ucv.edu.pe'
),
(
    'Carlos Alberto', 
    'Sánchez Díaz', 
    '70123456', 
    '987654323', 
    'PRACT-003', 
    'PRACT-003', 
    '$2b$10$92IXUNpkjO0rOQ5byMi.Ye4oKoEa3Ro9llC/.og/at2.uheWG/igi',
    'carlos.sanchez@ucv.edu.pe'
);

-- Insertar asistencias de ejemplo
INSERT INTO asistencias (practicante_id, fecha, hora, tipo, es_tardanza, registrado_por) 
VALUES 
(1, CURDATE() - INTERVAL 6 DAY, '07:55:00', 'entrada', FALSE, 1),
(1, CURDATE() - INTERVAL 6 DAY, '13:00:00', 'salida', FALSE, 1),
(2, CURDATE() - INTERVAL 6 DAY, '08:15:00', 'entrada', TRUE, 1),
(2, CURDATE() - INTERVAL 6 DAY, '13:05:00', 'salida', FALSE, 1),
(1, CURDATE() - INTERVAL 5 DAY, '08:00:00', 'entrada', FALSE, 1),
(1, CURDATE() - INTERVAL 5 DAY, '13:00:00', 'salida', FALSE, 1),
(3, CURDATE() - INTERVAL 5 DAY, '08:30:00', 'entrada', TRUE, 1),
(3, CURDATE() - INTERVAL 5 DAY, '12:45:00', 'salida', TRUE, 1),
(1, CURDATE() - INTERVAL 4 DAY, '07:58:00', 'entrada', FALSE, 1),
(1, CURDATE() - INTERVAL 4 DAY, '13:02:00', 'salida', FALSE, 1),
(2, CURDATE() - INTERVAL 4 DAY, '08:00:00', 'entrada', FALSE, 1),
(2, CURDATE() - INTERVAL 4 DAY, '13:00:00', 'salida', FALSE, 1),
(1, CURDATE(), '07:55:00', 'entrada', FALSE, 1),
(2, CURDATE(), '08:10:00', 'entrada', TRUE, 1),
(3, CURDATE(), '08:25:00', 'entrada', TRUE, 1);

-- Vistas para reportes
CREATE OR REPLACE VIEW vista_asistencias AS
SELECT 
    a.id,
    a.fecha,
    a.hora,
    a.tipo,
    a.es_tardanza,
    a.es_salida_temprana,
    p.id as practicante_id,
    p.codigo,
    CONCAT(p.nombre, ' ', p.apellidos) as practicante_nombre,
    p.documento,
    p.foto,
    adm.usuario as registrado_por_usuario
FROM asistencias a
INNER JOIN practicantes p ON a.practicante_id = p.id
LEFT JOIN administradores adm ON a.registrado_por = adm.id
ORDER BY a.fecha DESC, a.hora DESC;

CREATE OR REPLACE VIEW vista_estadisticas_practicantes AS
SELECT 
    p.id,
    p.codigo,
    CONCAT(p.nombre, ' ', p.apellidos) as nombre_completo,
    p.documento,
    p.foto,
    COUNT(DISTINCT CASE WHEN a.tipo = 'entrada' THEN a.fecha END) as total_asistencias,
    COUNT(CASE WHEN a.es_tardanza = TRUE THEN 1 END) as total_tardanzas,
    COUNT(CASE WHEN a.es_salida_temprana = TRUE THEN 1 END) as total_salidas_tempranas
FROM practicantes p
LEFT JOIN asistencias a ON p.id = a.practicante_id
WHERE p.activo = TRUE
GROUP BY p.id, p.codigo, p.nombre, p.apellidos, p.documento, p.foto;
```

---

## 🔐 Credenciales

```
ADMIN:
  Usuario: admin
  Contraseña: admin123

PRACTICANTES:
  Usuarios: PRACT-001, PRACT-002, PRACT-003
  Contraseña: 123456
```

---

## ✅ Verificación

Después de importar, deberías ver:
- ✅ 3 tablas creadas (administradores, practicantes, asistencias)
- ✅ 2 vistas creadas (vista_asistencias, vista_estadisticas_practicantes)
- ✅ 1 administrador
- ✅ 3 practicantes
- ✅ 15 registros de asistencia

---

## 🚀 Próximo Paso

Una vez importada la base de datos, puedes desplegar en Render.

Ver: **RENDER_DEPLOYMENT.md**

