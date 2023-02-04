<script>
import { ref } from 'vue'
import tt from '@tomtom-international/web-sdk-maps';


export default {
    name: "TomMap",
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


            const marker = new tt.Marker({})
                .setLngLat(this.London)
                .addTo(map);

            const marker2 = new tt.Marker({element : markerElement})
                .setLngLat(this.oxford)
                .addTo(map);  

                

    

            // this.map = Object.freeze(map);

            var popupOffsets = {
                  top: [0, 0],
                  bottom: [0, -30],
                  "bottom-right": [0, -70],
                  "bottom-left": [0, -70],
                  left: [25, -35],
                  right: [-25, -35],
                }

            //custom icon marker
            var markerElement = document.createElement("div")
            markerElement.className = "marker"
            markerElement.style.backgroundImage = 'url(../assets/brandforum_logo-tale-airbnb_the-belo.png)'
            // element.innerHTML = '<i class="fa-brands fa-airbnb"></i>' 
            //custom popup
            const customPopUp = '<div> <p style="color:black">London</p> </div>'
            const customPopUp2 = '<div> <p style="color:red">Oxford</p> </div>'
            
            var popup = new tt.Popup({ offset: popupOffsets }).setHTML(customPopUp)
            var popup2 = new tt.Popup({ offset: popupOffsets, closeOnMove: true}).setHTML(customPopUp2)
                popup2.addClassName('my-pop-up')


            marker.setPopup(popup).togglePopup()
            marker2.setPopup(popup2).togglePopup()


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
        .marker {
            width: 50px;
            height: 70px;
            color: black;
            background-image: url(../assets/brandforum_logo-tale-airbnb_the-belo.png);
            background-size: cover;
        }
        .my-pop-up{
            color: red!important;
            p{
                color: red;
            }

        }
</style>