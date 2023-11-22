def draw_hangman(lives):
    stages = [
        '''
        --------
        |    |
        |    O
        |   /|\\
        |   / \\
        |
        -
        ''',
        '''
        --------
        |    |
        |    O
        |   /|\\
        |   / 
        |
        -
        ''',
        '''
        --------
        |    |
        |    O
        |   /|\\
        |    
        |
        -
        ''',
        '''
        --------
        |    |
        |    O
        |   /|
        |    
        |
        -
        ''',
        '''
        --------
        |    |
        |    O
        |    |
        |    
        |
        -
        ''',
        '''
        --------
        |    |
        |    O
        |    
        |    
        |
        -
        ''',
        '''
        --------
        |    |
        |    
        |    
        |    
        |
        -
        '''
    ]
    return stages[lives]

import random

def hangman():
    wordlist= ["dairymilk", "melody", "kitkat", "perk", "munch", "snickers", "milkybar", "mars", "galaxy", "butterfun"]
    word = random.choice(wordlist)
    guessed_word = ['_'] * len(word)
    guessed_letters = []
    lives = 6
    attempts = 9

    print("Let's play hangman game!")
    print("You have only 6 lives")
    print("~~~Good luck~~~")
    print("Clue:Chocolates")

    while attempts > 0 and '_' in guessed_word:
        print(draw_hangman(lives))
        print(" ".join(guessed_word))
        guess = input("Guess a letter: ").lower()

        if len(guess) != 1 or not guess.isalpha():
            print("Please enter a single letter.")
            continue

        if guess in guessed_letters:
            print("You already guessed that letter. Try another one.")
            continue

        guessed_letters.append(guess)

        if guess in word:
            for i in range(len(word)):
                if word[i] == guess:
                    guessed_word[i] = guess
            print("Correct guess!")
        else:
            print("Incorrect guess.")
            lives -= 1
            print(f"You have {lives} lives left.")

        attempts -= 1

    if '_' not in guessed_word:
        print("Congratulations! You guessed the right word:", "".join(guessed_word))
    else:
        print("Sorry, you didn't find the correct word. The word was:", word)
        print(draw_hangman(lives))

hangman()
