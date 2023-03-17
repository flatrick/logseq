tags:: [[Logseq]], [[Database]], [[Query]], [[Clojure]]

- # Search for a specific word
  collapsed:: true
	- `{{query Logseq}}`
	  collapsed:: true
		- {{query "Logseq"}}
		  query-table:: false
- # Search for a phrase using a "quoted string"
  collapsed:: true
	- When we put quotation-marks around a string, we can search for a specific order of words
		- `{{query "order of words"}}`
		  collapsed:: true
			- {{query "order of words"}}
			  query-table:: false
- # Search for where a specific `[[link]]` is used
  collapsed:: true
	- `{{query [[Query]]}}`
		- {{query [[Query]]}}
- # Search for a page by name
  collapsed:: true
	- `{{query (page "Dynamic Variables")}}`
	  collapsed:: true
		- {{query (page "Dynamic Variables")}}
- # Search for anywhere a [[Property]] has a specific value #[[unfinished]]
- # Search for blocks in a specific timeperiod in the [[Journal]]
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
	  collapsed:: true
		- {{query (between -7d +7d)}}
- # Page-property #[[unfinished]]
- # Search for pages that have specific tags
  collapsed:: true
	- `{{query (Page-tags Clojure)}}`
		- {{query (Page-tags Clojure)}}
- # All-page-tags
  collapsed:: true
	- {{query (all-page-tags)}}
- # Task
- # Priority
- # Search using [[Dynamic Variables]]
	- `{{query (page <% current page %>) }}`
	  collapsed:: true
		- {{query (page <% current page %>) }}
- # Search using multiple criterias
	- ## AND
		- `{{query (and "Query" "Logseq")}}`
		  collapsed:: true
			- {{query (and "Query" "Logseq")}}
	- ## OR
		- `{{query (or "Query" "Logseq")}}`
		  collapsed:: true
			- {{query (or "Query" "Logseq")}}
	- ## NOT
		- `{{query (and "Query" (not "Logseq"))}}`
		  collapsed:: true
			- {{query (and "Query" (not "Logseq"))}}
- # Combining all options above #[[unfinished]]
	- `{{query (and [[Dynamic Variables]] <% current page %> )}}`
	  collapsed:: true
		- {{query (and [[Dynamic Variables]] <% current page %> )}}