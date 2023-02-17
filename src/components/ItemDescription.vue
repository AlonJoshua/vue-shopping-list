<template>
    <div class="item-view">
        <button class="item-view__back" type="button" @click="$emit('hideItemDescription')">
            <img src="../assets/return-arrow.svg" alt="back to shopping list icon">
        </button>
        <div class="item-view__body">
            <div class="item-view__title text-primary app-font-title">
                {{ selectedItem.name }}
            </div>
            <p class="item-view__content text-primary app-font-body">
                {{ selectedItem.description }}
            </p>
        </div>
    </div>
</template>

<script>
export default {
    name: 'ItemDescription',
    props: {
        selectedItem: Object
    }
}
</script>

<style scoped lang="scss">
.item-view {
    position: relative;
    height: 100%;
    width: 100%;
    &__back  {
        position: absolute;
        left: 10px;
        top: 10px;
        cursor: pointer;
        background: none;
        border: none;
    }
    &__title {
        margin-top: 13.4px;
        margin-bottom: 50px;
    }
    &__content {
        padding: 30px 15px
    }
}
</style>