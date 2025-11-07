🧾  MPI Programs in Python

This folder has three simple MPI programs made using Python and the mpi4py library.
MPI (Message Passing Interface) helps different processes (like small programs) talk to each other at the same time — this is called parallel programming.

⚙️ How to Run

Before running any program:

Install mpi4py:

pip install mpi4py


Run the program using:

mpiexec -n <number_of_processes> python <filename>.py


Example:

mpiexec -n 4 python hello.py

👋 Program 1: Hello World (hello.py)
What it does:

This is the simplest MPI program.

It just prints a message from each process, showing its rank number.

Code:
from mpi4py import MPI
comm = MPI.COMM_WORLD
rank = comm.Get_rank()
print("Hello world from process", rank)

Example Output:

If you run with 4 processes:

Hello world from process 0
Hello world from process 1
Hello world from process 2
Hello world from process 3


👉 Each process prints its own hello message.

🔄 Program 2: Alltoall Communication (alltoall.py)
What it does:

Every process sends data to all other processes (including itself).

It’s like everyone sharing their own data with everyone else.

Code:
from mpi4py import MPI
import numpy

comm = MPI.COMM_WORLD
size = comm.Get_size()
rank = comm.Get_rank()

senddata = (rank + 1) * numpy.arange(size, dtype=int)
recvdata = numpy.empty(size, dtype=int)

comm.Alltoall(senddata, recvdata)

print(f"Process {rank} sending {senddata} receiving {recvdata}")

Example Output:
Process 0 sending [0 1 2 3] receiving [0 1 2 3]
Process 1 sending [0 2 4 6] receiving [0 2 4 6]
Process 2 sending [0 3 6 9] receiving [0 3 6 9]
Process 3 sending [0 4 8 12] receiving [0 4 8 12]


👉 Think of it as a group chat, where everyone shares their data with everyone else.

📬 Program 3: Point-to-Point Communication (point_to_point.py)
What it does:

This shows direct communication between specific processes.

One process sends a message, and another one receives it.

Code:
from mpi4py import MPI

comm = MPI.COMM_WORLD
rank = comm.rank
print("My rank is:", rank)

if rank == 0:
    data = 10000000
    comm.send(data, dest=4)
    print("Sending data", data, "to process 4")

if rank == 1:
    data = "hello"
    comm.send(data, dest=8)
    print("Sending data", data, "to process 8")

if rank == 4:
    data = comm.recv(source=0)
    print("Data received is =", data)

if rank == 8:
    data1 = comm.recv(source=1)
    print("Data1 received is =", data1)

Example Output:
My rank is: 0
Sending data 10000000 to process 4
My rank is: 4
Data received is = 10000000
My rank is: 1
Sending data hello to process 8
My rank is: 8
Data1 received is = hello


👉 Think of it like sending a private message between two specific people.
