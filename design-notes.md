# El Poseído — Design notes v2

Iteración de reglas propuesta tras playtest inicial (post-presentación 2026-06-04). Aún no implementado en la app.

## Objetivos del rediseño

1. Hacer al poseído menos difícil de jugar (sintió presión alta).
2. Mantener vivos a los enfermos terminales salvados (se aburrían).
3. Subir tensión general al sacerdote (más razones para dudar).

## Mecánicas propuestas

### Escasez de cartas — a testear
- N cartas por jugador no-sacerdote (donde N = cantidad de no-sacerdotes), repartidas una sola vez al inicio.
- Cartas usadas se descartan, no vuelven al mazo.
- **Efecto previsto**: cada ronda hay menos opciones, las cartas resuenan menos con la palabra real → el sacerdote tiene más razones para dudar.
- **Posible contra-efecto**: el poseído sale perjudicado también (es quien más juega), porque queda con cartas malas en la última ronda.
- **Plan**: testear ambas versiones (con y sin escasez) para medir el impacto neto en el poseído.

### Persignarse ×2 (poseído)
- Pasa de 1 uso por partida a 2.
- Mismo flujo discreto, misma habilidad. Solo más oportunidades de tomar la palabra real.
- Balance: contrarresta el endurecimiento general del juego sin cambiar la mecánica core.

### Tentación (poseído, NUEVA)
- Aprieta un botón en su reveal → un **enfermo aleatorio activo** ve la palabra-vecina en su próxima ronda (en lugar de la real).
- **Restricción**: no se puede usar cuando solo queda 1 enfermo activo (sería victoria automática).
- **UX**: el poseído tiene Comulgar + Persignarse + Tentar en su reveal. Sigue siendo 1 toque, pero la pantalla tiene 3 botones visibles. Trade-off aceptado.
- **Sin confirmación**: la app no le muestra al poseído a quién tentó. Se entera la próxima ronda al ver quién juega mal.
- **Frecuencia**: 1 vez por partida (puede subirse después si parece poco poderosa).

### Demente — opt-in (nuevo rol oculto)
- Checkbox en setup: "Jugar con demente". Solo visible en partidas de **6+ jugadores**.
- Cuando se activa: 1 enfermo aleatorio recibe la palabra-vecina (la misma que el poseído) cada ronda, sin saber que está "demente".
- Cuenta como enfermo a efectos de victoria y puntaje.
- **Efecto**: el sacerdote tiene un segundo "sospechoso natural", da cobertura al poseído sin que este haga nada.
- Compatible con Persignarse y Tentación (no interfieren entre sí).

### Apuesta de los salvados (NUEVA)
- Justo después de ser salvado (después de la vela), la app le pide al jugador elegir, en privado, a quién cree que es el poseído.
- Su elección queda guardada y oculta hasta el fin de partida.
- **Puntuación**: +3 puntos extra si acierta. Independiente de si gana sacerdote o poseído.
- **Revelación**: la tabla de puntajes al final muestra ✓ o ✕ junto a cada salvado con su apuesta.
- **Demente y apuesta**: el demente, si lo salvan, también apuesta (no sabe que es demente).

### Cartas de confesión (sacerdote, NUEVA)
- El sacerdote arranca con 2 cartas de confesión por partida (versión sobria) o 1 por ronda (versión generosa).
- Durante la discusión, antes de la cuenta regresiva, puede gastar una para hacer una **pregunta de sí/no en voz alta** a un jugador.
- El interrogado responde en voz alta también (preferencia: público).
- **Diseño abierto**: ¿4 por partida (1 por ronda en 4-enfermos)? ¿2 fijas? ¿8 (2 × rondas)? A definir con testeo.

## Vista de categoría — sin decidir
- Idea: mostrar a todos (o solo al poseído) la categoría de la palabra real (e.g., "Naturaleza", "Cuerpo").
- Pro: pista útil para el poseído sin spoilear la palabra.
- Contra: pierde misterio para todos.
- En pausa hasta nuevo orden.

## Plan de playtest (4 versiones incrementales)

1. **Versión A** (mínima): Persignarse ×2 + apuesta de salvados + cartas de confesión (2 fijas por partida).
2. **Versión B**: A + escasez de cartas.
3. **Versión C**: B + Tentación ×1.
4. **Versión D**: C + Demente (solo en partidas 6+).

Jugar 3-4 partidas por versión, registrar:
- Cuántas veces gana el poseído.
- Sensación subjetiva del poseído (presión / placer).
- Cuán comprometidos siguen los salvados.
- Cuán determinante fue cada habilidad.

## Roadmap técnico

- **Corto plazo**: implementar versión A en la app HTML actual (cambios chicos).
- **Mediano plazo**: testear y ajustar.
- **Largo plazo**: migrar a Next.js + TypeScript en Vercel. Decidir si la app sigue siendo "pasar el celu" o pasa a multijugador online (decisión arquitectónica importante; afecta backend, websockets, auth).
