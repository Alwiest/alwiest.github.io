# Лабораторная работа 3
## Тема: Автоматическое развертывание сайта

### Цель работы
Настроить автоматический деплой статического сайта на MkDocs через GitHub Actions и Sourcecraft.

### Ход работы

1. Создан локальный репозиторий с сайтом на MkDocs.
2. Добавлены два удаленных репозитория:
   - origin (GitHub)
   - sourcecraft (Sourcecraft)

Команда добавления второго репозитория:
```bash
git remote add sourcecraft https://sathyscylo:[token]@git.sourcecraft.dev/sathyscylo/lr-3.git
```

3. Настроен файл .github/workflows/deploy.yml для GitHub Actions.
    - При пуше в ветку main запускается сборка сайта.
    - Готовые файлы публикуются на GitHub Pages.
4. В настройках Sourcecraft включена автоматическая сборка при обновлении кода.

### Результат

Сайт доступен по двум адресам:

1. GitHub: https://alwiest.github.io
2. Sourcecraft: https://sathyscylo.sourcecraft.site/lr-3
### Вывод
Изучены принципы CI/CD, работа с несколькими remote-репозиториями и настройка токенов доступа.