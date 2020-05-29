# JanoAbiezer
ATIVIDADE ED1

#include<stdlib.h> 
#include<stdio.h>


struct Fila {

	int elementosdafila;
	float *valores;
	int primeiro;
	int ultimo;
	int itens; 

};

void criarFila( struct Fila *f, int x ) { 

	f->elementosdafila = x;
	f->valores = (float*) malloc (f->elementosdafila * sizeof(float));
	f->primeiro = 0;
	f->ultimo = -1;
	f->itens = 0; 

}

void inserir(struct Fila *f, int v) {

	if(f->ultimo == f->elementosdafila-1)
		f->ultimo = -1;

	f->ultimo++;
	// incrementa ultimo e insere
	f->valores[f->ultimo] = v; 
	f->itens++; 

}

// item do começo da fila
int remover( struct Fila *f ) { 

// pega o valor e incrementa o primeiro
	int temp = f->valores[f->primeiro++]; 

	if(f->primeiro == f->elementosdafila)
		f->primeiro = 0;
		
//um item retirado
	f->itens--;  
	return temp;

}

// retorna verdadeiro quando a fila estiver vazia
int estaVazia( struct Fila *f ) { 

	return (f->itens==0);

}

// retorna verdadeiro quando a fila estiver cheia
int estaCheia( struct Fila *f ) { 

	return (f->itens == f->elementosdafila);
}

void mostrarFila(struct Fila *f){

	int cont, i;

	for ( cont=0, i= f->primeiro; cont < f->itens; cont++){

		printf("%.2f\t",f->valores[i++]);

		if (i == f->elementosdafila)
			i=0;

	}
	printf("\n\n");

}

int main () {

	int opcao, y;
	float valor;
	struct Fila umaFila;

	// cria a fila
	printf("\nelementosdafila: ");
	scanf("%d",&y);
	criarFila(&umaFila, y);

	// apresenta menu
	while( 1 ){

		printf("\n1 - Inserir elemento\n2 - Remover elemento\n3 - Mostrar Fila\n0 - Sair\n\nOpcao: ");
		scanf("%d", &opcao);

		switch(opcao){

			case 0: exit(0);

			case 1: // insere elemento
				if (estaCheia(&umaFila)){

					printf("\nFila Cheia!!!\n\n");

				}
				else {

					printf("\nValor do elemento a ser inserido: ");
					scanf("%f", &valor);
					inserir(&umaFila,valor);

				}

				break;

			case 2: // remove elemento
				if (estaVazia(&umaFila)){

					printf("\nFila vazia!!!\n\n");

				}
				else {

					valor = remover(&umaFila);
					printf("\n%1f removido com sucesso\n\n", valor) ; 

				}
				break;

				case 3: // mostrar fila
					if (estaVazia(&umaFila)){

						printf("\nFila vazia!!!\n\n");

					}
					else {

						printf("\nConteudo da fila => ");
						mostrarFila(&umaFila);

					}
					break;

				default:
					printf("\opcao Invalida\n\n");

		}
	}
}
