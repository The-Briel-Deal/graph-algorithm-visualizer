<script setup>
import { ref } from 'vue'
defineProps({
  msg: String
})
const currentAlgo = ref('Depth First Search')
const matrix = []
for (let i1 = 0; i1 < 30; i1++) {
  matrix.push([])
  for (let i2 = 0; i2 < 30; i2++) {
    matrix[i1].push(ref(0))
  }
}
const toVisit = ["5,5"]
const enqued = new Set()
for (let i = 0; i < 15; i++) {
  matrix[i][15].value = 2
}
for (let i = 0; i < 13; i++) {
  matrix[14][17 + i].value = 2
}
for (let i = 0; i < 13; i++) {
  matrix[12][16 + i].value = 2
}
for (let i = 0; i < 13; i++) {
  matrix[10][17 + i].value = 2
}
for (let i = 0; i < 13; i++) {
  matrix[8][16 + i].value = 2
}

const pickColor = (val) => {
  switch (val) {
    case 0:
      return 'grey'
    case 1:
      return '#FF0080'
    case 2:
      return 'red'
    default:
      return 'black'
  }
}



const dfs = () => {
  if (toVisit.length != 0) {
    // console.log(toVisit)
    let [x, y] = toVisit.pop().split(",")
    // console.log(toVisit)
    matrix[x][y].value = 1
    x = parseInt(x)
    y = parseInt(y)
    if (matrix[x + 1] && matrix[x + 1][y].value === 0 && !enqued.has(`${x + 1},${y}`)) {
      enqued.add(`${x + 1},${y}`)
      toVisit.push(`${x + 1},${y}`)
    }
    if (matrix[x][y + 1] && matrix[x][y + 1].value === 0 && !enqued.has(`${x},${y + 1}`)) {
      enqued.add(`${x},${y + 1}`)
      toVisit.push(`${x},${y + 1}`)
    }
    if (matrix[x - 1] && matrix[x - 1][y].value === 0 && !enqued.has(`${x - 1},${y}`)) {
      enqued.add(`${x - 1},${y}`)
      toVisit.push(`${x - 1},${y}`)
    }
    if (matrix[x][y - 1] && matrix[x][y - 1].value === 0 && !enqued.has(`${x},${y - 1}`)) {
      enqued.add(`${x},${y - 1}`)
      toVisit.push(`${x},${y - 1}`)
    }
  } else {
    console.log('finished!')
    return
  }
  setTimeout(dfs, 50)
}
const bfs = () => {
  if (toVisit.length != 0) {
    // console.log(toVisit)
    let [x, y] = toVisit.shift().split(",")
    // console.log(toVisit)
    matrix[x][y].value = 1
    x = parseInt(x)
    y = parseInt(y)
    if (matrix[x + 1] && matrix[x + 1][y].value === 0 && !enqued.has(`${x + 1},${y}`)) {
      enqued.add(`${x + 1},${y}`)
      toVisit.push(`${x + 1},${y}`)
    }
    if (matrix[x][y + 1] && matrix[x][y + 1].value === 0 && !enqued.has(`${x},${y + 1}`)) {
      enqued.add(`${x},${y + 1}`)
      toVisit.push(`${x},${y + 1}`)
    }
    if (matrix[x - 1] && matrix[x - 1][y].value === 0 && !enqued.has(`${x - 1},${y}`)) {
      enqued.add(`${x - 1},${y}`)
      toVisit.push(`${x - 1},${y}`)
    }
    if (matrix[x][y - 1] && matrix[x][y - 1].value === 0 && !enqued.has(`${x},${y - 1}`)) {
      enqued.add(`${x},${y - 1}`)
      toVisit.push(`${x},${y - 1}`)
    }
  } else {
    console.log('finished!')
    return
  }
  setTimeout(bfs, 50)
}


</script>

<template>
  <div>
    <div class="row">
      <div class="col" style="text-align: center;">
        <h3 style="color: #FF0080;">{{ currentAlgo }}</h3>
      </div>
    </div>
    <div class="row">
      <div class="col" style="text-align: center;">
        <q-btn style="background: #FF0080; color: white" label="👈 Previous Algorithm" />
      </div>
      <div class="col" style="text-align: center;">
        <q-btn style="color: #FF0080" label="Start" />
      </div>
      <div class="col" style="text-align: center;">
        <q-btn style="background: #FF0080; color: white" label="Next Algorithm 👉" />
      </div>
    </div>
    <br />
    <div class="row">
      <div class="col">
        <div v-for="row in matrix" :key="`row${row}`" style="font-size: 0; display: block;">
          <br />
          <div v-for="item in row" :key="`item${row},${item}`" style="display: inline-block;">
            <div :style="`height: 30px; width: 30px; background-color: ${pickColor(item.value)};`"></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
a {
  color: #42b983;
}
</style>
