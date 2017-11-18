# Array Helpers #

[All array helpers can be located here.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from)

Avoid writing for loops with these methods.

It is important to master these helper methods to really improve developing abilities.

- forEach
- map
- filter
- find
- every
- some
- reduce

## forEach ##
forEach loops through array and passes data as expected on each loop.

    var colors = ['red', 'blue', 'green'];

    colors.forEach(function(color) {
      console.log(color);
    });
    
## map ##
The map() method creates a new array with the results of calling a provided function on every element in the calling array.

    var numbers = [1, 5, 10, 15];
    var doubles = numbers.map(function(x) {
       return x * 2;
    });
    // doubles is now [2, 10, 20, 30]
    // numbers is still [1, 5, 10, 15]

    var numbers = [1, 4, 9];
    var roots = numbers.map(Math.sqrt);
    // roots is now [1, 2, 3]
    // numbers is still [1, 4, 9]
    
## filter ##
The filter() method creates a new array with all elements that pass the test implemented by the provided function.

    var words = ["spray", "limit", "elite", "exuberant", "destruction", "present"];

    var longWords = words.filter(function(word){
      return word.length > 6;
    })

    // Filtered array longWords is ["exuberant", "destruction", "present"]
    
## find ##
The find() method returns the value of the first element in the array that satisfies the provided testing function. Otherwise undefined is returned.

    function isBigEnough(element) {
      return element >= 15;
    }

    [12, 5, 8, 130, 44].find(isBigEnough); // 130
    
## every ##
The every() method tests whether all elements in the array pass the test implemented by the provided function.

function isBigEnough(element, index, array) { 
  return element >= 10; 
} 

    [12, 5, 8, 130, 44].every(isBigEnough);   // false
    [12, 54, 18, 130, 44].every(isBigEnough); // true
    
## some ##
The some() method tests whether some element in the array passes the test implemented by the provided function.

    function isBiggerThan10(element, index, array) {
      return element > 10;
    }

    [2, 5, 8, 1, 4].some(isBiggerThan10);  // false
    [12, 5, 8, 1, 4].some(isBiggerThan10); // true
    
## reduce ##
Every time you find yourself going from a list of values to one value ( reducing ) ask yourself if you could leverage the built-in Array.prototype.reduce() function. You can reduce with any sort of operation that combines two values. Not just addition. And not just arithmetic operations.

    var sum = [1, 2, 3].reduce(function(total, num) {
      return total + num 
    }, 0);
    
## for of loops ##
Allows a more approachable use of for loops with some benefits.

    const colors = ['red', 'green', 'green'];
    
    for (let color of colors) {
      console.log(color)
    }
