
## 🎰 LRU 캐시 자바로 구현하기 - 1️⃣

- 캐시 특성상 저장 공간 제한적입니다. ➜ `cacheSize`
- LRU는 최근 참조값들을 캐싱하는 방식 입니다.
  - 최근 참조된 요소들과 오래 참조된 요소들을 구분합니다. ➜ 링크드 리스트 순서
    - 최근 참조된 요소는 머리노드에 놓입니다. ➜`addFirst`
    - 머리노드 추가로 오래 참조된 요소는 뒤로 밀려납니다.
      - 제한적 공간으로 넘어갈시 꼬리 노드부터 삭제합니다. ➜`pollLast`
- 순서를 가지고, 머리노드와 꼬리노드에서 시간복잡도 O(1) 의 삽입, 추가가 가능한 Deque 자료구조를 사용 했습니다.

<br>

- 데이터 저장 과정에서 먼저 데이터가 보관되어 있는 데이터인지 확인합니다.
  - 때문에 `get()` 요청을 사용합니다.
  - 조회시 없을 경우 반환값 `-1`을 둠으로서 put()에서 구분가능해집니다.
  - `get()` 재활용으로 put() 에서의 별도의 if-else 문을 쓰지 않을 수 있었습니다.
- 조회시 시간복잡도 O(n), 공간 복잡도 O(n)
  - 조회시 `contains()` , `remove()` 로 인해 n만큼 순회해야 하기 때문에 시간 복잡도가 O(n) 입니다.
  - Deque 에 cacheSize인 n만큼 공간을 사용하기 때문에 공간 복잡도 O(n) 입니다.

``` java
public class LRUCache {
	private Deque<Integer> cache = new LinkedList<>();
	private int cacheSize;

	public LRUCache(int cacheSize) {
		this.cache = new LinkedList<>();
		this.cacheSize = cacheSize;
	}

	public int get(int data) {
		if (cache.contains(data)) {
			updateRecently(data);
			return data;
		} else {
			return -1;
		}
	}

	public void put(int data) {
		if (get(data) == -1) {
			if (cache.size() >= cacheSize) {
				cache.pollLast();
			}
			cache.addFirst(data);
		}
	}

	private void updateRecently(int data) {
		cache.remove(data);
		cache.addFirst(data);
	}

	private void print() {
		System.out.println(cache);
	}

	public static void main(String[] args) {
		LRUCache lru = new LRUCache(3);

		lru.put(1);
		lru.put(2);
		lru.put(3);
		lru.put(1);
		lru.put(4);
		lru.put(5);
		lru.put(2);
		lru.put(2);
		lru.put(1);

		lru.print();  // [1, 2, 5]
	}
}
```
