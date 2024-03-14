# Timetracker

* 2024-03-12
	* 7:45am PST - 8:22am PST
		* Warmup [Leetcode problem](https://leetcode.com/problems/permutations/description/). Solution:
			```javascript
			/**
			 * @param {number[]} nums
			* @return {number[][]}
			*/
			var permute = function(nums) {
				const resultArray = [];
				function recursiveBuilder(pmtArray, remainderArray) {
						if (remainderArray.length === 0) {
								resultArray.push(pmtArray.slice());
								return;
						}

						for (let i = 0; i < remainderArray.length; i++) {
								pmtArray.push(remainderArray[i]);
								const numsLeftArray = remainderArray.slice(0, i).concat(remainderArray.slice(i + 1));
								recursiveBuilder(pmtArray, numsLeftArray);
								pmtArray.pop();
						}
				}

				recursiveBuilder([], nums);
				return resultArray;
			};
			```
			* This one took some time to figure out. Was initially trying to do it non-recursively and realized that that would probably overcomplicate it.
	* 8:22am PST - 9am PST
		* Reading up on Angular authentication to try to understand some of the remaining topics in the video.
	* 9am PST - 9:10am PST
		* Scrum
	* 9:10am PST - 11:31am PST
		* Found another [Angular Auth video](https://www.youtube.com/watch?v=R8a8ituFkls). Appears that the main concept of an auth service is the same, but the difference may be that the original tutorial is using "guard-ed" routes.
		* Also looking into lazy loading from the [same source](https://www.youtube.com/watch?v=NFJbXP6Ci98).
		* Will continue following [original tutorial](https://www.youtube.com/watch?v=YohZzT7g_S8&list=PL3EibBwUnE37aZ937p2L2VoozXUKcsI76&index=12) to build [sample project](https://github.com/mejia-dev/students-details).
			* Render basic authentication portal with conditional buttons.
			* Add login and logout functions to form.
			* Finish first example form. Unclear how redirection is supposed to work with this implementation, but the videos usually get to important points in a roundabout way.
			* Noted that video tutorial has moved on from the login form. Checking example repo to see if solution is listed there.
				* No changes of note. Noticed that there is a delay of 2000 milliseconds set (since we're simulating using an actual auth API and not using a real one). While the console.log in the redirection code *is* returning `true` (indicating that the login has been completed successfully), there may be some sort of a delay required to process the redirection. Going to attempt to reduce 2000 millisecond delay to 1000, and try to see if I can implement another delay in the redirection code to account for the delay. If this works, will try to convert to async login function (as I assume it would be in a real-world scenario).
				* This did not work. There is a chance that some of this isn't working due to not using a real authentication platform. Everything is `console.log`ging fine and it is using the `subscribe` method which appears to asyncrhonously wait for an event to occur. 
				* Scoured [template repo](https://github.com/deepakjha14/yt-students-details-app/tree/main) but didn't see any significant changes between the way auth was handled in mine and in the template. Cloned the repo and confirmed that redirection works, although lots of the other functionality was different than the tutorial video.
				* Hilariously (🙃) located the issue. `auth.service.ts` was importing `delay` and `tap` from the `rxjs` library instead of the `rxjs/operators` library. I don't quite understand why this worked, or even caused an issue to begin with. Will look into it more later.
	* 11:31am PST - 11:49am PST
		* PDP Checkin meeting with Erik.
			* Discussed Angular progress.
			* Discussed Angular struggles, specifically with the import statements.
			* May have been wiser to learn an older version of Angular that is more common in the workplace and would potentially have some better guides and tutorials available. Will probably end up building out a portfolio-ready project and then moving away from Angular for a "final" project. Maybe instead of a [M](https://www.mongodb.com/)[A](https://angular.io/)[P](https://www.python.org/) stack as originally planned, I could do a [M](https://www.mongodb.com/)[R](https://react.dev/)[P](https://www.python.org/) stack instead. Will figure this out later.
			* Discussed potentially using JavaScript for my capstone despite having to manually write functions for collision detection, delta time calculations, etc. This would likely be more marketable to employers than using Unity/Godot. Will likely proceed with this idea.
			* Discussed time tracker.
	* 11:49am PST - 12pm PST
		* Notes cleanup.
	* 12pm PST - 1pm PST
		* Lunch
	* 1pm PST - 1:25pm PST
		* Continue watching Angular video. Started planning for portfolio-ready project.
	* 1:25pm PST - 1:35pm PST
		* Brief pause to assist Ravin with React Native. Determined that both `expo-router/babel` and `babel-preset-expo` were installed in the `babel.config.js` file. Commenting out the deprecated `expo-router/babel` allowed the app to compile for the web.
	* 1:35pm PST - pm PST
		* Begin portfolio project
		* Researching project ideas. Decided to go with a chat app frontend. Will add backend using Mongo and Python. 
			* Watching [Firestore authentication videos](https://www.youtube.com/watch?v=586O934xrhQ&list=PL5SnQaxNFeTElFjnhH6ylWXTCapePT2Th&index=2&pp=gAQBiAQB) and other lazy loading resources.
			* Created [project repo](https://github.com/mejia-dev/smaart-chat/).
		* Created project, created first component then realized I wasn't prompted for options like SG or SSR on install. Did some research and determined that it was because the app was created through the git bash terminal (a known issue on Windows). Deleted the project and recreated it through the command prompt.
		* Add basic components for login and registration. 
		* Create Firebase project.

* 2024-03-12
	* 7:45am PST - 8:14am PST
		* Warmup [Leetcode problem](https://leetcode.com/problems/reverse-integer/). Solution:
			```javascript
			/**
			 * @param {number} x
			* @return {number}
			*/
			var reverse = function(x) {
					let digitArray = x.toString().split("");
					let finalArray = [];
					if (digitArray[0] === "-") {
							finalArray.push("-");
							digitArray.shift();
					}
					for (let i = digitArray.length; i > 0; i--) {
							finalArray.push(digitArray[i - 1]);
					}
					return parseInt(finalArray.join(""));
			};
			```
	* 8:14am PST - 9am PST
		* Wanted to learn more of the logic behind what the [Angular video tutorial](https://www.youtube.com/watch?v=abIK3mAj_VA&list=PL3EibBwUnE37aZ937p2L2VoozXUKcsI76&index=10) is teaching. 
			* Started the [Codecademy course on AngularJS](https://www.codecademy.com/learn/learn-angularjs) only to discover project is set up differently.
			* After doing some more research, discovered that "Angular" was [built to replace "AngularJS"](https://radixweb.com/blog/angular-vs-angularjs). 
			* Looked for more Angular 17 explainers but didn't find many. Resolved to look through [the docs](https://angular.io/guide/understanding-angular-overview) instead. 
	* 9am PST - 9:12am PST
		* Scrum
	* 9:12 am PST - 12pm PST
		* More reading Angular docs: 
			* [Components](https://angular.io/guide/component-overview). 
			* [Architecture](https://angular.io/guide/architecture).
		* After understanding more about Angular, continued watching [ag-grid and Router tutorial](https://www.youtube.com/watch?v=abIK3mAj_VA&list=PL3EibBwUnE37aZ937p2L2VoozXUKcsI76&index=10) for use in [my sample project](https://github.com/mejia-dev/students-details).
			* Install [ag-grid](https://ag-grid.com/angular-data-grid/getting-started/) and add records component.
			* Add ag-grid to student records component.
			* Move landing-related elements and data to new "landing" component.
			* Setup prereqs for basic routing.
			* Learning about Angular Router
			* Fix bugs in app.config and app.routes and establish basic routing
			* Add working ag-grid implementation using column definitions.
			* Begin researching authentication.
			* Add "auth-guard" guard to project.
	* 12pm PST - 1pm PST
		* Lunch
	* 1pm PST - 1:30 PST
		* Add route restriction via auth-guard guard
	* 1:30pm PST - 1:53pm PST
		* Whiteboarding!
	* 1:53pm PST - 2:35pm PST
		* Learning about Angular lazy loading
	* 2:34pm - 2:57pm PST
		* Brain break
	* 2:57pm PST - 4:50pm PST
		* Add Login component
		* Add dashboard component
		* Quick pause on normal to do sourcemap research for Kim.
		* Update routing. Previously-created components now require authentication.
		* Update routing to lazily render dashboard and child components only after login
		* Update styling so that selected route on sidebar is highlighted
		* Learning about Angular template-driven forms.

* 2024-03-12
	* 7:45am PST - 8:12am PST
		* Setup for the day.
		* Warmup [Leetcode problem](https://leetcode.com/problems/add-two-numbers/).
	* 8:12am PST - 9am PST
		* Begin [Angular installation section](https://youtu.be/3qBXWUpoPHo?feature=shared&t=8432)
			* Needed to upgrade Node on my computer (Angular CLI requires minimum Node version of 18.13). Looking at LHTP / online resources to determine how to do this (using Epicodus-recommended `nvm` vs industry-standard(?) `npm install n` command.) Determined that the `n` module is only supported on Unix systems, so I am unable to use it.
			* Attempted to upgrade NVM and promptly broke it. Issue is the same as the one listed [here](https://github.com/coreybutler/nvm-windows/issues/1068). Appears to just be an issue with the latest version.
	* 9am PST - 9:13am PST
		* Scrum feat. Robo-Erik.
	* 9:13am PST - 10:31am PST
		* Working on downgrading NVM to 1.1.11.
			* Attempted to downgrade directly. Did not work.
			* Attempted to uninstall. Noted that uninstalling would remove all global packages. Attempted a manual overwrite of version 1.1.11 again. This seemed to work. Attempted manual upgrade to 1.1.12. Still not working. Went through manual overwrite process down to 1.1.11 again. Will stay on this version for now. Confirmed functionality.
		* Installed Node.js version 20.11.1 through NVM. All set to use.
		* Continued watching Angular video.
			* Installed `@angular/cli`
			* Ran into some issues getting installation to work, but got version 17.2.3 installed successfully.
			* Create first project - [Hotel Inventory App](https://github.com/mejia-dev/hotel-inventory).
			* Learn about automated testing through Jasmine (write) Karma (run). Perform walkthrough of Angular-specific webpack components.
			* Learned about mono-repo (creating multiple projects in singular workspace).
			* Noted that tutorial is using a severely outdated version of Angular and a lot of the component / modules are structured completely differently from the latest version. Looking for tutorials for Angular 17.
	* 10:31am PST - 11:31am PST
		* Located [Angular 17 tutorial](https://www.youtube.com/watch?v=2trkY4UfU7U&list=PL3EibBwUnE37aZ937p2L2VoozXUKcsI76&index=2). Updated tracker spreadsheet and will use this one going forward.
			* Learned about Angular 17 `angular.json` file and made configuration changes as necessary.
			* Learned about Bootstrapping.
			* Adjust my project to use SCSS instead of CSS.
	* 11:31am PST - 12:15pm PST
		* Noah's whiteboarding session
			* Realized what the point of the N value was in the whiteboarding prompt. My second attempt at it yesterday was actually correct, since I shouldn't have assumed that the array was sorted. This explains the need for the N variable, since N leads to us not needing an actual sorting algorithm, because we already have the upper bound defined. Nice!
			* Also kinda wondering if a `Set` could be used for this, then checking `Set.prototype.has()`. May explore this a bit after lunch.
			* Ended up exploring it while Noah was getting feedback lol. Seems like you don't even need `N` which is kinda cool (I'm pretty sure about that this time).
				```javascript
				function findMissing(array) {
					const setFromArray = new Set(array);
					// just gonna have i start from 1 to avoid having to do a -1
					for (let i = 1; i <= array.length; i++) {
						if (!setFromArray.has(i)) {
							return i;
						}
					}
					return null;
				}
				```
	* 12:15pm PST - 1:14pm PST
		* Lunch
	* 1:14pm PST - 4:49PM PST
		* More Angular!
			* Learned about linting and installed ESLint in project.
			* Renamed component prefixes.
			* Began reviewing frontend of finished example project. Learned about Bootstrap with Angular.
			* Installed ng-bootstrap in the application.
			* Working on creating homepage using Components.
			* Complete MVP for homepage.
			* Complete stylized searching with Bootstrap.
			* Learning SASS styling and BEM model for scalability of code.
			* Add new side-bar component to site.
			* Add function that expands and contracts sidebar.
			* Add autoresize of main content based on sidebar expansion.
			* Began working on adding [ag-grid.com](ag-grid.com) to the application. Will work more on this tomorrow.


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

	* 11:36am PST - 12:07pm PST
		Watch Henry's whiteboarding

	* 12:07pm PST - 1:06pm PST
		Lunch

	* 1:06pm PST - 4:39pm
		* Continue watching [Angular for Beginners](https://www.youtube.com/watch?v=3qBXWUpoPHo)
			* Learn proper TypeScript setup and configuration.
			* Learning types and type manipulation. Created [sample repo](https://github.com/mejia-dev/typescript-datatypes-sample).
			* Learned about Rest parameters.
			* Learning about Generic Functions.
			* Learning about getters/setters, etc. (incredibly similar to C#) in TypeScript.
			* Learning about the [differences between TS Intefaces and Classes](https://stackoverflow.com/questions/40973074/difference-between-interfaces-and-classes-in-typescript).
				* Rabbit hole learning about the [differences between TS Interfaces and Types](https://blog.logrocket.com/types-vs-interfaces-typescript/).
			* Learning about decorators
			* Learning about specific tsconfig.json configs.
		* Completed TypeScript fundamentals. Ending at Angular installation section [~2:20:32](https://youtu.be/3qBXWUpoPHo?feature=shared&t=8432). Will pick back up tomorrow.