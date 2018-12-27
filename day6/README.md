![cover](./cover.png)

# Day 6 

## Questions for today

Welcome back to the Day 3 of Daily Codes, as you might have noticed we are slowly stepping up our game in Strings. So today let's do 3 cool questions that seems pretty straightforward while reading the question but can be a little challenging when you actually try to solve them

#### Part A - Sentence Capitalization 

**Question** - Write a program to capitalize the first letter of each word in the string.

#### Part B - Word Reversal

**Question** - Given a sentence, Write a program to reverse each word in it.

#### Part C - Anagram Check

**Question** - Write a program to check whether the two provided strings are anagrams of each other. (Do not ignore the letter case)

![ques](./ques.png)

## Part A -- Sentence Capitalization

**Question** - Write a program to capitalize the first letter of each word in the string.

## JavaScript Implementation

### [Solution 1](./JavaScript/sentenceCap1.js)

```js
/**
 * @author MadhavBahlMD
 * @date 27/12/2018
 */

function capitalize (str) {
    // spit the string to array
    let wordArr = str.split(' ');
    
    // loop through each element of array and capitalize the first letter

    for (let i=0; i<wordArr.length; i++) {

        // Some people might proceed like this, but strings are immutable
        // let currentWord = wordArr[i];
        // currentWord[0] = currentWord[0].toUpperCase();
        // console.log(currentWord);

        // Append the first letter (capitalized)
        let currentWord = '';
        currentWord += wordArr[i][0].toUpperCase();
        
        // Append the rest of the word (can be easily done by String slice)
        for (let j=1; j<wordArr[i].length; j++) {
            currentWord += wordArr[i][j];
        }

        // replace the current word by currentWord
        wordArr[i] = currentWord;
    }

    // join the array into string
    return wordArr.join(' ');
}

console.log(capitalize ('hello world'));
```

### [Solution 2](./JavaScript/sentenceCap1.js)

```js
/**
 * @author MadhavBahlMD
 * @date 27/12/2018
 */

function capitalize (str) {
    // declare an empty array
    let capitalied = [];

    // loop through each word and capitalize the first letter
    for (let word of str.split(' ')) {
        capitalied.push(word[0].toUpperCase() + word.slice(1));
    }

    // join the array into string
    return capitalied.join(' ');
}
```

### [Solution 3](./JavaScript/sentenceCap1.js)

```js
/**
 * @author MadhavBahlMD
 * @date 27/12/2018
 */

 function capitalize (str) {
    let result = str[0].toUpperCase();

    for (let i=1; i<str.length; i++) {
        if (str[i-1] === ' ') {
            result += str[i].toUpperCase();
        } else { 
            result += str[i];
        }
    }

    return result;
}
```

## Java Implementation

### [Solution 1](./Java/SentenceCap1.java)

```java
/**
 * @author MadhavBahlMD
 * @date 27/12/2018
 */

import java.util.Scanner;

public class SentenceCap1 {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        System.out.print("Enter the sentence: ");
        String str = input.nextLine();

        String[] words = str.split("\\s+");

        for (int i=0; i<words.length; i++) {
            words[i] = Character.toUpperCase(words[i].charAt(0)) + words[i].substring(1, words[i].length());
        }

        // Join the array
        System.out.print(String.join(" ", words));
    }
}

```

### [Solution 2](./Java/SentenceCap2.java)

```java
/**
 * @author MadhavBahlMD
 * @date 27/12/2018
 */
 
import java.util.Scanner;

public class SentenceCap2 {
    public static void main(String[] args) {
        Scanner input = new Scanner (System.in);
        System.out.print("Enter the sentence: ");
        String sentence = input.nextLine();
        String capitalized = "";

        for (int i=0; i<sentence.length(); i++) {
            if (i==0)   capitalized += Character.toUpperCase(sentence.charAt(i));
            else {
                if (sentence.charAt(i-1) == ' ') {
                    capitalized  += Character.toUpperCase(sentence.charAt(i));
                } else {
                    capitalized += sentence.charAt(i);
                }
            }
        }

        // Print the results
        System.out.println("Capitalized String is: " + capitalized);
    }
}
```

## Part B -- Word Reversal

**Question** - Given a sentence, Write a program to reverse each word in it.

## JavaScript Implementation

### [Solution 1](./JavaScript/wordRev1.js)

```js
/**
 * @author MadhavBahlMD
 * @date 27/12/2018
 */

function wordRev (line) {
    // Split the line
    let words = line.split(' ');

    // reverse each word
    for (let i=0; i<words.length; i++) {
        words[i] = words[i].split('').reverse().join('');
    }

    // Join and return
    return words.join(' ');
}

console.log (wordRev("hello world Greetings"));
```

### [Solution 2](./JavaScript/wordRev2.js)

```js
/**
 * @author MadhavBahlMD
 * @date 27/12/2018
 */

 function wordRev (line) {
    let reversed = [];

    for(let word of line.split(' ')) {
        reversed.push(word.split('').reverse().join(''));
    }

    return reversed.join(' ');
}

console.log (wordRev("  hello  wow   world Greetings"));
```

### [Solution 3](./JavaScript/wordRev3.js)

```js
/**
 * @author MadhavBahlMD
 * @date 27/12/2018
 */

// Without inbuilt reverse or split, a straightforward method

function wordRev (line) {
    // iterate through the string and add each word in a new array (splitting it on white space)
    let words = [], count = 0, word = '';

    for (let i=0; i<line.length; i++) {
        if (line[i] !== ' ') {
            word += line[i];
        } else {
            words[count] = word;
            word = '';
            count++;
        }
    }
    // Add the last word as well to the words array as well
    words[count] = word;
    count++;

    // Reverse the words
    let temp;
    for (let i=0; i<count; i++) {
        temp = '';
        for (let j=words[i].length-1; j>=0; j--) {
            temp += words[i][j];
        }
        words[i] = temp;
    }

    // join the elements (Ok, let's not use the traditional join() method -_-)
    let reversed = '';
    for (let i=0; i<count; i++) {
        if (i!=count-1) {
            reversed += words[i] + ' ';
        } else {
            reversed += words[i];
        }
    }

    // print the result
    return reversed;
}

console.log(wordRev ('hello world greetings'));
```

## Java Implementation

### [Solution](./Java/WordRev.java)

```java
/**
 * @author MadhavBahlMD
 * @date 27/12/2018
 */

import java.util.Scanner;
import java.lang.*;

public class WordRev {
    public static void main(String[] args) {
        Scanner input = new Scanner (System.in);
        System.out.print("Enter the sentence: ");
        String sentence = input.nextLine();

        String[] words = sentence.split("\\s+");
        String reversed;

        for (int i=0; i<words.length; i++) {
            reversed = "";
            for (int j=0; j<words[i].length(); j++) {
                reversed = words[i].charAt(j) + reversed;
            }
            words[i] = reversed;
        }

        String wordsReversed = String.join(" ", words);
        System.out.println("String with reversed words: " + wordsReversed);
    }
}
```

## Part C -- Anagram Check

**Question** - Write a program to check whether the two provided strings are anagrams of each other.