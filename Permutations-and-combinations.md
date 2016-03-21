Permutations and combinations are very similar topics. They both involve combining groups of objects into different groups. For example, if you have a the String "ABC", it has six permutations:

	ABC
	ACB
	BAC
	BCA
	CAB
	CBA

However, it has only one combination:

	ABC

Do you see the difference? With permutations, the order matters.

To generate all the permutations of an ArrayList, you can use this code:
	
	void permute(ArrayList<Integer> list, int k, int len){
		for (int i = k; i < list.size(); i++) {
			Collections.swap(list, i, k);
			permute(list, k+1, len);
			Collections.swap(list, i, k);
		}

		if (k == len){
			printList(list, len);            
		}
	}

len is the length of the permutations and printList is a custom method that prints the values in the list, from index 0 to index len (exclusive). To modify this method for arrays or Strings, you need to manually swap the values at i and k instead of using Collections.swap().

To generate all the combinations of an array or ArrayList, you can use this:
	
	for (int subset = 0; subset < (1 << n); subset++) {
		for (int k = 0; k < n; k++) {
			int result = (1 << k) & subset;
			if (result != 0) {
				// The item at index k is in the current subset/combination.
			}
		}
	}

