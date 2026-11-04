---
name: "the-untold-story"
description: "Guía completa del canal de YouTube The Untold Story (vida oculta de civilizaciones antiguas, inglés, sin rostro): guion, voz, imágenes, miniaturas, branding, Shorts y checklist de subida."
---

# The Untold Story — guía de producción

Canal: @TheUntoldStory_channel (nombre exacto "The Untold Story"; id UCOHa-XY-r0LWkxj_c8KCVgg). Dueño: Roberto Muñoz Benedicto. Canal sin rostro, en inglés, narrado en segunda persona.

Legado descartado: la línea anterior (ensayos documentales sobre CEOs e íconos, narradora femenina, estilo risograph, 7 min, Ep01 MrBeast, Ep02 Bryan Johnson) ya no se usa. Se conserva solo su disciplina de escritura (abajo).

## Línea editorial
- Tema: la vida diaria oculta de civilizaciones antiguas (qué hacía la gente común de noche, en casa, en la calle). Roma primero; luego Egipto, Grecia, Japón Edo, etc.
- Segunda persona y presente, sensorial ("You are lying on a thin straw mattress, six floors above the street."). Un personaje recurrente por video puede aparecer en tercera persona (Marcus).
- Video largo (~25 min): gancho de ~30 s con promesa ("before this video ends I will tell you the one thing a Roman feared more than..."), bloques de 1–3 min con una escena concreta cada uno, fuentes antiguas citadas (Juvenal, Séneca, Plinio, Tácito), micro-giros cada ~2 min, cierre que cumple la promesa del gancho y deja una pregunta.
- Una sola idea-espina por video; todo lo demás la hace aterrizar. Nunca pedir al generador que "cubra" temas: pedirle que construya hacia una idea.
- Rigor: no inventar datos; si una cifra es incierta, decirlo. Incendio de Roma 64 d.C.: 6 días + 3 días, 3 de 14 distritos arrasados, 7 dañados, 4 intactos; empezó cerca del Circo Máximo.

## Escritura
- Voz propia y opinión, ritmo variado (frases de 3–5 palabras junto a otras de 20–30; nunca tres largas ni tres cortas seguidas). Pivote del canal: "And yet." en línea propia.
- Prohibido: delve, crucial, transformative, moreover, furthermore, additionally, in conclusion, let's face it, "the truth is", "shocking", "insane", "unbelievable", "smash that like button", "hit subscribe", lenguaje de balance "some say X, others Y".
- Pausas TTS con "..."; etiquetas [halting] máx. 3 y [drawn out] máx. 2 por guion; sin etiquetas de volumen.
- Cierre: pregunta personal, específica y cómoda de responder en comentarios. El narrador termina ~30 s antes del fade final.
- Descripciones sin spoilers: instalan la pregunta, el video la responde.

## Voz
- Gemini TTS, voz Achird, estilo: narrador documental calmado, grave, íntimo. Pilotos guardados como wavs por bloque (p1_00_gancho ... p1_08_amanecer_cierre_v3) en Documents/gemini-tts.
- Transcribir con faster-whisper (base.en, int8) para tiempos por palabra. Whisper falla con nombres propios (Juvenal sale "juvenile"): corregir en subtítulos.

## Estilo visual
- Caricatura editorial plana: contornos negros gruesos, colores saturados, noches índigo/púrpura, luz cálida naranja, personajes expresivos simplificados.
- Generación: Nano Banana (gemini-tts MCP generate_image), 2K. 16:9 para largos; 9:16 para Shorts (1536x2752). Se pueden lanzar varias en paralelo. El texto en imagen sale bien si se deletrea.
- Regla del proyecto ALTAR DIGITAL: todo HD y 16:9, excepto Shorts (9:16 por plataforma): avisar a Roberto de la desviación.
- QA de época OBLIGATORIO antes de usar una imagen (Roma): sin asfalto, chimeneas, vidrio, postigos modernos, luz eléctrica, relojes de arena, cúpulas, torres ni objetos modernos; sin Coliseo en el 64 d.C. (usar Circo Máximo, pista larga abierta en U); sin soldados, lanzas ni armaduras salvo que el guion los pida; revisar bordes blancos. Regenerar si falla.
- Ensamblaje: ffmpeg zoompan (Ken Burns), 24 fps, libx264, AAC 192k, marca "THE UNTOLD STORY" pequeña arriba a la derecha en el largo. Audio -14 LUFS / -1.5 dBTP. Subtítulos del largo en SRT aparte; los Shorts llevan subtítulos quemados.

