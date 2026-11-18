# lekalo-python-fastapi

Framework-пакет FastAPI для [Lekalo](https://github.com/ichinya/lekalo), подключаемый внутри процесса языкового адаптера [lekalo-python](https://github.com/ichinya/lekalo-python) через versioned provider API.

- FastAPI-факты: routes, dependencies, Pydantic input/output schemas;
- первый потребитель механизма framework packs — [ichinya/lekalo#197](https://github.com/ichinya/lekalo/issues/197) и [#2](https://github.com/ichinya/lekalo-python-fastapi/issues/2);
- библиотечный пакет с manifest и схемами — собственный демон не требуется.

Общий план отделения — [ichinya/lekalo#241](https://github.com/ichinya/lekalo/issues/241).

## Реализация

`crates/lekalo-python-fastapi` — самостоятельная библиотека правил: статическое разрешение приложений/роутеров, маршрутов, методов и обработчиков FastAPI. Она получает минимальные `Source`/`Symbol` факты от Python runtime и не импортирует его приватную модель. Не исполняет Python и не импортирует приложение.

```sh
cargo +1.97.0 test --locked
# Дополнительная проверка публичного process protocol с явно выбранным runtime:
LEKALO_PYTHON_ADAPTER_BIN=/absolute/path/to/lekalo-target-python node --test tests/fastapi.test.mjs
```

SDK подключён из `lekalo-adapter-sdk` по Git SHA и не хранится копией исходников. Python runtime включает provider как закреплённую библиотеку; динамическая загрузка сторонних providers остаётся отдельной задачей #2.

GitHub Actions запускает [проверки пакета](.github/workflows/ci.yml) для pull request и изменений в `main`.

The adapter SDK is supplied by an immutable Git dependency on [lekalo-adapter-sdk](https://github.com/ichinya/lekalo-adapter-sdk), recorded in Cargo.toml/Cargo.lock. There is no vendored SDK implementation in this repository.

## Portable rules

Select `gh/ichinya/lekalo-python-fastapi` in the component rules. The package supplies `contracts/http.json` for `http.routes/v1`. This opt-in check requires GET /health. The binding describes direct registrations in the listed entry files.
