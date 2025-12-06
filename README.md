#include <iostream>
#include <string>
using namespace std;

// Fonksiyon tanimi
string ucusGuvenligiKontrol(int yuk, int hiz, int yukseklik) {
    int pil = 100; // Baslangic pil seviyesi
    pil -= (hiz / 10) * 5; // Hiz degerine gore pil azalmasi

    // Pil seviyesini yazdir
    cout << "Hesaplanan pil seviyesi: " << pil << endl;

    // 1. Yuk kontrolu
    if (yuk > 500) {
        return "Agir yuk, ucamaz!";
    }
    // 2. Pil seviyesi kontrolu
    else if (pil < 30) {
        return "Pil seviyesi dusuk, ucus guvensiz!";
    }
    // 3. Yukseklik kontrolu
    else if (yukseklik > 200) {
        return "Radar disi, ucus guvensiz!";
    }
    else if (yukseklik < 20) {
        return "Yukseklik guvensiz, ucus guvensiz!";
    }
    // Tum kosullar uygunsa
    else {
        return "Ucus guvenli!";
    }
}

// 2.3 Yuk dizisini siralama fonksiyonu (bubble sort)
void siralaYuk(int dizi[], int boyut) {
    for (int i = 0; i < boyut - 1; i++) {
        for (int j = 0; j < boyut - i - 1; j++) {
            if (dizi[j] > dizi[j + 1]) {
                int temp = dizi[j];
                dizi[j] = dizi[j + 1];
                dizi[j + 1] = temp;
            }
        }
    }
}



// 2.3 Yuk arama fonksiyonu (linear search)
int araYuk(int dizi[], int boyut, int aranan) {
    for (int i = 0; i < boyut; i++) {
        if (dizi[i] == aranan) {
            return i; // bulundugu indexi dondur
        }
    }
    return -1; // bulunamadi
}

int main() {
    const int droneSayisi = 7;
    int yukler[droneSayisi] = {350, 600, 200, 450, 500, 100, 400};
    int hizlar[droneSayisi] = {40, 30, 80, 20, 50, 60, 155};
    int yukseklikler[droneSayisi] = {50, 70, 150, 10, 210, 180, 90};
    string durumlar[droneSayisi];

    cout << "=== Mini Drone Surusu Ucus Guvenligi Programi ===" << endl;

    // Her drone icin ucus guvenligini kontrol et
    for (int i = 0; i < droneSayisi; i++) {
        durumlar[i] = ucusGuvenligiKontrol(yukler[i], hizlar[i], yukseklikler[i]);
    }




    cout << "\n--- Drone Surusu Ucus Durumlari ---" << endl;
    for (int i = 0; i < droneSayisi; i++) {
        cout << "Drone " << i + 1 << ": " << durumlar[i] << endl;
    }

    // 2.3 Siralama ve arama islemleri
    cout << "\n--- Yuk Dizisini Sirala ---" << endl;
    siralaYuk(yukler, droneSayisi);
    for (int i = 0; i < droneSayisi; i++) {
        cout << i + 1 << ". siradaki Drone yuk: " << yukler[i] << endl;
    }

    // Yuk arama
    int arananYuk;
    cout << "\nAramak istediginiz yuk degerini giriniz: ";
    cin >> arananYuk;

    int bulunanIndex = araYuk(yukler, droneSayisi, arananYuk);
    if (bulunanIndex != -1) {
        cout << "Yuk degeri bulundu. Drone indeks: " << bulunanIndex << endl;
    } else {
        cout << "Yuk degeri dizide bulunamadi." << endl;
    }

    return 0;
}
