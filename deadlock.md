graph = {
    'P1': ['R1'],
    'P2': ['R2'],
    'R1': ['P2'],
    'R2': ['P1']
}

visited = set()
rec_stack = set()

def is_cyclic(v):
    visited.add(v)
    rec_stack.add(v)
    if v in graph:
        for neighbour in graph[v]:
            if neighbour not in visited:
                if is_cyclic(neighbour):
                    return True
            elif neighbour in rec_stack:
                return True
    rec_stack.remove(v)
    return False

deadlock = False
for node in graph:
    if node not in visited:
        if is_cyclic(node):
            deadlock = True
            break

if deadlock:
    print("System is in Deadlock State")
else:
    print("No Deadlock Detected")
