# Functional Programming

### Idempotency
Mathematically function is idempotent if f(f(x)) = f(x)   
e.g. -> Math.floor, ceil, lowercase/upperca
se, trim   
In FP, a function is idempotent, when we can call it many times with the same arguments and the result won’t change beyond initial calling      
E.g. HTTP GET,PUT, DELETE, sort

Idempotency is independent of side effects      
The function has side effects when
* it reads or modifies the global state
* writes or reads data from I/O or database
* uses a timestamp, current date
* uses something that has effects beyond it

f(x) = x+1 , pure but not idempotent  
in-place sort, idempotent but not pure  


Refs:   
https://szymonkrajewski.pl/what-is-idempotence/


### Imperative and Declarative Programming

Imperative programming (including OOP) describes computation in terms of the program state and changes to that state (How to do)

Declarative (functional) programming describes the desired results instead, and don’t specify changes to the state explicitly (What to do)




