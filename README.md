# Prova_Git
 Codice caricato per una prova repository Git
 
 #include <iostream>
#include <stdlib.h>
#include <fstream>
#include <string>
#define DIM 3

/*Scrivere un programma in C++ che memorizza e stampa la classifica punti e classifica marcatori
con la rispettiva squadra di appartenenza della serie A la struttura dati squadra è così:*/
///     squadra
///     {
///     nome
///     punti
///     capocannoniere_nome
///     capocannoniere_gol
///     }

using namespace std;

///struct
struct squadra{
    string nome;                      ///nome della squadra
    int punti;                       ///punti squadra
    string capocannoniere_nome;     ///nome del giocatore
    int capocannoniere_gol;        ///gol fatti dal giocatore
}squadre[DIM];

void inserimento()
{

    ofstream file("MioFile.dat",ios::out|ios::binary);
    if(!file)
        cout<<"errore apertura file ";
    else
    {
        string temp;
        for(int i=0;i<DIM;i++)
        {
            ///carico la struct
            cout<<"Inserimento della squadra numero"<<(i+1)<<endl;
            cout<<"Nome squadra:";
            fflush(stdin);
            getline(cin,temp);
            squadre[i].nome=temp;
            cout<<endl;
            cout<<"Punti squadra:";
            cin>>squadre[i].punti;
            cout<<endl;
            cout<<"Capocannoniere squadra:";
            fflush(stdin);
            getline(cin,temp);
            squadre[i].capocannoniere_nome=temp;
            cout<<endl;
            cout<<"Gol capocannoniere:";
            cin>>squadre[i].capocannoniere_gol;
            ///carico la struct sul file tramite il metodo write
            file.write((char *)&squadre[i],sizeof(squadre[i]));
        }
        for(int c=0; c<DIM; c++)
          {
             cout<<"Nome squadra: "<<squadre[c].nome<<" Punti: "<<squadre[c].punti<<" Nome capocannoniere:  "<<squadre[c].capocannoniere_nome<<" Gol: "<<squadre[c].capocannoniere_gol<<endl;

          }
    }
}

void classifica()
{
    squadra app;
    ifstream file("MioFile.dat",ios::in|ios::binary);
    if(!file)
        cout<<"errore apertura file";
    else
    {
        for(int i=0;i<DIM;i++)
            ///attraverso il metodo read carico il file sulla struct
            file.read((char *)&squadre[i],sizeof(squadre[i]));
            ///ordino la classifica dalla squadra in base alla squadra con il punteggio piu' alto
        for(int i=0;i<DIM;i++)
        {
            for(int j=i+1;j<DIM;j++)
            {
               if(squadre[i].punti<squadre[j].punti)
                {
                    app=squadre[j];
                    squadre[j]=squadre[i];
                    squadre[i]=app;
                }

            }
        }
    }
     for(int c=0; c<DIM; c++)
          {
             cout<<"Nome squadra: "<<squadre[c].nome<<" Punti: "<<squadre[c].punti<<endl;

          }
}

void marcatori()
{
 squadra app;
    ifstream file("MioFile.dat",ios::in|ios::binary);
    if(!file)
        cout<<"errore apertura file";
    else
    {
        for(int i=0;i<DIM;i++)
            file.read((char *)&squadre[i],sizeof(squadre[i]));
        for(int i=0;i<DIM;i++)
        {
            for(int j=i+1;j<DIM;j++)
            {
                 if(squadre[i].capocannoniere_gol<squadre[j].capocannoniere_gol)
                {
                    app=squadre[j];
                    squadre[j]=squadre[i];
                    squadre[i]=app;
                }
            }
        }
    }
     for(int c=0; c<DIM; c++)
          {
             cout<<"Nome squadra: "<<squadre[c].nome<<" Nome capocannoniere:  "<<squadre[c].capocannoniere_nome<<" Gol: "<<squadre[c].capocannoniere_gol<<endl;

          }
}

int main()
{
    int scelta;
    do
    {
        do
        {
            cout<<"Quale operazione vuoi eseguire?"<<endl;
            cout<<"1)Inserimento dati"<<endl;
            cout<<"2)Stampa classifica punti"<<endl;
            cout<<"3)Stampa classifica marcatori"<<endl;
            cout<<"4)Exit"<<endl;
            cin>>scelta;
        }
        while(scelta<1||scelta>4);
         system("cls");
        switch(scelta)
        {
            case 1:inserimento();
                   break;
            case 2:
                   classifica();
                   break;
            case 3:marcatori();
                   break;
            case 4:cout<<"Fine programma XD";
                   break;
        }
    }
    while(scelta!=4);
    return 0;
}



