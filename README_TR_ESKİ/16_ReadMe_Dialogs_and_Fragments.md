# Step 16: Dialogs and Fragments (Diyaloglar ve Parçacıklar)

https://sapui5.hana.ondemand.com/#/topic/4da72985139b4b83b5f1c1e0c0d2ed5a

Bu adımda **fragment** kavramını öğreniyoruz ve uygulamamıza bir **dialog (açılır pencere)** ekliyoruz.  
Fragment’ler:
- **Hafif** ve **yeniden kullanılabilir** UI parçalarıdır.
- **Controller** içermezler.
- Görünümler (`View`) içine gömülerek kullanılabilirler.
- Birden fazla görünümde tekrar kullanılacak veya koşula göre değiştirilecek UI parçaları için idealdir.

---

## 🎯 Amaç
- Panel içine yeni bir **"Say Hello With Dialog"** butonu eklemek.
- Buton tıklanınca, **fragment** ile tanımlanmış bir **dialog** açmak.
- Dialog yalnızca bir kez yüklenip, tekrar kullanılabilir olmalı.

---

## 📂 Klasör Yapısı
```

webapp/
├── controller/
│    ├── App.controller.js
│    └── HelloPanel.controller.js
├── view/
│    ├── App.view\.xml
│    ├── HelloPanel.view\.xml
│    └── HelloDialog.fragment.xml
├── i18n/
│    └── i18n.properties

````

---

## 📄 HelloPanel.view.xml Güncellemesi
**`webapp/view/HelloPanel.view.xml`**
```xml
<mvc:View
   controllerName="ui5.walkthrough.controller.HelloPanel"
   xmlns="sap.m"
   xmlns:mvc="sap.ui.core.mvc">
   <Panel
      headerText="{i18n>helloPanelTitle}"
      class="sapUiResponsiveMargin"
      width="auto" >
      <content>
         <Button
            id="helloDialogButton"
            text="{i18n>openDialogButtonText}"
            press=".onOpenDialog"
            class="sapUiSmallMarginEnd"/>
         <Button
            text="{i18n>showHelloButtonText}"
            press=".onShowHello"
            class="myCustomButton"/>
         <Input
            value="{/recipient/name}"
            valueLiveUpdate="true"
            width="60%"/>
         <FormattedText
            htmlText="Hello {/recipient/name}"
            class="sapUiSmallMargin sapThemeHighlight-asColor myCustomText"/>
      </content>
   </Panel>
</mvc:View>
````

### Değişiklikler:

* Yeni buton eklendi: **"Say Hello With Dialog"** (`id="helloDialogButton"`)
* Tıklama olayı `onOpenDialog` fonksiyonunu tetikliyor.
* **Stable ID** (sabit ID) kullanımı ileride test senaryolarında kolaylık sağlar.

---

## 📄 Yeni Fragment: HelloDialog.fragment.xml

**`webapp/view/HelloDialog.fragment.xml`**

```xml
<core:FragmentDefinition
   xmlns="sap.m"
   xmlns:core="sap.ui.core">
   <Dialog
      id="helloDialog"
      title="Hello {/recipient/name}"/>
</core:FragmentDefinition>
```

### Açıklama:

* `FragmentDefinition` → fragment tanımı.
* Controller belirtilmez (fragment’ler controller içermez).
* Dialog başlığı, modelden `/recipient/name` verisiyle dinamik olarak ayarlanır.
* Fragment kendi başına DOM’da görünmez; yalnızca içerdiği kontroller görünür.

---

## 📄 HelloPanel.controller.js Güncellemesi

**`webapp/controller/HelloPanel.controller.js`**

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
            // Dialog'u yalnızca ilk çağrıldığında yükle
            this.oDialog ??= await this.loadFragment({
                name: "ui5.walkthrough.view.HelloDialog"
            });
            this.oDialog.open();
        }
    });
});
```

### Açıklama:

* `async onOpenDialog()` metodu ile **lazy loading** uygulanıyor.
* `this.oDialog ??=` ifadesi → **Eğer `oDialog` tanımlı değilse yükle, varsa tekrar kullan**.
* `loadFragment({ name: "..." })` ile fragment yükleniyor.
* Dialog tekrar tekrar açılıp kapatılabilir.

---

## 📄 i18n.properties Güncellemesi

**`webapp/i18n/i18n.properties`**

```properties
# Hello Panel
showHelloButtonText=Say Hello
helloMsg=Hello {0}
helloPanelTitle=Hello World
openDialogButtonText=Say Hello With Dialog
```

---

## 📌 Önemli Notlar

1. **Fragment’ler** controller içermez → olaylar, fragment’in dahil olduğu view’ın controller’ından yönetilir.
2. **Dialog**, DOM ağacında view’a ait değil → bu yüzden fragment ile tanımlamak tekrar kullanım sağlar.
3. **Lazy loading** ile performans kazanılır → dialog sadece gerektiğinde yüklenir.

---


## 🔗 Kaynaklar

* [Fragments Kullanımı](https://ui5.sap.com/#/topic/b3d8f0d42e0d4c3c9fd0a004b50f9d8d)
* [Dialogs as Fragments](https://ui5.sap.com/#/topic/58c6e8b1b64f4169a97d8b2aef8b2bb0)
* [Stable ID Kullanımı](https://ui5.sap.com/#/topic/2d3f10e03085463b8734bfc41ac08e13)

```

