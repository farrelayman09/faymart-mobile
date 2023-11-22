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

***
***

# Tugas 8
Nama: Farrel Ayman Abisatyo<br>
Kelas: PBP F<br>
NPM: 2206828916<br>

## Jelaskan perbedaan antara Navigator.push() dan Navigator.pushReplacement(), disertai dengan contoh mengenai penggunaan kedua metode tersebut yang tepat!

- Navigator.push() adalah sebuat method yang berfungsi untuk menggantikan halaman saat ini dengan halaman baru di atas tumpukan halaman dan membuatnya dapat ditumpuk di atas halaman saat ini. Dengan itu, method ini bisa diibaratkan sebagai method push stack dengan stacknya berupa halaman app. Contoh penggunaaannya:
```
if (item.name == "Tambah Produk") {
        Navigator.push(context,
            MaterialPageRoute(builder: (context) => const ShopFormPage()));
    }
```

- Navigator.pushReplacement() adalah sebuah method yang befungsi untuk menggantikan halaman saat ini dengan halaman baru di tumpukan halaman serta menghapus halaman saat ini dari tumpukan halaman. Halaman saat ini tidak dapat diakses kembali dengan menekan tombol kembali; pengguna langsung melanjutkan ke halaman baru. Dengan itu, method ini bisa diibaratkan sebagai pop dan push stack dengan stacknya berupa halaman app. Contoh penggunaannya:
```
onTap: () {
        Navigator.pushReplacement(
        context,
        MaterialPageRoute(
            builder: (context) => MyHomePage(),
        ));
    },
```


## Jelaskan masing-masing layout widget pada Flutter dan konteks penggunaannya masing-masing!
Terdapat banyak sekali jenis layout widget pada Flutter. Berikut ini adalah beberapa yang sering digunakan:
- Container: widget umum yang digunakan untuk mengelola tata letak dan dekorasi elemen. Ini dapat berfungsi sebagai wadah/kontainer untuk widget lainnya atau sebagai widget tunggal dengan properti seperti padding, margin, dan lainnya.
- Column dan Row: Column digunakan untuk menempatkan widget secara vertikal, sementara Row digunakan untuk menempatkannya secara horizontal.
- ListView: digunakan untuk menampilkan daftar elemen yang dapat di-scroll.
- Stack: digunakan untuk menumpuk widget di atas satu sama lain.
- Align: meng-align child-nya di dalam dirinya sendiri dan menyesuiakan ukurannya berdasarkan ukuran size child-nya


## Sebutkan apa saja elemen input pada form yang kamu pakai pada tugas kali ini dan jelaskan mengapa kamu menggunakan elemen input tersebut!
Pada form untuk menambahkan item, saya menggunakan:
```
String _name = "";
int _price = 0;
String _description = "";
```
Sementara itu saya meng-setState dengan menggunakan sintaks seperti ini untuk menerima input yang sesuai
```_name = value!```, ```_price = int.parse(value!)```, serta ```_description = value!;```
Saya menggunakan elemen input sedemikian karena name dan description perlu menampilkan value berupa teks/String, sedangkan price perlu menampilkan value berupa angka/int

## Bagaimana penerapan clean architecture pada aplikasi Flutter?
Clean architecture adalah blueprint untuk sistem modular, yang secara ketat mengikuti prinsip desain yang disebut separation of concerns. Secara garis besar, clean architecture di Flutter dapat dibagi menjadi 3 layers
- **Feature**: Layer ini merupakan layer presentasi aplikasi. Ini adalah layer yang paling bergantung pada framework, karena berisi UI dan event handler UI.
- **Domain**: Domain Layer adalah bagian paling dalam dari semua of the layers (no dependencies with other layers) dan mengandung Entities, Use Cases & Repository Interfaces. Domain layer akan ditulis semua dalam Dart tanpa elemen Flutter. Alasannya adalah karena domain sepatutnya hanya perlu mengatur dengan business logic dari application.
- **Data**: Data layer merepresentasikan data layer dari aplikasi. Data module, yang merupakan bagian layer paling luar dari, bertanggung jawab untuk data retrieval. Hal ini bisa berupa API calls ke server atau local database. Layer ini juga berisi implementasi repositori.

## Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step! (bukan hanya sekadar mengikuti tutorial)
1. Pertama, saya membuat berkas baru di lib dengan nama shoplist_form.dart dengan isi berupa tampilan serta event handler untuk form penambahan item. Berikut adalah kodenya
```
import 'package:flutter/material.dart';
import 'package:faymart/widgets/left_drawer.dart';


class ShopFormPage extends StatefulWidget {
  const ShopFormPage({super.key});

  @override
  State<ShopFormPage> createState() => _ShopFormPageState();
}

class _ShopFormPageState extends State<ShopFormPage> {
  final _formKey = GlobalKey<FormState>();
  String _name = "";
  int _price = 0;
  String _description = "";
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Center(
          child: Text(
            'Form Tambah Item',
          ),
        ),
        backgroundColor: Colors.indigo,
        foregroundColor: Colors.white,
      ),
      drawer: const LeftDrawer(),
      body: Form(
        key: _formKey,
        child: SingleChildScrollView(
            child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              Padding(
                padding: const EdgeInsets.all(8.0),
                child: TextFormField(
                  decoration: InputDecoration(
                    hintText: "Nama Item",
                    labelText: "Nama Item",
                    border: OutlineInputBorder(
                      borderRadius: BorderRadius.circular(5.0),
                    ),
                  ),
                  onChanged: (String? value) {
                    setState(() {
                      _name = value!;
                    });
                  },
                  validator: (String? value) {
                    if (value == null || value.isEmpty) {
                      return "Nama tidak boleh kosong!";
                    }
                    return null;
                  },
                ),
              ),
              Padding(
                padding: const EdgeInsets.all(8.0),
                child: TextFormField(
                  decoration: InputDecoration(
                    hintText: "Harga",
                    labelText: "Harga",
                    border: OutlineInputBorder(
                      borderRadius: BorderRadius.circular(5.0),
                    ),
                  ),
                  onChanged: (String? value) {
                    setState(() {
                      _price = int.parse(value!);
                      });
                  },
                  validator: (String? value) {
                    if (value == null || value.isEmpty) {
                      return "Harga tidak boleh kosong!";
                    }
                    if (int.tryParse(value) == null) {
                      return "Harga harus berupa angka!";
                    }
                    return null;
                  },
                ),
              ),
              Padding(
                padding: const EdgeInsets.all(8.0),
                child: TextFormField(
                  decoration: InputDecoration(
                    hintText: "Deskripsi",
                    labelText: "Deskripsi",
                    border: OutlineInputBorder(
                      borderRadius: BorderRadius.circular(5.0),
                    ),
                  ),
                  onChanged: (String? value) {
                    setState(() {
                      _description = value!;
                    });
                  },
                  validator: (String? value) {
                    if (value == null || value.isEmpty) {
                      return "Deskripsi tidak boleh kosong!";
                    }
                    return null;
                  },
                ),
              ),
              Align(
                alignment: Alignment.bottomCenter,
                child: Padding(
                  padding: const EdgeInsets.all(8.0),
                  child: ElevatedButton(
                    style: ButtonStyle(
                      backgroundColor:
                      MaterialStateProperty.all(Colors.indigo),
                    ),
                    onPressed: () {
                      if (_formKey.currentState!.validate()) {
                        showDialog(
                          context: context,
                          builder: (context) {
                            return AlertDialog(
                              title: const Text('Item berhasil tersimpan'),
                              content: SingleChildScrollView(
                                child: Column(
                                  crossAxisAlignment:
                                  CrossAxisAlignment.start,
                                  children: [
                                    Text('Nama: $_name'),
                                    Text('Harga: $_price'),
                                    Text("Deskripsi: $_description"),
                                  ],
                                ),
                              ),
                              actions: [
                                TextButton(
                                  child: const Text('OK'),
                                  onPressed: () {
                                    Navigator.pop(context);
                                  },
                                ),
                              ],
                            );
                          },
                        );
                      }
                      _formKey.currentState!.reset();
                    },
                    child: const Text(
                      "Save",
                      style: TextStyle(color: Colors.white),
                    ),
                  ),
                ),
              ),
            ]
            ),
        ),
      ),
    );


  }
}
```
Bisa dilihat bahwa saya meng-set input form sedemikian sesuai dengan konteks dari penambahan barang, yakni name, price, dan description. Setelah saya menerima input, saya akan meng-setState dengan input yang baru diterima. Setelah input form berhasil disimpan, saya menampilkan AlertDialog atau popup yang menandakan item telah ditambahkan beserta atribut-atributnya.


