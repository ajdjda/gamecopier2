#bloxflip 
free predictor
copy this!
and paste it in tampermonkey!


// ==UserScript==

// @name         Black ESP V2

// @namespace    http://tampermonkey.net/

// @version      2.0

// @description  Made by BlackSalamalec !

// @author       BlackSalamalec i'm the real thug

// @match        https://bloxflip.com/*

// @connect      *

// @grant        GM_setValue

// @grant        GM_getValue

// @grant        none

// @icon         https://cdn.discordapp.com/attachments/1180514537284325427/1181059281462771813/static.png

// ==/UserScript==

(function() {

    'use strict';

      function _0x4afd1a() {

    alert("Logged in Black ESP");

  }

    let autoMinesActive = false; // Variable to track if Auto Mines is active

    let isDragging = false;
    let offsetX, offsetY;
    // Keybinding variables

    let bombminesKey = 'b';

    let minesKey = 'm';

    function createGUI() {

const guiHTML = `

var link = document.createElement('link');
link.rel = 'stylesheet';
link.href = 'https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700;800;900&display=swap';
document.head.appendChild(link);

<div id="bloxflipESP" style="position: fixed; top: 50%; left: 50%; transform: translate(-50%, -50%); background-color: #0e111f; padding: 20px; z-index: 999; color: #fff; width: 400px; height: 600px; border-radius: 20px; cursor: move; font-size: 16px; box-shadow: -4px 0 20px 2px rgba(212, 89, 255, 0.9), 0-4px 20px 2px rgba(212, 89, 255, 0.9), 4px 0 20px 2px rgba(212, 89, 255, 0.9));">
    <div style="display: flex;">
        <div style="flex: 1;">
            <h2 class="glow" style="margin-bottom: 7px; text-shadow: 0 0 10px #fff; text-align: center; font-family: 'Poppins', sans-serif;">Black ESP V2 </h2>

            <button class="predictButton glow" id="minesButton">Mines</button>

            <div id="mineAmountInput" style="text-align: center; margin-top: 10px;">
              <label for="mineAmount">Mine Amount:</label>
              <input type="number" id="mineAmount" value="3" style="width: 100px; margin-left: 5px; background-color: #1a1f40; color: #fff; border: 1px solid #0e121e; border-radius: 5px; padding: 5px; font-family: 'Poppins', sans-serif;">
              </div>

            <button class="predictButton glow" id="autoMinesButton">Auto Mines</button>

            <button class="unriggerButton glow" id="unriggerButton">Unrigger</button>

            <button class="slideButton glow" id="slideButton">Slide</button>

            <button class="crashButton glow" id="crashButton">Crash</button>

            <div style="text-align: center; margin-top: 20px;">
                <label for="borderColorInput" style="color: #fff; display: block; margin-bottom: 5px;">Border Color:</label>
                <input type="color" id="borderColorInput" style="background-color: #1a1f40; color: #fff; border: none; border-radius: 5px; display: block; margin: 0 auto;">

                <span id="crashPointText" style="display: block; margin-top: 10px; text-align: center; font-family: 'Poppins', sans-serif;"></span>
                <span id="estimateText" style="display: block; margin-top: 10px; text-align: center; font-family: 'Poppins', sans-serif;"></span>
                <hr style="margin-top: 10px; border: none; height: 3px; background-image: linear-gradient(to right, #ff6f69, #ff9f43, #ffcf33, #b8d433, #6ec6ff, #46a0ff, #4a86e8);">

                <span id="colorText" style="display: block; margin-top: 10px; text-align: center; font-family: 'Poppins', sans-serif;"></span>
                <button class="toggleChatButton" id="toggleChatButton">Hide Chat</button>

            </div>
        </div>
    </div>
</div>
`;

const styleCSS = `
.circle-button {
    border-radius: 50%;
    width: 30px;
    height: 30px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #000;
    color: #fff;
    border: none;
    cursor: pointer;
    font-size: 16px;

}

    .predictButton,
    .unriggerButton,
    .slideButton,
    .crashButton,
    .toggleChatButton {
        width: 280px;
        height: 40px;
        background-color: #323040;
        color: #808080; /* Default text color when not hovered */
        font-family: 'Roboto', sans-serif;
        display: block;
        margin: 5px auto;
        border-radius: 10px;
        transition: background-color 0.2s ease, color 0.2s ease;
        border: none;
        cursor: pointer;
    }

    .predictButton:hover,
    .unriggerButton:hover,
    .slideButton:hover,
    .crashButton:hover,
    .toggleChatButton:hover {
        background-color: #434352;
        color: #fff; /* Text color when hovered */
    }
}

`;

document.body.insertAdjacentHTML('beforeend', guiHTML);

// Add the style element to the head of the document

const styleElement = document.createElement('style');

styleElement.textContent = styleCSS;

document.head.appendChild(styleElement);

const guiElement = document.getElementById('bloxflipESP');

document.getElementById('minesButton').addEventListener('click', function() {
    // Fetching the mine amount from the input field
    var mineAmount = parseInt(document.getElementById('mineAmount').value);

    // Checking if the input is valid (a positive integer)
    if (!isNaN(mineAmount) && mineAmount > 0) {
        displayGif();
        resetMines(); // Reset previous outlines

        setTimeout(function() {
            // Call predictMines() function after the GIF is closed
            predictMines(mineAmount, "#aa00f2");
        }, 2000); // Adjust the time to match the duration of the GIF
    } else {
        alert("Please enter a valid positive number for the mine amount.");
    }
});
const colorText = document.getElementById('colorText');
const slideButton = document.getElementById('slideButton');

slideButton.addEventListener('click', function() {
    displayGif();
    fetch('https://api.bloxflip.com/games/roulette')
        .then(response => response.json())
        .then(data => {
            const rouletteHistory = data.history;
            const colorCounts = {
                red: 11,
                purple: 10,
                yellow: 3
            };

            // Count occurrences of each color in the history
            rouletteHistory.forEach(game => {
                const color = game.winningColor.toLowerCase();
                if (colorCounts.hasOwnProperty(color)) {
                    colorCounts[color]++;
                }
            });

            // Find the color with the maximum count
            const maxColor = Object.keys(colorCounts).reduce((a, b) => colorCounts[a] > colorCounts[b] ? a : b);
            const maxChance = (colorCounts[maxColor] / rouletteHistory.length) * 100;

            colorText.textContent = `${maxColor.charAt(0).toUpperCase() + maxColor.slice(1)} Past games Prediction: ${maxChance.toFixed(2)}%`;
        })
        .catch(error => {
            console.error('API request failed: ', error);
            colorText.textContent = 'Error fetching prediction';
        });
});

const crashButton = document.getElementById('crashButton');

crashButton.addEventListener('click', function() {
    displayGif();
    fetch("https://api.bloxflip.com/games/crash")
        .then(response => response.json())
        .then(data => {
            const previousGame = data.history[0].crashPoint;
            const av2 = (data.history[0].crashPoint + data.history[1].crashPoint);
            const chancenum = 100 / previousGame;
            const estnum = (1 / (1 - chancenum) + av2) / 2;
            const estimate = parseFloat(estnum.toFixed(2));
            const chance = parseFloat(chancenum.toFixed(2));

            const crashPointText = document.getElementById('crashPointText');
            const estimateText = document.getElementById('estimateText');

            crashPointText.textContent = `Previous Crash: ${previousGame}`;
            estimateText.textContent = `Estimated Safe: ${estimate}, Chance: ${chance}`;
        })
        .catch(error => {
            console.error('API request failed: ', error);
            const crashPointText = document.getElementById('crashPointText');
            const estimateText = document.getElementById('estimateText');

            crashPointText.textContent = 'Error ';
            estimateText.textContent = '';
        });
});

function toggleChatVisibility() {
    var chat = document.querySelector('#__next > div.layout_layout__JvcqL > div > div.layout_layoutChat__ksWYR > aside');
    var toggleChatButton = document.getElementById('toggleChatButton');
    if (toggleChatButton.textContent === "Hide Chat") {
        toggleChatButton.textContent = "Show Chat";
        chat.style.display = 'none';
    } else {
        chat.style.display = 'flex';
        toggleChatButton.textContent = "Hide Chat";
    }
}

// Add event listener to the toggle chat button
document.getElementById('toggleChatButton').addEventListener('click', toggleChatVisibility);


 const bloxflipESP = document.getElementById('bloxflipESP');
const glowElements = document.querySelectorAll('.glow');

document.getElementById('borderColorInput').addEventListener('input', function() {
    const newBorderColor = this.value;
    bloxflipESP.style.borderColor = newBorderColor;
    glowElements.forEach(element => {
        element.style.textShadow = `0 0 0 ${newBorderColor}`; // Adjusted blur radius to 0px
    });
    const boxShadowValue = `0 0 5px 0 ${newBorderColor}, 0 0 10px 0 ${newBorderColor}, 0 0 15px 0 ${newBorderColor}`; // Adjusted shadow values
    bloxflipESP.style.boxShadow = boxShadowValue;
});


        document.getElementById('autoMinesButton').addEventListener('click', function() {

            autoMinesActive = !autoMinesActive; // Toggle Auto Mines status

            this.textContent = autoMinesActive ? "Stop Auto Mines" : "Auto Mines";

            if (autoMinesActive) {
                startAutoMines();

            }

        });


        document.getElementById('unriggerButton').addEventListener('click', function() {

            const serverHash = prompt("Please enter your server hash:");

            if (serverHash !== null && serverHash !== "") {

                const randomNumber = Math.floor(Math.random() * 100) + 1;

                alert(`Succesfully unrigged!`);

            }

        });

        guiElement.addEventListener('mousedown', startDrag);

        document.addEventListener('mousemove', drag);

        document.addEventListener('mouseup', endDrag);

        document.getElementById('minimizeButton').addEventListener('click', function() {

            guiElement.style.display = 'none';

        });

        document.getElementById('toggleModeButton').addEventListener('click', function() {

            toggleMode();

        });

    }



function displayGif() {
    // Store the original position of the color picker
    const originalColorPickerPosition = document.getElementById('borderColorInput').style.position;

    // Hide elements within the menu except for the GIF
    const menuElementsToHide = document.querySelectorAll('#minesButton, #mineAmountInput, #autoMinesButton, #unriggerButton, #slideButton, #crashButton, #borderColorInput, #crashPointText, #estimateText, hr, #colorText, label[for="borderColorInput"]');
    menuElementsToHide.forEach(element => {
        element.style.display = 'none';
    });

    const gifURL = 'https://cdn.dribbble.com/users/563824/screenshots/4155980/media/c0715efb7408b3bd7ed21981dc331d68.gif'; // Replace with the actual URL of your GIF
    const gifContainer = document.createElement('div');
    gifContainer.style.textAlign = 'center'; // Align to the right
    const gifElement = document.createElement('img');
    gifElement.src = gifURL;
    gifElement.style.width = '100%'; // Adjust the width as needed
    gifElement.style.marginBottom = '0px'; // Add some margin below the GIF
    gifContainer.appendChild(gifElement);
    const projectLHeader = document.querySelector('h2.glow');
    projectLHeader.insertAdjacentElement('afterend', gifContainer);

    setTimeout(() => {
        gifElement.remove();
        // Show the hidden menu elements after removing the GIF
        menuElementsToHide.forEach(element => {
            element.style.display = 'block';
        });
        // Restore the original position of the color picker
        document.getElementById('borderColorInput').style.position = originalColorPickerPosition;
    }, 2000); // Adjust the time to display the GIF as needed
}


    function resetMines() {
        const tiles = document.querySelectorAll('.mines_minesGameItem__S2ytQ');
        tiles.forEach(tile => {
            tile.style.backgroundColor = '';
            tile.style.boxShadow = '';
        });
        if (predictionTextElement) {
            predictionTextElement.remove();
        }
    }

    let predictionTextElement;

  function predictMines(maxSpots, color) {
    // Select all mine buttons
    const mineButtons = document.querySelectorAll('div.mines_minesGameContainer__Ih15s > button');

    // Generate random indices for mine buttons
    const indices = [];
    while (indices.length < maxSpots) {
        const index = Math.floor(Math.random() * mineButtons.length);
        if (!indices.includes(index)) {
            indices.push(index);
        }
    }

    // Iterate through the indices and update mine styles
    indices.forEach(index => {
        const mine = mineButtons[index];
        if (mine) {
            // Update mine style based on color
            if (color === "#FF0000") {
                mine.style.boxShadow = '0 0 15px #FF0000, 0 0 10px #FF0000, 0 0 10px #FF0000';
            } else if (color === "#aa00f2") {
                mine.style.boxShadow = '0 0 15px #6324b5, 0 0 15px #6324b5, 0 0 15px #6324b5';
            }
        }
    });
}




function startAutoMines1() {
    const minesButton = document.getElementById('minesButton');

    // Trigger the click event on the minesButton to generate predictions
    // minesButton.click();

    // bombminesButton.click();

    // Wait for a short time (adjust the timeout value if needed) to ensure predictions are generated
    setTimeout(() => {
        const minesToClick = document.querySelectorAll('.mines_minesGameItem__S2ytQ:not([style*="box-shadow"])');

        minesToClick.forEach(mine => {
            mine.click();
        });

        // Disable autoMines feature after clicking the spots
        autoMinesActive = false;

        // Update the button text to reflect the state change
        const autoMinesButton = document.getElementById('autoMinesButton');
        autoMinesButton.textContent = "Auto Mines";
    }, 500); // 1000 milliseconds (1 second) timeout to wait for predictions, adjust if needed
}


function startAutoMines() {

    const minesButton = document.getElementById('minesButton');

    // Trigger the click event on the minesButton to generate predictions

    //minesButton.click();

    //bombminesButton.click();

    // Wait for a short time (adjust the timeout value if needed) to ensure predictions are generated

    setTimeout(() => {

        //const predictedSpots = document.querySelectorAll('button[style*="none"]');
        const predictedSpots = document.querySelectorAll('button[style*="box-shadow"]');

        predictedSpots.forEach(spot => {

            spot.click();

        });

        // Disable autoMines feature after clicking the spots

        autoMinesActive = false;

        // Update the button text to reflect the state change

        const autoMinesButton = document.getElementById('autoMinesButton');

        autoMinesButton.textContent = "Auto Mines";

    }, 500); // 1000 milliseconds (1 second) timeout to wait for predictions, adjust if needed

}



function startDrag(e) {
    isDragging = true;

    const guiElement = document.getElementById('bloxflipESP');

    // Calculate the offset between mouse pointer and GUI element
    const rect = guiElement.getBoundingClientRect();
    offsetX = e.clientX - rect.left;
    offsetY = e.clientY - rect.top;

    // Set GUI element position to absolute, adjust z-index, and prevent cursor change
    guiElement.style.position = 'absolute';
    guiElement.style.zIndex = '9999';
    guiElement.style.userSelect = 'none'; // Prevent cursor change

    // Attach event listeners for mousemove and mouseup events
    document.addEventListener('mousemove', drag);
    document.addEventListener('mouseup', stopDrag);
}

//function drag(e) {
//    if (isDragging) {
//        // Update GUI position based on mouse coordinates and initial offset
//        const guiElement = document.getElementById('bloxflipESP');
//        guiElement.style.left = e.clientX - offsetX + 'px';
//        guiElement.style.top = e.clientY - offsetY + 'px';
//    }
//}

function drag(e) {
    if (isDragging) {
        // Update GUI position based on mouse coordinates and initial offset
        const guiElement = document.getElementById('bloxflipESP');
        guiElement.style.left = e.clientX - offsetX + 'px';
        guiElement.style.top = e.clientY - offsetY + 'px';
        guiElement.style.transform = `translate(-0%, -0%)`;
    }
}

function stopDrag() {
    isDragging = false;

    // Remove event listeners for mousemove and mouseup events
    document.removeEventListener('mousemove', drag);
    document.removeEventListener('mouseup', stopDrag);
}




createGUI();
})();





