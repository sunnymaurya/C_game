#include <stdio.h>
#include <stdlib.h>


char matrix[3][3];  /* the tic tac toe matrix */

char check();
void init_matrix();
void get_player1_move();
void get_player2_move();
void get_computer_move();
void disp_matrix();

int main()
{
	char done;
	int cho;

	system("clear");

	printf("This is the game of Tic Tac Toe.\n");
	printf("\nWho do you want to play against??\n");
	printf("\nEnter:\n");
	printf("1.To play against computer\n");
	printf("2.To play against human opponent\n");
	printf("Your choice:");
	scanf("%d",&cho);

	if(cho==1)
	{
		done =  ' ';
		init_matrix();

		do
		{
			disp_matrix();
			printf("\nEnter your 'X' coordinates!!");
			get_player1_move();

			done = check(); /* see if winner */
			if(done!= ' ') break; /* winner!*/
			get_computer_move();
			done = check(); /* see if winner */
		 }
		 while(done== ' ');//do

		 if(done=='X')
			printf("You won!\n");
		 else
			printf("I won!!!!\n");
		 disp_matrix(); /* show final positions */

		 return 0;
	}
	else
	{
		done =  ' ';
		init_matrix();

		do
		{
			disp_matrix();
			printf("\nPLAYER 1....Enter your 'X' coordinates!!");
			get_player1_move();

			done = check(); /* see if winner */
			disp_matrix();
			if(done!= ' ')
				break; /* winner!*/
			printf("PLAYER 2....Enter your 'O' coordinates!!");
			get_player2_move();
			done = check(); /* see if winner */
		 }
		 while(done== ' ');//do

		if(done=='X')
		{
			disp_matrix(); /* show final positions */
			printf("\nPlayer 1 wins!!!\n");
		}
		else
		{
			disp_matrix(); /* show final positions */
			printf("\nPlayer 2 wins!!!!\n");
		}

	}
	return 0;
}

/* Initialize the matrix. */
void init_matrix(void)
{
	int i, j;

	for(i=0; i<3; i++)
		for(j=0; j<3; j++)
			matrix[i][j] =  ' ';
}

/* Get a player's move. */
void get_player1_move(void)
{
	int x, y;

	scanf("%d%*c%d", &x, &y);

	x--; y--;

	if(matrix[x][y]!= ' ')
	{
		printf("Invalid move, try again.\n");
		get_player1_move();
	}
	else matrix[x][y] = 'X';
}

void get_player2_move(void)
{
	int x, y,i,j;

	scanf("%d%*c%d", &x, &y);

	x--; y--;

	if(matrix[x][y]!= ' ')
	{
		printf("Invalid move, try again.\n");
		get_player2_move();
	}
	else
		matrix[x][y] = 'O';

	for(i=0; i<3; i++)
	{
		for(j=0; j<3; j++)
			if(matrix[i][j]==' ')
				break;
			if(matrix[i][j]==' ')
				break;
	}

	if(i*j==9)
	{
		printf("draw\n");
		exit(0);
	}
}

/* Get a move from the computer. */
void get_computer_move(void)
{
	int i, j;

	for(i=0; i<3; i++)
	{
		for(j=0; j<3; j++)
			if(matrix[i][j]==' ')
				break;
			if(matrix[i][j]==' ')
				break;
	}

	if(i*j==9)
	{
		printf("draw\n");
		exit(0);
	}
	else
		matrix[i][j] = 'O';
}

/* Display the matrix on the screen. */
void disp_matrix(void)
{
	int t;

	for(t=0; t<3; t++)
	{
		printf(" %c | %c | %c ",matrix[t][0],
		matrix[t][1], matrix [t][2]);
		if(t!=2) printf("\n---|---|---\n");
	}
	printf("\n");
}

/* See if there is a winner. */
char check(void)
{
	int i;

	for(i=0; i<3; i++)  /* check rows */
		if(matrix[i][0]==matrix[i][1] && matrix[i][0]==matrix[i][2])
			return matrix[i][0];

	for(i=0; i<3; i++)  /* check columns */
		if(matrix[0][i]==matrix[1][i] && matrix[0][i]==matrix[2][i])
			return matrix[0][i];

	/* test diagonals */

	if(matrix[0][0]==matrix[1][1] && matrix[1][1]==matrix[2][2])
		return matrix[0][0];

	if(matrix[0][2]==matrix[1][1] & matrix[1][1]==matrix[2][0])
		return matrix[0][2];

	return ' ';
}
