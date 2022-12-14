## Константы в Java
## 1. Что является константой в Java?
Поля класса со спецификатором final являются константами и не могут быть изменены после инициализации. Константу не обязательно инициализировать сразу же, это можно сделать и позже, но значение присвоенное первым так и останется навсегда.
    Константами в Java принято называть public static final переменные класса.
    Для Java констант принято соглашение объявлять их имена в верхнем регистре, слова разделяются символом подчеркивания – MY_CONSTANT.
    (public/private) static final type SPECIFIC_NAME = VALUE
    Тип Immutable - состояние его объектов изменить невозможно. При присвоении нового значения, создается новый объект. (Объекты обертки – Integer, Boolean, BigInteger и т.д., а также java.lang.StackTraceElement)
## 12.2. Что такое enum?
Перечисления представляют набор логически связанных констант. Объявление перечисления происходит с помощью оператора enum, после которого идет название перечисления. Затем идет список элементов перечисления через запятую:

enum Day {
MONDAY,
TUESDAY,
WEDNESDAY,
THURSDAY,
FRIDAY,
SATURDAY,
SUNDAY
}

Перечисления, как и обычные классы, могут определять конструкторы, поля и методы.
## 12.3. Правила использования enum
Все перечисления в Java неявно расширяют java.lang.Enum класс, который расширяет класс Object и реализует Serializable и Comparable интерфейсы, так что Enum не может наследовать классы.
Нельзя заканчивать имя пакета словом enum, например, com.javadevblog.enum —  недопустимое имя пакета.
Перечисления в Java могут реализовывать интерфейсы. (На пример есть Enum,
который реализовывает интерфейс Closeable.
Enum конструкторы в Java всегда private.
Нельзя создать экземпляр перечисления, используя оператор new.
Мы можем создавать абстрактные методы в Enum, поэтому все поля Enum должны реализовывать абстрактный метод. (В приведенном выше примере метод getDetail() является абстрактным и все поля в Enum реализовали его.
Мы можем определить метод в Enum, а поля могут переопределять их.
Все поля в Enum имеют пространство имен, поэтому мы можем использовать поле только с именем класса: ThreadStates.START
Перечисления могут быть использованы в switch. Пример использования увидим чуть позже в этом уроке.
Мы можем изменять существующее перечисление не нарушая существующей функциональности. Например, мы можем добавить новое поле NEW в ThreadStatesClass и это никак не повлияет на существующую функциональность.
Хорошим тоном считается написание большими буквами и нижнее подчеркивание для пробелом. Например, EAST, WEST, EAST_DIRECTION и т.д.
Enum константы неявно static и final
Enum константы являются final, но ее можно изменять. Например, мы можем использовать метод setPriority(), чтобы изменить приоритет констант в Enum. (Мы увидим его на практике в примере ниже).
Мы может безопасно сравнивать константы с помощью «==» и метода equals(). Они оба будут давать тот же результат.
## 12.4. Преимущества использования enum
– enum может наследовать интерфейсы, но не может наследовать другой класс. Это одно из больших преимуществ: он гарантирует, что всегда существует только тот набор значений, который определен в enum , и не более.
– enum правильно обрабатывает сериализацию. Это гарантирует, что e1.equals(e2) всегда подразумевает e1 == e2 для любых двух значений enum e1 и e2.
– Существуют специальные облегченные структуры данных, которые обрабатывают enums: EnumSet и EnumMap.
