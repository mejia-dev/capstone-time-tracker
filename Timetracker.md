# Timetracker

### Week 3


* 2024-03-25
	* 7:45am PST - 
		* [Whiteboarding prompt](https://full-time.learnhowtoprogram.com/capstone/capstone-week-4/whiteboarding-practice---week-3#longest-substring-with-at-most-two-distinct-characters)
			```javascript
			// Input: "eceba"
			// Output: 3
			// Explanation: The substring "ece" contains 2 distinct characters

			// Steps to solve:
				// define left and right for sliding window
				// define a character map
				// while right is less than the length of the input
					// perform window sliding function on right side
					// adjust left side accodingly until the character map size is not more than 2, increasing left variable by 1
				// increase right variable by 1

				function findLongestSubstring(inputString) {
					let leftIndex = 0;
					let rightIndex = 0;
					const charMap = new Map();
					let finalLength = 0;

					while (rightIndex < inputString.length) {
						const thisChar = inputString[rightIndex];
						charMap.set(thisChar, (charMap.get(thisChar) || 0) + 1);

						while (charMap.size > 2) {
							const leftChar = inputString[leftIndex];
							charMap.set(leftChar, charMap.get(leftChar) -1);
							if (charMap.get(leftChar) == 0) {
								charMap.delete(leftChar);
							}
							leftIndex++;
						}
						finalLength = Math.max(finalLength, rightIndex - leftIndex + 1);
						rightIndex++;
					}
					return finalLength;
				}
				// Time spent: 40 minutes. Hints used: none.
			```
		* No scrum today - Erik out sick.
		* Researching music APIs for my capstone.
			* [Discogs](https://www.discogs.com/developers)
			* [LibreSpot](https://github.com/librespot-org/librespot)
		* May try to integrate APIs into a simple project later to test them. Going to try and build a chat application for now. 
			* Begin [chat app tutorial](https://www.youtube.com/watch?v=Fzv-rgwcFKk).
		


* 2024-03-25
	* 8am PST - 9am PST
		* Reading through Monday homework.
		* Work on getting Django project from last week deployed on PythonAnywhere.
			* Ran into an issue with path of settings module. Appears it was one layer deeper than expected in the directory.
			* Ran into an issue with allowed hosts. Allowed [mejiadev.pythonanywhere.com](mejiadev.pythonanywhere.com) in the settings module. Eventually realized it needs to be a string instead. Site is now working but database and static files are not functional yet.
			* Learning about dotenv usage.
	* 9am PST - 9:10am PST
		* Scrum
	* 9:10am PST - 12pm PST
		* Continue learning about dotenv usage in Django.
		* Set up [PythonAnywhere MySQL database](https://help.pythonanywhere.com/pages/UsingMySQL/).
			* Keep getting access denied error when trying to sign in.
			* Appears that databse has to be manually created first for Django projects. Created database then migrated to it. Resolved.
		* Set up static files. Now getting error during template rendering when clicking on any page links: `'NoneType' object has no attribute 'startswith'`.
			* Appears to be related to a database connection but not sure what might be happening. Will check dotenv documentation again to ensure it is set up correctly. Especially strange since it migrated correctly according to the terminal message.
			* Referenced [documentation](https://help.pythonanywhere.com/pages/environment-variables-for-web-apps). Looks like the file was not defined in the wsgi.py file. Specifying it here resolved the issue.
		* Looking into Django secret key management. Hadn't realized that this needed to be secured.
			* Created a new secret key using:
				```python
				from django.core.management.utils import get_random_secret_key
				print(get_random_secret_key())
				```
			* Saved key in `.env`.
			* Change `DEBUG` to False and set `SECRET_KEY = os.getenv("SECRET_KEY")`.
			* Reloaded the site and confirmed full functionality.
		* This concludes Django learning.
		* Update README on [project](https://github.com/mejia-dev/ice_cream_shop) with lessons learned. Updated project info and GitHub pinned repos.
		* Begin [PostgreSQL Tutorial](https://www.youtube.com/watch?v=SpfIwlAYaKk).
	* 12pm PST - 1pm PST
		* Lunch
	* 1pm PST - 1:40pm PST
		* Continue watching [PostgreSQL Tutorial](https://www.youtube.com/watch?v=SpfIwlAYaKk). Installed and set up PostgreSQL and pgAdmin.
	* 1:40pm PST - 3:21pm PST
		* Apply for a [dream job](https://linusmediagroup.com/ft-junior-backend-developer).
	* 3:21pm PST - 4:13pm PST
		* Fixed issue with database restore through pgAdmin. Appears that the binary path sometimes needs to be [specified manually](https://stackoverflow.com/questions/77462578/pgadmin-error-when-restoring-database-from-tar-file) for newer versions of Python.
		* Complete Postgresql
	* 4:13pm PST - 4:45pm PST
		* Start researching best DB for a chat application.
		* May end up going with Cassandra as it seems to be largely popular for chat. Some of the more useful articles / threads:
			* https://www.reddit.com/r/node/comments/i0l97y/why_does_mongodb_get_so_much_hate_genuine_question/
			* https://discord.com/blog/how-discord-stores-billions-of-messages
			* https://www.reddit.com/r/Database/comments/8dpgyv/best_database_for_a_chat_application/
		* Will either begin learning [Flutter](https://flutter.dev/) tomorrow or build a chat app.

### Week 2

* 2024-03-20
	* 7:55am PST - 12pm PST
		* Fourth [whiteboarding question](https://full-time.learnhowtoprogram.com/capstone/capstone-week-3/whiteboarding-practice---week-2#valid-parentheses) for warmup:
			```javascript
			// Input: "()[]{}"
			//Output: true
			// Input: "([)]"
			// Output: false

			// Steps to Solve:
				// split input into array of individual single-character strings
				// final result should be set to true. 
				// Three if statements. 
					// If NOT array.filter() of "[" count is equal to array.filter() of "]" count, set to false.
					// If NOT array.filter() of "{" count is equal to array.filter() of "}" count, set to false.
					// If NOT array.filter() of "(" count is equal to array.filter() of ")" count, set to false.
				// return final result.

			function validMatches(inputString) {
				const splitArray = inputString.split("");
				let result = true;

				if (splitArray.filter(bracket => bracket === "[").length != (splitArray.filter(bracket => bracket === "]").length)) {
					result = false;
				}
				if (splitArray.filter(bracket => bracket === "{").length != (splitArray.filter(bracket => bracket === '}').length)) {
					result = false;
				}
				if (splitArray.filter(bracket => bracket === "(").length != (splitArray.filter(bracket => bracket === ')').length)) {
					result = false;
				}
				return result;
			}
			// resolved. Time taken: 5 minutes. No hints used.
			```
			* Begin determining which ASP.NET project to rebuild with Django.
			* Begin rebuilding project.
			* Found better gitignore template
			* Troubleshooting why django-admin won't run.
				* Appears that the command just wouldn't run in powershell. Works fine in cmd.
			* Pushed project to [repository](https://github.com/mejia-dev/pastry_paradise_bakery).
			* After comparing to some other sample projects, noticed some issues and not sure how to properly push a Django project. Watching [quick tutorial](https://www.youtube.com/watch?v=fVy9eJzloj8).
			* Deleted GitHub repository. Tore down entire project. Appears I was pushing too much.
			* Created a distributed file structure where venv is in a different place than the project data.
			* Started [new GH repo](https://github.com/mejia-dev/ice_cream_shop).
			* Began working on getting url and views set up. Template is having some trouble rendering.
			* Learning about dotenv in Python (using [python-dotenv](https://pypi.org/project/python-dotenv/)) and creating [many-to-many relationships](https://docs.djangoproject.com/en/5.0/topics/db/examples/many_to_many/).
	* 12pm PST - 1pm PST
		* Lunch
	* 1pm PST - 1:30pm PST
		* Add flavor and treat models to project.
		* Add migration to database and migrate successfully.
	* 1:33pm PST - 1:45pm PST
		* Meeting with Erik.
	* 1:45pm PST - 5:01pm PST
		* Set up superuser account.
		* Register Treat and Flavor in admin panel
		* Render flavors on page
		* Research into partials. Appears that there is no official support. For sake of time, will look into this later.
		* Add rendering for Treats Index
		* Research Python hosting -- found pythonanywhere.com
		* Add details page for treat
		* Add details page for flavor
		* Update Treat details to render flavors
		* Trying to get both sides of many-to-many rendering correctly.
		* Resolved issue -- appears that I was trying to use `{% if flavor.treats.all.count > 0 %}`, but this only works from one side of the many-to-many. Using `{% if flavor.treat_set.all %}` instead resolved the issue.

* 2024-03-20
	* 7:58am PST - 9am PST
		* Third [whiteboarding question](https://full-time.learnhowtoprogram.com/capstone/capstone-week-3/whiteboarding-practice---week-2#group-anagrams) for warmup:
			```javascript
			// Input: ["eat", "tea", "tan", "ate", "nat", "bat"]
			// Output: [["bat"], ["nat", "tan"], ["ate", "eat", "tea"]]

			// assuming only strings, no null or undefined

			// Steps to Solve:
				// For each string (str) in the input, set all characters to lowercase, sort characters alphabetically and use that value (sortedStr) as a key in hash map.
					// if sortedStr does not exist as a key  in the hash map, create an array where str is the only value.
					// if sortedStr DOES exist as a key in the hash map, locate the Value array and push str to it.
				// return value of hash map

			function getAnagrams(stringArray) {
				let hashMap = {};
				stringArray.forEach((str) => {
					const sortedStr = str.split('').sort();
					if (hashMap[sortedStr]) {
						hashMap[sortedStr].push(str);
					} else {
						hashMap[sortedStr] = [str];
					}
				})
				return Object.values(hashMap);
			}

			// solved in ~20 minutes. No hints used.
			```
		* Start working on Django [form processing tutorial](https://docs.djangoproject.com/en/5.0/intro/tutorial04/).
	* 9am PST - 9:12am PST
		* Scrum
	* 9:12am PST - 12pm PST
		* Continue working on form processing. 
		* Turn details page on [my project](https://github.com/mejia-dev/first-django) into form.
		* Learning about try/except/else statements in Django.
		* Learning about generic views in order to DRY up code.
		* Refactor urlConfig and viewsConfig to use generic views
		* Learning about Django's testing suite.
		* Successfully write and pass tests for Question model.
		* Begin testing UI.
	* 12pm PST - 1pm PST
		* Lunch
	* 1pm PST - 3:45pm PST
		* Continue working on testing UI
		* Write and pass tests for UI.
		* Rendering static files. Also reading up on [server-side deployment](https://docs.djangoproject.com/en/5.0/howto/static-files/deployment/) of static files.
		* Learning about tweaking admin display.
		* Change admin display for poll models. Will work on changing actual administration panel UI next.
	* 3:45pm PST - 4pm PST
		* Career Services meeting.
	* 4pm PST - 4:49pm PST
		* Trying to unravel the .gitignore file and see which parts are ignoring the admin directory.
		* Python chat with Henry.

* 2024-03-19
	* 7:45am PST - 9am PST
		* Second [whiteboarding question](https://full-time.learnhowtoprogram.com/capstone/capstone-week-3/whiteboarding-practice---week-2#container-with-most-water) for warmup:
			```javascript
			// Input: [1, 8, 6, 2, 5, 4, 8, 3, 7]
			// Output: 49
			// Explanation: The maximum area is obtained by selecting the minimum of the heights of the vertical lines ( ex: Math.min(8, 7) === 7) and multiplying it by the width between the lines (index 8 - index 1 === 7 spaces apart).
			//
			// Input: array = [1, 5, 4, 3]
			// Output: 6
			// Explanation : 
			// 5 and 3 are distance 2 apart. 
			// So the size of the base = 2. 
			// Height of container = min(5, 3) = 3. 
			// So total area = 3 * 2 = 6

			// Steps to Solve:
				// Determine two largest numbers. Get their indexes.
				// find the smaller of the two largest numbers
				// multiply that number by the indexes

			function mostWater(inputArray) {
				let maxArea = 0;
				let indexA = 0;
				let usedIndexA;
				let indexB = inputArray.length -1;
				for (let i = 0; i < inputArray.length; i++) {
					if (indexA < inputArray[i]) {
						indexA = inputArray[i];
						usedIndexA = i;
					}
				}
				for (let i = 0; i < inputArray.length; i++) {
					if (indexB < inputArray[i] && i != usedIndexA) {
						indexB = inputArray[i];
					}
				}
				return [indexA, indexB]
			}

			// first attempt above. This seems to be a little trickier than first expected, now noticing that values can be repeated. Rethinking steps.

			function mostWaterV2(inputArray) {
				let largest = 0;
				let indexOfLargest = 0;
				let secondLargest = 0;
				let indexOfSecondLargest = 0;
				for (let i = 0; i < inputArray.length; i++) {
					if (inputArray[i] > largest) {
						secondLargest = largest;
						indexOfSecondLargest = indexOfLargest;
						largest = inputArray[i]
						indexOfLargest = i;
					} else if (inputArray[i] > secondLargest && inputArray[i] < largest) {
						secondLargest = inputArray[i]
						indexOfSecondLargest = i;
					}
				}
				let sizeOfBase = indexOfLargest - indexOfSecondLargest;
				return secondLargest * sizeOfBase
			}

			// This is functional, but would probably require the absolute value of sizeOfBase to be called so that it doesn't return negative. I don't know this off the top of my head, but will consider this completed. Time spent: 49 minutes.
			// Researched and located Math.abs(). Second to last line should be:
			let sizeOfBase = Math.abs(indexOfLargest - indexOfSecondLargest);
			// Tested this and confirmed it is working.

			// Checking hints since there was likely a better way to do this.
			function mostWaterV3(inputArray) {
				let maxArea = 0;
				let leftIndex = 0;
				let rightIndex = inputArray.length -1;

				while (leftIndex < rightIndex) {
					const calculatedArea = Math.min(inputArray[leftIndex], inputArray[rightIndex]) * (rightIndex - leftIndex);
					if (calculatedArea > maxArea) {
						console.log(calculatedArea)
						maxArea = calculatedArea;
					}

					if (inputArray[leftIndex] < inputArray[rightIndex]) {
						leftIndex++;
					} else {
						rightIndex--;
					}
					return maxArea;
				}
			}
			// Attempt not quite working right. My method (v2) works as expected, so won't worry about it for now.
			```
	* 9am PST - 9:15am PST
		* Scrum.
		* Discussing Python progress with Python group.
	* 9:15am PST - 10:52am PST
		* Continued following [Django tutorial](https://docs.djangoproject.com/en/5.0/intro/tutorial01/).
		* Created virtual environment for first Django project.
		* Initialized Django project.
		* Reading up on gitignore practices for Django.
		* Created [GitHub repo](https://github.com/mejia-dev/first-django) for project.
		* Confirmed working development server by running `manage.py runserver`
		* Learning about views and urls in Django.
		* Reading about database backends with Django.
			* Documentation is spread across several different pages and isn't clear about which modules are actually needed to support MySQL.
			* Located [tutorial video](https://www.youtube.com/watch?v=5g_xIwxLSJk).
	* 10:52am PST - 11:30am PST
		* Quick pause to assist Brianca with relative path issue on a C# shared view where a logo would only show up on specific pages. Appears that line 4 of [the Header view](https://github.com/BriancaKnight/Pierre_Sweet_Treats.Solution/blob/main/Bakery/Views/Shared/_Header.cshtml) was set to use the relative path to the file `(src="../img/black.png")`. Changing it to the absolute path to the file `(src="~/img/black.png")` resolved the issue.
	* 11:30am PST - 12pm PST
		* Resume Django / MySQL [tutorial video](https://www.youtube.com/watch?v=5g_xIwxLSJk).
	* 12pm PST - 1pm PST
		* Lunch
	* 1pm PST - 4:45pm PST
		* Continued [Django tutorial](https://docs.djangoproject.com/en/5.0/intro/tutorial02/).
		* Created models and prepared project for database migration.
		* Added models to database and added custom functions for display strings.
		* Learned about the Django shell API.
		* Learned about Django admin page. Allowed Django admin to make changes to Question data.
		* Rendering database objects on pages
		* Learning about the render() shortcut
		* Learn about the get_object_or_404 shortcut.
		* Implemented basic routing between Index and Detail views.
		* [Template repo](https://github.com/mejia-dev/first-django) is in a good spot for today. Will start tomorrow with [form processing tutorial](https://docs.djangoproject.com/en/5.0/intro/tutorial04/).
		

* 2024-03-18
	* 7:45am PST - 9am PST
		* Read Week homework -- all review, skimmed mostly.
		* First [whiteboarding question](https://full-time.learnhowtoprogram.com/capstone/capstone-week-3/whiteboarding-practice---week-2#product-of-array-except-self) for warmup:
			```javascript
			// Input: [1, 2, 3, 4]
			// Output: [24, 12, 8, 6]
			// Given an array nums of n integers where n > 1, return an array output such that output[i] is equal to the product of all the elements of nums except nums[i].
			// Constraints: Do your best to complete this without a nested loop

			// Steps to Solve:
				// create empty newArray
				// multiply all the values in the inputArray and assign to a temp value called bigProduct.
				// for each indexItem in the inputArray, let the corresponding newArray position = bigProduct divided by the value of indexItem.
				// return newArray

			function multArrayExceptSelf(inputArray) {
				let newArray = [];
				let bigProduct = 1;
				inputArray.forEach((value) => {
					bigProduct *= value;
				})
				for (let i = 0; i < inputArray.length; i++) {
					newArray[i] = bigProduct / inputArray[i];
				}
				return newArray;
			}
			// No hints used. Time taken: 9 minutes.
			```
		* Begin working on Python.
		* Draft email to Erik.
		* Continue working on Python.
			* Reviewing basics through [Codecademy Harvard video](https://www.youtube.com/watch?v=nLRL_NcnK-4).
			* Found a faster [basics course](https://www.youtube.com/watch?v=VchuKL44s6E).
	* 9am PST - 9:15am
		* Scrum
	* 9:15am PST - 12pm PST
		* More Python review.
			* Brief sidetrack onto what modulo is used for. Seems to mostly be used for checking positive / negative. Most interesting use case would be to do something every `n`th time [through a loop](https://hatoum.com/blog/2012/12/practical-uses-for-modulo-operator.html):
				```javascript
				for (x=0; x <100000; x++) {

						// do regular stuff here
				
						// do something special every 9th time through
						// the loop
						if (x % 9 == 0) {
								// important stuff here
						}
				}
				```
		* More Python review.
			* experimenting with different for loop concepts.
			* More thorough review on comprehensions.
			* Do some more testing with *args and **kwargs. This is not something I'd learned much of previously. Will move on for now but may need to revisit later if this ends up being a core component of something I'm writing.
	* 12pm PST - 1pm PST
		* Lunch
	* 1pm PST - 2:28pm PST
		* Applying for [a dream job](https://boards.greenhouse.io/350org/jobs/5802026) I found that has an application deadline.
	* 2:28pm PST - 4:45pm PST
		* Complete application. Back to Python.
			* Reading some resources:
				* https://blog.hubspot.com/website/python-backend
				* https://www.freecodecamp.org/news/python-back-end-development-the-beginners-guide/
				* https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world
				* https://medium.com/quick-code/5-python-libraries-to-make-backend-development-easy-76141f47473a
			* Spent some time trying to figure out which backend framework shows up in jobs most often. Decided to go with Django instead of Flask. Django seems to be production / professional quality whereas Flask is more enthusiast-focused.
		* Following [Django tutorial](https://docs.djangoproject.com/en/5.0/intro/tutorial01/).
			* Running into some issues getting Django set up on my machine.
			* Appears Python version needed to be updated. Updated python to 3.12 and this resolved all the issues. Will likely start actually following tutorial tomorrow. 
			* Did some additional research into jobs requiring Django.

### Week 1

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
	* 1:35pm PST - 5:02pm PST
		* Begin portfolio project
		* Researching project ideas. Decided to go with a chat app frontend. Will add backend using Mongo and Python. 
			* Watching [Firestore authentication videos](https://www.youtube.com/watch?v=586O934xrhQ&list=PL5SnQaxNFeTElFjnhH6ylWXTCapePT2Th&index=2&pp=gAQBiAQB) and other lazy loading resources.
			* Created [project repo](https://github.com/mejia-dev/smaart-chat/).
		* Created project, created first component then realized I wasn't prompted for options like SG or SSR on install. Did some research and determined that it was because the app was created through the git bash terminal (a known issue on Windows). Deleted the project and recreated it through the command prompt.
		* Add basic components for login and registration. 
		* Create Firebase project.
		* WIP commit during Firebase setup/troubleshooting `ng add @angular/fire`.
		* Successfully added Firebase to project and registration is working.
		* Add working login.
		* Research how Firebase persists throughout different pages.
		* Add working logout button.
		* Push to [GitHub repo](https://github.com/mejia-dev/smaart-chat/). Still need to determine how to properly store enviornment variables in Angular before considering this working code.

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