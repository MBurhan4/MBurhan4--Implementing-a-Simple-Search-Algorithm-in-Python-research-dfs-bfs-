# MBurhan4--Implementing-a-Simple-Search-Algorithm-in-Python-research-dfs-bfs-

# Task

1. Research the Depth-First Search (DFS) & Breadth First Search (BFS)Algorithms.
2. Apply DFS and BFS on Romanian example
3. The program should take as input a graph and represents an adjacency list along with
source and goal nodes.
4. The program should output the shortest path or optimize path from source to the goal
node.
5. Also highlight which of the algorithm outperform other.

# Explanation;
Depth-First Search (DFS) and Breadth-First Search (BFS) are two popular graph traversal algorithms used in computer science.
DFS is a recursive algorithm that traverses a graph by visiting the deepest node first and then backtracking to visit the remaining nodes. It starts from the source node and goes as deep as possible, and then backtracks if it reaches a dead end. DFS is often implemented using a stack data structure.

BFS, on the other hand, is a non-recursive algorithm that traverses a graph by visiting all the nodes at the current depth before moving on to the next level. It starts from the source node and visits all the nodes at distance 1 from the source, then all the nodes at distance 2, and so on. BFS is typically implemented using a queue data structure

# Python code;
 
 from queue import Queue

def dfs(graph, source, goal, visited=None, path=None):
    if visited is None:
        visited = set()
    if path is None:
        path = []
    visited.add(source)
    path.append(source)
    if source == goal:
        return path
    for neighbor, distance in graph[source].items():
        if neighbor not in visited:
            new_path = dfs(graph, neighbor, goal, visited, path)
            if new_path:
                return new_path
    return None

def bfs(graph, source, goal):
    queue = Queue()
    visited = set()
    path = []
    queue.put([source])
    visited.add(source)
    while not queue.empty():
        path = queue.get()
        current_node = path[-1]
        if current_node == goal:
            return path
        for neighbor, distance in graph[current_node].items():
            if neighbor not in visited:
                new_path = list(path)
                new_path.append(neighbor)
                queue.put(new_path)
                visited.add(neighbor)
    return None

# Sample adjacency list representation of the Romania map
graph = {
    'Arad': {'Zerind': 75, 'Sibiu': 140, 'Timisoara': 118},
    'Zerind': {'Arad': 75, 'Oradea': 71},
    'Oradea': {'Zerind': 71, 'Sibiu': 151},
    'Sibiu': {'Arad': 140, 'Oradea': 151, 'Fagaras': 99, 'Rimnicu Vilcea': 80},
    'Timisoara': {'Arad': 118, 'Lugoj': 111},
    'Lugoj': {'Timisoara': 111, 'Mehadia': 70},
    'Mehadia': {'Lugoj': 70, 'Drobeta': 75},
    'Drobeta': {'Mehadia': 75, 'Craiova': 120},
    'Craiova': {'Drobeta': 120, 'Rimnicu Vilcea': 146, 'Pitesti': 138},
    'Rimnicu Vilcea': {'Sibiu': 80, 'Craiova': 146, 'Pitesti': 97},
    'Fagaras': {'Sibiu': 99, 'Bucharest': 211},
    'Pitesti': {'Rimnicu Vilcea': 97, 'Craiova': 138, 'Bucharest': 101},
    'Bucharest': {'Fagaras': 211, 'Pitesti': 101, 'Giurgiu': 90, 'Urziceni': 85},
    'Giurgiu': {'Bucharest': 90},
    'Urziceni': {'Bucharest': 85, 'Vaslui': 142, 'Hirsova': 98},
    'Vaslui': {'Urziceni': 142, 'Iasi': 92},
    'Iasi': {'Vaslui': 92, 'Neamt': 87},
    'Neamt': {'Iasi': 87}
}

source = 'Arad'
goal = 'Bucharest'

print("DFS path:", dfs(graph, source, goal))
print("BFS path:", bfs(graph, source, goal))

