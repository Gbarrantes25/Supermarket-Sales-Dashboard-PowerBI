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
```
</details>

### Paso 3: Conectar Power BI a Supabase
1. Abrir Power BI Desktop
2. Ir a Obtener datos > Base de datos PostgreSQL
3. Ingresar las credenciales de Supabase:
   - Servidor: Tu URL de Supabase
   - Base de datos: postgres
   - Usuario: postgres
   - Contraseña: Tu contraseña
4. Ejecutar las consultas SQL necesarias para extraer las tablas
   
<details>
<summary>📊 Consulta Productos</summary>
   
   ```sql
   SELECT 
    producto_id,
    producto_nombre,
    categoria,
    precio_unitario
   FROM productos
   ORDER BY producto_id
   ```
</details>

<details>
<summary>📅 Consulta Calendario</summary>
   ```sql
   SELECT 
    fecha,
    año,
    mes,
    dia,
    nombre_mes,
    trimestre
   FROM calendario
   ORDER BY fecha
   ```
</details>

### Paso 4: Abrir el Dashboard
1. Abrir el archivo Supermarket Sales.pbip con Power BI Desktop
2. Hacer clic en "Actualizar" en la pestaña Inicio
3. Verificar que todas las conexiones se establezcan correctamente
4. Explorar las diferentes páginas del dashboard

## 📂 Estructura del Repositorio

```
.
├── Supermarket Sales.Report/          # Componentes del reporte (formato .pbip)
│   ├── StaticResources/               # Recursos estáticos
│   ├── definition/                    # Definición del reporte
│   └── definition.pbir                # Archivo de definición
├── Supermarket Sales.SemanticModel/   # Modelo semántico
│   ├── DAXQueries/                    # Consultas DAX
│   ├── definition/                    # Definición del modelo
│   ├── .pbi/                          # Configuración Power BI
│   ├── diagramLayout.json             # Layout del diagrama
│   └── definition.pbism               # Archivo de definición
├── Supermarket Sales.pbip             # Proyecto Power BI (formato nuevo)
├── .gitignore                         # Archivo de configuración Git
└── README.md                          # Este archivo
```

## 🧮 Medidas DAX Implementadas
#### 📊 KPIs de Ventas (Métricas Comerciales)
<details>
<summary>Ver KPIs de Ventas</summary>

Total Ventas - Ingresos totales por ventas

```dax
=SUM(Ventas[total_venta])
```

Total Unidades - Cantidad total de unidades vendidas

```dax
=SUM(Ventas[cantidad])
```
Ticket Promedio - Valor promedio por transacción

```dax
=DIVIDE([Total Ventas], DISTINCTCOUNT(Ventas[venta_id]), 0)
```

Precio Promedio - Precio promedio por unidad

```dax
=DIVIDE([Total Ventas], [Total Unidades], 0)
```

Ventas LY - Ventas del año anterior (Last Year)

```dax
=CALCULATE(
    [Total Ventas],
    SAMEPERIODLASTYEAR(Calendario[fecha])
)
```

Crecimiento % - Porcentaje de crecimiento vs año anterior

```dax
VAR VentasActual = [Total Ventas]
VAR VentasLY = [Ventas LY]
RETURN
DIVIDE(VentasActual - VentasLY, VentasLY, 0)
```

Margen Bruto - Rentabilidad de las ventas

```dax
VAR Ingresos = [Total Ventas]
VAR CostoEstimado = [Total Ventas] * 0.7
RETURN
Ingresos - CostoEstimado
```

Margen % - Porcentaje de margen

```dax
=DIVIDE([Margen Bruto], [Total Ventas], 0)
```

</details>

#### 📈 Análisis Temporal
<details>
<summary>Ver medidas temporales</summary>

Ventas YTD - Ventas acumuladas del año (Year-To-Date)

```dax
=TOTALYTD(
    [Total Ventas],
    Calendario[fecha]
)
```

Ventas MTD - Ventas del mes (Month-To-Date)

```dax
=TOTALMTD(
    [Total Ventas],
    Calendario[fecha]
)
```

Ventas QTD - Ventas del trimestre (Quarter-To-Date)

```dax
=TOTALQTD(
    [Total Ventas],
    Calendario[fecha]
)
```
Promedio Móvil 3 Meses - Tendencia suavizada

```dax
=AVERAGEX(
    DATESINPERIOD(
        Calendario[fecha],
        LASTDATE(Calendario[fecha]),
        -3,
        MONTH
    ),
    [Total Ventas]
)
```
</details>

#### 🎯 Análisis de Productos

<details>
<summary>Ver análisis de productos</summary>

Ranking Productos - Posición del producto por ventas

```dax
=RANKX(
    ALL(Productos[producto_nombre]),
    [Total Ventas],
    ,
    DESC,
    Dense
)
```

Top 5 Productos - Filtro para top 5

```dax
=IF([Ranking Productos] <= 5, 1, 0)
```

Participación % - Porcentaje de participación del producto

```dax
=DIVIDE(
    [Total Ventas],
    CALCULATE([Total Ventas], ALL(Productos)),
    0
)
```

Productos Únicos - Conteo de productos vendidos

```dax
=DISTINCTCOUNT(Ventas[producto_id])
```

</details>

#### 🎨 Medidas con Formato Inteligente

<details>
<summary>Ver medidas formateadas</summary>

Ventas Formato - Ventas con formato K, M, B

```dax
VAR T = ABS([Total Ventas])
RETURN
SWITCH(TRUE(),
    T >= 1000000000, FORMAT(T, "$#,,,.00 B"),
    T >= 1000000, FORMAT(T, "$#,,.00 M"),
    T >= 1000, FORMAT(T, "$#,.00 K"),
    FORMAT(T, "$#,##0.00")
)
```

Unidades Formato - Unidades con formato K, M

```dax
VAR T = [Total Unidades]
RETURN
SWITCH(TRUE(),
    T >= 1000000, FORMAT(T, "#,,.00 M"),
    T >= 1000, FORMAT(T, "#,.00 K"),
    FORMAT(T, "#,##0")
)
```

Crecimiento Formato - Porcentaje con formato

```dax
VAR T = [Crecimiento %]
RETURN
FORMAT(T, "+0.0%;-0.0%;0.0%")
```

</details>

#### 🌓 Medidas para Modo Oscuro/Claro
<details>
<summary>Ver medidas de tema visual</summary>

Tema Actual - Estado del switcher de tema

```dax
=SELECTEDVALUE(Tema[Tema], "Claro")
Color Fondo - Color de fondo según tema
dax
VAR TemaActual = [Tema Actual]
RETURN
SWITCH(
    TemaActual,
    "Oscuro", "#1a1a1a",
    "Claro", "#ffffff",
    "#ffffff"
)
```

Color Texto - Color de texto según tema

```dax
VAR TemaActual = [Tema Actual]
RETURN
SWITCH(
    TemaActual,
    "Oscuro", "#ffffff",
    "Claro", "#000000",
    "#000000"
)
```

</details>

#### 🖱️ Tooltips Personalizados
<details>
<summary>Ver medidas para tooltips HTML</summary>

Tooltip Producto - Información contextual del producto

```dax
VAR Producto = SELECTEDVALUE(Productos[producto_nombre])
VAR Ventas = [Total Ventas]
VAR Unidades = [Total Unidades]
VAR PrecioProm = [Precio Promedio]
VAR Ranking = [Ranking Productos]

