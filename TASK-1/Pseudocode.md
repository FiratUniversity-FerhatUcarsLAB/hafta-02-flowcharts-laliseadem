BAŞLA

1. Kart takılır
2. PIN deneme sayısı = 0

3. TEKRARLA
      3.1 PIN'i kullanıcıdan al
      3.2 Eğer PIN doğruysa
              Devam et
          DEĞİLSE
              PIN deneme sayısı = PIN deneme sayısı + 1
              Eğer PIN deneme sayısı = 3 ise
                   Kartı bloke et
                   MESAJ: "Kartınız bloke olmuştur."
                   DUR
              Aksi halde MESAJ: "Hatalı PIN, tekrar deneyiniz."
   PIN doğru olana kadar veya 3 deneme dolana kadar döngü devam eder

4. Bakiye = Hesaptaki bakiye öğren
5. MESAJ: "Bakiyeniz: " + Bakiye

6. Çekilmek istenen tutarı gir
7. Eğer (Tutar > Bakiye) ise
        MESAJ: "Yetersiz bakiye"
        DUR

8. Eğer (Tutar 20 TL’nin katı değilse)
        MESAJ: "Tutar 20 TL’nin katı olmalı"
        DUR

9. Eğer (Tutar günlük limitten büyükse)
        MESAJ: "Günlük limit aşıldı"
        DUR

10. Bakiye = Bakiye - Tutar
11. Para ver
12. Fiş yazdır

13. MESAJ: "Lütfen paranızı ve kartınızı alınız."

14. Kullanıcıya sor: "Başka işlem yapmak ister misiniz? (E/H)"
15. Eğer cevap = "E" ise
        İşlemleri başa döndür
    DEĞİLSE
        MESAJ: "Teşekkürler, iyi günler."
        DUR

BİTİR
