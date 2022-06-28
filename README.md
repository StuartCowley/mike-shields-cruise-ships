# Cruise Ship
<sub><sup>
Author: Michael Shields
</sup></sub>
---

This repository is an assignment from the OOP track of the Manchester Codes Syllabus. The assignment is an opportunity to explore and practice:

- The Git/GitHub workflow
- Implementing Code in reference to User Stories
- "Mocks and Spies" in the [Jest]("https://jestjs.io/") TDD framework
- Object Oriented Programming using class syntax & Prototypical Inheritance
- Higher Order Functions & Built in Methods
- ES6 Modules 
- Dependency Injection & Inversion 
- Conditional logic
- Implementing Guard Clauses & Throwing exceptions
- Code Refactoring

---

## Project Brief

Over the next couple of weeks, we are going to cover further aspects of Object-oriented Programming - namely how we pass objects into one another and test for this, how we decide what methods and properties our objects should have, how we isolate objects in tests, and how we test behaviour that's outside of our control.

This week you are going to be building and working with many objects that allow a cruise ship to operate. Hopefully we don't hit any icebergs on the way 👀.

---
## Cloning and Setup

1. Clone the repository: 
   - via http: 
   ```bash
   git clone https://github.com/mike-shields-dev/cruise-ships.git
   ```
   - via ssh: 
   ```bash
   git clone git@github.com:mike-shields-dev/cruise-ships.git
   ```
2. Install dependencies: 
     ```bash
     cd cruise-ships && npm install
     ```
3. Testing:
  
    This repository utilises the [Jest]("https://jestjs.io/") JavaScript testing framework. 

    Test file is located in the `__tests__` directory. 

    To run the test suite once: 
    ```bash
    npm test
    ```
    To automatically run the tests as changes are made to the code: 
    ```bash 
    npm run test:watch
    ```

## Documentation

When creating **Ship** instances, an **Itinerary** instance must be provided. The **Itinerary** instance in turn must be provided with an **array** of **Port** instances.

Throughout the life cycle of the **ship**, it will proceed to "visit" each **port** in the provided **itinerary**, in turn, until all **ports** have been visited. 

---

#### Port
##### Creating a Port instance
```js
const port = new Port("Amsterdam");
port.name // "Amsterdam"
```
##### Properties:
- `name`: The name of the port
- `ships`: An array of ships currently docked at this port
##### Methods: 
*Note: It is solely the responsibility of a `ship` to invoke the `port` methods below* 

  - `addShip`: Adds the given `ship` to   `ships` array:

  ```js
  port.addShip(ship)
  ports.ships // [ship]
  ```
  
  - `removeShip`: Removes the given `ship` from `ships` array:
  
  ```js
  port.ships // [ship]
  port.removeShip(ship)
  port.ships // []
  ```
---

#### Itinerary

##### Creating an Itinerary instance 

```js
const ports = [port1, port2, port3]
const itinerary = new Itinerary(ports);
itinerary.ports // [port1, port2, port3]
```
---

#### Ship:
Creating a Ship instance

```js
const ship = new Ship(itinerary)
```

##### Properties:
- `itinerary`: The provided `itinerary` of ports
- `currentPort`: The `port` at which the `ship` is currently docked
- `previousPort`: The `port` at which the `ship` was previously docked
  
##### Methods: 
- `setSail`:
  - Removes `ship` from the `ships` array of the current `port`
  - Sets `previousPort` to be the value of `currentPort`
  - Sets `currentPort`  to equal `null`
  ```js
  const ship = new Ship(itinerary)

  ship.previousPort // null
  ship.currentPort // itinerary[0]
  ship.currentPort.ports // [ship]

  ship.setSail()

  ship.previousPort // itinerary[0]
  ship.previousPort.ports // []
  ship.currentPort // null
  ```

- `dock`: 
  - Adds `ship` to the `ports` array of the next `port` in the `itinerary`
  - Sets `currentPort` to be the next `port` in the  `itinerary`

  ```js
  // ...continues from setSail code example above
  ship.dock()

  ship.currentPort // ship.itinerary[1]
  ship.currentPort.ports // [ship]
  ```
