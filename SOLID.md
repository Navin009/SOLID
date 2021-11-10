# SOLID

SOLID is a popular set of design principles that are used in object-oriented software development. It
intends to make software designs more understandable, flexible, and maintainable.

> #### SOLID is an acronym that stands for five key design principles:
>
> 1.  **S**ingle responsibility principle
> 2.  **O**pen-closed principle
> 3.  **L**iskov substitution principle
> 4.  **I**nterface segregation principle
> 5.  **D**ependency inversion principle

## 1. Single responsibility principle (SRP)

> This principle states that `each class should have one responsibility, one single purpose.` This means that a class will do only one job, which leads us to conclude it should have only one reason to change.

```
public class TextManipulator {
    private String text;

    public TextManipulator(String text) {
        this.text = text;
    }

    public String getText() {
        return text;
    }

    public void appendText(String newText) {
        text = text.concat(newText);
    }

    public String findWordAndReplace(String word, String replacementWord) {
        if (text.contains(word)) {
            text = text.replace(word, replacementWord);
        }
        return text;
    }

    public String findWordAndDelete(String word) {
        if (text.contains(word)) {
            text = text.replace(word, "");
        }
        return text;
    }

    public void printText() {
        System.out.println(textManipulator.getText());
    }
}
```

This class has a lot of responsibilities, but it only has one reason to change. As a result, programmers can easily find and fix the problem.

## 2. Open-closed principle (OCP)

> `Software entities should be open for extension, but closed for modification.` It tells you to write your code so that you will be able to add new functionality without changing the existing code. That prevents situations in which a change to one of your classes also requires you to adapt all depending classes.

```
public interface CalculatorOperation {
    void perform();
}
```

```
public class Addition implements CalculatorOperation {
    private double left;
    private double right;
    private double result;

    // constructor, getters and setters

    @Override
    public void perform() {
        result = left + right;
    }
}
```

```
public class Division implements CalculatorOperation {
    private double left;
    private double right;
    private double result;

    // constructor, getters and setters
    @Override
    public void perform() {
        if (right != 0) {
            result = left / right;
        }
    }
}
```

```
public class Calculator {

    public void calculate(CalculatorOperation operation) {
        if (operation == null) {
            throw new InvalidParameterException("Cannot perform operation");
        }
        operation.perform();
    }
}
```
-   Software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification.


-   A class is closed, since it may be compiled, stored in a library, baselined, and used by client classes. But it is also open, since any new class may use it as parent, adding new features. When a descendant class is defined, there is no need to change the original or to disturb its clients.

## 3. Liskov substitution principle

> `A class should be substitutable for its subclasses.` This principle is a way to make software more flexible, and to make it easier to change the behavior of the software. It is also a way to make software more maintainable.

## 4. Interface segregation principle

> `Large interfaces should be made up of small interfaces.` This principle is a way to make software more flexible, and to make it easier to change the behavior of the software. It is also a way to make software more maintainable.

## 5. Dependency inversion principle

> `High-level modules should not depend on low-level modules. Both should depend on abstractions.` This principle is a way to make software more flexible, and to make it easier to change the behavior of the software. It is also a way to make software more maintainable.

## References

1. [SOLID by bmc](https://www.bmc.com/blogs/solid-design-principles/)
2. [SOLD by Visualstudiomagazine](https://visualstudiomagazine.com/articles/2013/04/01/solid-agile-development.aspx)
3. [Single responsibility principle](https://www.baeldung.com/java-single-responsibility-principle)
