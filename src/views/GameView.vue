<template>
  <container>
    <Map></Map>
    <Plane :x="planeInfo.x" :y="planeInfo.y"></Plane>
    <EnemyPlane :x="enemyPlane.x" :y="enemyPlane.y"></EnemyPlane>
    <!-- <EnemyPlane
      v-for="(enemy, index) in enemyPlanes"
      :key="index"
      :x="enemy.x"
      :y="enemy.y"
    ></EnemyPlane> -->
    <!-- <EnemyPlane v-for="(enemy, index) in enemyPlanes" :key="index"></EnemyPlane> -->
  </container>
</template>

<script setup="props,{emit}">
/* eslint-disable no-unused-vars */
// import { reactive } from "vue";
import Map from "../components/Map";
import Plane from "../components/Plane";
import EnemyPlane from "../components/EnemyPlane";

import { usePlane } from "../game/core/Plane";
import { useEnemyPlane } from "../game/core/EnemyPlane";
import { reactive, onMounted, onUnmounted } from "vue";
import { game } from "../game";
import { hitTestObject } from "../utils";

import { useFighting } from "../game/core/Fighting";

export default {
  components: {
    Map,
    Plane,
    EnemyPlane,
  },
};

const { planeInfo } = usePlane();
const { enemyPlane, enemyPlanes } = useEnemyPlane();

const gameOver = () => {
  emit("change-view", "EndView");
};

useFighting({
  planeInfo,
  enemyPlane,
  gameOver,
});

export { planeInfo, enemyPlane, enemyPlanes };
</script>

<style scoped></style>
