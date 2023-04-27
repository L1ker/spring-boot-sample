# Creational Design Patterns

## Factory Method

Interface for creating objects in superclass but allow for subclasses to alter the type of the object that will be created.
Instead of using `new` keyword to create objects new objects are created using a factory method this method's return type is an interface which is implemented by all different types of objects we want to create using the factory.

> Objects created by a factory are called _products_

Fancy things to say about factory methods:
- utilizes Single Responsibility Principle - only the factory is responsible for creating objects and the factory does nothing else
- utilizes Open/Closed Principle - open for extension, closed for modification, allows others to create new products easily without having to change existing code

#### Pros:
- very extensive - see Open/Closed Principle
- adaptive towards type changes in dependencies 
- can be used to monitor object creation and save compute by before creating a new instance (which can be expensive) to check if there is a suitable old instance first

#### Cons:
- some added complexity

## Abstract Factory

Imagine you not only want to create different types of furniture but each type of furniture also belongs to a certain other group.
E.g. you sell chairs and tables but each chair and table also has a certain style (like modern, Bauhaus or communist) using abstract factories you can be certain to create only furniture of a certain style.

#### How?
Create a FurnitureFactory interface with a createMethod for each type of furniture (just like a normal factory) except that you don't specify a certain class for the furniture but an interface for each type. So, you have the chair and table interface. 
Then create a ModernFurnitureFactory which only creates modern furniture and implements the create methods of your abstract factory (even though it's an interface). 


#### Pros: 
- similar to factory but also allows to be sure which group a certain product belongs to (kinda specific need imo)

#### Cons:
- even more complexity

## Builder

Usually when a certain class has different types of instances inheritance is a good choice. But with a huge number of configurations it may be smart to move them into the superclass and just use builders - which make the object completely configurable without having to change any constructors or having 20 nulls in your AllArgsConstructor. (Also, builders look nice in code because functional programming yes)

If you often need a similarly configured objects and have builders - use a director.

#### Pros:
- utilizes Single Responsibility Principle - allows for object creation to be decoupled from business logic (but not necessarily)
- as flexible as can be in object creation regarding different configurations

#### Cons:
- complexity if you are not used to it I guess

## Prototype

> Name is confusing as it is not really a prototype but rather a cell during cell division which clones itself.

Imagine you want to copy an object for your test but that's not possible because certain fields cannot be set from outside as they are private - also this would make your code depend on that class staying the same which it will most likely not

To fix that use prototypes - prototypes are classes that implement a cloning interface - inside the class access modifiers are no problem so here you can properly create a copy of an object.

> Objects that allow cloning (implement some cloning interface) are called prototypes

If you often need certain types of objects created you can use a PrototypeRegistry which gives you some common objects based on search criteria.

## Singleton 

> A singleton is a class which can have only one instance at a time & this instance is globally accessible but write protected

Usually good for classes that control access to a shared resource - you don't want another database connection but use the existing one, right?

#### How does it work in a nutshell?
Have private constructor which is only called in a static method (getSingleton) this static method creates a new object the first time and should subsequently only return the existing object

#### Pros:
- Well, kinda needed for managing access to shared resources

#### Cons:
- Single Responsibility Principle violated - one instance at a time **&** globally accessible
- rip in multi-thread environments
- mocking singletons is difficult as mocking usually uses the classes constructor which is private here - rip testing
