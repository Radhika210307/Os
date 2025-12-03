# Os
1 Execute various LINUX commands for:
i. Information Maintenance: wc, clear, cal, who, date, pwd
ii. File Management: cat, cp, rm, mv, cmp, comm, diff, find, grep, awk
iii. Directory Management: cd, mkdir, rmdir, ls

2. Execute various LINUX commands for:
i. Process Control: fork, getpid, ps, kill, sleep
ii. Communication: Input-output redirection, Pipe
iii. Protection Management: chmod, chown, chgrp









✅ PROGRAM – 4

Write a program to report behaviour of Linux kernel (kernel version, CPU info, memory info)


```

PYTHON CODE

import platform
import os

print("Kernel Version:", platform.release())
print("Operating System:", platform.system(), platform.version())

print("\nCPU Info:")
os.system("lscpu")

print("\nMemory Info:")
os.system("free -m")


```

✅ PROGRAM – 5

Report configured memory, free & used memory


```

PYTHON CODE

import os

print("Memory Information:")
os.system("free -h")


```


✅ PROGRAM – 6

Write a program to copy file using system calls


```

PYTHON CODE

src = "file1.txt"
dst = "file2.txt"

with open(src, "rb") as f1:
    data = f1.read()

with open(dst, "wb") as f2:
    f2.write(data)

print("File copied successfully!")


```



  

✅ PROGRAM – 7

Implement FCFS Scheduling


```

PYTHON CODE

n = int(input("Enter number of processes: "))
bt = []
for i in range(n):
    bt.append(int(input(f"Enter burst time for P{i+1}: ")))

wt = [0]*n
tat = [0]*n

for i in range(1, n):
    wt[i] = wt[i-1] + bt[i-1]

for i in range(n):
    tat[i] = wt[i] + bt[i]

print("\nProcess  BT  WT  TAT")
for i in range(n):
    print(f"P{i+1}\t{bt[i]}\t{wt[i]}\t{tat[i]}")


```




✅ PROGRAM – 8

Implement SJF Scheduling


```

PYTHON CODE

n = int(input("Enter number of processes: "))
bt = []

for i in range(n):
    bt.append(int(input(f"Enter burst time of P{i+1}: ")))

process = list(range(1, n+1))

# sort by burst time
for i in range(n):
    for j in range(n-i-1):
        if bt[j] > bt[j+1]:
            bt[j], bt[j+1] = bt[j+1], bt[j]
            process[j], process[j+1] = process[j+1], process[j]

wt = [0]*n
tat = [0]*n

for i in range(1, n):
    wt[i] = wt[i-1] + bt[i-1]

for i in range(n):
    tat[i] = bt[i] + wt[i]

print("\nProc  BT  WT  TAT")
for i in range(n):
    print(f"P{process[i]}\t{bt[i]}\t{wt[i]}\t{tat[i]}")


```






✅ PROGRAM – 9

Implement Priority Scheduling


```

PYTHON CODE

n = int(input("Enter number of processes: "))
bt = []
priority = []

for i in range(n):
    bt.append(int(input(f"Burst time of P{i+1}: ")))
    priority.append(int(input(f"Priority of P{i+1}: ")))

process = list(range(1, n+1))

for i in range(n):
    for j in range(n-i-1):
        if priority[j] > priority[j+1]:
            priority[j], priority[j+1] = priority[j+1], priority[j]
            bt[j], bt[j+1] = bt[j+1], bt[j]
            process[j], process[j+1] = process[j+1], process[j]

wt = [0]*n
tat = [0]*n

for i in range(1, n):
    wt[i] = wt[i-1] + bt[i-1]

for i in range(n):
    tat[i] = wt[i] + bt[i]

print("\nP   BT  Priority  WT  TAT")
for i in range(n):
    print(f"P{process[i]}\t{bt[i]}\t{priority[i]}\t{wt[i]}\t{tat[i]}")


```


✅ PROGRAM – 10

Implement Round Robin Scheduling (Time Quantum = 2)


