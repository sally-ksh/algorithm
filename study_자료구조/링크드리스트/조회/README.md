

## 🔙 뒤에서 n번째 조회

<br>

#### 단일 연결 리스트

Node

- data, next 상태만 가집니다.

SingleLinkedList

- head, current(tail) 상태만 가집니다.

current 노드에서 앞의 노드로 갈 방법이 없기 때문에 n 번째 요소를 알기 위해서 

- 전체 길이 이용한 조회
- 해시 이용한 조회


<br><br><br>


#### 1️⃣ 시간 복잡도 O(n) , 공간 복잡도 O(1)

- **리스트 전체 사이즈**를 알기 위해 순회 합니다.
- 리스트 전체 사이즈에서 요청한 n번째 만큼 순회하여 해당 데이터를 반환합니다.

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

#### 2️⃣ 시간 복잡도 O(n) , 공간 복잡도 O(n)

- **for문 두 번 순회를 줄이기 위해서** 
  - 처음 순회시 `Map`을 이용해 각 index 별로 Node를 담습니다.
  - 요청한 n번째를 Map에서 반환합니다.
- **인덱스로 배열**을 생각할 수 있지만, 
  - 추가/삭제 시마다 `전체 길이 체크하는 전역변수`를 추가해야 배열을 사용할 수 있습니다.

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

#### 3️⃣ 시간 복잡도 O(n) , 공간 복잡도 O(1)

- for문 1번만 순회하고, 공간복잡도를 O(1) 로 구현하기 위해서
  - `전체 사이즈 만큼 순회할 index`와 사용자가 요청한 `n번째 만큼 순회할 index`를 이용합니다.
  - 전체 사이즈와 n번째를 `gap` 으로 구분합니다.
  - 별도의 Node 변수에 `n번째 만큼 이동했을 때의 node` 를 저장합니다.

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
