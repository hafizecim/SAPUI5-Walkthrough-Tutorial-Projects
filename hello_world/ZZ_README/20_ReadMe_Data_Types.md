# SAPUI5 Walkthrough - Adım 20: Data Types

https://sapui5.hana.ondemand.com/#/topic/dfe04650afc046e0802abb1a1a90d2d9

Bu adımda, faturaların **fiyatlarını** kullanıcı dostu şekilde göstermek için **SAPUI5 data types** kullanıyoruz.  
Amaç: JSON modeldeki teknik fiyat değerlerini locale bağımlı formatta göstermek.

---

## 1. Amaç
- Fatura listesinde fiyatların doğru formatta görüntülenmesi.
- **sap.ui.model.type.Currency** kullanımı ile para birimi ve ondalık sayıları biçimlendirmek.
- Farklı modellerden gelen verileri tek bir property üzerinde binding yapmak (**Composite Binding / Calculated Fields**).

---

## 2. Güncellenen Dosyalar

### 📂 `webapp/view/InvoiceList.view.xml` _(Güncellendi)_
```xml
<mvc:View
    controllerName="ui5.walkthrough.controller.InvoiceList"
    xmlns="sap.m"
    xmlns:core="sap.ui.core"
    xmlns:mvc="sap.ui.core.mvc">
    <List
        headerText="{i18n>invoiceListTitle}"
        class="sapUiResponsiveMargin"
        width="auto"
        items="{invoice>/Invoices}">
        <items>
            <ObjectListItem
                core:require="{
                    Currency: 'sap/ui/model/type/Currency'
                }"
                title="{invoice>Quantity} x {invoice>ProductName}"
                number="{
                    parts: [
                        'invoice>ExtendedPrice',
                        'view>/currency'
                    ],
                    type: 'Currency',
                    formatOptions: {
                        showMeasure: false
                    }
                }"
                numberUnit="{view>/currency}"/>
        </items>
    </List>
</mvc:View>
````

📌 **Açıklama:**

* `number` property → Composite binding kullanarak iki modelden veri alır:

  * `invoice>ExtendedPrice` → JSON modelden fiyat
  * `view>/currency` → View modelden para birimi
* `core:require` ile **Currency type** yüklenir ve `type="Currency"` ile binding uygulanır.
* `showMeasure: false` → number alanında para birimi kodunu göstermez, `numberUnit` kullanılır.

---

### 📂 `webapp/controller/InvoiceList.controller.js` *(Yeni)*

```javascript
sap.ui.define([
	"sap/ui/core/mvc/Controller",
	"sap/ui/model/json/JSONModel"
], (Controller, JSONModel) => {
	"use strict";

	return Controller.extend("ui5.walkthrough.controller.InvoiceList", {
		onInit() {
			const oViewModel = new JSONModel({
				currency: "EUR"
			});
			this.getView().setModel(oViewModel, "view");
		}
	});
});
```

📌 **Açıklama:**

* Fiyatlar için kullanılan para birimi view modelde saklanır (`currency: "EUR"`).
* `numberUnit="{view>/currency}"` binding ile ObjectListItem kontrolüne aktarılır.
* View modeli, sadece kontrol yapılandırmaları ve ayarlar için kullanılır.

---

## 3. Data Types Mantığı

* SAPUI5 data types kullanımı → veri biçimlendirme, parsing ve validasyon sağlar.
* **Currency type** → locale bağımlı ondalık ayırıcı, ondalık hane sayısı ve para birimi gösterimi.
* Composite Binding → Farklı modellerden gelen verilerin tek property’de birleşmesini sağlar.

---

## 4. Sonuç

* Fatura listesinde fiyatlar artık **2 ondalık basamaklı, Euro cinsinden** gösterilir.
* SAPUI5’in data type ve composite binding özellikleri sayesinde locale bağımlı ve doğru biçimlendirilmiş veri gösterimi sağlanır.

---

## 5. Terminal Komutları

```bash
npm start
```

veya

```bash
ui5 serve
```

Tarayıcıda:

```
http://localhost:8080
```

---

## 6. Dosya Yapısı Özet

```
webapp/
├── controller/
│   └── InvoiceList.controller.js   # Yeni
├── view/
│   └── InvoiceList.view.xml       # Güncellendi
└── Invoices.json                  # JSON veri modeli
```

---
