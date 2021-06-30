<template>
    <canvas ref="bjsCanvas" />
</template>

<script>
import { Engine, Scene, FreeCamera, HemisphericLight, MeshBuilder, Vector3, Color4 } from "@babylonjs/core";
import { onMounted, ref } from '@vue/runtime-core';

const BJS_CANVAS_WIDTH = 500
const BJS_CANVAS_HEIGHT = 500
const BJS_CANVAS_ZINDEX = 9

export default {
    setup() {
        const bjsCanvas = ref(null)

        onMounted(() => 
        {
            bjsCanvas.value.width = BJS_CANVAS_WIDTH
            bjsCanvas.value.height = BJS_CANVAS_HEIGHT
            bjsCanvas.value.style.zIndex = BJS_CANVAS_ZINDEX
            const engine = new Engine(bjsCanvas.value)
            const scene = new Scene(engine)

            createScene(scene, bjsCanvas.value)
            setupRenderLoop(engine, scene)
        })

        const setupRenderLoop = (engine, scene) => {
            engine.runRenderLoop(function () {
                scene.render()
            })

            window.addEventListener("resize", function () {
                engine.resize()
            })
        }

        const createScene = (scene, canvas) => {
            const camera = new FreeCamera("camera1", new Vector3(0, 5, -10), scene);
            camera.setTarget(Vector3.Zero());
            camera.attachControl(canvas, true);

            scene.clearColor = new Color4(0.3, 0.2, 0.7, 1)

            const light = new HemisphericLight("light", new Vector3(0, 1, 0), scene);
            light.intensity = 0.7;

            const sphere = MeshBuilder.CreateSphere("sphere", {diameter: 2, segments: 32}, scene);
            sphere.position.y = 1;

            MeshBuilder.CreateGround("ground", {width: 6, height: 6}, scene);
        }

        return {
            bjsCanvas
        }
    }
}
</script>