#include <locale.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <math.h>
#include <time.h>
#include <stdbool.h>
//Constantes do GAME
#define MAX_ITENS 10
#define MAX_VALOR 100
#define MAX_VIDA 150
#define MAX_PODER 200
#define PFIS 6
#define PMEN 6
#define MAX_NOME 40

//Inicialização de personagem

#define PODER_INICIAL 20
#define VIDA_INICIAL 80
#define DINHEIRO_INICIAL 100

//Estrutura do Item
typedef struct
{

	char nome[MAX_NOME];
	int valor;
	int preco;
	int dano;

}Item;

//Struct principal - Personagem
typedef struct
{

	char nome[MAX_NOME];
	int vida;
	int poder;
	int dinheiro;
	char itens[10][MAX_NOME];


}Personagem;

//Distribuição de pontuação
typedef struct
{
	int forca;
	int constituicao;
	int destreza;
	int agilidade;
}pFis;

typedef struct
{
	int inteligencia;
	int forcaDeVon;
	int percepcao;
	int carisma;
}pMen;
//*
int dado();
int jaTem(Personagem p, Item it);
void verInventario(Personagem p);
Personagem adicionarItem(Personagem p, Item i);
Personagem removerItem(Personagem p, Item it);
Personagem criarPersonagem(char nome[MAX_NOME],pFis pFis,pMen pMen);
void Pergunta(int x);
void inicioJogo();
pFis solpFis(int forca,int const,int destreza,int agilidade);
pMen solpMen(int inteligencia, int forcaDeVon,int percepcao,int carisma);
Personagem jogador;
Item pistola;

Personagem p;
int main()
{
    setlocale(LC_ALL,"portuguese");

    int x;
    char nome[20];
    /*
    printf("Digite o numero 1 para iniciar a historia: ");
    scanf("%d",&x);
    */
    system("color 02");
    while(x!=1)
    {
        printf("\nDIGITE 1 PARA COMEÇAR\n");
        scanf("%s",&nome);

        if(strcmp(strlwr(nome),"1")==0)
        {
            system("cls");
            Pergunta(1);

        }
        x++;

    }

    Pergunta(x);
    Item maca;
	strcpy(maca.nome,"Maçã");
	maca.valor = 20;
	maca.preco = 100;

	Item espada;
	strcpy(espada.nome,"Espada");
	espada.valor = 30;
	espada.preco = 100;
	    //FIM DA AREA DE ITENS




	//Inicialização do Personagem Exemplificação
	/*
		As proximas 2 linhas instancia um novo personagem com os atributos iniciais definidos nas
		primeiras linhas de codigo desse arquivo, são constantes e vão ajudar na manutenção se caso precise
		Chama o struct e logo em seguida atribui a ele a função criarPersonagem
		Essa função retorna um personagem novo com os parametros passados pra ela, lembrando da ordem
		criarPersonagem(NOME,VIDA,PODER,DINHEIRO)
		não da pra passar itens no criarPersonagem

		Personagem p;
		p = criarPersonagem("Lucas",pFis,pMen);

		 as proximas 12 linhas adiciona 12 itens, enchendo o inventario e mostrando oque acontece
		 quando ele fica lotado, pra adicionar qualquer item basta chamar a função adicionarItem passando dois parametros
		 um vai ser o proprio personagem e o outro o item a adicionar que foi inicializado no começo do codigo.

		 SEMPRE QUE FOR ADICIONAR UM ITEM, SEMPRE ATRIBUIR AO PERSONAGEM
		 a função retorna um novo personagem com o item adicionado
		 só da pra adicionar um item de cada modelo

		 p = adicionarItem(p,maca)
		 p = adicionarItem(p,maca)
		 p = adicionarItem(p,maca)
		 p = adicionarItem(p,maca)
		 p = adicionarItem(p,maca)
		 p = adicionarItem(p,maca)
		 p = adicionarItem(p,maca)
		 p = adicionarItem(p,maca)
		 p = adicionarItem(p,maca)
		 p = adicionarItem(p,maca)
		 p = adicionarItem(p,maca)
		 p = adicionarItem(p,maca)

		 Pra remover um item do inventario:

		 p = removerItem(p,maca)

		 Pra ver o inventario:

		 verInventario(p)


		VARIAVEL GLOBAL JOGADOR
		para o personagem


		Personagem p;
		p = criarPersonagem("Lucas",pFis,pMen);

        p= criarPersoangem("peter",pFis,pMen);

        p= adicionarItem(p,maca);
		p = adicionarItem(p,maca);
		p = adicionarItem(p,espada);

		printf("Adiciona maca e espada \n");
		verInventario(p);


		p = removerItem(p,maca);
		printf("Remove Maca \n");
		verInventario(p);

		printf("Adiciona maca \n");
		p = adicionarItem(p,maca);
		verInventario(p);

		funcao dado()
		retorna um valor aleatorio de 1 a 6





/*
    Item ar15;
    strcpy(ar15.nome,"AR15");
    ar15.preco=10;
    ar15.dano=30;
    ar15.dano=jogador.vida-ar15.dano;
     p= adicionarItem(p,ar15);
     */



    /*
    strcpy(pistola[3].nome,"TH40c");
    pistola[3].preco=20;
    pistola[3].valor=30;
    */
 return 0;
}


int dado(){

	int x = 1 + (rand()%6);
	return x;
}

int jaTem(Personagem p, Item it){
	int i = 0;
	while(i<10){
		if(!(strlen(p.itens[i]) == 0)){
			// Posição no iventario não vazia
			if(strcmp(strlwr(p.itens[i]),strlwr(it.nome)) == 0){
				//Verifica a existencia do item

				return 1;
				break;
			}
			return 0;
		}
		i++;
	}
}


void verInventario(Personagem p){
	int i;
	for(i  =0; i<10; i++){
		printf("Posição: %d Item: %s \n",i,p.itens[i]);
	}
}


Personagem adicionarItem(Personagem p, Item it){
	int i = 0;
	int temEspaco = 0;
	if(jaTem(p,it) == 0){
		while(i<10){
			if(strlen(p.itens[i]) == 0){
				// Posição no iventario vazia

				strcpy(p.itens[i],it.nome);
				temEspaco = 1;
				break;
			}
			i++;
		}
		if(temEspaco == 1){
				printf("Você recebeu o item: %s \n",it.nome);
		}else{
				printf("Você não tem Espaço para receber o(a) %s \n",it.nome);
		}
	}else{
		printf("Você já possui o item\n");
	}
	return p;
}


