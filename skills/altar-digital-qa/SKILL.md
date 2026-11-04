---
name: "altar-digital-qa"
description: "Revisor de calidad en paralelo para El Altar Digital: guion con aprobación obligatoria de Claude y ChatGPT (instrucciones incluidas), más audio, imágenes, miniatura y metadata."
---

# QA de El Altar Digital

Corre en paralelo al agente que usa el skill `altar-digital-video-html-qa`. No produce nada: revisa, puntúa y devuelve veredicto. Español, respuestas cortas, sin saludos. No corrige solo: señala qué falla y cómo arreglarlo; el agente de producción corrige.

## Enganche (por carpeta del día)
Trabaja sobre `EL ALTAR DIGITAL/<día>/`. Lee lo que el agente de producción deja ahí y escribe sus resultados en `qa/`:
- `qa/informe-guion.json`, `qa/informe-audio.json`, `qa/informe-imagenes.json`, `qa/informe-miniatura.json`, `qa/informe-metadata.json`
- cada informe trae: `veredicto` (APROBADO, REVISAR o BLOQUEADO), `puntaje` por criterio, `hallazgos` (con escena, segundo o frase exacta) y `arreglo` sugerido.
- `qa/resumen.md`: una línea por etapa, para que Roberto vea el estado de un vistazo.
El agente de producción avisa al terminar cada etapa (dejando el archivo) o llama al revisor con el nombre de la etapa.

## Qué bloquea y qué no
- Guion: BLOQUEA. No se genera audio hasta que Claude y ChatGPT aprueben los dos.
- Audio: corre mientras se planean escenas e imágenes. BLOQUEA el paso de armar el HTML (cambia los tiempos).
- Imágenes: corre mientras se hacen subtítulos. Solo bloquea el render del MP4; se regeneran solo las escenas marcadas.
- Miniatura y metadata: BLOQUEAN la subida a YouTube.
Si Roberto dijo "hazlo solo", el revisor funciona igual: los bloqueos son del proceso. Solo se escala a Roberto en los casos de la sección final.

## 1. Guion: aprobación doble (Claude y ChatGPT)

### Las cinco pruebas
Cada revisor responde APRUEBA o NO APRUEBA en cada una, con puntaje de 1 a 10 y una frase de evidencia.
1. Estructura. Arco claro: gancho en las dos primeras frases (sin saludo ni preámbulo), situación humana, texto bíblico, giro, aplicación, invitación a escribir Amén. Una idea central, no tres. Se entiende al oído, ritmo variado, sin relleno.
2. Cumple su objetivo. El brief del día (o, si no existe, el objetivo que el propio guion se plantea) dice qué debe entender, sentir o hacer el oyente. El revisor lo enuncia en una frase antes de puntuar y comprueba que el guion lo logra. Duración: unas 800 a 950 palabras para unos 6 minutos; avisar si se aleja más de 15 %.
3. No alucina. Se extrae una lista de todas las afirmaciones verificables del guion (citas bíblicas, contexto histórico o cultural, costumbres de la época, atribuciones a santos, Padres de la Iglesia o autores, significados de palabras griegas o hebreas, hechos sobre el pasaje). Cada una se marca con su respaldo: texto bíblico del día, fuente consultada en la web, o conocimiento ampliamente establecido. Las citas bíblicas deben ser literales, completas y con la referencia correcta. Toda afirmación sin respaldo se elimina o se reescribe como algo que el texto sí dice. Una sola afirmación inventada = NO APRUEBA.
4. Interesante. Hay tensión o pregunta que sostiene la atención, una escena concreta en vez de abstracciones, un giro que sorprenda sin traicionar el texto. Responder también: ¿seguiría escuchando un creyente que no sabe nada del pasaje a los 30 segundos?
5. Relevante para cristianos. Conecta el pasaje con la vida real de quien cree, es fiel al texto y a la enseñanza cristiana de la tradición del canal, sirve a creyentes de cualquier país hispano y no suena a sermón genérico ni a opinión personal presentada como doctrina.

### Reglas duras (no se negocian; cualquier fallo = BLOQUEADO sin puntaje)
Ninguna cifra ni dato medible, ninguna mención a QR, "código" o "pantalla", ninguna promesa de algo que el video no trae (enlaces, descargas), erratas, caracteres rotos, nada centrado en un solo país, español que no sea neutro.

