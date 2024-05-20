RaceSimulator
=============

RaceSimulator is a fun and interactive race emulator built using HTML, CSS, and JavaScript. This project features various vehicles racing across the screen, a toggle switch to start and stop the race, background flashes for added excitement, and a checkered grandstand background.

Purpose
-------
The purpose of this project is to learn and practice JavaScript and animations, exploring how to create interactive and dynamic web experiences.

Features
--------

-   Various vehicles with different speeds.
-   A start/stop switch to control the race.
-   Background flashes when the race starts.
-   Checkered grandstand background for a realistic race day feel.

Getting Started
---------------

### Prerequisites

-   Web browser (Chrome, Firefox, Safari, etc.)

### Installation

1.  Clone the repository:

    ```sh
    `git clone https://github.com/yourusername/RaceSimulator.git`
    ```
2.  Navigate to the project directory:

    ```sh
    `cd RaceSimulator`
    ```

3.  Open `index.html` in your web browser to view the race simulator.

## Preview
-----
You can see a live preview of the application [here](https://darioernesto-roca.github.io/RaceSimulator/)

Usage
-----

### Classes and Objects

The `Vehicle` class is used to create vehicle objects with an emoji and a speed property. The `addToPage` method adds the vehicle to the DOM and sets its animation speed.

Example:

JavaScript Code

```javascript
class Vehicle {
    constructor (emoji, speed) {
        this.emoji = emoji;
        this.speed = speed;
    }
    addToPage() {
        const race = document.querySelector(".race");
        const path = document.createElement("div");
        path.textContent = this.emoji;
        path.classList.add("vehicle");
        path.style.animationDuration = `${10 / this.speed}s`;
        race.appendChild(path);
    }
}
```

### Animations

-   The `@keyframes moveRightToLeft` animation moves the vehicles from right to left across the screen.
-   The `@keyframes flash` animation creates the background flash effect when the race starts.

Example:

CSS Code

```css

@keyframes moveRightToLeft {
    from {
        transform: translateX(100%);
    }
    to {
        transform: translateX(-100%);
    }
}

@keyframes flash {
    0%, 100% {
        background-color: white;
    }
    50% {
        background-color: yellow;
    }
}

```

### DOM Scripting and Event Listeners

-   Vehicles are added to the DOM by creating `div` elements with the `vehicle` class and appending them to the `race` container.
-   An event listener on the toggle switch starts or stops the race, adding or removing vehicles from the DOM and triggering the background flash animation.

Example:

JavaScript Code

```javascript

const vehicles = [
    new Vehicle("🚴‍♂️", 1),
    new Vehicle("🏍️", 3),
    new Vehicle("🏎️", 4),
    new Vehicle("🚚", 2)
];

const button = document.getElementById('switch');
let raceStarted = false;

button.addEventListener('click', () => {
    if (!raceStarted) {
        vehicles.forEach(vehicle => vehicle.addToPage());
        startBackgroundFlash();
    } else {
        stopRace();
    }
    raceStarted = !raceStarted;
});

function startBackgroundFlash() {
    document.body.style.animation = 'flash 0.5s alternate 5';
}

function stopRace() {
    document.querySelectorAll('.vehicle').forEach(vehicle => vehicle.remove());
    document.body.style.animation = '';
}

```