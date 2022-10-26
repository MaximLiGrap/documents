<template>
  <div class="type">
    <div class="type__item">
      <div class="type__title">
          <button :class="{show: show}"
          class="type__btn-acordion" v-on:click="show = !show"></button>
        <div class="type__text">
          <h3>{{item.title}}</h3>
          <span>{{item.text}}</span>
        </div>
      </div>
      <ButtonCompomemt/>
    </div>
    <transition name="fade">
      <draggable v-if="show" :list="returtItem"
      group="documents" handle=".handle" ghost-class="ghost">
        <DocComponent :item="i"
          v-for="i in item.documents" :key="i.id+1000"/>
    </draggable>
    </transition>
  </div>
</template>

<script>
import draggable from 'vuedraggable';
import DocComponent from '@/components/DocComponent.vue';
import ButtonCompomemt from '@/components/Buttons/ButtonComponent.vue';

export default {
  data() {
    return {
      show: true,
    };
  },
  components: { DocComponent, ButtonCompomemt, draggable },
  props: ['item', 'search'],
  computed: {
    returtItem() {
      return this.item.documents;
    },
  },
};
</script>

<style>
.type .document {
  margin-left: 20px;
  max-width: 1140px;
  margin-bottom: -1px;
  margin-top: -1px;
}

.type__btn-acordion {
  transition: 0.5s;
  border: 1px solid #D3D8DF;
  background-color: unset;
  position: relative;
  border-radius: 100%;
  padding: unset;
  width: 22px;
  height: 22px;
  cursor: pointer;
}

.type__title {
  display: flex;
  gap: 20px;
  align-items: center;
}

.type__text {
  display: flex;
  align-items: center;
  gap: 15px;
}

.type__text span {
  font-weight: 400;
  font-size: 11px;
  color: #8E9CBB;
}

.type__title h3 {
  font-weight: 500;
  font-size: 15px;
  line-height: 108%;
}

.type__btn-acordion::before {
  position: absolute;
  left: 0;
  top: 30%;
  height: 30%;
  width: 1px;
  background-color: #0066FF;
  content: "";
  transform: translateX(10px) rotate(-45deg);
  transform-origin: left bottom;
}
.type__btn-acordion::after {
  position: absolute;
  left: 0;
  top: 53%;
  height: 1px;
  width: 30%;
  background-color: #0066FF;
  content: "";
  transform: translateX(10px) rotate(-45deg);
  transform-origin: left bottom;
}
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active до версии 2.1.8 */ {
  opacity: 0;
}

.type__btn-acordion.show {
  transform: rotate(180deg);
}

</style>
