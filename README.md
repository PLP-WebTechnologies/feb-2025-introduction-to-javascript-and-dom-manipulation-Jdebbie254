# Introduction to JavaScript and DOM Manipulation

## Objectives

Write basic JavaScript functions.
Manipulate the DOM dynamically.
Respond to user interactions.

## Instructions

- Create a script.js file and link it to a HTML.
- Structure the document using DOCTYPE, html, head, and body.

>[!NOTE]
>  - Write JavaScript that:
>  - Changes text content dynamically.
>  - Modifies CSS styles via JavaScript.
>  - Adds or removes an element when a button is clicked.


# Tasks
- Create a well-structured HTML5 document.
- Use at least 5 different HTML elements.
- Ensure semantic correctness.

Happy Coding! 💻✨

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DOM Manipulation Demo</title>
    <link rel="stylesheet" href="styles.css">
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f5f5;
        }
        section {
            background-color: white;
            padding: 20px;
            margin-bottom: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }
        button {
            background-color: #4CAF50;
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 4px;
            cursor: pointer;
            margin: 5px;
            transition: background-color 0.3s;
        }
        button:hover {
            background-color: #45a049;
        }
        .highlight {
            background-color: yellow;
            font-weight: bold;
            padding: 2px 5px;
        }
        #element-container {
            border: 2px dashed #ccc;
            padding: 15px;
            margin: 15px 0;
            min-height: 50px;
        }
        .new-element {
            background-color: #e7f3fe;
            border-left: 4px solid #2196F3;
            padding: 10px;
            margin: 5px 0;
        }
    </style>
</head>
<body>
    <header>
        <h1>JavaScript DOM Manipulation</h1>
        <p>Demonstrating dynamic content changes and user interactions</p>
    </header>

    <main>
        <!-- Section 1: Changing Text Content -->
        <section id="text-section">
            <h2>1. Change Text Content</h2>
            <p id="changeable-text">This text will change when you click the button below.</p>
            <button id="change-text-btn">Change Text</button>
            <button id="reset-text-btn">Reset Text</button>
        </section>

        <!-- Section 2: Modifying CSS Styles -->
        <section id="style-section">
            <h2>2. Modify CSS Styles</h2>
            <p id="styleable-text">This text will change style when you click the buttons.</p>
            <button id="highlight-btn">Highlight Text</button>
            <button id="bigger-btn">Increase Font Size</button>
            <button id="color-btn">Change Color</button>
        </section>

        <!-- Section 3: Adding/Removing Elements -->
        <section id="element-section">
            <h2>3. Add/Remove Elements</h2>
            <div id="element-container">
                <p>Existing element (click to remove)</p>
            </div>
            <button id="add-element-btn">Add New Element</button>
            <button id="remove-element-btn">Remove Last Element</button>
        </section>

        <!-- Section 4: Event Listeners -->
        <section id="event-section">
            <h2>4. Interactive Elements</h2>
            <div class="color-box" id="color-box" style="width: 100px; height: 100px; background-color: #ddd;"></div>
            <p>Mouse over the box to change its color. Click to reset.</p>
        </section>

        <!-- Section 5: Form Interaction -->
        <section id="form-section">
            <h2>5. Form Interaction</h2>
            <form id="demo-form">
                <label for="user-input">Enter some text:</label>
                <input type="text" id="user-input" placeholder="Type something...">
                <button type="submit">Submit</button>
            </form>
            <div id="form-output"></div>
        </section>
    </main>

    <footer>
        <p>DOM Manipulation Demo &copy; 2023</p>
    </footer>

    <script src="script.js"></script>
</body>
</html>

// Wait for the DOM to be fully loaded before executing JavaScript
document.addEventListener('DOMContentLoaded', function() {
    // 1. Changing Text Content
    const changeableText = document.getElementById('changeable-text');
    const originalText = changeableText.textContent;
    
    document.getElementById('change-text-btn').addEventListener('click', function() {
        changeableText.textContent = "The text has been changed dynamically using JavaScript!";
    });
    
    document.getElementById('reset-text-btn').addEventListener('click', function() {
        changeableText.textContent = originalText;
    });

    // 2. Modifying CSS Styles
    const styleableText = document.getElementById('styleable-text');
    
    document.getElementById('highlight-btn').addEventListener('click', function() {
        styleableText.classList.toggle('highlight');
    });
    
    document.getElementById('bigger-btn').addEventListener('click', function() {
        const currentSize = window.getComputedStyle(styleableText).fontSize;
        const newSize = parseInt(currentSize) + 2;
        styleableText.style.fontSize = newSize + 'px';
    });
    
    document.getElementById('color-btn').addEventListener('click', function() {
        const colors = ['red', 'blue', 'green', 'purple', 'orange'];
        const randomColor = colors[Math.floor(Math.random() * colors.length)];
        styleableText.style.color = randomColor;
    });

    // 3. Adding/Removing Elements
    const elementContainer = document.getElementById('element-container');
    let elementCounter = 1;
    
    document.getElementById('add-element-btn').addEventListener('click', function() {
        const newElement = document.createElement('div');
        newElement.className = 'new-element';
        newElement.textContent = `New Element #${elementCounter++} (click to remove)`;
        
        // Add click event to remove the element when clicked
        newElement.addEventListener('click', function() {
            elementContainer.removeChild(newElement);
        });
        
        elementContainer.appendChild(newElement);
    });
    
    document.getElementById('remove-element-btn').addEventListener('click', function() {
        if (elementContainer.lastChild) {
            elementContainer.removeChild(elementContainer.lastChild);
        }
    });
    
    // Add click to remove for existing elements
    const existingElements = elementContainer.querySelectorAll('p');
    existingElements.forEach(element => {
        element.addEventListener('click', function() {
            elementContainer.removeChild(element);
        });
    });

    // 4. Event Listeners with Mouse Events
    const colorBox = document.getElementById('color-box');
    const originalColor = colorBox.style.backgroundColor;
    
    colorBox.addEventListener('mouseover', function() {
        const colors = ['#ff9999', '#99ff99', '#9999ff', '#ffff99', '#ff99ff'];
        const randomColor = colors[Math.floor(Math.random() * colors.length)];
        colorBox.style.backgroundColor = randomColor;
    });
    
    colorBox.addEventListener('click', function() {
        colorBox.style.backgroundColor = originalColor;
    });

    // 5. Form Interaction
    const demoForm = document.getElementById('demo-form');
    const formOutput = document.getElementById('form-output');
    
    demoForm.addEventListener('submit', function(event) {
        event.preventDefault(); // Prevent form submission
        
        const userInput = document.getElementById('user-input').value;
        
        if (userInput.trim() !== '') {
            formOutput.textContent = `You entered: "${userInput}"`;
            formOutput.style.color = 'green';
            
            // Clear the input field
            document.getElementById('user-input').value = '';
        } else {
            formOutput.textContent = 'Please enter some text!';
            formOutput.style.color = 'red';
        }
    });
});
