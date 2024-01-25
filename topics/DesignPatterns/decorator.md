# Decorator

> This page requires more info!

aka: Wrapper

Group: Structural patterns

__Identification:__ Decorator can be recognized by creation methods or constructors that accept objects of the same class or interface as a current class.

Decorator is a pattern that lets you attach new behaviors to objects by placing these objects inside special wrapper objects that contain the behaviors.

An object can use the behavior of various classes, having references to multiple objects and delegating them all kinds of work. Aggregation/composition is the key principle behind many design patterns, including Decorator.

A _wrapper_ is an object that can be linked with some _target_ object. The wrapper contains the same set of methods as the target and delegates to it all requests it receives. However, the wrapper may alter the result by doing something either before or after it passes the request to the target.

When does a simple wrapper become the real decorator? As mentioned before, the wrapper implements the same interface as the wrapped object. That’s why from the client’s perspective these objects are identical. This will let you cover an object in multiple wrappers, adding the combined behavior of all the wrappers to it.

The client code would need to wrap a basic object into a set of decorators that match the client’s preferences. The resulting objects will be structured as a stack.

The last decorator in the stack would be the object that the client actually works with. Since all decorators implement the same interface as the base object, the rest of the client code won’t care whether it works with the “pure” object or the decorated one.

## Applicability

- Use the Decorator pattern when you need to be able to assign extra behaviors to objects at runtime without breaking the code that uses these objects.
- Use the pattern when it’s awkward or not possible to extend an object’s behavior using inheritance.


| Pros | Cons |
|------|------|
| ✅ You can extend an object’s behavior without making a new subclass. | ❌ It’s hard to remove a specific wrapper from the wrappers stack. |
| ✅ You can add or remove responsibilities from an object at runtime. | ❌ It’s hard to implement a decorator in such a way that its behavior doesn’t depend on the order in the decorators stack. |
| ✅ You can combine several behaviors by wrapping an object into multiple decorators. | ❌ The initial configuration code of layers might look pretty ugly. |
| ✅ Single Responsibility Principle. You can divide a monolithic class that implements many possible variants of behavior into several smaller classes. |


## Example

```js
/**
 * The base Component interface defines operations that can be altered by
 * decorators.
 */
interface Component {
    operation(): string;
}

/**
 * Concrete Components provide default implementations of the operations. There
 * might be several variations of these classes.
 */
class ConcreteComponent implements Component {
    public operation(): string {
        return 'ConcreteComponent';
    }
}

/**
 * The base Decorator class follows the same interface as the other components.
 * The primary purpose of this class is to define the wrapping interface for all
 * concrete decorators. The default implementation of the wrapping code might
 * include a field for storing a wrapped component and the means to initialize
 * it.
 */
class Decorator implements Component {
    protected component: Component;

    constructor(component: Component) {
        this.component = component;
    }

    /**
     * The Decorator delegates all work to the wrapped component.
     */
    public operation(): string {
        return this.component.operation();
    }
}

/**
 * Concrete Decorators call the wrapped object and alter its result in some way.
 */
class ConcreteDecoratorA extends Decorator {
    /**
     * Decorators may call parent implementation of the operation, instead of
     * calling the wrapped object directly. This approach simplifies extension
     * of decorator classes.
     */
    public operation(): string {
        return `ConcreteDecoratorA(${super.operation()})`;
    }
}

/**
 * Decorators can execute their behavior either before or after the call to a
 * wrapped object.
 */
class ConcreteDecoratorB extends Decorator {
    public operation(): string {
        return `ConcreteDecoratorB(${super.operation()})`;
    }
}

/**
 * The client code works with all objects using the Component interface. This
 * way it can stay independent of the concrete classes of components it works
 * with.
 */
function clientCode(component: Component) {
    // ...

    console.log(`RESULT: ${component.operation()}`);

    // ...
}

/**
 * This way the client code can support both simple components...
 */
const simple = new ConcreteComponent();
console.log('Client: I\'ve got a simple component:');
clientCode(simple);
console.log('');

/**
 * ...as well as decorated ones.
 *
 * Note how decorators can wrap not only simple components but the other
 * decorators as well.
 */
const decorator1 = new ConcreteDecoratorA(simple);
const decorator2 = new ConcreteDecoratorB(decorator1);
console.log('Client: Now I\'ve got a decorated component:');
clientCode(decorator2);
```



---

## Resources

- https://refactoring.guru/design-patterns/decorator
- https://refactoring.guru/design-patterns/decorator/typescript/example
