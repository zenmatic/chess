# chess
[![GoDoc](https://godoc.org/github.com/loganjspears/chess?status.svg)](https://godoc.org/github.com/loganjspears/chess)
[![Build Status](https://drone.io/github.com/loganjspears/chess/status.png)](https://drone.io/github.com/loganjspears/chess/latest)
[![Coverage Status](https://coveralls.io/repos/loganjspears/chess/badge.svg?branch=master&service=github)](https://coveralls.io/github/loganjspears/chess?branch=master)

package chess is a go library designed to accomplish the following:
- chess game / turn management
- move validation
- PGN encoding / decoding
- FEN encoding / decoding

## Usage

Using Moves
```go
game := chess.NewGame()
moves := game.ValidMoves()
game.Move(moves[0])
```

Using Squares
```go
game := chess.NewGame()
game.MoveSq(chess.E2,chess.E4,chess.NoPromo)
```

Using Algebraic Notation
```go
game := chess.NewGame()
game.MoveAlg("e4")
```

Random Game
```go
package main

import (
	"fmt"

	"github.com/loganjspears/chess"
)

func main() {
    game := chess.NewGame()
	// generate moves until game is over
    for game.Outcome() == chess.NoOutcome {
		// select a random move
        moves := game.ValidMoves()
        move := moves[rand.Intn(len(moves))]
		game.Move(move)
    }
	// print outcome and game PGN
	fmt.Println(game.State().Board().Draw())
	fmt.Printf("Game completed. %s by %s.\n", game.Outcome(), game.Method())
    fmt.Println(game.String())    
}
```

## cmd/chess
The chess command line tool includes:
- game recorder using algebraic notation
- fen viewer
- pgn viewer

## TODO
- HTML based tool w/ GopherJS
- More robust cli tool
