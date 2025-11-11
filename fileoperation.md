import os

filename = "sample.txt"

with open(filename, "w") as f:
    f.write("Hello, this is a sample file.\nThis file is created for OS Lab.\n")

with open(filename, "r") as f:
    content = f.read()
    print("File Content:\n", content)

if os.path.exists(filename):
    os.remove(filename)
    print(f"{filename} deleted successfully.")
else:
    print("File does not exist.")
