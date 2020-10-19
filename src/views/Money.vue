<template>
        <Layout class-prefix="layout">
            <number-pad/>
            <types/>
           <notes/>
           <tags/>
        </Layout>
</template>

<script lang="ts">
    import Nav from '@/components/Nav.vue';
    import NumberPad from '@/components/Money/NumberPad.vue';
    import Types from '@/components/Money/Types.vue';
    import Notes from '@/components/Money/Notes.vue';
    import Tags from '@/components/Money/Tags.vue';
    export default {
        name: 'money',
        components: {Tags, Notes, Types, NumberPad, Nav}
    };
</script>
<style lang="scss">
    .layout-content{
        border: 3px solid red;
        display: flex;
        flex-direction: column-reverse;
    }
</style>

<style lang="scss" scoped>





</style>

