# Лабораторная работа №2: Реализация базовых методов работы с массивами

## 🎯 Цель работы
Изучение принципов реализации базовых методов работы с массивами (`forEach`, `map`, `filter`, `find`, `some`, `every`, `reduce`) с использованием функций обратного вызова (колбэков). Закрепление навыков написания функций с корректным возвратом результатов и обработкой граничных случаев без использования встроенных методов итерации массивов.

## ⚠️ Условия и ограничения
- **Запрещено** использовать встроенные методы массивов: `Array.prototype.forEach`, `map`, `filter`, `find`, `some`, `every`, `reduce`.
- **Разрешено** использовать: цикл `for`, свойство `length`, обращение к элементам по индексу, метод `push` для формирования новых массивов.

---

## 💻 Реализованные функции (JS)
```javascript
/**
 * Вывод массива в консоль (подробный формат)
 * @param {Array<*>} arrToPrint - Массив для вывода
 * @returns {void}
 */
function printArray(arrToPrint) {
  for (let i = 0; i < arrToPrint.length; i++) {
    console.log(`Element ${i}: value ${arrToPrint[i]}`);
  }
}

/**
 * Вывод массива в консоль (краткий формат)
 * @param {Array<*>} arrToPrintShort - Массив для вывода
 * @returns {void}
 */
function printArrayShort(arrToPrintShort) {
  for (let i = 0; i < arrToPrintShort.length; i++) {
    console.log(`${i}: ${arrToPrintShort[i]}`);
  }
}

/**
 * Выполняет callback для каждого элемента массива
 * @template T
 * @param {Array<T>} arrToIterate - Исходный массив
 * @param {(element: T, index: number, array: Array<T>) => void} callback - Функция обратного вызова
 * @returns {void}
 */
function forEach(arrToIterate, callback) {
  for (let i = 0; i < arrToIterate.length; i++) {
    callback(arrToIterate[i], i, arrToIterate);
  }
}

/**
 * Создает новый массив с результатами вызова callback
 * @template T, R
 * @param {Array<T>} arrToMap - Исходный массив
 * @param {(element: T, index: number, array: Array<T>) => R} callback - Функция преобразования
 * @returns {Array<R>} Новый массив
 */
function map(arrToMap, callback) {
  const result = [];
  for (let i = 0; i < arrToMap.length; i++) {
    result.push(callback(arrToMap[i], i, arrToMap));
  }
  return result;
}

/**
 * Возвращает новый массив с элементами, прошедшими проверку callback
 * @template T
 * @param {Array<T>} arrToFilter - Исходный массив
 * @param {(element: T, index: number, array: Array<T>) => boolean} callback - Условие фильтрации
 * @returns {Array<T>} Отфильтрованный массив
 */
function filter(arrToFilter, callback) {
  const result = [];
  for (let i = 0; i < arrToFilter.length; i++) {
    if (callback(arrToFilter[i], i, arrToFilter)) {
      result.push(arrToFilter[i]);
    }
  }
  return result;
}

/**
 * Возвращает первый элемент, удовлетворяющий условию callback
 * @template T
 * @param {Array<T>} arrToSearch - Исходный массив
 * @param {(element: T, index: number, array: Array<T>) => boolean} callback - Условие поиска
 * @returns {T|undefined} Найденный элемент или undefined
 */
function find(arrToSearch, callback) {
  for (let i = 0; i < arrToSearch.length; i++) {
    if (callback(arrToSearch[i], i, arrToSearch)) {
      return arrToSearch[i];
    }
  }
  return undefined;
}

/**
 * Проверяет, есть ли хотя бы один элемент, удовлетворяющий условию callback
 * @template T
 * @param {Array<T>} arrToCheckSome - Исходный массив
 * @param {(element: T, index: number, array: Array<T>) => boolean} callback - Условие проверки
 * @returns {boolean} true, если найден хотя бы один подходящий элемент
 */
function some(arrToCheckSome, callback) {
  for (let i = 0; i < arrToCheckSome.length; i++) {
    if (callback(arrToCheckSome[i], i, arrToCheckSome)) {
      return true;
    }
  }
  return false;
}

/**
 * Проверяет, удовлетворяют ли все элементы массива условию callback
 * @template T
 * @param {Array<T>} arrToCheckEvery - Исходный массив
 * @param {(element: T, index: number, array: Array<T>) => boolean} callback - Условие проверки
 * @returns {boolean} true, если все элементы прошли проверку
 */
function every(arrToCheckEvery, callback) {
  for (let i = 0; i < arrToCheckEvery.length; i++) {
    if (!callback(arrToCheckEvery[i], i, arrToCheckEvery)) {
      return false;
    }
  }
  return true;
}

/**
 * Сводит массив к одному значению, используя аккумулятор
 * @template T, R
 * @param {Array<T>} arrToReduce - Исходный массив
 * @param {(accumulator: R, element: T, index: number, array: Array<T>) => R} callback - Редьюсер
 * @param {R} [initialValue] - Начальное значение аккумулятора
 * @returns {R|undefined} Итоговое значение или undefined для пустого массива без initialValue
 */
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
