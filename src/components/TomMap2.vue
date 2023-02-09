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
            map: null,
            logos: [],
        }
    },
    mounted(){
      this.initializeMap();
      this.animate();
      
    },
    created()
    {
        this.welcome();

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
         
                

            } ,
        animate(){
                const timeline = gsap.timeline({defaults: {duration: 1, }});
                    timeline
                    .from(".square", { y: '-400%',ease: "ease.Out", stagger: .1})
                    .from("#h1",{ y: '-100%',ease: "bounce"})
                    .from("#tom-map",{  opacity: 0, stagger: .6})

                        // .from(".column-right", {  x: "-100vw", ease: "power2.in"}, 1)
                        // .from(".column-left", {  x: "-100%", ease: "power2.in"}, "<.5")
                        // .to("footer", {  y: 0, ease: "elastic", })
                        // .fromTo("button", {  opacity: 0, scale: 0, rotation: 720 },{  opacity: 1,scale: 1, rotation: 0})

                        // const btn = document.querySelector("button")
                        // btn.addEventListener("click", () => {
                        //     timeline.timeScale(3);
                        //     timeline.reverse();
                        // })
        },
        welcome(){
            // var firstTime = localStorage.getItem("first_time");
            //     if(!firstTime) {
                    // first time loaded!
                    for (let i = 0; i < 10; i++) {
                        
                        this.logos.push("../assets/brandforum_logo-tale-airbnb_the-belo.png")
                        // console.log(this.logos);

                        const timeline = gsap.timeline({defaults: {duration: 1, }});
                            timeline
                                // .from("#yo",{  opacity: 0, stagger: .6})
                        
                    }

                    // localStorage.setItem("first_time","1");
                // }
        }  
}}
</script>
<template>
    <div id="welcome">
        <div v-for="logo in logos" class="square"></div>
        <div v-for="logo in logos" class="square" id="blue"></div>
        <div v-for="logo in logos" class="square"></div>
    </div>
    <div id="yo">
            <h1 id="h1">TomTom Maps Demo</h1>
            <div id='tom-map' ref="mapRef"></div>
                
    </div>
</template>
<style lang="scss" scoped>

#welcome >div{
    position: absolute;
    top: 50%;
    left: 85%;
    transform: translate(-50%, -50%);
    width: 10em;
    height: 10em;
    z-index: 1;
    display: block;
    background-color: white;
    border: 1px solid black;

    &#blue{
    background-color: blue !important;
    }
}

#tom-map {
    height: 50vh;
    width: 50vw;
    border-radius: 10px;
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