#include <iostream>
#include <cmath>
using namespace std;

int JUMLAH_BULAN = 12;
int main() {
    float luas , efisiensi, intensitas, energi[24];
    char pilihan;
    
    float produksiSurya[JUMLAH_BULAN];
    float konsumsiRumah[JUMLAH_BULAN];

    cout << "Program by: Gazza Alkaromi, Septy Angel, Anita Sari\n";
    cout <<"\n";
    cout << "=== Simulasi Panel Surya ===\n";
    cout << "Pilih salah satu:\n";
    cout << "a. Hitung Energi\n";
    cout << "b. Menghitung Data Energi Tahunan yang dihasilkan panel surya terhadap penggunanaa rumah tangga\n";
    cout << "Pilihan: ";
    cin >> pilihan;
    
    switch(pilihan) {
        case 'a':
            // Hitung Energi
            cout << "Masukkan luas panel (m2): ";
            cin >> luas;
            cout << "Masukkan efisiensi panel (%): ";
            cin >> efisiensi;
            cout << "Masukkan intensitas cahaya (W/m2): ";
            cin >> intensitas;
            
            for(int i = 0; i < 24; i++) {
                energi[i] = (luas * efisiensi / 100) * intensitas * sin(((i + 6) % 24) * M_PI / 12);
            }
            
            cout << "output energi per jam:\n";
            for(int i = 0; i < 24; i++) {
                cout << "Jam " << i << ": " << energi[i] << " Wh\n";
            }
            cout<< "note: hasil yang bernilai negatif dianggap 0 atau tidak menghasilkan dan jam ke 0 merupakan jam 12 siang \n";
            break;
            
        case 'b':
            cout << "Simulator Grid Terdesentralisasi: Manajemen Energi Terbarukan dengan Panel Surya" << endl;

              // bagian Memasukkan data produksi energi dari panel surya
            for (int i = 0; i < JUMLAH_BULAN; i++) {
                cout << "Masukkan produksi energi dari panel surya untuk bulan " << i+1 << " (kWh): ";
                cin >> produksiSurya[i];
            }

              // bagian Memasukkan data konsumsi energi rumah tangga
            for (int i = 0; i < JUMLAH_BULAN; i++) {
                cout << "Masukkan konsumsi energi rumah tangga untuk bulan " << i+1 << " (kWh): ";
                cin >> konsumsiRumah[i];
            }

             // program menghitung total produksi energi terbarukan dan total konsumsi energi
            float totalProduksi = 0;
            float totalKonsumsi = 0;

            for (int i = 0; i < JUMLAH_BULAN; i++) {
            totalProduksi += produksiSurya[i];
            totalKonsumsi += konsumsiRumah[i];
            }

            //program bagian hasil
            cout << "--------------------------------------------" << endl;
            cout << "Hasil Simulasi: " << endl;
            cout << "Total Produksi Energi Terbarukan: " << totalProduksi << " kWh" << endl;
            cout << "Total Konsumsi Energi: " << totalKonsumsi << " kWh" << endl;

            if (totalProduksi > totalKonsumsi) {
            cout << "Surplus Energi: " << totalProduksi - totalKonsumsi << " kWh" << endl;
            } else if (totalProduksi < totalKonsumsi) {
            cout << "Kekurangan Energi: " << totalKonsumsi - totalProduksi << " kWh" << endl;
            } else {
            cout << "Tidak ada surplus energi atau kekurangan energi" << endl;
            }
    
            cout << "--------------------------------------------" << endl;
            }
    
        return 0;
}
