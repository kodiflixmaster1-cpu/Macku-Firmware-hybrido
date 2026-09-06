1. ¿Para qué mandos y dispositivos funciona este Firmware?

El firmware implementa decodificadores y adaptadores de inyección específicos para los 3 protocolos principales de la industria:

A. Mandos de Xbox (Protocolo GIP - Xbox One / Xbox Series)

Mandos Oficiales de Microsoft:
Mando inalámbrico Xbox One (conectado por cable USB).
Mando inalámbrico Xbox Series X|S (conectado por cable USB-C).
Mandos Xbox Elite Series 1 y Elite Series 2.
Mandos Licenciados de terceros con protocolo GIP:
PowerA (Enhanced, Fusion Pro, Spectra).
Scuf (Instinct, Prestige).
GameSir (G7 SE, G7 HE, T4 Cyclone en modo Xbox).
Turtle Beach (Recon, React-R).

B. Mandos XInput (Xbox 360 y controles para PC)

Mandos 8BitDo:
8BitDo Ultimate 2C (Wired / 2.4G).
8BitDo Pro 2 / Ultimate (en modo XInput).
Mandos oficiales Xbox 360 y clones:
Controles genéricos para PC con protocolo XInput.
Cuenta con emulación del descriptor XUSB20 de Microsoft OS 1.0 para enlace automático de drivers en Windows.

C. Mandos de PlayStation (Protocolo Sony HID)

DualShock 4 (PS4):
Todos los modelos originales de PS4 (CUH-ZCT1 y CUH-ZCT2).
DualSense / DualSense Edge (PS5):
Detección automática del layout DS5 (stick de 8 bits y mapeo de gatillos adaptativos / touchpad).

D. Ratones USB (Modo Mouse)

Cualquier ratón USB estándar y Gamer:
Logitech: G Pro X Superlight, G502, G403, G305, etc.
Razer: DeathAdder, Viper, Basilisk, Cobra.
Otras marcas: Glorious, Zowie, SteelSeries, Corsair, Finalmouse, o ratones de oficina genéricos.
Soporta reportes Boot Mouse estándar (coordenadas de 8 bits) y ratones gaming de alta resolución con Report ID (coordenadas de 16 bits).

2. ¿Tiene passthrough hacia consolas Xbox?
Conectas un Mando Oficial de Xbox y Makcu a la consola Xbox 👉 SÍ FUNCIONA

Las consolas Xbox (Xbox One y Xbox Series X|S) exigen un chip criptográfico de seguridad de Microsoft que responde a desafíos de autenticación continuos.
La arquitectura de Makcu en pass_usb_device.c y PassUsbHost.cpp realiza un reenvío transparente de las transferencias de control (FRAME_CTRL_SETUP) y los paquetes de salida (FRAME_EP_OUT).
Cuando la consola Xbox envía los retos de autenticación, Makcu los transfiere al mando físico conectado en el puerto derecho. El mando real responde y la consola valida la conexión. La inyección de puntería (km.move) sobre el stick analógico se suma al flujo de datos sin romper la firma criptográfica.


## 📺 Video demostración
[Ver en YouTube](https://www.youtube.com/watch?v=yLCxIQ9p8EI)
