# 我们知道 ArrayList 是线程不安全，请编写一个不安全的案例并给出解决方案？
故障现象

```
public class ContainerDemo {
    public static void main(String[] args) {
        List<Integer> list = new ArrayList<>();
        Random random = new Random();
        for (int i = 0; i < 100; i++) {
            new Thread(() -> {
                list.add(random.nextInt(10));
                System.out.println(list);
            }).start();
        }
    }
}
```
`发现报 java.util.ConcurrentModificationException`

导致原因

并发修改导致的异常
解决方案

```
new Vector();
Collections.synchronizedList(new ArrayList<>());
new CopyOnWriteArrayList<>();
```
优化建议

在读多写少的时候推荐使用 CopeOnWriteArrayList 这个类