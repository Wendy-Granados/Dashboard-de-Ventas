# Dashboard-de-Ventas
Dashboard interactivo desarrollado en Power BI para analizar el desempeño comercial a partir de indicadores de ventas, costos, descuentos y margen de utilidad. El reporte integra información de clientes, productos, ubicaciones y equipos de venta, permitiendo identificar tendencias y comparar resultados mediante filtros y visualizaciones dinámicas.
# Dashboard de Ventas y Rentabilidad

## Descripción

Dashboard desarrollado en Power BI para analizar el desempeño de las ventas, costos, descuentos y utilidad de una empresa desde diferentes dimensiones comerciales.

El reporte permite consultar indicadores generales y analizar su comportamiento por periodo, región, equipo de ventas, productos y clientes.

## Objetivo

Centralizar y visualizar información comercial para facilitar el análisis de:

- Ventas totales.
- Costos y utilidad.
- Descuentos aplicados.
- Cantidad de productos vendidos.
- Comportamiento de las ventas a través del tiempo.
- Desempeño de las regiones.
- Comparación entre ventas y costos por equipo de ventas.

## Preguntas que responde el dashboard

- ¿Cuál es el total de ventas?
- ¿Cuál es el costo total asociado a las ventas?
- ¿Cuál es el margen de utilidad?
- ¿Cuál es el promedio de descuento aplicado?
- ¿Cuántos productos se han vendido?
- ¿Cómo se comportan las ventas a lo largo del tiempo?
- ¿Qué regiones concentran mayores ventas?
- ¿Qué equipos de ventas generan mayores ventas?
- ¿Cómo se comparan las ventas y los costos entre los equipos de ventas?
- ¿Qué productos, clientes y ubicaciones forman parte de las operaciones analizadas?

## Fuente y estructura de datos

El modelo está compuesto por una tabla principal de hechos y tablas auxiliares relacionadas mediante claves.

### Tabla principal: Ventas

Contiene el detalle de las operaciones comerciales.

Campos principales:

- Costo
- Clave Cliente
- Descuento
- Ubicación Clave
- Fecha de Orden
- Clave Producto
- Utilidad
- Cantidad
- Clave Vendedor
- Ventas
- Fecha Envío

### Tablas auxiliares

#### Clientes

- Clave Cliente
- Nombre Cliente
- Email
- Valor Cliente
- Primer Nombre
- Apellido

#### Productos

- Clave Producto
- Categoría
- Imagen Categoría
- Nombre Producto
- Sub-categoría

#### Fechas

- Fecha completa
- Día Mes
- Día Semana
- Nombre Semana
- Nombre Mes
- Mes Número
- Mes Abreviado
- Año

#### Ubicación

- Clave Ubicación
- Ciudad
- Código Postal
- Región
- Estado

#### Vendedores

- Clave Vendedores
- Nombre
- Apellido
- Nombre Completo
- Imagen Vendedor
- Email
- Equipo de Venta

## Limpieza y preparación de datos

Antes de construir las visualizaciones se revisó la calidad de los datos para identificar inconsistencias que pudieran afectar los cálculos, relaciones o resultados del dashboard.

### Criterios aplicados

#### 1. Revisión de valores nulos

Los valores nulos no se eliminan automáticamente.

Primero se debe determinar si la ausencia de información representa:

- Un dato realmente inexistente.
- Un campo opcional.
- Un error de captura.
- Una relación incompleta entre tablas.

Por ejemplo, si una columna contiene un valor vacío en algunos registros, pero sí existe información en otros, se debe revisar el significado del campo antes de sustituir o eliminar los valores.

La decisión debe depender del uso que tendrá la columna en el dashboard:

- Si es una clave utilizada para relacionar tablas, un valor nulo puede generar registros sin correspondencia y debe investigarse.
- Si es un atributo descriptivo que no afecta los cálculos, puede conservarse como vacío o clasificarse como "Sin información", dependiendo del análisis.
- Si es una variable numérica utilizada en cálculos, debe determinarse si el vacío representa cero o ausencia de información. **No deben sustituirse automáticamente los nulos por cero.**

#### 2. Revisión de tipos de datos

Se verificó que cada campo tuviera un tipo de dato adecuado para su función:

- Fechas → tipo fecha.
- Cantidades → número entero.
- Ventas, costos y utilidad → valores numéricos.
- Descuentos → valores numéricos que puedan utilizarse en cálculos porcentuales.
- Claves → tipo consistente entre las tablas relacionadas.
- Texto → campos descriptivos y categóricos.

#### 3. Revisión de claves

Las claves utilizadas para relacionar las tablas deben mantener:

- El mismo tipo de dato.
- El mismo formato.
- Valores consistentes.
- Ausencia de duplicados cuando funcionan como identificadores únicos.

Las claves de las tablas auxiliares deben permitir identificar correctamente cada registro relacionado con la tabla de Ventas.

#### 4. Revisión de duplicados

