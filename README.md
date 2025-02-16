
# A* Search Algorithm

This repository contains a Python implementation of the **A* Search Algorithm** to find the shortest path from a start node to a goal node using heuristic values and path cost.

## 📌 Overview
The **A* Search Algorithm** selects the next node based on the lowest **f-cost**, where:
- **f(n) = g(n) + h(n)**
- **g(n)**: Cost from the start node to the current node.
- **h(n)**: Estimated cost from the current node to the goal.

## 🚀 Features
- Implements **A* Search Algorithm**.
- Uses a **graph representation** with predefined **heuristic values**.
- Finds the optimal path to the goal.
- Outputs the sequence of nodes visited and the total cost.

## 📂 Project Structure
```
.
├── a_star_search.py    # Main script containing the algorithm
├── README.md           # Project documentation
```

## 📝 Algorithm Explanation
1. **Graph Representation**: The problem is represented as a dictionary where keys are nodes and values are lists of adjacent nodes with their respective path costs.
2. **Heuristic Function**: Each node has an associated heuristic value representing an estimate of the cost to reach the goal.
3. **Search Process**:
   - Start from the initial node.
   - Select the node with the **lowest f(n) = g(n) + h(n)**.
   - Repeat until the goal is reached or no more moves are possible.

## 🖥️ Code Implementation
```python
# Define the graph
graph = {
    'S': [('A', 1), ('G', 10)],
    'A': [('B', 2), ('C', 1)],
    'B': [('D', 5)],
    'C': [('D', 3), ('G', 4)],
    'D': [('G', 1)],
    'G': []
}

# Define heuristic values
heuristic = {
    'S': 5, 'A': 3, 'B': 4, 'C': 2, 'D': 6, 'G': 0
}

def find_min_f(open_list, g_values):
    min_node = open_list[0]
    min_f = g_values[min_node] + heuristic[min_node]

    for node in open_list:
        f_value = g_values[node] + heuristic[node]
        if f_value < min_f:
            min_f = f_value
            min_node = node
    return min_node

def a_star(start, goal):
    open_list = [start]  # Nodes to explore
    closed_list = []     # Explored nodes
    g_values = {start: 0}  # Cost from start to each node
    parent = {start: None} # To track the path

    while open_list:
        current = find_min_f(open_list, g_values)
        open_list.remove(current)
        closed_list.append(current)
        print(f"Visiting: {current}")

        if current == goal:
            path = []
            while current is not None:
                path.append(current)
                current = parent[current]
            path.reverse()
            print("Goal Reached!")
            print("Path:", " -> ".join(path))
            print("Cost:", g_values[goal])
            return

        for neighbor, cost in graph[current]:
            if neighbor in closed_list:
                continue
            tentative_g = g_values[current] + cost
            if neighbor not in open_list:
                open_list.append(neighbor)
            elif tentative_g >= g_values.get(neighbor, float('inf')):
                continue
            parent[neighbor] = current
            g_values[neighbor] = tentative_g

    print("Goal not reachable.")

a_star('S', 'G')
```

## 🛠️ Installation & Usage
1. **Clone the Repository**
```sh
git clone https://github.com/your-username/a-star-search.git
cd a-star-search
```

2. **Run the Script**
```sh
python a_star_search.py
```

## 🎯 Example Output
```
Visiting: S
Visiting: A
Visiting: C
Visiting: G
Goal Reached!
Path: S -> A -> C -> G
Cost: 6
```

## 📌 Limitations
- Requires a well-defined heuristic to perform efficiently.
- May consume more memory compared to other search algorithms.



---
Happy Coding! 🚀

