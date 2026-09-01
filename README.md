<h1>ExpNo 9: Solve Wumpus World Problem using Python demonstrating Inferences from Propositional Logic</h1> 
<h3>Name:     V.SHREYA                  </h3>
<h3>Register Number/Staff Id:    212224230266         </h3>
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




![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/8696111a-a4a7-47cb-ba4b-43a4ef88573f)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/4be5bf06-79fa-4fa0-9334-38a33f06060b)


<h3>Program</h3>

```py
# Wumpus World using Propositional Logic

# Facts about the Wumpus World
# True = present, False = absent

pit = {
    (1, 1): False,
    (1, 2): False,
    (1, 3): False,
    (1, 4): False,
    (2, 1): False,
    (2, 2): False,
    (2, 3): True,
    (2, 4): False,
    (3, 1): False,
    (3, 2): False,
    (3, 3): False,
    (3, 4): False,
    (4, 1): False,
    (4, 2): False,
    (4, 3): False,
    (4, 4): False
}

wumpus = {
    (1, 1): False,
    (1, 2): False,
    (1, 3): False,
    (1, 4): False,
    (2, 1): False,
    (2, 2): False,
    (2, 3): False,
    (2, 4): False,
    (3, 1): False,
    (3, 2): False,
    (3, 3): True,
    (3, 4): False,
    (4, 1): False,
    (4, 2): False,
    (4, 3): False,
    (4, 4): False
}


def neighbours(cell):
    x, y = cell
    result = []

    for dx, dy in [(1, 0), (-1, 0), (0, 1), (0, -1)]:
        nx = x + dx
        ny = y + dy

        if 1 <= nx <= 4 and 1 <= ny <= 4:
            result.append((nx, ny))

    return result


def get_percepts(cell):
    breeze = False
    stench = False

    for n in neighbours(cell):
        if pit[n]:
            breeze = True

        if wumpus[n]:
            stench = True

    return breeze, stench


def is_safe(cell):
    breeze, stench = get_percepts(cell)

    # A cell is safe if it has no pit and no Wumpus
    if not breeze and not stench:
        return True

    return False


# Start from [1,1]
current = (1, 1)
visited = set()
path = []

print("WUMPUS WORLD")
print("----------------")

while current != (4, 4):

    visited.add(current)
    path.append(current)

    breeze, stench = get_percepts(current)

    print("Current Room:", current)
    print("Breeze:", breeze)
    print("Stench:", stench)

    safe_moves = []

    for cell in neighbours(current):
        if cell not in visited and is_safe(cell):
            safe_moves.append(cell)

    if not safe_moves:
        print("No safe move available.")
        break

    # Choose the first safe room
    current = safe_moves[0]

    print("Moving to:", current)
    print()

# Add final room
if current == (4, 4):
    path.append(current)
    print("Agent reached the exit!")
else:
    print("Agent could not reach the exit.")

print()
print("Safe Path:", path)
```
<h3>output</h3>

<img width="681" height="816" alt="image" src="https://github.com/user-attachments/assets/5cbda106-1087-4578-9e14-2d2b8e0acdcf" />

<h3>Result</h3>
Thus, the Wumpus World Problem was successfully solved using Python by demonstrating inference from propositional logic.
