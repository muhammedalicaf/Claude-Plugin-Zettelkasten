# Web araştırma yöntemi (literatür notu için)

Modele yönelik talimat; kullanıcı çıktısı Türkçe.

## 1. Soruyu çerçevele (30 saniye)

- Konuyu tek cümlelik bir araştırma sorusuna çevir: "X nedir, nasıl çalışır, ne zaman
  kullanılır, sınırları ne?" Kullanıcı farklı bir açı istediyse onu kullan.
- 3–6 arama terimi üret: Türkçe (2–3), İngilizce (2–3). Teknik terimin yaygın İngilizce
  karşılığını parantez içinde tut; notta ilk geçtiği yerde "Kavram (English Term)" yaz.

## 2. Ara (önce Türkçe, sonra İngilizce)

Araçlar: `WebSearch` (standart mod; sonuç zayıfsa veya konu güncel/nişse genişletilmiş
mod), ardından her aday için `WebFetch` ile tam metni oku. Snippet'ten alıntı yapma.

Sıra:
1. Türkçe aramalar → en iyi 2–4 aday.
2. İngilizce aramalar → boşlukları dolduracak 1–3 aday.
3. Toplam 3–5 kaynak seç. Aynı siteden en fazla 1 kaynak (resmi dokümantasyon hariç).

## 3. Güvenilirlik sınıflandırması

Her kaynağı bir sınıfa koy; notun "Değerlendirme" bölümünde sınıf karışımını belirt.

| Sınıf | Örnek | Kullanım |
|---|---|---|
| A — Birincil / kurumsal | Resmi doküman, standart, yasa, orijinal makale, kurumun kendi sitesi, resmi istatistik | Tanım ve rakamlar için tercih edilir |
| B — Hakemli / editöryal | Hakemli dergi, üniversite yayını, ansiklopedi (TÜBİTAK, Britannica), tanınmış teknik yayın (NN/g, MDN) | Açıklama ve bağlam |
| C — İkincil / ticari | Şirket blogu, ajans yazısı, haber sitesi | Örnek ve güncel uygulama; tek başına iddia taşımaz |
| D — Kullanıcı üretimi | Forum, kişisel blog, video açıklaması | Yalnızca A–C ile desteklenirse; aksi halde kullanma |

Kırmızı bayraklar: tarih yok, yazar yok, kaynak göstermiyor, satış sayfası, otomatik
çeviri izleri, 3+ yaşında ve konu hızlı değişiyor. Bayraklı kaynağı not düş veya at.

## 4. Oku ve çıkar

Her kaynak için kısa bir fiş tut (scratchpad'de, kullanıcıya gösterilmez):

```
[n] Başlık — Site — Tarih — Sınıf
Ana iddialar: …
Rakam/tanım: … (sayfa içi konum)
Diğerleriyle çelişki: …
```

## 5. Sentezle

- Kaynak sırasına göre değil, **fikir sırasına** göre yaz: tanım → mekanizma → türler /
  tarihçe → uygulama → tartışma.
- Her paragrafta en az bir atıf; iki kaynağın uzlaştığı iddia `\[1\]\[2\]` taşır.
- Uzlaşmazlık varsa "X'e göre … \[1\]; Y ise … \[3\]" biçiminde ver, sonra hangisinin
  daha güvenilir olduğunu söyle.
- Kullanıcının mevcut notlarıyla ilişki: zettelkasten skill'i kopya kontrolünde benzer
  başlık bulduysa, notun "Değerlendirme" bölümünde o nota mention ver.

## 6. Kaynak listesi biçimi

`Kaynak` özelliği ve gövdedeki "Kaynaklar" bölümü birebir aynı:

```
1. Kaynak başlığı - https://tam.url/yol
2. Kaynak başlığı - https://tam.url/yol
```

- Başlık: sayfanın kendi başlığı (gerekirse kısaltılmış), site adı önekli olabilir
  ("Figma - Görsel Hiyerarşi Nedir?").
- URL: `WebFetch` ile gerçekten açılmış tam URL; takip parametreleri (`utm_*`) temizlenir.
- Erişilemeyen, 404 dönen veya paywall arkasındaki URL listeye girmez.

## 7. Durma koşulları

- 3 güvenilir kaynak bulunamadı → kullanıcıya söyle, devam etmek isteyip istemediğini sor.
- Konu kişisel veri, sağlık/hukuk/finans tavsiyesi gibi hassas alana giriyorsa A–B sınıfı
  kaynak şart; C–D ile yazma.
- Kullanıcının isteği "kendi bilgi birikiminle yaz" ise reddetme; ama notun `Kaynak`
  alanına kaynak yazamayacağını ve bu notun literatür notu değil geçici not olarak
  kaydedilmesi gerektiğini söyle.
