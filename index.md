

<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>Index</title>
</head>
<body>

    <div class="chat-overlay chat-overlay-closed">
  <div class="chat-overlay-wrapper">
        <div class="chat-overlay-header-mobile close">
        <img class="close" src="/close.png" alt="toggle chat overlay" />
      </div>
      <iframe id="receiver" class="close" src="https://amelia.ipsoft.com/Amelia/ui/PNCdemo/?as=internal&embed=iframe&domainCode=pncdemo" frameborder="0" width="100%" height="100%" allow="geolocation; microphone; camera">
        <p>Your browser does not support iframes.</p>
      </iframe>
      <div class="chat-overlay-header">
        <img class="chat-overlay-header-img close" src="/close.png" alt="toggle chat overlay" />
        <img class="chat-overlay-header-img open" src="/icon.png" alt="toggle chat overlay" />
      </div>
  </div>
</div>
  <style>
.chat-overlay {
  position: fixed;
  width: 376px;
  height: 500px;
  bottom: 24px;
  right: 24px;
  z-index: 90;
}

body {
        background-image: url("pnc-background-image.png");
        background-size: 100%;
}

.chat-overlay-open {
    height: 512px;
}
 
.chat-overlay-closed {
    height: 78px;
 
}
 
.chat-overlay-wrapper {
  width: 376px;
  height: 448px;
}
 
.chat-overlay-header-mobile {
    display: none;
}
 
.chat-overlay-header {
  position: relative;
  height: 56px;
  width: 56px;
  border: 1px solid black;
  background: #000;
  margin-left: auto;
  border-radius: 50%;
  box-shadow: 1rem 1rem 5rem rgba(0, 0, 0, 0.5);
}
 
#receiver {
  transition: opacity 1s ease-in-out;
  opacity: 1;
  background: rgba(0, 0, 0, 0.5);
  box-shadow: 1rem 1rem 5rem rgba(0, 0, 0, 0.5);
  border-radius: 0.5rem;
}
 
#receiver.close {
  height: 0;
  opacity: 0;
  overflow: hidden;
}
 
#receiver.open {
  height: 100%;
  opacity: 1;
  overflow: hidden;
}
 
.chat-overlay-header-img {
  position: absolute;
  max-width: 14px;
  max-height: 14px;
  transition: opacity 1s ease-in-out;
  opacity: 1;
  right: 0px;
  left: 0px;
  top: 0px;
  bottom: 0px;
  margin: auto;
}
 
.chat-overlay-header-img.open {
  opacity: 0;
}
   
.absolute-cart-box {
  display: none;
}
 
