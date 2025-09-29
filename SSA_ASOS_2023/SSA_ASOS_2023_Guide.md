# SSA ASOS 2023
## Информация и решение проблем
### Просмотр глав в методичке
Чтобы увидеть отдельную панель с оглавлением ключевых блоков можно нажать эту кнопку
![](images/SSA_ASOS_2023_Guide_20250930000648241.png)
### Топология  
![](images/SSA_ASOS_2023_Guide_20250920165649989.png)
### Пользователи
- Для серверных машин

| Пользователь     | Пароль    |
|------------------|-----------|
| Administrator    | P@ssw0rd  |

- Для клиентских машин

| Пользователь     | Пароль    |
|------------------|-----------|
| User1            | P@ssw0rd  |

### Не работает Ctrl+Alt+Delete
Попробуйте Ctrl+Alt+End
### Рекомендации
* В процессе настройки читайте все информационные блоки текста, это полезно и иногда может подсказать решение если что-либо не сработало
## Таблицы
### Таблица 1
| Имя компьютера | Имя домена  | IP-адреса                              |
|----------------|-------------|----------------------------------------|
| DC-IZ          |             | 172.19.0.1/24                          |
| CLIENT-IZ      |             | DHCP                                   |
| IIS-IZ         | Izhevsk.ru  | 172.19.0.3/24,                         |
| EDGE-IZ        |             | 172.19.0.250/24, 200.100.50.101/24     |
|----------------|-------------|----------------------------------------|
| DC-M           |             | 172.16.0.1/24                          |
| FILES-M        |             | 172.16.0.2/24                          |
| SUBCA-M        | Moscow.ru   | 172.16.0.4/24                          |
| EDGE-M         |             | 172.16.0.250/24, 200.100.50.100/24     |
| CLIENT-M       |             | DHCP                                   |
|----------------|-------------|----------------------------------------|
| ROOTCA-M       | None        | 172.16.0.3/24                          |
### Таблица 2
Внимание, в pdf файле задания имена в таблице неправильные, здесь она отредактирована
| Ресурс          | Расположение                     | Доступ на чтение     | Доступ на запись    |
|-----------------|----------------------------------|----------------------|---------------------|
| Budget          |                                  | Project_Budget-R          | Project_Budget-W         |
| Intranet        | FILES-M—D:\shares\projects       | Project_Intranet-R        | Project_Intranet-W       |
| Logistics       |                                  | Project_Logistics-R       | Project_Logistics-W      |
## Базовая настройка
- Установим операционные системы, настроим имена машин, их ip адреса в соответствии с таблицей 1, DNS сервера для них и разрешим ICMP только для **CLIENT-IZ**, **EDGE-IZ**, **DC-M**, **FILES-M**, **SUBCA-M**, **EDGE-M**, **CLIENT-M**, **ROOTCA-M**

- Важно, шлюзы (Default Gateway) отличаются для разных сегментов сети, для каждого сегмента сети шлюзом является адрес интерфейса машин с именем **EDGE**, который смотрит внутрь сети
- На машинах с именем **EDGE** шлюз указывать не нужно, так же интерфейсы на них имеют следующее соответствие:
- Здесь показаны примеры и пояснения к настройке, все остальные машины настроить по аналогии

| В топологии | GUI Interface | CLI Interface Index |
|-------------|---------------|---------------------|
| e0          | Instance 0    | 1             	  |
| e1          | Instance 0 2  | 2             	  |

- Для машин с именем **Client** не нужно настраивать адреса и DNS, они будут получать их когда мы настроим DHCP Server

Для серверных машин с графикой:
![](images/SSA_ASOS_2023_Guide_20250920124043594.png)
![](images/SSA_ASOS_2023_Guide_20250920124115976.png)
![](images/SSA_ASOS_2023_Guide_20250920124137609.png)
![](images/SSA_ASOS_2023_Guide_20250920124451141.png)
![](images/SSA_ASOS_2023_Guide_20250920125007409.png)
![](images/SSA_ASOS_2023_Guide_20250920125043583.png)

Подождать открытия Server Manager
![](images/SSA_ASOS_2023_Guide_20250920125443298.png)
![](images/SSA_ASOS_2023_Guide_20250920125532430.png)

Перезагружаемся, снова доходим до пункта Local Server
![](images/SSA_ASOS_2023_Guide_20250920125830718.png)
![](images/SSA_ASOS_2023_Guide_20250920125915448.png)
![](images/SSA_ASOS_2023_Guide_20250920130651496.png)
![](images/SSA_ASOS_2023_Guide_20250920131025264.png)

Включим ICMP in
![](images/SSA_ASOS_2023_Guide_20250920131729768.png)
![](images/SSA_ASOS_2023_Guide_20250920131932221.png)

Для серверных машин без графики

Если терминал не отзывается на нажатие Ctrl+Alt+Del или Ctrl+Alt+End


То закрыть окошко на крестик, и нажать Ctrl+Alt+Del или Ctrl+Alt+End
![](images/SSA_ASOS_2023_Guide_20250920132643325.png)
![](images/SSA_ASOS_2023_Guide_20250920132756724.png)
![](images/SSA_ASOS_2023_Guide_20250920132823687.png)

Вводим
```
sconfig
```
![](images/SSA_ASOS_2023_Guide_20250920133154846.png)
![](images/SSA_ASOS_2023_Guide_20250920133320694.png)
![](images/SSA_ASOS_2023_Guide_20250920133425604.png)

Вводим
```
sconfig
```
![](images/SSA_ASOS_2023_Guide_20250920144019420.png)
![](images/SSA_ASOS_2023_Guide_20250920144645381.png)
![](images/SSA_ASOS_2023_Guide_20250920144951677.png)
![](images/SSA_ASOS_2023_Guide_20250920145043095.png)
![](images/SSA_ASOS_2023_Guide_20250920145200647.png)

