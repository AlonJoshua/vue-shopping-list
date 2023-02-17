<template>
  <div>
    <h1 class="app-title app-font-title text-primary">{{ title }}</h1>
    <ul class="shopping-list app-font-body">
        <ListItem v-for="(item, index) in listItems" 
          :key="item.title" 
          :index="index" 
          :name="item.name" 
          :price="item.price" 
          :currency="currency" 
          :done="item.done" 
          :listItems="listItems"
          @deleteItem="deleteItem"
          @toggleItemStatus="toggleItemStatus"
          @showItemDescription="showItemDescription"
          @toggleItemForm="toggleItemForm"
        >
        </ListItem>
        <ListItem :isTotal="true" :price="totalPrice" :currency="currency"></ListItem>
    </ul>
    <button class="add-item-button" @click="$emit('toggleItemForm', true)">
      <div class="add-item-button__icon">
        <img src="../assets/plus.svg" alt="add list item icon">
      </div>
      <span class="add-item-button__text">
        add product
      </span>
    </button>
    <AddItemForm 
      v-if="isAddingItem"
      :selectedItem="selectedItem"
      :listItems="listItems"
      @toggleItemForm="toggleItemForm" 
      @editOrAddItem="editOrAddItem" 
    />
  </div>
</template>

<script>
import ListItem from './ListItem.vue';
import AddItemForm from './AddItemForm.vue';

export default {
  name: 'ShoppingList',
  components: {
    ListItem,
    AddItemForm,
  },
  props: {
    title: String,
    currency: String,
    listItems: Array,
    isAddingItem: Boolean,
    selectedItem: [Boolean, Object]
  },
  methods: {
    addItem(item) {
      this.$emit('deleteItem', item);
    },  
    deleteItem(index) {
      this.$emit('deleteItem', index);
    },
    toggleItemStatus(index) {
      this.$emit('toggleItemStatus', index);
    },
    toggleItemForm(isOpen, index) {
      this.$emit('toggleItemForm', isOpen, index);
    },
    editOrAddItem(item, index) {
      this.$emit('editOrAddItem', item, index);
    },
    showItemDescription(index) {
      this.$emit('showItemDescription', index);
    }
  },
  computed: {
    totalPrice() {
      return this.listItems.reduce((acc, item) => acc + parseInt(item.price), 0);
    }
  },
  mounted() {
  }
}
</script>

<style scoped lang="scss">
.shopping-list {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  gap: 15px;
  padding-inline-start: 0;
}
.add-item-button {
  all: unset;
  cursor: pointer;
  color: #FF941A;
  font-family: 'Inter', sans-serif;
  font-size: 15px;
  display: flex;
  align-items: center;
  &__icon {
    display: grid;
    place-content: center;
    width: 45px;
  }
  &__text {
    padding: 0 20px;
  }
}
</style>
