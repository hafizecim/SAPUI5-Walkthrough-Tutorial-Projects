# SAPUI5 Walkthrough - Adım 17: Fragment Callbacks

https://sapui5.hana.ondemand.com/#/topic/354f98ed2b514ba9960556333428d35e

Bu adımda, bir önceki adımda eklediğimiz **dialog** penceresine kullanıcı etkileşimi ekleyeceğiz.  
Kullanıcı, açılan dialog penceresini kapatabilmek için bir **"OK"** butonuna sahip olacak.

---

## 1. Amaç
- **Dialog** içine bir buton eklemek.
- Butona tıklandığında dialog'u kapatacak **event handler** (olay işleyici) yazmak.
- Buton metinlerini **i18n** dosyasında çok dilliliğe uygun olarak tanımlamak.

---

## 2. Dosya ve Kod Güncellemeleri

### 📂 `webapp/controller/HelloPanel.controller.js`
Dialog kapatma işlemini yönetecek yeni fonksiyon eklenir:  

```javascript
sap.ui.define([
	"sap/ui/core/mvc/Controller",
	"sap/m/MessageToast"
], (Controller, MessageToast) => {
	"use strict";

	return Controller.extend("ui5.walkthrough.controller.HelloPanel", {
		onShowHello() {
			const oBundle = this.getView().getModel("i18n").getResourceBundle();
			const sRecipient = this.getView().getModel().getProperty("/recipient/name");
			const sMsg = oBundle.getText("helloMsg", [sRecipient]);
			MessageToast.show(sMsg);
		},

		async onOpenDialog() {
			this.oDialog ??= await this.loadFragment({
				name: "ui5.walkthrough.view.HelloDialog"
			});
			this.oDialog.open();
		},

		onCloseDialog() {
			this.byId("helloDialog").close();
		}
	});
});
````

📌 **Açıklama:**

* `onCloseDialog()` → `helloDialog` ID’sine sahip dialog'u kapatır.
* `byId("helloDialog")` → Fragment içindeki kontrolü ID ile bulur.

---

### 📂 `webapp/view/HelloDialog.fragment.xml`

Dialog içine **"OK"** butonu eklenir:

```xml
<core:FragmentDefinition
   xmlns="sap.m"
   xmlns:core="sap.ui.core">
   <Dialog
      id="helloDialog"
      title ="Hello {/recipient/name}">
      <beginButton>
         <Button
            text="{i18n>dialogCloseButtonText}"
            press=".onCloseDialog"/>
      </beginButton>
   </Dialog>
</core:FragmentDefinition>
```

📌 **Açıklama:**

* `beginButton` → Butonun dialog’un sol tarafında görünmesini sağlar (LTR dillerde sol, RTL dillerde sağ).
* `press=".onCloseDialog"` → Butona tıklanınca `HelloPanel.controller.js` içindeki `onCloseDialog` çalışır.

---

### 📂 `webapp/i18n/i18n.properties`

Yeni buton metni eklenir:

```properties
# App Descriptor
appTitle=Hello World
appDescription=A simple walkthrough app that explains the most important concepts of SAPUI5

# Hello Panel
showHelloButtonText=Say Hello
helloMsg=Hello {0}
homePageTitle=Walkthrough
helloPanelTitle=Hello World
openDialogButtonText=Say Hello With Dialog
dialogCloseButtonText=Ok
```

📌 **Açıklama:**

* `dialogCloseButtonText` → Dialog üzerindeki kapatma butonunun metni.

---

## 3. Terminal Komutları

Bu adımda özel bir terminal komutu yoktur.
Ancak değişiklikleri görmek için yerel sunucuyu başlatabilirsiniz:

```sh
npm start
```

veya

```sh
ui5 serve
```

---

## 4. Dosya Yapısı

```
C:\sapui5\SAPUI5_TUTORIALS\hello_world\
│
├── webapp\
│   ├── controller\
│   │   ├── App.controller.js
│   │   └── HelloPanel.controller.js   # Güncellendi
│   ├── view\
│   │   ├── App.view.xml
│   │   ├── HelloPanel.view.xml
│   │   └── HelloDialog.fragment.xml   # Güncellendi
│   ├── i18n\
│   │   └── i18n.properties            # Güncellendi
│   ├── manifest.json
│   └── index.html
└── package.json
```

---

## 5. Sonuç

Bu adımda:

* **Dialog** artık bir **OK** butonuna sahip oldu.
* Kullanıcı butona tıklayınca dialog kapanıyor.
* Buton metni **i18n** ile çok dilliliğe uygun hale getirildi.

---
