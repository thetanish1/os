import os
import stat

dir_name = "Test_Dir"

if not os.path.exists(dir_name):
    os.mkdir(dir_name)
    print(f"Directory '{dir_name}' created.")
else:
    print(f"Directory '{dir_name}' already exists.")

os.chmod(dir_name, stat.S_IREAD)
print(f"Permissions changed: '{dir_name}' is now Read-Only.")

os.chmod(dir_name, stat.S_IWRITE)
print(f"Permissions changed: '{dir_name}' is now Writable.")

os.rmdir(dir_name)
print(f"Directory '{dir_name}' deleted.")
