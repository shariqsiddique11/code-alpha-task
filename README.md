# code-alpha-task
Number guessing code alpha task 
#include <iostream>  // For input and output
#include <cstdlib>   // For generating random numbers
#include <ctime>     // For time functions, to seed the random number generator
#include <limits>    // For numeric_limits, used for input validation

// Function to generate a random number within a specified range
int generateRandomNumber(int lower, int upper) {
    return lower + rand() % (upper - lower + 1);  // Random number between lower and upper (inclusive)
}

int main() {
    // Seed the random number generator with the current time
    std::srand(static_cast<unsigned>(std::time(0)));

    // Define the range of numbers
    int lowerLimit = 1;
    int upperLimit = 100;
    
    // Generate a random number to guess
    int targetNumber = generateRandomNumber(lowerLimit, upperLimit);

    // Provide a hint before starting the guessing
    std::cout << "Welcome to the Number Guessing Game!\n";
    std::cout << "I have selected a number between " << lowerLimit << " and " << upperLimit << ".\n";

    // Hint: tell whether the number is even or odd
    if (targetNumber % 2 == 0) {
        std::cout << "Hint: The number is even.\n";
    } else {
        std::cout << "Hint: The number is odd.\n";
    }

    int playerGuess = 0;
    int numberOfTries = 0;

    // Main game loop
    while (true) {
        std::cout << "Enter your guess: ";
        std::cin >> playerGuess;

        // Check if the input is valid
        if (std::cin.fail()) {
            std::cin.clear();  // Clear the error flag
            std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');  // Ignore invalid input
            std::cout << "Please enter a valid number.\n";
            continue;
        }

        numberOfTries++;

        // Check if the player's guess is correct
        if (playerGuess < targetNumber) {
            std::cout << "Too low! Try again.\n";
        } else if (playerGuess > targetNumber) {
            std::cout << "Too high! Try again.\n";
        } else {
            // Player guessed correctly
            std::cout << "Congratulations! You've guessed the correct number: " << targetNumber << "\n";
            std::cout << "It took you " << numberOfTries << " tries to guess the number.\n";
            break;  // Exit the loop since the player has guessed correctly
        }
    }

    return 0;  // End of the program
}

