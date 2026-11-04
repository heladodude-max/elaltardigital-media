---
name: "titi-mari-short"
description: "Crear un Short vertical 9:16 de Titi Mari (El Altar Digital): guion, imagen, video con Gemini Omni en 3 clips con cortes de cámara, edit tight y dinámico, ambiente protagonista, música suave según el tema y subida programada a YouTube."
---

# Titi Mari Short: flujo completo

Skill para el canal cristiano de YouTube "El Altar Digital" (cuenta heladodude@gmail.com). Titi Mari es un personaje femenino carismático de Shorts cristianos motivacionales, tono gracioso, ligero y sorpresivo, pensados para viralizar y compartirse (público hispano en general; no centrar nada en un solo país). Roberto Muñoz aprueba todo.

**Estilo aprobado (29 oct 2026): todos los videos de Titi Mari se hacen así:** 3 clips de Gemini Omni con cámara distinta, edit tight sin silencios, cortes con zoom alterno, ambiente del lugar muy presente y música suave de fondo. Referencia: Shorts "spinning" y "lluvia en Miami" (v2).

## 0. Reglas de trabajo con Roberto (innegociables)
- Responde en español, conciso y directo. Sin saludos ni recaps.
- Nunca enviar, subir ni publicar nada sin que él haya leído el texto exacto. Siempre mostrar guion, prompt, audio y costo y esperar su OK antes de gastar créditos o llamar APIs de pago.
- Cada video sale con el guion aprobado (sin retocarlo), la voz aprobada y el personaje aprobado. Los créditos gastados en tomas equivocadas le cuestan dinero: antes de generar, revisar el prompt contra el guion.
- Se trabaja desde Claude desktop. Preguntar antes de descargar archivos (nombre, origen, tamaño). Nunca ingresar credenciales. La Mac no borra: mover a `_to_delete`.
- Si hay un Excel, todas las fórmulas deben funcionar.
- Decir siempre qué no se pudo verificar: Claude no puede oír audio, así que voz, labios y ritmo se confirman con Roberto.

## 1. El personaje
**Quién es:** la tía directa con chispa. Habla como una tía querida que te dice las cosas con cariño y sin rodeos, con humor, energía altísima y sonrisa en la voz. Cristiana, cálida, nunca sermoneadora. Muy expresiva con los ojos y con las manos y nunca está quieta (siempre hay movimiento: pedalea, gesticula, se acomoda).

**Apariencia (referencia aprobada 28 oct 2026):** lentes cuadrados multicolor con cordón, flequillo, collar de margarita. Usar siempre la foto close-up del rostro (headshot, solo la cara) como referencia: `~/Documents/gemini-tts/titi-mari-headshot.jpg` (si no existe, recortarla de la referencia). Cuerpo y ropa del vestuario elegido.

**Vestuario:** distinto en cada video. Elegir uno de los 16 looks de cuerpo completo de `~/Downloads/EL ALTAR DIGITAL/titi mari` según la situación (running, yoga, tenis, pádel, ciclismo, golf, aeropuerto, brunch, shopping, playa, cine, casa, reunión casual, fin de semana, viaje activo, día lluvioso), ropa deportiva de colores vivos al estilo nike.com; el de pádel, más colorido. Se adapta al clima del lugar (ej. Miami lluvioso: impermeable liviano naranja, short y tenis, no abrigo). Evitar prendas y fondos con texto o logos legibles (salió "SOULCYCLE" en un jersey y un neón "Aura Garden" en un fondo; pedir "sin texto ni logos legibles").

**Voz:** Gemini TTS, voz **Autonoe**, con un toque ronco ("nuestra voz de siempre"). Estilo aprobado para TTS: "Voz ronca y rasposa, grave y con textura áspera, como una tía carismática de voz curtida y cálida; muy emocionada y entusiasta, energía altísima, vibrante, sonrisa en la voz, ritmo ágil; pausas marcadas entre frases; enfatiza con fuerza la palabra NO; el 'los quiero' final alargado, cariñoso y alegre; español dominicano neutro". Escribir el guion con signos de exclamación. Para yoga y escenas íntimas se usó versión susurrada.

**Frases de marca:**
- Entrada: "¡Mis amores, siéntense, que su Titi Mari les tiene que decir algo!" (sin "Miren"; variante: "Mira, mi amor, siéntate, que tu Titi Mari te tiene que decir algo").
- Cierre: una frase "Y recuerda que…" (Dios nunca te va a olvidar; eres lo más lindo para Dios; te ama tal cual estás hoy; lo que parece tarde para Dios es a tiempo; no hay que ser perfecto para que Dios te abrace; Dios no te dejó en visto, siempre responde) seguida de "¡Los quierooo!" (plural, alargado, cariñoso).