@media only screen and (max-width: 768px) {
  .chat-overlay {
    width: 100%;
    position: fixed;
    height: 100%;
  }
 
  .chat-overlay-header-mobile {
    display: flex;
    width: inherit;
    height: 9%;
    background: #4d5aff;
  }
 
  .chat-overlay-header-mobile img {
    height: 30%;
    padding: 1rem;
    margin-left: auto;
  }
 
  .chat-overlay-header-mobile.close {
    display: none;
  }
 
  #receiver {
    border-radius: 0;
  }
 
  #receiver.close {
    height: 0;
    opacity: 0;
    overflow: hidden;
  }
 
  #receiver.open {
    height: 91%;
    opacity: 1;
    overflow: hidden;
  }
 
  .chat-overlay-open {
    height: 100%;
    bottom: 0px;
    right: 0px;
    }
 
  .chat-overlay-closed {
        height: 70px;
    bottom: 24px;
    right: 24px;
    }
 
  .chat-overlay-wrapper {
    width: 100%;
    height: 100%;
  }
}
</style>
 <script>
 
  function openChatOverlay (receiverElem, imgElemOpen, imgElemClose) {
    document.getElementById('receiver').classList.add("open");
    document.getElementById('receiver').classList.remove("close");
    document.getElementsByClassName('chat-overlay')[0].classList.add("chat-overlay-open");
    document.getElementsByClassName('chat-overlay')[0].classList.remove("chat-overlay-closed");
    document.getElementsByClassName('chat-overlay-header-mobile')[0].classList.remove('close');
    imgElemClose.style.opacity = 1;
    imgElemOpen.style.opacity = 0;
    localStorage.setItem('chatOverlayOpen', true);
  }
 
  function closeChatOverlay (receiverElem, imgElemOpen, imgElemClose) {
    document.getElementById('receiver').classList.add("close");
    document.getElementById('receiver').classList.remove("open");
    document.getElementsByClassName('chat-overlay')[0].classList.add("chat-overlay-closed");
    document.getElementsByClassName('chat-overlay')[0].classList.remove("chat-overlay-open");
    document.getElementsByClassName('chat-overlay-header-mobile')[0].classList.add('close');
    imgElemOpen.style.opacity = 1;
    imgElemClose.style.opacity = 0;
    localStorage.setItem('chatOverlayOpen', false);
  }
 
  function toggleChatOverlay () {
    /**
     * Toggles opening and closing of the chatOverlay
     * @returns - no return
     */
    var chatOverlayHeaderImgElemOpen = document.getElementsByClassName('chat-overlay-header-img open')[0];
    var chatOverlayHeaderImgElemClose = document.getElementsByClassName('chat-overlay-header-img close')[0];
    var receiverElem = document.getElementById('receiver');
    if (receiverElem.classList.contains('close')) {
      openChatOverlay(receiverElem, chatOverlayHeaderImgElemOpen, chatOverlayHeaderImgElemClose);
    } else {
      closeChatOverlay(receiverElem, chatOverlayHeaderImgElemOpen, chatOverlayHeaderImgElemClose);
    }
  }
 
  var chatOverlayHeaderElem = document.getElementsByClassName('chat-overlay-header')[0];
  chatOverlayHeaderElem.addEventListener('click', toggleChatOverlay);
  var chatOverlayHeaderElemMobile = document.getElementsByClassName('chat-overlay-header-mobile')[0];
  chatOverlayHeaderElemMobile.addEventListener('click', toggleChatOverlay);
 
   
   var isSafari = navigator.vendor && navigator.vendor.indexOf('Apple') > -1 &&
               navigator.userAgent &&
               navigator.userAgent.indexOf('CriOS') == -1 &&
               navigator.userAgent.indexOf('FxiOS') == -1;
   
   var ua = window.navigator.userAgent;
   var iOS = !!ua.match(/iPad/i) || !!ua.match(/iPhone/i);
   var webkit = !!ua.match(/WebKit/i);
   var iOSSafari = iOS && webkit && !ua.match(/CriOS/i);
 
  if (typeof(Storage) !== "undefined") {
    var chatOverlayOpen = localStorage.getItem('chatOverlayOpen');
    var chatOverlayDefaultStateClosed = true;
    var chatOverlayHeaderImgElemOpen = document.getElementsByClassName('chat-overlay-header-img open')[0];
    var chatOverlayHeaderImgElemClose = document.getElementsByClassName('chat-overlay-header-img close')[0];
    var receiverElem = document.getElementById('receiver');
    if (chatOverlayOpen && localStorage.getItem('chatOverlayOpen') !== "true" || (chatOverlayOpen === null && chatOverlayDefaultStateClosed)) {
      closeChatOverlay(receiverElem, chatOverlayHeaderImgElemOpen, chatOverlayHeaderImgElemClose);
    } else {
      openChatOverlay(receiverElem, chatOverlayHeaderImgElemOpen, chatOverlayHeaderImgElemClose);
    }
  } else {
      // Sorry! No Web Storage support..
    console.log('No localStorage support')
  }
   
