
### **Basic Structure of a Java Class**
1. **Package Declaration** (optional)  
   - Specifies the package the class belongs to.  
   ```java
   package com.example.myapp;
   ```

2. **Imports** (optional)  
   - Import classes/packages needed for the current class.  
   ```java
   import java.util.List;
   import java.time.LocalDate;
   ```

3. **Class Declaration**  
   - Defined with `public`, `abstract`, `final`, or default (package-private) access modifier.  
   ```java
   public class Employee { 
       // Class body
   }
   ```

4. **Class Members**  
   - **Fields (Variables)**: Instance variables and static variables.  
     ```java
     private String name;    // Instance variable
     private int id;
     private static int count = 0; // Static variable
     ```
   - **Constructors**: Initialize objects.  
     ```java
     public Employee(String name, int id) {
         this.name = name;
         this.id = id;
         count++;
     }
     ```
   - **Methods**: Define behavior.  
     ```java
     public void displayDetails() {
         System.out.println("ID: " + id + ", Name: " + name);
     }
     ```
   - **Static Methods**: Called on the class itself.  
     ```java
     public static int getCount() {
         return count;
     }
     ```

5. **Blocks** (optional)  
   - **Static Initializer**: Runs once when the class is loaded.  
     ```java
     static {
         // Initialize static resources
     }
     ```
   - **Instance Initializer**: Runs before each constructor.  
     ```java
     {
         // Common initialization code
     }
     ```

6. **Nested Classes/Interfaces** (optional)  
   - Inner classes, enums, or interfaces.  
   ```java
   private class Address {
       String city;
       String country;
   }
   ```

7. **Comments/Annotations** (optional)  
   - JavaDoc comments or annotations like `@Override`.  
   ```java
   /**
    * Calculates the salary of the employee.
    * @return Monthly salary in USD.
    */
   public double calculateSalary() {
       // Logic here
   }
   ```

---

### **Example: Complete Java Class**
```java
package com.example.company;

import java.time.LocalDate;

public class Employee {
    // Fields
    private String name;
    private int id;
    private LocalDate hireDate;
    private static int employeeCount = 0;

    // Constructor
    public Employee(String name, int id, LocalDate hireDate) {
        this.name = name;
        this.id = id;
        this.hireDate = hireDate;
        employeeCount++;
    }

    // Instance method
    public void displayInfo() {
        System.out.println("Employee: " + name + " | ID: " + id);
    }

    // Static method
    public static int getEmployeeCount() {
        return employeeCount;
    }

    // Getters and Setters
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    // Main method (for testing)
    public static void main(String[] args) {
        Employee emp = new Employee("Alice", 101, LocalDate.now());
        emp.displayInfo();
        System.out.println("Total employees: " + Employee.getEmployeeCount());
    }
}
```

---

### **Key Conventions**
1. **Order of Elements**:  
   ```
   Package → Imports → Class → Fields → Constructors → Methods → Inner Classes
   ```
2. **Encapsulation**:  
   - Use `private` fields with `public` getters/setters.  
3. **Naming**:  
   - Class names: `PascalCase` (e.g., `BankAccount`).  
   - Variables/methods: `camelCase` (e.g., `calculateSalary()`).  

---

### **Mandatory vs. Optional**
- **Mandatory**: Class declaration and body (`public class MyClass { }`).  
- **Optional**: Package, imports, constructors (default constructor is auto-generated if none defined).  

Here's a guide to handling input validation in Java using `Scanner` with CLI input, including error handling using `try-catch` blocks:

---

### **Basic Input Validation with `Scanner`**
Use loops and `try-catch` to validate input and handle exceptions gracefully.

```java
import java.util.InputMismatchException;
import java.util.Scanner;

public class InputValidationExample {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int age = 0;
        boolean validInput = false;

        while (!validInput) {
            try {
                System.out.print("Enter your age: ");
                age = scanner.nextInt();
                
                // Additional validation (e.g., age range)
                if (age < 0 || age > 120) {
                    System.out.println("Invalid age. Must be between 0 and 120.");
                    continue;
                }
                validInput = true;
                
            } catch (InputMismatchException e) {
                System.out.println("Invalid input. Please enter a number.");
                scanner.nextLine(); // Clear the invalid input from the buffer
            }
        }

        System.out.println("Your age is: " + age);
        scanner.close();
    }
}
```

