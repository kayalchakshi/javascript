# javascript string padding

String padding
Two instance methods were added to String — String.prototype.padStart and String.prototype.padEnd — that allow appending/prepending either an empty string or some other string to the start or the end of the original string.

Example:
      'someString'.padStart(numberOfCharcters [,stringForPadding]); 
      '5'.padStart(10) // '          5'
      '5'.padStart(10, '=$') //'=$=$=$=$=5'
      '5'.padEnd(10) // '5         '
      '5'.padEnd(10, '=$') //'5=$=$=$=$='
      
⚠️ padStart and padEnd on Emojis and other double-byte chars
 
  Emojis and other double-byte chars are represented using multiple bytes of unicode. So padStart and padEnd might not work as expected!⚠️

  For example: Let’s say we are trying to pad the string heart to reach 10 characters with the ❤️ emoji. The result will look like below:

      //Notice that instead of 5 hearts, there are only 2 hearts and 1 heart that looks odd!

      'heart'.padStart(10, "❤️"); // prints.. '❤️❤️❤heart'

  This is because ❤️ is 2 code points long ('\u2764\uFE0F' )! The word heart itself is 5 characters, so we only have a total of 5 chars left to pad. So what happens is that JS pads two hearts using '\u2764\uFE0F' and that produces ❤️❤️. For the last one it simply uses the first byte of the heart \u2764 which produces ❤

  So we end up with: ❤️❤️❤heart
  
  
Object.getOwnPropertyDescriptors

      This method returns all the details (including getter getand setter set methods) for all the properties of a given object. The main motivation to add this is to allow shallow copying / cloning an object into another object that also copies getter and setter functions as opposed to Object.assign .

   Object.assign shallow copies all the details except getter and setter functions of the original source object.

   The example below shows the difference between Object.assign and Object.getOwnPropertyDescriptors along with Object.defineProperties to copy an original object Car into a new object ElectricCar . You’ll see that by using Object.getOwnPropertyDescriptors ,discount getter and setter functions are also copied into the target object.
   
         var Car = {
       name: 'BMW',
       price: 1000000,
       set discount(x) {
        this.d = x;
       },
       get discount() {
        return this.d;
       },
      };
      //Print details of Car object's 'discount' property
      console.log(Object.getOwnPropertyDescriptor(Car, 'discount'));
      //prints..
      // { 
      //   get: [Function: get],
      //   set: [Function: set],
      //   enumerable: true,
      //   configurable: true
      // }
      //Copy Car's properties to ElectricCar using Object.assign
      const ElectricCar = Object.assign({}, Car);
      //Print details of ElectricCar object's 'discount' property
      console.log(Object.getOwnPropertyDescriptor(ElectricCar, 'discount'));
      //prints..
      // { 
      //   value: undefined,
      //   writable: true,
      //   enumerable: true,
      //   configurable: true 

      // }
      //⚠️Notice that getters and setters are missing in ElectricCar object for 'discount' property !👎👎
      //Copy Car's properties to ElectricCar2 using Object.defineProperties 
      //and extract Car's properties using Object.getOwnPropertyDescriptors
      const ElectricCar2 = Object.defineProperties({}, Object.getOwnPropertyDescriptors(Car));
      //Print details of ElectricCar2 object's 'discount' property
      console.log(Object.getOwnPropertyDescriptor(ElectricCar2, 'discount'));
      //prints..
      // { get: [Function: get],  👈🏼👈🏼👈🏼
      //   set: [Function: set],  👈🏼👈🏼👈🏼
      //   enumerable: true,
      //   configurable: true 
      // }
      // Notice that getters and setters are present in the ElectricCar2 object for 'discount' property!
      
