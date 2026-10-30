<!-- work-report
scope: MmitekkUE5
root: D:\GitHub\MmitekkUE5
updated: 2026-10-30T20:09:26.659Z
status: done
-->

<!-- stage-list
-->

# MmitekkUE5 portfolio site

_Обновлено: 2026-10-31 01:09 · Статус: done · Область: MmitekkUE5_

<!-- state -->
## Текущее состояние

**Где остановились:** Сайт-портфолио полностью собран и опубликован на GitHub Pages; последняя задача — добавлен CrowVFXUE5 (№01), нумерация сдвинута до 11, счётчики обновлены, задеплоено и проверено на живой версии.

**Что проверено:** Живой сайт https://mmitekk.github.io/MmitekkUE5/ в браузере: 11 карточек, модалка CrowVFXUE5 (3 абзаца RU/EN, теги «Runtime · UE 5.2», ссылка верная), EN-описание первой строки, счётчик «11»; Pages-билд abfef91 = built; скриншот списка сделан.

**Следующий шаг:** По запросу пользователя — новые плагины добавлять по той же схеме (4 места правки). Возможный кандидат — публичный репо UnrealConfigGuard, пользователь пока не просил.

**Не повторять:** Для теста сайта в браузере автоматизации ZCode IAB: клики и reveal-анимации там не работают (кадры заморожены) — проверять через evaluate + инъекцию стиля `transition:none` + принудительный `.on`; для реальных браузеров это не баг. PATH в Git Bash сломан — задавать явно (`export PATH="/mingw64/bin:/usr/bin:/c/Python312:/c/Program Files/nodejs:$PATH"`).

<!-- stages -->
## Этапы

| Этап | Статус | Итог |
|---|---|---|
| — | — | — |

<!-- howto -->
## Как продолжить

**Окружение:** Сайт = один статический `index.html` в корне репозитория D:\GitHub\MmitekkUE5 (без сборки). GitHub Pages: ветка main, корень `/`, включён через API. Пуш: `git -C /d/GitHub/MmitekkUE5 push origin main` (remote закреплён за аккаунтом Mmitekk: `https://Mmitekk@github.com/...`).

**Команды:** Ожидание деплоя: `curl -s -H "Authorization: token $TOKEN" https://api.github.com/repos/Mmitekk/MmitekkUE5/pages/builds/latest` (TOKEN из `git credential fill`). Публичность репо: `PATCH /repos/{owner}/{repo} {"private":false}`. Синтаксис-чек JS: извлечь последний `<script>` блок и `node --check`.

**Точки входа:** Правки плагинов — 4 места в index.html: HTML-строка карточки (`a.repo`), I18N словари ru/en (`repo.X`), REPO_DATA в JS (num/name/tags/абзацы ru+en), счётчики «11» (hero-stats + section-head). После правок: commit → push → дождаться Pages build → проверить живую версию.

<!-- task:1 -->
## Задача 1 — Добавление CrowVFXUE5 на сайт — 2026-10-31

**Агент:** ZCode (GLM)

### Что сделано
- Собраны данные по репозиторию CrowVFXUE5 (публичный, desc «A raven (or a flock) that flies away as one approaches it», C++, UE 5.2): README прочитан полностью — три актора (BP_Crow/BP_Snowman/BP_CrowTrigger), BP_CrowFlock со сплайном и per-bird записью, три группы звука (Idle Caw/Alarm/Take Off), Auto Align Mesh Forward, требование пакета Animal Variety Pack.
- Добавлен первым (№01) на сайт: карточка с кратким описанием и тегом «Runtime · UE 5.2», модалка с 3 абзацами RU и EN по фактическому README.
- Существующие 10 карточек перенумерованы (02–11), обновлены num в REPO_DATA, счётчики «10» → «11» (hero-stats и section-head).
- Коммит «Add CrowVFXUE5 plugin» (abfef91) запушен, Pages-билд дождан (built), живая версия проверена.

### Изменённые файлы
- `index.html` — новая карточка №01, новый блок REPO_DATA CrowVFXUE5, ключи `repo.crow` в обоих I18N-словарях, перенумерация карточек и REPO_DATA, счётчики 10→11.

### Как проверить
- Открыть https://mmitekk.github.io/MmitekkUE5/ — 11 строк, №01 = CrowVFXUE5 «Runtime · UE 5.2».
- Клик по строке — модалка: 3 абзаца (RU/EN), кнопка «Открыть репозиторий» ведёт на github.com/Mmitekk/CrowVFXUE5.
- Счётчики: «11 repositories/репозиториев» в герое и «11» у заголовка секции.

### Решения и допущения
- CrowVFXUE5 поставлен первым как самый свежий плагин (создан 2026-10-25) — без вопроса пользователю: при прошлых добавлениях порядок «новые сверху» уже устоялся.
- Репозиторий уже публичный — переключение видимости не требовалось (в отличие от WaterFaucet/ShowerNiagara).
- В абзацах модалки упомянуто требование Animal Variety Pack (SK_Crow, анимации, звуки) — критично для установки, без него BP «битые».

### Открытые вопросы и риски
- Версии движков остальных 10 репо не перепроверялись в этот раз (последняя сверка 2026-10-18: всё актуально; SubsystemGameInstance без диапазона в README).
- UnrealConfigGuard (публичный, июльский) на сайте отсутствует — пользователь не просил.
