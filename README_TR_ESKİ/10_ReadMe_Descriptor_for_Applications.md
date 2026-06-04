# SAPUI5 Walkthrough - Step 10: Descriptor for Applications (manifest.json)

https://sapui5.hana.ondemand.com/#/topic/8f93bf2b2b13402e9f035128ce8b495f

Bu adımda, uygulamaya ait **konfigürasyon ayarlarını** `manifest.json` adlı **uygulama tanım dosyasına (descriptor)** taşıyacağız.  
Böylece **uygulama kodu ile konfigürasyon ayarları** birbirinden ayrılmış olacak ve uygulama **daha esnek** hale gelecek.

---

## 1. Amaç

- **Component.js** içinde tanımladığımız kök view (rootView) ve bazı model ayarlarını artık **manifest.json** üzerinden yönetmek.
- SAP Fiori Launchpad gibi ortamlarda uygulamanın **HTML dosyası olmadan** başlatılmasını sağlamak.
- Tüm SAPUI5 ve Fiori uygulamalarında standart olan **uygulama descriptor** yapısını öğrenmek.

---

## 2. Klasör Yapısı

Bu adım sonunda proje yapınız şu şekilde olacak:

```

webapp/
│
├── Component.js
├── manifest.json   <-- Yeni eklenecek dosya
├── index.html
├── i18n/
│   └── i18n.properties
├── view/
│   └── App.view\.xml
├── controller/
│   └── App.controller.js
└── resources/  (UI5 kütüphaneleri)

````

---

## 3. Yapılacak İşlemler

### 3.1 `manifest.json` oluşturma

📂 **webapp** klasörünün içine şu içeriği kaydedin:

```json
{
  "_version": "1.65.0",
  "sap.app": {
    "id": "ui5.walkthrough",
    "i18n": "i18n/i18n.properties",
    "title": "{{appTitle}}",
    "description": "{{appDescription}}",
    "type": "application",
    "applicationVersion": {
      "version": "1.0.0"
    }
  },
  "sap.ui": {
    "technology": "UI5",
    "deviceTypes": {
      "desktop": true,
      "tablet": true,
      "phone": true
    }
  },
  "sap.ui5": {
    "dependencies": {
      "minUI5Version": "1.108.0",
      "libs": {
        "sap.ui.core": {},
        "sap.m": {}
      }
    },
    "models": {
      "i18n": {
        "type": "sap.ui.model.resource.ResourceModel",
        "settings": {
          "bundleName": "ui5.walkthrough.i18n.i18n",
          "supportedLocales": [""],
          "fallbackLocale": ""
        }
      }
    },
    "rootView": {
      "viewName": "ui5.walkthrough.view.App",
      "type": "XML",
      "id": "app"
    }
  }
}
````

---

### 3.2 `Component.js` güncelleme

📂 **webapp/Component.js** dosyasını şu hale getirin:

```javascript
sap.ui.define([
   "sap/ui/core/UIComponent",
   "sap/ui/model/json/JSONModel"
], (UIComponent, JSONModel) => {
   "use strict";

   return UIComponent.extend("ui5.walkthrough.Component", {
      metadata : {
         interfaces: ["sap.ui.core.IAsyncContentCreation"],
         manifest: "json"
      },

      init() {
         // Parent init
         UIComponent.prototype.init.apply(this, arguments);

         // Data Model
         const oData = {
            recipient : {
               name : "World"
            }
         };
         const oModel = new JSONModel(oData);
         this.setModel(oModel);
      }
   });
});
```

> Artık `sap/ui/model/resource/ResourceModel` **import etmiyoruz** çünkü i18n modeli **manifest.json** üzerinden yükleniyor.

---

### 3.3 `index.html` düzenleme

📂 **webapp/index.html** şu şekilde olmalı:

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title>UI5 Walkthrough</title>
	<script
		id="sap-ui-bootstrap"
		src="resources/sap-ui-core.js"
		data-sap-ui-theme="sap_horizon"
		data-sap-ui-compat-version="edge"
		data-sap-ui-async="true"
		data-sap-ui-on-init="module:sap/ui/core/ComponentSupport"
		data-sap-ui-resource-roots='{
			"ui5.walkthrough": "./"
		}'>
	</script>
</head>
<body class="sapUiBody" id="content">
	<div data-sap-ui-component
	     data-name="ui5.walkthrough"
	     data-id="container"
	     data-settings='{"id" : "walkthrough"}'>
	</div>
</body>
</html>
```

> `index.js` dosyasına artık gerek **yok**, silebilirsiniz.

---

### 3.4 `i18n.properties` güncelleme

📂 **webapp/i18n/i18n.properties**

```properties
# App Descriptor
appTitle=Hello World
appDescription=A simple walkthrough app that explains the most important concepts of SAPUI5

# Hello Panel
showHelloButtonText=Say Hello
helloMsg=Hello {0}
```

---

## 4. Terminal Adımları

Bu adımlar sadece dosya oluşturma/güncelleme bittikten sonra **commit & push** için:

```bash
# Proje dizinine gir
cd C:/sapui5/SAPUI5_TUTORIALS/hello_world

# Git deposu başlat (eğer yoksa)
git init

# Gereksiz dosyaları .gitignore ile hariç tut
echo "node_modules/" >> .gitignore
echo "resources/" >> .gitignore

# Dosyaları ekle
git add .

# Commit yap
git commit -m "Step 10: Added manifest.json and updated Component.js"

# GitHub'a gönder (örnek)
git branch -M main
git remote add origin https://github.com/KULLANICI_ADI/REPO_ADI.git
git push -u origin main
```

---

## 5. Özet

* **manifest.json**: Uygulama tanımı ve konfigürasyonu burada.
* **Component.js**: Artık sadece veri modelimizi yükleyen kısım kaldı.
* **index.html**: ComponentSupport ile doğrudan manifest.json üzerinden component başlatma.
* **index.js**: Artık gereksiz, silinebilir.
* **i18n**: Uygulama başlığı ve açıklaması da burada tanımlı.

```
