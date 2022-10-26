<template>
  <div class="document">
    <div class="document__text">
      <h4 class="document__title">{{item.title}}</h4>
      <span>{{item.text}}</span>
    </div>
    <ButtonCompomemt/>
  </div>
</template>

<script>
import ButtonCompomemt from '@/components/Buttons/ButtonComponent.vue';

export default {
  components: { ButtonCompomemt },
  props: ['item'],
};
</script>

<style>
.document__text {
  display: flex;
  gap: 20px;
  align-items: center;
}

.document__text span {
  font-weight: 400;
  font-size: 11px;
  color: #8E9CBB;
}
.document {
  display: flex;
  padding: 10px 17px;
  justify-content: space-between;
  max-width: 1160px;
  border: 1px solid #C2C5CD;
  margin-top: -1px;
  margin-bottom: -1px;
}

.document__title {
  font-weight: 400;
  font-size: 13px;
  line-height: 108%;
}
</style>
