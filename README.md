# AP1-EC-banco
## Nome:Gabriel guedes de oliveira
## Nº Matricula: 202104964

//#Gabriel guedes de oliveira
//#nº matricula 202104964


#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>

typedef struct cliente CLIENTE;
struct cliente{
char codigo[15];
char nome[30];
char cpf[15];
char fone[15];
char endereco[80];
};
typedef struct dados DADOS;
struct dados{
char codigo[15];
char nome[30];
char cpf[15];
char fone[15];
char endereco[80];
char agencia[15];
char numeroc[15];
long int saldo_long;	
char descricao[100];
char saldo[30];
};
typedef struct trans TRANS;
struct trans{
	long int saldo_long;
	char descricao[100];
	char agencia[15];
	char numeroc[15];
	char nome[30];
	char cpf[15];
	char codigo[15];
	char saldo[30];
	int dia;
	int mes;
	int ano;
	
};

  

void cabecalho();
void inputdata();
void listar();
void pesquisar();
void apagarcliente();
void editarcliente();
void cadastroconta();
void listarconta();
void pesquisarconta();
void saque();
void deposito();
void transferencia();
void extrato();

int main() {
 char opcao;
 char opcao2;
 char opcao3;
  

 while(opcao != 'S') {
	cabecalho();
   printf("=============== Bem vindo! =================\n");
   printf("Digite um comando para prosseguir:\n");
   printf("C - Gerenciar Clientes\n");
   printf("T - Gerenciar Contas\n");
   printf("S - Sair\n");
   scanf("%s", &opcao);

    switch(opcao){
      case 'C':
      case 'c':
      cabecalho();
      printf("============ Gerenciar Clientes  ============\n");
      printf("Digite um comando para prosseguir:\n");
      printf("C - Cadastrar um cliente\n");
      printf("L - Listar todos os clientes cadastrados\n");
      printf("B - Buscar cliente ja cadastrado\n");
      printf("A - Atualizar um cliente cadastrado\n");
      printf("E - Excluir um cliente cadastrado\n");
      printf("S - Sair\n");
      scanf("%s", &opcao2);
      

        switch(opcao2){
          case 'C':
		  case 'c':
          inputdata();
          break;
          case 'L':
          case 'l':	
          listar();
          break;
          case 'B':
          case 'b':
          pesquisar();
          break;
          case 'A':
          case 'a':
          editarcliente();
          break;
          case 'E':
          case 'e': 
		  apagarcliente();	
          break;
          default:
          printf("voltando pro menu!");
          getch();
          break;
          
          

        }
        break;

    
    
      case 'T':
      case 't':
      cabecalho();
        printf("Digite um comando para prosseguir:\n");
        printf("R - Listagem de todas as contas cadastradas.\n");
        printf("C - Cadastrar uma conta para um cliente.\n");
        printf("L - Listar todas as contas de um cliente.\n");
        printf("W - Realizar um saque em uma conta.\n");
        printf("D - Realizar um deposito em uma conta.\n");
        printf("T - Realizar transferencia entre contas.\n");
        printf("E - Exibir extrato de uma conta.\n");
        printf("S - Sair\n");
        scanf("%s", &opcao3);
        

          switch(opcao3){
            case 'R':
            	case 'r':
            listarconta();
            break;
            case 'C':
            case 'c':
            cadastroconta();
            break;
            case 'L':
            	case 'l':
            	pesquisarconta();
            break;
            case 'W':
            	case 'w':
            	saque();
            break;
            case 'D':
            	case 'd':
            		deposito();
            break;
            case 'T':
            	case 't':
            		transferencia();
            break;
            case 'E':
            	case 'e':
            		extrato();
            break;
            default:
          	printf("voltando para o menu!");
          	getch();
         	break;
            

          }
        break;
  case 's':
  	cabecalho();
  	printf("digite S maiusculo para sair!");
  	getch();
  break;    
  }



 }

}



