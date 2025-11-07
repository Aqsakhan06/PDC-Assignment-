⚡ Multiprocessing vs Multithreading in Python

This project shows how Python runs tasks faster or slower when using multiple processes or multiple threads.
It helps you understand which one is better when your program needs a lot of CPU work (like heavy calculations).

🧠 What This Program Does

The code runs a CPU-heavy task — it calculates the sum of squares (like 1² + 2² + 3² …).
It runs this same task in two ways:

Using multiprocessing (many processes)

Using multithreading (many threads)

Then it measures how long each one takes to finish.

⚙️ How It Works
1. The main calculation
def heavy_calculation(n):
    total = 0
    for i in range(n):
        total += i * i
    return total


This is a CPU-heavy function — it does a lot of math work.

2. Running the task
def run_task(task_id, n):
    heavy_calculation(n)


Each process or thread runs this same task.

3. Running with different numbers

The code tests with:

sizes = [5, 10, 15]  # number of threads or processes
workload = 10_000_000  # how heavy the work is


For each number of workers:

It first uses processes

Then uses threads

And prints how long both take

🧩 What Happens Step by Step

It creates multiple workers (threads or processes)

Starts all of them

Waits until all finish

Prints the time taken

🧪 Example Output
===== Running with 5 PROCESSES =====
Multiprocessing (5 processes) time = 4.53 seconds

===== Running with 5 THREADS =====
Multithreading (5 threads) time = 11.87 seconds


(Your results may be different depending on your computer.)

💡 What You Learn

Multiprocessing runs faster for CPU-heavy work because:

Each process uses its own CPU core.

It can truly run tasks at the same time.

Multithreading is slower for CPU-heavy work because:

Python only allows one thread to run at a time (because of something called the GIL).

Threads take turns using the CPU instead of running together.

✅ In short:

Use multiprocessing for heavy math or CPU work.

Use multithreading for waiting tasks (like downloading files or reading data).
