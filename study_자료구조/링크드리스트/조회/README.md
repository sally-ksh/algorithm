

## ๐ ๋ค์์ n๋ฒ์งธ ์กฐํ

<br>

#### ๋จ์ผ ์ฐ๊ฒฐ ๋ฆฌ์คํธ

Node

- data, next ์ํ๋ง ๊ฐ์ง๋๋ค.

SingleLinkedList

- head, current(tail) ์ํ๋ง ๊ฐ์ง๋๋ค.

current ๋ธ๋์์ ์์ ๋ธ๋๋ก ๊ฐ ๋ฐฉ๋ฒ์ด ์๊ธฐ ๋๋ฌธ์ n ๋ฒ์งธ ์์๋ฅผ ์๊ธฐ ์ํด์ 

- ์ ์ฒด ๊ธธ์ด ์ด์ฉํ ์กฐํ
- ํด์ ์ด์ฉํ ์กฐํ


<br><br><br>


#### 1๏ธโฃ ์๊ฐ ๋ณต์ก๋ O(n) , ๊ณต๊ฐ ๋ณต์ก๋ O(1)

- **๋ฆฌ์คํธ ์ ์ฒด ์ฌ์ด์ฆ**๋ฅผ ์๊ธฐ ์ํด ์ํ ํฉ๋๋ค.
- ๋ฆฌ์คํธ ์ ์ฒด ์ฌ์ด์ฆ์์ ์์ฒญํ n๋ฒ์งธ ๋งํผ ์ํํ์ฌ ํด๋น ๋ฐ์ดํฐ๋ฅผ ๋ฐํํฉ๋๋ค.

``` java

    public int getFromLast(int lastIdx) {
        int size = 0;
        Node node = this.head;
        while (!Objects.isNull(node)) {
            node = node.next();
            size++;
        }
    
        size -= lastIdx;
        node = this.head;
        while (size-- > 0) {
            node = node.next();
        }
        return node.data();
    }

```

<br>

#### 2๏ธโฃ ์๊ฐ ๋ณต์ก๋ O(n) , ๊ณต๊ฐ ๋ณต์ก๋ O(n)

- **for๋ฌธ ๋ ๋ฒ ์ํ๋ฅผ ์ค์ด๊ธฐ ์ํด์** 
  - ์ฒ์ ์ํ์ `Map`์ ์ด์ฉํด ๊ฐ index ๋ณ๋ก Node๋ฅผ ๋ด์ต๋๋ค.
  - ์์ฒญํ n๋ฒ์งธ๋ฅผ Map์์ ๋ฐํํฉ๋๋ค.
- **์ธ๋ฑ์ค๋ก ๋ฐฐ์ด**์ ์๊ฐํ  ์ ์์ง๋ง, 
  - ์ถ๊ฐ/์ญ์  ์๋ง๋ค `์ ์ฒด ๊ธธ์ด ์ฒดํฌํ๋ ์ ์ญ๋ณ์`๋ฅผ ์ถ๊ฐํด์ผ ๋ฐฐ์ด์ ์ฌ์ฉํ  ์ ์์ต๋๋ค.

``` java

    public int getFromLast(int lastIdx) {
        int size = 0;
        Map<Integer, Node> nodeMap = new HashMap<>();
        Node node = this.head;
    
        while (!Objects.isNull(node)) {
            nodeMap.put(size++, node);
            node = node.next();
        }
        return nodeMap.get(size - lastIdx).data();
    }

```

<br>

#### 3๏ธโฃ ์๊ฐ ๋ณต์ก๋ O(n) , ๊ณต๊ฐ ๋ณต์ก๋ O(1)

- for๋ฌธ 1๋ฒ๋ง ์ํํ๊ณ , ๊ณต๊ฐ๋ณต์ก๋๋ฅผ O(1) ๋ก ๊ตฌํํ๊ธฐ ์ํด์
  - `์ ์ฒด ์ฌ์ด์ฆ ๋งํผ ์ํํ  index`์ ์ฌ์ฉ์๊ฐ ์์ฒญํ `n๋ฒ์งธ ๋งํผ ์ํํ  index`๋ฅผ ์ด์ฉํฉ๋๋ค.
  - ์ ์ฒด ์ฌ์ด์ฆ์ n๋ฒ์งธ๋ฅผ `gap` ์ผ๋ก ๊ตฌ๋ถํฉ๋๋ค.
  - ๋ณ๋์ Node ๋ณ์์ `n๋ฒ์งธ ๋งํผ ์ด๋ํ์ ๋์ node` ๋ฅผ ์ ์ฅํฉ๋๋ค.

``` java
    
    public int getFromLast(int lastIdx) {
        int left = 0;
        int right = 0;
        int gap = lastIdx - 1;
        Node node = this.head;
        Node result = this.head;
        while (!Objects.isNull(node)) {
            if (right - left > gap) {
                left++;
                result = result.next();
            }
            right++;
            node = node.next();
        }
        return result.data();
    }

```
