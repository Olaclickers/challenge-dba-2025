# 🧪 OlaClick DBA Challenge

## 🎯 Objetivo

Evaluar tus habilidades como **Administrador/a de Bases de Datos (DBA)** en entornos de producción críticos, con foco en:

- Modelado de datos eficiente y seguro
- Optimización de rendimiento (PostgreSQL)
- Uso de Redis para almacenamiento temporal o cache
- Estrategias de respaldo y recuperación
- Soporte a sistemas distribuidos y alta concurrencia
- Compatibilidad con ORMs (Eloquent, Prisma o Sequelize)
- ETL y monitoreo

---

## 📋 Contexto

OlaClick gestiona órdenes de restaurantes en múltiples países y zonas horarias. Se requiere mantener datos consistentes, consultas eficientes, monitoreo activo y alta disponibilidad en entornos PostgreSQL y Redis.

---

## 🔍 Parte 1: Modelado de Datos (Relacional)

### Requerimiento:

Diseña un modelo de datos relacional en PostgreSQL para soportar:

- Restaurantes con múltiples sucursales
- Clientes que realizan pedidos
- Pedidos que contienen uno o más productos
- Estado de cada pedido (`initiated`, `sent`, `delivered`)
- Registro de cambios de estado (con timestamp)

**Entregables:**

1. Script SQL con `CREATE TABLE` y relaciones (`FK`, `PK`, `constraints`, `indexes`)
2. Justificación de decisiones de modelado (ej. normalización, índices, tipos de datos)

---

## ⚙️ Parte 2: Optimización de Consultas

Dada la siguiente consulta:

```sql
SELECT p.id, p.total, c.name, r.name
FROM orders p
JOIN clients c ON p.client_id = c.id
JOIN restaurants r ON p.restaurant_id = r.id
WHERE p.status = 'sent'
AND p.created_at >= NOW() - interval '7 days';
```

Tareas:
1. Explica cómo identificarías cuellos de botella (usa EXPLAIN ANALYZE o pg_stat_statements)
2. Propón al menos 2 formas de optimizar la consulta (índices, particionamiento, etc.)
3. Justifica cómo afectaría la solución al sistema en producción

### 🧪 Parte 3: Redis
1. ¿Cómo usarías Redis para mejorar el rendimiento del sistema en lectura de órdenes por estado?
2. ¿Qué estrategias usarías para evitar inconsistencias entre Redis y PostgreSQL?
3. ¿Cuándo preferirías evitar usar Redis en un sistema de alta concurrencia?

### 🧯 Parte 4: Respaldo y Recuperación
1. Describe tu estrategia de backup para una base de datos de 100 GB que no puede tener más de 5 minutos de pérdida de datos (RPO).
2. ¿Cómo configurarías una réplica de solo lectura en PostgreSQL?
3. ¿Qué herramienta o enfoque usarías para automatizar y validar los backups?

### 🔐 Parte 5: Seguridad y Acceso
1. ¿Qué prácticas aplicarías para proteger las credenciales de conexión a la base de datos?
2. ¿Cómo controlarías el acceso a los datos entre entornos (producción, staging, desarrollo)?
3. ¿Cómo implementarías auditoría de acceso a datos sensibles?

### 📦 Entrega
1. Sube tu solución a un repositorio Git (puede ser privado).
2. Incluye un README.md con instrucciones claras para revisar tu trabajo.
   
¡Gracias por participar en el reto técnico de OlaClick! 🚀
