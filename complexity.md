# Complexity

##### Big O

Operation: O(1)

Loop: O(n)

Loop in Loop: O(n^2)

######## Log n

The most common attributes of logarithmic running-time function are that:
- the choice of the next element on which to perform some action is one of several possibilities, and
- only one will need to be chosen.
or 
- the elements on which the action is performed are digits of n

O(log n): Given a person's name, find the phone number by picking a random point about halfway through the part of the book you haven't searched yet, then checking to see whether the person's name is at that point. Then repeat the process about halfway through the part of the book where the person's name lies. (This is a binary search for a person's name.)

O(n log n): There was a mix-up at the printer's office, and our phone book had all its pages inserted in a random order. Fix the ordering so that it's correct by looking at the first name on each page and then putting that page in the appropriate spot in a new, empty phone book.


		        Array (Unsorted) 	Linked List 	Array (Sorted) 	Binary Search Tree (Balanced)
		Search  	O(n)   				O(n) 			O(log n) 			O(log n)
		Insert 		O(1) 				O(1) 			O(n) 				O()
		Remove 		O(n) 				O(n) 			O(n) 				O()



Best explanation http://stackoverflow.com/questions/2307283/what-does-olog-n-mean-exactly

