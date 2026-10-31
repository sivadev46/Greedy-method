# Design and Analysis of Algorithms — Greedy Method

This repository contains verified C language solutions using the **Greedy Method** algorithmic paradigm. These algorithms make locally optimal choices at each stage with the goal of finding a global optimum. The problems covered focus on structural optimizations including coin change distributions, pair scheduling, and array multiplications.

---

## 🚀 Problems Overview & Complexity Matrix

| Problem ID | Problem Description | Strategy / Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- | :--- | :--- |
| **Problem 1** | Indian Currency Coin Change | Largest Denomination First Choice | $O(1)$ *(Fixed Coins)* | $O(1)$ |
| **Problem 2** | Assign Cookies to Children | Two-Pointer Array Matching | $O(n \log n + m \log m)$ | $O(n + m)$ |
| **Problem 3** | Minimum Burnout Calories | Highest Weight First Sorting Pass | $O(n^2)$ | $O(n)$ |
| **Problem 4** | Maximize Array Index Product | Sort Ascending Matrix Multiplication | $O(n \log n)$ | $O(n)$ |
| **Problem 5** | Minimum Product Sum of Pairs | Sort Alternating Bounds (Asc / Desc) | $O(n \log n)$ | $O(n)$ |

---

## 🛠️ Detailed Implementations

### Problem 1: Indian Currency Coin Change
Given a target value $V$, this program determines the minimum number of notes/coins required to fulfill the exact amount using an infinite supply of standard Indian currency units `{1, 2, 5, 10, 20, 50, 100, 500, 1000}`.

```c
#include <stdio.h>

int main(){
    int v;
    if(scanf("%d", &v) == 0) return 1;

    int denomination[] = {1000, 500, 100, 50, 20, 10, 5, 2, 1};
    int count = 0;

    for(int i = 0; i < 9; i++){
        if(v == 0) break;
        count += v / denomination[i];
        v %= denomination[i];
    }

    printf("%d", count);
    return 0;
}
```

### Problem 2: Assign Cookies to Children
Maximizes the count of content children by sorting child greed factors ($g$) and cookie sizes ($s$), matching the smallest viable cookie sizes sequentially to content the least greedy requirements first.

```c
#include <stdio.h>
#include <stdlib.h>

int compare(const void *a, const void *b){
    return *(int *)a - *(int *)b;
}

int main(){
    int n, m;
    int g[30000], s[30000];

    scanf("%d", &n);
    for (int i = 0; i < n; i++) scanf("%d", &g[i]);

    scanf("%d", &m);
    for (int i = 0; i < m; i++) scanf("%d", &s[i]);

    qsort(g, n, sizeof(int), compare);
    qsort(s, m, sizeof(int), compare);

    int i = 0;
    int j = 0;

    while (i < n && j < m){
        if (s[j] >= g[i]) i++;
        j++;
    }

    printf("%d\n", i);
    return 0;
}
```

### Problem 3: Minimum Burnout Calories
To minimize the distance penalty run formula $\sum (3^i \times c)$, the largest calorie count values must be consumed first ($i=0$) to limit exponential scaling factors.

```c
#include <stdio.h>
#include <math.h>

int main(){
    int n;
    scanf("%d", &n);
    int arr[n];

    for(int i = 0; i < n; i++){
        scanf("%d", &arr[i]);
    }
    
    // Sort calories in descending order
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] < arr[j + 1]) {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
    
    int s = 0;
    for(int i = 0; i < n; i++){
        s += (pow(3, i)) * arr[i]; // Based on the standard 3^i * c multiplier rules
    }
    printf("%d", s);
    return 0;
}
```

### Problem 4: Maximize Array Index Product
Maximizes the value of $\sum (\text{arr}[i] \times i)$ by sorting the sequence elements in ascending order so that the largest values are multiplied by the largest index markers.

```c
#include <stdio.h>
#include <stdlib.h>

int compare(const void *a, const void *b)
{
    return *(int *)a - *(int *)b;
}

int main(){
    int n;
    scanf("%d", &n);
    int arr[n];
    for(int i = 0; i < n; i++) scanf("%d", &arr[i]);

    qsort(arr, n, sizeof(int), compare);

    int total = 0;
    for(int i = 0; i < n ;i++){
        total += arr[i] * i;
    }

    printf("%d", total);
    return 0;
}
```

### Problem 5: Minimum Product Sum of Pairs
Given two arrays of equal size $N$, this algorithm finds the minimum value of $\sum (A[i] \times B[i])$ by sorting the first array in ascending order and the second array in descending order.

```c
#include <stdio.h>
#include <stdlib.h>

int compare(const void *a, const void *b)
{
    return *(int *)a - *(int *)b;
}

int compareDescending(const void *a, const void *b)
{
    return *(int *)b - *(int *)a;
}

int main(){
    int n;
    scanf("%d", &n);
    int arr1[n], arr2[n];
    for(int i = 0; i < n; i++) scanf("%d", &arr1[i]);
    for(int i = 0; i < n; i++) scanf("%d", &arr2[i]);

    qsort(arr1, n, sizeof(int), compare);
    qsort(arr2, n, sizeof(int), compareDescending);

    int total = 0;
    for(int i = 0; i < n; i++){
        total += arr1[i] * arr2[i];
    }

    printf("%d", total);
    return 0;
}
```

---

## 📋 Compilation and Verification

Build any target project problem locally using standard terminal commands:

```bash
# Compile target problem solution file
gcc problem2.c -o greedy_runner

# Execute program with test criteria
./greedy_runner
```
