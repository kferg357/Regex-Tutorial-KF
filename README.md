# Regex Tutorial on What JavaScript Regex is.

The purpose of this tutorial is to discuss and explain a specific Regex but before we engage in this tutorial lets define Regex. A regular expression **(regex or regexp)**, is a sequence of characters that specifies a search pattern. Usually such patterns are used by string-searching algorithms for **"find"** or **find and replace** operations on strings, or input validation. It is a technique developed in theoretical computer science and formal language theory.


## Summary 

In this tutorial the regex I will be describing is JavaScript Regex. In this tutorial will explain the intricate scope and the particulars of JavaScript Regex.  Some content that we will discuss pertaining to JavaScript Regex are anchors, quantifiers, grouping constructs, bracket expressions, character classes, the OR operator, flags and character escapes. The following snippet is a regex ro prepend HTTP to Hyperlink.

```md
/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/
 ```

 Whether your're working in JavaScript, Ruby or PHP, this regular expression **(regex)** can provide very helpful. It will check any URL string to see if it has an HTTP/HTTPS prefix, and if not, prepend it accordingly.


## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)


## Regex Components 


### Anchors

The caret ^ and dollar $ characters have special meaning in a regexp. They are called “anchors”.

The caret ^ matches at the beginning of the text, and the dollar $ – at the end.

Anchors do not match any characters, they match a position before or after characters. 
```md
`/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`
```

In this example of an anchor we are trying to match an HTML TAG, the expression is testing to see if the string begins with the character of ```<```. We know this do to the fact of the caret ^ comes before the character (<) as followed. ``` ^<``` this expression would come back true because the information of the string does start with the character ```<```.

An example of a anchor thats not done the correct way or one that would return a false output using the caret ^ is as followed.

```md
/^J([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/
console
```

In this example the expression would check to see if string begins with a ```<```, which it does not. The console log would return falce because the string begins with the letter J.

???????CHANGE  In this next example the anchor of $ should be after the last character in this string. The expression will test to see if this is correct. 

```m
/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/
```
This output would return true because ```)$/``` matches the last character in the string of being ```)```.

### Quantifiers

What is the definition of quantifier. Quantifiers match number of instances of a character (letter or number), group or character class(allows you to match symbols) in a string. Quantifiers dont just quantify some given pattern, but instead the pattern immediately preceding them. Before we dive any further lets present a table of quantifiers and their meanings to better help you follow the tutorial

```m
**Quantifer	Meaning**

(+)	  Matches its preceding pattern for one or more number of times.

(*)   	Matches its preceding pattern for zero or more number of times.

?	  Matches its preceding pattern for zero or one number of times.

{n}  	Matches its preceding pattern exactly for n number of times.
 
{s, e}	 Matches its preceding pattern for s to e number of times.

{s,}  	Matches its preceding pattern for s or more number of times.
```

The quantifier of ```+``` takes the preceding pattern and quantifies it for one or more number of times. Example as followed.

```m
'/a+/' will match the strings of 'a', 'aa', 'aaa' etc... since the pattern preceding '+', which is 'a', will be looked for one or more times in the test string.

another example to help with real life application is as followed.
'/ca+t/' will match the strings 'cat', 'caat', 'caaat', 'caaaaat' etc...
The expression will look for a 'c' followed by 'a', one or more times, and then  finally 't'. At 't' the searching will end and then we will get the matched substring returned.

In both of these examples 'a' has been quantified by the ```+``` quantifier whose range is from 1 to infinity.
 ```


 The quantifier of ```*``` matches its preceding pattern for zero or more number of times. Unlike ```+```, it matches even those substrings where the preceind expression nver appears. It has the range  ```0-∞```. Example is as followed.

 ```m
 /^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/

In this code snippet I take a section out and talk about the quantifier of *.  The section of '+)*(' matches the string of '+(', '+)(', '+))(', '+)))(' etc. The first match here is '+(', it has zero occurances of the character ')' and will only mathc the quantifier '*', but not '+'.
```
*The '+' needs at least one occurence of its preceing character whereas '*' **needs NONE.**

### Grouping Constructs

Group Cpnstructs delineate (exact position using border or boundary)the subexpression and capture the substrings of an input string. Group contructs are determined by parentheses ```()```. Group Constructs can be use for the following: 

