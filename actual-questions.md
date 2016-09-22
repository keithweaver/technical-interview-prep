# Questions


#### Question

Use the shorest unique prefix to represent each word in the array 

input: ["zebra", "dog", "duck",”dot”] 

output: {zebra: z, dog: do, duck: du} 


#### My Solution

```
/**
 * Finds the shortest unique prefix for a word.
 * 
 * @param words
 *            - An array of fully formated words (no extra spaces)
 */
public static String[][] shortestUniquePrefix(String[] words) {
	Trie trieOfWords = new Trie();// TODO think of better variable name

	for (String word : words) {
		trieOfWords.insert(word);
	}

	String[][] prefixes = new String[words.length][2];
		
	for (int wordCount=0;wordCount < words.length;wordCount++) {
		String word = words[wordCount];
			
		for(int i = 0;i < word.length();i++){
			String prefixLookingUp = word.substring(0, i+1);
			
			TrieNode currentTrie = trieOfWords.searchNode(prefixLookingUp);
				
			if(currentTrie.numberOfChildern() < 2){
				prefixes[wordCount][0] = word;
				prefixes[wordCount][1] = prefixLookingUp;
				break;
			}
		}
			
	}
		
	return prefixes;
}
```

```
import java.util.HashMap;
import java.util.Map;

public class Trie {
	private TrieNode root;

	public Trie() {
		root = new TrieNode();
	}

	// Inserts a word into the trie.
	public void insert(String word) {
		HashMap<Character, TrieNode> children = root.children;

		for (int i = 0; i < word.length(); i++) {
			char c = word.charAt(i);

			TrieNode t;
			if (children.containsKey(c)) {
				t = children.get(c);
			} else {
				t = new TrieNode(c);
				children.put(c, t);
			}

			children = t.children;

			// set leaf node
			if (i == word.length() - 1)
				t.isLeaf = true;
		}
	}

	public TrieNode searchNode(String str) {
		Map<Character, TrieNode> children = root.children;
		TrieNode t = null;
		for (int i = 0; i < str.length(); i++) {
			char c = str.charAt(i);
			if (children.containsKey(c)) {
				t = children.get(c);
				children = t.children;
			} else {
				return null;
			}
		}

		return t;
	}
}

```

#### Question
Find the anagrams from a list of strings 
Input : {"tea", "ate", "eat", "apple", "java", "vaja", "cut", "utc"} 
Output : {"tea", "ate", "eat","java", "vaja", "cut", "utc"}

#### My Solution
```
import java.util.ArrayList;

public class Anagram {
	
	public static void main(String[] args) {
		String[] testAnogram = new String[]{"tea", "ate", "eat", "apple", "java", "vaja", "cut", "utc"};
		ArrayList<String> response = getValidAnagram(testAnogram);
		for(String word:response){
			System.out.println(word);
		}
	}
	/*
	 * Possible solutions:
	 * Sort each word (Loop through minimum twice (one to sort, one to find))
	 * Find ascii values, but they'd need to be matched with other equivalent lengths
	 * Cant use tries cause unless sorted
	 */
	/**
	 * Finds words that are anagrams. (Words have same characters).
	 * @param words
	 * @return
	 */
	public static ArrayList<String> getValidAnagram(String[] words){
		ArrayList<String> validAnagram = new ArrayList<>();
		for(String word:words){
			for(String innerWord:words){
				if(!word.equals(innerWord) && checkIfValidAnagram(word, innerWord)){
					if(!validAnagram.contains(word)){
						validAnagram.add(word);
					}
					if(!validAnagram.contains(innerWord)){
						validAnagram.add(innerWord);
					}
				}
			}
		}
		
		return validAnagram;
	}
	private static boolean checkIfValidAnagram(String wordOne, String wordTwo){
		if(wordOne.length() != wordTwo.length()){
			return false;
		}
		int totalAsciiValueOfWordOne = 0;
		int totalAsciiValueOfWordTwo = 0;
		for(int i=0;i<wordOne.length();i++){
			totalAsciiValueOfWordOne += (int) wordOne.charAt(i);
			totalAsciiValueOfWordTwo += (int) wordTwo.charAt(i);
		}
		if(totalAsciiValueOfWordOne != totalAsciiValueOfWordTwo){
			return false;
		}
		return true;
	}
	
}
```


#### Question
Write a routine that does secret santa in O(N) time.

#### My Solution
```
Shift every one down 1 elements so its N+1 and the last guy, move to the first position
Or
I'd actually go the other way, store user 1, then put user 2 in user 1 spot.
```


#### Question
Implement an online crossword puzzle solver.

#### My Solution

Not actually my solution, found on the internet (Link below).

```
The corssword problem is NP-Complete, so your best shot is brute force: just try all possibilities, and stop when a possibility is a valid. Return failure when you exhausted all possible solutions.


solve(words,grid):
   if words is empty:
       if grid.isValudSol():
          return grid
       else:
          return None
   for each word in words:
       possibleSol <- grid.fillFirst(word)
       ret <- solve(words\{word},possibleSol)
       if (ret != None):
          return ret
   return None



#pseudo-code
solve ( words , grid ) : solve ( words , grid , None ) 

solve ( words , grid , filledPositions ) :
    if words is empty :
        if grid is solved :
            return grid
        else :
            raise ( no solution )
    for ( current position ) as the first possible word position in grid 
            that is not of filledPositions :
        # note : a word position must have no letters before the word
            # 'before the word' means, eg, to the left of a horizontal word
            # no letters may be placed over a ' ' 
            # no letters may be placed off the grid
        # note : a location may have two 'positions' : one across , one down
        for each word in words :
            make a copy of grid
            try :
                fill grid copy, with the current word, at the current position
            except ( cannot fill position ) :
                break
            try :
                return solve ( words\{word} , grid copy , 
                        filledPositions+{current position} )
            except ( no solution ) :
                break
        raise ( no solution )
```
