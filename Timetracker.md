# Timetracker

* 2024-03-11
	* 7:45am PST - 8:30am PST
		* Create GH Repo for tracking time https://github.com/mejia-dev/capstone-time-tracker
		* Update goals list to include Flutter and Docker if there is time.
		* Begin watching [Angular for Beginners](https://www.youtube.com/watch?v=3qBXWUpoPHo)
			* Learned Angular history / concepts
			* Learned TypeScript history / concepts
	* 8:30am PST - 8:55am PST
		* Scrum. Discussed goals, additional reading, and assignments.
	* 8:55am PST - 9:40am PST
		* Read through homework on [LHTP](https://full-time.learnhowtoprogram.com/capstone/capstone-week-2/self-exploration-week-1-expectations).
		* Fill out [Capstone Sign-Up spreadsheet](https://docs.google.com/spreadsheets/d/12bYJwwhD-w-DBocdE0Fg4hQy8zMvYuK5mr8C7dk8-TU/edit#gid=0).
		* Watch [Demo Day Pitch video](https://www.youtube.com/watch?v=7u0cKqRPYhY).
		* Draft basic demo day pitch according to [LHTP lesson](https://full-time.learnhowtoprogram.com/capstone/capstone-week-2/capstones---preparing-your-pitch). 
		* Reviewed whiteboarding best practices and recursion.
	* 9:40am PST - 11:36am PST
		* [Whiteboarding Prompt 1](https://full-time.learnhowtoprogram.com/capstone/capstone-week-2/whiteboarding-practice---week-1#contiguous-subarray-with-greatest-sum)
			```javascript
			// Input: [-2, -3, 4, -1, -2, 1, 5, -3]
			// Ouput: 7 
			// The largest sum of a contiguous subarray is 7 (4 + -1 + -2 + 1 + 5 === 7)

			// DEFINITION: contiguous. adjective. con·​tig·​u·​ous kən-ˈtig-yə-wəs. : being in actual contact : touching along a boundary or at a point.

			// Time spent: 35 minutes.

			```
			* Spent quite a bit of time trying to understand "contiguous", how it differs from "consecutive" and what makes the array in the example "contiguous" since it definitely isn't consecutive and there are large gaps between the individual numbers in the array [4, -1, -2, 1, 5].
				* Looked at hints, not necessarily helpful in understanding what "contiguous" actually means.
				* Asked ChatGPT several times, still not entirely sure:
					```txt
					No problem! Understanding the difference between "consecutive" and "contiguous" can sometimes be a bit tricky, as they are related concepts but not quite the same.

					Consecutive: "Consecutive" refers to elements that follow one after the other in order, without skipping any elements in between. For example, in the sequence [1, 2, 3, 4, 5], all the numbers are consecutive because they follow one another in order without skipping any numbers.

					Contiguous: "Contiguous" refers to elements that are adjacent to each other and form a continuous sequence without any gaps in between. In other words, they are touching or next to each other in the sequence. For example, in the sequence [1, 2, 3, 4, 5], any subset like [2, 3, 4] or [3, 4, 5] is contiguous because the numbers are adjacent to each other without any gaps.

					In summary, while "consecutive" refers to the order of elements without gaps, "contiguous" refers to elements that are adjacent or touching each other without gaps. They often overlap in meaning but refer to slightly different aspects of sequence or array elements.
					```
				* Checked LHTP curriculum for prior use of the word, not finding it. 
				* [Contiguous memory](https://stackoverflow.com/questions/26998223/what-is-the-difference-between-contiguous-and-non-contiguous-arrays) makes at least some sense, but not entirely sure how it applies to arrays...
			* Genuinely stumped on the definition after half an hour of trying to figure it out.	I think once I understand the definition of contiguous, I will be able to figure out the problem relatively easily, but genuinely so confused. Will ask Erik / classmates later after other study has been completed.

		* [Whiteboarding Prompt 2](https://full-time.learnhowtoprogram.com/capstone/capstone-week-2/whiteboarding-practice---week-1#find-the-missing-number)
		```javascript
		// Input: arr = [1, 2, 3, 4, 6], N = 6
		// Output: 5 // The missing number

		// Steps to Solve:
		// 	- Find the problem number via foreach loop (just the number where itself + 1 doesn't equal the number after it)
		//	- return the problem number + 1

		// First attempt:
		function findMissing(array, N) {
			let problemNumber;
			for (let i = 0; i < array.length; i++) {
				if (array[i] + 1 != array[i + 1]) {
					problemNumber = array[i] + 1;
					break;
				}
			}
			return problemNumber;
		}

		// Ran in devtools, found the resultant number (5); Time spent: 5 minutes.
		// No hints used for solution. Unclear why the number N was needed since it is useless in solving the problem and is not needed even with the requirements. Will check hints to see if I missed something.
		// Checked hints. The suggestion from the hints seems to overcomplicate things. Seems like you'd essentially do it something like: 

		function findMissing(array, N) {
			let hashArray = new Array(N).fill(0); // there may be a better method for filling them all with 0s. This also doesn't seem to specifically be a "hash", but it's the best I could come up with...
			for (let i = 0; i < array.length; i++) {
        hashArray[array[i] - 1] = array[i]; // filling in each value in the hash array.
    	}
			for (let i = 0; i < hashArray.length; i++) {
        // finding the missing number
				if (hashArray[i] === 0) {
            return i + 1;
        }
    	}
		}

		// Overall, runtime appears to be the same between the two functions: O(n)
		// However, I would imagine that the second function might start to slow down a bit with larger sets of input. May have missed something about why it is better...

		```

		* [Whiteboarding Prompt 3](https://full-time.learnhowtoprogram.com/capstone/capstone-week-2/whiteboarding-practice---week-1#dutch-national-flag-problem)
		```c#
		// Input: {0, 1, 2, 0, 1, 2}
		// Output: {0, 0, 1, 1, 2, 2}

		// Input: {0, 1, 1, 0, 1, 2, 1, 2, 0, 0, 0, 1}
		// Output: {0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 2, 2}

		// Given prompt saying that Array must be used, and brackets are squiggly brackets, assuming C# is the language requested to solve this prompt.

		// Steps To Solve:
		// 	- Create three new arrays, one for 0s, one for 1s, and one for 2s.
		// 	- foreach loop through the unsorted array. If number is 0, push it to 0, etc.
		// Combine and return all three arrays of individual numbers.
		

		// first Attempt
		public int[] SortNumberArray(int[] unsortedArray)
		{
			int[] zeroesArray = {};
			int[] onesArray = {};
			int[] twosArray = {};
			foreach (int number in unsortedArray)
			{
				if (number == 0)
				{
					Array.resize(ref zeroesArray, zeroesArray.length + 1);
					zeroesArray[zeroesArray.Length -1] = number;
				}
				else if (number == 1)
				{
					Array.resize(ref onesArray, onesArray.length + 1);
					onesArray[onesArray.Length -1] = number;
				}
				else if (number == 2)
				{
					Array.resize(ref twosArray, twosArray.length + 1);
					twosArray[twosArray.Length -1] = number;
				}
			}

			int[] sortedArray = {};
			foreach(int zero in zeroesArray) 
			{
				Array.resize(ref sortedArray, sortedArray.length + 1);
				sortedArray[sortedArray.Length -1] = zero;
			}
			foreach(int one in onesArray) 
			{
				Array.resize(ref sortedArray, sortedArray.length + 1);
				sortedArray[sortedArray.Length -1] = one;
			}
			foreach(int two in twosArray) 
			{
				Array.resize(ref sortedArray, sortedArray.length + 1);
				sortedArray[sortedArray.Length -1] = two;
			}

			return sortedArray;
		}

		// Ran -- failure because "resize" and "length" are not recognized. Also forgot to make it static.
		// Second attempt, capitalized both methods and made function static.
		public static int[] SortNumberArray(int[] unsortedArray)
		{
			int[] zeroesArray = {};
			int[] onesArray = {};
			int[] twosArray = {};
			foreach (int number in unsortedArray)
			{
				if (number == 0)
				{
					Array.Resize(ref zeroesArray, zeroesArray.Length + 1);
					zeroesArray[zeroesArray.Length -1] = number;
				}
				else if (number == 1)
				{
					Array.Resize(ref onesArray, onesArray.Length + 1);
					onesArray[onesArray.Length -1] = number;
				}
				else if (number == 2)
				{
					Array.Resize(ref twosArray, twosArray.Length + 1);
					twosArray[twosArray.Length -1] = number;
				}
			}

			int[] sortedArray = {};
			foreach(int zero in zeroesArray) 
			{
				Array.Resize(ref sortedArray, sortedArray.Length + 1);
				sortedArray[sortedArray.Length -1] = zero;
			}
			foreach(int one in onesArray) 
			{
				Array.Resize(ref sortedArray, sortedArray.Length + 1);
				sortedArray[sortedArray.Length -1] = one;
			}
			foreach(int two in twosArray) 
			{
				Array.Resize(ref sortedArray, sortedArray.Length + 1);
				sortedArray[sortedArray.Length -1] = two;
			}

			return sortedArray;
		}

		// Tested and it is functional. Resolved, 15 minutes. No hints used.
		```

		* [Whiteboarding Prompt 4](https://full-time.learnhowtoprogram.com/capstone/capstone-week-2/whiteboarding-practice---week-1#length-of-the-longest-substring-without-repeating-characters)
		```javascript
		// Example 1:
		// Input: “ABCDEFGABEF”
		// Output: 7
		// Explanation: The longest substring without repeating characters are “ABCDEFG”, “BCDEFGA”, and “CDEFGAB” with lengths of 7

		// Example 2:
		// Input: “ILOVEEPICODUS”
		// Output: 8
		// Explanation: The longest substring without repeating characters is "EPICODUS, with a length of 8

		// Assumptions:
		// - String is not null

		// Steps to Solve: 
		//	- Create an empty array called "substringArray"
		// 	- foreach letter in string:
		// 		- create an array "tempArray"
		//		- run a for loop for all remaining characters in the input string.
		//			- if the character does not exist in the array, push it to the array
		// 			- if the character exists in the array, do not push it to the array. Instead, 
		// 				- if substringArray is null, let subStringArray = tempArray.
		// 				- if subStringArray is not null AND if substringArray.length < tempArray.length : substringArray = tempArray;

		//	- After each letter in the foreach loop has been itereated through, return substringArray.length;


		// Attempt 1. Realizing now that it needs to be a for loop initially instead of foreach loop.
		function nonRecurringSubString(stringInput) {
			let subStringArray = [];
			let stringArray = stringInput.split("");
			for (let i = 0; i < stringArray.length; i++) {
				let tempArray = [];
				tempArray.push(stringArray[i]);
				for (let j = i + 1; j < stringArray.length; j++){
					if (!tempArray.includes(stringArray[j])) {
						tempArray.push(stringArray[j]);
						console.log(tempArray);
					} else {
						break;
					}
				}
				if ((subStringArray === null) || ((subStringArray.length != null) && (tempArray.length > subStringArray.length))) {
					subStringArray = tempArray;
				}
			}
			return subStringArray.length;
		}

		// Tested and it is functional. Resolved, ~20 minutes. No hints used.

		```

	* 11:36am PST - 12:07 pm PST
		Watch Henry's whiteboarding