# Inbox

배열을 정렬할떄 Arrays.sort에 Comparable를 구현한 클래스를 넣어주면된다. Collections.reverseOrder() 등 미리 구현한 걸 사용해도 되고, 직접 구현해도 된다 Comparator는 compare() 만 구현하면되도록 되어있기때문에 따라서 익명함수로 사용이가능하다 구현할땐 기준을 정해주면 된다 기준은 주어진 객체(T o) 보다 작으면 음수, 같으면 0, 크면 양수를 리턴한다

```java
public class Test {
    public static void main(String[] args) {
        String[] arr = {"C", "B", "A"};
        Arrays.sort(arr, new Comparator<String>() {
            @Override
            public int compare(String o1, String o2) {
                return CompareUtil.compareTo(o1, o2);
            }
        });

        System.out.println(Arrays.toString(arr));
    }

    public static class CompareUtil {
        public static int compareTo(String l, String r) {
            if (l == null && r == null)
                return 0;
            if (l == null)
                return -1;
            if (r == null)
                return 1;
            return l.compareTo(r);
        }

    }
}
```

