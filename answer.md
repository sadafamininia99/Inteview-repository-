# JavaScript Hard Interview Questions with Answers


---

## 1. Event Loop

```js
console.log('A');

setTimeout(() => console.log('B'), 0);

Promise.resolve()
  .then(() => console.log('C'))
  .then(() => console.log('D'));

console.log('E');
```

**خروجی:**

```
A
E
C
D
B
```

**توضیح:** synchronous → microtask (Promise) → macrotask (setTimeout).

---

## 2. Closure + Loop Trap

```js
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
```

**خروجی:**

```
3
3
3
```

**راه حل:**

* استفاده از `let i`
* IIFE: `(function(i){ setTimeout(..., i); })(i);`

---

## 3. this – Binding پیچیده

```js
const obj = {
  name: 'JS',
  getName() {
    return function () {
      return this.name;
    };
  },
};

console.log(obj.getName()());
```

**خروجی:** `undefined`
**راه حل:**

* Arrow function
* bind(this)
* ذخیره this در متغیر و استفاده در callback

---

## 4. Prototype Chain

```js
function A() {}
A.prototype.x = 1;

const a = new A();
A.prototype = { x: 2 };

console.log(a.x);
```

**خروجی:** `1`
**توضیح:** instance به prototype زمان ساخت اشاره دارد، تغییر بعدی روی آن تاثیر ندارد.

---

## 5. Hoisting عمیق

```js
console.log(foo);
var foo = 1;
function foo() {}
console.log(foo);
```

**خروجی:**

```
[Function: foo]
1
```

**توضیح:** function declaration قبل از var hoist می‌شود.

---

## 6. Reference vs Value

```js
let a = { n: 1 };
let b = a;

a.x = a = { n: 2 };

console.log(a);
console.log(b);
```

**خروجی:**

```
{ n: 2 }
{ n: 1, x: { n: 2 } }
```

**توضیح مرحله‌به‌مرحله:** سمت راست اول اجرا می‌شود، سپس سمت چپ.

---

## 7. Promise Error Handling

```js
Promise.resolve()
  .then(() => { throw new Error('err1'); })
  .catch(err => { return 'handled'; })
  .then(res => { throw new Error('err2'); })
  .catch(err => console.log(err.message));
```

**خروجی:** `err2`
**توضیح:** throw داخل then → reject → catch بعدی اجرا می‌شود.

---

## 8. == vs ===

```js
console.log([] == ![]);
console.log([] == []);
console.log(![] == []);
```

**خروجی:**

```
true
false
true
```

**توضیح:** تبدیل نوع‌ها و reference comparison.

---

## 9. Memory Leak

```js
function heavy() {
  const big = new Array(1e6).fill('*');
  return () => big.length;
}

const fn = heavy();
```

**توضیح:** closure نگه داشتن `big` باعث می‌شود تا زمانی که `fn` موجود است حافظه آزاد نشود.

---

## 10. Async/Await + Race Condition

```js
let result = 0;

async function inc() {
  result += await Promise.resolve(1);
}

inc();
inc();

setTimeout(() => console.log(result), 0);
```

**خروجی:** `1` (ممکن است race condition رخ دهد)
**توضیح:** دو async همزمان اجرا می‌شوند، race condition وجود دارد و ممکن است مقدار نهایی متفاوت باشد.

---

