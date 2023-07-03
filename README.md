# Console Ninja

Console Ninja is a VS Code extension that displays `console.log` output and **runtime errors** directly in your editor from your running browser or node application. It's like your browser dev tools console tab or terminal output from your node app, but instead of having to context switch, values are connected to your code and displayed ergonomically in your editor.

![preview](https://console-ninja.com/images/docs-main.gif)

---

## Table of contents

- [Current status](#current-status)
- [Supported technologies](#supported-technologies)
- [Get started](#get-started)
- Community Edition Features
  - [console.log](#consolelog)
  - [console.trace](#consoletrace)
  - [console.time](#consoletime)
  - [Hover tooltip](#hover-tooltip)
  - [Log viewer](#log-viewer)
  - [Universal node applications](#universal-node-applications)
- [PRO Edition Features](#pro-features)
  - [Watchpoints](#watchpoints)
  - [Logpoints](#logpoints)
  - [Function logpoints](#function-logpoints)
  - [Class logpoints](#class-logpoints)
  - [Hover tooltip Pro](#hover-tooltip-pro)
  - [Log Viewer Pro](#log-viewer-pro)
  - [Filtering Pro](#output-filtering-pro)
  - [Tracepoints](#tracepoints)
  - [Timepoints](#timepoints)
- [Troubleshooting](#troubleshooting)
- [How does it work?](#how-does-it-work)
- [Differences between Console Ninja and other tools](#differences-between-console-ninja-and-other-tools)
  - [Quokka.js](#quokkajs)
  - [Wallaby.js](#wallabyjs)
  - [Error Lens extension](#error-lens-extension)

---

## Current status

Console Ninja is available for everyone to use for free at the moment. It's still very early days for the product, so we would appreciate if you [let us know](https://github.com/wallabyjs/console-ninja/issues) about any issues/bugs that you may find as well as any feature requests that you may have.

We plan to always have a free **Community** edition available with features such as displaying `console.log` output and runtime errors [directly in your editor](#get-started), showing all recorded logs and errors in the [log viewer](#log-viewer), etc. The **PRO** (paid) edition will be introduced at some point in the next few months and will have additional features that are [documented in a separate section](#pro-features). So unless the feature is documented as being available in the **PRO** edition, it will always be available in the **Community** edition for free.

Before we start working on our commercial model, we will be releasing **PRO** features and making them available to everyone for a limited time. This will give you the opportunity to try out the **PRO features for free**. If you do not want to use the free **PRO** features before the paid version becomes available, you can explicitly disable them in the extension settings.

## Supported technologies

Console Ninja currently supports the following tools:

- [Vite](https://vitejs.dev/), including
  - web applications that were generated by Vite CLI such the ones using React, Vue, Preact, Lit, Svelte, Vanilla, TypeScript or JavaScript;
  - web applications configured to use Vite;
  - web applications powered by app frameworks that are [using Vite](https://patak.dev/vite/ecosystem.html), such as [Nuxt](https://nuxtjs.org/) or [SvelteKit](https://kit.svelte.dev/).
- [Webpack](https://webpack.js.org/), including
  - [Create React App](https://create-react-app.dev/) generated applications;
  - [Angular CLI](https://angular.io/cli) and [Angular Nx](https://nx.dev/packages/angular) generated applications;
  - [Gatsby.js](https://www.gatsbyjs.com/);
  - any web applications configured to use Webpack node module.
- [Next.js](https://nextjs.org/), including first class support for client and server side logs.
- [Remix](https://remix.run/), including first class support for client and server side logs (no errors).
- [Nuxt](https://nuxt.com).
- [Astro](https://astro.build), including first class support for client and server side logs (no server side errors).
- [Shopify Hydrogen](https://apps.shopify.com/hydrogen).
- [Qwik](https://qwik.builder.io).
- [Serverless Offline](https://github.com/dherault/serverless-offline).
- [Jest](https://jestjs.io/) test runner (no errors).
- [Cypress.io](https://www.cypress.io/) end-to-end test runner.
- [http-server](https://www.npmjs.com/package/http-server), [live-server](https://www.npmjs.com/package/live-server) and [serve](https://www.npmjs.com/package/serve) static HTTP servers.
- [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) VS Code extension (`off` by default, can be turned on in the Console Ninja extension VS Code settings).
- [Live Preview](https://marketplace.visualstudio.com/items?itemName=ms-vscode.live-server) VS Code extension (`off` by default, can be turned on in the Console Ninja extension VS Code settings).

In addition to the technologies above, Console Ninja also supports `node app.js`-like workflows including Express, Hapi, Fastify and other similar frameworks. Custom node applications are also supported. To learn more, please refer to the [Universal Node applications](#universal-node-applications) section.

We have designed Console Ninja in such a way that adding support for new tools is fast and easy, so please [let us know](https://github.com/wallabyjs/console-ninja/issues) if there's another technology you want to use Console Ninja with.

## Get started

Console Ninja is designed to fit seamlessly into most typical dev workflows. After you have installed the extension in VS Code and opened your project, you may perform the same steps you usually take:

- run `npm/pnpm/yarn` script or CLI command that starts/opens your app in dev/watch/hot-reload mode **\***;
- start making code changes, such as adding `console.log` to your code **\*\***;
- if required **\*\*\***, perform the actions within your app that trigger the modified code, ie. click a button if you have added `console.log` to the button click handler;

**\*** _If your app is a custom nodejs application then you need to prefix your CLI command with `console-ninja`, please refer to [Universal Node applications](#universal-node-applications) for more information._

**\*\*** _Most modern tools run in watch mode with hot reload enabled. If your tool doesn't have such mode, then, the same way as without Console Ninja, you need to refresh your app page to make it run your modified code._

**\*\*\*** _Sometimes your modified code may be triggered immediately upon the (hot) reload of the app. For example, when code is located in the root of a component, it will be executed when the app (re)starts. If the modified code is not triggered by the app (re)start, then, the same way as without Console Ninja, you will need to perform your app specific actions to trigger the code execution._

![overview](https://console-ninja.com/images/docs-overview.png)

You should now be able to see logs (and errors, if any) in your editor, next to the relevant line of code. Hovering over the `console.log` or **error** value will display more details. **If you don't see the expected output, please [check Console Ninja's current status](#troubleshooting)**.

Using the `Show Output` command displays the log viewer, allowing you to explore more details and navigate between logs and code.

### console.log

Adding `console.log` to your code will display the log output in your editor, next to the relevant line of code. Hovering over the `console.log` value will display additional details. The log output is also displayed in the [log viewer](#log-viewer).

### console.trace

Adding [`console.trace`](https://developer.mozilla.org/en-US/docs/Web/API/console/trace) to your code will display the **call stack trace** right in your editor, next to the line of code with `console.trace`. The stack trace output is also displayed in the [log viewer](#log-viewer).

![tracepoints](https://console-ninja.com/images/docs-consoleTrace.png)

### console.time

Adding [`console.time('some_label')` and `console.timeEnd('some_label')`](https://developer.mozilla.org/en-US/docs/Web/API/console/time) to your code will display the time it took to execute the code between the calls right in your editor, next to the line of code with `console.timeEnd`. The time output is also displayed in the [log viewer](#log-viewer).

![timepoints](https://console-ninja.com/images/docs-consoleTime.png)

### Hover tooltip

Hovering over Console Ninja output, such as logs or errors, will display more details, such as the log value, error message, and stack trace.

![hover](https://console-ninja.com/images/docs-hover.png)

The hover tooltip also provides a few actions displayed as icons in the top right corner of the widget, for example:

- `Show in Console Output` action that opens Console Ninja's [log viewer](#log-viewer) and focuses on the log entry.
- `Open Filtering Settings` action that opens Console Ninja's output filtering settings.

### Log viewer

Using the `Show Output` command displays Console Ninja's log viewer. The log viewer shows all recorded logs and errors from your running application in chronological order, with newer entries at the bottom. When the command is triggered on a line with a `console.log` result, the last recorded log entry is focused in the log viewer.

Each log entry provides summary details and is collapsed by default, providing a short preview that can be expanded (via mouse or `Arrow Right` keyboard key after it is focused) to inspect its details. Once the details are expanded, the `Enter` keyboard key can be used to enter the details keyboard selection/navigation mode; the `Esc` key can be used to exit the mode.

Each entry preview and expanded error entry details contain clickable links to the target source code. Links that point to `http` locations are opened in the editor by downloading the file first (a setting allows `http` links to be opened in the browser instead).

Similar to browser dev tools, sequential entries of a primitive type, such as `string`, `boolean` and `number`, and any errors, that are logged from the same place in the code and have the same value are grouped together and displayed as a single entry. The entry prefix indicates the number of entires in the group.

The following keyboard shortcuts are supported for faster navigation:

- `Arrow Up` and `Arrow Down` to navigate to the next/previous displayed entry.
- `Home` and `End` to navigate to the first/last displayed entry.
- `Arrow Left` to collapse focused entry details and `Ctrl/Cmd + Arrow Left` to collapse all expanded entries details.

Additionally, the following commands (also displayed as icon buttons at the top of the log viewer) are available:

- `Clear all output` from Console Ninja, including inline output.
- `Toggle log entry date/time display` to show/hide date/time part of each dispalyed log entry.
- `Toggle auto-clearing of the output on any file change`. If auto-clearing is set to `off`, log entries recorded prior to the latest file change are dimmed, and the file links hover icon is changed to indicate that the displayed position may have changed since the entry was recorded.
- `Toggle auto-scrolling to the last log entry` when new log entries are added. If the output is manually scrolled up so that the last entry row is not visible, then auto-scrolling is paused until the output is manually scrolled to make the last entry row visible.

The log viewer supports search using the `Ctrl/Cmd + F` keyboard shortcut.

The log viewer can be displayed in two modes, either `Beside File` and `In View`, there is a setting to configure the mode.

![status](https://console-ninja.com/images/docs-view.gif)

In the `Beside File` mode (default, and recommended), the viewer is displayed in a new separate editor group to the left from your current editor. In this case, the view behaves like other opened editor tabs, i.e. it is visible in the `Opened Editors` in VS Code file explorer view.

In the `In View` mode, the viewer is displayed as VS Code side view. The view can also be moved to another VS Code panel. The recommended position for the viewer is to the right of the VS Code `Output` view in the bottom pane of your editor.

### Universal Node applications

Console Ninja supports virtually any node application (starting from node v16.15.0), including Express, Hapi, Fastify, and custom node applications. Simply prefix your `node app.js` command with `console-ninja` and run `console-ninja node app.js` in your terminal.

![shell scripts](https://console-ninja.com/images/docs-shellScripts.png)

Here are some more examples of how you may use the command:

- `console-ninja node --watch app.js`
- `console-ninja npx nodemon app.js`
- `console-ninja npm run dev`
- `console-ninja yarn node app.js`
- `console-ninja npx tsx app.ts`
- `console-ninja npx ts-node app.ts`

If `console-ninja` is not available in an external terminal session after executing `Console Ninja: Start` command and reloading your terminal session then you may need to add `~/.console-ninja/.bin` to `PATH` manually. On Windows, depending on how you start apps, you may need to restart Explorer process or re-login to the system.

On UNIX-based systems (e.g. MacOS, Linux) you may [source](https://ss64.com/bash/source.html) the `console-ninja` command for a terminal session. After that point, any commands you run in that terminal session will automatically be started with `console-ninja`. For example:

- `source console-ninja`
- `node app1.js`
- `node app2.js`

_Please note: if your project uses a tool that Console Ninja [supports](#supported-technologies) out of the box then you don't need to prefix your CLI commands with `console-ninja` the prefix._

## Troubleshooting

If Console Ninja is not working for you as expected, the first thing to check is the extension status. You may see the status info by hovering over the extension icon in VS Code status bar.

![status](https://console-ninja.com/images/docs-status.gif?v=1)

The status popup information dialog explains the current state of the tool and provides some tips on what to do next.

## How does it work

Console Ninja integrates with locally installed tools that are building/preparing your code, and then inspects and adjusts your code (in a way that doesn't change how it executes) before it gets to the runtime (browser or node process that runs the code).

To integrate with supported tools seamlessly, Console Ninja patches your locally installed node modules. When you stop Console Ninja in the editor with the `Pause` command, all patches are removed.

Console Ninja detects if you are running your tool in production mode (by checking CLI flags and process environment variables). When production mode is detected, the tool will not modify your application code even if Console Ninja is running. In the (unlikely) case that you are running production builds on your local dev computer and are deploying or sharing local builds outside of your machine, we recommend running the Console Ninja `Pause` command in your editor prior to running your build to guarantee that no instrumented code ends up in your production code.

Console Ninja instrumentation is limited to sending runtime values for `console.log` and errors to your locally running editor only (`localhost` hosted websocket server). The runtime data from your app is **never** sent outside of your local machine. If the code of your application is somehow instrumented by Console Ninja and then used outside of your local machine for some reason:

- in browser, it will simply do nothing if the app host is not `127.0.0.1`, `localhost`, or one of your network adapter's IP v4 addresses. To connect from a different host name, use the `console-ninja.allowedHosts` VS Code setting.
- in node, it will fail to connect to `localhost` and will not stop your app from working.

## Differences between Console Ninja and other tools

### Quokka.js

[Quokka.js](https://quokkajs.com/) is another awesome tool from [our team](https://wallabyjs.com/). Like Console Ninja, Quokka.js allows you to see various execution results without leaving the comfort of your editor.

The fundamental difference between Console Ninja and Quokka.js is that Quokka runs new scratch files or existing code files as a self-contained program. Quokka allows you to quickly execute and iterate code in an **isolated playground** without unnecessary application execution. Console Ninja on the other hand runs within your application (started by your dev server, or test runner), and allows you to debug any **end to end scenarios within your running app**.

### Wallaby.js

The [Wallaby.js](https://wallabyjs.com/) tool from our team runs your JavaScript and TypeScript tests immediately as you type, highlighting results in your IDE right next to your code.

While you may use Console Ninja to display logs from supported test runner CLIs, test errors are not handled by Console Ninja; this is because test errors are caught/handled by test runners themselves, and special processing is required to format and display test results.

Wallaby not only displays logs and test errors inline (and in a separate ergonomically designed view), but is also [packed with features](https://wallabyjs.com/#features), such as inline code coverage and a time travel debugger, that provide superpowers to your current testing framework/stack, such as [Jest, Vitest, Mocha. etc.](https://wallabyjs.com/#tools)

### Error Lens extension

[Error Lens](https://marketplace.visualstudio.com/items?itemName=usernamehw.errorlens) is a VS Code extension that provides inline output for VS Code `Problems` output window, typically **static code analysis errors** from your code linter or language service, such as a linter rule violation or TypeScript types-related error.

In contrast, Console Ninja runs within your application and displays **runtime logs and errors**.

## PRO features

We plan to always have a free **Community** edition available with features such as displaying `console.log` output and runtime errors [directly in your editor](#get-started), showing all recorded logs and errors in the [log viewer](#log-viewer), etc. The **PRO** (paid) edition will be introduced at some point in the next few months and will have additional features that are documented below. So unless the feature is documented as being available in the **PRO** edition, it will always be available in the **Community** edition for free.

Before we start working on our commercial model, we will be releasing **PRO** features and making them available to everyone for a limited time. This will give you the opportunity to try out the **PRO features for free**. If you do not want to use the free **PRO** features before the paid version becomes available, you can explicitly disable them in the extension settings.

### Watchpoints

The `Watch Value` feature allows you to keep the value of any logged expression displayed. While opened, the value can easily be monitored for any changes made to it as a result of your code modifications or some actions in your app.

![watchpoints](https://console-ninja.com/images/docs-watchpoints.gif)

The `Watch Value` feature is available for both `console.log` and [logpoints](#logpoints). The feature is available from the [hover tooltip](#hover-tooltip), as a code action (via the editor line `light-bulb`) and from the editor command pallette.

You can watch multiple values at the same time. Value widgets in the Console Output can be closed individually (close icon or `Ctrl/Cmd + W` keyboard shortcut on a focused value) or all at once. Arrow keys can be used to navigate between displayed values.

`Copy` is available from the focused widget header and via `Ctrl/Cmd + C` shortcut. Search (`Ctrl/Cmd + F`) can be used to find any specific content inside displayed values. The `Enter` key can be used on a focused value widget to enter the details keyboard selection/navigation mode; and the `Esc` key can be used to exit the mode.

![watchpoints-details](https://console-ninja.com/images/docs-watchpoints-details.png)

The Console Output value widgets layout can be changed from `automatic` (default) to `manual` (with drag & drop and resize support) via the `Toggle Value Layout Mode` command (also available as at the top of the watched `Values` view). [Log Highlighting](#log-viewer-pro) is also supported for displayed values via coloring the value widget header with the same highlight color as in the log viewer and editor.

### Logpoints

While using the `console.log` feature provides an excellent way to log expression values, oftentimes you may want to display or capture expression values **without modifying your code**. There are also many times when inserting `console.log` can get tedious, such as:

- when logging an arrow function expression return value or the function parameter value (ie. logging `e` or `e.prop` in `a.map(e => e.prop)`);
- or logging a JSX expression value (ie. logging `count` in `<span>count is {count}</span>`).
- or logging an expression in the middle of another expression (ie. logging the result of `a.b()` in `a.b().c();` without calling `a.b()` twice).

Console Ninja Logpoints allow you to log the value of any expression in your code, **without modifying your code**, by simply placing a VS Code breakpoint in your code. When Console Ninja is running (and the VS Code debugger is not), the breakpoint will not stop your code, but will act as a logpoint and will log the value of the expression next to your code and to the Console Ninja log viewer.

![logpoints](https://console-ninja.com/images/docs-logpoints.gif)

To use the feature, you may simply place a breakpoint (`F9`) on any line. If you want to be more precise about what to log on a line, you may place an **inline breakpoint** (`Shift + F9`) near/inside the expression that you would like to log.

In the example below:

- inline breakpoint on the line 8 outputs the value of the `document`;
- inline breakpoint on the line 23 outputs the value of the `e` parameter of the `onClick` button handler;
- inline breakpoints on the line 24 and line 30 outputs the value of the `count` variable.

![logpoints](https://console-ninja.com/images/docs-logpoints.png)

Once a breakpoint is placed and Console Ninja is ready to output some values for it, a special ⚡️ indicator is placed at the line with the breakpoint. If a breakpoint is placed and there's no special indicator visible, it means that it is placed in a location where Console Ninja cannot find anything to log (for example, on a line without executable JS/TS code).

### Function logpoints

Function logpoints are special types of Console Ninja [logpoints](#logpoints) that allow logging **every line of a function** and it's argument values, **without modifying your code**. Function logpoints are useful when you want to log the execution of a function, but do not want to insert `console.log` statements in the function body or place a logpoint on every line of the function.

![logpoints](https://console-ninja.com/images/docs-funclogpoints.gif)

To use the feature, you may simply place a breakpoint (`F9`) on a line of code where a function/method is defined. If there are multiple expressions or functions defined on a line, you may place an **inline breakpoint** (`Shift + F9`) near/inside the `function` keyword or method name, or at the start of an arrow function expression (`🔴() => ...`).

To override the value logged for a line within the logged function, **inline breakpoint** (`Shift + F9`) may be used near/inside a specific expression within the line.

### Class logpoints

Class logpoints are special types of Console Ninja [logpoints](#logpoints) that allow logging **every line of all functions of a class without modifying your code**.

To use the feature, you may simply place a breakpoint (`F9`) on a line of code where a `class` is defined.

To override the value logged for a line within the logged function, **inline breakpoint** (`Shift + F9`) may be used near/inside a specific expression within the line.

### Hover tooltip Pro

In addition to the [hover tooltip](#hover-tooltip) features available in the **Community** edition, the **PRO** edition includes additional actions:

- `Copy to Clipboard` action that copies the logged value or the error details to the clipboard. It's also available as a code action (via the editor line light-bulb).
- `Search the Web` action that opens a web browser with the error message as a search query. This action is only available for errors. The search engine can be configured in the Console Ninja extension settings via the `console-ninja.searchUrl` setting.

![hover](https://console-ninja.com/images/docs-hover.png)

### Log Viewer Pro

In addition to the [log viewer](#log-viewer) features available in the **Community** edition, the **PRO** edition includes additional features to provide an even more powerful way to analyze complex output.

![logviewerpro](https://console-ninja.com/images/docs-logviewerpro.png)

#### Indentation guides

**Indentation guides** provide a clear visual representation of the nested structure of
your objects.

#### Expand/collapse controls

**Expand/collapse controls** allow you to collapse and expand nodes within nested objects.
These features allow you to focus on specific sections of your logs without being overwhelmed by the
sheer size and complexity of the output.

#### Log entry highlighting

This feature allows you to highlight [log viewer](#log-viewer) entries that are logged from the same place in your code. No need to add prefixes like `console.log('!!! HERE', obj)` to your logs any longer - highlighted entries are decorated with a visually distinct colored & numbered indicator. Highlighting makes it easier to quickly identify specific log entries in scenarios with a lot of logs.

![logviewerpro](https://console-ninja.com/images/docs-highlighting.gif)

Both `console.log` statements and [logpoints](#logpoints) can be highlighted.

`Toggle Log Highlight` command allows you to toggle highlighting of the current log location. The command is available from the editor command pallette, from the log hover tooltip and as a code action (via the editor line light-bulb).

`Clear All Log Highlights` command allows you to clear all current log entry highlights.

#### Log entry grouping

Sequential entries, including logs and errors, that are logged from the same place in the code and have the same logged value are grouped together and displayed as a single entry. The entry prefix indicates the number of entires in the group. While similar Console Ninja Community edition feature only works for primitive types (just like browser dev tools), this Pro feature **works for any type of entries, including large complex objects**.

![logviewerpro](https://console-ninja.com/images/docs-grouping.png)

#### Log entry actions

- `Copy` action allows to copy selected log entry to clipboard. The action is available from the selected log entry toolbar and via `Ctrl/Cmd + C` shortcut.

### Output Filtering Pro

Console Ninja **PRO** edition includes output filtering features to make working in large projects or projects with a lot of output easier.

- `Capture and display errors` setting allows configuring whether to capture and display errors in the editor and in the log viewer. This is useful when you are working on a project with a lot of reported errors and you want to focus on logs only.

- `Capture and display logs only from files opened in editor` setting allows configuring whether to capture and display logs from all files or only the files that are opened in your editor. This is useful when you are working on a project with a lot of files with logs and you want to focus only on output from files that you are currently working on.

- `Display logs from multiple running tools together in a single list` setting allows to merge output from multiple running project tools, such as next.js server and next.js browser logs, Jest logs, etc., and display the output together in the [log viewer](#log-viewer). The merged output provides a holistic view of your running application, eliminating the need to
  switch between multiple output sources. This integrated view of logs from all of your tools
  provides an intuitive and efficient way to understand the complete behavior of your application.

![multitool](https://console-ninja.com/images/tile_multitool.gif)

- `Capture and display logs only from logpoints` setting allows configuring whether to capture and display logs from `console.log` and other `console.*` statements. This is useful when you are working on a project with a lot of `console.log` statements and you want to focus on output from your [logpoints](#logpoints) only.

### Tracepoints

Console Ninja Tracepoints allow you to trace the execution of any block of code and understand where it is being called from, **without modifying your code**. Similar to [logpoints](#logpoints), you may place a tracepoint (`Add Tracepoint` command) on any line/column, even in the middle of some expression, or next to a function parameter. When the code execution reaches the tracepoint, Console Ninja will log the **current stack trace** and the value of the expression located at the tracepoint position.

![tracepoints](https://console-ninja.com/images/docs-tracepoints.gif)

### Timepoints

Console Ninja Timepoints allow you to measure the execution time of any block of code, **without modifying your code**, by simply placing a pair of timepoints in your code.

First, place a timepoint (`Add Timepoint` command) on the line where you want to start measuring the execution time. Then, place another timepoint (`Add Timepoint` command) on the line where you want to stop measuring the execution time. The timepoints will be highlighted by Console Ninja, and the execution time will be displayed next to the end timepoint and in the Console Ninja log viewer.

![timepoints](https://console-ninja.com/images/docs-timepoints.gif)
