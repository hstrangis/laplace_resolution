# Placa de 20cmx10cm. Pasos de discretizacion de Dx=Dy=0.25cm
# Resulta en grilla de 80x40 divisiones
# Planteamos matriz de nodos Tmatrix(n x m), fils = 41, cols = 81  

## Para plantear el sistema A*x=b, armo una matriz A de 3321 x 3321, 
## cada fila es la ecuacion de un nodo, siendo  
kx = 81;  % Nodos X
ky = 41;  % Nodos Y
m = kx*ky;
n = kx*ky;
A = zeros(m, n);

%%%% Creacion de matriz A %%%%

% Definicion de la matriz con la discretizacion de diferencias finitas
  
for j = 1 : n                                  
  for i = 1 : m
    if(i == j && (j < kx + 2 || j > n - kx - 1))  % Nodos bordes
      A(i,j) = 1; 
    elseif(i == j && mod(j,kx) != 0 && mod(j - 1, kx) != 0) %% Con mod, descarto los nodos bordes, que son multiplos de kx
      A(i,j) = -4;
      A(i,j + 1) = 1;
      A(i,j - 1) = 1;
      A(i,j + kx) = 1;
      A(i,j - kx) = 1;
    elseif(i == j)
      A(i,j) = 1;
    endif
  endfor
endfor 

# Vector B con condiciones de borde de (A)
b = zeros(n,1);
for i = 1 : kx - 1     %Borde inferior
  b(i) = 0;
endfor
for i = n - kx + 1 : n - 1    % Borde superior
  b(i) = 0;
endfor
for i = 1 : kx : n - kx + 1   % Borde izquierdo
  b(i) = 0;
endfor  
for i = kx : kx : n     %Borde derecho
  b(i) = 63;
endfor  

######### SOR ##################

function [X, iter] = SOR(A, w, error, maxiter, b)

D = diag(diag(A));
L = tril(A)- D;
U = triu(A)- D;
Told = ones(rows(A),1);  
error = 1e-05;
MAXerr = 1000;
iter = 0;
P = inv(D + w*L);
C = w*U + (w-1)*D;

while iter < maxiter && MAXerr > error  
    X = P * (w * b - C * Told);
    MAXerr = norm(X - Told);
    iter = iter + 1;
    Told = X;
endwhile
endfunction
##############################################################

% Aplico el metodo SOR al sistema 

[X, iter] = SOR(A, 1.72, 1e-03, 300, b);

% Vuelco los resultados en la matriz de nodos Tmatrix

Tmatrix = zeros(ky,kx);
z = 1;
for i = ky : -1 : 1
  for j = 1 : kx
     Tmatrix(i,j) = X(z);
     z = z + 1;
   endfor
endfor;

#disp(Tmatrix)  
disp(iter) 

###### Grafico #######
[x,y] = meshgrid(1:kx,1:ky);
surf(x,y,Tmatrix);
shading flat;

