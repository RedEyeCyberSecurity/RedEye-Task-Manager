# RedEye-Task-Manager
RedEye-Task Manager


How to Run

git clone https://github.com/RedEyeCyberSecurity/RedEye-Task-Manager.git
cd simple-task-manager

Install dependencies (if not already installed):
pip install psutil


python app.py

## 🚀 Features

- 🖥️ **Process List Display**  
  View all active processes in real-time with their **PID** and **Name**.

- 🔄 **Refresh Process List**  
  Always stay updated with the latest running processes.

- ❌ **Terminate Processes**  
  Kill unwanted or problematic processes directly from the GUI.

- 🛡️ **Error Handling**  
  Handle permission issues, process access errors, and ensure a smooth user experience.

- 📊 **Cross-platform Support**  
  Built with [psutil](https://pypi.org/project/psutil/) for compatibility across **Windows, Linux, and macOS**.


```python
import tkinter as tk
from tkinter import messagebox
import psutil


# Function to refresh the process list
def refresh_process_list():
    # Clear the listbox
    process_listbox.delete(0, tk.END)

    # Populate the listbox with active processes
    for process in psutil.process_iter(['pid', 'name']):
        try:
            process_listbox.insert(tk.END, f"PID: {process.info['pid']} | Name: {process.info['name']}")
        except (psutil.NoSuchProcess, psutil.AccessDenied, psutil.ZombieProcess):
            pass


# Function to terminate selected process
def terminate_process():
    try:
        selected_item = process_listbox.get(tk.ACTIVE)
        pid = int(selected_item.split("|")[0].split(":")[1].strip())

        # Find the process by PID and terminate
        proc = psutil.Process(pid)
        proc.terminate()
        messagebox.showinfo("Success", f"Terminated Process: {proc.name()} (PID: {pid})")
    except Exception as e:
        messagebox.showerror("Error", f"Could not terminate process: {e}")


# Create GUI window
window = tk.Tk()
window.title("Simple Task Manager")
window.geometry("700x400")

# UI Widgets
tk.Label(window, text="Task Manager - Active Processes", font=("Arial", 14)).pack(pady=10)

# Scrollable listbox
process_listbox = tk.Listbox(window, selectmode=tk.SINGLE, width=80, height=15)
process_listbox.pack(pady=5)

# Buttons
tk.Button(window, text="Refresh Processes", command=refresh_process_list).pack(pady=5)
tk.Button(window, text="Terminate Process", command=terminate_process).pack(pady=5)

# Initial refresh
refresh_process_list()

# Main loop
window.mainloop()
```

 Why This Project?
This simple task manager demonstrates the following:

How to use psutil for real-time system monitoring.
GUI development with Tkinter.
Process management, including termination and monitoring.
It serves as a great educational tool for learning process management, ethical hacking simulations, and system monitoring.
