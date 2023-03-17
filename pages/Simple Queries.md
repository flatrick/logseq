tags:: [[Logseq]], [[Database]], [[Query]], [[Clojure]]

- # Search for **pages** and/or **blocks**
  collapsed:: true
	- ## Search for a specific word
	  collapsed:: true
		- collapsed:: true
		  ```clojure
		  {{query Logseq}}
		  ```
			- {{query Logseq}}
			  query-table:: false
	- ## Search for a phrase using a "quoted string"
	  collapsed:: true
		- When we put quotation-marks around a string, we can search for a specific order of words
		- collapsed:: true
		  ```clojure
		  {{query "order of words"}}
		  ```
			- {{query "order of words"}}
			  query-table:: false
	- ## Search for where a [[Property]] has a specific value
	  collapsed:: true
		- By using [[Properties]] on our pages and blocks, we can make our notes searchable based on [[Metadata]]
		- collapsed:: true
		  ```clojure
		  {{query (property alias "Property") }}
		  ```
			- {{query (property alias "Property") }}
- # Search for **pages**
  collapsed:: true
	- ## Search for a **page** by name
	  collapsed:: true
		- collapsed:: true
		  ```clojure
		  {{query (page "Dynamic Variables") }}
		  ```
			- {{query (page "Dynamic Variables")}}
	- ## Search for **pages** that has any **Page-property** set
	  collapsed:: true
		- collapsed:: true
		  ```clojure
		  {{query (page-property alias) }}
		  ```
			- {{query (page-property alias) }}
	- ## Search for **pages** where a **Page-property** has a specific value
	  collapsed:: true
		- collapsed:: true
		  ```clojure
		  {{query (page-property alias "EDN") }}
		  ```
			- {{query (page-property alias "EDN") }}
	- ## Search for **pages** that have a specific tag
	  collapsed:: true
		- collapsed:: true
		  ```clojure
		  {{query (Page-tags Clojure) }}
		  ```
			- {{query (Page-tags Clojure)}}
	- ## Search for a **page** using [[Dynamic Variables]]
	  collapsed:: true
		- collapsed:: true
		  ```clojure
		  {{query (page <% current page %>) }}
		  ```
			- {{query (page <% current page %>) }}
- # Search for **blocks**
  collapsed:: true
	- ## Search for **blocks** or **properties** contain a specific `[[link]]`
	  collapsed:: true
		- collapsed:: true
		  ```clojure
		  {{query [[Query]] }}
		  ```
			- {{query [[Query]]}}
	- ## Search for **blocks** in a specific timeperiod (#Journal only!)
	  collapsed:: true
		- [[Logseq]] only allows to filter blocks based on #[[Date And Time]] in the [[Journal]] for [[Simple Queries]]
		- These are the available symbols you can use with the filter `BETWEEN`
		  collapsed:: true
			- 1. ` today - yesterday - tomorrow - now`
			  2. `+` or `-` followed by a digit/number and then the type `y - m - w - d - h - min`
				- **y** = **y**ear(s)
				  **m** = **m**onth(s)
				  **w** = **w**eek(s)
				  **d** = **d**ay(s)
				  **h** = **h**our(s)
				  **min** = **min**ute(s)
					- So we can say *5 days into the future* by typing: `+5d`
					- Or *5 days into the past*: `-5d`
					- And *1 hour into the past* can be written as `-1h` or `-60min`
		- collapsed:: true
		  ```clojure
		  {{query (between -7d +7d) }}
		  ```clojure
			- {{query (between -7d +7d)}}
		- collapsed:: true
		  ```clojure
		  {{query (between today +7d) }}
		  ```
			- {{query (between today +7d) }}
	- ## Search for **blocks** that has a [[Priority]] set
	  collapsed:: true
		- collapsed:: true
		  ```clojure
		   {{query (priority a) }}
		  ```
			- {{query (priority a) }}
		- collapsed:: true
		  ```clojure
		  {{query (priority b) }}
		  ```
			- {{query (priority b) }}
		- collapsed:: true
		  ```clojure
		  {{query (priority c) }}
		  ```
			- {{query (priority c) }}
		- collapsed:: true
		  ```clojure
		  {{query (priority a b c) }}
		  ```
			- {{query (priority a b c) }}
	- ## Search for #Tasks based on what state they are in
	  collapsed:: true
		- query-table:: false
		  collapsed:: true
		  ```clojure
		  {{query (task now doing in-progress) }}
		  ```
			- {{query (task now doing in-progress) }}
		- collapsed:: true
		  ```clojure
		  {{query (task later todo) }}
		  ```
			- {{query (task later todo) }}
		- collapsed:: true
		  ```clojure
		  {{query (task wait waiting) }}
		  ```
			- {{query (task wait waiting) }}
		- collapsed:: true
		  ```clojure
		  {{query (task done canceled) }}
		  ```
			- {{query (task done canceled) }}
- # Search for all **tags** used as a **page-tag**
  collapsed:: true
	- collapsed:: true
	  ```clojure
	  {{query (all-page-tags) }}
	  ```
		- {{query (all-page-tags)}}
- # Search using multiple criterias
  collapsed:: true
	- ## AND
		- collapsed:: true
		  ```clojure
		  {{query (and "Query" "Logseq") }}
		  ```
			- {{query (and "Query" "Logseq")}}
	- ## OR
		- collapsed:: true
		  ```clojure
		  {{query (or "Query" "Logseq") }}
		  ```
			- {{query (or "Query" "Logseq")}}
	- ## NOT
		- collapsed:: true
		  ```clojure
		  {{query (and "Query" (not "Logseq") ) }}
		  ```
			- {{query (and "Query" (not "Logseq"))}}
- # SORTING
	- #+BEGIN_QUOTE
	  Format: 
	  (sort-by property-name order) or (sort-by property-name)
	  
	  key: Can be any user property as well as built-in properties created-at  and updated-at.
	  
	  order: desc or asc, omit means desc.)
	  
	  Note that created-at and updated-at only work for pages.
	  #+END_QUOTE
	- collapsed:: true
	  ```clojure
	  {{query (and (task now later) (sort-by created-at desc) ) }}
	  ```
		- {{query (and (task now later) (sort-by created-at desc))}}
- # Combining options from above #[[unfinished]]
	- collapsed:: true
	  ```clojure
	  {{query (and [[Dynamic Variables]] "today" ) }}
	  ```
		- {{query (and [[Dynamic Variables]] "today" )}}