BAŞLA

Sistem_Aktif = DOĞRU   // kullanıcı tarafından ayarlanabilir

TEKRARLA
    EĞER Sistem_Aktif = DOĞRU ise
        YAZ "Akıllı Ev Güvenlik Sistemi başlatıldı."

        // Sonsuz izleme döngüsü
        TEKRARLA
            // Sensör verilerini oku
            Hareket_Sensoru = okuHareketSensoru()
            Kapi_Pencere_Sensoru = okuKapiPencereSensoru()
            Kamera = okuKameraDurumu()
            Ev_Sahibi_Evde = kontrolEvSahibiDurumu()

            // Tehdit kontrolü
            EĞER Hareket_Sensoru = ALGILANDI veya 
                 Kapi_Pencere_Sensoru = AÇIK veya 
                 Kamera = HAREKET_GÖRÜLDÜ ise
                 
                 Tehdit = DOĞRU
                 YAZ "Tehdit algılandı!"
            DEĞİLSE
                 Tehdit = YANLIŞ
                 YAZ "Her şey normal, sistem izleme modunda."
            SON

            // Eğer tehdit varsa kontrol başlar
            EĞER Tehdit = DOĞRU ise
                EĞER Ev_Sahibi_Evde = DOĞRU ise
                    YAZ "Ev sahibi evde, olası yanlış alarm."
                    Alarm_Seviyesi = 1
                    Gönder_Bildirim("Olası yanlış alarm - Ev sahibi evde.")
                DEĞİLSE
                    // Alarm seviyesi belirleme
                    EĞER Kapi_Pencere_Sensoru = AÇIK ise
                        Alarm_Seviyesi = 3
                    DEĞİLSE EĞER Kamera = HAREKET_GÖRÜLDÜ ise
                        Alarm_Seviyesi = 2
                    DEĞİLSE
                        Alarm_Seviyesi = 1
                    SON

                    // Alarm ve bildirimler
                    YAZ "Alarm seviyesi: " + Alarm_Seviyesi
                    Gönder_SMS("Alarm seviyesi: " + Alarm_Seviyesi)
                    Gönder_App_Bildirim("Alarm seviyesi: " + Alarm_Seviyesi)
                    Gönder_Email("Alarm seviyesi: " + Alarm_Seviyesi)

                    // Bekle ve tekrar kontrol et
                    BEKLE(10 saniye)
                    Yeni_Durum = okuHareketSensoru()

                    EĞER Yeni_Durum = SAKİN ise
                        YAZ "Tehdit ortadan kalktı, alarm sıfırlandı."
                    DEĞİLSE
                        YAZ "Tehdit devam ediyor, alarm aktif kalıyor."
                    SON
                SON
            SON

            BEKLE(5 saniye)
        SONSUZA_KADAR

    DEĞİLSE
        YAZ "Sistem devre dışı. Aktifleştirme bekleniyor..."
        BEKLE(5 saniye)
    SON

SONSUZA_KADAR
BİTİR