Разрешим ICMP in

Вводим
```
sconfig
```
Далее вводим попорядку
```
4
3
```
![](images/SSA_ASOS_2023_Guide_20250921231153582.png)
![](images/SSA_ASOS_2023_Guide_20250921231206882.png)

Настройка имени компьютера для машин **CLIENT**
![](images/SSA_ASOS_2023_Guide_20250920162315507.png)
![](images/SSA_ASOS_2023_Guide_20250920162330870.png)
![](images/SSA_ASOS_2023_Guide_20250920162341206.png)

![](images/SSA_ASOS_2023_Guide_20250920162845366.png)
![](images/SSA_ASOS_2023_Guide_20250920162947699.png)
![](images/SSA_ASOS_2023_Guide_20250920163043970.png)
![](images/SSA_ASOS_2023_Guide_20250920163102710.png)
![](images/SSA_ASOS_2023_Guide_20250920163121161.png)

Здесь можно вписать любой текст, для быстрого выбора вопросов без открытия списка используйте колёсико мыши, повторяем трижды

![](images/SSA_ASOS_2023_Guide_20250920163258507.png)
![](images/SSA_ASOS_2023_Guide_20250920163337295.png)
Ждём перезагрузку

Настроим имя компьютера
![](images/SSA_ASOS_2023_Guide_20250920164718057.png)
![](images/SSA_ASOS_2023_Guide_20250920164937448.png)
![](images/SSA_ASOS_2023_Guide_20250920164955921.png)

Далее нажимаем "Закрыть" и нажимаем "Перезагрузить сейчас"

Включим ICMP in
![](images/SSA_ASOS_2023_Guide_20250920165255298.png)

Настроить по аналогии с тем, как настраивали для серверных машин с графикой

Проверим работу ICMP, пингуя те машины на которых разрешили его
![](images/SSA_ASOS_2023_Guide_20250920202530159.png)

Запретим использование «спящего режима» на **CLIENT-M**, для **CLIENT-IZ** по аналогии
![](images/SSA_ASOS_2023_Guide_20250927193015994.png)
![](images/SSA_ASOS_2023_Guide_20250927193023821.png)
![](images/SSA_ASOS_2023_Guide_20250927193237719.png)
![](images/SSA_ASOS_2023_Guide_20250927193304908.png)


## Поднятие домена
Пример для **DC-M**, для **DC-IZ** по аналогии
![](images/SSA_ASOS_2023_Guide_20250920202718199.png)
![](images/SSA_ASOS_2023_Guide_20250920202803403.png)
![](images/SSA_ASOS_2023_Guide_20250920202826822.png)
![](images/SSA_ASOS_2023_Guide_20250920202909406.png)
![](images/SSA_ASOS_2023_Guide_20250920202926239.png)
![](images/SSA_ASOS_2023_Guide_20250920202938517.png)
![](images/SSA_ASOS_2023_Guide_20250920203002282.png)
![](images/SSA_ASOS_2023_Guide_20250920203115411.png)
![](images/SSA_ASOS_2023_Guide_20250920203244932.png)
![](images/SSA_ASOS_2023_Guide_20250920203336492.png)
![](images/SSA_ASOS_2023_Guide_20250920203513309.png)
![](images/SSA_ASOS_2023_Guide_20250920203827198.png)
![](images/SSA_ASOS_2023_Guide_20250920203846582.png)
![](images/SSA_ASOS_2023_Guide_20250920203906851.png)
![](images/SSA_ASOS_2023_Guide_20250920203916157.png)
![](images/SSA_ASOS_2023_Guide_20250920203929458.png)
![](images/SSA_ASOS_2023_Guide_20250920204405826.png)
Сервер автоматически перезагрузится

Введём машины в домен в соответствии с таблицей 1
Для серверных машин с графикой
![](images/SSA_ASOS_2023_Guide_20250920224324533.png)
Вводим логин и пароль учетной записи администратора домена
![](images/SSA_ASOS_2023_Guide_20250920224425842.png)
Успешный ввод машины в домен выглядит так
![](images/SSA_ASOS_2023_Guide_20250920224508382.png)
![](images/SSA_ASOS_2023_Guide_20250920225153666.png)
![](images/SSA_ASOS_2023_Guide_20250920225216267.png)
![](images/SSA_ASOS_2023_Guide_20250920225224239.png)

Для серверных машин без графики
Вводим
```
sconfig
```
![](images/SSA_ASOS_2023_Guide_20250920224656816.png)
![](images/SSA_ASOS_2023_Guide_20250920224900660.png)
![](images/SSA_ASOS_2023_Guide_20250920225026276.png)
![](images/SSA_ASOS_2023_Guide_20250920225121001.png)
![](images/SSA_ASOS_2023_Guide_20250920225132815.png)
Клиентские машины в домен введём после настройки DHCP 

## Установка DHCP
На **DC-M**, на **DC-IZ** настроить DHCP по аналогии, но без failover

