# What is useRef()?
useRef() creates a persistent reference to a DOM node or value that does not cause a re-render when changed. Think of it like a box that can store a value — and stays the same between renders.

###  Common Use Cases
- Accessing DOM elements directly (like focusing an input)
- Storing previous values
- Avoiding re-renders for mutable values
- Timer/interval references
- Form validation without re-render

Syntax
```jsx 
const ref = useRef(initialValue);
```

## 1. Access DOM Element

```jsx 
import React, { useRef } from 'react';

export default function FocusInput() {
  const inputRef = useRef(null);

  const handleFocus = (e) => {
    e.preventDefault();
    inputRef.current.focus(); // DOM access
  };

  return (
    <div>
      <input ref={inputRef} type="text" placeholder="Type here" />
      <button onClick={handleFocus}>Focus Input</button>
    </div>
  );
}
```

## 2. Click Button for Change DOM
```jsx
const Test = () => {
    const inputRef = useRef('');
    const handleRef = () => {
        inputRef.current.innerText = 'You Clicked the Button!'
    } 
  return (
    <> 
        <h1 ref={inputRef}> Welcome Back!</h1>
        <button onClick={handleRef} > Click </button>
    </>
  );
};
```
## ✅ Full Example
```jsx 
import React, { useRef } from 'react';

export default function InputControl() {
  const inputRef = useRef();

  const handleClear = () => {
    inputRef.current.focus();         // Focus the input
    inputRef.current.value = '';      // Clear the input value
    inputRef.current.placeholder = 'Write again...'; // Set new placeholder
    inputRef.current.style.border = '2px solid red'; // Style it
  };

  return (
    <div>
      <input ref={inputRef} defaultValue="Mamun" />
      <button onClick={handleClear}>Clear Input</button>
    </div>
  );
}
```

## 1. Text/Content Elements (div, p, span, etc.)

| Syntax                           | Description                                 |
| -------------------------------- | ------------------------------------------- |
| `ref.current.innerText`          | Get/set visible text content (ignores HTML) |
| `ref.current.textContent`        | Get/set all text (similar to `innerText`)   |
| `ref.current.innerHTML`          | Get/set HTML content inside element         |
| `ref.current.style`              | Apply inline styles                         |
| `ref.current.classList.add()`    | Add CSS class                               |
| `ref.current.classList.remove()` | Remove CSS class                            |
| `ref.current.classList.toggle()` | Toggle CSS class                            |
| `ref.current.getAttribute()`     | Get HTML attribute                          |
| `ref.current.setAttribute()`     | Set HTML attribute                          |
| `ref.current.remove()`           | Remove element from DOM                     |

## 2. Button, Anchor, and Similar Controls

| Syntax                 | Description                            |
| ---------------------- | -------------------------------------- |
| `ref.current.click()`  | Simulate a click                       |
| `ref.current.disabled` | Enable/disable the button              |
| `ref.current.type`     | Button type (`submit`, `button`, etc.) |


##  3. Commonly Used Properties & Methods for input

| Syntax                         | Description                                              |
| ------------------------------ | -------------------------------------------------------- |
| `inputRef.current.focus()`     | Focus the input field                                    |
| `inputRef.current.blur()`      | Remove focus from the input                              |
| `inputRef.current.value`       | Get/set the current input value                          |
| `inputRef.current.placeholder` | Get/set the placeholder text                             |
| `inputRef.current.disabled`    | Enable/disable the input                                 |
| `inputRef.current.readOnly`    | Make input read-only                                     |
| `inputRef.current.style`       | Access CSS styles (like `style.backgroundColor = "red"`) |
| `inputRef.current.classList`   | Add/remove/toggle CSS classes                            |
| `inputRef.current.type`        | Get or set the input type (e.g., "text", "password")     | 

## 4. Form Elements (not <input>)

| Element      | Useful Properties/Methods              |
| ------------ | -------------------------------------- |
| `<textarea>` | `.value`, `.rows`, `.cols`             |
| `<select>`   | `.value`, `.selectedIndex`, `.options` |
| `<form>`     | `.submit()`, `.reset()`, `.elements`   |


<br>
<br>

## Example: 1 Text/Content Elements (div, p, span, etc.)

