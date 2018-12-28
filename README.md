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
      
