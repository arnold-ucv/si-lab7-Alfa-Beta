# Laboratorio: Minimax y Poda Alfa-Beta

## Descripción
Este proyecto implementa los algoritmos Minimax y Poda Alfa-Beta para resolver un árbol de decisión simplificado.

## Objetivo
Comparar el resultado y la eficiencia de Minimax frente a Poda Alfa-Beta.

## Instalación
```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Ejecución
```bash
python -m src.main
```

## Pruebas
```bash
pytest --cov=src --cov-report=term-missing
```

## Preguntas de análisis
1.	¿Por qué Alfa-Beta obtiene el mismo resultado que Minimax si no evalúa todo el árbol?
Obtiene el mismo resultado porque solo descarta ramas que no alteran la decisión final. Si se demuestra que una jugada es peor que una alternativa ya garantizada, un jugador racional no la elegirá, por lo que evaluarla es innecesario.
2.	¿Qué representa alpha dentro del algoritmo?
Representa el mejor valor (el más alto) que el jugador MAX tiene garantizado hasta el momento. Comienza en infinito negativo y se actualiza cuando MAX encuentra mejores opciones.
3.	¿Qué representa beta dentro del algoritmo?
Representa el mejor valor (el más bajo) que el jugador MIN tiene garantizado hasta el momento. Comienza en infinito positivo y se actualiza cuando MIN encuentra mejores opciones para reducir la puntuación de MAX.
4.	¿En qué casos la Poda Alfa-Beta ahorra más trabajo?
Ahorra más trabajo cuando los nodos se evalúan en el orden óptimo (los mejores movimientos primero). Esto permite podar la mayor cantidad de ramas y reduce la complejidad de tiempo a la mitad del exponente original.
5.	¿Por qué el orden de exploración afecta el rendimiento?
Porque si los mejores movimientos se evalúan al principio, los límites alpha y beta se ajustan rápidamente, lo que permite podar ramas enteras desde temprano. Si se evalúan en el peor orden, no se realiza ninguna poda y se comporta igual que Minimax.
6.	¿Qué pasaría si el rival no juega de manera racional?
El algoritmo asumirá que el rival siempre elegirá la mejor jugada posible. Aunque el rival cometa errores, Alfa-Beta seguirá tomando decisiones seguras y ganará o aprovechará los fallos del oponente, aunque no siempre elegirá la ruta más rápida para castigarlo.
7.	¿Cómo se relaciona este algoritmo con motores de ajedrez?
Es la base del motor de búsqueda de ajedrez clásico (como Stockfish en sus primeras versiones). Se combina con funciones de evaluación heurística, ordenamiento de jugadas y tablas de transposición para analizar millones de posiciones por segundo.
8.	¿Qué limitaciones tiene este enfoque frente a redes neuronales o aprendizaje por refuerzo?
Requiere explorar un árbol de estados explícito y depende de una función de evaluación diseñada manualmente, lo que lo hace inviable en juegos con un factor de ramificación enorme como el Go. Las redes neuronales y el aprendizaje por refuerzo aprenden patrones complejos sin necesidad de calcular todas las combinaciones posibles.