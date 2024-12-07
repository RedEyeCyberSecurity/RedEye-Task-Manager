# RedEye-Task-Manager
RedEye-Task Manager



Code Overview
Here’s how the features are implemented:

🛠️ 1. View Active Processes
Processes are fetched using psutil.process_iter() and dynamically updated in the Listbox on every refresh.

🔄 2. Refresh Process List
The Refresh Processes button uses the psutil.process_iter() to query real-time processes and repopulate the Listbox.

❌ 3. Terminate Process
You can terminate a process by selecting it in the process list and clicking Terminate Process.
