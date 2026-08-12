## Objetivo
Consolidar los datos de productos, clientes y ventas de dos semanas de operación de un restaurante para construir indicadores de ingresos, frecuencia de compra y recurrencia de clientes que apoyen decisiones sobre el menú y la fidelización. El análisis no incluye costos, cantidades ni descuentos, por lo que no se calculan rentabilidad, utilidad ni margen.
## Datos utilizados
 
| Archivo | Descripción | Filas |
|---|---|---|
| `Restaurant-Foods.csv` | Catálogo de productos y precio unitario (`Food ID`, `Food Item`, `Price`) | 10 |
| `Restaurant-Customers.csv` | Base de clientes (`ID`, `First Name`, `Last Name`, `Gender`, `Company`, `Occupation`) | 1,000 |
| `Restaurant-Week1-Sales.csv` | Transacciones semana 1 (`Customer ID`, `Food ID`) | 250 |
| `Restaurant-Week2-Sales.csv` | Transacciones semana 2 (`Customer ID`, `Food ID`) | 250 |
 
**Modelo relacional:** `Food ID` y `ID` (cliente) son claves únicas en sus respectivas tablas de catálogo; cada registro de venta referencia exactamente un producto y un cliente (relación 1:N desde `foods`/`customers` hacia `sales`).

## Instrucciones de ejecución
 
1. Colocar los cuatro archivos CSV en en el drive con el nombre `data/` (o montar Google Drive si se ejecuta en Colab).
2. Abrir `lab_Sem2_DA.ipynb` en Google Colab o Jupyter Notebook.
3. Ejecutar las celdas en orden, de la primera a la última, sin modificaciones manuales (criterio de reproducibilidad).
4. El notebook:
   - Al ejecutar la primera celda de código va aparecer una ventana emergente de de Google drive para enlazar con el colab.
   - Después de haber hecho el enlace de la primera vez va a aparecer otra segunda donde se van enlazar todo lo que este contenido en el drive con el colab.
   - Después de enlazar el drive con el colab se van a ejecutar todas las celdas en orden 
   - Carga y valida las claves (`Food ID`, `Customer ID`) y sus referencias entre tablas. 
   - Consolida `foods`, `customers` y las ventas de ambas semanas mediante `merge` con `validate='many_to_one'`.
   - Calcula KPIs de ingresos, frecuencia de compra, recurrencia e ingresos por ocupación.
   - Replica el resumen semanal con una consulta SQL en SQLite y compara contra el resultado en Pandas.
   - Genera tres visualizaciones: desempeño del menú, comparación semanal y recurrencia de clientes.
## Principales hallazgos
 
- **Ingresos totales registrados:** $3,886.56 en las dos semanas (500 registros de venta).
- **Semana 1 vs. semana 2:** los ingresos bajaron ligeramente de $1,962.68 a $1,923.88 (250 registros cada semana); el ingreso promedio por registro cayó de $7.85 a $7.70.
- **Desempeño del menú:** el *Burrito* tiene la mayor frecuencia de compra (57 registros), pero el *Steak* genera los mayores ingresos ($1,249.50), porque su precio unitario es más alto y compensa su menor rotación.
- **Recurrencia:** de 221 clientes únicos en la semana 1, solo 46 (20.8%) volvieron a comprar en la semana 2.
- **Perfil por ocupación:** las cinco ocupaciones con mayor gasto agregado (Compensation Analyst, Sales Representative, Marketing Manager, Cost Accountant, Assistant Media Planner) presentan valores cercanos entre $72.69 y $116.68, sin una concentración marcada.
