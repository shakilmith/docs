# Java Stream

In java, Stream operations are composed into a pipeline, through which data will flow and it provides predefined functions to operate on the data.

The package **java.util.stream.*;** provides few interfaces and classes to work with stream.

A stream pipeline consists of three things.

**1) A data source:** A data source can be an Array, A collection (List, Set, Map..), a generator function, an I/O channel etc.

**2) Zero or more intermediate operations:** It transforms a stream into another stream consisting of the results.
The useful intermediate operations are:
¡) map():
¡¡) filter():
¡¡¡) sorted():
¡v) distinct():
v) limit():
v¡) skip():

**3) Terminal:** It is the last part of a stream operation and should be written at last. It produces the result or side effects. But there is only one terminal operation possible in a stream.

The useful terminal operations are:
i) **collect()**
ii) **forEach()**
iii) **reduce()**
iv) **count()**
v) **findFirst()**
vi) **findAny()**
vii) **Max()/Min()**
viii) **toArray()**
ix) **anyMatch()**
etc.

**Note:** Streams are lazy; computation on the source data is only performed when the terminal operation is initiated/called, and source elements are consumed only as needed.

Remember that, a stream can not be reused means it should be operated on (invoking an intermediate or terminal stream operation) only once.

Stream pipelines may execute either sequentially or in parallel. Streams are created with an initial choice of sequential or parallel execution. (For example, **Collection.stream()** creates a sequential stream, and Collection.parallelStream() creates a parallel one.)

### Java Stream examples

Let's create a List of integer data and invoke the mechanism of stream in it.

### Returns a stream of data without using an intermediate operations.

```
import java.util.List;
import java.util.stream.Collectors;

public class Main{
  public static void main (String[] args) {
    
    //create list of integer data 
    List numbers = List.of(1, 2, 3, 4, 5);
    
    //returns a list using stream()
    List result = numbers.stream().collect(Collectors.toList());
    
    //print the stream result
    System.out.println(result); //returns array of list
  }
}
/**
 * Output:
 * [1, 2, 3, 4, 5]
 */
```

### Create a List of Integer and multiply each elements by 2

```
import java.util.List;
 import java.util.stream.Collectors;
 
 public class Main{
   public static void main (String[] args) {
     
     //creating list of integer 
     List numbers = List.of(1, 2, 3, 4, 5);
    
    //returns a list of stream
     List result = number.stream()
     .map(x -> x*2) //lambda expression as function
     .collect(Collectors.toList());
     
     //print the result
     System.out.println(result);
   }
 }
 
 /**
  * Output:
  * [2, 4, 6, 8, 10]
  */
```

### Create a List of integer and returns the result of square and cube of each elements

For achieving this we must use intermediate operator like map() and inside the parentheses we use lambda expression as function. We can say it computational operation as well.

```
import java.util.List;
 import java.util.stream.Collectors;
 
 public class Main{
   public static void main (String[] args) {
     
     //creating list of integer 
     List numbers = List.of(1, 2, 3, 4, 5);
    
    //returns square of the elements
     List squareResult= numbers.stream()
     .map(x -> x*x) //lambda expression as function
     .collect(Collectors.toList()); //returns a result as list
     
     //returns cube of the elements
     List cubeResult= numbers.stream()
     .map(x -> x*x) //lambda expression as function
     .collect(Collectors.toList()); // returns a result as list
     
     
     //print the results of the stream
     System.out.println(squareResult);
     System.out.println(cubeResult);
   }
 }
 
 /**
  * Output:
  * [1, 4, 9, 16, 25]
  * [1, 8, 27, 64, 125]
  */
```

## Using forEach() loop

**collect(Collectors.toList())** returns an ArrayList overall. But for iterating the elements of a collections we can use forEach() loop as a terminal operation in a stream.

```
import java.util.List;
import java.util.stream.Collectors;

public class Main{
  public static void main (String[] args) {
    
    List number = Arrays.asList(1, 2, 3, 4, 5);
    List  result =
    number.stream()
    .map(x -> x*x )
    .collect(Collectors.toList());
    
    System.out.println("Print the stream result using forEach loop");
    
    result.forEach(number -> System.out.println(number);)
  }
}
/**
 * Output:
 * 1
 * 2
 * 3
 * 4
 * 5
 */
```

The above one can also be written like this: (we can also use here method reference instead of lambda expression)

```
import java.util.List;
import java.util.stream.Collectors;

public class Main{
  public static void main (String[] args) {
    
    List numbers = List.of(1, 2, 3, 4, 5);
    //print the result using forEach loop
    numbers.stream.forEach(System.out::println);
  }
}
/**
 * Output:
 * 1
 * 2
 * 3
 * 4
 * 5
 */
```


