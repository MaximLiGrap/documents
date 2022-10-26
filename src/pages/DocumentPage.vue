<template>
  <div class="container">
      <div>
        <div class="header">
          <div>
            <h2 class="header__title">Документы</h2>
          </div>
          <div class="header__btn">
            <button class="header__btn-tab"><img src="@/assets/bookmark.png" alt=""></button>
            <button class="header__btn-type">Новый тип</button>
            <button class="header__btn-doc">Новый документ</button>
          </div>
        </div>
        <div class="search">
          <label class="search__label" for="search">
            <img class="search__img" src="@/assets/lop.png" alt="">
            <input placeholder="Поиск" v-model="search"
            class="search__input" name="search" type="text">
            <button v-if="this.search.length>0" @click="resetSearch" class="search__close"></button>
          </label>
        </div>
        <div>
          <draggable class="mb-5" handle=".handle"  ghost-class="ghost">
              <TypeComponent :item="item" class="list-group-item"
                v-for="item in seasrchType.length>0 ? seasrchType : createDoc" :key="item.id" />
          </draggable>
          <div>
            <draggable :list="documents"  group="documents" handle=".handle" ghost-class="ghost">
                <DocComponent :item="i" v-for="i in seasrchDocument" :key="i.id+1000"/>
            </draggable>
          </div>
        </div>
      </div>
    <div>
    </div>
  </div>
</template>

<script>
import draggable from 'vuedraggable';
import TypeComponent from '@/components/TypeComponent.vue';
import DocComponent from '@/components/DocComponent.vue';

export default {
  components: {
    TypeComponent, DocComponent, draggable,
  },
  data() {
    return {
      docType: [{
        title: 'Обязательные для всех', text: 'Документы, обязательные для всех сотрудников без исключения', id: 0, documents: [{ id: 0, title: 'Трудовая', text: '' }],
      },
      {
        title: 'Обязательные для трудоустройства', text: 'Документы, без которых невозможно трудоустройство человека на какую бы то ни было должность в компании вне зависимости от граж', id: 1, documents: [{ id: 1, title: 'Страховка', text: '' }],
      },
      {
        title: 'Специальные', text: '', id: 2, documents: [{ id: 2, title: 'Мед', text: '' }],
      }],
      documents: [{ id: 1000, title: 'Паспорт', text: '' }, { id: 1001, title: 'ИНН', text: '' }, { id: 1003, title: 'Тестовое задание кандидата', text: 'Россия, Белоруссия, Украина, администратор филиала, повар-сушист, повар-пиццмейкер, повар горячего цеха' }],
      value: '',
      search: '',
    };
  },
  computed: {
    seasrchType() {
      return this.docType.filter((item) => item.title.includes(this.search));
    },
    seasrchDocument() {
      return this.documents.filter((item) => item.title.includes(this.search));
    },
    createDoc() {
      return this.docType.filter((item) => item.documents.find(
        (elem) => elem.title.includes(this.search),
      ));
    },
  },
  methods: {
    createType() {
      this.docType.push({ text: this.value, id: this.docType.length, documents: [] });
    },
    resetSearch() {
      this.search = '';
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
h2, h3, h4{
  margin: 0;
}

.header__title {
  font-weight: 500;
  font-size: 22px;
  line-height: 108%;
}

.container {
  max-width: 1440px;
  padding: 30px;
}
.type {
  max-width: 1160px;
}

.type__item {
  display: flex;
  justify-content: space-between;
  padding: 13px 16px;
  max-width: 1160px;
  border: 1px solid #C2C5CD;
  margin-bottom: -1px;
  margin-top: -1px;
}

.ghost {
  box-shadow: 0px 3px 16px rgba(0, 102, 255, 0.7);
}

.mb-5 {
  margin-bottom: 14px;
}

.header {
  margin-bottom: 23px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.header__btn {
  display: flex;
  gap: 10px;
  align-items: center;
}
.header__btn-tab {
  cursor: pointer;
  width: 30px;
  height: 30px;
  border-radius: 100%;
  background-color: unset;
  border: none;
  padding: unset;
}

.header__btn-type, .header__btn-doc {
  cursor: pointer;
  position: relative;
  font-style: normal;
  font-weight: 500;
  font-size: 12px;
  background-color: white;
  border: 1px solid #D3D8DF;
  border-radius: 50px;
  padding: 8px 17px 8px 34px;
}
.header__btn-type::before, .header__btn-doc::before {
  content: '';
  left: 0;
  top: 1px;
  position:absolute;
  display:inline-block;
  width:28px;
  height:28px;
  background:
    linear-gradient(#0066FF,#0066FF),
    linear-gradient(#0066FF,#0066FF);
  background-position:center;
  background-size: 50% 2px,2px 50%; /*thickness = 2px, length = 50% (25px)*/
  background-repeat:no-repeat;
}

.search {
  margin-bottom: 20px;
  max-width: 564px;
}

.search__label {
  position: relative;
}

.search__img {
  width: 13px;
  height: 14px;
  position: absolute;
  left: 0;
  top: 3px;
}

.search__close {
  cursor: pointer;
  position: absolute;
  width: 11px;
  height: 11px;
  right: 0;
  top: 0;
  border: unset;
  background-color: unset;
}

.search__close::before,
.search__close::after {
  content: '';
  position: absolute;
  top: 10px;
  left: 0;
  display: block;
  width: 14px;
  height: 2px;
  background: #FF238D
;
}

.search__close::before {
  transform: rotate(45deg);
}

.search__close::after {
  transform: rotate(-45deg);
}

.search__input {
  width: 100%;
  padding-left: 25px;
  padding-bottom: 12px;
  border-top: none;
  border-left: none;
  border-right: none;
}

.search__input:focus {
  outline:none;
}

</style>
