<!-- work-report
scope: MmitekkUE5
root: D:\GitHub\MmitekkUE5
updated: 2026-11-03T22:00:54.386Z
status: done
-->

<!-- stage-list
-->

# MmitekkUE5 portfolio site

_Обновлено: 2026-11-04 03:00 · Статус: done · Область: MmitekkUE5_

<!-- state -->
## Текущее состояние

**Где остановились:** На сайте 13 репозиториев: добавлены два браузерных расширения — BrowserTabAudioMixer (№01, Opera GX sidebar) и BrowserStorageProfileSwitcher (№02, MV3), существующие 11 перенумерованы (03–13), версии всех перепроверены по свежим README (без изменений). Задеплоено (коммит 68f8305, Pages = built) и проверено на живой версии (DOM-проверки + скриншот).

**Что проверено:** Живой сайт: 13 карточек, модалки обоих новых расширений (3 абзаца RU/EN, теги «Extension · Opera GX · JS» / «Extension · MV3 · JS»), счётчики «13», чип «C++ · BP · Python · JS», hero-sub упоминает browser extensions в EN, CrowVFXUE5 теперь 03. Синтаксис JS (node --check) до пуша.

**Следующий шаг:** По запросу — новые плагины по той же схеме (4 места правок). Версии движков не менялись с 18.10; SubsystemGameInstance по-прежнему без диапазона в README.

**Не повторять:** Тест в браузере автоматизации ZCode IAB: клики/анимации не работают — только evaluate + инъекция `transition:none` + принудительный `.on`. PATH в Git Bash сломан — задавать явно (`export PATH="/mingw64/bin:/usr/bin:/c/Python312:/c/Program Files/nodejs:$PATH"`).

<!-- stages -->
## Этапы

| Этап | Статус | Итог |
|---|---|---|
| — | — | — |

<!-- howto -->
## Как продолжить

**Окружение:** Сайт = один статический `index.html` в корне D:\GitHub\MmitekkUE5 (без сборки). GitHub Pages: ветка main, корень `/`. Пуш: `git -C /d/GitHub/MmitekkUE5 push origin main` (remote закреплён за аккаунтом Mmitekk).

**Команды:** Ожидание деплоя: `curl -s -H "Authorization: token $TOKEN" https://api.github.com/repos/Mmitekk/MmitekkUE5/pages/builds/latest` (TOKEN из `git credential fill`). Синтаксис-чек JS: извлечь последний `<script>` блок в temp-файл и `node --check`.

**Точки входа:** Правки — 4 места в index.html: карточки `a.repo`, I18N словари ru/en (`repo.X`, `hero.sub`), REPO_DATA в JS (num/name/tags/абзацы ru+en), счётчики (hero-stats + section-head). Теперь в портфолио два типа проектов: UE5-плагины (теги с версией UE) и браузерные расширения (теги «Extension · браузер · JS»).

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

<!-- task:2 -->
## Задача 2 — BrowserTabAudioMixer + BrowserStorageProfileSwitcher и актуализация — 2026-11-04

**Агент:** ZCode (GLM)

### Что сделано
- Собраны данные по двум новым публичным репо (JavaScript, созданы 2026-11-03): BrowserTabAudioMixer — микшер громкости вкладок для Opera GX с глубокой интеграцией плееров (Twitch IVS+React-сеттер, YouTube Player API, HTML5/Shadow DOM); BrowserStorageProfileSwitcher — MV3-менеджер сессий (cookies + localStorage + sessionStorage + IndexedDB, race condition freeze, cross-account guard) для Opera GX/Chrome/Edge/Brave/Яндекс.
- Оба добавлены первыми (№01, №02), карточки + модалки 3 абзаца RU/EN по фактическим README.
- Существующие 11 карточек перенумерованы (03–13) — и на странице, и в REPO_DATA; счётчики 11 → 13.
- Актуализация: версии движков всех 11 существующих плагинов сверены по свежим README — изменений нет (Crow 5.2, WaterFaucet 5.8, Shower 5.8, BirdFlock 5.2–5.8, TabGuard 5.8, GameplayTagFilter 5.2–5.8, JsonObjectSerializer 5.8+, HISM 5.2, GasStove 5.2, SubsystemEditor 5.0–5.8, SubsystemGameInstance — не указан).
- Сайт подстроен под два типа проектов: hero-sub (RU/EN) теперь упоминает «плюс браузерные расширения на JavaScript», чип «C++ · BP · Python» → «C++ · BP · Python · JS».
- Коммит 68f8305 запушен, Pages-билд дождан (built), живая версия проверена в браузере (DOM-проверки + скриншот списка).

### Изменённые файлы
- `index.html` — две новые карточки и два блока REPO_DATA, ключи `repo.mixer`/`repo.profiles` в обоих I18N-словарях, перенумерация карточек и REPO_DATA, счётчики 11→13, hero-sub и чип в герое (RU/EN).

### Как проверить
- Открыть https://mmitekk.github.io/MmitekkUE5/ — 13 строк: №01 BrowserTabAudioMixer «Extension · Opera GX · JS», №02 BrowserStorageProfileSwitcher «Extension · MV3 · JS», №03 CrowVFXUE5.
- Клик по каждой новой строке — модалка с 3 абзацами (RU/EN) и кнопкой-ссылкой на репозиторий.
- Герой: «13 репозиториев», чип с JS; в EN-версии подзаголовок упоминает browser extensions.

### Решения и допущения
- Порядок внутри двух новых: №01 — BrowserTabAudioMixer, №02 — BrowserStorageProfileSwitcher (в порядке перечисления пользователем; по времени создания 02 на 6 минут новее — некритично).
- «Актуализировать информацию» истолковано как сверка версий/описаний с README (выполнено) плюс честная подстройка героя сайта под появление не-UE5 проектов — иначе «Unreal Engine 5 only» в подзаголовке стало бы неточным.
- Оба расширения — не UE5; теги сделаны в той же монохромной стилистике («Extension · … · JS»), чтобы список выглядел единообразно.

### Открытые вопросы и риски
- Заголовок-кикер «Unreal Engine 5 · Open Source» и бегущая строка не менялись (минимальное вмешательство); если расширений станет больше — возможно, стоит выделить их в отдельную секцию.
- UnrealConfigGuard (публичный UE-репо) по-прежнему не на сайте — пользователь не просил.
