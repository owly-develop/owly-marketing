# 🧭 Playbook — Caso Ancla en 1 Semana

> Anexo de uso interno del deck (slides 25-32). Cuando **aún no hay casos de éxito**, este playbook construye el "caso ancla" extrayendo datos de un proyecto en marcha. Incluye prompts operativos para Claude Code.

> 💡 **Para Claude Code (futuras sesiones)**: si el usuario pide "construir el caso ancla" o "sacar el baseline", estos son los pasos y prompts a ejecutar contra su base de datos real (en el repo `owly-sales-ecosystem`).

---

## Paso 01 — Qué extraer (las 7 cifras)

1. **Total de leads** recibidos en el período — desglosado por canal (Meta, Web, WhatsApp, referidos).
2. **% que cotizó online** — cotizaciones generadas / leads totales.
3. **Tiempo promedio de respuesta** — desde llegada del lead hasta primer mensaje del asesor.
4. **Distribución horaria de leads** — % que llega fuera de horario hábil (clave para la narrativa "9pm").
5. **Conversión lead → visita → cierre** — tres tasas separadas.
6. **Tiempo promedio del ciclo** — días desde primer contacto hasta firma de reserva.
7. **⭐ La más importante: una historia humana** — una venta concreta donde OWLY hizo la diferencia (quién, cuándo, qué pasó). Una anécdota vale más que diez gráficos.

---

## Paso 02 — Prompt Claude Code · Baseline de leads

```
# PROMPT 01 — BASELINE DE LEADS
Analiza la base de datos del proyecto [NOMBRE] y genera un reporte
ejecutivo con estas métricas, en formato tabla:

1. Total de leads recibidos en los últimos 90 días
2. Distribución por canal de origen (utm_source o source_id)
3. Distribución por día de semana y hora del día
4. % de leads que generaron al menos una cotización
5. % que pasaron a "visita agendada" (status correspondiente)
6. % que pasaron a "reserva firmada"
7. Tiempo promedio entre creación del lead y primer mensaje del asesor
   (de la tabla messages/conversations)
8. Tiempo promedio del ciclo completo lead → reserva

Ignora leads marcados como spam o test. Excluye conversaciones internas.
Devuelve también las queries SQL que usaste para re-correr el análisis
mensualmente.
```
➡️ Resultado: tabla con las 7 cifras reales → reemplaza placeholders en slides 4 y 14.

---

## Paso 03 — Prompt Claude Code · Storyboard real (la anécdota)

```
# PROMPT 02 — ANÉCDOTA REAL
Encuéntrame UN lead específico del proyecto [NOMBRE] que cumpla TODAS:
1. Llegó fuera del horario hábil (después 7pm o fin de semana)
2. Recibió primera respuesta de la IA en menos de 5 minutos
3. Generó al menos una cotización en la misma sesión
4. Terminó en visita agendada o reserva firmada
5. El lapso total fue menor a 7 días

Para ese lead, devuelve un timeline cronológico:
   - timestamp · canal · acción · contenido (anonimizado)

Anonimiza nombre y datos personales. Mantén timestamps exactos, unidades,
montos. Quiero reconstruir la historia en una infografía sin inventar nada.
```
➡️ Resultado: historia real con timestamps → reemplaza el slide 13.

---

## Paso 04 — Prompt Claude Code · Antes vs Después (delta)

```
# PROMPT 03 — DELTA ANTES/DESPUÉS
Para el proyecto [NOMBRE], compara dos períodos:
PRE-OWLY: [fecha inicio] → [fecha fin]
POST-OWLY: [fecha go-live] → hoy
Genera tabla comparativa con:
   - Cotizaciones por mes · Tiempo de respuesta
   - % cierres / leads · Costo por lead calificado
   - Ventas totales por mes
Calcula delta % con flecha (verde ↑ / rojo ↓).
Si no hay datos del PRE, dilo explícitamente. No inventes baseline.
Usa el primer mes post-OWLY como baseline.
```
➡️ Resultado: cifras para "Caso de éxito — [Nombre]".

---

## Paso 05 — Entrevista al cliente (30 min, 7 preguntas)

1. ¿Cómo era tu preventa antes de OWLY?
2. ¿Qué te frustraba más del día a día?
3. ¿Qué te llevó a probar OWLY?
4. ¿Qué fue lo primero que cambió?
5. ¿Una venta específica donde OWLY hizo la diferencia?
6. ¿Qué le dirías a otra constructora considerando OWLY?
7. ¿Si te quitaran OWLY mañana, qué extrañarías más?

**Formato**: Zoom/Loom con video, 30 min máx, en su oficina con dashboard OWLY abierto.
**Prohibido**: guion, lectura, slides. Necesitas su voz natural.
**Usos**: 3 reels de 30s, 1 video de 90s web, 5 quotes LinkedIn, 1 testimonial escrito.
**Derechos**: carta de uso de imagen firmada antes de grabar.

---

## Checklist — 1 semana al caso ancla

| Día | Tarea | Entregable |
|-----|-------|-----------|
| **LUN** | Prompt 01 a Claude Code | Baseline de leads — 7 cifras en mano |
| **MAR** | Prompt 02 — la anécdota | Lead-historia perfecto, timeline real |
| **MIÉ** | Entrevista al cliente | 30 min Zoom grabado con video |
| **JUE** | Reemplaza placeholders | Slides 4, 13, 14, 17 con cifras y nombre reales |
| **VIE** | Sales deck v2 listo | Deck con caso ancla real para la primera reunión |

> **Regla de oro: una cifra real vale más que diez bullets bien escritos.**

---

🔗 Relacionado: `01-pitch-narrativa.md` · `../02-estrategia/03-propuesta-comercial-2026.md` · repo de datos: `owly-sales-ecosystem`
