# TestFlight — Instrucciones de revisión y prueba
# Smart Hotels App (com.nexotechnologies.smarthotels)

## ──────────────────────────────────────────────────────────
## A) INFORMACIÓN PARA APPLE REVIEW (Beta App Review Information)
##    Copiar exactamente en App Store Connect → TestFlight →
##    "Beta App Review Information" → Notes
## ──────────────────────────────────────────────────────────

### Demo Credentials
Username: demo
PIN: 1234

### Notes for the reviewer
Smart Hotels is a professional tool for hotel housekeeping staff to control
motorized smart beds via Bluetooth and a local Wi-Fi hub (Raspberry Pi).
The production setup requires physical hardware, so a **fully functional
demo mode** is built into the app for review purposes.

**How to activate demo mode:**
1. Launch the app. The login screen appears.
2. Tap the small "DEMO" badge in the bottom-right corner of the login screen
   (or enter the credentials above and tap "Entrar").
3. The app switches to demo mode automatically: no Wi-Fi hub or Bluetooth
   hardware is required.

**What you can review in demo mode:**
- Full login / session flow (username + PIN).
- Bed scanner screen listing 5 simulated beds (rooms 101, 102, 103, 204, 305).
- Bed control screen: raise / lower / stop commands with animated state feedback.
- Error state display (room 305 shows a simulated OVERCURRENT alert).
- Voice command feature (microphone permission prompt + tap-to-speak control).
- Push notification permission request flow.
- Hub settings screen (IP address configuration).
- Help screen.

**Bluetooth / Location permissions:**
The app will request Bluetooth and Location permissions on first launch.
These are needed for BLE scanning in production. In demo mode they are not
actively used but the permission dialogs will still appear — this is expected.

**Network permission:**
The app requests local network access to reach the Raspberry Pi hub. In demo
mode no real connection is attempted.

**No account creation required.** The demo user 'demo / 1234' is embedded
in the app.


## ──────────────────────────────────────────────────────────
## B) DESCRIPCIÓN PARA TESTERS (Beta App Description)
##    Copiar en App Store Connect → TestFlight →
##    "Beta App Description"
## ──────────────────────────────────────────────────────────

**ES:**
Smart Hotels permite al personal de limpieza de un hotel controlar camas
elevables motorizadas de forma segura y eficiente. Conéctate a las camas
por Bluetooth o a través del hub del hotel, eleva/baja la cama con un toque
o usando comandos de voz, y recibe alertas en tiempo real sobre el estado
del equipamiento.

En esta versión beta:
- Nuevo flujo de inicio de sesión con PIN.
- Modo demo integrado (sin hardware) para evaluación y formación.
- Comandos de voz en español ("sube", "baja", "para").
- Notificaciones push de alertas de cama.

**EN:**
Smart Hotels lets hotel housekeeping staff safely and efficiently control
motorized adjustable beds. Connect to beds via Bluetooth or through the
hotel hub, raise/lower the bed with a tap or voice commands, and receive
real-time equipment alerts.

In this beta:
- New PIN-based login flow.
- Built-in demo mode (no hardware needed) for evaluation and training.
- Spanish voice commands ("sube", "baja", "para").
- Push notification alerts for bed status.


## ──────────────────────────────────────────────────────────
## C) USUARIOS DEMO DISPONIBLES
## ──────────────────────────────────────────────────────────

| Usuario | PIN  | Notas                     |
|---------|------|---------------------------|
| demo    | 1234 | Usuario de revisión Apple  |
| maria   | 1234 | Perfil camarera           |
| carlos  | 5678 | Perfil camarera           |
| ana     | 0000 | Perfil camarera           |

Todos los usuarios ven las mismas 5 camas simuladas:
- Habitación 101 → estado DOWN (normal)
- Habitación 102 → estado UP (normal)
- Habitación 103 → estado MIDDLE (normal)
- Habitación 204 → estado DOWN (normal)
- Habitación 305 → estado UP + error OVERCURRENT (para probar alertas)


## ──────────────────────────────────────────────────────────
## D) FLUJO RECOMENDADO PARA REVISOR (paso a paso)
## ──────────────────────────────────────────────────────────

1. Abrir la app.
   → Aparece pantalla de login oscura con logo.

2. Introducir:  Usuario: demo  |  PIN: 1234  →  Tocar "Entrar".
   → La app navega al escáner de camas.

3. En la pantalla del escáner:
   - Comprobar que aparecen las camas 101, 102, 103, 204, 305.
   - La cama 305 muestra un icono de alerta (OVERCURRENT).
   - Tocar cualquier cama (p. ej. habitación 101).

4. En la pantalla de control de cama:
   - Tocar el botón "▲ SUBIR" → la cama anima de DOWN a RAISING y luego UP.
   - Tocar "■ PARAR" → la cama se detiene.
   - Tocar "▼ BAJAR" → la cama baja de vuelta a DOWN.

5. Probar comandos de voz:
   - Tocar el botón de micrófono.
   - Decir "sube" → la cama ejecuta la subida.
   - Decir "para" → la cama se detiene.
   (Requiere conceder permiso de micrófono si no se ha hecho antes.)

6. Volver al escáner (botón atrás) → tocar habitación 305.
   → Se muestra el estado de error OVERCURRENT con su descripción.

7. Abrir ajustes (icono ⚙️ arriba a la derecha):
   → Aparece el diálogo de configuración del hub (IP y puerto).
   → No es necesario modificar nada en modo demo.

8. Abrir ayuda (icono ? arriba):
   → Pantalla de instrucciones de uso.


## ──────────────────────────────────────────────────────────
## E) INSTRUCCIONES PARA TESTERS (What to Test / Feedback)
##    Copiar en App Store Connect → TestFlight →
##    "What to Test" (campo de texto libre por build)
## ──────────────────────────────────────────────────────────

