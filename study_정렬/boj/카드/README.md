
## 😃 개인 풀이

- [boj 11653 카드](https://www.acmicpc.net/problem/11652)

- 입력받는 카드 번호값 long 이어야 한다.
- 배열 통해서 하는 간단한 방법도 있다.

``` java

class Card implements Comparable<Card> {
	int count;
	long num;

	public Card(long num) {
		this.count = 1;
		this.num = num;
	}

	@Override
	public int compareTo(Card another) {
		if (count == another.count) {
			return this.num < another.num ? -1 : 1;
		}
		return another.count - this.count;
	}
}

public class Boj11652 {
	static Map<Long, Card> map = new HashMap();

	static int N;

	static void input() {
		N = scan.nextInt();
		for (int i = 0; i < N; i++) {
			long number = scan.nextLong();
			if (map.containsKey(number)) {
				map.get(number).count++;
			} else {
				map.put(number, new Card(number));
			}
		}
	}
    
    static void pro() {
        PriorityQueue<Card> pq = new PriorityQueue<>();
        for (long key : map.keySet()) {
            pq.offer(map.get(key));
        }
    
        System.out.println(pq.peek().num);
    }
    
    public static void main(String[] args) {
        input();
        pro();
    }
}
```
