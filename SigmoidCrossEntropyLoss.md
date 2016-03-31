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

Look at the 4 kinds condisions. Condition 1 and Condition 3 are corrected classified, the loss is lower as 0.3133. When the predictions are wrong as Condision 2 and 3, the loss is bigger of 1.3133. 

1. if `x>=0 && y==1`, especially when `x=1`  
`loss=log(1+exp(-x))=0.3133`.
2. if `x>=0 && y==0`, especially when `x=1`  
`loss=x+log(1+exp(-x))=1.3133`
3. if `x<0 && y==1)`, especially when `x=-1`  
`loss=-x+log(1+exp(x))=1.3133`
4. if `x<0 && y==0`, especailly when `x=-1`  
`loss=log(1+exp(x))=0.3133`

##Backward
```
sigmoid_top_vec_.push_back(sigmoid_output_.get());
sigmoid_layer_->Forward(sigmoid_bottom_vec_, sigmoid_top_vec_);
const Dtype* sigmoid_output_data = sigmoid_output_->cpu_data();
caffe_sub(count, sigmoid_output_data, target, bottom_diff);
```
Translate it to the equation is:  
`diff=sigmoid(x)-y=1/(1+exp(-x))-y`

##Loss Functoin Derivation
The loss function of cross entroy is as following:  
![equation](http://latex.codecogs.com/gif.latex?E%20%3D%20%5Cfrac%7B-1%7D%7Bn%7D%20%5Csum%5Climits_%7Bn%3D1%7D%5EN%20%5Cleft%5B%20p_n%20%5Clog%20%5Chat%7Bp%7D_n%20&plus;%20%281%20-%20p_n%29%20%5Clog%281%20-%20%5Chat%7Bp%7D_n%29%20%5Cright%5D)
For Each example the loss is  
![equation](http://latex.codecogs.com/gif.latex?loss%20%3D%20-%20p_n%20%5Clog%20%5Chat%7Bp%7D_n%20&plus;%20%281%20-%20p_n%29%20%5Clog%281%20-%20%5Chat%7Bp%7D_n%29)


  
