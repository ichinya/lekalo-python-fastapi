# lekalo-python-fastapi

Framework-пакет FastAPI для [Lekalo](https://github.com/ichinya/lekalo), подключаемый внутри процесса языкового адаптера [lekalo-python](https://github.com/ichinya/lekalo-python) через versioned provider API.

- FastAPI-факты: routes, dependencies, Pydantic input/output schemas;
- первый потребитель механизма framework packs — [ichinya/lekalo#197](https://github.com/ichinya/lekalo/issues/197) и [#2](https://github.com/ichinya/lekalo-python-fastapi/issues/2);
- библиотечный пакет с manifest и схемами — собственный демон не требуется.

Общий план отделения — [ichinya/lekalo#241](https://github.com/ichinya/lekalo/issues/241).