void cabecalho(){
  system("cls");
}
void inputdata(){
  FILE* arquivo;
  
  CLIENTE cll;

  cabecalho();
  arquivo = fopen("arquivo.dat", "ab");

  if (arquivo == NULL){
    printf("problemas na abertura do arquivo!\n");
  } else {
    cabecalho();
    fflush(stdin);
    printf("digite um codigo:\n");
    gets(cll.codigo);

    fflush(stdin);
    printf("digite o nome:\n");
    gets(cll.nome);

    fflush(stdin);
    printf("digite o cpf:\n");
    gets(cll.cpf);

    fflush(stdin);
    printf("digite o telefone:\n");
    gets(cll.fone);

    fflush(stdin);
    printf("digite o endereco:\n");
    gets(cll.endereco);

    fwrite(&cll, sizeof(CLIENTE), 1, arquivo);

    fclose(arquivo);


  }
}
void listar(){
  FILE* arquivo;
  CLIENTE cll;

  arquivo = fopen("arquivo.dat", "rb");
  cabecalho();
  if (arquivo == NULL){
    printf("Nenhum cliente cadastrado.\n");
  } else {
    while ( fread(&cll, sizeof(CLIENTE), 1, arquivo)==1 ){
     printf("codigo: %s\n", cll.codigo);
     printf("nome: %s\n", cll.nome);
     printf("cpf: %s\n", cll.cpf);
     printf("telefone: %s\n", cll.fone);
     printf("endereco: %s\n", cll.endereco);
     printf("-----------------------------\n\n");

    }
  }
  fclose(arquivo);
  getch();
}
void pesquisar(){
  FILE* arquivo;
  CLIENTE cll;
  char nome[30];
  char codigo[15];
  char cpf[15];
  int tipo;

  cabecalho();
  arquivo = fopen("arquivo.dat", "rb");
  if (arquivo == NULL){
    printf("problemas na abertura do arquivo!\n");
  } else {
    printf("digite um comando para prosseguir\n");
    printf("1 - pesquisar por nome.\n");
    printf("2 - pesquisar por codigo.\n");
    printf("3 - pesquisar pro cpf.\n");
    scanf("%d", &tipo);
    switch(tipo){
      case 1:
      	cabecalho();
      fflush(stdin);
      printf("digite o nome a pesquisar: \n");
      gets(nome);
      while (fread(&cll, sizeof(CLIENTE), 1, arquivo)==1 ){
        if ( strcmp(nome, cll.nome )==0 ){
          printf("codigo: %s\n", cll.codigo);
          printf("nome: %s\n", cll.nome);
          printf("cpf: %s\n", cll.cpf);
          printf("telefone: %s\n", cll.fone);
          printf("endereco: %s\n", cll.endereco);
        }
      }
      break;
      case 2:
      	cabecalho();
      fflush(stdin);
      printf("digite o codigo a pesquisar: \n");
      gets(codigo);
      while (fread(&cll, sizeof(CLIENTE), 1, arquivo)==1 ){
        if ( strcmp(codigo, cll.codigo )==0 ){
          printf("codigo: %s\n", cll.codigo);
          printf("nome: %s\n", cll.nome);
          printf("cpf: %s\n", cll.cpf);
          printf("telefone: %s\n", cll.fone);
          printf("endereco: %s\n", cll.endereco);
        }
      }
      break;
      case 3:
      	cabecalho();
      fflush(stdin);
      printf("digite o cpf a pesquisar: \n");
      gets(cpf);
      while (fread(&cll, sizeof(CLIENTE), 1, arquivo)==1 ){
        if ( strcmp(cpf, cll.cpf )==0 ){
          printf("codigo: %s\n", cll.codigo);
          printf("nome: %s\n", cll.nome);
          printf("cpf: %s\n", cll.cpf);
          printf("telefone: %s\n", cll.fone);
          printf("endereco: %s\n", cll.endereco);
        }
      }
      break;
    

    }
  }
  
  fclose(arquivo);
  getch();

}


