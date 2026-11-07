# Procedimiento de publicación automática (autorizado por el usuario el 2026-11-07: "a partir de ahora publícalos tú todos"; quiere AVISO de cada subida)
La sesión principal (session_019ku4qY24Puv9gfxy1JVCbA, con el conector Metricool) publica TODOS los vídeos del canal
en TikTok, Instagram (Reel) y YouTube (Short) con Metricool, brand/blogId **7944183**, zona horaria Europe/Madrid.

## Horario fijo
| Hora | Vídeo |
|---|---|
| 09:00 | Noticia 1 (la más fuerte) |
| 10:00 | Noticia 2 |
| 12:00 | Noticia 3 |
| 14:00 | Tendencia del día |
| 16:00 | Acertijos |
| 18:00 | Curiosidades |
| 20:30 | Parte nueva de la serie MENSAJES |
| 22:00 | Parte nueva de la serie 30 DÍAS |
Si una hora ya pasó (o faltan < 30 min) cuando el vídeo esté listo: programar dentro de 30-45 min, separando ≥ 45 min entre vídeos.

## Pasos por vídeo
1. `git pull` del repo del proyecto y copiar `video_final.mp4` aquí como `AAAA-MM-DD/<proyecto>_<slug>.mp4`; commit + push.
   URL pública: https://raw.githubusercontent.com/artigasmarti33-blip/sobri-videos/main/AAAA-MM-DD/<archivo>.mp4 (comprobar 200 con curl).
2. Metricool `createScheduledPost` (blogId 7944183): providers tiktok + instagram + youtube; `text` = descripcion.txt; media = [URL];
   `instagramData: {type: "REEL", showReelOnFeed: true}`; `tiktokData: {privacyOption: "PUBLIC_TO_EVERYONE"}`;
   `youtubeData: {type: "short", title: <titulo_youtube.txt o el gancho ≤ 90 car. + " #Shorts">, privacy: "public", madeForKids: false, category: NEWS_POLITICS (noticias) / EDUCATION (curiosidades, acertijos, tendencias) / ENTERTAINMENT (serie)}`;
   `firstCommentText` = opción 1 de comentario.txt (en Instagram/TikTok queda como primer comentario para fijar).
3. AVISO 1 (al programar, ≥ 30 min antes): SendUserFile (proactive) con el vídeo + mensaje "📅 Programado: <vídeo> · <hora> · TikTok, Instagram y YouTube"
   con el texto y el plannerUrl, y PushNotification con el mismo resumen corto. Si dice "para", posponer en Metricool (updateScheduledPost con draft: true).
4. AVISO 2 (a la hora de publicación): programar con send_later un recordatorio a la hora exacta de publicación que haga:
   PushNotification + mensaje "🚀 Publicando ahora: <vídeo> en TikTok, Instagram y YouTube"; 10 min después comprobar con getScheduledPosts
   (ya no debe estar pendiente) y avisar "✅ Publicado" o "⚠️ Falló en <red>" con lo que haya que hacer.
5. Apuntar en el registro del proyecto: hora de publicación y redes.