```jsx
import React, { useRef } from 'react';

export default function RefTextExample() {
  const divRef = useRef();

  const handleAll = () => {
    // 1. innerText — Get or set visible text
    console.log("innerText:", divRef.current.innerText);
    divRef.current.innerText = "Text updated using innerText";

    // 2. textContent — Similar to innerText
    console.log("textContent:", divRef.current.textContent);

    // 3. innerHTML — Set HTML (dangerous if not sanitized)
    divRef.current.innerHTML = "<strong> Bold Text with innerHTML</strong>";

    // 4. style — Apply inline styles
    divRef.current.style.backgroundColor = "lightyellow";
    divRef.current.style.padding = "10px";

    // 5. classList.add() — Add CSS class
    divRef.current.classList.add("highlight");

    // 6. classList.remove() — Remove a class
    divRef.current.classList.remove("remove-this");

    // 7. classList.toggle() — Toggle a class
    divRef.current.classList.toggle("toggled-class");

    // 8. getAttribute() — Get an HTML attribute
    const dataValue = divRef.current.getAttribute("data-id");
    console.log("data-id attribute:", dataValue);

    // 9. setAttribute() — Set an HTML attribute
    divRef.current.setAttribute("data-id", "999");

    // 10. remove() — Remove the element from the DOM
    // divRef.current.remove(); // uncomment to test
  };

  return (
    <div>
      <div ref={divRef}  className="remove-this"  data-id="123" style={{ border: "1px solid gray" }}   >
         Initial div content
      </div>

      <button onClick={handleAll}> Run All DOM Ref Actions</button>
    </div>
  );
}
```
 

## Example: 2 Button, Anchor, and Similar Controls: Full Working Example

```jsx 
import React, { useRef } from 'react';

export default function ButtonRefExample() {
  const buttonRef = useRef();
  const anchorRef = useRef();

  const handleSimulateClick = () => {
    // 1. click() – Simulate a button click
    buttonRef.current.click();
  };

  const handleDisableToggle = () => {
    // 2. disabled – Toggle disabled/enabled state
    buttonRef.current.disabled = !buttonRef.current.disabled;
  };

  const showButtonType = () => {
    // 3. type – Get button type
    console.log(" Button type:", buttonRef.current.type);
  };

  const handleButtonClick = () => {
    alert(" Real Button Clicked!");
  };

  const handleAnchorClick = () => {
    alert(" Anchor clicked (but prevented default navigation)");
  };

  return (
    <div style={{ padding: "20px" }}>
      {/* The actual button with ref */}
      <button  ref={buttonRef}   type="submit"  onClick={handleButtonClick}  style={{ marginRight: "10px" }}  >
         Submit Button
      </button>

      {/* Simulate click */}
      <button onClick={handleSimulateClick}> Simulate Click</button>

      {/* Toggle disabled */}
      <button onClick={handleDisableToggle}> Toggle Disabled</button>

      {/* Check type */}
      <button onClick={showButtonType}> Check Button Type</button>

      <br /><br />

      {/* Anchor element example */}
      <a ref={anchorRef}  href="https://example.com"
        onClick={(e) => {
          e.preventDefault(); // prevent navigation
          handleAnchorClick();
        }}> Link (Click Me)
      </a>
    </div>
  );
}
```
 

