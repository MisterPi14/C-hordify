Estudiantes que elaboraron el código:

Piña Vargas Edgar Diego
Correa Torres Italo

Descripción del programa: Este programa tiene como simple utilidad servir con fines recreativos algunos conceptos musicales, así como su objetivo principal “Crear melodías de manera aleatoria”. A groso modo en el programa se encontrará con un generador de melodías, con una sección para visualizar datos de las notas musicales y los modos tonales, así como tambien una última sección para escuchar la diferencia entre un acorde mayor y menor, en el programa se contextualiza de manera breve los fundamentos de todos estos conceptos.
Para el desarrollo de este software, se usaron los siguientes conceptos de la programación orientada a objetos:
Clases
oEncapsulamiento de datos
ofunción miembro de la clase
Operador de alcance
oconstructor
odestructor
Herencia
Uso de plantilla o templete
Polimorfismo
oSobre carga de funciones 
osobrecarga de operadores
Programa
#include <iostream>
#include <windows.h>
#include<time.h>
#include <math.h>
#define acordes "Los acordes se definen como un conjunto de 3 o mas elementos (en este caso notas)\nsiendo las primeras 3 las mas comunes.\nSon llamadas fundamental, tercera y quinta\nLA TERCERA cuenta con una particularidad especial,\npues dependiendo de la distancia que tenga con respecto a la fundamental sera denominada (Mayor o Menor) \n\nEn esta seccion podra escuchar como suena un acorde mayor o menor. \n\nPulse 1=Mayor 2=Menor: "
#define info "\t\t\tLAS NOTAS Y LOS MODOS\n\nLa musica se compone de elementos conocidos como notas musicales,\nestas se definen desde la acustica como ondas que viajan en el espacio con una frecuencia especifica\nEn otros contextos historicos se crearon etiquetas que agrupan esas notas (Escalas o modos)"
#define info2 "\n\nLas notas musicales son: Do,Reb,Re,Mib,Mi,Fa,Solb,Sol,Lab,La,Sib,Si,Do,Reb,Re,Mib,Mi,Fa,Solb,Sol,Lab,La,Sib,Si\nY los modos tonales (conjuntos de notas) son: Mayor,Dorico,Frigio,Lidio,Mixolidio,Menor,Locrio:\n\n1.-Visualizar Frecuencia de una nota\n2.-Buscar un relativo de una escala mayor\n\nQue desea Realizar?...:"
using namespace std;
/*
-------------ANOTACIONES DEL PROGRAMA------------
REALIZADO POR ALUMNOS DE LA ESIME CULHUACAN....
NOMBRES:  Correa Torres Italo
		  Piña Vargas Edgar Diego

Beep(frec,t en milisegundos) 1000 milisegundos = 1 segundo ; 1 segundo = negra en 60 bpm; 0.5 segundos = 500 milisegundos = negra en 120 bpm
1000 - 60  parametro de tiempo en BEEP = (60*1000)/x donde x es el bpm que da el usuario al ser proporsicion inversa

Codigo del modo mayor= t,t,s,t,t,t,s
*/
///////////////////////////////////CLASE BASE///////////////////////////////////////////////////////////
class notas_id//Uso de clase
{
	private://Encapsulamiento de datos
	string nombre;
	string figura;
	public:
	notas_id(string,string);//Constructor
	void imprimir();//Funcion Miembro de la clase
};

notas_id :: notas_id(string _nombre, string _figura)//Uso del resolutor de ambito u operador de alcanze
{
	nombre=_nombre;
	figura=_figura;
}
void notas_id :: imprimir()
{
	cout<<nombre<<"("<<figura<<")";
}
/////////////////////////////////////////////CLASE DERIVADA 1 ///////////////////////////////////////////////////////////
class notas_data : public notas_id//Uso de clase y Herencia
{
	private://Encapsulamiento de datos
	float frec;
	double duracion;
	public:
	void reproducir();//Funcion Miembro de la clase
	notas_data(string,string,float,double);//Constructor
	~notas_data();//Destructor
};
void notas_data :: reproducir()
{
	notas_id :: imprimir();
	Beep(frec,duracion);
}
notas_data :: notas_data(string _nombre, string _fig, float _frec, double _dur) /*1*/: notas_id(_nombre,_fig) //1.-despues del 1 se envian los parametros a la clase base
{
	frec=_frec;
	duracion=_dur;
}
notas_data :: ~notas_data()
{
	cout<<" -> ";
}
////////////////////////////////////////////MAIN Y SELECCION///////////////////////////////////////////////////////////
int i;
void Generador_Melodias();
void Infografia();
void Actividad();

