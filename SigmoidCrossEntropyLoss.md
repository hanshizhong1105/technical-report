##Forward
```
for (int i = 0; i < count; ++i) {
    loss -= input_data[i] * (target[i] - (input_data[i] >= 0)) -
        log(1 + exp(input_data[i] - 2 * input_data[i] * (input_data[i] >= 0)));
}
```
`loss-=x*(y-(x>=0))-log(1+exp(x-2*x(x>=0)))`

if(x>=0 && y==1)
loss-=x*0-log(1+exp(-x))=-log(1+exp(-x))
if(x>=0 && y==0)
loss-=-x-log(1+exp(-x))
if(x<0 && y==1)
loss-=x-log(1+exp(x))
if(x<0 && y==0)
loss-=-log(1+exp(x))


  
