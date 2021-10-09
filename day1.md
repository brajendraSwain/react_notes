 - defining the function with bind this in constructor
 --- 
 Render is handled in different context, this is undefined in that case



 - error in async block are not detected
 ** The problem is that asynchronous code runs outside the render and commit phases of React. How can we fix it then? The solution is right in front of us. Luckily, Dan Abramov
 
 --
 setState(() => {
  throw new Error('hi')
})


===================

Forwarding Ref:
 - A ref can be passed to the component which is used as ref in side the component

--------------
const FancyButton = React.forwardRef((props, ref) => (
  <button ref={ref} className="FancyButton">
    {props.children}
  </button>
));

// You can now get a ref directly to the DOM button:
const ref = React.createRef();
<FancyButton ref={ref}>Click me!</FancyButton>;
-----------------------------------------------

# Fragments

# Higher order components (HOC)
========================================
Concretely, a higher-order component is a function that takes a component and returns a new component.

A HOC is a pure function with zero side-effects.

Mixins are considered harmful:::::]
---------------------------------
 React has declarative rendering and top-down data flow
 	= Mixins introduce implicit dependencies
 	= Mixins cause name clashes
---------------------------------------------------
- Don’t Mutate the Original Component. Use Composition.

Caveats:
  - Don’t Use HOCs Inside the render Method
  			-- Instead, apply HOCs outside the component definition so that the resulting component is created only once. Then, its identity will be consistent across renders. This is usually what you want, anyway.
  - Static Methods Must Be Copied Over
  - Refs Aren’t Passed Through
  		- That’s because ref is not really a prop — like key, it’s handled specially by React.
  		- f you add a ref to an element whose component is the result of a HOC, the ref refers to an instance of the outermost container component, not the wrapped component.
  		- The solution for this problem is to use the React.forwardRef API (introduced with React 16.3)
