# MatriciCsv
include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define DIM 10


int generaMatrice(int mat[][DIM]){
  int dim;

  do{
    printf("dimensione matrice ");
    scanf("%d", &dim);
  }while(dim<0 || dim>DIM);

  for(int i=0; i<dim; i++){
    for(int j=0; j<dim; j++){
      mat[i][j] = (rand()%50)+1;
    }
  }

  return dim;
}

FILE* aperturaFile(FILE* fp){
 fp = fopen("matrice.csv", "w");

  if(fp==NULL){
    printf("\nErrore apertura del file");
    exit(0);
  }

  return fp;
}

void salvaSuFile(FILE* fp, int mat[][DIM], int dim){
  for(int i=0; i<dim; i++){
    fprintf(fp, "\n");
    for(int j=0; j<dim; j++){
      if(j==dim-1){
        fprintf(fp, "%d", mat[i][j]);
      }else{
        fprintf(fp, "%d, ", mat[i][j]);
      }
    }
  }
}

int main(void) {
  int mat[DIM][DIM];
  FILE *fp;
  int scelta, dim;

  srand(time(NULL));

  do{
    printf("Inserire il numero scelto ");
    scanf("%d", &scelta);
    switch(scelta){
      case 1: 
        dim = generaMatrice(mat);
      break;
      case 2:
        aperturaFile(fp);
        salvaSuFile(fp, mat, dim);
      break; 
    } 
  }while(scelta!=0);
  
  
}
