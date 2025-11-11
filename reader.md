import threading
import time
import random

readcount = 0
mutex = threading.Semaphore(1)
wrt = threading.Semaphore(1)

def reader(reader_id):
    global readcount
    while True:
        time.sleep(random.uniform(0.5, 2))
        mutex.acquire()
        readcount += 1
        if readcount == 1:
            wrt.acquire()
        mutex.release()
        print(f"Reader {reader_id} is reading")
        time.sleep(random.uniform(0.5, 1.5))
        mutex.acquire()
        readcount -= 1
        if readcount == 0:
            wrt.release()
        mutex.release()
        print(f"Reader {reader_id} finished reading")

def writer(writer_id):
    while True:
        time.sleep(random.uniform(1, 3))
        wrt.acquire()
        print(f"Writer {writer_id} is writing")
        time.sleep(random.uniform(1, 2))
        wrt.release()
        print(f"Writer {writer_id} finished writing")

readers = [threading.Thread(target=reader, args=(i,)) for i in range(1, 4)]
writers = [threading.Thread(target=writer, args=(i,)) for i in range(1, 3)]

for t in readers + writers:
    t.start()

for t in readers + writers:
    t.join()
