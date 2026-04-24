# WeChat Layout HTML Skill

Turn finished Markdown or article drafts into WeChat Official Account HTML that survives real 公众号 paste behavior.

This repository packages the standalone `wechat-layout-html` skill so other agents or operators can install it directly from GitHub.

## What It Solves

Generic Markdown-to-HTML conversion is not enough for WeChat. This skill locks the output to the compatibility constraints that actually matter:

- all body content uses `<div>`, not `<p>`
- no `<h1>`, `<h2>`, `<blockquote>`, or `<section>`
- all styles are inline
- no `class`
- no `text-indent`
- no HTML comments

It also ships the approved blue visual baseline:

- blue section numerals and list markers
- blue keyword highlight background
- white quote blocks with blue left border
- restrained, long-form reading rhythm tuned for WeChat articles

## Repository Layout

```text
wechat-layout-html/
├── SKILL.md
├── README.md
├── manifest.yaml
├── LICENSE
└── references/
    ├── rules.md
    └── template.html
```

## Install

### Codex

Clone this repository into your Codex skills directory:

```bash
git clone https://github.com/stephanz1101/wechat-layout-html.git ~/.codex/skills/wechat-layout-html
```

If the directory already exists, update it with:

```bash
cd ~/.codex/skills/wechat-layout-html && git pull
```

You can also point any GitHub-based skill installer at:

```text
stephanz1101/wechat-layout-html
```

### Other Agent Environments

If your environment does not support direct GitHub skill install, copy this repository into that agent's local skills directory under:

```text
.../skills/wechat-layout-html/
```

The repository root is already structured as a standalone skill package, so no extra rearrangement is needed.

## Pair With Draft Publishing

This skill handles layout only.

If you also need one-step upload into the WeChat Official Account draft box, pair it with:

```text
stephanz1101/wechat-mp-publish
```

Recommended flow:

1. run `wechat-layout-html` to generate final WeChat-safe HTML
2. run `wechat-mp-publish` to upload that HTML to the draft box

## Agent Prompt Examples

Use prompts like these after installation:

```text
Use wechat-layout-html to turn this Markdown article into WeChat-safe HTML.
```

```text
按微信公众号排版规则，把这篇 Markdown 转成微信兼容 HTML。
```

```text
把这篇文章排成蓝色 div-only 风格的公众号 HTML，不要改原文内容。
```

```text
Generate final WeChat Official Account HTML from this article draft. Keep all styling inline and avoid p/h1/h2/blockquote/section.
```

## When To Use

Use this skill when you need:

- 微信公众号 / WeChat Official Account article body layout
- 微信兼容 HTML from Markdown or article drafts
- controlled blue div-only style instead of generic webpage markup
- stable HTML before uploading to a WeChat draft box

## What This Skill Does Not Do

- it does not rewrite the article
- it does not design cover images
- it does not publish by itself

For publishing, pair it with a separate WeChat draft upload skill or workflow after the final HTML is generated.

## Notes

- `SKILL.md` is the main executable instruction file
- `references/rules.md` contains the locked rules and QA checklist
- `references/template.html` is the starting skeleton

## License

MIT
