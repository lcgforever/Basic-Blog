# Basic-Blog

```Java
Java Polymorphism
```

The most important difference is between the static and dynamic types of objects and references to objects.

Say B extends A and C extends B.

The dynamic type of an object (the type used in the new) is its actual runtime type: it defines the actual methods that are present for an object.

The static type of an object reference (a variable) is a compile-time type: it defines, or rather declares, which methods can be called on the object the variable references.

The static type of a variable should always be of the same type or a supertype of the dynamic type of the object it references.

So in our example, a variable with static type A can reference objects with dynamic types A, B and C. A variable with static type B can reference objects with dynamic types B and C. A variable with static type C can only reference objects with dynamic type C.

Finally, calling a method on an object reference is a subtle and complex interaction between static and dynamic types. (Read the Java Language Spec on method invocation if you don't believe me.)

If both A and B implement a method f() for example, and the static type is A and the dynamic type involved is C for a method invocation, then B.f() will be invoked:

```html
B extends A, C extends B
public A.f() {}
public B.f() {}
A x = new C(); // static type A, dynamic type C
x.f(); // B.f() invoked
```

Simplifying greatly: first the static types of both receiver (type A) and arguments (no args) are used to decide the best-matching (most specific) method signature for that particular invocation, and this is done at compile-time. Here, this is clearly A.f().

Then, in a second step at runtime, the dynamic type is used to locate the actual implementation of our method signature. We start with type C, but we don't find an implementation of f(), so we move up to B, and there we have a method B.f() that matches the signature of A.f(). So B.f() is invoked.

In our example we say that method B.f() overrides method A.f(). The mechanism of overriding methods in a type hierarchy is called subtype polymorphism.
