# Content template GitHub

## Hello fellow contributor, we're glad to have you!

### Please use this template as a guide when creating pages for The Graph Academy Hub.

All pages use Markdown \(a cheat sheet for this can be found [here](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)\) so be sure to use `.md` as the extension when creating the page file. If you do not wish to use markdown, you can also use [Editor.md](https://pandao.github.io/editor.md/en.html) a open-source online markdown editor.

#### Click [here](./) for an example of what a fully-fledged page looks like.

## \[Template Begin\]

## Page Heading \[H1\]

### Summary \[H2\]

_A summary of what the page is about._

### Features \[H2\]

_Main features._

#### Sub-feature 1 \[H3\]

_Content for sub-feature 1._

#### Sub-feature 2 \[H3\]

_Content for sub-feature 2._

### Resources \[H2\]

_Relevant resources like website, github link, blog posts etc go here_


------------


# Content template GitBook

### All documentation written in the GitHub repo is automatically synced to http://docs.thegraph.academy/

## Section overview
To create a section overview, create a new folder and include an empty README.md only with the title of the section.

## Content structure
Use SUMMARY.md to structure of the content over at docs.thegraph.academy and to include/exclude files. Use this file for defining pages and subpages etc.

## Description

Add the following before the first headline to create a description

```
---
description: Detailed documentation about the roles within The Graph Network
---
```

## Page link

Add the following to create a page link

```
{% page-ref page="../the-graph-ecosystem/organizational-structure/edge-and-node.md" %}
```

## Hints

Add the following to create hints:
```
{% hint style="danger" %} Text. {% endhint %}
```
```
{% hint style="success" %} Text. {% endhint %}
```
```
{% hint style="success" %} Text. {% endhint %}
```
```
{% hint style="info" %} Text. {% endhint %} {% endtab %}
```

## Tabs
Add tabs this way
```
{% tabs %} {% tab title="Indexing rewards" %}
Text
{% tab title="Query fee rebates" %}
Text
```


