BAŞLA

// --- 1. Kullanıcı Girişi veya Yeni Hesap Açma ---
1. Kullanıcıdan e-posta ve parola al
2. Eğer e-posta sistemde kayıtlı değilse
       Yazdır("Kullanıcı bulunamadı")
       Yazdır("Yeni hesap açmak ister misiniz? (E/H)")
       cevap = Kullanıcıdan giriş al
       Eğer cevap == "E" ise
             isim = Kullanıcıdan isim al
             soyisim = Kullanıcıdan soyisim al
             yeni_parola = Kullanıcıdan parola al
             YeniHesapOluştur(isim, soyisim, e-posta, yeni_parola)
             Yazdır("Hesabınız oluşturuldu, giriş yapabilirsiniz.")
             kullanıcı_id = GirişYapanKullanıcıID()
       Değilse
             Yazdır("Giriş yapılmadı, işlem sonlandırıldı.")
             Bitir
3. Eğer parola yanlışsa
       Yazdır("Hatalı parola")
       Bitir
4. Oturum başlat
       kullanıcı_id = GirişYapanKullanıcıID()

// --- 2. Ürün Seçme ve Stok Kontrolü ---
5. Kullanıcıya ürün listesi göster
6. Kullanıcı ürün_id ve miktar seçer
7. StokKontrol(ürün_id, miktar)
       Eğer stok yetersizse
           Yazdır("Yeterli stok yok")
           Bitir
       Değilse devam et

// --- 3. Ürünü Sepete Ekleme ---
8. Eğer seçilen ürün sepette yoksa
       SepeteEkle(kullanıcı_id, ürün_id, miktar)
   Değilse
       Sepetteki miktarı güncelle
9. Yazdır("Ürün sepete eklendi")

// --- 4. İndirim Kodu Uygulama ---
10. Kullanıcıya "İndirim kodun var mı?" diye sor
11. Eğer kullanıcı kod girmek istiyorsa
        kod = Kullanıcıdan kod al
        Eğer KuponGeçerliMi(kod) ise
              İndirimiHesapla(kod)
              Yazdır("İndirim uygulandı")
        Değilse
              Yazdır("Kod geçersiz veya süresi dolmuş")

// --- 5. Kargo Hesaplama ---
12. Kullanıcıdan teslimat adresi al
13. KargoYöntemleriniListele()
14. Kullanıcı bir kargo yöntemi seçer
15. KargoTutarı = KargoHesapla(sepet, seçilen_kargo)
16. Yazdır("Kargo ücreti: ", KargoTutarı)

// --- 6. Sepet Toplamını Hesaplama ---
17. AraToplam = SepettekiÜrünFiyatlarınıTopla()
18. Toplamİndirim = Hesaplananİndirim()
19. Vergi = (AraToplam - Toplamİndirim) * 0.18
20. GenelToplam = AraToplam - Toplamİndirim + KargoTutarı + Vergi
21. Yazdır("Toplam ödenecek tutar: ", GenelToplam)

// --- 7. Ödeme Aşaması ---
22. Kullanıcıdan ödeme yöntemi seçmesini iste
       (Kredi kartı, havale vb.)
23. ÖdemeSonucu = ÖdemeYap(kullanıcı_id, GenelToplam)
24. Eğer ÖdemeSonucu == "Başarılı" ise
         Yazdır("Ödeme başarılı")
     Değilse
         Yazdır("Ödeme başarısız, tekrar deneyin")
         Bitir

// --- 8. Sipariş Oluşturma ve Stok Güncelleme ---
25. SiparişOluştur(kullanıcı_id, sepet, adres, GenelToplam)
26. Her ürün için
        StokAzalt(ürün_id, miktar)
27. SepetiTemizle(kullanıcı_id)
28. Yazdır("Sipariş oluşturuldu. Teşekkür ederiz!")

// --- 9. Bildirim ve Onay ---
29. Kullanıcıya e-posta ile sipariş özeti gönder
30. Sipariş durumunu "Hazırlanıyor" olarak işaretle

BİTİR
