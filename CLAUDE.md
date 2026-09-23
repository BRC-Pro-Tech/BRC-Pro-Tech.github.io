# Notas técnicas — BRC Pro Tech (electricista/service de electrodomésticos)

Este archivo guarda conocimiento técnico acumulado en sesiones de Claude Code, para que futuras sesiones sobre este repo tengan contexto sin repetir el diagnóstico desde cero. Se va ampliando caso a caso.

## Lavarropas LG carga frontal, serie Direct Drive con panel "perilla + Temp./Centrifugado" (ej. LG F1215TD, fabricado en Argentina)

Panel de referencia: perilla de programas + botones Acl. Caliente / Pre-Lavado / Intensivo / Antiarrugas a la izquierda, display de barra "Detectar-Lavado-Aclarado-Centrifugado", botones Play/Pausa, Centrifugado, Temp., Power.

### Entrar al modo técnico / autodiagnóstico
1. Lavarropas **apagado** (enchufado, sin tocar Power).
2. Mantener presionados simultáneamente **Temp. + Centrifugado**, y sin soltarlos presionar **Power**.
3. Mantener los tres ~3-5 s hasta que el display cambie (pantalla de identificación: en un caso se vio "1 - E/u alternando - 08", probablemente versión de software/región — no es un error).
4. Todos los LEDs de velocidad/temperatura/selector se encienden como parte de esta pantalla de entrada — es normal, no indica falla.
5. **Play/Pausa avanza paso a paso** la secuencia de test de actuadores. La perilla queda deshabilitada a propósito durante el modo test (no navega).
6. Salir: desenchufar, o mantener Power unos segundos.

### Secuencia típica de autodiagnóstico (orden observado en un caso real, puede variar por firmware)
| Paso (Play) | Qué hace la máquina | Test |
|---|---|---|
| 1 | Motor gira antihorario, cuenta ~49-50, se oye click/zumbido | Motor bajo giro + probable traba de puerta (solenoide) |
| 2 | Motor horario, RPM sube y oscila ~600-650 | Motor velocidad media + tacómetro |
| 3 | RPM sigue hasta ~1250-1260 | Centrifugado a velocidad máxima |
| 4 | Frena, carga agua | Electroválvula de agua **fría** |
| 5 | Activa válvula (sin manguera = sin agua pero se oye el solenoide) | Electroválvula de agua **caliente** |
| 6 | Motor gira de nuevo, ~50-51 | Otro paso de motor |
| 7 | Display "013", sin sonido | Resistencia calefactora (silenciosa, solo consume corriente) |
| 8 | Bomba de desagote enciende | Electrobomba de desagote |
| 9 | Se apaga | Fin de secuencia |

Este test es muy útil para validar de una sola pasada que motor (ambos sentidos/velocidades), ambas electroválvulas, resistencia y bomba responden bien — descarta fallas de potencia/actuadores rápidamente.

### Caso resuelto: "no enciende el panel" / display trabado con guiones
**Síntoma:** al encender (sin combo, uso normal), display muestra guion central en los dígitos de 7 segmentos, **todos los LEDs del anillo del encoder (selector de programas) encendidos**, ícono Play/Pausa intermitente, **la perilla no responde**, solo responde el botón Play.

**Diagnóstico diferencial:**
- Si el equipo estuvo con corte de luz a mitad de ciclo: descartar primero "ciclo memorizado" (la placa intenta resumir el último ciclo guardado). Se descarta si el síntoma persiste después de desenchufar varios minutos (para descargar la memoria volátil).
- Con panel desmontado/fuera del marco: revisar que el conector/cinta plana entre el panel de control y la placa principal esté bien asentado (fácil que quede en falso si el panel cuelga fuera del gabinete).
- **Causa real confirmada en un caso**: contacto sucio/oxidado o gastado en los **microswitches del encoder (perilla selectora)**. La placa se queda esperando una lectura válida de posición y no la recibe → se traba con todos los LEDs encendidos. Al **girar la perilla manualmente para un lado y otro** (sin ningún botón), en algún punto el contacto "engancha", pasa a un solo LED encendido y responde normal desde ahí. Coincide con reportes de foros de reparación: ~90% de los casos de "no responde el panel/Play" en estos LG son el selector.

