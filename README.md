# Resolución de ecuación diferencial de Laplace. Temperaturas en una placa

Mediante el Método de diferencias finitas, se discretiza un dominio (placa rectangular) con determinadas condiciones de borde (en este caso una temperatura de 63 grados aplicada en una de sus caras) y se analiza la propagación del calor a partir de la ecuación de Laplace. Se crea una matriz que contiene las ecuaciones de cada nodo que discretiza el dominio, y por medio del Método de sobrerelajaciones (SOR) se resuelve el sistema de ecuaciones lineales resultante. Luego se grafica la superficie, resultado:

![h=0 25](https://user-images.githubusercontent.com/72233852/130297976-6355c5ce-0af2-4875-a791-7f3ffe0bc8a4.jpg)