void apagarcliente(){
  	FILE* arquivo;
    FILE* temp;
    CLIENTE cll;
    char codigo[15];
    char cpf[15];
    int tipo1;
    char a;
    

	arquivo = fopen("arquivo.dat","rb");
	temp = fopen("tmp.dat","wb");

    if(arquivo == NULL && temp == NULL)
    {
	    printf("Não foi possível abrir o arquivo.txt\n");
	    getch();
    }
    else
    {
    	cabecalho();
    	printf("digite um comando para prosseguir\n");
    	printf("1 - pesquisar por codigo.\n");
    	printf("2 - pesquisar pro cpf.\n");
    	scanf("%d", &tipo1);
    	switch(tipo1){
    	case 1:
		cabecalho();
    	fflush(stdin);
    	printf("Digite o codigo do cliente que pertende apagar: \n");
    	gets(codigo);

    	while(fread(&cll, sizeof(CLIENTE), 1, arquivo) == 1)
    	{
        	if(strcmp(codigo, cll.codigo) == 0)
        	{
	            printf("codigo: %s\n", cll.codigo);
          printf("nome: %s\n", cll.nome);
          printf("cpf: %s\n", cll.cpf);
          printf("telefone: %s\n", cll.fone);
          printf("endereco: %s\n", cll.endereco);
				printf("-------------------------------------------\n\n");
        	}
	        else
	        {
	            fwrite(&cll, sizeof(CLIENTE), 1, temp);
	        }
	    }
        fclose(arquivo);
        fclose(temp);
        fflush(stdin);
        printf("Tem a certeza que pertende excluir os dados deste cliente(S/N)? \n");
        scanf("%s", &a);
	  	if(a == 'S' || a == 's')
	    {
	        if(remove("arquivo.dat") == 0 && rename ("tmp.dat", "arquivo.dat") == 0)
	            {
	            	
					
					printf("\n\ncliente excluido com sucesso!\n");
					getch();
	            }
	        else
	            {
	                remove("tmp.dat");
	            }
	    }
	    fclose(temp);
	    fclose(arquivo);
	    getch();
	    break;
	    case 2:
	    cabecalho();
    	fflush(stdin);
    	printf("Digite o cpf do cliente que pertende excluir: \n");
    	gets(cpf);

    	while(fread(&cll, sizeof(CLIENTE), 1, arquivo) == 1)
    	{
        	if(strcmp(cpf, cll.cpf) == 0)
        	{
	            printf("codigo: %s\n", cll.codigo);
          printf("nome: %s\n", cll.nome);
          printf("cpf: %s\n", cll.cpf);
          printf("telefone: %s\n", cll.fone);
          printf("endereco: %s\n", cll.endereco);
				printf("-------------------------------------------\n\n");
        	}
	        else
	        {
	            fwrite(&cll, sizeof(CLIENTE), 1, temp);
	        }
	    }
        fclose(arquivo);
        fclose(temp);
        fflush(stdin);
        printf("Tem a certeza que pertende excluir os dados deste cliente(S/N)? \n");
	  	scanf("%s", &a);
	  	if(a == 'S' || a == 's')
	    {
	        if(remove("arquivo.dat") == 0 && rename ("tmp.dat", "arquivo.dat") == 0)
	            {
	            
					
					printf("\n\ncliente excluido com sucesso!\n");
					getch();
	            }
	        else
	            {
	                remove("tmp.dat");
	            }
	    }
	    fclose(temp);
	    fclose(arquivo);
	    getch();	
	    break;
 	}
}
}



