---
title: "ValidityState: typeMismatch property"
short-title: typeMismatch
slug: Web/API/ValidityState/typeMismatch
page-type: web-api-instance-property
browser-compat: api.ValidityState.typeMismatch
---

{{APIRef("HTML DOM")}}

The read-only **`typeMismatch`** property of the [`ValidityState`](/en-US/docs/Web/API/ValidityState) interface indicates if the value of an {{HTMLElement("input")}}, after having been edited by the user, does not conform to the constraints set by the element's [`type`](/en-US/docs/Web/HTML/Reference/Elements/input#input_types) attribute.

If the `type` attribute expects specific strings, such as the {{HTMLElement("input/email", "email")}} and {{HTMLElement("input/url", "url")}} types and the value doesn't conform to the constraints set by the type, the `typeMismatch` property will be true.

The {{HTMLElement("input/email", "email")}} input type expects one or more valid email addresses, depending on whether the [`multiple`](/en-US/docs/Web/HTML/Reference/Attributes/multiple) attribute is present. A valid email address includes an email prefix and a domain, with or without a top level domain. If the value of the email input is not an empty string, a single valid email address, or one or more comma separated email address if the [`multiple`](/en-US/docs/Web/HTML/Reference/Attributes/multiple) attribute is present, there is a `typeMismatch`.

The {{HTMLElement("input/url", "url")}} input type expects one or more valid URLs, depending on whether the [`multiple`](/en-US/docs/Web/HTML/Reference/Attributes/multiple) attribute is present. A valid URL includes a protocol, optionally with an IP address, or an optional subdomain, domain, and top level domain combination. If the value of the URL input is not an empty string, a single valid URL, or one or more comma separated URLS if the [`multiple`](/en-US/docs/Web/HTML/Reference/Attributes/multiple) attribute is present, there is a `typeMismatch`.

| Input type                              | Value             | Expected value                                                 |
| --------------------------------------- | ----------------- | -------------------------------------------------------------- |
| {{HTMLElement("input/email", "email")}} | `x@y` or `x@y.z`  | email address, with or without [TLD](/en-US/docs/Glossary/TLD) |
| {{HTMLElement("input/url", "url")}}     | `x:` or `x://y.z` | protocol or full URL with protocol                             |

## Value

A boolean that is `true` if the `ValidityState` does not conform to the constraints.

## Examples

### Type mismatch on input element

The `typeMismatch` occurs when there is a disconnect between the [`value`](/en-US/docs/Web/HTML/Reference/Elements/input#value) expected via the [`type`](/en-US/docs/Web/HTML/Reference/Elements/input#input_types) attribute and the data that is actually present.
The `typeMismatch` is only one of the many possible errors and is only relevant for the {{HTMLElement("input/email", "email")}} and {{HTMLElement("input/url", "url")}} types.
When the value provided doesn't match the expected value based on the type for other input types, you get different errors.
For example, if the {{HTMLElement("input/number", "number")}} input value is not a floating point number, the `badInput` is `true`.
If the email is [`required`](/en-US/docs/Web/HTML/Reference/Attributes/required) but is empty, the {{domxref('ValidityState.valueMissing','valueMissing')}} will be `true`.

```html
<pre id="log">Validation logged here...</pre>
<p>
  <label>
    Enter an email address:
    <input id="emailInput" type="email" value="example.com" required />
  </label>
</p>
```

```css
input:invalid {
  border: red solid 3px;
}
```

```css hidden
body {
  margin: 0.5rem;
}
pre {
  padding: 1rem;
  height: 2rem;
  background-color: lightgrey;
  outline: 1px solid grey;
}
```

```js
const emailInput = document.getElementById("emailInput");
const logElement = document.getElementById("log");

function log(text) {
  logElement.innerText = text;
}

emailInput.addEventListener("input", () => {
  emailInput.reportValidity();
  if (emailInput.validity.valid) {
    log("Input OK…");
  } else if (emailInput.validity.typeMismatch) {
    log("Input is not an email.");
  } else {
    log(`Validation failed: ${emailInput.validationMessage}`);
  }
});
```

{{EmbedLiveSample("Examples", "100%", "160")}}

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- ValidityState [badInput](/en-US/docs/Web/API/ValidityState/badInput), [valid](/en-US/docs/Web/API/ValidityState/valid), [customError](/en-US/docs/Web/API/ValidityState/customError) properties.
- [Constraint validation](/en-US/docs/Web/HTML/Guides/Constraint_validation)
- [Forms: Data form validation](/en-US/docs/Learn_web_development/Extensions/Forms/Form_validation)
- [Regular Expressions](/en-US/docs/Web/JavaScript/Guide/Regular_expressions)
