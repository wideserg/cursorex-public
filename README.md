# Cursorex — public releases

Сюда выкладывается **только локальный bridge** (native host + bridge), чтобы пользователи расширения из Chrome Web Store могли поставить совместимую версию без доступа к приватному исходнику.

## Расширение (Chrome Web Store)

Установите **Cursorex** из магазина:

https://chromewebstore.google.com/detail/infbgmlkjfimojcjikknabbaifbafjoo?utm_source=github&utm_medium=wideserg-public&utm_campaign=cursorex_readme

## Что скачать здесь

Во вкладке **Releases** возьмите архив **`cursorex-bridge-*.zip`** (готовый бандл bridge, не исходники этого репозитория).

## Требования

- **Node.js** LTS (20+), команда `node` доступна в терминале  
- **Google Chrome** (stable)  
- **Cursor CLI** на машине (как в основной инструкции Cursorex), если будете работать через локальный app-server  

## Установка bridge (после распаковки zip)

Запускайте **один** скрипт под свою ОС (все лежат **в корне** распакованной папки):

| ОС | Установка | Удаление |
|----|-----------|----------|
| Windows | Дважды **`install_windows.bat`** | **`uninstall_windows.bat`** |
| macOS | Дважды **`install_macos.command`** | **`uninstall_macos.command`** |
| Linux | В терминале: **`chmod +x install_linux.sh`** (если нужно), затем **`./install_linux.sh`** | **`./uninstall_linux.sh`** |

Дальше в Chrome: **Перезагрузить** расширение → в боковой панели **Check connection**.

Нужен другой канал Chrome (Beta и т.д.) — см. флаги в `install-native-host.mjs` в полном репозитории или передайте аргументы тем же способом, что и для `node install-native-host.mjs`.

## Что это за репозиторий

- Артефакты bridge собираются из приватного репо и публикуются сюда автоматически.  
- Исходный код и CI здесь не ведутся — только релизы и эта памятка.
