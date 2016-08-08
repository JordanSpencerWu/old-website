---
layout: post
title: "Get Your Current Location With JavaScript"
date: 2016-07-09 12:15:00
categories: [blog]
---

The other day I downloaded a android game called Pokémon GO on my phone. I remember playing Pokémon back in the day when there was only 151 pokemons available to catch. I started playing this game and realized it was using my geolocation to find pokemons, gyms, and poke stops. It's crazy how technologies has change over a decade, I went from playing this game on my gameboy in elementary school to now playing it on my phone. The users will need to allow the game to have access to their location data for everything to work. In this blog I will talk about how to use JavaScript to get your current latitude and longitude location.  

Most of the devices that have access to the internet are capable of getting it's location using GPS, WiFi, or IP geolocation. This allows developers to implement all kinds of useful map interactions in apps and websites. JavaScript has a powerful api called <a href="https://developer.mozilla.org/en-US/docs/Web/API/Geolocation" target="_blank">Geolocation API</a>, this api uses the methods above to get your geo data.

#### Getting Started with Geolocation API

The Geolocation API is full cross-browser which means that all browsers has this API. You can check if the geolocation object exists by checking `Window.naviagor`. It's best practice to check for this object by running the code below:

{% highlight javascript %}
  if (naviagor.geolocation) {
    // geolocation is available
  }
  else {
    // gelocation is not supported
  }
{% endhighlight %}

Looking at the Geolocation API, there are a few methods that can be used to get gelocation data:

`Geolocation.getCurrentPosition()` - Finds the device's current location and gives back a `Position` object with the data.

`Geolocation.watchPosition()` - Listens for changes in the location and invokes a callback on every movement.

`Geolocation.clearWatch()` - Removes a `watchPosition` event handler.

Both the `getCurrentPosition()` and `watchPosition()` methods work asynchronously, trying to get the device position and depending on the outcome of the attempt calls a success callback or an error callback. This following code shows you how to implement the `getCurrentPosition()` methods with the two different callbacks:

{% highlight javascript %}
  if (naviagor.geolocation) {
    navigator.gelocation.getCurrentPosition(
      // Success callback
      function(position) {
        /*
        position = {
            coords: {
                latitude - Geographical latitude in decimal degrees.
                longitude - Geographical longitude in decimal degrees. 
                altitude - Height in meters relative to sea level.
                accuracy - Possible error margin for the coordinates in meters. 
                altitudeAccuracy - Possible error margin for the altitude in meters. 
                heading - The direction of the device in degrees relative to north. 
                speed - The velocity of the device in meters per second.
            }
            timestamp - The time at which the location was retrieved.
        }
        */
      },
      // Optional error callback
      function(error) {
          /* 
          In the error object is stored the reason for the failed attempt:

          error = {
              code - Error code representing the type of error 
                      1 - PERMISSION_DENIED
                      2 - POSITION_UNAVAILABLE
                      3 - TIMEOUT

              message - Details about the error in human-readable format.
          }
          */
      }
    );
  }
  else {
    // gelocation is not supported
  }
{% endhighlight %}

The `getCurrentPosition()` is easy to use and provides many useful information, when it is successful it passes the `Position` object as an argument into the success callback which allows you to use this object in the function, otherwise it will pass an `Error` object to the error callback. Now you can use the device's geolocation to do something useful!!

#### User Permission

Getting geolocation data is personal information and requires permission. When applications tries to access personal information for the first time, a dialog usually pops up requesting permission. This is similar to many phone apps which needs permission like location, camera, email, etc.

#### Using Google Maps API

Once we have the geolocation data we can use <a href="https://developers.google.com/maps/" target="_blank">Google Maps API</a> to display your current location. When using this api you will need a access key that allows you access to the api, once you get your api key remember to enable the google maps api. I'm going to be using <a href="https://hpneo.github.io/gmaps/" target="_blank">Gmaps.js</a>, this allows me to use Google Maps with less code. Now for a demonstration click the button below to find your current location!!

<button type="button" class="find-me btn btn-info btn-block" style="margin: 0 auto;">Find My Location</button>

<div id="map" style="height:50vh;width:100%;"></div>

#### Conclusion

The Pokémon GO game is watching your position which is similar to the `watchPosition()` method in the Geolocation API. Beware that watching your position using GPS or WiFi consumes your battery power at a faster rate. This bring back memory from when I played Pokémon on my gameboy, I still remember my first lvl 100 pokémon was Nidoking, well time to find a Nidoran in Pokémon GO!

<script src="https://maps.google.com/maps/api/js?key=AIzaSyAZhjK4Uio-T1ZkADdweo1uxHC9jRUYEM0"></script>
<script>
  function displayLocation(position) {
    var map = new GMaps({
      el: '#map',
      lat: position.coords.latitude,
      lng: position.coords.longitude
    });

    map.addMarker({
      lat: position.coords.latitude,
      lng: position.coords.longitude
    });
  }

  function displayError(error) {
    var errors = ["Unknown error", "Permission denied by user", "Position not available", "Timeout error"];
    var message = errors[error.code];
    console.warn("Error in getting your location: " + message, error.message);
  }

  window.onload = function() {
    var findMeButton = $('.find-me');
    var map = $('#map');
    map.hide();
    if (navigator.geolocation) {
      findMeButton.on('click', function(e) {
        navigator.geolocation.getCurrentPosition(displayLocation, displayError);
        map.show();
      });
    } else {
      alert("Sorry, this browser doesn't support geolocation!");
    }
    
  }
</script>