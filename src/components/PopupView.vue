<template>
  <div class="popup">
    <div class="popup-inner">
      <div class="header">
        <h2>Quick Pay</h2>
      </div>
        <slot />
        <button class="popup-close" @click="TogglePopup()">x</button>
        <img src="https://static.vecteezy.com/system/resources/thumbnails/016/070/795/small/3d-realistic-check-mark-button-illustration-vector.jpg" alt="">
        <p class="thank">Bezahlung erfolgreich. Vielen Dank für Ihre Rechnung</p>
        <div class="line"></div>
        <p class="foot">Total :  {{ btnText }} €</p>
        
    </div>

  </div>
</template>

<script>

export default {




    name: 'PopupView',
  props: ['TogglePopup', 'btnText']


}
</script>

<style scoped>

.popup {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 99;
  display: flex;
  align-items: center;
  justify-content: center;
}

.popup-inner {
  width: 400px;
height: 350px;
background: silver;
border-radius: 3px;
box-shadow: 0 2px 12px 0 rgba(0,0,0, .4);
position: relative;
}
.header {
  height: 68px;
  background: #27ae60;
  overflow: hidden;
  border-radius: 3px 3px 0 0;
  box-shadow: 0 2px 3px 0 rgba(0,0,0, .2);
}

.header h2 {
  color: white;
  padding-left: 32px;
  padding-top: 15px;
  font-weight: normal;
}

.popup-close {
  position: absolute;
  right:    0;
  top:   0;
  margin-right: 7px;
  margin-top: 7px;
  color: #e8f7fc;
  font-size: 25px;
  font-weight: bold;
  cursor: pointer;
  border: none;
  background: transparent;
}

img {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 50%;
}

.thank {
  padding-top: 10px;
  font-size: 19px;
  color: #1a1a1a;
  text-align: center;
}

.line {
  bottom: 60px;
  width: 100%;
  height: 1px;
  background: white;
}

.foot {
padding: 10px;
  font-size: 14px;
  color: #1a1a1a;
  text-align: right;
}
</style>