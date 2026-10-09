# Docker Cheatsheet · Cola de referência de comandos Docker

> 🌍 [中文](README.md) · [Español](README.es.md)

Uma **cola de uma página só** com comandos do Docker: 28 comandos reais de `docker` / `docker compose`. Cada entrada responde a apenas três perguntas: **o que ela faz, um comando pronto para copiar e colar, e etiquetas de uso**. Sem parâmetros inventados.

## Para quem é

Engenheiros de operações (SRE/DevOps), desenvolvedores backend e qualquer pessoa que trabalhe com contêineres todos os dias. Se cada `docker run` te obriga a pesquisar os parâmetros, esta cola resolve isso de uma vez.

## Como usar

1. Vá direto ao **[CHEATSHEET.md](CHEATSHEET.md)**: o corpo da referência; os comandos em inglês qualquer desenvolvedor entende.
2. Instale o Docker primeiro: Docker Desktop no seu computador, Docker Engine em servidores Linux. Verifique com `docker run hello-world`.
3. Siga a ordem da cola —imagens → contêineres → logs → volumes/redes → Dockerfile → Compose → limpeza → depuração— e teste cada comando na mão. Em uma hora você domina tudo.

## Teste em 30 segundos

```bash
docker run -d --name hello -p 8080:80 nginx:1.27   # sobe um nginx
curl localhost:8080                               # se vir a página de boas-vindas, funcionou
docker rm -f hello                                # apague ao terminar
```

## O que está incluído

| Categoria | Conteúdo |
|---|---|
| 🖼️ Imagens | pull / build / tag / push / rmi / prune (7) |
| 📦 Ciclo de vida | run (-d/--name/-p/-v) / ps / start·stop·restart / rm (5) |
| 🔍 Dentro do contêiner e logs | exec -it / logs -f / cp (3) |
| 💾 Volumes e redes | volume / network (3) |
| 📝 Dockerfile | instruções essenciais + exemplo funcional (2) |
| 🐳 Docker Compose | up -d / down / logs·ps·exec + exemplo de compose.yaml (3) |
| 🧹 Limpeza | system prune (com aviso) / container prune (2) |
| 🩺 Depuração | inspect / stats / top + receita de 3 passos (3) |

A documentação oficial é só https://docs.docker.com/; cada comando foi verificado contra ela.
## Contribuições são bem-vindas

Achou um comando errado, um parâmetro desatualizado ou uma tradução a melhorar? *Pull requests* são bem-vindos. Mantenha o formato (descrição / bloco bash / etiquetas) e **só comandos reais e verificados; na dúvida, melhor não incluir**.

## Licença

MIT © 2026 Guangyi Zhao. Veja [LICENSE](LICENSE).
