# Team App — Git и два пользователя в VS Code

Пошаговое упражнение для macOS: два пользователя работают в разных окнах VS Code, создают свои ветки, передают изменения через GitHub и разрешают конфликт в одном файле. У каждого пользователя свой локальный клон и своё имя автора коммитов. На GitHub оба входят под учётной записью `Pgv0304`.

Основа: документ `/Users/gennadij/Desktop/claude/Инструкция_Git_два_пользователя.docx`.

## 1. Выбери рабочие папки

В существующем `team_app` уже есть `header.txt`, `footer.txt`, `version.txt` и коммит «Разрешён конфликт версии». Папки `/Users/gennadij/Desktop/claude/user1` и `/Users/gennadij/Desktop/claude/user2` тоже существуют.

Чтобы посмотреть результат исходного упражнения, открой каждую из этих папок в отдельном окне через **File → New Window**, затем **File → Open Folder…**. В каждом окне открой **Source Control** и историю коммитов. Повторять создание тех же веток в этих папках не нужно.

Для полного повторения ниже используются новые имена:

| Назначение | Имя или путь |
| --- | --- |
| Новый репозиторий на GitHub | `Pgv0304/team_app_vscode` |
| Папка для первого коммита | `/Users/gennadij/Desktop/claude/team_app_vscode` |
| Рабочая папка User1 | `/Users/gennadij/Desktop/claude/user1_vscode` |
| Рабочая папка User2 | `/Users/gennadij/Desktop/claude/user2_vscode` |

Если эти новые имена уже заняты, выбери другие и замени соответствующие имена во всех шагах. Далее выполняй разделы по порядку.

## 2. Подготовь VS Code

### Основные элементы интерфейса

Названия команд приведены на английском. В русской локализации можно ориентироваться на назначение команды и значки.

| Действие | Как выполнить на Mac |
| --- | --- |
| Открыть палитру команд | `Cmd + Shift + P` |
| Открыть файлы проекта | **Explorer**, значок файлов слева |
| Открыть управление Git | **Source Control**, значок ветвления слева |
| Открыть встроенный терминал | **Terminal → New Terminal** |
| Сохранить файл | `Cmd + S` |
| Открыть новое окно | **File → New Window** |
| Посмотреть эту инструкцию с форматированием | Открыть `README.md`, нажать `Cmd + Shift + V` |

