# git-heatmap

> 终端版 Git 贡献热力图 —— 一个命令，把 GitHub 个人主页那张绿格子贡献图搬进你的终端

**单文件 · 零依赖 · 跨平台**，Python 3.6+ 开箱即用。

```text
$ python heatmap.py --days 120
     5月                  6月                          7月                          8月                          9月
 一  ···········
 二  ···········
 三  ···········
 四  ··········▓
 五  ···········
 六  ···········
 日  ···········

  总提交 87 次 | 活跃天数 23 天 | 统计区间 2026-05-20 ~ 2026-09-17（120 天）
  少 ·░▒▓█ 多
```

在支持 ANSI 256 色的终端里，会渲染成 GitHub 同款的绿→深绿色阶色块。

## 🚀 快速开始

```bash
# 克隆或直接下载 heatmap.py 单文件即可
python heatmap.py                    # 统计当前目录的 git 仓库，最近一年
python heatmap.py /path/to/repo      # 统计指定仓库
python heatmap.py --days 90          # 只看最近 90 天
python heatmap.py --author me@x.com  # 多人仓库只看自己的提交
```

无需 `pip install` 任何东西 —— 只用 Python 标准库。

## ✨ 特性

- **零依赖**：`argparse` / `subprocess` / `datetime` / `collections` 纯标准库实现
- **跨平台**：Windows / macOS / Linux 通用
- **智能渲染**：TTY 下自动启用 ANSI 256 色色阶（5 档热度）；管道/重定向时自动降级为字符模式 `·░▒▓█`，方便写进日志和 README
- **作者过滤**：`--author` 支持姓名或邮箱
- **统计摘要**：总提交数、活跃天数、统计区间一目了然

## 🔧 实现原理

1. `git log --pretty=format:%ad --date=format:%Y-%m-%d` 抽取每天的提交日期
2. `Counter` 聚合成「日期 → 提交次数」映射
3. 以周一为起点切周列，映射到 5 档热度色阶
4. `isatty()` 检测决定彩色 / 字符双渲染模式

核心逻辑不到 200 行，是一份不错的 Python 标准库综合运用示例。

## 📄 License

[MIT](./LICENSE)
