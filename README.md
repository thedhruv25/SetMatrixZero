
#include <iostream>
#include <vector>
using namespace std;

vector<vector<int>> zeroMatrix(vector<vector<int>> &matrix, int n, int m) {
  // int row[n]={0}  ..>matrix[...][j]  this is i th row
  // int col[0]={0}; ..>matrix[i][...]  this is j th col

  int col0 = 1; // ye alag se jo bana vo h outer box

  // step1 - traverse the matrix
  //  and mark the 1st  row and col accordingly
  for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) {
      if (matrix[i][j] == 0) {
        // mark i-th row 0
        matrix[i][0] = 0;
        // mark j-th column 0
        if (j != 0)
          matrix[0][j] = 0;
        else
          col0 = 0;
      }
    }
  }
  // step 2 :mark with 0 from (1,1) to (n-1,m-1)
  for (int i = 0; i < n; i++) {
    for (int j = 1; j < m; j++) {
      if (matrix[i][j] != 0) {
        if (matrix[i][0] == 0 || matrix[0][j] == 0) {
          matrix[i][j] = 0;
        }
      }
    }
  }
  // step 3 - finally, mark the 1 st col and 1 st row
  if (matrix[0][0] == 0) {
    for (int j = 0; j < m; j++) {
      matrix[0][j] = 0;
    }
  }
  if (col0 == 0) {
    for (int i = 0; i < n; i++) {
      matrix[i][0] = 0;
    }
  }
  return matrix;
}

int main() {
  vector<vector<int>> matrix = {{1, 1, 1}, {1, 0, 1}, {1, 1, 1}}; 
  int n = matrix.size(); // declairing n in main function
  int m = matrix[0].size(); //declairing m in main function
  vector<vector<int>> ans = zeroMatrix(matrix, n, m);

  cout << "The Final matrix is: " << endl;
  for (auto it : ans) {
    for (auto ele : it) {
      cout << ele << " ";
    }
    cout << endl;
    ;
  }
  return 0;
}
