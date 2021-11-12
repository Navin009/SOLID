SOLID is a popular set of design principles that are used in object-oriented software development. It
intends to make software designs more understandable, flexible, and maintainable.

#### SOLID is an acronym that stands for five key design principles:

1.  Single responsibility principle
2.  Open-closed principle
3.  Liskov substitution principle
4.  Integration principle
5.  Dependency inversion principle

## 1. Single responsibility principle (SRP)

This principle states that each class should have one responsibility, one single purpose. This means that a class will do only one job, which leads us to conclude it should have only one reason to change.

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

Software entities should be open for extension, but closed for modification. It tells you to write your code so that you will be able to add new functionality without changing the existing code. That prevents situations in which a change to one of your classes also requires you to adapt all depending classes.

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

## 3. Liskov substitution principle (LSP)

A class should be substitutable for its subclasses. If for each object o1 of type S there is an object o2 of type T such that for all programs P defined in terms of T, the behavior of P is unchanged when o1 is substituted for o2 then S is a subtype of T.

```
public abstract class Account {
    protected abstract void deposit(BigDecimal amount);
    protected abstract void withdraw(BigDecimal amount);
}
```

```
public class SavingAccount extends Account {
    @Override
    protected void deposit(BigDecimal amount) {
        // deposit logic
    }

    @Override
    protected void withdraw(BigDecimal amount) {
        // withdraw logic
    }
}
```

```
public class FixedTermDepositAccount extends Account {
    @Override
    protected void deposit(BigDecimal amount) {
        // Deposit into this account
    }

    @Override
    protected void withdraw(BigDecimal amount) {
        throw new UnsupportedOperationException("Withdrawals are not supported by FixedTermDepositAccount!!");
    }
}
```

```
Account myFixedTermDepositAccount = new FixedTermDepositAccount();
myFixedTermDepositAccount.deposit(new BigDecimal(1000.00));

Account mySavingAccount = new SavingAccount();
mySavingAccount.withdraw(new BigDecimal(100.00));
```

-   As we see in above example, FixedTermDepositAccount is substitutable for Account.
-   mySavingAccount is substitutable for Account.

## 4. Interface segregation principle (ISP)

Large interfaces should be made up of small interfaces. This principle is a way to make software more flexible, and to make it easier to change the behavior of the software. It is also a way to make software more maintainable.

```
public interface Payment {
    Object status();
    List<Object> getPayments();
}
```

```
public interface Bank extends Payment {
    void initiatePayments();
}

public interface Loan extends Payment {
    void intiateLoanSettlement();
    void initiateRePayment();
}
```

```
public class BankPayment implements Bank {

    @Override
    public void initiatePayments() {
        // ...
    }

    @Override
    public Object status() {
        // ...
    }

    @Override
    public List<Object> getPayments() {
        // ...
    }
}
```

```
public class LoanPayment implements Loan {

    @Override
    public void intiateLoanSettlement() {
        // ...
    }

    @Override
    public void initiateRePayment() {
        // ...
    }

    @Override
    public Object status() {
        // ...
    }

    @Override
    public List<Object> getPayments() {
        // ...
    }
}
```

![image](https://www.baeldung.com/wp-content/uploads/2020/07/interface_segregation_fixed.png)

-   As we can see, the interfaces don't violate the principle. This implementations don't have to provide empty methods. This keeps the code clean and reduces the chance of bugs.

## 5. Dependency inversion principle (DIP)

High-level modules should not depend on low-level modules. Abstractions should not depend on details. Details should depend on abstractions. This principle is a way to make software more flexible, and to make it easier to change the behavior of the software. It is also a way to make software more maintainable.

```
public class CustomerService {

    private final CustomerDao customerDao;

    // standard constructor / getter

    public Optional<Customer> findById(int id) {
        return customerDao.findById(id);
    }

    public List<Customer> findAll() {
        return customerDao.findAll();
    }
}
```

```
public interface CustomerDao {

    Optional<Customer> findById(int id);

    List<Customer> findAll();

}
```

```
public class SimpleCustomerDao implements CustomerDao {

    // standard constructor / getter

    @Override
    public Optional<Customer> findById(int id) {
        return Optional.ofNullable(customers.get(id));
    }

    @Override
    public List<Customer> findAll() {
        return new ArrayList<>(customers.values());
    }
}
```

![image](https://www.baeldung.com/wp-content/uploads/2019/04/direct-dip.png)

#### Another Example

![image](https://www.baeldung.com/wp-content/uploads/2019/04/alternative-dip.png)

-   Another example of DIP is the CustomerService class. It has a dependency on CustomerDao class.
-   SimpleCustomerDao depends on CustomerDao on the implementation.

## References

1. [SOLID by bmc](https://www.bmc.com/blogs/solid-design-principles/)
2. [SOLD by Visualstudiomagazine](https://visualstudiomagazine.com/articles/2013/04/01/solid-agile-development.aspx)
3. [Single responsibility principle](https://www.baeldung.com/java-single-responsibility-principle)

4. [Open-closed principle](https://www.baeldung.com/java-open-closed-principle)

5. [Liskov substitution principle](https://www.baeldung.com/java-liskov-substitution-principle)

6. [Interface segregation principle](https://www.baeldung.com/java-interface-segregation)

7. [Dependency Inversion Principle](https://www.baeldung.com/java-dependency-inversion-principle)
