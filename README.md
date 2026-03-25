# Лабораторная работа №2: Реализация базовых методов работы с массивами

## 🎯 Цель работы
Изучение принципов реализации базовых методов работы с массивами (`forEach`, `map`, `filter`, `find`, `some`, `every`, `reduce`) с использованием функций обратного вызова (колбэков). Закрепление навыков написания функций с корректным возвратом результатов и обработкой граничных случаев без использования встроенных методов итерации массивов.

## ⚠️ Условия и ограничения
- **Запрещено** использовать встроенные методы массивов: `Array.prototype.forEach`, `map`, `filter`, `find`, `some`, `every`, `reduce`.
- **Разрешено** использовать: цикл `for`, свойство `length`, обращение к элементам по индексу, метод `push` для формирования новых массивов.

---

## 💻 Реализованные функции и примеры использования

### 1. Вывод массива в консоль
Две функции для подробного и краткого вывода элементов массива.

```javascript
function printArray(arrToPrint) {
  for (let i = 0; i < arrToPrint.length; i++) {
    console.log(`Element ${i}: value ${arrToPrint[i]}`);
  }
}
2. forEach(array, callback)

Выполняет переданную функцию для каждого элемента массива. Ничего не возвращает (undefined).

JavaScript
function forEach(arrToIterate, callback) {
  for (let i = 0; i < arrToIterate.length; i++) {
    callback(arrToIterate[i], i, arrToIterate);
  }
}

// Пример:
forEach(['Али', 'Берик'], (name, index) => console.log(`${index}: ${name}`));
3. map(array, callback)

Создает новый массив с результатами вызова указанной функции для каждого элемента.

JavaScript
function map(arrToMap, callback) {
  const result = [];
  for (let i = 0; i < arrToMap.length; i++) {
    result.push(callback(arrToMap[i], i, arrToMap));
  }
  return result;
}
4. filter(array, callback)

Создает новый массив со всеми элементами, прошедшими проверку, заданную в передаваемой функции.

JavaScript
function filter(arrToFilter, callback) {
  const result = [];
  for (let i = 0; i < arrToFilter.length; i++) {
    if (callback(arrToFilter[i], i, arrToFilter)) {
      result.push(arrToFilter[i]);
    }
  }
  return result;
}
5. find(array, callback)

Возвращает первый элемент в массиве, удовлетворяющий условию переданной проверяющей функции.

JavaScript
function find(arrToSearch, callback) {
  for (let i = 0; i < arrToSearch.length; i++) {
    if (callback(arrToSearch[i], i, arrToSearch)) {
      return arrToSearch[i];
    }
  }
  return undefined;
}
6. some(array, callback) и every(array, callback)

Проверяют, удовлетворяет ли хотя бы один (some) или все (every) элементы массива условию.

JavaScript
function some(arrToCheckSome, callback) {
  for (let i = 0; i < arrToCheckSome.length; i++) {
    if (callback(arrToCheckSome[i], i, arrToCheckSome)) return true;
  }
  return false;
}

function every(arrToCheckEvery, callback) {
  for (let i = 0; i < arrToCheckEvery.length; i++) {
    if (!callback(arrToCheckEvery[i], i, arrToCheckEvery)) return false;
  }
  return true;
}
7. reduce(array, callback, initialValue)

Применяет функцию к аккумулятору и каждому значению массива, сводя его к одному значению.

JavaScript
function reduce(arrToReduce, callback, initialValue) {
  if (arrToReduce.length === 0 && initialValue === undefined) return undefined;

  let accumulator = initialValue !== undefined ? initialValue : arrToReduce[0];
  let startIndex = initialValue !== undefined ? 0 : 1;

  for (let i = startIndex; i < arrToReduce.length; i++) {
    accumulator = callback(accumulator, arrToReduce[i], i, arrToReduce);
  }
  return accumulator;
}
📝 Контрольные вопросы
Преимущества колбэков: Разделение логики обхода и обработки, переиспользуемость, декларативность кода.

Возможные проблемы: Потеря контекста this (решается стрелочными функциями) и мутация исходных данных (решается написанием чистых функций).

Реализация без встроенных методов: Использование цикла for с досрочным выходом (return) для оптимизации методов find, some и every.
