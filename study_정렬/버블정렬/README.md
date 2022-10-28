
## 💭 버블 정렬

- 처음부터 요소 2개를 순회하며 비교 - O(n)
  - 비교시 정렬 안 된 만큼 swap 발생
  - 순회하면서 가장 큰값은 뒤로 끝까지 이동하기 때문에 길이 요소 1개씩 만큼 감소

``` java
    private void bubbleSortDoubleIterator() {
		int size = arr.length;
		for (int i = 0; i < size; i++) {
			for (int j = 0; j < size - i-1; j++) {
				if (arr[j] > arr[j + 1]) {
					swap(arr, j, j + 1);
				}
			}
		}
	}
	
	private void swap(int[] arr, int bigger, int smaller) {
		int temp = arr[bigger];
		arr[bigger] = arr[smaller];
		arr[smaller] = temp;
	}
```


- 재귀

``` java
	private void bubbleRecursive(int length) {
		if (length <= 0) return;

		for (int i = 0; i < length-1; i++) {
			if (arr[i] > arr[i + 1]) {
				swap(arr, i, i + 1);
			}
		}
		bubbleRecursive(length-1);
	}
```