2. Kedua, saya membuka lib dan membuat berkas baru, left_drawer.dart, yang berisi kode sebagai berikut:
```
import 'package:flutter/material.dart';
import 'package:faymart/screens/menu.dart';
import 'package:faymart/screens/shoplist_form.dart';


class LeftDrawer extends StatelessWidget {
  const LeftDrawer({super.key});

  @override
  Widget build(BuildContext context) {
    return Drawer(
      child: ListView(
        children: [
          const DrawerHeader(
            decoration: BoxDecoration(
              color: Colors.indigo,
            ),
            child: Column(
              children: [
                Text(
                  'Faymart',
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 30,
                    fontWeight: FontWeight.bold,
                    color: Colors.white,
                  ),
                ),
                Padding(padding: EdgeInsets.all(10)),
                Text("Catat seluruh keperluan belanjamu di sini!",
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 15,
                    color: Colors.white,
                    fontWeight: FontWeight.normal,
                  ),
                ),
              ],
            ),
          ),
          ListTile(
            leading: const Icon(Icons.home_outlined),
            title: const Text('Halaman Utama'),
            // Bagian redirection ke MyHomePage
            onTap: () {
              Navigator.pushReplacement(
                  context,
                  MaterialPageRoute(
                    builder: (context) => MyHomePage(),
                  ));
            },
          ),
          ListTile(
            leading: const Icon(Icons.add_shopping_cart),
            title: const Text('Tambah Item'),
            // Bagian redirection ke ShopFormPage
            onTap: () {
              Navigator.push(context,
                  MaterialPageRoute(builder: (context) => const ShopFormPage()));
            },
          ),
        ],
      ),
    );
  }
}
```
Berkas dart ini berfungsi untuk menampilkan Drawer di kiri yang akan muncul/geser setelah dipencet. Bisa dilihat juga bahwa saya telah menambahkan method Navigator yang sesuai seperti push ataupun pushReplacement supaya halaman dapat berpindah dengan baik.


3. Setelah itu, untuk mengimplementasikan architecture Flutter yang lebih modular, cuplikan kode di menu.dart yang mengatur Kelas ShopItem akan saya pindahkan ke berkas baru di lib yakni shop_card.dart.
```
import 'package:flutter/material.dart';

class ShopItem {
  final String name;
  final IconData icon;
  final Color color;

  ShopItem(this.name, this.icon, this.color);
}
```

4. Kemudian, saya merefactor juga berkas-berkas lain ke dalam package/direktori yang sesuai supaya lebih clean. Saya membuat package screens yang di dalamnya terdapat menu.dart dan shoplist_form.dart. Selain itu, saya membuat package widgets yang berisi left_drawer.dart serta shop_card.dart. Setelah itu selesai, saya menyesuaikan kembali sintaks import supaya merefer ke directory path yang benar.

# Tugas 9

Nama: Farrel Ayman Abisatyo<br>
Kelas: PBP F<br>
NPM: 2206828916<br>

## Apakah bisa kita melakukan pengambilan data JSON tanpa membuat model terlebih dahulu? Jika iya, apakah hal tersebut lebih baik daripada membuat model sebelum melakukan pengambilan data JSON?
Ya, kita bisa melakukan pengambilan data JSON tanpa membuat model terlebih dahulu, tergantung pada kebutuhan dan tujuan yang kita inginkan. Pengambilan data JSON tanpa membuat model mungkin lebih cocok untuk skenario di mana kita hanya perlu membaca dan mengakses data JSON tanpa melakukan analisis atau transformasi data yang kompleks. 

## Jelaskan fungsi dari CookieRequest dan jelaskan mengapa instance CookieRequest perlu untuk dibagikan ke semua komponen di aplikasi Flutter.
Fungsi dari CookieRequest adalah untuk menyediakan akses ke data cookie yang dibutuhkan oleh berbagai bagian dari aplikasi. CookieRequest perlu untuk dibagikan ke semua komponen di aplikasi Flutter agar komponen-komponen yang berbeda dapat mengakses dan menggunakan data cookie tersebut tanpa perlu membuat instance CookieRequest baru setiap kali. Membagikan instance CookieRequest ke semua komponen mempermudah koordinasi dan pertukaran data antar komponen dalam aplikasi sehingga meningkatkan efisiensi dan konsistensi dalam penggunaan data cookie di aplikasi Flutter.

