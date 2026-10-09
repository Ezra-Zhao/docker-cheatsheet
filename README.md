# Docker 命令速查表 · Docker Cheatsheet

> 🌍 [Español](README.es.md) · [Português](README.pt.md)

一份**一页纸**的 Docker 命令速查表：28 条真实可用的 `docker` / `docker compose` 命令，每个条目只讲三件事——**它是干什么的、一条能直接复制粘贴的命令、适用场景标签**。不编造参数，不拼凑语法。

## 面向谁

运维工程师、后端开发者，以及每天跟容器打交道的你。如果你每次 `docker run` 都要现查参数，这张表能让你把最常用的命令一次记牢。

## 怎么用

1. 直接看 **[CHEATSHEET.md](CHEATSHEET.md)** ——速查表正文，英文命令全球开发者都无压力。
2. 先装好 Docker：桌面端用 Docker Desktop，Linux 服务器用 Docker Engine，装完跑 `docker run hello-world` 验证。
3. 按"镜像 → 容器 → 日志 → 数据卷/网络 → Dockerfile → Compose → 清理 → 调试"的顺序，每个条目亲手敲一遍，一小时就顺手了。

## 先跑起来（30 秒验证环境）

```bash
docker run -d --name hello -p 8080:80 nginx:1.27   # 起一个 nginx
curl localhost:8080                               # 看到欢迎页就是成了
docker rm -f hello                                # 用完删掉
```

## 收录了什么

| 分类 | 内容 |
|---|---|
| 🖼️ 镜像 | pull / build / tag / push / rmi / prune（7 条） |
| 📦 容器生命周期 | run（-d/--name/-p/-v）/ ps / start·stop·restart / rm（5 条） |
| 🔍 进容器与日志 | exec -it / logs -f / cp（3 条） |
| 💾 数据卷与网络 | volume / network（3 条） |
| 📝 Dockerfile | 常用指令速览 + 可跑示例（2 条） |
| 🐳 Docker Compose | up -d / down / logs·ps·exec + compose.yaml 示例（3 条） |
| 🧹 清理 | system prune（高危提示）/ container prune（2 条） |
| 🩺 调试 | inspect / stats / top + 排查三板斧（3 条） |

官方文档只链 https://docs.docker.com/，所有命令均对照官方文档核实过语法。

## 为什么是这 28 条

- **覆盖 90% 日常**：镜像、容器、日志、清理这几类就是每天敲的命令，冷门参数不收。
- **Compose 实战**：附 web+db 的 compose.yaml 示例，复制改两行就能跑。
- **调试三板斧**：容器起不来时 logs → inspect → exec，照着排查不抓瞎。

## 欢迎 PR

发现命令写错了、参数过时了、翻译不到位——欢迎提 Pull Request。新增条目请保持统一格式（一句话说明 / bash 代码块 / 标签），**只收真实可用的命令，不确定的宁可不收**。

## License

MIT © 2026 Guangyi Zhao，详见 [LICENSE](LICENSE)。
