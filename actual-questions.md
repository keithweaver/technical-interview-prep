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
