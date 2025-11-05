# Инструкция для анализа Angular проектов

**Проект:** SRE-Knowledge-Base

## Цель анализа

Провести комплексный анализ Angular/TypeScript проектов на соответствие лучшим практикам разработки, качеству кода, тестированию и автоматизации. Фокус на критичных аспектах, влияющих на maintainability, security и development efficiency.

---

## 1. Тестирование и качество кода

### 1.1 Автоматизация тестов
**Проверить:**
- ✅ Наличие unit тестов (Jasmine/Karma или Jest)
- ✅ Наличие e2e тестов (Protractor/Cypress/Playwright)
- ✅ Интеграция тестов в CI/CD pipeline
- ✅ Автоматический запуск тестов при коммитах
- ✅ Test scripts в `package.json`:
  - `npm test` или `ng test`
  - `npm run e2e` или `ng e2e`
  - `npm run test:ci` (для CI окружения)

**Проблемы:**
- ❌ Нет unit тестов
- ❌ Нет e2e тестов
- ❌ Тесты не запускаются автоматически
- ❌ Тесты не включены в CI/CD

### 1.2 Тестовое покрытие
**Проверить:**
- ✅ Настройка coverage reports (Karma coverage или Jest coverage)
- ✅ Минимальный threshold покрытия (рекомендуется >70% для критичных компонентов)
- ✅ Coverage отчеты публикуются в CI/CD
- ✅ Команда `npm run test:coverage` или `ng test --code-coverage`

**Проблемы:**
- ❌ Coverage < 60% для критичных компонентов
- ❌ Coverage не отслеживается
- ❌ Нет threshold для блокировки merge при низком покрытии

### 1.3 Структура тестов
**Проверить:**
- ✅ Тесты рядом с кодом (`*.spec.ts`) или в отдельной структуре
- ✅ Использование TestBed для компонентов
- ✅ Mocking зависимостей (services, HTTP calls)
- ✅ Изоляция тестов (каждый тест независим)

**Проблемы:**
- ❌ Тесты не изолированы
- ❌ Зависимости не замоканы
- ❌ Тесты зависят от порядка выполнения

---

## 2. Статический анализ и линтинг

### 2.1 TypeScript конфигурация
**Проверить:**
- ✅ `tsconfig.json` с `strict: true`
- ✅ `noImplicitAny: true`
- ✅ `strictNullChecks: true`
- ✅ `noUnusedLocals` и `noUnusedParameters`

**Проблемы:**
- ❌ `strict: false`
- ❌ Отключены важные проверки TypeScript
- ❌ Использование `any` без необходимости

### 2.2 ESLint/TSLint
**Проверить:**
- ✅ Наличие ESLint конфигурации (`.eslintrc.json` или в `angular.json`)
- ✅ Правила для Angular best practices
- ✅ Интеграция с IDE (автоматические предупреждения)
- ✅ Запуск линтера в CI/CD

**Проблемы:**
- ❌ Нет линтера
- ❌ Линтер не запускается автоматически
- ❌ Много игнорируемых правил

### 2.3 Code formatting
**Проверить:**
- ✅ Prettier или ESLint formatting rules
- ✅ Единый стиль кода
- ✅ Автоматическое форматирование при коммитах (pre-commit hooks)

**Проблемы:**
- ❌ Нет автоматического форматирования
- ❌ Разные стили кода в проекте

---

## 3. Анализ зависимостей

### 3.1 Управление зависимостями
**Проверить:**
- ✅ Использование `package-lock.json` или `yarn.lock`
- ✅ Фиксированные версии зависимостей
- ✅ Регулярные обновления зависимостей
- ✅ Автоматизация обновлений (Renovate, Dependabot)

**Проблемы:**
- ❌ Использование `^` или `~` без lock файла
- ❌ Устаревшие зависимости (>1 год без обновлений)
- ❌ Нет автоматического отслеживания обновлений

### 3.2 Security vulnerabilities
**Проверить:**
- ✅ `npm audit` или `yarn audit` в CI/CD
- ✅ Использование `npm audit fix` или автоматических PR для security patches
- ✅ Нет критичных vulnerabilities (score >= 7)

**Проблемы:**
- ❌ Критичные security vulnerabilities не исправлены
- ❌ Audit не запускается автоматически
- ❌ Security patches не применяются своевременно

