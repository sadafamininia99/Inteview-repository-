
# JavaScript Hard Interview Questions

۱۰ سؤال **سخت و مصاحبه‌ای جاوااسکریپت** (سطح میانی رو به ارشد). هر سؤال طوری طراحی شده که عمق درک مفاهیم را بسنجد، نه حفظیات.

---

## 1. Event Loop – خروجی چیست و چرا؟

```js
console.log('A');

setTimeout(() => console.log('B'), 0);

Promise.resolve()
  .then(() => console.log('C'))
  .then(() => console.log('D'));

console.log('E');
```

**سؤال:** ترتیب خروجی دقیق چیست؟ microtask و macrotask چه نقشی دارند؟

---

## 2. Closure + Loop Trap

```js
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
```

**سؤال:** خروجی چیست؟ چرا؟ دو راه حرفه‌ای برای اصلاح آن بگو (بدون تغییر منطق loop).

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

**سؤال:** خروجی چیست؟ حداقل ۳ راه مختلف برای اصلاح رفتار `this` نام ببر.

---

## 4. Prototype Chain

```js
function A() {}
A.prototype.x = 1;

const a = new A();
A.prototype = { x: 2 };

console.log(a.x);
```

**سؤال:** خروجی چیست؟ چرا تغییر prototype بعد از ساخت instance اثر ندارد؟

---

## 5. Hoisting عمیق

```js
console.log(foo);

var foo = 1;

function foo() {}

console.log(foo);
```

**سؤال:** خروجی هر دو `console.log` چیست و چرا؟

---

## 6. Reference vs Value

```js
let a = { n: 1 };
let b = a;

a.x = a = { n: 2 };

console.log(a);
console.log(b);
```

**سؤال:** خروجی چیست؟ ترتیب ارزیابی این خط را مرحله‌به‌مرحله توضیح بده.

---

## 7. Promise Error Handling

```js
Promise.resolve()
  .then(() => {
    throw new Error('err1');
  })
  .catch(err => {
    return 'handled';
  })
  .then(res => {
    throw new Error('err2');
  })
  .catch(err => console.log(err.message));
```

**سؤال:** خروجی چیست؟ تفاوت `throw` و `return Promise.reject` چیست؟

---

## 8. == vs === (دام مصاحبه)

```js
console.log([] == ![]);
console.log([] == []);
console.log(![] == []);
```

**سؤال:** خروجی‌ها چیست؟ تبدیل نوع‌ها را دقیق توضیح بده.

---

## 9. Memory Leak

```js
function heavy() {
  const big = new Array(1e6).fill('*');
  return () => big.length;
}

const fn = heavy();
```

**سؤال:** آیا این کد می‌تواند باعث memory leak شود؟ چرا؟ چه زمانی خطرناک است؟

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

**سؤال:** خروجی چیست؟ آیا race condition داریم؟ چرا؟

---

> این سوالات برای تمرین قبل از مصاحبه‌های سطح میانی تا ارشد توصیه می‌شوند و روی درک عمیق جاوااسکریپت تمرکز دارند.
