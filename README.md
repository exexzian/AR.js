# AR.js - Augmented Reality on the Web

<img src="https://github.com/jeromeetienne/AR.js/blob/master/AR.js-1920-1080-HD.png?raw=true" height="200" />

Logo by [Simon Poulter](https://twitter.com/viralinfo)

---


[![Build Status](https://travis-ci.org/jeromeetienne/AR.js.svg?branch=master)](https://travis-ci.org/jeromeetienne/AR.js)
[![Gitter chat](https://badges.gitter.im/AR-js/Lobby.png)](https://gitter.im/AR-js/Lobby)
[![Twitter Follow](https://img.shields.io/twitter/follow/nicolocarp.svg?style=plastic&label=nicolocarpignoli-twitter&style=plastic)](https://twitter.com/nicolocarp)
[![Twitter Follow](https://img.shields.io/twitter/follow/jerome_etienne.svg?style=plastic&label=jeromeetienne-twitter&style=plastic)](https://twitter.com/jerome_etienne)

AR.js is a lightweight library for Augmented Reality on the Web, coming with features like Image Tracking, Location based AR and Marker tracking.

Welcome to the official repository!

This project has been created by [@jeromeetienne](https://github.com/jeromeetienne) and it is now maintained by [@nicolocarpignoli](https://github.com/nicolocarpignoli).

🚀For frequent updates on AR.js you can follow [@nicolocarp](https://twitter.com/nicolocarp) and Watch this repo!

**Key points**:

- **Very Fast** : It runs efficiently even on phones - [60 fps on my 2 year-old phone](https://twitter.com/jerome_etienne/status/831333879810236421)!
- **Web-based** : It is a pure web solution, so no installation required. Full javascript based on three.js + jsartoolkit5
- **Open Source** : It is completely open source and free of charge!
- **Standards** : It works on any phone with [webgl](http://caniuse.com/#feat=webgl) and [webrtc](http://caniuse.com/#feat=stream)
- **Features** : It features Image Tracking, Location Based AR and Marker Tracking.

## ⚠️ AR.js is coming in two, different build. They are both maintained. They are exclusive.

Please import the one you need for your project, not both:

- **AR.js with Image Tracking + Location Based AR:**

  - AFRAME version: https://raw.githack.com/AR-js-org/AR.js/master/aframe/build/aframe-ar-nft.js

  - three.js version: https://raw.githack.com/AR-js-org/AR.js/master/three.js/build/ar-nft.js

- **AR.js with Marker Tracking + Location Based AR:**
  - AFRAME version: https://raw.githack.com/AR-js-org/AR.js/master/aframe/build/aframe-ar.js

  - three.js version: https://raw.githack.com/AR-js-org/AR.js/master/three.js/build/ar.js

## Get started

### 🖼 **Image Tracking**

// TODO add gif of trex

Run the following code and scan [this picture](https://raw.githack.com/AR-js-org/AR.js/master/aframe/examples/image-tracking/nft/trex-image.jpg) to see content over it.

```html
<script src='https://cdn.jsdelivr.net/gh/aframevr/aframe@1c2407b26c61958baa93967b5412487cd94b290b/dist/aframe-master.min.js'></script>

<script src='https://raw.githack.com/AR-js-org/AR.js/master/aframe/build/aframe-ar-nft.js'></script>

<style>
    .arjs-loader {
        height: 100%;
        width: 100%;
        position: absolute;
        top: 0;
        left: 0;
        background-color: rgba(0, 0, 0, 0.8);
        z-index: 9999;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .arjs-loader div {
        text-align: center;
        font-size: 1.25em;
        color: white;
    }
</style>

<body style='margin : 0px; overflow: hidden;'>
  <!-- minimal loader shown until image descriptors are loaded -->
    <div class="arjs-loader">
        <div>Loading, please wait...</div>
    </div>
    <a-scene
      vr-mode-ui="enabled: false;"
      renderer='logarithmicDepthBuffer: true;'
      embedded arjs='trackingMethod: best; sourceType: webcam;debugUIEnabled: false;'>

      <!-- we use cors-anywhere proxy to avoid cross-origin problems -->
      <a-nft
        type='nft'
        url='https://cors-anywhere.herokuapp.com/https:/raw.githack.com/AR-js-org/AR.js/master/afram/examples/image-tracking/nft/trex/trex-image/trex' smooth='true' smoothCount='10'
        smoothTolerance='.01'
        smoothThreshold='5'>
          <a-entity
            gltf-model='https://cors-anywhere.herokuapp.com/https://raw.githack.com/AR-js-org/AR.js/master/aframe/examples/image-tracking/nft/trex/scene.gltf' scale="5 5 5"
            position="50 150 0"
          >
          </a-entity>
        </a-nft>
		  <a-entity camera></a-entity>
    </a-scene>
</body>
```

### 🌍Location Based

<img height="569" width="320" src="https://github.com/nicolocarpignoli/GeoAR.js/blob/master/docs/click-places.gif?raw=true">

<img height="569" width="320" src="https://github.com/nicolocarpignoli/GeoAR.js/blob/master/docs/places-name.gif?raw=true">

Try the following snippet, and instead of `add-your-latitude` and `add-your-longitude` add the required values, without the `<>`.
Activate GPS on your phone and run the example. Look around. You should see the text looking at you, appearing in the requested position, even if you look around and move.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <title>GeoAR.js demo</title>
    <script src="https://cdn.jsdelivr.net/gh/aframevr/aframe@1c2407b26c61958baa93967b5412487cd94b290b/dist/aframe-master.min.js"></script>
    <script src="https://unpkg.com/aframe-look-at-component@0.8.0/dist/aframe-look-at-component.min.js"></script>
    <script src="https://rawcdn.githack.com/AR-js-org/AR.js/a5619a021e6ff40427ff8f9c62169e99a390f56b/aframe/build/aframe-ar-nft.min.js"></script>
    <!-- <script src="https://raw.githack.com/jeromeetienne/AR.js/3.0.0/aframe/build/aframe-ar-nft.min.js"></script> -->

    <!-- <script>ARjs.Context.baseURL = '../../../../../three.js/'</script> -->
  </head>

  <body style="margin: 0; overflow: hidden;">
    <a-scene
      vr-mode-ui="enabled: false"
      embedded
      arjs="sourceType: webcam; debugUIEnabled: false;"
    >
      <a-text
        value="This content will always face the user."
        look-at="[gps-camera]"
        scale="120 120 120"
        gps-entity-place="latitude: <add-your-latitude>; longitude: <add-your-longitude>;"
      ></a-text>
      <a-camera gps-camera rotation-reader> </a-camera>
    </a-scene>
  </body>
</html>
```

### Marker tracking

Scan [this marker](https://rawcdn.githack.com/AR-js-org/AR.js/a5619a021e6ff40427ff8f9c62169e99a390f56b/data/images/hiro.png) to see the content over it.

```html
<!DOCTYPE html>
<html>
  <script src="https://aframe.io/releases/1.0.0/aframe.min.js"></script>
  <!-- <script src="https://raw.githack.com/jeromeetienne/AR.js/3.0.0/aframe/build/aframe-ar.js"></script> -->
  <script src="https://raw.githack.com/jeromeetienne/AR.js/2.2.2/aframe/build/aframe-ar.min.js"></script>
  <body style="margin : 0px; overflow: hidden;">
    <a-scene embedded arjs>
      <a-marker preset="hiro">
        <a-entity position="0 0.5 0" gltf-model="https://rawcdn.githack.com/nicolocarpignoli/nicolocarpignoli.github.io/0c3112919b0f27ef508bf1d9e354adf15c0a94d7/roma/models/scene.gltf"></a-entity>
      </a-marker>
      <a-entity camera></a-entity>
    </a-scene>
  </body>
</html>
```


# Index
* [Image Tracking documentation](./ImageTracking.md)
* [Location Based documentation](./aframe/LocationBased.md)
* [Marker Tracking documentation](./aframe/MarkerTracking.md)
* [Browser Support](#Browser-Support)
* [Licenses](#Licenses)
* [Learn more](#Learn-More)

**You can find a lot of help on the old AR.js repositories issues. Please search on open/closed issues, you may find a interesting stuff.**

⚠️ *Please always give a look for new undocumented features on the [Changelog](https://github.com/jeromeetienne/AR.js/blob/master/CHANGELOG.md) until the documentation has been updated.*


# Browser Support

Demo tested on the following browser setups:

- **Desktop Chrome with webcam and 2 tabs** (one for Hero, one for result) (works!)
- **Android native 4.4.2** (doesn't work, doesn't ask for permission to use camera. I see white background and text)
- **Android native 5.0** (doesn't work, doesn't ask for permission, I see white background and text)
- **Chrome on Android 4.4.2** (works!)
- **Chrome on Android 5.0** (doesn't work, asks for permission, I see black background, text and a chart)
- **Safari and Chrome on iOS < 11** (doesn't work, doesn't ask for permission, I see white background and text)
- **Microsoft Edge on Windows 10** (Chrome on Google Pixel phone to view hologram)

To see the full compatibility list and contribute to it yourself go to this google spreadsheet:
[AR.js platform and browser compatibility](https://docs.google.com/spreadsheets/d/1e5YimbF_D1Sou2bx2vdBH58s1WdB_LgzBVYYD_uQLJk/edit#gid=318398375)

Credits: @HelloDeadline, @sorianog

# Licenses

It is **all open source**! jsartoolkit5 is under LGPLv3 license and additional permission.
And All my code in AR.js repository is under MIT license. :)

For legal details, be sure to check [jsartoolkit5 license](https://github.com/artoolkit/jsartoolkit5/blob/master/LICENSE.txt)
and [AR.js license](https://github.com/jeromeetienne/AR.js/blob/master/LICENSE.txt).

# Learn More

- [AR.js changelog](https://github.com/jeromeetienne/AR.js/blob/master/CHANGELOG.md)

- [Future plans](https://trello.com/b/63F7JlvD/arjs)

- [FAQ](https://jeromeetienne.github.io/AR.js-docs/misc/FAQ.html)

- [How to Release](https://github.com/jeromeetienne/AR.js/blob/master/HOW_TO_RELEASE.md)



//////////// TO MOVE ////////////
# What "Marker Based" means
AR.js uses `artoolkit`, and so it is marker based.
`artoolkit` is a software with years of experience doing augmented reality. It is able to do a lot!

It supports a wide range of markers: multiple types of markers [pattern](https://github.com/artoolkit/artoolkit5/tree/master/doc/patterns)/[barcode](https://github.com/artoolkit/artoolkit-docs/blob/master/3_Marker_Training/marker_barcode.md)
multiple independent markers at the same time, or [multiple markers acting as a single marker](https://github.com/artoolkit/artoolkit-docs/blob/master/3_Marker_Training/marker_multi.md) up to you to choose.

More details about markers:

* [Artoolkit Open Doc](https://github.com/artoolkit/artoolkit-docs/tree/master/3_Marker_Training)
* [Detailed Article about markers](https://medium.com/@nicolcarpignoli/ar-js-the-simplest-way-to-get-cross-browser-augmented-reality-on-the-web-10cbc721debc) by [@nicolocarpignoli](https://twitter.com/nicolocarp)

# What "Location Based" means

### Check out the Location Based documentation: [here](https://github.com/jeromeetienne/AR.js/blob/master/aframe/README.md#location-based).

AR.js, on its `aframe` implementation, comes with few custom components that make possible to integrate data from GPS sensors.

Basically, you can add `gps-entity-place` - custom `aframe` entities that have a specific longitude/latitude values.

You can add them with a script, loading them from APIs (Foursquare, Google Maps, and so on) or just add them statically on your HTML.

Once you have added one or more gps-entities, and added the `gps-camera` on the `camera` entity, the system calculates, at every frame, your position and the distance of places from you.

Using your phone sensors for orientation/position, AR.js is able to show on your camera a content for each place on its 'physical' place (so if you point the camera towards the place in real life, you will see the content near it).

If you move the camera, it calculates again orientation and position. If places are far, it shows smaller content. If places are near you, it shows it bigger.

Learn more with [this article](https://medium.com/@nicolcarpignoli/location-based-gps-augmented-reality-on-the-web-7a540c515b3c).

🌍Click on the examples below to try it out.
📲Open from mobile phone with GPS data enabled.

- [Click Places](https://nicolo-carpignoli.herokuapp.com/examples/basic.html)

    Show place icon for every place. Clicking on the icon will show the place name.

    <img height="569" width="320" src="https://github.com/nicolocarpignoli/GeoAR.js/blob/master/docs/click-places.gif?raw=true">

- [Places Name](https://nicolo-carpignoli.herokuapp.com/examples/places-name)

    Show icon and place name above. Clicking on places will redirect to a certain URL (now mocked up).

  <img height="569" width="320" src="https://github.com/nicolocarpignoli/GeoAR.js/blob/master/docs/places-name.gif?raw=true">

Every example uses the `places.js` script to load places. You set your places using static data, with specific coordinates, adding these info in the first lines of code (there are comments to explain it better).

Otherwise, as default, the script searches for places of interest near the user using Foursquare APIs. Please retrieve valid API credentials [here](https://developer.foursquare.com/) in order to use it. Place credentials (replace both Client Secret and Client Id) on `places.js`.

You can also use GeoAR.js **without** the script, adding `gps-entity-place` entities directly on the `index.html` file.as documentated [here](https://github.com/jeromeetienne/AR.js/blob/master/aframe/README.md).





See on [codepen](https://codepen.io/nicolocarpignoli/pen/vMBgob)

A-Frame magic :) All details are explained in this super post
["Augmented Reality in 10 Lines of HTML - AR.js with a-frame magic"](https://medium.com/arjs/augmented-reality-in-10-lines-of-html-4e193ea9fdbf)
by
[@AndraConnect](https://twitter.com/AndraConnect).

## Guides for beginners

### Marker Based

- [AR.js introduction and insight on markers](https://medium.com/@nicolcarpignoli/ar-js-the-simplest-way-to-get-cross-browser-augmented-reality-on-the-web-10cbc721debc)
- [Details about 3D models that can be used with AR.js](https://medium.com/@akashkuttappa/using-3d-models-with-ar-js-and-a-frame-84d462efe498)
- ["WebVR for Augmented Reality - Using WebVR to write cross-platform AR applications"](https://medium.com/arjs/webvr-for-augmented-reality-f1e69a505902)
  by [@jerome_etienne](https://twitter.com/jerome_etienne)
- ["AR-Code:a Fast Path to Augmented Reality - From QR Code to AR.js content"](https://medium.com/arjs/ar-code-a-fast-path-to-augmented-reality-60e51be3cbdf)
  by [@jerome_etienne](https://twitter.com/jerome_etienne)

### Location Based

- [Location Based (GPS) Augmented Reality on the Web](https://medium.com/@nicolcarpignoli/location-based-gps-augmented-reality-on-the-web-7a540c515b3c)
- [Tutorial for Location Based Augmented Reality on the Web](https://medium.com/chialab-open-source/build-your-location-based-augmented-reality-web-app-c2442e716564)

## Advanced guides

### Marker Based

- [How to deliver AR.js only with a QR Code](https://medium.com/@nicolcarpignoli/how-to-deliver-ar-on-the-web-only-with-a-qr-code-139bb90e82f1)
- [How to handle click with AR.js](https://medium.com/@nicolcarpignoli/how-to-handle-click-events-on-ar-js-f397ea5994d)
- [10 tips to enhance your AR.js app performances](https://medium.com/@nicolcarpignoli/10-tips-to-enhance-your-ar-js-app-8b44c6faffca)
- ["Area Learning with Multi-Markers in AR.js - For a Larger & More Stable Augmented Reality"](https://medium.com/arjs/area-learning-with-multi-markers-in-ar-js-1ff03a2f9fbe)
  by [@AndraConnect](https://twitter.com/AndraConnect)
- Great post about [WebAR for designer](http://www.nexusinteractivearts.com/webar/)
  by [nexus interactive arts](http://www.nexusinteractivearts.com/)

# Examples

Try to get inspired by this great works:

### Marker Based

- [Examples from official AR.js doc](https://jeromeetienne.github.io/AR.js-docs/misc/EXAMPLES.html)

### Location Based

- [Click Places](./aframe/examples/click-places) - set up remote credentials to fetch remote places (`places.js` file)
- [Places Name](./aframe/examples/places-name) - add new places statically on javascript (`places.js` file)
- [Only HTML](./aframe/examples/only-html) - add new places statically on html (`index.html` file)
- [Only HTML](./aframe/examples/always-face-user) - like only-html but here content always face the user (`index.html` file)

# Related Projects

- [Examples inspired from AR.js - not AR.js based](https://github.com/stemkoski/AR-Examples) from [@stemkoski](https://github.com/stemkoski)
- [AR-gif](https://github.com/rodrigocam/ar-gif):
  Easy to use web components to do web augmented reality. Currently supporting gifs, but open for contributions to
  add 3d objects, videos and so on.

## Augmented Website

[Seminal post](https://medium.com/arjs/augmenting-the-web-page-e893f2d199b8) explaining the concept.
The service is available [webxr.io/augmented-website](https://webxr.io/augmented-website/)

# Community

- AR.js on gitter: https://gitter.im/AR-js/Lobby
- Trello board for ongoing work: https://trello.com/b/63F7JlvD/arjs

# Tools

- [Pattern Marker Generator](https://jeromeetienne.github.io/AR.js/three.js/examples/marker-training/examples/generator.html):
  Generate a pattern marker with your own image.
- [ARCode Generator](https://jeromeetienne.github.io/AR.js/three.js/examples/arcode.html):
  Generator of AR-Code
  ([source](https://github.com/jeromeetienne/AR.js/blob/master/three.js/examples/arcode.html))

# Performance

We are still early in the project but here are some initial numbers to give you an idea.

- I got 60fps stable on nexus6p
- Some reports [Sony Xperia Z2 (2.5 years old) runs around 50fps](https://twitter.com/leinadkalpot/status/834121238087925763) - this is a 170euro phone
- Some reports [~50fps on a old nexus5, and ~60fps on nexus 9](https://twitter.com/Ellyll/status/834312442926751744) - nexus5 is 3.5 years old!
- Some reports it working on windows phone edge!! [13fps on Lumia 950](https://twitter.com/leinadkalpot/status/834299384510763012) for some.
  [40-45fps on lumia 930](https://twitter.com/fastclemmy/status/834817155665391616) for others.

Obviously you mileage may vary. The performance you get will depend on 3 things: How heavy your 3D is, How you tune your parameters
and the hardware that you are using.

# Standing on the Shoulders of Giants

So we shown it is now possible to do 60fps web-based augmented reality on a phone.
This is great for sure but how did we get here ? **By standing on the shoulders of giants!**
It is thanks to the hard work from others, that we can today reach this mythic 60fps AR.
So I would like to thanks :

- **three.js** for being a great library to do 3d on the web.
- **artoolkit**! years of development and experiences on doing augmented reality
- **emscripten and asm.js**! thus we could compile artoolkit c into javascript
- **chromium**! thanks for being so fast!

Only thanks to all of them, I could do my part : Optimizing performance from 5fps on high-end
phone, to 60fps on 2years old phone.

After all this work done by a lot of people, we have a _web-based augmented reality solution fast enough for mobile_!

Now, many people got a phone powerful enough to do web AR in their pocket.
I think this performance improvement makes web AR a reality.
i am all exited by what people are gonna with it :)

![screenshot](https://cloud.githubusercontent.com/assets/252962/23068128/40343608-f51a-11e6-8cb3-900e37a7f658.jpg)

## What’s New?

Recently, we’ve been getting creative and working on developing new things with AR.js. One of them is playing around with [shadows](https://twitter.com/jerome_etienne/status/837240034847764480), syncing the position of virtual lights with reality for a more life-like finish:
![screen shot 2017-03-16 at 21 06 24](https://cloud.githubusercontent.com/assets/6317076/24018623/7f787ba8-0a8c-11e7-8088-fea4799b5d09.png)

We’ve been collaborating very closely with [Fredrick Blomqvist](https://twitter.com/snigelpaogat). His input has had a great impact on AR.js innovation and we want to thank him. Together, we’ve been implementing [refraction](https://twitter.com/jerome_etienne/status/838749280999518208), giving the 3d a transparent/glassy effect. It ended up having a nice polished look. What do you guys think?

![screen shot 2017-03-06 at 16 31 28](https://cloud.githubusercontent.com/assets/6317076/23832948/9b64c79e-0736-11e7-9cb8-747f6a8fc082.png)

Other crazy ideas we’ve been working on include a [hole in the wall](https://twitter.com/jerome_etienne/status/836754117964017664) and a [portal into another world](https://twitter.com/jerome_etienne/status/838404908235776000). We want to take AR.js to new dimensions.

![screen shot 2017-03-12 at 15 19 51](https://cloud.githubusercontent.com/assets/6317076/23833024/b2e045be-0737-11e7-9ef0-8e1ac9e49ba8.png)
![screen shot 2017-03-07 at 10 08 39](https://cloud.githubusercontent.com/assets/6317076/23833015/947f6abe-0737-11e7-9a0d-1ea919f6ffbe.png)

# Status

- At the three.js level is the main one. It is working well and efficiently
- a-frame component - it export `<a-marker>` tag. It becomes real easy to use.
  It allows the things three.js extension does. Here are some slides
  [aframe-artoolkit](http://jeromeetienne.github.io/slides/artoolkit-aframe/)
- webvr-polyfill: it is kind of working - still a work-in-progress

# Folders

- `/three.js` is the extension to use it with [pure three.js](https://threejs.org)
- `/aframe` is the extension to use it with [a-frame](https://aframe.io)
- `/webvr-polyfill` is the WebVR polyfill so you can reuse your #AR / #VR content easily

# What's Next ?

We did good on performance, but there are still a lot of room for optimisation.
Using [webworkers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers)
would increase cpu usage. Compiling in [webassembly](https://webassembly.org) instead
of [asm.js](http://asmjs.org/) should improve loading time and likely cpu performance.
And obviously, we can still do more parameters tweaking :)

I would like people start experience augmented reality and play with it.
This is highly creative! Just look at this [puzzle game in #AR playing with mirror and laser beam](https://www.youtube.com/watch?v=OzLJb7HitvA).
You could do it with AR.js, so opensource and running on normal phones, no need to buy a new device. isn't that great!

Augmented reality on phone have applications in many fields:
[history education](https://www.youtube.com/watch?v=gyp8ZYtyu_M)
, [science](https://www.youtube.com/watch?v=gMxdBdLpVgc)
or [gaming](https://www.youtube.com/watch?v=kEMDgvfFUcI).
I exited to see what people will do with AR.js :)