### 3.3 Bundle size и производительность
**Проверить:**
- ✅ Анализ bundle size (`ng build --stats-json` + webpack-bundle-analyzer)
- ✅ Lazy loading модулей
- ✅ Tree-shaking работает корректно
- ✅ Отслеживание размера bundle в CI/CD

**Проблемы:**
- ❌ Bundle > 2MB (initial bundle)
- ❌ Нет lazy loading
- ❌ Большие библиотеки включены целиком

---

## 4. Информационная безопасность

### 4.1 Secrets management
**Проверить:**
- ✅ Нет хардкодных API keys, passwords, tokens в коде
- ✅ Использование environment variables
- ✅ `.env` файлы в `.gitignore`
- ✅ Secrets не коммитятся в Git

**Проблемы:**
- ❌ Secrets в коде или конфигурации
- ❌ `.env` файлы в репозитории
- ❌ API keys в коде

### 4.2 Dependency vulnerabilities
**Проверить:**
- ✅ Регулярные проверки `npm audit`
- ✅ Использование Snyk, WhiteSource или аналогичных инструментов
- ✅ Security scanning в CI/CD pipeline

**Проблемы:**
- ❌ Критичные vulnerabilities не исправлены
- ❌ Нет автоматического security scanning

### 4.3 Angular security best practices
**Проверить:**
- ✅ Использование Angular sanitization для user input
- ✅ Content Security Policy (CSP) headers
- ✅ HTTPS для всех API calls
- ✅ CORS настройки корректны

**Проблемы:**
- ❌ XSS vulnerabilities (не санитизированный user input)
- ❌ HTTP вместо HTTPS
- ❌ Небезопасные CORS настройки

---

## 5. CI/CD автоматизация

### 5.1 Build automation
**Проверить:**
- ✅ Автоматическая сборка в CI/CD (Jenkins, GitLab CI, Azure DevOps, etc.)
- ✅ Build scripts настроены (`ng build --prod`)
- ✅ Build артефакты публикуются автоматически
- ✅ Build failures блокируют merge

**Проблемы:**
- ❌ Ручная сборка
- ❌ Build не запускается автоматически
- ❌ Build failures не блокируют merge

### 5.2 Deployment automation
**Проверить:**
- ✅ Использование Ansible, Terraform, или аналогичных инструментов
- ✅ Автоматический deploy после успешного build
- ✅ Blue-Green или Canary deployments
- ✅ Rollback механизм настроен

**Проблемы:**
- ❌ Ручной deploy
- ❌ Нет автоматизации деплоя
- ❌ Нет механизма rollback

### 5.3 Quality gates в CI/CD
**Проверить:**
- ✅ Тесты запускаются перед merge
- ✅ Линтер запускается в CI/CD
- ✅ Security audit в CI/CD
- ✅ Build должен пройти перед merge

**Проблемы:**
- ❌ Quality gates не настроены
- ❌ Можно мержить без прохождения тестов
- ❌ Нет проверки безопасности

---

## 6. Commit history analysis

### 6.1 Размер коммитов
**Проверить:**
- ✅ Коммиты не слишком большие
- ✅ Количество измененных файлов: **аномалия если >30 файлов**
- ✅ Количество измененных строк: **аномалия если >500 строк**
- ✅ Коммиты логически связаны

**Анализ:**
```bash
# Примеры аномалий:
git log --stat --oneline | grep -E "files? changed" | awk '{if ($4 > 30) print}'
git log --stat --oneline | grep -E "insertions?" | awk '{if ($1 > 500) print}'
```

**Проблемы:**
- ❌ Коммиты с >30 файлами (слишком большие изменения)
- ❌ Коммиты с >500 строками (слишком много изменений)
- ❌ Смешивание несвязанных изменений в одном коммите

### 6.2 Commit messages
**Проверить:**
- ✅ Следование conventional commits или похожему формату
- ✅ Четкое описание изменений
- ✅ Разделение feature и refactoring в разных коммитах
- ✅ **Аномалия: смешивание feature и refactoring в одном коммите**

**Примеры проблемных сообщений:**
- ❌ "feat: add new component and refactor old service" (смешаны feature и refactoring)
- ❌ "fix: update dependencies and add new feature" (смешаны fix и feature)
- ❌ "update code" (слишком общее)

