# Connect Four
> A week and a half long paired project from Turing's Backend program highlighting enumerables and user interaction 

![connect_four](https://user-images.githubusercontent.com/98674727/179262274-7cc9e605-a2b1-4049-a949-2b80936021f6.gif)
## Table of Contents
* [Overview](#overview)
* [Future Additions](#potential-refactor)
* [Collaborators](#collaborators)

## Overview
This project was done primarily using paired programming in a driver navigator situation

#### Technologies
![ruby](https://img.shields.io/badge/Ruby-CC342D?style=for-the-badge&logo=ruby&logoColor=white)
![vscode](https://img.shields.io/badge/VSCode-0078D4?style=for-the-badge&logo=visual%20studio%20code&logoColor=white)

* RSpec
* Pry

#### To try it out: 
1. Clone this Repo
2. `cd` into the repo and run `ruby lib/connect_four.rb` from your terminal
3. Press p to play and press q when you are ready to not play anymore!
## Overcoming Difficulties
Diagonal Checks in both `lib` and `spec`

```sh
it "can determine a winning pattern diagonally from left side of board" do
  board = GameBoard.new
  expect(board.diagonal_winner?("O")).to eq false
  board.place_piece(:A, "O")
  board.place_piece(:A, "X")
  board.place_piece(:A, "X")
  board.place_piece(:A, "O")
  board.place_piece(:B, "X")
  board.place_piece(:B, "O")
  board.place_piece(:B, "O")
  board.place_piece(:C, "X")
  board.place_piece(:C, "O")
  board.place_piece(:C, "O")
  board.place_piece(:D, "O")
  board.place_piece(:D, "X")
  board.place_piece(:D, "O")
  board.place_piece(:D, "X")
  expect(board.diagonal_winner?("O")).to eq true
end

it "can determine winner diagonally from right side of board" do
  board = GameBoard.new
  expect(board.diagonal_winner?("O")).to eq false
  board.place_piece(:G, "O")
  board.place_piece(:G, "O")
  board.place_piece(:G, "O")
  board.place_piece(:G, "X")
  board.place_piece(:F, "X")
  board.place_piece(:F, "O")
  board.place_piece(:F, "O")
  board.place_piece(:E, "X")
  board.place_piece(:E, "O")
  board.place_piece(:E, "O")
  board.place_piece(:D, "O")
  board.place_piece(:D, "X")
  board.place_piece(:D, "X")
  board.place_piece(:D, "O")
  expect(board.diagonal_winner?("O")).to eq true
end
 ```
 ```sh
def diagonal_winner?(chip)
  #go through each row
  for i in 0..5
    row = i
    keys = @board.keys
    if check_diagonal_columns?(keys, row, i, chip)
      return true
    end
  end
  for i in 0..5
    row = i
    keys_reversed = @board.keys.reverse
    if check_diagonal_columns?(keys_reversed, row, i, chip)
      return true
    end
  end
  return false
end

def check_diagonal_columns?(column_array, row, i, chip)
  count_chips = 0
  column_array.each do |col|
    #do not allow loop to continue if row has been decremented past 0
    if row < 0 || row > 5
      break
    end
    #check downward diagonal if starting in rows 0-2
    if i <=2
      if @board[col][row] == chip
        count_chips += 1
        if count_chips == 4
          return true
        end
      else
        count_chips = 0
      end
      row += 1
    #check upward diagonal if starting in rows 3-5
    else
      if @board[col][row] == chip
        count_chips += 1
        # puts "chip at #{col} and #{row}"
        if count_chips == 4
          return true
        end
      else
        count_chips = 0
      end
      row = row - 1
    end
  end
  return false
end
```
## Potential Refactor
 * Make methods smaller for developer empathy and encapsulation logic
 * Add wins to a database to keep track of score
 * Perform more robust testing
    * Test for edge cases and sad paths

## Collaborators
[Thomas Haines](https://github.com/tjhaines-cap/connect_four)</br>
[Casey Fazio](https://github.com/casefaz)