## 2. Guion
- Duración del guion: 3 bloques de ~16-22 palabras, cada uno cabe en ~8 s hablados. Frases cortas y simples, ideas simples pero poderosas, nada complicado ni "business like".
- Estructura por bloques: Bloque 1 = pregunta gancho + apertura de marca; Bloque 2 = idea central; Bloque 3 = llamada a comentar + "Y recuerda que…" + "¡Los quierooo!". Forma corta de la llamada: "Si hoy necesitas [X], escribe Amén en los comentarios."
- Los guiones que Roberto pasa se usan exactamente como los pasa. Si los escribe Claude, mostrarlos y esperar aprobación.
- Vigilar repeticiones de una misma palabra ("fuerzas" 5 veces sonaba mal; máximo 2). Ofrecer el ajuste antes de generar.
- Reglas de viralidad: gancho en el primer segundo, ritmo que mantenga la atención, cierre con pago emocional.
- Para guiones que van a Gemini TTS se pueden usar las etiquetas vocales y de pausa de Gemini (<laugh>, <sigh>, <short pause>, etc.).
- Revisión: el guion pasa a audio/video solo si Claude y ChatGPT (consultar_chatgpt) coinciden en que está bien estructurado, no alucina y es interesante y relevante para cristianos.
- Situaciones: situaciones físicas absurdas o cotidianas donde Titi Mari aplique un mensaje (yoga en pose escorpión, spinning, lluvia en Miami, pádel, maleta, paraguas, apagón, plank, pose del árbol). Evitar que todo sea "cargar".

## 3. Imagen base (Nano Banana, MCP gemini-tts: edit_image)
- Referencias: headshot + imagen del look elegido. Salida 9:16, 2K, en `~/gemini-tts-mcp/images`. Mostrársela a Roberto antes de generar los clips.
- Describir la escena completa: lugar, clima, luces, otras personas desenfocadas, ropa adaptada al clima, manos al frente, estilo grabada con celular.

## 4. Video con Gemini Omni: 3 clips, una cámara distinta por clip
Usa `generate_video` del MCP gemini-tts. Limitaciones aprendidas:
- Cada clip dura 10 s. Extender/editar (`edit_video`) con clips de personas reales queda **bloqueado** (error 400 content_blocked aun con prompt mínimo). No intentarlo: generar clips separados.
- No acepta audio de referencia: la voz la inventa el modelo (no hay garantía de Autonoe).
- 9:16, 720p; los 3 clips se lanzan en paralelo (tardan unos minutos); seguir con `video_status`. Si una llamada devuelve ruta final inmediata, ya está lista.

Clips:
1. **Clip 1:** image_to_video desde la imagen base; plano medio frontal.
2. **Clip 2:** mode=reference (headshot + imagen); primer plano cerrado en leve contrapicado, cámara acercándose, detalles del clima (gotas, sudor, luz).
3. **Clip 3:** mode=reference; plano medio-abierto lateral 3/4 que orbita hacia el frente; cierre con sonrisa; el clima puede "abrirse" (ej. luz dorada tras la lluvia).

Plantilla de prompt: "Plano N de 3. Un solo plano continuo de 10 segundos, vertical, estilo grabado con teléfono, con ligero camera shake de cámara en mano constante. CÁMARA: [ángulo]. [Descripción de la mujer: lentes, ropa, escena, clima]. Ojos y manos muy expresivos, nunca quieta. Empieza a hablar a los 0.5 segundos, en español dominicano, voz grave y ronca, labios sincronizados palabra por palabra: \"[texto]\". Termina de hablar alrededor del segundo 8-8.5 y sostiene una sonrisa hasta el corte. SONIDO: solo voz y ambiente, SIN música de fondo: [ambiente detallado]. Sin texto en pantalla ni logos legibles."
- Ambiente SIEMPRE detallado y por debajo de la voz (spinning: volante, cadenas, respiración, gritos lejanos; lluvia en Miami: lluvia sobre el paraguas, truenos lejanos, autos sobre asfalto mojado, gotas en charcos, viento en palmeras; cancha de pádel: pelotas a lo lejos, brisa).
- Cada frase completa dentro de su clip, nada cruza un corte. Revisar fotogramas de cada clip.
- Costo: Omni se cobra por la API de Gemini; Roberto aprueba antes de generar.

## 4b. Alternativa Higgsfield (Seedance 2.5) cuando se necesita la voz exacta
MCP Higgsfield: modelo seedance_2_5, modo omni_reference, 4-30 s, 720p 9:16, ~7 créditos por segundo (un clip de 27 s costó 189). Permite audio de referencia (voz Autonoe) con generate_audio=true; hacer `get_cost` antes. Subida: media_upload, PUT con curl, media_confirm (audio mp3). Puede pronunciar mal el cierre ("los querio"): reemplazar solo esa frase con la TTS, estirada ~0.85 y con fadeout. Kling: omni_ref_video no hace lipsync con audio exacto y bloquea algunos guiones.

