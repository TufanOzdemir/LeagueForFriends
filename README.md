# LeagueForFriends

Bu projenin amacı arkadaşlarınız ile FIFA, PES veya EA FC gibi oyunları oynarken rekabeti artırmak ve eğlenceyi katlamaktır. İçerisindeki sistem tamamıyla eğlence amaçlıdır.

**⚽ Puan Tutucu** bu amaçla yapılmış lig ve puan takip uygulamasıdır (Android). Tek telefondan kullanılır; internet ve hesap gerektirmez.

## Özellikler

- **Oyuncular:** İstenen sayıda oyuncu; lig sürerken de eklenebilir.
- **Lig formatı:** Çift devre, tek devre veya serbest. Puanlama ayarlanabilir (varsayılan 3/1/0).
- **Puan durumu:** O, G, B, M, averaj, puan, son 5 maç formu, sıradaki maç ve tablo paylaşımı.
- **İstatistik:** Gol kralı, en iyi savunma, seriler, ikili rekabet, tüm zamanlar tablosu.
- **İddia (isteğe bağlı, sanal para):**
  - Başlangıç parası ve maç başı kazançlar lig kurulurken belirlenir.
  - Sadece oynanmamış maçlara 1 / X / 2 kuponu oynanır.
  - Oranlar puan, averaj, form, ev sahibi avantajı ve ikili rekabetten hesaplanır; 1.10–8.00 arasında kalır.
  - Bahisçiler maç yapmadan iddia oynar, oynanan her maç için para kazanır (varsayılan 100 ₺).
  - Para gönderilebilir veya harcanabilir; işlemler geri alınabilir.
- **Yedekleme:** Veriler telefonda tutulur; JSON olarak dışa/içe aktarılır.

> Uygulamadaki para sanaldır; gerçek para veya ödeme içermez.

## Kurulum

APK'yı [Releases](../../releases) sayfasından indirip telefonda açın. Android 7 veya üstü gerekir; "bilinmeyen kaynak" izni istenebilir.

## Geliştirme

Arayüzün tamamı `www/index.html` dosyasındadır (HTML/CSS/JS). Android kabuğu [Capacitor](https://capacitorjs.com) ile sağlanır.

Gerekenler: Node.js, JDK 21, Android SDK 36.

```bash
npm ci
npx cap sync android
cd android && ./gradlew assembleRelease
```

`android/keystore.properties` yoksa çıkan APK imzasız olur ve telefona kurulmaz.

## Sürüm çıkarma

`v*` etiketi gönderildiğinde GitHub Actions imzalı APK'yı derleyip Release'e ekler:

```bash
git tag v1.2.1 && git push origin v1.2.1
```

Önce `android/app/build.gradle` içindeki `versionCode` ve `versionName` artırılmalıdır.

### Gerekli GitHub Secrets

| Secret | İçerik |
| --- | --- |
| `KEYSTORE_BASE64` | `puantutucu.keystore` dosyasının base64 hali |
| `KEYSTORE_PASSWORD` | Keystore şifresi |
| `KEY_ALIAS` | Anahtar adı |
| `KEY_PASSWORD` | Anahtar şifresi |

İmza anahtarı ve şifreleri repoda tutulmaz (`.gitignore`). Anahtar kaybolursa yeni sürümler eskisinin üzerine kurulamaz; ayrıca güvenli bir yerde yedekleyin.
