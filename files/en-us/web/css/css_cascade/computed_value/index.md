---
title: Computed value
slug: Web/CSS/CSS_cascade/computed_value
page-type: guide
spec-urls:
  - https://www.w3.org/TR/CSS22/cascade.html#computed-value
  - https://drafts.csswg.org/css-cascade-5/#computed-value
---

{{CSSRef}}

The **computed value** of a [CSS](/en-US/docs/Web/CSS) property is the value that is transferred from parent to child during inheritance. It is calculated from the [specified value](/en-US/docs/Web/CSS/CSS_cascade/Value_processing#specified_value) by:

1. Handling the special values {{cssxref("inherit")}}, {{cssxref("initial")}}, {{cssxref("revert")}}, {{cssxref("revert-layer")}}, and {{cssxref("unset")}}.
2. Doing the computation needed to reach the value described in the "Computed value" line in the property's definition table.

The computation needed to reach a property's computed value typically involves converting relative values (such as those in `em` units or percentages) to absolute values. For example, if an element has specified values `font-size: 16px` and `padding-top: 2em`, then the computed value of `padding-top` is `32px` (double the font size).

However, for some properties (those where percentages are relative to something that may require layout to determine, such as `width`, `margin-right`, `text-indent`, and `top`), percentage-specified values turn into percentage-computed values. Additionally, unitless numbers specified on the `line-height` property become the computed value, as specified. The relative values that remain in the computed value become absolute when the [used value](/en-US/docs/Web/CSS/CSS_cascade/Value_processing#used_value) is determined.

> [!NOTE]
> The {{domxref("Window.getComputedStyle", "getComputedStyle()")}} DOM API returns the [resolved value](/en-US/docs/Web/CSS/resolved_value), which may either be the computed value or the [used value](/en-US/docs/Web/CSS/CSS_cascade/Value_processing#used_value), depending on the property.

## Specifications

{{Specifications}}

## See also

- {{domxref("window.getComputedStyle")}}
- CSS key concepts:
  - [CSS syntax](/en-US/docs/Web/CSS/CSS_syntax/Syntax)
  - [At-rules](/en-US/docs/Web/CSS/CSS_syntax/At-rule)
  - [Comments](/en-US/docs/Web/CSS/CSS_syntax/Comments)
  - [Specificity](/en-US/docs/Web/CSS/CSS_cascade/Specificity)
  - [Inheritance](/en-US/docs/Web/CSS/CSS_cascade/Inheritance)
  - [Box model](/en-US/docs/Web/CSS/CSS_box_model/Introduction_to_the_CSS_box_model)
  - [Layout modes](/en-US/docs/Glossary/Layout_mode)
  - [Visual formatting model](/en-US/docs/Web/CSS/CSS_display/Visual_formatting_model)
  - [Margin collapsing](/en-US/docs/Web/CSS/CSS_box_model/Mastering_margin_collapsing)
  - Values
    - [Initial values](/en-US/docs/Web/CSS/CSS_cascade/Value_processing#initial_value)
    - [Used values](/en-US/docs/Web/CSS/CSS_cascade/Value_processing#used_value)
    - [Resolved values](/en-US/docs/Web/CSS/resolved_value)
    - [Actual values](/en-US/docs/Web/CSS/CSS_cascade/Value_processing#actual_value)
  - [Value definition syntax](/en-US/docs/Web/CSS/CSS_Values_and_Units/Value_definition_syntax)
  - [Shorthand properties](/en-US/docs/Web/CSS/CSS_cascade/Shorthand_properties)
  - {{glossary("Replaced elements")}}
