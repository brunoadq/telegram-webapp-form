# Telegram Web App (GitHub Pages)

Formulario básico en HTML + JS listo para abrirse dentro de Telegram como **Web App** y enviar datos a **n8n**.

## Archivos

- `index.html`: la app completa (no necesita build).
- `README.md`: estas instrucciones rápidas.

## Uso rápido (GitHub Pages)

1. Crea un repositorio en GitHub (público o privado).
2. Sube `index.html` y `README.md` a la rama `main` (o `master`).
3. Ve a **Settings → Pages** y en *Build and deployment* elige:
   - **Source**: *Deploy from a branch*  
   - **Branch**: `main` — **/ (root)`
4. Guarda. En ~1–3 minutos verás la URL de tu sitio, por ejemplo:
   `https://TU_USUARIO.github.io/TU_REPO/`
5. Usa esa URL en el botón `web_app` de tu bot de Telegram.

## Integración con n8n

El archivo `index.html` trae dos modos:

- `mode: "telegram"` *(recomendado)*: envía los datos de vuelta al bot con `Telegram.WebApp.sendData(...)`. En n8n, captura el mensaje con **Telegram Trigger** y lee `{$json.message.web_app_data.data}` (JSON).
- `mode: "webhook"`: envía `POST` a tu Webhook de n8n. Debes configurar CORS en el **Webhook node** (headers: `Access-Control-Allow-Origin: *` y `Access-Control-Allow-Headers: *`).

Cambia `webhookUrl` en `index.html` si usas el modo `webhook`.

## Botón en el bot (ejemplo JSON de reply_markup)

```json
{
  "inline_keyboard": [[
    {
      "text": "Abrir formulario",
      "web_app": { "url": "https://TU_USUARIO.github.io/TU_REPO/" }
    }
  ]]
}
```

## Campos del formulario

- Fecha (prellenada con el día actual `2025-09-26`)
- Litros producidos (0–5000)
- Lechería (selector)
- Operario (texto)

## Notas
- Requiere HTTPS (GitHub Pages ya lo provee).
- Si usas `mode: "webhook"`, asegúrate de que tu n8n sea accesible por Internet y con CORS permitido.
- Si usas `mode: "telegram"`, no hay problema de CORS porque los datos van al bot.
- `telegram_initData` se adjunta por si quieres validar origen en backend.
