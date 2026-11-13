# Presentación · Estadística Descriptiva

Análisis de la base de **matrículas de educación superior 2021 de la región de Arica y Parinacota** (14.116 registros, 28 variables), hecho en Google Colab con Python, y la presentación animada que lo explica: código al lado de su resultado.

## Abrir la presentación

1. Descarga o clona el repositorio.
2. Abre `index.html` con Chrome o Edge (doble clic). No necesita servidor ni instalar nada.
3. Controles:

| Tecla | Acción |
|---|---|
| → · espacio · clic | Siguiente diapositiva |
| ← | Anterior |
| **F** | Pantalla completa |
| **N** | Notas del orador |
| Inicio / Fin | Primera / última |

Con internet se ven las fuentes originales (Google Fonts); sin internet usa fuentes parecidas y todo sigue funcionando.

## Estructura

```
index.html        ← presentación completa (HTML + CSS + JS en un solo archivo)
datos/            ← base de datos en Excel
colab/            ← notebook original y corregido
graficos/         ← gráficos exportados en PNG
docs/             ← documento de avance del proyecto (puntos, resultados, correcciones)
```

## Contenido (27 diapositivas, en el orden de la lista de cotejo)

Cada diapositiva indica arriba qué punto de la lista de cotejo cubre.

| # | Diapositiva | Punto |
|---|---|---|
| 1–5 | Portada · La base de datos · ¿Quiénes estudian? · Flujo de trabajo · Carga de datos | Contexto |
| 6 | Pregunta de investigación (X = matrícula, Y = arancel) | **Parte A** |
| 7 | Gráfico de dispersión | 1 |
| 8 | Covarianza y su signo (+ correlación) | 2 · 3 |
| 9 | Modelo de regresión lineal y R² | 4 · 6 |
| 10 | Interpretación: y = a + bx, pendiente y R² | 4 · 5 · 7 |
| 11 | Seis preguntas de probabilidad | **Parte B** |
| 12 | Probabilidad clásica | 8 |
| 13 | Unión | 9 |
| 14–15 | Intersección (2 preguntas) | 10 |
| 16–17 | Condicional (2 preguntas) | 11 · 12 |
| 18 | Histogramas con título y ejes | **Parte C** · 13 |
| 19 | Media, mediana y moda (¿son similares?) | 14 · 19 |
| 20–22 | Asimetría y curtosis: qué miden, cálculo e interpretación | 15 · 16 |
| 23 | Desviación estándar | 17 |
| 24 | Regla empírica: % de datos a 1 y 2 desviaciones vs 68 % y 95 % | **Parte D** · 21 · 22 |
| 25 | ¿Distribución normal? No: los cinco criterios juntos | 18 · 20 · 23 |
| 26–27 | Conclusiones · Cierre | |

### Resultados principales

| Cálculo | Resultado |
|---|---|
| Covarianza matrícula–arancel | 30.456.470.119,18 (relación directa) |
| Correlación de Pearson | r = 0,4996 (positiva moderada) |
| Regresión lineal | y = 7,502x + 1.724.716 · R² = 25,0% |
| P(U. de Tarapacá) | 50,43% |
| P(Femenino ∩ Carreras Técnicas) | 17,49% |
| P(Acreditada \| Salud) | 90,86% |
| P(Vespertino ∪ No acreditada) | 34,38% |
| P(Mujer ∩ 30 años o más) | 12,19% |
| P(Vespertino \| CFT) | 57,96% (CRUCH: 10,49%) |
| Edad: asimetría · curtosis | 1,8238 (positiva) · 3,5899 (leptocúrtica) |
| Matrícula: asimetría · curtosis | −0,8906 (negativa) · 0,0874 (≈ mesocúrtica) |
| Arancel: asimetría · curtosis | 0,0580 (≈ simétrica) · −0,8083 (platicúrtica) |
| Media · mediana · moda (edad) | 25,54 · 23 · 19 años |
| Desviación estándar | Edad 7,43 años · Matrícula $63.718 · Arancel $956.750 |
| % a 1 desviación (normal: 68 %) | Edad 81,77 % · Matrícula 67,46 % · Arancel 62,91 % |
| % a 2 desviaciones (normal: 95 %) | Edad 93,95 % · Matrícula 86,41 % · Arancel 98,53 % |
| ¿Distribución normal? | No en ninguna variable |

## Cómo editar la presentación

Todo está en `index.html`. Cada diapositiva es un `<section class="slide">` dentro de `<main id="stage">`, diseñada sobre un lienzo fijo de **1920 × 1080 px** que se escala a la pantalla.

**Atributos de cada diapositiva**

| Atributo | Para qué sirve | Valores |
|---|---|---|
| `class="slide dark"` / `class="slide light"` | Fondo negro o fondo papel | `dark`, `light` |
| `data-mode` | Animación de partículas del fondo | `constellation`, `grid`, `wind`, `flow`, `rain`, `orbit`, `orbit3`, `correlation`, `dim`, `line`, `proportion`, `universe`, `waves`, `skew`, `text` |
| `data-p` | Proporción de partículas iluminadas (modos `proportion` y `universe`) | entre `0` y `1` |
| `data-enter` | Transición de entrada | `blur`, `zoom`, `iris`, `wipe`, `rise` |

**Diapositiva de código + resultado** (`class="slide dark code-slide"`):
- El código va en texto plano dentro de `<pre class="code">…</pre>`; el resaltado y la animación de "escritura" se aplican solos.
- Lo que tiene clase `out` aparece después de que el código "se ejecuta".
- Un número con `data-count="50.43" data-dec="2" data-on="run"` se anima contando hasta ese valor.
- `<div class="waffle" data-on="50"></div>` dibuja 100 cuadros con 50 marcados.

**Otros detalles**
- Elementos con clase `r` y `style="--d:300"` aparecen con 300 ms de retraso.
- Las notas del orador van en `<aside class="notes">…</aside>` al final de cada `<section>`.
- Al agregar o quitar diapositivas, actualiza el contador inicial (`01 / 27`) en la barra de navegación.

## Trabajo en equipo

- Crea una rama para tu cambio: `git checkout -b nombre-del-cambio`
- Prueba abriendo `index.html` antes de subir.
- Sube la rama y abre un Pull Request para que el resto lo revise.

## Pendientes

- [ ] Reemplazar `[Integrantes del equipo]`, `[Asignatura]` y `[Docente]` en la portada y el cierre
