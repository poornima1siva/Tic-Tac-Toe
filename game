import math

class TicTacToe:
    def __init__(self):
        self.board = [[' ' for _ in range(3)] for _ in range(3)]
        self.player_symbol = ''
        self.ai_symbol = ''

    def print_board(self):
        print("\nCurrent Board:")
        for i, row in enumerate(self.board):
            print(" | ".join(row))
            if i < 2:
                print("---------")

    def display_move_guide(self):
        print("\nMove Guide (1-9):")
        for i in range(0, 9, 3):
            print(" | ".join(str(x) for x in range(i + 1, i + 4)))
            if i < 6:
                print("---------")

    def is_winner(self, symbol):
        b = self.board
        return any([
            all([b[i][j] == symbol for j in range(3)]) for i in range(3)
        ]) or any([
            all([b[i][j] == symbol for i in range(3)]) for j in range(3)
        ]) or all([b[i][i] == symbol for i in range(3)]) or all([b[i][2 - i] == symbol for i in range(3)])

    def is_full(self):
        return all(cell != ' ' for row in self.board for cell in row)

    def get_empty_cells(self):
        return [(i, j) for i in range(3) for j in range(3) if self.board[i][j] == ' ']

    def get_user_move(self):
        while True:
            try:
                move = int(input("Enter your move (1-9): "))
                if move < 1 or move > 9:
                    raise ValueError
                row, col = divmod(move - 1, 3)
                if self.board[row][col] != ' ':
                    print("Cell already taken!")
                else:
                    return row, col
            except ValueError:
                print("Invalid input. Try a number from 1 to 9.")

    def minimax(self, depth, is_maximizing, alpha, beta):
        if self.is_winner(self.ai_symbol):
            return 10 - depth
        elif self.is_winner(self.player_symbol):
            return depth - 10
        elif self.is_full():
            return 0

        if is_maximizing:
            max_eval = -math.inf
            for row, col in self.get_empty_cells():
                self.board[row][col] = self.ai_symbol
                eval = self.minimax(depth + 1, False, alpha, beta)
                self.board[row][col] = ' '
                max_eval = max(max_eval, eval)
                alpha = max(alpha, eval)
                if beta <= alpha:
                    break
            return max_eval
        else:
            min_eval = math.inf
            for row, col in self.get_empty_cells():
                self.board[row][col] = self.player_symbol
                eval = self.minimax(depth + 1, True, alpha, beta)
                self.board[row][col] = ' '
                min_eval = min(min_eval, eval)
                beta = min(beta, eval)
                if beta <= alpha:
                    break
            return min_eval

    def get_ai_move(self):
        best_score = -math.inf
        best_move = None
        for row, col in self.get_empty_cells():
            self.board[row][col] = self.ai_symbol
            score = self.minimax(0, False, -math.inf, math.inf)
            self.board[row][col] = ' '
            if score > best_score:
                best_score = score
                best_move = (row, col)
        return best_move

    def choose_symbol(self):
        while True:
            choice = input("Choose your symbol (X or O): ").strip().upper()
            if choice in ['X', 'O']:
                self.player_symbol = choice
                self.ai_symbol = 'O' if choice == 'X' else 'X'
                break
            else:
                print("Invalid choice. Please select X or O.")

    def play(self):
        self.board = [[' ' for _ in range(3)] for _ in range(3)]
        self.choose_symbol()
        print("\n🎮 Game Start!")
        self.display_move_guide()

        while True:
            self.print_board()
            print("\nYour move:")
            row, col = self.get_user_move()
            self.board[row][col] = self.player_symbol

            if self.is_winner(self.player_symbol):
                self.print_board()
                print("\n🎉 You win!")
                break
            if self.is_full():
                self.print_board()
                print("\nIt's a tie!")
                break

            print("\nComputer is thinking...")
            row, col = self.get_ai_move()
            self.board[row][col] = self.ai_symbol

            if self.is_winner(self.ai_symbol):
                self.print_board()
                print("\n💻 Computer wins!")
                break
            if self.is_full():
                self.print_board()
                print("\nIt's a tie!")
                break

def main():
    while True:
        game = TicTacToe()
        game.play()
        again = input("\nPlay again? (yes/no): ").strip().lower()
        if again != 'yes':
            print("Thanks for playing ❤️")
            break

if __name__ == "__main__":
    main()
