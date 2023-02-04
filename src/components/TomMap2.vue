<script>
import { ref } from 'vue'
import tt from '@tomtom-international/web-sdk-maps';


export default {
    name: "TomMap2",
    data() {
        return {
            KEY: "e3ENGW4vH2FBakpfksCRV16OTNwyZh0e",
            London: [-0.118092,51.509865],
            oxford: [-1.257677, 51.754845],
            map: null
        }
    },
    mounted(){
      this.initializeMap()
    },
    methods:{
        initializeMap() {
             const map = tt.map({
                key: this.KEY,
                container: this.$refs.mapRef,
                center: this.London,
                zoom: 7
            });
            //custom icon marker
            const markerElement = document.createElement("div")
            markerElement.id = "marker"
            const logo = new URL("../assets/brandforum_logo-tale-airbnb_the-belo.png", import.meta.url).href
            markerElement.style.backgroundImage = `url(${logo})`
            markerElement.style.width = "30px"
            markerElement.style.height = "30px"
            markerElement.style.backgroundSize = "cover"
            markerElement.style.borderRadius= "20px"

            

            const marker = new tt.Marker({element: markerElement, anchor: "center"})
                .setLngLat(this.London)
                .addTo(map);

            const popupOffsets = {
                  top: [0, 0],
                  bottom: [0, -15],
                  "bottom-right": [0, -70],
                  "bottom-left": [0, -70],
                  left: [25, -35],
                  right: [-25, -35],
                }

           
            //custom popup
            const customPopUp = document.createElement("div")
            customPopUp.id = "my-pop-up"
            customPopUp.innerHTML = "<p> Londra</p>"
            customPopUp.style.color = "black"
            customPopUp.style.width = "150px"
            
            // const popup = new tt.Popup({ offset: popupOffsets, closeOnMove: true }).setDOMContent(customPopUp)
            const popup = new tt.Popup({offset: popupOffsets, closeOnMove: true}).setDOMContent(customPopUp)
        
            marker.setPopup(popup).togglePopup()
         
                

            } 
}}
</script>
<template>
    <div>
            <h1>TomTom Maps Demo</h1>
            <div id='tom-map' ref="mapRef"></div>
                
    </div>
</template>
<style lang="scss" scoped>
#tom-map {
    height: 50vh;
    width: 50vw;
    }
        .my-pop-up{
            color: red!important;
            p{
                color: red;
            }
            button{
                color: red;
            }

        }
</style>