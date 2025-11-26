
**spring and spring boot - and more**

In summary, **Spring** is a powerful, comprehensive framework that gives you a lot of flexibility, but can be a bit overwhelming to set up. **Spring Boot** is a more opinionated, streamlined version of Spring that comes with a lot of built-in features to help you get started quickly and easily.


**Writing a failing test**

We'll take an alternative approach: we'll write tests _before_ implementing the application code. This is called test driven development (TDD).

Lab testing First


```` JAVA
// add this in new class
package example.cashcard;

import org.junit.jupiter.api.Test;
import static org.assertj.core.api.Assertions.assertThat;

class CashCardJsonTest {

   @Test //this is part of JUnit Library
   void myFirstTest() {
      assertThat(1).isEqualTo(42); //this is part of AssertJ library
   }
}
````



**REST**: Representational State Transfer. In a RESTful system, data objects are called Resource Representations. The purpose of a RESTful API (Application Programming Interface) is to manage the state of these Resources.