# 🚀 ¡Flashea tu dispositivo ahora mismo!

Para empezar a usar el firmware sin complicaciones, utiliza nuestra herramienta oficial de configuración y flasheo desde tu navegador:  
👉 **[Makcu Web Flasher](https://web-flasher-render.onrender.com)**

Configura curvas y macros directo en la memoria de tu Makcu:  
👉 **[Makcu Configurator](https://makcu-configurator.onrender.com/)**

---

## 📋 Controles Soportados
Esta tabla resume cómo el firmware clasifica e interactúa con cada mando o periférico:

|| Periférico / Mando | VID : PID | Modo Requerido en el Mando | Tipo en tu Firmware | Soporte en Hardware (Curvas, Recoil, Mods) | Comportamiento Técnico |
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

---

## 🖱️ Ratones Compatibles
- Logitech G Pro, G502, G305, G903  
- Razer Viper, DeathAdder, Basilisk  
- Glorious Model O/D/I  
- SteelSeries Aerox, Rival, Prime  
- Corsair Katar, M65, K70  
- Zowie / Vaxee / Pulsar / Finalmouse  

> ⚠️ Recomendación: si usas ratones de 4000 Hz u 8000 Hz, configúralos a **1000 Hz** para máxima estabilidad.

---

## ⌨️ Teclados Compatibles
- Keychron, Ducky, Akko, Epomaker  
- Logitech G Pro, G915, G413  
- Razer Huntsman, BlackWidow  
- Corsair K70, K100  
- SteelSeries Apex Pro, Apex 7  

---

## 📺 Mira a Makcu en Acción
¿Quieres ver cómo funciona todo esto en la práctica?  
Échale un vistazo a nuestra demostración:

[![Demo en YouTube](https://img.youtube.com/vi/sGvmNrihHaU/0.jpg)](https://www.youtube.com/watch?v=sGvmNrihHaU)

---

## 📌 Recordatorio de Conexión
- Puerto **USB3** → entrada de mando o ratón  
- Puerto **USB1** → salida hacia consola/PC  
- Slot 4 → modo limpio para software externo (DMA, Ultravision, Sunone, DS4Windows)
