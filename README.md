# Исследование ОС семейства Linux


## **CatScale**

Cat-Scale расшифровывается как "Compromise Assessments at Scale" и был разработан во время нескольких мероприятий по реагированию на инциденты и компрометации для сбора судебно-медицинских артефактов из различных сред Linux.

На протяжении многих лет мы активно используем этот сценарий, чтобы помочь клиентам расследовать, сдерживать и устранять инциденты всех размеров. Естественно, Cat-Scale также должен был развиваться, чтобы соответствовать ландшафту угроз и вмещать постоянно меняющиеся сети.[2]

Скрипт Cat-Scale для Linux от F-Secure является скриптом на языке bash, который использует собственные бинарники для сбора данных с хостов на базе Linux. Хотя некоторые данные захватываются из выводов консоли инструментов, остальные архивируются в своем первоначальном виде. Данные собираются в порядке устойчивости, чтобы обеспечить захват устойчивых данных в их чистом виде. После сбора данных аналитики могут просматривать вывод в виде текстовых файлов или использовать развертывание ELK для внедрения данных с использованием предоставленной конфигурации Logstash. Это позволяет аналитикам искать индикаторы компрометации на нескольких хостах, которые не подвергаются контролю EDR, или следить за подозрительной активностью, обнаруженной другим способом.

Следует отметить, что хотя Cat-Scale может предоставить обширный список артефактов, основная цель инструмента - предоставить профессионалам в области DFIR результаты триажа масштабно, чтобы определить степень нарушения и определить, был ли компрометирован определенный хост.

Результат работы Cat-Scale может вполне ответить на большинство ваших вопросов о компрометации. Инструмент не является заменой судебных приобретений, а скорее инструментом поддержки триажа. Следует отметить, что инструмент предоставляет свои собственные артефакты. Это следует учитывать перед выполнением. Инструмент не является заменой судебных приобретений, а скорее инструментом для поддержки начального триажа и помощи в более целенаправленных судебных приобретениях. Следует отметить, что активации триажа в режиме реального времени оставят свой след. Это следует учитывать перед выполнением.

На момент написания вывода данные, собранные Cat-Scale, сохраняются в архив tar.gz. В среднем мы обнаружили, что результирующий архив будет составлять от 200 до 300 Мб, что позволяет быстро загружать и загружать в масштабе.



https://github.com/WithSecureLabs/LinuxCatScale
[2] https://labs.withsecure.com/tools/cat-scale-linux-incident-response-collection



## **FastIR Collector Linux**
Этот инструмент собирает различные артефакты в Linux и записывает результаты в файлы csv. При анализе этих артефактов можно обнаружить. Весь код должен быть в файле python 2, а поддержка начинается с 2.4. Эта программа должна быть запускана как root. Эта консольная утилита для быстрого сбора данных о системе (файловая система, запущенные службы, реестр, процессы, настройка окружения, автозагрузка и т.д).
Артефакты

- Информация о системе[3]
- Версия ядра
- Модули ядра
- Сетевые интерфейсы
- Hostname (имя узла)
- Версии дистрибутивов
- Последние входы
- Соединения
- Данные пользователя
- Скрытые файлы в профилях пользователей
- Файлы .known_hosts в SSH
- Содержимое /tmp
- Автозапуски
- /etc/*.d
- /etc/crontab
- /etc/cron.*/
- Информация о дисках
- Список разделов
- MBR (загрузочный рекордер мастер-загрузочного сектора)
- Информация о файловой системе

[3] https://github.com/SekoiaLab/Fastir_Collector_Linux
https://github.com/SekoiaLab/Fastir_Collector
https://github.com/SekoiaLab/Fastir_Collector/blob/master/documentation/FastIR-Collector_v1.0_20160106_EN.pdf

## **unix_collector**
Скрипт оболочки для базового сбора данных различных артефактов с UNIX-систем. unix_collector - это скрипт, который запускается на различных Unix-системах и пытается собрать артефакты, которые могут быть проанализированы для выявления потенциальной угрозы системы. unix_collector написан как единый скрипт оболочки, поэтому его легко загрузить и запустить (в отличие от разархивирования, компиляции и установки). Он может работать как обычный пользователь, так и как root. Работает он лучше под root, потому что, конечно же, может прочитать больше файлов.
Действия скрипта[4]

