## What is it?
A simple library for simulating and solving [polymatrix games](https://en.wikipedia.org/wiki/Succinct_game#Polymatrix_games), where players are nodes of a network and edges represent two-player games.

Right now polymatrix can handle any amount of players and connections between them, but only two possible strategies and two state variables for each player. If your use case is not supported, reach out via email or post an issue, I'll see what I can do.

## Installation
```
pip install polymatrix
```

## Usage

Making a quick game between randomly connected 7 players and simulating 5 random rounds:

```python
game = polymatrix.QuickGame(7)
game.simulate(5)
```

Making a game between 5 players on a ring topology (each player connected to two others) and with a starting state of 100 units for all players. Then play some strategy profiles:

```python
game = polymatrix.PolymatrixGame(start_populations_matrix =[[100,100]]*5, topology="ring")
game.play(strategy_profile = [0,1,1,1,0])
print(game.state)
```

## Architecture

The the high-level functionality (such as payoff functions) are in the PolymatrixGame class in polymatrixgame.py module, which inherits from more general MultiplayerGame from multiplayergame.py. The fundamental data of the game is information about the players (player.py) and how they are connected (network.py). The game network is really a networkx graph but with some extra methods (such as random edge addition/removal which I used for genetic programming). This is a high-level overview of dependencies:

![Polymatrix game software architecture](https://github.com/python-polymatrix-games/polymatrix-games/blob/main/corpgame-architecture.png "Polymatrix game software architecture")

There are 3 types of attributes to define a game:
global_attributes, for example: probability of an edge existing, edge weight distribution, global utility etc
player_attributes (specific to a node)
link_attributes (specific to an edge)

## Literature

I highly recommend a 2016 paper by Cai, Candogan, Daskalakis and Papadimitriou about zero-sum polymatrix games: https://www.cs.mcgill.ca/~cai/pdf/zerosum.pdf

For general algorithmic game theory: https://www.cs.cmu.edu/~sandholm/cs15-892F13/algorithmic-game-theory.pdf


