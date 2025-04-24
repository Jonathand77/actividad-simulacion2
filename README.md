# 🚀 Actividad de Seguimiento - Simulación 2

## 👥 Integrantes

| 👨‍💻 Nombre | 📧 Correo | 🐙 Usuario GitHub |
|---|---|---|
| **Jonathan David Fernandez Vargas** | jonathand.fernandez@udea.edu.co | [jonathand77](https://github.com/jonathand77) |
| **Valeria Alvarez Fernandez** | valeria.alvarezf@udea.edu.co | [vaf88](https://github.com/vaf88) |

---

## 📜 Instrucciones

Antes de empezar a realizar esta actividad haga un **fork** de este repositorio y sobre este trabaje en la solución de las preguntas planteadas en la actividad de simulación. Las respuestas deben ser respondidas en español o si lo prefiere en ingles en el lugar señalado para ello (La palabra **answer** muestra donde).

---

## 🏡 Homework (Simulation)

This program, [mlfq.py](mlfq.py), allows you to see how the MLFQ scheduler presented in this chapter behaves. See the [README](https://github.com/remzi-arpacidusseau/ostep-homework/blob/master/cpu-sched-mlfq/README.md) for details.

### 📝 Questions

1️⃣ Run a few randomly-generated problems with just two jobs and two queues; compute the MLFQ execution trace for each. Make your life easier by limiting the length of each job and turning off I/Os.
   
   <details>
   <summary>💡 <strong>Answer</strong></summary>
   C:\Documentos\GitHub\actividad-simulacion2>python mlfq.py -n 2 -l 0,5,0:1,3,0 -m 0 -i 0 -M 0
Here is the list of inputs:
OPTIONS jobs 2
OPTIONS queues 2
OPTIONS allotments for queue  1 is   1
OPTIONS quantum length for queue  1 is  10
OPTIONS allotments for queue  0 is   1
OPTIONS quantum length for queue  0 is  10
OPTIONS boost 0
OPTIONS ioTime 0
OPTIONS stayAfterIO False
OPTIONS iobump False


For each job, three defining characteristics are given:
  startTime : at what time does the job enter the system
  runTime   : the total CPU time needed by the job to finish
  ioFreq    : every ioFreq time units, the job issues an I/O
              (the I/O takes ioTime units to complete)

Job List:
  Job  0: startTime   0 - runTime   5 - ioFreq   0
  Job  1: startTime   1 - runTime   3 - ioFreq   0

Compute the execution trace for the given workloads.
If you would like, also compute the response and turnaround
times for each of the jobs.

Use the -c flag to get the exact results when you are finished.
      
   1. Several scenarios have been run with two processes and two MLFQ scheduling queues, limiting the duration of each process to a maximum of 5 ticks and disabling I/O operations (ioFreq = 0). One scenario is presented below:

   ✅ ✅ Configuration:

2 queues (-n 2)

Job 0: starts at t=0, lasts 5 ticks

Job 1: starts at t=1, lasts 3 ticks

No I/O (ioFreq = 0, ioTime = 0)

Quantum = 10 in both queues

Allotment = 1 (only one turn at each level before demoting)

✅ Waited execution:

At t=0, Job 0 enters and executes until t=1.

At t=1, Job 1 arrives, but Job 0 continues its quantum, so Job 1 waits.

Job 0 exhausts its allocation and lowers its priority.

Job 1 enters queue 0 and executes completely.

Job 0 then resumes and terminates.

📌 Result:

You can see how MLFQ reorders its priority when it exhausts its allocation.

The jobs complete successfully and without I/O.
   </details>
   <br>
   
---

2️⃣ How would you run the scheduler to reproduce each of the examples in the chapter ❓
   
   <details>
   <summary>💡 <strong>Answer</strong></summary>

   C:\Documentos\GitHub\actividad-simulacion2>python mlfq.py -n 2 -l 0,20,0:5,5,0 -m 0 -i 0 -M 0
Here is the list of inputs:
OPTIONS jobs 2
OPTIONS queues 2
OPTIONS allotments for queue  1 is   1
OPTIONS quantum length for queue  1 is  10
OPTIONS allotments for queue  0 is   1
OPTIONS quantum length for queue  0 is  10
OPTIONS boost 0
OPTIONS ioTime 0
OPTIONS stayAfterIO False
OPTIONS iobump False


For each job, three defining characteristics are given:
  startTime : at what time does the job enter the system
  runTime   : the total CPU time needed by the job to finish
  ioFreq    : every ioFreq time units, the job issues an I/O
              (the I/O takes ioTime units to complete)

Job List:
  Job  0: startTime   0 - runTime  20 - ioFreq   0
  Job  1: startTime   5 - runTime   5 - ioFreq   0

Compute the execution trace for the given workloads.
If you would like, also compute the response and turnaround
times for each of the jobs.

Use the -c flag to get the exact results when you are finished.
   
   1. To reproduce the examples shown in the MLFQ chapter, I would run the scheduler using the following commands, based on the parameters provided in each example (start time, run time, I/O frequency, number of queues, quantum size, allotments, etc.). Here's one example:

   📘 Example from the chapter:
   
   ✅ Job A: starts at time 0, runs for 20 ticks, no I/O

   ✅ Job B: starts at time 5, runs for 5 ticks, no I/O

   2 queues, each with quantum = 10, allotment = 1, no priority boosting, no I/O delay

   Command:

   python mlfq.py -n 2 -l 0,20,0:5,5,0 -m 0 -i 0 -M 0
   
   ✅ This command sets up:

   -n 2: two queues

   -l 0,20,0:5,5,0: job list with two jobs

   -m 0: no boosting

   -i 0: I/O time is zero

   -M 0: I/O bump is off

   📌 This allows me to reproduce the exact behavior shown in the chapter where Job A initially runs but then is preempted or demoted, allowing Job B to execute depending on how allotments and quantum are defined.
   </details>
   <br>
   
---

 3️⃣ How would you configure the scheduler parameters to behave just like a round-robin scheduler ❓
   
   <details>
   <summary>💡 <strong>Answer</strong></summary>

   C:\Documentos\GitHub\actividad-simulacion2>python mlfq.py -n 1 -l 0,10,0:10,10,0 -m 0 -i 0 -M 0
Here is the list of inputs:
OPTIONS jobs 2
OPTIONS queues 1
OPTIONS allotments for queue  0 is   1
OPTIONS quantum length for queue  0 is  10
OPTIONS boost 0
OPTIONS ioTime 0
OPTIONS stayAfterIO False
OPTIONS iobump False


For each job, three defining characteristics are given:
  startTime : at what time does the job enter the system
  runTime   : the total CPU time needed by the job to finish
  ioFreq    : every ioFreq time units, the job issues an I/O
              (the I/O takes ioTime units to complete)

Job List:
  Job  0: startTime   0 - runTime  10 - ioFreq   0
  Job  1: startTime  10 - runTime  10 - ioFreq   0

Compute the execution trace for the given workloads.
If you would like, also compute the response and turnaround
times for each of the jobs.

Use the -c flag to get the exact results when you are finished.
      
   ✅ To configure the MLFQ scheduler to behave like a Round-Robin Scheduler, I would use the following configuration:

   Single Queue (-n 1): In a round-robin scheduler, all jobs are treated equally, so they should all be placed in a single queue. This ensures that no job is promoted or demoted to another queue.

   Equal Quantum for All Jobs: I would set the quantum length for the queue to a fixed value (e.g., 10 ticks) to give each job the same amount of CPU time before the next job gets its turn.

   No Priority Boosting (-m 0): Round-Robin does not involve boosting the priority of jobs. Therefore, priority boosting should be disabled by setting -m 0.

   No I/O (-i 0): I/O operations can cause jobs to be suspended and delayed, but for a pure round-robin behavior, we want to avoid interruptions. So, I set the I/O time to zero.

   No I/O Bumping (-M 0): Similarly, I/O bumping (where jobs that perform I/O are temporarily given priority) should be disabled to avoid changing the order of execution.

   Example Command:
   
   python mlfq.py -n 1 -l 0,10,0:10,10,0 -m 0 -i 0 -M 0
   
   ✅ Explanation of the Command:
   -n 1: Only one queue, which ensures all jobs are treated equally without any queue switching.

   -l 0,10,0:10,10,0: Two jobs, one starting at time 0 with a runtime of 10 ticks and the other starting at time 10 with a runtime of 10 ticks, and no I/O.

   -m 0: No priority boosting.

   -i 0: No I/O operations.

   -M 0: No I/O bumping.

   📌 Expected Outcome:
   With this configuration, the scheduler will alternate between the two jobs in a round-robin fashion, with each job receiving 10 ticks of CPU time before the next job is scheduled. This simulates the behavior     of a round-robin scheduler.
   </details>
   <br>
   
---

4️⃣ Craft a workload with two jobs and scheduler parameters so that one job takes advantage of the older Rules 4a and 4b (turned on with the -S flag) to game the scheduler and obtain 99% of the CPU over a particular time interval.
   
   <details>
   <summary>💡 <strong>Answer</strong></summary>

   C:\Documentos\GitHub\actividad-simulacion2>python mlfq.py -n 2 -l 0,50,0:5,5,0 -S -m 0 -i 0 -M 0
Here is the list of inputs:
OPTIONS jobs 2
OPTIONS queues 2
OPTIONS allotments for queue  1 is   1
OPTIONS quantum length for queue  1 is  10
OPTIONS allotments for queue  0 is   1
OPTIONS quantum length for queue  0 is  10
OPTIONS boost 0
OPTIONS ioTime 0
OPTIONS stayAfterIO True
OPTIONS iobump False


For each job, three defining characteristics are given:
  startTime : at what time does the job enter the system
  runTime   : the total CPU time needed by the job to finish
  ioFreq    : every ioFreq time units, the job issues an I/O
              (the I/O takes ioTime units to complete)

Job List:
  Job  0: startTime   0 - runTime  50 - ioFreq   0
  Job  1: startTime   5 - runTime   5 - ioFreq   0

Compute the execution trace for the given workloads.
If you would like, also compute the response and turnaround
times for each of the jobs.

Use the -c flag to get the exact results when you are finished.
      
   ✅ To configure a workload where a job takes advantage of Rules 4a and 4b and obtains 99% of the CPU time, I performed the following:

   1. Job Configuration:

   ✅ Job 1 (Job 0): Starts at time 0 and has a runtime of 50 CPU time units. This job performs no I/O operations (the ioFreq parameter is 0). By not performing I/O, it can take advantage of rules 4a and 4b, which allow a job without I/O to obtain more CPU time.

✅ Job 2 (Job 1): Starts at time 5 and has a runtime of only 5 CPU time units. It also performs no I/O.

2. Scheduler Parameters:

✅ I used two queues (-n 2), where both jobs compete for CPU time. Queue 0 has a higher priority, allowing the non-I/O job (Job 1) to get more CPU time due to rules 4a and 4b.

✅ I enabled Rules 4a and 4b using the -S parameter, which causes the non-I/O jobs to get more CPU time since they are not interrupted by I/O operations.

✅ I set a runtime of 50 units for Job 1, giving it a significant CPU advantage over Job 2, which only requires 5 units.

3. Command used:

python mlfq.py -n 2 -l 0,50,0:5,5,0 -S -m 0 -i 0 -M 0

4. Explanation of how job 1 obtains 99% of the CPU time:

✅Job 1 (with a runtime of 50 CPUs) does not perform I/O, so it is not interrupted by I/O operations and can continue running for an extended period without being blocked.

✅ Due to Rules 4a and 4b triggered by the -S parameter, the system prioritizes job 1 to run longer, allowing it to obtain 99% of the CPU time compared to job 2, which has only 5 CPUs.

5. Expected Result:

✅ Job 1: Uses almost all of the CPU time, as it does not perform I/O and benefits from the legacy rules, obtaining around 99% of the CPU time.

✅ Job 2: Uses only a small fraction of the CPU time (approximately 1%) due to its short execution time and the fact that it does not significantly interfere with Job 1.

📌 This behavior demonstrates how a job can "leverage" the scheduler by using Rules 4a and 4b to obtain the majority of the CPU time, thereby achieving the goal of obtaining 99% of the CPU time during the execution interval.
   </details>
   <br>
   
---

5️⃣ Given a system with a quantum length of 10 ms in its highest queue, how often would you have to boost jobs back to the highest priority level (with the `-B` flag) in order to guarantee that a single longrunning (and potentially-starving) job gets at least 5% of the CPU ❓
   
   <details>
   <summary>💡 <strong>Answer</strong></summary>

   C:\Documentos\GitHub\actividad-simulacion2>python mlfq.py -n 2 -l 0,50,0:5,5,0 -B 0 -m 0 -i 0 -M 0
Here is the list of inputs:
OPTIONS jobs 2
OPTIONS queues 2
OPTIONS allotments for queue  1 is   1
OPTIONS quantum length for queue  1 is  10
OPTIONS allotments for queue  0 is   1
OPTIONS quantum length for queue  0 is  10
OPTIONS boost 0
OPTIONS ioTime 0
OPTIONS stayAfterIO False
OPTIONS iobump False


For each job, three defining characteristics are given:
  startTime : at what time does the job enter the system
  runTime   : the total CPU time needed by the job to finish
  ioFreq    : every ioFreq time units, the job issues an I/O
              (the I/O takes ioTime units to complete)

Job List:
  Job  0: startTime   0 - runTime  50 - ioFreq   0
  Job  1: startTime   5 - runTime   5 - ioFreq   0

Compute the execution trace for the given workloads.
If you would like, also compute the response and turnaround
times for each of the jobs.

Use the -c flag to get the exact results when you are finished.
      
   ✅ Since the quantum length is 10 ms, Job 0 has a runtime of 50 ms, and Job 1 has a runtime of 5 ms, we can calculate how to adjust the boost frequency to ensure that Job 0 gets at least 5% of the CPU.

   ✅ Step 1: Calculating the Total Available CPU Time
For this system with two jobs and a quantum of 10 ms, in each run cycle, the highest-priority job receives up to 10 ms of CPU time (if it is not waiting for IO). If no boost is applied, Job 1 will execute first because it enters the system first and has a shorter runtime (5 ms). After Job 1 completes, Job 0 will receive CPU time.

   If we consider that Job 0 should receive at least 5% of the CPU, we calculate how many ms that would be:

\text{5% of 50 ms} = 0.05 \times 50 = 2.5 \, \text{ms}
So, Job 0 needs at least 2.5 ms to meet the 5% CPU usage.

   ✅ Step 2: Setting the Boost Frequency
In the event that Job 0 is potentially starving, we should ensure that it gets enough CPU time each cycle. If the system needs to prioritize Job 0 regularly, the -B parameter can help boost this job to the higher priority queue to prevent it from starving.

   You need to apply the -B parameter frequently enough so that Job 0 is not overshadowed by the shorter job, Job 1. This is achieved by applying the boost so that Job 0 receives its 5% of CPU time.

   📌 Conclusión:
   To ensure that Job 0 gets at least 5% of the CPU: You'll need to boost Job 0 regularly, using the -B parameter. In your case, with a 10 ms quantum, applying the boost frequently enough will ensure that Job 0 doesn't run out of CPU.
   </details>
   <br>
   
---

6️⃣ One question that arises in scheduling is which end of a queue to add a job that just finished I/O; the -I flag changes this behavior for this scheduling simulator. Play around with some workloads and see if you can see the effect of this flag.
   
   <details>
   <summary>💡 <strong>Answer</strong></summary>

   C:\Documentos\GitHub\actividad-simulacion2>python mlfq.py -n 2 -l 0,50,0:5,5,0 -m 0 -i 0 -M 0
Here is the list of inputs:
OPTIONS jobs 2
OPTIONS queues 2
OPTIONS allotments for queue  1 is   1
OPTIONS quantum length for queue  1 is  10
OPTIONS allotments for queue  0 is   1
OPTIONS quantum length for queue  0 is  10
OPTIONS boost 0
OPTIONS ioTime 0
OPTIONS stayAfterIO False
OPTIONS iobump False


For each job, three defining characteristics are given:
  startTime : at what time does the job enter the system
  runTime   : the total CPU time needed by the job to finish
  ioFreq    : every ioFreq time units, the job issues an I/O
              (the I/O takes ioTime units to complete)

Job List:
  Job  0: startTime   0 - runTime  50 - ioFreq   0
  Job  1: startTime   5 - runTime   5 - ioFreq   0

Compute the execution trace for the given workloads.
If you would like, also compute the response and turnaround
times for each of the jobs.

Use the -c flag to get the exact results when you are finished.


C:\Documentos\GitHub\actividad-simulacion2>python mlfq.py -n 2 -l 0,50,0:5,5,0 -I -m 0 -i 0 -M 0
Here is the list of inputs:
OPTIONS jobs 2
OPTIONS queues 2
OPTIONS allotments for queue  1 is   1
OPTIONS quantum length for queue  1 is  10
OPTIONS allotments for queue  0 is   1
OPTIONS quantum length for queue  0 is  10
OPTIONS boost 0
OPTIONS ioTime 0
OPTIONS stayAfterIO False
OPTIONS iobump True


For each job, three defining characteristics are given:
  startTime : at what time does the job enter the system
  runTime   : the total CPU time needed by the job to finish
  ioFreq    : every ioFreq time units, the job issues an I/O
              (the I/O takes ioTime units to complete)

Job List:
  Job  0: startTime   0 - runTime  50 - ioFreq   0
  Job  1: startTime   5 - runTime   5 - ioFreq   0

Compute the execution trace for the given workloads.
If you would like, also compute the response and turnaround
times for each of the jobs.

Use the -c flag to get the exact results when you are finished.
      
   ✅ The -I (--iobump) flag in the simulator controls where a process that has just completed an I/O operation is inserted into the queue. By default, processes are added to the end of their priority queue, but using -I adds the process returning from I/O to the front of the queue, giving it a more immediate opportunity to execute.

   To observe the effect of this flag, it is necessary to use workloads that include input/output (I/O) operations. In my initial tests, I used:

python mlfq.py -n 2 -l 0,50,0:5,5,0 -m 0 -i 0 -M 0
python mlfq.py -n 2 -l 0,50,0:5,5,0 -I -m 0 -i 0 -M 0

However, in those cases, the jobs do no I/O (ioFreq = 0), so the -I flag had no observable effect.

To really see the effect, I tried a new scenario where at least one job performs I/O frequently:

python mlfq.py -n 2 -l 0,50,10:5,5,0 -i 5 -M 0
python mlfq.py -n 2 -l 0,50,10:5,5,0 -I -i 5 -M 0

   ✅ In this new case:

   Job 0 performs I/O every 10 time units.

With -I, you can see that when job 0 returns from I/O, it executes faster because it is moved to the front of the queue.

Without -I, job 0 returns to the back of the queue and has to wait longer for CPU.

   📌 The -I flag can help reduce the wait time of processes that perform frequent I/O, which is beneficial in interactive systems where you want processes waiting for I/O to respond quickly.
   </details>
   <br>
   
---

## Conclusions

1. MLFQ scheduling is sensitive to parameter settings:

   - The number of queues, the length of the quanta, and the allocations per queue level directly impact the priority and CPU time each process receives.

2. Periodic boosting (-B) is essential to avoid starvation:

   - When you have a long-running job and short-running jobs, without -B, the short jobs can monopolize the CPU, leaving the long ones without a chance.

   - By periodically boosting with -B, low-priority jobs are pushed back to the highest queue, ensuring fairness and avoiding starvation.

   - For example, it was concluded that to ensure a job receives at least 5% of the CPU, the boost value must be carefully calculated based on the total CPU consumed.

3. Queue manipulation using the -I flag significantly affects jobs with I/O:

   - When a process completes an I/O operation:

      - Without -I, it returns to the end of the queue, which can cause more latency.

      - With -I, it returns to the beginning, gaining CPU immediately, which improves the performance of interactive processes.

   - This is useful for systems where high responsiveness is required (such as user interfaces or interactive servers).

4. Processes without I/O are not affected by the -I flag:

   - In simulations where processes do not perform I/O (ioFreq = 0), using the -I flag has no effect, which was empirically verified in your tests.

5. Simulation with different workloads is key to understanding real-world behavior:

   - Through tests with different combinations of arrival times, duration, and I/O frequency, we were able to observe how MLFQ dynamically adjusts priorities and execution times.

### Criterios de evaluación
- [x] Despligue de los resultados y analisis claro de los resultados respecto a lo visto en la teoria.
- [x] Creatividad y orden.
- [x] Sección con las conclusiones de los experimentos realizados.
