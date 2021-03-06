# Разбор работы JVM на примере
---
## Код

```java
public class JvmComprehension {
    public static void main(String[] args) {
        int i = 1;                      // 1
        Object o = new Object();        // 2
        Integer ii = 2;                 // 3
        printAll(o, i, ii);             // 4
        System.out.println("finished"); // 7
    }
    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   // 5
        System.out.println(o.toString() + i + ii);  // 6
    }
}
```
## Порядок работы
0)Изначально отрабатывают ClassLoader'ы - в метаспейс загружаются системные, платформенные классы и класс `JvmComprehension`. Происходят стадии связывания и инициализации. В стек попадает фрейм метод `main`.
1)Во фрейме заводится пременная `i`, ей устанавливается значени 1.
2)В хипе создается объектр типа `Object`, во фрейме `main` cоздается переменная `o`, ей присваивается ссылка на созданный в хипе объект типа `Object`.
3)В хипе создается объектр типа `Integer`, во фрейме `main` cоздается переменная `ii`, ей присваивается ссылка на созданный в хипе объект типа `Integer`.
4)В стек попадает фрейм метода `printAll`. Далее во фрейме заводятся переменные `o`, `i`, `ii`. Им присваиваются значения.
5)В хипе создается объектр типа `Integer`, во фрейме `printAll` cоздается переменная `uselessVar`, ей присваивается ссылка на созданный в хипе объект типа `Integer`.
6)В стек попадает фрейм метода `toString`, где получается значение объекта из переменной `o`. Далее фрейм метода `toString` удаляется из стека и в стек помещается фрейм `println`. В нем выполняется создание строки и вывод в консоль строки. Из стека удалются фрейм `println`, а за ним и `printAll`. Сборщик мусора удаляет объекты удаленных фреймов из хипа.
7)В стек помещается фрейм метода `println`. После выполнения метода из стека удаляются фрейм `println`, а за ним `main`.Сборщик мусора удаляет объекты удаленных фреймов из хипа.