Мы уже знаем как дойти до вкладки "Select server roles", поэтому продолжим инструкцию оттуда
![](images/SSA_ASOS_2023_Guide_20250920232630995.png)
![](images/SSA_ASOS_2023_Guide_20250920232652780.png)
![](images/SSA_ASOS_2023_Guide_20250920232711168.png)
![](images/SSA_ASOS_2023_Guide_20250920232755463.png)
![](images/SSA_ASOS_2023_Guide_20250920232942207.png)
![](images/SSA_ASOS_2023_Guide_20250920232957350.png)
![](images/SSA_ASOS_2023_Guide_20250920233018912.png)
![](images/SSA_ASOS_2023_Guide_20250920233040118.png)
![](images/SSA_ASOS_2023_Guide_20250920233047879.png)
![](images/SSA_ASOS_2023_Guide_20250920233220956.png)
![](images/SSA_ASOS_2023_Guide_20250920233847522.png)
![](images/SSA_ASOS_2023_Guide_20250920233906657.png)
![](images/SSA_ASOS_2023_Guide_20250920233931442.png)
![](images/SSA_ASOS_2023_Guide_20250920234100049.png)
![](images/SSA_ASOS_2023_Guide_20250920234112909.png)
![](images/SSA_ASOS_2023_Guide_20250920234128352.png)
![](images/SSA_ASOS_2023_Guide_20250920234139758.png)
![](images/SSA_ASOS_2023_Guide_20250920234224521.png)
![](images/SSA_ASOS_2023_Guide_20250920234319325.png)
![](images/SSA_ASOS_2023_Guide_20250920234335580.png)
![](images/SSA_ASOS_2023_Guide_20250920234345122.png)
### Ввод клиентских машин в домен
На **CLIENT-M**

Чтобы удостовериться, что клиент получил адрес от DHCP сервера перед тем как ввести его в домен, вводим в cmd
```
ipconfig
```
![](images/SSA_ASOS_2023_Guide_20250920234900361.png)
Если клиент не получил адрес, вводим
```
ipconfig /renew
```
Вводим клиента в домен

Мы уже знаем как перейти в "Свойства системы", продолжим оттуда
![](images/SSA_ASOS_2023_Guide_20250920235348122.png)
![](images/SSA_ASOS_2023_Guide_20250920235422408.png)
![](images/SSA_ASOS_2023_Guide_20250920235441500.png)
![](images/SSA_ASOS_2023_Guide_20250920235450342.png)
![](images/SSA_ASOS_2023_Guide_20250921000717375.png)

### Настройка DHCP failover
Установим DHCP на FILES-M

Заходим на DC-M
![](images/SSA_ASOS_2023_Guide_20250921094619303.png)
![](images/SSA_ASOS_2023_Guide_20250921094744777.png)
Теперь переходим на страницу "Select Destination Server"
![](images/SSA_ASOS_2023_Guide_20250921094941617.png)
![](images/SSA_ASOS_2023_Guide_20250921095014177.png)
![](images/SSA_ASOS_2023_Guide_20250921095023098.png)
![](images/SSA_ASOS_2023_Guide_20250921095032969.png)
![](images/SSA_ASOS_2023_Guide_20250921095057245.png)
![](images/SSA_ASOS_2023_Guide_20250921095137708.png)
![](images/SSA_ASOS_2023_Guide_20250921095149955.png)
![](images/SSA_ASOS_2023_Guide_20250921095200071.png)
![](images/SSA_ASOS_2023_Guide_20250921095209258.png)
![](images/SSA_ASOS_2023_Guide_20250921095221703.png)
![](images/SSA_ASOS_2023_Guide_20250921095306577.png)
![](images/SSA_ASOS_2023_Guide_20250921095356737.png)
![](images/SSA_ASOS_2023_Guide_20250921095409919.png)
![](images/SSA_ASOS_2023_Guide_20250921095520462.png)
![](images/SSA_ASOS_2023_Guide_20250921095713859.png)
![](images/SSA_ASOS_2023_Guide_20250921095806519.png)
![](images/SSA_ASOS_2023_Guide_20250921100146690.png)
![](images/SSA_ASOS_2023_Guide_20250921100251302.png)
![](images/SSA_ASOS_2023_Guide_20250921100259430.png)

