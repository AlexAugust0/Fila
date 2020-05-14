#include <stdio.h>
#include <stdlib.h>


struct Node{
	int num;
	struct Node *prox;
};typedef struct Node node;




void iniciar(node *fila){
	fila->prox=NULL;
	
}

node *newnode(){
	node *novo=(node*)malloc(sizeof(node));
	if(!novo){
		printf("Memoria indisponivel\n");
		exit(0);
	}else{
		printf("Novo numero: \t");
		scanf("%d",&novo->num);
		printf("\n");
		return novo;
	}
	
}

int vazia(node *fila){
	if (fila->prox==NULL){
	return 1;
	}else{
		return 0;
	}
}

int inserir(node *fila){
	node *novo=newnode();
	novo->prox=NULL;
	
	
		if(vazia(fila))
		fila->prox=novo;
	else{
		node *temp= fila->prox;
		while(temp->prox !=NULL)
		temp = temp->prox;
		temp->prox=novo;
	}
	
	
}

node *remover(node *fila){
	if(fila->prox == NULL){
		printf("A Fila esta vazia.\n\n");
		return NULL;
	}else{
		node *temp=fila->prox;
		fila->prox=temp->prox;
		return temp;
	}
}

void exibir(node *fila){
	if (vazia(fila)){
		printf("A fila esta vazia\n");
		printf("\n");
		return ;
	}else{
		node *temp;
		temp=fila->prox;
		printf("Fila: ");
		while(temp != NULL){
			printf("%5d",temp->num);
			temp = temp->prox;
		}
		printf("\n\n");
	}
}

void Limpar(node *fila){
	if(!vazia(fila)){
		node *proxnode,*atual;
		atual=fila->prox;
		while(atual != NULL){
			proxnode= atual->prox;
			free(atual);
			atual=proxnode;
		}
	}
}

int menu(){
	int opt;
	
	printf("Digite o numero correspondente a opcao desejada.\n");
	printf("0 - SAIR\n");
	printf("1 - INSERIR NUMERO NA FILA\n");
	printf("2 - RETIRAR NUMERO DA FILA\n");
	printf("3 - EXIBIR A FILA\n");
	printf("4 - LIMPAR FILA\n");
	printf("\n");
	scanf("%d",&opt);
	return opt;
	
}

void opcoes(node *fila,int opt){
	node *temp;
	switch(opt){
		case 0:
			system ("pause");
			break;
		case 1:
			(inserir(fila));
						
			break;
		case 2:
			temp=remover(fila);
		if (temp != NULL){
			printf("Numero %3d retirado com sucesso!\n",temp->num);
			printf("\n");
			free(temp);
		}	break;
		case 3:
			exibir(fila);
			break;
		case 4:
			Limpar(fila);
			printf("Fila foi Zerada! \n");
			printf("\n");
			iniciar(fila);
			break;
			default:
				printf("Escolha invalida por favor tente novamente.\n");
	}	
	
}

int main(){
	int opt;
	Node *fila=(struct Node*)malloc(sizeof(struct Node));
	if(!fila){
		printf("Memoria indisponivel");
		exit(4);
	}else{
		iniciar(fila);
		do{
			opt=menu();
			opcoes(fila,opt);
		}while(opt);
	}
	free(fila);
	
	
	return 0;
}
