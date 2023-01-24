# Software Engineering Paradigms and Best Practices

## Framework awareness
1. Unsupervised Top Down  
2. Unsupervised Bottom Up  
3. Supervised Top Down  
4. Supervised Bottom Up  

## PM Anti Patterns
1. Blowhard Jamboree: Pm reading junk media and pushing the tech stack on the developers
2. Viewgraph Engineering: Devs using automated documentation and viz tools due to lack of time
3. Death by Planning: Downstream problems by too complex scheduling
4. Fear of Success: Mania shortly before hitting success
5. Corncob: Difficult people obstructing the project
6. Intellectual Violence: Using knowledge about a specific subject to intimidate
7. Irrational Management: Indecisiveness and implicit de facto decision making
8. Smoke and Mirrors: Misrepresentations of the tech possibilities in sales
9. Project Mismanagement: Key activities overlooked and chaotic leadership
10. Throw It over the Wall: Guidelines written too literally
11. Fire Drill: Months of boredom due to non-tech stuff and then sudden need to deliver software
12. The Feud: Animosity among pms
13. E-mail Is Dangerous: Email used for sensitive communication

## SE Anti Patterns
1. The Blob: Procedural blob class; solution: isolating the effect of changes
2. Continuous Obsolescence new releases make compatibility hard; solution: focus on historically constant software
3. Lava Flow: Blocky code pieces inbetween; solution: refactor to smoothen out code reiteratively
4. Ambiguous Viewpoint: Concrete OOAD viewpoints are subjective and mix up interface with implementation; solution: make OOAD interfaces and implementation extremely clear in documentation
5. Functional Decomposition: Lots of function in huge classes; solution: focus on clear oop interfaces and implementation documentation
6. Poltergeists: Sneaky helper classes that are not atomic or distinct; solution: refactor to eliminate
7. Boat Anchor: Useless piece of software for show; solution: do not buy or use
8. Golden Hammer: Familiar technology or concept applied obsessively to many software problems; solution: study alternative technologies and approaches
9. Dead End: Irreversible modfication that leads to no-support policy for code; solution: think twice if no-support policy can be avoided
10. Spaghetti Code: Old ad hoc software structure; solution: refactor liberally and frequently
11. Input Kludge: Ad hoc algorithms are employed for handling program input; solution: keep to concrete system design telos
12. Walking through a Minefield: Original source code contains two to five bugs per line of code; solution: awareness and lots of dirty hands testing
13. Copypasta Programming: Maintenance problems due to copypasta methodology; solution: copypasta carefully
14. Mushroom Management: Policy to keep devs away from sales people; solution: good solution, sales people are wicked social sharks

## SE Design Atoms
1. Abstract Factory: Instance of several families of classes
2. Builder: separates object construction from its representation
3. Factory Method: Creates instance of several derived classes
4. Object Pool: Recycling objects that are no longer in use
5. Prototype: Fully initialized instance to be copied or cloned
6. Singleton: Class of which only a single instance can exist
8. Adapter: Matches interfaces of different classes
9. Bridge: separates an object’s interface from its implementation
10. Composite: Tree structure of simple and composite objects
11. Decorator: Adds responsibilities to objects dynamically
12. Facade: Single class that represents an entire subsystem
13. Flyweight: Fine-grained instance used for efficient sharing
14. Private Class Data: Restricts accessor/mutator access
15. Proxy: Object representing another object
16. Chain of responsibility: Way of passing a request between a chain of objects
17. Command: Encapsulate a command request as an object
18. Interpreter: Way to include language elements in a program
19. Iterator: Sequentially access the elements of a collection
20. Mediator: Defines simplified communication between classes
21. Memento: Capture and restore an object's internal state
22. Null Object: Default value of an object
23. Observer: Way of notifying change to a number of classes
24. State: Alter an object's behavior when its state changes
25. Strategy: Encapsulates an algorithm inside a class
27. Template Method: defer the exact steps of an algorithm to a subclass
28. Visitor: Defines a new operation to a class without change

## Linking
1. Interpreted: While running  
2. Compiled: Before running  

## Typing
1. Static: Program types KNOWN at COMPILE time  
2. Dynamic: Program types are KNOWN at RUN time  
3. Strong: Types are clearly ENFORCED in operations  
4. Weak: Types are language specifically/pragmatically USED in operations  

## Engineering
1. Imperative: Changes state (procedural (object oriented, event driven, modular, structured))  
2. Declarative: Doesn't change state (functional, first-oder logic, higher-order logic)  

## SOLID  
1. Single-Responsibility: There should never be more than one reason for a class to change  
2. Open-Closed: Open for extension but closed for modification  
3. Liskov substitution: Functions that use pointers or references to base classes must be able to use objects of derived classes without knowing it  
4. Interface-Segregation: Many client-specific interfaces are better than one general-purpose interface  
5. Dependency-Inversion: Depend upon abstractions, do not depend on concretions  

## ACID  
1. Atomicity: Fail entirely or do not fail  
2. Consistency: Roll back if not consistent according to preset rules  
3. Isolation: Atoms connot conflict with each other  
4. Durability: No log is ever lost and can be used to reinstate everything  

## 12 Factor App
1. One codebase tracked in revision control, many deploys  
2. Explicitly declare and isolate dependencies  
3. Store config in the environment  
4. Treat backing services as attached resources  
5. Strictly separate build and run stages  
6. Execute the app as one or more stateless processes  
7. Export services via port binding  
8. Scale out via the process model  
9. Maximize robustness with fast startup and graceful shutdown  
10. Keep development, staging, and production as similar as possible  
11. Treat logs as event streams  
12. Run admin/management tasks as one-off processes  

## Web App Speed
1. Point domain only, and only to load balancer  
2. Cache all slow, frequent and stable queries  
3. Static files HTTP caching for css, js, jpeg, png -> put on AWS S3/ Google Cloud  
4. Solve bottlenecks: Memory, CPU, Network I/O, Disk I/O  
5. Compute heavy logic offline/ Static web app HTML file  
6. Maintain database indexes  
7. CDN over subdomain/ CNAME, zip via gzip/minify  
8. Session data into redis, memcached  

## Web App Security
1. Keep only HTTP (80) SSL (443) ports open  
2. Disable ssh root and passauth (/etc/ssh/sshd_config/, PermitRootLogin no, PasswordAuthentication no)  
3. Manage access via ssh public keys (~/.ssh/authorized_keys)  
4. Never serve off nginx root/ Apache DocumentRoot  
5. Serve user content on entirely different domain  
6. Always use shelf Object Relational Mapper (ORM)  
7. Always use shelf HTML template library (ORM)  
8. Always use shelf CSRF Tokens  
9. Never open redirects  
10. Use crypto library to add unique salt to all user data  
11. Demand strong password input by design
12. Backcheck password input against huge rainbow table  
13. Never identify a user only through cookies  

## Security and legacy awareness
restrictive permissions
```
chmod 644 file; owner can read or write the file, others can only read it
chmod 600 file; owner can read or write the file, others can’t do anything with it
chmod 755 file; owner can read, write, or execute the file, others can read or execute it This is typically used for programs or for directories
chmod 700 file; owner can read, write, or execute the file, others can’t do anything with it
```
restrictive environment variables
```
export PATH=$PATH:set_clean_paths
~/.bash_profile
~/.bashrc
~/.profile
```
set shebang
```
#!/usr/bin/env setshebang
```
compelling code structure
```
#
# name
# copyright
# version
#
# synopsis
#
# classes
# methods
# main
#
```
expressive comments
```
# X Class does Y
```
