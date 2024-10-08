Architecture Linux

	1.1. Обзор внутреннего устройства

	В Linux выделяют два главных режима работы — ядерный режим (kernel mode) и внеядерный режим (user mode). Основное различие
	этих двух режимов состоит в привилегиях доступа к аппаратным средствам — памяти и устройствам ввода-вывода, к которым разрешен полный доступ из режима ядра и ограниченный доступ из режима пользователя.

	Ядро - это совокупность работающих в ядерном режиме программ называют ядром, которое в Linux состоит из основы (или же остова) и присоединяемых к ней объектов — динамически загружаемых модулей (подробнее см. разд. 4.1.1).


1.2. Внеядерные компоненты: программы и библиотеки

	Ядерные компоненты в основном обеспечивают решение задачи распределения ресурсов между потребителями и предоставляют им базовый интерфейс доступа к ресурсам. Обеспечения УДОБСТВА доступа реализуется компонентами внеядерного режима — библиотеками динамической и статической компоновки (подробнее см. разд. 4.1).

	Функции, реализуемые ядром, доступны для user mode посредством системных вызовов — специальных обращений для получения услуг ядра. Системные вызовы выполняются в ядре, а вызываются при помощи — библиотеки libc.so в пространстве пользователя.

	Функции, реализуемые в user mode, доступны посредством библиотечных вызовов и вызываются (выполняются) в самих библиотеках (например, алгоритмы сжатия информации в библиотеках libz.so и Hbbz2.so).


1.3. Ядерные компоненты: подсистемы управления процессами, памятью, вводом-выводом, файлами

	Одна из основных задач ядра — распределение ресурсов и это приводит к тому, что в ядре выделяются соответствующие (аппаратным ресурсам) менеджеры, так называемые подсистемы Управления Процессами, Памятью, Вводом-Выводом и Файловую Подсистему.
	
	ПОДСИСТЕМА УПРАВЛЕНИЯ ПРОЦЕССАМИ - распределяет время центральных процессоров (ЦП) между выполняющимися задачами, реализует многозадачность. Она создает и уничтожает такие сущности, как процессы и нити (см. разд. 4.2), и организует одновременное их выполнение при помощи планировщиков (scheduler).
	
	ПОДСИСТЕМА ВВОДА-ВЫВОДА - распределяет доступ к устройствам ввода-вывода (УВВ) между процессами и предоставляет им унифицированные интерфейсы блочного, символьного (см. разд. 3.2.5) и пакетного (сетевого) устройств (см. разд. 6.1). Для устройств внешней памяти (дисковых или твердотельных накопителей, более медленных по сравнению с оперативной памятью) подсистема ввода-вывода организует Кэширование при помощи подсистемы управления памятью.
	
	ПОДСИСТЕМА УПРАВЛЕНИЯ ПАМЯТЬЮ - распределяет пространство оперативного запоминающего устройства (ОЗУ) между процессами.
	
	ФАЙЛОВАЯ ПОДСИСТЕМА ЯДРА - предоставляет процессам интерфейс файлового доступа к внешней памяти (дискам) и распределяет между ними пространство ВЗУ при помощи файлов и файловых систем. Особенное назначение файловой подсистемы состоит еще и в том, что при помощи ее файлового интерфейса процессам предоставляется доступ и к другим подсистемам. Например:
		1. К CD/DVD-накопителю — через файл /dev/sr0
		2. К манипулятору мыши — через /dev/input/mouse0
		3. К физической памяти и памяти ядра — через /dev/mem и /dev/kmem
		4. Доступ процессов к страницам памяти друг друга — через файлы /ргос/PID/mem
		
	 Даже доступ к внутренним параметрам и статистике различных компонент ядра операционной системы возможен через файлы разнообразных псевдофайловых систем, например procfs, securityfs, debugfs и прочих, а к списку обнаруженных ядром устройств ввода-вывода — через файлы псевдофайловой системы sysfs.
	 
1.4. Трассировка системных и библиотечных вызовов

	Для наблюдения за обращениями программ к услугам ядра, т. е. за системными вызовами, служит утилита strace(1), предназначенная для трассировки — построения трасс выполнения той или иной программы.
	
	strace -fe uname,getcwd,geteuid,sethostname hostname