Personagem removerItem(Personagem p, Item it){
	int i = 0;
	while(i<10){
		if(!(strlen(p.itens[i]) == 0)){
			// Posição no iventario não vazia
			if(strcmp(p.itens[i],it.nome) == 0){
				//Remove o item que foi solicitado
				strcpy(p.itens[i],"");
				printf("Item %s removido \n",it.nome);
				break;
			}else{
				printf("[ERRO]Não tem o item %s \n",it.nome);
			}
			break;
		}
		i--;
	}
	return p;
}

pFis solpFis(int forca,int consti,int destreza,int agilidade){
	pFis p;
	p.forca = forca;
	p.constituicao = consti;
	p.destreza = destreza;
	p.agilidade = agilidade;
	return p;
}
pMen solpMen(int inteligencia, int forcaDeVon,int percepcao,int carisma){
	pMen p;
	p.inteligencia = inteligencia;
	p.forcaDeVon = forcaDeVon;
	p.percepcao = percepcao;
	p.carisma = carisma;
	return p;
}
Personagem criarPersonagem(char nome[MAX_NOME],pFis pFis,pMen pMen){

	Personagem p;
	strcpy(p.nome,nome);
	p.dinheiro = DINHEIRO_INICIAL;
	p.vida = VIDA_INICIAL;
	p.poder = floor((pFis.forca + pMen.forcaDeVon + pFis.agilidade + pFis.destreza)/4) * PODER_INICIAL;
	return p;
}
    char nom2[20];
    bool r;
    int DANOP=30;
    int DANOS=40;

     int i=1;
    Personagem ope;
    pMen pontos_mentais;
    pFis pontos_fisicos;
    Item itens;
    Item maca;
    Item ar15;
    Item faca;
    Item fuzil;
    Item espingarda;
    Item uzi;
    Item pistola38;
    int v;
