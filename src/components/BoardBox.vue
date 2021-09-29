<script>
export default {
  props: { sign: String },
};
</script>

<template>
  <div class="box">
    <div class="sign" :class="sign" />
  </div>
</template>

<style>
.box {
  display: flex;
  background: #fff;
  cursor: pointer;
  justify-content: center;
  align-items: center;
}
.box .sign {
  height: 100px;
  width: 100px;
  box-sizing: border-box;
}
.x-sign {
  position: relative;
}
.x-sign::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  background: linear-gradient(#333, #333), linear-gradient(#333, #333);
  background-position: center;
  background-size: 100% 5px, 5px 100%; /*thickness = 2px, length = 50% (25px)*/
  background-repeat: no-repeat;
  transform: rotate(45deg);
}
.o-sign {
  border: 5px solid #333;
  border-radius: 50%;
}
</style>