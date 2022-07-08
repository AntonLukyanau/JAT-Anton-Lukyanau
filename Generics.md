## 1 In which version of Java did parameterized types appear?
Parameterized types appeared in Java version 5.

## 2 Give 2 code examples: the first without a parameterized type; the second is the same code with a parameterized type, illustrating the advantage of this option.
    List list = new ArrayList();
    list.add("hello");
    String s = (String) list.get(0);
Advantage: using a parameterized type, the code does not require casting:

    List<String> list = new ArrayList<String>();
    list.add("hello");
    String s = list.get(0);

## 3 What types of data are prohibited as class parameters?
Primitive types.

## 4 The code is given:
    class Gen <T1, T2 extends Number, T3 extends Object> { … }

What types can be used as arguments T1, T2, T3?

T1 - any, T2 - Number and its subclasses (Byte, Short, Integer, Long, Float, Double), T3 - any (subclass Object - all objects).

## 5 Given the code:
    class Gen1 <T> { … }
    class Gen2 <T extends Object> { … }
    class Runner {
    private final static Gen1<Object> g11 = new Gen 1<>();
    private final static Gen1 g12 = new Gen1();
    private final static Gen2<Object> g21 = new Gen2<>();
    private final static Gen2 g22 = new Gen2();
    ...
    }

What is the difference between Gen1 and Gen2 class declarations?
Is there an advantage in declaring g11 over g12? Justify the answer.
Is there an advantage in declaring g21 over g12? Justify the answer.
In which case is the second method used (g12, g22)?
___
There is no difference in Gen1 and Gen2. In both cases, the Java compiler, as a result of type erasure, will replace T with Object.
g12 and g22 are raw types. The advantages in declaring g11 and g21 are that when using g12 and g22, the type checking option is lost, i.e. the type safety is lost. The second method is used if you need to ensure compatibility with code written before the introduction of parameterized types in Java.You should also use raw types in literal lxx constants or literals, for example: List.class it is allowed to use, but List<String>.class is not.
Also, raw types are used with the instanceof operator.

## Why can't I call a generic-type constructor?
The compiler does not know which constructor can be called and how much memory should be allocated when creating an object.

## 7 Why can't a static method have a generic parameter?
A static method in ordinary classes can have a generic parameter. An example from the Oracle tutorial.

    public static <K, V> boolean compare(Pair<K, V> p1, Pair<K, V> p2) {
    return p1.getKey().equals(p2.getKey()) &&
    p1.getValue().equals(p2.getValue());
    }

In parameterized classes, static methods cannot have generic parameters, because a static method belongs to the entire class, not to a specific instance of the class. Therefore, when referring to a static method, it would be unclear which type to use.
