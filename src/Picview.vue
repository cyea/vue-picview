<template>
    <div class="picview">
        <ul>
            <li v-for="(n ,i) in imgdata" :key="i">
                <img @click="picsee(src=n[props.original])" v-if="props&&props.thumbnail&&props.original" :src="n[props.thumbnail]" alt="" :style="`width:${width};height:${height}`">
                <img @click="picsee(src=n)" v-else :src="n" alt="" :style="`width:${width};height:${height}`">
            </li>
        </ul>
        <div @click="close($event)" ref="pop" class="picview-pop">
            <i ref="rote" class="rote" @click="rote">
                <svg class="icon" style="width: 40px; height: 40px;vertical-align: middle;fill: currentColor;overflow: hidden;" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="1408">
                    <path d="M951.629227 461.298248c-11.243065-11.478426-31.018457-11.573593-42.421158-0.393973l-19.681248 19.352767C879.102401 259.036661 699.342294 86.802972 477.064838 86.802972c-227.913826 0-413.357376 185.43127-413.357376 413.357376 0 227.943502 185.445596 413.373749 413.357376 413.373749 121.468492 0 236.415454-53.759391 314.960345-146.978493 3.494591-2.674922 6.330172-5.887081 8.469905-9.510608 0.283456-0.343831 0.599657-0.693802 0.913812-1.038656l2.016937-3.181459-0.661056-0.343831c1.353834-3.560082 1.984191-7.02602 1.984191-10.518564 0-17.229406-13.983479-31.240515-31.209816-31.240515-10.361999 0-20.060895 5.509481-25.698289 14.424524-67.300802 80.872912-165.997662 127.260405-270.775007 127.260405-194.21533 0-352.277252-158.031223-352.277252-352.24553 0-194.19998 158.060899-352.261902 352.277252-352.261902 192.954617 0 350.169241 155.936515 352.21483 348.388688l-35.052331-35.144428c-11.307533-11.385305-31.113625-11.417027-42.420135-0.096191-11.778254 11.701506-11.778254 30.753421-0.063445 42.48358l74.008574 74.194816c5.637394 5.701862 13.227256 8.818853 21.22644 8.818853l0.314155-0.029676 0.787946 0.218988c1.699712 0.441045 3.559059 0.944512 5.636371 0.944512 7.874341 0 15.337313-3.052522 21.00643-8.594749l76.558653-75.331709c5.732561-5.622044 8.943696-13.211906 9.008164-21.227464C960.351889 474.525504 957.266621 466.999087 951.629227 461.298248M675.059238 606.886067l-0.030699-0.124843 0.063445-234.57248c0-28.42233-23.147186-51.537793-51.554166-51.537793L311.508221 320.650951c-28.405957 0-51.522444 23.115464-51.522444 51.537793l0 268.680299c0 28.405957 23.116487 51.55212 51.522444 51.55212l312.030619 0c28.405957 0 51.554166-23.14514 51.554166-51.55212l-0.030699-32.500205 0-1.482771L675.059238 606.886067zM629.458667 374.252753l0 234.209206 0 15.150048 0 15.210423c0 4.408403-3.590781 7.997138-7.999185 7.997138L313.585533 646.819568c-4.408403 0-7.999185-3.589758-7.999185-7.997138L305.586348 374.252753c0-4.425799 3.590781-7.999185 7.999185-7.999185l307.872926 0C625.867886 366.253568 629.458667 369.826953 629.458667 374.252753M586.060251 439.742303c-6.455015 0-12.501732 2.487657-17.006326 6.974855l-83.424015 92.77908L430.235276 500.19207c-4.345981-4.077875-10.077519-6.26775-16.156982-6.26775-7.904017 0-13.951757 2.551102-18.581194 7.212262l-64.623833 86.414115c-8.345062 8.251941-8.345062 23.36822 0.913812 32.659841 4.535293 4.53427 10.519588 7.020904 16.848737 7.020904 6.487761 0 12.43931-2.548032 17.195637-7.336082l52.465932-70.101591L472.686111 588.339666c4.408403 4.122901 10.235109 6.329149 16.818037 6.329149 6.457062 0 12.472056-2.521426 17.005302-7.083326l96.746438-107.59553c4.15667-4.094248 6.643304-10.093892 6.643304-16.502859 0-6.392594-2.488681-12.392238-7.054673-16.895809C598.53333 442.261683 592.391447 439.742303 586.060251 439.742303M402.521075 487.689315c25.446555 0 46.168506-20.707624 46.168506-46.184879 0-25.446555-20.721951-46.153156-46.168506-46.153156-25.445532 0-46.167482 20.705578-46.167482 46.153156C356.353592 466.98169 377.075543 487.689315 402.521075 487.689315" p-id="1409"></path>
                </svg>
            </i>
            <img ref='img' :src="picsrc" alt="" :style="`transform: scale(${scale}) rotate(${roted}deg);width:${picW}px;height:${picH}px;top:${picTop}px;left:${picLeft}px`">
        </div>
    </div>
