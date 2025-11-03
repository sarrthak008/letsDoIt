# JavaScript Event Loop, Microtasks vs Macrotasks, Type Coercion, useMemo vs useCallback & CORS

------------------------------------------------------------------------

## ✅ JavaScript Event Loop (Easy Explanation)

JavaScript is a **single-threaded language**, meaning it executes one
command at a time.\
But still it handles **async functions** like:

-   Timers (`setTimeout`)
-   Promises
-   API calls
-   Event listeners

To manage all of this without blocking code, JS uses the **Event Loop**.

### 🧠 How It Works

-   **Call Stack** runs main code (synchronous)
-   **Queues** store async tasks until ready
-   **Event Loop** keeps checking:
    1)  If call stack is empty\
    2)  Then processes pending tasks

### Queue Priority

  ------------------------------------------------------------------------
  Queue           Tasks           Examples             Priority
  --------------- --------------- -------------------- -------------------
  **Microtask     Very small,     `Promise.then()`,    ✅ Runs first
  Queue**         high-priority   `async/await`,       
                  async tasks     `queueMicrotask()`   

  **Macrotask     Bigger async    `setTimeout`,        ▶️ Runs after
  Queue**         tasks           `setInterval`, DOM   microtasks
                                  events               
  ------------------------------------------------------------------------

**Flow:**\
Current code → Microtasks → Macrotasks → repeat

------------------------------------------------------------------------

## ✅ Microtask vs Macrotask Summary

  -----------------------------------------------------------------------
  Microtask                         Macrotask
  --------------------------------- -------------------------------------
  High Priority                     Normal Priority

  Runs immediately after current    Runs after microtasks
  code                              

  Promises, `queueMicrotask()`      `setTimeout`, `setInterval`, DOM
                                    events

  Used for critical fast async work Used for timed & browser events
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## ✅ JavaScript Type Coercion Examples (== vs ===)

  Expression         Result     Reason
  ------------------ ---------- ------------------------------
  `[] == 0`          ✅ true    `[] → "" → 0`
  `[''] == 0`        ✅ true    `[''] → "" → 0`
  `[1] == 1`         ✅ true    `[1] → "1" → 1`
  `{ } == { }`       ❌ false   objects compare by reference
  `'true' == true`   ❌ false   `"true" → NaN`, `true → 1`
  `null == 0`        ❌ false   null only equals undefined
  `undefined == 0`   ❌ false   undefined only equals null
  `[] == false`      ✅ true    `[] → "" → 0`, `false → 0`
  `" " == 0`         ✅ true    whitespace → `0`
  `false == "0"`     ✅ true    `"0" → 0`, `false → 0`

**Rules to remember** - `[] → "" → 0` - `" " → 0` - `true → 1`,
`false → 0` - `null == undefined` only - Objects compare by reference

------------------------------------------------------------------------

## ✅ useMemo vs useCallback (React)

  -----------------------------------------------------------------------------
  Hook              Purpose         Returns           When to Use
  ----------------- --------------- ----------------- -------------------------
  **useMemo**       Memoizes        Cached value      Expensive computation
                    **value**                         

  **useCallback**   Memoizes        Same function     Prevent re-renders in
                    **function**    reference         children
  -----------------------------------------------------------------------------

### 🧠 Example useMemo

``` js
const expensiveValue = useMemo(() => calc(data), [data]);
```

### 🧠 Example useCallback

``` js
const handleClick = useCallback(() => setCount(c => c+1), []);
```

### Easy Real-Life Example

  Hook          Real World Meaning
  ------------- ------------------------------------------------------
  useMemo       Remember bill total unless items change
  useCallback   Remember cashier instructions (don't rewrite always)

------------------------------------------------------------------------

## ✅ CORS (Cross-Origin Resource Sharing)

CORS is a **browser security feature** that controls API access across
different domains.

### 🎯 Why CORS Exists?

To protect users from malicious websites making requests on their
behalf.

### 🔥 Same-Origin Policy

Two URLs must match:

  Part       Example
  ---------- -------------
  Protocol   https://
  Domain     example.com
  Port       :3000

If any part differs → CORS check triggers.

### Example Dev Setup

  Frontend                  Backend
  ------------------------- -------------------------
  `http://localhost:5173`   `http://localhost:3000`

Browser blocks request unless server sends:

``` http
Access-Control-Allow-Origin: http://localhost:5173
Access-Control-Allow-Methods: GET, POST
Access-Control-Allow-Headers: Content-Type
Access-Control-Allow-Credentials: true
```

### Preflight Request

Browser sends:

    OPTIONS /api/login

To ask server if cross-origin request is allowed.

### Behind CORS

  Concept               Role
  --------------------- -----------------------------------
  Same-Origin Policy    Blocks unsafe cross-origin calls
  CORS                  Official way to allow safe access
  HTTP headers          Define access rules
  Preflight (OPTIONS)   Security handshake

------------------------------------------------------------------------

## ✅ Sessions & Cookies (Short Intro)

  Concept       What it does
  ------------- -------------------------------------------
  Cookie        Stores data in browser
  Session       Stores user data on server
  Token (JWT)   Stores identity in client (frontend apps)

------------------------------------------------------------------------

## 🎉 Summary

-   Event loop handles async code in order
-   Microtasks run before macrotasks
-   Loose equality (`==`) does type conversion --- be careful
-   `useMemo` for values, `useCallback` for functions
-   CORS protects browsers & APIs from cross-origin attacks

------------------------------------------------------------------------