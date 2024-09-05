# pythonodev2
import math  #matematiksel işlemler için math kütüphanesi ekledim.

# Bölge katsayıları
global bolge_katsayısı   # bölge katsayısı global değişken olarak tanımlandı.
deniz_kenari_katsayisi = 2
sehir_merkezi_katsayisi = 1.5
kirsal_katsayisi = 0.75

# Dış cephe tasarım puanlama fonksiyonları
def puanlama_modern(girilen_deger):          #modern dış cepce hesaplamsı yapılır.
    return girilen_deger * girilen_deger

def puanlama_geleneksel(girilen_deger):    # geleneksel için hesaplama yapar.
    return girilen_deger * math.pi

def puanlama_eski(girilen_deger):   #eski için hesaplama yapar
    return girilen_deger * math.exp(1)

 #ayrı fonksiyon içinde dış cephe hesaplamasını yapar.
def dis_cephe_fiyati(bolge_katsayisi, puanlama):   
    return bolge_katsayisi * puanlama * 500

# İç mekan fiyatını hesaplayan fonksiyon
def ic_cephe_fiyati(en, boy, duzenleme_katsayisi):  
    metre_kare = en * boy    #metre kare hesabı yapılır.
    return metre_kare * duzenleme_katsayisi * 1000

# Main fonksiyonu
def main():   
    dis_cephe_fiyatlari = []  #dış cephe ve iç cephe için listeler oluştururuz.
    ic_cephe_fiyatlari = []
    
    while True:  #eğer döngü doğruysa kullanıcıdan dış cephe tasarımı için değerler alınır.
        print("Dış Cephe Tasarımını Yapınız:")   
        print("1. Modern")       
        print("2. Geleneksel")      
        print("3. Eski")       
        secim = int(input("Seçiminizi yapın (1-3): "))  #1 ile 3 arasında seçim yapması istenir.
      
        if secim == 1:
            puanlama = puanlama_modern  # seçim1e eşitse modern puanlama yapılır.
        elif secim == 2:
            puanlama = puanlama_geleneksel #seçim 2 ise geleneksel puanlama yapılır.
        elif secim == 3:
            puanlama = puanlama_eski  # seçim 3 ise eski puanlama yapılır.
        else:
            print("Geçersiz seçim.Lütfen 1 ile 3 arasında bir değer girin!.")  #eğer 1-3 dışında değer girerse kullanıcıya tekrar sorar
            continue
        
        bolge_secim = input("Bölge seçimi (deniz/sehir/kirsal): ") #kullanıcıdan bölge seçimi yapması istenir.
      
        if bolge_secim == "deniz":
            bolge_katsayisi = deniz_kenari_katsayisi  #bölge seçimi denizse denizkenarı katsayısı alınır.
        elif bolge_secim == "sehir":    
            bolge_katsayisi = sehir_merkezi_katsayisi #bölge seçimi şehirse şehirkatsayısı alınır.
        elif bolge_secim == "kirsal":        
            bolge_katsayisi = kirsal_katsayisi    #bölge seçimi kırsalsa kırsal katsayısı alınır.
        else:           
            print("Geçersiz bölge seçimi. Lütfen deniz,sehir,kirsal' dan birini seçiniz.Program başa döndü!")  #eğer bunlar harici değer girerse kullanıcıya sorular baştan sorulur.
            continue
        
        girilen_deger = float(input("Puanlama İçin Değer Girin: ")) #kullanıcıdan puanlama için değer girmesi istenir.
        puanlama_sonucu = puanlama(girilen_deger) #girilen değerle puanlama fonk çağırılarak hesaplama yapılır.
        dis_cephe_fiyat = dis_cephe_fiyati(bolge_katsayisi, puanlama_sonucu) #dış cephe fiyatı fonksiyonu çağırılır hesaplama yapılır.
        dis_cephe_fiyatlari.append(dis_cephe_fiyat) #bulunan sonuç listeye eklenir.

        en = float(input("İç cephe en (metre): "))#kullanıcıdan en değeri istenir.
        boy = float(input("İç cephe boy (metre): ")) #kullanıcıdan boy değeri istenir.

        print("İç Mekan Düzenleme Seçiminizi Yapın.")  #iç mekan düzenlemeri ekranda gösterilirç
        print("1. Luks")    
        print("2. Guzel")     
        print("3. Idare Eder")

        duzenleme_secim = int(input("Düzenleme seçiminizi yapın (1-3): ")) #seçim kullanıcıdan alınır.
        if duzenleme_secim == 1:
            duzenleme_katsayisi = 5 #seçim 1e eşitse düz.katsayısı 5 alınır.
        elif duzenleme_secim == 2:
            duzenleme_katsayisi = 3  #seçim 2ye eşitse düz.katsayısı 3 alınır.
        elif duzenleme_secim == 3:
            duzenleme_katsayisi = 1.5  #seçim 3e eşitse düz.katsayısı 1.5 alınır.
        else:         
            print("Geçersiz düzenleme seçimi. Lütfen tekrar seçim yapın.") #gecersiz giriş yapılırsa sorular baştan tekrar sorulur.
            continue
      
        ic_cephe_fiyat = ic_cephe_fiyati(en, boy, duzenleme_katsayisi) #iç cephe fiyat fonk.gider hesaplama yapr.
        ic_cephe_fiyatlari.append(ic_cephe_fiyat)  #bulunan sonuç iç cephe listesine eklenir.
      
        devam_etme = input("Başka bir hesaplama yapmak ister misiniz? (h/H ile çıkış, e ile devam): ")  #devam edip etmek istemediği sorulur.  
        if devam_etme.lower() == 'h': #kullanıcı h ye basarsa program sonlanır.
            break
    
    for i in range(len(dis_cephe_fiyatlari)):#for döngüsü,dis_cephe_fiyatlari listesinin eleman sayısı kadar döndürür.i liste indeksi olarak kullanılır.
          print(f"{i+1}. Ev Fiyatı: {dis_cephe_fiyatlari[i]*40 + ic_cephe_fiyatlari[i]*60}") #girilen ev fiyatları tek tek hesaplanır.
    if dis_cephe_fiyatlari and ic_cephe_fiyatlari:# eğer dış ve iç cephe fiyatları oluştuysa bu kısım çalışır.
        ortalama_ev_fiyati = (sum(dis_cephe_fiyatlari) / len(dis_cephe_fiyatlari)) * 40 + (sum(ic_cephe_fiyatlari) / len(ic_cephe_fiyatlari)) * 60    #girilen evlerin ortalaması hesaplanır.
        print(f"Ortalama ev fiyatı: {ortalama_ev_fiyati}")   #ortalama ev fiyatı ekrana yazdırılır.

if __name__ == "__main__": #Python'ın dosya modül olarak mı direk mi çalıştırıldığını kontrol eder.
    main()
