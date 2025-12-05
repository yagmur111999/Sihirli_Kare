def sihirli_kare_olustur(n):
    """
    Tek sayı boyutunda sihirli kare oluşturur.
    
    Kurallar:
    1. Sayılar 1'den n*n'ye kadar
    2. 1 sayısı ilk satırın orta sütununa yerleştirilir
    3. Sonraki sayı: bir yukarı ve bir sola
    4. İstisna: Eğer hücre doluysa, son sayının bir alt satırına yerleştir
    """
    
    # n x n boyutunda sıfırlarla dolu kare oluştur
    kare = [[0 for _ in range(n)] for _ in range(n)]
    
    # 1 sayısını ilk satırın ortasına yerleştir
    satir = 0
    sutun = n // 2
    
    # 1'den n*n'ye kadar sayıları yerleştir
    for sayi in range(1, n * n + 1):
        kare[satir][sutun] = sayi
        
        # Bir sonraki pozisyonu hesapla (bir yukarı, bir sola)
        yeni_satir = (satir - 1) % n  # Küre gibi döner (üstten alta)
        yeni_sutun = (sutun - 1) % n  # Küre gibi döner (soldan sağa)
        
        # İstisna: Eğer hücre doluysa, son sayının bir alt satırına git
        if kare[yeni_satir][yeni_sutun] != 0:
            yeni_satir = (satir + 1) % n
            yeni_sutun = sutun
        
        satir = yeni_satir
        sutun = yeni_sutun
    
    return kare


def kareyi_yazdir(kare):
    """Sihirli kareyi düzgün formatta yazdırır"""
    n = len(kare)
    max_sayi = n * n
    genislik = len(str(max_sayi)) + 1
    
    for satir in kare:
        for sayi in satir:
            print(f"{sayi:>{genislik}}", end=" ")
        print()


def toplam_kontrol(kare):
    """Sihirli karenin doğruluğunu kontrol eder"""
    n = len(kare)
    sihirli_toplam = n * (n * n + 1) // 2
    
    print(f"\nSihirli Toplam: {sihirli_toplam}")
    print("\nKontrol:")
    
    # Satır toplamları
    print("Satır toplamları:", end=" ")
    for satir in kare:
        print(sum(satir), end=" ")
    print()
    
    # Sütun toplamları
    print("Sütun toplamları:", end=" ")
    for j in range(n):
        toplam = sum(kare[i][j] for i in range(n))
        print(toplam, end=" ")
    print()
    
    # Köşegen toplamları
    ana_kosegen = sum(kare[i][i] for i in range(n))
    ters_kosegen = sum(kare[i][n-1-i] for i in range(n))
    print(f"Ana köşegen: {ana_kosegen}")
    print(f"Ters köşegen: {ters_kosegen}")


# Ana program
if __name__ == "__main__":
    print("=== SİHİRLİ KARE OLUŞTURUCU ===\n")
    
    while True:
        try:
            n = int(input("Karenin boyutunu girin (tek sayı): "))
            
            if n % 2 == 0:
                print("Lütfen tek sayı girin!")
                continue
            
            if n < 1:
                print("Lütfen pozitif bir sayı girin!")
                continue
            
            break
        except ValueError:
            print("Lütfen geçerli bir sayı girin!")
    
    print(f"\n{n}x{n} Sihirli Kare:\n")
    
    # Sihirli kareyi oluştur
    kare = sihirli_kare_olustur(n)
    
    # Kareyi yazdır
    kareyi_yazdir(kare)
    
    # Toplamları kontrol et
    toplam_kontrol(kare)
