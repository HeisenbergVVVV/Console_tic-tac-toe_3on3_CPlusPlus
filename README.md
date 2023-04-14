#include <iostream>
void  print_board(const char(*a)[3]) {
    for (int i = 0; i < 3; i++) {
        std::cout << "| ";
        for (int j = 0; j < 3; j++) {
            std::cout << a[i][j] << " | ";
            if (j == 2) {
                std::cout << std::endl;
                std::cout << "|---|---|---|\n";
            }
        }
    }
}
void make_move(char(*a)[3], int& pos, bool* bufer,int&count_move) {
    char symbol = 'X';
        while (bufer[pos - 1] != 0) {
            if (pos < 1 || pos >9) {
                std::cout << "Enter valid values from 1 to 9 inclusive\n";
                std::cin >> pos;
            }
            else
            {
                std::cout << "this case is already taken" << std::endl;
                std::cin >> pos;
            }
        }
        
        if (count_move % 2 == 0)symbol = 'X';
        else symbol = 'O';
        int row = (pos - 1) / 3;
        int col = (pos - 1) % 3;
        a[row][col] = symbol;
        bufer[pos - 1]++;
        ++count_move;
        print_board(a);
        
          
}
char check__win(const char(*board)[3]) {
    const char player1 = 'X', player2 = 'O';
    if ((board[0][0] == player1 && board[0][1] == player1 && board[0][2] == player1) ||   // ряд 1
        (board[1][0] == player1 && board[1][1] == player1 && board[1][2] == player1) ||   // ряд 2
        (board[2][0] == player1 && board[2][1] == player1 && board[2][2] == player1) ||   // ряд 3
        (board[0][0] == player1 && board[1][0] == player1 && board[2][0] == player1) ||   // колонка 1
        (board[0][1] == player1 && board[1][1] == player1 && board[2][1] == player1) ||   // колонка 2
        (board[0][2] == player1 && board[1][2] == player1 && board[2][2] == player1) ||   // колонка 3
        (board[0][0] == player1 && board[1][1] == player1 && board[2][2] == player1) ||   // діагональ 1
        (board[0][2] == player1 && board[1][1] == player1 && board[2][0] == player1) == 1)  // діагональ 2
        return player1;
    else if ((board[0][0] == player2 && board[0][1] == player2 && board[0][2] == player2) ||
        (board[1][0] == player2 && board[1][1] == player2 && board[1][2] == player2) ||
        (board[2][0] == player2 && board[2][1] == player2 && board[2][2] == player2) ||
        (board[0][0] == player2 && board[1][0] == player2 && board[2][0] == player2) ||
        (board[0][1] == player2 && board[1][1] == player2 && board[2][1] == player2) ||
        (board[0][2] == player2 && board[1][2] == player2 && board[2][2] == player2) ||
        (board[0][0] == player2 && board[1][1] == player2 && board[2][2] == player2) ||
        (board[0][2] == player2 && board[1][1] == player2 && board[2][0] == player2) == 1)
        return player2;
    else return ' ';
}
void default_values(char(*a)[3], bool* bufer,int& count_move) {
    int tt = 1;
    count_move = 0;
    std::fill_n(bufer, 9, false);
    for (int i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++) {
            a[i][j] = char(tt+48);
            ++tt;
        } 
}
void game_question(int& i, char(*a)[3], bool* bufer,int& count_move) {
    bool r = 1;
    std::cout << "Do you want to play again?\nEnter 1(Yes) or 0(No)\n";
    std::cin >> r;
    if (r == 1) {
        i = 9;
        default_values(a, bufer,count_move);
        print_board(a);
    }
    else i = -1;
}

int main()
{
    bool bufer[9] = { 0, 0, 0, 0, 0, 0, 0, 0, 0 };
    char a[][3] = { {'1', '2', '3'}, {'4', '5', '6'}, {'7', '8', '9'} };
    int pos = 0, i = 9;
    int count_move = 0;
    print_board(a);
    do {
        std::cout << (i % 2 != 0 ? "Player X's turn: " : "Player O's turn: ");
        std::cin >> pos;
        make_move(a, pos, bufer,count_move);
        i--;
        if (check__win(a) != ' ') {
            std::cout << "Player " << check__win(a) << " won!\n";
            game_question(i, a, bufer,count_move);
        }
        else if (i == 0) {
            game_question(i, a, bufer,count_move);
        }
    } while (i > 0);
    return 0;
}
