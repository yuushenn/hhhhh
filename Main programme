# Tic Tac Toe 

import math

HUMAN = "X"
AI = "O"

def print_board(board):
    print()
    for i in range(3):
        print(" | ".join(board[i]))
        if i < 2:
            print("--+---+--")
    print()

def check_win(board, player):
    for row in board:
        if all(cell == player for cell in row):
            return True

    for col in range(3):
        if all(board[row][col] == player for row in range(3)):
            return True

    if all(board[i][i] == player for i in range(3)):
        return True

    if all(board[i][2 - i] == player for i in range(3)):
        return True

    return False

def is_draw(board):
    return all(cell in (HUMAN, AI) for row in board for cell in row)

def get_available_moves(board):
    moves = []
    for i in range(3):
        for j in range(3):
            if board[i][j] not in (HUMAN, AI):
                moves.append((i, j))
    return moves

def minimax(board, depth, is_maximizing):
    if check_win(board, AI):
        return 1
    if check_win(board, HUMAN):
        return -1
    if is_draw(board):
        return 0

    if is_maximizing:
        best_score = -math.inf
        for (i, j) in get_available_moves(board):
            board[i][j] = AI
            score = minimax(board, depth + 1, False)
            board[i][j] = str(i * 3 + j + 1)
            best_score = max(score, best_score)
        return best_score
    else:
        best_score = math.inf
        for (i, j) in get_available_moves(board):
            board[i][j] = HUMAN
            score = minimax(board, depth + 1, True)
            board[i][j] = str(i * 3 + j + 1)
            best_score = min(score, best_score)
        return best_score

def best_move(board):
    best_score = -math.inf
    move = None
    for (i, j) in get_available_moves(board):
        board[i][j] = AI
        score = minimax(board, 0, False)
        board[i][j] = str(i * 3 + j + 1)
        if score > best_score:
            best_score = score
            move = (i, j)
    return move

def main():
    board = [[str(i * 3 + j + 1) for j in range(3)] for i in range(3)]
    print("Tic Tac Toe — You are X, AI is O")
    print_board(board)

    while True:
        # Human turn
        while True:
            try:
                move = int(input("Enter your move (1-9): ")) - 1
                row, col = move // 3, move % 3
                if board[row][col] not in (HUMAN, AI):
                    board[row][col] = HUMAN
                    break
                else:
                    print("Cell already taken. Try again.")
            except (ValueError, IndexError):
                print("Invalid move. Choose 1–9.")

        print_board(board)
        if check_win(board, HUMAN):
            print("You win!")
            break
        if is_draw(board):
            print("It's a draw!")
            break

        # AI turn
        print("AI is thinking...")
        row, col = best_move(board)
        board[row][col] = AI
        print_board(board)

        if check_win(board, AI):
            print("AI wins!")
            break
        if is_draw(board):
            print("It's a draw!")
            break

if __name__ == "__main__":
    main()