int main()
{
	while(1)
	{
	system("cls"); int op;
    cout<<"\t\t\tBIENVENIDO A Chord++, un programa interactivo con la musica\n\nA donde te quieres dirigir?\n";
    cout<<"\n*Generador de Melodias (principal)\n*Observar datos de las notas musicales\n*Reproduccion de acordes (Mayores y Menores)"<<endl;
	cout<<"\nPara seleccionar alguno use 1, 2 o 3: ";

		cin>>op;
		if(op==1)
		Generador_Melodias();
		else if(op==2)
		Infografia();
		else if(op==3)
		Actividad();
		else
		{
			cout<<"\nIngrese una opcion valida"<<endl;
		}
	}
	return 0;
}


//////////////////////////////////////////////MELODIAS////////////////////////////////////////////////////////////
void Play(int scl, float bpm, int duracion)
{
	int ran,ran2; float suma=0;
	srand(time(NULL));
	string nom[]={"Do","Reb","Re","Mib","Mi","Fa","Solb","Sol","Lab","La","Sib","Si","Do","Reb","Re","Mib","Mi","Fa","Solb","Sol","Lab","La","Sib","Si"};
	float hz[]={16.3516,17.3239,18.3540,19.4454,20.6017,21.8268,23.1246,24.4997,25.9565,27.5,29.1353,30.8677,16.3516*2,17.3239*2,18.3540*2,19.4454*2,20.6017*2,21.8268*2,23.1246*2,24.4997*2,25.9565*2,27.5*2,29.1353*2,30.8677*2};
	
	notas_data *nota;//Se crea un puntero a una intancia de clase u objeto
	while(duracion>suma)
	{
		ran=rand()%24;//relacionado a la frecuencia
		if(ran==scl||ran==scl+2||ran==scl+4||ran==scl+5||ran==scl+7||ran==scl+9||ran==scl+11)
		{
			ran2=rand()%4;//relacionado al ritmo de la nota
			switch(ran2)
			{
				case 0:
				nota=new notas_data(nom[ran],"Blanca",hz[ran]*8,double((60000/bpm)*2)); suma+=((60/bpm)*2);//Uso del operador new para la creacion de objetos
				break;			
				case 1:
				nota=new notas_data(nom[ran],"Negra",hz[ran]*8,double((60000/bpm))); suma+=((60/bpm));
				break;			
				case 2:
				nota=new notas_data(nom[ran],"Corchea",hz[ran]*8,double((60000/bpm)/2)); suma+=((60/bpm)/2);
				break;
				case 3:
				nota=new notas_data(nom[ran],"Semicorchea",hz[ran]*8,double((60000/bpm)/4)); suma+=((60/bpm)/4);				
				break;
			}
			nota->reproducir();//Uso de las funciones mimbro
			delete(nota);//Entra el destructor
		}
	}
}

template<typename T> void Imprimir(T elemento)//Uso de plantilla o templete
{
	cout<<elemento;
}
void Generador_Melodias()
{
	system("cls"); float bpm; int escala,duracion;
	cout<<"\t\t\tPrograma para GENERAR MELODIAS MUSICALES\n";
	cout<<"\n**********Escalas musicales**********\n";
	
	string nom[]={"Do","Reb","Re","Mib","Mi","Fa","Solb","Sol","Lab","La","Sib","Si"};
	float hz[]={16.3516,17.3239,18.3540,19.4454,20.6017,21.8268,23.1246,24.4997,25.9565,27.5,29.1353,30.8677};
	
	for(int i=0; i<12; i++)
	{
		cout<<i+1<<".- Escala de: "; Imprimir(nom[i]); cout<<" ( "; Imprimir(hz[i]); cout<<" Hz )\n";
	}

	cout<<"\nQue escala (MAYOR) utilizaras: ";
	cin>>escala;
	cout<<"\nA que velocidad ira la melodia (BPM) 'Se recomiendan valores de 60 bpm a 120 bpm' : ";
	cin>>bpm;
	cout<<"\nCuantos segundos (aproximadamente) quiere que dure la melodia: ";
	cin>>duracion;
	Play(escala-1,bpm,duracion);
}
///////////////////////////////////////////////////////INFOGRAFIA///////////////////////////////////////////////////////////////

string notas_musicales[]={"Do","Reb","Re","Mib","Mi","Fa","Solb","Sol","Lab","La","Sib","Si"};
float frecuencias[]={16.3516,17.3239,18.3540,19.4454,20.6017,21.8268,23.1246,24.4997,25.9565,27.5,29.1353,30.8677};

