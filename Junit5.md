**Unit Test** , tests the behavior of the basic unit of work

Junit has significant change in Junit 5 version.It consists of three modules
- Junit Platform
  - Launches testing framework on JVM
  - Defines TestEngine to develop a test framework
- Junit Jupiter
  - Blending of the latest programming model and extension model, to write tests and extensions in JUnit 5
- Junit Vintage
  - Ensure backward compatibility with JUnit 3 and 4.
  - Provides TestEngine to execute JUnit 3 and JUnit 4 tests on the platform
As Junit5 has backward compatible to junit4 & 3 , they are holding the packages in below
JUnit 3 core classes are in **junit.framework** package but JUnit 4 packaged them under **org.junit**.

Junit5 dependencies :
```
<dependency>
 <groupId>org.junit.jupiter</groupId>
 <artifactId>junit-jupiter-api</artifactId>
 <version>5.0.1</version>
 <scope>test</scope>
</dependency>
 <dependency>
 <groupId>org.junit.jupiter</groupId>
 <artifactId>junit-jupiter-engine</artifactId>
 <version>5.0.1</version>
 <scope>test</scope>
</dependency>
<dependency>
 <groupId>org.junit.vintage</groupId>
 <artifactId>junit-vintage-engine</artifactId>
 <version>4.12.1</version>
 <scope>test</scope>
 </dependency>
<dependency>
 <groupId>org.junit.platform</groupId>
 <artifactId>junit-platform-launcher</artifactId>
 <version>1.0.1</version>
 <scope>test</scope>
</dependency>
<dependency>
 <groupId>org.junit.platform</groupId>
 <artifactId>junit-platform-runner</artifactId>
 <version>1.0.1</version>
 <scope>test</scope>
</dependency>
```
If we are using Eclipse , make sure Eclipse supports Junit5 Tests.
It has various types of annotations and all methods are function level annotations , mainly 
- @BeforeAll - Executes only once before all test cases
- @BeforeEach - Executes before each test case
- @Test - Actual test case need to be tested 
- @AfterAll - Executes after all test cases
- @AfterEach - Executes after each test case 

There are other annotations , 
Annotations
- @TestFactory – Indicates a method as test factory method, which will create dynamic tests.
- @Disabled – Can be used to disable some test cases or a test class during test execution.
- @DisplayName – Configures a custom name for the test case or test method.
- @Nested – Indicates the annotated class is a nested, non-static test class.
- @Tag – Used to declare tags at method level or test-class level for filtering.
- @ParameterizedTest – To indicate a test method is a parameterized test.
- @RepeatedTest – Denotes a method is a template for a repeated test.

Below Junit5 Test will fail as we did addition wrongly in actual implementation
**Main:** 
```
package com.tdd.calculator;
public class Calculator {
	public int add(int a, int b) {
		return a+b+1;
	}
}
```
**Test:**
```
import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.*;

public class AppTest 
{
	
	Calculator cal =new Calculator();
	@BeforeAll
	  public static void setUpBeforeClass() throws Exception {
	   System.out.println("In @BeforeAll");
	  }

	  @BeforeEach
	  public void setUp() throws Exception {
	   System.out.println("\n"+"In @BeforeEach");
	  }
	  
	  @AfterEach
	  public void tearDown() throws Exception {
	   System.out.println("\n"+"In @AfterEach");
	  }
	  @Test
	  public void testAdd()
	  { 
		  System.out.println("Testing Addition");
		  int a=1;
		  int b=2;
		  int c=3;
		  int d=cal.add(a,b);
		  assertEquals(c,d);
	  }

	  @AfterAll
	  public static void tearDownAfterClass() throws Exception {
	   System.out.println("\n"+"In @AfterAll");
	  }
}

```
