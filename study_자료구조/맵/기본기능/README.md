
## 👋 Map 기본 기능 구현하기


Entry를 배열에 담은 entries 를 기본 자료구조로 실제 맵과 다르게 O(n)의 시간 복잡도를 갖습니다.
entries는 DEFAULT_CAPACITY로 기본 공간을 가지며, 저장된 size를 저장시마다 체크하면서 배열 확장 기능을 갖도록 구현했습니다. 

- **put()** : 데이터 저장 요청시 O(n) 
  - entries 를 순회하면서 
    - 동일 키 값이 있으면 값만 변경합니다.
    - 동일 키 값이 없는 경우, 현재의 저장을 체크하는 size를 통해 entries 기본 크기와 비교하여 배열 크기를 확장하게 했습니다.
      - entries 배열 크기 비교는 DEFAULT_CAPACITY 로 하지 말아야 합니다.
        - 확장된 경우는 DEFAULT_CAPACITY 와 크기가 달라질 수 있기 때문에 실제 entries의 저장된 사이즈와 비교해야 합니다. 


- **get( key )** : 데이터 조회 요청시 O(n)
  - entries를 순회하면서 일치하는 key 가 있으면 그 값을 반환합니다.
  - 없을 땐, null을 반환합니다.


- **remove( key )** : 키값에 대한 삭제 요청시 O(n)
  - entries 순회하면서 동일 키값에 대해 값을 null 처리 합니다.
  - 이 때 저장된 값을 줄이는 size를 진행한다면, entries의 배열 사이즈 또한 줄여야 하는 로직이 추가되어야 합니다.
    - 동적으로 size 체크와 그와 맞는 배열 압축에 대한 고민을 좀더 해보고 싶어 남겨두었습니다.
    - 고민? 🙄 ...
      - 확장 체크시 entries 크기와 비교해야 하기 때문에 배열 압축이 필요합니다.
      - 동일 조건 비교이기 때문에, size가 나중에 증가하여 entries 의 압축하지 않은 사이즈 일 때 확장 로직을 수행 할 수 있습니다.
      - 하지만, 2배나 커진 배열 사이즈가 비효율 적일 수 있습니다.

- keySet() : O(n)
  - key는 중복될 수 없습니다.
  - 중복없도록 Set에 담아 반환합니다.
- values() : O(n)
  - 다양한 활용을 위해 Collection 타입으로 반환 합니다.

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
				// 배열 압축?
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
