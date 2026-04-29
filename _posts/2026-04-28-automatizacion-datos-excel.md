---
layout: post
title: "Análisis y Automatización de Datos: Ingeniería sobre Microsoft Excel"
date: 2026-04-28
categories: [data-automation, proyectos]
tags: [excel, dashboards, análisis-de-datos, business-intelligence]
---

Este proyecto demuestra la capacidad de transformar flujos de datos crudos en herramientas de decisión estratégica mediante la **arquitectura de dashboards dinámicos y programación lógica en Excel**, garantizando procesos escalables y eficientes.

### 📂 Fase 1: Ingesta y Normalización en Excel (CSV)

El proceso comienza con la recepción de información en formato plano (CSV). Como se observa en la siguiente comparativa, los datos iniciales carecen de estructura, lo que dificulta cualquier análisis técnico:

![Estructura de datos crudos CSV](/assets/images/csv-datos-crudos.png)
*Estado inicial: Información agrupada en una sola cadena de texto separada por comas.*

Para transformar este caos en una arquitectura funcional dentro de Excel, apliqué un flujo de normalización técnica:

1.  **Parseo con "Texto a columnas":** Segmentación precisa de variables para asignar cada dato a su celda correspondiente.
2.  **Enriquecimiento Geográfico:** Uso de tipos de datos de Excel para extraer automáticamente la **Población** basada en el país de origen.
3.  **Lógica Temporal:** Conversión de fechas e implementación de la **Función HOY** para reportes actualizados en tiempo real.
4.  **Generación de Atributos:** Uso de **Relleno Rápido (Flash Fill)** para normalizar registros y crear códigos únicos de identificación.

![Tabla normalizada en Excel](/assets/images/tabla-limpia-excel.png)
*Resultado final: Estructura de datos optimizada, limpia y lista para el análisis dinámico.*

### 🧠 Fase 2: Lógica Aritmética y Agregación Multicriterio en Excel

Una vez estructurada la base, establecí las reglas de negocio para la extracción de KPIs mediante funciones de agregación avanzada como `SUMAR.SI.CONJUNTO`, permitiendo segmentaciones precisas basadas en múltiples variables de forma simultánea.

![Funciones de suma avanzada en Excel](/assets/images/funciones-suma-excel.png)
*Implementación de fórmulas complejas para la generación de reportes dinámicos basados en criterios de negocio.*

### 🔍 Fase 3: Inteligencia de Búsqueda y Recuperación de Datos

Implementé una lógica de recuperación de información automatizada mediante **BUSCARV**, configurando motores de búsqueda exacta para extraer atributos de forma instantánea al seleccionar un identificador único, garantizando la integridad referencial.

![Motor de búsqueda con BUSCARV en Excel](/assets/images/motor-busqueda-excel.png)
*Implementación de la función BUSCARV para la recuperación dinámica de atributos.*

### ⚖️ Fase 4: Lógica Condicional y Categorización Automática

Desarrollé un motor de reglas mediante la **Función SI** con referencias absolutas para clasificar activos automáticamente bajo umbrales de negocio (ej. "Crítico" vs. "Aceptable"), modificables desde una tabla de parámetros centralizada.

![Lógica condicional con Función SI en Excel](/assets/images/funcion-si-excel.png)
*Uso de la Función SI para la categorización dinámica de datos basada en parámetros configurables.*

### 📊 Fase 5: Estructuración de Objetos "Tabla" para Dashboards

Realicé la transición de rangos simples a **Tablas oficiales de Excel** (`Ctrl + T`), asegurando que cualquier nuevo registro se integre automáticamente en el análisis y mejorando la auditoría del sistema mediante referencias estructuradas.

![Estructura de Tabla dinámica en Excel](/assets/images/estructura-tabla-excel.png)
*Conversión de datos normalizados en una Tabla oficial, habilitando la escalabilidad del análisis.*

### 📅 Fase 6: Preparación de Dimensiones y Formateo Avanzado

Enriquecí las dimensiones de la tabla anidando funciones como `=NOMPROPIO(TEXTO(celda, "mmmm"))` para extraer meses capitalizados estéticamente, asegurando que las etiquetas en la visualización final sean profesionales.

![Funciones de texto y tiempo en Excel](/assets/images/funciones-texto-tiempo.png)
*Uso de funciones anidadas para la preparación de dimensiones temporales de alto impacto visual.*

### 📈 Fase 7: Arquitectura de Reportes con Tablas Dinámicas

Con la data enriquecida, procedí a la creación de múltiples **Tablas Dinámicas** para obtener una visión 360° del negocio, desglosando resultados por variables críticas: Mes, Cliente, Región, Producto y Vendedor.

![Agregación de datos con Tablas Dinámicas](/assets/images/tablas-dinamicas-excel.png)
*Configuración de Tablas Dinámicas como motor analítico central del proyecto.*

### 🖱️ Fase 8: Interactividad y Control de Datos Multifiltro

Para convertir los reportes en una herramienta de exploración dinámica, integré dos niveles de control interactivo vinculados a todo el ecosistema de datos:

*   **Segmentación de Datos (Slicers):** Inserción de filtros táctiles para navegar por categorías específicas con un solo clic.
*   **Escala de Tiempo (Timeline):** Implementación de un control cronológico dedicado para segmentar la información por años o meses, permitiendo auditorías temporales rápidas y fluidas.

![Segmentación de datos interactiva en Excel](/assets/images/segmentacion-datos-excel.png)
*Implementación de segmentadores y escalas de tiempo para el control total y sincronizado de la información.*

### 🎨 Fase 9: Diseño de Interfaz y Maquetación (Wireframing)

Desarrollé un boceto estructural utilizando figuras para definir la jerarquía de información y asegurar una experiencia de usuario (UX) fluida antes de la integración visual definitiva.

![Boceto de Dashboard en Excel](/assets/images/boceto-dashboard-excel.png)
*Maquetación visual en Dark Mode y definición estratégica de espacios para la interfaz final.*

### 🚀 Fase 10: Dashboard Interactivo de Alto Impacto

La etapa final consistió en la integración de gráficas dinámicas sobre la interfaz maquetada, logrando un centro de mando integral con las siguientes características:

*   **KPIs de Rendimiento Humano:** Visualización del TOP 5 de vendedores con montos y perfiles integrados.
*   **Análisis Temporal y Regional:** Gráficos de barras para identificar tendencias estacionales y zonas geográficas de mayor valor.
*   **Distribución de Mercado:** Gráfico de anillos para visualizar la cuota de participación por marca.
*   **Navegación Centralizada:** Control global del rendimiento mediante la escala de tiempo y segmentadores interactivos.

![Dashboard Final de Análisis en Excel](/assets/images/dashboard-final-excel.png)
*Interfaz final: Una herramienta de Business Intelligence robusta, estética y lista para la toma de decisiones estratégicas.*
