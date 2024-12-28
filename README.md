# get_next_line
My école 42 get_next_line project

# get_next_line

`get_next_line` projesi, bir dosyadan veya standart girdiden satır satır okuma işlemini gerçekleştiren bir fonksiyonun yazılmasını amaçlar. Bu proje, düşük seviyeli dosya işlemleri, bellek yönetimi ve buffer kullanımı konularında pratik yapmanıza olanak tanır.

## İçindekiler

1. [Projenin Amacı](#projenin-amacı)
2. [Fonksiyon Prototipi](#fonksiyon-prototipi)
3. [Kurulum](#kurulum)
4. [Kullanım](#kullanım)
5. [Fonksiyonların Açıklamaları ve Örnek Kullanımları](#fonksiyonların-açıklamaları-ve-örnek-kullanımları)
6. [Katkıda Bulunma](#katkıda-bulunma)
7. [Lisans](#lisans)

---

## Projenin Amacı

`get_next_line` projesinin hedefleri şunlardır:

- Dosya veya standart girdiden satır satır veri okumayı öğrenmek.
- Bellek yönetimi ve dinamik tahsis ile çalışma.
- Statik değişkenlerin kullanımı ve bunların çoklu dosya tanımlayıcılarıyla (multi-FD) nasıl yönetileceğini anlamak.

---

## Fonksiyon Prototipi

```c
char *get_next_line(int fd);
```

### Parametreler
- `fd`: Dosya tanımlayıcısı (file descriptor).

### Dönüş Değeri
- Başarıyla okunan bir satırı içeren bir karakter dizisi (string).
- Eğer EOF (End of File) ulaşılmışsa ve okunacak veri kalmamışsa `NULL` döner.
- Bir hata durumunda `NULL` döner.

---

## Kurulum

1. Projeyi bilgisayarınıza klonlayın:
   ```bash
   git clone https://github.com/kullanici_adi/get_next_line.git
   cd get_next_line
   ```

2. Kütüphaneyi oluşturmak için `make` komutunu çalıştırın:
   ```bash
   make
   ```
   Bu işlem sonucunda bir `get_next_line.a` dosyası oluşturulacaktır.

---

## Kullanım

`get_next_line` fonksiyonunu bir projede kullanmak için aşağıdaki gibi bir `gcc` komutu kullanabilirsiniz:

```bash
gcc -Wall -Wextra -Werror -L. -lget_next_line your_program.c -o your_program
```

Bu komut:
- `-L.`: Kütüphane dosyasının bulunduğu dizini belirtir.
- `-lget_next_line`: `get_next_line.a` kütüphanesini kullanır.

---

## Fonksiyonların Açıklamaları ve Örnek Kullanımları

### 1. `get_next_line`
**Tanım:** Belirtilen dosya tanımlayıcısından bir satır okur ve döndürür.

**Prototip:**
```c
char *get_next_line(int fd);
```

**Örnek Kullanım:**
```c
#include "get_next_line.h"
#include <fcntl.h>
#include <stdio.h>

int main() {
    int fd = open("example.txt", O_RDONLY);
    if (fd == -1) {
        perror("Dosya açılamadı");
        return 1;
    }

    char *line;
    while ((line = get_next_line(fd)) != NULL) {
        printf("%s", line);
        free(line);
    }

    close(fd);
    return 0;
}
```

### 2. Buffer Kullanımı
**Açıklama:**
`get_next_line` fonksiyonu, dosya okuma işlemleri sırasında `BUFFER_SIZE` boyutunda bir buffer kullanır. Bu boyut, derleme sırasında tanımlanabilir:

```bash
gcc -D BUFFER_SIZE=42 your_program.c get_next_line.c -o your_program
```

**Örnek:**
Eğer `BUFFER_SIZE` tanımlanmazsa, varsayılan olarak belirlenmiş bir değer kullanılır.

---

## Katkıda Bulunma

Bu projeyi geliştirmek için katkıda bulunmak isterseniz, lütfen şu adımları takip edin:

1. Projeyi forklayın.
2. Yeni bir dal oluşturun:
   ```bash
   git checkout -b yeni-ozellik
   ```
3. Değişikliklerinizi yapın ve commitleyin:
   ```bash
   git commit -m "Yeni özellik eklendi"
   ```
4. Değişikliklerinizi GitHub'a gönderin:
   ```bash
   git push origin yeni-ozellik
   ```
5. Bir pull request oluşturun.

---

## Lisans

Bu proje herhangi bir lisansla sınırlandırılmamıştır. İstediğiniz gibi kullanabilirsiniz.

---

Daha fazla bilgi için benimle iletişime geçmekten çekinmeyin! 🎉

