<template>
    <nav>
        <router-link to="/money" class="item" active-class="selected">
            <Icon name="money"></Icon>
            记账
        </router-link>
        <router-link to="/labels" class="item" active-class="selected">
            <Icon name="labels"></Icon>
            标签
        </router-link>
        <router-link to="/statistics" class="item" active-class="selected">
            <Icon name="statistics"></Icon>
            统计
        </router-link>
    </nav>
</template>

<script lang="ts">
    export default {
        name: "Nav"
    }
</script>

<style lang="scss" scoped>
    nav{
        display: flex;
        box-shadow: 0 0 3px rgba(0, 0, 0, 0.25);
        flex-direction: row;
        font-size: 12px;
        > .item{
            padding: 2px 0;
            width: 33.333333%;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center ;
            .icon {
                width: 32px;
                height: 32px;
            }

        }
        > .item.selected{
            color: red;
        }
    }

</style>