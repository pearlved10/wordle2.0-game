"""
Name: Pearl Ved

"""
import random
from datetime import datetime

# Function opens the specified file (fn), reads words, strips whitespace, and returns them as a list
def get_words(fn):
    with open(fn, 'r') as fh:
        words = [word.strip() for word in fh.readlines()] # Read lines and strip whitespace
    return words

# Function to display rules and greetings; prints the current date/time and provides 
# a morning/evening greeting based on the time of day
def show_rules():
    current_time = datetime.now()
    formatted_time = current_time.strftime('%Y-%m-%d %H:%M:%S')
    print('Current Date & Time:' , formatted_time)
    
    # Greet user based on whether it's AM or PM
    if current_time.strftime('%p') == 'AM':
        print("Good morning! Welcome to Wordle 2.0. 🌤️")
    else:
        print("Good evening! Welcome to Wordle 2.0. 🌙")
    print() 
    
# Function to handle the mode selection; prompts user for a valid input ('easy' or 'hard'), 
# and continues asking until input is valid
def mode_selection():
    
    mode_input = input("Select your mode - Easy or Hard?: ").strip().lower() # removes whitespace/converts to lowercase for uniformity
    
    # Keeps asking until the user enters 'easy' or 'hard'
    while mode_input not in ['easy', 'hard']:
        print("Please enter a valid mode ('Easy' or 'Hard').")
        mode_input = input("Select your mode - Easy or Hard?: ").strip().lower()
    return mode_input

# Function to begin the Wordle game based on selected mode and word list; 
# sets the max number of guesses and word length based on the mode and starts the game
def begin_wordle(mode_input, words):
    
    # Sets the game rules based on whether the mode is easy or hard
    if mode_input == 'easy':
        print("You selected easy mode. Let's begin!")
        max_guesses = 6
        word_length = 5
    elif mode_input == 'hard':
        print("You selected hard mode. Let's begin!")
        max_guesses = 4
        word_length = 7
        
    print()

    # Select a random word of the specified length from the word list, in lowercase
    random_word = random.choice([word for word in words if len(word) == word_length]).lower()  
    print("The word has", str(word_length), "letters. Start guessing!")
    print()
    
    guesses_count = 0  # Tracks the number of guesses made so far
    
    # Game loop: Lets the player guess up to the maximum allowed guesses
    while guesses_count < max_guesses:
        guesses_count += 1 # Increment the guess counter for each attempt
        
        # Get the player's guess, strip any excess spaces, and convert it to lowercase for case-insensitive comparison
        guess = input('Guess # ' + str(guesses_count) + ': ').strip().lower()  
        
        # Validate the guess: it must be alphabetic (only letters) and match the required word length
        if not guess.isalpha():
            print("Please only type letters in your guess. Try again.")
            guesses_count -= 1  # Decrease the guess count to avoid penalizing the player
            continue
        
        if len(guess) != word_length:
            print('Your guess must be', word_length, 'letters long. Try again.')
            guesses_count -= 1  # Ignore this invalid attempt
            continue 
        
        # If the guess is correct, congratulate the player and end the game
        if guess == random_word:
            print("Congratulations! You guessed the right word! 🥳")
            break
        
        # If the guess is incorrect, provide a hint to the player
        hint = ''
        # Compare each letter of the guess to the corresponding letter of the target word
        for i in range(word_length):
            if guess[i] == random_word[i]:  # Correct letter in the right position
                hint += random_word[i] + ' '  # Display the correct letter
            elif guess[i] in random_word:  # Correct letter, but in the wrong position
                hint += ' (' + guess[i] + ') ' # Indicate with parentheses
            else:
                hint += ' __ '  # Display underscores for letters not present in the target word at all
            
        print("Hints:", hint)  # Print the generated hint for the player
    
    else:
        # If the player runs out of guesses, reveal the correct word
        print(f"Sorry, you're out of guesses 😞. The correct word was: {random_word}")
        
# Main function that drives the game
# It first displays the rules, loads the list of words from a file,
# then starts the game based on the user's selected difficulty mode
def game_executor():
    show_rules()
    words = get_words('words.txt') # Load words from file
    mode_input = mode_selection() # Get mode input from player
    begin_wordle(mode_input,words) # Start the game with chosen mode and words

# This checks if the script is being executed directly (not imported as a module),
# and if so, calls the game_executor function to start the game
if __name__ == '__main__':
    game_executor()

