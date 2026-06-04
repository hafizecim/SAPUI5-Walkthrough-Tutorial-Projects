
# 📘 SAPUI5 Walkthrough Tutorial – Step 2 (Bootstrap)

## 📌 Overview

<img width="928" height="228" alt="image" src="https://github.com/user-attachments/assets/3245cdef-26f5-4c97-84f0-278091bc661d" />


This step is part of the **Step 2** section of the OpenUI5 Walkthrough tutorial series.

The goal of this step is:

* Use OpenUI5 framework with UI5 CLI
* Add TypeScript support
* Set up UI5 middleware
* Create a basic bootstrap structure
* Run an `alert` when the application loads

---

## 🚀 Run

```bash
npm install
npm start
```

---

## 📁 Project Structure

```text
SAPUI5_TUTORIALS/
│
├── webapp/
│   ├── index.html
│   ├── index.ts
│
├── package.json
├── tsconfig.json
├── ui5.yaml
```

---

## ⚙️ 1. UI5 CLI Setup

```bash
ui5 use OpenUI5
ui5 add sap.ui.core themelib_sap_horizon
```

This step:

* Activates the OpenUI5 framework
* Adds the Horizon theme to the project

---

## ⚙️ 2. TypeScript Setup

```bash
npm install typescript --save-dev
```

TypeScript is added as a development dependency.

---

## ⚙️ 3. UI5 Middleware Setup

```bash
npm install ui5-middleware-livereload ui5-middleware-serveframework ui5-tooling-transpile --save-dev
```

These packages:

* 🔄 Provide live reload
* 🌐 Serve the OpenUI5 framework
* ⚙️ Transpile TypeScript → JavaScript

---

## 🧠 tsconfig.json

```json
{
  "compilerOptions": {
    "target": "es2023",
    "types": ["node", "@types/openui5"],
    "skipLibCheck": true,
    "allowJs": true,
    "strictPropertyInitialization": false,
    "rootDir": "./webapp",
    "paths": {
      "ui5/walkthrough/*": ["./webapp/*"]
    }
  },
  "include": ["./webapp/**/*"]
}
```

### Explanations:

* `target`: Generates ES2023 JavaScript output
* `types`: Node.js type support
* `rootDir`: Source folder
* `include`: Files to be compiled

---

## 🌐 index.html (Bootstrap)

```html
<script
  id="sap-ui-bootstrap"
  src="resources/sap-ui-core.js"
  data-sap-ui-theme="sap_horizon"
  data-sap-ui-compat-version="edge"
  data-sap-ui-async="true"
  data-sap-ui-on-init="module:ui5/walkthrough/index"
  data-sap-ui-resource-roots='{
    "ui5.walkthrough": "./"
  }'>
</script>
```

---

## ⚡ index.ts

```ts
alert("UI5 is ready");
```

---

## 🧩 ui5.yaml

```yaml
specVersion: "4.0"

metadata:
  name: ui5.walkthrough

type: application

framework:
  name: OpenUI5
  version: "1.148.0"
  libraries:
    - name: sap.ui.core
    - name: themelib_sap_horizon

builder:
  customTasks:
    - name: ui5-tooling-transpile-task
      afterTask: replaceVersion

server:
  customMiddleware:
    - name: ui5-tooling-transpile-middleware
      afterMiddleware: compression
    - name: ui5-middleware-serveframework
      afterMiddleware: compression
    - name: ui5-middleware-livereload
      afterMiddleware: compression
```

---

## 🎯 Result

When the application runs:

* UI5 framework is loaded
* TypeScript is transpiled
* Browser opens automatically
* The following appears:

```text
alert: UI5 is ready
```

---

## 🧭 What You Learned

* UI5 CLI usage
* OpenUI5 framework integration
* TypeScript setup
* Middleware architecture
* Bootstrap concept

---

## Learning Progress

* [ ] Step 1: Hello World
* [x] Step 2: Bootstrap
* [ ] Step 3: Controls
* [ ] Step 4: XML Views
* [ ] Step 5: Controllers
* [ ] Step 6: Modules
* [ ] Step 7: JSON Model
* [ ] Step 8: Translatable Texts
* [ ] Step 9: Component Configuration
* [ ] Step 10: Descriptor for Applications
* [ ] Step 11: Pages and Panels
* [ ] Step 12: Shell Control as Container
* [ ] Step 13: Margins and Paddings
* [ ] Step 14: Custom CSS and Theme Colors
* [ ] Step 15: Nested Views
* [ ] Step 16: Dialogs and Fragments
* [ ] Step 17: Fragment Callbacks
* [ ] Step 18: Icons
* [ ] Step 19: Aggregation Binding
* [ ] Step 20: Data Types
* [ ] Step 21: Expression Binding
* [ ] Step 22: Custom Formatters
* [ ] Step 23: Filtering
* [ ] Step 24: Sorting and Grouping
* [ ] Step 25: Remote OData Service
* [ ] Step 26: Mock Server Configuration
* [ ] Step 27: Unit Test with QUnit
* [ ] Step 28: Integration Test with OPA
* [ ] Step 29: Debugging Tools
* [ ] Step 30: Routing and Navigation
* [ ] Step 31: Routing with Parameters
* [ ] Step 32: Routing Back and History
* [ ] Step 33: Custom Controls
* [ ] Step 34: Responsiveness
* [ ] Step 35: Device Adaptation
* [ ] Step 36: Content Density
* [ ] Step 37: Accessibility
* [ ] Step 38: Build Your Application
