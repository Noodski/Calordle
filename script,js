const targetCalories = 95; // Example target calories for Apple
let guesses = [];
const maxGuesses = 6;

function submitGuess() {
    const input = document.getElementById('calorie-input');
    const guess = parseInt(input.value);
    
    if (isNaN(guess)) {
        alert("Please enter a valid number");
        return;
    }
    
    if (guesses.length >= maxGuesses) {
        return;
    }
    
    guesses.push(guess);
    updateGuesses();
    
    input.value = '';
    
    const diff = guess - targetCalories;
    const percentageDiff = Math.abs(diff / targetCalories * 100);
    
    let result = '';
    if (percentageDiff <= 3) {
        result = '✅';
        document.querySelector('.guess-count').textContent = `You win! Congratulations!🎉 The number of calories was ${targetCalories}`;
        document.getElementById('share-button').style.display = 'inline-block';
    } else if (diff > 0) {
        result = percentageDiff <= 10 ? '🟨⬇️' : '🟥⬇️';
    } else {
        result = percentageDiff <= 10 ? '🟨⬆️' : '🟥⬆️';
    }
    
    document.getElementById(`guess${guesses.length}`).textContent = guess;
    document.getElementById(`guess${guesses.length}`).classList.add(result);
    
    if (guesses.length >= maxGuesses && percentageDiff > 3) {
        document.querySelector('.guess-count').textContent = "You lost. Maybe next time!";
        document.getElementById('share-button').style.display = 'inline-block';
    } else {
        document.querySelector('.guess-count').textContent = `Guess ${guesses.length}/${maxGuesses}`;
    }
}

function updateGuesses() {
    for (let i = 1; i <= maxGuesses; i++) {
        document.getElementById(`guess${i}`).textContent = guesses[i - 1] || '';
    }
}

function shareResult() {
    const result = guesses.map(guess => {
        const diff = guess - targetCalories;
        const percentageDiff = Math.abs(diff / targetCalories * 100);
        
        if (percentageDiff <= 3) {
            return '✅';
        } else if (diff > 0) {
            return percentageDiff <= 10 ? '🟨⬇️' : '🟥⬇️';
        } else {
            return percentageDiff <= 10 ? '🟨⬆️' : '🟥⬆️';
        }
    }).join('\n');
    
    const shareText = `Calordle ${guesses.length}/${maxGuesses}\n${result}`;
    navigator.clipboard.writeText(shareText).then(() => {
        alert('Result copied to clipboard!');
    });
}
