<script setup lang="ts">
import { Magnifuer } from 'magnifuer'
import { offset } from '@floating-ui/vue'
import Image from '@/assets/img.jpg'

const src = Image
</script>

<template>
  <main>
    <div>
      <h1>🔍 Magnifuer</h1>
      <p>
        Feature-rich Vue component and tooling for creating customizable magnifying-glass-style interfaces
        with ease.
      </p>
    </div>

    <div>
      <h2>📷 Basic image magnifier</h2>
      <Magnifuer
        :scale="3"
        controllable
        :img="{
          src,
          width: 500
        }"
      />
    </div>

    <div>
      <h2>🔍 Rounded magnifying glass</h2>
      <Magnifuer
        :scale="3"
        :img="{
          src,
          width: 500
        }"
        :size="150"
        anchor="pointer"
        offset="-50%"
        border-radius="50%"
        cursor="none"
        allow-overflow
      />
    </div>

    <div>
      <h2>
        🎈 Smart positioning with <a
          href="https://floating-ui.com/"
          target="_blank"
        >Floating UI</a>
      </h2>
      <Magnifuer
        :scale="3"
        :img="{
          src,
          width: 500
        }"
        :floating="{
          placement: 'right',
          middleware: [offset(10)]
        }"
      />
    </div>

    <div>
      <h2>✨ Custom content</h2>
      <Magnifuer
        :scale="3"
        anchor="pointer"
        :size="{ width: 200, height: 100 }"
        :offset="{ x: '-50%', y: 20 }"
      >
        <article style="background-color: #fff">
          <h1>This text will be magnified</h1>
          <p>
            Magnifying any content would feel
            as natural as magnifying the image
          </p>
        </article>
      </Magnifuer>
    </div>

    <div>
      <h1>
        🚀 See the documentation on <a href="https://github.com/okdevme/magnifuer">GitHub</a>
      </h1>
    </div>
  </main>
</template>

<style lang="scss">
* {
  font-family: Roboto, sans-serif;
}

main {
  margin: 0 auto;
  padding: 100px 0 200px;
  width: fit-content;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 100px;

  > div {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
}

h1 {
  text-align: center;
}
</style>
