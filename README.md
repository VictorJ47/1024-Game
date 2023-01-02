# 1024-Game
#include <iostream>
#include <iomanip>
#include <vector>
#include "Board.hpp"
using namespace std;
/*
Board::Board():Board(3,3)
{
}

Board::Board(int m):Board(m,m)
{
}

Board::Board(int m, int n)
{
    if(m >= 1 && n >= 1)
    {
        numRows = m;
        numCols = n;
    }
    else
    {
        numRows = 3;
        numCols = 3;
    }
    panel = new int*[numRows];

    for(int i = 0; i < numRows; i++)
    {
        panel[i] = new int[numCols];

        for(int j = 0; j < numCols; j++)
        {
            panel[i][j] = 0;
        }
    }

    target = 32;
    max = 0;
} 

Board::~Board()
{
    for(int i = 0; i < numRows; i++)
    {
        delete[] panel[i];
        panel[i] = nullptr;
    }

    delete[] panel;
    panel = nullptr;
}*/

void printSeparateLine(int numCols)
{
    cout << "+";

    for (int i = 0; i < numCols; i++)
    {
        cout << "----+";
    }

    cout << endl;
}

void Board::print() const
{
    for (int i = 0; i < numRows; i++) {
        printSeparateLine(numCols);
        cout << "|";
        for (int j = 0; j < numCols; j++) {
            if (panel[i][j] > 0) {

                cout << setw(4) << panel[i][j] << "|";
            }
            else
                cout << setw(5) << "|";
        }
        cout << endl;

        
    }
    printSeparateLine(numCols);
}
/*
void Board::selectRandomCell(int& row, int& col)
{
	vector<int> list;
	for (int i = 0; i < numRows; i++)
	{
		for (int j = 0; j < numCols; j++)
        {
			if (panel[i][j] == 0)
            {
				list.push_back(i*numCols + j);
            }
        }
	}
	if (list.size() > 0)
	{
		int c = rand() % list.size() + 0;
		c = list.at(c);
		row = c / numCols;
		col = c % numCols;
		panel[row][col] = 1;
		Board::print();
	}
	if (noAdjacentSameValue() || list.size() == 0)
    {
		cout << "Game over. Try again." << endl;
    }
}
bool Board::noAdjacentSameValue() const
{
	for (int i = 0; i < numRows; i++)
	{
		for (int j = 1; j < numCols - 1; j++)
		{
			if (panel[i][j-1] == panel[i][j] || panel[i][j+1] == panel[i][j])
            {
				return false;
            }
		}
	}
	return true;
}*/

void Board::pressLeft()
{
	for (int i = 0; i < numRows; i++)
	{
		for (int j = 0; j < numCols - 1; j++)
		{
			if (panel[i][j] != 0 && panel[i][j] == panel[i][j+1])
			{
				panel[i][j] *= 2;
				for (int f = j+1; f < numCols - 1; f++)
					panel[i][f] = panel[i][f+1];
				panel[i][numCols - 1] = 0;
				j--;
			}
		}
	}
	int row, col;
	Board::selectRandomCell(row, col);
}
void Board::pressRight()
{
	for (int i = 0; i < numRows; i++)
	{
		for (int j = numCols - 1; j > -1; j--)
		{
			if (panel[i][j] != 0 && panel[i][j] == panel[i][j - 1])
			{
				panel[i][j] *= 2;
				for (int f = j-1; f > 0; f--)
					panel[i][f] = panel[i][f-1];
				panel[i][0] = 0;
				j++;
			}
		}
	}
	int row, col;
	Board::selectRandomCell(row, col);
}
void Board::pressUp()
{
        for (int i = 0; i < numRows - 1; i++)
        {
                for (int j = 0; j < numCols; j++)
                {
                        if (panel[i][j] != 0 && panel[i][j] == panel[i+1][j])
                        {
                                panel[i][j] *= 2;
                                for (int f = i+1; f < numRows - 1; f++)
                                	panel[f][j] = panel[f+1][j];
                                panel[numRows - 1][j] = 0;
                        }
                }
        }
	int row, col;
	Board::selectRandomCell(row, col);
}
void Board::pressDown()
{
	for (int i = numRows - 1; i > 0; i--)
	{
		for (int j = 0; j < numCols; j++)
		{
			if (panel[i][j] != 0 && panel[i][j] == panel[i-1][j])
			{
				panel[i][j] *= 2;
				for (int f = i-1; f > 0; f--)
					panel[f][j] = panel[f-1][j];
				panel[0][j] = 0;
			}
		}
	}
	int row, col;
	Board::selectRandomCell(row, col);
}
