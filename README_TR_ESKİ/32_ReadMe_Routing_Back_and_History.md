# Adım 32: Geri Dönme ve Geçmiş Yönetimi (Routing Back and History)

https://sapui5.hana.ondemand.com/#/topic/8ef57cfd37b44f089f7e3b52d56597eb

Artık detay sayfasına gidebiliyor ve bir faturayı görüntüleyebiliyoruz,  
ancak overview sayfasına geri dönemiyoruz. Bu adımda, detay sayfasına bir geri butonu ekleyecek ve overview sayfasına dönüşü sağlayacak bir fonksiyon oluşturacağız.

---

## 1. Detail View

`Detail.view.xml`:

```xml
<mvc:View controllerName="ui5.walkthrough.controller.Detail">
  <Page
    title="{i18n>detailPageTitle}"
    showNavButton="true"
    navButtonPress=".onNavBack">
    <ObjectHeader
      intro="{invoice>ShipperName}"
      title="{invoice>ProductName}"/>
  </Page>
</mvc:View>
````

* `showNavButton="true"` ile geri butonu gösterilir.
* `navButtonPress=".onNavBack"` ile tıklandığında çağrılacak event handler atanır.

---

## 2. Detail Controller

`Detail.controller.js`:

```javascript
sap.ui.define([
  "sap/ui/core/mvc/Controller",
  "sap/ui/core/routing/History"
], (Controller, History) => {
  "use strict";

  return Controller.extend("ui5.walkthrough.controller.Detail", {

    onInit() {
      const oRouter = this.getOwnerComponent().getRouter();
      oRouter.getRoute("detail").attachPatternMatched(this.onObjectMatched, this);
    },

    onObjectMatched(oEvent) {
      this.getView().bindElement({
        path: "/" + window.decodeURIComponent(oEvent.getParameter("arguments").invoicePath),
        model: "invoice"
      });
    },

    onNavBack() {
      const oHistory = History.getInstance();
      const sPreviousHash = oHistory.getPreviousHash();

      if (sPreviousHash !== undefined) {
        window.history.go(-1);
      } else {
        const oRouter = this.getOwnerComponent().getRouter();
        oRouter.navTo("overview", {}, true);
      }
    }
  });
});
```

* `History` bağımlılığı ile uygulama içi navigation geçmişi yönetilir.
* `onNavBack` fonksiyonu:

  * Önce önceki hash kontrol edilir.
  * Geçmiş varsa tarayıcı geçmişi ile geri gidilir.
  * Geçmiş yoksa router doğrudan overview sayfasına yönlendirir (`true` parametresi history state’i değiştirir).
* Bu, kullanıcı doğrudan detay sayfasını açsa bile overview’a geri dönmeyi garanti eder.

---

## 3. Sonuç

* Detail sayfasında geri butonuna tıkladığınızda, kullanıcı overview sayfasına geri döner.
* Uygulama dışından gelen linkler veya tarayıcı bookmark’ları için de düzgün çalışır.

---

## Konvansiyonlar

* Geçmiş durumu belirsiz olduğunda, ebeveyn sayfaya dönüş path’i ekleyin.

---

**Önceki Adım:** Step 31: Routing with Parameters
**Sonraki Adım:** Step 33: Custom Controls
**İlgili Kaynaklar:**

* [Routing and Navigation](https://sapui5.hana.ondemand.com/#/topic/…)
* [Tutorial: Navigation and Routing](https://sapui5.hana.ondemand.com/#/topic/…)

```

