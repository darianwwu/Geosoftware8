<template>
  <div>
  <h1> {{ ausgabe }} </h1>
  <h1> {{ count }} </h1>
  <h1> {{point[0]}} </h1>
  <button @click="calculateDistance"> LOOOOL </button>
  <br>
  <button @click="countUp"> Hochzähler </button>
  </div>
</template>

<script>

import point from './point'
import cities from './cities'
var ausgabe = ""
export default {
  name: 'geosoft_8',
  data(){
    return{
      message: "Hello World",
      count: 0,
      point,
      cities,
      ausgabe
    };
  },
  methods: {
    countUp() {
      this.count++;
    },
    calculateDistance(){

     var lat1 = point[1];
     var lon1 = point[0];
    
     // Array erstellen, welche so groß wie "cities" ist
     var distances= Array.apply(null, Array[cities.length])
     for(var i = 0; i < cities.length; i++){

        var lon2 = cities[i][0];
        var lat2 = cities[i][1];
    
        const R = 6371e3; 
        const φ1 = lat1 * Math.PI/180; 
        const φ2 = lat2 * Math.PI/180;
        const Δφ = (lat2-lat1) * Math.PI/180;
        const Δλ = (lon2-lon1) * Math.PI/180;
    
        const a = Math.sin(Δφ/2) * Math.sin(Δφ/2) +
              Math.cos(φ1) * Math.cos(φ2) *
              Math.sin(Δλ/2) * Math.sin(Δλ/2);
        const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1-a));
    
        const d = Math.round(R * c); // Hier wird die Distanz gerundet
    
        distances[i] = d; // Speicherung der Distanz in einem Array
        console.log(d)

        for(var j = 0; j < distances.length; j++) {

        ausgabe = ausgabe + distances[j] + " Meter <br />";

      }
      
    }
  },
}
}
</script>

