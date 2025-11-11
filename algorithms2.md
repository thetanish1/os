from collections import deque

# Process Data: [pid, arrival_time, burst_time, priority]
processes = [
    [1, 0, 5, 2],
    [2, 1, 3, 1],
    [3, 2, 8, 4],
    [4, 3, 6, 3]
]

def print_table(result, algo_name):
    print(f"\n===== {algo_name} Scheduling =====")
    print("PID\tAT\tBT\tWT\tTAT")
    total_wt, total_tat = 0, 0
    for p in result:
        total_wt += p['WT']
        total_tat += p['TAT']
        print(f"{p['PID']}\t{p['AT']}\t{p['BT']}\t{p['WT']}\t{p['TAT']}")
    n = len(result)
    print(f"Average Waiting Time: {total_wt/n:.2f}")
    print(f"Average Turnaround Time: {total_tat/n:.2f}")


# 1️⃣ FCFS (First Come First Serve)
def fcfs(processes):
    procs = sorted(processes, key=lambda x: x[1])
    time = 0
    result = []
    for p in procs:
        at, bt = p[1], p[2]
        if time < at:
            time = at
        wt = time - at
        tat = wt + bt
        time += bt
        result.append({'PID': p[0], 'AT': at, 'BT': bt, 'WT': wt, 'TAT': tat})
    print_table(result, "FCFS")


# 2️⃣ SJF (Shortest Job First) - Non Preemptive
def sjf(processes):
    procs = sorted(processes, key=lambda x: x[1])
    completed = []
    time = 0
    ready = []
    while procs or ready:
        # Add to ready queue if arrived
        while procs and procs[0][1] <= time:
            ready.append(procs.pop(0))
        if not ready:
            time = procs[0][1]
            continue
        ready.sort(key=lambda x: x[2])  # shortest burst first
        p = ready.pop(0)
        at, bt = p[1], p[2]
        wt = time - at
        tat = wt + bt
        time += bt
        completed.append({'PID': p[0], 'AT': at, 'BT': bt, 'WT': wt, 'TAT': tat})
    print_table(completed, "SJF (Non-Preemptive)")


# 3️⃣ Round Robin
def round_robin(processes, quantum=2):
    procs = [dict(PID=p[0], AT=p[1], BT=p[2], RT=p[2]) for p in processes]
    ready = deque()
    time = 0
    result = []
    visited = set()
    while procs or ready:
        # Move arrived processes to ready queue
        for p in list(procs):
            if p['AT'] <= time and p['PID'] not in visited:
                ready.append(p)
                visited.add(p['PID'])
        if not ready:
            time += 1
            continue
        p = ready.popleft()
        exec_time = min(p['RT'], quantum)
        p['RT'] -= exec_time
        time += exec_time
        # Check for newly arrived processes
        for x in list(procs):
            if x['AT'] <= time and x['PID'] not in visited:
                ready.append(x)
                visited.add(x['PID'])
        if p['RT'] == 0:
            tat = time - p['AT']
            wt = tat - p['BT']
            result.append({'PID': p['PID'], 'AT': p['AT'], 'BT': p['BT'], 'WT': wt, 'TAT': tat})
            procs = [x for x in procs if x['PID'] != p['PID']]
        else:
            ready.append(p)
    print_table(result, f"Round Robin (Quantum={quantum})")


# 4️⃣ Priority Scheduling (Non Preemptive)
def priority_scheduling(processes):
    procs = sorted(processes, key=lambda x: x[1])  # sort by arrival
    completed = []
    time = 0
    ready = []
    while procs or ready:
        while procs and procs[0][1] <= time:
            ready.append(procs.pop(0))
        if not ready:
            time = procs[0][1]
            continue
        ready.sort(key=lambda x: x[3])  # lower number = higher priority
        p = ready.pop(0)
        at, bt, pr = p[1], p[2], p[3]
        wt = time - at
        tat = wt + bt
        time += bt
        completed.append({'PID': p[0], 'AT': at, 'BT': bt, 'WT': wt, 'TAT': tat, 'PR': pr})
    print_table(completed, "Priority Scheduling")


# Run all algorithms
fcfs(processes)
sjf(processes)
round_robin(processes, quantum=2)
priority_scheduling(processes)
