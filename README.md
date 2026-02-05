# Supermarket Dashboard


## 📃 Descripción General
Este proyecto fue elaborado con información ficticia de un supermercado. Se empleó una base de datos remota alojada en Supabase; para la parte gráfica se empleó "tooltips", menú de navegación interactivo, y switcher para modo noche/día.


## 📊 Contenido del proyecto
- Página "Overview": Contiene una vista general del análisis.
- Página "Branch": Contiene el análisis por sucursal del supermecado.
- Página "Customer": Contiene el análisis de los mejores clientes.
- Página "Seller": Contiene el análisis por vendedor.
- Página "Products" Contiene el análisis de las categorías y mejores productos.


## 🛠️ Herramientas y Tecnologías Utilizadas
- Visualización: Power BI Desktop.
- Supabase (https://supabase.com/)
- Fuente de Datos:
  - [DimBranch.csv](https://github.com/Gbarrantes25/Supermarket-Sales-Dashboard-PowerBI/blob/main/Data%20Source/DimBranch.csv)
  - [DimCustomer.csv](https://github.com/Gbarrantes25/Supermarket-Sales-Dashboard-PowerBI/blob/main/Data%20Source/DimCustomer.csv)
  - [DimProducts.csv](https://github.com/Gbarrantes25/Supermarket-Sales-Dashboard-PowerBI/blob/main/Data%20Source/DimProducts.csv)
  - [DimSeller.csv](https://github.com/Gbarrantes25/Supermarket-Sales-Dashboard-PowerBI/blob/main/Data%20Source/DimSeller.csv)
  - [FactSales.csv](https://raw.githubusercontent.com/Gbarrantes25/Supermarket-Sales-Dashboard-PowerBI/refs/heads/main/Data%20Source/FactSales.csv)
  - [DimPPTO.csv](https://github.com/Gbarrantes25/Supermarket-Sales-Dashboard-PowerBI/blob/main/Data%20Source/DimPPTO.csv)
    
- Lenguajes: DAX para las medidas calculadas y Power Query (Lenguaje M) para la transformación de datos.


## ⚙️ Configuración del Entorno
- Software Necesario: Power BI Desktop, PostgreSQL, Supabase y OBDC 64 bits.
- Instalar [PostgreSQL](https://www.postgresql.org/download/) en tu PC.
- Supabase creación de vista:
  - Registrarse en Supabase, crear un proyecto y las tablas, luego importar la información en formato .csv.
  - Crear la vista de tabla PPTO vs Sales:
    <code>
    DROP VIEW IF EXISTS "FactSalesVsPPTO";
    CREATE VIEW "FactSalesVsPPTO" AS(
    SELECT 
      f."Id_Tienda",
      EXTRACT(YEAR FROM f."Fecha") AS Año,
      EXTRACT(MONTH FROM f."Fecha") AS Mes,
      SUM(f."Total") AS Ventas,
      COALESCE(MAX(p."PPTO"), 0) AS Presupuesto
    FROM "FactSales" f
    LEFT JOIN "DimPPTO" p 
      ON TO_CHAR(f."Fecha", 'YYYYMM') = (p."Anio"::text || LPAD(p."Mes"::text, 2, '0')) AND f."Id_Tienda" = p."Id_Tienda"
      GROUP BY 1, 2, 3
      ORDER BY 1, 2, 3 ASC);
    NOTIFY pgrst, 'reload schema';
    </code>
- Supabase credenciales:
  -  Nos dirigimos al apartado "Connect to your project"/"Connection String"/"Transaction Pooler". Esto logrará que obtengas unas credenciales similares a esta:
  - "postgresql://postgres.kpjdjiykitgolfayqmfd:[YOUR-PASSWORD]@aws-1-us-east-1.pooler.supabase.com:6543/postgres", donde se desglosará de la siguiente manera:
    - Database: postgres
    - Server: aws-1-us-east-1.pooler.supabase.com
    - Port: 6543
    - Usuario: postgres.kpjdjiykitgolfayqmfd
    - Contraseña: (La misma que tiene tu proyecto).
- Configurando el OBDC 64 bits:
  <details>
    <summary>Mini Guía</summary>
    - Buscamos en nuestra PC ODBC 64bits.
      <img width="1025" height="726" alt="image" src="https://github.com/user-attachments/assets/df501f19-5e11-4794-9aca-dc5d24e3cf8f" />
    - Clic en "Agregar" y buscamos el driver PostgreSQL ODBC Driver ANSI.
      <img width="1095" height="707" alt="image" src="https://github.com/user-attachments/assets/df633e64-851a-4d4b-9fe8-e487a1aee2ad" />
    - En la ventana le colocaremos las credenciales que vimos anteriormente (el Data Source puede tener cualquier nombre). No te olvides de seleccionar "Requiere" en SSL Mode. Finalmente testeas tu conexión, debe salir como "Conexión exitosa".
      <img width="797" height="458" alt="image" src="https://github.com/user-attachments/assets/16d88672-50d7-46ab-affb-e619adf58a38" />
      <img width="797" height="446" alt="image" src="https://github.com/user-attachments/assets/cc43b3ee-f13d-4211-a267-e2cd008be1e5" />
      <img width="736" height="489" alt="image" src="https://github.com/user-attachments/assets/e92d97aa-cf10-47b0-acc7-feae6827b828" />
    - En Power BI, nos vamos a obtenber datos y seleccionados la conexión que creamos en el ODBC (si gustas puedes realizar una consulta SQL para realizar una transacción). En caso pida una credencial adicional, solo es cuestión de darle el usuario y contraseña.
      <img width="1156" height="341" alt="image" src="https://github.com/user-attachments/assets/26f634eb-b096-41be-8515-9741bc1196d5" />
      <img width="1191" height="887" alt="image" src="https://github.com/user-attachments/assets/fd384188-2925-4599-8349-22277dda5a44" />
      <img width="574" height="876" alt="image" src="https://github.com/user-attachments/assets/5278ff10-5d09-4fc3-b696-8cee1e361159" />

    
  </details>
- Instalación:
  - Una vez realizada la instalación de PostgreSQL (o su driver ODBC) y configuración anterior, proceder al siguiente paso.
  - Descargar [Supermarket Sales.pbix](https://github.com/Gbarrantes25/Supermarket-Sales-Dashboard-PowerBI/blob/main/Supermarket%20Sales.pbix) con Power BI Desktop.
  - Entrar a Inicio y darle click a "Actualizar".


## 📂 Estructura del Repositorio
<code>.
  ├── Data Source                  # Contiene las tablas en formato .csv
  |── Images                       # Carpeta donde se alojan los íconos.
  ├── Supermarket Sales.pbix       # Archivo que será ejecutado con Power BI Desktop.
  └── README.md                    # Este archivo.
</code>


## ✅ Características Principales
- Transformaciones en Power Query: Se realizaron procesos de limpieza y modelado de datos para optimizar el rendimiento.
- Medidas DAX: Se implementaron cálculos para los KPI's del Revenue Management.
  - <code>%Occ = DIVIDE([Total RNs],[RNs Disponibles],0)</code>
  - <code>Conteo Días = COUNT(Calendario[Date])</code>
  - <code>RNs Disponibles = SUMX(Habitaciones,Habitaciones[Cantidad de Habitaciones]*[Conteo Días])</code>
  - <code>ADR = DIVIDE([Total Revenue],[Total RNs],0)</code>
  - <code>Total Revenue = SUMX(Reservaciones,Reservaciones[RN]*Reservaciones[Precio Unitario])</code>
  - <code>Total RNs = SUM(Reservaciones[RN])</code>
  - <code>RevPar = [ADR]*[%Occ]</code>
  - <code>Total A&B = SUM(Reservaciones[A&B])</code>
- Medidas Formateadas DAX: Se implementaron medidas formateadas para visualizar de manera corta los números extensos ("B", "M" y "K").
  - <code>ADR*** = 
          VAR T = ABS([ADR])
          RETURN
              SWITCH(TRUE(),
                  T >= 1000000000, FORMAT(T, "$#,,,.00 B"),
                  T >= 1000000, FORMAT(T, "$#,,.00 M"),
                  T >= 1000, FORMAT(T, "$#,.00 K"),
                      SUBSTITUTE(FORMAT(T, "$#.00"),",","."))
    </code>
  - <code>RNs*** = 
          VAR T = [Total RNs]
          RETURN
              SWITCH(TRUE(),
                  T >= 1000000000, FORMAT(T, "#,,,.00 B"),
                  T >= 1000000, FORMAT(T, "#,,.00 M"),
                  T >= 1000, FORMAT(T, "#,.00 K"),
                      FORMAT(T,"0"))
    </code>
  - <code>Revenue*** = 
          VAR T = [Total Revenue]
          RETURN
              SWITCH(TRUE(),
                  T >= 1000000000, FORMAT(T, "$#,,,.00 B"),
                  T >= 1000000, FORMAT(T, "$#,,.00 M"),
                  T >= 1000, FORMAT(T, "$#,.00 K"),
                      FORMAT(T,"$0.00"))
    </code>
  - <code>A&B*** = 
          VAR T = [Total A&B]
          RETURN
              SWITCH(TRUE(),
                  T >= 1000000000, FORMAT(T, "$#,,,.00 B"),
                  T >= 1000000, FORMAT(T, "$#,,.00 M"),
                  T >= 1000, FORMAT(T, "$#,.00 K"),
                      FORMAT(T,"$0"))
    </code>
- Diseño Interactivo: Uso de paginado para navegación y segmentación de datos.


## 🖼️ Vistas Previas del proyecto
<details>
  <summary>Capturas</summary>


  Página "Regions"


  ![Animation1](https://github.com/user-attachments/assets/0d3de5f3-ae65-43e6-abc6-72e97e6a6be9)


  Página "Hotel Branches"


  ![Animation2](https://github.com/user-attachments/assets/0d347ecd-a7cb-496e-940e-a18ad0723a01)


</details>

<details>
  <summary>Video</summary>
  https://www.youtube.com/watch?v=TMqiaGSsMXk
</details>



## 👤 Autor
- Giancarlo Barrantes
- Lima, Perú
- [Linkedin](https://www.linkedin.com/in/gb25/)
