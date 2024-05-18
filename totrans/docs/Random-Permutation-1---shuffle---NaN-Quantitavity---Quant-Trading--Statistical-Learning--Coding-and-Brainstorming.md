<!--yml
category: 未分类
date: 2024-05-18 13:57:45
-->

# Random Permutation 1 – shuffle | NaN Quantitavity - Quant Trading, Statistical Learning, Coding and Brainstorming

> 来源：[https://quantlife.wordpress.com/2013/03/13/random-permutation-1-shuffle/#0001-01-01](https://quantlife.wordpress.com/2013/03/13/random-permutation-1-shuffle/#0001-01-01)

### Random Permutation 1 – shuffle

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

No comments yet.