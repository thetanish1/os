from collections import deque

pages = [7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2]
frame_size = 3

def fifo(pages, frame_size):
    frame = deque()
    faults = 0
    for p in pages:
        if p not in frame:
            faults += 1
            if len(frame) == frame_size:
                frame.popleft()
            frame.append(p)
        print(f"Page: {p} | Frame: {list(frame)}")
    print(f"Total Page Faults (FIFO): {faults}\n")

def lru(pages, frame_size):
    frame = []
    recent = {}
    faults = 0
    for i, p in enumerate(pages):
        if p not in frame:
            faults += 1
            if len(frame) < frame_size:
                frame.append(p)
            else:
                lru_page = min(recent, key=recent.get)
                frame[frame.index(lru_page)] = p
                del recent[lru_page]
        recent[p] = i
        print(f"Page: {p} | Frame: {frame}")
    print(f"Total Page Faults (LRU): {faults}\n")

fifo(pages, frame_size)
lru(pages, frame_size)
