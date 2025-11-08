Locks, RLocks, and Semaphores in Python (Thread Synchronization)

This project shows how Python handles multiple threads safely using three different synchronization tools:
👉 Lock, RLock (Reentrant Lock), and Semaphore.

These are used to control how threads share resources, so they don’t cause conflicts or unexpected behavior when running at the same time.

🧠 What You’ll Learn

When multiple threads run together, they may try to:

Print to the screen at the same time

Change shared data at once

Cause unexpected results

To prevent this, we use thread synchronization tools — they help threads wait their turn.

This project has 3 examples:

🔐 Lock Example

🔁 RLock Example

🚦 Semaphore Example

1️⃣ Lock Example (threadLock)
📄 File: lock_example.py
🧩 What It Does

Creates 9 threads

Each thread prints messages and waits for a few seconds

A Lock ensures only one thread prints at a time

💡 Why Use Lock?

When multiple threads print at the same time, outputs can get mixed up.
The lock makes each thread wait until the other finishes.

⚙️ How It Works
threadLock = threading.Lock()

threadLock.acquire()   # Lock taken by one thread
print("Thread running...")
time.sleep(duration)
threadLock.release()   # Lock released so another thread can run


Each thread locks the section when running and releases it when done.

🧪 Output Example
---> Thread#1 running...
---> Thread#1 over
---> Thread#2 running...
---> Thread#2 over
...
End
--- 12.432 seconds ---


✅ Result: Only one thread prints at a time (no mixing).

2️⃣ RLock Example (Reentrant Lock)
📄 File: rlock_example.py
🧩 What It Does

Has a shared Box that stores item count

Two threads:

One adds items

One removes items

Uses an RLock to manage access to shared data

💡 Why Use RLock?

An RLock allows a thread to lock the same section multiple times safely.
This is useful when a function with a lock calls another function that also has a lock.

⚙️ How It Works
self.lock = threading.RLock()

def execute(self, value):
    with self.lock:
        self.total_items += value

def add(self):
    with self.lock:
        self.execute(1)


Here, add() calls execute() — both use the same lock, and RLock prevents deadlock.

🧪 Output Example
N° 15 items to ADD
ADDED one item --> 14 items to ADD
N° 6 items to REMOVE
REMOVED one item --> 5 items to REMOVE
...


✅ Result: Threads can safely add and remove items without crashing.

3️⃣ Semaphore Example
📄 File: semaphore_example.py
🧩 What It Does

Simulates a producer-consumer problem

Producer makes an item

Consumer waits for an item

Both run using threads and a Semaphore

💡 Why Use Semaphore?

A Semaphore controls how many threads can access a shared resource at the same time.
It’s like a signal:

🚦 Red = Wait

🟢 Green = Go

In this case:

Consumer waits until the producer produces something

Once ready, the producer releases the semaphore

⚙️ How It Works
semaphore = threading.Semaphore(0)

def consumer():
    semaphore.acquire()  # Waits for producer
    print("Consumer got item")

def producer():
    semaphore.release()  # Signals consumer
    print("Producer created item")

🧪 Output Example
Consumer is waiting
Producer notify: item number 543
Consumer notify: item number 543


✅ Result: The consumer waits until the producer is ready — no race condition.
