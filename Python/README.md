# Python
An implementation of Grover's algorithm on qiskit.

## Übersicht
Um eine eine Übersicht der Funktionen zu erhalten ist die Datei `python grover_test.py -h` auszuführen.

### Als Modul
Importiere das `grover_test` Modul in einem Python Interpreter und führe die Funktion `build_and_run(n, x_star, real, backend_name)` aus. Dabei ist:
  * `n` die Anzahl der Qubits (2 oder 3)
  * `x_star` ist der markierte Zustand (zwischen 0 und 2**n), d.h. der Zustand für den das Orakel 1 zurückgibt. Im Allgemeinen sollte das Orakel als eine Blackbox abstrahiert werden. In unserem Fall bauen wir jedoch das Orakel selbst. 
  * `real` ist True für ein IBMQ-Backend und ist False (default) für das Simulator-Backend. Wenn die Variable auf True gesetzt ist, wird die online Variable automatisch auch auf True gesetzt.
  * `online` ist True für ein online IBMQ-Backend und ansonsten False (default).
  * `backend_name` ist der Name des Backends, das verwendet wird. Falls die Variable leer gelassen wird, wird eine Standartauswahl genommen. Ist nur für online Backends sinnvoll.

```
usage: grover_test.py [-h] [-r] [-o] [-i] [-b BACKEND_NAME]
                      [--img_dir IMG_DIR] [--plot]
                      n x_star [x_star ...]
```

## Ausführungsbeispiel mit IBMQ-Backend
Beispiel eines Experiments mit 3 Qubits und dem markierten Zustand 5:
- __Python__
``` python
import grover_test as gt

gt.build_and_run(3, [5], real=True, online=True)
```
- __Command line__
``` bash
>python src/grover_test.py 3 5 -r
```
oder wenn spezifisch z.B. auf den ibmq_16_melbourne zugegriffen werden möchte:
``` bash
>python src/grover_test.py 3 5 -r -i -b ibmq_16_melbourne
```
## Ausführungsbeispiel mit Simulator-Backend  
Beispiel eines Experiments mit 2 Qubits und dem markierten Zustand 3:
- __Python__
``` python
import grover_test as gt

gt.build_and_run(2, [3])
```
- __Command line__
``` bash
>python src/grover_test.py 2 3
```

## Results 
Für n > 3 ist die Anzahl der verwendeten Gatter riesig und keines der Geräte kann liefert eine genaues Ergebnis. Die Simulation hingegen lieferen immer die richtigen Ergebnisse.


