# DIPrinciple
## SOLID principles :
SOLID principles là một nguyên lý thiết kế được công bố bởi Robert C.Martin. SOLID là một nguyên tắc thiết kế nổi tiếng nhất trong lập trình hướng đối tượng. Nó viết tắt của 5 nguyên lý sau.
* Single responsibility
* Open - close
* Liskov substitution 
* Interface segregation.
* Dependency inversion. 

### Single responsibility.
* Benefit: make your software easier to implement and prevents những rủi do không mong muốn khi thay đổi trong tương lai… 
* Mỗi class hay 1 component nên chỉ làm duy nhất 1 trách nhiệm nhất định. Mỗi khi có thay đổi về yêu cầu về trách nhiệm của 1 class chúng ta nên đặt câu hỏi: : What is the responsibility of your class/component/microservice?

### Open - close

### Liskov substitution 
### Interface segregation.

### Dependency inversion. 
the dependency inversion principle is a specific form of decoupling software modules.
When following this principle, the conventional dependency relationships established from high-level, policy-setting modules to low-level, dependency modules are reversed,
 thus rendering **high-level modules independent of the low-level module implementation details**. 
 
The principle states:

- **High-level modules should not depend on low-level modules. Both should depend on abstractions (e.g. interfaces)**.
- **Abstractions should not depend on details. Details (concrete implementations) should depend on abstractions.**

#### Example 
- Main class
```C#
class Program
    {
        static void Main(string[] args)
        {
            Person owner = new Person
            {
                FirstName = "Tim",
                LastName = "Corey",
                EmailAddress = "tim@iamtimcorey.com",
                PhoneNumber = "555-1212"
            };

            Chore chore = new Chore
            {
                choreName = "Take out the trash",
                owner = owner
            };

            chore.PerformedWork(3);
            chore.PerformedWork(1.5);
            chore.CompleteChore();

            Console.ReadLine();
        }
    }
```
--> Main class is **High-Level** , it depending **Low-Level** class are Person and Chore. 
- Chore class
```C#
 public class Chore
    {
        public string choreName { get; set; }
        public Person owner { get; set; }
        public double hoursWorked { get; private set; }
        public bool IsComplete { get; private set; }

        public void PerformedWork(double hours)
        {
            hoursWorked += hours;
            Logger log = new Logger();
            log.Log($"Performed work on { choreName }");
        }

        public void CompleteChore()
        {
            IsComplete = true;

            Logger log = new Logger();
            log.Log($"Completed { choreName }");

            Emailer emailer = new Emailer();
            emailer.SendEmail(owner, $"The chore { choreName } is complete.");
        }
    }
```
--> Chore class is **High-Level** , it depending **Low-Level** class are Person, Email and Logger. 

- Person class
```C#
 public class Person
    {
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public string PhoneNumber { get; set; }
        public string EmailAddress { get; set; }   
    }
```
- Logger Class
```C#
  public class Logger
      {
          public void Log(string message)
          {
              Console.WriteLine($"Write to Console: { message }");
          }
      }
  ```
