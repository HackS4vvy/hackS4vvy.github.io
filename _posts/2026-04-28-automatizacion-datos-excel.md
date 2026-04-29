---
title: "Data Analysis & Automation: Ingeniería de Dashboards Dinámicos en Excel"
date: 2026-04-28 10:00:00
categories:
  - "Análisis de Datos"
header:
  teaser: /assets/images/dashboard-final-excel.png
tags:
  - Excel
  - VBA
  - Dashboards
  - Automatización
toc: true
toc_label: "Contenido del Proyecto"
---

### El Desafío del Negocio
El objetivo de este proyecto fue transformar un flujo de datos transaccionales desordenados (formato CSV) en una herramienta de **Business Intelligence** centralizada. El reto principal consistió en normalizar información inconsistente y automatizar la generación de reportes para permitir una toma de decisiones estratégica en tiempo real.

### Metodología y Herramientas
Para este desarrollo utilicé **Microsoft Excel** como motor analítico, aplicando técnicas de ingeniería de datos para asegurar que el sistema fuera escalable. El proceso cubrió desde la ingesta de archivos planos hasta la creación de una interfaz interactiva de usuario.

### Habilidades Técnicas Aplicadas
A través de una arquitectura robusta, se implementaron las siguientes soluciones:
*   **Ingesta y Normalización:** Limpieza profunda de archivos CSV y estructuración de tablas.
*   **Lógica Dinámica:** Uso de funciones avanzadas de búsqueda y agregación multicriterio.
*   **Diseño de Interfaz:** Maquetación funcional (Wireframing) y visualización de alto impacto.

---

### Fase 1: Ingesta y Normalización de Datos (CSV)

El proceso comienza con la recepción de información en formato plano. Como se observa en la comparativa, los datos iniciales carecen de estructura, lo que impide cualquier análisis técnico.

<div style="text-align: center;">
  <img src="/assets/images/csv-datos-crudos.png" alt="Datos CSV Crudos" style="border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.2);">
  <p><i>Estado inicial: Información agrupada en una sola cadena de texto.</i></p>
</div>

Para transformar este caos en una arquitectura funcional, apliqué un flujo de normalización:
*   **Parseo de Datos:** Uso de "Texto a columnas" para delimitar variables (`Producto`, `Marca`, `Origen`).
*   **Enriquecimiento Geográfico:** Uso de tipos de datos de Excel para extraer automáticamente la **Población**.
*   **Estructuración de Tablas (`Ctrl + T`):** Conversión a objeto Tabla para asegurar la dinamicidad de las fórmulas.

<div style="text-align: center;">
  <img src="/assets/images/tabla-limpia-excel.png" alt="Tabla Normalizada" style="border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.2);">
  <p><i>Resultado final: Estructura de datos optimizada y lista para el análisis.</i></p>
</div>

---

### Fase 2: Inteligencia de Búsqueda y Lógica Aritmética

Una vez estructurada la base, implementé una capa de lógica para la extracción de KPIs y recuperación de información:

*   **Agregación Multicriterio:** Uso de `SUMAR.SI.CONJUNTO` para reportes basados en múltiples condiciones.
*   **Motores de Búsqueda:** Implementación de `BUSCARV` para consultas dinámicas de atributos.
*   **Lógica Condicional:** Uso de la **Función SI** con referencias absolutas para categorizar automáticamente registros críticos.

<div style="text-align: center;">
  <img src="/assets/images/funciones-suma-excel.png" alt="Funciones de Suma" style="border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.2); margin-bottom: 10px;">
  <img src="/assets/images/motor-busqueda-excel.png" alt="Motor BUSCARV" style="border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.2);">
  <p><i>Implementación de lógica analítica y recuperación dinámica de información.</i></p>
</div>

---

### Fase 3: Diseño de Interfaz y Maquetación (Wireframing)

Antes de integrar las gráficas finales, desarrollé un **boceto estructural** utilizando figuras y formas nativas de Excel. Esta fase de maquetación permitió definir la jerarquía de información y asegurar una experiencia de usuario fluida.

<div style="text-align: center;">
  <img src="/assets/images/boceto-dashboard-excel.png" alt="Boceto Dashboard" style="border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.2);">
  <p><i>Maquetación funcional: Definición de espacios para KPIs, gráficos y controles de filtro.</i></p>
</div>

---

### Fase 4: Arquitectura de Reportes e Interactividad

Tras procesar los datos, utilicé **Tablas Dinámicas** para generar el motor analítico, permitiendo cruzar variables de Mes, Cliente y Región.

#### Control de Datos Multifiltro:
Para maximizar la interacción, integré controles que responden en tiempo real:
*   **Segmentación de Datos (Slicers):** Filtros táctiles para navegar por marcas y productos.
*   **Escala de Tiempo (Timeline):** Control cronológico para auditorías por año y mes.

<div style="text-align: center;">
  <img src="/assets/images/segmentacion-datos-excel.png" alt="Segmentadores" style="border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.2);">
  <p><i>Interactividad: Sincronización de filtros para una exploración de datos fluida.</i></p>
</div>

---

### Visualización Final: Dashboard de Alto Impacto (Dark Mode)

El resultado final es una herramienta de **Business Intelligence** diseñada bajo un esquema de "Modo Oscuro" para mejorar la legibilidad y estética profesional.

<div style="text-align: center;">
  <img src="/assets/images/dashboard-final-excel.png" alt="Dashboard Final" style="border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.2);">
  <p><i>Interfaz final interactiva: Control total sobre KPIs de rendimiento y ventas.</i></p>
</div>

#### Hallazgos Clave del Proyecto:
*   **Rendimiento Humano:** Identificación inmediata del TOP 5 de vendedores y su contribución al ingreso total.
*   **Análisis Territorial:** Visualización de las regiones con mayor volumen de órdenes para optimización logística.
*   **Mix de Productos:** Desglose porcentual de participación de mercado por marca mediante gráficos de anillos dinámicos.

---

### 💡 Conclusiones e Insights de Negocio

La implementación de este Dashboard permitió centralizar la operación en tres pilares:

*   **Eficiencia Operativa:** Reducción del tiempo de generación de reportes manuales en un 90%.
*   **Precisión de Datos:** Eliminación del error humano mediante la automatización de la lógica de búsqueda y suma condicional.
*   **Escalabilidad:** El sistema es capaz de absorber nuevos registros de ventas simplemente actualizando la fuente, manteniendo la integridad de todas las gráficas.

> **Nota técnica:** Este enfoque demuestra que Excel, bien estructurado, funciona como una base de datos relacional capaz de alimentar interfaces de alta fidelidad para la toma de decisiones.
