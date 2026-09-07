## 🚀 ¡Flashea tu dispositivo ahora mismo!

Para empezar a usar el firmware de inmediato sin complicaciones, utiliza nuestra herramienta oficial de configuración y flasheo desde tu navegador:
👉 **[Mackm Web Flasher](https://mackmwebflasher.netlify.app)**

---

## 🎮 ¿Qué mandos y dispositivos soporta el Firmware?

Nuestro firmware es una bestia todoterreno. Implementa decodificadores avanzados y adaptadores de inyección específicos para los **3 protocolos principales de la industria gaming**, garantizando una compatibilidad masiva:

### 🟢 1. Ecosistema Xbox (Protocolo GIP - Xbox One / Xbox Series)

Soporte total para mandos con protocolo GIP.

* **Mandos Oficiales de Microsoft:**
* Mando inalámbrico Xbox One *(vía cable USB).*
* Mando inalámbrico Xbox Series X|S *(vía cable USB-C).*
* Mandos Premium: Xbox Elite Series 1 y Elite Series 2.


* **Mandos Licenciados de Terceros:**
* **PowerA:** Enhanced, Fusion Pro, Spectra.
* **Scuf:** Instinct, Prestige.
* **GameSir:** G7 SE, G7 HE, T4 Cyclone *(en modo Xbox).*
* **Turtle Beach:** Recon, React-R.



### 💻 2. Mundo PC y XInput (Xbox 360)

* **Familia 8BitDo:** Ultimate 2C (Wired / 2.4G), Pro 2, Ultimate *(en modo XInput).*
* **Clásicos y Genéricos:** Mandos oficiales de Xbox 360, clones y cualquier control genérico para PC con protocolo XInput.
* 🧠 *Detalle técnico:* Cuenta con emulación nativa del descriptor **XUSB20 de Microsoft OS 1.0**, asegurando el enlace automático y transparente de drivers en Windows.

### 🔵 3. Ecosistema PlayStation (Protocolo Sony HID)

* **PlayStation 4:** Soporte para todos los modelos originales de DualShock 4 (CUH-ZCT1 y CUH-ZCT2).
* **PlayStation 5:** Soporte para DualSense y DualSense Edge.
* 🧠 *Detalle técnico:* Detección automática del *layout* de PS5, con soporte para el stick de 8 bits y mapeo preciso de gatillos adaptativos / touchpad.

### 🖱️ 4. Periféricos USB (Modo Ratón)

Compatible con cualquier ratón USB, desde modelos de oficina hasta hardware de grado eSports:

* **Logitech:** G Pro X Superlight, G502, G403, G305, etc.
* **Razer:** DeathAdder, Viper, Basilisk, Cobra.
* **Otras marcas premium:** Glorious, Zowie, SteelSeries, Corsair, Finalmouse.
* 🧠 *Detalle técnico:* Soporta tanto reportes *Boot Mouse estándar* (coordenadas de 8 bits) como protocolos de alta resolución con *Report ID* para ratones gaming (coordenadas de 16 bits).

---

## 🛡️ Passthrough 100% Indetectable para Consolas Xbox

**¿Conectas un mando oficial de Xbox y Makcu directamente a tu consola Xbox? 👉 SÍ FUNCIONA.**

Las consolas Xbox (One y Series X|S) cuentan con medidas de seguridad estrictas, exigiendo un chip criptográfico para responder a constantes desafíos de autenticación. Makcu supera esto de forma brillante:

* **Ingeniería de Reenvío Transparente:** La arquitectura de Makcu (a través de `pass_usb_device.c` y `PassUsbHost.cpp`) realiza un bypass transparente de las transferencias de control (`FRAME_CTRL_SETUP`) y los paquetes de salida (`FRAME_EP_OUT`).
* **Validación Física:** Cuando la consola envía los retos de seguridad, Makcu los redirige inmediatamente al mando físico conectado en el puerto derecho. El mando real procesa el desafío, responde, y la consola valida la conexión con éxito.
* **Inyección Perfecta:** La inyección de puntería (`km.move`) sobre el stick analógico se fusiona matemáticamente con el flujo de datos legítimo, **sin romper jamás la firma criptográfica**.

---

## 📺 Mira a Makcu en Acción

¿Quieres ver cómo funciona todo esto en la práctica? Échale un vistazo a nuestra demostración:

[](https://www.youtube.com/watch?v=yLCxIQ9p8EI)
*Haz clic [aquí para ver el video en YouTube](https://www.youtube.com/watch?v=yLCxIQ9p8EI).*
