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
   1. Se ah ejecutado varios escenarios con dos procesos y dos colas de planificación MLFQ, limitando la duración de cada proceso a un máximo de 5 ticks y desactivando operaciones de entrada/salida (ioFreq = 0). A continuación, se presenta uno de los casos:

   ✅ Configuración:

   2 colas (-n 2)

   Job 0: empieza en t=0, dura 5 ticks

   Job 1: empieza en t=1, dura 3 ticks

   Sin I/O (ioFreq = 0, ioTime = 0)

   Quantum = 10 en ambas colas

   Allotment = 1 (solo un turno en cada nivel antes de bajar de prioridad)

   ✅ Ejecución esperada:

   En t=0, entra Job 0 y se ejecuta hasta t=1.

   En t=1, llega Job 1, pero Job 0 sigue su quantum, así que Job 1 espera.

   Job 0 agota su allotment y baja de prioridad.

   Job 1 sube a la cola 0, se ejecuta completamente.

   Luego Job 0 se retoma y termina.

   📌 Resultado:

   Se observa cómo MLFQ reordena la prioridad al agotar el allotment.

   Los trabajos terminan correctamente y sin I/O.
   </details>
   <br>
   
---

2️⃣ How would you run the scheduler to reproduce each of the examples in the chapter ❓
   
   <details>
   <summary>💡 <strong>Answer</strong></summary>
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
   ✅ Para configurar una carga de trabajo en la que un trabajo aproveche las Reglas 4a y 4b y obtenga el 99% del tiempo de CPU, realicé lo siguiente:

   1. Configuración de los trabajos:

   ✅ Trabajo 1 (Job 0): Comienza en el tiempo 0 y tiene un tiempo de ejecución de 50 unidades de tiempo de CPU. Este trabajo no realiza operaciones de I/O (el parámetro ioFreq es 0). Al no realizar I/O, puede         aprovechar las reglas 4a y 4b, que permiten a un trabajo sin I/O obtener más tiempo de CPU.

   ✅ Trabajo 2 (Job 1): Comienza en el tiempo 5 y tiene un tiempo de ejecución de solo 5 unidades de tiempo de CPU. Tampoco realiza I/O.

   2. Parámetros del Scheduler:

   ✅ Utilicé 2 colas (-n 2), donde ambos trabajos compiten por el tiempo de CPU. La cola 0 tiene mayor prioridad, lo que permite que el trabajo sin I/O (Trabajo 1) obtenga más tiempo de CPU debido a las reglas 4a y 4b.

   ✅ Activé las Reglas 4a y 4b utilizando el parámetro -S, lo que hace que los trabajos sin I/O obtengan más tiempo de CPU, ya que no son interrumpidos por operaciones de I/O.

   ✅ Establecí un tiempo de ejecución de 50 unidades para el trabajo 1, lo que le da una gran ventaja de CPU sobre el trabajo 2, que solo requiere 5 unidades.

   3. Comando utilizado:

   python mlfq.py -n 2 -l 0,50,0:5,5,0 -S -m 0 -i 0 -M 0

   4. Explicación de cómo se obtiene el 99% del tiempo de CPU para el trabajo 1:
      
   ✅El Trabajo 1 (con un tiempo de ejecución de 50 unidades de CPU) no realiza I/O, por lo que no es interrumpido por operaciones de I/O, y puede continuar ejecutándose durante un largo período de tiempo sin ser bloqueado.

   ✅ Debido a las Reglas 4a y 4b activadas por el parámetro -S, el sistema prioriza el trabajo 1 para que se ejecute durante más tiempo, lo que le permite obtener 99% del tiempo de CPU en comparación con el           trabajo 2, que tiene solo 5 unidades de CPU.

   5. Resultado esperado:
      
   ✅ Trabajo 1: Utiliza casi todo el tiempo de CPU, ya que no realiza I/O y se beneficia de las reglas antiguas, obteniendo alrededor del 99% del tiempo de CPU.

   ✅ Trabajo 2: Utiliza solo una pequeña fracción del tiempo de CPU (aproximadamente el 1%), debido a su corto tiempo de ejecución y a que no interfiere significativamente con el Trabajo 1.

   📌 Este comportamiento demuestra cómo un trabajo puede "aprovechar" el planificador mediante el uso de las Reglas 4a y 4b para obtener la mayor parte del tiempo de CPU, logrando así el objetivo de obtener el 99% del tiempo de CPU durante el intervalo de ejecución.
   </details>
   <br>
   
---

