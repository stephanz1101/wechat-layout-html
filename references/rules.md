# WeChat Layout Rules

This file is the longer reference behind `wechat-layout-html`.

## Contract

- Input: finished Markdown article
- Output: WeChat-compatible HTML body
- Default objective: stable paste behavior in 微信公众号 with restrained brand identity
- Out of scope: content rewriting, cover design, uploading to WeChat

## Hard Constraints

### Allowed structure

- Use `<div>` for body-level content
- Use `<span>` for inline emphasis
- Use `<img>` only if the user explicitly keeps inline article images

### Forbidden structure

- `<p>`
- `<h1>`
- `<h2>`
- `<blockquote>`
- `<section>`
- HTML comments
- CSS classes for article rendering

### CSS behavior

- Style inline
- Never use `text-indent`
- Avoid layout tricks that depend on browser defaults

## Visual Direction

The house style is:
- businesslike, not cold
- branded, not loud
- long-read friendly, not poster-like

The page should feel like a well-edited analyst memo with a soft personal signature.

## Approved Default Tokens

- Brand blue: `#2E50F5`
- Highlight background: `rgb(232,238,255)`
- Body text: `#333333`
- Section title text: `#222222`
- Paragraph: `font-size:15px; line-height:2.25; margin-bottom:5px`
- Section numeral: `font-size:52px; font-style:italic; margin-top:28px`
- Section title: `font-size:22px; font-weight:bold; font-style:italic; margin-top:3px; margin-bottom:8px`
- Subheading: `font-size:18px; line-height:1.9; margin-top:12px; margin-bottom:8px`
- Quote block: `border-left:3px solid #2E50F5; background:#FFFFFF; padding:2px 10px 2px 16px; margin:2px 0; border-radius:0 8px 8px 0`
- Quote text: same as body text, do not shrink it
- List row: `font-size:15px; line-height:1.55; margin-bottom:0`
- List marker: blue `> ` instead of numeric bullets

## Emphasis Heuristics

Use highlight spans for:
- claims with strategic weight
- labels in manual argument lists
- phrases that connect the article's thesis to user action

Avoid highlights for:
- filler transitions
- repeated product names
- adjacent phrases in the same sentence

## QA Pass

Search the output for these strings before returning:

- `<p`
- `<h1`
- `<h2`
- `<blockquote`
- `<section`
- `class=`
- `text-indent`
- `<!--`

Then inspect:
- are section numerals visually prominent?
- are quotes visibly distinct but still quiet enough not to compete with body copy?
- do paragraphs still feel breathable?
- did highlight usage stay sparse?
- are quote text metrics identical to body copy metrics?
- do all lists use the blue `> ` marker instead of numeric bullets?
