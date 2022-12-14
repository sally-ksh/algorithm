
## π κ°μΈ νμ΄

- [boj 15970 νμ΄ν κ·Έλ¦¬κΈ°](https://www.acmicpc.net/problem/15970)


``` java

class ColorPoint implements Comparable<ColorPoint> {
	int color;
	int point;

	public ColorPoint(int color, int point) {
		this.color = color;
		this.point = point;
	}

	public int shortDistance(int left, int right) {
		int leftDistance = point - left;
		int rightDistance = right - point;
		return (leftDistance < rightDistance) ? leftDistance : rightDistance;
	}

	@Override
	public int compareTo(ColorPoint another) {
		if (color == another.color) {
			return point - another.point;
		}
		return color - another.color;
	}
}

public class Boj15970 {
	static List<ColorPoint> points = new ArrayList<>();

	static int N;

	static void input() {
		N = scan.nextInt();

		for (int i = 1; i <= N; i++) {
			int coord, color;
			coord = scan.nextInt();
			color = scan.nextInt();
			points.add(new ColorPoint(color, coord));
		}
	}

	static void pro() {
		points.sort(ColorPoint::compareTo);
		// μ’/μ° κ±°λ¦¬ λΉκ΅μμ κ°μ₯ μ§§μ κ°μ κ±°λ¦¬μ +
		int ans = points.get(1).point - points.get(0).point;  // μμ->
		ans += points.get(N - 1).point - points.get(N-2).point;  // <-λ
		for (int i = 1; i < N-1; i++) {
			ColorPoint left = points.get(i - 1);
			ColorPoint counter = points.get(i);
			ColorPoint right = points.get(i + 1);

			if (right.color != counter.color) {
				ans += counter.point - left.point;
				continue;
			}
			if (left.color != counter.color) {
				ans += right.point - counter.point;
				continue;
			}
			ans += counter.shortDistance(left.point, right.point);
		}
		System.out.println(ans);
	}

	public static void main(String[] args) {
		input();
		pro();
	}
}

```
