# Adım 31: Parametre ile Routing

https://sapui5.hana.ondemand.com/#/topic/2366345a94f64ec1a80f9d9ce50a59ef

Artık Overview ve Detail sayfaları arasında gezinebiliyoruz, fakat seçilen öğe detay sayfasında henüz görünmüyor.  
Tipik bir kullanım senaryosu, seçilen öğenin detaylarını detay sayfasında göstermek olacaktır.

---

## 1. Routing Yapılandırması (manifest.json)

```json
"routes": [
  {
    "pattern": "",
    "name": "overview",
    "target": "overview"
  },
  {
    "pattern": "detail/{invoicePath}",
    "name": "detail",
    "target": "detail"
  }
]
````

* `invoicePath` parametresi ile seçilen öğenin bilgisi detay sayfasına aktarılır.
* Zorunlu parametreler `{}` içinde tanımlanır.

---

## 2. Detail View

`Detail.view.xml`:

```xml
<mvc:View controllerName="ui5.walkthrough.controller.Detail">
  <Page title="{i18n>detailPageTitle}">
    <ObjectHeader
      intro="{invoice>ShipperName}"
      title="{invoice>ProductName}"/>
  </Page>
</mvc:View>
```

* ObjectHeader ile fatura modelindeki iki alan gösterilir.
* Daha fazla alan eklemek mümkün, örnek basit tutuldu.

---

## 3. Invoice List Controller

`InvoiceList.controller.js`:

```javascript
onPress(oEvent) {
  const oItem = oEvent.getSource();
  const oRouter = this.getOwnerComponent().getRouter();
  oRouter.navTo("detail", {
    invoicePath: window.encodeURIComponent(
      oItem.getBindingContext("invoice").getPath().substring(1)
    )
  });
}
```

* Tıklanan öğe `getSource()` ile alınır.
* `navTo` ile `invoicePath` parametresi URL’e eklenir ve detay sayfasına geçilir.
* Binding path URL için uygun şekilde encode edilir.

---

## 4. Detail Controller (Yeni)

`Detail.controller.js`:

```javascript
sap.ui.define(["sap/ui/core/mvc/Controller"], (Controller) => {
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
    }
  });
});
```

* Router’dan `detail` route’u izlenir.
* `onObjectMatched` ile URL parametresi alınır ve view bağlanır (`bindElement`).
* `decodeURIComponent` ile URL’deki encode edilmiş path çözülür.

---

## 5. Sonuç

* Artık bir öğeye tıkladığınızda, detay sayfasında seçilen fatura bilgileri görüntülenir.
* `bindElement` ile model ve path bağlanır, UI otomatik güncellenir.

---

## Konvansiyonlar

* Routing yapılandırmasını `manifest.json` içinde tanımlayın.
* Router’ı Component#init içinde başlatın.

---

**Önceki Adım:** Step 30: Routing and Navigation
**Sonraki Adım:** Step 32: Routing Back and History
**İlgili Kaynaklar:**

* [Routing and Navigation](https://sapui5.hana.ondemand.com/#/topic/…)
* [Tutorial: Navigation and Routing](https://sapui5.hana.ondemand.com/#/topic/…)

```
