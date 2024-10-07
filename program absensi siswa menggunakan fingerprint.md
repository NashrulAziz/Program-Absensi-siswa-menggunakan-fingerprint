# Program-Absensi-siswa-menggunakan-fingerprint
#include <iostream>
#include <vector>
#include <ctime>
#include "Siswa.hpp"

using namespace std;

// Fungsi untuk mengambil waktu saat ini
stirng getCurrentTime() {
time_t now = time(0);
    char* dt = ctime(&now);
    return string(dt);
}

void tampilkanMenu() {
    cout << "===== Program Absensi Siswa =====\n";
    cout << "1. Tambah Siswa\n";
    cout << "2. Absensi Siswa (Fingerprint)\n";
    cout << "3. Lihat Data Absensi\n";
    cout << "4. Keluar\n";
    cout << "Pilih menu: ";
}

void tambahSiswa(vector<Siswa>& daftarSiswa) {
    string nama;
    int id;
    cout << "Masukkan ID Siswa: ";
    cin >> id;
    cout << "Masukkan Nama Siswa: ";
    cin >> nama;
    Siswa siswaBaru(id, nama);
    daftarSiswa.push_back(siswaBaru);
    cout << "Siswa berhasil ditambahkan!\n";
}

void absensiSiswa(vector<Siswa>& daftarSiswa) {
    int id;
    cout << "Scan Fingerprint (Masukkan ID Siswa): ";
    cin >> id;
    bool found = false;
    for (auto& siswa : daftarSiswa) {
        if (siswa.getID() == id) {
            string waktu = getCurrentTime();
            siswa.absensi(waktu);

            // Simpan ke file
            ofstream file("absensi.txt", ios::app);
            if (file.is_open()) {
                file << "ID: " << siswa.getID() << ", Nama: " << siswa.getNama() << ", Waktu: " << waktu;
                file.close();
            }

            cout << "Absensi berhasil untuk " << siswa.getNama() << " pada " << waktu;
            found = true;
            break;
        }
    }
    if (!found) {
        cout << "Siswa dengan ID tersebut tidak ditemukan!\n";
    }
}

void lihatDataAbsensi() {
    ifstream file("absensi.txt");
    string line;
    if (file.is_open()) {
        cout << "===== Data Absensi =====\n";
        while (getline(file, line)) {
            cout << line << endl;
        }
        file.close();
    } else {
        cout << "Belum ada data absensi.\n";
    }
}

int main() {
    vector<Siswa> daftarSiswa;
    int pilihan;
    do {
        tampilkanMenu();
        cin >> pilihan;
        if (pilihan == 1) {
            tambahSiswa(daftarSiswa);
        } else if (pilihan == 2) {
            absensiSiswa(daftarSiswa);
        } else if (pilihan == 3) {
            lihatDataAbsensi();
        } else if (pilihan == 4) {
            cout << "Terima kasih telah menggunakan program absensi siswa.\n";
        } else {
            cout << "Pilihan tidak valid, coba lagi.\n";
        }
    } while (pilihan != 4);

    return 0;
}
#ifndef SISWA_HPP
#define SISWA_HPP

#include <iostream>
#include <string>

using namespace std;

class Siswa {
private:
    int id;
    string nama;
    string waktuAbsensi;

public:
    Siswa(int i, string n) : id(i), nama(n), waktuAbsensi("") {}

    int getID() const {
        return id;
    }

    string getNama() const {
        return nama;
    }

    void absensi(string waktu) {
        waktuAbsensi = waktu;
    }

    string getWaktuAbsensi() const {
        return waktuAbsensi;
    }
};

#endif
ID: 101, Nama: Budi, Waktu: Mon Oct  7 10:00:00 2024
ID: 102, Nama: Ani, Waktu: Mon Oct  7 10:05:00 2024

