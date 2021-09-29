<script>
export default {
  props: { xScore: Number, oScore: Number },
};
</script>

<template>
  <div class="scoreboard">
    <div class="score">
      <div class="sign x-sign" />
      {{ xScore }}
    </div>
    <div class="score">
      <div class="sign o-sign" />
      {{ oScore }}
    </div>
  </div>
</template>

<style>
.scoreboard {
  display: flex;
  justify-content: center;
  margin: 20px 0;
}
.scoreboard .score {
  display: flex;
  align-items: center;
}
.scoreboard .sign {
  height: 25px;
  width: 25px;
  box-sizing: border-box;
  margin: 0 15px;
}
</style>