void Pergunta(int x){
    system("color 02");
    ar15.valor=20;
    ar15.preco=40;
    strcpy(ar15.nome,"AR15");
    maca.valor=20;
    strcpy(maca.nome,"Maçã");
    faca.valor=20;
    faca.preco=13;
    strcpy(faca.nome,"Faca Tática");
    fuzil.valor=40;
    fuzil.preco=27;
    strcpy(fuzil.nome,"Fuzil");
    espingarda.valor=50;
    espingarda.valor=30;
    strcpy(espingarda.nome,"Espingarda");
    uzi.valor=40;
    uzi.preco=30;
    strcpy(uzi.nome,"UZI");
    strcpy(pistola38.nome,"Pistola-38");
    pistola38.valor=10;
    pistola38.preco=17;
    strcpy(pistola.nome,"Pistola 9mm");
    pistola.preco=10;
    pistola.valor=15;

    //pMen pontos_mentais;
    //pFis pontos_fisicos;
    char nome[MAX_NOME];
	char opcao[3] = "";
	switch(x){
	    /*
Estilo missão impossível:
Força - 2
Constituição - 1
Destreza – 2
Agilidade –  1

Inteligência - 2
Força de Vontade - 2
Percepção - 1
Carisma - 1

Estilo Jason Bourne
Força - 2
Constituição - 2
Destreza - 1
Agilidade – 1

Inteligência - 2
Força de Vontade - 1
Percepção - 2
Carisma - 1

Estilo 007
Força - 1
Constituição - 2
Destreza - 1
Agilidade – 1

Inteligência - 2
Força de Vontade - 1
Percepção - 1
Carisma – 3

*/
		case(1):
        pontos_fisicos = solpFis(2,1,2,3);// Adicionar os atributos.
        pontos_mentais = solpMen(2,2,1,1);// Adicionar Atributos
        printf("\nBem vindo ao game Underground");
		printf("\nQuem é Você, Heroi?");
		printf("\nDigite seu Nome:");
		scanf("%s",&nome);
		fflush(stdin);
		printf("\nBem vindo %s, agora\nEm qual estilo você se encaixa?",nome);
		printf("\n(1) Missão Impossivel");
		printf("\n(2) Jason Bourne");
		printf("\n(3) 007\n");
		int hur=0;
		int op;
		scanf("%d",&op);
		fflush(stdin);
		switch(op){
			case 1:
				pontos_fisicos = solpFis(2,1,2,5);
				pontos_mentais = solpMen(2,2,1,1);
                ope.vida=100;
				printf("\nDistribuição de Pontos - Missão Impossivel\n-----------FISICO:-----------\n");
				printf("Força: %d\n",pontos_fisicos.forca);
				printf("Constituição:%d\n",pontos_fisicos.constituicao);
				printf("Destreza:%d\n",pontos_fisicos.destreza);
				printf("Agilidade:%d\n",pontos_fisicos.agilidade);
                printf("hp do Personagem:%d\n",ope.vida);
                printf("Poder do Personagem:%d\n",ope.poder);
				printf("\nDistribuição de Pontos - Missão Impossivel\n-----------MENTAL:-----------\n");
				printf("Inteligencia: %d\n",pontos_mentais.inteligencia);
				printf("Força de Vontade:%d\n",pontos_mentais.forcaDeVon);
				printf("Percepção:%d\n",pontos_mentais.percepcao);
				printf("Carisma:%d\n",pontos_mentais.carisma);

			break;
			case 2:
				pontos_fisicos = solpFis(2,2,1,5);
				pontos_mentais = solpMen(2,1,2,1);
                ope.vida=100;
                ope.poder=50;
				printf("\nDistribuição de Pontos - Jason Bourne\n-----------FISICO:-----------\n");
				printf("Força: %d\n",pontos_fisicos.forca);
				printf("Constituição:%d\n",pontos_fisicos.constituicao);
				printf("Destreza:%d\n",pontos_fisicos.destreza);
				printf("Agilidade:%d\n",pontos_fisicos.agilidade);
				printf("hp do Personagem:%d\n",ope.vida);
                printf("Poder do Personagem:%d\n",ope.poder);
				printf("\nDistribuição de Pontos - Jason Bourne\n-----------MENTAL:-----------\n");
				printf("Inteligencia: %d\n",pontos_mentais.inteligencia);
				printf("Força de Vontade:%d\n",pontos_mentais.forcaDeVon);
				printf("Percepção:%d\n",pontos_mentais.percepcao);
				printf("Carisma:%d\n",pontos_mentais.carisma);

			break;
			case 3:

				pontos_fisicos = solpFis(1,2,2,5);
				pontos_mentais = solpMen(2,1,1,2);
                ope.vida=100;
                ope.poder=50;
				printf("\nDistribuição de Pontos - 007\n-----------FISICO:-----------\n");
				printf("Força: %d\n",pontos_fisicos.forca);
				printf("Constituição:%d\n",pontos_fisicos.constituicao);
				printf("Destreza:%d\n",pontos_fisicos.destreza);
				printf("Agilidade:%d\n",pontos_fisicos.agilidade);
                printf("hp do Personagem:%d\n",ope.vida);
                printf("Poder do Personagem:%d\n",ope.poder);
				printf("\nDistribuição de Pontos - 007\n-----------MENTAL:-----------\n");
				printf("Inteligencia: %d\n",pontos_mentais.inteligencia);
				printf("Força de Vontade:%d\n",pontos_mentais.forcaDeVon);
				printf("Percepção:%d\n",pontos_mentais.percepcao);
				printf("Carisma:%d\n",pontos_mentais.carisma);

				//printf("Dritibuiçao de itens - 007\n--------------ITENS----------------\n");
				//printf("\nItens: \nNome = %s\nPreço = %d\nPoder = %d\n",pistola[1].nome,pistola[1].preco,pistola[1].valor);

            break;

        }
       // scanf("%d",&hur);
        //printf("Dinheiro do jogador=%d\n Itens do jogador=%d\nNome do jogador%s\nPoder do jogador%d",jogador.dinheiro,jogador.itens,jogador.nome,jogador.poder);
        jogador = criarPersonagem(nome,pontos_fisicos,pontos_mentais);
        char opcao[30];
        //printf("\nO Tipo de JOgo que o senho escolheu foi: %s\n",jogador);
        system("pause");
        system("cls");
        printf("\n|-------------------------------------------------------------------------------------------------------------|\n");
        printf("\nCarga desconhecida chega ao porto de Suape com destino de entrega para o carnaval de Olinda. Contendo material");
		printf("\ndesconhecido, no container está escrito: Prefeitura da Cidade do Recife. O conteúdo da carga tem como objetivo\n");
		printf("cometer um dos maiores atentados da história do Brasil. Até o momento o seu conteúdo dentro do container é um");
		printf("\nmistério...\n");
        printf("\n|-------------------------------------------------------------------------------------------------------------|\n");
		system("pause");
        system("cls");
        printf("\n|-------------------------------------------------------------------------------------------------------------|\n");
        printf("\n                                      Dia 20 de dezembro, Recife, UFPE.\n                                        ");
        printf("\n|-------------------------------------------------------------------------------------------------------------|\n");

        printf("O Aluno fecha a porta e de longe você escuta a palavra “BABACA!”.Você até que poderia abrir a porta para trocar\n");
		printf("algumas ofensas com o aluno, mas FELIZMENTE hoje é um dia feliz,  SIM! Hoje é o seu último dia de aula a partir\n");
		printf("do momento em que você colocar os pés pra fora da faculdade você estará de férias. Ao apagar a luz e ao sair da\n");
		printf("sala você se depara com Suzana, secretária do departamento de Química.\n");
        printf("\nSuzana: Professor tem uma pessoa querendo falar urgentemente com o senhor, eu até disse que o senhor estava\nocupado, mas...\n");

        printf("\nUm dos soldados do Exercito: Senhor %s, precisa vir comigo agora!\n",nome);
        printf("\n            WRITE THE NUMBER OF OPTION AND PRESS ENTER:               \n");
        printf("\nOpção(1)- Você vai com eles sem pestanejar.\n");
        printf("opção (2)- Usa seu Carisma para perguntar do que se trata\n");
        printf("Opção (3)- Faz Uso da força para se desvencilhar dos soldados e fugir\n ");








        //jogador = criarPersonagem(nome,pontos_fisicos,pontos_mentais);





        Pergunta(2);
        int o;
		case(2):

            system("pause");
            system("cls");
            printf("\nUm dos soldados do Exercito: Senhor %s, precisa vir comigo agora!\n",nome);
            printf("\n            WRITE THE NUMBER OF OPTION AND PRESS ENTER:               \n");
            printf("\nOpção(1)- Você vai com eles sem pestanejar.\n");
            printf("opção (2)- Usa seu Carisma para perguntar do que se trata\n");
            printf("Opção (3)- Faz Uso da força para se desvencilhar dos soldados e fugir\n ");
            gets(opcao);
            fflush(stdin);

                 if(strcmp(strlwr(opcao),"1") == 0){
                    printf("Você entra no carro em silêncio, durante o percurso percebe que o seu destino é o Aeroporto dos\nGuararapes.\n\n");


                    Pergunta(3);
                }else if(strcmp(strlwr(opcao),"2")==0){
                    printf("Você entra no carro em silêncio, durante o percurso percebe que o seu destino é o Aeroporto dos\nGuararapes.\n\n");

                    Pergunta(3);
                }
                else if(strcmp(strlwr(opcao),"3")==0)
                {
                    printf("Você consegue se desvencilhar de um dos soldados, porém acaba  imobilizado pelo outro soldado,\npor uma arma de choque, depois de imobilizado.\n\n");
                    Pergunta(3);


                }
                else{
                Pergunta(2);
                }








            //printf("%d",dado());

		break;

		case(3):
		    system("pause");
            system("cls");
            printf("\nVocê está sentado no banco de trás e sua localização é a Avenida Recife, os soldados estão\nmeio que brigando pra ver quem comanda o som do carro, e ao passar pela Churrascaria Sal e\nBrasa um dos soldados fala...\n");
		 	printf("\nSoldado: JÁ COMI CARNE DE JAVALI NESSE LUGAR. O SENHOR JÁ COMEU CARNE DE JAVALI, PROFESSOR?\n");
		 	printf("\n                        WRITE THE NUMBER OF OPTION AND PRESS ENTER:                        \n");
            printf("\nopção(1):sim\nopção(2):não\nopção(3):Ficar em silêncio-+1 de inteligência\n");
            gets(opcao);
            fflush(stdin);


                if(strcmp(strlwr(opcao),"1") == 0){

                    printf("\nDepois de responder a pergunta você encosta a cabeça no apoio, ao som de Pode Balançar, do Mc Troia.\n");
                    printf("\nChegando no Aeroporto, o carro pega uma rota de acesso direto a pista de pouso.\nO carro estaciona há uns dez metros de distância de um helicóptero.\nAo sair do carro, sendo escoltado pelos soldados você se depara com um senhor de óculos\ne cabelo grisalho usando uma camiseta do Jurassic Park.\n\n");
                    Pergunta(4);
                }
                else if(strcmp(strlwr(opcao),"2")==0){

                    printf("\nDepois de responder a pergunta você encosta a cabeça no apoio, ao som de Pode Balançar, do Mc Troia.\n");
                    printf("\nChegando no Aeroporto, o carro pega uma rota de acesso direto a pista de pouso.\nO carro estaciona há uns dez metros de distância de um helicóptero.\nAo sair do carro, sendo escoltado pelos soldados você se depara com um senhor de óculos\ne cabelo grisalho usando uma camiseta do Jurassic Park.\n\n");

                    Pergunta(4);
                }
                else if(strcmp(strlwr(opcao),"3")==0){

                    pontos_mentais.inteligencia=pontos_mentais.inteligencia+i;
                    printf("\nDepois de responder a pergunta você encosta a cabeça no apoio, ao som de Pode Balançar, do Mc Troia.\n\n- adicionado mais um ponto de inteligência +1 |Intelgência Atual -> %d|\n\n",pontos_mentais.inteligencia);
                    printf("\nChegando no Aeroporto, o carro pega uma rota de acesso direto a pista de pouso. O carro\nestaciona há uns dez metros de distância de um helicóptero. Ao sair do carro, sendo\nescoltado pelos soldados você se depara com um senhor de óculos\ne cabelo grisalho usando uma camiseta do Jurassic Park.\n");
                    Pergunta(4);
                }

                else{
                Pergunta(3);
                }



		break;
		case(4):
		    system("pause");
		    system("cls");
            printf("\nO senhor se aproxima de você e estende a mão para cumprimentá-lo....\n");
            printf("Você irá cumprimentalo?\nResponda com 'sim' ou 'não'\n");
            printf("Opção(1):sim\n");
            printf("Opção(2):não\n");
            gets(opcao);
            fflush(stdin);

            if(strcmp(strlwr(opcao),"1") == 0){
                printf("\nVocê aperta a mão dele.\n");
                Pergunta(5);
            }else if(strcmp(strlwr(opcao),"2")==0){
                printf("\nVocê não aperta a mão dele\n");
                Pergunta(5);
            }
            else{
                Pergunta(4);
            }

        break;
		case(5):
		    system("pause");
            system("cls");
            printf("\nJoão: Professor %s, eu li o seu relatório... Plataforma P-36 em 2001,\nDeepwater Horizon 2010 e rompimento da Samarco em 2015, você fez um trabalho incrível lá.\nPrazer! Meu nome é João, faço parte do 1º Batalhão de Defesa Química,\nindependente a situação, é um prazer conhecê-lo.\n",jogador.nome);
            printf("opção(1):Gostei da camisa- +1 de carisma\n");
            printf("opção(2):Sim! Era para eu estar de férias hoje.\n");
            gets(opcao);
            fflush(stdin);

            if(strcmp(strlwr(opcao),"1") == 0){
                //jogador = criarPersonagem(nome,pontos_fisicos,pontos_mentais);
                pontos_mentais.carisma=pontos_mentais.carisma + i;
                printf("\n-carisma atribuido +1 agora vc tem %d de carisma-\n",pontos_mentais.carisma);
                printf("\nAo entrar no helicóptero você depara com o homem de cabelos grisalhos \ne roupa do exército brasileiro.");
                Pergunta(6);
            }else if(strcmp(strlwr(opcao),"2") == 0){
                printf("\nAo entrar no helicóptero você depara com o homem de cabelos grisalhos e roupa do exército brasileiro.\n");
                Pergunta(6);
            }
            else{
                Pergunta(5);
            }


           break;
        case(6):
            system("pause");
            system("cls");
            printf("\nJan:Você trouxe um professor universitário pra salvar o Brasil!? EU REALMENTE NÃO ACREDITO!\n");
            printf("Opção(1):A faculdade me paga bem cara!\n");
            printf("Opção(2):Como assim! Salvar o Brasil?\n");
            gets(opcao);
            fflush(stdin);

                if(strcmp(strlwr(opcao),"1")==0)
                {
                    printf("\nJoão: Esse Tabacudo aí é o Jan, ele trabalhou para inteligência nacional, um dos únicos\nanalistas brasileiros que trabalhou no desastre de Chernobyl. E sim professor!\nO senhor foi chamado para uma missão que pode salvar o Brasil de uma grande catástrofe.\n");
                    Pergunta(7);

                }
                else if(strcmp(strlwr(opcao),"2")==0){
                    printf("\nJoão: Esse Tabacudo aí é o Jan, ele trabalhou para inteligência nacional, um dos únicos\nanalistas brasileiros que trabalhou no desastre de Chernobyl. E sim professor!\nO senhor foi chamado para uma missão que pode salvar o Brasil de uma grande catástrofe.\n");
                    Pergunta(7);
                }
                else{
                    Pergunta(6);
                }


            break;

        case(7):
            system("pause");
            system("cls");
            printf("\nJan: Então %s, chegou um carregamento no Porto de Suape contendo uma substância química, o mesmo encontrado em Goiás.\nEsse carregamento tinha como objetivo abastecer um galpão localizado em Olinda.\nSão mais de 80 quilos de material químico. Nosso objetivo é saber de onde veio e carga e pegar os filhos da mãe.\n",jogador.nome);
            printf("\nOpção(1):Então, o que estamos esperando!?Dá a partida nisso aí, cara.\n");
            printf("\nOpção(2):É muita responsabilidade...Eu tenho alguma outra alternativa?\n");
            gets(opcao);
            fflush(stdin);

            if(strcmp(strlwr(opcao),"1")==0)
            {
                printf("\nJan: Não. Temos suspeita de que uma organização terrorista está por trás de tudo isso. \n");
                printf("\nO helicóptero da a partida com destino para o porto de Suape. Durante o voo\nJoão tira seu Game boy Advance e começa a jogar,\nvocê não sabe que  jogo ele está jogando. Jan olha para a sua cara e apontando para ele diz: Nerd. \n");
                Pergunta(8);
            }
            else if(strcmp(strlwr(opcao),"2")==0)
            {
                printf("\nO helicóptero da a partida com destino para o porto de Suape. Durante o voo\nJoão tira seu Game boy Advance e começa a jogar,\nvocê não sabe que  jogo ele está jogando. Jan olha para a sua cara e apontando para ele diz: Nerd. \n");
                Pergunta(8);
            }
            else{
                Pergunta(7);
            }



            break;
        case(8):
            system("pause");
            system("cls");
            printf("\nO sol está se pondo e ao chegar no seu destino Jan com seu laptop aberto fala:\nstrutura Portuária tem Profundidade de 8 metros a 20 metros,\nna bacia de evolução, píeres e cais de atracação. Área total do porto organizado: 3.232,58 hectares. Bacia de evolução\ndo Porto Externo: profundidade, em alguns pontos, de 20 metros e largura 1.200 metros.\n");
            printf("\nO helicóptero pousa e você avista várias tendas há cerca de 20\nmetros e vê grupo de agentes vestidos com uniformes de segurança nuclear.\nChegando na tenda você encontra várias pessoas conversando em um link direto e quem está na\ntela conversando com eles é nada mais nada menos que Paulo Câmara.\n");
            printf("\n---------------------------------------------------------------------------------------------------\n");
            printf("\nAssim que você entra na tenda, você pega o Governador falando: Este caso não pode conter\nvazamento por conta até que estamos próximos do carnaval. Isso iria agravar fortemente a economia do estado.\n");
            printf("\nMal chegando na conversa João se manifesta e diz:\njá conseguimos uma analista para o caso.\nO Nome dele é %s, na análise do Rompimento da barragem em Mariana\n",jogador.nome);
            printf("\nO governador olha para você e diz: %C, você tem uma hora parar me dar uma resposta.\n");
            printf("\nOpção(1):Ajudá-lo\n");
            printf("\nOpção(2): COnfrotálo\n");
            gets(opcao);
            fflush(stdin);

            if(strcmp(strlwr(opcao),"1")==0)
            {
                pontos_mentais.percepcao=pontos_mentais.percepcao+i;
                printf("\nE se eu descobrir mais uma vez que esse caso se trata de uma\nempresa que age fora dos conformes dos governamentais, vocês\nvão querer me calar e ameaçar toda a minha família, Como vocês fizeram da última vez!?\n");
                printf("\n\n[+1] de Percepeção-%d\n\n",pontos_mentais.percepcao);
                printf("\nVeja bem como fala senhor %s, falo isso para o bem de sua carreira profissional.\n",jogador.nome);
                Pergunta(9);
            }
            else if(strcmp(strlwr(opcao),"2")==0)
            {
                printf("\nO governo tentou me calar quando descobri\nquem estava por trás do desastre de Mariana. Tentaram me matar e\ntentaram matar toda a minha família!Por que deveria ajudar vocês?!\n");

                Pergunta(9);
            }
            else{
                Pergunta(8);
            }



        break;
        case(9):
            system("pause");
            system("cls");
            printf("\nVeja bem como fala senhor %s, falo isso para o bem de sua carreira profissional.\n",jogador.nome);
            printf("\nDepois disso a transmissão se encerra e Jan diz em tom sarcástico: Bem gente!!\nÉ nisso que dá votar num economista para governador.Vamos ao Trabalho!\n");
            printf("\nVocê é levado para um caminhão/laboratório, onde passa por todo processo\nde higienização e recebimento de uma roupa antirradiação e um contador Geiger.\nSaindo do compartimento você se dirige ao local onde está a carga contaminada.\n");
            printf("\nContainer com 6,058m de comprimento e 2,438m de largura,\nde cor branca e com detalhes de ferrugem por conta da maresia\ne com o logo da prefeitura da cidade do Recife impresso.\nA porta com container é aberta e você entra.\n");
            printf("\nO que encontrará dependerá do nivel da sua percepção\n");
            printf("\nEscreva um [1] para continuar\n");
            gets(opcao);
            fflush(stdin);
            while(x)
            {
                /*

                if(strcmp(opcao,"1")!=1)
                {
                    printf("Opção Inválida\nEscreva novamente\n");
                    gets(opcao);
                }
                else if(strcmp(opcao,"2")!=2)
                {
                    printf("Opção Inválida\nEscreva novamente\n");
                    gets(opcao);
                }
                else if(strcmp(opcao,"3")!=3)
                {
                    printf("Opção Inválida\nEscreva novamente\n");
                    gets(opcao);
                }
                */
                if(strcmp(strlwr(opcao),"1")==0)
                {
                    if(pontos_mentais.percepcao==6)
                    {
                        printf("\nDentro você encontra várias caixas madeira contendo garrafas de pitu. Você pega uma garrafa e percebe que dentro de uma delas tem uma cápsula de chumbo.\n");
                        printf("\nRecolhe as cápsulas para análise.\n");
                        Pergunta(10);
                    }
                    else if(pontos_mentais.percepcao<6)
                    {
                        printf("\nDentro você encontra várias caixas madeira contendo garrafas de pitu.\n");
                        printf("\nVocê liga as luzes do container e percebe que dentro delas tem uma cápsula de chumbo.\n");
                        Pergunta(10);
                    }
                }
                else{
                    Pergunta(9);
                }



            break;

        case(10):
            system("pause");
            system("cls");
            printf("\nNo laboratório você coloca a garrafa de pitu dentro de uma parede de proteção,\ne utilizando luvas você manuseia o objeto, a garrafa de pitu, já sem a tampa.  Ao remover a garrafa\nde dentro da parede de proteção, a cápsula contida nela é aberta e lá é encontrado um pó azul, parecido com purpurina. No momento em\nque você recolhe o material para análise, acaba percebendo barulhos de tiros na parte externa do laboratório, seguido de um blackout.\n");
            printf("\nO que a contecerá dependerá da sua agilidade\n");
            printf("\nDigite [1] para continuar na historia\n");
            gets(opcao);
            fflush(stdin);
            /*
            while(x)
            {

                if(strcmp(opcao,"1")!=1)
                {
                    printf("Opção Inválida\nEscreva novamente\n");
                    gets(opcao);
                }
                else if(strcmp(opcao,"2")!=2)
                {
                    printf("Opção Inválida\nEscreva novamente\n");
                    gets(opcao);
                }
                else if(strcmp(opcao,"3")!=3)
                {
                    printf("Opção Inválida\nEscreva novamente\n");
                    gets(opcao);
                }
                */
                if(strcmp(strlwr(opcao),"1")==0)
                {
                    if(pontos_fisicos.agilidade==3)
                    {
                        pontos_fisicos.agilidade=pontos_fisicos.agilidade+i;
                        printf("\nVocê se joga no chão rapidamente e espera o tiroteio acabar. Logo,\npercebe que o conteúdo azul está brilhando, notando agora que se trata da substância chamada césio-137. \n");
                        printf("\nVoce ganhou um ponto em agilidade-[%d]\n",pontos_fisicos.agilidade);
                        Pergunta(11);
                    }
                    else if(pontos_fisicos.agilidade<3)
                    {
                        pontos_fisicos.agilidade=pontos_fisicos.agilidade+i;
                        printf("\nVocê percebe que o conteúdo azul está brilhando, notando agora que se trata da substância chamada césio-137.\n");
                        printf("\nVoce ganhou um ponto em agilidade-[%d]\n",pontos_fisicos.agilidade);
                        Pergunta(11);
                    }

                    else if(pontos_fisicos.agilidade>3)
                    {
                        pontos_fisicos.agilidade=pontos_fisicos.agilidade+i;
                        printf("\nVocê se joga no chão rapidamente e espera o tiroteio acabar. Logo,\npercebe que o conteúdo azul está brilhando, notando agora que se trata da substância chamada césio-137. \n");
                        printf("\nVoce ganhou um ponto em agilidade-[%d]\n",pontos_fisicos.agilidade);
                        Pergunta(11);
                    }
                }
                else{
                Pergunta(10);
			}



            break;
        case(11):
            system("pause");
            system("cls");
            printf("\nJan entra no recinto segurando uma pistola 9mm e atira utilizando a porta do laboratório como proteção.\n");
            printf("\n---------------------------------------------------------------------------------------------------\n");
            printf("\nDescrição do laboratório: Uma força tarefa monta um laboratório dentro\n de um armazém localizadopróximo da costa do Porto. Além\ndo laboratório provisório tem várias caixas contendo materiais logísticos.\n");
            printf("\nVários homens com máscaras de políticos brasileiros e vestindo roupas de times pernambucanos entram atirando por todo o laboratório.\n");
            printf("\nEnquanto Jan lhe dá cobertura, atirando nos homens na tentativa de fazer\nvocê correr em direção a porta, um dos atiradores, que está vestido com\na máscara do Jair Bolsonaro e camisa do Náutico, consegue ver você e aponta uma arma em sua direção.\n");
            printf("\nOpção(1)Ataca pela esquerda.-para ter sucesso precisa no mínimo 6p de agilidade\n");
            gets(opcao);
            fflush(stdin);
            if(strcmp(strlwr(opcao),"1")==0)
            {
                if(pontos_fisicos.agilidade==6 || pontos_fisicos.agilidade>6)
                {

                    printf("\nVocê pula em cima dele na tentativa de um combate corpo a corpo.\n");
                    Pergunta(12);
                }
                else if(pontos_fisicos.agilidade<6)
                {
                    jogador.vida=jogador.vida-DANOP;
                    printf("\nVocê toma um tiro perdendo 30 pontos de sangue.\n");
                    printf("Você perdeu 30 pontos de sangue. Restam...[%d]",jogador.vida);
                    Pergunta(12);

                }
                else if(jogador.vida<=0)
                {
                    printf("-----------------------GAME OVER-----------------------");
                    Pergunta(1);
                }
            }
            else{
                Pergunta(11);
			}
            break;
        case(12):
            system("pause");
            system("cls");
            printf("\nVocê começa a lutar pela sua vida com o Bolsominion e utiliza de suas habilidades para se defender.\n");
            printf("O resultado ira depender da sua destreza...\n");
            printf("\nAperte [1] para descobrir:\n");
            gets(opcao);
            fflush(stdin);
            if(strcmp(strlwr(opcao),"1")==0)
            {
                if(pontos_fisicos.destreza==3)
                {
                    printf("\nVocê desconcerta o oponente e ele bate na mesa onde\n está o material radioativo, deixando-o desabilitado temporariamente.\n");
                    Pergunta(13);
                }
                else if(pontos_fisicos.destreza>3)
                {
                    printf("\nVocê pula e dá uma voadora na pleura peridural do Bolsominion no estilo Jack Chan finalizado inimigo.\n");
                    Pergunta(13);
                }
                else if(pontos_fisicos.destreza<3)
                {
                    jogador.vida=jogador.vida-20;
                    printf("\nO atirador te acerta com uma coronhada fazendo você perder 20 pontos de vida.\nVocê perdeu 20 pontos de vida. Restam...[%d]\n",jogador.vida);
                    Pergunta(13);
                }
            }
            else{
                Pergunta(12);
			}
            break;
        case(13):
            system("pause");
            system("cls");
            printf("\nDepois de deixá-lo inconsciente, você se aproxima\nlentamente do oponente, abre a parede de proteção para\nretirar apenas a garrafa de pitu e acerta ele\ncom apenas um golpe na cabeça, fazendo ele apagar na hora.\n");
            printf("\nJan: meu irmão, véi, tu sabes lutar é!? Esses movimentos de Bruce Lee aí, aprendesse onde?\n");
            printf("\nOpção(1):Você ignora a pergunta e responde.\n");
            printf("\nOpção(2):Não responder nada.");
            gets(opcao);
            fflush(stdin);
            if(strcmp(strlwr(opcao),"1")==0)
            {
                printf("\nEssa parada aqui é césio-137. Temos que impedi-los o mais rápido possível.\n");
                Pergunta(14);

            }
            else if(strcmp(strlwr(opcao),"2")==0){
                printf("\nEntrega o material radioativo protegido com chumbo a Jan e diz: É que eu ando assistindo muitos filmes\n");
                Pergunta(14);

            }
            else{
                Pergunta(13);
			}
            break;

        case(14):
            system("pause");
            system("cls");
            printf("\nJoão: Um dos galerosos levou um dos matérias que estava no container e fugiu de barco.\n");
            printf("\nJan : MERDA!\n");
            printf("\n----------------------------------------------------------------------------\n");
            printf("\n[Derby Domingo, 14:30h, Museu da Polícia Militar de Pernambuco.]\n");
            printf("\n----------------------------------------------------------------------------\n");
            printf("\nVocê, João e Jan estão sentados na sala de interrogatório para arrancar\nalguma informação do atirador que você apagou no laboratório improvisado\n");
            printf("\nJan joga água na cara do galeroso e diz: ACORDA PRA TOMAR GAGAL BOY!\n");
            printf("\nAo perceber que foi pego o galeroso grita: VIDA LONGA E PROSPERA!. Abre a boca e bate bem forte com os dentes.\n");
            printf("\nOpção(1):“CIANURETO!”  Desfere um soco no estomago.\n");
            printf("\nOpção(2):“CIANURETO!” Segura a garganta dele na hora com um mata-leão.\n");
            gets(opcao);
            fflush(stdin);
            if(strcmp(strlwr(opcao),"1")==0)
            {
                printf("\nO galeroso vomita parte da substância ficando sem voz.\n");
                printf("\nJoão pega papel e caneta, dá um soco nele e diz: ESCREVA QUEL É O SEU PLANO!\n");
                printf("\nO Galeroso escreve: “Carnavau. Olinda. Esplosão. Prefeitura.\n”João: vamos locomover grupo tático para prefeitura Olinda, em 5 minutos!\n");
                Pergunta(15);
            }
            else if(strcmp(strlwr(opcao),"2")==0)
            {
                printf("\nO galeroso vomita toda a substância que tentou ingerir.\n");
                printf("\nJan pega o telefone e bate duas vezes na cara dele e diz: FALA ONDE ELES ESTÃO, OU VOCÊ QUER APANHAR MAIS!\n");
                printf("\nGaleroso: Somos a NUCAD! e vamos acabar com o carnaval de Olinda. Estamos neste momento pondo\nem ação nosso plano nas prévias de Olinda,\no ataque está sendo pondo em prática neste momento, na prefeitura.\n");
                printf("\nOpção(1):O que é Nucad?\n");
                printf("\nOpção(2):Ignora o galeroso:\n");
                gets(opcao);
                fflush(stdin);

                if(strcmp(strlwr(opcao),"1")==0)
                {
                    printf("\nGaleroso:  NERDS UNIDOS CONTRA A DEMOCRACIA!\nJoão difere um soco no interrogado e diz: A sigla não precisa ter “A”,\nJUMENTO!Temos que reunir o grupo tático e partir em 5 minutos!\n");
                    Pergunta(15);
                }
                else if(strcmp(strlwr(opcao),"2")==0)
                {
                    printf("\nJoão: Atenção Torre! Precisamos de uma força tática cercando o perímetro da prefeitura de Olinda, agora!\n");
                    Pergunta(15);
                }


            }
            else{
                Pergunta(14);
			}
            break;
        case(15):



            system("pause");
            system("cls");
            printf("\nNeste momento você está na avenida Agamenon Magalhaes, destino prefeitura de Olinda. Neste exato\n momento estão rolando as previas para o carnaval do ano que está por vir.\n");
            printf("\nJan:Ei %s Sabe atirar ?\n",jogador.nome);
            printf("Opção(1):Me dê o que você tem e eu te mostro como é que se faz, Jogador.\n");
            printf("Opção(2):: Claro que sim, jogador. tem alguma coisa violenta aí?\n");
            gets(opcao);
            fflush(stdin);
            if(strcmp(strlwr(opcao),"1")==0)
            {
                //p= adicionarItem(p,ar15);

	            printf("\nVocê Ganha uma  Pistola 9mm com supressor e um Fuzil . \n");
                printf("Adiciona pistola 9mm \n");
                p = adicionarItem(p,pistola);
                printf("Adicionar AR15\n ");
                p=adicionarItem(p,ar15);
                verInventario(p);
                Pergunta(16);


            }
            else if(strcmp(strlwr(opcao),"2")==0)
            {
                printf("\nJan:kkkkkkkkkk!! Te entrega uma Faca Tática.\n");
                p=adicionarItem(p,faca);
                faca.valor=faca.valor-jogador.vida;
                verInventario(p);
                Pergunta(16);


            }
            else{
                Pergunta(15);
			}
            break;
        case(16):
            system("pause");
            system("cls");
            printf("\n---------------------------------------------\n");
            printf("\n1- [Av. Liberdade - Carmo, Olinda. 14:45.]\n");
            //system("color 02");
            printf("\n----------------------------------------------------\n");
            printf("\n2-	Você é junto com o grupo tático fecham todas as saídas dão acesso a prefeitura de Olinda. Há cerca de 20 metros\nde distância um grupo de foliões estão atrás de um bloco cujo o estandarte está escrito,\nPokéBloco, a maioria dos foliões estão fantasiados de pokémon.\n");
            printf("\nNo lado oeste você avista uma pessoa com máscara de Sérgio Moro\ne camiseta da Inferno Coral descendo a pitombeira, em sua direção.\n");
            printf("\nOpção(1):Seguir ele.\n");
            printf("\nOpção(2):Avisa pra Jan chegar nele para ver do que se trata.\n");
            gets(opcao);
            fflush(stdin);
            if(strcmp(strlwr(opcao),"1")==0)
            {
                printf("\nEle percebe sua presença, avisa alguém através de uma escuta e um tiro de Fuzil vem do\n ultimo andar da janela da prefeitura em sua direção e quase te acerta\n");

                Pergunta(17);
            }
            else if(strcmp(strlwr(opcao),"2")==0)
            {
                printf("\nO mascarado percebe a presença de Jan e corre para dentro da\nprefeitura atirando e chamando a atenção\nde todo mundo, inclusive dos nerds fantasiados de Pokémon causando o maior caos.\n");

                Pergunta(17);
            }
            else{
                Pergunta(18);
			}
            break;
        case(17):
            system("pause");
            system("cls");
            printf("\nDepois dos primeiros tiros vindos do inimigo a multidão se assusta e em seguida vem a troca de tiros vindos de seu time tático.\n");
            printf("\nOpção(1):Você está desarmado e pede uma arma ao companheiro mais próximo\n");
            printf("\nOpção(2):Você pega com João um fuzil e uma metralhadora e se junta a multidão\nno modo stealth para ter boa visão da entrada da prefeitura.\n");
        	gets(opcao);
			fflush(stdin);

            if(strcmp(strlwr(opcao),"1")==0)
            {
                printf("\nJan grita: SEGURA ISSO! joga para você uma espingarda calibre 12 e um fuzil.\n");
                p=adicionarItem(p,espingarda);
                p=adicionarItem(p,pistola38);
                printf("\nEsses são os itens na sua bolsa\n");
                verInventario(p);
                Pergunta(18);
            }
            else if(strcmp(opcao,"2")==0)
            {
                printf("\nEm meio a multidão e tiros, você avista um homem na entrada trocando tiros com o grupo tático.\n E outro homem correndo para os fundos da residência com uma garrafa de Pitu na mão. \n");
                Pergunta(18);
            }
            else{
                Pergunta(17);
            }


            break;
        case(18):
			system("pause");
			system("cls");
			printf("\nvocê em movimento você recebe as armas do seu companheiro e se joga atrás de uma arvore em frente à prefeitura.\n");
			printf("opção(1): Na guerra ou você mira, ou você atira.\n");
			printf("opção(2): Diga olá para minha amiguinha!\n");
			printf("opção(3): Hasta La Vista, Baby!\n");
			gets(opcao);
			fflush(stdin);
			if (strcmp(opcao,"1")==0){
				printf("\nvocê inabilita o inimigo com um tiro de fuzil no braço que segura a arma. Inimigo fica de joelhos e você finaliza com\n um tiro de espingarda no meio do peito, no estilo Schwarzenegger, fazendo ele voar por 3 metros.\n");
				Pergunta(19);
			}
			else if(strcmp(opcao,"2")==0){
				jogador.vida=jogador.vida-DANOS;
				printf("\nNo estilo Scarface, você sai da proteção da árvore e atira contra o inimigo gritando!\n");
				printf("\ninfelizmente os tiros não acertam o inimigo fazendo com que você tome dano de uma AK-47.\nLevando de você 40 pontos de dano. restam...[%d] \n",jogador.vida);
				if (jogador.vida<=0){
					printf("-----------------------GAME OVER-----------------------");
					Pergunta(1);
				}
				else if(jogador.vida>0){
					printf("você acerta o inimigo na cabeça em caráter de contra-ataque");
					Pergunta(19);
				}
			}
			else if(strcmp(opcao,"3")==0){
				printf("Um único tiro foi suficiente para você por fim a vida do inimigo.");
				Pergunta(19);
			}
			else{
                Pergunta(18);
			}
			break;
		case(19):
			system("pause");
			system("cls");
			printf("Ao finalizar o inimigo você chega no acesso ao saguão da prefeitura, com um fuzil na mão esquerda e uma espingarda calibre 12 na mão direita.\nNa mesa da recepção tem uma rádio e nele toca uma música um tanto peculiar Careless Whisper do George Michael");
			printf("\nNo rádio já diz que o atirador conseguiu identificar apenas um homem na prefeitura. A imagem do meliante foi passada para polícia que analisou\no banco de dados e descobriu que se tratava de Evanílson, um dos terroristas mais procurados do mundo. Envolvido na sabotagem do avião de um \ncandidato a presidente, na implantação de dinamite na barragem de Mariana e na contaminação da água de uma estação de tratamento.\n");
			printf("\n\nSubindo as escadas você escuta o barulho de alguém correndo para se esconder.\n\n");
			printf("opção(1): Cara! Eu vim aqui para mastigar chiclete e chutar a sua bunda, só que tem um problema... acabaram os chicletes.\n");
			printf("opção(2): Aumenta o volume da música do George Michael e canta: ''I'm never gonna dance again, guilty feet have got no rhythm,\nthough it's easy to pretend i know you're not a fool.''\n");
			gets(opcao);
			fflush(stdin);
			if(strcmp(opcao,"1")==0){
				printf("\nO cara atira e denotando sua localização\n");
				Pergunta(20);
			}
			else if(strcmp(opcao,"2")==0){
				printf("O terrorista completa cantando:''Should've known better than to cheat a friend, and waste the chance that I've been given''\nDenotando sua localização.\n");
				Pergunta(20);
			}
			else{
                Pergunta(19);
			}
			break;
		case(20):
			system("pause");
			system("cls");
			printf("Sabendo a localização do terrorista você sobe as escadas correndo recebido vários tiros pela culatra, deixando evidente a falta\nde mira do elemento.\n");
			printf("opção(1): Atirar para acertar nas pernas com a espingarda.\n");
			printf("opção(2): Atirar para acertar na cabeça.\n");
			gets(opcao);
			fflush(stdin);
			if(strcmp(opcao,"1")==0){
				printf("Você inabilita o inimigo deixando-o caído\n");
				Pergunta(21);
			}
			else if(strcmp(opcao,"2")==0){
				jogador.vida=jogador.vida-10;
				printf("O Tiro sai bastante estilhaçado não acertando o inimigo.\n");
				printf("Voce perde 10 pontos de vida de um dano de pistola 9mm em caráter de contra-ataque. restam...[%d]\n",jogador.vida);
				if(jogador.vida<=0){
					printf("-----------------------GAME OVER-----------------------");
					Pergunta(1);
				}
				else if(jogador.vida>0){
					printf("você acerta o inimigo nas pernas inabilitando ele em caráter de contra-ataque.");
					Pergunta(21);
				}
			}
			else{
                Pergunta(20);
			}
			break;
		case(21):
			system("pause");
			system("cls");
			printf("\nAo chegar perto no inimigo caído ele fala: Isso não vai ficar assim EU VOU ESPALHAR A DOENÇA PELO MUNDO. VOCÊ ESTÁ SENDO ENGANADO\nPELO GOVERNO ASSSIM COMO EU FUI, SEU OTÁRIO.\n");
        	printf("opção(1): Você diz: Você é a doença e eu sou a cura!\n");
        	printf("opção(2): Você diz: Yippee ki yay, motherfocker!\n");
            gets(opcao);
            fflush(stdin);
        	if(strcmp(opcao,"1")){
        		printf("\nVocê tira a vida do inimigo com apenas um tiro na cabeça.\n");
	       		Pergunta(22);
			}
			else if(strcmp(opcao,"2")){
				printf("\nJan, João e a força tarefa chegam no local e dão voz de prisão para o para o terrorista.\n");
                Pergunta(22);
			}
			else{
                Pergunta(21);
			}
			break;
		case(22):
			system("pause");
			system("cls");
			printf("Enquanto a policia faz a checagem dos cômodos. Para fazer a varredura do perímetro você não vê mais motivos para ficar no local.\nAo sair pela porta Jan para você e pergunta:\n");
		 	printf("Tem certeza que você é professor?");
		 	printf("\nopção(1): Claro que sim, estou até de férias.\n");
		 	printf("\nopção(2): Ficar em silêncio e dá um sorriso sem graça.\n");
			gets(opcao);
			fflush(stdin);
		 	if(strcmp(opcao,"1")==0){
		 		printf("\n-------------CONGRATULAÇÕES! FIM DE JOGO!-------------\n");
		 		Pergunta(23);
			 }
			else if(strcmp(opcao,"2")==0){
				printf("\nFIM DE JOGO CONGRATULAÇÕES! EM BREVE TEREMOS MAIS UMA AVERTURA!\n");
				Pergunta(23);
			}
			else{
                Pergunta(22);
			}
			break;
        case(23):
            printf("\n           --------------CREDITOS--------------------\n");
            printf("\nDensenvolvedores: Peter Bhremmer, Lucas Mendes, William Brasil, João Gabriel, Ivandro Junior e Bruna Alana.\n ");
            system("pause");
            exit(0);
            break;


	 	}
	}
}
