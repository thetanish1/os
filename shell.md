import os
import subprocess

while True:
    command = input("myshell> ").strip()
    if command.lower() in ["exit", "quit"]:
        print("Exiting shell...")
        break
    if command == "":
        continue
    try:
        result = subprocess.run(command, shell=True, check=True, text=True, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
        print(result.stdout, end="")
        if result.stderr:
            print(result.stderr, end="")
    except subprocess.CalledProcessError as e:
        print(f"Error: {e}")
