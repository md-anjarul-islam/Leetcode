# Problem
The n-queens puzzle is the problem of placing n queens on an n x n chessboard such that no two queens attack each other.

Given an integer n, return all distinct solutions to the n-queens puzzle. You may return the answer in any order.

Each solution contains a distinct board configuration of the n-queens' placement, where 'Q' and '.' both indicate a queen and an empty space, respectively.

# Solution
```
class Solution {
    vector<bool> col, leftBottomToRightUp, rightBottomToLeftUp;
    int N;
    vector<string> board;
    vector<vector<string>> ans;

    void solve(int pos){
        if(pos == N){
            ans.push_back(board);
            return ;
        }

        // Now we are at pos row. we need to place a queen at any column in this row
        for(int j=0; j<N; j++){

            if(
                col[j] == false // if the column has no queen yet.
                && leftBottomToRightUp[pos+j] == false // if no queen in left bottom to right up diagonal
                && rightBottomToLeftUp[pos-j+N] == false // if no queen in left top to right bottom corner
            ){
                col[j] = true;
                leftBottomToRightUp[pos+j] = true;
                rightBottomToLeftUp[pos-j+N] = true;
                board[pos][j] = 'Q';
               
                solve(pos+1);
               
                col[j] = false;
                leftBottomToRightUp[pos+j] = false;
                rightBottomToLeftUp[pos-j+N] = false;
                board[pos][j] = '.';
            }
        }
    }
public:
    vector<vector<string>> solveNQueens(int n) {
        col = vector<bool>(n, false);
        leftBottomToRightUp = vector<bool>(2*n, false);
        rightBottomToLeftUp = vector<bool>(2*n, false);

        board = vector<string>(n, string(n, '.'));
        N = n;

        solve(0);

        return ans;
    }
};
```
