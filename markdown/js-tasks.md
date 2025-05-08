# Типовые задачи собеседования по JavaScript: "Что выведет код?"

---

## 1. Пример с hoisting

```js
console.log(a);
var a = 5;
```

**Ответ:** `undefined`

**Пояснение:**
Объявление `var a` поднимается наверх, но не инициализация. Код становится:

```js
var a;
console.log(a); // undefined
a = 5;
```

---

## 2. Замыкание в цикле

```js
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 0);
}
```

**Ответ:** `3 3 3`

**Пояснение:**
`var` не создаёт блочную область, поэтому все функции замыкают одно и то же значение `i`, которое после цикла равно 3.

---

## 3. let в цикле

```js
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 0);
}
```

**Ответ:** `0 1 2`

**Пояснение:**
`let` создаёт новое значение `i` на каждой итерации — каждая функция замыкает своё.

---

## 4. typeof null

```js
console.log(typeof null);
```

**Ответ:** `'object'`

**Пояснение:**
Историческая ошибка в спецификации JS, сохранена для совместимости.

---

## 5. Сравнение объектов

```js
console.log({} === {});
```

**Ответ:** `false`

**Пояснение:**
Объекты сравниваются по ссылке. Это два разных объекта в памяти.

---

## 6. Преобразование типов

```js
console.log([] + {});
console.log({} + []);
```

**Ответ:**

```
"[object Object]"
0
```

**Пояснение:**

* `[] + {}` → строка: `'' + '[object Object]'`
* `{}` + `[]` без скобок интерпретируется как блок кода и выражение `+[]` → `0`

---

## 7. this в обычной и стрелочной функции

```js
const obj = {
  value: 42,
  getValue: function () {
    return this.value;
  },
  getValueArrow: () => {
    return this.value;
  }
};

console.log(obj.getValue());
console.log(obj.getValueArrow());
```

**Ответ:** `42` и `undefined`

**Пояснение:**

* `getValue` — обычная функция, `this` ссылается на `obj`
* `getValueArrow` — стрелочная, берёт `this` из внешнего контекста (обычно `window` или `undefined` в strict)

---

## 8. Очередь событий (event loop)

```js
console.log('start');
setTimeout(() => console.log('timeout'));
Promise.resolve().then(() => console.log('promise'));
console.log('end');
```

**Ответ:**

```
start
end
promise
timeout
```

**Пояснение:**

* Сначала выполняется синхронный код
* Затем микротаски (Promise)
* Потом макротаски (setTimeout)

---

## 9. delete и свойства объекта

```js
const user = { name: 'Alice' };
delete user.name;
console.log(user.name);
```

**Ответ:** `undefined`

**Пояснение:**
`delete` удаляет свойство объекта. В данном случае — `name`.

---

## 10. Порядок приведения типов

```js
console.log('5' - 2);
console.log('5' + 2);
```

**Ответ:**

```
3
"52"
```

**Пояснение:**

* `'-'` приводит оба операнда к числам
* `'+'` с участием строки приводит к конкатенации

---

