---
title: scripting.executeScript()
slug: Mozilla/Add-ons/WebExtensions/API/scripting/executeScript
page-type: webextension-api-function
browser-compat: webextensions.api.scripting.executeScript
sidebar: addonsidebar
---

Injects a script into a target context. The script is run at `document_idle` by default.

> [!NOTE]
> This method is available in Manifest V3 or higher in Chrome and Firefox 101. In Safari and Firefox 102+, this method is also available in Manifest V2.

To use this API you must have the `"scripting"` [permission](/en-US/docs/Mozilla/Add-ons/WebExtensions/manifest.json/permissions) and permission for the target's URL, either explicitly as a [host permission](/en-US/docs/Mozilla/Add-ons/WebExtensions/manifest.json/permissions#host_permissions) or using the [activeTab permission](/en-US/docs/Mozilla/Add-ons/WebExtensions/manifest.json/permissions#activetab_permission). Note that some special pages do not allow this permission, including reader view, view-source, and PDF viewer pages.

In Firefox and Safari, partial lack of host permissions can result in a successful execution (with the partial results in the resolved promise). In Chrome, any missing permission prevents any execution from happening (see [Issue 1325114](https://crbug.com/1325114)).

The scripts you inject are called [content scripts](/en-US/docs/Mozilla/Add-ons/WebExtensions/Content_scripts).

This is an asynchronous function that returns a [`Promise`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise).

## Syntax

```js-nolint
let results = await browser.scripting.executeScript(
  details             // object
)
```

### Parameters

- `details`
  - : An object describing the script to inject. It contains these properties:
    - `args` {{optional_inline}}
      - : An array of arguments to carry into the function. This is only valid if the `func` parameter is specified. The arguments must be JSON-serializable.
    - `files` {{optional_inline}}
      - : `array` of `string`. An array of path of the JS files to inject, relative to the extension's root directory. Exactly one of `files` and `func` must be specified.
    - `func` {{optional_inline}}
      - : `function`. A JavaScript function to inject. This function is serialized and then deserialized for injection. This means that any bound parameters and execution context are lost. Exactly one of `files` and `func` must be specified.
    - `injectImmediately` {{optional_inline}}
      - : `boolean`. Whether the injection into the target is triggered as soon as possible, but not necessarily prior to page load.
    - `target`
      - : {{WebExtAPIRef("scripting.InjectionTarget")}}. Details specifying the target to inject the script into.
    - `world` {{optional_inline}}
      - : {{WebExtAPIRef("scripting.ExecutionWorld")}}. The execution environment for a script to execute in.

### Return value

A [`Promise`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) that fulfills with an array of `InjectionResult` objects, which represent the result of the injected script in every injected frame.

The promise is rejected if the injection fails, such as when the injection target is invalid. When script execution has started, its result is included in the result, whether successful (as `result`) or unsuccessfully (as `error`).

Each `InjectionResult` object has these properties:

- `frameId`
  - : `number`. The frame ID associated with the injection.
- `result` {{optional_inline}}
  - : `any`. The result of the script execution.
- `error` {{optional_inline}}
  - : `any`. If an error occurs, contains the value the script threw or rejected with. Typically this is an error object with a message property but it could be any value (including primitives and undefined).

    Chrome does not support the `error` property yet (see [Issue 1271527: Propagate errors from scripting.executeScript to InjectionResult](https://crbug.com/1271527)). As an alternative, runtime errors can be caught by wrapping the code to execute in a try-catch statement. Uncaught errors are also reported to the console of the target tab.

The result of the script is the last evaluated statement, which is similar to the results seen if you executed the script in the [Web Console](https://firefox-source-docs.mozilla.org/devtools-user/web_console/index.html) (not any `console.log()` output). For example, consider a script like this:

```js
let foo = "my result";
foo;
```

Here the results array contains the string `"my result"` as an element.

The script result must be a [structured cloneable](/en-US/docs/Web/API/Web_Workers_API/Structured_clone_algorithm) value in Firefox or a [JSON-serializable](/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify#description) value in Chrome. The [Chrome incompatibilities](/en-US/docs/Mozilla/Add-ons/WebExtensions/Chrome_incompatibilities) article discusses this difference in more detail in the [Data cloning algorithm](/en-US/docs/Mozilla/Add-ons/WebExtensions/Chrome_incompatibilities#data_cloning_algorithm) section.

## Examples

This example executes a one-line code snippet in the active tab:

```js
browser.action.onClicked.addListener(async (tab) => {
  try {
    await browser.scripting.executeScript({
      target: {
        tabId: tab.id,
      },
      func: () => {
        document.body.style.border = "5px solid green";
      },
    });
  } catch (err) {
    console.error(`failed to execute script: ${err}`);
  }
});
```

This example executes a script from a file (packaged with the extension) called `"content-script.js"`. The script is executed in the active tab. The script is executed in subframes and the main document:

```js
browser.action.onClicked.addListener(async (tab) => {
  try {
    await browser.scripting.executeScript({
      target: {
        tabId: tab.id,
        allFrames: true,
      },
      files: ["content-script.js"],
    });
  } catch (err) {
    console.error(`failed to execute script: ${err}`);
  }
});
```

{{WebExtExamples}}

## Browser compatibility

{{Compat}}

> [!NOTE]
> This API is based on Chromium's [`chrome.scripting`](https://developer.chrome.com/docs/extensions/reference/api/scripting#method-executeScript) API.
