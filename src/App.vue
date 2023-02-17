<template>
  <div class="app-mobile-wrapper">
    <ShoppingList 
      v-if="!isItemDescriptionView"
      :title="title" 
      :currency="currency" 
      :listItems="listItems" 
      :isAddingItem="isAddingItem" 
      :selectedItem="selectedItem"
      @toggleItemForm="toggleItemForm" 
      @toggleItemStatus="toggleItemStatus" 
      @deleteItem="deleteItem" 
      @editOrAddItem="editOrAddItem"
      @showItemDescription="showItemDescription"
    />
    <ItemDescription 
      v-if="isItemDescriptionView" 
      :selectedItem="selectedItem" 
      @hideItemDescription="hideItemDescription" 
    />
  </div>
</template>

<script>
import ShoppingList from './components/ShoppingList.vue'
import ItemDescription from './components/ItemDescription.vue'

export default {
  name: 'App',
  components: {
    ShoppingList,
    ItemDescription
  },
  data() {
    return {
      title: "Shopping List",
      currency: "NIS",
      isAddingItem: false,
      isItemDescriptionView: false,
      selectedItem: false,
      listItems: [
        {
          name: "Tomatos",
          price: 5,
          description: "Lorem ipsum, dolor sit amet consectetur adipisicing elit. Voluptatum odit animi ipsam minima incidunt quos tempora quibusdam est aliquid saepe natus odio, mollitia voluptate eum officiis aperiam corporis nam vero. tomatos",
          done: true
        },
        {
          name: "Cucumbers",
          price: 3,
          description: "Lorem ipsum, dolor sit amet consectetur adipisicing elit. Voluptatum odit animi ipsam minima incidunt quos tempora quibusdam est aliquid saepe natus odio, mollitia voluptate eum officiis aperiam corporis nam vero. cucumbers",
          done: false
        },
        {
          name: "Bread",
          price: 10,
          description: "Lorem ipsum, dolor sit amet consectetur adipisicing elit. Voluptatum odit animi ipsam minima incidunt quos tempora quibusdam est aliquid saepe natus odio, mollitia voluptate eum officiis aperiam corporis nam vero. bread",
          done: false
        },
        {
          name: "Grapes",
          price: 4,
          description: "Lorem ipsum, dolor sit amet consectetur adipisicing elit. Voluptatum odit animi ipsam minima incidunt quos tempora quibusdam est aliquid saepe natus odio, mollitia voluptate eum officiis aperiam corporis nam vero. grapes",
          done: false
        }
      ]
    }
  },
  methods: {
    editOrAddItem(item, index) {
      if (Number.isInteger(index)) {
        this.listItems[index] = item;
      } else {
        this.listItems.push(item);
      }
    },  
    deleteItem(index) {
      this.listItems.splice(index, 1);
    },
    toggleItemStatus(index) {
      this.listItems[index].done = !this.listItems[index].done;
    },
    toggleItemForm(isOpen, index) {
      if (Number.isInteger(index)) {
        this.selectedItem = this.listItems[index];
      }
      if (isOpen) {
        return this.isAddingItem = true;
      }
      this.selectedItem = false;
      return this.isAddingItem = false;
    },
    showItemDescription(index) {
      this.selectedItem = this.listItems[index];
      this.isItemDescriptionView = true; 
    },
    hideItemDescription() {
      this.selectedItem = false;
      this.isItemDescriptionView = false; 
    }
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Inter&family=Montserrat+Alternates:wght@700&display=swap');
@import './assets/style.scss';
.app {
  &-title {
    margin-bottom: 50px;
  }
  &-font {
    &-title {
      font-family: 'Montserrat Alternates', sans-serif; 
      font-size: $title-size;
    }
    &-body {
      font-family: 'Inter', sans-serif; 
      font-size: $paragraph-size;
    }
  }
  &-mobile-wrapper {
    max-width: 375px; 
    height: 90vh;
    margin: 50px auto 20px; 
    text-align: center; 
    display: flex;
    justify-content: center;
    border-radius: 20px;
    padding: 5px 10px;
    border: 1px solid gray;
  }
}
.text {
  &-primary {
    color: $dark-grey;
  }
  &-strikethrough {
    color: $light-grey;
  }
  &-orange {
    color: $orange;
  }
  &-light {
    color: $pale-grey;
  }
}
</style>
