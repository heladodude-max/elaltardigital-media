---
name: "altar-digital-shorts"
description: "Crear 3 shorts verticales 9:16 (1-3 min) por día de El Altar Digital a partir del video largo del día, con voz Finn, música Lyria, miniaturas verticales y subida programada a YouTube."
---

# Shorts de El Altar Digital

Tres shorts independientes por día, sacados del guion y de las imágenes del video largo de ese día. Publican a las 5:00 am (-04:00) junto al largo.

## Reglas de contenido
- Cada short es independiente y útil solo. Una idea por short.
- Guion nuevo, hecho para short (no un recorte del largo). 170-260 palabras (1-3 min).
- Gancho en la primera frase (primeros 3 s). Promesa cumplida. Giro. Sin tramos planos.
- Cierre en bucle: la última frase vuelve a la primera sin repetirla igual.
- Sin cifras, estadísticas, ni dígitos. Sin QR ni 'el código de la pantalla'.
- Voz honesta con el texto bíblico. Si el tema lo pide, aviso de ayuda profesional.
- Título, miniatura y gancho prometen lo mismo.

## Aprendizajes de la auditoría vidIQ (29 oct 2026)
Los Shorts son el motor del canal: promedian 1,066 vistas contra 5 de los largos, pero convierten poco (2,719 vistas dieron +14 suscriptores netos). Muestra de 35 videos: señal, no ley.
- Fórmula de título y primera frase: afirmación contraintuitiva + personaje bíblico + conflicto humano, menos de 110 s cuando se pueda. Funcionaron: "El versículo del matrimonio que casi todos citan mal" (2,103 vistas), "Tenía razón y aun así estaba equivocado" (2,065), "El equipo imposible de Jesús" (1,646). Sin fechas en el título.
- CTA de marca fijo de unos 3 s al final: "La Palabra Diaria, todos los días." Sin hora. Se suma al CTA propio de cada short, que sigue siendo distinto en los tres del día.
- Serie Matrimonio: 5 Shorts con misma portada y mismo gancho inicial. En los títulos, sin dígitos (regla de cifras): "primera parte", "segunda parte" o un subtítulo propio.
- Al menos un Short por día retoma desde otro ángulo el tema del Short más visto de la semana.
- Los Shorts son siempre 9:16 (1080x1920). El 16:9 HD aplica solo a largos y miniaturas de largos.
- Cada semana, medir con vidIQ vistas, retención y suscriptores ganados por Short, y repetir lo que gane.

## Reglas anti-repetición (obligatorias)
- Un CTA distinto por short dentro del mismo día (por ejemplo: compartir el video, suscribirse, comentar algo concreto, escribir Amén). Nunca el mismo CTA en los tres.
- Ninguna frase de 4 o más palabras copiada del guion largo ni entre los tres shorts del día. Verificar con una comparación de 4-gramas normalizados (sin tildes ni puntuación) contra el guion largo y entre shorts. Reescribir hasta que no queden coincidencias (salvo citas bíblicas inevitables y muletillas de 4 palabras).
- Cada imagen se usa una sola vez por día entre los tres shorts. Dentro de un short, una imagen se repite como máximo dos veces y nunca seguida.
- Reutilizar el video largo más reciente del día (si hay guion-v2 o video-html-v2, usar esos).

