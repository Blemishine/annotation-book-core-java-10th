#  Chapter 1: The Java SE 8 Stream Library   Java SE 8的流库 

# Contents

[代码讲解](#code)


# references 
 

IBM developerWorks [Java 8 中的 Streams API 详解](https://www.ibm.com/developerworks/cn/java/j-lo-java8streamapi/)

Java 8 文档中对 stream 包的说明 [java.util.stream (Java Platform SE 8 )](https://docs.oracle.com/javase/8/docs/api/java/util/stream/package-summary.html)

[CarpenterLee/JavaLambdaInternals: 深入理解Java函数式编程和Streams API](https://github.com/CarpenterLee/JavaLambdaInternals)



# key-word

 “what, not how”  做什么 而非如何做
 

# code 

[CollectingIntoMaps](../src/main/v2ch01/collecting/CollectingIntoMaps.java)
 
[Collectors](#Collectors)  [toMap](#toMap)

 
 
 
 


# Collectors

[Collectors (Java Platform SE 8 )](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Collectors.html)

public final class Collectors
extends Object

Implementations of Collector that implement various useful reduction operations, such as accumulating elements into collections, summarizing elements according to various criteria, etc.

实现各种有用的约简操作的收集器的实现，例如将元素累积到集合中，根据各种标准汇总元素等。

The following are examples of using the predefined collectors to perform common mutable reduction tasks:

以下是使用预定义收集器执行常见的可变减少任务的示例：


     // Accumulate names into a List
     //将名称累积到List中
     List<String> list = people.stream().map(Person::getName).collect(Collectors.toList());

     // Accumulate names into a TreeSet
      //将名称累积到TreeSet中
     Set<String> set = people.stream().map(Person::getName).collect(Collectors.toCollection(TreeSet::new));

     // Convert elements to strings and concatenate them, separated by commas
      //将元素转换为字符串并将它们连接起来，用逗号分隔
     String joined = things.stream()
                           .map(Object::toString)
                           .collect(Collectors.joining(", "));

     // Compute sum of salaries of employee
       //计算员工工资总额
     int total = employees.stream()
                          .collect(Collectors.summingInt(Employee::getSalary)));

     // Group employees by department
     //按部门分组员工
     Map<Department, List<Employee>> byDept
         = employees.stream()
                    .collect(Collectors.groupingBy(Employee::getDepartment));

     // Compute sum of salaries by department
      //按部门计算工资总额
     Map<Department, Integer> totalByDept
         = employees.stream()
                    .collect(Collectors.groupingBy(Employee::getDepartment,
                                                   Collectors.summingInt(Employee::getSalary)));

     // Partition students into passing and failing
         //将学生分成传球和失败
     Map<Boolean, List<Student>> passingFailing =
         students.stream()
                 .collect(Collectors.partitioningBy(s -> s.getGrade() >= PASS_THRESHOLD));

 

Since:
    1.8 
    
# Collectors.toMap

    toMap

    public static <T,K,U,M extends Map<K,U>> Collector<T,?,M> toMap(Function<? super T,? extends K> keyMapper,
                                                                    Function<? super T,? extends U> valueMapper,
                                                                    BinaryOperator<U> mergeFunction,
                                                                    Supplier<M> mapSupplier)
  
     

  Returns a Collector that accumulates elements into a Map whose keys and values are the result of applying the provided mapping functions to the input elements.    

  If the mapped keys contains duplicates (according to Object.equals(Object)), the value mapping function is applied to each equal element, and the results are merged using the provided merging function. The Map is created by a provided supplier function.    

  Implementation Note:    
    The returned Collector is not concurrent. For parallel stream pipelines, the combiner function operates by merging the keys from one map into another, which can be an expensive operation. If it is not required that results are merged into the Map in encounter order, using toConcurrentMap(Function, Function, BinaryOperator, Supplier) may offer better parallel performance.    
    Type Parameters:    
        T - the type of the input elements    
        K - the output type of the key mapping function    
        U - the output type of the value mapping function    
        M - the type of the resulting Map    
    Parameters:    
        keyMapper - a mapping function to produce keys    
        valueMapper - a mapping function to produce values    
        mergeFunction - a merge function, used to resolve collisions between values associated with the same key, as supplied to Map.merge(Object, Object, BiFunction)    
        mapSupplier - a function which returns a new, empty Map into which the results will be inserted    
    Returns:    
        a Collector which collects elements into a Map whose keys are the result of applying a key mapping function to the input elements, and whose values are the result of applying a value mapping function to all input elements equal to the key and combining them using the merge function
    See Also:    
        toMap(Function, Function), toMap(Function, Function, BinaryOperator), toConcurrentMap(Function, Function, BinaryOperator, Supplier)    

返回一个收集器，它将元素累积到一个Map中，其键和值是将提供的映射函数应用于输入元素的结果。    

   如果映射的键包含重复项（根据Object.equals（Object）），则将值映射函数应用于每个相等的元素，并使用提供的合并函数合并结果。地图由提供的供应商功能创建。    

  实施说明：    
   返回的收集器不是并发的。对于并行流管道，组合器功能通过将键从一个映射合并到另一个映射来操作，这可能是昂贵的操作。如果不需要将结果合并到遇到顺序的Map中，则使用toConcurrentMap（函数，函数，BinaryOperator，供应商）可以提供更好的并行性能。    
    类型参数：    
        T - 输入元素的类型    
        K - 键映射函数的输出类型    
        U - 值映射函数的输出类型    
        M - 结果Map的类型    
    参数：    
        keyMapper - 用于生成密钥的映射函数    
        valueMapper - 用于生成值的映射函数    
        mergeFunction - 一个合并函数，用于解决与同一个键关联的值之间的冲突，如提供给Map.merge（Object，Object，BiFunction）    
        mapSupplier - 一个函数，它返回一个新的空Map，结果将插入其中    
    返回：    
        收集器将元素收集到Map中，其键是将键映射函数应用于输入元素的结果，其值是将值映射函数应用于与键相等的所有输入元素并使用合并将它们组合的结果功能    
    也可以看看：    
        toMap（函数，函数），toMap（函数，函数，BinaryOperator），toConcurrentMap（函数，函数，BinaryOperator，供应商）        