# BBDD
Repositorio de asignatura BBDD


Sistema de Gestión del Camping Buena Vista
Proyecto académico de la asignatura Bases de Datos del Bachelor en Informática. Consiste en una aplicación de consola desarrollada en Python que utiliza SQLite para gestionar las operaciones básicas de un camping de autocaravanas con 20 parcelas.
Objetivo
Sustituir la gestión manual mediante hojas de cálculo por una solución que permita registrar clientes y vehículos, controlar la ocupación de parcelas y calcular la facturación de las estancias.
Funcionalidades implementadas
Inicialización de la base de datos: crea las tablas necesarias y registra las 20 parcelas iniciales.
Alta de clientes y autocaravanas: almacena datos personales básicos y asocia cada vehículo a su cliente mediante matrícula y país.
Check-in: asigna automáticamente una parcela disponible y registra las fechas de entrada y salida prevista.
Check-out: cierra la estancia, calcula las noches, guarda una factura y la muestra en consola.
Consulta de parcelas libres: muestra las parcelas sin estancias en curso.
La aplicación funciona mediante un menú interactivo en consola, sin interfaz gráfica ni sistema de reservas anticipadas.
Tecnologías utilizadas
Python 3
SQLite, mediante el módulo estándar `sqlite3`
`datetime`, para calcular la duración de las estancias
No requiere instalar dependencias externas.
Estructura del proyecto
```text
.
├── jmo_buenavista_v4.py       # Aplicación principal
├── Proyecto_FIN_BBDD_JMO.pdf  # Memoria académica y documentación técnica
├── README.md                  # Presentación e instrucciones
└── buenavista.db              # Base de datos generada al ejecutar el programa
```
El archivo `buenavista.db` se crea automáticamente en el directorio de ejecución y no necesita incluirse inicialmente en el repositorio.
Instalación y ejecución
Tener instalado Python 3.
Descargar o clonar el repositorio.
Abrir una terminal en la carpeta del proyecto.
Ejecutar:
```bash
python jmo_buenavista_v4.py
```
En algunos sistemas puede ser necesario utilizar `python3` en lugar de `python`.
Al iniciar, aparece el siguiente menú:
```text
--- Camping Buena Vista ---
1) Inicializar BD
2) Alta cliente
3) Check-in
4) Check-out
5) Ver parcelas libres
0) Salir
```
Importante: en la primera ejecución, seleccionar la opción 1) Inicializar BD antes de utilizar las demás funciones. Esta opción puede repetirse sin duplicar las 20 parcelas iniciales.
Modelo de datos
La base de datos utiliza cinco tablas:
Tabla	Contenido
`clientes`	Identificación y datos de contacto de los clientes
`autocaravanas`	Matrícula, país y cliente asociado
`parcelas`	Identificador de parcela e indicador de actividad
`estancias`	Vehículo, parcela, fechas y estado de ocupación
`facturas`	Estancia facturada, fecha, noches e importe total
La tabla `autocaravanas` utiliza una clave primaria compuesta por matrícula y país. La aplicación activa las claves foráneas de SQLite al inicializar el esquema y utiliza consultas SQL parametrizadas para incorporar datos introducidos por el usuario.
Cálculo de facturación
La factura se calcula automáticamente durante el check-out según la fórmula:
```text
Total = 20 € + (número de noches × 40 €)
```
Por ejemplo, una estancia de tres noches tiene un coste de 140 €. El programa guarda la factura en SQLite y presenta su desglose en pantalla.

Alcance y limitaciones de esta versión:
Esta es una implementación académica básica, pensada para uso local y monousuario. La versión del código incluida en este repositorio no incorpora todavía una opción de consulta histórica por matrícula, aunque dicha funcionalidad se contempla en la memoria de requisitos.

Tampoco implementa todas las validaciones y restricciones descritas en el diseño técnico: por ejemplo, no comprueba expresamente que una autocaravana esté registrada antes del check-in, no impide de forma explícita varias estancias activas para un mismo vehículo y no incluye un tratamiento completo de excepciones con `rollback`. La indicación de pago realizado se muestra en la factura, pero no existe una integración real con medios de pago.

Estas mejoras quedan como posibles líneas de evolución del proyecto, junto con una interfaz gráfica, un sistema de reservas y consultas históricas.
Documentación

El archivo `Proyecto_FIN_BBDD_JMO.pdf` contiene el análisis funcional de requisitos, el modelo conceptual de datos, las reglas de negocio, los diagramas del sistema, la memoria técnica y ejemplos de ejecución.

Autoría:
José María Ochoa Carriches  
Bachelor en Informática — Asignatura de Bases de Datos  

Curso académico 2025/2026
Proyecto de uso académico.
