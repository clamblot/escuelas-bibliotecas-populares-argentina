# Escuelas y bibliotecas populares en Argentina

Análisis de la distribución de establecimientos educativos y bibliotecas populares por departamento, teniendo en cuenta la población en edad escolar.

Proyecto realizado en la materia **Laboratorio de Datos** (FCEN, UBA, 2025) junto a Nicole Lamblot e Iván Pérez.

**Tecnologías:** Python · pandas · DuckDB (SQL) · matplotlib · seaborn

## Qué hace

A partir de tres fuentes públicas (padrón de población, establecimientos educativos y bibliotecas populares de CONABIP), el proyecto:

1. Evalúa la **calidad de los datos** con la técnica GQM (Goal, Question, Metric).
2. **Limpia y unifica** los datasets, y los reorganiza en un modelo relacional en tercera forma normal (DER incluido en el informe).
3. Responde cuatro **consultas SQL** sobre ese modelo (escuelas por nivel y población, bibliotecas fundadas desde 1950, cantidad de escuelas/bibliotecas/población por departamento y dominio de mail más frecuente).
4. Genera **cuatro visualizaciones** para explorar cómo se relacionan escuelas, bibliotecas y población.

## Decisiones de modelado

- La unidad geográfica común a los tres datasets es el **departamento**. Se adoptaron los códigos del padrón de población como estándar.
- Las 15 comunas de CABA se unificaron en un único departamento (código `02000`), y sus valores se normalizaron dividiendo por 15.
- Se trabajó solo con establecimientos de **modalidad común** de nivel inicial, primario y secundario.
- Las edades se agruparon por nivel: jardín (2–5), primaria (6–12) y secundaria (13–18).
- Las columnas de contacto múltiple (mails con varios valores) y las casi vacías se descartaron o se marcaron como problema de calidad.

El detalle completo (DER, modelo relacional, dependencias funcionales y justificación de cada decisión) está en el informe: [`Escuelas_y_Bibliotecas_Informe.pdf`](Escuelas_y_Bibliotecas_Informe.pdf).

## Estructura del repositorio

```
.
├── README.md
├── requirements.txt
├── analisis_escuelas_bibliotecas.py         # GQM, limpieza, consultas SQL y gráficos
├── Escuelas_y_Bibliotecas_Informe.pdf       # informe completo del trabajo
├── TablasOriginales/                        # datasets de origen
│   ├── establecimientos_educativos.csv
│   ├── bibliotecas-populares.csv
│   └── padron_poblacion.csv
└── TablasModelo/                            # tablas del modelo relacional (el script las regenera)
```

## Cómo ejecutarlo

1. Instalar las dependencias:

```bash
pip install -r requirements.txt
```

2. Ejecutar el script **desde la carpeta del repositorio**, ya que las rutas a `TablasOriginales/` y `TablasModelo/` son relativas:

```bash
python analisis_escuelas_bibliotecas.py
```

`analisis_escuelas_bibliotecas.py`, `TablasOriginales/` y `TablasModelo/` deben estar en el mismo directorio. El script sobrescribe las tablas de `TablasModelo/` en cada ejecución, así que puede correrse las veces que se quiera sin alterar el resultado. Está dividido en celdas (`#%%`), por lo que también se puede correr por secciones desde Spyder o VS Code.

## Principales conclusiones

- La cantidad de escuelas crece de forma clara con la población en edad escolar de cada departamento.
- Las bibliotecas populares también se concentran en zonas más pobladas, pero la relación es bastante más débil.
- Al normalizar por cada mil habitantes no aparece una relación clara entre escuelas y bibliotecas: que un departamento tenga muchas escuelas no implica que tenga muchas bibliotecas.
- Las provincias más pobladas (Buenos Aires, Córdoba, Santa Fe) muestran mucha desigualdad interna entre sus departamentos.

## Fuentes de datos

- Padrón de población (INDEC).
- Registro de establecimientos educativos (Ministerio de Educación).
- Bibliotecas populares (CONABIP).

## Autores

- Camila Lamblot
- Nicole Lamblot
- Iván Pérez
