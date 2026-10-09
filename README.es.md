# Docker Cheatsheet · Hoja de referencia de comandos Docker

> 🌍 [中文](README.md) · [Português](README.pt.md)

Una **hoja de referencia de una sola página** con comandos de Docker: 28 comandos reales de `docker` / `docker compose`. Cada entrada responde solo tres preguntas: **qué hace, un comando listo para copiar y pegar, y etiquetas de uso**. Sin parámetros inventados.

## Para quién es

Ingenieros de operaciones (SRE/DevOps), desarrolladores backend y cualquiera que trabaje con contenedores a diario. Si cada `docker run` te obliga a buscar los parámetros, esta hoja te los deja grabados de una vez.

## Cómo usarla

1. Ve directo a **[CHEATSHEET.md](CHEATSHEET.md)**: el cuerpo de la referencia; los comandos en inglés los entiende cualquier desarrollador.
2. Instala Docker primero: Docker Desktop en tu equipo, Docker Engine en servidores Linux. Verifícalo con `docker run hello-world`.
3. Sigue el orden de la hoja —imágenes → contenedores → logs → volúmenes/redes → Dockerfile → Compose → limpieza → depuración— y prueba cada comando a mano. En una hora los dominas.

## Pruébalo en 30 segundos

```bash
docker run -d --name hello -p 8080:80 nginx:1.27   # levanta un nginx
curl localhost:8080                               # si ves la bienvenida, funciona
docker rm -f hello                                # bórralo al terminar
```

## Qué incluye

| Categoría | Contenido |
|---|---|
| 🖼️ Imágenes | pull / build / tag / push / rmi / prune (7) |
| 📦 Ciclo de vida | run (-d/--name/-p/-v) / ps / start·stop·restart / rm (5) |
| 🔍 Dentro del contenedor y logs | exec -it / logs -f / cp (3) |
| 💾 Volúmenes y redes | volume / network (3) |
| 📝 Dockerfile | instrucciones esenciales + ejemplo funcional (2) |
| 🐳 Docker Compose | up -d / down / logs·ps·exec + ejemplo de compose.yaml (3) |
| 🧹 Limpieza | system prune (con aviso) / container prune (2) |
| 🩺 Depuración | inspect / stats / top + receta de 3 pasos (3) |

La documentación oficial es solo https://docs.docker.com/; cada comando está verificado contra ella.
## Contribuciones bienvenidas

¿Un comando incorrecto, un parámetro desactualizado o una traducción mejorable? Los *pull requests* son bienvenidos. Mantén el formato (descripción / bloque bash / etiquetas) y **solo comandos reales y verificados; ante la duda, mejor no incluirlo**.

## Licencia

MIT © 2026 Guangyi Zhao. Ver [LICENSE](LICENSE).
