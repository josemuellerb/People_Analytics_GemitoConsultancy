# 📊 Modelo Transaccional de Core HR, Compensaciones y Bienestar Psicosocial
**Firma de Consultoría:** Gemito Consulting  
**Área de Aplicación:** People Analytics & Strategic Workforce Planning  
**Fase del Proyecto:** Cimientos de Arquitectura & Diccionario de Datos (MVP v1.0)  

---

## 🎯 1. Visión General del Proyecto
Este proyecto despliega una arquitectura de datos transaccional optimizada para organizaciones matriciales complejas de servicios profesionales. El objetivo principal es unificar métricas financieras, operativas y psicosociales bajo un **Modelo en Estrella (Star Schema)** altamente eficiente, utilizando **Instantáneas Mensuales (Snapmonths)** e históricos simulados del periodo 2021-2026.

---

## 🗺️ 2. Diagrama Entidad-Relación (ERD) Inicial

```mermaid
erDiagram
    dim_Asociados {
        varchar ID_Asociado PK
        varchar Nombres
        varchar Apellidos
        date Fecha_Nacimiento
        varchar Genero
        date Fecha_Ingreso
    }
    dim_Piramide {
        varchar id_piramide PK
        varchar Departamento
        varchar Cargo
        varchar Nivel_Jerarquico
        decimal Banda_Salarial_Min
        decimal Banda_Salarial_Max
        int Plazas_Autorizadas
    }
    dim_Calendario {
        int Fecha_Llave PK
        int Anio
        varchar Mes_Nombre
        varchar Trimestre
    }
    fact_Compensaciones_CTC {
        int ID_Planilla PK
        int Fecha_Llave FK
        varchar ID_Asociado FK
        varchar id_piramide FK
        decimal Sueldo_Base
        decimal Horas_Extras
        decimal Costo_Total_CTC
    }
    fact_Ausentismo_Mensual {
        int ID_Ausentismo PK
        int Fecha_Llave FK
        varchar ID_Asociado FK
        varchar id_piramide FK
        int Dias_Vacaciones
        int Dias_Licencia_Medica
        int Faltas_Injustificadas
    }
    fact_Performance_Trimestral {
        int ID_Performance PK
        int Fecha_Llave FK
        varchar ID_Asociado FK
        varchar id_piramide FK
        decimal Calificacion_KPI
        int Evaluacion_Competencias
    }
    fact_Bienestar_Perfil_Psicologico {
        int ID_Bienestar PK
        int Fecha_Llave FK
        varchar ID_Asociado FK
        varchar id_piramide FK
        int Indice_Engagement
        varchar Nivel_Burnout
    }
    fact_Novedades {
        int ID_Novedad_Evento PK
        int Fecha_Llave FK
        varchar ID_Asociado FK
        varchar id_piramide FK
        varchar Tipo_Novedad
        text Detalle_Cualitativo
    }
    dim_Asociados ||--o{ fact_Compensaciones_CTC : "registra"
    dim_Asociados ||--o{ fact_Ausentismo_Mensual : "padece"
    dim_Asociados ||--o{ fact_Performance_Trimestral : "obtiene"
    dim_Asociados ||--o{ fact_Bienestar_Perfil_Psicologico : "reporta"
    dim_Asociados ||--o{ fact_Novedades : "experimenta"
    dim_Piramide ||--o{ fact_Compensaciones_CTC : "presupuesta"
    dim_Piramide ||--o{ fact_Ausentismo_Mensual : "afecta_a"
    dim_Piramide ||--o{ fact_Performance_Trimestral : "mide_en"
    dim_Piramide ||--o{ fact_Bienestar_Perfil_Psicologico : "monitorea_en"
    dim_Piramide ||--o{ fact_Novedades : "sucede_en"
    dim_Calendario ||--o{ fact_Compensaciones_CTC : "ocurre_en"
    dim_Calendario ||--o{ fact_Ausentismo_Mensual : "ocurre_en"
    dim_Calendario ||--o{ fact_Performance_Trimestral : "cierra_en"
    dim_Calendario ||--o{ fact_Bienestar_Perfil_Psicologico : "mapea_en"
    dim_Calendario ||--o{ fact_Novedades : "registra_en"