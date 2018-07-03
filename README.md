# Floyd-Program
Code for Floyd program
//  main.cpp
//  FloydProgram
//
//  Created by Margie Ruffin on 4/29/18.
//  Copyright © 2018 Margie Ruffin. All rights reserved.
// https://www.sanfoundry.com/cpp-program-implement-floyd-warshall-algorithm/
// Program creates a chart of shortest paths from one city to another
#include <iostream>
#include <array>
#include <string>
#include <iomanip>
using namespace std;


//---------------------------------------Floyd Algorithm------------------------------------------------------
void floyd(int b[][15])
{
    int i, j, k;
    for (k = 0; k < 15; k++)
    {
        for (i = 0; i < 15; i++)
        {
            for (j = 0; j < 15; j++)
            {
                if ((b[i][k] * b[k][j] != 0) && (i != j))
                {
                    if ((b[i][k] + b[k][j] < b[i][j]) || (b[i][j] == 0))
                    {
                        b[i][j] = b[i][k] + b[k][j];
                    }
                }
            }
        }
    }
    string arrayName[15] = {"Atlanta","Chicago","Dallas ","Las Ang","Las Veg","Miami  ","Milw.  ","Minn.  ","New Orl","NewYork","OakCity","Phoenix","SanFran","Seattle","Wash DC"};
    
    cout << "All points shortest path matrix" << endl;
    for(int r=0; r <15; r++)
    {
        cout << setw(13)<< arrayName[r];
    }
    cout << endl;
    cout << "---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------" << endl;

    //cout << endl;
    for (i = 0; i < 15; i++)
    {
        cout <<  arrayName[i]<< "|";
        
        //cout<<"\nMinimum Cost With Respect to Node:"<<i<<endl;
        for (j = 0; j < 15; j++)
        {
            cout<< setw(12)<< b[i][j];
        }
        cout << endl;
        
    }
}
//---------------------------------------------------------------------------------------------------------------

//---------------------------------------- Recover the paths ----------------------------------------------------

int A[15][15], P[15][15];
int i, j, k;
void recoverPath(int C[][15])
{
    
    for (i = 0; i < 15; i++)
    {
        for(j=0; j < 15; j++)
        {
            A[i][j]= C[i][j];
            P[i][j] = 0;
            
        }
    }
    for(i = 0; i< 15; i++)
    {
        A[i][i] = 0;
        
    }
    for(k= 0; k < 15; k++)
    {
        for(i = 0; i < 15; i++)
        {
            for(j =0; j < 15; j++)
            {
                if((A[i][k] + A[k][j]) < (A[i][j]))
                {
                    A[i][j] = A[i][k] + A[k][j];
                    P[i][j] = k;
                }
            }
        }
    }
    
    
    
    // At this point in the code Matrix A has all of the shortest paths and Matrix P is nothing but 0's....
    // Trying to figure out how to print out these k'th paths
    
    
    /*
    string arrayName[15] = {"Atlanta","Chicago","Dallas ","Las Ang","Las Veg","Miami  ","Milw.  ","Minn.  ","New Orl","NewYork","OakCity","Phoenix","SanFran","Seattle","Wash DC"};
    
    cout << "3rd Matrix" << endl;
    for(int r=0; r <15; r++)
    {
        cout << setw(13)<< arrayName[r];
    }
    cout << endl;
    cout << "---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------" << endl;
    
    //cout << endl;
    for (i = 0; i < 15; i++)
    {
        cout <<  arrayName[i]<< "|";
        
        //cout<<"\nMinimum Cost With Respect to Node:"<<i<<endl;
        for (j = 0; j < 15; j++)
        {
            cout<< setw(12)<< A[i][j];
        }
        cout << endl;
        
    }
    */
  
}
//---------------------------------------------------------------------------------------------------------------


//---------------------------------------- Print the shortest path -----------------------------------------------


// At this point i understand how this code is supposed to run but i can not figure out how to get I and J into this function. I'm not sure if they are supposed to be global or not
//The code is what i was able to come up with.
void shortPath(int I, int J)
{
    k = P[I][J];
    // trying to see where the error is
    cout << "Debug" << endl;
    if(k == 0)
    {
        return;
    }
    // trying to see where the error is
    cout << "Debug" << endl;
    shortPath(I, k);
    //doesn't cout anything...
    cout << k << endl;
    shortPath(k, J);
 
    
    
}

//---------------------------------------------------------------------------------------------------------------

int main()
{
    //matrix
    int arrayC[15][15] = {
        {0,9999,9999,9999,9999,9999,9999,9999,500,9999,9999,9999,9999,9999,663},
        {9999,0,9999,9999,1780,1423,9999,9999,948,9999,9999,9999,9999,2060,9999},
        {9999,9999,0,1440,1440,9999,9999,949,9999,517,1614,9999,9999,9999,9999},
        {9999,9999,1440,0,272,9999,9999,9999,9999,9999,9999,9999,414,9999,9999},
        {9999,1780,9999,272,0,9999,9999,9999,9999,9999,9999,9999,9999,9999,9999},
        {9999,1423,9999,9999,9999,0,9999,9999,9999,9999,9999,9999,9999,9999,9999},
        {9999,9999,9999,9999,9999,9999,0,9999,9999,9999,9999,1771,2257,9999,811},
        {9999,9999,949,9999,9999,9999,9999,0,9999,1217,729,9999,9999,9999,9999},
        {500,948,517,9999,9999,9999,9999,9999,0,9999,9999,9999,9999,9999,9999},
        {9999,9999,1614,9999,9999,9999,9999,1217,9999,0,9999,9999,9999,9999,237},
        {9999,9999,9999,9999,9999,9999,9999,9999,9999,9999,0,9999,9999,9999,9999},
        {9999,9999,9999,9999,9999,9999,1771,9999,9999,9999,9999,0,9999,9999,9999},
        {9999,9999,9999,414,9999,9999,2257,9999,9999,9999,9999,9999,0,804,9999},
        {9999,2060,9999,9999,9999,9999,9999,9999,9999,9999,9999,9999,804,0,9999},
        {663,9999,9999,9999,9999,9999,811,9999,9999,9999,237,9999,9999,9999,0}};
    
    //array with the names of the places to visit
    string arrayName[15] = {"Atlanta","Chicago","Dallas ","Las Ang","Las Veg","Miami  ","Milw.  ","Minn.  ","New Orl","NewYork","OakCity","Phoenix","SanFran","Seattle","Wash DC"};

    
    // Print the array
    cout << "The original Matrix" << endl;
    for(int r=0; r <15; r++)
    {
        //names of the places
        cout << setw(13)<< arrayName[r];
    }
    cout << endl;
    cout << "-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------" << endl;
    //int r =0;
    for(int row=0; row<15; row++)
    {
        // names of the places virticle
        cout <<  arrayName[row]<< "|";
        
        for(int column=0; column<15; column++)
        {
            cout <<setw(12) << arrayC[row][column];
        }
        
        cout << endl;
    }
    cout << endl;
    

    //calling the floyd algorithm
    floyd(arrayC);

    
    //int arrayA[15][15]= {{0}};
    //int arrayP[0][0];
    
    //Recovery algorithm
    recoverPath(arrayC);
  
    
    //calling the shortest path algorithm
    //shortPath(i, j);
    
    
    return 0;


}
