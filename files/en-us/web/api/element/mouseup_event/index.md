---
title: "Element: mouseup event"
short-title: mouseup
slug: Web/API/Element/mouseup_event
page-type: web-api-event
browser-compat: api.Element.mouseup_event
---

{{APIRef}}

The **`mouseup`** event is fired at an {{domxref("Element")}} when a button on a pointing device (such as a mouse or trackpad) is released while the pointer is located inside it.

`mouseup` events are the counterpoint to {{domxref("Element.mousedown_event", "mousedown")}} events.

This behavior is different from {{domxref("Element/pointerup_event", "pointerup")}} events. When using a physical mouse, `mouseup` events fire whenever any button on a mouse is released. `pointerup` events fire only upon the last button release; previous button releases, while other buttons are held down, don't fire `pointerup` events.

## Syntax

Use the event name in methods like {{domxref("EventTarget.addEventListener", "addEventListener()")}}, or set an event handler property.

```js-nolint
addEventListener("mouseup", (event) => { })

onmouseup = (event) => { }
```

## Event type

A {{domxref("MouseEvent")}}. Inherits from {{domxref("UIEvent")}} and {{domxref("Event")}}.

{{InheritanceDiagram("MouseEvent")}}

## Event properties

_This interface also inherits properties of its parents, {{domxref("UIEvent")}} and {{domxref("Event")}}._

- {{domxref("MouseEvent.altKey")}} {{ReadOnlyInline}}
  - : Returns `true` if the <kbd>alt</kbd> key was down when the mouse event was fired.
- {{domxref("MouseEvent.button")}} {{ReadOnlyInline}}
  - : The button number that was pressed (if applicable) when the mouse event was fired.
- {{domxref("MouseEvent.buttons")}} {{ReadOnlyInline}}
  - : The buttons being pressed (if any) when the mouse event was fired.
- {{domxref("MouseEvent.clientX")}} {{ReadOnlyInline}}
  - : The X coordinate of the mouse pointer in [viewport coordinates](/en-US/docs/Web/CSS/CSSOM_view/Coordinate_systems#viewport).
- {{domxref("MouseEvent.clientY")}} {{ReadOnlyInline}}
  - : The Y coordinate of the mouse pointer in [viewport coordinates](/en-US/docs/Web/CSS/CSSOM_view/Coordinate_systems#viewport).
- {{domxref("MouseEvent.ctrlKey")}} {{ReadOnlyInline}}
  - : Returns `true` if the <kbd>control</kbd> key was down when the mouse event was fired.
- {{domxref("MouseEvent.layerX")}} {{Non-standard_inline}} {{ReadOnlyInline}}
  - : Returns the horizontal coordinate of the event relative to the current layer.
- {{domxref("MouseEvent.layerY")}} {{Non-standard_inline}} {{ReadOnlyInline}}
  - : Returns the vertical coordinate of the event relative to the current layer.
- {{domxref("MouseEvent.metaKey")}} {{ReadOnlyInline}}
  - : Returns `true` if the <kbd>meta</kbd> key was down when the mouse event was fired.
- {{domxref("MouseEvent.movementX")}} {{ReadOnlyInline}}
  - : The X coordinate of the mouse pointer relative to the position of the last {{domxref("Element/mousemove_event", "mousemove")}} event.
- {{domxref("MouseEvent.movementY")}} {{ReadOnlyInline}}
  - : The Y coordinate of the mouse pointer relative to the position of the last {{domxref("Element/mousemove_event", "mousemove")}} event.
- {{domxref("MouseEvent.offsetX")}} {{ReadOnlyInline}}
  - : The X coordinate of the mouse pointer relative to the position of the padding edge of the target node.
- {{domxref("MouseEvent.offsetY")}} {{ReadOnlyInline}}
  - : The Y coordinate of the mouse pointer relative to the position of the padding edge of the target node.
- {{domxref("MouseEvent.pageX")}} {{ReadOnlyInline}}
  - : The X coordinate of the mouse pointer relative to the whole document.
- {{domxref("MouseEvent.pageY")}} {{ReadOnlyInline}}
  - : The Y coordinate of the mouse pointer relative to the whole document.
- {{domxref("MouseEvent.relatedTarget")}} {{ReadOnlyInline}}
  - : The secondary target for the event, if there is one.
- {{domxref("MouseEvent.screenX")}} {{ReadOnlyInline}}
  - : The X coordinate of the mouse pointer in [screen coordinates](/en-US/docs/Web/CSS/CSSOM_view/Coordinate_systems#screen).
- {{domxref("MouseEvent.screenY")}} {{ReadOnlyInline}}
  - : The Y coordinate of the mouse pointer in [screen coordinates](/en-US/docs/Web/CSS/CSSOM_view/Coordinate_systems#screen).
- {{domxref("MouseEvent.shiftKey")}} {{ReadOnlyInline}}
  - : Returns `true` if the <kbd>shift</kbd> key was down when the mouse event was fired.
- {{domxref("MouseEvent.mozInputSource")}} {{non-standard_inline()}} {{ReadOnlyInline}}
  - : The type of device that generated the event (one of the `MOZ_SOURCE_*` constants).
    This lets you, for example, determine whether a mouse event was generated by an actual mouse or by a touch event (which might affect the degree of accuracy with which you interpret the coordinates associated with the event).
- {{domxref("MouseEvent.webkitForce")}} {{non-standard_inline()}} {{ReadOnlyInline}}
  - : The amount of pressure applied when clicking.
- {{domxref("MouseEvent.x")}} {{ReadOnlyInline}}
  - : Alias for {{domxref("MouseEvent.clientX")}}.
- {{domxref("MouseEvent.y")}} {{ReadOnlyInline}}
  - : Alias for {{domxref("MouseEvent.clientY")}}.

## Examples

See [`mousemove` event](/en-US/docs/Web/API/Element/mousemove_event#examples) for example code.

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- [Learn: Introduction to events](/en-US/docs/Learn_web_development/Core/Scripting/Events)
- {{domxref("Element/mousedown_event", "mousedown")}}
- {{domxref("Element/mousemove_event", "mousemove")}}
- {{domxref("Element/click_event", "click")}}
- {{domxref("Element/dblclick_event", "dblclick")}}
- {{domxref("Element/mouseover_event", "mouseover")}}
- {{domxref("Element/mouseout_event", "mouseout")}}
- {{domxref("Element/mouseenter_event", "mouseenter")}}
- {{domxref("Element/mouseleave_event", "mouseleave")}}
- {{domxref("Element/contextmenu_event", "contextmenu")}}
- {{domxref("Element/pointerup_event", "pointerup")}}
