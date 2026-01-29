202503041204
Status: #idea
Tags:[[OOP]]

An abstract class is a class that guides the design of subclasses but cannot itself be instantiated as an object. Ex: An abstract Shape class might also specify that any subclass must define a computeArea() method.

An abstract method is a method that is not implemented in the base class, thus all derived classes must override the method. An abstract method is denoted by the keyword `abstract` in front of the method signature. A method signature defines the method's name and parameters. Ex: `abstract double computeArea();` declares an abstract method named computeArea().