```java

//новый класс JvmComprehension для загрузки в систему загрузчиков классов через ClassLoaders, 
//в котором   JvmComprehension поочередно на ClassLoaders, делегирующих загрузку классов - разных уровней: 
//Bootstrap ClassLoader, Platform ClassLoader, Application ClassLoader. В результате, класс JvmComprehension 
//перемещается в Metaspace, область памяти хранения мета-информации, для сохранения данных о нем самом.

public class JvmComprehension {

 //в момент вызова метода main () в стеке создается фрейм для данного метода
  
    public static void main(String[] args) {
        int i = 1;                      // 1 - в фрейме метода main () создается и помещается целочисленная переменная i со значением равном 1 (единице)
        Object o = new Object();        // 2 - - в фрейме метода main () создается и помещается переменная o, хранящая в себе ссылку  на  объект new Object, 
                                        // который создается и хранится в куче
        Integer ii = 2;                 // 3 - в фрейме метода main () создается и помещается переменная ii, хранящая в себе ссылку  на  объект Integer 
                                        // равный 2 (двум), который создается и хранится в куче
        printAll(o, i, ii);             // 4 - в стеке создается фрейм printAll, в котором  записываются переменные i, o и ii
        System.out.println("finished"); // 7 - в стеке создается фрейм для метода  println(), в который помещается ссылка из кучи на объект String со 
                                        // значением finished и после извлечения которой метод main () удаляется из стека
    }
    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   // 5 - в фрейме метода printAll () создается и помещается переменная uselessVar, хранящая в себе ссылку 
                                                    // на  объект Integer равный 700 (семьсот), который создается и хранится в куче
        System.out.println(o.toString() + i + ii);  // 6 - в стеке создается фрейм для метода  println(), в котором формируется и помещается в кучу результат 
                                                    // выражения через созданный фрейм toString() с переданными переменными i, o и ii
    }
}

// Выполнение кода программы построчно, методы поочередно компилируются машинный код, интерпретатор интерпретирует машинный код построчно и затем выполняет, 
// периодически происходит остановка программы и сборка мусора.

```
