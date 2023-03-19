- [[Outliner]]
	- **Branch**: a block with blocks underneath it
		- **Leaf**: a block with no blocks underneath it.
	- **Parent & Child** relations describe the hierarchy of blocks
		- A **Parent** can have *multiple* **Children**
		- A **Child** has *only one* **Parent**
		- A block can be a **Parent** and a **Child** at the same time
			- The **block** above this is a **parent** to this **block**
			- It is also a **child** to the **block** one level above it
- **Blocks** are the smallest *unit of information* that you can work with in **Logseq**
	- A **Page** corresponds to a single file on disk where we can store our **Blocks** inside of
		- **Logseqs** has multiple abilites to collect data from other different pages and blocks
			- So *a single page could contain only references to data in other places* and show it as if the data exists in that page itself
				- You can use [[Queries]] to show all data that matches your criteria
				- You can use [[Block references]] to:
					- make a link to a different **block**
					- embed the content of that **block** and all its **children**
					  id:: 64172cb8-6313-40a9-9d89-c1ffb78da2be
					- make a link/shortcut to that block that can be used outside **Logseq** to quickly open **Logseq** and show the block
				- You can even *embed entire pages* into your page -> ((64163108-4642-4bff-b3fd-c8fd45fde761))
- **Logseq** is built around the concept of [[Networked thinking]]
	- Because of this, the ability to link from one note to another is a very central concept of the application
	- You can either use `[[Links]]` which is the primary way to connect notes
	- And you can also give blocks and/or pages  `#tags` to connect notes
	  collapsed:: true
		- It is mostly a question of aesthetics as a **link** will look differently than a **tag**
			- But it does affect how you reference these connections in [[Queries]]
		- If a **tag** contains spaces, you can `#[[Write tags like this]]`
		  collapsed:: true
			- #+BEGIN_CAUTION
			  When using tags with the second syntax (`#[[Write tags like this]]`), there is a tiny bug you should know of:
			  
			  
			  #+BEGIN_EXAMPLE
			  This will not create the #[[tag]]s that you are expecting.
			  But this link to [[tag]]s will behave as expected.
			  #+END_EXAMPLE 
			  #+END_CAUTION
		- By default, the destination of a **tag** is a **page** with the same name as the **tag**
			- So you could have a page that describes what the tag stands for in more details
	- A very important detail about **links** _(and **tags**)_ in **Logseq** is that they are all **bi-directional**
		- Meaning that any link you make from **Page A** to *Page B*
			- **Page B** will be aware of and create a link back to *Page A*
				- Which leads us to the next topic: [[Graph View]]
- **Logseq** allows you to add [[Metadata]] about any page and/or block
- [[Commands]]
- [[Macros]]
- [[Customize Logseq]]