# .MD basics
- linking --> example [[Math symbols in md]]
	```use [[the notes name u want to link]]```
	
- usage of tags  $\to$ #math
	```#the tag u want to tag xD```
	
- using bold and italics $\to$ *omale* and **omale**
	```
	*put text to be italics* 
	**put text here to be bold**
	```
- use 1. or - to number and bulletins
- header $\to$ # [put text here] and there is a 6 levels such as #, ##, ###, ... , ######
- for math writing refer [[Math symbols in md]] 
-  to code in a snippet use as following :
```c
float Q_rsqrt( float number )
{
	long i;
	float x2, y;
	const float threehalfs = 1.5F;

	x2 = number * 0.5F;
	y  = number;
	i  = * ( long * ) &y;                       // evil floating point bit level hacking
	i  = 0x5f3759df - ( i >> 1 );               // what the fuck? 
	y  = * ( float * ) &i;
	y  = y * ( threehalfs - ( x2 * y * y ) );   // 1st iteration
//	y  = y * ( threehalfs - ( x2 * y * y ) );   // 2nd iteration, this can be removed

	return y;
}
```

> excel to table --> [link](https://tabletomarkdown.com/convert-spreadsheet-to-markdown/)