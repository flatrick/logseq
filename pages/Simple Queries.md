tags:: [[Logseq]], [[Database]], [[Query]], [[Clojure]]

- # Search for a specific word
	- `{{query Logseq}}`
	  collapsed:: true
		- {{query "Logseq"}}
		  query-table:: false
- # Search for a phrase using a quoted string
	- When we put quotation-marks around a string, we can search for a specific order of words
		- `{{query "Query"}}`
		  collapsed:: true
			- {{query "Query"}}
			  query-table:: false
- # Search using dynamic variables
	- `{{query (page <% current page %>) }}` #[[Dynamic Variables]]
	  collapsed:: true
		- {{query (page <% current page %>) }}
- # Search using multiple matching criterias
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
- `{{query (and [[Dynamic Variables]] <% current page %> )}}` #[[Dynamic Variables]]
  collapsed:: true
	- {{query (and [[Dynamic Variables]] <% current page %> )}}