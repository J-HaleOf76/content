---
title: runtime.connect()
slug: Mozilla/Add-ons/WebExtensions/API/runtime/connect
page-type: webextension-api-function
browser-compat: webextensions.api.runtime.connect
sidebar: addonsidebar
---

Make a connection between different contexts inside the extension.

You can call this:

- in an extension's content scripts, to establish a connection with the extension's background scripts (or similarly privileged scripts, like popup scripts or options page scripts).
- in an extension's background scripts (or similarly privileged scripts), to establish a connection with a different extension.

Note that you can't use this function to connect an extension to its content scripts. To do this, use {{WebExtAPIRef('tabs.connect()')}}.

By default, this connection enables the extension to exchange messages with itself or any other extension (if `extensionId` is specified). However, the [`externally_connectable`](/en-US/docs/Mozilla/Add-ons/WebExtensions/manifest.json/externally_connectable) manifest key can be used to limit communication to specific extensions and enable communication with websites. Connections within the extension trigger the {{WebExtAPIRef('runtime.onConnect')}} event, connections from other extensions or web pages trigger the {{WebExtAPIRef('runtime.onConnectExternal')}} event.

## Syntax

```js-nolint
let port = browser.runtime.connect(
  extensionId, // optional string
  connectInfo  // optional object
)
```

### Parameters

- `extensionId` {{optional_inline}}
  - : `string`. The ID of the extension to connect to. If the target has set an ID explicitly using the [browser_specific_settings](/en-US/docs/Mozilla/Add-ons/WebExtensions/manifest.json/browser_specific_settings) key in manifest.json, then `extensionId` should have that value. Otherwise it should have the ID that was generated for the target.
- `connectInfo` {{optional_inline}}
  - : `object`. Details of the connection:
    - `name` {{optional_inline}}
      - : `string`. Will be passed into {{WebExtAPIRef("runtime.onConnect")}} for processes that are listening for the connection event.
    - `includeTlsChannelId` {{optional_inline}}
      - : `boolean`. Whether the TLS channel ID will be passed into {{WebExtAPIRef("runtime.onConnectExternal")}} for processes that are listening for the connection event.

### Return value

{{WebExtAPIRef('runtime.Port')}}. Port through which messages can be sent and received. The port's `onDisconnect` event is fired if the extension does not exist.

## Examples

This content script:

- connects to the background script and stores the `Port` in a variable called `myPort`.
- listens for messages on `myPort` and logs them.
- sends messages to the background script, using `myPort`, when the user clicks the document.

```js
// content-script.js

let myPort = browser.runtime.connect({ name: "port-from-cs" });
myPort.postMessage({ greeting: "hello from content script" });

myPort.onMessage.addListener((m) => {
  console.log("In content script, received message from background script: ");
  console.log(m.greeting);
});

document.body.addEventListener("click", () => {
  myPort.postMessage({ greeting: "they clicked the page!" });
});
```

The corresponding background script:

- listens for connection attempts from the content script.
- when it receives a connection attempt:
  - stores the port in a variable named `portFromCS`.
  - sends the content script a message using the port.
  - starts listening to messages received on the port, and logs them.

- sends messages to the content script, using `portFromCS`, when the user clicks the extension's browser action.

```js
// background-script.js

let portFromCS;

function connected(p) {
  portFromCS = p;
  portFromCS.postMessage({ greeting: "hi there content script!" });
  portFromCS.onMessage.addListener((m) => {
    console.log("In background script, received message from content script");
    console.log(m.greeting);
  });
}

browser.runtime.onConnect.addListener(connected);

browser.browserAction.onClicked.addListener(() => {
  portFromCS.postMessage({ greeting: "they clicked the button!" });
});
```

{{WebExtExamples}}

## Browser compatibility

{{Compat}}

> [!NOTE]
> This API is based on Chromium's [`chrome.runtime`](https://developer.chrome.com/docs/extensions/reference/api/runtime#method-connect) API. This documentation is derived from [`runtime.json`](https://chromium.googlesource.com/chromium/src/+/master/extensions/common/api/runtime.json) in the Chromium code.

<!--
// Copyright 2015 The Chromium Authors. All rights reserved.
//
// Redistribution and use in source and binary forms, with or without
// modification, are permitted provided that the following conditions are
// met:
//
//    * Redistributions of source code must retain the above copyright
// notice, this list of conditions and the following disclaimer.
//    * Redistributions in binary form must reproduce the above
// copyright notice, this list of conditions and the following disclaimer
// in the documentation and/or other materials provided with the
// distribution.
//    * Neither the name of Google Inc. nor the names of its
// contributors may be used to endorse or promote products derived from
// this software without specific prior written permission.
//
// THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
// "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
// LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
// A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
// OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
// SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
// LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
// DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
// THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
// (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
// OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
-->
