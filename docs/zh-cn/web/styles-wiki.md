# CSS 手机适配

```css
@media (device-height:568px) and (-webkit-min-device-pixel-ratio:2){/* 兼容iphone5 */} 
@media only screen and (max-device-width :480px){ } 
@media only screen and (min-device-width :481px){ } 

/*6*/ 
@media (min-device-width : 375px) and (max-device-width : 667px) and (-webkit-min-device-pixel-ratio : 2){ } 

/*6+*/ 
@media (min-device-width : 414px) and (max-device-width : 736px) and (-webkit-min-device-pixel-ratio : 3){ } 

/*魅族*/ 
@media only screen and (min-device-width :1080px) and (-webkit-min-device-pixel-ratio : 2.5){ } 

/*mate7*/ 
@media only screen and (min-device-width :1080px) and (-webkit-min-device-pixel-ratio : 3){ } 

/*4 4s*/ 
@media only screen and (device-height :480px) and (-webkit-device-pixel-ratio:2){ } 

```