---
layout: default
title: php数组总结
---

## 新建数组 ##

数组没有大小限制，所以只需建立引用就可以创建数组，例如：

```
$state[0]= ‘111';
$state[1]= ‘222';
``` 

如果索引值是数值索引而且是递增的，还可以在创建时省略索引值。

```
$state[] =‘111';
$state[] =‘222';
``` 

可以使用array()创建数组,如：

```
$state =array(‘111', ‘222');
$state =array(‘one'=>'111', ‘two'=>'222');
``` 

使用list()提取数组,例如：

```
$state= array(‘one', ‘two', ‘three');
list($one,$two, $three) = $state;
``` 

	数组内的三个值分别赋给了$one, $two,$three, 可直接输出。

用预定义的值范围填充数组，例如：

```
$num= range(1, 6);
//类似于$num =array(1, 2, 3, 4, 5, 6);
可选择奇偶：$num =range(1, 6, 2);
 
//$num= array(1, 3, 5);
可选择字母：$ch =range(“A”, “F”);
//$ch= array(“A”, “B”, “C”, “D”, “E”, “F”);
``` 

## 输出数组 ##

输出数组内容最常用的方法就是迭代处理各个数组键，并输出相应的值。
 
* foreach()函数可以很方便的遍历一个数组，得到每个value和key。
 
* print_r()函数很方便将数组的内容输出到屏幕上。prinf_r()函数接受一个变量，并将其

内容发送给标准输出，成功时返回TRUE，否则返回FALSE。

* var_dump(); 详细打印数组信息;
  
## 测试数组 ##
  
通过is_array()函数知道某个特定变量是否一个数组。
 
is_array()函数确定某变量是否为数组，如果是则返回TRUE，否则返回FALSE。即使数组只包含一个值，也将被认为是一个数组。 

## 添加和删除数组元素 ##

PHP为扩大和缩小数组提供了一些函数，对模仿各种队列实现提供便利。
 
* 在数组头添加元素：

__array_unshift()__函数在数组头添加元素。所有已有的数值键都会相应地修改，以反映其在数组中的新位置，但是关联键不受影响。

```
$state= array(‘11', ‘22', ‘33');
array_unshift($state,‘00');
//$state= array(‘00', ‘11', ‘22', ‘33');
```
 
* 在数组尾添加元素：

__array_push()__函数将值添加到数组的末尾，添加新的值之后返回数组中的元素总数。同时通过将这个变量作为输入参数传递给此函数，向数组压入多个变量(元素)，其形式为：
```
$state= array(‘1', ‘2');
array_push($state,‘3');
//$state= array(‘1', ‘2', ‘3');
```
 
* 从数组头删除元素：

__array_shift()__函数删除并返回数组中找到的第一个元素。其结果是，如果使用的是数值键，则所有相应的值都会下移，而使用关联键的数组不受影响，其形式为：
```
$state= array(‘1', ‘2');
array_shift($state);
//$state= array(‘2');
```
 
* 从数组尾删除元素：

__array_pop()__函数删除并返回数组的最后一个元素，其形式为：
```
$state= array(‘1', ‘2');
array_pop($state);
//$state= array(‘1'); 
```
 
## 定位数组元素 ##  

* 搜索数组：

__in_array()__函数在数组中搜索一个特定值，如果找到这个值则返回TRUE，否则返回FALSE，其形式如下：

```
$user= array(‘111', ‘222', ‘333');
$str= ‘111';
if(in_array($str,$user)){
    echo‘yes';
}else{
    echo ‘no';
}
```

第三个参数strict可选，它强制in_array()在搜索时考虑类型。
 
* 搜索关联数组：

如果在一个数组中找到一个指定的键，函数__array_key_exists()__返回TRUE，否则返回FALSE。其形式如下：

```
$arr= array('one'=>'1', 'two'=>'2', 'three'=>'3');
if(array_key_exists('two',$arr)){
    echo'yes';
}else{
    echo‘no';
}
```
 
* 搜索关联数组：

__array_search()__函数在一个数组中搜索一个指定的值，如果找到则返回相应的值，否则返回FALSE，其形式如下：

```
$arr= array('one'=>'1', 'two'=>'2', 'three'=>'3');
if(array_search('1',$arr)){
    echo'yes';
}else{
    echo‘no';
}
```
 
* 获取数组键：

__array_key()__函数返回一个数组，其中包含所搜索数组中找到的所有键，其形式如下：
```
$arr= array('one'=>'1', 'two'=>'2', 'three'=>'3');
$keys= array_keys($arr); var_dump($keys);
//array(3) {[0]=> string(3) "one" [1]=> string(3) "two" [2]=>string(5) "three" }
```
 
