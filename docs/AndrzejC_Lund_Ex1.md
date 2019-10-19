## Exercises I: Filter

#### Summary
* The most difficult part for me was to add libraries to **the existing gradle project**. 
For a long time Junit5 and Hamcrest were not visible. 
Apparently neither getting them directly via IntelliJ, nor downloading and linking jar files are enough. 
Gradle has to be built correctly :)
* I know that code inputs do not look very nice, but this is the best I managed. 
Code works, this is important :)

#### RectangleArrayProcessor - Implementation of the following methods:
* **removeRectanglesLargerThan**
  * takes a Rectangle array and an int n 
  * returns an array containing only the rectangles with a smaller area than n  
  *   _public Rectangle[] removeRectanglesLargerThan(Rectangle[] array, int maxArea) {  
        ArrayList<Rectangle> resultArray = new ArrayList<>();  
        for (Rectangle rectangle: array) if (rectangle.area() <= maxArea) resultArray.add(rectangle);  
        return resultArray.toArray(new Rectangle[resultArray.size()]);  
     }_
* **removeRectanglesLargerThan**
  * takes a Rectangle array and a Rectangle r
  * returns an array containing only the rectangles with a smaller area than r's area
  *   _public Rectangle[] removeRectanglesLargerThan(Rectangle[] array, Rectangle r) {  
        ArrayList<Rectangle> resultArray = new ArrayList<>();  
        for (Rectangle rectangle: array) if (rectangle.compareTo(r) < 0) resultArray.add(rectangle);  
        return resultArray.toArray(new Rectangle[resultArray.size()]);  
    }_
* **containsSquare** 
  * takes a Rectangle array
  * returns true if the array contains a square or false otherwise
  *   _public boolean containsSquare(Rectangle[] array) {  
        for (Rectangle rectangle: array) if (rectangle.getHeight() == rectangle.getWidth()) return true;  
        return false;  
    }_
* **filterRectanglesWithEqualArea**
  * takes a Rectangle array and a Rectangle r
  * returns an array containing only the rectangles with an area equal to r's area
  *   _public Rectangle[] filterRectanglesWithEqualArea(Rectangle[] array, Rectangle r) {  
        ArrayList<Rectangle> resultArray = new ArrayList<>();  
        for (Rectangle rectangle: array) if (rectangle.compareTo(r) == 0) resultArray.add(rectangle);  
        return resultArray.toArray(new Rectangle[resultArray.size()]);  
    }_

#### RectangleArrayProcessorTest - Implementation of the following test methods:
* **removeRectanglesLargerThan** (both, with input int and Rectangle)
  *   _@Test  
      void testProcessorRemovesRectanglesLargerThan() {  
        // Arrange  
        Rectangle[] inputArray = {new Rectangle(2, 2), new Rectangle(2, 3), new Rectangle(5, 4), new Rectangle(1, 5)};  
        int inputMaxArea = 5;  
        Rectangle[] expectedArrayForMaxArea = {new Rectangle(2, 2), new Rectangle(1, 5)};  
        Rectangle r = new Rectangle(4, 4);  
        Rectangle[] expectedArrayForR = {new Rectangle(2, 2), new Rectangle(2, 3), new Rectangle(1, 5)};  
        // Act  
        Rectangle[] actualArrayForMaxArea = rectangleArrayProcessor.removeRectanglesLargerThan(inputArray, inputMaxArea);  
        Rectangle[] actualArrayForR = rectangleArrayProcessor.removeRectanglesLargerThan(inputArray, r);  
        // Assert  
        assertArrayEquals(expectedArrayForMaxArea, actualArrayForMaxArea);  
        assertArrayEquals(expectedArrayForR, actualArrayForR);  
        assertNotEquals(actualArrayForR, actualArrayForMaxArea);  
    }_
* **containsSquare** 
  *   _@Test  
    void testContainsSquare() {  
        // Arrange  
        Rectangle[] inputArrayWithSquare = {new Rectangle(2, 2), new Rectangle(2, 3), new Rectangle(5, 4), new Rectangle(1, 5)};  
        Rectangle[] inputArrayWithoutSquare = {new Rectangle(2, 3), new Rectangle(5, 4), new Rectangle(1, 5)};  
        // Act  
        boolean checkOfArrayWithSquare = rectangleArrayProcessor.containsSquare(inputArrayWithSquare);  
        boolean checkOfArrayWithoutSquare = rectangleArrayProcessor.containsSquare(inputArrayWithoutSquare);  
        // Assert  
        assertTrue(checkOfArrayWithSquare);  
        assertFalse(checkOfArrayWithoutSquare);  
    }_
* **filterRectanglesWithEqualArea**
  *   _@Test  
    void testFilterRectanglesWithEqualArea() {  
        // Arrange  
        Rectangle[] inputArrayWith = {new Rectangle(2, 2), new Rectangle(2, 3), new Rectangle(5, 4), new Rectangle(3, 2),  
                new Rectangle(1, 6), new Rectangle(5, 3), new Rectangle(3, 5)};
        Rectangle[] inputArrayWithout = {new Rectangle(2, 2), new Rectangle(5, 4), new Rectangle(5, 3), new Rectangle(3, 5)};  
        Rectangle r = new Rectangle(6, 1);  
        Rectangle[] expectedArrayWithForR = {new Rectangle(2, 3), new Rectangle(3, 2), new Rectangle(1, 6),};  
        // Act  
        Rectangle[] actualArrayWithForR = rectangleArrayProcessor.filterRectanglesWithEqualArea(inputArrayWith, r);  
        int actualSizeArrayWithoutForR = rectangleArrayProcessor.filterRectanglesWithEqualArea(inputArrayWithout, r).length;  
        // Assert  
        assertArrayEquals(expectedArrayWithForR, actualArrayWithForR);  
        assertEquals(0, actualSizeArrayWithoutForR);  
    }_