### Protocolo de consenso
1. Claude revisa el guion con las cinco pruebas y las reglas duras. Antes de ver nada de ChatGPT, deja su veredicto escrito en `qa/informe-guion.json`.
2. ChatGPT revisa de forma independiente con `consultar_chatgpt`. El mensaje es el bloque de "Instrucciones para ChatGPT" (más abajo, copiado tal cual) seguido del BRIEF y el GUION completos. No se le envía el veredicto de Claude en esta primera ronda, para que no se contagie. Cada llamada a `consultar_chatgpt` es una conversación nueva: las instrucciones se incluyen siempre completas.
3. Se comparan. Hay aprobación solo si los dos dicen APRUEBA en las cinco pruebas, con media de 7.5 o más cada uno y ninguna prueba bajo 6.
4. Si hay desacuerdo en alguna prueba, se abre una ronda de debate: cada parte envía a la otra su objeción con la frase exacta y el motivo (a ChatGPT, con las instrucciones completas de nuevo, el guion, y la objeción de Claude y su respuesta anterior). Claude no cede por cortesía: mantiene la objeción si tiene evidencia y la retira si el argumento la desmonta. El objetivo es converger sobre un cambio concreto al guion.
5. El agente de producción aplica los cambios acordados y el guion se reevalúa completo por los dos. Máximo dos rondas de debate y corrección.
6. Si tras dos rondas siguen sin coincidir en las cinco pruebas, se escala a Roberto con el guion, las dos posturas lado a lado y una recomendación en una línea. En alucinación no hay desempate: basta que uno de los dos no pueda respaldar una afirmación para que se elimine o reescriba.
7. El informe final registra: veredicto de cada revisor por prueba, afirmaciones verificadas con su fuente, cambios aplicados y número de rondas. APROBADO solo si ambos aprueban.

### Instrucciones para ChatGPT (copiar tal cual en cada llamada)
```
Eres el revisor editorial de guiones de El Altar Digital, un canal de YouTube que explica el Evangelio del día a cristianos hispanohablantes de todo el mundo, en español neutro, en videos de unos 6 minutos narrados. Revisas un guion antes de que se grabe. Eres exigente e independiente: tu trabajo es encontrar fallas, no elogiar. No suavices ni cedas para ser amable.

Recibirás un BRIEF (objetivo del día) y un GUION. Si no hay brief, deduce el objetivo del propio guion y escríbelo.

Evaluación. Para cada una de las cinco pruebas responde APRUEBA o NO APRUEBA, un puntaje de 1 a 10, la frase exacta del guion que lo justifica y el cambio concreto que propones (con texto de reemplazo cuando sea posible).

1. ESTRUCTURA. ¿Las dos primeras frases enganchan sin saludo ni preámbulo? ¿Hay arco claro: situación humana, texto bíblico, giro, aplicación, invitación a escribir Amén en los comentarios? ¿Hay una sola idea central? ¿Se entiende al oído, con ritmo variado y sin relleno?
2. CUMPLE SU OBJETIVO. Escribe en una frase el objetivo (qué debe entender, sentir o hacer el oyente) y decide si el guion lo logra. El guion debe tener unas 800 a 950 palabras; si se aleja más de 15 %, dilo.
3. NO ALUCINA. Haz una lista numerada de TODAS las afirmaciones verificables del guion: citas bíblicas (deben ser literales, completas y con la referencia correcta), contexto histórico o cultural, costumbres de la época, atribuciones a santos, Padres de la Iglesia o autores, significados de palabras griegas o hebreas, hechos sobre el pasaje. Para cada una indica: RESPALDADA (di en qué: pasaje bíblico exacto, o fuente concreta que existe), DUDOSA o NO PUEDO RESPALDARLA. Nunca inventes una fuente, un nombre, un año ni una cita para sonar seguro: si no estás seguro, escribe NO PUEDO RESPALDARLA. Una sola afirmación inventada o no respaldable = NO APRUEBA.
4. INTERESANTE. ¿Hay tensión o pregunta que sostenga la atención, escenas concretas en vez de abstracciones, un giro que sorprenda sin traicionar el texto? Responde además: ¿seguiría escuchando a los 30 segundos un creyente que no sabe nada del pasaje? Sí o no, y por qué.
5. RELEVANTE PARA CRISTIANOS. ¿Conecta el pasaje con la vida real de quien cree? ¿Es fiel al texto bíblico y a la enseñanza cristiana? ¿Sirve a creyentes de cualquier país hispano? ¿Evita sonar a sermón genérico o a opinión personal presentada como doctrina?

REGLAS DURAS. Revisa una por una y responde CUMPLE o FALLA con la frase afectada: (a) ninguna cifra, porcentaje, estadística, monto ni dato medible (se permiten números propios del texto sagrado dichos con naturalidad); (b) ninguna mención a QR, "código" ni "pantalla"; (c) ninguna promesa de enlaces o descargas; (d) sin erratas; (e) nada centrado en un solo país y español neutro, sin giros locales.

FORMATO DE RESPUESTA (siempre este, sin saludos ni preámbulos):
OBJETIVO: <una frase>
PRUEBA 1 ESTRUCTURA: APRUEBA|NO APRUEBA | <n>/10 | <frase exacta> | <cambio>
PRUEBA 2 OBJETIVO: ...
PRUEBA 3 NO ALUCINA: ... y debajo la lista numerada de afirmaciones con su estado
PRUEBA 4 INTERESANTE: ...
PRUEBA 5 RELEVANTE: ...
REGLAS DURAS: a) CUMPLE|FALLA ... e) CUMPLE|FALLA ...
VEREDICTO FINAL: APRUEBA solo si las cinco pruebas aprueban y ninguna regla dura falla; si no, NO APRUEBA, con los tres cambios más importantes.

Si en un mensaje posterior recibes la objeción de otro revisor, responde para cada punto MANTENGO o RETIRO, con la razón. Solo retira una objeción si el argumento te convence, no por cortesía. Si tu objeción es sobre una afirmación que no puedes respaldar, la objeción se mantiene hasta que se muestre el pasaje o la fuente exacta.
```

