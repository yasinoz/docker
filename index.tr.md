---
title: Docker Laboratuvarları
lang: tr
slug: index
section: index
order: 0
status: updated
upstream: index.md
---
# Docker Laboratuvarları

Uygulamalı Docker laboratuvarları — container, imaj, Compose ve
orkestrasyon. Her şey kendi makinenizde çalışır.

> 🇬🇧 [English version](index.md)

## Ön Koşullar

İlk lab'a başlamadan **önce** şunları yapın:

1. **[Ortamınızı kurun](setup/README.md)** — Docker, Git ve bir terminal.
2. **Lab dosyalarını indirin:**

   ```
   git clone https://github.com/yasinoz/docker.git
   cd docker
   ```

3. **Docker Hub'a giriş yapın** (ücretsiz hesap). Sınıf ortamında bu opsiyonel
   değil: Docker Hub anonim imaj çekme işlemlerini *IP adresi başına*
   sınırlıyor; aynı bağlantıyı paylaşan yirmi kişi limiti doldurur ve lab'ın
   ortasında `toomanyrequests` hatası alır.

   ```
   docker login
   ```


<!-- labs:start -->

## Container Temelleri

Container çalıştırmak, imaj derlemek ve registry kullanmak.

| Lab | Süre | Gerekir |
|---|---|---|
| [Container Çalıştırmak](labs/containers/README.md) _(EN)_ | 40 dk | docker |
| [Container Ortamını Kurmak](labs/env/README.md) _(EN)_ | 40 dk | docker |
| [Container İmajları Derlemek](labs/images/README.md) _(EN)_ | 45 dk | docker |
| [Registry Üzerindeki İmajlara Erişmek](labs/registries/README.md) _(EN)_ | 30 dk | docker |

## Docker Compose

Çok container'lı uygulamaları modellemek ve çalıştırmak.

| Lab | Süre | Gerekir |
|---|---|---|
| [Docker Compose](labs/compose/README.md) _(EN)_ | 45 dk | docker |
| [Compose ile Uygulama Modellemek](labs/compose-model/README.md) _(EN)_ | 45 dk | docker |
| [Compose ile Uygulama Derlemek](labs/compose-build/README.md) _(EN)_ | 45 dk | docker |
| [Compose'un Sınırları](labs/compose-limits/README.md) _(EN)_ | 35 dk | docker |

## İleri İmaj ve Ağ

Çok aşamalı build ve container'ların birbiriyle konuşması.

| Lab | Süre | Gerekir |
|---|---|---|
| [Çok Aşamalı Build](labs/multi-stage/README.md) _(EN)_ | 40 dk | docker |
| [Container Ağı](labs/networking/README.md) _(EN)_ | 40 dk | docker |

## Orkestrasyon

Container'ları birden fazla makinede çalıştırmak.

| Lab | Süre | Gerekir |
|---|---|---|
| [Docker Swarm ile Orkestrasyon](labs/orchestration/README.md) _(EN)_ | 50 dk | docker |
| [Kubernetes](labs/kubernetes/README.md) _(EN)_ | 50 dk | docker |

## Gerçek Dünya

Ne bozulur ve sebebini nasıl bulursunuz.

| Lab | Süre | Gerekir |
|---|---|---|
| [Container'lı Uygulamalarda Sorun Giderme](labs/troubleshooting/README.md) _(EN)_ | 50 dk | docker |

<!-- labs:end -->

## Bir lab nasıl işler

Her lab aynı kalıbı izler:

- **Kaynaklar** — gerçek dökümantasyona bağlantılar.
- **Anlatım** — adım adım yönlendirme, komutlar kopyala-yapıştır çalışır.
- 📋 **Görevler** — bunları kendiniz çözeceksiniz; cevap hemen altındaki
  `Takıldınız mı?` bloğunda gizli.
- **Lab** — anlatımı olmayan, daha zor bir alıştırma. `hints` yol gösterir,
  `solution` cevabı verir.
- **Temizlik** — mutlaka çalıştırın; yoksa sonraki lab aynı portlar için
  kavga eder.

> Henüz Türkçeye çevrilmemiş lablar listede _(EN)_ işaretiyle görünür ve
> İngilizce sürümüne bağlanır. Çeviri durumu dosya varlığından okunur.

## Durum

Lablar 2021-2025 arası bir kaynaktan modernize edildi. Mekanik düzeltmeler
(compose v2, güncel imaj sürümleri, kırık bağlantılar) uygulandı; lablar
henüz uçtan uca çalıştırılarak doğrulanmadı.

Bozuk bir şey bulursanız issue açın — derste patlayan bir lab, hiç olmayan
lab'dan kötüdür.

## Emeği Geçenler

[Elton Stoneman](https://github.com/sixeyed) tarafından hazırlanan
[courselabs/docker](https://github.com/courselabs/docker) çalışmasından
türetilmiştir; CC BY-SA 4.0 kapsamında kullanılmış ve yeniden dağıtılmıştır.
Ayrıntı: [ATTRIBUTION.md](ATTRIBUTION.md).

Türkçe çeviri, modernizasyon ve lab altyapısı:
[Mehmet Yasin Özkasapoğlu](https://github.com/yasinoz) — `sudo2go`.
