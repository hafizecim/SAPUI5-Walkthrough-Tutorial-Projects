# SAPUI5 Walkthrough - Adım 22: Custom Formatters

https://sapui5.hana.ondemand.com/#/topic/0f8626ed7b7542ffaa44601828db20de

Bu adımda, **daha karmaşık veri formatlama** işlemleri için özel bir formatter fonksiyonu ekliyoruz.  
Örnek: Faturaların teknik statü kodlarını kullanıcı dostu metinlerle göstermek.

---

## 1. Amaç
- Data modeldeki teknik durum kodlarını (A, B, C) okunabilir metinlere çevirmek.  
- **Custom formatter** kullanarak daha esnek veri biçimlendirme sağlamak.  
- View içinde doğrudan bu formatter fonksiyonunu çağırmak.

---

## 2. Yeni Dosya ve Fonksiyon

### 📂 `webapp/model/formatter.js`
```javascript
sap.ui.define([], () => {
	"use strict";

	return {
		statusText(sStatus) {
			const oResourceBundle = this.getOwnerComponent().getModel("i18n").getResourceBundle();
			switch (sStatus) {
				case "A":
					return oResourceBundle.getText("invoiceStatusA");
				case "B":
					return oResourceBundle.getText("invoiceStatusB");
				case "C":
					return oResourceBundle.getText("invoiceStatusC");
				default:
					return sStatus;
			}
		}
	};
});
````

📌 **Açıklama:**

* `statusText(sStatus)` → Teknik durumu alır ve i18n kaynağından okunabilir metin döndürür.
* `this.getOwnerComponent().getModel("i18n")` → View yerine **component modeli** üzerinden erişim sağlar, view attach olmadan da çalışır.

---

## 3. Güncellenen View

### 📂 `webapp/view/InvoiceList.view.xml`

```xml
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
    numberUnit="{view>/currency}"
    numberState="{= ${invoice>ExtendedPrice} > 50 ? 'Error' : 'Success' }">
    <firstStatus>
        <ObjectStatus
            core:require="{
                Formatter: 'ui5/walkthrough/model/formatter'
            }"
            text="{
                path: 'invoice>Status',
                formatter: 'Formatter.statusText.bind($controller)'
            }"/>
    </firstStatus>
</ObjectListItem>
```

📌 **Açıklama:**

* `firstStatus` → ObjectListItem’in durum metni için kullanılan aggregation.
* `formatter: 'Formatter.statusText.bind($controller)'` → Custom formatter fonksiyonu çağırılır, `this` bağlamı controller’a atanır.
* `core:require` → XML view içinde formatter modülünü yüklemek için kullanılır.

---

## 4. i18n Kaynakları

### 📂 `webapp/i18n/i18n.properties`

```properties
invoiceStatusA=New
invoiceStatusB=In Progress
invoiceStatusC=Done
```

📌 **Açıklama:**

* Teknik statü kodlarına karşılık gelen kullanıcı dostu metinler.
* Formatter fonksiyonu bu metinleri ObjectStatus kontrolüne uygular.

---

## 5. Sonuç

* Fatura listesi artık statü bilgisini okunabilir bir şekilde gösteriyor.
* Custom formatter, view içinde karmaşık mantıkları ve lokalizasyonu destekler.

---

## 6. Öneriler

* Basit formatlama için **expression binding**, karmaşık veya locale-dependent işlemler için **custom formatter** kullanın.
* Formatter fonksiyonları model verilerini UI’ye uygun biçimde dönüştürmek için idealdir.

---

## 7. Dosya Yapısı Özet

```
webapp/
├── model/
│   └── formatter.js       # Yeni custom formatter
├── view/
│   └── InvoiceList.view.xml
├── controller/
│   └── InvoiceList.controller.js
└── i18n/
    └── i18n.properties
```

---