void editarcliente()
{
	FILE* arquivo;
    FILE* temp;
    CLIENTE cll;
    char codigo[15];
    char cpf[15];
    int tipo1;
    char a;
    

	arquivo = fopen("arquivo.dat","rb");
	temp = fopen("tmp.dat","wb");

    if(arquivo == NULL && temp == NULL)
    {
	    printf("Não foi possível abrir o arquivo.txt\n");
	    getch();
    }
    else
    {
    	cabecalho();
    	printf("digite um comando para prosseguir\n");
    	printf("1 - pesquisar por codigo.\n");
    	printf("2 - pesquisar pro cpf.\n");
    	scanf("%d", &tipo1);
    	switch(tipo1){
    	case 1:
		cabecalho();
    	fflush(stdin);
    	printf("Digite o codigo do cliente que pertende editar: \n");
    	gets(codigo);

    	while(fread(&cll, sizeof(CLIENTE), 1, arquivo) == 1)
    	{
        	if(strcmp(codigo, cll.codigo) == 0)
        	{
	            printf("codigo: %s\n", cll.codigo);
          printf("nome: %s\n", cll.nome);
          printf("cpf: %s\n", cll.cpf);
          printf("telefone: %s\n", cll.fone);
          printf("endereco: %s\n", cll.endereco);
				printf("-------------------------------------------\n\n");
        	}
	        else
	        {
	            fwrite(&cll, sizeof(CLIENTE), 1, temp);
	        }
	    }
        fclose(arquivo);
        fclose(temp);
        fflush(stdin);
        printf("Tem a certeza que pertende alterar os dados deste cliente(S/N)? \n");
        scanf("%s", &a);
	  	if(a == 'S' || a == 's')
	    {
	        if(remove("arquivo.dat") == 0 && rename ("tmp.dat", "arquivo.dat") == 0)
	            {
	            	FILE* ficheiro;
					CLIENTE cll;
					
					ficheiro = fopen("arquivo.dat", "ab");
	            	
	         cabecalho();
            fflush(stdin);
            printf("digite um codigo:\n");
            gets(cll.codigo);

            fflush(stdin);
            printf("digite o nome:\n");
            gets(cll.nome);

            fflush(stdin);
            printf("digite o cpf:\n");
            gets(cll.cpf);  

            fflush(stdin);
            printf("digite o telefone:\n");
            gets(cll.fone);

            fflush(stdin);
            printf("digite o endereco:\n");
            gets(cll.endereco);
					
					fwrite(&cll, sizeof(CLIENTE), 1, arquivo);
					
					printf("\n\ncliente alterado com sucesso!\n");
	            }
	        else
	            {
	                remove("tmp.dat");
	            }
	    }
	    fclose(temp);
	    fclose(arquivo);
	    getch();
	    break;
	    case 2:
	    cabecalho();
    	fflush(stdin);
    	printf("Digite o cpf do cliente que pertende editar: \n");
    	gets(cpf);

    	while(fread(&cll, sizeof(CLIENTE), 1, arquivo) == 1)
    	{
        	if(strcmp(cpf, cll.cpf) == 0)
        	{
	            printf("codigo: %s\n", cll.codigo);
          printf("nome: %s\n", cll.nome);
          printf("cpf: %s\n", cll.cpf);
          printf("telefone: %s\n", cll.fone);
          printf("endereco: %s\n", cll.endereco);
				printf("-------------------------------------------\n\n");
        	}
	        else
	        {
	            fwrite(&cll, sizeof(CLIENTE), 1, temp);
	        }
	    }
        fclose(arquivo);
        fclose(temp);
        fflush(stdin);
        printf("Tem a certeza que pertende alterar os dados deste cliente(S/N)? \n");
	  	scanf("%s", &a);
	  	if(a == 'S' || a == 's')
	    {
	        if(remove("arquivo.dat") == 0 && rename ("tmp.dat", "arquivo.dat") == 0)
	            {
	            	FILE* ficheiro;
					CLIENTE cll;
					
					ficheiro = fopen("arquivo.dat", "ab");
	            	
	         cabecalho();
            fflush(stdin);
            printf("digite um codigo:\n");
            gets(cll.codigo);

            fflush(stdin);
            printf("digite o nome:\n");
            gets(cll.nome);

            fflush(stdin);
            printf("digite o cpf:\n");
            gets(cll.cpf);  

            fflush(stdin);
            printf("digite o telefone:\n");
            gets(cll.fone);

            fflush(stdin);
            printf("digite o endereco:\n");
            gets(cll.endereco);
					
					fwrite(&cll, sizeof(CLIENTE), 1, arquivo);
					
					printf("\n\ncliente alterado com sucesso!\n");
	            }
	        else
	            {
	                remove("tmp.dat");
	            }
	    }
	    fclose(temp);
	    fclose(arquivo);
	    getch();	
	    break;
 	}
}
}


