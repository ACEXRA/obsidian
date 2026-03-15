2026-03-15 22:07

Status: #In-Progress

Tag:[[Frontend-Techniques]] 

# Debounce
- Debouncing is a technique of delaying a function call until a specific time has passed since event is triggered.
- For example, their is a search API, which is tied to search text box on each keystroke type of user the API gets called. An average user type 5-6 character a sec, this can result in multiple API call in a second overloading the server.
- Debouncing only call the function after user stopped typing for some time (a delay since the last event triggered).
## How to implement debouncing:
### Use Custom Hook(useDebounce) :
- The name useDebounce can be whatever, Its just a func name widely used.
```
import { useState, useEffect } from 'react';

function useDebounce(value, delay) {
  const [debouncedValue, setDebouncedValue] = useState(value);

  useEffect(() => {
    // Set a timer to update the debounced value after the delay
    const handler = setTimeout(() => {
      setDebouncedValue(value);
    }, delay);

    // Cleanup: cancel the timer if value or delay changes (user is still typing)
    return () => {
      clearTimeout(handler);
    };
  }, [value, delay]);

  return debouncedValue;
}
```

- Usage Example
```
// Usage Example
function SearchComponent() {
  const [searchTerm, setSearchTerm] = useState('');
  const debouncedSearch = useDebounce(searchTerm, 500);

  useEffect(() => {
    if (debouncedSearch) {
      console.log('API call with:', debouncedSearch);
    }
  }, [debouncedSearch]);

  return (
    <input 
      type="text" 
      value={searchTerm} 
      onChange={(e) => setSearchTerm(e.target.value)} 
    />
  );
}
```

# Throttling
- Throttling is a technique which ensures that a function is called once every specific interval.
- For Example : You want to run a function on a event based on scroll for user , but if you call the function by scroll event handler it would fire the function call hundreds of time in a second which cause performance issue.
## How to Implement Throttling
### Use Custom Hooks:
- The common name used is useThrottle.
```
import { useState, useEffect, useRef } from 'react';

function useThrottle(value, delay = 500) {
  const [throttledValue, setThrottledValue] = useState(value);
  const lastExecuted = useRef(Date.now());

  useEffect(() => {
    const handler = setTimeout(() => {
      const now = Date.now();
      const timeElapsed = now - lastExecuted.current;

      if (timeElapsed >= delay) {
        setThrottledValue(value);
        lastExecuted.current = now;
      }
    }, delay - (Date.now() - lastExecuted.current));

    return () => clearTimeout(handler);
  }, [value, delay]);

  return throttledValue;
}

```

- Usage Example
```
import { useMemo, useEffect } from 'react';
import throttle from 'lodash.throttle';

function ScrollComponent() {
  const handleScroll = () => {
    console.log("Scroll position:", window.scrollY);
  };

  // useMemo ensures the same throttled function instance is used
  const throttledScroll = useMemo(
    () => throttle(handleScroll, 1000),
    []
  );

  useEffect(() => {
    window.addEventListener('scroll', throttledScroll);
    // Cleanup to prevent memory leaks and pending executions
    return () => {
      window.removeEventListener('scroll', throttledScroll);
      throttledScroll.cancel();
    };
  }, [throttledScroll]);

  return <div style={{ height: '200vh' }}>Scroll to see throttling in action</div>;
}

```

# Key Differences Between Debouncing and Throttling

| Feature       | Debouncing                                                        | Throttling                                                       |
| ------------- | ----------------------------------------------------------------- | ---------------------------------------------------------------- |
| Definiton     | Executes a function after a specific delay since last event       | Executes the function once in a specific interval                |
| Best Use case | Search input, resize events, validation checks                    | scroll event, window resize, limit button clicks                 |
| When it runs  | Only after user stops triggering the event after a specific delay | Repeatedly, but no more than once within the set interval delay. |
| Example       | Fires search API 500ms after user stop typing in search input     | Fires every 200ms during scrolling.                              |
## Note
**Loadash package in react has both debounce and throttle in built**

## Reference

[Debouncing VS Throttling](https://medium.com/@ignatovich.dm/debouncing-and-throttling-in-react-whats-the-difference-and-how-to-implement-them-0a500b649235) 