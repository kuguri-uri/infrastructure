Использовался `pnpm`.

```
npm i pnpm -g
```

## Commits

Валидация сообщений коммитов через [git-commit-msg-linter](https://www.npmjs.com/package/git-commit-msg-linter). Запускается автоматически после установки.

Рекомендуемый формат сообщения:

```
<type>(<scope?>): <short summary>
```

где:

- `type` - тип коммита, например *feat|fix|docs|style|refactor|test|chore|perf|ci|build|temp*;
- `scope` - область коммита, опционально, может быть чем угодно, например *CHANGELOG|compiler|README*;
- `short summary` - краткое описание, текст в строчном регистре, без точки в конце.

Примеры:

- Плохой: `Correct spelling of CHANGELOG`;
- Хороший: `docs: correct spelling of CHANGELOG`;
- Отличный: `docs(CHANGELOG): correct spelling`.

## Linting

Для проекта добавлен и настроен `eslint`. Настройки были вынесены из `package.json` и перенесены в `.eslintrc.json`. Дополнительно добавлены исключения для тестовых файлов (модульных, так и интеграционных).

Для запуска процесса проверки необходимо воспользоваться командой:

```
pnpm run lint
```

## Tests

Они через `test.yaml`.

Данный экшен запускатся на каждый pull_request или push.

Экшен состоит из трёх этапов. Первый необходим для скачивания зависимостей проекта и создания кэша. Второй и третий этапы - прогонка модульных и интеграционных тестов соответственно - запускаются параллельно, используя закэшированные зависимости.

После завершения тестов генерируются артефакты с отчётом об итогах тестирования.

## Build & Deploy

Для сборки приложения используется экшен `build-and-deploy.yaml`.

Данный экшен запускается при изменениях в основной `master` ветке. Предварительно экшен запускает `test.yaml` для прогонки тестов и после успешного тестирования проводит сборку приложения, генерируя артефакт.



В этом репозитории находится пример приложения с тестами:

- [e2e тесты](e2e/example.spec.ts)
- [unit тесты](src/example.test.tsx)

Для запуска примеров необходимо установить [NodeJS](https://nodejs.org/en/download/) 16 или выше.

Как запустить:

```sh
# установить зависимости
npm ci

# запустить приложение
npm start
```

Как запустить e2e тесты:

```sh
# скачать браузеры
npx playwright install

# запустить тесты
npm run e2e
```

Как запустить модульные тесты:

```sh
npm test
```