void cadastroconta(){
	FILE* arquivo;
	FILE* contas;
  CLIENTE cll;
  DADOS db;
  char codigo[15];
  char cpf[15];
  int tipo;
  float nada=0;
  
  cabecalho();
  arquivo = fopen("arquivo.dat", "rb");
  contas = fopen("contas.dat", "ab");
  if (arquivo == NULL){
    printf("problemas na abertura do arquivo!\n");
  } else {
    printf("digite um comando para prosseguir\n");
    printf("1 - pesquisar por codigo.\n");
    printf("2 - pesquisar pro cpf.\n");
    scanf("%d", &tipo);
    switch(tipo){
      case 1:
      	cabecalho();
      fflush(stdin);
      printf("digite o codigo do cliente: \n");
      gets(codigo);
     while (fread(&cll, sizeof(CLIENTE), 1, arquivo)==1 ){
        if ( strcmp(codigo, cll.codigo )==0 ){
          printf("nome: %s\n", cll.nome);
          printf("codigo: %s\n", cll.codigo);
          printf("cpf: %s\n", cll.cpf);
          printf("telefone: %s\n", cll.fone);
          printf("endereco: %s\n", cll.endereco);
		  printf("-------------------------------------------\n\n");
		  
		  strcpy(db.nome, cll.nome);
		  strcpy(db.cpf, cll.cpf);
		  strcpy(db.fone, cll.fone);
		  strcpy(db.endereco, cll.endereco);
		  strcpy(db.codigo, cll.codigo);
		  
         	
         	fflush(stdin);
            printf("digite o numero conta:\n");
            gets(db.numeroc); 
			    

            fflush(stdin);
            printf("digite o numero agencia:\n");
            gets(db.agencia); 
            
           
		   fflush(stdin);
           printf("digite 0 para continuar!\n");
            scanf("%ld", &db.saldo_long);
            
            
            fwrite(&db, sizeof(DADOS), 1, contas);
         
        }
      }
      printf("para finalizar o cadastro faca um deposito na conta!\n");
      break;
      case 2:
      	cabecalho();
      fflush(stdin);
      printf("digite o cpf do cliente: \n");
      gets(cpf);
     while (fread(&cll, sizeof(CLIENTE), 1, arquivo)==1 ){
        if ( strcmp(cpf, cll.cpf )==0 ){
         printf("nome: %s\n", cll.nome);
          printf("codigo: %s\n", cll.codigo);
          printf("cpf: %s\n", cll.cpf);
          printf("telefone: %s\n", cll.fone);
          printf("endereco: %s\n", cll.endereco);
		  printf("-------------------------------------------\n\n");
		  
		  strcpy(db.nome, cll.nome);
		  strcpy(db.cpf, cll.cpf);
		  strcpy(db.fone, cll.fone);
		  strcpy(db.endereco, cll.endereco);
		  strcpy(db.codigo, cll.codigo);
		  
         	
         	fflush(stdin);
            printf("digite o numero conta:\n");
            gets(db.numeroc); 
			    

            fflush(stdin);
            printf("digite o numero agencia:\n");
            gets(db.agencia); 
            
           fflush(stdin);
           printf("digite 0 para continuar!\n");
            scanf("%ld", &db.saldo_long);
            
            fwrite(&db, sizeof(DADOS), 1, contas);
         
        }
      }
      printf("para finalizar o cadastro faca um deposito na conta!\n");
      break;
    

    }
  }
  fclose(contas);
  fclose(arquivo);
  getch();

	
}
void listarconta(){
	FILE* trans;
	
    TRANS tr;
    DADOS db;
	
  trans = fopen("trans.dat", "rb");
 
  cabecalho();
  
		
  if (trans == NULL){
   printf("contas nao cadastradas!\n");
   getch();
  
   } else {
    while ( fread(&tr, sizeof(TRANS), 1, trans)==1 ){
     printf("nome: %s\n", tr.nome);
     printf("cpf: %s\n", tr.cpf);
     printf("agencia: %s\n", tr.agencia);
     printf("numero da conta: %s\n", tr.numeroc);
     
     
     printf("saldo: %s\n", tr.saldo);
    
     printf("-----------------------------\n\n");


    }
	}
  
  fclose(trans);
 
  getch();
}

