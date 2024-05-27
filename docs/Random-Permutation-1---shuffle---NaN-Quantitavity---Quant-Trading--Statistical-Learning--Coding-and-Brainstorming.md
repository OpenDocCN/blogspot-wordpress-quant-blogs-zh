<!--yml

分类：未分类

日期：2024-05-18 13:57:45

-->

# 随机置换 1 – 洗牌 | 非数值量化 - 量化交易、统计学习、编程和头脑风暴

> 来源：[`quantlife.wordpress.com/2013/03/13/random-permutation-1-shuffle/#0001-01-01`](https://quantlife.wordpress.com/2013/03/13/random-permutation-1-shuffle/#0001-01-01)

### 随机置换 1 – 洗牌

```
public static void shuffleArray(int[] array) {
    Random generator = new Random();
    for (int j = 0; j < array.length; j++) {
    int index = generator.nextInt(array.length-j)+j; // random number between j and n
    int temp = array[index];
    array[index] = array[j];
    array[j] = temp;
    }
}
```

暂无评论。
