
[Oracle Official Tutorial](https://docs.oracle.com/javase/tutorial/essential/regex/index.html)

##Notes

	Enter your regex: a?
	Zero-Length Matches

	Enter input string to search: ababaaaab
	I found the text "a" starting at index 0 and ending at index 1.
	I found the text "" starting at index 1 and ending at index 1.
	I found the text "a" starting at index 2 and ending at index 3.
	I found the text "" starting at index 3 and ending at index 3.
	I found the text "a" starting at index 4 and ending at index 5.
	I found the text "a" starting at index 5 and ending at index 6.
	I found the text "a" starting at index 6 and ending at index 7.
	I found the text "a" starting at index 7 and ending at index 8.
	I found the text "" starting at index 8 and ending at index 8.
	I found the text "" starting at index 9 and ending at index 9.

	Enter your regex: a*
	Enter input string to search: ababaaaab
	I found the text "a" starting at index 0 and ending at index 1.
	I found the text "" starting at index 1 and ending at index 1.
	I found the text "a" starting at index 2 and ending at index 3.
	I found the text "" starting at index 3 and ending at index 3.
	I found the text "aaaa" starting at index 4 and ending at index 8.
	I found the text "" starting at index 8 and ending at index 8.
	I found the text "" starting at index 9 and ending at index 9.

	Enter your regex: a+
	Enter input string to search: ababaaaab
	I found the text "a" starting at index 0 and ending at index 1.
	I found the text "a" starting at index 2 and ending at index 3.
	I found the text "aaaa" starting at index 4 and ending at index 8.



	Greedy	Reluctant	Possessive	Meaning
	X?	    X??	        X?+	        X, once or not at all
	X*	    X*?	        X*+	        X, zero or more times
	X+	    X+?	        X++	        X, one or more times
	X{n}	X{n}?	    X{n}+	    X, exactly n times
	X{n,}	X{n,}?	    X{n,}+	    X, at least n times
	X{n,m}	X{n,m}?	    X{n,m}+	    X, at least n but not more than m times

	Greedy quantifiers are considered "greedy" because they force the matcher to read in, or eat, the entire input string prior to attempting the first match.
	If the first match attempt (the entire input string) fails, the matcher backs off the input string by one character and tries again, repeating the process until a match is found or there are no more characters left to back off from.
	Depending on the quantifier used in the expression, the last thing it will try matching against is 1 or 0 characters.

	The reluctant quantifiers, however, take the opposite approach: They start at the beginning of the input string, then reluctantly eat one character at a time looking for a match.
	The last thing they try is the entire input string.

	Finally, the possessive quantifiers always eat the entire input string, trying once (and only once) for a match.
	Unlike the greedy quantifiers, possessive quantifiers never back off, even if doing so would allow the overall match to succeed.

	Enter your regex: .*foo  // greedy quantifier
	Enter input string to search: xfooxxxxxxfoo
	I found the text "xfooxxxxxxfoo" starting at index 0 and ending at index 13.

	Enter your regex: .*?foo  // reluctant quantifier
	Enter input string to search: xfooxxxxxxfoo
	I found the text "xfoo" starting at index 0 and ending at index 4.
	I found the text "xxxxxxfoo" starting at index 4 and ending at index 13.

	Enter your regex: .*+foo // possessive quantifier
	Enter input string to search: xfooxxxxxxfoo
	No match found.

