alias:: [[Datalog]], [[Datascript]]

- # Unsorted notes
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
			- #### `(pull ?VARIABLE [*]`
				- using the "pull API"
				- asking for all attributes found and stored in `?VARIABLE`
			- #### :where ...
				- the initial variable
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