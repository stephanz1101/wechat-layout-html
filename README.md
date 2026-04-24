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

Use the GitHub repo path with the local skill installer:

```text
stephanz1101/wechat-layout-html
```

If you already have Codex skill installation wired up, install this repository as a standalone skill repo.

### Manual Fallback

If your agent environment does not support direct GitHub skill install, copy this repository into your local skills directory as:

```text
.../skills/wechat-layout-html/
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
