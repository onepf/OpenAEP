Summary
-------------

Open Application Exchange Protocol (OpenAEP) is designed to simplify deals when one appstore (source appstore) licenses its catalog of applications to another appstore (distributor appstore) for distribution. It is an HTTP REST based protocol with XML based result format. [AppDF](http://www.onepf.org/appdf) is used an an application description format.

Functions 
-------------
OpenAEP consists of five HTTP(s) based functions:

<table>
  <tr>
    <th>Function name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>App list</td>
    <td>List of all applications sorted by last update date with brief information about each (package, version, last update, etc)</td>
  </tr>
  <tr>
    <td>App description</td>
    <td>Detailed information about the given app(s) in AppDF format</td>
  </tr>
  <tr>
    <td>App reviews</td>
    <td>User review information about the given app(s)</td>
  </tr>
  <tr>
    <td>Downloads</td>
    <td>List of all app downloads with detailed information about each download provided by the distributor appstore</td>
  </tr>
  <tr>
    <td>Purchases</td>
    <td>List of all app purchases with detailed information about each purchase provided by the distributor appstore</td>
  </tr>
</table>

Sample
-------------

### App List
Request:
```
https://www.sourceappstore.com/openaep/applist
```

Response:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<application-list version="1" platform="android" last-updated="20130228T000000">
  <application package="com.softspb.flashcards.sv" version="1.3.1" build="81" last-updated="20130225T235959" last-review="20130227T110425">
  <application package="ru.yandex.shell" version="2.11" build="1765" last-updated="20130220T183142" last-review="20130110T202020">
</application-list>
```
 
### App Description
Request:
```
https://www.sourceappstore.com/openaep/appdescription?package=com.mxtech.videoplayer.ad,com.softspb.geo_game
```

Response:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<application-description-file version="1">
  <application platform="android" package="com.mxtech.videoplayer.ad">
    <categorization>
      <type>application</type>
      <category>Video</category>
      <subcategory></subcategory>
    </categorization>
    <description>
      <texts>
        <title>MX Player</title>
        <keywords>video, player, movie, media, play</keywords>
        <short-description>MX Player - The best way to enjoy your movies.</short-description>
        <full-description>
MX Player - The best way to enjoy your movies.
a) HARDWARE DECODING - With new h/w decoder, more videos can take benefit from hardware acceleration.
b) MULTI-CORE DECODING - MX Player is the first Android video player that performs multi-core decoding. According to the test results on dual-core devices, it shows up to 70% performance improvement than single-core devices.
c) PINCH TO ZOOM - Easily zoom in and out by pinching and swiping across screen.
d) SUBTITLE SCROLL - Scroll on subtitle text and playback position will be adjusted to match previous or next subtitle timing.
e) KIDS LOCK - Keep your kids entertained without having to worry about making calls or touching other apps. (plugin required)
f) ANDROID 4.1 - Fully supports Android 4.1 Jelly Bean.
        </full-description>
      </texts>
      <images>
        <app-icon width="512" height="512">appicon.png</app-icon>
        <large-promo width="1024" height="500">promo.png</large-promo>
        <screenshots>
            <screenshot width="480" height="800" index="1">screenshot01_en.png</screenshot>
            <screenshot width="480" height="800" index="2">screenshot02_en.png</screenshot>
            <screenshot width="480" height="800" index="3">screenshot03_en.png</screenshot>
            <screenshot width="480" height="800" index="4">screenshot04_en.png</screenshot>
            <screenshot width="480" height="800" index="5">screenshot05_en.png</screenshot>
        </screenshots>
      </images>
    </description>
    <price free="yes">
    </price>
    <apk-files>
     <apk-file>mxplayer.apk</apk-file>
    </apk-files>
    <customer-support>
      <phone>+1 (555) 1234-56-78</phone>
      <email>mxtechs.hq@gmail.com</email>
      <website>https://sites.google.com/site/mxvpen/</website>
    </customer-support>
  </application>
  <application platform="android" package="com.softspb.geo_game">
    <categorization>
      <type>game</type>
      <category>Trivia</category>
      <subcategory></subcategory>
    </categorization>
    <description>
      <texts>
        <title>SPB Geo Game</title>
        <keywords>spb, game, geo, world, capital, flag, country, trivia</keywords>
        <short-description>With SPB Geo Game you can study national capitals and flags.</short-description>
        <full-description>
With SPB Geo Game you can study national capitals and flags.
Features:
* World Flags<
* World Capitals
* 3D Globe
* Educational Animation
        </full-description>
        </texts>
      <images>
        <app-icon width="512" height="512">appicon.png</app-icon>
        <screenshots>
          <screenshot width="480" height="800" index="1">geogamead_ss1.png</screenshot>
          <screenshot width="480" height="800" index="2">geogamead_ss2.png</screenshot>
          <screenshot width="480" height="800" index="3">geogamead_ss3.png</screenshot>
          <screenshot width="480" height="800" index="4">geogamead_ss4.png</screenshot>
          <screenshot width="480" height="800" index="5">geogamead_ss5.png</screenshot>
          <screenshot width="480" height="800" index="6">geogamead_ss6.png</screenshot>
          <screenshot width="480" height="800" index="7">geogamead_ss7.png</screenshot>
          <screenshot width="480" height="800" index="8">geogamead_ss8.png</screenshot>
        </screenshots>
      </images>
      <videos>
       <youtube-video>WAyMMGOqXDE</youtube-video>
      </videos>
    </description>
    <description-localization language="fr">
      <texts>
        <title>SPB Geo Game</title>
        <keywords>spb, géo, le gibier, les pays, les capitales, drapeaux, trivia</keywords>
        <short-description>Avec le jeu SPB Geo vous pouvez étudier les capitales et les drapeaux.</short-description>
        <full-description>
Avec le jeu SPB Geo vous pouvez étudier les capitales et les drapeaux.
* Drapeaux du monde
* Capitales du monde
* Globe 3d
* Animation éducative
        </full-description>
      </texts>
    </description-localization>
    <price free="no">
      <base-price>0.99</base-price>
    </price>
    <apk-files>
      <apk-file>SPBGeoGame.apk</apk-file>
    </apk-files>
    <customer-support>
      <phone>+7 (812) 3356993</phone>
      <email>support@spband.yandex.ru</email>
      <website>http://www.yandex.ru</website>
    </customer-support>
  </application>
</application-description-file>
```
 
### App Reviews
Request:
```
https://www.sourceappstore.com/openaep/appreviews?package=com.softspb.flashcards.sv,com.softspb.geo_game
```

Response:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<review-list version="1" last-updated="20130228T000000">
  <application-reviews package="com.softspb.flashcards.sv" last-updated="20130225T235959-00">
    <review>
      <version>1.3.1</version>
      <build>81</build>
      <last-updated>20130227T110425</last-updated>
      <stars>4</stars>
      <user-name>Bill White</user-name>
      <user-url>https://plus.google.com/108973876811926673453/posts</user-url>
      <device-model>SHW-M130K</device-model>
      <device-name>Samsung GT-i9082</device-name>
      <country>US</country>
      <title>Greate to learn language</title>
      <text>Just perfect as it was since Win Mobile times</text>
      <useful>-2</useful>
    </review>
    <review>
      <version>1.3.1</version>
      <build>81</build>
      <last-updated>20130227T110425</last-updated>
      <stars>5</stars>
      <device-model>SHW-M130K</device-model>
      <device-name>Samsung GT-i9082</device-name>
      <country>US</country>
    </review>
  </application-reviews>
    <application-reviews package="com.softspb.geo_game" last-updated="20130222T233030-00">
    <review>
      <version>1.0</version>
      <build>50</build>
      <last-updated>20130222T233030-00</last-updated>
      <stars>5</stars>
      <device-model>SHW-M130K</device-model>
      <device-name>Samsung GT-i9082</device-name>
      <country>US</country>
    </review>
    <review>
      <version>1.0</version>
      <build>50</build>
      <last-updated>20130222T233030-00</last-updated>
      <stars>5</stars>
      <device-model>HTC One X</device-model>
      <device-name>HTC One X</device-name>
      <country>DE</country>
    </review>
  </application-reviews>
</review-list>
```

### Downloads
Request:
```
https://www.distributorappstore.com/openaep/downloads
```

Response:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<downloads version="1">
  <download>
    <package>com.softspb.geo_game</package>
    <datetime>20130222T233030</datetime>
    <version>1.0</version>
    <build>50</build>
    <last-updated>20130227T110425</last-updated>
    <device-model>SHW-M130K</device-model>
    <device-name>Samsung GT-i9082</device-name>
    <country>US</country>
    <is-update>no</is-update>
  </download>
  <download>
    <package>com.softspb.flashcards.sv</package>
    <datetime>20130222T233029</datetime>
    <version>1.3.1</version>
    <build>81</build>
    <last-updated>20130227T110425</last-updated>
    <device-model>HTC One X</device-model>
    <device-name>HTC One X</device-name>
    <country>DE</country>
    <is-update>yes</is-update>
  </download>
</downloads>
```

### Purchases
Request:
```
https://www.distributorappstore.com/openaep/purchases
```

Response:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<purchases version="1">
  <purchase>
    <id>90812378</id>
    <package>com.softspb.geo_game</package>
    <datetime>20130222T233030</datetime>
    <version>1.0</version>
    <build>50</build>
    <last-updated>20130227T110425</last-updated>
    <device-model>SHW-M130K</device-model>
    <device-name>Samsung GT-i9082</device-name>
    <country>US</country>
    <user-price>0.99</user-price>
    <user-currency>USD</user-currency>
    <inner-price>0.99</inner-price>
    <inner-currency>USD</inner-currency>
  </purchase>
  <purchase>
    <id>90812379</id>
    <package>com.softspb.flashcards.sv</package>
    <datetime>20130222T233029</datetime>
    <version>1.3.1</version>
    <build>81</build>
    <last-updated>20130227T110425</last-updated>
    <device-model>HTC One X</device-model>
    <device-name>HTC One X</device-name>
    <country>DE</country>
    <user-price>1.70</user-price>
    <user-currency>EUR</user-currency>
    <inner-price>2.50</inner-price>
    <inner-currency>USD</inner-currency>
  </purchase>
</purchases>
```

Status
-------------
Current status: draft  
Specification version: 0.70
Last update: April 11, 2013  

License
-------------
This file is licensed under the Creative Commons Attribution 2.5 license:  
http://creativecommons.org/licenses/by/2.5/

Source code is licensed under Apache License, Version 2.0:  
http://www.apache.org/licenses/LICENSE-2.0.html


