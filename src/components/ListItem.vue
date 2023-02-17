<template>
    <li class="shopping-list-item">
        <button type="button" class="shopping-list-item__index text-orange" @click="$emit('toggleItemStatus', index)">
            <span>{{ currIndex }}</span>
        </button>
        <button type="button" class="shopping-list-item__details" :class="{'shopping-list-item__done': done}" @click="$emit('showItemDescription', index)">
            <div class="shopping-list-item__name">
                <span :class="[done ? 'text-strikethrough': 'text-primary']">{{ currName }}</span>
            </div>
            <div class="shopping-list-item__price">
                <span :class="[done ? 'text-strikethrough': 'text-primary']">{{ price }} {{ currency }}</span>
            </div>
        </button>
        <div v-if="!isTotal" class="shopping-list-item__buttons">
            <button class="shopping-list-item__button">
                    <img src="../assets/pencil.svg" alt="edit list item icon">
            </button>
            <button class="shopping-list-item__button">
                <img src="../assets/garbage.svg" alt="delete list item icon" @click="$emit('deleteItem', index)">
            </button>
        </div>
    </li>
</template>

<script>
export default {
    name: "ListItem",
    props: {
        index: Number,
        name: String,
        price: Number,
        currency: String,
        description: String,
        done: Boolean,
        isTotal: Boolean
    },
    data() {
        return {
            total: "Total :"
        }
    },
    computed: {
        currIndex() {
            if (this.isTotal) {
                return;
            }
            return this.index + 1;
        },
        currName() {
            if (this.isTotal) {
                return this.total;
            }
            return this.name;
        }
    }
}
</script>

<style scoped lang="scss">
.shopping-list {
    &-item {
        display: flex;
        box-shadow: 0 1px 0 0 #E3E3E5;
        height: 48px;
        &:last-child {
            box-shadow: none;
            & .shopping-list-item__index {
                box-shadow: none;
            }
        }
        &__index {
            font-size: 24px;
            width: 45px;
            box-shadow: 1px 0 0 0 #E3E3E5;
            display: grid;
            place-content: center;
            cursor: pointer;
            background: none;
            border: none;
        }
        &__details {
            display: flex;
            align-items: center;
            cursor: pointer;
            background: none;
            border: none;
        }
        &__name {
            display: flex;
            align-items: center;
            padding: 0 20px;
            min-width: 120px;
        }
        &__price {
            display: grid;
            place-content: center;
            padding: 0 10px;
            white-space: nowrap;
        }
        &__done {
            position: relative;
            & .shopping-list-item__name span {
                text-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
            }
            &:after {
                content: '';
                position: absolute;
                top: 50%;
                left: 10px;
                height: 1px;
                width: calc(100% - 10px);
                background: #E3E3E5;
            }
        }
        &__buttons {
            display: flex;
            align-items: center;
            margin-left: auto;
        }
        &__button {
            all: unset;
            cursor: pointer;
            display: grid;
            place-content: center;
            padding: 3px 10px;
            &:first-child {
                border-right: 1px solid;
            }
        }
    }

}
</style>