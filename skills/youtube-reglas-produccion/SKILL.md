---
name: "youtube-reglas-produccion"
description: "Reglas fijas para todo video, Short o miniatura de los canales de YouTube de Roberto (El Altar Digital, The Untold Story): reutilizar imágenes ya generadas antes de generar, revisar toda miniatura con youtube-thumbnail-master y basarla en el patrón de las mejores de la competencia, que el video entretenga y no parezca una clase, y capítulos con tiempos en la descripción."
---

# Reglas de producción para los canales de YouTube de Roberto

Se aplican siempre que haya que hacer un video largo, un Short, una miniatura o cualquier imagen para El Altar Digital, The Untold Story o un canal nuevo suyo. Mandan junto a los skills propios de cada canal (altar-digital-video-html, altar-digital-shorts, altar-digital-footage, altar-digital-qa, the-untold-story); si alguno dice menos, estas reglas se suman.

## 1. Librería de imágenes: reutilizar antes de generar (obligatoria)
Generar imágenes cuesta dinero. Antes de pedir cualquier imagen nueva (escena de largo, escena de Short, fondo de miniatura), buscar entre las ya generadas y usar la que funcione.
- Dónde mirar en la Mac de Roberto: ~/gemini-tts-mcp/images/ (todo lo que sale de Nano Banana), las carpetas de pilotos en ~/Documents/gemini-tts/ (piloto1/, piloto2/...) y, en El Altar Digital, EL ALTAR DIGITAL/<día>/ de días anteriores. Si no se ven, pedir acceso con device_request_folder_access.
- Cómo buscar: listar, filtrar por nombre y por el tema de la frase o escena, stagear las candidatas, armar una hoja de contacto numerada con PIL y MIRARLA. Nunca elegir solo por el nombre del archivo.
- Catálogo: mantener un images-catalogo.tsv por canal (archivo, tema, época o estilo, personajes, formato 16:9 o 9:16, video donde se usó). Cada imagen nueva se agrega al generarla.
- Sirve si: ilustra lo que dice la frase; mismo estilo visual del canal; formato correcto (16:9 para largos, 9:16 para Shorts; un 16:9 se puede recortar a vertical solo si el sujeto queda centrado); sin texto legible, logos ni cruces; pasa el mismo QA de época o de registro que una imagen nueva (en The Untold Story, nada anacrónico; en El Altar Digital, B óleo, A foto documental, Q Biblia, sin mezclar).
- No sirve si encaja a medias (otra hora, otra acción, otro personaje): se genera. No forzar.
- Límites de repetición: en un mismo video una imagen no sale más de dos veces ni seguida; en El Altar Digital cada imagen se usa una sola vez por día entre los tres Shorts. Los Shorts pueden reutilizar imágenes de su video largo (ya están pagadas). Entre videos distintos solo se reutiliza lo genérico, nunca una escena muy reconocible.
- Las escenas modernas con clip de video siguen el orden de altar-digital-footage: librería de clips, stock gratis, y solo después foto (de la librería de imágenes primero, generada al final).
- Las imágenes nuevas se guardan con nombre descriptivo y entran al catálogo.
- Al terminar, el resumen dice cuántas imágenes se reutilizaron y cuántas se generaron.

