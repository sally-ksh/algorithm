
## 이진 탐색

> 학습 참조 : "이것이 취업을 위한 코딩 테스트다.", 나동빈 저자, 한빛미디어
> 

``` java
    private int binary_search(int search, int left, int right) {
		if (left > right) {
			System.out.println("no");
			return -1;
		}

		int mid = (left + right) / 2;
		if (search < data[mid]) {
			return binary_search(search, left, mid - 1);
		}
		if (data[mid] == search) {
			return mid;
		}
		return binary_search(search, mid+1, right);
	}
```
