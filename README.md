## 🚀 ¡Flashea tu dispositivo ahora mismo!

Para empezar a usar el firmware de inmediato sin complicaciones, utiliza nuestra herramienta oficial de configuración y flasheo desde tu navegador:
👉 **[Makcu Web Flasher](https://web-flasher-render.onrender.com)**


Configura curvas macros directo en la memoria de tu macku
👉 **[Makcu Configuratorr](https://web-flasher-render.onrender.com](https://makcu-configurator.onrender.com/)**


📋 Lista Completa y Detallada de Controles Soportados por el Firmware

Esta tabla resume cómo el firmware  clasifica e interactúa con cada mando o periférico:

| Periférico / Mando | VID : PID | Modo Requerido en el Mando | Tipo en tu Firmware | Soporte en Hardware (Curvas, Recoil, Mods) | Comportamiento Técnico |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **Sony PS5 DualSense** | `054C:0CE6` | USB Cable | `DEV_TYPE_CONTROLLER` (DS5) | 🟢 **100% Completo** | Reportes de 64 bytes (`0x01`). Curvas de 5 nodos, retroceso, sticky aim rotacional y mods activos. |
| **Sony PS5 DualSense Edge** | `054C:0DF2` | USB Cable | `DEV_TYPE_DS_EDGE` | 🌟 **100% Exclusivo Pro** | Decodificación nativa del byte 10 (`buf[10]`): **paletas traseras L/R y botones Fn** transmitidos a telemetría y consola. |
| **Sony PS4 DualShock 4 V2** | `054C:09CC` | USB Cable | `DEV_TYPE_CONTROLLER` (DS4) | 🟢 **100% Completo** | Detección automática por función `detect_ds4()`. Pleno soporte de mods y curvas. |
| **Xbox Series X \| S** | `045E:0B12` | USB Cable | `DEV_TYPE_CONTROLLER` (GIP) | 🟢 **100% Completo** | Protocolo GIP Microsoft nativo. Cambio de slots por hardware (`Share + D-Pad`) y supresión de botones. |
| **Xbox Elite Series 2** | `045E:0B00` | USB Cable | `DEV_TYPE_CONTROLLER` (GIP) | 🟢 **100% Completo** | Protocolo GIP nativo. Sticks analógicos de 16 bits, gatillos y paletas procesadas por hardware. |
| **Xbox 360 Controller** | `045E:02E8` | USB Cable | `DEV_TYPE_CONTROLLER` (XInput) | 🟢 **100% Completo** | Interfaz XInput (`0xFF/0x5D/0x01`). Reportes estándar de 20 bytes procesados en `apply_xinput()`. |
| **GameSir Tarantula Pro** | `3537:103D` / etc. | **Modo PC / XInput** | `DEV_TYPE_CONTROLLER` (XInput) | 🟢 **100% Completo** *(en Modo PC)* | Al activarlo en modo PC/XInput, el hardware le inyecta curvas, recoil, rapidfire y sticky aim al 100%. |
| **GameSir G7 / G7 SE / Kaleid / Cyclone** | `3537:103D`, `1073`, `2106` | **Modo Xbox / PC** | `GIP` o `XInput` | 🟢 **100% Completo** *(en Modo Xbox/PC)* | Mismo comportamiento: en modo Xbox (GIP) o PC (XInput) recibe todo el procesamiento de hardware. |
| **Razer Wolverine V3 Tournament** | `1532:0A45` | Modo Xbox / PC | `GIP` o `XInput` | 🟢 **100% Completo** | Es mando licenciado Xbox; entra por protocolo GIP o XInput con soporte total de combate. |
| **8BitDo Ultimate / Pro 2 / Clones** | `2DC8:xxxx` | **Modo X (XInput)** | `DEV_TYPE_CONTROLLER` (XInput) | 🟢 **100% Completo** | Reconocimiento automático ultrarrápido con inyección completa. |
| **Logitech G PRO Wireless** | `046D:C08C` | USB Cable | `DEV_TYPE_MOUSE` | 🟢 **100% Ratón** | Clase HID 3, Protocolo 2. Deltas de movimiento procesados en `apply_mouse()`. |
| **Logitech LIGHTSPEED Receiver** | `046D:C547` | Dongle USB | `DEV_TYPE_MOUSE` | 🟢 **100% Ratón** | Receptor inalámbrico reconocido directamente como ratón gaming. |
| **Teclados USB Gaming** | Estándar HID | USB Cable | `DEV_TYPE_KEYBOARD` | 🟢 **100% Teclado** | Clase HID 3, Protocolo 1. Passthrough limpio + comandos remotos (`km.press`, etc.). |
| **SCUF Envision / Envision Pro** | `2E95:434D` / `434E` | USB Cable | `DEV_TYPE_GENERIC_HID` | 🟡 **Passthrough Transparente** | La PC lo reconoce y juegas normal con Corsair iCUE, pero **no recibe curvas ni recoil locales** (usa protocolo de reportes propietario de Corsair). |
| **Nintendo Switch Pro** | `057E:2009` | USB Cable | `DEV_TYPE_GENERIC_HID` | 🟡 **Passthrough Transparente** | Se retransmite sin interferencias hacia la consola/PC, pero sin curvas locales (formato de 12 bits de Nintendo). |
| **DragonRise / SHANWAN Gamepad** | `0079:0122`, `181C` | DirectInput | `DEV_TYPE_GENERIC_HID` | 🟡 **Passthrough Transparente** | Passthrough limpio; nunca se confunden con ratones y mantienen sus entradas intactas. |


⚡ ¿Compatibles con MAKCU y con software que envíe señales por UART (Ultravision, Sunone version by Derian, DMA, DS4Windows version by Derian)?

La arquitectura del firmware fue construida específicamente para este caso de uso:

```
[Mando Físico (PS5 / Xbox / GameSir)] 
              ↓ (USB3 Host)
    [ESP32-S3 Right]
              ↓ (IPC UART a 4 Mbps)
    [ESP32-S3 Left] ←── (Comandos UART: km.move, km.mask, km.trim) ── [PC / DMA / Ultravision / Sunone / DS4Windows]
              ↓ (USB1 Device TinyUSB)
   [Consola (PS5/Xbox) o PC de Juego]


¿Por qué funciona con CUALQUIER software externo por UART?

1. **El protocolo `km.*` es universal:**
   Todos los softwares mencionados (**Ultravision Cuda/DML**, **Sunone version by Derian**, **clientes DMA 2-PC** y tu versión modificada de **DS4Windows version by Derian**) se comunican con MAKCU enviando cadenas estándar por el puerto COM serie a 4,000,000 baud (CH343):
   * `km.move(dx, dy)` → Inyección de puntería / aimbot.
   * `km.mask(btn, mode)` → Supresión de botones físicos.
   * `km.trim(x, y)` → Compensación de punto de mira.

2. **Fusión Asimétrica Inteligente en `km_inject.c`:**
   En los mandos **PlayStation (DS4, DualSense, DualSense Edge)** y **Xbox (GIP, XInput, GameSir, 8BitDo)**, el firmware realiza una **mezcla en tiempo real** (*stick blending*):
   * Si tú mueves el stick físico con la mano y al mismo tiempo el software externo (**Ultravision** o **Sunone**) envía una corrección de puntería por UART, el firmware **combina ambas señales de forma continua sin que el juego note saltos ni tartamudeos**.

3. **El Modo Especial "Slot 4 — Mando Limpio / Bypass PC" (`0x40`):**
   Tu firmware incluye un modo pensado exactamente para software DMA y de PC:
   * Al seleccionar el **Slot 4** (ya sea desde el Web Configurator o pulsando `Share + D-Pad Izquierda` en el mando), el hardware **apaga el recoil y las curvas internas del ESP32**.
   * De este modo, el mando queda completamente "puro" para que softwares como **Ultravision**, **Sunone version by Derian** o **DS4Windows version by Derian**, **DMA**  tengan el **100% del control del apuntado sin que las curvas del hardware colisionen con los cálculos del aimbot en PC**.
   
   
   
   

## 1. 🖱️ Ratones USB Soportados (`DEV_TYPE_MOUSE`)

### ¿Cómo los detecta el firmware?
* **Clase USB:** `0x03` (HID).
* **Protocolo:** `0x02` (Mouse).
* Lo identifica automáticamente como `is_mouse_device_ = true;` y lo envía a Left como **`DEV_TYPE_MOUSE`**.

### Protocolos y Formatos de Reporte que procesa `apply_mouse()`:
1. **Ratones Gaming de Alta Resolución (Deltas de 16 bits):** Procesa coordenadas relativas `X, Y` de alta precisión (-32767 a +32767).
2. **Ratones Estándar (Deltas de 8 bits):** Coordenadas clásicas (-127 a +127).
3. **Soporte de Report ID (`0x01` / `0x02`):** Detecta automáticamente si el paquete inicia con Report ID (muy común en ratones gaming modernos).
4. **Hasta 5 Botones Físicos + Clics Inyectados:** Fusión de clic izquierdo, derecho, central y laterales con clics remotos (`km.click`, `km.left`, `km.right`).

### Marcas y Modelos de Ratones Compatibles:
* **Logitech G:** G Pro Wireless, G Pro X Superlight (1 y 2), G502 (Hero/Lightspeed), G305, G403, G703, G903 (cableados o con dongle USB LIGHTSPEED).
* **Razer:** Viper (V2 Pro, V3 Pro, Mini, Ultimate), DeathAdder (V2, V3, Essential), Basilisk, Naga.
* **Glorious:** Model O, Model D, Model I (cableados y wireless con dongle 2.4 GHz).
* **SteelSeries:** Aerox 3/5/9, Rival 3/5/600, Prime.
* **Corsair:** Katar Pro, M65, Harpoon, Scimitar, Dark Core.
* **Zowie / Vaxee:** Series EC, FK, ZA, S (100% plug & play sin software requerido).
* **Pulsar / Lamzu / Endgame Gear / Ninjutso / Finalmouse:** Cualquier ratón USB HID estándar (cableado o dongle 2.4 GHz).

> ⚠️ **Recomendación de Polling Rate:** Si usas un ratón de 4000 Hz u 8000 Hz (ej. Razer 8K), configúralo a **1000 Hz** en su software antes de conectarlo a MAKCU para máxima estabilidad con el USB del microcontrolador.


2. ⌨️ Teclados USB Soportados (`DEV_TYPE_KEYBOARD`)

### ¿Cómo los detecta el firmware?
* **Clase USB:** `0x03` (HID).
* **Protocolo:** `0x01` (Keyboard).
* Lo clasifica como `is_keyboard_device_ = true;` y lo envía a Left como **`DEV_TYPE_KEYBOARD`**.

### Protocolos que procesa `apply_keyboard()`:
1. **Reportes Estándar USB Boot Keyboard de 8 bytes:**
   * **Byte 0:** Teclas modificadoras (Ctrl Izq/Der, Shift Izq/Der, Alt, AltGr, GUI/Windows).
   * **Byte 1:** Reservado (0x00).
   * **Bytes 2 al 7:** Hasta 6 teclas simultáneas (6KRO) con keycodes USB universales.
2. **Fusión Inteligente de Teclas:**
   * Si tú mantienes presionado **WASD** físicamente en tu teclado, el firmware **respeta tus pulsaciones físicas** y añade en los bytes libres (`buf[i] == 0`) las teclas que envíe el software externo por UART (`km.press`, `km.down`, `km.up`) sin soltar las tuyas.

### Marcas y Teclados Compatibles:
* **Teclados Mecánicos y Custom:** Keychron, Ducky, Akko, Varmilo, Epomaker, Royal Kludge, Glorious GMMK.
* **Logitech G:** G Pro Keyboard, G915, G413, G512, G213.
* **Razer:** Huntsman (Mini, V2, Analog), BlackWidow, DeathStalker, Cynosa.
* **Corsair:** K70, K65, K60, K55, K100 (en modo estándar/bios).
* **SteelSeries:** Apex Pro, Apex 7, Apex 3.
* **Wooting:** 60HE, Two HE (en modo USB estándar).
* Cualquier teclado de membrana o mecánico USB estándar con protocolo HID.

---

## 3. ¿Cómo interactúan con el Software UART (DMA, Ultravision, Sunone, DS4Windows)?

Cuando conectas un **ratón** en el puerto USB3 de entrada física de MAKCU:

  **Con Ratón conectado:**
   * Las señales de movimiento físico de tu mano van a la PC.
   * Si **Ultravision**, **Sunone** o un software de puntería **DMA** envían comandos `km.move(dx, dy)`, el firmware ejecuta la función `apply_mouse()`: **suma los deltas del software (`inj_x, inj_y`) a los deltas reales de tu mano**.
   * Resultado: Movimiento humano asistido con micro-correcciones instantáneas por hardware.


## 📌 Recordatorio de Conexión Física (USB 1:1)

El puerto **USB3** de MAKCU opera en modo **enlace punto a punto 1:1**:
* Puedes conectar **1 dispositivo físico a la vez** (tu mando preferido o tu ratón)
## 📺 Mira a Makcu en Acción

¿Quieres ver cómo funciona todo esto en la práctica? Échale un vistazo a nuestra demostración:

[](https://www.youtube.com/watch?v=RvRYKfn_mKU)
*Haz clic [aquí para ver el video en YouTube](https://www.youtube.com/watch?v=RvRYKfn_mKU).*
