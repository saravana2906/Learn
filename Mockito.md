### Mockito:
Mockito helps us to implement fake calls using stubs.

Dependency needed for Mockito :

```
<!-- https://mvnrepository.com/artifact/org.mockito/mockito-core -->
<dependency>
    <groupId>org.mockito</groupId>
    <artifactId>mockito-core</artifactId>
    <version>2.25.0</version>
    <scope>test</scope>
</dependency>
```

```
public interface CalculatorService
{
public int add(int i,int j);
}
```

### Without Mockito:
### Test Class:
```
import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.*;

public class AppTest 
{
	CalculatorService cls=new CalculatorService()
			{
		public int sub(int i,int j)
		{
			return i-j;
		}
			};
	Calculator cal =new Calculator(cls);
   @Test
	  public void testSub()
	  {
		  int a=5,b=3;
		  int d=cal.sub(a, b);
		  assertEquals(2,d);
	  }
 }
  ```
  
  ### Main Class:
  
  ```
  public class Calculator {
	
	CalculatorService cls;
	
	public Calculator(CalculatorService cls)
	{
		this.cls=cls;
	}
		public int sub(int i,int j)
	{
		
		return cls.sub(i, j);
	}
	
}
```

With & Without Mockito :

Test Class:
```

import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.*;
import org.mockito.Mockito;


public class AppTest 
{
//Below anonymous class to demonstarte without Mockito
	CalculatorService cls=new CalculatorService()
	
			{
		public int sub(int i,int j)
		{
			return i-j;
		}
			};
      //Below is using Mockito to mock the class
			CalculatorService calsm=Mockito.mock(CalculatorService.class);
	Calculator cal =new Calculator(cls);
	Calculator calm=new Calculator(calsm);
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
    
    //Testing Subtraction without Mockito using Anonymous class
	  @Test
	  public void testSub()
	  {
		  int a=5,b=3;
		  int d=cal.sub(a, b);
		  assertEquals(2,d);
	  }
    //testing Subtraction using Mockito
	  @Test
	  public void testSubwithMock()
	  {
		  int a=5,b=3;
		  Mockito.when(calsm.sub(5, 3)).thenReturn(2);//This is to tell Mockito to return 2 when value is 5,3
		  int d=calm.sub(a, b);
		  assertEquals(2,d);
		  Mockito.verify(calsm).sub(5,3);// To verify whether service call is really made in Calculator class
	  }

	  @AfterAll
	  public static void tearDownAfterClass() throws Exception {
	   System.out.println("\n"+"In @AfterAll");
	  }
}
```
Source : https://www.youtube.com/watch?v=HsQ9OwKA79s