//   (function() {
//     window.onload = function (e) {
//       var wnd = window.open("https://ipsoft-amelia-uiux-v3.ipsoft.com/Amelia/ui/releaseTesting/?embed=iframe&domainCode=Anonymous", "", "width=200,height=100");
//       console.log('------------------- im outside setTimeout', wnd);
//       setTimeout(function() {
//         console.log('------------------- im in setTimeout', wnd);
//         wnd.close();
//         document.getElementById('receiver').src = "https://ipsoft-amelia-uiux-v3.ipsoft.com/Amelia/ui/releaseTesting/?embed=iframe&domainCode=Anonymous";
//       }, 2000);
//       return false;
//     };
//   })();

   function getCookie(cname) {
    var name = cname + "=";
    var decodedCookie = decodeURIComponent(document.cookie);
    var ca = decodedCookie.split(';');
    for(var i = 0; i <ca.length; i++) {
      var c = ca[i];
      while (c.charAt(0) == ' ') {
        c = c.substring(1);
      }
      if (c.indexOf(name) == 0) {
        return c.substring(name.length, c.length);
      }
    }
    return false;
  }
   
  function setCookie(cname, cvalue, exdays) {
    var d = new Date();
    d.setTime(d.getTime() + (exdays*24*60*60*1000));
    var expires = "expires="+ d.toUTCString();
    document.cookie = cname + "=" + cvalue + ";" + expires + ";path=/";
  }
   
   if (isSafari || iOSSafari) {
      (function() {
        document.getElementsByClassName("chat-overlay-header")[0].onclick = function (e) {
          e.preventDefault();
          var ameliaChatOverlayCookie = getCookie('ameliaChatOverlay');
          if (!ameliaChatOverlayCookie) {
            var wnd = window.open("https://ipsoft-amelia-uiux-v3.ipsoft.com/Amelia/ui/releaseTesting/?embed=iframe&domainCode=Anonymous", "", "width=1,height=1");
            setTimeout(function() {
              wnd.close();
              document.getElementById('receiver').src = "https://ipsoft-amelia-uiux-v3.ipsoft.com/Amelia/ui/releaseTesting/?embed=iframe&domainCode=Anonymous";
            }, 3000);
            setCookie('ameliaChatOverlay', true, 3);
          }
          return false;
        };
      })();
   }
   
   //Chat Overlay drag and drop
      var dragItem = document.querySelector(".chat-overlay");
      var touchItem = document.querySelector(".chat-overlay-header-img.open");
      var chatOverlayWrapper = document.querySelector('.chat-overlay-wrapper');
      var container = document.querySelector("body");

      var active = false;
      var currentX;
      var currentY;
      var initialX;
      var initialY;
      var xOffset = 0;
      var yOffset = 0;

      container.addEventListener("touchstart", dragStart, false);
      container.addEventListener("touchend", dragEnd, false);
      container.addEventListener("touchmove", drag, false);

      container.addEventListener("mousedown", dragStart, false);
      container.addEventListener("mouseup", dragEnd, false);
      container.addEventListener("mousemove", drag, false);

      function dragStart(e) {
        dragged = false;
        if (e.type === "touchstart") {
          initialX = e.touches[0].clientX - xOffset;
          initialY = e.touches[0].clientY - yOffset;
        } else {
          initialX = e.clientX - xOffset;
          initialY = e.clientY - yOffset;
        }

        if (e.target === touchItem) {
          active = true;
        }
      }

      function dragEnd(e) {
        initialX = currentX;
        initialY = currentY;

        active = false;
        const bodyBound = document.body.getBoundingClientRect();
        const chatOverlayHeaderBound = document.getElementsByClassName('chat-overlay-header')[0].getBoundingClientRect();
        const center = {
          x: chatOverlayHeaderBound.x + chatOverlayHeaderBound.width/2,
          y: chatOverlayHeaderBound.y + chatOverlayHeaderBound.height/2
        };
        if(center.x < bodyBound.width/2 && center.y < bodyBound.height/2) {
          console.log('left side/ top side');
        } else if (center.x < bodyBound.width/2 && center.y > bodyBound.height/2) {
          console.log('left side/ bottom side');
        } else if (center.x > bodyBound.width/2 && center.y < bodyBound.height/2 ) {
          console.log('right side/ top side');
        } else {
          console.log('right side/ bottom side');
        }


        console.log('center', center);
      }

      function drag(e) {
        if (active) {
          e.preventDefault();

          dragged = true;
          if (e.type === "touchmove") {
            currentX = e.touches[0].clientX - initialX;
            currentY = e.touches[0].clientY - initialY;
          } else {
            currentX = e.clientX - initialX;
            currentY = e.clientY - initialY;
          }

          xOffset = currentX;
          yOffset = currentY;
          setTranslate(currentX, currentY, dragItem);
        }
      }

      function setTranslate(xPos, yPos, el) {
        el.style.transform = "translate3d(" + xPos + "px, " + yPos + "px, 0)";
      }
 
</script>
</body>
</html>
