<h1>ExpNo 9: Solve Wumpus World Problem using Python demonstrating Inferences from Propositional Logic</h1> 
<h3>Name:    Jebin Raj J                   </h3>
<h3>Register Number/Staff Id:     212224030012           </h3>
<H3>Aim:</H3>
<p>
    To solve  Wumpus World Problem using Python demonstrating Inferences from Propositional Logic
</p>
<h1>Problem Description</h1>
<hr>
<h2>Wumpus World</h2>
<hr>
The Wumpus world is a simple world example to illustrate the worth of a knowledge-based agent and to represent knowledge representation.

The figure below shows a Wumpus world containing one pit and one Wumpus. There is an agent in room [1,1]. The goal of the agent is to exit the Wumpus world alive. The agent can exit the Wumpus world by reaching room [4,4]. The wumpus world contains exactly one Wumpus and one pit. There will be a breeze in the rooms adjacent to the pit, and there will be a stench in the rooms adjacent to Wumpus.

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/cd6b68dc-c79f-4dcb-8126-04da90d65912)

<center>Wumpus World Representation</center>
<p>
This is a python program that uses propositional logic sentences to check which rooms are safe. 

It is assumed that there will always be a safe path that the agent can take to exit the Wumpus world. The logical agent can take four actions: Up, Down, Left and Right. These actions help the agent move from one room to an adjacent room. The agent can perceive two things: Breeze and Stench.
</p>

<hr>
<h1>Sample Input and Output:</h1>
<hr>
# -----------------------------------------------
# Wumpus World Problem using Propositional Logic
# -----------------------------------------------

# Author: AI-based Inference Example
# Demonstrates reasoning of safe cells using logic
# -----------------------------------------------

class WumpusWorld:
    def __init__(self, size=4):
        self.size = size
        # Initialize perception grids
        self.breeze = [[False]*size for _ in range(size)]
        self.stench = [[False]*size for _ in range(size)]
        self.pit = [[False]*size for _ in range(size)]
        self.wumpus = [[False]*size for _ in range(size)]
        self.safe = [[None]*size for _ in range(size)]  # Unknown initially

    def set_pit(self, x, y):
        self.pit[x][y] = True
        # Adjacent cells will have breeze
        for i, j in self.get_adjacent(x, y):
            self.breeze[i][j] = True

    def set_wumpus(self, x, y):
        self.wumpus[x][y] = True
        # Adjacent cells will have stench
        for i, j in self.get_adjacent(x, y):
            self.stench[i][j] = True

    def get_adjacent(self, x, y):
        adj = []
        if x > 0:
            adj.append((x-1, y))
        if x < self.size-1:
            adj.append((x+1, y))
        if y > 0:
            adj.append((x, y-1))
        if y < self.size-1:
            adj.append((x, y+1))
        return adj

    # Logical Inference based on percepts
    def infer_safe_cells(self):
        print("Inferring safe cells using Propositional Logic...\n")
        for x in range(self.size):
            for y in range(self.size):
                if (x, y) == (0, 0):
                    self.safe[x][y] = True  # Start position always safe
                    continue

                # If there is no breeze and no stench perceived -> Safe cell
                if not self.breeze[x][y] and not self.stench[x][y]:
                    self.safe[x][y] = True
                else:
                    # If there's a breeze or stench, mark as uncertain/unsafe
                    self.safe[x][y] = False

    def print_world(self):
        print("\nWumpus World Environment (4x4):\n")
        for x in range(self.size):
            for y in range(self.size):
                cell = ""
                if self.wumpus[x][y]:
                    cell += "W "
                elif self.pit[x][y]:
                    cell += "P "
                else:
                    cell += "- "
                print(cell, end=" ")
            print()

        print("\nBreeze Percepts:")
        for row in self.breeze:
            print(row)

        print("\nStench Percepts:")
        for row in self.stench:
            print(row)

    def print_safe_inference(self):
        print("\nInference Results:")
        for x in range(self.size):
            for y in range(self.size):
                status = "SAFE" if self.safe[x][y] else "UNSAFE"
                print(f"Cell [{x+1},{y+1}] → {status}")
        print()


# --------------------------
# MAIN EXECUTION
# --------------------------
if __name__ == "__main__":
    ww = WumpusWorld(4)

    # Define positions (index starts at 0)
    ww.set_pit(1, 2)        # Pit at [2,3]
    ww.set_wumpus(2, 0)     # Wumpus at [3,1]

    ww.print_world()

    ww.infer_safe_cells()

    ww.print_safe_inference()


![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/8696111a-a4a7-47cb-ba4b-43a4ef88573f)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/4be5bf06-79fa-4fa0-9334-38a33f06060b)

