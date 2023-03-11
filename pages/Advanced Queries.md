alias:: [[Datalog]], [[Datascript]]

- # Unsorted notes
  collapsed:: true
	- a questionmark followed by letters are used as placeholders (variables) for data
	  collapsed:: true
		- according to some docs, [[Logseq]] treats `?b` and `?p` differently
			- `?b` = block
			- `?p` = page
			- LATER Verify if this is really true or a misunderstanding that has spread
			  :LOGBOOK:
			  CLOCK: [2023-03-11 Sat 14:39:28]
			  :END:
	- Queries are written in [[Extensible Data Notation]]
		- simple
		- declarative
		- logic
		- `$name` refers to a database
		- `?name` refers to a variable
		- `_ATTRIBUTE` will ask for the parent that holds the specific attribute
		- `:keyword` / `:namespace/keyword` can refer to **functions** or **attribute-names**
		- `_` can be used as a wildcard for the parts you want to discard
- # Hiccup
- # The parts of a query
	- ## :title
	- ## :query
		- ### :find
		  id:: 640c9a94-4943-47d3-bea4-eed3a8a7ee7b
			- if only supply a variable-name, the ID of the matched entity will be returned
			- #### `(pull ?VARIABLE [*])` / `(pull ?VARIABLE [:ATTRIBUTE1 :ATTRIBUTE2])`
				- by using the **Pull Syntax/API**, we can ask for some/all **attributes** of the **entities**
				- `?VARIABLE [:ATTRIBUTE1 :ATTRIBUTE2]`
					- this would return a list of all **entities**, showing only the two **values** of the requested **attributes** for each **entity**
				- `(pull ?VARIABLE [*])`
					- this would return a list of all entities, showing all **values** for each **entity** thanks to the wildcard *(the asterisk)*
			- #### :in _(optional)_
			  collapsed:: true
				- **:in** can be omitted and then it will use the entire database
				- when used, you need to define which database to use *(`$` can often be used as a shortcut)*
				- to use dynamic values as input, we need to supply the variable here (`?var`)
					- ```clojure
					  [ :find ?person
					   :in $ ?day
					   :where
					   [$ ?d :meeting/date ?day]
					   [$ ?s :staff/employee ?p]
					   [$ ?s :staff/name ?person] ]
					  :input [ :today ]
					  ```
						- this query will list the names of all people who attended the meeting today using the special **macro** `:today`
					- when used outside of [[Logseq]], these variables can be supplied when calling this query
					- if more than one dynamic values are needed, all of these must be defined in the `:in` clause
						- and in the case of [[Logseq]], their values must be added to `:input [ ]`
				- ##### collections #unfinished
					- If you want to find
					- ```clojure
					  [:find ?title
					   :in $ [?director ...]
					   :where
					   [?p :person/name ?director]
					   [?m :movie/director ?p]
					   [?m :movie/title ?title]]
					  :input [ "James Cameron" "Ridley Scott" ]
					  ```
			- #### :where
				- the **initial variable** is the collection the operation will be performed on
				- the second part is the **attribute** to be looked at
				- the third/last part *(optional)* can be:
					- 1. a string/int that it will use to find **entities** where the **attribute** matches
					- 2. a **variable** (`?var`) that stores a list of **entities** that has the specified **attribute** that can be used in later stages or to be returned to the
					- 3. a **variable** that is set from input that is used to find matching **entities**
						- in the case of [[Logseq]], it is in the `:input [ ]` clause
					- *if omitted,* it will return the **entity/entities** that have the **attribute** defined in this **where-clause**
						- more specifically, their *unique identifier* will be returned
							- in the **:find** clause we can select the specific **attribute** to extract
				- multiple **where-clauses** are implicitly added as **AND**
				  collapsed:: true
					- in other words, all clauses must match with an **entity** for it to be returned
				- the following **where-clause** will only match **entities** that has the **attribute** `age` and where the **value** of `age` is `21` or higher
				  collapsed:: true
					- ```clojure
					  :where
					  [?e :user/age ?age]
					  [(>= ?age 21)]
					  ```
						- `?e` is the _collection of **entities**_ that we want to get data from
						- the **entities** must have the **attribute** `:user/age`
						- we keep track of these entities' `:user/age`-**attribute** in the **variable** `?age`
						- then we say that we only want the **entities** where `:user/age` is **21 or higher**
	- ## :inputs
	- ## :view
	  collapsed:: true
		- ## `(fn [query-result] [:div ...])`
	- ## :result-transform
		- ### `(fn [query-result] ...)`
	- ## :collapsed?
	- ## :rules [...]
- # Example
	- ```clojure
	  {:title  [:h2 "Your query title"]
	   :query  [:find (pull ?b [*])
	            :where ...]
	   :inputs [...]
	   :view (fn [query-result] [:div ...]) ;; or :keyword from config.edn
	   :result-transform (fn [query-result] ...) ;; or :keyword from config.edn
	   :collapsed? true
	  :rules [...]}
	  ```
- # Links
	- [Max Datom - An Interactive Datomic Learning Experience](https://max-datom.com/)
	- [Datomic Queries and Rules](https://docs.datomic.com/on-prem/query/query.html)
	- [Learn DataLog Today](https://www.learndatalogtoday.org/)
	- [Datascript - Getting started](https://github.com/tonsky/datascript/wiki/Getting-started)
	- [Datascript and Datomic: Data Modeling for Heroes - Mark Bastian](https://youtu.be/tV4pHW_WOrY)
	- [Logseq Schema](https://github.com/logseq/logseq/blob/master/deps/db/src/logseq/db/schema.cljs)
	- [Logseq Rules](https://github.com/logseq/logseq/blob/master/deps/db/src/logseq/db/rules.cljc)
	- [Learning resources for advanced queries (Datalog)](https://discuss.logseq.com/t/learning-resources-for-advanced-queries-datalog/8619)
	- [Advanced Queries - Docs Logseq](https://docs.logseq.com/#/page/advanced%20queries)
	- [Datomic Tutorial - Missing Link Tutorials](https://github.com/ftravers/datomic-tutorial)
	- [Intro to Datalog - qwxlea](https://qwxlea.github.io/#/page/datalog%2FIntro%20to%20Datalog)