_English version: [README.md](README.md)_

# ASNForge

ASNForge создаёт воспроизводимые артефакты данных об ASN и происхождении префиксов (prefix-origin) для обогащения IP-данных, аналитики маршрутизации и конвейеров данных безопасности. Он компилирует публичные данные реестров и маршрутизации в компактную IP-to-ASN базу MaxMind DB, канонические таблицы ASN, снимки prefix-origin, метаданные сборки, контрольные суммы и архивы, готовые к выпуску.

<p align="center">
  <img src="./site/banner.png" alt="ASNForge routing and registry intelligence compiler" width="100%">
</p>

<p align="center">
  <a href="https://github.com/ipanalytics/ASNforge/actions/workflows/ci.yml"><img alt="CI" src="https://img.shields.io/github/actions/workflow/status/ipanalytics/ASNforge/ci.yml?branch=main&label=ci"></a>
  <a href="https://github.com/ipanalytics/ASNforge/releases"><img alt="Release" src="https://img.shields.io/github/v/release/ipanalytics/ASNforge?include_prereleases&label=release"></a>
  <a href="./LICENSE"><img alt="License" src="https://img.shields.io/badge/license-Apache%202.0-blue"></a>
  <img alt="Go" src="https://img.shields.io/badge/go-1.22%2B-00ADD8">
  <img alt="Dataset" src="https://img.shields.io/badge/dataset-public--safe-success">
  <a href="https://ipanalytics.github.io/ASNforge/"><img alt="GitHub Pages" src="https://img.shields.io/badge/pages-docs-brightgreen"></a>
</p>

---


<!-- ASNFORGE:RELEASE-STATS BEGIN -->
## Статистика последнего релиза

| Поле | Значение |
| --- | ---: |
| Идентификатор сборки | `20260912-130901Z` |
| Профиль | `public-safe` |
| Сгенерировано | `2026-09-12T13:09:01Z` |
| Качество | `PASS` |
| ASN-профилей | 140,493 |
| ASN-профилей с именами | 122,113 |
| Префиксов | 1,471,704 |
| Префиксов, вставленных в MMDB | 1,471,704 |
| Префиксов MOAS | 13,545 |
| Записей с приватными ASN | 152 |
| Записей с зарезервированными ASN | 28 |
| ASN неизвестного типа | 126,348 |
| Длительность сборки, секунды | 69.92 |

## Источники

