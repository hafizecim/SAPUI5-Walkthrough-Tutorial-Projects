# 📘 SAPUI5 Walkthrough Tutorial – Step 2 (Bootstrap)

## 📌 Genel Bakış

<img width="928" height="228" alt="image" src="https://github.com/user-attachments/assets/3245cdef-26f5-4c97-84f0-278091bc661d" />

Bu adım OpenUI5 Walkthrough eğitim serisinin **Step 2** bölümüdür.

Bu aşamada amaç:

* UI5 CLI ile OpenUI5 framework kullanmak
* TypeScript desteği eklemek
* UI5 middleware kurulumunu yapmak
* Basit bir bootstrap yapısı oluşturmak
* Uygulama yüklendiğinde `alert` çalıştırmak

---

## 🚀 Çalıştırma

```bash
npm install
npm start
```

---

## 📁 Proje Yapısı

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

## ⚙️ 1. UI5 CLI Kurulumu

```bash
ui5 use OpenUI5
ui5 add sap.ui.core themelib_sap_horizon
```

Bu adım:

* OpenUI5 framework’ünü aktif eder
* Horizon temasını projeye ekler

---

## ⚙️ 2. TypeScript Kurulumu

```bash
npm install typescript --save-dev
```

TypeScript projeye geliştirme bağımlılığı olarak eklenir.

---

## ⚙️ 3. UI5 Middleware Kurulumu

```bash
npm install ui5-middleware-livereload ui5-middleware-serveframework ui5-tooling-transpile --save-dev
```

Bu paketler:

* 🔄 Live reload sağlar
* 🌐 OpenUI5 framework servis eder
* ⚙️ TypeScript → JavaScript dönüşümü yapar

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

### Açıklamalar:

* `target`: ES2023 JavaScript üretir
* `types`: Node.js tip desteği
* `rootDir`: kaynak klasör
* `include`: derlenecek dosyalar

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

## 🎯 Sonuç

Uygulama çalıştığında:

* UI5 framework yüklenir
* TypeScript transpile edilir
* Tarayıcı otomatik açılır
* Ekranda:

```text
alert: UI5 is ready
```

görülür

---

## 🧭 Öğrenilenler

* UI5 CLI kullanımı
* OpenUI5 framework entegrasyonu
* TypeScript kurulumu
* Middleware yapısı
* Bootstrap mantığı

---

## Eğitim İlerleme Durumu

* [ ] Adım 1: Hello World
* [x] Adım 2: Bootstrap
* [ ] Adım 3: Controls
* [ ] Adım 4: XML Views
* [ ] Adım 5: Controllers
* [ ] Adım 6: Modules
* [ ] Adım 7: JSON Model
* [ ] Adım 8: Translatable Texts
* [ ] Adım 9: Component Configuration
* [ ] Adım 10: Descriptor for Applications
* [ ] Adım 11: Pages and Panels
* [ ] Adım 12: Shell Control as Container
* [ ] Adım 13: Margins and Paddings
* [ ] Adım 14: Custom CSS and Theme Colors
* [ ] Adım 15: Nested Views
* [ ] Adım 16: Dialogs and Fragments
* [ ] Adım 17: Fragment Callbacks
* [ ] Adım 18: Icons
* [ ] Adım 19: Aggregation Binding
* [ ] Adım 20: Data Types
* [ ] Adım 21: Expression Binding
* [ ] Adım 22: Custom Formatters
* [ ] Adım 23: Filtering
* [ ] Adım 24: Sorting and Grouping
* [ ] Adım 25: Remote OData Service
* [ ] Adım 26: Mock Server Configuration
* [ ] Adım 27: Unit Test with QUnit
* [ ] Adım 28: Integration Test with OPA
* [ ] Adım 29: Debugging Tools
* [ ] Adım 30: Routing and Navigation
* [ ] Adım 31: Routing with Parameters
* [ ] Adım 32: Routing Back and History
* [ ] Adım 33: Custom Controls
* [ ] Adım 34: Responsiveness
* [ ] Adım 35: Device Adaptation
* [ ] Adım 36: Content Density
* [ ] Adım 37: Accessibility
* [ ] Adım 38: Build Your Application

---
