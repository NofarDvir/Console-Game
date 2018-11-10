// Game.cpp

#include <iostream>

using namespace std;

// Const global
const int GAME_BORD_LRNGTH = 20;

// Struct definition
struct COORD 
{
	int X;
	int Y;
};

// Prototype definition
void PrintBord(char icGameBord[GAME_BORD_LRNGTH][GAME_BORD_LRNGTH], COORD icrdPlayer);
void Move(char icGameBord[GAME_BORD_LRNGTH][GAME_BORD_LRNGTH], COORD* icrdPlayer, char icCurrMove);

void main()
{
	// Const definition
	bool bGameIsRunning = true;


	// Variable definition 
	char GameBord[GAME_BORD_LRNGTH][GAME_BORD_LRNGTH];
	int  nBordRows;
	int  nBordCols;
	char cCurrMove;
	COORD crdPlayer{1, 1};

	// Init the bord 
	for (nBordRows = 0; nBordRows < GAME_BORD_LRNGTH; nBordRows++)
	{
		for (nBordCols = 0; nBordCols < GAME_BORD_LRNGTH; nBordCols++)
		{
			if (nBordRows == 0 || nBordCols == 0 ||
				nBordCols == (GAME_BORD_LRNGTH - 1) ||
				nBordRows == (GAME_BORD_LRNGTH - 1))
			{
				GameBord[nBordRows][nBordCols] = '#';
			}
			else if (nBordRows == crdPlayer.Y && nBordCols == crdPlayer.X)
			{
				GameBord[nBordRows][nBordCols] = '@';
			}
			else
			{
				GameBord[nBordRows][nBordCols] = ' ';
			}
		}
	}

	PrintBord(GameBord, crdPlayer);

	while (bGameIsRunning)
	{
		cin >> cCurrMove;

		Move(GameBord, &crdPlayer, cCurrMove);

		system("cls");
		PrintBord(GameBord, crdPlayer);
	}

	system("pause");
}

void PrintBord(char icGameBord[GAME_BORD_LRNGTH][GAME_BORD_LRNGTH], COORD icrdPlayer)
{
	// Variable definition 
	int  nBordRows;
	int  nBordCols;

	// Print the game bord
	for (nBordRows = 0; nBordRows < GAME_BORD_LRNGTH; nBordRows++)
	{
		for (nBordCols = 0; nBordCols < GAME_BORD_LRNGTH; nBordCols++)
		{
				cout << " " << icGameBord[nBordRows][nBordCols];
		}
		cout << endl;
	}
}

void Move(char icGameBord[GAME_BORD_LRNGTH][GAME_BORD_LRNGTH], COORD* icrdPlayer, char icCurrMove)
{
	// Const definition
	const char UP = 'w';
	const char RIGHT = 'd';
	const char LEFT = 'a';
	const char DOWN = 's';

	icGameBord[icrdPlayer->Y][icrdPlayer->X] = ' ';
	switch (icCurrMove)
	{
		case(UP):
		{
			if (icrdPlayer->Y == 1)
			{
				icrdPlayer->Y = (GAME_BORD_LRNGTH - 2);
			}
			else
			{
				icrdPlayer->Y--;
			}

			break;
		}
		case(RIGHT):
		{
			if (icrdPlayer->X == (GAME_BORD_LRNGTH - 2))
			{
				icrdPlayer->X = 1;
			}
			else
			{
				icrdPlayer->X++;
			}

			break;
		}
		case(LEFT):
		{
			if (icrdPlayer->X == 1)
			{
				icrdPlayer->X = (GAME_BORD_LRNGTH - 2);
			}
			else
			{
				icrdPlayer->X--;
			}

			break;
		}
		case(DOWN):
		{
			if (icrdPlayer->Y == (GAME_BORD_LRNGTH - 2))
			{
				icrdPlayer->Y = 1;
			}
			else
			{
				icrdPlayer->Y++;
			}

			break;
		}
		default:
		{
			break;
		}
	}
	icGameBord[icrdPlayer->Y][icrdPlayer->X] = '@';
}
