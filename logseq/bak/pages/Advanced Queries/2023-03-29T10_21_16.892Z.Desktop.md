filters:: {}
tags:: [[Extensible Data Notation]], [[Logseq]], [[Datalog]], [[Datascript]], [[Database]], [[Query]], [[Clojure]]

- # Unsorted notes
	- a questionmark followed by letters are used as placeholders (variables or symbols) for data
		- according to some docs, [[Logseq]] treats `?b` and `?p` differently
			- `?b` = block
			- `?p` = page
			- LATER Verify if this is really true or a misunderstanding that has spread
			  :LOGBOOK:
			  CLOCK: [2023-03-11 Sat 14:39:28]
			  :END:
				- https://github.com/logseq/logseq/blob/master/deps/db/src/logseq/db/rules.cljc#L64
	- Queries are written in [[Extensible Data Notation]]
		- simple
		- declarative
		- logic
		- `$name` refers to a database
		- `?name` refers to a variable
		- `_ATTRIBUTE` will ask for the parent that holds the specific attribute
		- `:keyword` / `:namespace/keyword` can refer to **functions** or **attribute-names**
		- `_` When we don't care about certain components of the tuples in a query, but must put something in the clause in order to get to the positions we care about we can use the underscore symbol
			- It is a blank placeholder, *matching anything without binding or unifying*
				- Using a variable instead of **_** will cause unnecessary work for the query engine
- # Grammar / Terminology
  collapsed:: true
	- `''` = literal
	- `""` = string
	- `[]` = list or vector
	- `{}` = map {k1 v1 ...}
	- `()` = grouping
	- `|` = choice
	- `?` = zero or more
	- `+` = one or more
	- `:keyword` = keywords are functions we use to describe what/how to get the data we want
	- `:namespace/keyword` = a keyword in a namespace.
		- Namespaces are used to show a relationship between multiple keywords
	- `?symbol` = symbols are what most other languages would call a **variable**.
		- It holds (a reference to) data, either input from the user or output from a step
- # The parts of a query
  collapsed:: true
	- ## :title
		- ### [[Hiccup]]
	- ## :query
		- ### :find
			- if you only supply a variable-name, the ID of the matched entity will be returned
			- #### Aggregates (min, max, sum)
				- https://docs.datomic.com/on-prem/query/query.html#aggregates
			- #### Pull Syntax/API
				- by using the **Pull Syntax/API**, we can ask for some or all **attributes** of the **entities**
				- `(pull ?VARIABLE [:ATTRIBUTE1 :ATTRIBUTE2])`
					- this would return a list of all **entities**, showing only the two **values** of the requested **attributes** for each **entity**
				- `(pull ?VARIABLE [*])`
					- this would return a list of all entities, showing all **values** for each **entity** thanks to the wildcard *(the asterisk)*
			- #### :in _(optional)_
				- **:in** can be omitted in [[Logseq]] when you aren't using ((640e3bfb-0c22-493b-8222-0acbfe19ccb9)) variables
					- since there is only one database, it will know which one to use
					- https://docs.datomic.com/on-prem/query/query.html#implicit-data-source
				- when used, you first need to define which database to use by writing `$`
				- to use dynamic values as input, we need to supply the variable in the `:in`-clause
					- ```clojure
					  [ :find ?person
					   :in $ ?day
					   :where
					   [$ ?d :meeting/date ?day]
					   [$ ?d :meeting/participants ?p]
					   [$ ?p :staff/name ?person] ]
					  :input [ :today ]
					  ```
						- this query will list the names of all people who attended the meeting today using the special **macro** `:today`
					- when used outside of [[Logseq]], these variables can be supplied when calling this query
					- if more than one dynamic value is needed, all of these must be defined in the `:in`-clause
						- and in the case of [[Logseq]], their values must be added to `:input [ ]` clause further down
				- ##### **collections**
					- If you want to search for multiple entities with different values, you can use three dots after the variable name (`[?var ...]`)
						- ```clojure
						  [:find ?title
						   :in $ [?director ...]
						   :where
						   [?p :person/name ?director]
						   [?m :movie/director ?p]
						   [?m :movie/title ?title]]
						  :input [ "James Cameron" "Ridley Scott" ]
						  ```
						- this query would do two searches, one per input, and return them as one result
			- #### :where
				- the initial **variable** is the collection the operation will be performed on
					- if it hasn't been used yet, it will point to the whole database
					- if it was used as the last part in a previous step
						- this part will only be run against those entities that was matched in that previous step
				- the second part is the **attribute** to be looked at
				- the third/last part *(optional)* can be:
					- 1. a string/int that it will use to find **entities** where the **attribute** matches
					- 2. a **variable** (`?var`) that stores a list of **entities** that has the specified **attribute** that can be used in later stages, or to be returned to the `pull` clause
					- 3. a **variable** that is set from input that is used to find matching **entities**
						- in the case of [[Logseq]], it is in the `:input [ ]` clause
					- *if omitted,* it will return the **entity/entities** that have the **attribute** defined in this **where-clause**
						- more specifically, their *unique identifier* will be returned
							- in the **:find** clause we can select the specific **attribute** to extract
				- the following **where-clause** will only match **entities** that has the **attribute** `age` and where the **value** of `age` is `21` or higher
					- ```clojure
					  :where
					  	[?e :user/age ?age]
					  	[(>= ?age 21)]
					  ```
						- `?e` is the _collection of **entities**_ that we want to get data from
						- the **entities** must have the **attribute** `:user/age`
						- we keep track of these entities' `:user/age`-**attribute** in the **variable** `?age`
						- then we say that we only want the **entities** where `:user/age` is **21 or higher**
				- ##### AND (filtering on multiple values)
					- [[Datascript]] uses **AND** implicitly so any new where-clauses will all have to match
				- ##### OR
					- https://docs.datomic.com/on-prem/query/query.html#or-clauses
					- ```clojure
					  :where
					  	[?e :user/age ?age]
					  	(or
					  		[(>= ?age 21)]
					       	[(<= ?age 12)]
					       )
					  ```
				- ##### NOT
					- https://docs.datomic.com/on-prem/query/query.html#not-clauses
					- ``` clojure
					  :where
					  	[?e :user/age ?age]
					  	(not
					  		[(>= ?age 21)]
					       	[(<= ?age 12)]
					       )
					  ```
			- #### :with
				- https://docs.datomic.com/on-prem/query/query.html#with
	- ## :input
	  id:: 640e3bfb-0c22-493b-8222-0acbfe19ccb9
		- ```clojure
		  [:find ?title
		   :in $ [?director ]
		   :where
		   [?p :person/name ?director]
		   [?m :movie/director ?p]
		   [?m :movie/title ?title]]
		  :input [ "James Cameron" ]
		  ```
	- ## :view
		- ## `(fn [query-result] [:div ...])`
	- ## :result-transform
		- ### `(fn [query-result] ...)`
	- ## :collapsed?
	- ## :rules [...]
		- https://docs.datomic.com/on-prem/query/query.html#rules