## Jelaskan mekanisme pengambilan data dari JSON hingga dapat ditampilkan pada Flutter.
1. Mengirimkan GET Request ke url http://farrel-ayman-tugas.pbp.cs.ui.ac.id/json/ untuk mendapatkan JSON yang berisi list of Items.
2. Menggunakan jsonDecode untuk mengubah http response body menjadi bentuk JSON.
3. Membuat object Item menggunakan data JSON yang telah didapatkan kemudian menyimpannya dalam List<Item> list_product
4. Menampilkan semua Item menggunakan ListView.builder(). Setiap Item ditampilkan menggunakan Card() yang dibungkus oleh InkWell().
5. Jika suatu Item diklik, maka seluruh data Item tersebut akan dikirimkan ke halaman ShopFormPage() untuk kemudian ditampilkan semua item secara lebih detail.

## Jelaskan mekanisme autentikasi dari input data akun pada Flutter ke Django hingga selesainya proses autentikasi oleh Django dan tampilnya menu pada Flutter.
1. Pertama, dibuat objek request dengan CookieRequest yang telah diimpor
2. Kemudian, di aplikasi, kita dapat meng-input username beserta password
3. Lalu, username dan password tersebut dikirim dan masuk ke fungsi login_request
4. Jika autentikasi berhasil maka akan diarahkan ke MyHomePage(), tetapi jika tidak, akan diarahkan ke AlertDialog

## Daftar Widget pada Tugas ini beserta Kegunaannya
1. MaterialPageRoute: Widget ini digunakan untuk memberikan efek animasi ketika berpindah antar page.
2. Align: Widget ini digunakan untuk meng-align child-nya di dalam dirinya sendiri dan menyesuiakan ukurannya berdasarkan ukuran size child-nya
3. Row: Widget ini digunakan untuk mengatur letak children widgetnya secara horizontal.
4. Provider: Widget ini menyediakan objek atau data supaya dapat diakses oleh widget di bawahnya.
5. ListView: Widget ini digunakan untuk mengatur letak children widgetnya dalam sebuah scrollable list secara vertikal.
6. LeftDrawer: Widget untuk menampilkan drawer di bagian kiri pada halaman utama yang membesar ketika diklik.
7. ElevatedButton: Widget untuk menampilkan tombol untuk memicu tindakan tertentu.
8. TextFormField: Widget yang berfungsi menerima input teks dari pengguna.
9. CircularProgressIndicator: Widget ini digunakan sebagai indikator loading ketika aplikasi sedang menunggu data dari server
10. Navigator.push: Widget ini digunakan untuk berpindah page dalam bentuk push ke stack/page saat ini.

## Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step! (bukan hanya sekadar mengikuti tutorial).
1. Pertama, saya mengaktifkan virtual environment
2. Lalu, saya men-download packages yang dibutuhkan menggunakan command
```
flutter pub add provider
flutter pub add pbp_django_auth
```
3. Setelah itu, saya memodifikasi main.dart menjadi sedemikian rupa
```
class MyApp extends StatelessWidget {
    const MyApp({Key? key}) : super(key: key);

    @override
    Widget build(BuildContext context) {
        return Provider(
            create: (_) {
                CookieRequest request = CookieRequest();
                return request;
            },
            child: MaterialApp(
                title: 'Flutter App'
                theme: ThemeData(
                    colorScheme: ColorScheme.fromSeed(seedColor: Colors.indigo),
                    useMaterial3: true,
                ),
                home: MyHomePage()),
            ),
        );
    }
}
```
4. Di package screens, saya membuat file login.dart yang berfungsi mengatur sistem autentikasi user yang ingin masuk ke aplikasi
5. Lalu, saya membuat model custom untuk aplikasi flutter menggunakan website QuickType yang memudahkan pembuatan model tersebut dengan memasukkan data dari endpoint JSON dan membuat item.dart yang berisi model tersebut
6. Kemudian, saya menambahkan dependensi flutter dengan ```flutter pub add http``` di terminal serta menambahkan kode berikut di AndroidManifest.xml
```
...
    <application>
    ...
    </application>
    <!-- Required to fetch data from the Internet. -->
    <uses-permission android:name="android.permission.INTERNET" />
...
```
7. Lalu, saya memodifikasi file item_form.dart pada direktori screens agar dapat mengubah input yang diterima ke dalam JSON kemudian mengirimkannya ke server.
8. Setelah itu, saya membuat file di screens, yakni list_item.dart yang berfungsi memproses endpoint yang disediakan sehingga dapat menampilkan item-item yang ada beserta informasinya.
9. Kemudian, saya mengintegrasi Form FLutter di Django dengan membuat create_item_flutter di main.views.py projek Django serta menghubungakn shoplist_form.dart dengan CookieRequest
10. Terakhir, saya membuat fungsi logout di authentication.views.py serta mengintegrasinya dengan Flutter di shop_card.dart
