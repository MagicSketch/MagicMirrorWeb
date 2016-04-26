<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="chrome=1">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <meta name="author" content="JamzTang">
    <meta name="description" content="Present your slides or deck directly within Sketch using Magic Presenter.">

    <meta property="og:title" content="Magic Presenter">
    <meta property="og:type" content="website">
    <meta property="og:url" content="http://www.google.com/">
    <meta property="og:image" content="./images/presenter_ogimage.png">
    <meta property="og:site_name" content="Magic Presenter">
    <meta property="og:description" content="Present your slides or deck directly within Sketch using Magic Presenter.">

    <meta name="twitter:card" content="summary_large_image">
    <meta name="twitter:site" content="@jamztang">
    <meta name="twitter:url" content="http://www.google.com/">
    <meta name="twitter:title" content="Magic Presenter">
    <meta name="twitter:image" content="./images/presenter_ogimage.png">
    <meta name="twitter:description" content="Present your slides or deck directly within Sketch using Magic Presenter.">

    
    <!-- Latest compiled and minified CSS -->
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css" integrity="sha384-1q8mTJOASx8j1Au+a5WDVnPi2lkFfwwEAa8hDDdjZlpLegxhjVME1fgjWPGmkzs7" crossorigin="anonymous">
    <link rel="stylesheet" href="./css/font-awesome.min.css">
    <link rel="stylesheet" href="./css/presenter.css">
    <title>Magic Presenter</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/2.2.2/jquery.min.js"></script>
    
    <script>
      var versionCheckApi = "https://api.github.com/repos/jamztang/MagicMirror/releases/latest";
      var version = "0.1";
      var versionTag = "v0.1.1";
      var isPageReady = false;
      var downloadLink = "https://github.com/jamztang/MagicPresenter/releases/download/{VERSION}/MagicPresenter.sketchplugin.zip";

      function downloadButtonClick(){
        if(!isPageReady){
          return;
        }
        var realDownloadLink = downloadLink.replace("{VERSION}", versionTag);
        window.location.href = realDownloadLink;
      }

      $( document ).ready(function() {
        $.ajax({
          url: versionCheckApi,
          method: "GET",
          dataType: "json",
          complete: function(json){
            isPageReady = true;
          },
          success: function(json){
            console.log(json);

            versionTag = json.tag_name;
            version = versionTag.substr(1);

            $(".version-text").html('version '+version);
          },
          error: function(e){

          }
        });
      });

    </script>

  </head>
  <body>
    <div class="col-md-12 col-xs-12 col-sm-12 head-section">
      <div class="section-bg"></div>
      <div class="col-md-12 col-xs-12 col-sm-12 header-bar">
        <div class="col-md-9 col-xs-8 col-sm-8">
          <object data="./images/presenter_icon.svg" type="image/svg+xml" align="top">
            <img src="./images/presenter_icon.png" align="top" />
          </object>
          <span class="title-text thin-text">Magic Presenter</span>
        </div>
        <div class="col-md-3 col-xs-4 col-sm-4 pull-right social-icon-container">
          <a href="https://twitter.com/intent/tweet?text=Present your slides or deck directly within Sketch using Magic Presenter <Link>" target="_blank"><span class="fa fa-twitter light-text social-icon"></span></a>
          <a href="http://www.facebook.com/sharer/sharer.php?" target="_blank"><span class="fa fa-facebook light-text social-icon"></span></a>
        </div>
      </div>
      <div class="head-content col-md-12 col-xs-12 col-sm-12">
        <p class="big-title light-text thin-text">Present your slides/deck</p>
        <p class="light-text sub-title thin-text">directly within Sketch</p>

        <button class="download-btn btn btn-default thin-text" onClick="downloadButtonClick()"}>Free Download</button>
        <p class="version-text thin-text">Getting update...</p>

        <div class="movie-display">
          <div class="video-wrapper">
            <video src="./video/demo.mp4" controls>
              Sorry, your browser doesn't support embedded videos.
            </video>
          </div>
        </div>
      </div>
    </div>
    
    <div class="body-content col-md-12 col-xs-12 col-sm-12">
      <p class="body-title dark-text thin-text">Why Magic Presenter?</p>
      <p class="body-sub-title dark-text thin-text">Time is money. With a single shortcut, you can put your artboards presentable slides. No more switching between presentation tools and re-exporting assets when the content is updated.</p>
      <hr class="content-hr">
      <p class="body-title-who dark-text thin-text">Who's behind</p>
      
      <div class="profile">
        <div class="profile-image"><img src="../images/profile.png" /></div>
        <div class="thin-text profile-content">
          <div class="info1">
            <span class="my-name">James Tang</span> <a href="https://twitter.com/jamztang" target="_blank"><span class="twitter-text">@jamztang</span></a>
          </div>
          <div class="info2">
            <span class="thin-text twitter-text">Creator of <a href="http://magicmirror.design/" target="_blank" class="magic-mirror-link">Magic Mirror for Sketch</a></span>
          </div>
        </div>
      </div>
      <div class="clearfix"></div>
    
    </div>

    <div class="footer col-md-12 col-xs-12 col-sm-12"><a href="https://github.com/jamztang/MagicPresenter" target="_blank"><span class="fa fa-github"></span></a></div>

  </body>
</html>

https://github.com/jamztang/MagicPresenter/releases/latest
https://github.com/jamztang/MagicPresenter/releases/download/latest/MagicPresenter.sketchplugin.zip