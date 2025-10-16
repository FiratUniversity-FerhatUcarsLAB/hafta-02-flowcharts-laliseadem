BAŞLA

1. ÖğrenciNo ve Şifreyi al
2. Eğer ÖğrenciNo ve Şifre doğruysa
       DersListesi <- TümDersleriGöster
       ToplamKredi <- 0
       SeçilenDersler <- BoşListe

       TEKRARLA
            DersSeç <- KullanıcıdanDersSeçimiAl
            Eğer DersSeç = "Çıkış" ise
                  ÇIKIŞ YAP
            Eğer Kontenjan(DersSeç) doluysa
                  Yazdır "Kontenjan dolu, başka ders seçiniz"
                  DEVAM ET
            Eğer ÖnKoşulSağlanmadı(DersSeç) ise
                  Yazdır "Ön koşul dersi tamamlanmamış"
                  DEVAM ET
            Eğer ZamanÇakışmasıVar(DersSeç, SeçilenDersler) ise
                  Yazdır "Zaman çakışması var, başka ders seçiniz"
                  DEVAM ET
            Eğer (ToplamKredi + Kredi(DersSeç)) > 35 ise
                  Yazdır "Kredi limiti aşıldı"
                  DEVAM ET
            Aksi halde
                  DersEkle(SeçilenDersler, DersSeç)
                  ToplamKredi <- ToplamKredi + Kredi(DersSeç)
                  Yazdır "Ders başarıyla eklendi"

            Kullanıcıya "Başka ders eklemek istiyor musunuz?" sor
       DÖNGÜ SONU (cevap = "Hayır" olana kadar)

       Eğer GPA < 2.5 ise
             Yazdır "Danışman onayı gerekiyor"
             DanışmanOnayı <- Al
             Eğer DanışmanOnayı = "Red" ise
                    Yazdır "Kayıt tamamlanamadı"
                    BİTİR
       KayıtÖzetiGöster(SeçilenDersler, ToplamKredi)
       Yazdır "Kayıt başarıyla tamamlandı"

Aksi halde
       Yazdır "Geçersiz öğrenci no veya şifre, tekrar deneyiniz"

BİTİR
