<template>
    <div class="add-item-form app-font-body">
        <button type="button" class="add-item-form__close" @click="$emit('toggleItemForm', false)">
            <img src="../assets/close.svg" alt="close add item form icon">
        </button>
        <div class="add-item-form__inputs">
            <div class="add-item-form__inputs__text">
                <label class="text-strikethrough">Name</label>
                <input type="text" name="name" v-model="name">
            </div>
            <div class="add-item-form__inputs__text">
                <label class="text-strikethrough">Price</label>
                <input type="text" name="price" v-model="price">
            </div>
        </div>
        <div class="add-item-form__textarea">
            <label class="text-strikethrough">Description</label>
            <textarea v-model="description"></textarea>
        </div>
        <div class="add-item-form__submit">
            <button type="button" @click="editOrAddItem">
                <img src="../assets/send.svg" alt="add item icon">
            </button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'ListItem',
    props: {
        selectedItem: [Boolean, Object],
        listItems: Array
    },
    data() {
        return {
            name: this.selectedItem ? this.selectedItem.name : "",
            price : this.selectedItem ? this.selectedItem.price : "",
            description: this.selectedItem ? this.selectedItem.description : ""
        }
    },
    methods: {
        editOrAddItem() {
            const itemData = {
                name: this.name,
                price: this.price,
                description: this.description
            };
            if (this.selectedItem) {
                const index = this.listItems.indexOf(this.selectedItem)
                itemData.done = this.selectedItem.done;
                this.$emit('editOrAddItem', itemData, index);
            } else {
                itemData.done = false;
                this.$emit('editOrAddItem', itemData, false);
            }
            this.$emit('toggleItemForm', false);
        }
    },
}
</script>

<style scoped lang="scss">
.add-item-form {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 375px;
    background: white;
    padding-top: 40px;
    overflow-y: scroll;
    &__close {
        all: unset;
        cursor: pointer;
        position: absolute;
        right: 10px;
        top: 10px;
    }
    &__inputs {
        display: flex;
      &__text {
        flex: 1 0 calc(50% - 15px);
        text-align: left;
        & input {
            all: unset;
            margin-top: 10px;
            box-shadow: 0 1px 1px 0 #E3E3E5;
        }
      }
    }
    &__textarea {
        display: flex;
        flex-direction: column;
        text-align: left;
        & label {
            padding: 25px 0;
        }
        & textarea {
            all: unset;
            height: max-content;
            min-height: 200px;
        }
    }
    &__submit {
        display: flex;
        justify-content: flex-end;
        margin-right: 10px;
        & button {
            all: unset;
            cursor: pointer;
        }
    }
}
</style>