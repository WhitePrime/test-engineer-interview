# Page 1



Обычно, слово Шпаргалка звучит как что-то запрещенное. В справочнике по программированию шпаргалка - это то, что используется для быстрой справки или для того, чтобы узнать что-то слишком конкретное без каких-либо подробностей, в основном коды, синтаксис или формулы. Таким образом, это руководство предназначено для быстрого ознакомления с некоторыми командами, кодами и синтаксисом Postman. Обратите внимание, что весь синтаксис и код, используемые здесь, соответствуют последнему стилю написания кодов/тестов в Postman.

Для более подробной информации вы можете посетить сайт: [https://learning.getpostman.com/docs/postman/scripts/test\_examples/](https://learning.getpostman.com/docs/postman/scripts/test\_examples/)

#### Переменные

Коды для работы с окружением и переменными

**Установка переменных**

_**Глобальные переменные**_

```
pm.globals.set('variable name', "value");
```

_**Локальная переменная**_

```
var variable_name = value;
```

_**Переменная среды**_

```
pm.environment.set('variable_name' , 'value');
```

**Получение переменных**

_**Глобальные переменные**_

```
pm.globals.get('variable_name');
```

_**Переменная среды**_

```
pm.environment.get('varibable_name');
```

_**Переменная данных**_

```
pm.iterationData.get('variable_name');
```

_**Локальная переменная**_

```
variable_name;
```

**Очистка переменных**

_**Глобальные переменные (только одна)**_

```
pm.globals.unset('variable_name');
```

_**Глобальные переменные (все)**_

```
pm.globals.clear();
```

_**Переменная среды (только одна)**_

```
pm.environment.unset('variable_name');
```

_**Переменная среды (все)**_

```
pm.environment.clear();
```

#### Ассерты

**Ответ**

Различные коды относящиеся к ответам запроса

_**Ответ содержит строку**_

```
pm.test("String found", function(){

pm.expect(pm.response.text()).to.include("string you want to search");

});
```

_**Тело ответа равно строке**_

```
pm.test("Body is equal to string", function(){

pm.response.to.have.body("string you want to check");
 
});
```

**Статус код**

Код, относящийся к статус кодам в Postman

_**Один статус код**_

```
pm.response.to.have.status(status_code);
```

_**Несколько статус кодов**_

```
pm.expect(pm.response.code).to.be.oneOf([status_code, status_code]);
```

**Время ответа**

```
pm.expect(pm.response.responseTime.to.be.below(time));
```

**Проверка значения JSON**

```
pm.test("Your_Test_Name", function(){

var jsonData = pm.response.json();

pm.expect(jsonData.value).to.eql(value);

});
```

**Заголовок содержит Content-Type**

```
pm.test("Your_Test_Name", function(){

pm.response.to.have.header("Content-Type");

});
```

**Ответ содержит куки sessionID**

```
pm.expect(pm.cookies.has('sessionID')).to.be.true;
```

**Тело ответа**

Код относящийся к телу ответа

_**Точное совпадение**_

```
pm.response.to.have.body("OK");
pm.response.to.have.body('{"success"=true}');
```

_**Частичное совпадение**_

```
pm.expect(pm.response.text()).to.include('ToolsQA');
```

**Отправить асинхронный запрос**

```
pm.sendRequest("https://postman-echo.com/get", function(err, response){

console.log(response.json());

});
```

#### JSON ответ

_**Распарсить тело**_

```
var jsonData = pm.response.json();
```

_**Проверить количество массивов в ответе**_

```
pm.test("ISBN Count", function () {
pm.expect(2).to.eql(pm.response.json().arrayName.length);
});
```

_**Проверить конкретное значение внутри массива**_

В этом примере проверяется конкретный номер ISBN среди всех книг, полученных в ответе, и возвращается значение true, если оно найдено.

```
pm.test("Test Name", function () {
var result;
for (var loop = 0; loop < pm.response.json().arrayName.length; loop++)
{
if (pm.response.json().arrayName[loop].arrayElement=== pm.variables.get("arrayElementValue")){
result=true;
break;
}
}
pm.expect(true).to.eql(result);
});
```

В двух приведенных выше примерах использовался Javascript, поскольку Postman Sandbox работает с javascript. Этот код не имеет конкретного отношения к Postman.

_**Проверить значение**_

```
pm.expect(jsonData.age).to.eql(value);

pm.expect(jsonData.name).to.eql("string");
```

_**Преобразование тела XML в объект JSON**_

```
var jsonObject = xml2Json(responseBody);
```

#### Рабочие процессы

_**Установка следующего запроса**_

```
postman.setNextRequest("Request Name");
```

_**Прекратить выполнение запроса**_

```
postman.setNextRequest(null);
```

#### Библеотека ассертов Chai

_**Найти число в массиве**_

```
pm.test(“Number included”, function(){
pm.expect([1,2,3]).to.include(3);
});
```

_**Проверить, пустой ли массив**_

```
pm.test(“Empty Array”, function(){
pm.expect([2]).to.be.an(‘array’).that.is.empty;
});
```

Переведено командой QApedia. Еще больше переведенных статей вы найдете на нашем [телеграм-канале](https://t.me/qa\_wiki).
