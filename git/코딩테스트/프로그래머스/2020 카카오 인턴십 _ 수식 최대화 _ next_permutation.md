# 2020 카카오 인턴십 _ 수식 최대화 : next_permutation

- 문제 풀이 방식

  - `oper 벡터` : 연산자의 우선순위를 정해준다

    - `0` : + / `1` : - / `2` : *

  - `tmp_operation1[i]`의 연산자를 기준으로 `tmp_number1[i]`와 `tmp_number1[i+1]`을 계산한다.

    - 우선순위 연산자라면?

      ```c++
      tmp_number1[j+1] = tmp_number1[j] ( + / - / * ) tmp_number1[j+1];
      ```

      

    - 아니라면?

      ```c++
      tmp_number2.push_back(tmp_number1[j]);
      tmp_operation2.push_back(tmp_operation1[j]);
      ```

      

    - tmp_number1의 마지막 원소는 tmp_number2에 추가한다.



- 문제가 되었던 부분
  - <long long> 처리 안해서
  - abs 절댓값 처리 안해서



```c++
#include <string>
#include <vector>
#include <algorithm>

using namespace std;
vector<int> oper;
vector<long long> number;
vector<int> operation;

long long solution(string expression) {
    long long answer = 0;
    int oper_num[3] = {0,};
    
    string num = "";
    for(int i=0; i<expression.size(); i++){
        char c = expression[i];
        if(c=='+') {operation.push_back(0); number.push_back(stoi(num)); num=""; oper_num[0]++;}
        else if(c=='-') {operation.push_back(1); number.push_back(stoi(num)); num=""; oper_num[1]++;}
        else if(c=='*') {operation.push_back(2); number.push_back(stoi(num)); num=""; oper_num[2]++;}
        else num+=c;
    }
    number.push_back(stoi(num));
    
    //oper_num은 해당 연산이 몇개있는지 확인한다
    if(oper_num[0]>0) oper.push_back(0);
    if(oper_num[1]>0) oper.push_back(1);
    if(oper_num[2]>0) oper.push_back(2);

    // next_permutation은 숫자를 순서대로 배열
    // 문자를 넣어서 순열을 돌리면 원하는대로 모든 경우의 수가 나오지 않음
    do{ //oper의 순서가 계속 변화함
        string str = expression;
        vector<long long> tmp_number1;
        vector<long long> tmp_number2;
        vector<int> tmp_operation1;
        vector<int> tmp_operation2;
        
        tmp_number1 = number;
        tmp_operation1 = operation;
        
        for(int i=0; i<oper.size(); i++){
            int tmp_oper = oper[i];
            for(int j=0; j<tmp_operation1.size(); j++){
                if(tmp_operation1[j]==oper[i]){
                    if(tmp_oper==0){tmp_number1[j+1] = tmp_number1[j]+tmp_number1[j+1];}
                    else if(tmp_oper==1){tmp_number1[j+1] = tmp_number1[j]-tmp_number1[j+1];}
                    else{tmp_number1[j+1] = tmp_number1[j]*tmp_number1[j+1];}
                }
                else{
                    tmp_number2.push_back(tmp_number1[j]);
                    tmp_operation2.push_back(tmp_operation1[j]);
                }
                if(j==tmp_operation1.size()-1){
                    tmp_number2.push_back(tmp_number1[j+1]);
                }
            }
            tmp_number1.clear();
            tmp_operation1.clear();
            tmp_number1 = tmp_number2;
            tmp_operation1 = tmp_operation2;
            tmp_number2.clear();
            tmp_operation2.clear();
        }
        if(answer<abs(tmp_number2[0])) answer = abs(tmp_number2[0]);
    }while(next_permutation(oper.begin(), oper.end()));

    return answer;
}
```

