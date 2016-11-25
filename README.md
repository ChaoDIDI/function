# 函数定义和调用 

## 定义函数 
 在javaScript中,定义函数的方法如下:
 ```javascript
 var x = 9;
 function abs(x){
 if(x >=0){
 retrun x;}else{ return -x;}}
 ```
 上述 abd()函数的定义如下:
  - function指出这是一个函数定义;
  - abs是函数的名称;
  - (x)括号内列出函数的参数,多个参数以,分割;
  - {.....}之间的代码是函数体,可以包含若干语句,甚至可以没有任何语句 
  
 请注意,函数体内部的语句在执行时,一旦执行到return时,函数就执行完毕,并将结果返回,因此,函数内部通过条件判断和循环可以实现非常复杂的逻辑 

 如果没有return语句,函数执行完毕后也会返回结果,只是结果为Undefined 

 由于javaScript的函数也是一个对象,上述定义的Abs()函数实际上是一个函数对象,而函数名abs可以视为指向该函数的变量    

 因此,第二种定义函数的方式如下:
 ```javascript 
 var abs =function(x){
 if(x>=0){return x;
 }else{ return -x;}
 };
 ```
在这种方式下, function(x){....}是一个匿名函数,它没有函数名,但是,这个匿名函数赋值给了变量abs.  
所以,通过变量abs就可以调用该函数.上述两种定义<b>完全等价</b>.注意第二种方式 按照完整语法需要在函数体末尾加一个;表示赋值语句结束.  
# 调用函数  
调用函数时, 按顺序传入参数即可:
 ```javascript 
 abs(10);//返回10
 abs(9);//返回9
 ```
由于javaScript允许传入任意个参数而不影响调用,因此传入的阐述比定义的参数多也没有问题,虽然函数内部并不需要这些参数:  
```javaScript
abs(10,'blablabla');//返回0
abs(-9;'haha','hehe',null);;//返回9
```
传入的参数比定义的少也没有问题:  
```javaScript
abs();//返回NaN
```
此时abs(x)函数的参数x将受到undefined,计算结果为NaN.  
要避免受到Undefined,可以对参数进行检查:  
```javascript
function abs(x){
if(typrof x !=='number'){
throw 'Not a number';
}if(x>=0){ 
return x;
}else{
return -x;}
}
```
## arguments 
javascript还有一个免费赠送的关键字arguments,它只在函数内部起作用,并且永远指向当前函数的调用者所传入的所有参数.arguments类似Array但他不是一个Array:  
```javascript
function foo(x){alert(x);//10
for(var i=0;i<arguments.length;i++){
alert(arguments[i]);//10 20 30 
}
}
foo(10,20,30);
```
利用auguments,你可以或得调用者传入的所有参数.也就是说,即使函数不定义任何参数,还是可以拿到参数的值:
```javascript
function abs(){
if(arguments.length==0){
return 0;
}
var x=arguments[0];
return x>= 0?x:-x;
}
abs()//0
abs(10);//10
abs(-9)//9
```
实际上arguments最常用于判断传入参数的个数.你可能会看到这样的写法:
```javascript
//foo(a[,b],c)
//接收2~3个参数,b是可选参数,如果只传2个参数,b默认为null;
function foo(a,b,c){
if(arguments.length ===2){
//实际拿到的参数是ab,c为undefined
c=b;//把b赋给c
b=null;//b变为默认值}
//....
}
```
要把中间的参数b变为'可选'参数,就只能通过arguments判断,然后重新调整参数并赋值.  
# rest参数
由于javaScript函数允许接收任意个参数,于是我们不得不用arguments来落去所有参数:  
```javascript
function foo(a,b){
var i,rest=[];
if(arguments.length>2){
for (i=2; i<arguments.length;i++){
rest.push(arguments[i]);}}
console.log('a='+a);
console.log('b='+b);
console.log(rest);
}
```