* 获取数组值：

__array_values()__函数返回一个数组中的所有值，并自动为返回的数组提供数组索引，其形式如下：

```
$arr= array('one'=>'1', 'two'=>'2', 'three'=>'3');
$values= array_values($arr); var_dump($values);
//array(3) {[0]=> string(1) "1" [1]=> string(1) "2" [2]=>string(1) "3" } 
```
  
## 遍历数组 ##
 
通常需要遍历数组并获得各个键或值(或者同时获得键和值)，PHP提供了一些函数来满足需求。许多函数能完成两项任务，不仅能获取当前指针位置的键或值，还能将指针移向下一个适当的位置。
 
* 获取当前数组键：

__key()__函数返回数组中当前指针所在位置的键，其形式如下：

```
$arr= array('one'=>'1', 'two'=>'2', 'three'=>'3');
$key= key($arr);
var_dump($key);
//string(3) "one"
```

注意：每次调用key()时不会移动指针。
 
* 获取当前数组值：

__current()__函数返回数组中当前指针所在位置的数组值。其形式如下：

```
$arr= array('one'=>'1', 'two'=>'2', 'three'=>'3');
$value= current($arr);
var_dump($value);
//string(1)“1”
```
 
* 获取当前数组键和值：

__each()__函数返回数组的当前键/值对，并将指针推进一个位置，其形式如下：

```
$arr =array('one'=>'1', 'two'=>'2', 'three'=>'3');
var_dump(each($arr));
//array(4) {[1]=> string(1) "1" ["value"]=> string(1)"1" [0]=> string(3) "one" ["key"]=>string(3)"one" ["key"]=>string(3) "one" }
```

返回的数组包含4个键，键0和key键包含键名，而键1和value包含相应的数据。如果执行each()前指针位于数组末尾，则返回FALSE。
 
  
## 移动数组指针 ##
 
1. 将指针移动到下一个数组位置
 
	__next()__函数返回紧接着放在当前数组指针下一个位置的数组值，如果指针本来就位于数组的最后一个位置，则返回FALSE

	```
	$arr= array('one'=>'1', 'two'=>'2', 'three'=>'3');
	echo next($arr);
	//输出2
	echo next($arr);
	//输出3
	```
 
2. 将指针移动到前一个数组位置
 
	__prev()__函数返回位于当前指针前一个位置的数组值，如果指针本来就位于数组的第一个位置，则返回FALSE
 
3. 将指针移动到第一个数组位置
 
	__reset(__)函数用于将数组指针设置回数组的开始位置，如果需要在脚本中多次查看或处理一个数组，经常使用这个函数，另外这个函数还经常在排序结束时使用。
 
4. 将指针移动到最后一个数组位置
 
	__end()__函数将指针移动到数组的最后一个位置，并返回最后一个元素。
 
* 向函数传递数组值：
 
	__array_walk()__函数将数组中的各个元素传递到用户自定义函数。如果需要对各个数组元素完成某个特定动作，这个函数将起作用。其形式如下：

``` 
function test($value ,$key){
    echo$value.' '.$key."";
}
$arr= array('one'=>'1', 'two'=>'2', 'three'=>'3');
array_walk($arr,'test');
//1 one
//2 two
//3 three
```

如果使用多维数组，PHP5中引入的array_walk_recursive()函数可以递归地对数组中的每一个元素应用一个用户定义函数。
 
  
## 确定数组大小和元素唯一性 ## 

* 确定数组的大小：

__count()__函数返回数组中值的总数
 
如果启动了可选的mode参数(设置为1)，数组将进行递归计数统计元素。count(array(), 1);
 
	注意：sizeof()函数是count()的别名。功能一致。
 
* 统计数组元素出现的频率：

__array_count_values()__函数返回一个包含关联键/值对的数组，其形式如下：

```
$arr= array('A', 'B', 'C', 'A');
$res= array_count_values($arr);
print_r($res);
//Array( [A] => 2 [B] => 1 [C] => 1 )
```

值表示出现的频率。
 
* 确定唯一的数组元素：

__array_unique()__函数会删除数组中所有重复的值，返回一个由唯一值组成的数组，其形式如下：

```
$arr= array('A', 'B', 'C', 'A');
$res= array_unique($arr); print_r($res);
//Array( [0] => A [1] => B [2] => C )
```

可选参数sort_flags(PHP5.2.9中新增)可以确定如何对数组键排序。默认地，值会被作为字符串排序，不过也可以按数值对值排序(SORT_NUMERIC)，或使用PHP默认的排序方法(SORT_REGULAR)，还可以根据本地化环境排序(SORT_LOCALE_STRING)。
  
