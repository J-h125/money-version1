<template>
    <div class="tags">
        <div class="new">
            <button @click="createTag"><Icon name="plus"/>新增标签</button>
        </div>
        <ul class="current">
            <li v-for="tag in tagList" :key="tag.id"
            :class="{selected:selectedTags.indexOf(tag)>=0}"
            @click="toggle(tag)">{{tag.name}}
           </li>
         </ul>
    </div>
</template>

<script lang="ts">
    import Vue from 'vue';
    import {Component,Prop} from 'vue-property-decorator';
    import TagHelper from '@/mixins/tagHelper';
    import {mixins} from 'vue-class-component';


    @Component
    export default class Tags extends mixins(TagHelper){

       selectedTags:string[] = [];
       get tagList(){
           return this.$store.state.tagList;
       }
       created(){
           this.$store.commit('fetchTags');
       }

       toggle(tag:string){
          const index =  this.selectedTags.indexOf(tag);
          if(index>=0){
            this.selectedTags.splice(index,1);
          }else {
              this.selectedTags.push(tag);
          }
          this.$emit('update:value',this.selectedTags)
       }
    };
</script>

<style lang="scss" scoped>
    .tags{
       
        background: white;
        font-size: 14px;
        padding: 16px;
        flex-grow: 1;
        display: flex;
        flex-direction: column-reverse;
        > .current{
           
            display: flex;
            flex-wrap: wrap;

            > li{
                $bg:#d9d9d9;
                background: $bg;
                $h:24px;
                height: $h;
                line-height: $h;
                border-radius: ($h/2);
                padding: 0 16px;
                margin-right: 12px;
                margin-top:6px;
                &.selected{
                    background: darken($bg,50%);
                    color:white;
                }
            }
        }
        > .new{
            
            padding-top: 16px;
            button{
                cursor: pointer;
                background: #5a5a5a;
                color:white;
                padding:0 3px;
                border: none;
                border-radius:12px ;
                padding: 4px 8px;
                .icon{
                    
                    height: 1.5em;
                    width: 1.5em;
                   vertical-align:bottom;
                }
            }
        }
    }
</style>