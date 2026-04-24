---
name: wechat-layout-html
description: Use when turning Markdown or article drafts into 微信公众号 / WeChat Official Account HTML, especially for 公众号排版, 微信 HTML, 微信兼容排版, 粘贴到公众号, or the locked blue div-only style.
---

# WeChat Layout HTML

Turn a finished Markdown article into WeChat-friendly HTML without drifting back into generic webpage markup.

This skill is for article body layout only. It does not rewrite content, design cover images, or publish to the WeChat draft box.

## When To Use

Use this skill when:
- the source content is already written in Markdown
- the user wants HTML that can be pasted into 微信公众号 with minimal deformation
- the article needs a restrained knowledge-style layout with a light brand signature
- the user wants to iterate on colors, spacing, and emphasis using HTML samples

Do not use this skill when:
- the user only needs article writing or rewriting
- the user wants a cover image or complex visual asset system
- the user already provides final WeChat-safe HTML and only needs upload

If the user asks to upload a Markdown/article draft to WeChat, use this skill first to generate the final HTML, then use `wechat-mp-publish` to send that HTML to the draft box. Do not send Markdown through a generic publisher renderer when this house style is expected.

## Core Rule

WeChat compatibility outranks generic web elegance.

If a choice looks slightly nicer on the open web but is less stable inside WeChat, reject it.

## Baseline Failure Pattern

Common bad outputs look “HTML-complete” but fail the actual WeChat use case:
- using `<p>` and getting forced indentation
- using `<h1>` / `<h2>` / `<blockquote>` / `<section>` and losing style control
- relying on `<style>` blocks or CSS classes that WeChat strips or weakens
- producing generic list and quote markup instead of controlled inline components
- highlighting too many phrases until the page looks noisy

If the draft looks like a normal article webpage, assume it is wrong until proven otherwise.

## Locked Compatibility Rules

These rules are mandatory unless the user explicitly overrides them.

### HTML structure

- Use `<div>` for all body paragraphs and content blocks
- Do not use `<p>`
- Do not use `<h1>`, `<h2>`, `<blockquote>`, or `<section>`
- Do not use HTML comments
- Do not use `class`

### CSS rules

- Put all styling inline through `style`
- Do not use `text-indent`
- Do not rely on external CSS or `<style>` blocks for article body behavior

### Tone of layout

- Default to restrained professional structure
- Put brand signature in a few places only: section numbers, keyword highlights, quote block accents, and manual list markers
- Every paragraph gets at most 1 to 2 highlight treatments

## Locked Visual System

### Color tokens

| Usage | Value |
|---|---|
| Section number / list marker / keyword text | `#2E50F5` |
| Keyword highlight background | `rgb(232,238,255)` |
| Quote background | `#FFFFFF` |
| Quote left border | `#2E50F5` |
| Body text | `#333333` |
| Section title text | `#222222` |
| Quote text | `#333333` |

### Body metrics

- Outer container: `padding:0 20px; font-family:'PingFang SC','Hiragino Sans GB','Microsoft YaHei',sans-serif;`
- Paragraph: `font-size:15px; line-height:2.25; color:#333333; margin-bottom:5px;`
- Section number: `font-size:52px; font-weight:bold; font-style:italic; color:#2E50F5; margin-top:28px; line-height:1;`
- Section title: `font-size:22px; font-weight:bold; font-style:italic; color:#222222; margin-top:3px; margin-bottom:8px; line-height:1.4;`
- Subheading: `font-size:18px; line-height:1.9; color:#222222; font-weight:bold; margin-top:12px; margin-bottom:8px;`
- Quote block: `border-left:3px solid #2E50F5; background:#FFFFFF; padding:2px 10px 2px 16px; margin:2px 0; border-radius:0 8px 8px 0;`
- Quote text: `font-size:15px; line-height:2.25; color:#333333;`
- List row: `font-size:15px; line-height:1.55; color:#333333; margin-bottom:0;`

## Component Mapping

Map Markdown structure to WeChat-safe blocks like this:

