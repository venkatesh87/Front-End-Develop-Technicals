### I. Flex Those JavaScript Array Muscles
---

**1. Sort and Reverse**
---
```javascript
const array = [1, 8, 3, 5, 9, 7];
```

- Imagine you were handed this array, but you wanted to show it starting from the lowest number to the highest one. What sort does is sort any array given ascending so in this case, if you did this:
```javascript
let sortedArray = array.sort();
```

- It would return a new array with the values:
```javascript
[1, 3, 5, 7, 8, 9]
```

- This sort method also works with names and string characters so if you would like to alphabetically order an array of names or anything involving strings it would do that without any parameters.
- You can also pass one parameter to it, and that parameter is the sorting function, by default what javascript does is this:
```javascript
array.sort((a, b) => {
    // a = current item in array
    // b = next item in array
    return a < b;
});
```

- What this function does in concrete is that it goes through every element in the array and sees if the current one is smaller than the next one and in that way organizes your new array. So if you wanted to this backward all you would have to do is see if the current item is bigger than the next one, like so:
```javascript
array.sort((a, b) => {
    return a > b;
});

// [9, 8, 7, 5, 3, 1]
```

- There is also another way to reverse an array, and this is where the reverse function comes in, all this function does is reverse the order of an array, so instead, we can do this:
```javascript
array.sort().reverse();

// [9, 8, 7, 5, 3, 1]
```
**2. filter() the Array**
---
```javascript
const people = [
  {
    name: 'Sara',
    age: 25,
    gender: 'f',
    us: true
  },
  {
    name: 'Mike',
    age: 18,
    gender: 'm',
    us: false,
  },
   {
    name: 'Peter',
    age: 17,
    gender: 'm',
    us: false,
  },
   {
    name: 'Ricky',
    age: 27,
    gender: 'm',
    us: false,
  },
  {
    name: 'Martha',
    age: 20,
    gender: 'f',
    us: true
  }
];
```

>**Get the Women**
---
- To use this to get the women we would do something like this:
```javascript
let women = people.filter(function(person) {
    // only return the objects that have the key gender equal to f
    return person.gender === 'f';
});
```

- We can actually improve this a lot using ES6 and arrow functions:
```javascript
let women = people.filter((person) => person.gender === 'f');
```

> Cool tip: In cases like this you can use ```console.table``` instead of ```console.log``` to get a table as the output instead of getting the object references.

![Image of Yaktocat](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/console_table.jpg)

>**Getting People Old Enough to Drink**
---
- Now to get into something a little more tricky using filter, imagine you only want to return the people who are old enough to drink, and this defers whether you are from the US or not, for simplicity sake let's assume everyone outside the US has a legal drinking age of 18, in this case we first need to check if the person is in the US or not and then either return people who are older then 21 or if they are not from the US return anyone older than 18.

```javascript
let legal = people.filter((person) => {
    // If the person in the US only return it if they are older or 21
    // If not return the person if the are 18 or above
    return person.us ? person.age >= 21 : person.age >= 18;
});
```
- If you now ```console.table``` the legal variable you will see this:

![Image of Yaktocat](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/console_table_us.jpg)

**5. map() the Array**
---
- We already created an array that only has the people who have the legal age to drink but wouldn't it be better to add legal as a key of every object and set it to true or false?

- This type of transformation is what the map function does, it runs a function for every element in the array we give it and it returns our new array.

- In this case, half our work is already done, all this function needs to do is the same conditional statement we just ran in the filter function, the only change it needs to have is get a parameter that will be the object, so we need a function like this:

```javascript
let legalFunction = (person) => person.us ? person.age >= 21 : person.age >= 18;
```

- This function either returns true or false depending on the location of the person. Let's move on to the ```map``` function and run this ```legalFunction``` everytime map loops the array we give it:
```
let legalFunction = (person) => person.us ? person.age >= 21 : person.age >= 18;

let legalIncluded = people.map((person) => {
    // set the new legal key equal to the return of the function we just set
    person.legal = legalfunction(person);

    // return this person but with the legal key added
    return person;
});
```

- Again if we ```console.table()``` this we get:
![Image of Yaktocat](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/console_table_tf.jpg)

- If you check, all the values are correct and our new array has all the information we need. This is of course a simple example of what the map function actually does, if you can run a function for every element in an array you can literally do anything, so if you wanted add 10 years to each person you could simply do:
```javascript
let increaseAge = people.map((person) => {
    // set the age key equal it plus 10
    person.age = person.age + 10;
    return person;
});
```

**6. reduce() the Array**
---
```javascript

```

**7. Other Important Array Methods**
---
```javascript

```


