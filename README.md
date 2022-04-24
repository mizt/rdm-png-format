### rdm-png-format

![](./data.png)

テスト動画[「クジ」／時里充](https: //vimeo.com/160485702)

#### Resolution

Width: `(width+15)&~0xF`  
Height: `((height+15)&~0xF)+(((height+15)&~0xF)>>3)`

#### Residual

X: `0`  
Y: `0`  
Width: `(width+15)&~0xF`  
Height: `(height+15)&~0xF`  

value: `-128~127` (YCbCr 4: 4: 4)  

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

##### Golden (5)
`0x00FF00`  

<div style="width: 16px;height: 16px;background: rgb(0,255,0);"></div>

##### Golden + MV (6)
`0x00FFC0`

<div style="width: 16px;height: 16px;background: rgb(192,255,0);"></div>


##### Inter (0)
`0xFF0000`

<div style="width: 16px;height: 16px;background: rgb(0,0,255);"></div>

##### Inter + MV (2, 3, 4, 7)
`0xFF4000`  
`0xFF6000`  
`0xFF8000`  
`0xFFE000`  
<div style="width: 16px;height: 16px;background: rgb(0,64,255);"></div>
<div style="width: 16px;height: 16px;background: rgb(0,96,255);"></div>
<div style="width: 16px;height: 16px;background: rgb(0,128,255);"></div>
<div style="width: 16px;height: 16px;background: rgb(0,224,255);"></div>

##### Intra (1)
`0x0000FF`

<div style="width: 16px;height: 16px;background: rgb(255,0,0);"></div>

```
char cm = -1;		
if((rgb&0xFF0000)==0xFF0000) {
  cm = (rgb-(rgb&0xFF0000)>>(8+5));
  if(cm==1||(cm>=5&&cm!=7)) cm = -1;
}
else if((rgb&0xFF00)==0xFF00) {
  cm = 5 + (!!(rgb-(rgb&0xFF00)));
}
else if((rgb&0xFF)==0xFF) {
  cm = 1;
}
```

#### Motion Vector

X: `(((width+15)&~0xF)>>3)<<1`   
Y: `(height+15)&~0xF`  
Width: `((width+15)&~0xF)>>3`  
Height: `((height+15)&~0xF)>>3`

value: `(0x80+x)<<16|0x8000|(0x80+y))`

#### See also
[rdm03.js](https: //mizt.github.io/blog/?id=rdm03)