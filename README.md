# Clojure Basics

References
  - https://www.braveclojure.com/do-things/
  - https://clojuredocs.org

#### Forms
- "Form" is a term to reffer a valid code, that could be two types of structures: literal expressions of data structures and operations.
- Clojure evaluates every form to produce a value.

### Literal expressions

#### Numbers
```clojure
(type 5) ;;=> java.lang.Long
(type 5.5) ;;=> java.lang.Double
```
#### Strings
```clojure
(str "Hello Clojure World") ;;=> "Hello Clojure World"
(str "Hello \"JVM\" World") ;;=> "Hello \"JVM\" World"
(str "Hello! ", "Functional Programming") ;;=> "Hello! Functional Programming"

(def greeting "Hello Friends") ;;=> #'user/greeting
(str greeting) ;;=> "Hello Friends"
```
#### Maps
- A hash to associate a value with other value.
- There are two types: hash maps and sorted maps.

##### Hash Maps
```clojure
(def country {:name "Brazil" :language "Portuguese"}) ;;=> #'user/country
(def state {:name "São Paulo" :country [country]}) ;;=> #'user/state

(get state :name) ;;=> "São Paulo"
(get-in state [:country 0 :name]) ;;=> "Brazil"

(hash-map :city "São Paulo" :population 12106920) ;;=> {:city "São Paulo", :population 12106920}
(get {:city "São Paulo" :population 12106920} :gdp "unknown") ;;=> "unknown"
```
##### Sorted Maps
- Sort a map by its keys
```clojure
(sorted-map :c "Cake" :b "Ball" :a "Art") ;;=> {:a "Art", :b "Ball", :c "Cake"}
```
#### Vectors
- A Vector is a collection of values indexed by contiguous integer
 - Just like an array, with a 0-indexed collection and offers efficient random access (by index)
 - conj function is used to append a new value at the end of the vector
```clojure
[10 20 30] ;;=> [10 20 30]
(get [10 20 30] 0) ;;=> 10

(def country-vector ["Brazil" "Chile" "Portugal"]) ;;=> #'user/country-vector
(get country-vector 0) ;;=> "Brazil"
(get country-vector 5 "Unknown") ;;=> "Unknown"

(conj country-vector "Argentina") ;;=> ["Brazil" "Chile" "Portugal" "Argentina"]
```
#### Lists
- A List is a collections, access or modifications of list head is efficient, random access is not.
- Use Lists if you need to easily add items to the beginning of a sequence or if you’re writing a macro.

```clojure
'(1 2 3 4) ;;=> 
(list :a :b :c) ;;=> (:a :b :c)
(nth '("Brazil" "Chile" "Portugal", "The Netherlands") 0) ;;=> "Brazil"
(conj '(:two :three :four) :one) ;;=> (:one :two :three :four)
```

#### Sets
- A set is a collection of unique values.
- Two kinds of Sets: hash sets and sorted sets

##### Hash Sets
- Kind of set that is used more often

```clojure
(hash-set 1 1 1 2 3 4 5 5) ;;=> #{1 2 3 4 5}

(= (hash-set 1 2 3) #{1 2 3}) ;;=> true

;; Add a new item to the set
(conj #{:a :b} :c :d :e) ;;=> #{:a :c :b :d :e}

;; creating a set from an existing vector or list
(set [1 1 2 3 3 4 5 5]) ;;=> #{1 2 3 4 5}
(set '(1 1 2 3 3 4 5 5)) ;;=> #{1 2 3 4 5}

;; check for set membership
;; contains? returns true or false
(contains? #{:a :b :c} :a) ;;=> true

;; get and keyword lookup will returns the value if it exists or nil if it doesn't
(get #{:a :b :c} :a) ;;=> :a
(:b #{:a :b :c}) ;;=> :b
```

##### Sorted Sets
- Return a new sorted set with unique items
- It's only accepted items of the same type, otherwise will thrown an java.lang.ClassCastException exception

```clojure
(sorted-set 3 2 2 4 1) ;;=> #{1 2 3 4}
(sorted-set :c :b :a) ;;=> #{:a :b :c}
```
