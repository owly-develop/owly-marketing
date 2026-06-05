# 🎯 Landing owlysales.ai — objetivo, CTA y formulario

> Spec de la landing demo (`app/landing/`). Para alinear marketing y el equipo de producto.

---

## Objetivo (uno solo)

**Que el prospecto agende el diagnóstico gratuito de 2h.** Es la puerta de entrada del embudo del deck: Diagnóstico → Propuesta → Piloto 90d. Todo en la página empuja a esa única acción.

> Métrica de éxito de la landing: **# de diagnósticos agendados** (no visitas, no likes).

---

## Jerarquía de CTAs

| Nivel | CTA | Dónde |
|-------|-----|-------|
| **Primario** | "Agendar diagnóstico" | nav, hero, sección final (form) |
| Secundario | WhatsApp directo | sección final (fallback baja fricción) |

Todos los botones primarios llevan al formulario (`#contacto`). Un solo verbo, repetido.

---

## Formulario (mínimo)

Campos: **Nombre · WhatsApp.** Nada más (menos fricción = más conversión).

### Integración con la app OWLY (para el equipo de producto)
El form hace `POST` a un endpoint configurable. **Solo hay que setear la URL** en `app/landing/*.html`:

```js
const API_ENDPOINT = "";  // ← pegar aquí el endpoint del CRM OWLY
```

**Payload** (JSON) que envía:
```json
{
  "nombre": "string",
  "whatsapp": "string",
  "fuente": "landing-owlysales",
  "url": "https://...",
  "utm": { "source": "...", "medium": "...", "campaign": "..." },
  "ts": "ISO-8601"
}
```

Comportamiento:
- Con `API_ENDPOINT` seteado → envía al CRM y muestra confirmación.
- Sin endpoint (hoy) → muestra confirmación + ofrece WhatsApp como respaldo, para que la página sea demostrable ya.
- Captura UTMs de la URL automáticamente (para medir qué canal trae los diagnósticos).

---

## Pendiente

- [ ] Equipo de producto: exponer endpoint del CRM y pegar la URL.
- [ ] Definir qué pasa tras agendar (¿email/WhatsApp automático de confirmación? ¿Calendly mientras tanto?).
- [ ] Conectar GA4 + evento "lead_diagnostico" para medir.

---

🔗 Relacionado: `../02-estrategia/04-plan-marketing-90-dias.md` · `README.md` · landing: `app/landing/`