</template>
<script>
export default {
    name: "Picview",
    props: {
        imgdata: Array,
        props: {
            type: Object
        },
        width: String,
        height: String
    },
    data() {
        return {
            picsrc: "",
            picW: "",
            picH: "",
            scale: 1,
            roted: 0,
            picTop: 0,
            picLeft: 0
        };
    },
    methods: {
        picsee(src) {
            this.picsrc = src;
            this.scale = 1;
            this.roted = 0;
            this.$refs.pop.style.display = "block";
            let img = new Image();
            img.src = src;
            let vm = this;
            img.onload = function() {
                vm.zoom();
                vm.drag();
                vm.countImg();
            };
            window.onresize = function() {
                vm.countImg();
            };
        },
        zoom() {
            let vm = this;
            document.body.onmousewheel = function(event) {
                event = event || window.event;
                if (event.deltaY > 0) {
                    vm.scale = vm.scale > 0.2 ? vm.scale - 0.1 : vm.scale;
                } else {
                    vm.scale += 0.1;
                }
            };
        },
        drag() {
            let oDiv = this.$refs.img;
            let vm = this;
            oDiv.onmousedown = function(en) {
                var ev = ev || event;
                var disX = en.clientX - oDiv.offsetLeft;
                var disY = en.clientY - oDiv.offsetTop;
                if (oDiv.setCapture) {
                    oDiv.setCapture();
                }
                document.onmousemove = function(en) {
                    var ev = ev || event;
                    if (
                        en.clientY > 0 &&
                        en.clientY < vm.$refs.pop.clientHeight &&
                        en.clientX > 0 &&
                        en.clientX < vm.$refs.pop.clientWidth
                    ) {
                        // oDiv.style.top = en.clientY - disY + "px";
                        // oDiv.style.left = en.clientX - disX + "px";
                        vm.picTop = en.clientY - disY;
                        vm.picLeft = en.clientX - disX;
                    }
                };
                document.onmouseup = function() {
                    document.onmousemove = null;
                    if (oDiv.releaseCapture) {
                        oDiv.releaseCapture();
                    }
                };
                return false; //阻止默认行为（如果页面中有文字，则会默认拖动文字），ie8及一下不行
            };
        },
        rote() {
            this.roted += 90;
        },
        close(e) {
            if (
                e.target != this.$refs.img &&
                e.target.contains(this.$refs.rote)
            ) {
                this.$refs.pop.style.display = "none";
            } else {
                return false;
            }
        },
        countImg() {
            let picW = this.$refs.img.naturalWidth;
            let picH = this.$refs.img.naturalHeight;
            let Width = this.$refs.pop.offsetWidth;
            let Height = this.$refs.pop.offsetHeight;
            if (Width / Height <= picW / picH) {
                this.picW = Width;
                this.picH = `${Number(picH) * Width / Number(picW)}`;
                this.picTop = (Height - this.picH) / 2;
                this.picLeft = 0;
            } else {
                this.picH = Height;
                this.picW = `${Number(picW) * Height / Number(picH)}`;
                this.picTop = 0;
                this.picLeft = (Width - this.picW) / 2;
            }
        }
    }
};
</script>
<style  scoped>
li,
ul {
    margin: 0;
    padding: 0;
    list-style: none;
}
ul:after {
    content: "";
    display: block;
    clear: both;
}
li {
    float: left;
}
li img {
    display: block;
    cursor: pointer;
}
.picview-pop {
    display: none;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.3);
    user-select: none;
    overflow: hidden;
}
.picview-pop .rote {
    display: block;
    width: 40px;
    height: 40px;
    cursor: pointer;
    position: absolute;
    right: 50%;
    margin-right: -20px;
    top: 90%;
    z-index: 9999;
}
.picview-pop img {
    cursor: move;
    position: absolute;
}
</style>


