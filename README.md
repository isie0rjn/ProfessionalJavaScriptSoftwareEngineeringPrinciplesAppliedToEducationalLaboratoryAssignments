/**
 * 1.1. Вывод массива в консоль (подробный формат)
 * @param {Array} arrToPrint - Исходный массив для подробного вывода
 */
function printArray(arrToPrint) {
  for (let i = 0; i < arrToPrint.length; i++) {
    console.log(`Element ${i}: value ${arrToPrint[i]}`);
  }
}

console.log("--- 1.1 printArray ---");
const fruitsArray = ['Яблоко', 'Банан', 'Вишня'];
printArray(fruitsArray);
// Ожидаемый вывод: 
// Element 0: value Яблоко
// Element 1: value Банан
// Element 2: value Вишня


/**
 * 1.1. Вывод массива в консоль (краткий формат)
 * @param {Array} arrToPrintShort - Исходный массив для краткого вывода
 */
function printArray1(arrToPrintShort) {
  for (let i = 0; i < arrToPrintShort.length; i++) {
    console.log(`${i}:  ${arrToPrintShort[i]}`);
  }
}

console.log("\n--- 1.1 printArray1 ---");
const techArray = ['HTML', 'CSS', 'JS'];
printArray1(techArray);
// Ожидаемый вывод: 
// 0:  HTML
// 1:  CSS
// 2:  JS


/**
 * 1.2. Выполняет переданный колбэк для каждого элемента массива
 * @param {Array} arrToIterate - Исходный массив для обхода
 * @param {Function} callback - Функция обратного вызова callback(element, index, array)
 * @returns {undefined}
 */
function forEach(arrToIterate, callback) {
  for (let i = 0; i < arrToIterate.length; i++) {
    callback(arrToIterate[i], i, arrToIterate);
  }
}

console.log("\n--- 1.2 forEach ---");
const namesArray = ['Али', 'Берик', 'Серик'];
forEach(namesArray, (name, index) => {
  console.log(`Студент №${index + 1}: ${name}`);
});
// Ожидаемый вывод: Студент №1: Али, Студент №2: Берик, Студент №3: Серик


/**
 * 2. Создает новый массив с результатами вызова колбэка для каждого элемента
 * @param {Array} arrToMap - Исходный массив для преобразования
 * @param {Function} callback - Функция обратного вызова callback(element, index, array)
 * @returns {Array} Новый массив
 */
function map(arrToMap, callback) {
  const result = [];
  for (let i = 0; i < arrToMap.length; i++) {
    result.push(callback(arrToMap[i], i, arrToMap));
  }
  return result;
}

console.log("\n--- 2. map ---");
const numbersArray = [1, 2, 3, 4];
const squaredNumbers = map(numbersArray, (num) => num * num);
console.log("Квадраты чисел:", squaredNumbers); 
// Ожидаемый вывод: Квадраты чисел: [1, 4, 9, 16]


/**
 * 3. Создает новый массив со всеми элементами, прошедшими проверку в колбэке
 * @param {Array} arrToFilter - Исходный массив для фильтрации
 * @param {Function} callback - Функция проверки, должна возвращать boolean
 * @returns {Array} Отфильтрованный массив
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

console.log("\n--- 3. filter ---");
const mixedNumbersArray = [10, 15, 20, 25, 30];
const evenNumbersOnly = filter(mixedNumbersArray, (num) => num % 2 === 0);
console.log("Только четные:", evenNumbersOnly); 
// Ожидаемый вывод: Только четные: [10, 20, 30]


/**
 * 4. Возвращает первый элемент массива, удовлетворяющий условию
 * @param {Array} arrToSearch - Исходный массив для поиска
 * @param {Function} callback - Функция проверки, должна возвращать boolean
 * @returns {*} Найденный элемент или undefined
 */
function find(arrToSearch, callback) {
  for (let i = 0; i < arrToSearch.length; i++) {
    if (callback(arrToSearch[i], i, arrToSearch)) {
      return arrToSearch[i];
    }
  }
  return undefined;
}

console.log("\n--- 4. find ---");
const usersArray = [
  { id: 1, role: 'user' },
  { id: 2, role: 'admin' },
  { id: 3, role: 'user' }
];
const firstAdmin = find(usersArray, (user) => user.role === 'admin');
console.log("Первый админ:", firstAdmin); 
// Ожидаемый вывод: Первый админ: { id: 2, role: 'admin' }


/**
 * 5. Проверяет, удовлетворяет ли хотя бы один элемент условию
 * @param {Array} arrToCheckSome - Исходный массив
 * @param {Function} callback - Функция проверки, должна возвращать boolean
 * @returns {boolean} true, если найден хотя бы один подходящий, иначе false
 */
function some(arrToCheckSome, callback) {
  for (let i = 0; i < arrToCheckSome.length; i++) {
    if (callback(arrToCheckSome[i], i, arrToCheckSome)) {
      return true;
    }
  }
  return false;
}

console.log("\n--- 5. some ---");
const temperaturesArray = [-5, -2, 0, 3, -1];
const hasPositiveTemp = some(temperaturesArray, (temp) => temp > 0);
console.log("Есть ли плюсовая температура?", hasPositiveTemp); 
// Ожидаемый вывод: Есть ли плюсовая температура? true


/**
 * 6. Проверяет, удовлетворяют ли все элементы массива условию
 * @param {Array} arrToCheckEvery - Исходный массив
 * @param {Function} callback - Функция проверки, должна возвращать boolean
 * @returns {boolean} true, если все проходят проверку, иначе false
 */
function every(arrToCheckEvery, callback) {
  for (let i = 0; i < arrToCheckEvery.length; i++) {
    if (!callback(arrToCheckEvery[i], i, arrToCheckEvery)) {
      return false;
    }
  }
  return true;
}

console.log("\n--- 6. every ---");
const agesArray = [21, 25, 30, 18];
const allAdults = every(agesArray, (age) => age >= 18);
console.log("Все ли совершеннолетние?", allAdults); 
// Ожидаемый вывод: Все ли совершеннолетние? true


/**
 * 7. Последовательно обрабатывает элементы, накапливая результат
 * @param {Array} arrToReduce - Исходный массив
 * @param {Function} callback - Функция callback(accumulator, element, index, array)
 * @param {*} [initialValue] - Начальное значение
 * @returns {*} Итоговое значение
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

console.log("\n--- 7. reduce ---");
const pricesArray = [1000, 2500, 500];
const totalPrice = reduce(pricesArray, (acc, price) => acc + price, 0);
console.log("Итоговая сумма:", totalPrice); 
// Ожидаемый вывод: Итоговая сумма: 4000
