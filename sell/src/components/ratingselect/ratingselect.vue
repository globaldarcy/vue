<template>
  <div class="ratingselect">
    <div class="rating-type">
      <span @click="select(2)" class="block positive" :class="{'active':sType===2}">{{desc.all}}<span
        class="count">{{ratings.length}}</span></span>
      <span @click="select(0)" class="block positive" :class="{'active':sType===0}">{{desc.positive}}<span
        class="count">{{positives.length}}</span></span>
      <span @click="select(1)" class="block negative" :class="{'active':sType===1}">{{desc.negative}}<span
        class="count">{{negatives.length}}</span></span>
    </div>
    <div @click="toggleContent" class="switch" :class="{'on':oContent}">
      <span class="icon-check_circle"></span>
      <span class="text">只看有内容的评价 </span>
    </div>
  </div>
</template>

<script>
  import {vm} from '../../components/event'
  const POSITIVE = 0
  const NEGATIVE = 1
  const ALL = 2
  export default{
    data(){
      return {
        sType: this.selectType,
        oContent: this.onlyContent
      }
    },
    props: {
      ratings: {
        type: Array,
        default(){
          return []
        }
      },
      selectType: {
        type: Number,
        default: ALL
      },
      onlyContent: {
        type: Boolean,
        default: false
      },
      desc: {
        type: Object,
        default(){
          return {
            all: '全部',
            positive: '满意',
            negative: '不满意'
          }
        }
      }
    },
    computed: {
      positives(){
        return this.ratings.filter((rating) => {
          return rating.rateType === POSITIVE
        })
      },
      negatives(){
        return this.ratings.filter((rating) => {
          return rating.rateType === NEGATIVE
        })
      }
    },
    methods: {
      select(type){
        this.sType = type
        this.$emit('select-type', type)
        //http://blog.csdn.net/o_Mario_o/article/details/77035451
      },
      toggleContent(){
        this.oContent = !this.oContent
        this.$emit('toggle-content', this.oContent)
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import '../../common/stylus/mixin'
  .ratingselect
    .rating-type
      padding: 18px 0
      margin: 0 18px
      border-1px(rgba(7, 17, 27, 0.1))
      font-size: 0
      .block
        display: inline-block
        padding: 8px 12px
        margin-right: 8px
        border-radius: 2px
        color: rgb(77, 85, 93)
        font-size: 12px
        &.active
          color: #fff
        .count
          margin-left: 2px
          line-height: 16px
          font-size: 8px
        &.positive
          background: rgba(0, 160, 220, 0.2)
          &.active
            background: rgb(0, 160, 220)
        &.negative
          background: rgba(77, 85, 93, 0.2)
          &.active
            background: rgb(77, 85, 93)
    .switch
      padding: 12px 18px
      line-height: 24px
      border-1px(rgba(7, 17, 27, 0.1))
      color: rgb(143, 153, 159)
      font-size: 0
      &.on
        .icon-check_circle
          color: #00c850
      .icon-check_circle
        display: inline-block
        vertical-align: top
        margin-right: 4px
        font-size: 24px
        line-height: 24px
      .text
        display: inline-block
        vertical-align: top
        font-size: 12px
</style>
