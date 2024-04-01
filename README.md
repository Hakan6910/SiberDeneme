# SiberDeneme

#include <iostream>
#include <vector>
#include <string>
#include <algorithm>

using namespace std;

// Öğrenci sınıfı tanımlaması
class Ogrenci {
public:
    string ad;
    string soyad;
    int notu;

    // Kurucu fonksiyon
    Ogrenci(string a, string s, int n) : ad(a), soyad(s), notu(n) {}

    // Bilgileri ekrana yazdıran fonksiyon
    void bilgileriYazdir() {
        cout << "Ad: " << ad << ", Soyad: " << soyad << ", Not: " << notu << endl;
    }
};

// Not yönetim sistemi sınıfı tanımlaması
class NotYonetimSistemi {
private:
    vector<Ogrenci> ogrenciler;

public:
    // Yeni öğrenci eklemek için fonksiyon
    void ogrenciEkle(string ad, string soyad, int notu) {
        Ogrenci yeniOgrenci(ad, soyad, notu);
        ogrenciler.push_back(yeniOgrenci);
    }

    // Öğrenci bilgilerini güncellemek için fonksiyon
    void ogrenciGuncelle(string ad, string soyad, int notu) {
        for (int i = 0; i < ogrenciler.size(); ++i) {
            if (ogrenciler[i].ad == ad && ogrenciler[i].soyad == soyad) {
                ogrenciler[i].notu = notu;
                cout << "Ogrenci bilgileri guncellendi." << endl;
                return;
            }
        }
        cout << "Ogrenci bulunamadi." << endl;
    }

    // Öğrenci notlarını silmek için fonksiyon
    void ogrenciSil(string ad, string soyad) {
        for (int i = 0; i < ogrenciler.size(); ++i) {
            if (ogrenciler[i].ad == ad && ogrenciler[i].soyad == soyad) {
                ogrenciler.erase(ogrenciler.begin() + i);
                cout << "Ogrenci silindi." << endl;
                return;
            }
        }
        cout << "Ogrenci bulunamadi." << endl;
    }

    // Öğrenci bilgilerini listelemek için fonksiyon
    void ogrenciListele() {
        for (const auto& ogrenci : ogrenciler) {
            ogrenci.bilgileriYazdir();
        }
    }
};

int main() {
    NotYonetimSistemi notSistemi;

    // Örnek öğrencileri ekleyelim
    notSistemi.ogrenciEkle("Ali", "Yılmaz", 85);
    notSistemi.ogrenciEkle("Ayşe", "Demir", 70);
    notSistemi.ogrenciEkle("Ahmet", "Kaya", 90);

    // Tüm öğrenci bilgilerini listeleme
    cout << "Tum ogrenci bilgileri:" << endl;
    notSistemi.ogrenciListele();
    cout << endl;

    // Bir öğrencinin notunu güncelleme
    notSistemi.ogrenciGuncelle("Ali", "Yılmaz", 90);

    // Güncellenmiş öğrenci bilgilerini listeleme
    cout << "Guncellenmis ogrenci bilgileri:" << endl;
    notSistemi.ogrenciListele();
    cout << endl;

    // Bir öğrenciyi silme
    notSistemi.ogrenciSil("Ayşe", "Demir");

    // Silinmiş öğrenci bilgilerini listeleme
    cout << "Silinmis ogrenci bilgileri:" << endl;
    notSistemi.ogrenciListele();
    cout << endl;

    return 0;
}
