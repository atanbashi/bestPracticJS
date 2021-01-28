# Best Practice JavaScript.

### 1. Ограничение доступа к переменным и свойствам. 

Задача состоит в том, чтобы сократить время доступа к переменным и свойствам объектов в приложениях.
Причина заключается в том, что при каждом обращении процессору необходимо получить доступ к элементу в памяти, чтобы вычислить его результаты. 
Следовательно, это действие нужно выполнять как можно реже.

`плохой пример`
``` js 
for (let i = 0; i < arr.length; i++) {}
```
`хороший пример`
``` js
let length = arr.length;
for (let i = 0; i < length; i++) {}
```
Таким образом, на arr.length ссылаются один раз за цикл, а не обращаются к нему на каждой итерации. 

### 2. Не объявляйте ненужные переменные

При каждом объявлении переменных, браузер должен выделить пространство памяти для них. Следовательно, чтобы уменьшить использование памяти, необходимо сократить количество объявления переменных.

`плохой пример`
``` js
const foo = document.querySelector('#foo');
const p = foo.querySelector('p');
p.textContent = 'foo';
```
`хороший пример`
``` js
document.querySelector('#foo p').textContent = 'foo';
```

### 4. Отложенная загрузка сценариев

Загрузка файлов JavaScript — дорогостоящая операция. Браузер должен загрузить файл, проанализировать содержимое, а затем преобразовать его в машинный код и запустить.
Браузер загружает один файл построчно, не допуская выполнения других операций. Следовательно, нам нужно отложить эту операцию. Для этого разместите тег script в конце кода.

### 5. Простые и понятные имена переменных, функций и классов.

Названия функций должны быть краткими и содержательными.

`плохой пример`
``` js
 const soVeryUselessLongBirthdayVariable;
 function isOverEighteen();
 ```
`хороший пример`
``` js
const birthday;
function isAdult();
```

### 6. Избегайте частого использования глобальных переменных и функций.

В JavaScript всё запускается в одной и той же области видимости. И это реальная проблема, потому что некоторые данные могут быть случайно изменены в одной части кода, которая повлияет на другой код, использующий эти же данные.К счастью, начиная с ES6, JavaScript имеет несколько возможностей для решения этой проблемы. Одна из них - использование модулей. С модулями, только то, что мы явно экспортируем, доступно для использования другими модулями.
Также должен быть включен строгий режим JavaScript, чтобы предотвратить случайное объявление глобальных переменных.

### 7. Переменные и константы должны быть наверху

Объявление переменных и вверху файла делает код чище. Также это помешает случайно ссылаться на переменные, объявленные с let или const до того, как они будут определены.
Если strict mode выключен, мы также избегаем создания глобальных переменных и случайного повторного объявления. Большинство текстовых редакторов отлавливает повторные объявления, но вероятность пропустить их остается.

### 8. Избегайте мысленного сопоставления

Не заставляйте людей запоминать контекст переменной. Переменные следует понимать даже тогда, когда читателю не удалось проследить всю историю их возникновения.

`плохой пример`
``` js
const names = ["John", "Jane", "Joseph"];
names.forEach(v => {
 doStuff();
 doSomethingExtra();
 // ...
 // ...
 // ...
 // What is this 'v' for?
 dispatch(v);
});
```
`хороший пример`
``` js
const names = ["John", "Jane", "Joseph"];
names.forEach(name => {
 doStuff();
 doSomethingExtra();
 // ...
 // ...
 // ...
 // 'name' makes sense now
 dispatch(name);
});
```

### 9. Используйте строгую проверку типа

Используйте === вместо == . Это поможет избежать всяких ненужных проблем в дальнейшем. Если не делать проверки должным образом, то это может существенно повлиять на логику программы.

``` js
 0 == false // true
 0 === false // false
 2 == "2" // true
 2 === "2" // false
 ```
 
 ### 10. По-минимуму количество параметров функции
 
 В идеале следует избегать большого количества параметров. Уменьшение количества параметров функции облегчило бы ее тестирование.

Один или два аргумента - идеальный вариант, а три следует по возможности избегать. Все, что больше этого, должно быть сведено воедино. Обычно, если у вас более двух аргументов, то ваша функция пытается сделать слишком много. В тех случаях, когда это не так, в большинстве случаев в качестве аргумента будет достаточно высокоуровненового объекта.

`плохой пример`
``` js
function createMenu(title, body, buttonText, cancellable) {
 // ...
}
createMenu("Foo", "Bar", "Baz", true);
```
`хороший пример`
``` js
function createMenu({ title, body, buttonText, cancellable }) {
 // ...
}
createMenu({
 title: "Foo",
 body: "Bar",
 buttonText: "Baz",
 cancellable: true
});
```
