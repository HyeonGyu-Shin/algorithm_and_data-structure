# Q. ์คํ

---

### ์คํ  
<br/>
<br/>

![Untitled](../stack/assets/Untitled.png)
  
<br/>
<br/>
  
๐ ์คํ์ ๋ฌผ๊ฑด์ ์ธ๋ก๋ก ์๋๋ค๊ณ  ์๊ฐํ๋ฉด ๋๋ค.
์์ฌ์๋ ๋ฌผ๊ฑด๋ค ์ค ํ๋๋ฅผ ๊บผ๋ด๋ ค๋ฉด ์์์๋ถํฐ ์ฐจ๋ก๋ก ๊บผ๋ด์ผํ๋ค.
  
<br/>
<br/>
  

![Untitled](../stack/assets/Untitled%201.png)
  
<br/>
<br/>
  

๐ ์คํ์์ ๋ฐ์ดํฐ๋ฅผ ์ถ๊ฐํ  ๋๋ ๊ฐ์ฅ ์์ ์ถ๊ฐ๊ฐ ๋๋ค. ์ด๋ฅผ pushํ๊ณ  ํ๋ค.  
  
<br/>
<br/>
  

![Untitled](../stack/assets/Untitled%202.png)
  
<br/>
<br/>
  

๐ ์คํ์์ ๋ฐ์ดํฐ๋ฅผ ๊บผ๋ผ ๋๋ ๊ฐ์ฅ ์, ์ฆ ๊ฐ์ฅ ์ต๊ทผ์ ์ถ๊ฐํ ๋ฐ์ดํฐ๊ฐ ๊บผ๋ด์ง๋ค. ์ด๋ฅผ pop์ด๋ผ๊ณ  ํ๋ค.  
<br/>


๐ ์ด๋ฌํ ๊ตฌ์กฐ๋ฅผ โLast In First Outโ์ด๋ผ ํ๋ฉฐ โLIFOโ๋ผ๊ณ ๋ ํ๋ค.
  
<br/>
  

๐ ์ด์  ์ด๋ฅผ ๋ฐํ์ผ๋ก ์ฝ๋๋ก ์์๋ณด์!
  
<br/>
  

```jsx
const Stack = (function () {   ... 1
    function Stack() {
        this.top = null;
        this.count = 0;
    };

    function Node(data) {
        this.data = data;
        this.next = null;
    }

    return Stack;
})();

const stack = new Stack();   ... 2
console.log(stack);

==========================

Stack{ top: null, count: 0 }
```
<br/>

๐ ์ด๋ป๊ฒ Stack ์ธ์คํด์ค๊ฐ ์์ฑ๋์๋์ง ์์๋ณด์.  
<br/>


1. ์ฆ์์คํ ํจ์๊ฐ ์คํ์ด ๋๊ณ , return ๊ฐ์ธ Stack ํจ์๋ฅผ const Stack์ ๋ฃ์ด์ค๋ค.

2. ๊ฒฐ๊ตญ Stack์ ํธ์ถํ๋ฉด ์ฆ์์คํ ํจ์์ Stack ํจ์๊ฐ ์คํ์ด ๋๋ค.

ํ์ง๋ง ์ฐ๋ฆฐ ์ธ์คํด์ค๋ฅผ ์ฌ์ฉํด์ผ ํ๋ค. ๋ฐ๋ผ์ new ํค์๋ ์ฌ์ฉํ์ฌ ์ธ์คํด์ค๋ฅผ ์์ฑํ๋ค.

์๋ฆฌ๋ ๋ค์๊ณผ ๊ฐ๋ค. new ํค์๋๋ฅผ ์ฌ์ฉํ๋ฉด ๋น ๊ฐ์ฒด this๋ฅผ ๋ง๋ ๋ค. ์์์๋ ์ด this์ top = null, count = 0์ ๋ฃ์ด์ค๋ค. Stack์๋ return์ด ์๊ธฐ ๋๋ฌธ์ ๋ฐฉ๊ธ ๋ง๋  ์ ๊ฐ์ฒด๋ฅผ return ํ๋๋ก ์ฒ๋ฆฌํด์ค๋ค.

๋ฐ๋ผ์ stack์๋ Stack ์ธ์คํด์ค๊ฐ ํ ๋น๋๊ฒ ๋๋ค.
  
<br/>
  

