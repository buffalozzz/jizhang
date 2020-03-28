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
        <Tags :data-source.sync="tags" @update:value="onUpdateTags"/>
    </Layout>
</template>

<script lang="ts">
    import Vue from 'vue'
    import {Component, Watch} from 'vue-property-decorator'
    import NumberPad from "@/components/money/NumberPad.vue";
    import Types from "@/components/money/Types.vue";
    import Tags from "@/components/money/Tags.vue";
    import FormItem from "@/components/money/FormItem.vue";
    import recordListModel from "@/models/recordListModel";

    const recordList = recordListModel.fetch();

    @Component({
        components: {FormItem, Tags, Types, NumberPad},
    })

    export default class Money extends Vue{
        tags= window.tagList;
        recordList: RecordItem[] = recordList;
        record: RecordItem = {
            tags: [],
            notes: '',
            type: '-',
            amount: 0,
        };

        onUpdateTags(value: string[]){
            this.record.tags = value
        }
        onUpdateFormItem(value: string){
            this.record.notes = value
        }
        onUpdateNumberPad(value: number){
            this.record.amount = value
        }
        saveRecord(){
            recordListModel.create(this.record)
        }
        @Watch('recordList')
        onRecordChange(){
            recordListModel.save()
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

