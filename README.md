# travel-services-aggregator

Агрегатор услуг для путешествий

- [Технологический стек](#технологический-стек)
- [Установка и запуск](#установка-и-запуск)
  - [Окружение для локальной разработки](#окружение-для-локальной-разработки)
- [Правила разработки](#правила-разработки)
  - [Линтинг](#линтинг)
  - [Ветки](#ветки)
  - [Коммиты](#коммиты)
  - [Форматирование](#форматирование)
- [CI/CD](#cicd)
  - [Стэнды](#стэнды)
  - [Continuous Integration](#continuous-integration)
    - [Триггеры](#триггеры)
    - [Этапы пайплайна](#этапы-пайплайна)
    - [Docker-образ](#docker-образ)
  - [Continuous Delivery](#continuous-delivery)

## Технологический стек

- `next@16`
- `react@19` + `react-compiler`
- `typescript@5.9`
- `tailwindcss@4`

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

### Окружение для локальной разработки

- **Node.js** ≥ 24.11.0
- **pnpm** ≥ 10.10.0

Рекомендуется использовать [nvm](https://github.com/nvm-sh/nvm) или [fnm](https://github.com/Schniz/fnm) для управления версией Node.js.

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

### Ветки

Для каждой задачи или фичи необходимо создавать отдельную ветку от `main`. Работа напрямую в `main` запрещена.

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

## CI/CD

### Стэнды

- [Dev](https://travel-services-aggregator.dev.1cepeak-shelter.ru/)

### Continuous Integration

Сборка и релиз настроены через **GitHub Actions** (`.github/workflows/release.yml`).

#### Триггеры

- **Push** в ветку `main`
- **Pull Request** в ветку `main`

#### Этапы пайплайна

1. Установка зависимостей
2. Линтинг (`pnpm lint:code`, `pnpm lint:types`)
3. Сборка кода (`pnpm build`)
4. Сборка Docker-образа и публикация в GitHub Container Registry (только при push в `main`):
   - Сборка Docker-образа
   - Генерация attestation для проверки происхождения образа
   - Публикация в **GitHub Container Registry** (`ghcr.io`)

#### Docker-образ

Образ публикуется в `ghcr.io` (GitHub Container Registry) и может быть использован для развёртывания:

```bash
docker pull ghcr.io/1cepeak/travel-services-aggregator:main
```

### Continuous Delivery

TODO