๐ ์ ์ด์  stack์ ๋ง๋ค์๊ณ , ์ด์  push์ pop์ ๊ตฌํํ๋ฌ ๊ฐ๋ณด์.
  
<br/>
  

```jsx
Stack.prototype.push = function (data) {
        const node = new Node(data);
        node.next = this.top;   ... 1
		    this.top = node;   ... 2
				this.count++;

				return this.count;
    }
.
.
.

const stack = new Stack();
stack.push(1);
stack.push(2);
console.log(stack);

==========================

Stack {
  top: Node { data: 2, next: Node { data: 1, next: null } },
  count: 2
}
```
  
  
๐ ์คํ์ ๋งจ ์์ ๋ฐ์ดํฐ๋ฅผ ๋ฃ๋ push ๋ฉ์๋์ด๋ค.
  
  

1. ์๋ก ๋ง๋ค์ด์ง node์ ๋ค์ node ์์น๋ฅผ ํ์ฌ์ node๋ก ์ฐ๊ฒฐํด์ค๋ค. ๊ทธ ๊ฒฐ๊ณผ ๋ฐฐ์ด๊ณผ ๊ฐ์ ํํ๋ผ๋ฉด ๋งจ ์, ์คํ์ด๋ฉด ๋งจ ์์ node๊ฐ ๋ค์ด๊ฐ๊ฒ ๋๋ค.

2. ํ ์์น๋ฅผ ๋ํ๋ด๋ this.top์ด node๋ฅผ ๊ฐ๋ฆฌํค๊ฒ ํ๋ค.
  
<br/>
  

```jsx
Stack.prototype.pop = function () {
	      let data;
        if (!this.top) {   ... 1
            return console.log('stack์ด ๋น์์ต๋๋ค.');
        }
        data = this.top.data; ... 2
        this.top = this.top.next;   ... 3
        this.count--;
        return data;

    }
.
.
.

const stack = new Stack();
stack.push(1);
stack.push(2);
console.log(stack.pop());
console.log(stack.pop());
console.log(stack.pop());
console.log(stack);

=======================

2
1
stack์ด ๋น์์ต๋๋ค.
undefined
Stack { top: null, count: 0 }
```
  
  
๐ stack์ ์ต์์์ธ this.top์ด ๊ฐ๋ฆฌํค๋ ๋ฐ์ดํฐ๋ฅผ ๋ฐํํด์ฃผ๋ pop ๋ฉ์๋์ด๋ค.
  
  
1. this.top์ด null์ ๊ฐ๋ฆฌํค๊ฒ ๋๋ฉด ์ค๋ฅ๊ฐ ๋ฐ์ํ๊ฒ ๋๋ค. ๋ฐ๋ผ์ ์ด๋ฅผ ๋ฐฉ์งํ๊ธฐ ์ํด this.top์ด ๋น์๋ค๋ฉด ํจ์๋ฅผ ๋๋ธ๋ค.

2. this.top์ด ๊ฐ๋ฆฌํค๋ ์ต์์ ๋ธ๋์ ๋ฐ์ดํฐ ๊ฐ์ ๋ฃ์ด์ค๋ค. ์ถํ ์ด๋ฅผ ๋ฐํํ๋ค.

3. this.top.next๋ ์๋ก์ด node๊ฐ ๋ค์ด์ค๊ธฐ ์ ์ ์ต์์ ๋ธ๋๋ฅผ ๊ฐ๋ฆฌํค๊ณ  ์๋ค. ์ด๋ฅผ this.top์ ๋ฃ์ด์ฃผ๋ฉด this.top์ด ์ด์ ์ ๊ฐ์ ๊ฐ๋ฆฌํค๊ธฐ ๋๋ฌธ์ stack์ด ๊ฐ์ด ๋๊ฐ ํ ์ต์ ํ ๋ ๊ฒ ์ฒ๋ผ ํํํ  ์ ์๋ค.
  
<br/>
  

```jsx
Stack.prototype.stackTop = function () {
  return this.top.data;
};

Stack.prototype.getCount = function () {
  return this.count;
};
```

๐ ๊ทธ ์ธ์๋ ์์ฒ๋ผ ์ฌ๋ฌ ๋ฉ์๋๋ฅผ ์ถ๊ฐ๋ก ๋ง๋ค ์ ์๋ค.