### ES — Qué probar en esta versión

Gracias por participar en las pruebas de Smart Hotels. Por favor, centra
tu feedback en los siguientes escenarios:

**1. Login y sesión**
- Accede con tus credenciales de prueba (usuario: `demo`, PIN: `1234`).
- Cierra sesión (menú → Cerrar sesión) y vuelve a entrar.
  → ¿La sesión se recuerda correctamente entre cierres de la app?

**2. Escáner de camas**
- Abre el escáner y verifica que aparecen las habitaciones 101–305.
- *(Con hardware real)* Acércate a una cama con Bluetooth activado.
  → ¿La cama aparece en la lista y la señal es estable?
- *(Sin hardware)* Usa el modo demo (botón DEMO en login).

**3. Control de cama**
- Toca una cama → pantalla de control.
- Prueba **Subir**, **Parar** y **Bajar** en ese orden.
  → ¿El estado (UP / DOWN / MOVING) se actualiza correctamente?
- Espera sin hacer nada 30 segundos.
  → ¿La app sigue respondiendo o se queda colgada?

**4. Comandos de voz**
- Toca el botón de micrófono y di **"sube"**, **"baja"** o **"para"**.
  → ¿El comando se reconoce y ejecuta bien?
- Prueba en un entorno con algo de ruido de fondo.
  → ¿Hay falsos positivos o falta de respuesta?

**5. Alertas y errores**
- Selecciona la habitación **305** (tiene un error simulado OVERCURRENT).
  → ¿Se muestra el aviso de error claramente?
- Activa el modo avión y luego intenta conectar.
  → ¿La app muestra un mensaje de error comprensible y no se cuelga?

**6. Notificaciones push**
- Acepta el permiso de notificaciones cuando se solicite.
  → ¿Recibes la notificación de prueba enviada desde el hub?
- *(Si no tienes hub)* Comprueba que el permiso se solicita sin errores.

**7. Rendimiento y estabilidad**
- Usa la app durante al menos 5 minutos seguidos.
- Pon la app en segundo plano y vuelve a abrirla.
  → ¿Recupera el estado correctamente?
- Prueba en condiciones de señal Wi-Fi débil (aleja el dispositivo del router).

---

### EN — What to Test in this Build

Thank you for beta-testing Smart Hotels. Please focus your feedback on
the following scenarios:

**1. Login & session persistence**
- Log in with test credentials (username: `demo`, PIN: `1234`).
- Log out (⚙️ menu → Log out) and log back in.
  → Does the app remember your session correctly between restarts?

**2. Bed scanner**
- Open the scanner and check that rooms 101–305 appear.
- *(With real hardware)* Walk near a bed with Bluetooth on.
  → Does the bed appear in the list with a stable signal?
- *(Without hardware)* Use demo mode (DEMO button on login screen).

**3. Bed control**
- Tap a bed → control screen.
- Test **Raise**, **Stop** and **Lower** in sequence.
  → Does the status (UP / DOWN / MOVING) update correctly?
- Leave the screen idle for 30 seconds.
  → Does the app stay responsive?

**4. Voice commands**
- Tap the microphone button and say **"sube"**, **"baja"** or **"para"**.
  → Is the command recognised and executed correctly?
- Try in a noisy environment.
  → Are there false triggers or missed commands?

**5. Alerts and errors**
- Select room **305** (simulated OVERCURRENT error).
  → Is the error displayed clearly?
- Enable airplane mode and try to connect.
  → Does the app show a clear error without freezing?

**6. Push notifications**
- Accept the notification permission when prompted.
  → Do you receive the test notification from the hub?

**7. Performance and stability**
- Use the app for at least 5 consecutive minutes.
- Background the app and return to it.
  → Does it restore state correctly?

---

### Cómo enviar feedback / How to send feedback

- **Capturas de pantalla:** mantén presionada la pantalla con dos dedos en
  TestFlight para adjuntar una captura directamente al reporte.
- **Bugs:** usa el shake gesture (agitar el dispositivo) para abrir el
  formulario de feedback de TestFlight con los logs adjuntos automáticamente.
- **Contacto directo:** support@nexotechnologies.es

### Limitaciones conocidas en esta beta / Known limitations

| # | Descripción | Impacto |
|---|-------------|---------|
| 1 | El modo demo no simula latencia de red variable | Bajo |
| 2 | Los comandos de voz sólo reconocen español (es_ES) | Medio |
| 3 | Sin hub real, las notificaciones push no se envían | Bajo |
| 4 | Primera conexión BLE en iOS puede tardar hasta 15 s | Bajo |


## ──────────────────────────────────────────────────────────
## F) CHECKLIST ANTES DE SUBIR EL BUILD A TESTFLIGHT
## ──────────────────────────────────────────────────────────

- [ ] URL de política de privacidad configurada en App Store Connect:
      https://danielms812.github.io/smartbed-legal/
- [ ] Bundle ID coincide: com.nexotechnologies.smarthotels
- [ ] ITSAppUsesNonExemptEncryption = false (ya en Info.plist)
- [ ] Firebase GoogleService-Info.plist incluido en el bundle
- [ ] Modo demo accesible sin hardware externo
- [ ] Todos los permisos con NSUsageDescription en Info.plist:
      ✓ NSBluetoothAlwaysUsageDescription
      ✓ NSMicrophoneUsageDescription
      ✓ NSSpeechRecognitionUsageDescription
      ✓ NSLocalNetworkUsageDescription
      ✓ NSLocationAlwaysAndWhenInUseUsageDescription
      ✓ NSLocationWhenInUseUsageDescription
- [ ] Versión y build number incrementados respecto al build anterior
