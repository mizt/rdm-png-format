### rdm-png-format

![](./data.png)

Width: `(width+15)&~0xF`  
Height: `((height+15)&~0xF)+(((height+15)&~0xF)>>3)`

#### Residual

X: `0`  
Y: `0`  
Width: `(width+15)&~0xF`  
Height: `(height+15)&~0xF`  

YCbCr: `4`:`4`:`4`   
Range is `-128`~`127` 


#### Display Fragments

X: `((width+15)&~0xF)>>3`   
Y: `(height+15)&~0xF`  
Width: `((width+15)&~0xF)>>3`  
Height: `((height+15)&~0xF)>>3`

value: `0` or `0xFFFFFF`

#### Coding Mode

X: `0`  
Y: `(height +15)&~0xF`  
Width: `((width+15)&~0xF)>>3`  
Height: `((height+15)&~0xF)>>3`  

value:

```
char mv = -1;		
if((rgb&0xFF0000)==0xFF0000) {
  mv = (rgb-(rgb&0xFF0000)>>13);
  if(mv==1||(mv>=5&&mv!=7)) mv = -1;
}
else if((rgb&0xFF00)==0xFF00) {
  mv = 5 + (!!(rgb-(rgb&0xFF00)));
}
else if((rgb&0xFF)==0xFF) {
  mv = 1;
}
```

##### Intra (1)
`rgb(0,0,255)`

<div style="width:16px;height:16px;background:rgb(0,0,255);"></div>

##### Golden (5)
`rgb(0,255,0)`  

<div style="width:16px;height:16px;background:rgb(0,255,0);"></div>

##### Golden + MV (6)
`rgb(0,255,192)`  

<div style="width:16px;height:16px;background:rgb(0,255,196);"></div>


##### Inter (0)
`(255,0,0)`

<div style="width:16px;height:16px;background:rgb(255,0,0);"></div>

##### Inter + MV (2,3,4,7)
`rgb(255,64,0)`  
`rgb(255,96,0)`  
`rgb(255,128,0)`  
`rgb(255,224,0)`  
<div style="width:16px;height:16px;background:rgb(255,64,0);"></div>
<div style="width:16px;height:16px;background:rgb(255,96,0);"></div>
<div style="width:16px;height:16px;background:rgb(255,128,0);"></div>
<div style="width:16px;height:16px;background:rgb(255,224,0);"></div>


#### Motion Vector

X: `(((width+15)&~0xF)>>3)<<1`   
Y: `(height+15)&~0xF`  
Width: `((width+15)&~0xF)>>3`  
Height: `((height+15)&~0xF)>>3`

value: `((unsigned char)((y+0x80)&0xFF))<<16|0x8000|((unsigned char)((x+0x80)&0xFF))`

See also  
[rdm03.js](https://mizt.github.io/blog/?id=rdm03)