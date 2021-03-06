# Naming conventions

CSS relies on _structured class names_ and _meaningful hyphens_ (i.e., not
using hyphens merely to separate words). This helps to work around the current
limits of applying CSS to the DOM (i.e., the lack of style encapsulation), and
to better communicate the relationships between classes.

The primary architectural division is between **[utilities](../design-principles/utilities.md)** and
**[components](../design-principles/components.md)**.

**Table of contents**

* [u-utilityName](#u-utilityName)
* [ComponentName](#ComponentName)
* [ComponentName--modifierName](#ComponentName--modifierName)
* [ComponentName-descendentName](#ComponentName-descendentName)
* [ComponentName.is-stateOfComponent](#is-stateOfComponent)

## [Utilities](utilities)

Low-level structural and positional traits. Utilities can be applied directly
to any element within a component.

Syntax: `u-<utilityName>`

<a name="u-utilityName"></a>
### u-utilityName

Utilities must use a camel case name. What follows is an example of how various
utilities can be used to create a simple structure within a component.

```html
<div class="u-clearfix">
	<a class="u-floatLeft" href="{{url}}">
		<img class="u-block" src="{{src}}" alt="">
	</a>
	<p class="u-sizeFill">
		…
	</p>
</div>
```

### Responsive utilities

Certain utilities have responsive variants using the patterns. eg: `u-small-<name>`,
`u-medium-<name>`, and `u-large-<name>` for small, medium, and large Media Query
breakpoints.


## [Components](components)

The CSS responsible for component-specific styling.

Syntax: `[<namespace>-]<ComponentName>[--modifierName|-descendentName]`

This has several benefits when reading and writing HTML and CSS:

* It helps to distinguish between the classes for the root of the component,
	descendent elements, and modifications.
* It keeps the specificity of selectors low.
* It helps to decouple presentation semantics from document semantics.

### namespace (optional)

If necessary, components can be prefixed with a namespace. For example, you may
wish to avoid the potential for collisions between libraries and your custom
components by prefixing all your components with a namespace.

```scss
.theme-Button { /* … */ }
.theme-Tabs { /* … */ }
```

This makes it clear, when reading the HTML, which components are part of your
library.

<a name="ComponentName"></a>
### ComponentName

The component's name must be written in pascal case. Nothing else in the
HTML/CSS uses pascal case.

```scss
.MyComponent { /* … */ }
```

```html
<article class="MyComponent">
	…
</article>
```

<a name="ComponentName--modifierName"></a>
### ComponentName--modifierName

A component modifier is a class that modifies the presentation of the base
component in some form (e.g., for a certain configuration of the component).
Modifier names must be written in camel case and be separated from the
component name by two hyphens. The class should be included in the HTML _in
addition_ to the base component class.

```scss
/* Core button */
.Button { /* … */ }

/* Default button style */
.Button--default { /* … */ }
```

```html
<button class="Button Button--default" type="button">…</button>
```

<a name="ComponentName-descendentName"></a>
### ComponentName-descendentName

A component descendent is a class that is attached to a descendent node of a
component. It's responsible for applying presentation directly to the
descendent on behalf of a particular component. Descendent names must be
written in camel case.

```html
<article class="Tweet">
	<header class="Tweet-header">
		<img class="Tweet-avatar" src="{{src}}" alt="{{alt}}">
		…
	</header>
	<div class="Tweet-bodyText">
		…
	</div>
</article>
```

<a name="is-stateOfComponent"></a>
### ComponentName.is-stateOfComponent

Use `is-stateName` to reflect changes to a component's state. The state name
must be camel case. **Never style these classes directly; they should always be
used as an adjoining class.**

This means that the same state names can be used in multiple contexts, but
every component must define its own styles for the state (as they are scoped to
the component).

```scss
.Tweet { /* … */ }
.Tweet.is-expanded { /* … */ }
```

```html
<article class="Tweet is-expanded">
	…
</article>
```
