# Лабораторная работа №3
## Тема: Автоматическое развертывание статического сайта (CI/CD)

### 1. Цель работы
Реализовать сценарий автоматического развертывания статического сайта, построенного на движке MkDocs, с использованием платформ GitHub Pages и Yandex SourceCraft. Освоить принципы CI/CD, работу с множественными удаленными репозиториями и настройку токенов доступа.

### 2. Организация репозитория
Работа ведется в едином локальном репозитории. Для синхронизации кода с двумя платформами настроены два удаленных репозитория:
- **origin**: основной репозиторий на GitHub (`https://github.com/alwiest/alwiest.github.io.git`).
- **sourcecraft**: репозиторий на платформе SourceCraft (`https://git.sourcecraft.dev/sathyscylo/lr-3.git`).

Добавление второго репозитория выполнено командой:
```bash
git remote add sourcecraft https://sathyscylo:[TOKEN]@git.sourcecraft.dev/sathyscylo/lr-3.git
```
где `[TOKEN]` — персональный токен доступа (PAT), созданный в настройках безопасности SourceCraft с правами на запись.

Структура проекта:
- `src/mkdocs.yml`: конфигурационный файл генератора MkDocs
- `src/docs/`: исходные md-файлы страниц сайта
- `.github/workflows/deploy.yml`: конфигурация пайплайна для GitHub Actions
- `.sourcecraft/ci.yaml`: конфигурация пайплайна для встроенного CI SourceCraft
- `.sourcecraft/sites.yaml`: настройки публикации сайта на SourceCraft

### 3. Выполненные действия и настройки деплоя

#### 3.1. Деплой на GitHub Pages (через GitHub Actions)
Для автоматической сборки и публикации сайта на GitHub был создан workflow файл `.github/workflows/deploy.yml`.

**Настройки в репозитории GitHub:**
1. В разделе **Settings -> Actions -> General** установлены права **Read and write permissions** для рабочих процессов.
2. В разделе **Settings -> Pages** источник публикации (Source) установлен в значение **GitHub Actions**.

**Логика:**
- При пуше в ветку `main` запускается сборка сайта с помощью команды `mkdocs build`.
- Собранные статические файлы публикуются в ветку `gh-pages` с использованием экшена `peaceiris/actions-gh-pages`.

#### 3.2. Деплой на SourceCraft (через встроенный CI)
Для автоматической сборки и публикации сайта на SourceCraft использован встроенный механизм CI/CD платформы.

**Настройки в репозитории SourceCraft:**
1. Создан файл `.sourcecraft/ci.yaml`, описывающий процесс сборки Docker-контейнера с Python, установки зависимостей (`mkdocs`, `mkdocs-material`) и генерации сайта.
2. Создан файл `.sourcecraft/sites.yaml` со следующей конфигурацией:
   ```yaml
   site:
     root: "."
     ref: "release"
   ```
   Это указывает платформе брать готовые файлы из корня ветки `release`.
3. Пайплайн автоматически создает ветку `release`, копирует туда собранные HTML-файлы и выполняет принудительный пуш (`git push -f`).

### 4. Результаты
Сайт успешно развернут и доступен по следующим адресам:
1. **GitHub Pages:** [https://alwiest.github.io](https://alwiest.github.io)
2. **SourceCraft:** [https://sathyscylo.sourcecraft.site/lr-3](https://sathyscylo.sourcecraft.site/lr-3)

### 5. Вывод
В ходе лабораторной работы был реализован полный цикл CI/CD для статического сайта. Изучены механизмы PAT, работа с множественными remote-репозиториями в Git, а также настройка GitHub Actions и встроенном CI SourceCraft. Получен опыт решения проблем при работе с ветками и настройки прав доступа для автоматического деплоя.
```