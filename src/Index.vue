<template>
    <div id="mapContainer"></div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import Prompt from "./js/prompt/prompt.js"
import util from "./js/util"
import Heatmap from "./js/heatmap.js"
let viewer = undefined;
let mapContainer = ref()
onMounted(() => {
    viewer = new Cesium.Viewer('mapContainer', {
        imageryProvider: new Cesium.ArcGisMapServerImageryProvider({
            url: "http://map.geoq.cn/arcgis/rest/services/ChinaOnlineStreetPurplishBlue/MapServer"
        }),
        terrainProvider: new Cesium.CesiumTerrainProvider({
            url: "http://data.marsgis.cn/terrain"
        }),
        animation: false,  // 设置动画小组件关闭展示
        timeline: false, // 时间轴关闭展示
        infoBox: false, // 信息盒子关闭展示
        geocoder: false, // 地理编码搜索关闭展示
        baseLayerPicker: false, // 基础图层选择器关闭展示
        sceneModePicker: false, // 场景选择器关闭展示
        fullscreenButton: false, // 全屏按钮关闭展示
        navigationInstructionsInitiallyVisible: false, // 导航说明是否最初展示
        navigationHelpButton: false, // 导航帮助按钮关闭展示
        homeButton: false
    });
    document.getElementsByClassName("cesium-viewer-bottom")[0].style.display = "none";

    util.setCameraView({
        "x": 117.28886022164883,
        "y": 31.451717348795132,
        "z": 55465.26169812524,
        "heading": 359.31729907269107,
        "pitch": -55.72672188549485,
        "roll": 359.979088652007,
        "duration": 0
    },viewer)

    let list = [];
    for (let i = 0; i < 100; i++) {
        list.push({
            "lnglat": [
                117.28 + Math.random() * (Math.random() > 0.5 ? 1 : -1),
                31.923 + Math.random() * (Math.random() > 0.5 ? 1 : -1)
            ],
            "value": 100 * Math.random()
        })
    }
    new Heatmap(viewer, {
        list: list
    })

    for (let ind = 0; ind < list.length; ind += 2) {
        let position = Cesium.Cartesian3.fromDegrees(list[ind].lnglat[0], list[ind].lnglat[1]);
        viewer.entities.add({
            position: position,
            label: {
                text: Math.floor(list[ind].value) + "",
                heightReference: 1,
                scale: 0.5,
                disableDepthTestDistance: Number.MAX_VALUE
            }
        })
    }
})



</script>

<style scoped>
.toolbar {
    position: absolute;
    top: 20px;
    left: 20px;
    z-index: 999;
}

.toolbar-btn {
    margin: 10px;
}

#mapContainer {
    margin: 0;
    padding: 0;
    height: 100%;
}
</style>

