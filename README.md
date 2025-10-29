# WP Tools для DDEV

Полноценный пакет инструментов для разработки WordPress проектов с использованием DDEV.

## 🚀 Быстрый старт

```bash
# Клонируйте репозиторий
git clone https://github.com/Artemib/ddev-wp-tools.git ~/Sites/wp-tools

# Перейдите в папку
cd ~/Sites/wp-tools

# Установите инструменты
./install-wp-tools

# ⚠️ ВАЖНО: Перезагрузите shell профиль для применения изменений PATH
source ~/.zshrc  # или ~/.bashrc

# Альтернативно: перезапустите терминал

# 🔧 Если команды не работают, добавьте путь вручную:
# echo 'export PATH="$HOME/Sites/wp-tools/commands:$PATH"' >> ~/.zshrc
# source ~/.zshrc
```

## 📁 Структура пакета

```
wp-tools/
├── commands/           # Исполняемые команды
│   ├── wp-new         # Создание WordPress проектов
│   ├── wp-del         # Удаление проектов
│   ├── wp-help        # Справка и информация
│   └── wp-plugins     # Управление плагинами
├── plugins/            # Конфигурация плагинов
│   ├── plugins.txt    # Список плагинов для установки
│   ├── licenses-example.txt # Пример файла лицензий
│   └── *.zip          # Архивы плагинов
├── install-wp-tools   # Установочный скрипт
├── uninstall-wp-tools # Скрипт удаления
└── README.md          # Документация
```

## 🛠 Команды

### Общие команды

```bash
wp-help                    # Показать справку
wp-plugins --keys          # Показать лицензионные ключи
wp-plugins --list          # Показать список плагинов для установки
```

### Команды для проектов

```bash
wp-new <project> [Title]   # Создать WordPress проект
wp-del <project>           # Удалить проект
wp-help <project>          # Сводка по проекту
wp-plugins <project>       # Установить плагины в проект
wp-plugins <project> --list # Показать установленные плагины
```

## 📋 Создание проекта

```bash
# Создать новый проект
wp-new my-project "Мой сайт"

# Проект будет создан в ~/Sites/my-project
# Доступен по адресу: https://my-project.ddev.site
# Поддомены: https://any.my-project.ddev.site
# PhpMyAdmin: https://my-project.ddev.site:8037
```

## 🔌 Управление плагинами

### Конфигурация

1. **Добавьте плагины в `plugins/plugins.txt`:**
   ```
   classic-editor
   query-monitor
   contact-form-7
   seo-by-rank-math
   ```

2. **Создайте файл `plugins/licenses.txt` на основе `licenses-example.txt` и добавьте лицензионные ключи:**
   ```bash
   cp ~/Sites/wp-tools/plugins/licenses-example.txt ~/Sites/wp-tools/plugins/licenses.txt
   ```
   Затем отредактируйте `licenses.txt`:
   ```
   seo-by-rank-math=your-license-key-here
   wp-super-cache=your-license-key-here
   ```

3. **Поместите архивы плагинов в `plugins/`:**
   ```
   plugins/
   ├── my-plugin.zip
   └── another-plugin.zip
   ```

### Использование

```bash
# Установить все плагины в проект
wp-plugins my-project

# Показать установленные плагины
wp-plugins my-project --list

# Показать лицензионные ключи
wp-plugins --keys
```

## ⚙️ Особенности

### WordPress проекты
- **Локализация:** ru_RU
- **База данных:** db (стандартная DDEV)
- **Поддомены:** Поддержка wildcard поддоменов
- **Админ:** admin/admin
- **URL:** https://project.ddev.site

### Плагины
- **Установка:** Только установка, без автоматической активации
- **Источники:** WordPress маркет + архивы
- **Лицензии:** Централизованное хранение ключей

### DDEV интеграция
- **Автозапуск:** Проекты запускаются автоматически
- **Совместимость:** Полная совместимость с DDEV
- **Контейнеры:** Использует стандартные DDEV контейнеры

## 🔧 Устранение неполадок

### Команды не найдены
```bash
# Перезагрузите shell профиль
source ~/.zshrc  # или ~/.bashrc

# Или перезапустите терминал
```

### Команды все еще не работают после source ~/.zshrc
```bash
# Проверьте, добавлен ли путь в .zshrc
grep "wp-tools" ~/.zshrc

# Если нет, добавьте вручную:
echo 'export PATH="$HOME/Sites/wp-tools/commands:$PATH"' >> ~/.zshrc
source ~/.zshrc

# Проверьте, что команды теперь работают:
wp-help
```

### Удаление wp-tools из системы
```bash
# Используйте скрипт удаления (может не работать в текущей сессии)
./uninstall-wp-tools

# Или очистите вручную:
# 1. Удалите записи из .zshrc
sed -i '' '/wp-tools/d' ~/.zshrc

# 2. Перезапустите терминал (ОБЯЗАТЕЛЬНО!)
exec zsh

# 3. Проверьте, что команды недоступны
wp-help  # должно показать "command not found"

# 4. Для полного удаления пакета
rm -rf ~/Sites/wp-tools/
```

**⚠️ Важно:** Для полного удаления обязательно перезапустите терминал или выполните `exec zsh`!

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

## 📝 Примеры использования

### Создание блога
```bash
wp-new my-blog "Мой блог"
wp-plugins my-blog
```

### Создание интернет-магазина
```bash
wp-new shop "Интернет-магазин"
# Добавьте WooCommerce в plugins.txt
wp-plugins shop
```

### Удаление проекта
```bash
wp-del old-project
```

## 🤝 Поддержка

- **DDEV:** https://ddev.readthedocs.io/
- **WordPress CLI:** https://wp-cli.org/
- **OrbStack:** https://orbstack.dev/

## 📄 Лицензия

MIT License
