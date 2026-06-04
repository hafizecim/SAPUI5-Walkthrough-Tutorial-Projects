# SAPUI5 Walkthrough Learning Project

## Overview

This repository contains my implementation of the official SAPUI5/OpenUI5 Walkthrough tutorial.

Unlike creating a separate project for each tutorial step, this repository follows a progressive approach where a single application is continuously enhanced throughout all tutorial stages.

Each completed step is committed to GitHub, making it possible to track the evolution of the application from a simple "Hello World" page to a complete SAPUI5 application.

---

## Project Structure

```text
SAPUI5_TUTORIALS
│
├── package.json
├── package-lock.json
├── ui5.yaml
├── README.md
│
└── webapp
    ├── index.html
    ├── manifest.json
    └── ...
```

---

## Step 1 – Hello World

### Folder Structure

```text
1. Create main folder:
   SAPUI5_TUTORIALS

2. Inside SAPUI5_TUTORIALS create:
   webapp

3. Inside webapp create:
   index.html
   manifest.json

4. Inside SAPUI5_TUTORIALS create:
   package.json
```

---

### Create webapp/index.html

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>UI5 TypeScript Walkthrough</title>
</head>
<body>
    <div>Hello World</div>
</body>
</html>
```

---

### Create webapp/manifest.json

```json
{
    "_version": "1.60.0",
    "sap.app": {
        "id": "ui5.walkthrough",
        "type": "application",
        "title": "OpenUI5 TypeScript Walkthrough",
        "applicationVersion": {
            "version": "1.0.0"
        }
    }
}
```

---

### Create package.json

```json
{
    "name": "ui5.walkthrough",
    "version": "1.0.0",
    "description": "OpenUI5 TypeScript Walkthrough",
    "private": true,
    "scripts": {
        "start": "ui5 serve -o index.html"
    }
}
```

---

## Installation

Open a terminal in the project root directory:

```bash
cd C:\sapui5\SAPUI5_TUTORIALS
```

Install UI5 CLI:

```bash
npm install --save-dev @ui5/cli
```

Initialize UI5 configuration:

```bash
ui5 init
```

Start the development server:

```bash
npm start
```

---

## Tutorial Progress

* [x] Step 1: Hello World
* [ ] Step 2: Bootstrap
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

---

## Learning Strategy

This repository uses a single project that grows throughout the tutorial series.

Each tutorial step builds upon the previous step, following the same development approach used in real SAPUI5 enterprise applications.

Every milestone is committed to GitHub, allowing the complete learning journey to be tracked through commit history.
