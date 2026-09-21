# Claude-Plugin-Zettelkasten
Veri analitiği alanında uzmanlaştırılmış olan bu model, kullanıcıdan gelen direktifler doğrultusunda analitik çalışmalar gerçekleştirir ve çalışma sonuçlarını ‘’zettelkasten’’ formatında ‘’Notion veritabanına’’ kaydeder.

## İçerik
Bu plugin içerisinde 2 adet Skill ve bir adet Connetcor kullanılmıştır.

### Claude Skills
- **Veri Analitiği:** Modelin; araştırma, işleme, analiz ve görselleştirme becerilerini geliştirmek amacıyla üretilir.
- **Zettelkasten:** Uygulamanın asıl değer önerisidir. Modele, Zettelkasten metodu hakkında rehberlik eder.

### Connectors
- **Notion MCP:** Kullanıcının çalışma alanına bağlanmak için Notion MCP kullanılır.

## Kullanım Kılavuzu
Kullanıcı bu plugin aracılığıyla 3 temel fonksiyonu ve bazı diğer ek fonksiyonları gerçekleştirebilir:
1. Geçici Not Oluşturma
2. Lİteratür Not Oluşturma
3. Zettelkasten Not Oluşturma

**NOT:** Bu fonksiyonlar bir paket halinde tek oturumda kullanılabileceği gibi ayrı ayrı da kullanılabilir.

### Geçici Not Oluşturma
Kullanıcının plugin komutunu çağırmasıyla plugin devreye girer. Kullanıcı aklındaki fikri Claude’a anlatır. Claude bunları yapılandılırmış hale Notion veritabanına kaydeder. Claude, kayıt öncesi kısa bir özet sunarak onay ister.

### Literatür Not Oluşturma
Kullanıcının plugin komutu ile oturumu başlatır ve internet üzerinden araştırmalar başlar. Bu noktada ‘’kaynak belirtme zorunluluğundan’’ ötürü, Claude kendi eğitim verilerinden değil internet üzerinden araştırmalar gerçekleştirir.

Araştırma oturumu sonunda elde edilen bilgiler ve kayıtlar ‘’kullanıcı onayı’’ ardından Notion veritabanına literatür not şablonu referans alınarak kaydedilir.

### Kalıcı Not Oluşturma
Kullanıcı dilerse Notion içerisindeki hazır bulunan literatür ve geçici notları kullanarak kalıcı notlar oluşturabilir.

### Zettelkasten Paketi
Kullanıcı plugin komutunu çalıştırarak oturumu başlatır. Ardından geçici notlar, literatür notlar ve zettelkasten notlar tek bir oturum içerisinde oluşturularak Notion’a üç ayrı kategori (not türüne göre) altında kaydedilir.

Bu aşamada geçici not oluşturma, literatür not oluşturma ve kalıcı notlar oluşturma tek bir oturum içerisinde uçtan uca ve sıfırdan gerçekleştirilir.

### Diğer Kullanımlar
- **Beyin Fırtınası:** Kullanıcı aklındaki fikri geçici not haline getirmeden önce veya getirdikten sonra Claude ile beyin fırtınası yaparak notu geliştirebilir.
- **Düzenleme ve Organizasyon:** Claude’un veritabanı asistanı olarak kullanılması ile Notion içerisinde ‘’etiket atama, dağınık notları şablona uygun hale getirme ve fazlalık notları silme’’ gibi veritabanı işlemleri gerçekleştirilir.

## Sürüm Geçmişi
Mevcut Sürüm: v1.0

*Sürümler ilgili klasörlerde tüm içeriği ile birlikte arşivlenmektedir.*
