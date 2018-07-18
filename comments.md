---
date: 2018-07-18
---
<head>
<title>留言板</title>
<link rel="icon" href="https://avatars1.githubusercontent.com/u/21288752?s=40&amp;v=4" type="image/x-icon">
<script type="text/javascript"> 
  window.onload = function() {  
    var show = document.getElementById("show");  
    setInterval(function() {   
      var time = new Date();   // 程序计时的月从0开始取值后+1   
      var m = time.getMonth() + 1;   
      if(m < 10) m ="0" + m;
      var d = time.getDate();   
      if(d < 10) d ="0" + d;
      var h = time.getHours();   
      if(h < 10) h ="0" + h;
      var min = time.getMinutes();   
      if(min < 10)min ="0" + min;
      var sec = time.getSeconds();   
      if(sec < 10)sec ="0" + sec;
      var t = time.getFullYear() + "-" + m + "-"     
      + d + " " + h + ":"     
      + min + ":" + sec;   
      show.innerHTML = t;  
    }, 1000); 
};
</script>
</head>
<body>
<script>
var idcomments_acct = '4e68ed3635838eee1563143fe75435eb';
var idcomments_post_id;
var idcomments_post_url;
</script>
<span id="IDCommentsPostTitle" style="display:none"></span>
<script type='text/javascript' src='https://www.intensedebate.com/js/genericCommentWrapperV2.js'></script>
<script>
var idcomments_acct = '4e68ed3635838eee1563143fe75435eb';
var idcomments_post_id;
var idcomments_post_url;
</script>
<p align="right" id="show"></p>
</body>