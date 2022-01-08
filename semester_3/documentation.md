---
layout: page
title: Projekto planavimas
permalink: /semester_3/documentation/
---

<body>
<style>
    
.button {
  transition-duration: 0.4s;
  display: inline-block;
  padding: 10px 15px;
  cursor: pointer;
  text-align: center;
  text-decoration: none;
  outline: none;
  color: #fff;
  background-color: grey;
  border: none;
  border-radius: 15px;
  box-shadow: 0 9px #999;
}

.button:hover {
  background-color: #1C2833; /* Green */
  color: white;
}
</style>
<div id="loginbox" style="text-align:center" >
        Slaptažodis<br />
        <input style="margin: 16px; text-align: center;" id="password" type="password" placeholder="password" /> <br />
        <p id="wrongPassword" style="display: none;color: red;font-weight: bold;">*Netinkamas slaptažodis</p>
        <button class="button" id="loginbutton" type="button">Enter/Patvirtinti</button>
	</div>

<script type="text/javascript" src="https://code.jquery.com/jquery-1.12.0.min.js"></script>

<script src="https://cdnjs.cloudflare.com/ajax/libs/jsSHA/2.0.2/sha.js"></script>

<script type="text/javascript">
"use strict";

function loadPage(pwd) {

    var hashM = new jsSHA("SHA-512","TEXT", {numRounds: 1});
    hashM.update(pwd);
    var hash = hashM.getHash("HEX");
    var url= hash + "";
    var originUrl="";

    $.ajax({
        url : url,
        dataType : "html",
        success : function(data) {

            window.location= url;

        },
        error : function(xhr, ajaxOptions, thrownError) {

            alert("Netinkamas slaptažodis; Incorect password;");
            window.location=originUrl;
            parent.location.hash= hash;
            $("#password").attr("placeholder","wrong password");
            $("#password").val("");
        }
    });
}


$("#loginbutton").on("click", function() {
    loadPage($("#password").val());
});
$("#password").keypress(function(e) {
    if (e.which == 13) {

        loadPage($("#password").val());
    }
});
$("#password").focus();

</script>
</body>