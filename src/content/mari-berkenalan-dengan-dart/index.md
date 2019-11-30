---
layout: post
title: Mari Berkenalan Dengan Dart
image: img/dart.jpg
description: Dart adalah bahasa pemrograman yang dioptimalkan klien untuk aplikasi cepat di berbagai platform. Ini dikembangkan oleh Google dan digunakan untuk membangun aplikasi mobile, desktop, backend, dan web.
author: Wahyu Permadi
date: 2019-11-30T07:03:47.149Z
tags: [ENGINEERING]
draft: false
---

[Dart](https://dart.dev) merupakan sebuah bahasa pemrograman yang dikembangkan oleh <b>Google</b> untuk membangun aplikasi <i>mobile</i>, <i>desktop</i>, <i>backend</i> dan <i>web</i>. Mungkin bagi teman-teman yang sudah familiar ngoding <i>javascript</i>, belajar Dart bukanlah hal yang terlalu menyulitkan.
* [Flutter](https://flutter.dev/docs/get-started/install) merupakan Framework Dart untuk membuat aplikasi baik Android maupun iOS atau dengan katalain aplikasi <i>cross-platform</i>.
* [Web](https://dart.dev/tutorials/web/get-started) merupakan pengembangan Dart dalam dunia Web, terutama dalam hal <i>front-end</i>, yang dimana kode program yang ditulis dengan Dart dikompilasi (<i>transpile</i>) menjadi <i>javascript</i> sehingga dapat dimengerti oleh <i>web browser</i>. Sebagai contoh [AngularDart](https://angulardart.dev/).
* [Server/CLI](https://dart.dev/tutorials/server/get-started) merupakan pengembangan Dart dalam pembuatan aplikasi berbasis <i>text</i> (CLI), <i>backend</i>, IoT dan sebagainya. Sebagai contoh [Exspress](https://github.com/dartist/express).

---

Nah disini gw nggak akan bahas bagaimana implementasi Dart untuk web, mobile mauapun server. Melainkan gw bakal bahas dasar-dasar dari Dart, seperti : 
* Tipe Data 
* Variabel 
* Operator 
    1. <i>Arithmetic</i>
    2. <i>Relational</i> 
    3. <i>Type Test</i>
    4. <i>Assigment</i>
    5. <i>Conditional</i>
    6. <i>Ternary</i> 
* Loop Control


# Tipe Data
Bahasa pemrograman Dart memiliki tipe data seperti dibawah ini.

| Tipe Data              | Default       |
| ---------------------- |:-------------:|
| `String`               | null          |
| `Integer | Double`     | null          |
| `Boolean`              | null          |
| `List | Set`           | null          |
| `Maps`                 | null          |
| `Runes`                | null          |

Semua tipe data dalam bahasa pemrograman Dart memiliki `default value null`, dan untuk tipe data `String`, `Integer`, `Double` dan `Maps` mungkin sudah tidak asing lagi ditelinga kalian. 
1. Tipe data <b>Set</b> merupakan tipe data sejenis List, namun akan menghapus value yang memiliki nilai yang sama. Sehingga tidak ada duplikat value seperti dibawah ini.
```javascript
void main(){
        var data = Set();
        data.add("1");
        data.add("2");
        data.add("2");
        print(data);
}
```
dan hasilnya akan seperti dibawah ini.
```javascript 
{1, 2} 
```
2. Tipe data <b>Runes</b> atau Unit Code merupakan sebuah tipe data yang digunakan untuk membaca `String` yang memiliki deretan kode unit `UTF-32`, karena secara <i>default</i> `String` merupakan menggunakan kode unit `UTF-16`. untuk menggunakan `Runes`, diperlukan library `dart:core`.
```javascript
main() {
        var clapping = '\u{1f44f}';
        print(clapping);
        print(clapping.codeUnits);
        print(clapping.runes.toList());
        Runes input = new Runes(
      '\u2665  \u{1f605}  \u{1f60e}  \u{1f47b}  \u{1f596}  \u{1f44d}');
        print(new String.fromCharCodes(input));
}
```
dan hasilnya seperti dibawah ini.
```css
👏
[55357, 56399]
[128079]
♥  😅  😎  👻  🖖  👍
```


# Variabel
Deklarasi variabel di Dart dapat dideklarasikan secara eksplisit maupun implisit, sebagai contoh.
```javascript
    var nama = "Wahyu Permadi"
```
Deklarasi variabel diatas merupakan 
   salah satu contoh deklarasi secara implisit, karena tidak memberitahukan tipe data dari variabel `nama` itu apa, bisa
`string`, `int`, dsb. Tipe variabel jika dideklarasikan secara implisit akan bergantung dari <i>value</i> yang di-<i>assign</i>, dan variabel `nama` tersebut secara tidak 
langsung bertipe data `String`, karena di-<i>assign</i> sebuah `String` <i>value</i>. Contoh deklarasi secara eksplisit adalah seperti dibawah ini.
```javascript
    String nama = "Wahyu Permadi"
```
Jika ingin membuat sebuah variabel yang nilainya bersifat tetap, dapat menggunakan `const` maupun `final`. Keduanya memiliki perbedaan, dimana `const` akan dibuat ketika aplikasi pertama kali di compile atau dengan kata lain `compile-time` variabel. Sedangkan `final` adalah variabel yang dibuat pada saat `runtime`. Penggunannya seperti contoh dibawah ini.
```javascript
    const phi = 3.14; 
    // nilai phi tetap dan diketahui sebelum runtime
```
```javascript
    final dateNow = new DateTime.now(); 
    // nilai datenow hanya diketahui pada saat runtime, jadi gunakan final
```


# Operator Arithmetic
Operator arithmetic merupakan operator yang digunakan untuk melakukan perhitungan mamtematis, contoh dari operator arithmetic adalah sebagai berikut.

| Operator               | Meaning                 |
| ---------------------- |:-----------------------:|
| +                      | Add                     |
| -                      | Substract               |
| *                      | Multiply                |
| /                      | Divide                  |
| %                      | Modulo                  |
| -expr                  | Unary Minus             |
| ~/                     | Divide (Return Integer) |
| ++                     | Increment               |
| --                     | Decrement               |

Contoh penggunaan dari operator arithmetic adalah sebagai berikut.
```javascript
void main(){
    print(1 + 1);
    print(5 - 2);
    print(3 * 3);
    print(4 / 2);
    print(5 % 2);
    print(-5);
    print(5 ~/ 2);
    var increment = 0;
    print(++increment);
    var decrement = 5;
    print(--decrement);
}
```
```javascript
1+1 = 2
5-2 = 3
3*3 = 9
4/2 = 2
5%2 = 1
-(5)= -5
5 ~/ 2 = 2 (return always integer not double)
++increment = 1 (increment = increment + 1) 
--decrement = 4 (decrement = decrement - 1)
```


# Operator Relational
Operator relational merupakan operator yang digunakan untuk menentukan relasi atau hubungan dari duah buah operand. Operator relational ditempatkan 
untuk membandingkan dua ekspresi yang kemudian hasilnya menentukan apakah benar atau tidaknya hasil operasi itu. Contoh dari operator relational dapat
dilihat dibawah ini.

| Operator               | Meaning                    |
| ---------------------- |:--------------------------:|
| >                      | Greater Than               |
| <                      | Less Than                  |
| >=                     | Greater Than or Equal To   |
| <=                     | Less Than or Equal To      |
| ==                     | Equal To                   |
| !=                     | Not Equal To               |

contoh penggunaannya sebagai berikut.
```javascript
void main(){
    print(3 > 1); //true
    print(5 < 10); //true
    print(3 >= 3); //true
    print(5 <= 6); //true
    print(10 == 10); //true
    print(10 != 5); //true
    print(10 == 9); //false
}
```

# Operator Type Test
Operator <i>type test</i> biasanya digunakan untuk mengecek apakah suatu variabel/object memiliki tipe data sesuai apa yang diinginkan.
Contoh dari operator <i>type test</i> seperti dibawah ini.

| Operator               | Meaning                                  |
| ---------------------- |:----------------------------------------:|
| is                     | True if the object has specified type    |
| is!                    | True if the object has not specified type|

Contoh penggunaannya seperti dibawah ini.
```javascript
void main(){
    var nama = "Wahyu Permadi";
    print(nama is String); // true
    
    var jumlah = 100;
    print(jumlah is Map); // false
}
```
Seperti contoh diatas, dimana dilakukan type checking terhadapat variabel dengan nama `name` dan `jumlah`, untuk variabel `name is String` return `True`, karena
benar variabel tersebut adalah `String`, sedangkan variabel `jumlah is Map` return `False` karena tipe dari variabel `jumlah` adalah `Integer` bukan `Map`. 

# Operator Assigment
Operator <i>assigment</i> merupakan operator yang digunakan untuk memberikan suatu nilai ke sebuah variabel. Contoh dari operator <i>assigment</i> adalah sebagai berikut.

| Operator               | Meaning                                            |
| ---------------------- |:--------------------------------------------------:|
| =                      | Assign value from right operand to left operand    |
| ??=                    | Assign value only if the value is null             |

contoh penggunannya seperti ini.
```javascript
void main(){
    var nama = "Wahyu";
    nama = "Wahyu Permadi";
    
    String title = "Wahyu";
    title ??= "Putu Wahyu";
    
    String jobs = null;
    jobs ??= "Android Engineer";
    
    print(nama);
    print(title);
    print(jobs);
}
```
Hasilnya sudah pasti bisa kalian tebak dong bagaimana, okeh jadi hasilnya seperti ini.
```javascript
Wahyu Permadi
Wahyu
Android Engineer
```
Nah operator `??=` hanya akan mengisi variabel tersebut jika variabel yang akan di-<i>assign</i> `null`, itulah mengapa pada variabel `title` valuenya tidak berubah. 

# Operator Conditional
Operator <i>conditional</i> merupakan operator yang digunakan untuk mengecek kondisi dari satu, dua atau lebih `boolean` <i>expressions</i>. Contoh operator <i>conditional</i> adalah sebagai berikut.

| Operator               | Meaning                                            |
| ---------------------- |:--------------------------------------------------:|
| &&                     | Return true if all conditions are true             |
| II                     | Return true if any one conditions are true         |
| !                      | Return the inverese of the result                  |

Contoh implementasinya sebagai berikut.
```javascript
void main(){
    var isWahyuMale = true;
    var isWahyuStupid = true;
    print(isWahyuMale && isWahyuStupid);
    
    var isWahyuGanteng = true;
    var isWahyuDokter = false;
    print(isWahyuGanteng && isWahyuDokter);
    
    print(isWahyuGanteng || isWahyuDokter);
    
    print(!isWahyuGanteng);
}
```
Nah dari contoh implementasi diatas, sudah bisa ditebak dong hasilnya bagaimana. Yap benar hasilnya seperti dibawah ini.
```javascript
true
false
true
false
```

# Operator Ternary
Operator ternary bisa dikatakan operator seperti `if-else` namun lebih pendek penulisannya, sebagai contoh disini kita akan mengecek apakah seseorang ini benar adalah `wahyu`, jika benar maka `print("wahyu")` jika tidak maka `print("bukan")`. Pertama kita gunakan `if-else` seperti dibawah ini.

```javascript
    void main(){
        var isThisWahyu = true;
    
        if(isThisWahyu){
            print("wahyu");
        }else{
            print("bukan");
        }
    }
```
Nah dengan ternary operator, kita dapat mempersingkatnya menjadi.
```javascript
    void main(){
        var isThisWahyu = true;
        isThisWahyu ? print("wahyu") : print("bukan");
    }
```
Cukup mudah bukan untuk dipahami, `?` digunakan untuk kondisi `true`, dan `:` digunakan sebagai pengganti `else`.

# Loop Control
Perulangan didalam bahasa pemrograman Dart bisa menggunakan `For`, `While` dan `Do-While`.
1. For sendiri memerlukan `initial count value`, `termination condition` dan `step`. Contoh penggunaan dari `For` seperti ini.
```javascript
void main() { 
   var num = 5; 
   var factorial = 1; 
   
   for( var i = num ; i >= 1; i-- ) { 
      factorial *= i ; 
   } 
}
```
`var i = num` merupakan <i>initial count value<i>, `i >= 1` merupakan <i>termination condition</i> (bertujuan agar tidak loopoing foreva), dan `i--` merupakan <i>step</i>.

2. Penggunaan `While` memerlukan `termination condition` dan `step` seperti ini. 
```javascript
void main() { 
   var num = 5; 
   var factorial = 1; 

   while(num >= 1){
     factorial*=num;
     num--;
   }
}
```
`num >= 1` merupakan <i>termination condition</i> dan `num--` merupakan <i>step</i>.

3. Dan yang terakhir penggunaan `Do-While`, `Do-While` sendiri melaukan proses terlebih dahulu, baru kemudian melakukan checking kondisi. seperti dibawah ini.
```javascript
void main() { 
    var num = 5; 
    var factorial = 1; 

        do{
            factorial*=num;
            num--;
        }while(num >= 1);
}
```

Terimakasih, sekian dari saya semoga artikel ini bermanfaat dan jika ada kekurangan bisa dibantu untuk <i>create issue</i> di [github]("https://github.com/wahyupermadie/personal-blog") sata, terimakasih :)

# References
1.  [Dart.dev]("Dart.dev")
2.  [Tutorialspoint]("https://www.tutorialspoint.com/dart_programming/dart_programming_overview.htm")