## 2. Audio
Sobre el WAV y el guion limpio (`narr.txt`):
- Duración con ffprobe frente a lo esperado por palabras; desvío grande = pausas o saltos.
- `silencedetect` (-38dB): marcar silencios de más de 2.5 s en medio de la narración y silencios iniciales o finales excesivos.
- `volumedetect` y picos: marcar recortes (pico en 0 dB) o volumen muy bajo; el nivel medio debe ser parejo de principio a fin (comparar RMS por tramos; saltos bruscos = revisar).
- Transcribir con sherpa-onnx whisper base (modelo de GitHub, no Hugging Face) y comparar con `narr.txt` por difflib sobre texto normalizado. Marcar tramos de 4 o más palabras seguidas del guion que no aparecen en el audio, palabras repetidas, o texto añadido. Esos tramos se oyen antes de dar por malo el audio: Whisper base se equivoca con nombres bíblicos.
- Revisar a mano la pronunciación de nombres propios y referencias bíblicas.
- Veredicto: REVISAR con la lista de segundos exactos; para regenerar, sugerir solo el párrafo afectado.

## 3. Imágenes
Generar un contact sheet (ffmpeg tile) y mirar escena por escena con la lista de escenas (tipo, mood, frase ancla):
- Relevancia: la imagen ilustra lo que dice el narrador en esa frase, no un tema parecido.
- Registro: B es pintura al óleo pulido, A es foto documental; Q es Biblia abierta con texto desenfocado. Nunca mezclados.
- Mood de las A: la luz y el color coinciden con el mood declarado.
- Prohibidos: texto legible, letreros, cruces, logos o marcas, banderas o matrículas, interfaces legibles en pantallas, personas reales identificables.
- Escenas A: personajes hispanohablantes de edades y países variados, sin delatar un solo país.
- Variedad: no más de dos encuadres casi iguales seguidos; el ritmo visual cambia cada 5 a 8 s.
- Calidad: manos, caras y objetos sin deformaciones, 16:9, resolución correcta.
- Devolver la lista de escenas a regenerar con un prompt corregido para cada una.

## 4. Miniatura
REGLA OBLIGATORIA: toda miniatura se revisa con el skill youtube-thumbnail-master (anthropic-skills:youtube-thumbnail-master). Hay que correr su `scripts/thumb_check.py` sobre la miniatura (simulación móvil a 168 px, squint, escala de grises, zona de duración) y puntuarla con su rúbrica de 100 puntos (`references/qa-and-testing.md`). Menos de 80 = REVISAR con el arreglo concreto. No se da APROBADO sin esa revisión, y el informe `qa/informe-miniatura.json` anota el puntaje obtenido y las banderas de thumb_check.
Además, los criterios propios del canal:
- 1280x720, JPG, menos de 2 MB.
- Gancho de 2 a 4 palabras, sin cifras ni dígitos, que genere curiosidad y el video cumpla; acentos, ñ y ¿ correctos.
- Marca "LA PALABRA DIARIA" visible, que se lee en versión de 168x94, fuera de la esquina inferior derecha y sin tapar el sujeto.
- Sujeto claro, contraste suficiente, se entiende en un celular.
- La imagen es relevante al tema del video y al gancho.
- Si el video ya es público, puntuar además con vidIQ (`score_thumbnail` con videoId). En privados no funciona.

## 5. Metadata de YouTube (antes de subir)
- Título de unos 70 caracteres como máximo, empieza con "Evangelio de hoy", lleva fecha y pasaje, sin cifras estadísticas, sin clickbait que el video no cumpla.
- Descripción: dos primeras líneas fuertes, bloque "En este video:", línea fija de La Palabra Diaria, invitación a escribir Amén, 3 a 5 hashtags, sin QR ni estadísticas.
- Tags: unos 15, de general a específico.
- `publish_at` a las 05:00 de Santo Domingo del día correcto (-04:00), privacidad private, lista "LA PALABRA DIARIA" planificada, sin duplicado del día en `youtube_list_videos`.

## Escalamiento a Roberto
Solo cuando: el guion no logra consenso tras dos rondas, o un fallo no tiene arreglo automático. El mensaje es corto: qué falló, evidencia, dos opciones.

## Trampas
- No dar por bueno lo que no se vio o no se escuchó: toda conclusión sobre imágenes sale de mirarlas, no de leer el prompt.
- ChatGPT también alucina: sus respaldos de afirmaciones históricas se contrastan con una búsqueda web antes de aceptarlos.
- Un falso positivo de Whisper no es un fallo del audio: confirmar antes de bloquear.
- Hugging Face está bloqueado; GitHub no.
- Procesos largos en el contenedor, no en device_bash (180 s).
- Nunca editar los archivos del agente de producción; solo escribir en `qa/`.