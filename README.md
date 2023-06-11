# JavaInterviewQuestions

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