---

### **Key Steps for Robust Validation**
1. **Loop Until Valid Input**  
   Use a `while` loop to repeatedly prompt the user until valid input is provided.

2. **Catch `InputMismatchException`**  
   Handle non-integer input (e.g., letters for a numeric field).

3. **Clear the Scanner Buffer**  
   Use `scanner.nextLine()` after catching an error to flush invalid input from the buffer.

4. **Additional Validation**  
   Add checks for ranges, formats, or other constraints after parsing the input.

---

### **Example: Validate a Double Input**
```java
public class DoubleValidation {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        double price = 0.0;
        boolean isValid = false;

        while (!isValid) {
            try {
                System.out.print("Enter product price: ");
                price = scanner.nextDouble();
                
                if (price <= 0) {
                    System.out.println("Price must be greater than 0.");
                    continue;
                }
                isValid = true;
                
            } catch (InputMismatchException e) {
                System.out.println("Invalid input. Enter a numeric value (e.g., 9.99).");
                scanner.nextLine();
            }
        }

        System.out.printf("Price set to: $%.2f%n", price);
        scanner.close();
    }
}
```

---

### **Example: String Input Validation**
Validate non-empty strings or specific patterns (e.g., email):
```java
public class StringValidation {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String name = "";
        boolean isValid = false;

        while (!isValid) {
            System.out.print("Enter your name: ");
            name = scanner.nextLine().trim();

            if (name.isEmpty()) {
                System.out.println("Name cannot be empty.");
            } else if (!name.matches("[a-zA-Z\\s]+")) { // Check for letters/spaces only
                System.out.println("Invalid characters in name.");
            } else {
                isValid = true;
            }
        }

        System.out.println("Hello, " + name + "!");
        scanner.close();
    }
}
```

---

### **Handling Multiple Inputs in Sequence**
Use `try-catch` for each input field to avoid cascading errors:
```java
public class MultiInputValidation {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int quantity = 0;
        double price = 0.0;
        boolean validQuantity = false;
        boolean validPrice = false;

        // Validate quantity
        while (!validQuantity) {
            try {
                System.out.print("Enter quantity: ");
                quantity = scanner.nextInt();
                if (quantity < 1) throw new IllegalArgumentException();
                validQuantity = true;
            } catch (InputMismatchException | IllegalArgumentException e) {
                System.out.println("Invalid quantity. Enter a positive integer.");
                scanner.nextLine();
            }
        }

        // Validate price
        while (!validPrice) {
            try {
                System.out.print("Enter price per unit: ");
                price = scanner.nextDouble();
                if (price <= 0) throw new IllegalArgumentException();
                validPrice = true;
            } catch (InputMismatchException | IllegalArgumentException e) {
                System.out.println("Invalid price. Enter a positive number.");
                scanner.nextLine();
            }
        }

        System.out.printf("Total cost: $%.2f%n", quantity * price);
        scanner.close();
    }
}
```

---

### **Common Patterns**
1. **Reusable Validation Helper**  
   Create a method to validate inputs:
   ```java
   public static int getValidInt(Scanner scanner, String prompt, int min, int max) {
       int value;
       while (true) {
           try {
               System.out.print(prompt);
               value = scanner.nextInt();
               if (value < min || value > max) {
                   System.out.printf("Input must be between %d and %d.%n", min, max);
                   continue;
               }
               return value;
           } catch (InputMismatchException e) {
               System.out.println("Invalid input. Enter an integer.");
               scanner.nextLine();
           }
       }
   }
   ```

2. **Close the Scanner**  
   Use `scanner.close()` at the end of your program to release resources.

---

### **Best Practices**
- **Clear the Buffer**: Always use `scanner.nextLine()` after `nextInt()`/`nextDouble()` to avoid leftover newline characters.
- **Validate Early**: Check constraints (e.g., ranges) **after** parsing the input.
- **Use Specific Exceptions**: Catch `InputMismatchException` instead of generic `Exception`.

Here's a concise cheat sheet of the **most commonly used built-in methods** for `String`, `int`/`Integer`, and related conversions (including `toString()`, case manipulation, and parsing):

---

### **String Class Methods**
1. **`length()`**  
   Returns the length of the string.  
   ```java
   String s = "Hello";
   int len = s.length(); // 5
   ```

