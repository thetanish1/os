import os

print(f"Before fork: Current PID = {os.getpid()}")

pid = os.fork()  # Create a new process

if pid == 0:
    print(f"Child Process:\n   PID = {os.getpid()}\n   Parent PID = {os.getppid()}")
else:
    print(f"Parent Process:\n   PID = {os.getpid()}\n   Child PID = {pid}")
