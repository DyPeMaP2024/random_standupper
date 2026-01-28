# random_standupper

Простой инструмент для выбора **докладчика на сегодня** по производственному календарю РФ (2026), с поддержкой:

- редактируемого **пула имён**;
- списка **кого пропустить сегодня**;
- **сохранения** распределения докладчиков на все рабочие дни года (чтобы результат не менялся от запуска к запуску).

## Что внутри

- `random_standupper.py` — консольная версия.
- `random_standupper_gui.py` — кроссплатформенное десктопное приложение (GUI на `tkinter`).

## Логика

- В коде зашит список **рабочих дней 2026 года**.
- Если **сегодня нерабочий день** — выводится: `сегодня отдыхаем-с!`
- Распределение докладчиков на весь год сохраняется в JSON:
  - консоль: `assignments_2026.json`
  - GUI: `assignments_2026_gui.json`
- Распределение **пересчитывается** только если изменился вход:
  - список имён (в GUI), или
  - список `skip` (кого пропустить сегодня).

## Запуск (Linux/macOS/Windows с Python)

### Консоль

```bash
python3 random_standupper.py
```

Пропускающие (аргументами командной строки):

```bash
python3 random_standupper.py Вася Петя
```

### GUI (Desktop)

```bash
python3 random_standupper_gui.py
```

В окне приложения:
- слева — список имён (по одному в строке);
- справа — кого пропустить сегодня (по одному в строке);
- кнопка покажет, кто сегодня докладчик.

## Сборка приложения

### Windows 10 (.exe) — рекомендуемый вариант (сборка на Windows)

```cmd
py -m venv .venv
.venv\\Scripts\\activate
pip install --upgrade pip
pip install pyinstaller
pyinstaller --noconfirm --clean --onefile --windowed random_standupper_gui.py
```

Результат: `dist\\random_standupper_gui.exe`

### Windows 10 (.exe) из Linux через Wine (общая схема)

1) Установить Wine (`wine`, `winetricks`)
2) Создать отдельный `WINEPREFIX`
3) Установить Windows-Python внутри Wine
4) `wine python -m pip install pyinstaller`
5) `wine python -m PyInstaller --onefile --windowed random_standupper_gui.py`

### macOS (.app)

Сборка возможна **только на macOS**:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install pyinstaller
pyinstaller --noconfirm --clean --windowed --name RandomStandupper random_standupper_gui.py
```

Результат: `dist/RandomStandupper.app`
