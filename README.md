# JavaInterviewQuestions

## In Java strings are?
- [ ] Mutable
- [x] Immutable

## Is String a primitive type in Java?
- [ ] Yes
- [x] No

## What is the difference between StringBuilder and StringBuffer?
| StringBuffer     | StringBuilder    |
| ---------------- | ---------------- |
| Thread Safe      | Not Thread Safe  |
| Synchronized     | Not Synchronized |
| Slower           | Faster           |

## Write a code to create a custom immutable class.
- Class must be declared as final.
- Data members in the class must be declared as private.
- Data members in the class must be declared as final.
- Use parameterized constructor.
- Use getter methods for data members.
- Don't use setter methods for data members.
```java
// 1. Class must be declared as final. [Reason : So that child class can't be created]
public class Employee {

    // 2. Data members in the class must be declared as private. [Reason : So that direct access is not allowed]

    // 3. Data members in the class must be declared as final. [Reason : We can't change the value of it after object creation]
    private final String name;
    private final int age;
    private final int salary;

    // 4. Introduce parameterized constructor. [Reason : All the final data members must initialize under parameterized constructor]

    Employee(String name,int age,int salary) {
        this.name = name;
        this.age = age;
        this.salary = salary;
    }

    // 5. Don't provide setter methods for data members. Only getter method should be allowed.
    public int getAge() {
        return this.age;
    }

    public String getName() {
        return this.name;
    }

    public int getSalary() {
        return this.salary;
    }
}
```

## Can we create an object of an Abstract class?
- [ ] Yes
- [x] No

## Can we declare abstract constructor or abstract static methods?
- [ ] Yes
- [x] No

## Can we create a reference to an abstract class so that it can be used to point to a subclass object?
- [x] Yes
- [ ] No

## Abstract Classes - Which of the following is true?
* Abstract classes should necessarily have abstract methods.
* Classes having abstract methods should be abstract.
- [ ]  Both are correct.
- [ ]  Both are incorrect.
- [ ]  i is correct, ii is incorrect.
- [x]  i is incorrect, ii is correct.
  
## Which keyword is used to make a non-inheritable class in Java?
- [ ]  static.
- [ ]  abstract.
- [x]  final.
- [ ]  finally.

## What is Marker Interface?
A marker interface is an interface that **doesn’t have** any **methods** or **constants** inside it.
It provides **run-time** type information about the objects. So the compiler and JVM have additional information about the object.

## Name some built in marker interface in Java.
- Serializable.
- Cloneable.
- Remote.

## Difference Between Aggregation and Composition.
| Aggregation                                                     | Composition                                               |
| --------------------------------------------------------------- | --------------------------------------------------------- |
| Weak Association.                                               | Strong Association.                                       |
| Classes in relation can exist independently.                    | One class is dependent on Another Independent class.      |
| One class **has-a** relationship with another class.            | Once class **belongs-to** another class.                  |
| Helps with code reusability. Since classes exist independently. | Code is not that reusable as the association is dependent.|

## Executors and callables. - Which of the following is correct?
* Executor manages the assignment of tasks  to threads within the thread pool. 
* Waiting Queue holds the tasks that couldn't be assigned to threads in the thread pool.
- [x]  Both a and b are true.
- [ ]  Only a is true.
- [ ]  Only b is true.
- [ ]  Both a and b are false.

## Executors and callables. - Which of the following is correct?
* ExecutorService.submit returns a Future object. 
* The method name to receive a value from Future object is get.
- [x]  Both a and b are true.
- [ ]  Only a is true.
- [ ]  Only b is true.
- [ ]  Both a and b are false.

## Executors and callables. - Which of the following is correct?
* The responsibility of the Executor is to decide how to run different tasks on different threads.
* The responsibility of class implementing Callable is to do define a task to be done on a separate thread.
- [x]  Both a and b are true.
- [ ]  Only a is true.
- [ ]  Only b is true.
- [ ]  Both a and b are false.

## Runnable vs Callable. - Which of the following is correct?
* Runnable interface is used to create classes that run on a separate thread and return values to the main thread.
* Callable interface is used to create classes that run on a separate thread and don’t need to return values to the main thread.
- [ ]  Both a and b are true.
- [ ]  Only a is true.
- [ ]  Only b is true.
- [x]  Both a and b are false.

## Callables. - Which of the following is correct?
* A class implementing Callable<Integer> will have a call function that returns Integer.
* To get a value from a class implementing Callable<Integer>, we can use Future<Integer>.
- [x]  Both a and b are true.
- [ ]  Only a is true.
- [ ]  Only b is true.
- [ ]  Both a and b are false.
  
## Threads with Callables.
* Write code to achieve the following.
  - A class Client with a main method.
  - Create a class ArrayCreator which takes as input a number (n)
  - ArrayCreator should create an ArrayList which should contain numbers from 1 to n
  - ArrayCreator should implement appropriate Callable interface and return the arraylist discussed above to calling thread
  - Client class should invoke ArrayCreator over a new thread and get the arraylist from ArrayCreator class and print it.

**ArrayCreator.java**
```java
import java.util.ArrayList;
import java.util.*;
import java.util.concurrent.Callable;

public class ArrayCreator implements Callable<List<Integer>> {
    int number;

    ArrayCreator(int number) {
        this.number = number;
    }

    @Override
    public List<Integer> call() {
        List<Integer> listOfNumbers = new ArrayList<>();
        for (int i = 1; i <= number; i++) {
            listOfNumbers.add(i);
        }
        return listOfNumbers;
    }
}
```

**Client.java**
```java
 public class Client {
    public static void main(String args[]) throws ExecutionException, InterruptedException {
        ExecutorService service = Executors.newSingleThreadExecutor();
        Scanner scanner = new Scanner(System.in);
        int number = scanner.nextInt();
        ArrayCreator arrayCreator = new ArrayCreator(number);
        Future<List<Integer>> list = service.submit(arrayCreator);
        List<Integer> result = list.get();
        System.out.println(result.toString());
        service.shutdown();
    }
}
```

## Serialization and Deserialization.
- Serialization is the process of converting the **state** of an object to a **byte stream.**
- Deserialization is the **reverse** of serialization and converts the **byte stream** back to the **original object**.
- Only **non-static** data members get serialized.
- A class must implement **Serializable** interface to be eligible for serialization.
- **ObjectOutputStream** class helps to serialize an object.
- **ObjectInputStream** class helps to deserialize an object.
- Java **transient** keyword helps to prevent a particular field from being serialized.
- While converting the **byte stream** back to the **original object**, the **constructor** of the object is not called.
- **Serializable** interface has no methods or fields of it’s own.
- If the parent class has already implemented the **Serializable interface**, in that case a child class doesn’t have to implement it.
- **Serializable** interface must be implemented by all **associated** objects.

