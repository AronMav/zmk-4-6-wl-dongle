# ZMK конфигурация для Charybdis 4x6 Wireless с донглом

Конфигурация прошивки ZMK для сплит-клавиатуры Charybdis 4x6 с беспроводной поддержкой и USB-донглом.

## Возможности

- Поддержка ZMK Studio для настройки раскладки
- Автоматическая визуализация раскладки через keymap-drawer
- Pre-commit хуки для контроля качества кода
- CI/CD через GitHub Actions
- Полноценная поддержка русской и английской раскладки

## Слои клавиатуры

| Слой      | Описание                      |
| --------- | ----------------------------- |
| Base EN   | Основной английский слой      |
| Lower EN  | Навигация и цифры (английский)|
| Raise EN  | Символы (английский)          |
| Base RU   | Основной русский слой         |
| Lower RU  | Навигация и цифры (русский)   |
| Raise RU  | Символы (русский)             |
| Mouse     | Управление мышью (трекбол)    |
| Media     | Медиа-клавиши                 |
| Function  | Управление Bluetooth          |

## Особенности раскладки

### Переключение языка

- Переключение языка осуществляется через **Win+Space** (Super+Space)
- На слое Raise EN: клавиша для перехода на русскую раскладку
- На слое Raise RU: клавиша для перехода на английскую раскладку

### Специальные функции

- **Двойной Shift** = Caps Word (заглавные буквы для одного слова)
- **Комбо для Х**: одновременное нажатие соседних клавиш на русском слое
- **Комбо для Ъ**: одновременное нажатие соседних клавиш на русском слое
- Макросы для ввода специальных символов (@, $, #, |, &, <, >, [, ], {, }, ') на русской раскладке

### Системные комбо

| Комбо                            | Действие                      |
| -------------------------------- | ----------------------------- |
| Крайние левые верхние клавиши    | Bootloader (левая половина)   |
| Крайние правые верхние клавиши   | Bootloader (правая половина)  |
| F1 + Q                           | Сброс (левая половина)        |
| F12 + P                          | Сброс (правая половина)       |
| F2 + A                           | Bluetooth профиль 0           |
| F3 + S                           | Bluetooth профиль 1           |
| F4 + D                           | Bluetooth профиль 2           |
| F5 + F                           | Очистить Bluetooth            |
| F1 + F5                          | Разблокировать ZMK Studio     |

## Настройка Linux

Для корректной работы переключения языка на Linux необходимо настроить переключение раскладки через **Super+Space**.

### GNOME (Ubuntu, Fedora)

```bash
# Установить переключение раскладки на Super+Space
gsettings set org.gnome.desktop.wm.keybindings switch-input-source "['<Super>space']"
gsettings set org.gnome.desktop.wm.keybindings switch-input-source-backward "['<Shift><Super>space']"
```

Или через GUI:

1. Настройки → Клавиатура → Сочетания клавиш
2. Найти "Переключение на следующий источник ввода"
3. Установить Super+Space

### KDE Plasma

1. Системные настройки → Устройства ввода → Клавиатура → Раскладки
2. Включить "Настроить раскладки"
3. Добавить нужные раскладки (Русский, Английский)
4. В разделе "Переключение" выбрать "Meta+Space" (или настроить вручную)

Альтернативно через командную строку:

```bash
# Проверить текущие настройки
kreadconfig5 --file kxkbrc --group Layout --key SwitchMode
# Настроить переключение (может потребоваться перезапуск)
kwriteconfig5 --file kxkbrc --group Layout --key SwitchMode "Global"
```

### X11 (универсальный способ)

Добавить в `~/.xprofile` или `~/.xinitrc`:

```bash
# Настройка раскладок с переключением по Super+Space
setxkbmap -layout us,ru -option grp:win_space_toggle
```

Или создать файл `/etc/X11/xorg.conf.d/00-keyboard.conf`:

```
Section "InputClass"
    Identifier "system-keyboard"
    MatchIsKeyboard "on"
    Option "XkbLayout" "us,ru"
    Option "XkbOptions" "grp:win_space_toggle"
EndSection
```

### Wayland (Sway, Hyprland)

Для **Sway** добавить в `~/.config/sway/config`:

```
input type:keyboard {
    xkb_layout us,ru
    xkb_options grp:win_space_toggle
}
```

Для **Hyprland** добавить в `~/.config/hypr/hyprland.conf`:

```
input {
    kb_layout = us,ru
    kb_options = grp:win_space_toggle
}
```

## Настройка разработки

### Pre-commit хуки

В репозитории используются pre-commit хуки для обеспечения качества кода.

**Установка:**

```bash
# Установить pre-commit
pip install pre-commit

# Установить хуки
pre-commit install
pre-commit install --hook-type commit-msg
```

**Проверки:**

- Форматирование C/C++ кода (clang-format)
- Форматирование YAML/JSON/Markdown (prettier)
- Проверка сообщений коммитов (conventional commits)
- Удаление trailing whitespace
- Валидация YAML
- Проверка на большие файлы

### Формат сообщений коммитов

Используется формат conventional commits:

```
<тип>: <описание>

[опциональное тело]

[опциональный футер]
```

**Типы:** `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert`

**Примеры:**

```bash
git commit -m "feat: добавить слой для скролла мыши"
git commit -m "fix: исправить поворот thumb cluster в physical layout"
```

## Сборка прошивки

Прошивка автоматически собирается через GitHub Actions при каждом push. Скачать последнюю сборку можно во вкладке Actions.

### Ручная сборка

1. Форкнуть репозиторий
2. Внести изменения в конфигурацию
3. Push в репозиторий
4. Скачать артефакты из GitHub Actions

## Визуализация раскладки

Диаграммы раскладки автоматически генерируются и сохраняются в папку `keymap-drawer/` при каждом push.

## Прошивка клавиатуры

1. Скачать ZIP-архив с прошивкой из GitHub Actions
2. Распаковать архив
3. Перевести нужную половину клавиатуры (или донгл) в режим bootloader:
   - Использовать комбо (см. таблицу выше)
   - Или дважды нажать кнопку reset на плате
4. Скопировать соответствующий `.uf2` файл на появившийся диск

## Полезные ссылки

- [ZMK Documentation](https://zmk.dev/docs)
- [ZMK Studio](https://zmk.studio)
- [Keymap Drawer](https://github.com/caksoylar/keymap-drawer)
