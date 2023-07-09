# Ruby Puzzle Game

# Define the puzzle board
board = [
  ['A', 'B', 'C'],
  ['D', 'E', 'F'],
  ['G', 'H', 'I']
]

# Initialize variables
moves = 0
completed = false

# Display the instructions
puts "Welcome to the Ruby Puzzle Game!"
puts "Instructions: Rearrange the letters to form the word 'RUBY'."

# Game loop
while !completed
  # Display the current board
  puts "\nCurrent Board:"
  board.each { |row| puts row.join(' ') }

  # Prompt the user for a move
  puts "\nEnter the letter you want to move (or 'Q' to quit):"
  move = gets.chomp.upcase

  # Handle the user's move
  case move
  when 'Q'
    puts "\nThanks for playing!"
    completed = true
  when 'A'..'I'
    row_index = nil
    col_index = nil

    # Find the current position of the selected letter
    board.each_with_index do |row, i|
      if row.include?(move)
        row_index = i
        col_index = row.index(move)
        break
      end
    end

    if row_index.nil? || col_index.nil?
      puts "Invalid move. Please select a letter from the board."
    else
      # Swap the selected letter with the empty space (represented by ' ')
      empty_row_index = nil
      empty_col_index = nil

      board.each_with_index do |row, i|
        if row.include?(' ')
          empty_row_index = i
          empty_col_index = row.index(' ')
          break
        end
      end

      board[row_index][col_index], board[empty_row_index][empty_col_index] = board[empty_row_index][empty_col_index], board[row_index][col_index]
      moves += 1

      # Check if the puzzle is solved
      if board.flatten.join('') == 'RUBY'
        completed = true
        puts "\nCongratulations! You solved the puzzle in #{moves} moves."
      end
    end
  else
    puts "Invalid move. Please enter a valid letter from the board."
  end
end