| Имя | URL | Размер | SHA256 |
| --- | --- | ---: | --- |
| `afrinic` | [delegated-afrinic-extended-latest](https://ftp.afrinic.net/pub/stats/afrinic/delegated-afrinic-extended-latest) | 992,722 | `66f1d06b8f27` |
| `apnic` | [delegated-apnic-extended-latest](https://ftp.apnic.net/stats/apnic/delegated-apnic-extended-latest) | 9,230,393 | `14fea13a7d6b` |
| `arin` | [delegated-arin-extended-latest](https://ftp.arin.net/pub/stats/arin/delegated-arin-extended-latest) | 12,777,947 | `adaaabf0ef8c` |
| `lacnic` | [delegated-lacnic-extended-latest](https://ftp.lacnic.net/pub/stats/lacnic/delegated-lacnic-extended-latest) | 4,562,227 | `51e3e77910dc` |
| `ripe` | [delegated-ripencc-extended-latest](https://ftp.ripe.net/pub/stats/ripencc/delegated-ripencc-extended-latest) | 18,054,950 | `f1721be8041b` |
| `ed2d58969c8c-table.jsonl` | [table.jsonl](https://bgp.tools/table.jsonl) | 75,918,047 | `af581f105d6f` |
| `asn_catalog` | [asns.csv](https://bgp.tools/asns.csv) | 5,569,562 | `79c9dd2e2e4e` |
| `asn_signals` | [asn-signals.csv](https://raw.githubusercontent.com/ipanalytics/IP-Knowledge-Layer/main/data/current/asn-signals.csv) | 119 | `f27bb5dba8a1` |
| `asn_signals` | [asn-signals.csv](https://raw.githubusercontent.com/ipanalytics/ASN-Signal-Graph/main/data/current/asn-signals.csv) | 606,331 | `e96515cd0805` |

## Артефакты

| Артефакт | Размер | Записей |
| --- | ---: | ---: |
| `asnforge-asn.csv.gz` | 2,864,927 | 140,493 |
| `asnforge-asn.jsonl.gz` | 3,628,119 | 140,493 |
| `asnforge-diff.json` | 224 | - |
| `asnforge-prefixes.csv.gz` | 8,856,313 | 1,471,704 |
| `asnforge-prefixes.jsonl.gz` | 10,837,876 | 1,471,704 |
| `asnforge.mmdb.gz` | 6,164,017 | 1,471,704 |
| `manifest.json` | 3,719 | - |
| `quality-report.md` | 2,664 | - |

## Числовые изменения (Diff)

| Метрика | Значение |
| --- | ---: |
| `baseline` | true |
| `new_asns` | 0 |
| `removed_asns` | 0 |
| `changed_asn_profiles` | 0 |
| `new_prefixes` | 0 |
| `removed_prefixes` | 0 |
| `changed_prefix_origins` | 0 |
| `new_moas_prefixes` | 0 |
| `resolved_moas_prefixes` | 0 |

## Качество

Предупреждений и ошибок нет.
<!-- ASNFORGE:RELEASE-STATS END -->



















































































































## Обзор

ASNForge — это локальный компилятор наборов данных о ASN-профилях и происхождении префиксов (prefix-origin). Он предназначен для команд, которым нужны детерминированные, поддающиеся проверке артефакты вместо собираемых скриптами ad hoc файлов обогащения.

Конвейер v0.1 принимает делегированную статистику RIR, экспорты prefix-origin и каталога ASN из bgp.tools, статические сигнальные ленты ipanalytics, нормализованные локальные входные данные и курируемые переопределения. Он выдаёт стабильные таблицы JSONL/CSV для аналитики и соединений (join), а также компактную базу MaxMind DB для чувствительного к задержкам обогащения IP-данных.

Компилятор записывает идентификаторы сборок, версии схем, хеши источников, хеши артефактов, результаты проверки качества и манифесты релизов, чтобы сгенерированные данные можно было отслеживать и сравнивать между сборками.

## Поведение системы

```text
RIR delegated stats     manual overrides
        │                    │
        ▼                    ▼
   ASN allocation table ── ASN profile normalization
        │                    │
        │                    ▼
BGP prefix-origin feed ── prefix-origin aggregation ── MOAS policy
        │                    │
        ├───────────────┬────┴───────────────┐
        ▼               ▼                    ▼
  ASN JSONL/CSV   Prefix JSONL/CSV       Compact MMDB
  ASN -> profile  prefix -> origins      IP -> ASN profile
```

ASNForge создаёт три связанных семейства артефактов:

| Артефакт | Схема доступа | Назначение |
| --- | --- | --- |
| `asnforge.mmdb` | IP-адрес -> профиль ASN-источника | MaxMind DB с ключом по префиксу для локального обогащения |
| `asnforge-asn.jsonl` / `.csv` | ASN -> профиль ASN | Каноническая таблица для прямого поиска по ASN и операций соединения |
| `asnforge-prefixes.jsonl` / `.csv` | Префикс -> наблюдаемое состояние источника | Снимок соответствий префикс-источник с состоянием MOAS и коллекторов |

## Возможности

- Парсер расширенного формата RIR delegated для записей о выделениях ASN.
- Нормализованный парсер CSV/TSV соответствий префикс-источник BGP с агрегацией с учётом коллекторов.
- Парсер полных таблиц bgp.tools для production-снимков соответствий префикс-источник.
- Парсер каталога ASN bgp.tools для имён ASN и грубых классов источников.
- Статическое обогащение ASN-сигналами из IP-Knowledge-Layer и ASN-Signal-Graph.
- Консервативный резервный механизм классификации по именам для очевидных категорий ASN.
- Ручные переопределения ASN для курируемых значений имени, организации, типа, тегов, уровня доверия и источников полей.
- Обработка MOAS с детерминированными политиками: `mark_ambiguous`, `most_observed`, `lowest_asn`.
- Обработка частных и зарезервированных ASN с политиками `flag`, `drop` и `keep`.
- Компактный модуль записи MaxMind DB для поиска по IP-префиксам.
- Стабильные выходные файлы JSONL и CSV с фиксированными заголовками и отсортированными записями.
- Метаданные сборки с хешами источников, хешами артефактов, версией схемы, идентификатором сборки и вердиктом качества.
- Smoke-тесты, команда валидации, контрольные суммы, манифест релиза и вывод diff относительно базовой версии.
- CI GitHub Actions и релизный workflow для публикации артефактов по расписанию или по тегам.

## Быстрый старт

Профиль локальной разработки детерминирован и не требует доступа к сети.

```sh
go run ./cmd/asnforge build \
  --config config/local-dev.yaml \
  --out release/current \
  --build-id local-dev

go run ./cmd/asnforge validate --out release/current --strict
```

Просмотр сгенерированных данных:

```sh
go run ./cmd/asnforge inspect-ip 8.8.8.8 \
  --mmdb release/current/asnforge.mmdb \
  --format json

go run ./cmd/asnforge inspect-asn 15169 \
  --asn-table release/current/asnforge-asn.jsonl

go run ./cmd/asnforge stats --out release/current --format json
```

## Установка

Сборка из исходного кода:

```sh
git clone https://github.com/ipanalytics/ASNforge.git
cd ASNforge
go build -o asnforge ./cmd/asnforge
```

Запуск компилятора:

```sh
./asnforge build --config config/local-dev.yaml --out release/current
./asnforge validate --out release/current --strict
```

Требования:

| Компонент | Версия |
| --- | --- |
| Go | 1.22 или новее |
| ОС | Linux, macOS или любая среда, поддерживаемая Go |
| Сеть | Требуется только для загрузки настроенных HTTP-источников |

## CLI

```text
asnforge build
asnforge download
asnforge validate
asnforge inspect-ip <ip>
asnforge inspect-asn <asn>
asnforge stats
asnforge version
```

Общие флаги:

| Флаг | По умолчанию | Описание |
| --- | --- | --- |
| `--config` | `config/public-safe.yaml` | Конфигурация сборки |
| `--out` | `release/current` | Каталог вывода релиза |
| `--cache` | `data/cache` | Каталог кеша источников |
| `--build-id` | метка времени UTC | Явный идентификатор сборки |
| `--schema-version` | `asnforge.v0.1` | Версия схемы артефактов |
| `--private-asn-policy` | значение конфигурации | `flag`, `drop` или `keep` |
| `--moas-policy` | значение конфигурации | `mark_ambiguous`, `most_observed` или `lowest_asn` |
| `--mmdb` | `<out>/asnforge.mmdb` | Путь к MMDB для сборки или команды inspect |
| `--skip-download` | `false` | Использовать кешированные/локальные файлы источников |
| `--strict` | `false` | Считать предупреждения о качестве ошибками сборки |
| `--format` | `text` | `text` или `json` там, где поддерживается |

## Выходные данные

Успешная сборка записывает полный каталог релиза:

```text
release/current/
├── asnforge.mmdb
├── asnforge.mmdb.gz
├── asnforge-asn.jsonl
├── asnforge-asn.jsonl.gz
├── asnforge-asn.csv
├── asnforge-asn.csv.gz
├── asnforge-prefixes.jsonl
├── asnforge-prefixes.jsonl.gz
├── asnforge-prefixes.csv
├── asnforge-prefixes.csv.gz
├── metadata.json
├── checksums.txt
├── quality-report.md
├── asnforge-diff.json
└── manifest.json
```

| Файл | Описание |
| --- | --- |
| `asnforge.mmdb` | Компактная база MaxMind DB для поиска профиля IP -> ASN |
| `asnforge-asn.jsonl` | Каноническая таблица профилей ASN |
| `asnforge-asn.csv` | CSV-форма таблицы профилей ASN |
| `asnforge-prefixes.jsonl` | Канонический снимок происхождения префиксов (prefix-origin) |
| `asnforge-prefixes.csv` | CSV-форма состояния происхождения префиксов |
| `metadata.json` | Метаданные сборки, хеши источников, хеши артефактов, сводка, вердикт качества |
| `checksums.txt` | Контрольные суммы SHA256 для артефактов релиза |
| `quality-report.md` | Отчёт о сборке и качестве в удобочитаемом виде |
| `asnforge-diff.json` | Структура diff относительно базовой версии или между релизами |
| `manifest.json` | Машинночитаемый манифест артефактов |

## Форматы данных

Каждая основная запись включает:

- `schema_version`
- `build_id`

Эти поля делают операции объединения (joins) явными и предотвращают случайное смешивание несовместимых сборок.

### Профиль ASN

`asnforge-asn.jsonl` и `asnforge-asn.csv` содержат одну строку на каждый ASN:

```json
{
  "schema_version": "asnforge.v0.1",
  "build_id": "local-dev",
  "asn": 15169,
  "asn_name": "Google LLC",
  "asn_org": "Google",
  "asn_type": "cloud",
  "asn_tags": ["cloud", "dns", "manual-override", "search"],
  "registration_country": "US",
  "rir": "arin",
  "asn_confidence": 100
}
```

`registration_country` — это страна выделения ресурса в реестре из делегированных данных RIR. Это не геолокация пользователя, хоста или сервиса.

### Происхождение префикса

`asnforge-prefixes.jsonl` и `asnforge-prefixes.csv` сохраняют состояние наблюдений маршрутизации:

```json
{
  "prefix": "8.8.8.0/24",
  "origin_asns": [15169],
  "selected_origin_asn": 15169,
  "moas": false,
  "origin_policy": "most_observed",
  "observation_count": 2,
  "source_collectors": ["ris-rrc00", "routeviews2"],
  "prefix_confidence": 90,
  "rpki_state": "unknown"
}
```

### Запись MMDB

MMDB индексируется по префиксу и оптимизирована для локального обогащения данных по IP:

```json
{
  "schema_version": "asnforge.v0.1",
  "build_id": "local-dev",
  "asn": 15169,
  "asn_name": "Google LLC",
  "asn_org": "Google",
  "asn_type": "cloud",
  "asn_tags": ["cloud", "dns", "manual-override", "search"],
  "registration_country": "US",
  "rir": "arin",
  "moas": false,
  "asn_confidence": 100
}
```

Подробное состояние MOAS, массивы origin-AS, наблюдения коллекторов и происхождение на уровне полей принадлежат таблицам префиксов и ASN. Исключение этих полей из MMDB сохраняет дедупликацию секции данных и обеспечивает компактность базы.

## Примечания по эксплуатации

- Сборки детерминированы при одинаковых входных данных, конфигурации, версии схемы и build id.
- Строки ASN отсортированы по числовому значению ASN.
- Строки префиксов отсортированы по семейству IP, байтам адреса и длине префикса.
- Списковые поля CSV используют стабильный порядок с разделителем-точкой с запятой.
- `metadata.json` фиксирует пути к источникам, URL, хеши SHA256, размеры, время генерации, хеши артефактов и сводку качества.
- `validate --strict` предназначен для CI и релизных workflow.

## Профили источников

| Профиль | Назначение | Требуется сеть |
| --- | --- | --- |
| `config/local-dev.yaml` | Детерминированная сборка фикстур для разработки и CI | Нет |
| `config/public-safe.yaml` | Публично безопасный (public-safe) релизный профиль, использующий делегированные файлы RIR, экспорты bgp.tools и статические фиды сигналов ASN ipanalytics | Да |
| `config/research-caida.yaml` | Публично безопасные источники плюс опциональные файлы полной выгрузки CAIDA ASRank, AS2Org и AS relationships | Да, плюс предоставляемые оператором файлы CAIDA |

Публично безопасный профиль загружает `https://bgp.tools/table.jsonl` для входных данных prefix-origin в production, `https://bgp.tools/asns.csv` для имён ASN и классов источников, а также статические необработанные экспорты CSV сигналов из IP-Knowledge-Layer и ASN-Signal-Graph. Детерминированная фикстура в `examples/testdata` намеренно ограничена профилем `config/local-dev.yaml`.

Профиль research CAIDA выделен отдельно, поскольку наборы данных CAIDA имеют собственные условия допустимого использования, цитирования и распространения. Поля CAIDA записываются в артефакты ASN JSONL/CSV и намеренно исключены из компактной MMDB.

Входные данные CAIDA research по умолчанию:

| Набор данных | Файл |
| --- | --- |
| AS2Org | `https://publicdata.caida.org/datasets/as-organizations/latest.as-org2info.txt.gz` |
| AS relationships | Актуальный `*.as-rel2.txt.bz2`, определяемый по `https://publicdata.caida.org/datasets/as-relationships/serial-2/` |
| ASRank | Предоставляемый оператором путь или URL к CSV; обход ASRank API не используется |

Репозиторий включает ежемесячный/запускаемый вручную workflow `release-caida`, который публикует prerelease с тегом `research-caida-YYYYMMDD-HHMMSSZ`.

Публично безопасный профиль v0.1 не включает данные CAIDA по умолчанию. Опциональная поддержка PeeringDB, CAIDA, RPKI и нативного MRT отслеживается как последующие профили источников и расширения парсеров.

## Сценарии использования

- Обогащение данных по IP в системах SIEM, анализа мошенничества, злоупотреблений и аналитики трафика.
- Локальные соединения (join) ASN-профилей в хранилищах данных и потоковых обработчиках.
- Снимки prefix-origin для аналитики маршрутизации и анализа MOAS.
- Воспроизводимые артефакты релизов для внутренних конвейеров данных безопасности.
- Валидация изменений сторонних реестровых и маршрутных источников на этапе сборки.

## Область применения

ASNForge v0.1 сфокусирован на форме конвейера: парсеры, нормализованные модели, детерминированные выходные данные, генерация компактных MMDB, метаданные, валидация и автоматизация релизов.

Классификация консервативна. `asn_type` — это оценочная операционная классификация, а не авторитетный факт из реестра. Уверенность (confidence) описывает согласованность источников, полноту или силу наблюдения; это не оценка риска.

## Ограничения

- Нативный парсинг MRT не реализован в v0.1.
- Входные данные prefix-origin — нормализованные CSV/TSV.
- Состояние RPKI по умолчанию — `unknown`.
- Классификация ASN без опциональных источников обогащения намеренно неполная.
- Данные живой маршрутизации различаются в зависимости от коллектора и времени сбора.

## Структура каталогов

```text
.
├── cmd/asnforge/          # CLI entry point
├── internal/asn/          # ASN models, classification, private/reserved policy
├── internal/bgp/          # Prefix-origin parser and aggregation
├── internal/build/        # Build pipeline, metadata, quality, diff
├── internal/config/       # Config loading and CLI options
├── internal/download/     # Source download, hashing, source state
├── internal/mmdb/         # MaxMind DB writer and inspector
├── internal/output/       # JSONL, CSV, gzip, checksums
├── internal/rir/          # RIR delegated parser
├── internal/smoke/        # Smoke test runner
├── config/                # Build profiles
├── schemas/               # JSON Schemas
├── examples/              # Overrides, smoke cases, deterministic testdata
├── docs/                  # Data source and artifact documentation
└── .github/workflows/     # CI and release automation
```

## Развёртывание

Артефакты релизов предназначены для публикации через GitHub Releases, а не для коммита в репозиторий.

Workflow релиза собирает CLI, запускает настроенную сборку public-safe, валидирует выходные данные, вычисляет контрольные суммы, создаёт тег релиза и загружает сжатые артефакты данных вместе с метаданными:

```sh
./asnforge build --config config/public-safe.yaml --out release/current
./asnforge validate --out release/current --strict
```

Для внутренних развёртываний выполняйте те же команды в CI и публикуйте `release/current/*` в объектное хранилище, реестры пакетов или внутренние репозитории артефактов.

## Документация

- [Источники данных](docs/DATA_SOURCES.md)
- [Сторонние данные](docs/THIRD_PARTY_DATA.md)
- [Классификация](docs/CLASSIFICATION.md)
- [Вывод в формате MMDB](docs/MMDB_OUTPUT.md)
- [Артефакты релизов](docs/RELEASE_ARTIFACTS.md)
- [Уверенность](docs/CONFIDENCE.md)

## Лицензия

ASNForge распространяется по лицензии [Apache License 2.0](LICENSE).

## Отказ от ответственности

ASNForge агрегирует реестровые и наблюдаемые данные маршрутизации для защитных, аналитических и операционных целей. Данные маршрутизации носят наблюдательный характер и могут различаться в зависимости от коллектора и времени сбора.
