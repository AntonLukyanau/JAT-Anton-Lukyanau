## 1. What are exceptions?
The term exception is an abbreviation for the phrase "exceptional event". An exception is an event that occurs during the execution of a program, which leads to a violation of the normal flow of program instructions.
## 2. What actions does the runtime system perform when an exception occurs?
Answer. The runtime system searches the call stack for a method containing a block of code that can handle an exception. The search starts with the method in which the error occurred and continues through the call stack in the reverse order in which the methods were called.
## 3. What is the name of the block of code that handles the exception?
Answer. Exception handler.
## 4. How is the "Catch or Specify" requirement implemented?
Answer. The code that can throw a specific exception should:
1) or be enclosed in a try block with further exception handling;
2) either the method that throws an exception must contain a throws declaration that lists exceptions.
   Code that does not meet the "Catch or Point" requirements will not compile.
## 5. What three types of exceptions can be distinguished?
Answer.
1) Checked exceptions are exceptional situations that a well–written application should expect and recover from. Checked exceptions are subject to Catch or Specify requirements.
2) Errors are exceptional situations external to the application that the application cannot anticipate or recover. Errors do not fall under the Catch or Specify requirements.
3) Run–time exceptions (RuntimeException) are exceptional situations that are internal to the application, and which the application usually cannot expect or recover. They usually indicate programming errors, such as logical errors or incorrect API usage. Runtime exceptions are not subject to Catch or Specify requirements. The application can catch this kind of exception, but it probably makes sense to fix the error that caused the exception to occur.
## 6. What types of exceptions are unverifiable?
 Errors and runtime exceptions.
## 7. What components can be included in the exception handler?
The exception handler can contain three components – the try, catch and finally blocks.
## 8. For what situations is the try-with-resources operator used?
Answer. The try-with-resources statement is especially suitable for situations that use Closeable resources, such as threads. In case of an exception, this operator is guaranteed to automatically close all threads.
## 9. What code is in the try block?
Answer. A section of code that can cause an exception.
## 10. Is the entire code of the try block executed in case of an exception?
Answer. When an exception occurs, the runtime immediately stops executing the try block on the line that caused the exception. Executed method calls remain incomplete. The executing system starts searching for the appropriate exception handler.
## 11. Can only one try block be used (without catch or finally)?
Answer. No, the try block is not used separately.
## 12. What is the purpose of the catch block?
Answer. The catch block is an exception handler. It handles the type of exception that is specified by its argument. Catch contains code that is executed if and when an exception handler is called.
## 13. How many catch blocks can be contained after the try statement?
Answer. Any number.
## 14.If several catch blocks are used, in what order are they called in case of an exception?
Answer. The execution system calls catch blocks in the order in which they appear after the try statement. However, the catch block that contains the corresponding exception type is executed. 
## 15. Can a catch block be used without a try block?
Answer: No. The catch block necessarily follows the try block.
## 16. How many types of exceptions can one catch block handle?
Answer. In Java SE 7 and later, a single catch block can handle multiple types of exceptions. This feature can reduce code duplication and reduce the temptation to catch an exception that is too wide.
In this case, in the catch block, the types of exceptions that the block can handle are specified through a vertical line ( | ).
## 17. If there is no exception in the try block, is the catch block executed?
Answer. If there are no exceptions in the try block, the runtime system transfers control to the finally block (if any). The catch block is skipped.
## 18.What is the finally block used for?
Answer. The finally block is always executed. This block is guaranteed to be executed even in case of an unexpected exception. The runtime system always executes the code inside finally regardless of what happens inside the try block. Finally is a key tool for preventing resource leaks and restoring an application.
## 19. Can try-finally blocks be used without a catch block?
Answer. Yes, they can. After exiting the try block, the finally block is executed, which can take over the catch functions or optimize the code.
## 20. Which operator can be used instead of try-with-resources?
Answer. The finally statement will ensure that the resource is closed regardless of whether the try block completes normally or with an exception. The finally operator can be used instead of try-with-resources.
## 21.Can the try-with-resources operator be used in conjunction with the finally block?
Answer. The try-with-resources operator can have catch and finally blocks like a regular try operator. In the try-with-resources statement, any catch or finally block is executed after the declared resources have been closed.
## 22. What keyword is used in the method signature to indicate the possibility of throwing an exception by it?
Answer. To indicate that a method can throw an exception, you must use the throws keyword at the end of the method declaration. The throws keyword is declared after the method name and argument list and before the curly brace that defines the scope of the method.
## 23. How many exceptions can a method throw?
Answer. Any number.
## 24. What keyword is used to guarantee throwing an exception?
Answer. An exception is guaranteed to be thrown when using the throw keyword. In this case, the object of the thrown exception is used as an argument.
## 25.Is it possible to create your own exception classes?
Answer. Yes. It is possible to create your own exception classes. This is useful when you want to distinguish between an error that might occur in a custom package and errors that occur in the Java platform or other packages.
## 26.Give examples of the most well-known subclasses of the Exception class.
Answer.
RuntimeException - Exceptions that indicate incorrect use of the API.
IllegalAccessException - Signals that a particular method cannot be found.
IndexOutOfBoundsException - out of bounds for a valid value, such as the size of an array.
NullPointerException - The method is trying to access an object through a null reference.
IOException - Invalid I/O exceptions.
FileNotFoundException - missing file while working with I/O.
## 27.What are chained exceptions?
Answer. An application often reacts to an exception by throwing another exception. Essentially, the first exception throws the second exception. This is the essence of chained exceptions.
## 28. What information is given in the stack trace at the time of the exception?
Answer. The stack trace contains information about the execution history of the current thread and lists the names of classes and methods that were called at the time the exception occurred. The stack trace is a useful debugging tool that you usually use when an exception occurs.
## 29. When is it appropriate to create your own exception class?
Answer.
1) The need to throw a unique exception that is not present in the Java platform.
2) The need to distinguish your exception from the exceptions thrown by classes written by other programmers.
3) Code throws more than one chained exception and should be optimized.
4) The need for independence and autonomy, including with regard to thrown exceptions (working within your package with exceptions).
## 30. Which exception class can be used as a superclass for its own exception?
Answer. The Exception class and its child classes.
## 31. Which exceptions should be made checked, and which unchecked?
Answer. If it is reasonable to expect the client to recover from an exception, then such an exception should be checked. If the client cannot do anything to recover from the exception, the exception must be an unchecked exception.
## 32. What are the benefits of throwing and handling exceptions?
Answer.
1) Separation of the error handling code from the main logic of the program.
2) Propagation of error messages in the method call stack.
3) Grouping and differentiation of exception types.
## 33. Is it possible to throw exceptions in constructors?
Answer. Yes, you can. As usual with the throw keyword.
## 34. Are exceptions transactional?
Answer. Exceptions do not have the transactional property - actions performed in the try block before the exception occurs are not canceled after it occurs.
## 35. Give an example of the most common reusable exceptions and why they are used.
Answer.
1) IllegalArgumentException - Invalid non-null parameter value
2) IllegalStateException - Invalid object state for method call
3) NullPointerException - Unresolved null parameter value
4) IndexOutOfBoundsException - Index parameter out of range
5) ConcurrentModificationException - An illegal concurrent modification of an object was detected
6) UnsupportedOperationException - The object does not support the method
## 36.What is exception translation, when is it used, and what are the rules for its use? Give an example of exception translation.
Answer. If it is not known what to do at this level, a new exception is thrown to the next level. If a method throws an exception that has no apparent connection to the problem being solved, it's confusing. Often this happens when a method passes on an exception thrown by a lower-level abstraction. This not only confuses the programmer, but also pollutes the top-level API with implementation details. If the top-level implementation changes in the next release, the exceptions it throws may also change, causing existing client programs to stop working. To avoid this problem, the upper layers of the application must catch lower-level exceptions and in turn throw exceptions that can be explained in terms of the upper-level abstraction. This idiom is known as exception translation:
  
      try {
    ...
    } catch(LowerLevelException e) {
    throw new HigherLevelException(...);
    }

