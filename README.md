# Wizard de Tarifas · Supersonik

Configurador público de tarifas paso a paso. El cliente responde preguntas guiadas en el panel izquierdo y el desglose con el precio se construye progresivamente a la derecha.

> 🌐 Web standalone — sin frameworks, sin build, sin servidor. Un solo `index.html`.

---

## 🎯 Cómo funciona

El wizard guía al cliente con **una pregunta por pantalla**. A medida que responde, el panel derecho se va llenando con los conceptos correspondientes. Cuando termina (modalidad de pago), aparecen arriba los totales destacados (Pago inicial y Cuota recurrente) y una flecha animada lo señala.

```
┌──────────────────────────────┐    ┌──────────────────────────────┐
│  IZQUIERDA · WIZARD          │    │  DERECHA · DESGLOSE          │
│                              │    │                              │
│  ▰▱▱▱▱▱  Paso 1 de 7         │    │   💼  Tu tarifa irá aquí     │
│                              │    │                              │
│  ¿Cuántos clientes activos?  │    │   (vacío hasta el 1er click) │
│                              │    │                              │
│  [0–50] [51–150] [151–300]   │    │                              │
│  [301–500] [501–1000]        │    │                              │
│  [Más de 1000]               │    │                              │
│                              │    │                              │
│  ← Atrás       Siguiente →   │    │                              │
└──────────────────────────────┘    └──────────────────────────────┘
```

---

## 🧭 Flujo de preguntas

1. **¿Cuántos clientes activos tienes?** → 6 tramos
   - `0–50` · `51–150` · `151–300` · `301–500` · `501–1000` · `Más de 1000`
2. **¿Tienes más de una sucursal?** → Sí / No (preseleccionado No)
3. (si Sí) **¿Cuántas sedes?** → `1`–`6+`
4. **¿Te interesa controlar el acceso de los clientes con alguna barrera física?** → Sí / No (preseleccionado No)
5. (si Sí) **¿Es una instalación desde 0 para un nuevo centro o quieres adaptar uno o más tornos que ya tienes instalados?**
6.    (nueva) **¿Qué tipo de barrera quieres implementar?** → Torno / Cerradura
7.       (torno) **¿Cuántos tornos necesitas?** → 1–5
8.    (adaptación) **¿Qué tienen actualmente instalado?** → Torno / Puerta (preseleccionado Torno)
9.       (adap+torno) **¿Cuántos tornos hay que adaptar?** → 1–5
10. (si accesos Sí) **¿Cómo quieres que se identifiquen tus clientes?** → QR + Proximidad / Face-ID
11. **¿Cómo prefieres pagar?** → Anual −20% (recomendado, pulso naranja) / Mensual

Defaults silenciosos (no se preguntan, se aplican):

| Concepto | Default |
|---|---|
| App móvil | Starter (gratis) |
| Implantación | Avanzado |
| Modelo de torno | Aspas (MTS1000) |
| Portillo | No |
| Qué controlar | Solo entrada |
| Modalidad | Anual |

---

## 💰 Tarifa de licencias (unificada)

| Clientes activos | €/mes | €/año (−20%) |
|---|---:|---:|
| 0–50 | 99,90 € | 959,04 € |
| 51–150 | 169,90 € | 1.631,04 € |
| 151–300 | 189,90 € | 1.823,04 € |
| 301–500 | 209,99 € | 2.015,90 € |
| 501–1000 | 239,99 € | 2.303,90 € |
| Más de 1.000 | 299,99 € | 2.879,90 € |

**Multisede**: licencia × nº de sedes (a partir de 6 sedes la tarifa es a medida).
**Anual**: −20 % sobre licencia y app, pago a la firma.
**IVA**: aplica solo en España peninsular y Baleares.

---

## 🧱 Construcción progresiva del desglose

El panel derecho **arranca vacío** y solo se llena tras el primer click consciente del usuario:

- Click en un tramo de clientes → aparece la línea de licencia
- Avanza a multisede → si elige Sí, aparece "× N sedes"
- Avanza a accesos → si elige No, salta directo a Modalidad
- Si elige Sí accesos + Torno → aparece la línea del torno
- Si elige QR + Proximidad → se añaden controladora, lector RFID y pulsadores
- Si elige Face-ID → se añaden lectores Face-ID + soportes
- Al pulsar la modalidad (Anual o Mensual) → aparecen arriba los totales destacados y, durante 5 s, una flecha animada apunta hacia ellos.

---

## 🔗 URL única por interacción

Cada click y cada navegación generan una **entrada de historial única** vía `pushState`. La URL contiene todo el estado del wizard:

```
?step=acc_disp&clientes=500&multisede=no&sedes=1&modalidad=anual&accesos=1&acc_tipo=nueva&acc_disp=torno&acc_qty=1
```

- **Botón Atrás del navegador**: retrocede entre pasos del wizard. Cuando llega antes del wizard, aparece un modal "¿Salir del configurador?".
- **Compartir URL**: al recargar, el usuario aterriza en el mismo paso que estaba — pero el panel derecho **arranca siempre vacío** hasta el primer click consciente (evita confusión con importes "fantasma").
- **Botón Reset** (arriba a la izquierda): navega a la URL base sin query params y arranca de cero.

---

## 🚀 Despliegue en GitHub Pages

1. Crea un repo público en [github.com/new](https://github.com/new) (ej. `wizard-tarifas-supersonik`).
2. Arrastra `index.html` y `README.md` al repo (no requiere terminal).
3. **Settings → Pages**: source `Deploy from a branch`, branch `main` `/` (root), **Save**.
4. Espera 1-2 min → tu URL pública estará lista (ej. `https://tu-usuario.github.io/wizard-tarifas-supersonik/`).

---

## 📂 Estructura del proyecto

```
.
├── index.html      ← TODO va aquí: HTML + CSS + JS vanilla
├── README.md       ← Esta documentación
└── .gitignore
```

Sin dependencias externas (excepto la fuente Host Grotesk de Google Fonts y el logo de Trainingym en la cabecera). Sin build, sin npm, sin nada.

---

## ⚙️ Stack técnico

- **HTML/CSS/JS vanilla** — un solo archivo
- **Tipografía**: Host Grotesk (Google Fonts)
- **Sin frameworks** (no React, no Vue, no jQuery)
- **Sin localStorage/sessionStorage** — todo el estado se sincroniza en la URL
- **Responsive**: layout de 2 columnas en desktop, columna única con bottom-sheet de desglose en móvil

---

## 📝 Disclaimer

> Esta tarifa no contempla personalizaciones del software ni adaptaciones específicas del control de accesos. Para esos casos te atenderemos personalmente.

---

*Supersonik · Configurador de tarifas paso a paso*
