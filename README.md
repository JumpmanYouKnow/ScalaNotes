ScalaNotes
====================
I wrote more than 5000 lines of scala code about 1 year ago, but later on I don't have any chance to write it. (Univeristy doesn't teach it, previous internships don't use it, what a pity, such a beautiful language)

Now I'm picking it up as the University teaches spark by scala, but I feel that I forgot lots of not only syntax but also some key knowledge about scala.

Therefore I want to open this repo as my scala notes.



Side Effect
---------------------

### 1. map on iterator no side effect: https://stackoverflow.com/questions/12631778/scala-map-on-iterator-does-not-produce-side-effects

> List(1,2,3,4).iterator.map((x: Int) => println(x))

doesn't print

while

> List(1,2,3,4).map((x: Int) => println(x)) 

> List(1,2,3,4).foreach((x: Int) => println(x))

> List(1,2,3,4).iterator.foreach((x: Int) => println(x))

all do
#### Note:

- map on iterator is lazy, put "toList" in the end will fix it.
- but should use foreach, as it is designed for side effects(won't allow laziness)
