# 📊 Supermarket Sales Dashboard

[![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=flat&logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=flat&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Supabase](https://img.shields.io/badge/Supabase-3ECF8E?style=flat&logo=supabase&logoColor=white)](https://supabase.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Version](https://img.shields.io/badge/Version-1.0-blue.svg)]()

---

## 📋 Tabla de Contenidos

- [Descripción General](#-descripción-general)
- [Características Principales](#-características-principales)
- [Contenido del Proyecto](#-contenido-del-proyecto)
- [Herramientas y Tecnologías](#️-herramientas-y-tecnologías-utilizadas)
- [Configuración del Entorno](#️-configuración-del-entorno)
- [Estructura del Repositorio](#-estructura-del-repositorio)
- [Vistas Previas](#️-vistas-previas-del-proyecto)
- [Autor](#-autor)
- [Licencia](#-licencia)

---

## 📃 Descripción General

Dashboard profesional de **Supermarket Sales** desarrollado en Power BI, diseñado para analizar el rendimiento comercial de un supermercado mediante datos ficticios. Este proyecto se conecta a una base de datos remota **Supabase (PostgreSQL)** y transforma datos en información accionable mediante:

- 📊 **Vistas Analíticas:** Análisis completo de ventas por producto, categoría y período
- 📈 **Medidas DAX Avanzadas:** KPIs de ventas, rentabilidad y análisis de tendencias
- 🎯 **Análisis Comercial:** Ingresos, cantidades vendidas, márgenes y comparativas temporales
- 🎨 **Diseño Moderno:** Tooltips personalizados, menú de navegación interactivo
- 🌙 **Modo Oscuro/Claro:** Switcher dinámico para cambiar entre temas visuales
- 🖱️ **Navegación Interactiva:** Segmentación por producto, categoría y período de tiempo

---

## ✨ Características Principales

### 🔄 Transformaciones en Power Query
- Procesos de limpieza y modelado de datos para optimizar el rendimiento
- Conexión a base de datos remota Supabase
- Preparación de tablas dimensionales y de hechos

### 📐 Modelo de Datos
- **Tablas de Dimensión:** Productos, Categorías, Calendario, Clientes
- **Tabla de Hechos:** Ventas con información detallada de transacciones
- Relaciones optimizadas para análisis de ventas

### 🎨 Diseño Interactivo
- Navegación por páginas con menú interactivo
- **Tooltips personalizados** con información contextual
- **Switcher Modo Noche/Día** para mejor experiencia visual
- Segmentación de datos dinámica por múltiples dimensiones
- Diseño responsivo y profesional

---

## 📊 Contenido del Proyecto

| Página | Descripción | Contenido Principal |
|--------|-------------|---------------------|
| **Overview** | Vista general ejecutiva | KPIs globales de ventas, ingresos, unidades vendidas |
| **Sales Analysis** | Análisis de ventas | Desglose por categoría, producto, tendencias temporales |
| **Product Performance** | Rendimiento de productos | Top productos, análisis de rentabilidad, comparativas |

---

## 🛠️ Herramientas y Tecnologías Utilizadas

### Software Requerido
- **Power BI Desktop** (versión más reciente)

### Fuente de Datos
- **Supabase** - Base de datos remota PostgreSQL en la nube
- Datos ficticios de ventas de supermercado

### Lenguajes y Tecnologías
- **DAX** - Cálculo de medidas y KPIs especializados en ventas
- **Power Query (Lenguaje M)** - Transformación y limpieza de datos
- **HTML + CSS** - Tooltips personalizados y elementos visuales avanzados
- **PostgreSQL** - Motor de base de datos en Supabase

### Características Visuales Avanzadas
- 🎨 **Tooltips HTML/CSS** - Información contextual enriquecida
- 🌓 **Switcher Modo Noche/Día** - Cambio dinámico de temas
- 🧭 **Menú de Navegación** - Navegación intuitiva entre páginas

---

## ⚙️ Configuración del Entorno

### Prerequisitos
1. Descargar e instalar [Power BI Desktop](https://powerbi.microsoft.com/desktop/)
2. Crear cuenta en [Supabase](https://supabase.com/)

### Paso 1: Configurar Supabase
1. Crear cuenta en [Supabase](https://supabase.com/)
2. Crear un nuevo proyecto
3. Configurar la base de datos PostgreSQL
4. Obtener las credenciales de conexión:
   - **Host:** Tu URL de Supabase
   - **Database:** postgres (o el nombre de tu base)
   - **User:** postgres
   - **Password:** Tu contraseña de base de datos

### Paso 2: Crear Tablas en Supabase
Conectarse a Supabase usando pgAdmin, DBeaver o el SQL Editor de Supabase y crear las tablas necesarias:

<details>
<summary>📄 Ver Script SQL - Estructura de Tablas</summary>

```sql
-- Tabla de Productos
CREATE TABLE productos (
    producto_id INT PRIMARY KEY,
    producto_nombre TEXT NOT NULL,
    categoria TEXT NOT NULL,
    precio_unitario DECIMAL(10,2) NOT NULL
);

-- Tabla de Ventas
CREATE TABLE ventas (
    venta_id INT PRIMARY KEY,
    producto_id INT REFERENCES productos(producto_id),
    fecha DATE NOT NULL,
    cantidad INT NOT NULL,
    total_venta DECIMAL(10,2) NOT NULL,
    cliente_tipo TEXT
);

-- Tabla Calendario
CREATE TABLE calendario (
    fecha DATE PRIMARY KEY,
    año INT,
    mes INT,
    dia INT,
    nombre_mes TEXT,
    trimestre INT
);
