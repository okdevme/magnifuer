# 🔍 Magnifuer

Feature-rich Vue component and tooling for creating customizable magnifying-glass-style interfaces
with ease.

## 🕹️ [Demo](https://okdevme.github.io/magnifuer/)

- [⚡ Stackblitz Playground](https://stackblitz.com/edit/magnifuer-playground?file=src%2FApp.vue)

## 🚀 Features

- ✨ **Magnify anything** — not restricted to images
- 🎨 **Style-free** — injects only basic layout styles
- 🎯 **Smart positioning** — use the full power provided by [🎈 Floating UI](https://floating-ui.com/)
- 🛠️ **Tooling** — provides utilities to create your own magnifier components
- 🛡️ **Type-safe** and ⚡ **SSR-friendly**

## 📦 Install

```bash
npm i magnifuer
```

Optionally install [🎈 Floating UI](https://floating-ui.com/) if you plan to use smart positioning:
```bash
npm i @floating-ui/vue
```

## 🎯 Quick start

```vue
<script setup lang="ts">
import { Magnifuer } from 'magnifuer'
import 'magnifuer/style.css'

// Optional
import { offset } from '@floating-ui/vue'
</script>

<template>
  <!-- 📷 Basic image magnifier -->
  <Magnifuer
    :scale="3"
    controllable
    :img="{
      src: '/path/to/image',
      width: 500
    }"
  />

  <!-- 🔍 Rounded magnifying glass -->
  <Magnifuer
    :scale="3"
    controllable
    :img="{
      src: '/path/to/image',
      width: 500
    }"
    :size="150"
    anchor="pointer"
    offset="-50%"
    border-radius="50%"
    cursor="none"
    allow-overflow
  />

  <!-- 🎈 Smart positioning with Floating UI -->
  <Magnifuer
    :scale="3"
    :img="{
      src: '/path/to/image',
      width: 500
    }"
    :floating="{
      placement: 'right',
      middleware: [offset(10)]
    }"
  />
  
  <!-- ✨ Custom content -->
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
</template>
```

## 🧩 API Reference

### `Magnifuer`

Component providing all the essential needs for magnifying images or other content.

#### Usage:

```vue
<script setup lang="ts">
import { Magnifuer } from 'magnifuer'
import 'magnifuer/style.css' // Can be imported only once in `main.ts`
</script>

<template>
  <Magnifuer
    :scale="3"
    :img="{
      src: {
        default: '/path/to/compressed/image',
        magnifier: '/path/to/original/image'
      },
      width: 500
    }"
  />
</template>
```

#### Type Declarations:

<details>
<summary>Show Type Declarations</summary>

<!-- SOURCE dist/types/component.d.ts -->
```ts
import { CSSProperties, HTMLAttributes, ImgHTMLAttributes, TransitionProps } from 'vue';
import { UseFloatingOptions } from '@floating-ui/vue';
import { UseMagnifuerState } from '../composables/useMagnifuer';
import { MagnifuerPosition, MagnifuerSize, OptionsToProp } from '.';
import { UseMagnifuerScaleOptions } from '../composables/useMagnifuerScale';
export interface MagnifuerState extends UseMagnifuerState {
  /**
   * Whether the magnifier is currently active
   */
  active: boolean
  /**
   * Absolute position and size of the anchor
   */
  anchor: MagnifuerPosition & MagnifuerSize
  /**
   * Magnifier offset value as CSS values
   */
  offset?: MagnifuerPosition<string>
}

export interface MagnifuerImgSrc {
  /**
   * Image source for the default slot
   *
   * @see https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img#src
   */
  default: string
  /**
   * Image source for the magnifier slot
   *
   * @see https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img#src
   */
  magnifier: string
}
export interface MagnifuerImg extends Omit<ImgHTMLAttributes, 'src'> {
  src: string | MagnifuerImgSrc
}

export interface MagnifuerOffset {
  x: number | string
  y: number | string
}

export interface MagnifuerProps {
  /**
   * Allow user to control the magnifier scale using the mouse wheel
   *
   * @default false
   * @see {@link UseMagnifuerScaleOptions}
   */
  controllable?: boolean | OptionsToProp<UseMagnifuerScaleOptions>
  /**
   * Provide the image to be magnified
   *
   * @see Use {@link MagnifuerSlots|`default` and `magnifier` slots} to provide custom contents
   */
  img?: MagnifuerImg
  /**
   * Anchor for the magnifier
   *
   * - `'self'` - Container element
   * - `'pointer'` - Pointer (cursor, touch, etc.)
   * - `HTMLElement` - Reference to a custom element
   *
   * @default 'self'
   */
  anchor?: 'self' | 'pointer' | HTMLElement
  /**
   * Position of the magnifier
   *
   * - `'anchor'` - Set position equal to the anchor position
   * - `{ x: number, y: number }` - Set position to absolute coordinates
   *
   * @default 'anchor'
   * @see Use {@link MagnifuerProps.floating|`floating`} to use [Floating UI](https://floating-ui.com/docs/vue) for the positioning
   */
  position?: 'anchor' | MagnifuerPosition
  /**
   * Use transform for positioning the magnifier element.
   * Disable to use `top` and `left` properties instead.
   *
   * Applies only when used with {@link MagnifuerProps.position|`position`}.
   *
   * @default true
   */
  transform?: boolean
  /**
   * Offset the magnifier element by specified values.
   * Accepts any CSS value or a number in px.
   *
   * Provide a single value to apply to both axes.
   */
  offset?: number | string | MagnifuerOffset
  /**
   * Use [Floating UI](https://floating-ui.com/docs/vue) for positioning the magnifier element.
   *
   * {@link MagnifuerProps.position|`position`} is ignored when this one is provided.
   *
   * @see https://floating-ui.com/docs/vue#options
   */
  floating?: OptionsToProp<UseFloatingOptions<HTMLElement>>
  /**
   * Size of the magnifier
   *
   * - `'anchor'` - set size equal to the anchor size
   * - `number` - set width and height to the same value
   * - `{ width: number, height: number }` - set width and height to absolute values
   *
   * @default 'anchor'
   */
  size?: 'anchor' | number | MagnifuerSize
  /**
   * Element for the magnifier to be teleported to, `false` to disable the teleport
   *
   * @default 'body'
   * @see https://vuejs.org/guide/built-ins/teleport.html
   */
  teleport?: string | HTMLElement | false
  /**
   * Enable Vue transition for the magnifier element
   *
   * @see https://vuejs.org/guide/built-ins/transition.html
   */
  transition?: string | TransitionProps
  /**
   * Z-index for the magnifier element
   *
   * @default 1000
   */
  zIndex?: number
  /**
   * Disable the magnifier
   *
   * @default false
   */
  disabled?: boolean
  /**
   * Allow the magnifying area to overflow the container
   *
   * @default false
   * @see {@link UseMagnifuerOptions}
   */
  allowOverflow?: boolean
  /**
   * Display the magnifying area in the container
   *
   * @default true
   * @see Use {@link MagnifuerSlots.area|`area` slot} to customize it
   */
  area?: boolean
  /**
   * Cursor to apply to the container
   *
   * @see https://developer.mozilla.org/en-US/docs/Web/CSS/cursor
   */
  cursor?: CSSProperties['cursor']
  /**
   * Border radius to apply to the magnifier and default magnifying area elements
   *
   * @see https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius
   */
  borderRadius?: string | number
  /**
   * Class to apply to the default magnifying area element
   */
  areaClass?: HTMLAttributes['class']
  /**
   * Class to apply to the magnifier element
   */
  magnifierClass?: HTMLAttributes['class']
  /**
   * Class to apply to the magnifier content element
   */
  contentClass?: HTMLAttributes['class']
}

export type MagnifuerBaseSlot = (props: { state: MagnifuerState }) => unknown
export interface MagnifuerSlots {
  /**
   * Slot to be used for both the container and the magnifier.
   *
   * Overridable by the {@link MagnifuerSlots.magnifier|`magnifier` slot} for the magnifier.
   *
   * @param props.state Current state
   * @param props.isMagnifier Specifies whether this slot is currently being rendered in the {@link MagnifuerSlots.magnifier|`magnifier` slot}
   * @see Use {@link MagnifuerProps.img|`img`} to render an image by default
   */
  default?: (props: { state: MagnifuerState, isMagnifier: boolean }) => unknown
  /**
   * Contents of the magnifier
   */
  magnifier?: MagnifuerBaseSlot
  /**
   * Use to make a custom magnifying area
   *
   * @see Use {@link MagnifuerProps.areaClass|`areaClass`} to alter the styles of the default magnifying area element
   */
  area?: MagnifuerBaseSlot
}

```
<!-- SOURCE END -->
</details>

### `useMagnifuer`

Utility composable for making custom magnifying-glass-style component.
Provides all the essential calculations updated in real-time for positioning the elements.

#### Usage:

```vue
<script setup lang="ts">
import { ref } from 'vue'
import { useMagnifuer } from 'magnifuer'

const containerRef = ref<HTMLElement>()
const scale = ref(2)

const state = useMagnifuer(
  containerRef,
  scale,
  { width: 200, height: 100 }
)
</script>

<template>
  <div ref="containerRef">
    <img src="/path/to/image" alt="Image to magnify">
    
    <div
      id="magnifying-area"
      :style="{
        width: state.areaSize.width + 'px',
        height: state.areaSize.height + 'px',
        transform: [
          `translate(-50%, -50%)`,
          `translate(${state.absolute.x}px, ${state.absolute.y}px)`
        ].join(' ')
      }"
    />
  </div>

  <div
    v-if="state.pointer.isInside"
    id="magnifier"
    :style="{
      width: state.size.width + 'px',
      height: state.size.height + 'px'
    }"
  >
    <div
      id="magnifier-content"
      :style="{
        width: state.containerSize.width + 'px',
        height: state.containerSize.height + 'px',
        transform: [
          `scale(${state.scale})`,
          `translate(${-state.x * 100}%, ${-state.y * 100}%)`
        ].join(' ')
      }"
    >
      <img src="/path/to/image" alt="Magnified image">
    </div>
  </div>
</template>
```

See the implementation of `Magnifuer` to further understand
how to use the values provided by `useMagnifuer`.

#### Type Declarations:

<details>
<summary>Show Type Declarations</summary>

<!-- SOURCE dist/composables/useMagnifuer.d.ts -->
```ts
import { MaybeRef, MaybeRefOrGetter, Reactive } from 'vue';
import { MagnifuerPosition, MagnifuerSize } from '../types';
export interface UseMagnifuerOptions {
    /**
     * Allow the magnifying area to overflow the container
     *
     * @default false
     */
    allowOverflow?: MaybeRefOrGetter<boolean>;
}
export interface MagnifuerPointer extends MagnifuerPosition {
    /**
     * Absolute position of the pointer in px
     */
    absolute: MagnifuerPosition;
    /**
     * Whether the pointer is inside the container
     */
    isInside: boolean;
}
export interface UseMagnifuerState {
    /**
     * Current scale value
     */
    scale: number;
    /**
     * Current position of the magnifier on X axis relative to container width as a fractional value (0-1)
     */
    x: number;
    /**
     * Current position of the magnifier on Y axis relative to container height as a fractional value (0-1)
     */
    y: number;
    /**
     * Absolute position of the magnifier relative to the container in px
     */
    absolute: MagnifuerPosition;
    /**
     * Pointer state relative to the container
     */
    pointer: MagnifuerPointer;
    /**
     * Size of the magnifier in px
     */
    size: MagnifuerSize;
    /**
     * Size of the container in px
     */
    containerSize: MagnifuerSize;
    /**
     * Size of the magnifying area in px
     */
    areaSize: MagnifuerSize;
}
/**
 * Utility composable for making custom magnifying-glass-style component.
 * Provides all the essential calculations updated in real-time for positioning the elements.
 *
 * @param container Reference to the container element whose content is to be magnified
 * @param scale Scale value
 * @param size Size of the magnifier in px
 * @param options Additional options
 */
declare function useMagnifuer(container: MaybeRef<HTMLElement | null | undefined>, scale: MaybeRefOrGetter<number>, size: MagnifuerSize<MaybeRefOrGetter<number>>, options?: UseMagnifuerOptions): Reactive<UseMagnifuerState>;
export default useMagnifuer;

```
<!-- SOURCE END -->
</details>

### `useMagnifuerScale`

Utility composable for controlling the scale value of a magnifier.
Keeps the scale within limits and provides callbacks to alter it.

#### Usage:

```vue
<script setup lang="ts">
import { ref } from 'vue'
import { useMagnifuerScale } from 'magnifuer'

const scale = ref(2)

const { alter, onWheel } = useMagnifuerScale(scale, {
  min: 1,
  max: 10,
  speed: 1.3
})
</script>

<template>
  <p>{{ scale }}</p>
  <button @click="alter(1)">Increase scale</button>
  <button @click="alter(-1)">Decrease scale</button>
  <div
    id="container"
    @wheel="onWheel"
  >
    <!-- ... -->
  </div>
</template>
```

#### Type Declarations:

<details>
<summary>Show Type Declarations</summary>

<!-- SOURCE dist/composables/useMagnifuerScale.d.ts -->
```ts
import { MaybeRefOrGetter, Ref } from 'vue';
export interface UseMagnifuerScaleOptions {
    /**
     * Minimal scale value
     *
     * @default 1
     */
    min?: MaybeRefOrGetter<number | undefined>;
    /**
     * Maximal scale value
     *
     * @default 10
     */
    max?: MaybeRefOrGetter<number | undefined>;
    /**
     * Speed value for the default scale step function
     *
     * @default 1.3
     */
    speed?: MaybeRefOrGetter<number | undefined>;
    /**
     * Scale computation function on step
     *
     * @param current Current scale
     * @param direction Step direction (±1)
     * @returns The new scale value
     * @default (current, direction) => current * Math.pow(speed, direction)
     */
    step?: (current: number, direction: number) => number;
}
export interface UseMagnifuerScaleReturn {
    /**
     * Safe-guarded scale guaranteed to be within limits
     */
    scale: Ref<number>;
    /**
     * Alter the scale
     *
     * @param value Altering direction (±1)
     */
    alter: (value: number) => void;
    /**
     * Callback for the `wheel` event which automatically triggers the altering
     * and blocks native scrolling
     *
     * @param event
     */
    onWheel: (event: WheelEvent) => void;
}
/**
 * Utility composable for controlling the scale value of a magnifier.
 * Keeps the scale within limits and provides callbacks to alter it.
 *
 * @param scale Raw scale value
 * @param options Additional options
 */
declare function useMagnifuerScale(scale: Ref<number>, options?: UseMagnifuerScaleOptions): UseMagnifuerScaleReturn;
export default useMagnifuerScale;

```
<!-- SOURCE END -->
</details>

### Utility types

Miscellaneous types used across the package.

#### Type Declarations:

<details>
<summary>Show Type Declarations</summary>

<!-- SOURCE dist/types/index.d.ts -->
```ts
import { MaybeRefOrGetter } from 'vue';
import { MaybeReadonlyRefOrGetter } from '@floating-ui/vue';
export type ToValue<T> = T extends MaybeReadonlyRefOrGetter<infer U>
  ? U
  : T extends MaybeRefOrGetter<infer U>
    ? U
    : T

export type OptionsToProp<T> = {
  [key in keyof T]: ToValue<T[key]>
}

export interface MagnifuerPosition<T = number> {
  x: T
  y: T
}

export interface MagnifuerSize<T = number> {
  width: T
  height: T
}

```
<!-- SOURCE END -->
</details>
