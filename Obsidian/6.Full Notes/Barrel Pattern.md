2026-03-14 23:13

Status: #Done 

Tag: [[Design Pattern]]  

# Barrel Pattern

### what is Barrel pattern?
- A barrel pattern is a file organizing pattern that allows export of all modules under a single file inside a directory usually the file is named index.js or index.ts called barrel file.
### How to use it
- Lets say you have a project with module for shared components
```
/components  
|-- Button.js  
|-- Input.js  
|-- Checkbox.js
```
- In above structure you can export each component separately inside each file but when you import it will look like this
```
import Button from ./components/button
import Input from ./components/input
import Checkbox form ./components/checkbox
```
- But in larger project this make a cluster of large import 
- Lets make a barrel file index.js and reimport everything inside now
```
/components  
|-- Button.js  
|-- Input.js  
|-- Checkbox.js
|-- index.js
```
- Content of index.js look like this
```
export { default as Button } from './Button';  
export { default as Input } from './Input';  
export { default as Checkbox } from './Checkbox';
```
- Now you can import like below which make it cleaner and easy to manage
```
import { Button, Input, Checkbox } from './components';
```

### When to use it
- The barrel pattern make the code readability and manageability easy but in smaller project like under a directory one file we create a barrel file(index.js), we end up creating a engineering overhead.
- The main purpose is to make things easy, make sure to use it in larger file to make a maintainable , readable code.
- You can use this barrel file as a central management under a directory to keep things organised.
## Reference
[Medium blog post for barrel pattern](https://medium.com/@denisultanoglu/using-barrel-pattern-in-react-typescript-projects-e8e855730182)
