

<template>
    <div ref="container" style="width: 400px; height: 400px;"></div>
</template>

<script>
import * as THREE from 'three';

export default {
    mounted() {
        // Set up the scene
        const scene = new THREE.Scene();

        // Set up the camera
        const camera = new THREE.PerspectiveCamera(
            75,
            this.$refs.container.offsetWidth / this.$refs.container.offsetHeight,
            0.1,
            1000
        );
        camera.position.z = 5;

        // Set up the renderer
        const renderer = new THREE.WebGLRenderer({ antialias: true });
        renderer.setSize(
            this.$refs.container.offsetWidth,
            this.$refs.container.offsetHeight
        );
        this.$refs.container.appendChild(renderer.domElement);

        // Set up the cube
        const geometry = new THREE.BoxGeometry(1, 1, 1);
        const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
        const cube = new THREE.Mesh(geometry, material);
        scene.add(cube);

        // Animation loop
        const animate = () => {
            requestAnimationFrame(animate);

            cube.rotation.x += 0.01;
            cube.rotation.y += 0.01;

            renderer.render(scene, camera);
        };

        animate();
    },
};
</script>

<style>
div {
    display: flex;
    justify-content: center;
    align-items: center;
}
</style>