* Match a subexpression that is repeated in the input string.

```m

      string pattern = @"(\w+)\s(\1)\W";
      string input = "He said that that was the the correct answer.";
      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.IgnoreCase))
         Console.WriteLine("Duplicate '{0}' found at positions {1} and {2}.",
                           match.Groups[1].Value, match.Groups[1].Index, match.Groups[2].Index);
```
### In this string there are 2 subexpressions


1. (\w+) this subexpression will match one or more word characters. This is the first capturing group._ This is searching for any word character(underscore or aplhaunumeric character)


2. (\1) this will match the string in the first captured group. This is the second captured group. The backreference \1 (backslash one) references the first capturing group. \1 matches the exact same text that was matched by the first capturing group.



* Applied to a quantifier to a subexpression that has multiple regular expression language elements.

```md
N/A
```


* Include a subexpression in the string that is returned by the Regex.Replace and Match.Result metheod.

```md
N/A
```



* Retriece individual subexpressins from the Match.Group property and process them separately from the matched text as a whole.

```m
string pattern = @"(\w+)\s(\1)\W";
      string input = "He said that that was the the correct answer.";
      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.IgnoreCase))
         Console.WriteLine("Duplicate '{0}' found at positions {1} and {2}.",
                           match.Groups[1].Value, match.Groups[1].Index, match.Groups[2].Index);
```

1. ```(\w+)``` is being checked in the console.log where ```'match.Group[1].Value, match.Group[1].Index.```

2. ```(\1)``` is being checked in the console.log where ```match.Groups[2].Index)```.


### Bracket Expressions

A bracket expression is a list of characters enclosed by [].
Inside a character class, only the character class metacharacters (backslash, circumflex anchor and hyphen) have special meaning.

You must use a backslash when you use character class metacharacters as literals inside a character class only. Square brackets that are used as literals must always be escaped with backslash, both inside and outside a character class.

```m
For example, [[abc] should be written: [\[abc]
```

### Character classes

A character class (also called character set) defines a set of characters, any one of which can occur in an input string for a match to succeed. The regular expression language in . NET supports the following character classes: Positive character groups. A character in the input string must match one of a specified set of characters.

You can also create your own character classes using [ ]:

```m
[abc]: matches a, b, or c.
[a-z]: matches every character between a and z (in Unicode code point order).
[^abc]: matches anything except a, b, or c.
[\^\-]: matches ^ or -.
There are a number of pre-built classes that you can use inside []:

[:punct:]: punctuation.
[:alpha:]: letters.
[:lower:]: lowercase letters.
[:upper:]: upperclass letters.
[:digit:]: digits.
[:xdigit:]: hex digits.
[:alnum:]: letters and numbers.
[:cntrl:]: control characters.
[:graph:]: letters, numbers, and punctuation.
[:print:]: letters, numbers, punctuation, and whitespace.
[:space:]: space characters (basically equivalent to \s).
[:blank:]: space and tab.
```

### The OR Operator

The OR operator is a Boolean operator which would return the value TRUE or Boolean value of 1 if either or both of the operands are TRUE or have Boolean value of 1. The OR operator can also be used in combination with other logical operators. Or is expressed using ```| or ||```. Here is an example to follow.

```m
^I like (dogs|penguins), but not (lions|tigers).$

The above expression will match the following strings.
I like dogs, but not lions.
I like dogs, but not tigers.
I like penguins, but not lions.
I like penguins, but not tigers.
```

However, there is an unintended side-effect of our grouping and alternation, as written above. This pattern will match any combination of the terms we’ve supplied, as expected, but it will also store those matches into match groups for later inspection.

If you don’t want your grouping and alternation to interfere with other numbered groups in your expression, each “or” group must be prefixed with ? . Here is an example. 
```m
^I like (?:dogs|penguins), but not (?:lions|tigers).$
```

You can also combine alternation with look-ahead and look-behind statements, notice that we are using both positive and negative look-aheads in order to restrict the value of what is matched by the word character class ```\\w+```. Here is an example.

```m
^I like (?=dogs|penguins)\\w+, but not (?!dogs|penguins)\\w+$
```

### Flags

