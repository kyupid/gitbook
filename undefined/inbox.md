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

### InputStream OutputStream

* input: 외부에서 들어오는 리소스
* output: 외부로 보낼 리소스&#x20;

#### 파일 쓰고 읽을때 바이트배열에 정수를 넣는것의 의미



```java
        byte[] bytes = {'a', 'b', '7', 6, 3, 4, 3, 2, 1, 0};
 
        File file = new File("write_test.txt");
        OutputStream outputStream = Files.newOutputStream(file.toPath());

        for (int b : bytes) {
            outputStream.write(b);
        }

        //바이트를 한번에 넣을 수 있다.
//        outputStream.write(bytes);

        outputStream.close();
```

6,3,4 … 는 해당되는 숫자그대로 바이트로 들어가기때문에 읽을때 ACK 이런식으로 아스키코드표에나오는 코드표대로 나온다

![](<../.gitbook/assets/image (1).png>)

‘a’ 등은 따옴표로 해주면 그 문자에 상응하는 바이트코드가 들어가게 되서 출력할때 잘나오게된다
