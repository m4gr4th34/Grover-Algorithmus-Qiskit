# Python
An implementation of Grover's algorithm on qiskit.

## Übersicht
Um eine eine Übersicht der Funktionen zu erhalten ist die Datei `python grover_test.py -h` auszuführen.

### Als Modul
Importiere das `grover_test` Modul in einem Python Interpreter und führe die Funktion `build_and_run(n, x_star, real, backend_name)` aus. Dabei ist:
  * `n` die Anzahl der Qubits (2 oder 3)
  * `x_star` ist der markierte Zustand (zwischen 0 und 2**n), d.h. der Zustand für den das Orakel 1 zurückgibt. Im Allgemeinen sollte das Orakel als eine Blackbox abstrahiert werden. In unserem Fall bauen wir jedoch das Orakel selbst. 
  * `real` is True for a real backend, False (default) for the qasm simulator. If it is set to True, the online option is automatically set to True also.
  * `online` is True for an online IBMQ device, False (default) otherwise.
  * `backend_name` is the name of the backend you want to use; omit it if you want a default choice. Most of the time, you want to leave it blank. It makes sense only for an online experiment, because the only local backend is qasm.

If you just want to know some useful infos about the circuit, such as the number of actual gates the circuit gets compiled into, run the `build_and_info()` function which takes the same number of parameters.
  
For example, if you want to run an experiment on a real device with 3 qubits and selecting 5 as the x_star of the oracle, just run

``` python
import grover_test as gt

gt.build_and_run(3, [5], real=True, online=True)
```
Note that we can also omit the online parameter, which is automatically True when a real device is used.
  
To run a local simulation with 2 qubits and 3 as the special x_star state 

``` python
import grover_test as gt

gt.build_and_run(2, [3])
```

### From command line ###
You can also run the `grover_test.py` file from the command line. You can see the full help by running `grover_test.py` with the `-h` flag.
Here is a brief description
```
usage: grover_test.py [-h] [-r] [-o] [-i] [-b BACKEND_NAME]
                      [--img_dir IMG_DIR] [--plot]
                      n x_star [x_star ...]
```

For the same examples as for the case above, we could write
``` bash
>python src/grover_test.py 3 5 -r
>python src/grover_test.py 2 3
```

If instead we only want to know how many gates are needed for the ibmq_16_melbourne device to run our first circuit

``` bash
>python src/grover_test.py 3 5 -r -i -b ibmq_16_melbourne
```

## Results ##
The results are promising even for real ibmq devices when n is less than 3. However, even in this case, due to the high number of gates used when compiling on ibmqx5 and ibmq_16_melbourne, those quantum devices return wrong results; ibmqx2 and ibmqx4, on the other hand, give the right answer with an high degree of accuracy.
For n > 3, the number of gates used is really huge and none of the device can really give a precise answer. The simulation, instead, always return the correct results.

## TODO ##
  * Change code to use `add_register(ancillas)` function
  * Start porting to v 0.7.0
  * Better test on how it works with multiple x_stars
  * Check circuits w/ other unitary_simulator
