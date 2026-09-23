# MEMORY — Soporte técnico BRC PRO TECH

Notas acumulativas entre sesiones de Claude Code para tareas de soporte técnico
de Andrés (BRC PRO TECH) que no son cambios de código en este repo, pero que
conviene tener a mano en cualquier sesión.

---

## Biométrico Hikvision DS-K1T331W — Cliente Cocrear

**Estado (última actualización: 2026-09-23)**

- Equipo: Hikvision DS-K1T331W, reconocimiento facial + huella dactilar.
  Interfaz del equipo ya configurada en español.
- Se reinstaló IVMS-4200 en la PC de administración de Cocrear. El software
  perdió su base de datos local, pero el equipo conserva todos los datos
  internos (usuarios, huellas, caras) en su memoria.
- Flujo de recuperación:
  1. Volver a agregar el dispositivo en Gestión de Dispositivos (IP + usuario/clave admin del equipo).
  2. En Gestión de Personal, usar "Obtener desde Dispositivo" / "Get from Device"
     para traer los perfiles existentes a la base local del software nuevo.
- Se dio de alta un empleado de prueba en IVMS para validar el flujo de alta
  end-to-end.

**Bloqueo abierto:** no aparece el botón "Aplicar a Dispositivo" / "Apply to
Device" para enviar ese empleado (foto/huella) al biométrico.

Hipótesis a verificar en la próxima sesión, en este orden:
1. Que la persona no esté en la misma Área/Organización que el dispositivo
   dentro de IVMS (el dispositivo se agrega a un Área específica; si el
   empleado quedó en otra, no aparece la opción).
2. Que el flujo correcto pase por el módulo **Control de Acceso** → **Grupo
   de Personal** ("Person Group") en lugar de por Gestión de Personal
   ("Person") — en algunas versiones de IVMS el botón "Aplicar Todo al
   Dispositivo" solo está ahí.
3. Que el equipo no figure "En línea" (verde) en Gestión de Dispositivos en
   ese momento.
4. Que falte tildar el checkbox de la fila del empleado antes de que el
   botón se habilite (a veces queda gris/inactivo).

**Pendiente de confirmar con Andrés:** en qué módulo exacto está parado
(Person vs. Access Control) y si el dispositivo figura online — necesario
para terminar el diagnóstico.

### Exportar fichajes para liquidación de sueldos

Módulo Control de Acceso → Búsqueda de Eventos ("Search"/"Event Search"), o
el módulo de Asistencia ("Time & Attendance") si está disponible:
- Filtrar por dispositivo (DS-K1T331W) + rango de fechas del período a liquidar.
- Exportar resultado a Excel (.xlsx) o CSV.
- Si existe el módulo de Asistencia, es preferible: calcula horas trabajadas,
  llegadas tarde y salidas anticipadas automáticamente en vez de dar solo el
  log crudo de entrada/salida (requiere configurar turnos/horarios por
  empleado primero).

Pendiente confirmar si esta instalación de IVMS tiene el módulo de
Asistencia separado o solo el log de eventos de Control de Acceso.

---

## Convención de este archivo

Agregar una entrada nueva (fecha + qué cambió) cada vez que se avance en
soporte técnico de campo (biométricos, alarmas GARNET, CCTV, IoT AVISTA en
instalación, etc.) que valga la pena recordar entre sesiones. No usar este
archivo para tareas de desarrollo del sitio web — esas van directo en los
commits y en el código.
