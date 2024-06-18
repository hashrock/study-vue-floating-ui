<script setup lang="ts">
import { useFloating, offset } from '@floating-ui/vue';
import { ref } from 'vue';

const reference = ref(null);
const floating = ref(null);
const { floatingStyles } = useFloating(reference, floating, {
  middleware: [offset(4)],
});

let isOpen = ref(false);

const dismiss = () => {
  isOpen.value = false;
};

</script>

<template>
  <div>
    <div>
      <div class="popup">Tooltip</div>
    </div>
    <button ref="reference" @click="isOpen = !isOpen">Button</button>


    <Teleport to="body">
      <Transition>
        <div v-if="isOpen">

          <div class="backdrop" @click="dismiss"></div>
          <div class="popup" ref="floating" :style="floatingStyles">

            <div class="item">My Account</div>

            <hr>

            <button class="item">
              <div>
                Profile
              </div>
              <div>
                Ctrl + P
              </div>
            </button>

            <button class="item">
              <div>
                Billing
              </div>
              <div>
                Ctrl + B
              </div>
            </button>

          </div>
        </div>
      </Transition>
    </Teleport>
  </div>
</template>

<style>
body {
  margin: 10rem
}

.backdrop {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}

hr {
  background-color: rgb(228, 228, 231);
  border: none;
  height: 1px;
}

.popup {
  background-color: white;
  padding: 10px;
  border: 1px solid rgb(228, 228, 231);
  border-radius: 5px;
  width: max-content;
  color: rgb(9, 9, 11);
  line-height: 20px;

  box-shadow: 0 6px 4px rgba(0, 0, 0, 0.1);
  /* font-family: ui-sans-serif, system-ui, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "Noto Color Emoji"; */
  font-size: 14px;
  padding: 4px;
  font-weight: 500;
}

.item {
  display: flex;
  gap: 32px;
  justify-content: space-between;
  padding: 6px 8px;
  cursor: pointer;
}

.item:hover {
  background-color: rgb(244, 244, 245)
}

.v-enter-active,
.v-leave-active {
  transition: opacity 0.1s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>
