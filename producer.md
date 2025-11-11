import threading
import time
import random

BUFFER_SIZE = 5
buffer = []

# Semaphores
mutex = threading.Semaphore(1)         
empty = threading.Semaphore(BUFFER_SIZE)  
full = threading.Semaphore(0)         

def producer():
    item_id = 1
    while True:
        time.sleep(random.uniform(0.5, 2))  
        item = f"Item-{item_id}"
        empty.acquire()                    
        mutex.acquire()                   
        buffer.append(item)
        print(f"[Producer] Produced {item} | Buffer: {buffer}")
        mutex.release()                    
        full.release()                     
        item_id += 1

def consumer():
    while True:
        full.acquire()                      
        mutex.acquire()                     
        item = buffer.pop(0)
        print(f"   [Consumer] Consumed {item} | Buffer: {buffer}")
        mutex.release()                     
        empty.release()                    
        time.sleep(random.uniform(1, 2.5))   

producer_thread = threading.Thread(target=producer)
consumer_thread = threading.Thread(target=consumer)

producer_thread.start()
consumer_thread.start()

producer_thread.join()
consumer_thread.join()
