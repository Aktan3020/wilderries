<template>
    <div :class="{ 'modal_hidde': isOpenModal, modal: true }">
        <div class="main_categories">
            <div class="main_categories_item" v-for="(item, index) in categories" :key="index"
                @mousemove="showchildren(item)">
                <span class="category_item_wrap"><img :src="item.image" class="category_image" /> {{ item.title }}</span>
                <span class="category_wrap_arrow"><span v-if="item.children.length > 0">></span></span>
            </div>
        </div>
        <div class="modal_children" v-show="isChildren">
            <div class="main_categories_item" v-for="(item, index) in children_items" :key="index"
                @click="showchildren_children(item)">
                <span class="category_item_wrap"><img :src="item.image" class="category_image" /> {{ item.title }}</span>
                <span class="category_wrap_arrow"><span v-if="item.children.length > 0">></span></span>
            </div>
            <div class="modal_children_image">
                <img src="" alt="">
                <p></p>
            </div>
        </div>
        <div class="modal_children" v-show="isChildren_children">
            <div class="main_categories_item" v-for="(item, index) in children_items_items" :key="index">
                <span class="category_item_wrap"><img :src="item.image" class="category_image" /> {{ item.title }}</span>
                <span class="category_wrap_arrow"><span v-if="item.children?.length > 0">></span></span>
            </div>
            <div class="modal_children_image">
                <img src="" alt="">
                <p></p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'ModalCategory',
    data() {
        return {
            categories: [],
            isChildren: false,
            isChildren_children: false,
            children_items: [],
            children_items_items: []

        }

    },
    methods: {
        showchildren(item) {
            if (item.children?.length > 0) {
                this.isChildren = true
                this.children_items = item.children
            } else {
                this.isChildren = false
            }
        },
        showchildren_children(item) {
            console.log('chil', item);
            if (item.children?.length > 0) {
                this.isChildren_children = true
                this.children_items_items = item.children
            } else {
                this.isChildren_children = false;
            }
        }

    },
    props: {
        isOpenModal: Boolean,
    },
    mounted() {
        const getCategories = async () => {
            try {
                const response = await fetch('https://sindbad.pythonanywhere.com/api/v1/categories/');
                if (!response.ok) {
                    throw new Error('Ошибка при получении категорий');
                }
                const data = await response.json();
                this.categories = data.results;
            } catch (error) {
                console.error(error);
            }
        }
        getCategories();
    }
}
</script>

<style>
.modal {
    position: absolute;
    left: 0;
    width: 100%;
    height: calc(100vh - 125px);
    transition: 0.5s;
    z-index: 2;
    padding: 0 50px;
    display: flex;
}

.modal_hidde {
    left: -100%;
}

.category_wrap_arrow {
    opacity: 0;
    transition: 0.3s;
}

.main_categories {
    padding-right: 10px;
    overflow-y: auto;
    height: 100%;
    border-right: 1px solid rgba(72, 70, 70, 0.482);
    width: fit-content;
}

.main_categories_item {
    width: 350px;
    height: 40px;
    display: flex;
    align-items: center;
    padding-left: 10px;
    transition: 0.3s;
    border-radius: 15px;
    cursor: pointer;
    justify-content: space-between;
    padding-right: 5px;
    gap: 10px;
}

.category_item_wrap {
    display: flex;
    gap: 10px;
}

.main_categories_item:hover {
    background: #000;
    background: #f6f6f9;
}

.main_categories_item:hover .category_wrap_arrow {
    opacity: 1;
}

.category_image {
    width: 30px;
    height: 30px;
    object-fit: contain;
}

.modal_children {
    width: 360px;
    border-right: 1px solid rgba(72, 70, 70, 0.482);
    height: 100%;
}

.modal_children_items {
    padding-right: 10px;
}
</style>