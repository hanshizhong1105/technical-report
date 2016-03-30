##Forward
The original code is as following:
```
for (int i = 0; i < count; ++i) {
    loss -= input_data[i] * (target[i] - (input_data[i] >= 0)) -
        log(1 + exp(input_data[i] - 2 * input_data[i] * (input_data[i] >= 0)));
}
```
For simplifying, we set `x=input_data[i]` as input feature, and `y=target[i]` as label.  
`loss=-x*(y-(x>=0))+log(1+exp(x-2*x(x>=0)))`

Look at the 4 kinds condision

1. if `x>=0 && y==1`, especially when `x=1`  
`loss=log(1+exp(-x))=0.3133`.
2. if `x>=0 && y==0`, especially when `x=1`  
`loss=x+log(1+exp(-x))=-1.3133`
3. if `x<0 && y==1)`, especially when `x=-1`  
`loss=x+log(1+exp(x))=-1.3133`
4. if `x<0 && y==0`, especailly when `x=-1`  
`loss=log(1+exp(x))=0.3133`


  
