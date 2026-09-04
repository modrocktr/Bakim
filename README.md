# Bakım sayfası

Vercel projeyi kota aşımından duraklattığında ziyaretçinin göreceği sayfa.

## Neden ayrı bir yerde durmalı

Vercel bir projeyi duraklattığında o projede barındırılan **hiçbir sayfa
çalışmaz** — kendi hata ekranını gösterir. Yani "site kapanınca şu sayfa
çıksın" isteğini Vercel'in içinden çözmek mümkün değil. Bu dosya Vercel'in
dışında durmak zorunda.

`index.html` tek dosya, dış bağımlılığı yok (yazı tipi, CSS, JS hepsi içinde).
Nereye konursa konsun çalışır.

## Şimdiden hazırlık (site kapanmadan yap)

1. **DNS TTL'ini düşür.** Squarespace DNS panelinde `modrocktr.com` A kaydının
   TTL'ini en düşük değere çek (genelde 300 sn). Yoksa kayıt değiştirildiğinde
   yayılması saatler sürer.

2. **GitHub Pages deposunu kur.**
   - Bu klasörü ayrı bir depoya koy (ör. `modrocktr/bakim`)
   - Depo → Settings → Pages → Source: `main` dalı, kök klasör
   - `username.github.io/bakim` adresinden açıldığını doğrula

3. **Alan adını GitHub'a önceden doğrulat.** GitHub → Settings → Pages →
   "Verify domain": verdiği TXT kaydını Squarespace DNS'e ekle. TXT kaydı A
   kaydını etkilemez, yani site çalışırken bunu yapabilirsin. Böylece kapanma
   anında alan adını eklemek anlık olur.

## Site kapandığında (2 adım)

1. GitHub deposu → Settings → Pages → Custom domain: `modrocktr.com`
2. Squarespace DNS → `modrocktr.com` A kaydını GitHub Pages IP'lerine çevir:

   ```
   185.199.108.153
   185.199.109.153
   185.199.110.153
   185.199.111.153
   ```

   (Vercel'in `216.198.79.1` kaydını sil.)

## Site geri geldiğinde

A kaydını Vercel'e geri çevir (`216.198.79.1`) ve GitHub Pages'ten custom
domain'i kaldır. Vercel panelinde alan adı birkaç dakika "yapılandırılıyor"
görünebilir, sonra düzelir.
