# Sorting

##### Code for all programs below
```
public static void main(String[] args) {
	Integer[] testInts = generateTestIntegerList();
	
	printArrayOfIntegers(testInts);
	
	//Example of running a sorting algorithm
	Integer[] sortedByBubbleSort = bubbleSort(testInts);
	printArrayOfIntegers(sortedByBubbleSort);
}

/**
 * Displays the list of integers in console friendly way. Wrapped
 * square brackets around with commas separating.
 * 
 * @param listOfIntegers - An array of Integers
 */
public static void printArrayOfIntegers(Integer[] listOfIntegers){
	String strBeingPrinted = "";
	for(int i=0;i<listOfIntegers.length;i++){
		if(strBeingPrinted.length() > 0){
			strBeingPrinted += ",";
		}
		strBeingPrinted += String.valueOf(listOfIntegers[i]);
	}
	System.out.println("[" + strBeingPrinted + "]");
}
	
/**
 * Used for testing sorting.
 * @return A random size array of integers that contains random integers
 */
public static Integer[] generateTestIntegerList(){
	int maxSize = (int)(Math.random() * 50 + 1);
	
	Integer[] testIntegerList = new Integer[maxSize];
	
	for(int i=0;i<maxSize;i++){
		int randomInt = (int) (Math.random() * 25 + 1);
		testIntegerList[i] = randomInt;
	}
	
	return testIntegerList;
}
```


### Bubble Sort


```	
/**
 * Bubble Sort algorithm will loop through n (size of array) 
 * to find highest value and move it to the right.
 * 
 * @param listOfIntegers - Unsorted array of Integers
 * @return - Sorted array of integers
 */
public static Integer[] bubbleSort(Integer[] listOfIntegers){
	int temp = 0;
	
	for(int i = 0;i < listOfIntegers.length;i++){
		for(int j = 1;j < (listOfIntegers.length - i);j++){
			
			if(listOfIntegers[j-1] > listOfIntegers[j]){
				temp = listOfIntegers[j];
				listOfIntegers[j] = listOfIntegers[j-1];
				listOfIntegers[j-1] = temp;
			}
			
		}
	}
	return listOfIntegers;
}
```



### Quick Sort

Best Case: O(n log n)
Worst Case: O(n^2)

Sudo
1. Pick a pivot (most right element)
2. Start at the lowest index
3. Put all elements lower to the left
4. Put all elements higher to the right
5. If you find a value lower than the pivot, find an element that is higher than the pivot starting from the lowest index.
6. If value is greater than pivot leave it
7. if current == pivote, put the pivot in the center

https://www.youtube.com/watch?v=aQiWF4E8flQ

```
/**
 * QuickSort implementation to sort a list in n log n.
 * 
 * @param listOfIntegers - An array of integers with at least one
 * @param low - Lowest value in the current list
 * @param high - The highest position in the current list
 * @return - Returns a sorted list
 */
public static Integer[] quickSort(Integer[] listOfIntegers, int low, int high){
	if(listOfIntegers.length <= 1){
			return listOfIntegers;
	}
		
	int i = low;
	int j = high;
	int pivot = listOfIntegers[low + (high-low)/2];//find middle elemnt
	while (i <= j) {
		while (listOfIntegers[i] < pivot) {//item in left list is smaller than pivot move on
			i++;
		}
		while (listOfIntegers[j] > pivot) {//item in right list is larger than pivot move on
			j--;
		}
		if (i <= j) {
			int temp = listOfIntegers[i];
			listOfIntegers[i] = listOfIntegers[j];
		    listOfIntegers[j] = temp;
		    
			i++;
			j--;
		}
	}
	if (low < j){
		quickSort(listOfIntegers, low, j);
	}
	if (i < high){
		quickSort(listOfIntegers, i, high);
	}
	
	return listOfIntegers;
}
```


### Merge Sort

Best Case: O(n log n)
Worst Case: O(n log n)

1. Split the array into two
2. Compare the first value of the two halfs
3. Remove the larger one
4. Compare the first value of the two half again (repeat till either side is empty)

https://upload.wikimedia.org/wikipedia/commons/c/cc/Merge-sort-example-300px.gif

```
/**
 * Merge sort implementation to sort a list of integers
 * @param listOfIntegers - The integers that need to be sorted (or part)
 * @param low - the lowest position
 * @param high - the highest position
 * @return - the sorted list
 */
public static Integer[] mergeSort(Integer[] listOfIntegers, int low, int high){
	
	if(listOfIntegers.length <= 1){
		return listOfIntegers;
	}
	
	if (low < high) {
		int middle = low + (high - low) / 2;
		mergeSort(listOfIntegers, low, middle);
		mergeSort(listOfIntegers, middle + 1, high);
		//Combine the two
		Integer[] helper = new Integer[listOfIntegers.length];
		for (int i = low; i <= high; i++) {
			helper[i] = listOfIntegers[i];
		}
		
		int i = low;
		int j = middle + 1;
		int k = low;
		
		while (i <= middle && j <= high) {
			if (helper[i] <= helper[j]) {
				listOfIntegers[k] = helper[i];
				i++;
			}else{
				listOfIntegers[k] = helper[j];
				j++;
			}
			k++;
		}
		while (i <= middle) {
			listOfIntegers[k] = helper[i];
			k++;
			i++;
		}
	}
	
	return listOfIntegers;
}
```



### QuickSort vs MergeSort

Pros for QuickSort:
- Quicksort in particular requires little additional space and exhibits good cache locality, and this makes it faster than merge sort in many cases.
- it’s very easy to avoid quicksort’s worst-case run time of O(n2) almost entirely by using an appropriate choice of the pivot – such as picking it at random (this is an excellent strategy).
- Extremely fast on average

Con for QuickSort:
- O(n2) worst-case runtime and O(nlogn) average case runtime
- In the worst case, could cause a stack overflow

Pros for Merge Sort:
- Guaranteed to be O(n.log n)

Cons for Merge Sort:
- Not as fast on average as Quick sort


### Heap Sort
- Go to the last parent (bottom right), working your way back level and towards the left.
- if the child (pick biggest) > parent, swap them
- doing stuff above once
- put everything in the array, root is position 1 and its kids are x*2 (x = being parent/current) & (x*2) +1


Reference: 

http://www.brucemerry.org.za/manual/algorithms/sorting.html

https://www.youtube.com/watch?v=PqS5T9ZKZno