**Правильные примеры:**
- ✅ "feat: add user profile component"
- ✅ "refactor: extract authentication service"
- ✅ "fix: resolve memory leak in data service"

### 6.3 Commit frequency и patterns
**Проверить:**
- ✅ Регулярные коммиты (не все изменения в одном коммите в конце)
- ✅ Логическая последовательность коммитов
- ✅ Нет "commit dumps" (все изменения за неделю в одном коммите)

**Проблемы:**
- ❌ Редкие большие коммиты вместо частых маленьких
- ❌ Коммиты только в конце спринта
- ❌ Нет логической последовательности

---

## 7. Angular best practices

### 7.1 Архитектура компонентов
**Проверить:**
- ✅ OnPush change detection strategy где возможно
- ✅ Разделение на smart/dumb компоненты
- ✅ Использование lazy loading для модулей
- ✅ Компоненты не слишком большие (<400 строк)

**Проблемы:**
- ❌ Все компоненты используют Default change detection
- ❌ Нет разделения на smart/dumb компоненты
- ❌ Компоненты >500 строк
- ❌ Нет lazy loading

### 7.2 RxJS best practices
**Проверить:**
- ✅ Правильное использование Observables
- ✅ Unsubscribe от subscriptions (или использование async pipe)
- ✅ Нет memory leaks от подписок
- ✅ Использование операторов вместо вложенных subscribe

**Проблемы:**
- ❌ Memory leaks (не отписываются от subscriptions)
- ❌ Nested subscribes вместо операторов
- ❌ Неправильное использование async pipe

### 7.3 Dependency Injection
**Проверить:**
- ✅ Использование DI для сервисов
- ✅ ProvidedIn: 'root' где возможно
- ✅ Нет создания экземпляров через `new`
- ✅ Правильное использование Injectable decorator

**Проблемы:**
- ❌ Создание сервисов через `new` вместо DI
- ❌ Сервисы не Injectable
- ❌ Неправильный scope сервисов

### 7.4 Performance
**Проверить:**
- ✅ Lazy loading модулей
- ✅ OnPush change detection
- ✅ TrackBy функции для *ngFor
- ✅ Виртуализация для больших списков
- ✅ Оптимизация bundle size

**Проблемы:**
- ❌ Нет lazy loading
- ❌ Нет trackBy для *ngFor
- ❌ Большие списки без виртуализации
- ❌ Большой bundle size

---

## 8. Дополнительные аспекты

### 8.1 Документация
**Проверить:**
- ✅ README.md с инструкциями по setup
- ✅ Комментарии в коде для сложной логики
- ✅ JSDoc для публичных методов
- ✅ CHANGELOG или release notes

**Проблемы:**
- ❌ Нет README
- ❌ Нет инструкций по запуску
- ❌ Отсутствует документация API

### 8.2 Environment configuration
**Проверить:**
- ✅ Разделение конфигураций для dev/staging/prod
- ✅ Environment variables используются правильно
- ✅ Нет хардкодных значений окружения

**Проблемы:**
- ❌ Хардкодные значения для разных окружений
- ❌ Нет разделения конфигураций

### 8.3 Error handling
**Проверить:**
- ✅ Global error handler настроен
- ✅ HTTP error handling (interceptors)
- ✅ User-friendly error messages
- ✅ Логирование ошибок

**Проблемы:**
- ❌ Нет global error handler
- ❌ Ошибки не обрабатываются
- ❌ Технические ошибки показываются пользователю

---

## Формат отчета

После анализа предоставить:

1. **Критичные проблемы** (блокирующие)
   - Тестирование
   - Security
   - CI/CD

2. **Важные улучшения** (высокий приоритет)
   - Best practices
   - Performance
   - Code quality

3. **Рекомендации** (средний приоритет)
   - Оптимизации
   - Документация
   - Улучшения процессов

4. **Статистика**
   - Test coverage %
   - Bundle size
   - Количество security vulnerabilities
   - Commit history anomalies

---

**Примечание:** Этот анализ фокусируется на критичных аспектах, влияющих на качество, безопасность и maintainability проекта. GitHub Actions не упоминается, так как фокус на Jenkins, Ansible и других enterprise инструментах.

