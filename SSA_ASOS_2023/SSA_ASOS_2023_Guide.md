# SSA ASOS 2023
## Информация и решение проблем
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
| Ресурс          | Расположение                     | Доступ на чтение     | Доступ на запись    |
|-----------------|----------------------------------|----------------------|---------------------|
| Budget          |                                  | RU-Budget-R          | RU-Budget-W         |
| Intranet        | FILES-M—D:\shares\projects       | RU-Intranet-R        | RU-Intranet-W       |
| Logistics       |                                  | RU-Logistics-R       | RU-Logistics-W      |
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

Перейдём на **CLIENT-M**

Перезагрузим его

Зайдём под пользователем `sidorova.o`

Если на рабочем столе нет корзины, значит политика применилась
![](images/SSA_ASOS_2023_Guide_20250925225738297.png)