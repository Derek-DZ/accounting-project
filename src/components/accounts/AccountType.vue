<template>
  <ul class="accountList">
    <li class="accountTitle" v-for="record in recordTree"
        :key="record.id">
      <h3 class="title">{{beautifyTitle(record.title)}}</h3>
      <ul>
        <li v-for="item in record.data" :key="item.id" class="account">
          <Tag :tag-name="item.tagName"/>
          <div class="test-wrapper">
            <span class="accountNote">{{ item.note }}</span>
            <span class="accountTime">{{ beautifyAccount(item.date) }}</span>
          </div>
          <span class="accountMoney">{{ item.type }}￥{{ item.number }}</span>
        </li>
      </ul>
    </li>
    <li class="noData" v-if="recordTree.length===0">暂无数据</li>
  </ul>
</template>

<script lang="ts">
  import Vue from 'vue';
  import {Component, Prop} from 'vue-property-decorator';
  import Tag from '@/components/Tag.vue';

  @Component({
    components: {Tag}
  })
  export default class AccountType extends Vue {
    @Prop() recordTree!: RecordTree;
    @Prop(Function) beautifyTitle!: Function;
    @Prop(Function) beautifyAccount!: Function;
  }


</script>

<style lang="scss" scoped>
  @import "~@/assets/style/helper.scss";

  .accountList {
    background-color: $color-box;
    border-radius: 10px;
    margin-top: -8px;
    min-height: 5vh;
    overflow-y: scroll;
    padding-top: 5px;
    z-index: 10;

    > .noData {
      font-size: 18px;
      font-weight: bold;
      text-align: center;
      padding: 10px;
    }

    > .accountTitle {
      padding: 5px;
      justify-content: start;
      margin: 2px 8px 2px 8px;


      > .title {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
        background-color: $color-background;
        padding-left: 5px;

        > .icon {
          margin-right: 8px;
        }
      }

      > ul {
        > .account {
          display: flex;
          flex-direction: row;
          align-items: flex-start;
          margin: 5px;
          background-color: white;
          border-radius: 10px;

          > .tag {
            margin-right: 10px;
          }

          > .test-wrapper {
            display: flex;
            flex-direction: column;
            font-family: $font-hei;

            > .accountNote {
              height: 20px;
              line-height: 22px;
              font-size: 13px;
            }

            > .accountTime {
              height: 20px;
              line-height: 22px;
              font-size: 13px;
            }
          }

          > .accountMoney {
            flex-grow: 1;
            align-self: center;
            text-align: end;
            margin-right: 10px;
          }
        }
      }
    }
  }
</style>