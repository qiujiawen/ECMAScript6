# for-in 和 for-of 的区别

1、推荐在循环对象属性的时候，使用for...in,在遍历数组的时候的时候使用for...of。

2、for...in循环出的是key，for...of循环出的是value

3、注意，for...of是ES6新引入的特性。修复了ES5引入的for...in的不足

4、for...of不能循环普通的对象，需要通过和Object.keys()搭配使

### 示例

遍历一个数组：aArray = ['a',123,{a:'1',b:'2'}]

#### for...in循环
```
for(let index in aArray){
    console.log(`${aArray[index]}`, typeof aArray[index], aArray[index],index);
}
```
控制台输出
```
a string a 0
123 number 123 1
[object Object] object Object{a: "1", b: "2"} 2
```

#### for...of循环
```
for(var value of aArray){
    console.log(value, typeof value);
}
```
控制台输出
```
a string
123 number
Object{a: "1", b: "2"} object
```

## for...in的缺陷和不足

往数组添加一个属性name
```
aArray.name = 'demo'
```
#### for...in循环
```
for(let index in aArray){
    console.log(`${aArray[index]}`;
}
```
控制台输出
```
a
123
[object Object]
demo
```

#### for...of循环
```
for(var value of aArray){
    console.log(value);
}
```
控制台输出
```
a
123
Object {a: "1", b: "2"}
```
缺陷：for-in循环除了遍历数组元素以外,还会遍历自定义属性

总结：for...of循环不会循环对象的key，只会循环出数组的value，因此for...of不能循环遍历普通对象,对普通对象的属性遍历推荐使用for...in

## for...of遍历普通对象的属性

可以通过和Object.keys()搭配使用，先获取对象的所有key的数组，然后遍历。

#### Object.keys()
Object.keys 返回一个所有元素为字符串的数组。
##### 示例

```
var arr = ['a', 'b', 'c'];
console.log(Object.keys(arr)); // console: ['0', '1', '2']

var obj = { 0: 'a', 1: 'b', 2: 'c' };
console.log(Object.keys(obj)); // console: ['0', '1', '2']

var anObj = { 100: 'a', 2: 'b', 7: 'c' };
console.log(Object.keys(anObj)); // console: ['2', '7', '100']
```
#### 遍历对象
```
var student={
    name:'jw',
    age:22,
    locate:{
    country:'china',
    city:'gz',
    }
}
for(let key of Object.keys(student)){
    console.log(key+": "+student[key]);
}
```
控制台输出：
```
name: jw
age: 22
locate: [object Object]
```