## Librería de imágenes: reutilizar antes de generar (REGLA OBLIGATORIA)
Generar cuesta dinero. Antes de pedir cualquier imagen nueva (escena de largo, escena de Short, fondo de miniatura), buscar en lo ya generado y reutilizar la que funcione.
- Dónde está: /Users/rmunozb/gemini-tts-mcp/images/ (p1*, p2*, p1sh*, p2sh*, miniaturas) y las carpetas de cada piloto en Documents/gemini-tts/ (piloto1/, piloto2/). Pedir acceso con device_request_folder_access si hace falta.
- Cómo buscar: listar la carpeta, filtrar por nombre y por la frase de la escena; armar una hoja de contacto con PIL (etiquetas con el nombre) y MIRARLA. Nunca elegir solo por el nombre. Mantener un catálogo images-catalogo.tsv (archivo, tema, época, personaje, formato 16:9 o 9:16, video donde se usó) y ponerle al día cada imagen nueva.
- Cuándo sirve: mismo tema o momento (calle de noche, insula, letrinas, horno, banquete), época correcta, estilo idéntico, formato correcto, sin texto o marcas que choquen, personaje coherente (Marcus). Pasa el QA de época igual que una nueva. Una imagen 16:9 se puede recortar a 9:16 si el sujeto queda centrado; si no, no sirve para Short.
- Cuándo no: si encaja solo a medias (otra hora, otra acción, otro personaje), no se fuerza; se genera.
- Límites: dentro de un mismo video una imagen no se repite más de dos veces ni seguida. Los Shorts sí pueden reutilizar imágenes de su video largo. Entre videos distintos, reutilizar únicamente si el espectador no lo nota (escena genérica, no una escena firma).
- Solo si nada sirve se genera, y la nueva se guarda con nombre descriptivo (p<n>_tema_n.jpg) y se agrega al catálogo.
- En el resumen al terminar, decir cuántas imágenes se reutilizaron y cuántas se generaron.

## Branding (publicado)
- Logo tus_logo_final_800.png y banner tus_banner_final_2560x1440.jpg, ambos con el texto "THE UNTOLD STORY", en /Users/rmunozb/gemini-tts-mcp/images/.
- Miniaturas 1920x1080 (1280x720 al subir si pesa más de 2 MB), texto grande en inglés (ej. "ROME AFTER DARK", "WHAT THEY GUARDED"), alto contraste, una escena clara, sin caras reales. Generar 3 variantes (A/B/C) de tipos distintos; el arte sale sin texto y el texto se compone aparte con PIL (Poppins Bold, contorno negro grueso, última línea en dorado). Piloto 1 usa la A.
- REGLA OBLIGATORIA: toda miniatura de este canal se revisa con el skill youtube-thumbnail-master (anthropic-skills:youtube-thumbnail-master) antes de mostrarla a Roberto y antes de subirla: elegir 2 o 3 tipos distintos, correr scripts/thumb_check.py (simulación móvil a 168 px, squint, escala de grises, zona de duración abajo a la derecha) y puntuar con su rúbrica (meta 80 o más sobre 100). Si baja de 80, corregir primero. Aplica a A/B/C, a rehacer miniaturas y a miniaturas de Shorts si las hay. El fondo de la miniatura también sale primero de la librería si algo sirve.

## Piloto 1
"What Ancient Romans Did After Dark" (25:18, 1080p), público: https://youtu.be/mStTOVMQjQE. Carpeta: Documents/gemini-tts/piloto1/. Inglés, divulgación de IA = Sí, no para niños, tags puestos.

## Shorts (playbook, aplicado en piloto1/shorts/)
- 1080x1920, 25–45 s, un momento fuerte por Short, cortado del audio del largo en límites de frase.
- Gancho de texto enorme en 0–2,8 s (3–6 palabras, dorado con contorno negro); la voz arranca en el segundo 0, sin intro ni logo.
- Subtítulos quemados palabra a palabra (Poppins Bold ~96 px, 3 palabras por bloque, palabra activa en dorado) en el tercio medio-bajo, lejos de la interfaz de Shorts; nunca dos bloques solapados.
- Cortes de imagen cada ~4–5 s con zoom ≥1.10 alternando in/out (oculta bordes). Sin música obligatoria.
- Final: imagen oscurecida + tarjeta "FULL STORY ON THE CHANNEL / título del largo" + CTA hablado en Achird ("The full story is on the channel. Link in the description."). Terminar en frase que deje promesa o pregunta.
- Descripción: línea gancho, link al largo, 3–5 hashtags (#AncientRome #History #Shorts). Comentario fijado con el link. Título corto con palabra clave y curiosidad.
- Ritmo: ~3 por semana, escalonados. Medir retención a 3 s y % visto; replicar los que pasen del 85 %.
- Cortes del Piloto 1: S1 ventanas/Juvenal (p1_03 24.60–45.90), S2 gancho (p1_00 0–28.06 + 51.44–61.05), S3 antorchas (p1_01 52.48–73.80 + 75.30–86.25), S4 incendio (p1_03b 41.80–62.40 + 69.10–76.15), S5 Marcus (p1_04 74.30–109.65). Script de armado: ~/work/shbuild.py (audio/segs/ass/final).

## Checklist de subida
1. Subir en el canal correcto ("The Untold Story"), no en el personal: verificar avatar antes.
2. Título, descripción, tags, miniatura (ya revisada con youtube-thumbnail-master), idioma del video = English (se resetea tras publicar: verificar), divulgación de IA = Yes, no para niños.
3. Claude in Chrome no lee videos grandes (límite 10 MB y permisos): Roberto arrastra el archivo; las miniaturas sí suben con file_upload. El MCP de YouTube pide reautorizar si da invalid_grant.
4. Nunca publicar en público sin que Roberto lo diga explícitamente en el chat.

## Preferencias de trabajo con Roberto
Español, conciso. Subir al chat todo entregable (videos, imágenes, miniaturas, archivos) con SendUserFile, siempre, sin que lo pida. Una pregunta a la vez. No enviar mensajes en su nombre sin que lea el texto exacto.