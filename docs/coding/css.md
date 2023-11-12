---
layout: default
nav_order: 2
title: css
permalink: coding/css
parent: coding
#grand_parent: 
#has_children: true
has_toc: True
#date: 2023-11-12 08:51:23 +0300
#tags: []
#categories: []
math: true
mermaid: true
last_modified_date: 2023-11-12 +0300
---

# css
{: .no_toc}

This is notes for css.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Number in Circle

```css
<style>
.numberCircle {
    border-radius: 50%;
    width: 36px;
    height: 36px;
    padding: 8px;

    #background: #fff;
    border: 2px solid #666;
    #color: #666;
    text-align: center;
    font: 32px Arial, sans-serif;
}
.numberCircle2 {
    width: 120px;
    line-height: 120px;
    border-radius: 50%;
    text-align: center;
    font-size: 32px;
    border: 2px solid #666;
}	
</style>
```

Example:

```markdown
<div class="numberCircle">1</div>
<div class="numberCircle">10</div>
<div class="numberCircle2">1000</div>
```

## Color

```css
<style>
	red {color: red}
	orange {color: orange}
	lime {color: Lime}
	aqua {color: Aqua}
	fuchsia {color: Fuchsia}
	grey {color: Grey}
	blue {color: Blue}
</style>
```


Example:

```markdown
- <span style="color:blue">HTML Blue text</span>
- <red>Red</red>
- <orange>Orange</orange>
- <lime>Lime</lime>
- <aqua>Aqua</aqua>
- <fuchsia>Fuchsia</fuchsia>
- <grey>Grey</grey>
- <blue>Blue</blue>
```