Se revisaron posibles registros duplicados para evitar que una misma operación fuera contabilizada más de una vez.

La eliminación de duplicados debe realizarse únicamente cuando se confirme que los registros representan la misma operación y no transacciones legítimas repetidas.

#### 5. Revisión de valores atípicos o inconsistentes

Se deben revisar valores que puedan afectar la interpretación de los indicadores, por ejemplo:

- Ventas negativas.
- Cantidades inusuales.
- Descuentos fuera del rango esperado.
- Costos o utilidades inconsistentes.
- Fechas de envío anteriores a la fecha de orden.

Los valores atípicos no deben eliminarse únicamente por ser diferentes; primero debe determinarse si representan una operación válida o un error en los datos.

## Modelo de datos
<img width="1162" height="493" alt="Captura de pantalla 2026-09-11 115551" src="https://github.com/user-attachments/assets/43cfd2b8-7533-42c5-84bf-dc7767118545" />

Se utilizó un modelo basado en una tabla principal de hechos:

**Ventas**

Relacionada con las siguientes tablas dimensionales:

- Ventas → Clientes mediante `Clave Cliente`
- Ventas → Productos mediante `Clave Producto`
- Ventas → Fechas mediante `Fecha de Orden`
- Ventas → Ubicación mediante `Ubicación Clave`
- Ventas → Vendedores mediante `Clave Vendedor`

La tabla Ventas concentra las transacciones y las tablas auxiliares proporcionan información descriptiva para realizar análisis por diferentes dimensiones.

## Indicadores principales

El dashboard contiene tarjetas para visualizar:

- **Total de Ventas**
- **Promedio de Descuento (%)**
- **Margen de Utilidad (%)**
- **Cantidad de Productos**
- **Total de Costos**

Las métricas fueron construidas mediante medidas DAX para permitir que los resultados respondan dinámicamente a los filtros y segmentaciones aplicados.

## Filtros y segmentaciones

### Filtros por categoría

- Muebles
- Oficina
- Tecnología

### Segmentación temporal

Se incorporó un filtro de fecha para analizar los resultados dentro de diferentes periodos.

## Visualizaciones

### Embudo — Total de Ventas por Región

Permite identificar y comparar la participación de las diferentes regiones en las ventas totales.

### Gráfico de barras agrupadas — Ventas vs. Costos por Equipo de Venta

Compara el total de ventas y costos generado por cada equipo de ventas.

Permite identificar diferencias entre el volumen de ventas y los costos asociados.

### Gráfico de áreas — Total de Ventas por Mes

Muestra la evolución de las ventas utilizando el mes como dimensión temporal.

La tabla de fechas permite ordenar correctamente los meses mediante el número de mes y evitar que los nombres abreviados se presenten en orden alfabético.

## Tablas de detalle

El modelo también permite consultar información relacionada con:

- Clientes.
- Productos.
- Ubicaciones.
- Vendedores.
- Fechas.
- Transacciones de ventas.

Estas tablas proporcionan el nivel de detalle necesario para complementar el análisis de los indicadores y visualizaciones.

## Medidas DAX

Las medidas utilizadas en el dashboard incluyen cálculos para:

- Total de Ventas.
- Promedio de Descuento.
- Margen de Utilidad.
- Cantidad de Productos.
- Total de Costos.

> Las expresiones DAX utilizadas se documentan de forma independiente para facilitar su consulta y mantenimiento.

## Resultado

El dashboard permite integrar información de ventas, costos, descuentos y utilidad en una sola vista interactiva.

<img width="758" height="426" alt="Captura de pantalla 2026-09-11 115718" src="https://github.com/user-attachments/assets/4c51e382-557f-40d2-97ca-5f0bddfeb528" />

La combinación de indicadores, filtros, dimensiones comerciales y análisis temporal facilita la identificación de tendencias y diferencias en el desempeño de las ventas.

## Alcance del proyecto
Integración y preparación de datos de ventas.
Construcción de un modelo de datos relacional.
Creación de medidas DAX para los principales indicadores.
Diseño de visualizaciones para el análisis de ventas, costos y utilidad.
Incorporación de filtros por categoría y periodo.
Análisis de información por región, equipo de ventas, productos y clientes.

Nota: Los datos utilizados en este proyecto son de práctica y se emplearon con fines demostrativos y de aprendizaje.

## Aprendizajes

- Importancia de realizar una revisión de calidad antes de construir las visualizaciones.
- Uso de criterios para determinar cuándo conservar, transformar o investigar valores nulos.
- Importancia de mantener consistencia en las claves utilizadas para relacionar tablas.
- Aplicación de un modelo de datos basado en una tabla de hechos y tablas dimensionales.
- Uso de una tabla de fechas para realizar análisis temporales correctamente.
- Creación de medidas DAX para generar indicadores dinámicos.
- Selección de visualizaciones de acuerdo con la pregunta que se busca responder.
