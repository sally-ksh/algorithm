
## ๐ Map ๊ธฐ๋ณธ ๊ธฐ๋ฅ ๊ตฌํํ๊ธฐ


Entry๋ฅผ ๋ฐฐ์ด์ ๋ด์ entries ๋ฅผ ๊ธฐ๋ณธ ์๋ฃ๊ตฌ์กฐ๋ก ์ค์  ๋งต๊ณผ ๋ค๋ฅด๊ฒ O(n)์ ์๊ฐ ๋ณต์ก๋๋ฅผ ๊ฐ์ต๋๋ค.
entries๋ DEFAULT_CAPACITY๋ก ๊ธฐ๋ณธ ๊ณต๊ฐ์ ๊ฐ์ง๋ฉฐ, ์ ์ฅ๋ size๋ฅผ ์ ์ฅ์๋ง๋ค ์ฒดํฌํ๋ฉด์ ๋ฐฐ์ด ํ์ฅ ๊ธฐ๋ฅ์ ๊ฐ๋๋ก ๊ตฌํํ์ต๋๋ค. 

- **put()** : ๋ฐ์ดํฐ ์ ์ฅ ์์ฒญ์ O(n) 
  - entries ๋ฅผ ์ํํ๋ฉด์ 
    - ๋์ผ ํค ๊ฐ์ด ์์ผ๋ฉด ๊ฐ๋ง ๋ณ๊ฒฝํฉ๋๋ค.
    - ๋์ผ ํค ๊ฐ์ด ์๋ ๊ฒฝ์ฐ, ํ์ฌ์ ์ ์ฅ์ ์ฒดํฌํ๋ size๋ฅผ ํตํด entries ๊ธฐ๋ณธ ํฌ๊ธฐ์ ๋น๊ตํ์ฌ ๋ฐฐ์ด ํฌ๊ธฐ๋ฅผ ํ์ฅํ๊ฒ ํ์ต๋๋ค.
      - entries ๋ฐฐ์ด ํฌ๊ธฐ ๋น๊ต๋ DEFAULT_CAPACITY ๋ก ํ์ง ๋ง์์ผ ํฉ๋๋ค.
        - ํ์ฅ๋ ๊ฒฝ์ฐ๋ DEFAULT_CAPACITY ์ ํฌ๊ธฐ๊ฐ ๋ฌ๋ผ์ง ์ ์๊ธฐ ๋๋ฌธ์ ์ค์  entries์ ์ ์ฅ๋ ์ฌ์ด์ฆ์ ๋น๊ตํด์ผ ํฉ๋๋ค. 


- **get( key )** : ๋ฐ์ดํฐ ์กฐํ ์์ฒญ์ O(n)
  - entries๋ฅผ ์ํํ๋ฉด์ ์ผ์นํ๋ key ๊ฐ ์์ผ๋ฉด ๊ทธ ๊ฐ์ ๋ฐํํฉ๋๋ค.
  - ์์ ๋, null์ ๋ฐํํฉ๋๋ค.


- **remove( key )** : ํค๊ฐ์ ๋ํ ์ญ์  ์์ฒญ์ O(n)
  - entries ์ํํ๋ฉด์ ๋์ผ ํค๊ฐ์ ๋ํด ๊ฐ์ null ์ฒ๋ฆฌ ํฉ๋๋ค.
  - ์ด ๋ ์ ์ฅ๋ ๊ฐ์ ์ค์ด๋ size๋ฅผ ์งํํ๋ค๋ฉด, entries์ ๋ฐฐ์ด ์ฌ์ด์ฆ ๋ํ ์ค์ฌ์ผ ํ๋ ๋ก์ง์ด ์ถ๊ฐ๋์ด์ผ ํฉ๋๋ค.
    - ๋์ ์ผ๋ก size ์ฒดํฌ์ ๊ทธ์ ๋ง๋ ๋ฐฐ์ด ์์ถ์ ๋ํ ๊ณ ๋ฏผ์ ์ข๋ ํด๋ณด๊ณ  ์ถ์ด ๋จ๊ฒจ๋์์ต๋๋ค.
    - ๊ณ ๋ฏผ? ๐ ...
      - ํ์ฅ ์ฒดํฌ์ entries ํฌ๊ธฐ์ ๋น๊ตํด์ผ ํ๊ธฐ ๋๋ฌธ์ ๋ฐฐ์ด ์์ถ์ด ํ์ํฉ๋๋ค.
      - ๋์ผ ์กฐ๊ฑด ๋น๊ต์ด๊ธฐ ๋๋ฌธ์, size๊ฐ ๋์ค์ ์ฆ๊ฐํ์ฌ entries ์ ์์ถํ์ง ์์ ์ฌ์ด์ฆ ์ผ ๋ ํ์ฅ ๋ก์ง์ ์ํ ํ  ์ ์์ต๋๋ค.
      - ํ์ง๋ง, 2๋ฐฐ๋ ์ปค์ง ๋ฐฐ์ด ์ฌ์ด์ฆ๊ฐ ๋นํจ์จ ์ ์ผ ์ ์์ต๋๋ค.

- keySet() : O(n)
  - key๋ ์ค๋ณต๋  ์ ์์ต๋๋ค.
  - ์ค๋ณต์๋๋ก Set์ ๋ด์ ๋ฐํํฉ๋๋ค.
- values() : O(n)
  - ๋ค์ํ ํ์ฉ์ ์ํด Collection ํ์์ผ๋ก ๋ฐํ ํฉ๋๋ค.

``` java

public class MyMap<K, V> {
	private final class Entry<K, V> {
		private final K key;
		private V value;

		public Entry(K key, V value) {
			this.key = key;
			this.value = value;
		}

		public K getKey() {
			return key;
		}

		public V getValue() {
			return value;
		}

		public void setValue(V value) {
			this.value = value;
		}

		@Override
		public String toString() {
			return "[" + key + " :" + value + ']';
		}
	}

	private static final int DEFAULT_CAPACITY = 16;
	private int size;
	private Entry<K, V>[] entries = new Entry[DEFAULT_CAPACITY];

	public V get(K key) {
		for (int i = 0; i < size; i++) {
			if (entries[i] != null) {
				if (entries[i].getKey().equals(key)) {
					return entries[i].getValue();
				}
			}
		}
		return null;
	}

	public void put(K key, V value) {
		boolean isSaved = false;
		for (int i = 0; i < size; i++) {
			if (entries[i].getKey().equals(key)) {
				entries[i].setValue(value);
				isSaved = true;
			}
		}

		if (!isSaved) {
			checkCapacityAndResize();
			entries[size++] = new Entry<>(key, value);
		}
	}

	private void checkCapacityAndResize() {
		if (size == entries.length) {
			int extendSize = entries.length * 2;
			entries = Arrays.copyOf(entries, extendSize);
		}
	}

	public void remove(K key) {
		for (int i = 0; i < size; i++) {
			if (entries[i].getKey().equals(key)) {
				entries[i] = null;
				size--;
				// ๋ฐฐ์ด ์์ถ?
			}
		}
	}

	public Set<K> keySet() {
		return Arrays.stream(entries)
			.map(Entry::getKey)
			.collect(Collectors.toSet());
	}

	public Collection<V> values() {
		return Arrays.stream(entries)
			.map(Entry::getValue)
			.collect(Collectors.toList());
	}
}

```
