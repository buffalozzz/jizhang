<template>
    <button class="button">
        <slot/>
    </button>
</template>

<script lang="ts">
    import Vue from 'vue'
    import {Component} from 'vue-property-decorator'

    @Component
    export default class Button extends Vue {
    }
</script>

<style lang="scss" scoped>
    .button {
        background: #767676;
        color: white;
        border-radius: 4px;
        border: none;
        height: 36px;
        padding: 0 16px;
        &-wrapper{
            text-align: center;
            padding: 18px;
            margin-top: 44-18px;
        }
    }
</style>