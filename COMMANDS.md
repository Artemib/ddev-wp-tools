# WP Tools - Справочник команд

Полный справочник по всем командам пакета wp-tools для работы с WordPress проектами в DDEV.

## 📋 Содержание

- [Установка](#установка)
- [Основные команды](#основные-команды)
- [Управление плагинами](#управление-плагинами)
- [DDEV команды](#ddev-команды)
- [Файлы конфигурации](#файлы-конфигурации)
- [Примеры использования](#примеры-использования)

---

## Установка

```bash
# Клонируйте репозиторий
git clone <repository-url> ~/Sites/wp-tools

# Перейдите в папку
cd ~/Sites/wp-tools

# Установите инструменты
./install-wp-tools
```

---

## Основные команды

### `wp-new <project> [Title]`

**Описание:** Создает новый WordPress проект с полной настройкой DDEV.

**Параметры:**
- `<project>` - название папки проекта (обязательно)
- `[Title]` - заголовок сайта (опционально, по умолчанию = название проекта)

**Что делает:**
- Создает папку проекта в `~/Sites/<project>`
- Инициализирует DDEV с типом WordPress
- Настраивает wildcard домены `*.project.ddev.site`
- Скачивает и устанавливает WordPress на русском языке (ru_RU)
- Создает админа: `admin` / `admin`
- Подключает phpMyAdmin add-on
- Настраивает базу данных `db` (стандартная DDEV)

**Примеры:**
```bash
wp-new mysite "Мой сайт"
wp-new blog
```

**Результат:**
- Сайт: `https://project.ddev.site`
- Wildcard: `https://any.project.ddev.site`
- phpMyAdmin: `https://project.ddev.site:8037`
- Админ: `admin` / `admin`
- База данных: `db`

---

### `wp-del <project>`

**Описание:** Полностью удаляет DDEV проект и все связанные данные.

**Параметры:**
- `<project>` - название проекта для удаления

**Что делает:**
- Останавливает и удаляет DDEV контейнеры
- Удаляет тома базы данных
- Удаляет сетевые настройки
- Удаляет папку проекта `~/Sites/<project>`

**Примеры:**
```bash
wp-del mysite
wp-del old-project
```

**⚠️ Внимание:** Эта команда необратимо удаляет все данные проекта!

---

### `wp-help [project]`

**Описание:** Показывает справку по командам или информацию о конкретном проекте.

**Параметры:**
- `[project]` - название проекта (опционально)

**Без параметров:**
- Показывает общую справку по всем командам
- Список активных DDEV проектов
- Список проектов в папке `~/Sites`
- Полезные DDEV команды
- Быстрые WP-CLI команды

**С параметром:**
- Показывает детальную информацию о проекте
- Статус DDEV контейнеров
- URL-адреса проекта

**Примеры:**
```bash
wp-help              # Общая справка
wp-help mysite       # Информация о проекте mysite
```

---

## Управление плагинами

### `wp-plugins [project] [опции]`

**Описание:** Управляет плагинами WordPress проекта.

**Параметры:**
- `[project]` - название проекта (опционально)
- `[опции]` - дополнительные опции (см. ниже)

**Общие команды (без проекта):**
- `--help` - показать справку по плагинам
- `--keys` - показать лицензионные ключи
- `--list` - показать список плагинов для установки

**Команды для проекта:**
- `<project>` - установить все плагины в проект
- `<project> --list` - показать установленные плагины в проекте

**Что делает при установке:**
- Устанавливает плагины из архивов (.zip файлы)
- Устанавливает плагины из WordPress маркета
- Показывает лицензионные ключи для активации
- Автоматически запускает проект если он не запущен

**Примеры:**
```bash
wp-plugins --help                    # Справка по плагинам
wp-plugins --keys                    # Показать лицензии
wp-plugins --list                    # Список плагинов для установки
wp-plugins mysite                    # Установить все плагины
wp-plugins mysite --list             # Показать установленные плагины
```

---

## DDEV команды

### Основные команды DDEV

```bash
ddev start                    # Запустить проект
ddev stop                     # Остановить проект
ddev restart                  # Перезапустить проект
ddev describe                 # Показать информацию о проекте
```

### Работа с WordPress

```bash
ddev wp <команда>             # Выполнить WP-CLI команду
ddev wp plugin list           # Список плагинов
ddev wp theme list            # Список тем
ddev wp user list             # Список пользователей
ddev wp search-replace 'old' 'new' --all-tables  # Замена в БД
```

### Отладка и логи

```bash
ddev ssh                      # Войти в контейнер
ddev xdebug enable            # Включить Xdebug
ddev xdebug disable           # Выключить Xdebug
ddev logs -s web              # Логи веб-сервера
ddev mailpit                  # Открыть Mailpit UI
```

### Быстрые WP-CLI команды

```bash
ddev wp plugin install query-monitor --activate
ddev wp theme install twentytwentyfour --activate
ddev wp search-replace 'https://old.tld' 'https://project.ddev.site' --all-tables
```

---

## Файлы конфигурации

### Структура пакета

```
~/Sites/wp-tools/
├── commands/                 # Исполняемые команды
│   ├── wp-new              # Создание WordPress проектов
│   ├── wp-del              # Удаление проектов
│   ├── wp-help             # Справка и информация
│   └── wp-plugins          # Управление плагинами
├── plugins/                 # Конфигурация плагинов
│   ├── plugins.txt         # Список плагинов для установки
│   ├── licenses.txt        # Лицензионные ключи
│   ├── licenses-example.txt # Пример файла лицензий
│   └── *.zip               # Архивы плагинов
├── install-wp-tools        # Установочный скрипт
├── README.md               # Основная документация
└── COMMANDS.md             # Этот справочник команд
```

### `plugins/plugins.txt`

Файл со списком плагинов для установки из WordPress маркета:

```
# Комментарии начинаются с #
classic-editor
query-monitor
contact-form-7
woocommerce
```

### `plugins/licenses.txt`

Файл с лицензионными ключами для плагинов:

```
# Формат: plugin-slug=license-key
seo-by-rank-math=your-license-key-here
wp-super-cache=your-license-key-here
clearfy-pro=your-license-key-here
```

### `plugins/*.zip`

Архивы плагинов для установки. Поместите .zip файлы плагинов в папку `plugins/`.

---

## Примеры использования

### Создание нового проекта

```bash
# Создать проект с кастомным названием
wp-new mysite "Мой новый сайт"

# Перейти в папку проекта
cd ~/Sites/mysite

# Установить плагины
wp-plugins mysite

# Запустить проект (если не запущен)
ddev start
```

### Работа с существующим проектом

```bash
# Показать информацию о проекте
wp-help mysite

# Установить плагины
wp-plugins mysite

# Показать установленные плагины
wp-plugins mysite --list

# Показать лицензии
wp-plugins --keys

# Войти в контейнер
ddev ssh

# Выполнить WP-CLI команду
ddev wp plugin install query-monitor --activate
```

### Удаление проекта

```bash
# Полностью удалить проект
wp-del mysite
```

### Создание блога

```bash
wp-new my-blog "Мой блог"
wp-plugins my-blog
```

### Создание интернет-магазина

```bash
wp-new shop "Интернет-магазин"
# Добавьте WooCommerce в plugins/plugins.txt
wp-plugins shop
```

---

## URL-адреса проектов

После создания проекта доступны следующие адреса:

- **Основной сайт:** `https://project.ddev.site`
- **Wildcard поддомены:** `https://any.project.ddev.site`
- **phpMyAdmin:** `https://project.ddev.site:8037`
- **Mailpit:** `https://project.ddev.site:8026`

---

## Особенности пакета

### WordPress проекты
- **Локализация:** ru_RU
- **База данных:** db (стандартная DDEV)
- **Поддомены:** Поддержка wildcard поддоменов
- **Админ:** admin/admin
- **URL:** https://project.ddev.site

### Плагины
- **Установка:** Только установка, без автоматической активации
- **Источники:** WordPress маркет + архивы
- **Лицензии:** Централизованное хранение ключей в `plugins/licenses.txt`

### DDEV интеграция
- **Автозапуск:** Проекты запускаются автоматически при необходимости
- **Совместимость:** Полная совместимость с DDEV
- **Контейнеры:** Использует стандартные DDEV контейнеры

---

## Устранение неполадок

### Команды не найдены
```bash
# Перезагрузите shell профиль
source ~/.zshrc  # или ~/.bashrc

# Или перезапустите терминал
```

### Проект не запускается
```bash
# Запустите проект вручную
cd ~/Sites/my-project
ddev start
```

### Плагины не устанавливаются
```bash
# Проверьте файл конфигурации
cat ~/Sites/wp-tools/plugins/plugins.txt

# Проверьте права доступа
ls -la ~/Sites/wp-tools/plugins/
```

---

## Требования

- DDEV установлен и настроен
- OrbStack или Docker Desktop
- Bash shell
- Команды должны быть в PATH

---

## Поддержка

Для получения помощи используйте:
```bash
wp-help                    # Общая справка
wp-plugins --help         # Справка по плагинам
ddev help                 # Справка DDEV
```

**Полезные ссылки:**
- **DDEV:** https://ddev.readthedocs.io/
- **WordPress CLI:** https://wp-cli.org/
- **OrbStack:** https://orbstack.dev/

---

## Лицензия

MIT License