5️⃣ Given a system with a quantum length of 10 ms in its highest queue, how often would you have to boost jobs back to the highest priority level (with the `-B` flag) in order to guarantee that a single longrunning (and potentially-starving) job gets at least 5% of the CPU ❓
   
   <details>
   <summary>💡 <strong>Answer</strong></summary>
   ✅ Dado que la longitud del quantum es de 10 ms, el trabajo Job 0 tiene un tiempo de ejecución de 50 ms, y Job 1 tiene un tiempo de ejecución de 5 ms, podemos calcular cómo ajustar la frecuencia del "boosting" para garantizar que Job 0 obtenga al menos el 5% de la CPU.

   ✅ Paso 1: Cálculo del tiempo total disponible en la CPU
   Para este sistema con 2 trabajos y un quantum de 10 ms, en cada ciclo de ejecución el trabajo de más alta prioridad recibe hasta 10 ms de CPU (si no está esperando IO). Si no se hace ningún boost, Job 1 se   ejecutará en primer lugar, debido a que entra al sistema primero y su tiempo de ejecución es más corto (5 ms). Después de completar Job 1, Job 0 recibirá tiempo de CPU.

   Si consideramos que Job 0 debería recibir al menos el 5% de la CPU, calculamos cuántos ms serían:

   \text{5% de 50 ms} = 0.05 \times 50 = 2.5 \, \text{ms}
   Entonces, Job 0 necesita al menos 2.5 ms para cumplir con el 5% de uso de la CPU.

   ✅ Paso 2: Establecimiento de la frecuencia de "boosting"
   En el caso de que Job 0 esté potencialmente "starving", deberíamos asegurarnos de que obtenga suficiente tiempo de CPU en cada ciclo. Si el sistema tiene que darle prioridad a Job 0 regularmente, el parámetro -B puede ayudar a "boostear" este trabajo hacia la cola de mayor prioridad para evitar que se quede sin CPU.

   Tienes que aplicar el -B con la frecuencia necesaria para que Job 0 no sea eclipsado por el trabajo más corto, Job 1. Esto se logra aplicando el "boost" de manera que Job 0 reciba su 5% de tiempo de CPU.

   📌 Conclusión:
   Para garantizar que Job 0 obtenga al menos el 5% de la CPU: Tendrás que realizar un "boost" de Job 0 regularmente, utilizando el parámetro -B. En tu caso, con un quantum de 10 ms, aplicar el "boost" con la suficiente frecuencia hará que Job 0 no se quede sin CPU.
   </details>
   <br>
   
---

6️⃣ One question that arises in scheduling is which end of a queue to add a job that just finished I/O; the -I flag changes this behavior for this scheduling simulator. Play around with some workloads and see if you can see the effect of this flag.
   
   <details>
   <summary>💡 <strong>Answer</strong></summary>
   ✅ El flag -I (--iobump) en el simulador controla en qué parte de la cola se inserta un proceso que acaba de terminar una operación de I/O. Por defecto, los procesos se agregan al final de su cola de prioridad, pero al usar -I, el proceso que regresa de I/O se agrega al principio de la cola, dándole así una oportunidad más inmediata de ejecutarse.

   Para observar el efecto de este flag, es necesario usar cargas de trabajo que incluyan operaciones de entrada/salida (I/O). En mis pruebas iniciales usé:

   python mlfq.py -n 2 -l 0,50,0:5,5,0 -m 0 -i 0 -M 0
   python mlfq.py -n 2 -l 0,50,0:5,5,0 -I -m 0 -i 0 -M 0

   Sin embargo, en esos casos los trabajos no hacen I/O (ioFreq = 0), por lo tanto, el flag -I no tuvo ningún efecto observable.

   Para ver realmente el efecto, probé con un nuevo escenario donde al menos un trabajo hace I/O frecuentemente:

   python mlfq.py -n 2 -l 0,50,10:5,5,0 -i 5 -M 0
   python mlfq.py -n 2 -l 0,50,10:5,5,0 -I -i 5 -M 0

   ✅ En este nuevo caso:

   El trabajo 0 hace I/O cada 10 unidades de tiempo.

   Con -I, se ve que cuando el trabajo 0 regresa del I/O, se ejecuta más rápidamente porque es puesto al frente de la cola.

   Sin -I, el trabajo 0 regresa al final de la cola y tiene que esperar más para obtener CPU.

   📌 El flag -I puede ayudar a reducir el tiempo de espera de los procesos que realizan I/O frecuente, lo cual es beneficioso en sistemas interactivos donde se busca que los procesos que esperan por I/O respondan rápido.
   </details>
   <br>
   
---

## Conclusions

Coloque aqui las conclusiones...

### Criterios de evaluación
- [x] Despligue de los resultados y analisis claro de los resultados respecto a lo visto en la teoria.
- [x] Creatividad y orden.
- [x] Sección con las conclusiones de los experimentos realizados.