RETURN
"
<div style='padding:10px; font-family:Segoe UI;'>
    <h3 style='margin:0; color:#2c3e50;'>" & Producto & "</h3>
    <hr style='border:1px solid #3498db; margin:5px 0;'>
    <p><strong>💰 Ventas:</strong> $" & FORMAT(Ventas, "#,##0.00") & "</p>
    <p><strong>📦 Unidades:</strong> " & FORMAT(Unidades, "#,##0") & "</p>
    <p><strong>💵 Precio Prom:</strong> $" & FORMAT(PrecioProm, "#,##0.00") & "</p>
    <p><strong>🏆 Ranking:</strong> #" & Ranking & "</p>
</div>
"
```
</details>

## 🖼️ Vistas Previas del Proyecto
<details>
<summary>📸 Ver Capturas de Pantalla</summary>

Vista Overview - Modo Claro
<img width="1638" height="845" alt="image" src="https://github.com/user-attachments/assets/2fd045ab-6628-42f5-b608-d509a9fd8bef" />

Vista Overview - Modo Oscuro
<img width="1643" height="838" alt="image" src="https://github.com/user-attachments/assets/008cd7b3-41ff-472e-b5c2-e322c75bb8d0" />

</details>

<details>
<summary>🎥 Ver Video Demostrativo</summary>

Demo del Dashboard
https://youtu.be/NiG0zqzfKKQ?si=0ELI7Pe8n3QeuA2L
</details>

## 👤 Autor
Giancarlo Barrantes

Business Intelligence Developer | Power BI Specialist


<a href="https://www.linkedin.com/in/gb25"><img width="70" height="20" alt="image" src="https://github.com/user-attachments/assets/e0d69586-c6f9-4f66-9a3d-bc8dfa146463" /></a>
<a href="https://www.instagram.com/gbarrantes25"><img width="70" height="20" alt="image" src="https://github.com/user-attachments/assets/68773029-5e0f-49da-92e9-fb93a223dd09" />
</a>
<a href="https://www.tiktok.com/@gbarrantes25"><img width="65" height="20" alt="image" src="https://github.com/user-attachments/assets/349c87c0-1f3a-4368-8517-64a6012565c0" /></a>
<a href="https://www.youtube.com/@gbarrantes25"><img width="70" height="20" alt="image" src="https://github.com/user-attachments/assets/d9e2cb69-29ec-47fc-93ae-30896a7b533d" />
</a>

## 📝 Licencia
Este proyecto está bajo la Licencia MIT - ver el archivo <a href="https://mit-license.org/">LICENSE</a> para más detalles.

## ⭐ Agradecimientos
Si este proyecto te resultó útil, considera darle una ⭐ en GitHub y compartirlo con otros profesionales de Business Intelligence.

<div align="center">
   Hecho por <a href="https://gbarrantes25.github.io/">Giancarlo Barrantes</a>
</div>
