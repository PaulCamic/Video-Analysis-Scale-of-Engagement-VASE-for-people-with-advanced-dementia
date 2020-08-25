# Video-Analysis-Scale-of-Engagement-VASE-for-people-with-advanced-dementia
This project seeks to develop a visually-based method of easily assessing engagement in advanced stages of dementia through use of a tablet style computer. Using a 7 point Likert-type vertical measure the observer taps the tablet whenever they assess a change in engagement during a specified social activity. The activities we looked at were listening to music and then participating in a musical activity. 
VASE html source code
<!DOCTYPE html>
<html>
<meta charset="utf-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1">
<head><title>replace-tab-title</title></head>
<body>
<style type="text/css">
body{
  background-color: #b0e2d4;
  font-family: "Raleway", sans-serif;
}
.container {
    margin-right: auto;
    margin-left: auto;
    padding-left: 15px;
    padding-right: 15px;
    width:90%;
}
.center-block {
    display: block;
    margin-left: auto;
    margin-right: auto;
}
.site--panel{
    background: #fff;
    border-radius: 8px;
    -webkit-box-shadow: 0 0 40px -10px #000;
    box-shadow: 0 0 40px -10px #000;
    margin-top: 10px;
    /* margin: calc(0vh - 20px) auto; */
    padding: 10px 10px;
    /* max-width: calc(100vw - 40px); */
    -webkit-box-sizing: border-box;
    /*box-sizing: border-box;*/
    /* font-family: 'Montserrat',sans-serif; */
    position: relative;
    border-color: transparent;
 width:870px;
 
    margin-bottom: 22px;
}
.video-wrap{
  border: 1px solid #eeeeee;
   margin-right: auto;
    /*margin-left: auto;*/
/*    padding: 15px;*/
    width: 850px;
    
}
.slider-wrap{
  width:100%;
  padding:10px 0;
}
input[type="range"] {
    display: block;
    width: 100%;
}
.btn-results{
  border:1px solid #000;
  cursor: pointer;
}
.range-left{
  padding-right:5px;
  margin-top:-10px;
}
.range-right{
  padding-left:5px;
}
.btn-warning {
    color: #fff;
    background-color: #2ab27b;
    border-color: #259d6d;
}
.btn {
    display: inline-block;
    margin-bottom: 0;
    font-weight: normal;
    text-align: center;
    vertical-align: middle;
    -ms-touch-action: manipulation;
    touch-action: manipulation;
    cursor: pointer;
    background-image: none;
    border: 1px solid transparent;
    white-space: nowrap;
    padding: 6px 12px;
    font-size: 14px;
    line-height: 1.6;
    border-radius: 4px;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
}
.slider-range{
  margin:10px 0;
}
.slider-range .max { float:right }
.slider-range .min { float:left }
.pad-top-bot{
  margin:10px 0;
}
textarea#results {
  display:block;
  width: 100%;
  height: 120px;
  border: 2px solid #cccccc;
  
}
.heading{
  margin:10px 0;
}
</style>
<div class="container">  
   
        <div class="panel panel-default site--panel">
            <div class="panel-heading clearfix"><h1 class="error">Music-1</h1> </div>
                <div class="video-wrap">
                <video id="myVideo" width="850" height="500" controls>
                  <source src="file:set1.mp4" type="video/mp4" />
                  <source src="file:set1.mp4" type="video/ogg" />
                  Your browser does not support HTML5 video.
                </video>
           
            <div class="pad-top-bot">Playback position: <span id="txtPlaytime"></span></div>
            <div class="pad-top-bot">Rating : <span id="txtRating"></span></div>
            <div class="slider-range">
              <span class="min">1</span>
              <span class="max">7</span>
            </div>
            <div class="slider-wrap">
                <input type="range" min="1" max="7" value="0" list="ticks"/>
                
                <datalist id="ticks">
                    <option>1</option>
                    <option>2</option>
                    <option>3</option>
                    <option>4</option>
                    <option>5</option>
                    <option>6</option>
                    <option>7</option>
                </datalist>
            </div>
<div class="btn btn-warning" onclick="showRes();">click me when done</div>
<!-- <div class="btn btn-warning" onclick="CopyToClipboard('results');">Show res (click me at the end)</div> -->
<div class="heading">Results: Click anywhere in box below, Ctrl-a = select all, ctrl-v to copy, ctrl-c to paste</div>
<textarea id="results" class="styled"></textarea>
 </div><!-- end video wrap -->
</div>
</div>
<script>
  window.Res = [];
  //find the vid div
  var vid = document.getElementById("myVideo");
  // Assign an ontimeupdate event to the video
  vid.ontimeupdate = function() {videoPlayTimeUpdate()};
  function videoPlayTimeUpdate() {
      // Display the current position of the video
      document.getElementById("txtPlaytime").innerHTML = vid.currentTime;
  }
  function getRes(){
    //dump the results out
    var str = 'playtime ,rating \r\n';
    window.Res.forEach(function(i){
            str += i + '\r\n';
    });
    
    return str;
  }
  function showRes(){
    
    document.getElementById("results").value = getRes();
  }
  //our slider
  var rng = document.querySelector("input");
  //listen function for slider
  var listener = function() {
    window.requestAnimationFrame(function() {
      window.Res.push(vid.currentTime +' , '+rng.value  );
      document.getElementById("txtRating").innerHTML = rng.value;
      // document.getElementById("results").innerHTML = rng.value + ' at ' + vid.currentTime;
    });
  };

rng.addEventListener("change", function() {
    listener();
    
  });
</script>
</body>
</html>


