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
- # The parts of a query
	- # :title
	- # :query
	  collapsed:: true
		- ## :find
		  collapsed:: true
			-
		- ## :where
	- # :inputs
	- # :view
	  collapsed:: true
		- ## `(fn [query-result] [:div ...])`
	- # :result-transform
	  collapsed:: true
		- ## `(fn [query-result] ...)`
	- # :collapsed?
	- # :rules [...]
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
	- https://max-datom.com/
	- https://qwxlea.github.io/#/page/datalog%2FIntro%20to%20Datalog
	- https://youtu.be/tV4pHW_WOrY
	-