---
title: "@namespace"
slug: Web/CSS/@namespace
page-type: css-at-rule
browser-compat: css.at-rules.namespace
sidebar: cssref
---

**`@namespace`** is an [at-rule](/en-US/docs/Web/CSS/CSS_syntax/At-rule) that defines XML [namespaces](/en-US/docs/Glossary/Namespace) to be used in a [CSS](/en-US/docs/Glossary/CSS) [style sheet](/en-US/docs/Web/API/StyleSheet).

{{InteractiveExample("CSS Demo: @namespace", "tabbed-shorter")}}

```css interactive-example
@namespace svg url("http://www.w3.org/2000/svg");

a {
  color: orangered;
  text-decoration: underline dashed;
  font-weight: bold;
}

svg|a {
  fill: blueviolet;
  text-decoration: underline solid;
  text-transform: uppercase;
}
```

```html interactive-example
<p>
  <a href="#">This is an ordinary HTML link</a>
</p>

<svg width="250px" viewBox="0 0 250 20" xmlns="http://www.w3.org/2000/svg">
  <a href="#">
    <text x="0" y="15">This is a link created in SVG</text>
  </a>
</svg>
```

## Syntax

```css
/* Default namespace */
@namespace url(XML-namespace-URL);
@namespace "XML-namespace-URL";

/* Prefixed namespace */
@namespace prefix url(XML-namespace-URL);
@namespace prefix "XML-namespace-URL";
```

## Description

The defined namespaces can be used to restrict the [universal](/en-US/docs/Web/CSS/Universal_selectors), [type](/en-US/docs/Web/CSS/Type_selectors), and [attribute](/en-US/docs/Web/CSS/Attribute_selectors) [selectors](/en-US/docs/Learn_web_development/Core/Styling_basics/Basic_selectors) to only select elements within that namespace. The `@namespace` rule is generally only useful when dealing with documents containing multiple namespaces—such as HTML with inline SVG or MathML, or XML that mixes multiple vocabularies.

Any `@namespace` rules must follow all {{cssxref("@charset")}} and {{cssxref("@import")}} rules, and precede all other at-rules and [style declarations](/en-US/docs/Web/API/CSSStyleDeclaration) in a style sheet.

`@namespace` can be used to define the **default namespace** for the style sheet. When a default namespace is defined, all universal and type selectors (but not attribute selectors, see note below) apply only to elements in that namespace.

The `@namespace` rule can also be used to define a **namespace prefix**. When a universal, type, or attribute selector is prefixed with a namespace prefix, then that selector only matches if the namespace _and_ name of the element or attribute matches.

In HTML, known [foreign elements](https://html.spec.whatwg.org/multipage/syntax.html#foreign-elements) will automatically be assigned namespaces. This means that HTML elements will act as though they are in the XHTML namespace (`http://www.w3.org/1999/xhtml`), even if there is no `xmlns` attribute anywhere in the document, and the [`<svg>`](/en-US/docs/Web/SVG/Reference/Element/svg) and [`<math>`](/en-US/docs/Web/MathML/Reference/Element/math) elements will be assigned their proper namespaces (`http://www.w3.org/2000/svg` and `http://www.w3.org/1998/Math/MathML`, respectively).

> [!NOTE]
> In XML, unless a prefix is defined directly on an attribute (_e.g._, `xlink:href`), that attribute has no namespace. In other words, attributes do not inherit the namespace of the element they're on. To match this behavior, the default namespace in CSS does not apply to attribute selectors.

## Formal syntax

{{csssyntax}}

## Examples

### Specifying default and prefixed namespaces

```css
@namespace url(http://www.w3.org/1999/xhtml);
@namespace svg url(http://www.w3.org/2000/svg);

/* This matches all XHTML <a> elements, as XHTML is the default unprefixed namespace */
a {
}

/* This matches all SVG <a> elements */
svg|a {
}

/* This matches both XHTML and SVG <a> elements */
*|a {
}
```

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- [Namespaces crash course](/en-US/docs/Web/SVG/Guides/Namespaces_crash_course)
- [CSS at-rule functions](/en-US/docs/Web/CSS/CSS_syntax/At-rule_functions)
