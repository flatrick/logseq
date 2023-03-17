- Creating a task can be done in multiple ways:
	- These can written by hand (in uppercase) at the beginning of a block to turn it into a task (see example below)
		- ```
		  NOW I am working on this
		  DOING And I am also working on this
		  IN-PROGRESS This is also being worked on
		  LATER I should work on this
		  TODO I should also work on this
		  WAIT I'm waiting on something to continue working on this
		  WAITING I'm also waiting on something to continue working on this
		  DONE I'm done working on this
		  CANCELED I won't be finishing this task
		  ```
	- They can be created using [[Slash-commands]]
	- You can turn a block into a task by using [[Keyboard Shortcuts]]
	  collapsed:: true
		- _under **Block editing general** called **Rotate the TODO state of the current item** will show you which combo is configured in your installation_
		- By using this toggle, you can switch between the most common states
		  collapsed:: true
			- `IN-PROGRESS`, `WAIT`, `WAITING` or `CANCELED` are not in the list of states the toggle will switch between
			  id:: 641494d2-5877-4d3a-92e1-419585706623
			  :LOGBOOK:
			  CLOCK: [2023-03-17 Fri 17:27:12]--[2023-03-17 Fri 17:27:13] =>  00:00:01
			  :END:
	- `IN-PROGRESS` and `WAIT` are not available through the [[Slash-commands]] nor through the toggle and has to be typed out by hand
		- These are most likely deprecated and/or forgotten to be removed
- # Examples
	- NOW I am working on this
	  :LOGBOOK:
	  CLOCK: [2023-03-17 Fri 17:04:02]
	  CLOCK: [2023-03-17 Fri 17:04:05]
	  :END:
	- DOING And I am also working on this
	  :LOGBOOK:
	  CLOCK: [2023-03-17 Fri 17:04:41]
	  CLOCK: [2023-03-17 Fri 17:04:44]
	  :END:
	- IN-PROGRESS This is also being worked on
	- LATER I should work on this
	- TODO I should also work on this
	- WAIT I'm waiting on something to continue working on this
	- WAITING I'm also waiting on something to continue working on this
	- DONE I'm done working on this
	- CANCELED I won't be finishing this task