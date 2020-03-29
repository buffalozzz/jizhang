<template>
    <Layout>
        <div class="navBar">
            <Icon class="leftIcon" name="left" @click.native="goBack"/>
            <span class="title">编辑标签</span>
            <span class="rightIcon"/>
        </div>
        <div class="form-wrapper">
            <FormItem :value="tag.name"
                      @update:value="updateTag"
                      field-name="请输入标签名"
                      placeholder="标签名"
            />
        </div>
        <div class="button-wrapper">
            <Button @click.native="remove">刪除标签</Button>
        </div>
    </Layout>
</template>

<script lang="ts">
    import Vue from 'vue';
    import {Component} from 'vue-property-decorator';
    import FormItem from "@/components/money/FormItem.vue";
    import Button from "@/components/Button.vue";

    @Component({
        components: {Button, FormItem},
    })
    export default class EditLabel extends Vue {
        get tag() {
            return this.$store.state.currentTag;
        }

        created() {
            const id = this.$route.params.id;
            this.$store.commit('fetchTags');
            this.$store.commit('setCurrentTag', id);
            if (!this.tag) {
                this.$router.replace('/404');
            }
        }

        updateTag(name: string) {
            this.$store.commit('updateTag',{id:this.tag.id, name: name})
        }

        remove() {
            if (this.tag){
                this.$store.commit('removeTag',(this.tag.id))
            }
        }

        goBack() {
            this.$router.back();
        }
    }
</script>

<style lang="scss" scoped>
    .navBar {
        text-align: center;
        font-size: 16px;
        padding: 12px 16px;
        background: #ffffff;
        display: flex;
        align-items: center;
        justify-content: space-between;

        > .title {
            border: 1px solid red;
        }

        > .leftIcon {
            border: 1px solid red;

        }

        > .rightIcon {
            border: 1px solid red;

        }
    }

    .form-wrapper {
        margin-top: 8px;
        background: #ffffff;
    }

    .button-wrapper {
        text-align: center;
        padding: 16px;
        margin-top: 44-16px;
    }
</style>