### Let's modify the above example using the intermediate map() and filter() operations together.

Note: the filter() intermediate method needs a predicate to perform operations on the elements of the list. (It's should be boolean expression or more concisely we can say it is used to provide certain condition over elements of the current Collections)

```
import java.util.List;
import java.util.stream.Collectors;

public class Main{
  public static void main (String[] args) {
    
    List numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
    //print the result using forEach loop
    numbers.stream.map(x -> x*x).filter(y -> y > 50).forEach(System.out::println);
  }
}
/**
 * Output:
 * 64
 * 81
 * 100
 */
```

Here, things you should remember while using stream,

**map():** It is an intermediate operation. It returns a stream consisting of the results of applying the given function (lambda expression..) to the elements of the current stream.

**filter():** It is also an intermediate operation of a stream. It returns a stream consisting of the elements of the current stream that match the given predicate (provides certain condition over elements).

**forEach():** It is a terminal operation, can be written only once. It helps to iterate the computational elements of the current stream and returns the result.

### Filter the current list using filter() method

In this example we return a result that contains certain characters using filter() method of a stream.

```
import java.util.List;
import java.util.stream.*;

public class Main{
  public static void main (String[] args) {
    
    List languages = List.of("C++", "Java", "Ruby", "Python", "Rust");
    //print the result using forEach loop
    numbers.stream.filter(r -> r.startsWith("R")).forEach(System.out::println);
  }
}
/**
 * Output:
 * Ruby
 * Rust
 */
```

### Using count() method

Let's calculate the how many elements we have in our predefined collection...

```
import java.util.List;
import java.util.stream.*;

public class Main{
  public static void main (String[] args) {
    
    List numbers= List.of(10, 20, 30, 40, 50);
    //count the elements of the stream
    System.out.println("Total elements of this list are: "+numbers.stream().count()); //output 5
    
    //storing total elements number in a variable
    long totalElements= numbers.stream().count();
    System.out.println("Total elements of this list are: "+totalElements); //output 5
  }
}
```

When you execute the above code, the following output you will get:

Total elements of this list are: 5 Total elements of this list are: 5

## Print the distinct elements of a List

```
import java.util.List;
import java.util.stream.*;

public class Main{
  public static void main (String[] args) {
    
    List numbers= List.of(1, 2, 3, 2, 5, 1);
    
    //Print only the distinct elements number of the list (non similar)
    
    long countDistinct = numbers.stream().distinct().count();
    
    System.out.println("Total distinct  elements of this list are: "+countDistinct); // 4 (duplicate excluded)
  };
}
/**
 * Output: 
 * Total distinct elements of this list are: 4
 */
```

### Print the summation and average using stream sum() method for the provided list.

Let's first of all, we see how we can print the summation of given list of numbers or Integers without using stream **sum()** method. (Yes, we have to write down few more lines of code!)


```
import java.util.*;

public class Main{
  public static void main (String[] args) {
    
    List numbers = List.of(10, 20, 30, 40, 50);
    
    //using iterator to access the elements 
    
    Iterator itr = numbers.iterator();
 

        int summation = 0;

        while (itr.hasNext()) {

            int number = itr.next();
 

            // adding the elements greater than 5

            if (number > 5) {

                summation += number;

            }

        }
        System.out.println("Summation of given list: "+summation);
  };
}
/**
 * Summation of given list: 150
 */
```

The above program could be replaced by the following one.

```
import java.util.*;
import java.util.stream.*;

public class Main{
  public static void main (String[] args) {
    
    List numbers = List.of(10, 20, 30, 40, 50);
    // create a stream of integers
    // filter the stream
    // add the integers
   long summation = numbers.stream().filter(x -> x > 5)
    .mapToInt(x -> x)
    .sum();
  
    //print the summation
    System.out.println("Summation of given list: "+summation);
  };
}
/**
 * Summation of the given list: 150
 */
```

Likewise the above program, it is also possible to get the average of given list of numbers. Here we will use the average() method but it's type is double, thus we convert the Integer to Double by **mapToDouble()** method including method reference.

```
import java.util.*;
import java.util.stream.*;

public class Main{
  public static void main (String[] args) {
    
    List numbers = List.of(10, 20, 30, 40, 50);
    
    double average = numbers.stream()
      .mapToDouble(Integer::doubleValue) //convert Integer to Double 
      .average() //return average
      .orElse(0.0); //prints it if no average found 
      
      //print the average number
    System.out.println("Average of the given numbers : " + average);
    
  };
}
/**
 * Average of the given numbers: 30.0
 */
```

