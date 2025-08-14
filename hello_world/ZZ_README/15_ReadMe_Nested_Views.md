# Step 15: Nested Views (İç İçe Görünümler)

https://sapui5.hana.ondemand.com/#/topic/df8c9c3d79b54c928855162bafcd88ee

Bu adımda uygulamamızın **panel içeriklerini** ana görünümden (`App.view.xml`) ayırarak **yeni bir alt görünüm (HelloPanel.view.xml)** haline getiriyoruz.  
Bunun amacı:
- **Kodun okunabilirliğini artırmak**
- **Daha modüler bir yapı kurmak**
- **Yeniden kullanılabilir bileşenler** elde etmek

> Görsel değişiklik yoktur, ancak proje yapısı daha düzenli hale gelir.

---

## 📂 Klasör Yapısı
```

webapp/
├── controller/
│    ├── App.controller.js
│    └── HelloPanel.controller.js
├── view/
│    ├── App.view\.xml
│    └── HelloPanel.view\.xml
├── css/
│    └── style.css
├── manifest.json

````

---

## 📄 App.view.xml Güncellemesi
**`webapp/view/App.view.xml`**
```xml
<mvc:View
	controllerName="ui5.walkthrough.controller.App"
	xmlns="sap.m"
	xmlns:mvc="sap.ui.core.mvc"
	displayBlock="true">
	<Shell>
		<App class="myAppDemoWT">
			<pages>
				<Page title="{i18n>homePageTitle}">
					<content>
						<mvc:XMLView viewName="ui5.walkthrough.view.HelloPanel"/>
					</content>
				</Page>
			</pages>
		</App>
	</Shell>
</mvc:View>
````

### Açıklama:

* Panel içeriğini doğrudan `App.view.xml` içine yazmak yerine `<mvc:XMLView>` etiketi ile **HelloPanel** görünümünü dahil ediyoruz.
* `viewName` → Görünümün **tam isim alanı (namespace)**.

---

## 📄 Yeni Görünüm: HelloPanel.view\.xml

**`webapp/view/HelloPanel.view.xml`**

```xml
<mvc:View
   controllerName="ui5.walkthrough.controller.HelloPanel"
   xmlns="sap.m"
   xmlns:mvc="sap.ui.core.mvc">
   <Panel
      headerText="{i18n>helloPanelTitle}"
      class="sapUiResponsiveMargin"
      width="auto">
      <content>
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
```

### Açıklama:

* Tüm panel içeriği artık burada tanımlı.
* `controllerName` → Panelin kendi controller dosyasına bağlanmasını sağlar.
* Önceki adımda eklediğimiz `myCustomButton` ve `myCustomText` CSS sınıfları kullanılmaya devam ediyor.

---

## 📄 Yeni Controller: HelloPanel.controller.js

**`webapp/controller/HelloPanel.controller.js`**

```javascript
sap.ui.define([
   "sap/ui/core/mvc/Controller",
   "sap/m/MessageToast"
], (Controller, MessageToast) => {
   "use strict";

   return Controller.extend("ui5.walkthrough.controller.HelloPanel", {
      onShowHello() {
         // i18n modelinden mesajı oku
         const oBundle = this.getView().getModel("i18n").getResourceBundle();
         const sRecipient = this.getView().getModel().getProperty("/recipient/name");
         const sMsg = oBundle.getText("helloMsg", [sRecipient]);

         // Mesajı göster
         MessageToast.show(sMsg);
      }
   });
});
```

### Açıklama:

* `onShowHello` metodu App controller’dan buraya taşındı.
* Artık buton tıklama olayı (`press`) bu controller içindeki `onShowHello` metodunu tetikliyor.

---

## 📄 App.controller.js Güncellemesi

**`webapp/controller/App.controller.js`**

```javascript
sap.ui.define([
   "sap/ui/core/mvc/Controller"
], (Controller) => {
   "use strict";

   return Controller.extend("ui5.walkthrough.controller.App", {
      // Şimdilik boş, ilerleyen adımlarda kullanılacak
   });
});
```

* App controller artık boş, sadece temel tanımı barındırıyor.
* İlerleyen adımlarda başka işlevler ekleyeceğiz.

---

## 📖 Önemli Noktalar

1. **Modülerlik**

   * Panel içeriği ayrı bir view dosyasına taşındı.
   * Daha okunabilir ve yönetilebilir kod yapısı.

2. **Yeniden Kullanılabilirlik**

   * `HelloPanel` başka sayfalarda veya uygulamalarda kolayca kullanılabilir.

3. **Controller Ayrımı**

   * Panelin kendi controller’ı var.
   * App controller yalnızca uygulama genelini yönetir.

---

## 🔗 İlgili Kaynaklar

* [XML Views](https://ui5.sap.com/#/topic/91f086396f4d1014b6dd926db0e91070)
* [Controller Usage](https://ui5.sap.com/#/topic/68b9644a253741e8a4b9e4279a35c247)
* [Walkthrough Tutorial](https://ui5.sap.com/#/topic/3d18f20bd2294228acb6910d8e8c65e1)

```
