---
layout: post
title: Dependency Injection dengan Dagger 2
image: img/dagger.png
description: Bagaimana cara menggunakan Dagger2 sebagai dependency injection di Android Project
author: Wahyu Permadi
date: 2019-11-13T07:03:47.149Z
tags: [dependency-injection]
draft: false
---

Hallo temen-temen, kali ini gw membahas tentang Dagger2 + Kotlin. Sebelumnya udah pada familiar belum dengan yang namanya DI (<i>Depedency Injection</i>), selanjutnya dibaca DI ? kalau belum, secara garis besarnya DI itu.

> DI (<i>Depedency Injection</i>) merupakan sebuah proses untuk memasukan (<i>inject</i>) sebuah <i>object</i> kedalam <i>class</i> lain yang membutuhkannya.

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
Dari kode diatas dapat dilihat bahwa ketika kita ingin membuat <i>object</i> dari class Car, kita perlu membuat object class Wheel dan object class Pertamax juga. Coba bayangkan saja jika class Car digunakan di banyak <i>Activity</i> maupun <i>Fragment</i>, berapa kali kalian akan membuat instance object yang sama ? tentunya banyak bukan. Nah karena itulah DI itu ada.

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

Sebelum menggunakan <b>@Inject</b>, pastikan <i>dependencies</i> yang diperlukan sudah di <b>Provides</b> sebelumnya.
<b>@ContributesAndroidInjector</b> pada dagger-android berfungsi untuk meng-generate AndroidInjector sesuai dengan tipe dari method tersebut. Sehingga proses mendaftarkan <i>Activity</i> / <i>Fragment</i> yang telah dibuat kedalam <b>Dagger Graph</b> menjadi lebih mudah.
<b>@Modules</b> merupakan <i>annotation</i> untuk mendefinisikan sebuah <i>class yang menyediakan</i> <i>dependencies</i> yang diperlukan seperti <b>NetworkModule</b> dibawah ini.

```css
@Module
class NetworkModule {
    @Provides
    @Singleton
    fun gson(): Gson = Gson()

    @Provides
    @Singleton
    fun provideOkHttpClient(): OkHttpClient{
        val httpInterceptor = HttpLoggingInterceptor(HttpLoggingInterceptor.Logger {
            Log.d("Movie", it)
        })

        val dispatcher = Dispatcher()
        dispatcher.maxRequests = 1

        val interceptor = Interceptor { chain ->
            SystemClock.sleep(1000)
            chain.proceed(chain.request())
        }

        httpInterceptor.level = HttpLoggingInterceptor.Level.BASIC

        return OkHttpClient.Builder().addInterceptor(httpInterceptor)
            .addNetworkInterceptor(interceptor)
            .dispatcher(dispatcher)
            .build()
    }

    @Provides
    @Singleton
    fun provideRestClient(okHttpClient: OkHttpClient) : Retrofit{
        return Retrofit.Builder()
            .baseUrl(BuildConfig.BASE_URL)
            .client(okHttpClient)
            .addConverterFactory(GsonConverterFactory.create())
            .build()
    }

    @Provides
    @Singleton
    fun apiService(retrofit: Retrofit): ApiService{
        return retrofit.create(ApiService::class.java)
    }
}
```

Pada <i>NetworkModule</i> terdapat <i>annotation</i> <b>@Provides</b> dan <b>@Singleton</b>, <b>@Singleton</b> sendiri berfungsi untuk membuat <i>instance</b> dari <i>object</i> tersebut cukup sekali saja, dan @Provides digunakan untuk membuat dependencies dari <i>object</i> tersebut, sehingga dapat dibaca oleh <b>@Inject</b> <i>annotation</i> dan penggunaan <b>@Provides</b> hanya bisa digunakan didalam class yang memiliki annotation <b>@Module</b>.

<b>@Component</b> merupakan sebuah <i>annotation</i> yang digunakan untuk menampung modul-modul yang telah dibuat dan digunakan untuk memulai Dipendency Injection. Seperti ApplicationComponent dibawah ini.

```css
@Singleton
@Component(modules = [(AndroidInjectionModule::class),
    (ActivityBuilder::class),
    (NetworkModule::class),
    (AppModule::class)])
interface ApplicationComponent {

    @Component.Builder
    interface Builder {
        @BindsInstance
        fun application(application: Application) : Builder
        fun build(): ApplicationComponent
    }

    fun inject(app: MainApplication)
}
```

pada <b>@Component</b> kita daftarkan <i>module</i>-<i>module</i> apa saja yang telah dibuat, <i>module</i>-<i>module</i> tersebut akan di-<i>generate</i> untuk menghasilkan <i>depedencies</i> yang diperlukan didalam aplikasi. <b>@Binds</b> sejauh yang gw pahami, biasanya digunakan untuk <i>method</i> yang bertipe <i>abstract</i>, hampir mirib seperti <b>@Provides</b>, namun tidak memiliki <i>return instance</i>.

Nah untuk mengimplementasikan Dagger kedalam sebuah <i>project</i> Android, jangan lupa untuk meng-<i>install dependency</i> <i>library</i>-nya terlebih dahulu ke dalam <b>build.gradle/app</b>.

```css
implementation 'com.google.dagger:dagger-android:2.x'
implementation 'com.google.dagger:dagger-android-support:2.x'
annotationProcessor 'com.google.dagger:dagger-android-processor:2.x'
```

Untuk implementasi sederhana Dagger 2 dengan Kotlin, dapat dilihat pada Repo berikut, pada branch master menggunakan MVP dan pada branch MVVM menggunakan MVVM pattern. Thank you
[GithubRepository](https://github.com/wahyupermadie/try-dagger)

#### References:
[Dagger](https://dagger.dev/)

*[HTML]: Hyper Text Markup Language
*[CSS]: Cascading Style Sheets
