
 
### **README - Aplikasi Penghitung Kata**  

---

## **📌 Deskripsi Proyek**  
Aplikasi **Penghitung Kata** adalah program berbasis GUI (Graphical User Interface) yang dibuat dengan **Java NetBeans**. Aplikasi ini berfungsi untuk menghitung jumlah **kata, karakter, dan kalimat** dalam sebuah teks. Selain itu, aplikasi ini juga memiliki fitur tambahan seperti:  
✅ **Menghitung kata & karakter secara real-time** saat mengetik.  
✅ **Mencari jumlah kemunculan kata tertentu dalam teks.**  
✅ **Menyimpan & membuka file teks** untuk menyimpan catatan penting.  

---

## **📂 Fitur Aplikasi**  
### ✨ **1. Menghitung Kata, Karakter, dan Kalimat**  
- **Fungsi utama aplikasi** adalah menghitung jumlah kata, karakter (tanpa spasi), dan kalimat dari teks yang dimasukkan pengguna.  
- **Hitungan diperbarui secara otomatis** setiap kali pengguna mengetik di `jTextArea`.  

### ✨ **2. Pencarian Kata dalam Teks**  
- Pengguna dapat mengetik kata tertentu di `txtCariKata`, lalu klik tombol **Cari Kata**.  
- Aplikasi akan menghitung dan menampilkan jumlah kemunculan kata tersebut dalam teks.  

### ✨ **3. Menyimpan & Membuka File Teks**  
- **Menyimpan teks ke file `.txt`** menggunakan tombol **Simpan File Catatan**.  
- **Membuka file `.txt`** untuk memuat kembali teks yang telah disimpan sebelumnya.  

---

## **📥 Cara Menggunakan Aplikasi**  
### **1️⃣ Menjalankan Aplikasi**
1. **Buka NetBeans**, lalu **jalankan** proyek ini (`Run` -> `Run File`).  
2. Aplikasi akan terbuka dalam bentuk GUI.  

### **2️⃣ Menggunakan Fitur Penghitungan Kata**
1. Ketikkan teks di area `jTextArea`.  
2. Jumlah **kata, karakter, dan kalimat** akan otomatis muncul di bagian kanan.  
3. Klik tombol **HITUNG KATA** jika ingin menghitung ulang secara manual.  

### **3️⃣ Menggunakan Fitur Pencarian Kata**
1. Ketik kata yang ingin dicari di `txtCariKata`.  
2. Klik tombol **Cari Kata**.  
3. Aplikasi akan menampilkan jumlah kemunculan kata tersebut dalam teks.  

### **4️⃣ Menyimpan & Membuka File**
1. **Untuk menyimpan teks**, klik tombol **Simpan File Catatan**, lalu pilih lokasi penyimpanan.  
2. **Untuk membuka file teks**, klik tombol **Buka File Catatan**, lalu pilih file `.txt`.  
3. Isi dari file akan dimuat ke dalam `jTextArea`.  

---

## **⚙️ Teknologi yang Digunakan**
✅ **Java SE (Swing & AWT) untuk GUI**  
✅ **JTextArea untuk input teks**  
✅ **JFileChooser untuk menyimpan & membuka file**  
✅ **JOptionPane untuk notifikasi**  

---

## **📌 Struktur Kode Utama**
### **1️⃣ Menghitung Kata, Karakter, dan Kalimat Secara Real-Time**
Kode ini dipanggil setiap kali pengguna mengetik di `jTextArea`:
```java
private void jTextAreaKeyReleased(java.awt.event.KeyEvent evt) {                                    
    hitungKataDanKarakter();
}   

private void hitungKataDanKarakter() {
    String teks = jTextArea.getText();
    String[] kata = teks.trim().split("\\s+");
    int jumlahKata = (teks.isEmpty()) ? 0 : kata.length;
    int jumlahKarakter = teks.replace(" ", "").length();
    String[] kalimat = teks.split("[.!?]");
    int jumlahKalimat = (teks.isEmpty()) ? 0 : kalimat.length;

    labelHasilKata.setText("Jumlah Kata: " + jumlahKata);
    labelHasilKarakter.setText("Jumlah Karakter: " + jumlahKarakter);
    labelHasilKalimat.setText("Jumlah Kalimat: " + jumlahKalimat);
}
```

### **2️⃣ Pencarian Kata dalam Teks**
Kode untuk mencari kata yang dimasukkan pengguna:
```java
private void btnCariKataActionPerformed(java.awt.event.ActionEvent evt) {                                            
    String teks = jTextArea.getText();
    String kataDicari = txtCariKata.getText().trim();

    if (kataDicari.isEmpty()) {
        JOptionPane.showMessageDialog(this, "Masukkan kata yang ingin dicari!");
        return;
    }

    int count = 0;
    String[] words = teks.split("\\s+");
    for (String word : words) {
        if (word.equalsIgnoreCase(kataDicari)) {
            count++;
        }
    }

    JOptionPane.showMessageDialog(this, "Kata '" + kataDicari + "' ditemukan sebanyak " + count + " kali.");
}
```

### **3️⃣ Simpan & Buka File**
Kode untuk menyimpan teks ke file:
```java
private void btnSimpanActionPerformed(java.awt.event.ActionEvent evt) {                                          
    JFileChooser fileChooser = new JFileChooser();
    int option = fileChooser.showSaveDialog(this);
    
    if (option == JFileChooser.APPROVE_OPTION) {
        try {
            java.io.File file = fileChooser.getSelectedFile();
            java.io.FileWriter writer = new java.io.FileWriter(file);
            writer.write(jTextArea.getText());
            writer.close();
            JOptionPane.showMessageDialog(this, "File berhasil disimpan!");
        } catch (Exception e) {
            JOptionPane.showMessageDialog(this, "Gagal menyimpan file!", "Error", JOptionPane.ERROR_MESSAGE);
        }
    }
}
```
Kode untuk membuka file:
```java
private void btnBukaActionPerformed(java.awt.event.ActionEvent evt) {                                        
    JFileChooser fileChooser = new JFileChooser();
    int option = fileChooser.showOpenDialog(this);
    
    if (option == JFileChooser.APPROVE_OPTION) {
        try {
            java.io.File file = fileChooser.getSelectedFile();
            java.util.Scanner scanner = new java.util.Scanner(file);
            StringBuilder content = new StringBuilder();
            
            while (scanner.hasNextLine()) {
                content.append(scanner.nextLine()).append("\n");
            }
            scanner.close();
            jTextArea.setText(content.toString());
            JOptionPane.showMessageDialog(this, "File berhasil dibuka!");
        } catch (Exception e) {
            JOptionPane.showMessageDialog(this, "Gagal membuka file!", "Error", JOptionPane.ERROR_MESSAGE);
        }
    }
}
```

---



---



---

### **🎯 Kesimpulan**
Aplikasi ini **sangat berguna** untuk menghitung kata, mencari kata, serta menyimpan & membuka file teks. Silakan gunakan dan kembangkan sesuai kebutuhan! 🚀