2. **`charAt(int index)`**  
   Returns the character at the specified index.  
   ```java
   char c = s.charAt(1); // 'e'
   ```

3. **`substring(int beginIndex, int endIndex)`**  
   Extracts a substring (endIndex is exclusive).  
   ```java
   String sub = s.substring(1, 3); // "el"
   ```

4. **`equals(Object obj)`**  
   Compares string content (use instead of `==`).  
   ```java
   boolean isEqual = s.equals("hello"); // false (case-sensitive)
   ```

5. **`equalsIgnoreCase(String other)`**  
   Case-insensitive comparison.  
   ```java
   boolean isEqual = s.equalsIgnoreCase("hello"); // true
   ```

6. **`toLowerCase()` / `toUpperCase()`**  
   Converts the string to lower/upper case.  
   ```java
   String lower = s.toLowerCase(); // "hello"
   ```

7. **`trim()`**  
   Removes leading/trailing whitespace.  
   ```java
   String trimmed = "  Hi  ".trim(); // "Hi"
   ```

8. **`replace(oldChar, newChar)`**  
   Replaces characters or substrings.  
   ```java
   String replaced = s.replace('l', 'z'); // "Hezzo"
   ```

9. **`split(String regex)`**  
   Splits the string into an array using a regex.  
   ```java
   String[] parts = "a,b,c".split(","); // ["a", "b", "c"]
   ```

10. **`contains(CharSequence s)`**  
    Checks if the string contains a substring.  
    ```java
    boolean hasEll = s.contains("ll"); // true
    ```

11. **`indexOf(String str)`**  
    Returns the index of the first occurrence of `str`.  
    ```java
    int idx = s.indexOf("l"); // 2
    ```

---

### **int ↔ String Conversions**
1. **String to int**  
   Use `Integer.parseInt()` or `Integer.valueOf()`.  
   ```java
   String numStr = "123";
   int num = Integer.parseInt(numStr); // 123
   Integer numObj = Integer.valueOf(numStr); // Integer object
   ```

2. **int to String**  
   Use `Integer.toString()` or `String.valueOf()`.  
   ```java
   int num = 456;
   String s1 = Integer.toString(num); // "456"
   String s2 = String.valueOf(num);   // "456"
   ```

---

### **`toString()` Method**
- **Default behavior** (from `Object` class):  
  Returns a string like `ClassName@hashCode`.  
  ```java
  MyClass obj = new MyClass();
  System.out.println(obj); // e.g., MyClass@1a2b3c
  ```

- **Override `toString()`** for meaningful output:  
  ```java
  class Person {
      String name;
      int age;
      
      @Override
      public String toString() {
          return "Person [name=" + name + ", age=" + age + "]";
      }
  }
  ```

---

### **Utility Methods**
1. **`String.format()`**  
   Format strings using placeholders.  
   ```java
   String formatted = String.format("Name: %s, Age: %d", "Alice", 30);
   ```

2. **`String.join()`**  
   Join strings with a delimiter.  
   ```java
   String joined = String.join("-", "2023", "09", "15"); // "2023-09-15"
   ```

3. **`String.valueOf()`**  
   Convert any type to a `String` (works for primitives and objects).  
   ```java
   String s = String.valueOf(10); // "10"
   ```

---

### **Common Pitfalls**
- **`==` vs `equals()`**:  
  Use `equals()` to compare string **content**, not `==` (which checks object references).  
- **Case Sensitivity**:  
  Use `equalsIgnoreCase()` for case-insensitive comparisons.  
- **Number Parsing**:  
  Handle `NumberFormatException` when converting strings to numbers.  
  ```java
  try {
      int num = Integer.parseInt("abc");
  } catch (NumberFormatException e) {
      System.out.println("Invalid number format!");
  }
  ```

---

**Quick Reference**  
```java
// Common String Operations
String s = "Hello World";
s.length();          // 11
s.substring(6);      // "World"
s.replace("World", "Java"); // "Hello Java"

// Case Conversion
s.toLowerCase();     // "hello world"
s.toUpperCase();     // "HELLO WORLD"

// int ↔ String
int num = 123;
String numStr = Integer.toString(num); // "123"
int parsed = Integer.parseInt(numStr); // 123
```