| Markdown input | Output shape |
|---|---|
| `# Title` | one title `<div>` with stronger size and darker text |
| plain paragraph | standard paragraph `<div>` |
| `## 1 Title` | separate section number `<div>` + section title `<div>` |
| `### 1.1 Title` | smaller bold paragraph-style heading `<div>` |
| `> quote` | custom quote `<div>` with left border and controlled white background |
| `- item` | paragraph-like list row with manual blue `>` marker treatment |
| `**keyword**` | convert selectively into controlled emphasis; do not blindly bold every case |
| inline key phrase | use highlight span only when it sharpens the paragraph |

## Required Components

### 1. Container

```html
<div style="padding:0 20px; font-family:'PingFang SC','Hiragino Sans GB','Microsoft YaHei',sans-serif;">
  ...
</div>
```

### 2. Standard paragraph

```html
<div style="font-size:15px; line-height:2.25; color:#333333; margin-bottom:5px;">
  正文内容。
</div>
```

### 3. Section number + title

```html
  <div style="font-size:52px; font-weight:bold; font-style:italic; color:#2E50F5; margin-top:28px; line-height:1;">1</div>
<div style="font-size:22px; font-weight:bold; font-style:italic; color:#222222; margin-top:3px; margin-bottom:8px; line-height:1.4;">
  眼脑手一起优化，推进复杂现实项目交付
</div>
```

### 4. Quote block

```html
<div style="border-left:3px solid #2E50F5; background:#FFFFFF; padding:2px 10px 2px 16px; margin:2px 0; border-radius:0 8px 8px 0;">
  <div style="font-size:15px; line-height:2.25; color:#333333;">
    更高的复杂任务成功率
  </div>
</div>
```

### 5. Manual list row

```html
<div style="font-size:15px; line-height:1.55; color:#333333; margin-bottom:0;">
  <span style="color:#2E50F5; font-weight:bold;">&gt;</span>
  更高的复杂任务成功率
</div>
```

### 6. Keyword highlight

```html
<span style="background:rgb(232,238,255); padding:0 4px; border-radius:3px; font-weight:bold; color:#2E50F5;">深度用户</span>
```

## Decision Standard

Choose the lighter treatment by default.

Escalate emphasis only when one of these is true:
- the phrase is the paragraph's main claim
- the phrase is a list item label
- the phrase is a transition sentence the reader must not miss

Do not highlight:
- obvious nouns with no strategic value
- every bold phrase from the Markdown source
- more than 2 phrases in the same paragraph

## Recommended Workflow

1. Read the Markdown article fully before touching HTML
2. Mark the true section boundaries
3. Pull out only the highest-value phrases for highlight treatment
4. Convert all body content to div-based blocks
5. Replace generic quotes and lists with controlled inline components
6. Scan for banned tags and styling patterns
7. Save one output HTML and, when useful, a second stylistic variant for review

## Release Gate

Before returning HTML, verify all of the following:

- no `<p>` tags
- no `<h1>`, `<h2>`, `<blockquote>`, or `<section>`
- no `class=`
- no HTML comments
- no `text-indent`
- all visible styling is inline
- section structure is visually obvious
- quote blocks use the locked blue system
- highlights are sparse and intentional

## Common Mistakes

| Mistake | Why it fails | Correct move |
|---|---|---|
| Converting Markdown directly to generic HTML | Produces web markup, not WeChat-safe markup | Rebuild body with div-based components |
| Keeping all original bold text | Visual noise and weak hierarchy | Keep only the phrases that carry argument weight |
| Using list tags for convenience | Style control becomes inconsistent | Write each item as a styled row |
| Designing like a landing page | Too decorative for long reading | Return to restrained body copy and sparse accents |
| Over-branding | Kills reading flow | Put brand only in section numerals, list markers, highlights, and quote accents |

## Reference Files

- Use [references/rules.md](references/rules.md) for the full locked rules and QA checklist
- Use [references/template.html](references/template.html) as the starting skeleton
- Use the HTML samples in `output/wechat-skill-samples/` as visual anchors when tuning
- Treat `output/wechat-skill-samples/opus47-signature-full-strict.html` as the approved default baseline
