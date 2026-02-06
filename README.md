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
- Creación de tabla calendario y tabla mode (mode light/dark)
- Medidas DAX:
  - ColourDesign:
  	- <details><summary>Abrir</summary>
		- <code>ColourBar = IF(SELECTEDVALUE(Mode[Activo])=1,"#00ffcc","#00A383")</code>
    	</details>
  - Images:
  	-  <details><summary>Abrir</summary>
		- <code>Img_IconGoal = 
	          SWITCH(TRUE(),
	            [#%Goal]>=0.95 && SELECTEDVALUE(Mode[Activo])=0,"https://raw.githubusercontent.com/Gbarrantes25/Supermarket-Sales-Dashboard/refs/heads/main/Images/ArribaLight.png",
	            [#%Goal]>=0.95 && SELECTEDVALUE(Mode[Activo])=1,"https://raw.githubusercontent.com/Gbarrantes25/Supermarket-Sales-Dashboard/refs/heads/main/Images/ArribaDark.png",
	            [#%Goal]>=0.85 && SELECTEDVALUE(Mode[Activo])=0,"https://raw.githubusercontent.com/Gbarrantes25/Supermarket-Sales-Dashboard/refs/heads/main/Images/FlechaLight.png",
	            [#%Goal]>=0.85 && SELECTEDVALUE(Mode[Activo])=1,"https://raw.githubusercontent.com/Gbarrantes25/Supermarket-Sales-Dashboard/refs/heads/main/Images/FlechaDark.png",
	            [#%Goal]<0.85 && SELECTEDVALUE(Mode[Activo])=0,"https://raw.githubusercontent.com/Gbarrantes25/Supermarket-Sales-Dashboard/refs/heads/main/Images/AbajoLight.png",
	            [#%Goal]<0.85 && SELECTEDVALUE(Mode[Activo])=1,"https://raw.githubusercontent.com/Gbarrantes25/Supermarket-Sales-Dashboard/refs/heads/main/Images/AbajoDark.png"
	          )
        </code><br>
		- <code>Img_IconGoal2 = 
	          SWITCH(TRUE(),
	            [#%GoalNotFilter]>=0.95 && SELECTEDVALUE(Mode[Activo])=0,"https://raw.githubusercontent.com/Gbarrantes25/Supermarket-Sales-Dashboard/refs/heads/main/Images/ArribaLight.png",
	            [#%GoalNotFilter]>=0.95 && SELECTEDVALUE(Mode[Activo])=1,"https://raw.githubusercontent.com/Gbarrantes25/Supermarket-Sales-Dashboard/refs/heads/main/Images/ArribaDark.png",
	            [#%GoalNotFilter]>=0.85 && SELECTEDVALUE(Mode[Activo])=0,"https://raw.githubusercontent.com/Gbarrantes25/Supermarket-Sales-Dashboard/refs/heads/main/Images/FlechaLight.png",
	            [#%GoalNotFilter]>=0.85 && SELECTEDVALUE(Mode[Activo])=1,"https://raw.githubusercontent.com/Gbarrantes25/Supermarket-Sales-Dashboard/refs/heads/main/Images/FlechaDark.png",
	            [#%GoalNotFilter]<0.85 && SELECTEDVALUE(Mode[Activo])=0,"https://raw.githubusercontent.com/Gbarrantes25/Supermarket-Sales-Dashboard/refs/heads/main/Images/AbajoLight.png",
	            [#%GoalNotFilter]<0.85 && SELECTEDVALUE(Mode[Activo])=1,"https://raw.githubusercontent.com/Gbarrantes25/Supermarket-Sales-Dashboard/refs/heads/main/Images/AbajoDark.png"
	          )
        </code><br>
		- <code>Img_Menubar = 
	            VAR light = "https://raw.githubusercontent.com/Gbarrantes25/Supermarket-Sales-Dashboard/refs/heads/main/Images/MenuLight.png"
	            VAR dark = "https://raw.githubusercontent.com/Gbarrantes25/Supermarket-Sales-Dashboard/refs/heads/main/Images/MenuDark.png"
	            RETURN IF(SELECTEDVALUE(Mode[Activo])=0,light,dark)
        </code><br>
		- <code>Img_MenubarClose = 
	            VAR light = "https://raw.githubusercontent.com/Gbarrantes25/Supermarket-Sales-Dashboard/refs/heads/main/Images/CerrarLight.png"
	            VAR dark = "https://raw.githubusercontent.com/Gbarrantes25/Supermarket-Sales-Dashboard/refs/heads/main/Images/CerrarDark.png"
	            RETURN IF(SELECTEDVALUE(Mode[Activo])=0,light,dark)
        </code>
    </details>
  - KPIS:
  	- <details><summary>Abrir</summary>
		- <code>#%AccuRankCategory = 
                VAR sales = CALCULATE([#TotalSales],ALL(DimProducts[Categoria]))
                RETURN DIVIDE([#AccuRankCategory],sales,0)
        </code><br>
		- <code>#%AccuRankProduct = 
				VAR sales = CALCULATE([#TotalSales],ALL(DimProducts[Producto]))
	            RETURN DIVIDE([#AccuRankProduct],sales,0)
        </code><br>
		- <code>#%ActiveCustomers = 
				VAR referencedate = LASTDATE(ALL(FactSales[Fecha]))
              	VAR startdate = referencedate - 90
              	VAR result = CALCULATE(
              		DISTINCTCOUNT(FactSales[Id_Cliente]),
              		FactSales[Fecha] >= startdate
              	)
	            VAR customers = DISTINCTCOUNT(FactSales[Id_Cliente])
              	RETURN DIVIDE(result,customers,0)
        </code><br>
		- <code>#%Goal = 
	              VAR _goal = DIVIDE([#TotalSales],[#TotalBudget],0)
	              VAR _result = IF(_goal>1,1,_goal)
	              RETURN _result
        </code><br>
		- <code>#%GoalNotFilter = 
	              VAR _sales = CALCULATE([#TotalSales],ALL(DimSeller[Vendedor]))
	              VAR _budget = CALCULATE([#TotalBudget],ALL(DimSeller[Vendedor]))
	              VAR _goal = DIVIDE(_sales,_budget,0)
	              VAR _result = IF(_goal>1,1,_goal)
	              RETURN _result
        </code><br>
		- <code>#%MoM = 
	              VAR _value = DIVIDE([#TotalSales],[#TotalSalesPreviusMonth],0)-1
	              RETURN IF(_value>=0,"▲"& FORMAT(_value,"#0.00%","En-US"),"▼"&FORMAT(_value,"#0.00%","En-Us"))
        </code><br>
		- <code>#%TotalSaleAll = 
	              VAR _customer = HASONEVALUE(DimCustomer[Nombre])
	              VAR _seller = HASONEVALUE(DimSeller[Vendedor])
	              VAR _branch = HASONEVALUE(DimBranch[Tienda])
	              RETURN 
	                  SWITCH(TRUE(),
	                      _customer,[#%TotalSalesCustomer],
	                      _seller,[#%TotalSalesSeller],
	                      _branch,[#%TotalSalesBranch])
        </code><br>
		- <code>#%TotalSalesBranch = 
	              VAR sales = CALCULATE([#TotalSales],ALL(DimBranch[Tienda]))
	              RETURN DIVIDE([#TotalSales],sales,0)
        </code><br>
		- <code>#%TotalSalesCategory = 
	              VAR sales = CALCULATE([#TotalSales],ALL(DimProducts[Categoria]))
	              RETURN DIVIDE([#TotalSales],sales,0)
        </code><br>
		- <code>#%TotalSalesCustomer = 
	              VAR sales = CALCULATE([#TotalSales],ALL(DimCustomer[Nombre]))
	              RETURN DIVIDE([#TotalSales],sales,0)
        </code><br>
		- <code>#%TotalSalesProducts = 
	              VAR sales = CALCULATE([#TotalSales],ALL(DimProducts[Producto]))
	              RETURN DIVIDE([#TotalSales],sales,0)
        </code><br>
		- <code>#%TotalSalesSeller = 
	              VAR sales = CALCULATE([#TotalSales],ALL(DimSeller[Vendedor]))
	              RETURN DIVIDE([#TotalSales],sales,0)
        </code><br>
		- <code>#AccuRankCategory = 
	              VAR tbt = ADDCOLUMNS(ALL(DimProducts[Categoria]),"Total",[#TotalSales],"Rank",RANKX(ALL(DimProducts[Categoria]),[#TotalSales],,DESC))
	              VAR ranknow = RANKX(ALL(DimProducts[Categoria]),[#TotalSales],,DESC)
	              RETURN
	                  SUMX(
	                      FILTER(tbt,[Rank]<=ranknow),[#TotalSales])
        </code><br>
		- <code>#AccuRankProduct = 
	              VAR tbt = ADDCOLUMNS(ALL(DimProducts[Producto]),"Total",[#TotalSales],"Rank",RANKX(ALL(DimProducts[Producto]),[#TotalSales],,DESC))
	              VAR ranknow = RANKX(ALL(DimProducts[Producto]),[#TotalSales],,DESC)
	              RETURN
	                  SUMX(
	                      FILTER(tbt,[Rank]<=ranknow),[#TotalSales])
      	</code><br>
		- <code>#AccuSales = TOTALYTD([#TotalSales],'Calendar'[Date])
      	</code><br>
    	- <code>#AverageTicket = 
	              VAR transactions = DISTINCTCOUNT(FactSales[Id_transaccion])
	              RETURN DIVIDE([#TotalSales],transactions,0)
      	</code><br>
		- <code>#AverageUnitPrice = AVERAGEX(DimProducts,DimProducts[Precio_Unit])</code><br>
		- <code>#CustomersPortfolio =
				VAR ReferenciaDate = LASTDATE(ALL(FactSales[Fecha]))
				VAR Stardate = ReferenciaDate-90
				VAR Customers = CALCULATE( DISTINCTCOUNT(FactSales[Id_Cliente] ), FactSales[Fecha] < StartDate)
				RETURN Customers
		</code><br>
		- <code>#GAPSelling = [#TotalSales]-[#TotalBudget]
		</code><br>
		- <code>#InactiveCustomers = 
				VAR referencedate = LASTDATE(ALL(FactSales[Fecha]))
				VAR startdate = referencedate - 90
				VAR result = CALCULATE(
					DISTINCTCOUNT(FactSales[Id_Cliente]),
					FactSales[Fecha] >= startdate
				)
				VAR customers = DISTINCTCOUNT(FactSales[Id_Cliente])
				RETURN customers-result
		</code><br>
		- <code>#MoMSales = [#TotalSales]-[#TotalSalesPreviusMonth]</code><br>
		- <code>#NewCustomers = 
				VAR ReferenceDate = LASTDATE(ALL(FactSales[Fecha]))
				VAR Stardate = ReferenceDate-90
				VAR tbtlongtimecustomers = CALCULATETABLE(VALUES(FactSales[Id_Cliente]),FactSales[Fecha]<Stardate)
				VAR tbtactivecustomers = CALCULATETABLE(VALUES(FactSales[Id_Cliente]),FactSales[Fecha]>=Stardate)
				VAR tbtnewcustomers = COUNTROWS(EXCEPT(tbtactivecustomers,tbtlongtimecustomers))
				RETURN tbtnewcustomers
		</code><br>
		- <code>#PurchaseFrequency = 
				DIVIDE(DISTINCTCOUNT(FactSales[Id_transaccion]),DISTINCTCOUNT(FactSales[Id_Cliente]),0)
		</code><br>
		- <code>#QuantityProducts = DISTINCTCOUNT(FactSales[Id_Producto])</code><br>
		- <code>#TotalBudget = 
				VAR SelectedBranch = SELECTEDVALUE(DimBranch[Id_Tienda])
				VAR ppto = SUMX(FILTER(FactSalesVsPPTO,FactSalesVsPPTO[Id_Tienda]=SelectedBranch),FactSalesVsPPTO[Presupuesto])
				RETURN IF(ISBLANK(ppto),SUMX(FactSalesVsPPTO,FactSalesVsPPTO[Presupuesto]),ppto)
		</code><br>
		- <code>#TotalSales = SUMX(FactSales,FactSales[Cantidad]*RELATED(DimProducts[Precio_Unit]))</code><br>
		- <code>#TotalSalesPreviusMonth = CALCULATE([#TotalSales],DATEADD('Calendar'[Date],-1,MONTH))</code><br>
		- <code>#Transactions = COALESCE(DISTINCTCOUNT(FactSales[Id_transaccion]),0)</code><br>
		- <code>#Units = SUMX(FactSales,FactSales[Cantidad])</code><br>
		- <code>#UnitsPerTransaction = DIVIDE([#Units],[#Transactions],0)</code><br>
		- <code>#YearvsLY = 
				VAR lastyear = CALCULATE([#TotalSales],SAMEPERIODLASTYEAR('Calendar'[Date]))
				VAR yearnow = [#TotalSales]
				RETURN DIVIDE(yearnow-lastyear,lastyear,0)</code></details>
  - KPIs Format:
    - <details><summary>Abrir</summary>
		- <code>AverageTicketFormat = Fx_FormatNumberUSD([#AverageTicket])</code><br>
		- <code>DiffSalesMonthFormat = Fx_FormatNumberUSD([#MoMSales])</code><br>
		- <code>GAPFormat = Fx_FormatNumberUSD([#GAPSelling])</code><br>
		- <code>QuantityProductsFormat = Fx_FormatNumber([#QuantityProducts])</code><br>
		- <code>TotalBudgetFormat = Fx_FormatNumberUSD([#TotalBudget])</code><br>
		- <code>TotalSalesFormat = Fx_FormatNumberUSD([#TotalSales])</code><br>
		- <code>UnitsFormat = Fx_FormatNumber([#Units])</code>
	</details>
  - VisualesHTML:
   	- <details><summary>Abrir</summary>
		- CardAverageTicket_GAPSelling = https://uiverse.io/vamsidevendrakumar/soft-shrimp-94 <br>
		- CardClientesAntiguos_Nuevo = https://uiverse.io/vamsidevendrakumar/soft-shrimp-94 <br>
		- CardClientesInactivos_%Activos = https://uiverse.io/vamsidevendrakumar/soft-shrimp-94 <br>
		- CardSales_Budget = https://uiverse.io/vamsidevendrakumar/soft-shrimp-94 <br>
		- CardUnits_Products = https://uiverse.io/vamsidevendrakumar/soft-shrimp-94
	</details>
  - Others:
       - <code>FilterBranchSeller = COUNT(FactSales[Id_Vendedor])</code>
			
- Diseño Interactivo: Uso de paginado para navegación, tooltips, marcadores y segmentación de datos.

## 🖼️ Vistas Previas del proyecto
<details>
  <summary>Capturas</summary>

  <img width="1894" height="1064" alt="image" src="https://github.com/user-attachments/assets/be13fcfc-a3b5-4dca-8e7d-14471dcb7072" />
  <img width="1883" height="1054" alt="image" src="https://github.com/user-attachments/assets/fd9e6fe1-4336-4bb8-8c04-e0a22c7adaad" />
  <img width="1874" height="1049" alt="image" src="https://github.com/user-attachments/assets/c701d2ff-c488-4699-ab92-5839d05dfec3" />
  <img width="1881" height="1045" alt="image" src="https://github.com/user-attachments/assets/071ede32-2c46-4135-93de-5f1b19ad0c26" />
</details>

<details>
  <summary>Video</summary>
  https://youtu.be/NiG0zqzfKKQ?si=KqO9DkIukfFloHaU
</details>



## 👤 Autor
- Giancarlo Barrantes
- Lima, Perú
- [Linkedin](https://www.linkedin.com/in/gb25/)
