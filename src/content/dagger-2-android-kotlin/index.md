---
layout: post
title: Dependency Injection dengan Dagger 2
image: img/dagger.png
author: Ghost
date: 2019-11-13T07:03:47.149Z
tags: [depencey-injection]
draft: false
---

Hallo temen-temen, kali ini gw membahas tentang Dagger2 + Kotlin. Sebelumnya udah pada familiar belum dengan yang namanya DI (Dependency Injection), selanjutnya dibaca DI ? kalau belum, secara garis bersarnya DI itu.

> DI (Depedency Injection) merupakan sebuah proses untuk memasukan (inject) sebuah class kedalam class lain yang membutuhkannya.

Sebagai contoh lain ada sebuah class Car yang tersusun dari class Pertamax, dan class Wheel.

```css
class Car{
    private lateinit var wheel : Wheel
    private lateinit var pertamax : Pertamax
    
    constructor(wheel: Wheel, pertamax: Pertamax){
        this.wheel = wheel
        this.pertamax = pertamax
    }
    fun getWheel(){
        println("Jumlah Roda "+wheel.wheels())
    }
    
    fun getPertamaxName(){
        println(pertamax.getName())
    }
    fun getPertamaxPrice(){
        println(pertamax.getPrice())
    }
}
class Wheel{
    fun wheels() : String{
        return "4 Wheels"
    }
}
class Pertamax(){
    fun getName() : String {
        return "Pertamax"
    }
    
    fun getPrice() : String {
        return "12.000"
    }
}
fun main(){
    var car = Car(Wheel(), Pertamax())
    car.getWheel()
    car.getPertamaxName()
    car.getPertamaxPrice()
}
```
Dari kode diatas dapat dilihat bahwa ketika kita ingin membuat object dari class Car, kita perlu membuat object class Wheel dan object class Pertamax juga. Coba bayangkan saja jika class Car digunakan di banyak Activity maupun Fragment, berapa kali kalian akan membuat instance object yang sama ? tentunya banyak bukan. Nah karena itulah DI itu ada.

---

DI yang akan gw bahas disini adalah Dagger dengan versi 2.24, kenapa Dagger ? karena Dagger merupakan salah satu DI favorite dikalangan para Android Developer selain [Koin](https://insert-koin.io/). Pada Dagger nanti kita akan mengenal dengan yang namanya Annotation, seperti <b>@Inject</b>, <b>@Module</b>, <b>@Component</b>, <b>@SubComponent</b>,<b>@Binds</b>, <b>@Provides</b>, <b>@ContributesAndroidInjector</b> dan sebagainya.

<b>@Inject</b> merupakan sebuah annotation yang berfungsi untuk me-request depedencies. Annotation ini dapat digunakan didalam constructor, field maupun class.
```css
class MoviesViewModel @Inject constructor(
    val apiService: ApiService
) : ViewModel(){
   // function here
}
```

*[HTML]: Hyper Text Markup Language
*[CSS]: Cascading Style Sheets
