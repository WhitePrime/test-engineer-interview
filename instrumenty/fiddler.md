# Fiddler



[IT-инфраструктура \*](https://habr.com/ru/hub/it-infrastructure/)[Серверное администрирование \*](https://habr.com/ru/hub/s\_admin/)![](https://habrastorage.org/r/w1560/getpro/habr/upload\_files/96c/d40/6ee/96cd406ee9c316214b2127c35410b7bc.png)

Привет. В данной статье расскажу как и зачем можно изменять HTTP пакеты при отправке на сервер и при получении ответов от сервера.\
В статье много практических примеров.

### Зачем это делать ?

Пример 1. **Анализ трафика.**\
Пользователи вашей сети пользуются вашим прокси-сервером. Вы можете увидеть на какие сайты заходят пользователи, запрещать дальнейшие переходы на эти сайты.

Пример 2. **Сбор данных.**\
Ваши пользователи пользуются через вас некоторыми веб-ресурсами. Например, они вводят vin-номер своего автомобиля на сайте дилера авто и получают в ответ данные этого автомобиля. Вы можете сохранять эти данные в свою базу данных.

Пример 3. **Подмена HTTP-пакетов.**\
Вам нужно изменить для ваших пользователей внешний вид сайта. Вы можете изменить стили сайта, скрывать любые элементы, добавить свои элементы, вырезать определенные слова или заменить их на другие слова, изменить картинку сайта на любую свою.

Пример 4. **Подмена POST-данных.**\
Вам нужно подправить данные передаваемые на веб-сервер через POST-запрос. Существует множество информации передаваемой в POST-запросах. Пример: отправка логина/пароля на сервер в процессе авторизации. Или онлайн тест отправляет на сервер результаты вашего теста.

### Установка Fiddler

1. Переходим на [https://www.telerik.com/download/fiddler](https://www.telerik.com/download/fiddler), скачиваем Fiddler Classic.
2. Установка простая и быстрая.
3. Запускаем программу.

### Настройка Fiddler

![](https://habrastorage.org/r/w1560/getpro/habr/upload\_files/5f2/649/514/5f2649514ec6e2f7a04b16b311084ded.png)

В меню File есть опция "_Capture Traffic_". По умолчанию опция включена. Это означает что Fiddler прописывает в реестре Windows себя в качестве прокси-сервера. Браузеры Internet Explorer, Edge, Chrome используют данную настройку, а значит HTTP-пакеты от этих браузеров пойдут через Fiddler.

![](https://habrastorage.org/r/w1560/getpro/habr/upload\_files/cc0/246/69c/cc024669c29d19a4ec79e634d81806ec.png)

Если опция "_File -> Capture Traffic_" выключена, то Fiddler перестает работать как системный прокси-сервер и перехватывает только те пакеты, которые идут непосредственно на адрес Fiddler. Это может быть когда вы настроили ваше приложение или браузер сами для работы через ip/port Fiddler. По умолчанию Fiddler слушает на порту 127.0.0.1:8888

Опция "_Keep: All sessions_".\
В данном режиме Fiddler не очищает журнал собранных HTTP-пакетов. Если требуется продолжительная работа Fiddler, то при большой нагрузке этих пакетов будет очень много и Fiddler скушает всю доступную оперативную память компьютера. Чтобы этого не случилось переключите в режим "Keep: 100 sessions".

Опция "_Decode_".\
По умолчанию выключена. В процессе анализа собранных пакетов рекомендуется включить чтобы пакеты автоматически декодировались. Либо можно выделить собранные пакеты через Ctrl+A, вызвать меню нажатием правой кнопки мыши по выделенным пакетам и нажать "Decode Selected Sessions".

![](https://habrastorage.org/r/w1560/getpro/habr/upload\_files/b29/502/e12/b29502e12a7bbd3ceefb1f17b60fdacb.png)

### Основные настройки

Переходим в "_Tools -> Options..._".\
\
**Вкладка "HTTPS".**\
После установки Fiddler не собирает HTTPS-трафик, это необходимо включить. Ставим галочку в опции "_Decrypt HTTPS traffic_". После этого Fiddler сгенерирует самоподписанный сертификат и спросит хотите ли установить данный сертификат. Отвечаем да.\
\
Опция "_Ignore server certificate errors (unsafe)_" - сразу можно не включать. На некоторых порталах бывают ошибки сертификатов, но это редко. Как увидите так включите )\
Настройка протоколов. По умолчанию стоит значение "\<client>;ssl3;tls1.0". Советую сразу установить значение на "\<client>;ssl3;tls1.0;tls1.1;tls1.2". После изменения настроек необходимо перезапустить программу чтобы настройки вступили в силу.

![](https://habrastorage.org/r/w1560/getpro/habr/upload\_files/a68/31f/d34/a6831fd34c7a038a1496b358ee8b8d90.png)

Кнопка "_Actions_":

![](https://habrastorage.org/r/w1560/getpro/habr/upload\_files/ce5/299/81a/ce529981a561b30b9e58ab0686e1f173.png)

"_Trust Root Certificate_" - если сгенерированный Fiddler сертификат вы не установили после включения опции "Decrypt HTTPS traffic", то можно это сделать здесь.

"_Export Root Certificate to Desktop_" - если вы планируете использовать Fiddler как прокси-сервер локальной сети, то на каждом устройстве пользователя необходимо установить сгенерированный выше сертификат. С помощью этой опции сохраняете сертификат на ваш рабочий стол.

"_Reset All Certificates_" - в некоторых случаях необходимо сгенерировать новый сертификат взамен старого. В этом случае сбрасываем все Fiddler-сертификаты и генерируем новый сертификат.

**Вкладка "Connections".**\
Здесь устанавливаем на каком порту Fiddler работает как прокси-сервер. Порт по умолчанию "8888".

"_Allow remote computers to connect_" - включаем опцию чтобы Fiddler начал принимать подключения от других компьютеров.

"_Act as system proxy on startup_" - по умолчанию опция включена. Если включена, то при запуске опция "File -> Capture Traffic" включена.

![](https://habrastorage.org/r/w1560/getpro/habr/upload\_files/f63/b7c/6a3/f63b7c6a3f856092758ff31a6723587b.png)

После изменения данных настроек необходимо перезапустить программу чтобы настройки вступили в силу.

**Вкладка "Gateway".**\
Здесь устанавливаем куда Fiddler отправляет входящие пакеты, какой прокси использует.

"_Use System Proxy (recommended)_" - использование системного прокси из реестра текущего пользователя.

"_Manual Proxy Configuration_" - возможность задать вручную прокси-сервер.

"_No proxy_" - задаем что выход в Интернет напрямую, без использования прокси.

После изменения данных настроек необходимо перезапустить программу чтобы настройки вступили в силу.

![](https://habrastorage.org/r/w1560/getpro/habr/upload\_files/013/6b3/8aa/0136b38aa2eca2be628f8f97a9ce6440.png)

### Установка сертификатов на Windows устройствах

После того как сгенерированный сертификат скопирован на рабочий стол этот сертификат необходимо установить на каждое устройство которое будет использовать данный Fiddler в качестве прокси-сервера.

Для установки сертификата используем консоль управления MMC: в коммандной строке вводим команду "mmc".

В меню файл выбираем "_Добавить или удалить оснастку_". Из доступных оснасток выбираем "_Сертификаты_" и с помощью кнопки "_Добавить_" выбираем данную оснастку. Нажимаем "Ок" и выбираем "_учетной записи компьютера_". Это нужно чтобы открыть сертификаты которые установлены для всего компьютера, а затем установить сертификат Fiddler именно в это хранилище. Если открыть сертификаты "_моей учетной записи пользователя_", то после установки сертификата Fiddler в это хранилище другие пользователи данного компьютера не смогут подключиться к Fiddler.

![](https://habrastorage.org/r/w1560/getpro/habr/upload\_files/203/9a1/1b3/2039a11b37a6222f3644dd3f28959092.png)

Установку сертификата производим в "Доверенные корневые центры сертификации".

![](https://habrastorage.org/r/w1560/getpro/habr/upload\_files/d97/8ad/d13/d978add13e7a945ff6bc4c07ee454aa6.png)

Если ваши компьютеры находятся в домене, то используйте инструменты домена для установки сертификата каждому пользователю или на каждый компьютер сети.

### Анализ трафика

В процессе работы Fiddler сниффит все HTTP-запросы и их обычно много. Для поиска необходимых запросов можно использовать фильтры. Правой кнопкой мыши выбираем лишний запрос, выбираем "_Filter Now_" и "_Hide '...'_" чтобы скрыть запросы к данному домену. Можно удалять вручную выделенные запросы используя кнопку "_Delete_".

![](https://habrastorage.org/r/w1560/getpro/habr/upload\_files/835/8c4/7bc/8358c47bccd65d7394ca318a6b247047.png)

Кроме использования фильтров можно искать отдельный текст в теле запросов/ответов: "_Ctrl+F_" для открытия меню поиска. Найденные запросы подсвечиваются по умолчанию желтым цветом.

![](https://habrastorage.org/r/w1560/getpro/habr/upload\_files/dda/9e6/3d1/dda9e63d187e1c2bd9458a16f2eaf023.png)

### Изменение данных запросов

В Fiddler существует инструмент "_Fiddler ScriptEditor_" (Редактор скриптов) для создания правил модификации трафика. Запуск редактора скриптов через "_Ctrl+R_" или выбора пункта меню "_Rules -> Customize Rules..._".

В редакторе скриптов есть два основных метода: "_OnBeforeRequest_" и "_OnBeforeResponse_":

"_OnBeforeRequest_" - выполнение скриптов в этом методе происходит перед отправкой пакетов на веб-сервер.

"_OnBeforeResponse_" - выполнение скриптов в этом методе происходит после получения ответа от веб-сервера.

Ниже приведены примеры скриптов с указанием в каком методе их расположить.

### Задача 1: Запрет сайта

Запрещаем переход на адрес сайта содержащий строку.

```
// OnBeforeRequest
if (oSession.uriContains("//ya.ru/")) oSession.host = 'access.denied';
```

### Задача 2: Запрет загрузки ресурса

Запрещаем загрузку "_.svg_" файлов для заданного адреса сайта.

```
// OnBeforeRequest
if (oSession.uriContains("yastatic.net") && oSession.url.EndsWith(".svg"))
{
		oSession.host = 'na.derevnu.dedushke';
}

// или

// OnBeforeRequest
if (oSession.uriContains("yastatic.net") && oSession.url.EndsWith(".svg"))
{
		oSession.responseBodyBytes = new byte[0];
}

// OnBeforeResponse
if (oSession.uriContains("yastatic.net") && oSession.url.EndsWith(".svg"))
{
		oSession.ResponseBody = null;
}
```

### Задача 3: Переадресация запроса

Переадресация запроса на адрес сайта содержащий строку.

```
// OnBeforeRequest
if (oSession.uriContains("//ya.ru/")) oSession.url = "yandex.ru"
```

### Задача 4: Сбор данных

Пользователи подключаются через данный прокси-сервер и делают в браузерах некоторые запросы вида "_https://myhost.ru?key=abcd\&vin=VF38BLFXE81078232\&lang=ru_". Задача записать в базу данных событие поиска и передать значение vin-номера. Данный скрипт создает файлы с названием включающем vin-номер. Кроме скрипта необходимо создать утилиту/службу, которая раз в заданный интервал читает каталог "_C:\vinsearch\\_" и записывает данные в базу данных.

```
// OnBeforeResponse
if(oSession.uriContains("https://myhost.ru?key=") && oSession.uriContains("&vin="))
{
		oSession.utilDecodeResponse();
		// поиск позиции индекса начала vin-номера
		var startVin = oSession.url.IndexOf("vin=") + 4;

		// поиск позиции индекса конца vin-номера
		var endVin = oSession.url.IndexOf("&", startVin);

  	// поиск подстроки зная индекс начала и индекс конца подстроки
		var vin = oSession.url.Substring(startVin, endVin - startVin);

		// создание файла с именем типа vin_текущееЗначениеМиллисекунд.txt
		oSession.SaveResponseBody("C:\\vinsearch\\" + vin + "_" + DateTime.Now.Millisecond + ".txt");
}
```

### Задача 5: Изменить текст в ответе

В данном примере меняем текст "_Иванов_" на "_Петров_".

```
// OnBeforeResponse
if (oSession.uriContains("https://myhost.ru"))
{
		oSession.utilDecodeResponse();
  	oSession.utilReplaceInResponse('Иванов','Петров');
}
```

### Задача 6: Заменить ресурс веб-портала на локальный ресурс

Заменим картинку веб-портала на картинку расположенною на локальном диске.

```
// OnBeforeResponse
if (oSession.uriContains("/Static/app/img/world.svg"))
{
		oSession.LoadResponseFromFile("c:/scripts/lang.png");	
}
```

### Задача 7: Изменение свойств HTML-объектов

Например, есть картинка с заданными размерами в HTML и нужно эти размеры изменить.

```
// OnBeforeResponse
oSession.utilReplaceInResponse('/Static/app/img/world.svg" height="15" width="15" style="height: 15px','/Static/app/img/world.svg" height="1" width="1" style="height: 1px');
```

### Задача 8: Скрыть элементы по className меняя css-файлы

В данном примере скрываем элементы зная их className в css-файле добавляя свойство "_visibility: hidden;_"

```
// OnBeforeResponse
oSession.utilDecodeResponse();
oSession.utilReplaceInResponse("#header_Area_Right {", "#header_Area_Right { visibility: hidden; ");
```

### Задача 9: Заставить страницу открываться в текущем окне

Пример: существует JavaScript, который открывает ссылку в новом окне. Нужно сделать чтобы ссылка открывалась в текущем окне.

```
// OnBeforeResponse
if (oSession.uriContains("myhost.ru") && oSession.uriContains(".js"))
{
		oSession.utilDecodeResponse();
		oSession.utilReplaceInResponse("window.open(url, '_blank', option);", "window.open(url);");
}
```

### Задача 10: Выполнение скриптов для определенных IP

В данном примере меняем текст "_Иванов_" на "_Петров_" только для IP = "_192.168.0.100_"

```
// OnBeforeResponse
if (oSession.clientIP == '192.168.0.100')
{
		oSession.utilDecodeResponse();
		oSession.utilReplaceInResponse('Иванов','Петров');
}
```

### Задача 11: Меняем css-стили портала

Css-файлы веб-портала можно сохранить на локальном диске, отредактировать и настроить скрипт отдавать стили с локального диска, а не с портала.

```
// OnBeforeResponse	
if (oSession.uriContains("/banner.css"))
{
		oSession.LoadResponseFromFile("c:/scripts/banner.css");	
}
```

### Задача 12: Запрет PUT-команды и аналогичных

Запрет команды по ее типу: "_PUT_", "_DELETE_", etc.

```
// OnBeforeRequest
if (oSession.HTTPMethodIs("PUT") && oSession.uriContains("https://myhost.ru/"))
{
		oSession.host = 'access.denied';
}
```

### Задача 13: Изменение тела POST-запроса

Изменить тело POST-запроса для заданного портала. При авторизации на данном портале вне зависимости от введенных пользователем данных на веб-портал отправятся данные из скрипта.

```
// OnBeforeRequest		
if (oSession.uriContains("https://myhost.ru/") && oSession.RequestMethod == "POST")
{
		oSession.utilSetRequestBody("username=xxx&password=yyy");	
}
```

### Задача 14: Меняем заголовки HTTP-пакета

Заголовки пакетов можно легко редактировать: удалять, добавлять, изменять.

```
// OnBeforeRequest

// Удалить заголовок с именем 'User-Agent'
oSession.oRequest.headers.Remove("User-Agent");

// Добавить заголовок 'xxx' со значением 'yyy'
oSession.oRequest.headers.Add("xxx", "yyy");

// Изменить значение заголовка с именем 'User-Agent' на значение 'xxx' 
oSession.oRequest.headers["User-Agent"] = "xxx";
```

### Задача 15: Меняем Cookie

Работа с Cookie: добавление, удаление, редактирование

```
// OnBeforeRequest - добавить в запрос Cookie
oSession.oRequest["Cookie"] = (oSession.oRequest["Cookie"] + ";mycookie=xxx");

// OnBeforeRequest - изменить значение Cookie 'JSESSIONID' на 'xxx'
oSession.oRequest['Cookie'] = oSession.oRequest['Cookie'].Replace("JSESSIONID=","ignoredCookie=") + ";JSESSIONID=xxx";

// OnBeforeRequest - удалить Cookie 'JSESSIONID'
oSession.oRequest['Cookie'] = oSession.oRequest['Cookie'].Replace("JSESSIONID=","ignoredCookie=");
```

```
// Всем удачи на полях сниффинга данных )
```
