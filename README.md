----------


> **Installation**

**Install the Cordova and Ionic Native plugins:**
>  ionic cordova plugin add cordova-plugin-geolocation
       
>  npm install --save @ionic-native/geolocation
       
>  ionic cordova plugin add cordova-plugin-mauron85-background-geolocation
>  
>  npm install --save @ionic-native/background-geolocation

**usage**
*app.module.ts*

    import {LocationTrackerProvider} from '../providers/location-tracker/location-tracker';
    import { BackgroundGeolocation } from '@ionic-native/background-geolocation';
    import { Geolocation } from '@ionic-native/geolocation';
**add to providers**

    providers: [
        BackgroundGeolocation,
        Geolocation,
		 LocationTrackerProvider]
**Create location.provider.ts**

   

     import {  NgZone } from '@angular/core';
    import { BackgroundGeolocation } from '@ionic-native/background-geolocation';
    import { Geolocation, Geoposition } from '@ionic-native/geolocation';


**Usage**

    this.backgroundGeolocation.configure(config).subscribe((location) => {
    
          console.log('BackgroundGeolocation:  ' + location.latitude + ',' + location.longitude);
    
          // Run update inside of Angular's zone
          this.zone.run(() => {
            this.lat = location.latitude;
            this.lng = location.longitude;
          });
    
        }, (err) => {
    
          console.log(err);
    
        });
    
        // Turn ON the background-geolocation system.
        this.backgroundGeolocation.start();
    
    
        // Foreground Tracking
    
      let options = {
        frequency: 3000,
        enableHighAccuracy: true
      };
    
      this.watch = this.geolocation.watchPosition(options).filter((p: any) => p.code === undefined).subscribe((position: Geoposition) => {
    
        console.log(position);
    
        // Run update inside of Angular's zone
        this.zone.run(() => {
          this.lat = position.coords.latitude;
          this.lng = position.coords.longitude;
        });
    
      });

