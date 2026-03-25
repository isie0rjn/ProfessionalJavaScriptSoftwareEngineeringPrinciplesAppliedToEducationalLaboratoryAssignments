# Лабораторная работа №2: Реализация базовых методов работы с массивами

## 🎯 Цель работы
Изучение принципов реализации базовых методов работы с массивами (`forEach`, `map`, `filter`, `find`, `some`, `every`, `reduce`) с использованием функций обратного вызова (колбэков). Закрепление навыков написания функций с корректным возвратом результатов и обработкой граничных случаев без использования встроенных методов итерации массивов.

## ⚠️ Условия и ограничения
- **Запрещено** использовать встроенные методы массивов: `Array.prototype.forEach`, `map`, `filter`, `find`, `some`, `every`, `reduce`.
- **Разрешено** использовать: цикл `for`, свойство `length`, обращение к элементам по индексу, метод `push` для формирования новых массивов.

---

## 💻 Реализованные функции (JS)
```javascript
// 1. Вывод массива в консоль (подробный)
function printArray(arrToPrint) {
  for (let i = 0; i < arrToPrint.length; i++) {
    console.log(`Element ${i}: value ${arrToPrint[i]}`);
  }
}

// 1.1 Вывод массива в консоль (краткий)
function printArrayShort(arrToPrintShort) {
  for (let i = 0; i < arrToPrintShort.length; i++) {
    console.log(`${i}: ${arrToPrintShort[i]}`);
  }
}

// 2. forEach(array, callback)
// Выполняет callback для каждого элемента массива, ничего не возвращает
function forEach(arrToIterate, callback) {
  for (let i = 0; i < arrToIterate.length; i++) {
    callback(arrToIterate[i], i, arrToIterate);
  }
}

// 3. map(array, callback)
// Создает новый массив с результатами вызова callback для каждого элемента
function map(arrToMap, callback) {
  const result = [];
  for (let i = 0; i < arrToMap.length; i++) {
    result.push(callback(arrToMap[i], i, arrToMap));
  }
  return result;
}

// 4. filter(array, callback)
// Возвращает новый массив с элементами, прошедшими проверку
function filter(arrToFilter, callback) {
  const result = [];
  for (let i = 0; i < arrToFilter.length; i++) {
    if (callback(arrToFilter[i], i, arrToFilter)) {
      result.push(arrToFilter[i]);
    }
  }
  return result;
}

// 5. find(array, callback)
// Возвращает первый элемент, удовлетворяющий условию, или undefined
function find(arrToSearch, callback) {
  for (let i = 0; i < arrToSearch.length; i++) {
    if (callback(arrToSearch[i], i, arrToSearch)) {
      return arrToSearch[i];
    }
  }
  return undefined;
}

// 6. some(array, callback)
// Проверяет, есть ли хотя бы один элемент, удовлетворяющий условию
function some(arrToCheckSome, callback) {
  for (let i = 0; i < arrToCheckSome.length; i++) {
    if (callback(arrToCheckSome[i], i, arrToCheckSome)) {
      return true;
    }
  }
  return false;
}

// 7. every(array, callback)
// Проверяет, удовлетворяют ли все элементы условию
function every(arrToCheckEvery, callback) {
  for (let i = 0; i < arrToCheckEvery.length; i++) {
    if (!callback(arrToCheckEvery[i], i, arrToCheckEvery)) {
      return false;
    }
  }
  return true;
}

// 8. reduce(array, callback, initialValue)
// Сводит массив к одному значению, используя аккумулятор
function reduce(arrToReduce, callback, initialValue) {
  if (arrToReduce.length === 0 && initialValue === undefined) {
    return undefined;
  }

  let accumulator = initialValue !== undefined ? initialValue : arrToReduce[0];
  let startIndex = initialValue !== undefined ? 0 : 1;

  for (let i = startIndex; i < arrToReduce.length; i++) {
    accumulator = callback(accumulator, arrToReduce[i], i, arrToReduce);
  }

  return accumulator;
}
```

## 📝 Контрольные вопросы
- Преимущества колбэков: разделение логики обхода и обработки, переиспользуемость, декларативность кода.
- Возможные проблемы: потеря контекста `this` (решается стрелочными функциями) и мутация исходных данных (решается написанием чистых функций).
- Реализация без встроенных методов: использование цикла `for` с досрочным выходом (`return`) для оптимизации методов `find`, `some` и `every`.
