<template>
  <div>
    <svg viewBox="0,0 300 200">
      <line
        stroke="#c4c4c4"
        stroke-width="2"
        x1="0"
        y1="100"
        x2="300"
        y2="100"
      />
      <!-- en polyline (0,0)  es esq-sup-izq, (max,max) esq-inf-der -->
      <polyline
        fill="none"
        stroke="#0689b0"
        stroke-width="2"
        points="100,0 100,100 200,100 200,0 100,0"
      />
      <line
        stroke="#04b500"
        stroke-width="2"
        x1="200"
        y1="0"
        x2="200"
        y2="200"
      />
    </svg>
    <p>Ultimos 30 días</p>
  </div>
</template>

<style scoped>
svg {
  width: 100%;
}

p {
  text-align: center;
}
</style>
