<!-- work-report
scope: MmitekkUE5
root: D:\GitHub\MmitekkUE5
updated: 2026-11-21T16:17:01.483Z
status: done
-->

<!-- stage-list
-->

# MmitekkUE5 portfolio site

_Обновлено: 2026-11-21 21:17 · Статус: done · Область: MmitekkUE5_

<!-- state -->
## Текущее состояние

**Где остановились:** На сайте 17 репозиториев четырёх типов: добавлены LaunchQueue (№01, App Windows C#), Adaptive-Lab (№02, Web Tool JS), PinRefBoard (№03, Web Site JS), IPWatch (№04, App Windows C#); прежние 13 перенумерованы (05–17), версии всех перепроверены по свежим README (без изменений). Задеплоено (коммит 6eb6298, Pages = built), живая версия проверена (DOM-проверки + скриншот).

**Что проверено:** Живой сайт: 17 карточек, модалки LaunchQueue и IPWatch (3 абзаца RU/EN, верные теги и ссылки), счётчики «17», чип «C++ · BP · Python · C# · JS», hero-sub (RU/EN) упоминает browser extensions + Windows utilities + web projects, Mixer теперь 05. Синтаксис JS (node --check) до пуша.

**Следующий шаг:** По запросу — новые проекты по той же схеме (4 места правок). Версии UE-плагинов не менялись с 18.10; SubsystemGameInstance по-прежнему без диапазона в README.

**Не повторять:** Пуш 403 «denied to Mmitekk» при валидном токене = fine-grained PAT с read-only Contents (API permissions.push=true обманчив, git-пуш режет). Фикс: `git-credential-manager github logout Mmitekk` + push (браузерная реавторизация) — сработал и 14.10, и 21.11. Тест сайта в ZCode IAB: только evaluate + инъекция `transition:none` + принудительный `.on`. PATH в Git Bash задавать явно (`export PATH="/mingw64/bin:/usr/bin:/c/Python312:/c/Program Files/nodejs:$PATH"`).

<!-- stages -->
## Этапы

| Этап | Статус | Итог |
|---|---|---|
| — | — | — |

<!-- howto -->
## Как продолжить

**Окружение:** Сайт = один статический `index.html` в корне D:\GitHub\MmitekkUE5 (без сборки). GitHub Pages: ветка main, корень `/`. Пуш: `git -C /d/GitHub/MmitekkUE5 push origin main` (remote закреплён за Mmitekk: `https://Mmitekk@github.com/...`).

**Команды:** Ожидание деплоя: `curl -s -H "Authorization: token $TOKEN" https://api.github.com/repos/Mmitekk/MmitekkUE5/pages/builds/latest` (TOKEN из `git credential fill`; после logout — берёт свежий OAuth). Синтаксис-чек JS: извлечь последний `<script>` блок и `node --check`.

**Точки входа:** Правки — 4 места в index.html: карточки `a.repo`, I18N словари ru/en (`repo.X`, `hero.sub`), REPO_DATA в JS (num/name/tags/абзацы ru+en), счётчики (hero-stats + section-head). Типы проектов и их теги: UE5 «Runtime/Editor/VFX · UE …», расширения «Extension · … · JS», вин-утилиты «App · Windows · C#», веб-проекты «Web Tool/Web Site · JS».

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

<!-- task:3 -->
## Задача 3 — LaunchQueue + Adaptive-Lab + PinRefBoard + IPWatch и актуализация — 2026-11-21

**Агент:** ZCode (GLM)

### Что сделано
- Данные по четырём публичным репо (описаний в API нет — факты из README): LaunchQueue (C#/WinForms/.NET 9: очередь запуска с интервалами/задержками, окна по мониторам, JSON-профили, закрытие окна по таймеру в v1.1.0), Adaptive-Lab (монохромная лаборатория адаптивности на Pages+Actions: настоящий Chromium, снимки, свои эвристики вместо алгоритма Яндекс.Вебмастера), PinRefBoard (витрина пинов досок character/reference: masonry, монохром+цвет по наведению, модалка orig с зумом, синк кнопкой/Actions 04:00 UTC), IPWatch (трей Windows: внешний IP, флаг страны VPN-узла, живые часы по IP, пинг, шлюз, провайдер; самодостаточный exe).
- Все четыре добавлены первыми (№01–04, в порядке перечисления пользователем), карточки + модалки 3 абзаца RU/EN; прежние 13 перенумерованы (05–17) в карточках и REPO_DATA; счётчики 13 → 17.
- Актуализация: версии/описания всех 13 существующих сверены по свежим README — изменений нет.
- Сайт подстроен: hero-sub (RU/EN) — «плюс браузерные расширения, утилиты для Windows и веб-проекты», чип «C++ · BP · Python · C# · JS».
- Коммит 6eb6298 запушен (после починки 403), Pages-билд дождан, живая версия проверена в браузере (DOM-проверки + скриншот).

### Изменённые файлы
- `index.html` — четыре новые карточки и четыре блока REPO_DATA, ключи `repo.launchqueue`/`repo.adaptivelab`/`repo.pinrefboard`/`repo.ipwatch` в обоих I18N-словарях, перенумерация карточек и REPO_DATA, счётчики 13→17, hero-sub и чип (RU/EN).

### Как проверить
- Открыть https://mmitekk.github.io/MmitekkUE5/ — 17 строк: №01 LaunchQueue «App · Windows · C#», №02 Adaptive-Lab «Web Tool · JS», №03 PinRefBoard «Web Site · JS», №04 IPWatch «App · Windows · C#», №05 BrowserTabAudioMixer.
- Клик по каждой новой строке — модалка с 3 абзацами (RU/EN) и кнопкой-ссылкой на репозиторий.
- Герой: «17 репозиториев», чип «C++ · BP · Python · C# · JS».

### Решения и допущения
- Порядок новых — по перечислению пользователя (по датам создания был бы IPWatch/LaunchQueue/Adaptive-Lab/PinRefBoard); в прошлые разы порядок перечисления уже устоялся как норма.
- «Актуализировать» = сверка версий по README (выполнено) + подстройка героя под новые типы проектов (четвёртое расширение портфолио за месяц: UE5 → +расширения → +вин-утилиты и веб-проекты).
- GitHub-описания у всех четырёх репо пустые — не мешает сайту (тексты берутся из REPO_DATA), но стоит заполнить поля About на GitHub.

### Открытые вопросы и риски
- 403 при пуше вернулся: у Mmitekk в GCM оказалась fine-grained PAT с read-only Contents; вылечено logout+реавторизацией. Если повторится — тот же рецепт (записан в state).
- Список из 17 строк уже длинный: типы смешаны в одном списке; если продолжит расти — стоит подумать о группировке по секциям (UE5 / расширения / утилиты / веб).
- UnrealConfigGuard (публичный UE-репо) по-прежнему не на сайте — пользователь не просил.
