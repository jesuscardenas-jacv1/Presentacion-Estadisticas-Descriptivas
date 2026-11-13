# Proyecto Presentación — Estadística Descriptiva

**Base:** Matrículas de Educación Superior · Arica y Parinacota 2021 (misma base de la Evaluación 1)
**Herramientas:** Google Colab · pandas · numpy · matplotlib · scikit-learn
**Encargo de la profesora:** presentación que explique el contexto y el flujo completo del Colab, mostrando **el código al lado de su resultado** para poder explicarlo.

Última actualización: 29-10-2026

---

## Estado general

| # | Punto | Estado |
|---|-------|--------|
| 1 | Carpeta del proyecto con datos, Colab y gráficos | ✅ Listo |
| 2 | Verificación de resultados del Colab contra el Excel | ✅ Listo (2 errores encontrados y corregidos) |
| 3 | Colab corregido | ✅ Listo — falta subirlo a Google Colab |
| 4 | Gráficos para la presentación | ✅ Listo |
| 5 | Presentación v1 (Slides, colores violeta) | ✅ Descartada por colores |
| 5b | **Presentación v2 animada (HTML, blanco y negro, partículas, 16 diapositivas)** | ✅ Versión actual |
| 6 | Completar datos del equipo en portada y cierre | ⬜ Pendiente |
| 7 | Revisión del equipo + ensayo | ⬜ Pendiente |
| 8 | Exportar a PDF / PowerPoint si la profesora lo pide | ⬜ Pendiente |

**Presentación actual (v2 animada):** https://claude.ai/artifact/PMnN5mxVFxTr745j2cwM8h — copia local: `04_Presentacion/matriculas-arica-2021.html` (abrir con Chrome; necesita internet solo para las fuentes)
**Presentación v1 (Slides):** https://claude.ai/artifact/1yPpvwY7m6vvRqWkh1xqM7
Ambas son privadas: compartir desde el menú *Share* para que el equipo las vea.

### Cómo usar la v2
- ← → / espacio / clic: avanzar o retroceder · **N**: notas del orador · **F**: pantalla completa · deslizar en celular
- En las diapositivas de código, el código se "escribe" y luego se "ejecuta" antes de mostrar el resultado (~3 s)
- Cada diapositiva tiene su propio movimiento de partículas, ligado al contenido: nube con r ≈ 0,5 en correlación, 25% de partículas sobre la recta en regresión, 50% / 17% / 91% iluminadas en probabilidad, la palabra "Gracias" al cierre
- Diapositiva nueva 3: paisaje a tinta de Parinacota (volcanes Parinacota y Pomerape, lago Chungará, vicuñas) con quiénes estudian: 56,6% mujeres, mediana 23 años, 46% entre 20 y 24, todas las sedes en Arica, matrículas por tipo de institución

---

## Estructura de la carpeta

```
Presentacion Estadisticas Descriptivas/
├── AVANCE_PROYECTO.md            ← este documento
├── Presentacion.url              ← acceso directo a la presentación v1 (Slides)
├── 04_Presentacion/
│   └── matriculas-arica-2021.html  ← presentación v2 animada
├── 01_Datos/
│   └── 01_MATRICULAS_ED_SUPERIOR_ARICA_Y_PARINACOTA_2021.xlsx
├── 02_Colab/
│   ├── Proyecto_Segunda_Presentacion_ORIGINAL.ipynb
│   └── Proyecto_Segunda_Presentacion_CORREGIDO.ipynb
└── 03_Graficos/
    ├── grafico_dispersion.png
    ├── grafico_regresion.png
    └── colab_original_dispersion.png
```

---

## Contexto de la base

- **14.116 filas** (un estudiante por fila) × **28 columnas**
- **11 instituciones**, 4 tipos: CFT 3.594 · IP 1.430 · Universidades CRUCH 7.849 · Universidades privadas 1.243
- Columnas usadas: VALOR MATRICULA (PESOS), VALOR ARANCEL (PESOS), NOMBRE DE INSTITUCION, TIPO DE INSTITUCION, NIVEL CARRERA, GENERO, AREA CONOCIMIENTO, ACREDITACION INSTITUCIONAL

---

## Flujo del Colab y resultados (verificados)

### Parte 1 — Asociación entre variables
- **Pregunta:** ¿el valor de la matrícula explica el valor del arancel?
- **x (independiente):** VALOR MATRICULA · **y (dependiente):** VALOR ARANCEL

| Paso | Código clave | Resultado | Interpretación |
|------|--------------|-----------|----------------|
| Covarianza | `.cov()` | 30.456.470.119,18 | Positiva → relación directa |
| Correlación | `.corr()` | r = 0,4996 | Positiva **moderada** |
| Gráfico | `ax.scatter()` | Nube ascendente con franjas verticales | Muchas carreras comparten matrícula con aranceles distintos |
| Regresión | `np.polyfit(x, y, 1)` | y = 7,502x + 1.724.716 | +$1 de matrícula → +$7,50 de arancel; base $1.724.716 |
| Determinación | `r2_score()` | R² = 25,0% | La matrícula explica ¼ de la variación (0,4996² ≈ 0,25) |

