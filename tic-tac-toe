import math

# Function to print the TicTacToe board
def print_board(board):
    for row in board:
        print(" ".join(row))
    print()

# Function to check if the board is full
def is_board_full(board):
    for row in board:
        if " " in row:
            return False
    return True

# Function to check if the game is over
def is_game_over(board):
    # Check rows, columns, and diagonals for a win
    for i in range(3):
        if board[i][0] == board[i][1] == board[i][2] != " " or \
           board[0][i] == board[1][i] == board[2][i] != " ":
            return True
    if board[0][0] == board[1][1] == board[2][2] != " " or \
       board[0][2] == board[1][1] == board[2][0] != " ":
        return True
    # Check if the board is full
    if is_board_full(board):
        return True
    return False

# Function to get available moves on the board
def available_moves(board):
    moves = []
    for i in range(3):
        for j in range(3):
            if board[i][j] == " ":
                moves.append((i, j))
    return moves

# Function to evaluate the board and return a score
def evaluate(board):
    # Check rows, columns, and diagonals for a win
    for i in range(3):
        if board[i][0] == board[i][1] == board[i][2] != " ":
            return 10 if board[i][0] == 'X' else -10
        if board[0][i] == board[1][i] == board[2][i] != " ":
            return 10 if board[0][i] == 'X' else -10
    if board[0][0] == board[1][1] == board[2][2] != " ":
        return 10 if board[0][0] == 'X' else -10
    if board[0][2] == board[1][1] == board[2][0] != " ":
        return 10 if board[0][2] == 'X' else -10
    return 0  # No winner yet

# Minimax algorithm with alpha-beta pruning
def minimax(board, depth, maximizing_player, alpha, beta):
    if is_game_over(board):
        return evaluate(board)

    moves = available_moves(board)

    if maximizing_player:
        max_eval = -math.inf
        for move in moves:
            board[move[0]][move[1]] = 'X'
            eval = minimax(board, depth + 1, False, alpha, beta)
            board[move[0]][move[1]] = ' '
            max_eval = max(max_eval, eval)
            alpha = max(alpha, eval)
            if beta <= alpha:
                break
        return max_eval
    else:
        min_eval = math.inf
        for move in moves:
            board[move[0]][move[1]] = 'O'
            eval = minimax(board, depth + 1, True, alpha, beta)
            board[move[0]][move[1]] = ' '
            min_eval = min(min_eval, eval)
            beta = min(beta, eval)
            if beta <= alpha:
                break
        return min_eval

# Function to find the best move for AI player using Minimax
def find_best_move(board):
    best_move = (-1, -1)
    best_eval = -math.inf
    alpha = -math.inf
    beta = math.inf
    moves = available_moves(board)
    for move in moves:
        board[move[0]][move[1]] = 'X'
        eval = minimax(board, 0, False, alpha, beta)
        board[move[0]][move[1]] = ' '
        if eval > best_eval:
            best_eval = eval
            best_move = move
    return best_move

# Function to play TicTacToe
def play_tictactoe():
    board = [[" " for _ in range(3)] for _ in range(3)]
    print("Welcome to Tic Tac Toe!")
    print_board(board)
    
    while not is_game_over(board):
        # Player's turn
        player_move = input("Enter your move (row[1-3] column[1-3]): ")
        row, col = map(int, player_move.split())
        row -= 1
        col -= 1
        if board[row][col] != " ":
            print("Invalid move. Try again.")
            continue
        board[row][col] = 'O'
        print_board(board)
        
        if is_game_over(board):
            break
        
        # AI's turn
        print("AI is making a move...")
        ai_move = find_best_move(board)
        board[ai_move[0]][ai_move[1]] = 'X'
        print_board(board)
    
    # Game result
    if evaluate(board) == 10:
        print("You lose! AI wins.")
    elif evaluate(board) == -10:
        print("Congratulations! You win!")
    else:
        print("It's a draw!")

# Play the game
play_tictactoe()