Flags are tokens that modify its behavior of searching. Flags are optional parameters that we can add to a plain expression to make it search in a different way. Each flag is denoted by a single alphabetic character, and serves different purposes in modifying the expression's searching behaviour. Here is a table of 6 flags.


* i - Ignore Casing	Makes the expression search case-insensitively.

```m
var str = "Hello world! This 'Hello World' convention is quite common in introducing programming languages.";
var exp = /hello/;

The flag needed to modify the expression to make /hello/ match "Hello" would be to add i, as followed: "exp = /hello/i;"
Thus making hello and Hello the same.

```


* g - Global	Makes the expression search for all occurences. hence 
(global). By default, when a regex engine finds the first match for a given pattern in a given test string, it terminates and prevents any further searching. To modify this behaviour, we have at our dispense the g flag.

```m
var str = "home sweet home";
var replacedStr = str.replace(/home/g, "cake");
new str = "cake sweet cake";
```


* s - (single-line mode) Dot All Makes the wild character . match newlines as well.
The flag s means dot all. That is, it makes the . dot character (technically refered to as the wildcard character) match everything, even newlines. In other words, with the s flag, the dot matches all possible characters.

```m
For instance, the regexp A.B matches A, and then B with any character between them, except a newline \n:

alert( "A\nB".match(/A.B/) ); // null (no match)
alert( "A\nB".match(/A.B/s) ); // A\nB (match!)
```



* m - Multiline-mode.	Makes the boundary characters ^ and $ match the beginning and  ending of every single line instead of the beginning and ending of the whole string.

```m
Without the flag m only the first digit is matched.

let str = `1st place: Winnie
2nd place: Piglet
3rd place: Eeyore`;

alert( str.match(/^\d/g) ); // 1

The pattern /^\d/gm takes a digit from the beginning of each line:
let str = `1st place: Winnie
2nd place: Piglet
3rd place: Eeyore`;

alert( str.match(/^\d/gm) ); // 1, 2, 3
```


* y - Sticky	Makes the expression start its searching from the index indicated in its lastIndex property.

```m
var str = "Cats love cats, and we love cats."
"Cats love cats, and we love cats." in this expression all the words cat match.

var str = "Cats love cats, and we love cats."
var exp = /cats/igy;
exp.lastIndex = 4;
the new string would look like this:
var str = "Cats love cats, and we love cats." but will only the second and third reccurances of cats matching 
```

* u - Unicode	Makes the expression assume individual characters as code points, not code units, and thus match 32-bit characters as well.
This means that with the u flag set, we can get our expressions to behave normally on characters that are outside the BMP range of the UTF-16 encoding.
The u flag is only required in special cases, where test strings contain characters outside the normal range of the UTF-16 character set. It's not a flag you'll be using very often.
Consider the simple example below to understand how u works.

```m
Construct an expression to match all occurences of the non-BMP character 𐍅 in a given test string.
Since 𐍅 is outside the range of UTF-16's normal characters, we will need to use the unicode flag u in order to match it. And we will also need the global flag g to match all such occurences.

The expression to solve this problem is "/\u{10345}/ug."
```

### Character Escapes

Character escaping is what allows certain characters (reserved by the regex engine for manipulating searches) to be literally searched for and found in the input string. Escaping depends on context, therefore this example does not cover string or delimiter escaping. A backslash ```\``` is used to denote character classes, e.g. ```\d```. So it’s a special character in regexps (just like in regular strings).

There are other special characters as well, that have special meaning in a regexp. They are used to do more powerful searches. Here’s a full list of them: ```[ \ ^ $ . | ? * + ( )```.

Let’s say we want to find literally a dot. Not “any character”, but just a dot.
To use a special character as a regular one, prepend it with a backslash: \..
That’s also called “escaping a character”.

```m
alert( "Chapter 5.1".match(/\d\.\d/) ); // 5.1 (match!)
alert( "Chapter 511".match(/\d\.\d/) ); // null (looking for a real dot \.)
```

Parentheses are also special characters, so if we want them, we should use ```\```(. The example below looks for a string ```"g()"```:

```m
alert( "function g()".match(/g\(\)/) ); // "g()"
```

## Author

The author of this READme.MD is Kenneth A. Ferguon. I am currently a student at UNC Coding Bootcamp. here is the link to my profile ?????????????