```

PYTHON CODE

bt = list(map(int, input("Enter burst times: ").split()))
n = len(bt)
qt = 2
rt = bt.copy()
t = 0

wt = [0]*n
tat = [0]*n

while True:
    done = True
    for i in range(n):
        if rt[i] > 0:
            done = False
            if rt[i] > qt:
                t += qt
                rt[i] -= qt
            else:
                t += rt[i]
                wt[i] = t - bt[i]
                rt[i] = 0

    if done:
        break

for i in range(n):
    tat[i] = wt[i] + bt[i]

print("BT  WT  TAT")
for i in range(n):
    print(bt[i], wt[i], tat[i])


```



✅ PROGRAM – 11

Calculate sum of ‘n’ numbers using 2 child processes


```

PYTHON CODE

import os

numbers = [1, 2, 3, 4, 5, 6]

pid = os.fork()

if pid == 0:
    print("Child 1 sum:", sum(numbers[:3]))
else:
    pid2 = os.fork()
    if pid2 == 0:
        print("Child 2 sum:", sum(numbers[3:]))
    else:
        os.wait()
        os.wait()


```



✅ PROGRAM – 12

Implement First Fit, Best Fit, Worst Fit Memory Allocation


```

PYTHON CODE

blocks = [100, 500, 200, 300, 600]
process = [212, 417, 112, 426]

def first_fit():
    b = blocks.copy()
    print("\nFIRST FIT")
    for p in process:
        for i in range(len(b)):
            if b[i] >= p:
                print(f"Process {p} allocated to block {b[i]}")
                b[i] -= p
                break

def best_fit():
    b = blocks.copy()
    print("\nBEST FIT")
    for p in process:
        best = -1
        for i in range(len(b)):
            if b[i] >= p:
                if best == -1 or b[i] < b[best]:
                    best = i
        if best != -1:
            print(f"Process {p} allocated to block {b[best]}")
            b[best] -= p

def worst_fit():
    b = blocks.copy()
    print("\nWORST FIT")
    for p in process:
        worst = -1
        for i in range(len(b)):
            if b[i] >= p:
                if worst == -1 or b[i] > b[worst]:
                    worst = i
        if worst != -1:
            print(f"Process {p} allocated to block {b[worst]}")
            b[worst] -= p

first_fit()
best_fit()
worst_fit()


```

Q3 3. Write a program (using fork () and/or exec () commands) where parent and child execute:
i. same program, same code.
ii. same program, different code.
iii. before terminating, the parent waits for the child to finish its task.
✔ C Code (Linux Terminal)



```
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>

int main() {
    pid_t pid = fork();

    if (pid < 0) {
        printf("Fork failed!\n");
        return 1;
    }
    else if (pid == 0) {
        printf("Child: Executing SAME code. PID = %d\n", getpid());
    }
    else {
        wait(NULL); // parent waits
        printf("Parent: Executing SAME code. PID = %d\n", getpid());
    }

    return 0;
}

✔ Output
Child पहले चलेगा → फिर Parent


```

✅ PART (ii) — Same Program, Different Code

(Parent & Child एक ही program के अंदर different code blocks चलाते हैं)

✔ C Code




```
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>

int main() {
    pid_t pid = fork();

    if (pid == 0) {
        printf("Child: I am running DIFFERENT code.\n");
    }
    else {
        wait(NULL);
        printf("Parent: I am running DIFFERENT code.\n");
    }

    return 0;
}

✔ अलग-अलग outputs मिलेंगे।


```

✅ PART (iii) — Parent waits until Child finishes

(Child अपना काम पूरा करे → Parent बाद में execute हो)


✔ C Code



```
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>

int main() {
    pid_t pid = fork();

    if (pid == 0) {
        printf("Child: Working...\n");
        sleep(2);      // child slow task
        printf("Child: Finished!\n");
    }
    else {
        wait(NULL);    // PARENT WAITS
        printf("Parent: Child finished, now I am ending.\n");
    }

    return 0;
}

```




