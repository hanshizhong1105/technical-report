##Forward
The original code is as following:
```
for (int i = 0; i < count; ++i) {
    loss -= input_data[i] * (target[i] - (input_data[i] >= 0)) -
        log(1 + exp(input_data[i] - 2 * input_data[i] * (input_data[i] >= 0)));
}
```
For simplifying, we set `x=input_data[i]` as input feature, and `y=target[i]` as label. 
`loss-=x*(y-(x>=0))-log(1+exp(x-2*x(x>=0)))`
Look at the 4 kinds condision

1. if `x>=0` and `y==1`
`loss=x*0-log(1+exp(-x))=-log(1+exp(-x))=-0.3133`, when `x=1`.
2. if(x>=0 && y==0)
loss-=-x-log(1+exp(-x))
3. if(x<0 && y==1)
loss-=x-log(1+exp(x))
4. if(x<0 && y==0)
loss-=-log(1+exp(x))


  