void pesquisarconta(){
  FILE* trans;
  TRANS tr;
  char nome[30];
  char codigo[15];
  char cpf[15];
  int tipo;

  cabecalho();
  trans = fopen("trans.dat", "rb");
  if (trans == NULL){
    printf("Nenhuma conta cadastrada!\n");
  } else {
    printf("digite um comando para prosseguir\n");
    printf("1 - pesquisar por codigo.\n");
    printf("2 - pesquisar pro cpf.\n");
    scanf("%d", &tipo);
    switch(tipo){
      case 1:
      	cabecalho();
      fflush(stdin);
      printf("digite o codigo a pesquisar: \n");
      gets(codigo);
      while (fread(&tr, sizeof(TRANS), 1, trans)==1 ){
        if ( strcmp(codigo, tr.codigo )==0 ){
          printf("nome: %s\n", tr.nome);
		  printf("codigo: %s\n", tr.codigo);
          printf("cpf: %s\n", tr.cpf);
          printf("agencia: %s\n", tr.agencia);
          printf("numero da conta: %s\n", tr.numeroc);
          printf("saldo: %s\n", tr.saldo);
        } else {
        	printf("Nenhuma conta cadastrada!\n");
		}
      }
      break;
      case 2:
      	cabecalho();
      fflush(stdin);
      printf("digite o cpf a pesquisar: \n");
      gets(cpf);
      while (fread(&tr, sizeof(TRANS), 1, trans)==1 ){
        if ( strcmp(cpf, tr.cpf )==0 ){
          printf("nome: %s\n", tr.nome);
		  printf("codigo: %s\n", tr.codigo);
          printf("cpf: %s\n", tr.cpf);
          printf("agencia: %s\n", tr.agencia);
          printf("numero da conta: %s\n", tr.numeroc);
          printf("saldo: %s\n", tr.saldo);
        } else {
        	printf("Nenhuma conta cadastrada!\n");
		}
      }
      break;
    

    }
  }
  
  fclose(trans);
  getch();

}
void saque(){
	 FILE* trans;
	 FILE* trans2;
  DADOS db;
  TRANS tr;
  
  char conta[15];
  char agencia[15];
  int tipo, i;
  long int valor, vet[7];
  char valor1[10];

  cabecalho();
  trans = fopen("trans.dat", "rb");
  if (trans == NULL){
    printf("Nenhuma conta cadastrada!\n");
  } else {
    
      
      cabecalho();
      fflush(stdin);
      printf("digite o numero da agencia: \n");
      gets(agencia);
      
      fflush(stdin);
      printf("digite o numero da conta: \n");
      gets(conta);
      
      
      while (fread(&tr, sizeof(TRANS), 1, trans)==1 ){
        if ( strcmp(agencia, tr.agencia )==0 && strcmp(conta, tr.numeroc )==0){
          cabecalho();
		  printf("nome: %s\n", tr.nome);
		  printf("codigo: %s\n", tr.codigo);
          printf("cpf: %s\n", tr.cpf);
          printf("agencia: %s\n", tr.agencia);
          printf("numero da conta: %s\n", tr.numeroc);
          printf("saldo: %s\n", tr.saldo);
          
          
		  tr.saldo_long = atol(tr.saldo);
		  
          fclose(trans);
  
		  } else {
		  		printf("conta nao cadastrada!\n");
		  }
		  
		  fflush(stdin);
          printf("digite o valor do saque!\n");
          scanf("%ld", &valor);
          
          
          if ( strcmp(agencia, tr.agencia )==0 && strcmp(conta, tr.numeroc )==0){
          trans2 = fopen("trans.dat", "ab");
          
          if(valor <= tr.saldo_long){
          	tr.saldo_long = tr.saldo_long-valor;
          	ltoa(tr.saldo_long,tr.saldo,10);
          	
          	fflush(stdin);
			printf("digite a descricao da operacao realizada!\n");
          	gets(tr.descricao);
          	
          	
          	ltoa(valor,valor1,10);
		  
		  strcat(tr.descricao,"|R$-");
		  strcat(tr.descricao,valor1);
          fflush(stdin);
          printf("digite a data do saque ../../....\n");
          scanf("%d %d %d", &tr.dia, &tr.mes, &tr.ano);
          	
          	fwrite(&tr, sizeof(TRANS), 1, trans2);
          	
          	for(i = 0; i < 7; i++){
			vet[i] = 0;
		}
	
	
		while(valor >= 200){
			vet[0] ++;
			valor = valor - 200;
		}
		while(valor >= 100){
			vet[1] ++;
			valor = valor - 100;
		}
		while(valor >= 50){
			vet[2] ++;
			valor = valor - 50;
		}
		while(valor >= 20){
			vet[3] ++;
			valor = valor - 20;
		}
		while(valor >= 10){
			vet[4] ++;
			valor = valor - 10;
		}
		while(valor >= 5){
			vet[5] ++;
			valor = valor - 5;
		}
		while(valor > 2){
			vet[6] ++;
			valor = valor - 2;
		}
		printf("Quantidade de NOTAS SACADAS:\n");
		printf("%ld -- R$200\n", vet[0]);
		printf("%ld -- R$100\n", vet[1]);
		printf("%ld -- R$50\n", vet[2]);
		printf("%ld -- R$20\n", vet[3]);
		printf("%ld -- R$10\n", vet[4]);
		printf("%ld -- R$5\n", vet[5]);
		printf("%ld -- R$2\n", vet[6]);

          	fclose(trans2);
          	getch();
          	
          	
			  } else {
			cabecalho();
		  	printf("valor insuficiente!\n");
		  	getch();
			  }
        } else {
        	printf("conta nao cadastrada!\n");
		}
		
		
  	  }
}

}
void deposito(){
	FILE* contas;
	FILE* trans;
	
  DADOS db;
  TRANS tr;
 
  
 	char tm_mday3[5];
	char tm_mon3[5]; 
	char tm_year3[5];
  
  char conta[15];
  char agencia[15];
  int tipo;
  long int valor;
  char valor1[10];

  cabecalho();
  
  contas = fopen("contas.dat", "rb");
  trans = fopen("trans.dat", "ab");
  if (contas == NULL){
    printf("Nenhuma conta cadastrada!\n");
  } else {
    
      
      cabecalho();
      fflush(stdin);
      printf("digite o numero da agencia: \n");
      gets(agencia);
      
      fflush(stdin);
      printf("digite o numero da conta: \n");
      gets(conta);
      
      
      while (fread(&db, sizeof(DADOS), 1, contas)==1 ){
        if ( strcmp(agencia, db.agencia )==0 && strcmp(conta, db.numeroc )==0){
          cabecalho();
		  printf("nome: %s\n", db.nome);
		  printf("codigo: %s\n", db.codigo);
          printf("cpf: %s\n", db.cpf);
          printf("agencia: %s\n", db.agencia);
          printf("numero da conta: %s\n", db.numeroc);
          printf("saldo: %ld\n", db.saldo_long);
          
          
          fflush(stdin);
          printf("digite o valor do deposito!\n");
          scanf("%ld", &valor);
          
          
          	db.saldo_long = db.saldo_long+valor;
          	
          	
          	
          
          	fflush(stdin);
			printf("digite a descricao da operacao realizada!\n");
          	gets(db.descricao);
          
          
          strcpy(tr.nome, db.nome);
          strcpy(tr.codigo, db.codigo);
          strcpy(tr.cpf, db.cpf);
          strcpy(tr.agencia, db.agencia);
          strcpy(tr.numeroc, db.numeroc);
          strcpy(tr.descricao, db.descricao);
          
          tr.saldo_long=db.saldo_long;
  	
		  ltoa(db.saldo_long,db.saldo,10);
		  ltoa(valor,valor1,10);
		  strcpy(tr.saldo,db.saldo);
		  strcat(tr.descricao,"|R$+");
		  strcat(tr.descricao,valor1);
		  fflush(stdin);
          printf("digite a data do deposito ../../....\n");
          scanf("%d %d %d", &tr.dia, &tr.mes, &tr.ano);
          
          	fwrite(&tr, sizeof(TRANS), 1, trans);
         
		  
        } else {
        	printf("conta nao cadastrada!\n");
		} 
		  
		
  	  }
}
fclose(trans);
fclose(contas);
  getch();
}

