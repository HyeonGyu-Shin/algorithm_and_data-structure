# Q. ํ

---

### ํ

<br/>

![Untitled](../queue/assets/Untitled.png)

๐ ํ๋ โ๋๊ธฐ ํ๋ ฌโ์ด๋ผ๊ณ  ๋ถ๋ฆฐ๋ค. ๋ง ๊ทธ๋๋ก ์ค์ ์๋ ๊ฒ์ ์๊ฐํ๋ฉด ๋๋ค.์ฆ, ๋จผ์  ์จ ์ฌ๋์ด ๋จผ์  ๋๊ฐ๋ค๊ณ  ์๊ฐํ๋ฉด ๋๋ค.
<br/>
<br/>

![Untitled](../queue/assets/Untitled%201.png)
<br/>

๐ ํ์ ๋ฐ์ดํฐ๋ฅผ ์ถ๊ฐํ๋ ๊ฒ์ enqueue(์ํ)๋ผ๊ณ  ํ๋ค. enqueue๋ฅผ ํ๋ฉด ๋ฐ์ดํฐ์ ๊ฐ์ฅ ๋ค์ ๋ฐ์ดํฐ๊ฐ ์ถ๊ฐ๋๋ค.
<br/>
<br/>

![Untitled](../queue/assets/Untitled%202.png)
<br/>
<br/>

๐ ํ์์ ๋ฐ์ดํฐ๋ฅผ ๊บผ๋ด๋ ๊ฒ์ dequeue(๋ํ)๋ผ๊ณ  ํ๋ค. dequeue๋ฅผ ํ๋ฉด ํ์ ๊ฐ์ฅ ๋(์ ์ผ ์ค๋๋ ๋ฐ์ดํฐ)์์ ๋ฐ์ดํฐ๋ฅผ ๋นผ๋ธ๋ค.
<br/>
<br/>

๐ ์ด์  ์ฝ๋๋ก ์์๋ณด์! ์ด๋ฒ์๋ ์ ๋ฒ๊ณผ ๋ฌ๋ฆฌ es6์ ํด๋์ค๋ฅผ ์ด์ฉํ์ฌ ๊ตฌํํด๋ณด๋๋ก ํ๊ฒ ๋ค.
<br/>
<br/>

```jsx
class Queue {
  constructor() {
    this.head = null;
    this.rear = null;
    this.count = 0;
  }
}

class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}
```

๐ย  es6์ ํด๋์ค๋ฅผ ์ด์ฉํ์ฌ Queue๋ฅผ ๊ตฌํํ๋ค. ์ด์  ๋ฉ์๋๋ฅผ ์์ฑํด๋ณด์.

```jsx
enqueue(data) {
    const node = new Node(data);
    if (!this.head) {
      this.head = node;   ... 1
    } else {
      this.rear.next = node;   ... 3
    }
    this.rear = node;   ... 2
    this.count++;

    return this.count;
  }
.
.
.

const queue = new Queue();
queue.enqueue(1);
queue.enqueue(2);
console.log(queue);

=========================

Queue {
  head: Node { data: 1, next: Node { data: 2, next: null } },
  rear: Node { data: 2, next: null },
  count: 2
}
```

<br/>
<br/>

๐ย  queue์ ๋ฐ์ดํฐ๋ฅผ ๋ฃ์ด์ฃผ๋ enqueue ๋ฉ์๋์ด๋ค.

1. this.head๊ฐ false์ธ ๊ฒฝ์ฐ๋ ํ๊ฐ ๋น์์ ๊ฒฝ์ฐ์ด๋ค. ์ด๋๋ ํ์ ๋งจ ์ฒ์์ ๊ฐ๋ฆฌํค๋ this.head์
   ์์ฑํ node๋ฅผ ๋ฃ์ด์ค๋ค.

2. ํ์ ๋งจ ๋ค๋ฅผ ๊ฐ๋ฆฌํค๋ this.rear์ ์์ฑํ node๋ฅผ ๋ฃ์ด์ค๋ค. ๊ทธ ๊ฒฐ๊ณผ this.rear๋ ์์ฑํ ๋ธ๋๋ง ๊ฐ๋ฆฌํค๊ฒ ๋๋ค.

3. ํ์ ๋ฐ์ดํฐ๊ฐ ์กด์ฌํ๋ ๊ฒฝ์ฐ ํ์ ๋งจ ๋ค์ธ this.rear์ next ์์ฑ์ ์์ฑํ ๋ธ๋๋ฅผ ๋ฃ๋๋ค. ์ด๋, this.head์ this.rear๋ ๊ฐ์ ๋ธ๋๋ฅผ ์ฐธ์กฐํ๊ณ  ์๊ธฐ ๋๋ฌธ์ this.head ๋ํ ๊ฐฑ์ ์ด ๋๋ค.
   <br/>

```jsx
dequeue() {
    let data;
    if (!this.head) {   ... 1
      return console.log(`ํ๊ฐ ๋น์์ต๋๋ค.`);
    }
    data = this.head.data;   ... 2
    this.head = this.head.next;   ... 3
    this.count--;
    return data;
  }
.
.
.

const queue = new Queue();
queue.enqueue(1);
queue.enqueue(2);
queue.enqueue(3);
queue.dequeue();
console.log(queue);

===================

Queue {
  head: Node { data: 2, next: Node { data: 3, next: null } },
  rear: Node { data: 3, next: null },
  count: 2
}
```

<br/>

๐ย  ํ์ ๋งจ ์ฒ์์ ์๋ ๋ฐ์ดํฐ๋ฅผ ๋ฐํํด์ฃผ๋ dequeue ๋ฉ์๋์ด๋ค.

1. this.head๊ฐ ๋น์๋ค๋ ๊ฑด ํ๊ฐ ๋น์๋ค๋ ๋ป์ด๊ธฐ ๋๋ฌธ์ ๋ฐํํ  ๊ฐ์ด ์๋ค. ๋ฐ๋ก return์ ํ์ฌ ์ข๋ฃ์ํค์.

2. ํ์ ๋งจ์ฒ์์ ์๋ ๊ฐ์ ๋ฐํํ๊ธฐ ์ํด data ๊ฐ์ ๋ณ์์ ์ ์ฅํ๋ค.

3. ๊ฐ์ ๊ฐ์ ธ์๊ธฐ ๋๋ฌธ์ this.head.next์ ์๋ node๋ฅผ this.head๊ฐ ๊ฐ๋ฆฌํค๋๋ก ํ๋ค. ๊ทธ ๊ฒฐ๊ณผ ๋งจ ์ฒ์์ ์๋ ๋ธ๋๋ ์ฐ๊ฒฐ์ด ๋์ด์ง๊ณ  ๊ทธ ๋ค์ ๋ธ๋๊ฐ ๋งจ ์ฒ์์ผ๋ก ๋ค์ด์ค๊ฒ ๋๋ค.
   <br/>
   <br/>

```jsx
class Queue {
  constructor() {
    this.head = null;
    this.rear = null;
    this.count = 0;
  }

  enqueue(data) {
    const node = new Node(data);
    if (!this.head) {
      this.head = node;
    } else {
      this.rear.next = node;
    }
    this.rear = node;
    this.count++;

    return this.count;
  }

  dequeue() {
    let data;
    if (!this.head) {
      return console.log(`ํ๊ฐ ๋น์์ต๋๋ค.`);
    }
    data = this.head.data;
    this.head = this.head.next;
    this.count--;
    return data;
  }
}

class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

const queue = new Queue();
queue.enqueue(1);
queue.enqueue(2);
console.log(queue);
```
