# Step 12: Shell Control as Container

https://sapui5.hana.ondemand.com/#/topic/4df1d914e52d4b1aa0805eb01522537e

Bu adımda, uygulamamızı **Shell** kontrolü içine alarak, onu yeni kök (root) elemanımız olarak kullanıyoruz. **Shell**, masaüstü ekranlarında uygulamanın genişliğini sınırlayan "letterbox" görünümünü sağlar ve farklı cihaz ekran boyutlarına uyum sağlar.

---

## 🎯 Amaç
- **Shell** kontrolünü uygulamanın dış kapsayıcısı (root container) olarak eklemek.
- Masaüstü ekranlarda "letterbox" (orta hizalanmış dar görünüm) ile daha profesyonel bir görüntü sağlamak.
- Mobil uyum desteğini korumak.

---

## 📂 Güncellenen Dosya

**`webapp/view/App.view.xml`**
```xml
<mvc:View
	controllerName="ui5.walkthrough.controller.App"
	xmlns="sap.m"
	xmlns:mvc="sap.ui.core.mvc"
	displayBlock="true">
	<Shell>
		<App>
			<pages>
				<Page title="{i18n>homePageTitle}">
					<content>
						<Panel
							headerText="{i18n>helloPanelTitle}">
							<content>
								<Button
									text="{i18n>showHelloButtonText}"
									press=".onShowHello"/>
								<Input
									value="{/recipient/name}"
									description="Hello {/recipient/name}"
									valueLiveUpdate="true"
									width="60%"/>
							</content>
						</Panel>
					</content>
				</Page>
			</pages>
		</App>
	</Shell>
</mvc:View>
````

---

## 📖 Açıklamalar

* **sap.m.Shell**

  * Uygulamanın en dış kapsayıcısı olarak çalışır.
  * Geniş ekranlarda **letterbox** görünümü verir.
  * Mobil cihazlarda ekran boyutuna otomatik uyum sağlar.
  * İsteğe bağlı olarak **arka plan resmi**, **arka plan rengi** veya **logo** eklenebilir.
* **Kullanım Notu**

  * Eğer uygulama **SAP Fiori Launchpad** gibi zaten bir Shell içinde çalışıyorsa, XML View içinde ekstra Shell eklenmez.
* **App** ve **Page** yapısı önceki adımlarla aynı şekilde korunur.


---

## 🔗 İlgili Kaynaklar

* [API Reference: sap.m.Shell](https://ui5.sap.com/#/api/sap.m.Shell)
* [Samples: sap.m.Shell](https://ui5.sap.com/#/entity/sap.m.Shell)

```