## Librería de imágenes: reutilizar antes de generar (REGLA OBLIGATORIA)
Generar cuesta dinero. Antes de pedir una imagen nueva, buscar en lo ya generado y usar la que funcione.
- Orden: 1) imágenes del video largo del día (ya pagadas); 2) librería de días anteriores en EL ALTAR DIGITAL/<día>/ y en ~/gemini-tts-mcp/images/; 3) generar solo si nada sirve.
- Cómo buscar: hoja de contacto numerada con PIL de las candidatas (por nombre y tema de la frase) y mirarla. Nunca elegir solo por el nombre. Mantener un catálogo (archivo, tema, estilo A/B/Q, día en que se usó) y ponerlo al día.
- Sirve si: ilustra lo que dice la frase, mismo registro visual (B óleo, A foto documental, Q Biblia), sin texto legible, logos ni cruces, y el sujeto se deja centrar en vertical (el recorte 9:16 muestra cerca del 32 % del ancho).
- Sigue valiendo la regla de una imagen una sola vez por día entre los tres shorts. Entre días distintos se puede reutilizar una imagen genérica; una escena muy reconocible no se repite a la semana.
- Las nuevas se guardan con nombre descriptivo y entran al catálogo. En el resumen final decir cuántas se reutilizaron y cuántas se generaron.

## Pipeline
1. Preparar por día una hoja de contactos numerada de las imágenes del largo y un tar con ellas; mirar la hoja para elegir imágenes por tema (y completar con la librería según la sección anterior antes de generar nada).
2. Escribir los 3 guiones. Verificar anti-repetición.
3. Voz: Gemini TTS, voz Finn, estilo 'narrador devocional cálido, cercano y pausado, con convicción tranquila'. Un archivo por short.
4. Alinear: convertir a 16 kHz mono, alinear palabras con whisper-base (sherpa-onnx) y difflib contra el guion, guardar words.json.
5. Música: base Lyria ambiente a factor 0.06 con cola de 3 s; el nivel integrado debe quedar a 0.5 dB o menos de la voz.
6. Plan por short (JSON): lista de (frase ancla, imagen, foco x0, foco x1) y tarjetas de cita. Un recorte vertical de una imagen 16:9 muestra cerca del 32% del ancho, así que el foco (0 a 1) debe centrar al sujeto. Escenas a menos de 1.7 s se descartan.
7. Plantilla HTML 1080x1920: paneo Ken Burns horizontal, fundido 0.22 s, subtítulos de 4-5 palabras con la palabra activa en amarillo, tarjeta final de 3 s con logo y 'LA PALABRA DIARIA'.
8. Render con Playwright a 25 fps. TOTAL DE FRAMES = (duración de voz + 3) x 25. Error ya cometido: renderizar solo la duración de la voz deja el video sin tarjeta final y con 3 s de audio sobre una imagen congelada. Verificar siempre que la duración de video y audio coincidan y mirar el último frame.
9. Codificar libx264 CRF 19 y mezclar con loudnorm I=-16 TP=-1.5, aac 192k.
10. Miniatura vertical 1080x1920: 3-4 palabras en amarillo y blanco con contorno negro, etiqueta 'LA PALABRA DIARIA' arriba a la izquierda, imagen distinta si es posible (de la librería antes que generar). OBLIGATORIO: revisarla con el skill youtube-thumbnail-master (anthropic-skills:youtube-thumbnail-master) antes de subirla: correr su thumb_check.py (simulación móvil, squint, escala de grises) y puntuar con su rúbrica (meta 80 o más sobre 100); corregir si baja.
11. Entrega a la Mac en partes de 24 MB (máximo 100 MB por llamada de commit), unir con cat y probar decodificación con ffmpeg. Subir al chat los tres MP4 y las miniaturas con SendUserFile.
12. Subir a YouTube: privado con publish_at del día 05:00:00-04:00, categoría 22, descripción con gancho, versículo y enlace al largo del día, hashtags. Después fijar la miniatura (ya aprobada por youtube-thumbnail-master). Guardar guiones y estado.json en la carpeta shorts del día.

## Notas operativas
- Disco del contenedor pequeño: borrar frames tras codificar. No lanzar dos renders del mismo short a la vez (comparten carpeta de frames).
- Si hay que reemplazar un short ya subido, no se puede borrar por API: renombrar a '[DUPLICADO - BORRAR]', dejar privado y mover publish_at a una fecha lejana para que no se publique; el dueño lo borra a mano.
- No usar pkill -f con un patrón que aparezca en el propio comando.