void DatosMusicales(string nota)//Sobre carga de funciones -> Polinorfismo 
{
	int pos;
	for(int i=0;i<12;i++)
	{
		if(notas_musicales[i]==nota)
		{pos=i; break;}
	}
	for(int i=0;i<9;i++)
	cout<<"La frecuencia en hz de la nota "<<notas_musicales[pos]<<" en la octava "<<i<<" es de: "<<frecuencias[pos]*pow(2,i)<<"hz\n";
}

void DatosMusicales(string nota, string modo)//Sobre carga de funciones
{
	int pos;
	for(int i=0;i<12;i++)
	{
		if(notas_musicales[i]==nota)
		{pos=i; break;}
	}
	string music[]={"Do","Reb","Re","Mib","Mi","Fa","Solb","Sol","Lab","La","Sib","Si","Do","Reb","Re","Mib","Mi","Fa","Solb","Sol","Lab","La","Sib","Si"};
	if(modo=="Dorico")
	cout<<"El relativo Dorico de "<<nota<<" mayor es: "<<music[pos+2]<<" Dorico"<<endl;
	else if(modo=="Frigio")
	cout<<"El relativo Frigio de "<<nota<<" mayor es: "<<music[pos+4]<<" Frigio"<<endl;
	else if(modo=="Lidio")
	cout<<"El relativo Lidio de "<<nota<<" mayor es: "<<music[pos+5]<<" Lidio"<<endl;
	else if(modo=="Mixolidio")
	cout<<"El relativo Mixolidio de "<<nota<<" mayor es: "<<music[pos+7]<<" Mixolidio"<<endl;
	else if(modo=="Menor")
	cout<<"El relativo Menor de "<<nota<<" mayor es: "<<music[pos+9]<<" Menor"<<endl;
	else if(modo=="Locrio")
	cout<<"El relativo Locrio de "<<nota<<" mayor es: "<<music[pos+11]<<" Locrio"<<endl;
	else if(modo=="Mayor")cout<<"El relativo mayor de una escala mayor es esa misma escala."<<endl;
	else cout<<"No se encontro el modo que solicitaste, Verifica que este bien escrito.\n";
}


void Infografia()
{
	bool res=0;
	while(res==0)
	{
		system("cls"); int opc;
		cout<<info<<info2;
		cin>>opc;
		string id_nota;
		switch(opc)
		{
			case 1:
					{cout<<"Nota: ";
					cin.ignore(); getline(cin, id_nota);
					DatosMusicales(id_nota);}
				break;
			case 2:
					{cout<<"Nota de la escala mayor: ";
					cin.ignore(); getline(cin, id_nota);
					cout<<"Modo relativo a buscar: ";
					string modo;
					getline(cin, modo);
					DatosMusicales(id_nota,modo);}
				break;
		}
		cout<<"\nDesea salir al menu principal? (1=Si 0=No): "; cin>>res;
	}

}
////////////////////////////////////////////////////////////ACTIVIDAD INTERACTIVA///////////////////////////////////////////////////////////////
class intervalo
{
	private:
	float frec=16.3516*8;
	public:
	intervalo operator + (intervalo fun)//Obtiene la tercera mayor de una nota fundamental SOBRECARGA DE OPERADORES
	{
		intervalo ter;
		ter.frec=fun.frec*pow(2,(.333));
		return ter;
	}
	intervalo operator - (intervalo fun)//Obtiene la tercera menor de una nota fundamental SOBRECARGA DE OPERADORES
	{
		intervalo ter;
		ter.frec=fun.frec*pow(2,(.25));
		return ter;
	}
	void Reproducir()
	{
		Beep(frec,300);
	}
};
void Actividad()
{
	int opc2; bool res=0;
	while(res==0)
	{
		system("cls"); 	intervalo a,b,c;
		cout<<"\t\tLos acordes y su composicion\n\n"<<acordes; cin>>opc2;
		if(opc2==1)
		{c=a+b; cout<<"\nAcorde de Do Mayor\n\n";}
		else if(opc2==2)
		{c=a-b; cout<<"\nAcorde de Do Menor\n\n";}
		else cout<<"Solo se pueden ingresar 1 o 2, intente de nuevo";

		cout<<"Nota: Do (fundamental)  ->  ";  a.Reproducir();
		cout<<"Nota: Mi (Tercera)  ->  ";  c.Reproducir();
		cout<<"Nota: Do (Quinta)";  Beep(24.4997*8,300);
		
		cout<<"\nDesea salir al menu principal? (1=Si 0=No): "; cin>>res;
	}
}