## 数组排序 ##
 
* 逆置数组元素排序

__array_reverse()__函数将数组中元素的顺序逆置，其形式如下：

```
$arr= array('A', 'B', 'C');
$res= array_reverse($arr);
print_r($res);
//Array( [0] => C [1] => B [2] => A )
```

如果可选参数preserve_keys设置为TRUE，则保持键映射，否则重新摆放后的各个值将对应于先前该位置上的相应键。

``` 
$arr= array('A', 'B', 'C');
$res= array_reverse($arr, true);
print_r($res);
//Array( [2] => C [1] => B [0] => A )
``` 
 
* 置换数组键和值：

__array_flip()__函数将置换数组中键及其相应值的角色，其形式如下：

``` 
$arr= array('A', 'B', 'C');
$res= array_flip($arr);
print_r($res);
//Array( [A] => 0 [B] => 1 [C] => 2 )
```
 
* 数组排序
 
__sort()__函数对数组进行排序，各元素按值由低到高的顺序排列，其形式如下：
 
sort()函数不返回排序后的数组，相反它只是“就地”对数组排序，不论结果如何都不返回任何值。sort_flags参数可选，将根据这个参数指定的值修改该函数的默认行为。
 
1. SORT_NUMERIC，按数值排序。对整数和浮点数排序很有用。
 
2. SORT_REGULAR，按照相应的ASCII值对元素排序。
 
3. SORT_STRING，按接近于人所认知的正确顺序对元素排序。
 
要保持初始键/值对应条件下的数组排序需要用到asort()函数。
 
__assort()__函数与__sort()__函数相同，以升序对数组排序，只不过它将保持键/值的关联，其形式如下：

``` 
$arr= array('C', 'B', 'A');
$res= $arr;
print_r($arr);
sort($arr);
print_r($arr);
asort($res);
print_r($res);
//Array ( [0]=> C [1] => B [2] => A ) Array ( [0] => A [1] => B [2] => C )Array ( [2] => A [1] => B [0] => C )
```
 
* 以逆序对数组排序
 
__rsort()__函数与sort()函数相同，只不过它以相反的顺序(降序)对数组元素排序。
 
如果使用可选的sort_flags参数，具体的排序行为将由这个值确定。
 
保持键/值对的条件下以逆序对数组排序
 
与asort()一样，__arsort()__函数会保持键/值的关联，但是它以逆序对数组up

``` 
$arr= array('C', 'B', 'A', 'D');
arsort($arr); print_r($arr);
//Array( [3] => D [0] => C [1] => B [2] => A )
```

如果使用可选的sort_flags参数，具体的排序行为将由这个值确定。
 
* 数组自然排序

__natsort()__函数提供了一种相当于人们平常使用的排序机制。
 
1. 典型算法排序如下：

	p1.jpg,p10.jpg, p2.jpg, p20.jpg
 
	使用natsort()函数如下：
 
	p1.jpg,p2.jpg, p10.jpg, p20.jpg
 
2. 不区分大小写的自然排序：
 
	Picture1.jpg,PICTURE10.jpg, picture2.jpg, picture20.jpg
 
3. 按键值对数组排序
 
	ksort()函数按键对数组排序，如果成功则返回TRUE，失败将返回FALSE
 
4. 以逆序对数组键排序
 
	krsort()函数的操作与ksort()相同，也按键排序，将以逆序排序。
 
5. 根据用户自定义规则排序

	usort()函数提供了另一种排序方法，可以使用在该函数中指定的用户自定义比较算法对数组排序。如果需要以某种方法对数据排序，而PHP的任何内置排序函数没有提供相应支持，就需要该函数。

## 数组合并、拆分、接合和分解 ## 

* 合并数组

__array_merge()__函数将数组合并到一起，返回一个联合的数组。所得到的数组以第一个输入数组参数开始，按后面数组参数出现的顺序依次追加。其形式如下：

```
$arr= array('C', 'B', 'A', 'D');
$arr1= array('1', '2', '3', '4');
$arr2= array_merge($arr, $arr1); print_r($arr2);
//Array( [0] => C [1] => B [2] => A [3] => D [4] => 1 [5] => 2 [6]=> 3 [7] => 4 )
```
 
* 递归追加数组

__array_merge_recursive()__函数与__array_merge()__相同，可以将两个或多个数组合并到一起，形成一个联合的数组。两者之间的区别在于，当某个输入数组中的某个键已经存在于结果数组中时该函数会采取不同的处理方法。array_merge()会覆盖前面存在的键/值对，将其替换为当前输入数组中的键/值对，而array_merge_recursive()将两个值合并在一起，形成一个新的数组并以原有的键作为数组名。其形式为：

