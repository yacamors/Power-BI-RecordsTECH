Dashboard de Análisis de Margen y Beneficio en Power BI
Este repositorio contiene el proyecto de visualización de datos en Power BI enfocado en analizar márgenes y beneficios basados en datos de ventas por país, cliente y marca.

Descripción del Proyecto
El objetivo de este proyecto es proporcionar una herramienta interactiva para analizar y visualizar datos financieros clave, incluyendo ingresos, gastos, beneficios y márgenes, utilizando Power BI. El dashboard incluye múltiples visualizaciones que permiten a los usuarios explorar y entender mejor los datos de ventas desde diferentes perspectivas.

Características Principales
Tarjetas de Resumen: Total de ingresos, gastos, beneficios y margen global.
Tablas Detalladas:
Por país: Beneficios y margen.
Por cliente: Beneficios y margen.
Por marca: Beneficios y margen.
Gráficos de Barras Apiladas: Comparativa de márgenes y beneficios entre diferentes categorías.
Líneas de Tendencia: Seguimiento de la evolución de beneficios y márgenes a lo largo del tiempo.
Filtros Interactivos: Permite filtrar datos por año, país, cliente y marca para análisis específicos.
Medidas Utilizadas

DAX:

Beneficios = [Total-Ingresos] - [Total-Gastos]

Ganancia Neta por Marca = 
VAR TotalIngresos = SUM('Registros Tecnologicos'[Ingresos])
VAR TotalGastos = SUM('Registros Tecnologicos'[Gastos])
VAR GananciaNeta = TotalIngresos - TotalGastos
RETURN
DIVIDE(GananciaNeta, COUNTROWS(VALUES('Registros Tecnologicos'[Marca])))


Ingresos Acumulados por Cliente = 
CALCULATE(
    SUM('Registros Tecnologicos'[Ingresos]),
    ALLEXCEPT('Registros Tecnologicos', 'Registros Tecnologicos'[Cliente])
)

Ingresos Acumulados por Fecha = 
CALCULATE(
    SUM('Registros Tecnologicos'[Ingresos]),
    FILTER(
        ALLSELECTED('Registros Tecnologicos'),
        'Registros Tecnologicos'[Fecha] <= MAX('Registros Tecnologicos'[Fecha])
    )
)

Margen (%) = DIVIDE([Beneficios], [Total-Ingresos], 0)

Promedio Ingresos por País = AVERAGEX(VALUES('Registros Tecnologicos'[País]), CALCULATE(SUM('Registros Tecnologicos'[Ingresos])))

Total-Gastos = SUM('Registros Tecnologicos'[Gastos])

Total-Ingresos = SUM('Registros Tecnologicos'[Ingresos])

Explicación de Medidas
Beneficios: Esta medida calcula el beneficio neto restando los gastos totales de los ingresos totales.

Ganancia Neta por Marca: Calcula la ganancia neta promedio por marca en función de los ingresos y gastos totales.

Ingresos Acumulados por Cliente: Permite ver los ingresos acumulados para cada cliente en el contexto actual de filtrado.

Ingresos Acumulados por Fecha: Muestra los ingresos acumulados hasta la fecha más reciente disponible.

Margen (%): Calcula el margen como porcentaje de los beneficios sobre los ingresos totales, útil para entender la rentabilidad.

Promedio Ingresos por País: Ofrece una visión promedio de los ingresos por país, facilitando comparaciones entre regiones.

Total-Gastos y Total-Ingresos: Proporcionan las sumas totales de gastos e ingresos, fundamentales para los cálculos financieros básicos.