## 5. Edición (ffmpeg en el contenedor): tight y dinámica
Roberto rechazó el montaje con espacios en blanco (clips de 10 s completos con silencios). El estándar es:
1. **Detectar el habla de cada clip** por energía de voz (filtro pasa banda ~250-3200 Hz, ventanas de 50 ms, umbral ~28 sobre ~12 del ruido de fondo). Agrupar tramos, cerrando huecos menores a 0.4 s.
2. **Recortar**: empezar ~0.1-0.15 s antes de la primera sílaba, terminar ~0.15 s después de la última; cortar las pausas internas mayores a 0.4 s (jump cuts). En el último clip dejar ~0.5 s extra de sonrisa antes del final. Resultado típico: ~21 s en vez de 30.
3. **Zoom alterno en cada corte**: toma normal (1.0) y toma con zoom 1.10 (scale + crop centrado 720x1280) para que parezca edición intencional.
4. Audio de cada tramo con fades de 12 ms; concatenar.
5. **Ambiente protagonista**: cama continua construida con el propio ambiente de los clips (colas silenciosas de cada clip, concatenadas con crossfades de 0.3 s y llevadas a nivel audible) + capa sintética del lugar (lluvia: hiss filtrado 1.2-7 kHz con gotas aleatorias; truenos: ruido filtrado <140 Hz con envolvente, a ~5, ~14 y ~20 s; spinning: volante, cadenas, gritos lejanos). Nivel claramente audible, por debajo de la voz, sin cortarse en los saltos.
6. **Música**: elegir según el tema, SIEMPRE muy baja. Spinning/energía: techno sintético 128 BPM continuo (volumen ~1.4 con sidechaincompress ratio 1.6), con flashes rosado 0xff2d95 / azul 0x2d7bff al compás (ataque seco, exp(-13t), adelantados 30 ms, pico ~0.65, blend con all_expr, render lento en background). Emocional/consuelo (lluvia): piano suave con colchón ambiental (Lyria `lyria-3-clip-preview`, 30 s, instrumental), volumen ~0.16 (~0.26 en el último tercio), sidechaincompress ratio 3, fade in 0.5 s; el piano casi no debe notarse, solo en las pausas (Roberto pidió "mucho menos piano" cuando estaba a ~0.85).
7. **Igualar volumen** entre voces distintas (medir RMS/picos); fade out final de ~0.6 s; limitador 0.95.
8. **Subtítulos** (si Roberto los pide o en el estándar del canal): drawtext con textfile (DejaVuSans-Bold 48, blanco con borde negro 5), abajo (y≈1110 de 1280) para no tapar la cara, máx. ~19 caracteres por línea y 4 palabras por tarjeta; alinear con las pausas reales de la voz recortada. Verificar en fotogramas.
9. Camera shake extra solo si Roberto lo pide (±5 px con zoom 1.04; el fuerte se vio exagerado). Los clips de Omni ya traen shake.
10. Exportar: libx264 crf 18, yuv420p, aac 192k, faststart, 9:16 HD. Revisar con contact sheet de fotogramas antes de entregar.

## 6. Entrega para revisión
- SendUserFile y copiar a `~/Documents/gemini-tts/` con nombre versionado (v1, v2, …); no sobrescribir ni borrar versiones previas.
- Resumen corto: qué contiene, qué cambió y qué NO se pudo verificar (voz, labios, ritmo, balance de audio). Esperar feedback e iterar con cambios puntuales sin rehacer todo.

## 7. Publicación en YouTube
- Mostrar título y descripción exactos; cuando Roberto dice "ponlo en la programación" se sube privado y programado y se le muestra el texto usado (puede cambiarse con youtube_update_video antes de salir). Título: gancho + "| Titi Mari" + emoji + #Shorts. Descripción: 1-2 frases del mensaje, "Escribe 'Amén' en los comentarios 🙏", "¡Los quierooo!" y hashtags (#TitiMari #Fe #Shorts #PalabraDiaria #Dios). Tags: Titi Mari, fe, Dios, + tema, Shorts, palabra diaria.
- `youtube_upload_video`: privacy private + `publish_at` en hora de Santo Domingo (-04:00), **uno por día a las 12:00 pm** (revisar con youtube_list_videos cuál es el siguiente día libre), categoría 22, idioma es, no para niños. Miniatura: fotograma automático.
- Playlist "Titi Mari" en el canal (crearla en Studio si no existe; la API no la crea) y añadir cada video.
- **Reemplazar una versión ya programada: la API no puede quitar `publishAt`** (una vez se publicó una versión "[NO PUBLICAR]" a su hora). Mejor: NO subir una segunda versión con la primera ya programada; si pasa, pedirle a Roberto que quite la programación en Studio, o pasar la vieja a privado justo después de que salga. Borrar es permanente y lo decide Roberto.
- Los Shorts se pueden replicar como Reels en @elaltardigital (con aprobación).
- A las 48-72 h comparar rendimiento (vidIQ / youtube_list_videos) y aprender qué situaciones funcionan.

## 8. Estado de referencia
Shorts hechos: yoga (pose escorpión, susurrada), pádel, Miami "Da el primer paso", spinning (Omni con cortes, público 29 oct), lluvia en Miami "Cuando todo pinta mal, la fe te sostiene" (v2 tight, programado 30 oct 12:00). Pendiente de feedback: dembow cristiano de gratitud (Lyria).