<template>
    <Layout class-prefix="layout">
        <NumberPad @update:value="onUpdateNumberPad" @submit="saveRecord"/>
        <Types :value.sync="record.type"/>
        <div class="m-from-wrap">
            <FormItem field-name="备注"
                      placeholder="请输入备注"
                      @update:value="onUpdateFormItem"
            />
        </div>
        <Tags/>
    </Layout>
</template>

<script lang="ts">
    import Vue from 'vue'
    import {Component} from 'vue-property-decorator'
    import NumberPad from "@/components/money/NumberPad.vue";
    import Types from "@/components/money/Types.vue";
    import Tags from "@/components/money/Tags.vue";
    import FormItem from "@/components/money/FormItem.vue";

    @Component({
        components: {FormItem, Tags, Types, NumberPad},
        computed: {
            // recordList(){
            //     return this.$store.state.recordList;
            //     // return store.recordList
            // }
        }
    })

    export default class Money extends Vue{
        get recordList(){
            return this.$store.state.recordList;
        }

        record: RecordItem = {
            tags: [],
            notes: '',
            type: '-',
            amount: 0,
        };
        created(){
            this.$store.commit('fetchRecords')
        }
        onUpdateFormItem(value: string){
            this.record.notes = value
        }
        onUpdateNumberPad(value: number){
            this.record.amount = value
        }
        saveRecord(){
            this.$store.commit('createRecord', this.record)
        }
    }
</script>

<style lang="scss">
    .layout-content {
        display: flex;
        flex-direction: column-reverse;
    }
    .m-from-wrap{
        padding: 10px 0;
        background: #f5f5f5
    }
</style>