- # Examples
	- ```clojure
	  {:title  [:h2 "Your query title"]
	   :query  [:find (pull ?b [*])
	            :in $
	            :where ...]
	   :inputs [...]
	   :view (fn [query-result] [:div ...]) ;; or :keyword from config.edn
	   :result-transform (fn [query-result] ...) ;; or :keyword from config.edn
	   :collapsed? true
	  :rules [...]}
	  ```
	- ## Combining [[Simple Queries]] and [[Advanced Queries]]
	  id:: 6414d3e8-cf73-41de-a7b7-1c2d178cbfb0
		- ```clojure
		  {:title "🔨 All todos with current pages tag"
		   :query (and (task TODO DOING) <% current page %>)
		   :result-transform (fn [result]
		                       (sort-by (fn [h]
		                                  (get h :block/priority "Z")) result))
		   }
		  ```
- # Links
	- ## [[Logseq]] Query Learning Sprint (Summer 2022)
		- [Lesson 1](https://discuss.logseq.com/t/lesson-1-what-are-logseq-queries-and-why-you-should-learn-to-use-them/9987) What Are Logseq Queries and Why You Should Learn to Use Them
		- [Lesson 2](https://discuss.logseq.com/t/lesson-2-why-you-should-outline-and-link-your-notes/10038) Why You Should Outline and Link Your Notes
		- [Lesson 3](https://discuss.logseq.com/t/lesson-3-how-to-think-like-a-computer-using-boolean-logic/10074) How to Think Like a Computer Using Boolean Logic
		- [Lesson 4](https://discuss.logseq.com/t/lesson-4-how-to-search-your-notes-using-query-filters-and-links/10131) How to Search Your Notes Using Query Filters and Links
		- [Lesson 5](https://discuss.logseq.com/t/lesson-5-how-to-power-your-workflows-using-properties-and-dynamic-variables/10173) How to Power Your Workflows Using [[Properties]] and [[Dynamic Variables]]
		- [Challenge 1](https://discuss.logseq.com/t/challenge-1-build-a-dynamic-notes-index/10274) Build a Dynamic Notes Index
		- [Challenge 2](https://discuss.logseq.com/t/challenge-2-build-a-content-consumption-pipeline/10305) Build a Content Consumption Pipeline
		- [Challenge 3](https://discuss.logseq.com/t/challenge-3-build-a-content-creation-pipeline/10333) Build a Content Creation Pipeline
		- [Challenge 4](https://discuss.logseq.com/t/challenge-4-build-a-project-management-dashboard/10384) Build a Project Management Dashboard
		- [Challenge 5](https://discuss.logseq.com/t/challenge-5-build-a-personal-learning-dashboard/10418) Build a Personal Learning Dashboard
	- ## unsorted list
		- [Learning resources for advanced queries (Datalog)](https://discuss.logseq.com/t/learning-resources-for-advanced-queries-datalog/8619)
		- [Advanced Queries - Docs Logseq](https://docs.logseq.com/#/page/advanced%20queries)
		- [Logseq Schema](https://github.com/logseq/logseq/blob/master/deps/db/src/logseq/db/schema.cljs)
		- [Logseq Rules](https://github.com/logseq/logseq/blob/master/deps/db/src/logseq/db/rules.cljc)
		- [Intro to Datalog - qwxlea](https://qwxlea.github.io/#/page/datalog%2FIntro%20to%20Datalog)
		- [Learn DataLog Today](https://www.learndatalogtoday.org/)
		- [Datomic Queries and Rules](https://docs.datomic.com/on-prem/query/query.html)
		- [Datascript - Getting started](https://github.com/tonsky/datascript/wiki/Getting-started)
		- [Datomic Tutorial - Missing Link Tutorials](https://github.com/ftravers/datomic-tutorial)
		- [Datascript and Datomic: Data Modeling for Heroes - Mark Bastian](https://youtu.be/tV4pHW_WOrY)