### Parte 2 — Probabilidad (tablas con `pd.crosstab(..., margins=True)`)

| Tipo | Pregunta | Cálculo | Resultado |
|------|----------|---------|-----------|
| Simple P(A) | ¿Universidad de Tarapacá? | 7.119 / 14.116 | **50,43%** |
| Conjunta P(A∩B) | ¿Femenino y Carreras Técnicas? | 2.469 / 14.116 | **17,49%** |
| Condicional P(A\|B) | Si es de Salud, ¿acreditada? | 2.634 / 2.899 | **90,86%** |

---

## Correcciones hechas al Colab (importante)

1. **Probabilidad simple:** el código dividía por `140116` (un 0 de más) → daba 5,08%. Correcto: 7119 / 14116 = **50,43%**.
2. **Probabilidad conjunta:** se usó la tabla TIPO DE INSTITUCION × GENERO y se dividió 2221 / 3594 = 61,80%. Eso es una probabilidad *condicional* (Femenino dado CFT) y de otra variable. La pregunta pide NIVEL CARRERA = Carreras Tecnicas, y la conjunta se divide por el total: 2469 / 14116 = **17,49%**.
3. **Texto de la correlación:** decía "positiva débil"; r ≈ 0,50 se considera **positiva moderada**.
4. **Celda con error de crosstab:** la salida guardada mostraba `ValueError` por pasar 3 columnas a `crosstab`; quedó con 2 columnas.
5. Nombre del Excel unificado (una celda usaba `... 2021 (1).xlsx`).

La covarianza, correlación, regresión, R² y la probabilidad condicional (90,86%) estaban correctas.

---

## Presentación — orden de diapositivas

1. Portada · 2. La base de datos · 3. Flujo de trabajo · 4. Carga (código + resultado)
5. Pregunta de investigación · 6. Covarianza y correlación (código + resultado) · 7. Gráfico de dispersión (código + gráfico)
8. Regresión lineal (código + resultado) · 9. Interpretación del modelo
10. Las 3 preguntas de probabilidad · 11. P. simple · 12. P. conjunta · 13. P. condicional (código + tabla + resultado)
14. Conclusiones · 15. Cierre

Cada diapositiva tiene **notas del orador** con lo que hay que decir.

## Pendientes / ideas

- [ ] Reemplazar `[Integrantes del equipo]`, `[Asignatura]` y `[Docente]` en portada y cierre
- [ ] Subir `Proyecto_Segunda_Presentacion_CORREGIDO.ipynb` a Colab y ejecutarlo con el Excel
- [ ] Repartir diapositivas entre los integrantes y ensayar

---

## Preguntas nuevas de probabilidad (referencia: Laboratorio 07)

| # | Tipo | Pregunta | Tabla sugerida |
|---|------|----------|----------------|
| 1 | Unión P(A ∪ B) | Si se selecciona un estudiante al azar, ¿cuál es la probabilidad de que estudie en jornada **Vespertina** o en una institución **No acreditada**? | `crosstab(JORNADA, ACREDITACION INSTITUCIONAL)` |
| 2 | Conjunta con rango | ¿Cuál es la probabilidad de que un estudiante elegido al azar sea **mujer** y tenga **al menos 30 años**? | `crosstab(RANGO EDAD, GENERO)` |
| 3 | Condicional comparativa (decisión) | Se quiere abrir más cupos vespertinos para personas que trabajan. ¿En qué tipo de institución es más probable que un estudiante estudie en jornada **Vespertina**? Justificar con P(Vespertino \| tipo). | `crosstab(TIPO DE INSTITUCION, JORNADA)` |

Resultados (verificados con el Excel): 1) 4.853/14.116 = **34,38%** (29,07% + 16,60% − 11,29%) · 2) (678+455+588)/14.116 = **12,19%** · 3) P(Vespertino | tipo): CFT **57,96%**, IP 46,57%, U. privadas 42,80%, U. CRUCH 10,49%

Estado: ✅ agregadas a la presentación (diapositivas 15–18, 20 en total) · ⬜ agregar las celdas al Colab (In [14]–[18])

---

## Lista de cotejo (Prof. Arlette Mella Suárez) · 13-11-2026

Revisión de la presentación contra los 18 indicadores de la hoja:
- Cumplían desde antes: 1–12; 15 y 16 (aporte de KanninoX, rama `asimetria-curtosis`, ya unida a `main`).
- Completados: 13 (eje Y "Frecuencia" y eje X rotulado en los histogramas), 14 (diapositiva de media, mediana y moda), 17 (diapositiva de desviación estándar) y 18 (diapositiva que justifica por qué ninguna variable tiene forma de campana).
- Ecuación del modelo expresada como y = a + bx: y = 1.724.716 + 7,502x.
- Diapositivas reordenadas del punto 1 al 18; cada una indica arriba el punto que cubre (26 en total).
- Colab corregido con las celdas nuevas (preguntas Lab 07, histogramas, medidas, desviación y conclusión de normalidad), ejecutado y verificado.
- La hoja indica puntaje sobre 29, pero muestra 18 indicadores: falta revisar la segunda página.
