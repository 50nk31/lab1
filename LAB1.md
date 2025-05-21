# Лабораторная работа №1 в RedOS: Работа с командной строкой и файлами #
## 1. Навигация и поиск по файловой системе ##

**Выполненные действия:**
- Создана рабочая папка 'lab1_test' в домашнем каталоге
- Созданы тестовые файлы с разными расширениями
- Использованы команды 'find' и 'grep' для поиска файлов и содержимого

**Команды и вывод:**
```bash
[50nk31@localhost ~]$ mkdir lab1_test
[50nk31@localhost ~]$ cd lab1_test
[50nk31@localhost lab1_test]$ echo "Hello World, Test! > exmp.txt
[50nk31@localhost lab1_test]$ echo "System logs" > system.log
[50nk31@localhost lab1_test]$ echo "TOP SECRET" > secret.file
[50nk31@localhost lab1_test]$ find .-name "*.log"
./system.log
[50nk31@localhost lab1_test]$ grep "Test *
exmp.txt:Hello World, Test!
[50nk31@localhost lab1_test]$ mkdir src
[50nk31@localhost lab1_test]$ echo "Main file" > src/original.txt
[50nk31@localhost lab1_test]$ ln src/original.txt hard_link
[50nk31@localhost lab1_test]$ ln -s src/original.txt sym_link
[50nk31@localhost lab1_test]$ ls -li

[50nk31@localhost lab1_test]$ sudo touch /etc/protected.conf
[50nk31@localhost lab1_test]$ sudo chmod 600 /etc/protected.conf
[50nk31@localhost lab1_test]$ sudo chattr +i /etc/protected.conf
[50nk31@localhost lab1_test]$ sudo echo "test" | sudo tee /etc/protected.conf
```
## Результат команды ``` grep "Test" ```
![Картинка "grep "Test"](https://i.imgur.com/AYQgx3B.jpeg)
## Результат команды ``` ls -li ```
![Картинка результата команды ls -li](https://i.imgur.com/L7z2W01.jpeg)
## Результат команды ``` find . -name "*.log" ```
![Картинка результата команды find](https://i.imgur.com/8Ix9gDf.jpeg)

## Код файла скрипта ##
- Скрипт писался через ``` nano ```
- В скрипте присутствуют только дата, пользователь, имя хоста и нагрузка на ЦП
- Лог файл сохраняется
- Запуск скрипта по расписанию работает
- Старые лог файлы удаляются
```bash
#!/bin/bash

LOG_DIR="var/log/sysinfo"
mkdir -p "$LOG_DIR"

LOG_FILE="$LOG_DIR/sysinfo-$(date +%Y%m%d).log"

{
echo "===Sytem report ==="
echo "Date: $(date)"
echo "User: $(whoami)"
echo "Host name: $(hostname)"
echo "CPU Uptime: $(uptime)"

} > "$LOG_FILE"

find "$LOG_DIR" -name "sysinfo-*.log" -type f mtime + -delete

echo "Log saved in $LOG_FILE"
```
## Скриншот лог-файла из скрипта 
![Лог-файл скрипта](https://i.imgur.com/LBtfwms.jpeg)

