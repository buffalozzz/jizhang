<template>
    <div>
        <label class="FormItem">
            <span class="name">{{this.fieldName}}</span>
            <input type="text"
                   :value="value"
                   @input="onValueChanged($event.target.value)"
                   :placeholder="placeholder">
        </label>
    </div>
</template>

<script lang="ts">
    import Vue from 'vue'
    import {Component, Prop, Watch} from 'vue-property-decorator'
    @Component

    export default class FormItem extends Vue{
        @Prop({default: ''})readonly value!: string

        @Prop({required:true})fieldName!: string
        @Prop()placeholder?: string

        onValueChanged(value: string){
            this.$emit('update:value', value)
        }
    }
</script>

<style lang="scss" scoped>
    .FormItem {
        font-size: 14px;
        /*background: #f5f5f5;*/
        padding-left: 16px;
        display: flex;
        align-items: center;
        .name {
            padding-right: 16px;
        }
        input {
            height: 44px;
            flex-grow: 1;
            background: transparent;
            border: none;
            padding-right: 16px;
        }
    }
</style>