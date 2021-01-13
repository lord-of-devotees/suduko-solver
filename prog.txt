#include<stdio.h>
#include<conio.h>

void print(int mat[9][9]);
int is_valid(int mat[9][9], int row, int col, int n);
int solve(int mat[9][9], int row, int col);

int main(){
	int mat[9][9]={5,3,0,0,7,0,0,0,0,
				  6,0,0,1,9,5,0,0,0,
				  0,9,8,0,0,0,0,6,0,
				  8,0,0,0,6,0,0,0,3,
				  4,0,0,8,0,3,0,0,1,
				  7,0,0,0,2,0,0,0,6,
				  0,6,0,0,0,0,2,8,0,
				  0,0,0,4,1,9,0,0,5,
				  0,0,0,0,8,0,0,7,9
				  };

	print(mat);
	if(solve(mat,0,0)==1)		
		print(mat);
	else
		printf("\n\nInvlaid sudoku");	
	return 0;
}

int solve(int mat[9][9], int row, int col){
	if(row==8 && col==9)
		return 1;
	if(col==9){
		row++;
		col=0;
	}	
	if(mat[row][col]>0){
		return solve(mat, row, col+1);
	}
	
	int i;
	for(i=1; i<10; i++){
		if(is_valid(mat, row, col, i)==1){
			mat[row][col]=i;
			
			if(solve(mat, row, col+1)==1)
				return 1;		
		}
		mat[row][col]=0;
	}
	return 0;
}

int is_valid(int mat[9][9], int row, int col, int n)
{
	int row_start, col_start, i, j;
//	checking row
	for(col_start=0; col_start<9; col_start++){
		if(n==mat[row][col_start])
			return 0;
	}
	
//	checking in col
	for(row_start=0; row_start<9; row_start++){
		if(n==mat[row_start][col])
			return 0;
	}
	
//	checking in sub matrix
	row_start = row-row%3;
	col_start = col-col%3;
	
	for(i=0; i<3; i++){
		for(j=0; j<3; j++){
			if(n==mat[row_start+i][col_start+j])
				return 0;
		}
	}
//	if number is valid in the place
	return 1;
}

void print(int mat[9][9]){
	int i,j;
	for(i=0; i<9; i++){
		if(i%3==0)
			printf("-----------------------------\n");
		for(j=0; j<9; j++){
			if(j%3==0)
				printf("|| ");
			if(mat[i][j]!=0)	
				printf("%d ",mat[i][j]);
			else
				printf("_ ");
		}
	printf("||\n");
	}
	printf("-----------------------------\n");
}