# SAPUI5 Walkthrough - Adım 23: Filtering

https://sapui5.hana.ondemand.com/#/topic/5295470d7eee46c1898ee46c1b9ad763

Bu adımda, **ürün listesi için arama ve filtreleme** ekliyoruz.  
Kullanıcı arama alanına bir terim girdiğinde, liste otomatik olarak güncellenir ve sadece eşleşen öğeler gösterilir.

---

## 1. Amaç
- Listeyi kullanıcı tarafından girilen arama terimine göre filtrelemek.  
- SearchField kontrolü ile liste başlığına arama alanı eklemek.  
- SAPUI5 `Filter` ve `FilterOperator` kullanarak binding üzerinde filtre uygulamak.

---

## 2. Güncellenen View

### 📂 `webapp/view/InvoiceList.view.xml`
```xml
<List
    id="invoiceList"
    class="sapUiResponsiveMargin"
    width="auto"
    items="{invoice>/Invoices}" >
    <headerToolbar>
        <Toolbar>
            <Title text="{i18n>invoiceListTitle}"/>
            <ToolbarSpacer/>
            <SearchField 
                width="50%" 
                search=".onFilterInvoices"/>
        </Toolbar>
    </headerToolbar>
    ...
</List>
````

📌 **Açıklama:**

* `id="invoiceList"` → Listeyi controller içinde tanımlamak için gereklidir.
* `headerToolbar` → Liste başlığı yerine daha esnek bir toolbar sağlar.
* `SearchField` → Kullanıcının arama yapabileceği alan. `search=".onFilterInvoices"` ile event handler bağlanır.
* Toolbar içindeki `ToolbarSpacer` → Başlık ve arama alanını iki uçta konumlandırır.

---

## 3. Güncellenen Controller

### 📂 `webapp/controller/InvoiceList.controller.js`

```javascript
sap.ui.define([
	"sap/ui/core/mvc/Controller",
	"sap/ui/model/json/JSONModel",
	"sap/ui/model/Filter",
	"sap/ui/model/FilterOperator"
], (Controller, JSONModel, Filter, FilterOperator) => {
	"use strict";

	return Controller.extend("ui5.walkthrough.controller.InvoiceList", { 
		onInit() {
			const oViewModel = new JSONModel({
				currency: "EUR"
			});
			this.getView().setModel(oViewModel, "view");
		},

		onFilterInvoices(oEvent) {
			// filtre dizisi oluştur
			const aFilter = [];
			const sQuery = oEvent.getParameter("query");
			if (sQuery) {
				aFilter.push(new Filter("ProductName", FilterOperator.Contains, sQuery));
			}

			// bindingi filtrele
			const oList = this.byId("invoiceList");
			const oBinding = oList.getBinding("items");
			oBinding.filter(aFilter);
		}
	});
});
```

📌 **Açıklama:**

* `Filter` → Filtreleme yapılandırmasını tutar.
* `FilterOperator.Contains` → Girilen metni `ProductName` alanında arar.
* `oEvent.getParameter("query")` → SearchField eventinden arama terimini alır.
* Eğer arama terimi boş ise, filtreleme yapılmaz ve tüm öğeler listelenir.
* `oList.getBinding("items").filter(aFilter)` → Listeyi filtreler ve UI otomatik olarak güncellenir.

---

## 4. Sonuç

* Liste başına eklenen **SearchField** ile kullanıcı arama yapabilir.
* Arama terimine göre liste filtrelenir ve yalnızca eşleşen öğeler gösterilir.
* Filtre case-insensitive çalışır.

---

## 5. Öneriler

* İleride birden fazla alanda arama yapmak isterseniz, `aFilter.push()` ile birden fazla Filter ekleyebilirsiniz.
* Daha karmaşık filtreleme için `FilterOperator` dokümantasyonuna bakabilirsiniz.

---

## 6. Dosya Yapısı Özet

```
webapp/
├── view/
│   └── InvoiceList.view.xml   # SearchField ve headerToolbar eklendi
├── controller/
│   └── InvoiceList.controller.js # onFilterInvoices fonksiyonu eklendi
└── i18n/
    └── i18n.properties
```

---