**Solución:**
1. Limpieza de contactos del encoder con limpiacontactos/spray dieléctrico, girando varias veces para arrastrar suciedad/óxido.
2. Si sigue siendo intermitente después de limpiar (necesita "menearse" para enganchar), el switch está gastado mecánicamente → reemplazar la placa del panel frontal completa (en LG el encoder va soldado a esa placa, no se vende suelto).
3. Verificar con varios ciclos de apagado/encendido reales (no solo modo test) que arranca solo, sin necesitar mover la perilla.

**Antecedente relevante a seguir de cerca:** en el caso resuelto, el equipo había estado ~1.5 años parado en un garage. El dueño anterior (con otro técnico) reportaba que "desconectando la bomba de desagote" el panel respondía — hipótesis de fuga de corriente en el bobinado de la bomba (plausible por humedad prolongada). El test de autodiagnóstico confirmó que la bomba enciende/apaga limpio y no disparó nada raro, pero **queda pendiente medir aislación bobinado-carcasa de la bomba con multímetro/megóhmetro** como chequeo preventivo antes de dar el equipo 100% sano — es un mecanismo de falla distinto e independiente del encoder, y ambos son plausibles en un equipo con ese historial de humedad/inactividad.

## Lavarropas Longvie carga superior con agitador (familia L2616/L2617/L4613/L4616/L4815/L5616, ~1999-2005)

No hay manual de service oficial digitalizado accesible para esta generación (dominios con documentación bloqueados por proxy de red en este entorno: dmelectronic, yoreparo, manualslib, lg.com, etc. — probar acceso directo en otro entorno/navegador si se necesita).

Repuesto "fuelle con pico" (bellows con boca para detergente) confirmado como pieza común/compatible entre L4613, L4616, L4815, L5616 — mismo diseño de gabinete que la familia L2616/L2617. Sella el borde superior de la cuba contra la consola, con un pico por donde entra el agua/detergente del dispensador.

**Procedimiento genérico para acceder al fuelle (no verificado contra manual oficial, confirmar en cada equipo antes de forzar):**
1. Desenchufar, cerrar llave de agua, desconectar mangueras de entrada.
2. Sacar la bandeja dosificadora de jabón/suavizante (tirar hacia arriba o liberar seguro lateral).
3. Buscar tornillos ocultos en el hueco donde estaba la bandeja del dispensador.
4. Revisar también el borde trasero superior del gabinete (por detrás, debajo del borde de la tapa/consola) — suele haber 1-2 tornillos ahí.
5. La consola superior generalmente se libera deslizándola hacia atrás y levantándola (o basculando sobre clips/lengüetas traseras) — no tirar derecho hacia arriba de entrada, puede haber clips plásticos no visibles.
6. Con la consola retirada, el aro superior de la cuba tiene el fuelle viejo sujeto con abrazadera (alambre tipo resorte o banda metálica). Soltar, limpiar asiento, montar fuelle nuevo alineando el pico con la salida del dispensador, poner abrazadera nueva.
7. Rearmar en orden inverso.

## Método general: olor a quemado / carbonilla en placa de control de electrodoméstico

1. **No reenergizar** la placa hasta identificar el componente dañado — si hay un semiconductor en corto en la etapa de potencia, reconectar puede repetir/agravar el daño o generar riesgo de fuego.
2. La causa más común de olor a quemado en placas de electrodomésticos es la **etapa de fuente conmutada (SMPS)** que convierte tensión de red a la baja tensión de lógica (5V/3.3V) — maneja tensión de red rectificada (~300V DC en 220V AR) y corrientes de conmutación altas. Buscar ahí primero: IC controlador/switcher, diodos rectificadores SMD, MOSFET de conmutación, electrolíticos cercanos.
3. Con la placa desenchufada, inspeccionar con buena luz/lupa cada componente de esa zona: cuerpo agrietado/hinchado/con punto negro, marcado ilegible por calor, soldadura ennegrecida en vez de gris/plateada.
4. Oler de cerca cada componente (equipo frío y desenchufado) para aislar cuál es el origen real vs. hollín depositado alrededor por otro componente.
5. Antes de dar por buena una reparación, medir con multímetro los semiconductores sospechosos (diodos en corto, MOSFET gate-source) antes de volver a energizar.
