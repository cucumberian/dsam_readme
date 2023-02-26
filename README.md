# ARM book bot 

## Подключение к серверу
### Софт
Для подключения понадоится любой эмулятор терминала с рабочей командой `ssh`.
- `Командная строка` из набора служебных прграмм Windows 10. Находится `Пуск` -> `Служебные Windows` -> `Командная строка`.
- `Windows Power Shell`. Более новый аналог *Командной стоки* из стандартного набора Windows: `Пуск` -> `Windows Power Shell` -> `Windows Power Shell`
- `Windows Terminal`. Красивая и удобная консоль от Microsoft. Берется из стандартного магазина приложений **Microsoft Store** через поиск или по ссылке [ссылка на Windows Terminal](https://www.microsoft.com/store/productId/9N0DX20HK701)
- `MobaXTerm` - стороняя многофункциональная программка. Скачать можно по адресу [mobaxterm.mobatek.net](https://mobaxterm.mobatek.net/)

### Подключение
Для подключения к серверу через протокол `ssh` потребуется ввести одну команду в консоли:
```bash
ssh имя_пользователя@адрес_сервера
```
например, чтобы подключитсья к серверу по ip адресу `31.341.24.203` как пользователь с именем `alex`надо ввести команду:
```bash
ssh alex@31.341.24.203
```
Далее надо будет ввести пароль. Вводимые символы не отображаются.

### Отключение
При закрытии терминала вы автоматически отключаетесь от сессии.
Все программы что были запущены и не умеет работать при неактивном сеансе закрываются.
Альтернативно закрытию окна можно использовать команду `exit` в терминале.


## Бот

### Управление ботом
Скорее всего наиболее полезными будут всего несколько команд:

**Запуск бота:**
```bash
systemctl start dsam-telbot.service
```
**Остановка бота:**
```bash
systemctl stop dsam-telbot.service
```

**Перезапуск бота:**
```bash
systemctl restart dsam-telbot.service
```

**Посмотр логов бота:**
```bash
journalctl -xefu dsam-telbot.service
```
Чтобы выйти из режима просмотра логов бота нажмите комбинацию клавиш `Ctrl+C`

### Путь до бота
Бот хранится в катклоге `/root/script/google-sheet-telegram-bot`

### Логи бота
Логи хранятся в каталоге `/root/script/google-sheet-telegram-bot/logs`


## tmux
TMUX - оболочка, которая продолжит работу, даже когда вы отключитесь от сервера.

### Запуск tmux

#### Запуск новой сессии tmux
```bash
tmux
```

#### Просмотр всех текущих открытых сессий

```bash
tmux ls
0: 2 windows (created Sun Dec 25 15:18:41 2022) [152x41]
1: 1 windows (created Sun Feb 26 03:05:19 2023) [152x41]
```

Увидим, что запущено две сессии tmux с именем `0` (2 окна) и `1` (1 окно).

#### Подключение к сессиям
**К последней открытой сессии:**
```bash
tmux a
```

**Подключеник к сессии с именем `0`:**
```bash
tmux a -t 0
```
**Подключение к сессии с именем `1`:**
```bash
tmux a -t 1
```

По большому после подключения можно и не использовать tmux. Tmux удобен если вы что-то запускаете в консоли и хотите, чтобы это работало, когда вы отключитесь от сервера. Использование tmux - это самый простой способ так сделать.

### Горячие клавиши
Tmux имеет множество горячих клавиш, которые позволяют управлять терминальными сессиями и окнами. Нажимаете сначала комбинацию `CTRL+b`, отпускаете клавиши и дальше нужную кнопку.

Комбинация | Действие
--|--
`Ctrl+b c` | создает новую вкладку.
`Ctrl+b n` | переключается на следующее окно в текущей сессии.
`Ctrl+b p` | переключается на предыдущее окно в текущей сессии.
`Ctrl+b d` | **Отключиться от tmux, не закрывая сессию**.
`Ctrl+b x` | закрывает текущую панель.
`Ctrl+b %` | разделяет текущее окно на две части по вертикали.
`Ctrl+b "` | разделяет текущее окно на две части по горизонтали.
`Ctrl+b стрелка вверх` | перейти на верхнюю панель
`Ctrl+b стрелка вниз` | перейти на нижнюю панель
`Ctrl+b стрелка влево` | перейти на левую панель
`Ctrl+b стрелка впаво` | перейти на правую панель
`Ctrl+b ?` | выводит список всех доступных горячих клавиш.

## Systemd
Systemd - это системный менеджер инициализации для Linux, который выполняет роль аналога служб в Windows. Он управляет процессами и запускает демоны (службы), которые запускаются при загрузке системы и работают в фоновом режиме. Также systemd позволяет контролировать процессы, перезапускать службы в случае ошибок, регистрировать события и многое другое.

Телеграм бот DSAM работает в качестве демана с именем `dsam-telbot.service`

### Команды systemd

Команда | Описание
--|--
`systemctl start <service>` | запускает службу
`systemctl stop <service>` | останавливает службу
`systemctl restart <service>` | перезапускает службу
`systemctl reload <service>` | перезагружает конфигурацию службы без остановки и запуска службы
`systemctl enable <service>` | добавляет службу в автозапуск при старте системы
`systemctl disable <service>` | удаляет службу из автозапуска при старте системы
`systemctl status <service>` | выводит текущее состояние службы
`systemctl is-active <service>` | проверяет, активна ли служба в данный момент
`systemctl is-enabled <service>` | проверяет, включена ли служба в автозапуск при старте системы
`journalctl -u <service>` | выводит журнал событий для службы
`journalctl -xefu <service>` | постоянно выводит журнал событий для службы
`systemctl list-units` | выводит список всех запущенных служб и их состояние
`systemctl daemon-reload` | перезагружает systemd после изменения конфигурации служб
`systemctl --failed` | показывает список служб, которые завершились с ошибкой


## Midnight Commander
Для привычной навигации можно использовать панельный менеджер **Midnight Commander**. 
Midnight Commander запускается командой
```bash
mc
```
**Выход** из Midnight Commander - клавиша F10
**Просмотр** файла под курсором - клавиша F3
Список действий через функциональные клавиши (F1 - F12) - внизу экрана.
