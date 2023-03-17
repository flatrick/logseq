tags:: [[Logseq]], [[Database]], [[Query]], [[Clojure]]

- # Search for a specific word
	- `{{query Logseq}}`
	  collapsed:: true
		- {{query Logseq}}
		  query-table:: false
- # Search for a phrase using a "quoted string"
	- When we put quotation-marks around a string, we can search for a specific order of words
	- `{{query "order of words"}}`
	  collapsed:: true
		- {{query "order of words"}}
		  query-table:: false
- # Search for where a specific `[[link]]` is used
	- `{{query [[Query]]}}`
		- {{query [[Query]]}}
- # Search for a **page** by name
	- `{{query (page "Dynamic Variables")}}`
		- {{query (page "Dynamic Variables")}}
- # Search for **blocks** and **pages** where a [[Property]] has a specific value
	- By using [[Properties]] on our pages and blocks, we can make our notes searchable based on [[Metadata]]
	- {{query (property alias "Property")}}
- # Search for **blocks** in a specific timeperiod (#Journal only!)
	- [[Logseq]] only allows to filter blocks based on #[[Date And Time]] in the [[Journal]] for [[Simple Queries]]
	- These are the available symbols you can use with the filter `BETWEEN`
		- 1. ` today - yesterday - tomorrow - now`
		  2. `+` or `-` followed by a digit/number and then the type `y - m - w - d - h - min`
			- **y** = **y**ear(s)
			  **m** = **m**onth(s)
			  **w** = **w**eek(s)
			  **d** = **d**ay(s)
			  **h** = **h**our(s)
			  **min** = **min**ute(s)
				- So we can say 5 days into the future by typing: `+5d`
				- Or 5 days into the past: `-5d`
				- 1 hour into the past can be written as `-1h` or `-60min`
	- `{{query (between -7d +7d)}}`
		- {{query (between -7d +7d)}}
	- `{{query (between today +7d)}}`
- # Search for **pages** that has any **Page-property** set
	- {{query (page-property alias)}}
- # Search for **pages** where a **Page-property** has a specific value
	- {{query (page-property alias "EDN")}}
- # Search for **pages** that have a specific tag
	- `{{query (Page-tags Clojure)}}`
		- {{query (Page-tags Clojure)}}
- # All-page-tags
	- {{query (all-page-tags)}}
- # Search for #Task based on what state they are in
	- {{query (task now doing in-progress)}}
	  query-table:: false
	- {{query (task later todo)}}
	- {{query (task wait waiting)}}
	- {{query (task done canceled)}}
- # Search for **blocks** that has a [[Priority]] set
	- {{query (priority a)}}
	- {{query (priority b)}}
	- {{query (priority c)}}
	- {{query (priority a b c)}}
- # Search using [[Dynamic Variables]]
	- `{{query (page <% current page %>) }}`
		- {{query (page <% current page %>) }}
- # Search using multiple criterias
	- ## AND
		- `{{query (and "Query" "Logseq")}}`
			- {{query (and "Query" "Logseq")}}
	- ## OR
		- `{{query (or "Query" "Logseq")}}`
			- {{query (or "Query" "Logseq")}}
	- ## NOT
		- `{{query (and "Query" (not "Logseq"))}}`
			- {{query (and "Query" (not "Logseq"))}}
- # SORTING
	- #+BEGIN_QUOTE
	  Format: (sort-by key order) or (sort-by key)
	  
	  key: created-at | updated-at
	  order: desc or asc, omit means desc.
	  
	  (and (task now later) (sort-by created-at desc))
	  #+END_QUOTE
- # Combining all options above #[[unfinished]]
	- `{{query (and [[Dynamic Variables]] <% current page %> )}}`
		- {{query (and [[Dynamic Variables]] <% current page %> )}}