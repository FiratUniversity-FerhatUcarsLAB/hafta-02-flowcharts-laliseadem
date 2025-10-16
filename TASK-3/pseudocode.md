BAŞLA

Tekrarla
    Hasta_TC = kullanıcıdan_TC_no_al
    Eğer Hasta_TC geçerliyse
        Çık_döngü
    Değilse
        Yaz "Geçersiz TC Kimlik numarası!"
        Yaz "Tekrar denemek ister misiniz? (E/H)"
        tekrar = kullanıcıdan_girdi_al
        Eğer tekrar = "H" ise
            BİTİR
Döngü_son

Tekrarla
    Yaz "İşlem seçiniz:"
    Yaz "1 - Randevu Al"
    Yaz "2 - Tahlil Sonucu Gör"
    işlem = kullanıcıdan_seçim_al

    Eğer işlem = 1 ise
        Yaz "Poliklinik seçiniz:"
        poliklinik = kullanıcıdan_poliklinik_al
        doktor_listesi = polikliniğe_göre_doktorları_getir
        Yaz doktor_listesi
        doktor = kullanıcıdan_doktor_seç
        uygun_saatler = doktorun_uygun_saatlerini_getir
        Yaz uygun_saatler

        Tekrarla
            saat = kullanıcıdan_saat_seç
            Eğer saat uygun ise
                randevu_oluştur(Hasta_TC, doktor, saat)
                Yaz "Randevunuz onaylandı."
                SMS_gönder(Hasta_TC, randevu_bilgisi)
                Çık_döngü
            Değilse
                Yaz "Seçilen saat dolu, lütfen başka bir saat seçin."
        Döngü_son

    Değilse eğer işlem = 2 ise
        tahlil_var_mı = tahlil_kontrol(Hasta_TC)
        Eğer tahlil_var_mı = EVET ise
            sonuç_hazır_mı = sonuç_kontrol(Hasta_TC)
            Eğer sonuç_hazır_mı = EVET ise
                Yaz "Tahlil Sonuçlarınız:"
                sonuçları_görüntüle(Hasta_TC)
                Yaz "PDF olarak indirmek ister misiniz? (E/H)"
                cevap = kullanıcıdan_girdi_al
                Eğer cevap = "E" ise
                    PDF_oluştur_ve_indir(Hasta_TC)
            Değilse
                Yaz "Tahlil sonuçlarınız henüz hazır değil. Lütfen daha sonra tekrar deneyiniz."
        Değilse
            Yaz "Üzerinize kayıtlı tahlil bulunamadı."

    Değilse
        Yaz "Geçersiz seçim yaptınız."

    Yaz "Başka bir işlem yapmak ister misiniz? (E/H)"
    devam = kullanıcıdan_girdi_al
Döngü devam = "E" olduğu sürece

BİTİR
