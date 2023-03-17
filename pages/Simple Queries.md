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
	- `{{query (page "Dynamic Variables")}}`
	  collapsed:: true
		- {{query (page "Dynamic Variables")}}
- # Search for anywhere a [[Property]] has a specific value
- # Page-property
- # Page-tags
- # All-page-tags
  collapsed:: true
	- {{query (all-page-tags)}}
- # Task
- # Priority
- # Search using [[Dynamic Variables]]
	- `{{query (page <% current page %>) }}`
	  collapsed:: true
		- {{query (page <% current page %>) }}
- # Search using multiple matching criterias
  collapsed:: true
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
	- ## BETWEEN
		- `{{query (between -7d +7d)}}`
		  collapsed:: true
			- {{query (between -7d +7d)}}
- # Combining all options above [[unfinished]]
	- `{{query (and [[Dynamic Variables]] <% current page %> )}}`
	  collapsed:: true
		- {{query (and [[Dynamic Variables]] <% current page %> )}}