void transferencia(){
	FILE* trans;
	FILE* trans2;
	TRANS tr;

	char conta[15];
  	char agencia[15];
  	char conta2[15];
  	char agencia2[15];
  	char valor1[10];
  	char valor2[10];
  	long int valor;
  	int i, j;
  		trans2 = fopen("trans.dat", "ab");
  	 trans = fopen("trans.dat", "rb");
  if (trans == NULL){
    printf("Nenhuma conta cadastrada!\n");
  } else {
  	cabecalho();
      fflush(stdin);
      printf("digite o numero da agencia da conta de origem: \n");
      gets(agencia);
      
      fflush(stdin);
      printf("digite o numero da conta de origem: \n");
      gets(conta);
      
      while (fread(&tr, sizeof(TRANS), 1, trans)==1 ){
        if ( strcmp(agencia, tr.agencia )==0 && strcmp(conta, tr.numeroc )==0){
          cabecalho();
		  printf("nome: %s\n", tr.nome);
		  printf("codigo: %s\n", tr.codigo);
          printf("cpf: %s\n", tr.cpf);
          printf("agencia: %s\n", tr.agencia);
          printf("numero da conta: %s\n", tr.numeroc);
          printf("saldo: %s\n", tr.saldo);
          
          
          fflush(stdin);
          printf("digite o valor que deseja transferir:\n");
          scanf("%ld", &valor);
          
          tr.saldo_long = atol(tr.saldo);
          if(valor <= tr.saldo_long){
          	tr.saldo_long = tr.saldo_long-valor;
          	ltoa(tr.saldo_long,tr.saldo,10);
          ltoa(valor,valor1,10);
          strcpy(tr.descricao,"Transferencia para conta:");
          strcat(agencia, "-");
          strcat(agencia, conta);
          strcat(tr.descricao, agencia);
          strcat(tr.descricao,"|R$-");
          strcat(tr.descricao,valor1);
          fflush(stdin);
          printf("digite a data do transferencia ../../....\n");
          scanf("%d %d %d", &tr.dia, &tr.mes, &tr.ano);
          printf("%s\n", tr.descricao);
          fwrite(&tr, sizeof(TRANS), 1, trans2);
} else {
        	printf("valor insuficiente!\n");
}
		
		fflush(stdin);
      printf("digite o numero da agencia da conta de destino: \n");
      gets(agencia2);
      
      fflush(stdin);
      printf("digite o numero da conta de destino: \n");
      gets(conta2);
      
      while (fread(&tr, sizeof(TRANS), 1, trans)==1 ){
        if ( strcmp(agencia2, tr.agencia )==0 && strcmp(conta2, tr.numeroc )==0){
        
		  printf("nome: %s\n", tr.nome);
		  printf("codigo: %s\n", tr.codigo);
          printf("cpf: %s\n", tr.cpf);
          printf("agencia: %s\n", tr.agencia);
          printf("numero da conta: %s\n", tr.numeroc);
          printf("saldo: %s\n", tr.saldo);
		
		tr.saldo_long = atol(tr.saldo);
		tr.saldo_long = tr.saldo_long+valor;
		ltoa(tr.saldo_long,tr.saldo,10);
		ltoa(valor,valor1,10);
	
		strcpy(tr.descricao,"Transferencia da conta:");
		 strcat(agencia2, "-");
          strcat(agencia2, conta2);
          strcat(tr.descricao, agencia2);
          strcat(tr.descricao,"|R$+");
          strcat(tr.descricao,valor1);
          
          printf("%s\n", tr.descricao);
          fflush(stdin);
          printf("digite a data do transferencia ../../....\n");
          scanf("%d %d %d", &tr.dia, &tr.mes, &tr.ano);
		fwrite(&tr, sizeof(TRANS), 1, trans2);
		
		} 


}
} else {
	printf("conta nao cadastrada!\n");
}
}

fclose(trans);
fclose(trans2);
getch();
}
}
void extrato(){
		 FILE* trans;
	

  TRANS tr;
  
  char conta[15];
  char agencia[15];
  int tipo;
  int dia1, dia2, mes1, mes2, ano1, ano2;
 

  cabecalho();
  trans = fopen("trans.dat", "rb");
  if (trans == NULL){
    printf("Nenhuma conta cadastrada!\n");
  } else {
    
      
      cabecalho();
      fflush(stdin);
      printf("digite o numero da agencia: \n");
      gets(agencia);
      
      fflush(stdin);
      printf("digite o numero da conta: \n");
      gets(conta);
      
      
      fread(&tr, sizeof(TRANS), 1, trans)==1; 
        if ( strcmp(agencia, tr.agencia )==0 && strcmp(conta, tr.numeroc )==0){
          cabecalho();
		  printf("nome: %s\n", tr.nome);
		  printf("codigo: %s\n", tr.codigo);
          printf("cpf: %s\n", tr.cpf);
          printf("agencia: %s\n", tr.agencia);
          printf("numero da conta: %s\n", tr.numeroc);
          printf("saldo: %s\n", tr.saldo);
          
          printf("deseja ver o extrato da data de:\n");
          scanf("%d %d %d", &dia1, &mes1, &ano1);
          printf("ate a data de:\n");
          scanf("%d %d %d", &dia2, &mes2, &ano2);
          
          
         
          
          
          if(dia1<tr.dia<dia2 && mes1<tr.mes<mes2 && ano1<tr.ano<ano2){
          	printf("data %02d/%02d/%d|", tr.dia, tr.mes, tr.ano);
          	printf("descricao:%s", tr.descricao);
		  } 
          
      } else {
      	printf("conta nao encontrada!\n");
	  }
  }
  fclose(trans);
getch();
}

