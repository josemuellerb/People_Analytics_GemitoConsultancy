# \# 📊 Modelo Transaccional de Core HR, Compensaciones y Bienestar Psicosocial

# \*\*Firma de Consultoría:\*\* Gemito Consultancy  

# \*\*Área de Aplicación:\*\* People Analytics \& Strategic Workforce Planning  

# \*\*Fase del Proyecto:\*\* Cimientos de Arquitectura \& Diccionario de Datos (MVP v1.0)  

# 

# \---

# 

# \## 🎯 1. Visión General del Proyecto

# Este proyecto despliega una arquitectura de datos transaccional optimizada para organizaciones matriciales complejas de servicios profesionales. El objetivo principal es unificar métricas financieras, operativas y psicosociales bajo un \*\*Modelo en Estrella (Star Schema)\*\* altamente eficiente, utilizando \*\*Instantáneas Mensuales (Snapmonths)\*\* e históricos simulados del periodo 2021-2026.

# 

# \---

# 

# \## 🗺️ 2. Diagrama Entidad-Relación (ERD) Inicial

# ```mermaid

# erDiagram

# &#x20;   dim\_Asociados {

# &#x20;       varchar ID\_Asociado PK

# &#x20;       varchar Nombres

# &#x20;       varchar Apellidos

# &#x20;       date Fecha\_Nacimiento

# &#x20;       varchar Genero

# &#x20;       date Fecha\_Ingreso

# &#x20;   }

# &#x20;   dim\_Piramide {

# &#x20;       varchar id\_piramide PK

# &#x20;       varchar Departamento

# &#x20;       varchar Cargo

# &#x20;       varchar Nivel\_Jerarquico

# &#x20;       decimal Banda\_Salarial\_Min

# &#x20;       decimal Banda\_Salarial\_Max

# &#x20;       int Plazas\_Autorizadas

# &#x20;   }

# &#x20;   dim\_Calendario {

# &#x20;       int Fecha\_Llave PK

# &#x20;       int Anio

# &#x20;       varchar Mes\_Nombre

# &#x20;       varchar Trimestre

# &#x20;   }

# &#x20;   fact\_Compensaciones\_CTC {

# &#x20;       int ID\_Planilla PK

# &#x20;       int Fecha\_Llave FK

# &#x20;       varchar ID\_Asociado FK

# &#x20;       varchar id\_piramide FK

# &#x20;       decimal Sueldo\_Base

# &#x20;       decimal Horas\_Extras

# &#x20;       decimal Costo\_Total\_CTC

# &#x20;   }

# &#x20;   fact\_Ausentismo\_Mensual {

# &#x20;       int ID\_Ausentismo PK

# &#x20;       int Fecha\_Llave FK

# &#x20;       varchar ID\_Asociado FK

# &#x20;       varchar id\_piramide FK

# &#x20;       int Dias\_Vacaciones

# &#x20;       int Dias\_Licencia\_Medica

# &#x20;       int Faltas\_Injustificadas

# &#x20;   }

# &#x20;   fact\_Performance\_Trimestral {

# &#x20;       int ID\_Performance PK

# &#x20;       int Fecha\_Llave FK

# &#x20;       varchar ID\_Asociado FK

# &#x20;       varchar id\_piramide FK

# &#x20;       decimal Calificacion\_KPI

# &#x20;       int Evaluacion\_Competencias

# &#x20;   }

# &#x20;   fact\_Bienestar\_Perfil\_Psicologico {

# &#x20;       int ID\_Bienestar PK

# &#x20;       int Fecha\_Llave FK

# &#x20;       varchar ID\_Asociado FK

# &#x20;       varchar id\_piramide FK

# &#x20;       int Indice\_Engagement

# &#x20;       varchar Nivel\_Burnout

# &#x20;   }

# &#x20;   fact\_Novedades {

# &#x20;       int ID\_Novedad\_Evento PK

# &#x20;       int Fecha\_Llave FK

# &#x20;       varchar ID\_Asociado FK

# &#x20;       varchar id\_piramide FK

# &#x20;       varchar Tipo\_Novedad

# &#x20;       text Detalle\_Cualitativo

# &#x20;   }

# &#x20;   dim\_Asociados ||--o{ fact\_Compensaciones\_CTC : "registra"

# &#x20;   dim\_Asociados ||--o{ fact\_Ausentismo\_Mensual : "padece"

# &#x20;   dim\_Asociados ||--o{ fact\_Performance\_Trimestral : "obtiene"

# &#x20;   dim\_Asociados ||--o{ fact\_Bienestar\_Perfil\_Psicologico : "reporta"

# &#x20;   dim\_Asociados ||--o{ fact\_Novedades : "experimenta"

# &#x20;   dim\_Piramide ||--o{ fact\_Compensaciones\_CTC : "presupuesta"

# &#x20;   dim\_Piramide ||--o{ fact\_Ausentismo\_Mensual : "afecta\_a"

# &#x20;   dim\_Piramide ||--o{ fact\_Performance\_Trimestral : "mide\_en"

# &#x20;   dim\_Piramide ||--o{ fact\_Bienestar\_Perfil\_Psicologico : "monitorea\_en"

# &#x20;   dim\_Piramide ||--o{ fact\_Novedades : "sucede\_en"

# &#x20;   dim\_Calendario ||--o{ fact\_Compensaciones\_CTC : "ocurre\_en"

# &#x20;   dim\_Calendario ||--o{ fact\_Ausentismo\_Mensual : "ocurre\_en"

# &#x20;   dim\_Calendario ||--o{ fact\_Performance\_Trimestral : "cierra\_en"

# &#x20;   dim\_Calendario ||--o{ fact\_Bienestar\_Perfil\_Psicologico : "mapea\_en"

# &#x20;   dim\_Calendario ||--o{ fact\_Novedades : "registra\_en"

