# Animal_Class_Inheritance_Kotlin_Example

## Kotlin Uygulamasında Kalıtım Türleri Örnekleri

### Tekli Kalıtım (Single Inheritance)

```bash
open class Hayvan {
    fun beslenme() {
        println("Hayvan besleniyor...")
    }
}

class Kedi : Hayvan() {
    fun miyavlama() {
        println("Miyav miyav...")
    }
}

fun main() {
    val kedi = Kedi()
    kedi.beslenme() // Hayvan besleniyor...
    kedi.miyavlama() // Miyav miyav...
}

```

### Çoklu Kalıtım (Multiple Inheritance)

Kotlin'de doğrudan çoklu kalıtım desteklenmez.

Kotlin'de Çoklu Kalıtım (Multiple Inheritance) Yerine Ne Kullanılır?
Kotlin'de doğrudan çoklu kalıtım desteklenmez. Bunun yerine, aşağıdaki yöntemlerden birini kullanabilirsiniz:

1. Arayüzler (Interfaces)

Arayüzler, bir sınıfın sahip olması gereken davranışları tanımlar. Bir sınıf birden fazla arayüzü uygulayabilir. Bu sayede, çoklu kalıtımın getirdiği karmaşıklık olmadan, bir sınıfa birden fazla davranış kazandırabilirsiniz.


```bash
interface UcmaYetenekli {
    fun ucma()
}

interface KonusmaYetenekli {
    fun konusma()
}

class Papagan : UcmaYetenekli, KonusmaYetenekli {
    override fun ucma() {
        println("Uçuyorum...")
    }

    override fun konusma() {
        println("Merhaba...")
    }
}

fun main() {
    val papagan = Papagan()
    papagan.ucma() // Uçuyorum...
    papagan.konusma() // Merhaba...
}

```

2. Sınıf Hiyerarşisi (Class Hierarchy)

Bir sınıf, başka bir sınıftan miras alarak (inheritance) onun özelliklerini ve davranışlarını devralabilir. Bu şekilde, bir sınıf hiyerarşisi oluşturabilirsiniz.

```bash
open class Hayvan {
    fun beslenme() {
        println("Hayvan besleniyor...")
    }
}

class Kus : Hayvan() {
    fun ucma() {
        println("Uçuyorum...")
    }
}

class Papagan : Kus() {
    fun konusma() {
        println("Merhaba...")
    }
}

fun main() {
    val papagan = Papagan()
    papagan.beslenme() // Hayvan besleniyor...
    papagan.ucma() // Uçuyorum...
    papagan.konusma() // Merhaba...
}

```

3. Delegasyon (Delegation)

Delegasyon, bir nesnenin sahip olmadığı bir özelliği veya davranışı başka bir nesneye devretme yeteneğidir. Bu sayede, kod tekrarını önleyebilir ve daha modüler bir tasarım oluşturabilirsiniz.

```bash
class UcmaYetenekli {
    fun ucma() {
        println("Uçuyorum...")
    }
}

class Papagan {
    private val ucmaYetenekli = UcmaYetenekli()

    fun ucma() {
        ucmaYetenekli.ucma()
    }

    fun konusma() {
        println("Merhaba...")
    }
}

fun main() {
    val papagan = Papagan()
    papagan.ucma() // Uçuyorum...
    papagan.konusma() // Merhaba...
}

```

Hangi Yöntem Kullanılmalı?

Hangi yöntemin kullanılacağı, özel ihtiyaçlarınıza bağlıdır. Arayüzler, bir sınıfa birden fazla davranış kazandırmanın en basit yoludur. Sınıf hiyerarşisi, daha karmaşık davranışlar ve kod tekrarını önlemek için kullanılabilir. Delegasyon ise daha modüler bir tasarım oluşturmak için kullanılabilir.

Not:

* Kotlin'de çoklu kalıtım desteklenmez, çünkü bu durum karmaşıklık ve elmas problemlerine yol açabilir.
* Yukarıdaki yöntemler, çoklu kalıtımın işlevselliğini taklit etmenin farklı yollarını sunar.
* Hangi yöntemin kullanılacağına karar vermeden önce, her birinin avantajlarını ve dezavantajlarını göz önünde bulundurmanız önemlidir.

### Çok Seviyeli Kalıtım (Multilevel Inheritance)

```bash
open class Hayvan {
    fun beslenme() {
        println("Hayvan besleniyor...")
    }
}

open class Memeli : Hayvan() {
    fun sutVerme() {
        println("Memeli süt veriyor...")
    }
}

class Kedi : Memeli() {
    fun miyavlama() {
        println("Miyav miyav...")
    }
}

fun main() {
    val kedi = Kedi()
    kedi.beslenme() // Hayvan besleniyor...
    kedi.sutVerme() // Memeli süt veriyor...
    kedi.miyavlama() // Miyav miyav...
}

```

### Hiyerarşik Kalıtım (Hierarchical Inheritance)

```bash
open class Hayvan {
    fun beslenme() {
        println("Hayvan besleniyor...")
    }
}

interface EvcilHayvan {
    fun sevgiGosterme()
}

class Kedi : Hayvan(), EvcilHayvan {
    override fun sevgiGosterme() {
        println("Mır mır...")
    }

    fun miyavlama() {
        println("Miyav miyav...")
    }
}

fun main() {
    val kedi = Kedi()
    kedi.beslenme() // Hayvan besleniyor...
    kedi.sevgiGosterme() // Mır mır...
    kedi.miyavlama() // Miyav miyav...
}

```

### Hibrit Kalıtım (Hybrid Inheritance)

```bash
open class Hayvan {
    fun beslenme() {
        println("Hayvan besleniyor...")
    }
}

interface UcmaYetenekli {
    fun ucma()
}

interface KonusmaYetenekli {
    fun konusma()
}

class Papagan : Hayvan(), UcmaYetenekli, KonusmaYetenekli {
    override fun ucma() {
        println("Uçuyorum...")
    }

    override fun konusma() {
        println("Merhaba...")
    }

    fun miyavlama() {
        println("Miyav miyav...") // Papağanlar miyavlamaz!
    }
}

fun main() {
    val papagan = Papagan()
    papagan.beslenme() // Hayvan besleniyor...
    papagan.ucma() // Uçuyorum...
    papagan.konusma() // Merhaba...
    papagan.miyavlama() // Papağanlar miyavlamaz!
}

```

## Notlar:

* Bu örnekler, Kotlin'de kalıtım türlerinin nasıl kullanılabileceğini gösterir.
* Gerçek uygulamalarda, ihtiyaçlarınıza en uygun kalıtım türünü seçmeniz önemlidir.
* Kalıtım karmaşık bir konu olabilir, bu nedenle daha fazla bilgi edinmek için Kotlin dokümantasyonuna bakabilirsiniz.
  
Umarım bu örnekler Kotlin'de kalıtım türlerini anlamanıza yardımcı olur.