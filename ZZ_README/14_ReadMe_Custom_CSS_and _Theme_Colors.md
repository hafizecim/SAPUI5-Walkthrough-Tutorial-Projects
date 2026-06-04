# Step 14: Custom CSS ve Tema Renkleri

https://sapui5.hana.ondemand.com/#/topic/723f4b2334e344c08269159797f6f796

Bu adımda SAPUI5’in sunduğu standart margin/padding sınıflarının ötesine geçerek **kendi özel CSS stillerimizi** ekleyeceğiz.  
Bu sayede:
- Piksel hassasiyetinde boşluk ayarlamaları
- Özel metin biçimlendirmeleri
- Tema uyumlu renk kullanımı  
yapabileceğiz.

⚠ **Dikkat**  
SAPUI5 tarafından üretilen HTML ve CSS, **public API** değildir ve sürüm güncellemelerinde değişebilir.  
Bu nedenle:
- SAPUI5 sürümünü kontrol edebildiğiniz senaryolarda (ör. bağımsız uygulama) stil üzerine yazma uygundur.
- **SAP Fiori Launchpad** üzerinde çalışan uygulamalarda stil üzerine yazmaktan kaçının.

---

## 📂 Klasör Yapısı
```

webapp/
├── css/
│    └── style.css
├── view/
│    └── App.view\.xml
├── manifest.json

````

---

## 📄 style.css (Yeni)
**`webapp/css/style.css`**
```css
html[dir="ltr"] .myAppDemoWT .myCustomButton.sapMBtn {
   margin-right: 0.125rem;
}

html[dir="rtl"] .myAppDemoWT .myCustomButton.sapMBtn {
   margin-left: 0.125rem;
}

.myAppDemoWT .myCustomText {
   display: inline-block;
   font-weight: bold;
}
````

### Açıklamalar:

* `.myAppDemoWT` → Uygulamamıza özel **namespace class**.
  CSS sadece bu sınıfa sahip container içinde geçerli olur.
* `.myCustomButton` → Butona eklediğimiz özel sınıf.
  LTR dilde sağa, RTL dilde sola **0.125rem** (\~2px) boşluk ekler.
* `.myCustomText` → Metni **kalın** ve **inline-block** yapar.

---

## 📄 manifest.json Güncellemesi

**`webapp/manifest.json`**

```json
"resources": {
  "css": [
    {
      "uri": "css/style.css"
    }
  ]
}
```

* `resources.css` kısmına `style.css` eklenir.
* SAPUI5 bu dosyayı `<link>` etiketiyle HTML sayfasına yükler.

---

## 📄 App.view\.xml Güncellemesi

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
					</content>
				</Page>
			</pages>
		</App>
	</Shell>
</mvc:View>
```

---

## 📖 Önemli Noktalar

1. **App.container sınıfı**

   * `App` kontrolüne `myAppDemoWT` sınıfı eklendi.
   * Bu, CSS seçimlerinin yalnızca bu uygulamada geçerli olmasını sağlar.

2. **Buton boşluğu**

   * Standart `sapMBtn` margin’i üzerine yazıldı.
   * LTR ve RTL diller için farklı yönlerde boşluk verildi.

3. **Metin biçimlendirmesi**

   * `FormattedText` kontrolü ile HTML desteği sağlandı.
   * `myCustomText` ile metin **bold** yapıldı.
   * `sapThemeHighlight-asColor` ile tema uyumlu renk atandı.

---

## 🎨 Tema Uyumluluğu

* Renkler **özel CSS** içinde sabit kodlanmadı.
* Bunun yerine **SAPUI5 tema sınıfları** (`sapThemeHighlight-asColor`) kullanıldı.
* Böylece tema değiştiğinde renk otomatik uyum sağlar.

---

## 🔗 İlgili Kaynaklar

* [Manifest.json Kullanımı](https://ui5.sap.com/#/topic/62b1485d949d46f39a6e69e0cc943c13)
* [CSS Classes for Theme Parameters](https://ui5.sap.com/#/topic/bd59f36f8f4b4c29bdf7cf337c7a6d12)
* [Creating Themable User Interfaces](https://ui5.sap.com/#/topic/3d18f20bd2294228acb6910d8e8c65e1)

```
