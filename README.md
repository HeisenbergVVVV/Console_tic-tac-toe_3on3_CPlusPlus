This is a Tic Tac Toe game written in C++. Here is a brief summary of the functions:

print_board: Prints the current state of the game board. 
make_move: Takes the user input for the position they want to place their symbol (X or O) on the board, and updates the board. 
check_win: Checks if the game has ended (either X or O won or the game is a draw) and returns the winner or a blank character if the game is not over. 
default_values: Initializes the game board to its default state and resets the counter for the number of moves made. 
game_question: Asks the user if they want to play again, and resets the game if the answer is yes. 
The main function contains the game loop. The loop continues until the user decides to quit. The make_move and check_win functions are called in each iteration of the loop. The loop exits when the game is over or when the user decides to quit. 
