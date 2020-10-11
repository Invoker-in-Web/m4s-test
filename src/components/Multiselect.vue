<template>
  <div class="multiselect">
    <label for="custom_multiselect"
      >Одиночный выбор осуществляется по клику на элемент выпадающего списка,
      множественный - <b>ctrl+click / cmd+click </b>. Отображение элементов
      осуществляется по нажатию на <b>&#x2193;</b>.
    </label>

    <div class="select_wrapper">
      <div class="input_wrapper">
        <input
          type="text"
          v-model="searchQuery"
          :disabled="isInputDisabled"
          placeholder="Выберите страну проживания"
        />

        <button
          @click="changeSelectVisibility"
          :class="{ dropdown_opened: isDropdownVisible }"
        >
          &#x2193;
        </button>
      </div>

      <select
        id="custom_multiselect"
        multiple
        v-model="selectedList"
        :size="initialItems.length"
        v-show="isDropdownVisible"
      >
        <option v-for="option in initialItems" :key="option">
          {{ option }}
        </option>
      </select>
    </div>

    <div class="chosen" v-if="selectedList.length">
      <b>Выбрано:</b>

      <div>
        {{ selectedList.join(", ") }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["list"],

  data() {
    return {
      isDropdownVisible: false,
      isInputDisabled: true,
      selectedList: [],
      searchQuery: "",
    };
  },

  methods: {
    changeSelectVisibility() {
      this.isDropdownVisible = !this.isDropdownVisible;
      this.isInputDisabled = !this.isInputDisabled;
    },
  },

  computed: {
    initialItems() {
        return this.list.filter((item) => item.indexOf(this.searchQuery) !== -1);
    },
  },

};
</script>

<style lang="scss">
.multiselect {
  display: flex;
  flex-direction: column;
  padding: 1em;

  label {
    margin: 0 auto;
  }

  .select_wrapper {
    margin: 2em auto;
    width: 500px;

    .input_wrapper {
      position: relative;

      input {
        width: 95%;
      }

      button {
        position: absolute;
        top: 0;
        right: 0;
      }

      .dropdown_opened {
        transform: rotate(180deg);
      }
    }

    select {
      width: 500px;
    }
  }

  .chosen {
    width: 150px;
    padding: 1em;
    background-color: lightgray;

    div {
      overflow: hidden;
      white-space: nowrap;
      text-overflow: ellipsis;
      margin-top: 1em;
    }
  }
}
</style>