## 2. Miniaturas: revisar con youtube-thumbnail-master (obligatoria)
Toda miniatura, de video largo o de Short, se revisa con el skill youtube-thumbnail-master (anthropic-skills:youtube-thumbnail-master) antes de mostrársela a Roberto y antes de subirla.
- Elegir 2 o 3 tipos distintos de su catálogo y definir el concepto antes de generar.
- Antes de definir el concepto, mirar qué miniaturas ganan hoy en la competencia que más se parece a nuestro contenido (mismo nicho e idioma): vidiq_similar_thumbnails con una descripción visual del concepto y vidiq_outliers por palabra clave e idioma, con minEngagementRate cerca de 0.02 para limpiar resubidas y granjas de clics. Tomar 5 a 10 ejemplos y anotar de cada uno el tipo T, qué hay en cuadro, la emoción, cuántas palabras lleva y dónde, la paleta y la composición. Lo que se repite en las que mejor rinden es el patrón ganador; se guarda en benchmark-miniaturas.md del canal.
- Se copia el patrón, no la imagen. La miniatura nueva es original: mismo tipo, misma composición, misma emoción y mismo ritmo de texto, con nuestro personaje, nuestra escena y la paleta del canal. Nunca se reproduce, recorta, recolorea ni retoca la miniatura de otro canal, ni su rostro, su logo o su texto exacto.
- El patrón pasa por los límites de cada canal: en The Untold Story sin caras reales (personajes de caricatura expresivos); en El Altar Digital sin cifras ni cruces y con la marca "LA PALABRA DIARIA".
- vidIQ gasta créditos: la investigación se hace una vez por canal o serie y se refresca de vez en cuando o si el nicho cambia, no en cada miniatura. Entre refrescos se reutiliza la ficha.
- La imagen generada sale sin texto; el texto se compone después (PIL o scripts/compose_text.py). El fondo también sale primero de la librería de imágenes si algo sirve.
- Auditar con `python scripts/thumb_check.py <imágenes> --out <carpeta>` (simulación móvil a 168 px, squint, escala de grises, zona de duración abajo a la derecha) y puntuar con su rúbrica de 100 puntos (references/qa-and-testing.md). Meta: 80 o más; si baja, corregir antes de seguir.
- Formato final 1280x720 (o 1920x1080 en The Untold Story), menos de 2 MB. El Short usa 1080x1920 con su propio gancho.
- El puntaje queda anotado (en El Altar Digital, en qa/informe-miniatura.json). Sin esta revisión no se sube.
- Si el video ya es público y hay créditos, se puede sumar vidiq_score_thumbnail.

## 3. Entrega
Todo lo que Roberto deba ver (videos, imágenes, miniaturas, archivos) se sube al chat con SendUserFile, siempre, sin que lo pida.

## 4. Que entretenga, no que parezca una clase (obligatoria desde el 1 de noviembre de 2026)
Todo video de los canales de Roberto, largo o Short, tiene que entretener. Se siente como una historia o una experiencia, nunca como una clase de historia. Esta regla se suma al skill de cada canal sin romper su tono, su rigor ni sus reglas duras: en El Altar Digital sigue mandando la voz cálida, respetuosa y empática; ahí entretener es narrar con escena, tensión y giro, no hacer chistes ni bajar el respeto.
Prueba de sí o no antes de grabar y antes de entregar; si algo falla, se reescribe:
- Abre con una escena, un personaje o una pregunta, no con contexto, una definición o una fecha.
- Hay un giro, una sorpresa o un cambio de ritmo al menos cada 2 minutos.
- El espectador sigue a alguien o algo (una persona, un conflicto, una duda) y no un inventario de datos.
- No hay frases de aula: "a continuación veremos", "es importante señalar", "en este video hablaremos de".
- Los datos entran dentro de una escena o de un giro, nunca en fila. El rigor no se negocia: entretener no permite inventar ni exagerar.
- Alguien que no sabe nada del tema seguiría viendo a los 30 segundos y en el minuto 10.
El resultado de la prueba se anota en el estado del video.

## 5. Capítulos con tiempos en la descripción (obligatoria desde el 1 de noviembre de 2026)
Todo video largo lleva capítulos: una lista de tiempos en la descripción, un tiempo por línea y el título al lado (por ejemplo "0:00 Título"). Formato mm:ss, y h:mm:ss si pasa de una hora.
- Requisitos de YouTube: el primero va en 0:00, mínimo 3 capítulos, cada uno de 10 segundos o más, un tiempo por línea con su título y en orden. Los Shorts no llevan capítulos: duran muy poco.
- Los tiempos salen de la alineación real del audio (en The Untold Story, los tiempos por palabra de faster-whisper o la suma de los wavs por bloque; en un video armado como HTML, los tiempos de escena de datos.json), nunca de una estimación a ojo. Se comprueban contra el MP4 final, contando cualquier intro o cierre sumado.
- Cada capítulo es un bloque real de la estructura del guion, más o menos uno cada 1 a 3 minutos (en un largo de 25 minutos, unos 8 a 12).
- Títulos de 2 a 5 palabras, en el idioma del video, que den curiosidad sin spoilers: instalan la pregunta, el video la responde.
- Van en la descripción debajo de las dos primeras líneas, que siguen siendo el gancho. Después de subir, mirar en YouTube Studio que los reconoció (se ven como segmentos en la barra de reproducción).
- Excepciones: en El Altar Digital no se agregan hasta que Roberto confirme que los tiempos son una excepción a su regla "sin cifras". En Corazones en Penumbra y Metamorfisis solo si Roberto lo pide, porque los títulos de capítulo adelantarían la trama.