## Example: 3 with input and All Common Methods
```jsx 
import React, { useRef } from 'react';

export default function InputRefExample() {
  const inputRef = useRef();

  const handleFocus = () => {
    inputRef.current.focus(); //  Focus the input
  };

  const handleBlur = () => {
    inputRef.current.blur(); //  Remove focus
  };

  const handleSetValue = () => {
    inputRef.current.value = "AN Mamun"; //  Set value
  };

  const handleGetValue = () => {
    alert("Value: " + inputRef.current.value); //  Get value
  };

  const handlePlaceholder = () => {
    inputRef.current.placeholder = "Enter your name..."; //  Set placeholder
  };

  const handleDisable = () => {
    inputRef.current.disabled = !inputRef.current.disabled; //  Toggle disable
  };

  const handleReadonly = () => {
    inputRef.current.readOnly = !inputRef.current.readOnly; //  Toggle readOnly
  };

  const handleStyle = () => {
    inputRef.current.style.backgroundColor = "lightblue"; //  Change background color
    inputRef.current.style.color = "darkblue";
  };

  const handleClassList = () => {
    inputRef.current.classList.toggle("highlight"); //  Toggle class
  };

  const handleChangeType = () => {
    inputRef.current.type = inputRef.current.type === "password" ? "text" : "password"; // Toggle type
  };

  return (
    <div style={{ padding: "20px" }}>
      <h3> Input Ref Methods Demo</h3>

      <input  ref={inputRef}  type="text"   placeholder="Type here"  defaultValue=""  className="input"
        style={{ padding: "10px", border: "1px solid #ccc" }}
      />

      <br /><br />

      <button onClick={handleFocus}> Focus</button>
      <button onClick={handleBlur}> Blur</button>
      <button onClick={handleSetValue}> Set Value</button>
      <button onClick={handleGetValue}> Get Value</button>
      <button onClick={handlePlaceholder}> Set Placeholder</button>
      <button onClick={handleDisable}> Toggle Disabled</button>
      <button onClick={handleReadonly}> Toggle ReadOnly</button>
      <button onClick={handleStyle}> Change Style</button>
      <button onClick={handleClassList}> Toggle Class</button>
      <button onClick={handleChangeType}> Toggle Type</button>

      <style>{` .highlight {
          border: 2px dashed red;
          background-color: #ffeeee;
        }  `}</style>
    </div>
  );
}
```





## Example: 4 Form Elements (not <input>)
```jsx 
import React, { useRef } from 'react';

export default function FormElementsExample() {
  const textareaRef = useRef();
  const selectRef = useRef();
  const formRef = useRef();

  const handleSubmit = (e) => {
    e.preventDefault();

    // Access textarea
    const textValue = textareaRef.current.value;
    const rows = textareaRef.current.rows;
    const cols = textareaRef.current.cols;

    // Access select
    const selectedValue = selectRef.current.value;
    const selectedIndex = selectRef.current.selectedIndex;
    const allOptions = Array.from(selectRef.current.options).map(opt => opt.value);

    console.log(" Textarea value:", textValue);
    console.log(" Rows:", rows, "Cols:", cols);
    console.log(" Selected value:", selectedValue);
    console.log(" Selected index:", selectedIndex);
    console.log(" All options:", allOptions);
  };

  const handleFormSubmitDirectly = () => {
    // Submits the form programmatically
    formRef.current.submit();
  };

  const handleFormReset = () => {
    // Resets the form
    formRef.current.reset();
  };

  return (
    <form ref={formRef} onSubmit={handleSubmit} style={{ padding: "20px" }}>
      <h3> Form Element Demo</h3>

      <label> Your Message:
        <br />
        <textarea ref={textareaRef} rows="4" cols="50" defaultValue="Type here..." />
      </label>
      <br /><br />

      <label> Choose a Topic:
        <br />
        <select ref={selectRef} defaultValue="react">
          <option value="html">HTML</option>
          <option value="css">CSS</option>
          <option value="javascript">JavaScript</option>
          <option value="react">React</option>
        </select>
      </label>
      <br /><br />

      <button type="submit"> Submit</button>
      <button type="button" onClick={handleFormSubmitDirectly}>  Direct Submit</button>
      <button type="button" onClick={handleFormReset}> Reset</button>
    </form>
  );
}
```
  
<br>
<br>
<br>
<br>
<br>
<br>







---


## 2. Store a Mutable Value
```jsx 
function Counter() {
  const countRef = useRef(0);

  const increment = () => {
    countRef.current += 1;
    console.log("Clicked:", countRef.current);
  };

  return <button onClick={increment}>Click me</button>;
}
```

✅ No re-render happens when countRef.current changes.

## 3. Store Previous State

```jsx 
import { useState, useEffect, useRef } from 'react';

function ShowPreviousValue() {
  const [count, setCount] = useState(0);
  const prevCount = useRef();

  useEffect(() => {
    prevCount.current = count;
  }, [count]);

  return (
    <div>
      <p>Now: {count}</p>
      <p>Before: {prevCount.current}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```
## 4. With setTimeout / setInterval

```jsx 
function Timer() {
  const timerRef = useRef();

  const start = () => {
    timerRef.current = setInterval(() => {
      console.log("Tick");
    }, 1000);
  };

  const stop = () => {
    clearInterval(timerRef.current);
  };

  return (
    <>
      <button onClick={start}>Start</button>
      <button onClick={stop}>Stop</button>
    </>
  );
}
```
 