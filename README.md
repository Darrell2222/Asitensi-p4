# Asitensi-p4

Program ini memiliki struct Barang beranggota char nama[50], int harga, int stock dan struct Member beranggota char nama[50], int poin serta fungsi-fungsi yang berinteraksi dengan struct tersebut.

#Tugas

1.Untuk tugas satu, harga dapat diupdate menggunakan fungsi ini:
updateHarga(&dbBarang[0], 7500);  // Mengubah harga Sabun (indeks 0)
updateHarga(&dbBarang[4], 25000); // Mengubah harga Kopi (indeks 4)
void updateHarga(Barang *b, int hargaBaru) {
    b->harga = hargaBaru; // Memanipulasi data asli menggunakan operator ->
    printf("\n[ADMIN] Harga %s berhasil diupdate menjadi Rp%d\n", b->nama, b->harga);
}

2. Untuk tugas dua, nama barang dapat diupdate menggunakan fungsi ini:
void updateNama(Barang *b, char namaBaru[]) {
    char namaLama[50];
    strcpy(namaLama, b->nama); // Simpan nama lama untuk dicetak
    strcpy(b->nama, namaBaru); // Timpa nama dengan yang baru
    printf("\n[ADMIN] Nama barang '%s' berhasil dikoreksi menjadi '%s'\n", namaLama, b->nama);
}

3. Untuk tugas tiga, 
void tukarPoin(Member *m, int poinDitukar) {
    if (m->poin >= poinDitukar) {
        m->poin -= poinDitukar;
        int diskon = poinDitukar * 100; // Asumsi 1 Poin bernilai diskon Rp100
        printf("\n[MEMBER] %s menukarkan %d Poin. Dapat diskon Rp%d! (Sisa Poin: %d)\n", m->nama, poinDitukar, diskon, m->poin);
    } else {
        printf("\n[GAGAL] Poin %s (Tersisa: %d) tidak cukup untuk ditukar sebanyak %d Poin!\n", m->nama, m->poin, poinDitukar);
    }
}

4. Untuk tuga tambahan (bonus)
int main() {
   
    Barang dbBarang[5] = { {"Sabun", 5000, 10}, {"Sampo", 15000, 5}, {"Roti", 12000, 8}, {"Susu", 25000, 15}, {"Kopi", 22000, 20} };
    Member dbMember[2] = { {"Anisa", 500}, {"Budi", 100} };

    int pilihan, idBarang, idMember, qty;

    printf("=== SELAMAT DATANG DI MINIMARKET ===\n");

    while (1) {
        // Tampilan Menu
        printf("\n=== MENU UTAMA ===\n");
        printf("[1] Lihat Barang\n");
        printf("[2] Cek Member\n");
        printf("[3] Beli Barang\n");
        printf("[4] Keluar\n");
        printf("Pilih menu (1-4): ");
        scanf("%d", &pilihan);


     if (pilihan == 4) {
            printf("\nTerima kasih telah berbelanja!\n");
            break; // Perintah break di sini akan menghentikan loop while(1)
        }
        switch (pilihan) {
            case 1:
                cekBarang(dbBarang, 5);
                break;
            case 2:
                cekMember(dbMember, 2);
                break;     
            case 3:
                printf("\n--- FORM PEMBELIAN ---\n");
                printf("Pilih Nomor Barang (1-5): ");
                scanf("%d", &idBarang);       
                printf("Pilih Nomor Member (1-2, ketik 0 jika bukan member): ");
                scanf("%d", &idMember);
                printf("Masukkan Jumlah Beli: ");
                scanf("%d", &qty);
                if (idBarang >= 1 && idBarang <= 5) {
                    if (idMember >= 1 && idMember <= 2) {
                        beliBarang(&dbBarang[idBarang - 1], &dbMember[idMember - 1], qty);
                    } else {
                        beliBarang(&dbBarang[idBarang - 1], NULL, qty); // Pembeli non-member
                    }
                } else {
                    printf("\n[ERROR] Nomor barang tidak valid!\n");
                }
                break;
            default:
                printf("\n[ERROR] Pilihan menu tidak tersedia! Silakan coba lagi.\n");
                break;
        }
    }

    return 0;
}
