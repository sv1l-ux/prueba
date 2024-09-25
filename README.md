Parcial Estructuras de datos

Nombre: Ana Sofia Ossa Betancur

Resolución pregunta 1:
1. Revisemos los pasos que conlleva el primer algoritmo y el segundo: 

Primero:
- Aumentar capacity en un factor x
- Crear un nuevo puntero newStorage a un arreglo en memoria
- Pasar todos los datos de storage actual a newStorage
- Eliminar storage
- Asignar storage=newStorage

Segundo:
- Aumentar capacity en un factor x y aquí entra una parte importante, porque la forma en la que creemos el nuevo newStorage define la forma en la que incrementamos la capacidad del vector, por ejemplo si queremos crear un newStorage con un size que dependa de un factor de crecimiento, debemos tener una variable size también para ese newStorage, entonces ya no solo almacenaríamos un puntero, sino que también tendríamos que almacenar su tamaño y por motivos que mencionaré más adelante, también debemos tener en cuenta su capacidad como otra variable (es decir, por sus propiedades es un elemento de la clase vector). En cambio si no elegimos un factor de crecimiento, entonces estaríamos creando una y otra vez un vector del mismo tamaño lo que ya se ha visto en las clases que es ineficiente.
- Ahora el vector se compondría de un storage que va a ser un arreglo de punteros a vectores.
- Crear un nuevo newStorage.

Eso en cuanto al resize, cuando tengamos funciones que recorran el vector, debemos tener en cuenta que una vez se alcance al último elemento de un vector, es decir, su capacidad, debemos acceder al siguiente vector del arreglo de vectores.

A nivel de código esto nos agrega mucha verbosidad debido a la forma en la que se debe recorrer el vector, además de que debemos de apartar espacio adicional en memoria para los atributos de estos sub-vectores. 

Así que es peor con la implementación de sub-vectores de tamaño estático y en cuanto a optimización es mejor si se hace con sub-vectores de tamaño dinámico, pero si hablamos de la legibilidad del código y la comodidad del programador, es una mala opción.

2. Depende de la utilidad. Por ejemplo si requiero un programa donde necesito acceder a elementos aleatorios de la estructura de datos, es mucho mejor un vector porque uno puede acceder fácilmente mediante los índices, mientras que en una lista enlazada hay que recorrer cada uno de los nodos anteriores al que se quiere encontrar.

Con respecto a operaciones que requieran remover elementos que no son el final de la estructura de datos, es mucho más eficiente una lista, puesto que solo hay que modificar el puntero del nodo anterior del eliminado y liberar el espacio en memoria del eliminado.

Pregunta 2

1. operaciones de crecimiento para x:

5*2=10*2=20*2=40*2=80*2=160*2=320*2=640*2=1280*2=2560*2=5120*2=10240, entonces 10240 es la capacidad final

(11 veces se llama resize)

operaciones de crecimiento para y:

10*1.8=18*1.8=32*1.8=58*1.8=104*1.8=187*1.8=338*1.8=608*1.8=1095*1.8=1972*1.8=3.550*1.8=6391*1.8=11504
entonces 11504 es la capacidad final

(12 veces se llama resize)

operaciones de crecimiento para z:

100*2.0=200*2.0=400*2.0=800*2.0=1600*2.0=3200*2.0=6400*2.0=12800
entonces 12800 es la capacidad final

(7 veces se llama el resize)

Por tanto el desperdicio de cada uno es:
x: 10240-10000=240 elementos de desperdicio, que en este caso son enteros, por lo tanto se desperdician 240*4= 960 bytes en memoria

y: 11504-10000=1504 elementos de desperdicio, que en este caso son enteros, por lo tanto se desperdician 1504*4= 6016 bytes en memoria

z: 12800-10000=2800 elementos de desperdicio, que en este caso son enteros, por lo tanto se desperdician 2800*4= 11200 bytes en memoria

2. En cuanto a este programa en específico, fue más eficiente el vector x porque fue el segundo que menos llamó a resize (11 veces) y es el que menos bytes en memoria desperdicia (960 bytes). 

Pregunta 3:

1. #include <iostream>
#include <cassert>
#include <stdbool.h>

using namespace std;

template <typename T>
AdjancencyList{
    //Importante, estamos suponiendo, que como en el ejemplo, todas las ciudades tienen nombre único, i.e: 0,1,2,3,4,5 (importante para la operacion findConnections)
    private:
        T myData;
        Vector<AdjancencyList<T>> myConnections;
    public:
        AdjancencyList: myData(),myConnections(){};
        AdjancencyList: myData(T elem), myConnections(){};
        AdjancencyList: myData(T elem), myConnections(Vector<AdjancencyList<T>>){}; //si ya tiene creado un vector que contenga sus conexiones, se usa este constructor

        T getData(){
            return myData;
        }
        unsigned int numConnections(){
            return myConnections.getSize();
        }
        bool empty(){
            return myConnections.empty();
        }
        //2.
        void pushBackConnections(AdjancencyList other){
            myConnections.push_back(other);
            other.myConnections.push_back(this);
        }
        void pushFrontConnections(AdjancencyList other){
            myConnections.push_front(other);
            other.myConnections.push_back(this);
        }
        unsigned int findConnections(T data){
            for(unsigned int i=0; i<myConnections.getSize();i++){
                if(data==myConnections.at(i).getData()){
                    return i;
                }
            }
        }
        AdjancencyList at(unsigned int pos){
            myConnections.at(pos);
        }
        void popBackConnections(){
            assert(!myConnections.getSize()==0 && "No tienes conexiones!");
            at((myConnections.getSize())-1).myConnections.remove(at(findConnections(data))); //Quita este AdjancencyList del AdjancencyList que estamos quitando
            myConnections.pop_back();
        }
        void removeConnections(unsigned int pos){
            assert((pos>=0&&pos<=getSize.myConnections()) && "pos fuera de los limites");
            at((myConnections.at(pos)).myConnections.remove(at(findConnections(data)))); //Quita este AdjancencyList del AdjancencyList que estamos quitando
            myConnections.remove(pos);
        }
        void changeData(T elem){
            myData= elem;
        }
        //3.  
        void printConnections(){
            assert(!myConnections.getSize()==0 && "No tienes conexiones!");
            for(unsigned int=0;i<myConnections.getSize();i++){
                cout<<myConnections.at(i).myData<<" ";
            };
        }
};

