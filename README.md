# Metodología Trainingym — Las 4 palancas

Página web interactiva que presenta la metodología Trainingym para hacer crecer un negocio fitness:
**Captación · Ahorro de tiempo · Fidelización · Ingresos.**

Diseñada para presentación comercial (pantalla compartida, sala de reuniones). Navegación entre palancas, ecosistema visual (Manager + App + Control de acceso + Pagos) y códigos QR para reservar reuniones o firmar acuerdos.

## Estructura

Un único archivo autocontenido:

- `index.html` — toda la página (HTML + CSS + JS inline, sin dependencias locales)

Recursos externos que carga vía CDN:

- Tipografía **Host Grotesk** desde Google Fonts
- Logo Trainingym desde `trainingym.com`
- QR generados por `api.qrserver.com`

## Navegación interna

Hash routing — cada palanca tiene su URL:

- `/` o `/#` — vista home con los 4 puntos
- `/#cap` — Captación
- `/#tiem` — Ahorro de tiempo
- `/#fid` — Fidelización
- `/#ing` — Ingresos

## Acciones (clicks externos)

| Click | Destino |
|---|---|
| € Tarifas (topbar — destacado) | `mirkotrain.github.io/wizard_tarifas_supersonik/?step=clientes` |
| Calendario (topbar) | QR a HubSpot — reservar reunión con experto |
| Contrato (topbar) | QR a PandaDoc — firmar acuerdo con 10% descuento |
| Imagotipo Trainingym (topbar) | QR a `app.tgmanager.com/auth` — crear licencia gratis |
| MacBook del ecosistema | `app.tgmanager.com/auth` |
| App móvil del ecosistema | `mirkotrain.github.io/navegaci-n-app/#hoy` |

## Publicar en GitHub Pages

1. Crea un repo nuevo en GitHub (vacío, sin README).
2. Desde esta carpeta en PowerShell:
   ```powershell
   git init
   git add .
   git commit -m "Versión inicial"
   git branch -M main
   git remote add origin https://github.com/<usuario>/<repo>.git
   git push -u origin main
   ```
3. En GitHub: **Settings → Pages → Source: Deploy from a branch → Branch: main / Folder: / (root) → Save**.
4. En 1–2 minutos la página estará disponible en `https://<usuario>.github.io/<repo>/`.
