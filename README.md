# xv6-lottery-scheduling

Implement and test  lottery scheduling , a randomized algorithm that allows processes to receive a proportional share of the CPU without explicitly tracking how long each process has been run.

Specifically, you should modify xv6 so that:
1. Each  struct proc  has an additional field,  tickets , that tracks how many tickets it has.
2. New processes are assigned  10  lottery tickets when they are created.
3. When the scheduler runs, it picks a random number between 0 and the total number of
tickets. It then uses the algorithm described in class to loop over runnable processes and
pick the one with the winning ticket.
4. User processes have a new system call,  settickets , that allows a process to specify
how many lottery tickets it wants. Normally this would be a bad idea, since it would let a process hog the CPU by specifying an arbitrary number of tickets -- but xv6 has no security anyway, so this is not that big a deal.

### Hints:
1. One possible way to track the total number of tickets is by carefully finding each place where the process state changes, and adding or subtracting tickets from a global as appropriate. However, this is actually rather tricky to get right. An alternative is to simply compute the number of tickets each time we enter the scheduler loop, before choosing the winning ticket.
2. Right now, the scheduler loop picks up where it left off after scheduling a process -- so if it finds a runnable process at index  i , the next time the scheduler runs it will keep going through the list at index  i+1 . In order to make the lottery algorithm work, you will need to restructure the scheduler loop so that it starts back at the beginning of the list every time we return to the scheduler.
3. No changes are needed to the process list itself; you can continue to use the ptable.proc  array (i.e., you don't have to implement a process queue).
4. You can consult the slides to find out how to add a new system call when adding settickets  .
5. The use of gdb to debug your code is highly encouraged.
6. If you want to see the list of running processes at any time, you can type  Control-p  at
the xv6 console and it will print out a list of running processes. You may also want to modify this function ( procdump  in  proc.c ) to print out the number of tickets each process has so that you can debug your  settickets  call.
