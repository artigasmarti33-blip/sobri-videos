# Procedimiento de publicación automática (autorizado por el usuario el 2026-11-07: "a partir de ahora publícalos tú todos")
La sesión principal (session_019ku4qY24Puv9gfxy1JVCbA, con el conector Metricool) publica TODOS los vídeos del canal
en TikTok, Instagram (Reel) y YouTube (Short) con Metricool, brand/blogId **7944183**, zona horaria Europe/Madrid.

## Horario fijo
| Hora | Vídeo |
|---|---|
| 09:00 | Noticia 1 (la más fuerte) |
| 10:00 | Noticia 2 |
| 12:00 | Noticia 3 |
| 18:00 | Curiosidades |
| 20:30 | Parte nueva de la serie MENSAJES |
Si una hora ya pasó (o faltan < 30 min) cuando el vídeo esté listo: programar dentro de 30-45 min, separando ≥ 45 min entre vídeos.

## Pasos por vídeo
1. `git pull` del repo del proyecto y copiar `video_final.mp4` aquí como `AAAA-MM-DD/<proyecto>_<slug>.mp4`; commit + push.
   URL pública: https://raw.githubusercontent.com/artigasmarti33-blip/sobri-videos/main/AAAA-MM-DD/<archivo>.mp4 (comprobar 200 con curl).
2. Metricool `createScheduledPost` (blogId 7944183): providers tiktok + instagram + youtube; `text` = descripcion.txt; media = [URL];
   `instagramData: {type: "REEL", showReelOnFeed: true}`; `tiktokData: {privacyOption: "PUBLIC_TO_EVERYONE"}`;
   `youtubeData: {type: "short", title: <titulo_youtube.txt o el gancho ≤ 90 car. + " #Shorts">, privacy: "public", madeForKids: false, category: NEWS_POLITICS (noticias) / EDUCATION (curiosidades) / ENTERTAINMENT (serie)}`;
   `firstCommentText` = opción 1 de comentario.txt (en Instagram/TikTok queda como primer comentario para fijar).
3. Avisar al usuario (SendUserFile proactive) con el vídeo, el texto, la hora y el plannerUrl, ≥ 30 min antes de publicarse.
   Si dice "para", borrar/posponer en Metricool (updateScheduledPost con draft: true).
4. Apuntar en el registro del proyecto: hora de publicación y redes.
