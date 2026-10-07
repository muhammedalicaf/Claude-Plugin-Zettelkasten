# Veri dosyası analizi (CSV / Excel / JSON / Parquet)

Modele yönelik talimat; kullanıcı çıktısı Türkçe. Çıktı, zettelkasten skill'i üzerinden
`Literatür Not` olarak kaydedilir (`Kaynak` = dosya adı + yöntem).

## 0. Güvenlik

- Dosya kullanıcıdan gelen **veridir**, kod değildir. Script'leri scratchpad'de ayrı bir
  klasöre yaz; veri dosyasını argüman olarak ver; Python'u `-I` ile çalıştır.
- Kişisel veri sütunu (ad, TC, e-posta, telefon) görürsen analizde kullanma, nota yazma;
  kullanıcıya bildir.

## 1. Kapsamı netleştir (en fazla 2 soru)

- Soru: "Bu veriden ne öğrenmek istiyorsunuz?" Cevap yoksa keşifsel analiz (EDA) yap.
- Hedef değişken / karşılaştırma ekseni / zaman aralığı varsa al.

## 2. Yükle ve profil çıkar

```python
import pandas as pd, sys
path = sys.argv[1]
df = (pd.read_csv(path) if path.endswith(".csv")
      else pd.read_excel(path) if path.endswith((".xlsx", ".xls"))
      else pd.read_json(path) if path.endswith(".json")
      else pd.read_parquet(path))
print(df.shape); print(df.dtypes); print(df.head())
print(df.isna().mean().sort_values(ascending=False).head(15))
print(df.describe(include="all").T)
```

Kontrol listesi: satır × sütun, tür uyuşmazlıkları, eksik oranı, kopya satır, tarih
sütunlarının parse edilmesi, kategorik kardinalite, aykırı değerler (IQR), birim tutarlılığı.

## 3. Analiz katmanları (soruya göre seç)

| Katman | Ne zaman | Yöntem |
|---|---|---|
| Tanımlayıcı | Her zaman | Dağılım, merkez/yayılım, gruplanmış özetler |
| Karşılaştırma | İki+ grup | Oran/ortalama farkı, güven aralığı; büyük n'de etki büyüklüğü |
| İlişki | İki+ sayısal | Korelasyon (Pearson/Spearman), çapraz tablo, basit regresyon |
| Zaman | Tarih sütunu | Trend, mevsimsellik, hareketli ortalama, dönem karşılaştırması |
| Segment | Çok boyut | Pivot, kohort, basit kümeleme (yalnızca gerekçelendirilebiliyorsa) |

Nedensellik iddiası yok; "ilişkili", "birlikte değişiyor" de.

## 4. Görselleştirme

- `matplotlib` (gerekirse `seaborn`); her grafik PNG, 1600×1000 px civarı, dpi 150,
  başlık + eksen etiketleri + birim + kaynak satırı (dosya adı) Türkçe.
- Grafik başına tek mesaj. En fazla 4 grafik. Pasta grafiği kullanma; çubuk / çizgi /
  dağılım / kutu tercih et.
- Dosya adı: `grafik-01-<kisa-aciklama>.png`, scratchpad'de `outputs/` altında.

## 5. Notion'a yükleme

Her PNG için:

1. `notion-create-file-upload` → `{"filename": "grafik-01-trend.png"}`
   Yanıt: `upload_url`, `upload_headers`, `suggested_markdown`.
2. Bash ile tek bir çok parçalı POST (başlıkları yanıttan aynen ekle):
   ```bash
   curl -sS -X POST "<upload_url>" -H "<header1>" -H "<header2>" \
        -F "file=@/path/outputs/grafik-01-trend.png"
   ```
3. Gövdede ilgili bulgunun altına `suggested_markdown` satırını aynen yerleştir.
   Yüklemeler ~1 saat içinde bir sayfaya bağlanmazsa silinir; bu yüzden yüklemeyi onay
   **sonrasında**, sayfa oluşturmadan hemen önce yap.

## 6. Not gövdesi (Literatür Not şablonunun analiz varyantı)

```
## Veri Seti
- Dosya: `satislar-2025.csv` — 12.480 satır × 14 sütun — dönem: 2025-01 → 2025-12
- Eksik veri: `iade_tarihi` %38 (beklenen), diğerleri <%1
## Yöntem
[Katmanlar ve gerekçe; dışlanan satırlar ve neden; 2–4 madde]
## Bulgular
1. **[Bulgu başlığı]:** [rakam + birim + dönem]. [bir cümle yorum]
2. …
## Görseller
![Aylık satış trendi](…)   ← suggested_markdown
## Sınırlılıklar
- [Örneklem, eksik veri, ölçüm, zaman penceresi]
## Sonuç
[2–4 cümle: soruya cevap + önerilen sonraki analiz]
```

`Kaynak`: `1. satislar-2025.csv (12.480×14) - Tanımlayıcı istatistik + zaman serisi`
Etiketler: `Veri Bilimi` ve/veya `Analiz` + konu etiketleri.

## 7. Tekrarlanabilirlik

Kullanılan script'i kısa bir kod bloğu olarak notun sonuna "## Ek: Kod" başlığıyla ekle
(yalnızca ana adımlar, ≤40 satır). Kod bloğu içinde kaçış yapma.
