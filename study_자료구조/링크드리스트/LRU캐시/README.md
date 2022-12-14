
## π° LRU μΊμ μλ°λ‘ κ΅¬ννκΈ° - 1οΈβ£

- μΊμ νΉμ±μ μ μ₯ κ³΅κ° μ νμ μλλ€. β `cacheSize`
- LRUλ μ΅κ·Ό μ°Έμ‘°κ°λ€μ μΊμ±νλ λ°©μ μλλ€.
  - μ΅κ·Ό μ°Έμ‘°λ μμλ€κ³Ό μ€λ μ°Έμ‘°λ μμλ€μ κ΅¬λΆν©λλ€. β λ§ν¬λ λ¦¬μ€νΈ μμ
    - μ΅κ·Ό μ°Έμ‘°λ μμλ λ¨Έλ¦¬λΈλμ λμλλ€. β`addFirst`
    - λ¨Έλ¦¬λΈλ μΆκ°λ‘ μ€λ μ°Έμ‘°λ μμλ λ€λ‘ λ°λ €λ©λλ€.
      - μ νμ  κ³΅κ°μΌλ‘ λμ΄κ°μ κΌ¬λ¦¬ λΈλλΆν° μ­μ ν©λλ€. β`pollLast`
- μμλ₯Ό κ°μ§κ³ , λ¨Έλ¦¬λΈλμ κΌ¬λ¦¬λΈλμμ μκ°λ³΅μ‘λ O(1) μ μ½μ, μΆκ°κ° κ°λ₯ν Deque μλ£κ΅¬μ‘°λ₯Ό μ¬μ© νμ΅λλ€.

<br>

- λ°μ΄ν° μ μ₯ κ³Όμ μμ λ¨Όμ  λ°μ΄ν°κ° λ³΄κ΄λμ΄ μλ λ°μ΄ν°μΈμ§ νμΈν©λλ€.
  - λλ¬Έμ `get()` μμ²­μ μ¬μ©ν©λλ€.
  - μ‘°νμ μμ κ²½μ° λ°νκ° `-1`μ λ μΌλ‘μ put()μμ κ΅¬λΆκ°λ₯ν΄μ§λλ€.
  - `get()` μ¬νμ©μΌλ‘ put() μμμ λ³λμ if-else λ¬Έμ μ°μ§ μμ μ μμμ΅λλ€.
- μ‘°νμ μκ°λ³΅μ‘λ O(n), κ³΅κ° λ³΅μ‘λ O(n)
  - μ‘°νμ `contains()` , `remove()` λ‘ μΈν΄ nλ§νΌ μνν΄μΌ νκΈ° λλ¬Έμ μκ° λ³΅μ‘λκ° O(n) μλλ€.
  - Deque μ cacheSizeμΈ nλ§νΌ κ³΅κ°μ μ¬μ©νκΈ° λλ¬Έμ κ³΅κ° λ³΅μ‘λ O(n) μλλ€.

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