``` 
$arr= array('one'=>'C', 'one'=>'B');
$arr1= array('three'=>'1', 'one'=>'2');
$arr2= array_merge_recursive($arr, $arr1); print_r($arr2);
//Array( [one] => Array ( [0] => B [1] => 2 ) [three] => 1 )
``` 
 
* 合并两个数组

__array_combine()__函数会生成一个新数组，这个数组由一组提交的键和对应的值组成，其形式为：

``` 
$arr= array('A', 'B');
$arr1= array('1', '2');
$arr2= array_combine($arr, $arr1);
print_r($arr2); //Array( [A] => 1 [B] => 2 )
``` 
 
* 拆分数组
 
__array_slice()__函数将返回数组中的一部分，从键offset开始，到offset+length位置结束。
 
offset为正值时，拆分将从距数组开头的offset位置开始;如果offset为负值，则拆分从距数组末尾的offset位置开始。如果省略了可选参数length，则拆分将从offset开始，一直到数组的最后一个元素。如果给出了length且为正数，则会在距数组开头的offset+length位置结束。相反，如果给出了length且为负数，则在距数组开头的count(array) - |length|位置结束。其形式如下：

```
$arr= array('A', 'B', 'C', 'D');
$arr1= array_slice($arr, 2, 1);
print_r($arr1); //Array( [0] => C )
``` 
 
* 求数组的交集

__array_intersect()__函数返回一个保留了键的数组，这个数组只由第一个数组中出现的且在其他每个输入数组中都出现的值组成。其形式如下：

``` 
$arr= array('A', 'B', 'C', 'D');
$arr1= array('A', 'B', 'E');
$arr2= array('A', 'F', 'D');
$arr3= array_intersect($arr, $arr1, $arr2);
print_r($arr3);
//Array( [0] => A )
```
 
注意：只有在两个元素有相同的数据类型时，array_intersect()才会认为它们相等。
 
* 求关联数组的交集

__array_intersect_assoc()__与__array_intersect()__基本相同，只不过它在比较中还考虑了数组的键。因此，只有在第一个数组中出现，且在所有其他输入数组中也出现的键/值对才被返回到结果数组中。其形式如下：

```
$arr= array('a'=>'A', 'b'=>'B', 'c'=>'C', 'd'=>'D');
$arr1= array('a'=>'A', 'c'=>'B', 'E');
$arr2= array('a'=>'A', 'b'=>'F', 'd'=>'B');
$arr3= array_intersect_assoc($arr, $arr1, $arr2);
print_r($arr3);
//Array( [a] => A )
```
 
 
* 求关联数组的差集

函数__array_diff_assoc()__与array_diff()基本相同，只是它在比较时还考虑了数组的键，因此，只在第一个数组中出现而不在其他输入数组中出现的键/值对才会被返回到结果数组中。其形式如下：

``` 
$arr= array('a'=>'A', 'b'=>'B', 'c'=>'C', 'd'=>'D');
$arr1= array('a'=>'A', 'b'=>'B', 'e'=>'E');
$arr3= array_diff_assoc($arr, $arr1);
print_r($arr3);
//Array( [c] => C [d] => D )
``` 
 
* 其他有用的数组函数
 
返回一组随机的键
 
__array_rand()__函数将返回数组中的一个或多个键。其形式为：

```
$arr= array('a'=>'A', 'b'=>'B', 'c'=>'C', 'd'=>'D');
$arr1= array_rand($arr, 2);
print_r($arr1);
//Array( [0] => b [1] => d )
``` 
 
* 随机洗牌数组元素
* 
__shuffle()__函数随机地对数组元素重新排序。
 
* 对数组中的值求和

__array_sum()__函数将数组内的所有值加在一起，返回最终的和，其形式如下：

```
$arr= array('A', 32, 12, 'B');
$count= array_sum($arr);
print_r($count);
//44
```
 
如果数组中包含其他数据类型(例如字符串)，这些值将被忽略。
 
* 划分数组

__array_chunk()__函数将数组分解为一个多维数组，这个多维数组由多个包含size个元素的数组所组成。其形式如下：

``` 
$arr= array('A', 'B', 'C', 'D');
$arr1= array_chunk($arr, 2);
print_r($arr1);
//Array( [0] => Array ( [0] => A [1] => B ) [1] => Array ( [0] => C [1]=> D ) )  
```
 

<center><strong>{{ page.date | date_to_string }}</strong></center>