Встроенного Git в VS Code достаточно для этого упражнения. Для работы с локальными клонами нужны установленный Git и авторизация при отправке на GitHub. Расширения для Pull Request можно установить отдельно. [Документация VS Code о GitHub](https://code.visualstudio.com/docs/sourcecontrol/github).

### Проверь Git

Во встроенном терминале выполни:

```bash
git --version
```

Должен появиться номер версии. Если Git не установлен, установи его по [официальной инструкции Git для macOS](https://git-scm.com/downloads/mac), затем перезапусти VS Code.

Команды в блоках ниже приведены без комментариев `#`, поэтому дополнительная настройка zsh из исходного документа здесь не требуется. Выполняй команды по очереди; если команда завершилась ошибкой, сначала разберись с ней.

### Включи запуск VS Code командой code

В палитре команд введи `shell command` и выбери команду установки `code` в `PATH`. Название может быть **Shell Command: Install 'code' command in PATH** либо **Shell Command: Install 'code' and optionally 'copilot' commands in PATH**. Если появится предложение установить Copilot CLI, для упражнения достаточно варианта **No**. После установки открой новый терминал. [Настройка команды code на macOS](https://code.visualstudio.com/docs/setup/mac).

Если не используешь `code`, открывай указанные далее папки через **File → Open Folder…** в отдельных окнах.

## 3. Создай стартовый проект и отправь его на GitHub

### Подготовь папку и Git

Во встроенном терминале:

```bash
cd /Users/gennadij/Desktop/claude
mkdir team_app_vscode
cd team_app_vscode
git init -b main
git config --local user.name "Pgv0304"
git config --local user.email "practice@example.com"
code -n /Users/gennadij/Desktop/claude/team_app_vscode
```

Почта `practice@example.com` — учебный пример. Для привязки собственных коммитов к профилю GitHub укажи почту этого профиля. Параметр `--local` задаёт автора только для текущего репозитория.

Дальше работай в открывшемся окне `team_app_vscode`. Внизу слева должна быть ветка `main`.

### Создай файлы через Explorer

Создай `README.md` с содержимым:

```markdown
# Team App

Учебный проект для работы двух пользователей с Git в VS Code.
```

Создай `index.txt`:

```text
Главная страница
```

Сохрани оба файла.

### Сделай первый коммит через Source Control

1. Открой **Source Control**.
2. Наведи указатель на `README.md` в списке **Changes** и нажми `+` — **Stage Changes**.
3. Так же добавь `index.txt`. Оба файла окажутся в **Staged Changes**.
4. В поле сообщения введи `Первый коммит`.
5. Нажми **Commit**.

Сохранение файла, коммит и отправка на сервер — отдельные действия. После **Commit** история сохранена локально. [Подготовка файлов и создание коммитов](https://code.visualstudio.com/docs/sourcecontrol/staging-commits).

### Опубликуй репозиторий из VS Code

1. В палитре команд найди **Publish to GitHub**.
2. При запросе авторизации войди в браузере под `Pgv0304` и вернись в VS Code.
3. Задай имя `team_app_vscode` и выбери приватный или публичный репозиторий.
4. После публикации открой `https://github.com/Pgv0304/team_app_vscode` и проверь наличие двух файлов.

**Publish to GitHub** создаёт репозиторий на GitHub и отправляет в него проект. Предварительно создавать пустой репозиторий на сайте для этого варианта не требуется. [Публикация из VS Code](https://code.visualstudio.com/docs/sourcecontrol/repos-remotes#publish-to-github).

Если уже создал **пустой** `team_app_vscode` на сайте GitHub, вместо **Publish to GitHub** выполни в терминале папки `team_app_vscode`:

```bash
git remote add origin https://github.com/Pgv0304/team_app_vscode.git
git push -u origin main
```

Это два альтернативных способа подключения одного проекта: выбери подходящий для своего случая.

## 4. Создай два рабочих места

В терминале выполни:

```bash
cd /Users/gennadij/Desktop/claude
git clone https://github.com/Pgv0304/team_app_vscode.git user1_vscode
git clone https://github.com/Pgv0304/team_app_vscode.git user2_vscode
code -n /Users/gennadij/Desktop/claude/user1_vscode
code -n /Users/gennadij/Desktop/claude/user2_vscode
```

Команды клонирования позволяют сразу задать разные имена папок. Клонирование также доступно через **Git: Clone** в палитре команд. [Клонирование репозитория](https://code.visualstudio.com/docs/sourcecontrol/repos-remotes#clone-repositories).

Теперь есть два отдельных окна VS Code. Смотри на имя папки в заголовке окна перед каждым действием. Папка `team_app_vscode` выполнила свою роль при создании проекта; дальше работай в `user1_vscode` и `user2_vscode`.

### Окно User1

Открой встроенный терминал окна `user1_vscode` и выполни:

```bash
cd /Users/gennadij/Desktop/claude/user1_vscode
git config --local user.name "User1"
git config --local user.email "user1@example.com"
git config --local pull.rebase false
git config --local pull.ff only
git config user.name
git config user.email
```

Ожидаемый автор: `User1`, почта: `user1@example.com`.

### Окно User2

В терминале окна `user2_vscode`:

```bash
cd /Users/gennadij/Desktop/claude/user2_vscode
git config --local user.name "User2"
git config --local user.email "user2@example.com"
git config --local pull.rebase false
git config --local pull.ff only
git config user.name
git config user.email
```

Ожидаемый автор: `User2`, почта: `user2@example.com`.

Здесь `user.name` и `user.email` задают автора коммита. Вход на GitHub остаётся под `Pgv0304`; переключать аккаунт между окнами не нужно.

Настройки `pull` делают получение изменений предсказуемым для упражнения: **Pull** обновляет ветку только при возможности fast-forward. Если история разошлась, команда остановится, а объединение нужно выполнить отдельно. [Параметр ff-only в Git](https://git-scm.com/docs/git-pull).

## 5. User1 добавляет шапку в своей ветке

**Окно:** `user1_vscode`. **Исходная ветка:** `main`.

1. Открой палитру команд и выполни **Git: Create Branch…**.
2. Введи `feature-header` и нажми Enter. VS Code создаст ветку и переключится на неё.
3. Проверь, что внизу слева написано `feature-header`.
4. Создай через Explorer файл `header.txt`:

```text
Шапка сайта
```

Сохрани файл. В **Source Control** добавь его через `+`, введи сообщение `Добавлена шапка` и нажми **Commit**.

Нажми **Publish Branch**, чтобы отправить новую ветку на GitHub. Если VS Code попросит выбрать удалённый репозиторий, выбери `origin`. В дальнейшем для этой ветки будет достаточно **Git: Push**.

Создание ветки выполняется от текущего коммита. Слияние через **Git: Merge…** добавляет выбранную ветку в ту, которая сейчас открыта. [Работа с ветками в VS Code](https://code.visualstudio.com/docs/sourcecontrol/branches-worktrees).

## 6. User2 добавляет подвал в своей ветке

**Окно:** `user2_vscode`. **Исходная ветка:** `main`.

1. Выполни **Git: Create Branch…**, имя — `feature-footer`.
2. Создай `footer.txt`:

```text
Подвал сайта
```

Сохрани файл, добавь через `+` в **Source Control**, сделай коммит `Добавлен подвал` и нажми **Publish Branch**.

Теперь на GitHub есть `feature-header` от User1 и `feature-footer` от User2. В `main` этих файлов пока нет: публикация ветки сама по себе не выполняет слияние.

## 7. User1 добавляет шапку в main

**Окно:** `user1_vscode`.

1. Нажми название ветки внизу слева и выбери локальную `main`.
2. В палитре команд выполни **Git: Pull**.
3. Выполни **Git: Merge…** и выбери `feature-header`.
4. Проверь, что `header.txt` появился в текущей `main`.
5. Выполни **Git: Push**.

Эквивалент во встроенном терминале этого окна:

```bash
git switch main
git pull --ff-only origin main
git merge --no-edit feature-header
git push origin main
```

Выбирай интерфейс **или** команды для одного и того же шага. После успешного выполнения повторять шаг вторым способом не требуется.

## 8. User2 получает шапку и добавляет подвал в main

**Окно:** `user2_vscode`.

1. Переключись на локальную `main` и выполни **Git: Pull**. В Explorer появится `header.txt`.
2. Переключись обратно на `feature-footer`.
3. Выполни **Git: Merge…**, выбери локальную `main`.
4. Если VS Code оставит слияние на этапе коммита, заверши его через **Source Control → Commit** с сообщением `Обновлена ветка подвала из main`.
5. Выполни **Git: Push**, оставаясь в `feature-footer`.
6. Переключись на `main`.
7. Выполни **Git: Merge…**, выбери `feature-footer`.
8. Выполни **Git: Push**.

Эквивалент в терминале User2:

```bash
git switch main
git pull --ff-only origin main
git switch feature-footer
git merge --no-edit main
git push origin feature-footer
git switch main
git merge --no-edit feature-footer
git push origin main
```

**Окно User1:** переключись на `main` и выполни **Git: Pull**. В обоих окнах в `main` теперь должны быть `README.md`, `index.txt`, `header.txt` и `footer.txt`.

## 9. Создай конфликт в version.txt

В этом разделе соблюдай порядок переключения окон. Оба пользователя должны изменить одну строку от общей версии `1.0`.

### 9.1. User1 создаёт общую версию

**Окно:** `user1_vscode`. **Ветка:** `main`.

Создай `version.txt`:

```text
Версия 1.0
```

Сохрани файл, добавь через `+`, сделай коммит `Добавлен файл версии`, затем выполни **Git: Push**.

### 9.2. User2 начинает свою правку от версии 1.0

**Окно:** `user2_vscode`.

1. В ветке `main` выполни **Git: Pull**.
2. Открой `version.txt` и убедись, что там `Версия 1.0`.
3. Создай ветку `new-version` через **Git: Create Branch…**.
4. Замени содержимое `version.txt`:

```text
Версия 2.0 (User2)
```

Сохрани файл, добавь через `+`, сделай коммит `Версия 2.0` и нажми **Publish Branch**. Пока оставь это окно в ветке `new-version`.

### 9.3. User1 меняет ту же строку

**Окно:** `user1_vscode`. **Исходная ветка:** `main` с версией `1.0`.

Создай ветку `fix-version`. Замени содержимое `version.txt`:

```text
Версия 1.1 (User1)
```

Сохрани файл, добавь через `+`, сделай коммит `Версия 1.1` и нажми **Publish Branch**.

Затем переключись на `main`, выполни **Git: Merge… → fix-version** и **Git: Push**.

Теперь на GitHub в `main` находится `Версия 1.1 (User1)`, а в ветке `new-version` у User2 — `Версия 2.0 (User2)`.

### 9.4. User2 получает изменения и запускает слияние

**Окно:** `user2_vscode`. **Ветка:** `new-version`.

В палитре команд выполни **Git: Fetch**, затем **Git: Merge…** и выбери `origin/main`.

Эквивалент в терминале User2:

```bash
git fetch origin
git merge origin/main
```

Ожидаемый результат — конфликт в `version.txt`. **Fetch** обновил сведения о GitHub, а **Merge** попытался объединить две правки.

### 9.5. Разреши конфликт в редакторе VS Code

В **Source Control → Merge Changes** открой `version.txt`. При просмотре обычного файла конфликт выглядит так:

  ```text
  <<<<<<< HEAD
  Версия 2.0 (User2)
  =======
  Версия 1.1 (User1)
  >>>>>>> origin/main
  ```

Для этого слияния **Current** — `new-version` User2, **Incoming** — полученная `origin/main` с правкой User1.

| Действие в редакторе | Что останется |
| --- | --- |
| **Accept Current Change** | `Версия 2.0 (User2)` |
| **Accept Incoming Change** | `Версия 1.1 (User1)` |
| **Accept Both Changes** | Обе строки; итоговый формат нужно проверить |

Для упражнения оставь одну согласованную строку:

```text
Версия 2.0 (согласовано User1 и User2)
```

Можно вручную заменить конфликтный фрагмент и удалить все маркеры. Либо выбери **Open in Merge Editor**, отредактируй панель **Result** и нажми **Complete Merge**. Эта кнопка подготавливает файл к коммиту; затем нужно завершить слияние.

Сохрани результат, добавь файл через `+`, если он ещё не в **Staged Changes**, и нажми **Commit** с сообщением `Разрешён конфликт версии`. [Разрешение конфликтов в VS Code](https://code.visualstudio.com/docs/sourcecontrol/merge-conflicts).

### 9.6. Отправь согласованный результат в main

**Окно:** `user2_vscode`.

1. После коммита разрешения конфликта выполни **Git: Push** в ветке `new-version`.
2. Переключись на `main` и выполни **Git: Pull**.
3. Выполни **Git: Merge… → new-version**.
4. Выполни **Git: Push**.

Эквивалент после коммита разрешения конфликта:

```bash
git push origin new-version
git switch main
git pull --ff-only origin main
git merge --no-edit new-version
git push origin main
```

**Окно User1:** переключись на `main` и выполни **Git: Pull**. Теперь согласованная строка должна быть в обоих клонах и на GitHub.

## 10. Проверь результат

В каждом окне открой терминал и выполни:

```bash
git branch --show-current
git status
git log --graph --all --format="%h %an: %s"
git branch -a
```

Ожидаемый результат:

- Текущая ветка — `main`, незакоммиченных изменений нет.
- Есть пять файлов: `README.md`, `index.txt`, `header.txt`, `footer.txt`, `version.txt`.
- В `version.txt` одна строка: `Версия 2.0 (согласовано User1 и User2)`.
- В истории есть авторы `User1` и `User2`, а также коммит `Разрешён конфликт версии`.
- На GitHub в ветке `main` видно то же содержимое файлов.

Историю можно также посмотреть в **Source Control Graph**. Если вывод `git log` занял терминал и появился просмотрщик, нажми `q`, чтобы выйти.

## 11. Шпаргалка для следующих задач

### Полный цикл работы

1. Открой папку своего пользователя и проверь текущую ветку.
2. Переключись на `main` и получи обновления через **Git: Pull**.
3. Создай отдельную ветку для задачи.
4. Измени и сохрани файлы.
5. Проверь изменения в **Source Control**, добавь нужные файлы через `+`.
6. Сделай **Commit** с понятным сообщением.
7. Для новой ветки нажми **Publish Branch**, для уже опубликованной — **Git: Push**.
8. Перед объединением обнови `main`, влей её в рабочую ветку и разреши возможные конфликты.
9. Отправь рабочую ветку, затем объедини её с `main` и отправь `main`.
10. Во втором клоне получи обновлённую `main`.

### Что делают команды обмена

| Команда VS Code | Действие |
| --- | --- |
| **Git: Fetch** | Обновляет сведения об удалённых ветках; рабочие файлы остаются прежними |
| **Git: Pull** | Получает и интегрирует изменения в текущую ветку |
| **Git: Push** | Отправляет локальные коммиты текущей ветки |
| **Publish Branch** | Публикует новую ветку и настраивает её upstream |
| **Sync Changes** | Сначала выполняет Pull, затем Push |

В упражнении команды получения и отправки указаны отдельно, чтобы был виден каждый этап обмена. [Fetch, Pull, Push и Sync](https://code.visualstudio.com/docs/sourcecontrol/repos-remotes#push-pull-and-sync).

### Если что-то не получается

| Ситуация | Что проверить |
| --- | --- |
| Файл не попал в коммит | Сохрани его и добавь через `+` в **Staged Changes** |
| Коммит есть, а на GitHub изменения не видны | Выполни **Git: Push** и проверь выбранную ветку на GitHub |
| Изменения User1 не появились у User2 | В окне User2 переключись на `main` и выполни **Git: Pull** |
| Неясно, в какой папке терминал | Выполни `pwd` и `git branch --show-current` |
| Git просит имя или почту | Повтори локальную настройку автора в соответствующем клоне |
| Git сообщает о незавершённом слиянии | Проверь `git status`, разреши все конфликты, добавь файлы и заверши коммит |
| Pull остановился из-за расхождения истории | Выполни Fetch, проверь историю и явно объедини нужные ветки; в этом сценарии после шагов по порядку main обновляется fast-forward |
| Push отклонён из-за новых коммитов на сервере | Получи изменения, объедини их со своей работой и повтори Push |
| Имя ветки или папки уже существует | Проверь, не выполнен ли этот шаг раньше; для нового повторения выбери новое имя |

Если Git в терминале открывает непривычный редактор для сообщений коммитов, после настройки команды `code` можно назначить VS Code редактором **в каждом нужном клоне**:

```bash
git config --local core.editor "code --wait"
```

В дальнейшем введи сообщение в открывшейся вкладке, сохрани его и закрой вкладку, чтобы Git продолжил операцию. Команды `git merge --no-edit` в этой инструкции принимают стандартное сообщение слияния автоматически.

## 12. Удали завершённые рабочие ветки при необходимости

После проверки результата можно оставить только `main`. Все четыре рабочие ветки в этом варианте упражнения были опубликованы и объединены с `main`.

В терминале **User1**:

```bash
git switch main
git pull --ff-only origin main
git branch -d feature-header fix-version
git push origin --delete feature-header feature-footer fix-version new-version
git fetch --prune origin
```

В терминале **User2**:

```bash
git switch main
git pull --ff-only origin main
git branch -d feature-footer new-version
git fetch --prune origin
```

Удаление объединённых веток сохраняет их коммиты в истории `main`. Папки проектов и репозиторий на GitHub можно сохранить для следующих упражнений.
