# SAPUI5 Walkthrough - Adım 18: Icons

https://sapui5.hana.ondemand.com/#/topic/776f7352807e4f82b18176c8fbdc0c56

https://ui5.sap.com/test-resources/sap/m/demokit/iconExplorer/webapp/index.html

Bu adımda, dialog penceremizi görsel olarak zenginleştirmek için **SAPUI5 Icon Font** kullanacağız.  
SAPUI5, 500’den fazla vektör tabanlı ikon ile birlikte gelir. Bu ikonlar kalite kaybı olmadan ölçeklenebilir.

---

## 1. Amaç
- Dialog’u açan butona **icon** eklemek.
- Dialog içine **Hello World** ikonunu eklemek.
- SAPUI5’in `sap-icon://` protokolünü kullanmayı öğrenmek.

---

## 2. Dosya ve Kod Güncellemeleri

### 📂 `webapp/view/HelloPanel.view.xml`
Dialog’u açan butona **world** ikonu eklenir:

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
            icon="sap-icon://world"
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

📌 **Açıklama:**

* `icon="sap-icon://world"` → SAPUI5’in **Icon Font** içindeki **world** ikonunu kullanır.
* `sap-icon://<ikon-adı>` formatı ile ikon çağrılır.

---

### 📂 `webapp/view/HelloDialog.fragment.xml`

Dialog içine **Hello World** ikonu eklenir:

```xml
<core:FragmentDefinition
   xmlns="sap.m"
   xmlns:core="sap.ui.core" >
   <Dialog
      id="helloDialog"
      title ="Hello {/recipient/name}">
      <content>
         <core:Icon
            src="sap-icon://hello-world"
            size="8rem"
            class="sapUiMediumMargin"/>
      </content>
      <beginButton>
         <Button
            text="{i18n>dialogCloseButtonText}"
            press=".onCloseDialog"/>
      </beginButton>
   </Dialog>
</core:FragmentDefinition>
```

📌 **Açıklama:**

* `src="sap-icon://hello-world"` → SAPUI5’in **Hello World** ikonunu çağırır.
* `size="8rem"` → İkonun boyutu ayarlanır.
* `class="sapUiMediumMargin"` → İkona orta seviyede margin eklenir.

---

## 3. Icon Explorer Kullanımı

SAPUI5’te mevcut tüm ikonları görmek için **Icon Explorer** aracını kullanabilirsiniz:
🔗 [Icon Explorer](https://sapui5.hana.ondemand.com/iconExplorer.html)

Kullanım formatı:

```
sap-icon://ikon-adi
```

Örnek:

```
sap-icon://add
sap-icon://delete
sap-icon://world
```

---

## 4. Terminal Komutları

Kod değişikliklerinden sonra projeyi çalıştırmak için:

```sh
npm start
```

veya

```sh
ui5 serve
```

---

## 5. Dosya Yapısı

```
C:\sapui5\SAPUI5_TUTORIALS\hello_world\
│
├── webapp\
│   ├── controller\
│   │   └── HelloPanel.controller.js
│   ├── view\
│   │   ├── HelloPanel.view.xml         # Güncellendi
│   │   └── HelloDialog.fragment.xml    # Güncellendi
│   ├── i18n\
│   │   └── i18n.properties
│   ├── manifest.json
│   └── index.html
└── package.json
```

---

## 6. Sonuç

Bu adımda:

* Dialog’u açan butona **world** ikonu eklendi.
* Dialog içine büyük boyutlu **Hello World** ikonu yerleştirildi.
* SAPUI5’in `sap-icon://` ikon protokolü öğrenildi.
* Uygulama daha görsel ve kullanıcı dostu hale geldi.

---

```
