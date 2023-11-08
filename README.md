# Tugas 7
Nama: Farrel Ayman Abisatyo<br>
Kelas: PBP F<br>
NPM: 2206828916<br>

## Apa perbedaan utama antara stateless dan stateful widget dalam konteks pengembangan aplikasi Flutter?
Perbedaan utama antara keduanya adalah bagaimana mereka mengelola dan merespons perubahan dalam data atau keadaan aplikasi. Berikut adalah perbedaan utama antara keduanya:
- Stateless Widget:
  - Stateless widget merupakan widget yang tidak memiliki *state* internal. Artinya, sekali widget ini dibuat, tidak mungkin mengubah keadaannya.
  - Mereka cocok untuk elemen tampilan yang tidak berubah seiring waktu, seperti teks statis, icon, atau gambar.
  - Stateless widget didefinisikan dengan membuat kelas yang mengimplementasikan StatelessWidget dan meng-override metode build untuk mendefinisikan tampilan widget.
- Stateful Widget:
  - Stateful widget merupakan widget yang memiliki keadaan *state* internal yang dapat berubah seiring waktu.
  - Mereka cocok untuk elemen tampilan yang memerlukan pembaruan berdasarkan perubahan data atau tindakan pengguna, seperti formulir, daftar yang dapat di-scroll, atau komponen dinamis lainnya.
  - Stateful widget didefinisikan dengan membuat dua kelas: kelas yang mengimplementasikan StatefulWidget untuk mengelola keadaan dan kelas yang mengimplementasikan State untuk mendefinisikan tampilan widget dan reaksi terhadap perubahan keadaan.
 
## Sebutkan seluruh widget yang kamu gunakan untuk menyelesaikan tugas ini dan jelaskan fungsinya masing-masing.
- StatelessWidget: MyHomePage and ShopCard merupakan stateless widgets. Mereka merupakan bagian dari user interface yang tidak memiliki state internal dan tidak berubah seiring waktu berjalan. 
- Scaffold: Scaffold merupakan material design widget yang menyediakan struktur dasar dari app ini
- AppBar: AppBar merupakan widget yang merepresentasikan top app bar yang memiliki title beserta background color
- SingleChildScrollView: SingleChildScrollView merupakan widget yang memungkinkan app untuk discroll ketika konten yang ditampilkan lebih besar dari screen device
- Column: Column merupakan widget yang mengatur children-nya di sebuah vertical column. Widget ini digunakan untuk meng-stack widgets secara vertical di dalam SingleChildScrollView.
- GridView.count: GridView.count merupakan widget yang membuat scrollable grid widgets dengan column berjumlah fixed number. Ini digunakan untuk mendisplay grid of ShopCard widgets.
- InkWell: InkWell merupakan material design widget yang menyediakan touch feedback ketika user meng-tap child widget.
- Icon and Text: Icon dan Text merupakan basic widgets yang digunakan untuk men-display icons dan text di dalam ShopCard widget.
- SnackBar: SnackBar merupakan widget yang men-display temporary message di bagian bawah screen. ini digunakan untuk menunjukkan pesan ketika ShopCard is tapped.
- Material: Material merupakan widget yang menyediakan background color untuk ShopCard. Ini merepresentasikan material design card berbentuk persegi panjang.

## Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step (bukan hanya sekadar mengikuti tutorial)
1. Pertama, saya membuat new flutter app dengan menulis ```flutter create faymart``` di direktori yang saya inginkan
2. Kemudian, saya masuk ke direktori tersebut dan menulis ```cd faymart``` dan ```flutter run``` untuk menguji berhasil atau tidaknya app
3. Setelah itu, saya membuka editor Android App Studio dan merapikan file di direktori lib di dalam root folder.
4. Di faymart.lib.main.dart saya menulis ```import 'package:flutter/material.dart';``` di bagian atas untuk mengimport material-material dart
5. Kemudian saya membuat file baru menu.dart dan memindahkan baris kode dari MyHomePage sampai bawah
6. Di menu.dart saya men-delete MyHomePageState karena bagian ini tidak digunakan
7. Di main.dart, saya mengimport ```import 'package:shopping_list/menu.dart';``` supaya file yang dipindahkan ke menu.dart tetap direcognize
8. Di menu.dart saya mengubah MyHomePage menjadi sedemikian rupa
```
class MyHomePage extends StatelessWidget {
    MyHomePage({Key? key}) : super(key: key);

    @override
    Widget build(BuildContext context) {
        return Scaffold(
```
9. Kemudian, saya membuat Class baru yakni class ShopItem yang isinya
 ```
ShopItem {
  final String name;
  final IconData icon;
  final Color color;

  ShopItem(this.name, this.icon, this.color);
}
```
Dapat dilihat bahwa terdapat tiga atribut, yakni name untuk teks, icon untuk ikon yang ditunjukkan, serta color untuk meng-set background color tombol
10. Lalu saya menginstantiate tiga buah tombol ShopItem dengan kode
```
final List<ShopItem> items = [
  ShopItem("Lihat Item", Icons.checklist, Colors.green),
  ShopItem("Tambah Item", Icons.add_shopping_cart, Colors.blue),
  ShopItem("Logout", Icons.logout, Colors.red),
];
```
11. Setelah itu, saya mengisi Widget Scaffold di MyHomePage dengan beberapa widget yang dibutuhkan app, yakni
```
class MyHomePage extends StatelessWidget {
  MyHomePage({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text(
          'Faymart',
          style: TextStyle(color: Colors.white),
        ),

        backgroundColor: Colors.indigo,
      ),
      body: SingleChildScrollView(
        // Widget wrapper yang dapat discroll
        child: Padding(
          padding: const EdgeInsets.all(10.0), // Set padding dari halaman
          child: Column(
            // Widget untuk menampilkan children secara vertikal
            children: <Widget>[
              const Padding(
                padding: EdgeInsets.only(top: 10.0, bottom: 10.0),
                // Widget Text untuk menampilkan tulisan dengan alignment center dan style yang sesuai
                child: Text(
                  'PBP Shop', // Text yang menandakan toko
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 30,
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ),
              // Grid layout
              GridView.count(
                // Container pada card kita.
                primary: true,
                padding: const EdgeInsets.all(20),
                crossAxisSpacing: 10,
                mainAxisSpacing: 10,
                crossAxisCount: 3,
                shrinkWrap: true,
                children: items.map((ShopItem item) {
                  // Iterasi untuk setiap item
                  return ShopCard(item);
                }).toList(),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```
12. Terakhir, saya membuat stateless widget ShopCard supaya dapat menjadi hasil return bagian kode ```return ShopCard(item);``` di atas
```
class ShopCard extends StatelessWidget {
  final ShopItem item;

  const ShopCard(this.item, {super.key}); // Constructor

  @override
  Widget build(BuildContext context) {
    return Material(
      color: Colors.indigo,
      child: InkWell(
        // Area responsive terhadap sentuhan
        onTap: () {
          // Memunculkan SnackBar ketika diklik
          ScaffoldMessenger.of(context)
            ..hideCurrentSnackBar()
            ..showSnackBar(SnackBar(
                content: Text("Kamu telah menekan tombol ${item.name}!")));
        },
        child: Container(
          // Container untuk menyimpan Icon dan Text
          padding: const EdgeInsets.all(8),
          child: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Icon(
                  item.icon,
                  color: Colors.white,
                  size: 30.0,
                ),
                const Padding(padding: EdgeInsets.all(3)),
                Text(
                  item.name,
                  textAlign: TextAlign.center,
                  style: const TextStyle(color: Colors.white),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}
```





