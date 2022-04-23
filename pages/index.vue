<template>
  <div class="container">
    <div class="selectColor">
      <input type="color" v-model="currentColor">
      <!-- <div class="row">
        <span class="cell" v-for="color in aviableColors" :key="color" :style="'background-color: ' + color" @click="changeSelectedColor(color)"></span>
      </div> -->
    </div>
    <div class="table">
      <div class="row" v-for="height in h" :key="height">
        <span :style="'background-color:' + getAllColors[height-1][width-1]" @click="changeColor(height, width)" class="cell" v-for="width in w" :key="width"></span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  asyncData() {
    let h = 20
    let w = 50
    let getAllColors = []
      for (let i = 0; i < h; i++) {
        getAllColors[i] = []
        for (let j = 0; j < w; j++) {
          getAllColors[i][j] = '#fff'
        }
      }
      return {
        h,
        w,
        currentColor: '#000',
        getAllColors,
        aviableColors: ['#00ff00', '#ff0000', '0000ff'],
      }
  },
  methods: {
    changeColor(height, width) {
      this.getAllColors[height-1].splice(width-1, 1)
      this.getAllColors[height-1].splice(width-1, 0, this.currentColor)
      console.log(height-1, width-1)
    },
    changeSelectedColor(color) {
      this.currentColor = color
    },
  }
}
</script>

<style scoped>
.container {
  min-height: 100vh;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  gap: 32px;
}
.select-color {
  border: 1px solid black;
}
.table {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
.cell {
  border: 1px solid black;
  height: 20px;
  width: 20px;
  display: block;
}
.row {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  max-width: 1000px;
}
</style>