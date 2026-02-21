# airport-services-aggregator

Агрегатор услуг для путешествий

## Технологический стек

- `next@16`
- `react@19` + `react-compiler`
- `typescript@5.9`
- `tailwindcss@4`

## Окружение для локальной разработки

- **Node.js** ≥ 24.11.0
- **pnpm** ≥ 10.10.0

Рекомендуется использовать [nvm](https://github.com/nvm-sh/nvm) или [fnm](https://github.com/Schniz/fnm) для управления версией Node.js.

## Установка и запуск

```bash
# Установка зависимостей
pnpm install

# Режим разработки (http://localhost:3000)
pnpm dev

# Сборка для production
pnpm build

# Запуск production-сборки
pnpm start
```

## Правила разработки

### Линтинг

- **ESLint** — проверка кода (Next.js, Prettier, сортировка импортов)
- **TypeScript** — проверка типов без генерации файлов

```bash
# Проверка кода
pnpm lint:code

# Проверка типов
pnpm lint:types
```

Перед каждым коммитом автоматически запускаются `lint:code` и `lint:types` (pre-commit hook).

### Коммиты

Используется [Conventional Commits](https://www.conventionalcommits.org/) — сообщения коммитов проверяются через **Commitlint** и **Husky** (commit-msg hook).

Примеры допустимых сообщений:

```
feat: добавить страницу поиска
feat(api): интеграция с API расписания рейсов
fix: исправить отображение времени
fix(auth): утечка памяти при выходе из сессии
docs: обновить README
style: привести отступы к единому стилю
refactor: вынести логику фильтрации в отдельный хук
perf: оптимизировать рендер списка рейсов
test: добавить тесты для компонента SearchForm
ci: настроить GitHub Actions для деплоя
build: обновить конфигурацию Next.js
chore: обновить зависимости
chore(deps): обновить eslint до v9
```

### Форматирование

**Prettier** интегрирован в ESLint и применяется при линтинге.
