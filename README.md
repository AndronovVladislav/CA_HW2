# CA_HW2

# Пункт 1
Программа запускается и завершается при корректных данных.
# Пункт 2
Набор {2, 1, 5, -12, 3, -9} сортируется правильно.
# Пункт 3
Неисправность была обнаружена на наборе {5, 4, 3, 2, 1}.

![image](https://user-images.githubusercontent.com/97717897/190877090-030f118f-30b6-41c9-a84f-a46df7722c83.png)
# Пункт 5
Ошибка состояла в передаче в качестве аргумента в функцию сортировки argc в качестве параметра size, что неверно, так как _argc_ - размер массива _argv_, который хранит название программы. Тестирование проводилось на наборах {5, 4, 3, 2, 1} и {5, 543, 0, -10, 5, 5}.
![image](https://user-images.githubusercontent.com/97717897/190876997-4215925f-09b4-4f96-b651-cd07408d081d.png)

```
/* shell-sort.c - Сортировка Шелла */

#include <stdio.h>
#include <stdlib.h>

static void shell_sort(int a[], int size) {
  int i, j;
  int h = 1;

  do {
    h = h * 3 + 1;
  } while (h <= size);

  do {
    h /= 3;
    for (i = h; i < size; i++) {
      int v = a[i];
      for (j = i; j >= h && a[j - h] > v; j -= h) {
        a[j] = a[j - h];
      }
      if (i != j) {
        a[j] = v;
      }
    }
  } while (h != 1);
}

int main(int argc, char *argv[]) {
  int *a;
  int i;

  a = (int *)malloc((argc - 1) * sizeof(int));
  for (i = 0; i < argc - 1; i++) {
    a[i] = atoi(argv[i + 1]);
  }
  shell_sort(a, argc);
  printf("Output: ");
  for (i = 0; i < argc - 1; i++) {
    printf("%d ", a[i]);
  }
  printf("N\n");
  free(a);
  return 0;
}
```
