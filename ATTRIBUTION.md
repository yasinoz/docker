# Atıf / Attribution

## Türkçe

Bu repo, **courselabs/docker** çalışmasından türetilmiştir.

- **Özgün eser:** [Docker Course Labs](https://github.com/courselabs/docker)
- **Özgün yazar:** [Elton Stoneman](https://github.com/sixeyed) — *Learn Docker
  in a Month of Lunches* ve *Learn Kubernetes in a Month of Lunches*
  kitaplarının yazarı
- **Özgün yayın:** https://docker.courselabs.co
- **Lisans:** [Creative Commons Attribution-ShareAlike 4.0 International](LICENSE)
  (CC BY-SA 4.0)
- **Türetildiği sürüm:** `bb2fed6` (2025-01-07) — bu repoda `upstream-baseline`
  etiketiyle işaretlidir

CC BY-SA 4.0 lisansı gereği:

1. Özgün yazara atıf yapılmıştır (bu dosya).
2. Yapılan değişiklikler belirtilmiştir (aşağıda).
3. Bu türetilmiş eser **aynı lisansla** (CC BY-SA 4.0) dağıtılmaktadır.

### Yapılan değişiklikler

- `docker-compose` (v1) çağrıları `docker compose` (v2) olarak değiştirildi —
  v1 Haziran 2023'te EOL oldu ve Docker Desktop ile gelmiyor
- Container imajları güncel sürümlere taşındı; sürüm matrisi:
  [`VERSIONS.yaml`](https://github.com/yasinoz/labs-platform/blob/main/VERSIONS.yaml)
- Kırık göreli bağlantılar onarıldı (Jekyll'e özgü mutlak yollar ve Windows
  ters bölü işaretleri)
- İki dilli yapı eklendi (`sections.yaml`, `manifest.json`, `*.tr.md`)
- Lab doğrulama altyapısı eklendi (`.github/workflows/validate.yml`)
- Tarama/analiz lablarının hedefi olan imajlar **bilinçli olarak eski
  bırakıldı** — güncellenirse o lablar anlamsız hale gelir

Tüm değişiklikler: `git diff upstream-baseline`

Bu değişiklikler **özgün yazarın onayı veya katılımı olmadan** yapılmıştır;
hatalar bu reponun sorumluluğundadır, courselabs'in değil.

---

## English

This repository is derived from **courselabs/docker**.

- **Original work:** [Docker Course Labs](https://github.com/courselabs/docker)
- **Original author:** [Elton Stoneman](https://github.com/sixeyed)
- **Original site:** https://docker.courselabs.co
- **Licence:** [Creative Commons Attribution-ShareAlike 4.0 International](LICENSE)
  (CC BY-SA 4.0)
- **Derived from:** commit `bb2fed6` (2025-01-07), tagged `upstream-baseline` here

As required by CC BY-SA 4.0: the original author is credited, the changes are
documented above, and this derivative work is distributed under the **same
licence**. See `git diff upstream-baseline` for the complete set of changes.

Changes were made **without the involvement or endorsement of the original
author**. Any errors introduced here are the responsibility of this repository,
not of courselabs.
