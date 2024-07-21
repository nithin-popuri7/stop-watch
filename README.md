# React + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react/README.md) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh


### HelloWorld.jsx:
```js
import React, { useState, useEffect } from 'react';
import './HelloWorld.css';

const HelloWorld = () => {
    const [milliseconds, setMilliseconds] = useState(0);
    const [isRunning, setIsRunning] = useState(false);
    const [intervalId, setIntervalId] = useState(null);

    useEffect(() => {
        if (isRunning) {
            const id = setInterval(() => {
                setMilliseconds(prevMilliseconds => prevMilliseconds + 10);
            }, 10);
            setIntervalId(id);
        } else if (intervalId) {
            clearInterval(intervalId);
            setIntervalId(null);
        }

        return () => {
            if (intervalId) {
                clearInterval(intervalId);
            }
        };
    }, [isRunning]);

    const formatTime = (totalMilliseconds) => {
        const totalSeconds = Math.floor(totalMilliseconds / 1000);
        const hours = Math.floor(totalSeconds / 3600);
        const minutes = Math.floor((totalSeconds % 3600) / 60);
        const seconds = totalSeconds % 60;
        const millis = totalMilliseconds % 1000;
        return `${String(hours).padStart(2, '0')}:${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}:${String(millis).padStart(2, '0')}`;
    };

    return (
        <div className="container">
            <div className="timer">
                <h1 className="header">Hello There....!</h1>
                <h3 className="header">Timer</h3>
                <p className="time">{formatTime(milliseconds)}</p>
                <div className="buttonContainer">
                    <button className="button" onClick={() => setIsRunning(true)}>Start</button>
                    <button className="button" onClick={() => setIsRunning(false)}>Pause</button>
                    <button className="button" onClick={() => { setIsRunning(false); setMilliseconds(0); }}>Reset</button>
                </div>
            </div>
        </div>
    );
};

export default HelloWorld;

```
### HelloWorld.css:

```css
/* Set the background image for the entire page */
body {
    margin: 0;
    padding: 0;
    height: 100vh;
    background-image: url('/src/img.jpg'); /* Replace with your background image path */
    background-size: cover;
    background-position: center;
}

/* Styles for the main container */
.container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

/* Styles for the timer box */
.timer {
    position: relative;
    text-align: center;
    padding: 20px;
    border-radius: 10px;
    background-color: #fff;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

/* Header styles */
.header {
    color: #333;
    margin-bottom: 20px;
}

/* Timer text styles */
.time {
    color: #666;
    font-size: 24px;
    margin-bottom: 20px;
}

/* Button container styles */
.buttonContainer {
    display: flex;
    justify-content: center;
}

/* Button styles */
.button {
    margin: 0 10px;
    padding: 5px 10px;
    font-size: 16px;
    cursor: pointer;
    background-color: #050e0d;
    color: #fff;
    border: none;
    border-radius: 5px;
    transition: background-color 0.3s;
}

.button:hover {
    background-color: #7e7e7e;
}

/* Overlay image styles */
.overlay-image {
    position: absolute;
    bottom: 0;
    right: 0;
    width: 50px; /* Adjust size as needed */
    height: 50px; /* Adjust size as needed */
}

```

### Output:

![image](https://github.com/user-attachments/assets/b0750d25-05fa-48dd-af9d-b1bf896afd76)
