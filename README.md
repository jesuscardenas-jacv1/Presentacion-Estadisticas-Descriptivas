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

## Contenido (24 diapositivas)

1. Portada · 2. La base de datos · 3. ¿Quiénes estudian? (paisaje de Parinacota) · 4. Flujo de trabajo
5. Carga de datos · 6. Pregunta de investigación · 7. Covarianza y correlación · 8. Gráfico de dispersión · 9. Regresión lineal · 10. Interpretación
11. Probabilidad: 3 preguntas · 12. Simple · 13. Conjunta · 14. Condicional
15. Nuevas preguntas (Lab 07) · 16. Unión · 17. Conjunta con rango · 18. Condicional para decidir
19. Forma de la distribución · 20. Asimetría y curtosis · 21. Histogramas · 22. Interpretación de la forma
23. Conclusiones · 24. Cierre

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
- Al agregar o quitar diapositivas, actualiza el contador inicial (`01 / 24`) en la barra de navegación.

## Trabajo en equipo

- Crea una rama para tu cambio: `git checkout -b nombre-del-cambio`
- Prueba abriendo `index.html` antes de subir.
- Sube la rama y abre un Pull Request para que el resto lo revise.

## Pendientes

- [ ] Reemplazar `[Integrantes del equipo]`, `[Asignatura]` y `[Docente]` en la portada y el cierre
- [ ] Agregar al Colab las celdas de las preguntas nuevas (In [14]–[18])
