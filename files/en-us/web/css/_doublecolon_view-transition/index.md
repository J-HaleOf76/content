---
title: ::view-transition
slug: Web/CSS/::view-transition
page-type: css-pseudo-element
browser-compat: css.selectors.view-transition
sidebar: cssref
---

The **`::view-transition`** [CSS](/en-US/docs/Web/CSS) [pseudo-element](/en-US/docs/Web/CSS/Pseudo-elements) represents the root of the [view transitions](/en-US/docs/Web/API/View_Transition_API) overlay, which contains all view transition snapshot groups and sits over the top of all other page content.

During a view transition, `::view-transition` is included in the associated pseudo-element tree as explained in [The view transition pseudo-element tree](/en-US/docs/Web/API/View_Transition_API/Using#the_view_transition_pseudo-element_tree). It is the top-level node of this tree, and has one or more {{cssxref("::view-transition-group()")}}s as children.

`::view-transition` is given the following default styling in the UA stylesheet:

```css
:root::view-transition {
  position: fixed;
  inset: 0;
}
```

All {{cssxref("::view-transition-group()")}} pseudo-elements are positioned relative to the view transition root.

## Syntax

```css
::view-transition {
  /* ... */
}
```

## Examples

```css
::view-transition {
  background-color: rgb(0 0 0 / 25%);
}
```

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- [View Transition API](/en-US/docs/Web/API/View_Transition_API)
- [Smooth transitions with the View Transition API](https://developer.chrome.com/docs/web-platform/view-transitions/)
