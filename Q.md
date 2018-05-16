var v1 = 0,v2=0,v3=0;
for(var i=1;i<4;i++){
  var i2=i; 
  (function(){
    var i3 = i;
    setTimeout((function(){
      v1+=i;
      v2+=i2;
      v3+=i3;
    }),5);
  })();
}
setTimeout((function(){
  console.log('v1='+v1+',v2='+v2+',v3='+v3);
}),10);