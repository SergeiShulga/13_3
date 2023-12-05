### 13_3 «Защита сети» - "Сергей Шульга"

Подготовка к выполнению заданий

Подготовка защищаемой системы:

установите Suricata,

установите Fail2Ban.

Подготовка системы злоумышленника: установите nmap и thc-hydra либо скачайте и установите Kali linux.

Обе системы должны находится в одной подсети.

### Задание 1
Проведите разведку системы и определите, какие сетевые службы запущены на защищаемой системе:

sudo nmap -sA 10.10.10.1 

nmap  с ключом -sA используется для сканирования и определения настроек брандмауэра.

С запущенным Syricate все 1000 отсканированных портов на 10.10.10.1 находятся в игнорируемых состояниях и их состояние не показывается.

![alt text](https://github.com/SergeiShulga/13_3/blob/main/img/001.png)



sudo nmap -sT < ip-адрес > 

Сканирование подключения TCP [-sT]
Это основная форма сканирования TCP, которая считается самой открытой. Инструмент пытается установить полное соединение с портами диапазона, указанными с помощью трехстороннего обмена рукопожатиями (SYN – > SYN/ACK – > ACK). Успешное соединение указывает на открытый порт. Это тип сканирования по умолчанию используется Nmap при выполнении действий непривилегированным пользователем.

sudo nmap -sS < ip-адрес > - ключ для определения открытых портов

Сканирование TCP SYN [-sS]
Его еще называются полуоткрытое сканирование, оно является более скрытным, чем сканирование TCP, поскольку инструмент никогда не устанавливает полное соединение. Сканирование TCP SYN — это тип сканирования по умолчанию, выполняемый от имени привилегированного пользователя. Непривилегированные пользователи не будут иметь разрешения на запуск этого сканирования, поскольку оно требует определенных привилегий для запуска необработанного сокета или необработанного пакета.

sudo nmap -sV < ip-адрес > - ключ для определения версий сервисов

Сканирование версии
Nmap также помогает сканировать запущенные службы и получить информацию об их версиях из открытых портов. Это полезно при сканировании служб, работающих на уязвимых версиях, и может быть использовано для снижения риска. Этот параметр может быть включен с помощью флага «sV».

По желанию можете поэкспериментировать с опциями: https://nmap.org/man/ru/man-briefoptions.html.

В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.

![alt text](https://github.com/SergeiShulga/13_3/blob/main/img/2023-12-03_08-48-03.png)

![ait text](https://github.com/SergeiShulga/13_3/blob/main/img/2023-12-03_09-35-47.png)

### Задание 2
Проведите атаку на подбор пароля для службы SSH:

hydra -L users.txt -P pass.txt < ip-адрес > ssh

Настройка hydra:

создайте два файла: users.txt и pass.txt;

в каждой строчке первого файла должны быть имена пользователей, второго — пароли. В нашем случае это могут быть случайные строки, но ради эксперимента можете добавить имя и пароль существующего пользователя.

Дополнительная информация по hydra: https://kali.tools/?p=1847.

Включение защиты SSH для Fail2Ban:

открыть файл /etc/fail2ban/jail.conf,

найти секцию ssh,

установить enabled в true.

Дополнительная информация по Fail2Ban:https://putty.org.ru/articles/fail2ban-ssh.html.

В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.

![alt text](https://github.com/SergeiShulga/13_3/blob/main/img/2023-12-04_14-36-23.png)
