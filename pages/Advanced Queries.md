alias:: [[Datalog]], [[Datascript]]

- `?b` = block
- `?p` = page
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
	-