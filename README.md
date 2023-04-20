# IT314_Lab-8_202001157

## Name - Harsh Buddhdev <br><br> Student ID - 202001157

### 1.  Create a new Eclipse project, and within the project create a package.

Here in eclipse, I created a constructor Boa with necessary arguments -

![image](https://user-images.githubusercontent.com/77343146/233312213-fb1b9ad1-8f66-4c4e-abfb-dc88a4b88f48.png)

### 2.  Creating a testcase for the class Boa by testing the two different classes - 

a.  Testing the class isHealthy(). We create two Boa objects with different favorite foods, and verify that isHealthy returns true for the first object and false for the second object.

b.  Testing the class fitsInCage(). We create two Boa objects with different lengths, and test whether they fit in cages of different lengths. We expect the first boa to fit in a cage of length 5 but not 3, and the second boa to fit in a cage of length 12 but not 9.

    import org.junit.Test;
    import static org.junit.Assert.*;

    public class BoaTest {
    
      @Test
      public void testIsHealthy() {
          Boa boa1 = new Boa("Sneaky", 6, "granola bars");
          assertTrue(boa1.isHealthy());

          Boa boa2 = new Boa("Slithery", 8, "pizza");
          assertFalse(boa2.isHealthy());
      }
      
      @Test
      public void testFitsInCage() {
          Boa boa1 = new Boa("Slinky", 4, "mice");
          assertTrue(boa1.fitsInCage(5));
          assertFalse(boa1.fitsInCage(3));

          Boa boa2 = new Boa("Curly", 10, "rabbits");
          assertTrue(boa2.fitsInCage(12));
          assertFalse(boa2.fitsInCage(9));
      }
    }
    
### 3.  Unit tests with stubs for several methods and modified setUp() method in the BoaTest class - 

a.  Here I, added private fields for jen and ken to the BoaTest class, and initialized them in the setUp method. We also updated the testIsHealthy and testFitsInCage methods to use these Boa objects for testing.

b.  @Before annotation denotes that the setUp method will be executed before each test method, so any changes made to the Boa objects during a test will not affect the objects used in other tests.

    import org.junit.Before;
    import org.junit.Test;
    import static org.junit.Assert.*;

    public class BoaTest {

    private Boa jen;
    private Boa ken;

    @Before
    public void setUp() throws Exception {
        jen = new Boa("Jennifer", 2, "grapes");
        ken = new Boa("Kenneth", 3, "granola bars");
      }
    }
    
    
c.  Modified testIsHealthy() method in the BoaTest class - Added assertions to the testIsHealthy method to check that the isHealthy method returns true for both Boa objects. We also added assertions to the testFitsInCage method to check that the fitsInCage method returns the expected results for the Boa objects.

      @Test
      public void testIsHealthy() {
      
          // check that ken is healthy
          assertTrue(ken.isHealthy());
          
          // check that jen is not healthy
          assertFalse(jen.isHealthy());
      }

d.  Modified testFitsInCage() method in the BoaTest class - In this example, I added assertions to the testFitsInCage method to check that the fitsInCage method returns the expected results for both jen and ken when the cage length is less than, equal to, and greater than the length of the boa.

Note that the testFitsInCage method is now more robust, as it checks the behavior of the fitsInCage method for different input values.

      @Test
      public void testFitsInCage() {
          // Test for ken
          assertFalse(ken.fitsInCage(2)); // cage length is less than length of boa
          assertFalse(ken.fitsInCage(3)); // cage length is equal to length of boa
          assertTrue(ken.fitsInCage(5)); // cage length is greater than length of boa
          
          // Test for jen
          assertFalse(jen.fitsInCage(1)); // cage length is less than length of boa
          assertFalse(jen.fitsInCage(2)); // cage length is equal to length of boa
          assertTrue(jen.fitsInCage(3)); // cage length is greater than length of boa
      }

![image](https://user-images.githubusercontent.com/77343146/233319587-3d3f8942-ed35-45e5-94f8-4727a91f3367.png)


### 4.  Running the test cases - 

![image](https://user-images.githubusercontent.com/77343146/233316888-e8998ad3-cf20-4b6f-a0d1-05d3f2e85cbd.png)


### 5.  Modified Boa class with the new lengthInInches() method -

Here is the updated code for the BoaTest class with the new testLengthInInches() method.

      public class Boa {
          private String name;
          private int length; // the length of the boa, in feet
          private String favoriteFood;

          public Boa(String name, int length, String favoriteFood) {
              this.name = name;
              this.length = length;
              this.favoriteFood = favoriteFood;
          }

          // returns true if this boa constrictor is healthy
          public boolean isHealthy() {
              return this.favoriteFood.equals("granola bars");
          }

          // returns true if the length of this boa constrictor is
          // less than the given cage length
          public boolean fitsInCage(int cageLength) {
              return this.length < cageLength;
          }

          // produces the length of the Boa in inches
          public int lengthInInches() {
              return this.length * 12;
          }
      }

![image](https://user-images.githubusercontent.com/77343146/233315913-fe56fcb9-dea7-404b-84d8-683ba12404ee.png)

### 6.  An example of a new test case in the BoaTest class that tests the lengthInInches() method -

This new test case checks that the lengthInInches() method returns the expected value when called on each of the Boa objects created in the setUp() method. It uses the assertEquals() method to compare the expected value to the actual value returned by the lengthInInches() method. The @Test annotation indicates that this is a test method that should be run by JUnit.

      import static org.junit.Assert.assertEquals;
      import org.junit.Before;
      import org.junit.Test;

      public class BoaTest {
          private Boa jen;
          private Boa ken;

          @Before
          public void setUp() throws Exception {
              jen = new Boa("Jennifer", 2, "grapes");
              ken = new Boa("Kenneth", 3, "granola bars");
          }

          @Test
          public void testLengthInInches() {
              assertEquals(24, jen.lengthInInches());
              assertEquals(36, ken.lengthInInches());
          }
      }