- Перечислить основную информацию хоста, такую как версию ядра, процессы, имя хоста и сохранить детали в каталоге вывода.
- Перечислить файлы, записанные на диск, и создать базовую временную линию, используя команду 'stat'.
- Перечислить сетевую информацию и сохранить детали в каталоге вывода.
- Перечислить информацию о патче и установленном программном обеспечении и сохранить детали в каталоге вывода.
- Перечислить список процессов и другую информацию о процессе и сохранить детали в каталоге вывода.
- Перечислить списки приложений, plist/apk для iOS/Android и сохранить их в каталоге вывода.
- Хэшировать файлы в различных папках, таких как /home/ /opt/ /usr/ и сохранить детали в каталоге вывода.
- Хэшировать файлы, помеченные как SGID или SUID, и сохранить детали в каталоге вывода.
- Скопировать различные файлы, такие как задания cron, plist или другие файлы, в каталог вывода.
- Скопировать двоичные файлы SUID/SGID в каталог вывода.
- Скопировать домашние каталоги в каталог вывода.
- Скопировать определенные файлы /proc/ в каталог вывода.
- Скопировать системные журналы (т. е. /var/log или /var/adm/) в каталог вывода.
- Создать TAR-архив всего каталога вывода и использовать имя хоста в качестве имени файла с текущей датой.
- При копировании или хэшировании файлов размером более 500 МБ они будут пропущены. Это поведение по умолчанию может быть изменено внутри скрипта, изменив глобальные переменные RSYNC_MAX_FILESIZE, TAR_MAX_FILESIZE и HASH_MAX_FILESIZE.

Требования

- Достаточно места на диске, чтобы журналы и другие файлы могли быть скопированы в одно место (или запуститься с примонтированного диска или сетевого раздела).
- sh (оболочка Unix-систем)

[4] https://github.com/op7ic/unix_collector?tab=readme-ov-file#unix_collector


## **TuxResponse**
TuxResponse - это скрипт реагирования на инциденты для систем Linux, написанный на bash. Он может автоматизировать действия по реагированию на инциденты в системах Linux и позволяет быстро проводить триаж систем, не нарушая результатов. Обычно на корпоративных системах должны быть какая-то форма мониторинга и контроля, но есть исключения из-за теневой IT и неподходящих образов, развернутых в корпорациях. То, что обычно требует ввода 10 команд с пробными тестами, может быть сделано нажатием одной кнопки.[5]

Проверено на:
- Ubuntu 14+
- CentOS 7+

Основная цель:
- Использовать встроенные инструменты и функциональность в Linux (инструменты вроде dd, awk, grep, cat, netstat и т. д.).
- Сократить количество команд, которые инцидент-респондер должен помнить/использовать в сценарии реагирования.
- Автоматизация

Внешние инструменты в пакете:
- LiME
- Exif
- Chckrootkit
- Yara + правила сканирования для Linux (требуется сеть для загрузки репозитория)

[5] https://github.com/la3ar0v/TuxResponse 


## **auditd**
 нативный инструмент предназначенный для мониторинга событий операционной системы и записи их в журналы событий, разрабатываемый и поддерживаемый компанией RedHat. Был создан для тесного взаимодействия с ядром операционной системы — во время своей работы наблюдает за системными вызовами и может записывать события — чтение, запись, выполнение, изменение прав - связанные с файлами ОС. Таким образом, с его помощью можно отслеживать практически любые события, происходящие в операционной системе.[6][7]

 Плюсы auditd:
- работает на низком уровне мониторинга — отслеживает системные вызовы и действия с файлами;
- имеет неплохой набор утилит в комплекте для удобства работы;
- постоянно развивается и обновляется;
- бесплатен и легко устанавливается.

Минусы auditd:
- большинство событий, возникающих при атаках характерных для конкретного приложения, практически невозможно отслеживать поскольку на уровне системных вызовов и работе с файлами трудно отличить взлом от нормальной работы приложения. Такие события лучше отслеживать на уровне самих приложений;
- auditd может замедлять работу ОС. Это связанно с тем, что подсистеме аудита необходимо проводить анализ системных вызовов;
- не слишком гибок в настройке правил;
- на данный момент это не лучший инструмент для работы с контейнерами.

| Имя скрипта | Docker | Logs | Music | Persistence(Службы и драйвер)	| Podman	| Process_and_Network	| System_Info	| User_Files	| Virsh(управление ВМ)	| Install Software |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| CatScale  | + | + | + | + | + | + | + | + | - | - |
| FastIR Collector Linux (python 2) | - | +(last_output) | - | +(drivers) | - | +(netstat) | + | +(fs) | - | - |
| unix_collector | - | + | - | + | - | + | + | + | - | - |
| TuxResponse  | + | +(/var/log) | - | - | - | + | + | + | - | + |



[7] https://github.com/Neo23x0/auditd
[5] https://habr.com/ru/articles/553036/
https://linux-audit.com/tuning-auditd-high-performance-linux-auditing/

*Для того чтобы включить набор клавиатуры в Docker контейнере, используется механизм проброса клавиатуры из хост-системы в контейнер.
docker run -it my_auto_image *












