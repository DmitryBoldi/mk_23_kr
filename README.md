# mk_23_kr
# Курсовые работы по дисциплине "Микроконтроллеры мехатронных устройств"


## Автор курсовой работы , студент группы №133 Болдин Дмитрий Вадимович

## Подсистема позиционирования на основе GPS/ГЛОНАС приёмника для робота-ассистента

### Теория используемых интерфейсов
    (1) SPI. Serial Peripheral Interface — последовательный периферийный интерфейс, шина SPI — последовательный синхронный стандарт передачи данных в режиме полного дуплекса, предназначенный для обеспечения простого и недорогого высокоскоростного сопряжения микроконтроллеров и периферии.Использует 4 отсновныхз сигнала:

       MOSI — выход ведущего, вход ведомого (англ. Master Out Slave In). Служит для передачи данных от ведущего устройства ведомому.

       MISO — вход ведущего, выход ведомого (англ. Master In Slave Out). Служит для передачи данных от ведомого устройства ведущему.

       SCLK или SCK — последовательный тактовый сигнал (англ. Serial Clock). Служит для передачи тактового сигнала для ведомых устройств.

       CS или SS — выбор микросхемы, выбор ведомого (англ. Chip Select, Slave Select).

    (2) UART. UART (Universal asynchronous receiver/transmitter) или УАПП (универсальный асинхронный приемопередатчик). Преимуществом UART является его асинхронность — передатчик и приемник не используют общий тактовый сигнал. Хотя это значительно упрощает протокол, данное свойство предъявляет определенные требования к передатчику и приемнику. Поскольку у них нет общего тактового сигнала, оба конца должны передавать с одинаковой заранее заданной скоростью, чтобы иметь одинаковую синхронизацию битов. Наиболее распространенные скорости передачи данных UART, используемые сегодня: 4800, 9600, 19,2 кбит/с, 57,6 кбит/с и 115,2 кбит/с. 

    (3)Интерфейс связи SWD. терфейс для отладки и прошивки МК — Serial Wire Debug, сокращено SWD. Его удобство заключается в том, что для отладки надо подключить всего два информационных вывода и два вывода питания. Один провод SWCLK отвечает за тактовый сигнал, второй SWDIO – за передачу информации. Со стороны мастера процесс проходит в три этапа: передача байта управления → переключение линии SWDIO на прием и чтение подтверждения → переключение лини SWDIO на передачу и запись данных.
    

    (4)USB. Последовательный интерфейс для подключения периферийных устройств к вычислительной технике.Интерфейс позволяет не только обмениваться данными, но и обеспечивать электропитание периферийного устройства.


### Применение интерфейсов в проекте

 1) SPI.При помощи данного интерфейса происходит связь между компанентами робоат. На плате размещены штерьевые выводы, для подключения дополнительного устройства. Штырьевые выводы разведены и подключены к выводам микроконтроллера STM32F407: MISO-32 вывод , MOSI-31 вывод, SS-29 вывод. А так же обезательно наличие дополнитлельно разъёма под землю , для обеспечения разности потенциалов
 2) SWD.Данный интерфес применяеться для подключения программатора микроконтроллера . На плате размещены штерьевые выводы, для подключения дополнительного устройства. Штырьевые выводы разведены и подключены к выводам микроконтроллера STM32F407: SWDIO-72 вывод , SWCLK-76 вывод. Для этого разъёма применена аналогвая земла , так как малые значения напряжения.
 3) UART. При помощи данного интерфейса происходит общение GPS/ГЛОНАС модуля GEOS3R c МК .  RX1- 26 вывод, TX1- 25 вывод, а так же запасные RX0- 79 вывод, TX0- 78 вывод.
 4) USB. Данный интерфс преднозначен для связи готового устройства с USB, т.е для того того что бы снимать данные с датчика. Разъём USB подключается к USB - для отсеивания не нужных помех. Подключение к МК : D(in)2--60 , D(in)3-59. 

###  Внешние устройства 


    В прокте применяется глонас/GPS модуль GEOS3R. 
        Питание модуля :
           3.3V/1.8V- для напряжения питания ввода/вывода, 
           основное питание 1.8V использует для 
           
        "Общения" с МК (STM32f407) :
           tx(переадчу) и rx(принятие) данных

           Световая индикация:
           Светодиот подключаем к специальным выводам, которые отвечают за вкл/выкл модуля, за соганл пробуждения, за состояние модуля(логические уровни определяються напряжением питания VDD_IO), а так же за индикацию, которая показывает Активность и Сон модуля. Для каждого состояния работает своя индикация . Всего установленно 5 с ветодиодов. 

           Разъём под антенну подключается к специальному выводу.

           Выводы которые не используються подключаться к STM32f407 и передают в него свои данные , которые в дальнейшем нигде не используютсья. 

    В схеме не используються преоразователи напряжения: 
        
        1-- Из 12v-->5 v

        2-- Из 5v-->3.3 v

        3-- Из 3.3v-->1.8 v


    


