
## π­ λ²λΈ μ λ ¬

- μ²μλΆν° μμ 2κ°λ₯Ό μννλ©° λΉκ΅ - O(n)
  - λΉκ΅μ μ λ ¬ μ λ λ§νΌ swap λ°μ
  - μννλ©΄μ κ°μ₯ ν°κ°μ λ€λ‘ λκΉμ§ μ΄λνκΈ° λλ¬Έμ κΈΈμ΄ μμ 1κ°μ© λ§νΌ κ°μ

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


- μ¬κ·

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