## DNS и AD
На **DC-M** 
![](images/SSA_ASOS_2023_Guide_20250921113942126.png)
![](images/SSA_ASOS_2023_Guide_20250921113949963.png)
![](images/SSA_ASOS_2023_Guide_20250921114010183.png)
![](images/SSA_ASOS_2023_Guide_20250921114036316.png)
![](images/SSA_ASOS_2023_Guide_20250921114046381.png)
![](images/SSA_ASOS_2023_Guide_20250921114054182.png)
![](images/SSA_ASOS_2023_Guide_20250921114120640.png)
![](images/SSA_ASOS_2023_Guide_20250921114148117.png)
![](images/SSA_ASOS_2023_Guide_20250921114249245.png)
![](images/SSA_ASOS_2023_Guide_20250921114306250.png)
![](images/SSA_ASOS_2023_Guide_20250921114457007.png)
![](images/SSA_ASOS_2023_Guide_20250921114853072.png)
![](images/SSA_ASOS_2023_Guide_20250921115230340.png)
![](images/SSA_ASOS_2023_Guide_20250921115239156.png)
![](images/SSA_ASOS_2023_Guide_20250921115420306.png)
![](images/SSA_ASOS_2023_Guide_20250921115432443.png)
![](images/SSA_ASOS_2023_Guide_20250921115448359.png)
![](images/SSA_ASOS_2023_Guide_20250921115517679.png)
![](images/SSA_ASOS_2023_Guide_20250921115854454.png)
Настроим и создадим PTR зону, а так же её репликацию на FILES-M 
![](images/SSA_ASOS_2023_Guide_20250921120104356.png)
![](images/SSA_ASOS_2023_Guide_20250921121924697.png)
![](images/SSA_ASOS_2023_Guide_20250921121931785.png)
![](images/SSA_ASOS_2023_Guide_20250921121959435.png)
![](images/SSA_ASOS_2023_Guide_20250921122014984.png)
![](images/SSA_ASOS_2023_Guide_20250921122025068.png)
![](images/SSA_ASOS_2023_Guide_20250921122131520.png)
![](images/SSA_ASOS_2023_Guide_20250921122215973.png)
![](images/SSA_ASOS_2023_Guide_20250921122233311.png)
![](images/SSA_ASOS_2023_Guide_20250921122628865.png)
Операцию создания PTR записи повторить для всех записей типа "A", кроме записей для машин **EDGE**, в которых IP адрес находится в другой подсети
![](images/SSA_ASOS_2023_Guide_20250921123034162.png)
Проверим, что зоны DNS реплицировались на **FILES-M**
![](images/SSA_ASOS_2023_Guide_20250921123447935.png)
![](images/SSA_ASOS_2023_Guide_20250921123558451.png)
## USERGATE
Его не будет, т.к. на текущем стенде в поставляемом образе отсутствует установщик :(
## RRAS
На **DC-M**, по аналогии настроить на **DC-IZ**
![](images/SSA_ASOS_2023_Guide_20250921135331560.png)
![](images/SSA_ASOS_2023_Guide_20250921135455901.png)
![](images/SSA_ASOS_2023_Guide_20250921135614119.png)
![](images/SSA_ASOS_2023_Guide_20250921135644748.png)
![](images/SSA_ASOS_2023_Guide_20250921135722387.png)
![](images/SSA_ASOS_2023_Guide_20250921135732945.png)
![](images/SSA_ASOS_2023_Guide_20250921135834840.png)
![](images/SSA_ASOS_2023_Guide_20250921135844746.png)
![](images/SSA_ASOS_2023_Guide_20250921135856138.png)
![](images/SSA_ASOS_2023_Guide_20250921135914902.png)
![](images/SSA_ASOS_2023_Guide_20250921135935011.png)
![](images/SSA_ASOS_2023_Guide_20250921140305996.png)
Далее пример настройки маршрутизации в сегменте Ижевска, по аналогии сделать в Москве
На **DC-IZ**
![](images/SSA_ASOS_2023_Guide_20250921221251567.png)
![](images/SSA_ASOS_2023_Guide_20250921221331687.png)
![](images/SSA_ASOS_2023_Guide_20250921221413479.png)
![](images/SSA_ASOS_2023_Guide_20250921221426435.png)
![](images/SSA_ASOS_2023_Guide_20250921221456656.png)
![](images/SSA_ASOS_2023_Guide_20250921221511070.png)
![](images/SSA_ASOS_2023_Guide_20250921221519214.png)
![](images/SSA_ASOS_2023_Guide_20250921221535513.png)
![](images/SSA_ASOS_2023_Guide_20250921221603344.png)
![](images/SSA_ASOS_2023_Guide_20250921221625596.png)
![](images/SSA_ASOS_2023_Guide_20250921222141968.png)
![](images/SSA_ASOS_2023_Guide_20250921222433982.png)
![](images/SSA_ASOS_2023_Guide_20250921222601169.png)
![](images/SSA_ASOS_2023_Guide_20250921223622111.png)
![](images/SSA_ASOS_2023_Guide_20250921223656643.png)
![](images/SSA_ASOS_2023_Guide_20250921223708679.png)
![](images/SSA_ASOS_2023_Guide_20250921225027983.png)
![](images/SSA_ASOS_2023_Guide_20250921225536628.png)
![](images/SSA_ASOS_2023_Guide_20250921225730942.png)
![](images/SSA_ASOS_2023_Guide_20250921225749600.png)
![](images/SSA_ASOS_2023_Guide_20250921225811066.png)
![](images/SSA_ASOS_2023_Guide_20250921225826484.png)
![](images/SSA_ASOS_2023_Guide_20250921225854425.png)
![](images/SSA_ASOS_2023_Guide_20250921225919814.png)
![](images/SSA_ASOS_2023_Guide_20250921230200276.png)
![](images/SSA_ASOS_2023_Guide_20250921232014077.png)
Теперь чтобы наши настройки точно применились, перезагрузим RRAS
![](images/SSA_ASOS_2023_Guide_20250921232256699.png)
Проверим, что между сетями есть связь, с **DC-M** пинганём **DC-IZ**
![](images/SSA_ASOS_2023_Guide_20250922210350979.png)

## Настройка трастов
Выполним задание
```
Настройка DC-M

Настройте одностороннее нетранзитивное доверие с доменом Izhevsk.ru – пользователи домена
Moscow.ru должны иметь доступ к ресурсам домена Izhevsk.ru, но не наоборот.
```
На **DC-M**
Добавим DNS сервер домена Izhevsk.ru на **DC-M**
![](images/SSA_ASOS_2023_Guide_20250922214046753.png)
![](images/SSA_ASOS_2023_Guide_20250922214056637.png)

Приступим к настройке трастов
![](images/SSA_ASOS_2023_Guide_20250922210830908.png)
![](images/SSA_ASOS_2023_Guide_20250922211039885.png)
![](images/SSA_ASOS_2023_Guide_20250922211204302.png)
![](images/SSA_ASOS_2023_Guide_20250922211951767.png) 
![](images/SSA_ASOS_2023_Guide_20250922214311756.png)
![](images/SSA_ASOS_2023_Guide_20250922215759333.png)
![](images/SSA_ASOS_2023_Guide_20250922215938680.png)
![](images/SSA_ASOS_2023_Guide_20250922220101342.png)
![](images/SSA_ASOS_2023_Guide_20250922220201122.png)
![](images/SSA_ASOS_2023_Guide_20250922220246775.png)
![](images/SSA_ASOS_2023_Guide_20250922220334367.png)
![](images/SSA_ASOS_2023_Guide_20250922220424666.png)
![](images/SSA_ASOS_2023_Guide_20250922220635947.png)
![](images/SSA_ASOS_2023_Guide_20250922220731945.png)

Теперь подтвердим траст
![](images/SSA_ASOS_2023_Guide_20250922223332251.png)
![](images/SSA_ASOS_2023_Guide_20250922223237165.png)
![](images/SSA_ASOS_2023_Guide_20250922223245248.png)

Теперь проверим что на **DC-IZ** траст тоже подтвержден
![](images/SSA_ASOS_2023_Guide_20250922223828138.png)
![](images/SSA_ASOS_2023_Guide_20250922224045161.png)

Чтобы проверить, что односторонний траст был настроен, на **CLIENT-IZ** зайдем под пользователем Administrator в домене Moscow.ru
![](images/SSA_ASOS_2023_Guide_20250922224620896.png)
Если нас впустило, то всё сработало
![](images/SSA_ASOS_2023_Guide_20250922224926227.png)


Проверим противоположное на **CLIENT-M**, авторизация не должна сработать
![](images/SSA_ASOS_2023_Guide_20250922224457148.png)
![](images/SSA_ASOS_2023_Guide_20250922224528222.png)

## GPO
### Элементы доменной инфраструктуры
Выполним задание
```
Cоздайте подразделения: Experts, Competitors, Managers, Visitors, IT и Project;
```
Дополнительно создадим ```CompanyUsers, ClientPCs```

![](images/SSA_ASOS_2023_Guide_20250924211310959.png)
![](images/SSA_ASOS_2023_Guide_20250924212040032.png)
![](images/SSA_ASOS_2023_Guide_20250924212119122.png)
Создайте оставшиеся OU по аналогии

Выполним задание
```
В соответствующих подразделениях создайте доменные группы:
Experts, Competitors, Managers, Visitors,IT , Project_Budget-R, Project_Budget-W, Project_Intranet-R, Project_Intranet-W, Project_Logistics-R, Project_Logistics-W;
```

![](images/SSA_ASOS_2023_Guide_20250924213935911.png)
![](images/SSA_ASOS_2023_Guide_20250924214228940.png)

Создайте остальные доменные группы по аналогии

```
Создайте 3-4 пользователя(вся имеющаяся информация о пользователях должна быть внесена в Active Directory); поместите пользователей в
соответствующие подразделения и группы; все созданные учетные записи должны быть включены и доступны;
```
#### Информация о пользователях
| Полное имя       | Логин     | Должность           | Отдел      | Группы AD       | Email               | Телефон       | Пароль   |
|------------------|-----------|---------------------|------------|-----------------|---------------------|---------------|----------|
| Ivan Petrov      | petrov.i  | System Administrator | IT  | Experts, IT     | petrov.i@company.ru | +74951112288 | P@ssw0rd |
| Olga Sidorova    | sidorova.o| Guest               | External Relations | Visitors      | sidorova.o@company.ru | +74951112299 | P@ssw0rd |
| Dmitry Kovalev   | kovalev.d | Logistics Manager   | Logistics  | Logistics, Managers | kovalev.d@company.ru | +74951113300 | P@ssw0rd |


![](images/SSA_ASOS_2023_Guide_20250924224506035.png)
![](images/SSA_ASOS_2023_Guide_20250924224819600.png)
![](images/SSA_ASOS_2023_Guide_20250924224921810.png)
![](images/SSA_ASOS_2023_Guide_20250924224932019.png)
![](images/SSA_ASOS_2023_Guide_20250924225038411.png)
![](images/SSA_ASOS_2023_Guide_20250924225503896.png)
![](images/SSA_ASOS_2023_Guide_20250924225630384.png)
![](images/SSA_ASOS_2023_Guide_20250924225912037.png)
Остальных пользователей создать по аналогии

### Остальные задания GPO

На **DC-M**
Выполним задание

```
запретите анимацию при первом входе пользователей в систему на всех клиентских компьютерах
домена
```
![](images/SSA_ASOS_2023_Guide_20250922234153722.png)
![](images/SSA_ASOS_2023_Guide_20250922234319643.png)
![](images/SSA_ASOS_2023_Guide_20250922234445124.png)
![](images/SSA_ASOS_2023_Guide_20250922234936589.png)
![](images/SSA_ASOS_2023_Guide_20250922235006667.png)
![](images/SSA_ASOS_2023_Guide_20250922235354592.png)
![](images/SSA_ASOS_2023_Guide_20250922235551584.png)
![](images/SSA_ASOS_2023_Guide_20250922235611446.png)
![](images/SSA_ASOS_2023_Guide_20250925182213874.png)
![](images/SSA_ASOS_2023_Guide_20250925182349965.png)
![](images/SSA_ASOS_2023_Guide_20250925182420062.png)
![](images/SSA_ASOS_2023_Guide_20250925182607845.png)
![](images/SSA_ASOS_2023_Guide_20250925182735064.png)

Проверим отсутствие анимации на **CLIENT-M**, авторизировавшись на нём от имени администратора домена, но перед этим компьютер нужно перезагрузить для применения групповых политик
![](images/SSA_ASOS_2023_Guide_20250923002144465.png)
![](images/SSA_ASOS_2023_Guide_20250923000036949.png)

Если всё сработало, то во время входа будет надпись "Подготовка Windows" вместо стандартной анимации, начинающийся с текста "Привет!"

Выполним задание 
```
Члены группы IT должны быть членами группы локальных администраторов на всех клиентских компьютерах домена;
```
![](images/SSA_ASOS_2023_Guide_20250925185340599.png)
![](images/SSA_ASOS_2023_Guide_20250925185409133.png)
![](images/SSA_ASOS_2023_Guide_20250925185432565.png)
![](images/SSA_ASOS_2023_Guide_20250925185719638.png)
![](images/SSA_ASOS_2023_Guide_20250925185952629.png)
![](images/SSA_ASOS_2023_Guide_20250925190119565.png)
![](images/SSA_ASOS_2023_Guide_20250925190239591.png)

Проверим работу этой политики
Заходим на **CLIENT-M** под юзером `petrov.i`
Обновим политики
![](images/SSA_ASOS_2023_Guide_20250925200114389.png)
![](images/SSA_ASOS_2023_Guide_20250925200156679.png)
![](images/SSA_ASOS_2023_Guide_20250925200325798.png)

Выполним задание
```
Запретите изменение экранной заставки и Корзину на рабочем столе для всех пользователей домена, кроме членов группы локальных администраторов клиентских компьютеров
```
На **DC-M** создадим политику для всего домена с именем wallpapers_and_bin и настроим её
![](images/SSA_ASOS_2023_Guide_20250925201733747.png)
![](images/SSA_ASOS_2023_Guide_20250925201818858.png)
Теперь уберём корзину с рабочего стола
![](images/SSA_ASOS_2023_Guide_20250925202045026.png)
![](images/SSA_ASOS_2023_Guide_20250925202108888.png)
Так же отключим применение для группы IT
![](images/SSA_ASOS_2023_Guide_20250927160441074.png)

Перейдём на **CLIENT-M**

Перезагрузим его

Зайдём под пользователем `sidorova.o`

Если на рабочем столе нет корзины, значит политика применилась
![](images/SSA_ASOS_2023_Guide_20250925225738297.png)

#### RAID-5 на FILES-M
```
Из трех имеющихся жестких дисков создайте RAID-5 массив; назначьте ему букву D:\.
```
Перейдём на **FILES-M**
![](images/SSA_ASOS_2023_Guide_20250926202543517.png)

Перед тем как сделать диск динамическим, нужно прописать
```
attribute clear disk readonly
```

Иначе будет следующая ошибка: 
![](images/SSA_ASOS_2023_Guide_20250926202713127.png)

После очистки атрибута `readonly` всё отрабатывает корректно
![](images/SSA_ASOS_2023_Guide_20250926203042281.png)

Эти действия необходимо проделать так же с 2 и 3 дисками, должно получиться следующее

![](images/SSA_ASOS_2023_Guide_20250926203712058.png)
После этого, создадим рейд массив

![](images/SSA_ASOS_2023_Guide_20250926204009797.png)
Буква D уже занята, поэтому сначала удалим её а потом присвоим нашему рейд массиву

![](images/SSA_ASOS_2023_Guide_20250926204257831.png)
Отформатируем раздел

![](images/SSA_ASOS_2023_Guide_20250926211049069.png)

Выполним задание
```
Для членов группы Experts настройте перенаправление папок my Documents и Desktop по адресу FILES-M→d:\shared\redirected
```
На **FILES-M** создадим папку
```
mkdir D:\shared\redirected
```

Теперь на **DC-M** создадим шару
![](images/SSA_ASOS_2023_Guide_20250926221311396.png)
![](images/SSA_ASOS_2023_Guide_20250926221412092.png)
![](images/SSA_ASOS_2023_Guide_20250926221659926.png)
![](images/SSA_ASOS_2023_Guide_20250926221730297.png)
![](images/SSA_ASOS_2023_Guide_20250926223158597.png)
![](images/SSA_ASOS_2023_Guide_20250926223222741.png)
![](images/SSA_ASOS_2023_Guide_20250926223513478.png)
![](images/SSA_ASOS_2023_Guide_20250927020432890.png)
![](images/SSA_ASOS_2023_Guide_20250927020600590.png)
![](images/SSA_ASOS_2023_Guide_20250927020634822.png)
![](images/SSA_ASOS_2023_Guide_20250927020902609.png)
![](images/SSA_ASOS_2023_Guide_20250927020922759.png)
![](images/SSA_ASOS_2023_Guide_20250927021205259.png)
![](images/SSA_ASOS_2023_Guide_20250927021220647.png)
![](images/SSA_ASOS_2023_Guide_20250927021302555.png)
![](images/SSA_ASOS_2023_Guide_20250927021335541.png)
![](images/SSA_ASOS_2023_Guide_20250927021530645.png)
![](images/SSA_ASOS_2023_Guide_20250927021602580.png)
![](images/SSA_ASOS_2023_Guide_20250927021703255.png)
![](images/SSA_ASOS_2023_Guide_20250927021712649.png)
![](images/SSA_ASOS_2023_Guide_20250927021743051.png)
![](images/SSA_ASOS_2023_Guide_20250927021759878.png)
![](images/SSA_ASOS_2023_Guide_20250927021807869.png)
![](images/SSA_ASOS_2023_Guide_20250927021815384.png)
![](images/SSA_ASOS_2023_Guide_20250927021842020.png)
![](images/SSA_ASOS_2023_Guide_20250927021916759.png)
![](images/SSA_ASOS_2023_Guide_20250927022019109.png)
![](images/SSA_ASOS_2023_Guide_20250927022027849.png)
![](images/SSA_ASOS_2023_Guide_20250927022039517.png)
![](images/SSA_ASOS_2023_Guide_20250927022402806.png)

Создадим групповую политику в корне домена под названием `RedirectExperts` и отредактируем её
![](images/SSA_ASOS_2023_Guide_20250927022720502.png)
![](images/SSA_ASOS_2023_Guide_20250927022825801.png)
По аналогии сделаем с `Documents`

Зайдём на **CLIENT-M** под пользователем `ivan.p` и обновим политики в cmd
```
gpupdate /force
```
![](images/SSA_ASOS_2023_Guide_20250927023639977.png)

Снова логинимся под пользователем `ivan.p`
Проверим, где теперь находятся файлы на рабочем столе
![](images/SSA_ASOS_2023_Guide_20250927023913400.png)
![](images/SSA_ASOS_2023_Guide_20250927024005539.png)

Выполним задание из пункта "Элементы доменной инфраструктуры" 
```
Для каждого пользователя создайте автоматически подключаемую в качестве диска U:\ домашнюю папку по адресу FILES-M→d:\shares\users.
```
На **DC-M**
Создадим нужные папки на **FILES-M**

![](images/SSA_ASOS_2023_Guide_20250927162359845.png)
![](images/SSA_ASOS_2023_Guide_20250927162612390.png)

В итоге должен получиться следующий путь
![](images/SSA_ASOS_2023_Guide_20250927162701807.png)
Так же внутри папки `users` создадим папки с системным именем пользователей в качестве названия
```
kovalev.d
petrov.i
sidorova.o
```
Для каждой из них настроим доступ конкретному пользователю
![](images/SSA_ASOS_2023_Guide_20250927174629127.png)
![](images/SSA_ASOS_2023_Guide_20250927174934261.png)



Настроим сетевую шару выбирая путь `d:\shares\users` 
![](images/SSA_ASOS_2023_Guide_20250927164215326.png)
![](images/SSA_ASOS_2023_Guide_20250927164242768.png)
![](images/SSA_ASOS_2023_Guide_20250927164340138.png)
![](images/SSA_ASOS_2023_Guide_20250927164437722.png)
![](images/SSA_ASOS_2023_Guide_20250927164801735.png)
![](images/SSA_ASOS_2023_Guide_20250927165145421.png)
![](images/SSA_ASOS_2023_Guide_20250927165304211.png)
![](images/SSA_ASOS_2023_Guide_20250927165338650.png)
![](images/SSA_ASOS_2023_Guide_20250927165907053.png)
![](images/SSA_ASOS_2023_Guide_20250927165926827.png)
![](images/SSA_ASOS_2023_Guide_20250927165511496.png)
![](images/SSA_ASOS_2023_Guide_20250927165547963.png)
![](images/SSA_ASOS_2023_Guide_20250927165605873.png)
![](images/SSA_ASOS_2023_Guide_20250927165627700.png)
![](images/SSA_ASOS_2023_Guide_20250927170622218.png)
![](images/SSA_ASOS_2023_Guide_20250927170652342.png)
![](images/SSA_ASOS_2023_Guide_20250927170703094.png)
![](images/SSA_ASOS_2023_Guide_20250927170714453.png)
Создадим GPO для автоподключения диска в корне домена под именем "DiskU" и настроим его
![](images/SSA_ASOS_2023_Guide_20250927175748154.png)
Теперь зайдём на **CLIENT-M** под чьим-либо аккаунтом и проверим что диск подключен, так же попробуем создать файл
![](images/SSA_ASOS_2023_Guide_20250927175839804.png)

## Общие папки
```
Cоздайте общие папки для подразделений (Competitors, Experts and Managers) по адресу FILES-M→d:\shares\departments;
Обеспечьте привязку общей папки подразделения к соответствующей группе в качестве диска G:\;
```
Создадим папку на **FILES-M** вследующем расположении
![](images/SSA_ASOS_2023_Guide_20250927210931588.png)

Пошарим эту папку по сети
![](images/SSA_ASOS_2023_Guide_20250927211522860.png)
![](images/SSA_ASOS_2023_Guide_20250927211537032.png)
![](images/SSA_ASOS_2023_Guide_20250927211625516.png)
![](images/SSA_ASOS_2023_Guide_20250927211656404.png)
![](images/SSA_ASOS_2023_Guide_20250927211824274.png)
![](images/SSA_ASOS_2023_Guide_20250927211907744.png)
![](images/SSA_ASOS_2023_Guide_20250927211947444.png)
![](images/SSA_ASOS_2023_Guide_20250927212142635.png)
![](images/SSA_ASOS_2023_Guide_20250927212250080.png)
![](images/SSA_ASOS_2023_Guide_20250927212310615.png)
![](images/SSA_ASOS_2023_Guide_20250927212359314.png)
![](images/SSA_ASOS_2023_Guide_20250927212420361.png)
![](images/SSA_ASOS_2023_Guide_20250927212537402.png)
![](images/SSA_ASOS_2023_Guide_20250927212548197.png)
![](images/SSA_ASOS_2023_Guide_20250927212601136.png)
![](images/SSA_ASOS_2023_Guide_20250927212615336.png)
Создадим папки и выдадим права нужным группам
![](images/SSA_ASOS_2023_Guide_20250927213226716.png)
![](images/SSA_ASOS_2023_Guide_20250927213326856.png)
![](images/SSA_ASOS_2023_Guide_20250927213442658.png)
![](images/SSA_ASOS_2023_Guide_20250927213603577.png)
![](images/SSA_ASOS_2023_Guide_20250927213616533.png)
Оставшимся папкам настроим права по аналогии

Создадим GPO в корне домена и назовём его "DiskG", а так же настроим
![](images/SSA_ASOS_2023_Guide_20250927213855748.png)
![](images/SSA_ASOS_2023_Guide_20250927214615046.png)
![](images/SSA_ASOS_2023_Guide_20250927214634817.png)

Тут представлена настройка для "Competitors", для остальных настройте по аналогии
![](images/SSA_ASOS_2023_Guide_20250927214727873.png)
![](images/SSA_ASOS_2023_Guide_20250927214933298.png)
![](images/SSA_ASOS_2023_Guide_20250927214945581.png)
![](images/SSA_ASOS_2023_Guide_20250927215000979.png)
![](images/SSA_ASOS_2023_Guide_20250927215231212.png)

В итоге должно получиться так
![](images/SSA_ASOS_2023_Guide_20250927220441118.png)

Перейдём на **CLIENT-M** и обновим политики
```
gpupdate /force
```
![](images/SSA_ASOS_2023_Guide_20250927215738221.png)

Проверим работу политики, залогинимся под юзером `petrov.i`, откроем диск и создадим файл
![](images/SSA_ASOS_2023_Guide_20250927220255980.png)

Выполним задания
```
Создайте общую папку проектов по адресу FILES-M→d:\shares\projects;
В папке d:\shares\projects создайте следующие папки: Budget, Intranet, Logistics; 
Настройте разрешения этих папок в соответствии с таблицей 2;
```
![](images/SSA_ASOS_2023_Guide_20250927220616057.png)
![](images/SSA_ASOS_2023_Guide_20250927220909966.png)

Пример для `Budget`, оставшиеся настроить по аналогии
![](images/SSA_ASOS_2023_Guide_20250927221026910.png)
![](images/SSA_ASOS_2023_Guide_20250928110948704.png)
![](images/SSA_ASOS_2023_Guide_20250928111039144.png)
![](images/SSA_ASOS_2023_Guide_20250928111048645.png)

Расшарим папку по сети
![](images/SSA_ASOS_2023_Guide_20250928133225838.png)
![](images/SSA_ASOS_2023_Guide_20250928133238213.png)
![](images/SSA_ASOS_2023_Guide_20250928133246103.png)
![](images/SSA_ASOS_2023_Guide_20250928133349772.png)
![](images/SSA_ASOS_2023_Guide_20250928133415259.png)
![](images/SSA_ASOS_2023_Guide_20250928133847048.png)
![](images/SSA_ASOS_2023_Guide_20250928133910346.png)
![](images/SSA_ASOS_2023_Guide_20250928134032158.png)
![](images/SSA_ASOS_2023_Guide_20250928143435108.png)
![](images/SSA_ASOS_2023_Guide_20250928143456341.png)
![](images/SSA_ASOS_2023_Guide_20250928144841160.png)
![](images/SSA_ASOS_2023_Guide_20250928144858706.png)
![](images/SSA_ASOS_2023_Guide_20250928144928365.png)
![](images/SSA_ASOS_2023_Guide_20250928144951725.png)
![](images/SSA_ASOS_2023_Guide_20250928145342299.png)
![](images/SSA_ASOS_2023_Guide_20250928145409645.png)
![](images/SSA_ASOS_2023_Guide_20250928145438378.png)
![](images/SSA_ASOS_2023_Guide_20250928145507377.png)
![](images/SSA_ASOS_2023_Guide_20250928145521361.png)
![](images/SSA_ASOS_2023_Guide_20250928145530469.png)

Создадим в корне домена GPO с именем "DiskP", а так же настроим эту политику
![](images/SSA_ASOS_2023_Guide_20250928145829047.png)
![](images/SSA_ASOS_2023_Guide_20250928150109018.png)
![](images/SSA_ASOS_2023_Guide_20250928150122303.png)
![](images/SSA_ASOS_2023_Guide_20250928150242318.png)
![](images/SSA_ASOS_2023_Guide_20250928150514755.png)

Переходим на **CLIENT-M** и обновляем политики
```
gpupdate /force
```
![](images/SSA_ASOS_2023_Guide_20250928150934158.png)

Логинимся под пользователем `kovalev.d` и проверяем, что у нас показывается на диске P:
Пользователь может видеть только папку, к которой у него есть доступ
![](images/SSA_ASOS_2023_Guide_20250928152702079.png)
Проверим права записи, создав файл
![](images/SSA_ASOS_2023_Guide_20250928152750997.png)

## Квоты/Файловые экраны
На **DC-M**
![](images/SSA_ASOS_2023_Guide_20250929220013066.png)
![](images/SSA_ASOS_2023_Guide_20250929220114246.png)
![](images/SSA_ASOS_2023_Guide_20250929220152266.png)
![](images/SSA_ASOS_2023_Guide_20250929220216543.png)
![](images/SSA_ASOS_2023_Guide_20250929220323182.png)
![](images/SSA_ASOS_2023_Guide_20250929221740716.png)
![](images/SSA_ASOS_2023_Guide_20250929221809333.png)

Зайдём на **CLIENT-M** и проверим работу квоты
- если уже были залогинены под юзером то нужно перезайти
![](images/SSA_ASOS_2023_Guide_20250929221926475.png)

Выполним задание
```
Запретите хранение в домашних папках пользователей файлов с расширениями .cmd и .exe; учтите, что файлы остальных типов пользователи вправе хранить в домашних папках.
```
На **FILES-M** необходимо предварительно отключить файрвол на время настройки
```
netsh fi set opmode DISABLE
```
Продолжим настройку с **DC-M**
![](images/SSA_ASOS_2023_Guide_20250929222734212.png)
![](images/SSA_ASOS_2023_Guide_20250929222745590.png)
![](images/SSA_ASOS_2023_Guide_20250929222759799.png)
![](images/SSA_ASOS_2023_Guide_20250929222806752.png)
![](images/SSA_ASOS_2023_Guide_20250929222830790.png)
![](images/SSA_ASOS_2023_Guide_20250929222837284.png)
![](images/SSA_ASOS_2023_Guide_20250929222945403.png)
![](images/SSA_ASOS_2023_Guide_20250929223005600.png)
![](images/SSA_ASOS_2023_Guide_20250929223056458.png)
![](images/SSA_ASOS_2023_Guide_20250929233818290.png)
![](images/SSA_ASOS_2023_Guide_20250929235948895.png)
![](images/SSA_ASOS_2023_Guide_20250929234138753.png)
![](images/SSA_ASOS_2023_Guide_20250929234441808.png)
![](images/SSA_ASOS_2023_Guide_20250929234556886.png)
![](images/SSA_ASOS_2023_Guide_20250929234726299.png)
![](images/SSA_ASOS_2023_Guide_20250929234824346.png)

Проверим настройки на **CLIENT-M**

Создадим на рабочем столе файл с расширением .exe и попробуем переместить его в сетевую папку
![](images/SSA_ASOS_2023_Guide_20250929235015306.png)
![](images/SSA_ASOS_2023_Guide_20250929235123280.png)
![](images/SSA_ASOS_2023_Guide_20250930000239781.png)