## 37. How can you avoid using broadcasts and why should you do it?
Answer. Although exception translation is better than meaningless lower-level exception transmission, it should not be abused. Where possible, the best way to handle low-level exceptions is to eliminate their possibility entirely by making sure that the low-level method call succeeds. This can sometimes be achieved by validating the arguments of the top-level method before passing them to the bottom level. If it is not possible to prevent lower layers from throwing exceptions, then the best solution is to have the upper layer silently handle these exceptions, isolating the client from the problems of the lower level. In such circumstances, it is often sufficient to log exceptions using an appropriate logging mechanism such as java.util.logging. This allows the programmer to study the problem while isolating client code and users from it.
## 38. When should translation chaining be preferred?
Answer. In cases where a low-level exception can be useful for analyzing the situation that caused the exception, it is better to use a special kind of exception translation called exception chaining. In this case, the lower-level exception is passed to the upper-level exception, which, in turn, provides an accessor method (the getCause method in Throwable) that allows you to get the lower-level exception
## 39. Is it possible for an exception to define a class that is not a subclass of Exception, RuntimeException, Error.
## If so, how will it manifest itself (as checked-exception or as unchecked-exception)?
Answer. For an exception, you can define a class that is not a subclass of Exception, RuntimeException, or Error. The Java Language Specification does not explicitly state this, but it is implicitly assumed that such classes will behave in the same way as ordinary checked exceptions (which are subclasses of Exception, not RuntimeException). However, it is desirable not to use such a class. Having no advantage over a regular checked exception, it will only confuse users of your API.
## 40.If a method fails, what should be done with the object on which the method was called?
Answer. After an object throws an exception, it needs to remain in a well-defined, usable state, even if a failure occurs in the middle of an operation. This is especially true for checked exceptions, where the caller is expected to recover the program.
Generally speaking, a method call that fails should leave the object being checked in the same state as it was before the call. A method that has this property is called failure atomic.
