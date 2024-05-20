<!--yml
category: 未分类
date: 2024-05-18 13:57:40
-->

# Random Permutation 2 – Random sample m out of n | NaN Quantitavity - Quant Trading, Statistical Learning, Coding and Brainstorming

> 来源：[https://quantlife.wordpress.com/2013/03/13/random-permutation-2-random-sample-m-out-of-n/#0001-01-01](https://quantlife.wordpress.com/2013/03/13/random-permutation-2-random-sample-m-out-of-n/#0001-01-01)

### Random Permutation 2 – Random sample m out of n

```
int[] pickMRandomly(int[] array, int m) {
    int[] subset = new int[m];
    for (int j = 0; j < m; j++) {
        int index = random(j, n); // random number between j and n
        int temp = array[index];
        array[index] = array[j];
        array[j] = temp;
        subset[j] = temp;
    }
    return subset;
}
```