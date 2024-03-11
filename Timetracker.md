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
	* 9:40am PST - 
		* [Whiteboarding Prompt 1](https://full-time.learnhowtoprogram.com/capstone/capstone-week-2/whiteboarding-practice---week-1#contiguous-subarray-with-greatest-sum)
			```javascript
			// Input: [-2, -3, 4, -1, -2, 1, 5, -3]
			// Ouput: 7 
			// The largest sum of a contiguous subarray is 7 (4 + -1 + -2 + 1 + 5 === 7)

			// DEFINITION: contiguous. adjective. con·​tig·​u·​ous kən-ˈtig-yə-wəs. : being in actual contact : touching along a boundary or at a point.


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
		```