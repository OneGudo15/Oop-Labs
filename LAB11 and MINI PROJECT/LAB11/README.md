# Lab 11 answers
Run: `javac *.java && java SingletonFactoryDemo && java StrategyObserverDemo`

Lab 11 has no written exercises, only two programs, so these are both run and checked against the manual's expected output (`expected_output_11.1.txt`, `expected_output_11.2.txt`).

Viva notes
- Singleton: private constructor + static final instance -> `a == b` is true.
- Factory: callers depend on `Notification`, not on `EmailNotification`/`SmsNotification`; adding a type means one new class and one `case`.
- Strategy: `DiscountStrategy` has one method, so a lambda can replace a class. `setStrategy` swaps behaviour at run time.
- Observer: `GradeBook` knows only the `GradeListener` interface (loose coupling), so listeners can be added without changing it.
