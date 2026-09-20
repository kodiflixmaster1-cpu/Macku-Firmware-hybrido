# 🚀 ¡Flashea tu dispositivo ahora mismo!

Para empezar a usar el firmware sin complicaciones:  
👉 **[Makcu Web Flasher](https://web-flasher-render.onrender.com)**  

Configura curvas y macros directo en la memoria de tu Makcu:  
👉 **[Makcu Configurator](https://makcu-configurator.onrender.com/)**  

---

## 📋 Lista Completa de Controles Soportados

| Periférico / Mando | VID : PID | Modo Requerido | Tipo Firmware | Soporte HW | Comportamiento Técnico |
|--------------------|-----------|----------------|---------------|------------|------------------------|
| **Sony PS5 DualSense** | `054C:0CE6` | USB Cable | DS5 | 🟢 100% Completo | Reportes de 64 bytes, curvas, recoil y mods |
| **Sony PS5 DualSense Edge** | `054C:0DF2` | USB Cable | DS Edge | 🌟 Exclusivo Pro | Paletas traseras y botones Fn transmitidos a telemetría |
| **Sony PS4 DualShock 4 V2** | `054C:09CC` | USB Cable | DS4 | 🟢 100% Completo | Detección automática con `detect_ds4()`, soporte total |
| **Xbox Series X/S** | `045E:0B12` | USB Cable | GIP | 🟢 100% Completo | Protocolo GIP nativo, cambio de slots HW |
| **Xbox Elite Series 2** | `045E:0B00` | USB Cable | GIP | 🟢 100% Completo | Sticks analógicos 16 bits, paletas procesadas por HW |
| **Xbox 360 Controller** | `045E:02E8` | USB Cable | XInput | 🟢 100% Completo | Reportes estándar de 20 bytes en `apply_xinput()` |
| **GameSir Tarantula Pro** | `3537:103D` | Modo PC/XInput | XInput | 🟢 100% Completo | Curvas, recoil, rapidfire y sticky aim |
| **GameSir G7 / SE / Kaleid / Cyclone** | `3537:1073` etc. | Modo Xbox/PC | GIP/XInput | 🟢 100% Completo | Procesamiento completo en ambos modos |
| **Razer Wolverine V3 Tournament** | `1532:0A45` | Xbox/PC | GIP/XInput | 🟢 100% Completo | Licenciado Xbox, soporte total |
| **8BitDo Ultimate / Pro 2** | `2DC8:xxxx` | XInput | XInput | 🟢 100% Completo | Reconocimiento automático ultrarrápido |
| **Logitech G PRO Wireless** | `046D:C08C` | USB Cable | Mouse | 🟢 100% Ratón | Procesado en `apply_mouse()` |
| **Logitech LIGHTSPEED Receiver** | `046D:C547` | Dongle USB | Mouse | 🟢 100% Ratón | Reconocido como ratón gaming |
| **Teclados USB Gaming** | HID estándar | USB Cable | Keyboard | 🟢 100% Teclado | Passthrough + comandos remotos |
| **SCUF Envision / Pro** | `2E95:434D` | USB Cable | HID | 🟡 Passthrough | Reconocido pero sin curvas locales |
| **Nintendo Switch Pro** | `057E:2009` | USB Cable | HID | 🟡 Passthrough | Retransmisión limpia sin curvas |
| **DragonRise / SHANWAN Gamepad** | `0079:0122` | DirectInput | HID | 🟡 Passthrough | Entradas intactas, sin confusión con ratones |

---

## 🖱️ Ratones Compatibles
- Logitech G Pro, G502, G305, G903  
- Razer Viper, DeathAdder, Basilisk  
- Glorious Model O/D/I  
- SteelSeries Aerox, Rival, Prime  
- Corsair Katar, M65, Harpoon  
- Zowie / Vaxee / Pulsar / Finalmouse  

> ⚠️ Si usas ratones de 4000 Hz u 8000 Hz, configúralos a **1000 Hz** para máxima estabilidad.

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
