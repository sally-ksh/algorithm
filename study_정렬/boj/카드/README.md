
## π κ°μΈ νμ΄

- [boj 11653 μΉ΄λ](https://www.acmicpc.net/problem/11652)

- μλ ₯λ°λ μΉ΄λ λ²νΈκ° long μ΄μ΄μΌ νλ€.
- λ°°μ΄ ν΅ν΄μ νλ κ°λ¨ν λ°©λ²λ μλ€.

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
